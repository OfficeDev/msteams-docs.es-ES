---
title: Llamadas multimedia en tiempo real y reuniones en línea con Microsoft Teams
description: Comprender conceptos clave en la creación de bots que pueden realizar llamadas de audio y vídeo en tiempo real y reuniones en línea.
ms.topic: conceptual
localization_priority: Normal
keywords: audio stream video stream audio/video calling meeting real-time media application-hosted media hosted media service-hosted media
ms.openlocfilehash: deedc47f67fe6848cf7f84457247d2271257e3f0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020158"
---
# <a name="real-time-media-calls-and-meetings-with-microsoft-teams"></a>Llamadas multimedia en tiempo real y reuniones con Microsoft Teams

La Plataforma multimedia en tiempo real permite a los bots interactuar con Microsoft Teams llamadas y reuniones mediante el uso compartido de voz, vídeo y pantalla en tiempo real. Se trata de una funcionalidad avanzada que permite al bot enviar y recibir contenido de voz y vídeo fotograma por fotograma. El bot tiene acceso sin procesar a las secuencias multimedia de voz, vídeo y pantalla compartida. Hay bots multimedia hospedados en servicios más sencillos que dependen de la Plataforma multimedia en tiempo real para todo el procesamiento de medios. Los bots que procesan los medios por sí mismos se denominan bots multimedia hospedados en aplicaciones.

Por ejemplo, en una llamada 1:1 con un bot, mientras el usuario habla, el bot recibe 50 fotogramas de audio por segundo, con cada fotograma que contiene 20 milisegundos (ms) de audio. Un bot multimedia hospedado por la aplicación puede realizar el reconocimiento de voz en tiempo real a medida que se reciben los fotogramas de audio, en lugar de tener que esperar una grabación después de que el usuario haya dejado de hablar. El bot también puede enviar y recibir vídeo de resolución de alta definición, incluido el contenido de uso compartido de pantalla basado en vídeo.

La plataforma proporciona una API sencilla como socket para que el bot envíe y reciba medios. Controla la codificación y decodificación en tiempo real de paquetes de audio o vídeo con códecs como SILK y G.722 para audio y H.264 para vídeo. La plataforma también controla automáticamente todo el cifrado o descifrado de paquetes multimedia y la transmisión de red de paquetes. El bot solo se preocupa por el contenido real de audio o vídeo. Un bot multimedia en tiempo real participa en llamadas 1:1, así como reuniones con varios participantes.

## <a name="media-session"></a>Sesión multimedia

Cuando un bot multimedia en tiempo real responde a una llamada entrante o se une a una reunión Teams, debe declarar qué modalidades debe admitir. Para cada modalidad admitida, el bot declara si puede enviar y recibir medios, recibir solo o enviar solo. Por ejemplo, un bot diseñado para controlar las llamadas Teams 1:1, requiere enviar y recibir audio, pero solo enviar vídeo, ya que no requiere recibir el vídeo del autor de la llamada. El conjunto de modalidades de audio y vídeo establecidas entre el bot y el Teams o reunión se denomina sesión multimedia.

Se admiten dos tipos de modalidades de vídeo, el vídeo principal y el uso compartido de pantalla basado en vídeo. El vídeo principal se usa para transportar el vídeo desde la cámara web de un usuario. El uso compartido de pantalla basado en vídeo permite que un usuario comparta su pantalla como una secuencia de vídeo. La plataforma permite que un bot envíe y reciba ambos tipos de vídeo.

Cuando se une a una reunión Teams, un bot puede recibir varias secuencias de vídeo principales simultáneamente hasta diez por sesión multimedia. Esto permite que el bot vea a más de un participante en la reunión.

La siguiente sección proporciona detalles sobre el bot que envía y recibe medios como una secuencia de fotogramas.

## <a name="frames-and-frame-rate"></a>Fotogramas y velocidad de fotogramas

Un bot multimedia en tiempo real interactúa directamente con las modalidades de audio y vídeo de una sesión multimedia. Esto significa que el bot envía y recibe medios como una secuencia de fotogramas, donde cada fotograma representa una unidad de contenido. Un segundo de audio se transmite como una secuencia de 50 fotogramas, con cada fotograma que contiene 20 ms que es el 1/50 de un segundo de contenido de voz. Un segundo de vídeo se transmite como una secuencia de 30 imágenes fijas, cada una destinada a ser vista durante solo 33,3 ms, es decir, 1/30 de segundo antes de que se muestre el siguiente fotograma de vídeo. El número de fotogramas transmitidos o representados por segundo se denomina velocidad de fotogramas.

En la siguiente sección se proporcionan detalles sobre el formato de audio y vídeo que se usa en las reuniones y llamadas multimedia en tiempo real.

## <a name="audio-and-video-format"></a>Formato de audio y vídeo

En formato de audio, cada segundo de audio se representa como 16 000 muestras, y cada muestra contiene 16 bits de datos. Un marco de audio de 20 ms contiene 320 muestras que son 640 bytes de datos.

En formato de vídeo, se admiten varios formatos. Dos propiedades clave de un formato de vídeo son el tamaño del marco y el formato de color. Los tamaños de fotograma admitidos incluyen 640 x 360 píxeles, 1280 x 720 píxeles y 1920 x 1080 píxeles. Los formatos de color admitidos incluyen NV12 que es de 12 bits por píxel y RGB24 que es de 24 bits por píxel.

Un marco de vídeo de 720p contiene 921 600 píxeles que es 1280 veces 720. En el formato de color RGB24, cada píxel se representa como 3 bytes de 24 bits compuestos de un byte cada uno de los componentes de color rojo, verde y azul. Por lo tanto, un único fotograma de vídeo RGB24 de 720p requiere 2.764.800 bytes de datos que son 921.600 píxeles por 3 bytes por píxel. A una velocidad de fotogramas de 30 fps, enviar fotogramas de vídeo RGB24 de 720p significa procesar aproximadamente 80 megabytes por segundo de contenido, que el códec de vídeo H.264 comprime considerablemente antes de la transmisión de red.

Una funcionalidad avanzada de la plataforma permite que un bot envíe o reciba vídeo como fotogramas H.264 codificados. Esto admite bots que proporcionan su propio codificador o descodificador H.264, o no requieren que la secuencia de vídeo se descodifica en mapas de bits RGB24 o NV12 sin procesar.

En la siguiente sección se proporcionan detalles acerca de qué participantes de la reunión hablan los que son oradores activos y dominantes.

## <a name="active-and-dominant-speakers"></a>Altavoces activos y dominantes

Cuando se une a una Teams que consta de varios participantes, un bot puede identificar qué participantes de la reunión están hablando actualmente. Los altavoces activos identifican qué participantes se escuchan en cada fotograma de audio recibido. Los altavoces dominantes identifican qué participantes son actualmente más activos o dominantes en la conversación de grupo, aunque su voz no se escucha en todos los fotogramas de audio. El conjunto de altavoces dominantes puede cambiar a medida que los diferentes participantes toman turnos de palabra.

En la siguiente sección se proporcionan detalles sobre las solicitudes de suscripción de vídeo realizadas por un bot.

## <a name="video-subscription"></a>Suscripción de vídeo

En una llamada 1:1, el bot recibe automáticamente el vídeo del autor de la llamada si el bot está habilitado para recibir el vídeo. En una Teams, el bot debe indicar a la plataforma qué participantes quiere ver. Una suscripción de vídeo es una solicitud del bot para recibir el vídeo principal o el contenido para compartir pantalla de un participante. A medida que los participantes en la reunión llevan a cabo su conversación, el bot modifica sus suscripciones de vídeo deseadas en función de las actualizaciones del conjunto de altavoces dominante o las notificaciones que indican qué participante está compartiendo pantalla actualmente.

En la siguiente sección se proporcionan detalles sobre lo que debe instalar y los requisitos para desarrollar un bot multimedia hospedado en la aplicación.

## <a name="developer-resources"></a>Recursos para desarrolladores

Para desarrollar un bot multimedia hospedado por la aplicación, debe instalar [microsoft.Graph. La biblioteca .NET Calls.Media](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) NuGet paquete dentro del Visual Studio proyecto.

Los bots multimedia hospedados en aplicaciones requieren .NET o C# y Windows Server. Para obtener más información, vea [requisitos y consideraciones para bots multimedia hospedados en aplicaciones.](requirements-considerations-application-hosted-media-bots.md#c-or-net-and-windows-server-for-development)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Registrar un bot de llamadas](~/bots/calls-and-meetings/registering-calling-bot.md)
