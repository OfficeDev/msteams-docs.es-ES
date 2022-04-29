---
title: Reuniones en línea y llamadas multimedia en tiempo real con Microsoft Teams
description: Comprenda los conceptos clave en la creación de bots que puedan realizar llamadas de audio y vídeo en tiempo real y reuniones en línea. Más información sobre las sesiones multimedia, la velocidad de fotogramas, el formato de audio y vídeo y las referencias a los recursos de desarrolladores
ms.topic: conceptual
ms.localizationpriority: high
keywords: secuencia de audio secuencia de vídeo audio y vídeo llamadas reuniones en tiempo real hospedado multimedia hospedado multimedia hospedado servicio multimedia medios multimedia
ms.openlocfilehash: 0e5343567be3843c457885fcf506446b20b6dcf7
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111993"
---
# <a name="real-time-media-calls-and-meetings-with-microsoft-teams"></a>Reuniones y llamadas multimedia en tiempo real con Microsoft Teams

La plataforma multimedia en tiempo real permite que los bot interactúen con las llamadas y reuniones de Microsoft Teams mediante voces en tiempo real, vídeo y la pantalla compartida. La plataforma multimedia en tiempo real es una funcionalidad avanzada que permite a los bot enviar y recibir contenido de voz y vídeo fotograma a fotograma. El bot tiene acceso sin formato a las secuencias multimedia de voz, vídeo y pantalla compartida. Hay bots multimedia hospedados por servicio más sencillos que se basan en la plataforma de medios en tiempo real para todo el procesamiento multimedia. Los bot que procesan multimedia ellos mismos se denominan bots multimedia hospedados en la aplicación.

Por ejemplo, en una llamada 1:1 con un bot, a medida que el usuario hable el bot recibirá 50 fotogramas de audio por segundo. El bot recibirá fotogramas de audio y cada fotograma contendrá de 20 milisegundos (ms) de audio. Un bot multimedia hospedado en aplicaciones podrá realizar el reconocimiento de voz en tiempo real a medida que se reciban los fotogramas de audio. No es necesario esperar una grabación después de que el usuario haya dejado de hablar. El bot también podrá enviar y recibir vídeo de alta definición, incluyendo contenidos de uso compartido de pantalla basados en vídeo.

La plataforma proporciona una API sencilla y similar a un socket para que el bot envíe y reciba medios. Controla la codificación y descodificación en tiempo real de paquetes de audio o vídeo. Usa códecs, como SILK y G.722 para audio, y H.264 para vídeo. La plataforma también controla todo el cifrado o descifrado de paquetes multimedia y la transmisión de red de paquetes. El bot solo hace referencia al contenido real de audio o vídeo. Un bot multimedia en tiempo real participa en llamadas y reuniones 1:1 con varios participantes.

## <a name="media-session"></a>Sesión multimedia

Un bot multimedia en tiempo real deberá declarar qué modalidades debe admitir. El bot multimedia en tiempo real deberá declarar compatibilidad cuando responda a una llamada entrante o se una a una reunión de Teams. Para cada modalidad admitida, el bot declarará si puede enviar y recibir medios, solamente recibir o solo enviar. Por ejemplo, un bot diseñado para controlar llamadas 1:1 de Teams, requerirá enviar y recibir audio. Pero el bot solo deberá enviar vídeo, ya que no necesita recibir el vídeo del autor de la llamada. El conjunto de modalidades de audio y vídeo establecido entre el bot y el autor de la llamada o de la reunión de Teams se denomina sesión multimedia.

Se admiten dos tipos de modalidades de vídeo: vídeo principal y uso compartido de pantalla basado en vídeo. El vídeo principal se usa para transportar el vídeo desde la cámara web de un usuario. El uso compartido de pantalla basado en vídeo permitirá a un usuario compartir la pantalla. La plataforma permite que un bot envíe y reciba ambos tipos de vídeo.

Cuando se una a una reunión de Teams, un bot podrá recibir varias secuencias de vídeo principales simultáneamente, hasta 10 por cada sesión multimedia. El bot puede ver a más de un participante en la reunión.

En la sección siguiente, se proporcionan detalles sobre el bot que envía y recibe medios como una secuencia de fotogramas.

## <a name="frames-and-frame-rate"></a>Fotogramas y velocidad de fotogramas

Un bot multimedia en tiempo real interactúa directamente con las modalidades de audio y vídeo de una sesión multimedia. El bot envía y recibe multimedia como una secuencia de fotogramas, y cada fotograma es una unidad de contenido. Un segundo de audio se transmite como una secuencia de 50 fotogramas. Cada fotograma contiene 20 ms, que es 1/50 de un segundo de contenido de voz. Un segundo de vídeo se transmitirá como una secuencia de 30 imágenes fijas. Cada imagen está pensada para ser vista durante solo 33,3 ms, que es 1/30 de segundo, antes del siguiente fotograma de vídeo. El número de fotogramas transmitidos o representados por segundo se denomina velocidad de fotogramas.

En la sección siguiente, se proporcionan detalles sobre el formato de audio y vídeo que se usa en las reuniones y llamadas multimedia en tiempo real.

## <a name="audio-and-video-format"></a>Formatos de audio y vídeo

En formato de audio, cada segundo de audio se representa como 16 000 muestras, conteniendo cada una 16 bits de datos. Un fotograma de audio de 20 ms contiene 320 muestras, que son 640 bytes de datos.

En formato de vídeo, se admiten varios formatos. Dos propiedades clave de un formato de vídeo son su tamaño de fotograma y su formato de color. Los tamaños de fotograma admitidos incluyen 640 x 360, que son 360 píxeles, 1280 x 720, que son 720 píxeles, y 1920 x 1080, que son 1080 píxeles. Los formatos de color admitidos incluyen NV12, que es de 12 bits por píxel, y RGB24, que es de 24 bits por píxel.

Un fotograma de vídeo de 720-p contiene 921 600 píxeles, que son 1280 veces 720. En el formato de color RGB24, cada píxel se representa como 3 bytes, que son 24 bits, incluyendo 1 byte cada uno de los componentes de color rojo, verde y azul. Un único fotograma de vídeo RGB24 de 720p requiere de 2 764 800 bytes de datos, que son 921 600 veces píxeles 3 bytes por píxel. A una velocidad de fotogramas variable, el envío de fotogramas de vídeo RGB24 de 720p significará procesar, aproximadamente, 80 megabytes por segundo de contenido. El códec de vídeo H.264 comprime sustancialmente 80 megabytes antes de la transmisión de red.

Una funcionalidad avanzada de la plataforma permite que un bot envíe o reciba vídeo como fotogramas H.264 codificados. Se admiten los bot que proporcionen su propio codificador o descodificador H.264, o bien la secuencia de vídeo descodificada en mapas de bits RGB24 o NV12 sin procesar no es necesaria.

En la sección siguiente, se proporcionan detalles sobre qué participantes de la reunión hablan, que son los hablantes activos y dominantes.

## <a name="active-and-dominant-speakers"></a>Hablantes activos y dominantes

Cuando se une a una reunión de Teams que conste de varios participantes, un bot podrá identificar qué participantes de la reunión están hablando en ese momento. Los hablantes activos identificarán qué participantes son escuchados en cada fotograma de audio recibido. Los hablantes dominantes identificarán qué participantes son en ese momento más activos o dominantes en la conversación de grupo, aunque su voz no se escuche en cada fotograma de audio. El conjunto de hablantes dominantes podrá cambiar a medida que diferentes participantes se turnen para hablar.

En la sección siguiente, se proporcionarán detalles sobre las solicitudes de suscripción de vídeo realizadas por un bot.

## <a name="video-subscription"></a>Suscripción de vídeo

En una llamada 1:1, el bot recibirá automáticamente el vídeo del autor de la llamada si el bot está habilitado para recibir el vídeo. En una reunión de Teams, el bot deberá indicar a la plataforma qué participantes quiere ver. Una suscripción de vídeo es una solicitud del bot para recibir el contenido principal de vídeo o de pantalla compartida de un participante. A medida que los participantes en la reunión conversen, el bot modificará las suscripciones de vídeo necesarias. El bot modificará las suscripciones de vídeo en función de las notificaciones o actualizaciones del conjunto de altavoces dominante que indiquen qué participante está compartiendo la pantalla en ese momento.

En la sección siguiente, se proporcionan detalles sobre lo que deberá instalar, así como los requisitos para desarrollar un bot multimedia hospedado en aplicaciones.

## <a name="developer-resources"></a>Recursos para programadores

Para desarrollar un bot multimedia hospedado en aplicaciones, deberá instalar el paquete NuGet de la [biblioteca de .NET Microsoft.Graph.Calls.Media](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) que se ubica en el proyecto de Visual Studio.

Los bot multimedia hospedados en aplicaciones requieren .NET o C#, además de Windows Server. Para obtener más información, consulte [requisitos y consideraciones sobre los bot multimedia hospedados en aplicaciones](requirements-considerations-application-hosted-media-bots.md#c-or-net-and-windows-server-for-development).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Registrar un bot de llamadas](~/bots/calls-and-meetings/registering-calling-bot.md)

## <a name="see-also"></a>Consulte también

[Formatos multimedia admitidos para bots](~/resources/media-formats.md)
