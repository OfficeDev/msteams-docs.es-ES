---
title: Llamadas de medios en tiempo real y reuniones en línea con Microsoft Teams
description: Comprenda los conceptos clave de Building bot que pueden realizar llamadas de audio y vídeo en tiempo real y reuniones en línea.
keywords: 'secuencia de vídeo de audio secuencia de vídeo llamada de audio y vídeo llamada a medios en tiempo real: medios hospedados en el servicio de medios hospedados por la aplicación'
ms.openlocfilehash: 0ec99d1caa8810d292170c7c70a1518de7301873
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675873"
---
# <a name="real-time-media-calls-and-meetings-with-microsoft-teams"></a>Llamadas de medios en tiempo real y reuniones con Microsoft Teams

La plataforma de medios en tiempo real permite que los bots interactúen con las llamadas y las reuniones de Microsoft Teams mediante el uso compartido de voz, vídeo y pantalla en tiempo real. Se trata de una función avanzada que permite al robot enviar y recibir contenido de voz y vídeo *por trama*. El bot tiene acceso "sin procesar" a las secuencias multimedia de voz, vídeo y uso compartido de la pantalla. (Bots que procesan los propios medios se llaman bots _de medios hospedados_ por la aplicación, en lugar de los bots de _medios hospedados por servicios_ más sencillos que se basan en la plataforma de medios en tiempo real para todo el procesamiento de medios).

Por ejemplo, en una llamada de 1:1 con un bot, a medida que el usuario habla, el bot recibirá 50 fotogramas de audio por segundo, con cada fotograma que contenga 20 milisegundos (MS) de audio. Un bot? o de medios hospedado en la aplicación puede realizar el reconocimiento de voz en tiempo real a medida que se reciben las tramas de audio, en lugar de tener que esperar una grabación después de que el usuario haya dejado de hablar. El bot también puede enviar y recibir vídeo de alta definición, incluido el contenido de uso compartido de pantalla basado en el vídeo.

La plataforma proporciona una API similar a un socket para que el bot envíe y reciba medios, y controla la codificación y descodificación en tiempo real de los paquetes de audio/vídeo mediante códecs como seda y G. 722 para audio y H. 264 para vídeo. La plataforma también administra todo el cifrado y descifrado de paquetes de medios y la transmisión de la red de paquetes, por lo que el bot solo tiene que preocuparse del contenido real de audio y vídeo. Un bot? a de medios en tiempo real puede participar en llamadas de 1:1, así como en reuniones con varios participantes.

En este artículo se presentan conceptos clave relacionados con la creación de un bot que puede realizar llamadas de audio y vídeo en tiempo real con Microsoft Teams.

## <a name="media-session"></a>Sesión de medios

Cuando un bot? o de medios en tiempo real responde a una llamada entrante o se une a una reunión de Microsoft Teams, debe declarar qué modalidades tiene previsto admitir. Para cada modalidad admitida, el bot declara si puede enviar y recibir medios, recibir solo o enviar sólo. Por ejemplo, un bot diseñado para controlar las llamadas de 1:1 Teams puede desear enviar y recibir audio, pero solo *Enviar* vídeo (ya que no es necesario recibir el vídeo del autor de la llamada). El conjunto de modalidades de audio y vídeo establecidas entre el bot y el autor de la llamada o la reunión de Microsoft Teams se denomina la **sesión de medios**.

Se admiten dos tipos de modalidades de vídeo: el **vídeo principal** y **el uso compartido de pantalla basado en vídeo**. El vídeo principal se usa para transportar el vídeo desde la cámara web de un usuario. La pantalla compartida basada en vídeo permite al usuario compartir su pantalla como una secuencia de vídeo. La plataforma permite a un bot enviar o recibir *ambos* tipos de vídeo.

Cuando se une a una reunión de Microsoft Teams, un bot puede recibir varias secuencias de vídeo principales a la vez, hasta 10 por sesión de medios. Esto permite que el bot "vea" más de un participante en la reunión.

## <a name="frames-and-frame-rate"></a>Velocidad de fotogramas y fotogramas

Un robot de medios en tiempo real interactúa directamente con las modalidades de audio y vídeo de una sesión de medios. Esto significa que el bot está enviando o recibiendo medios como una secuencia de **Marcos**, donde cada fotograma representa una unidad de contenido. Un segundo de audio puede transmitirse como una secuencia de 50 fotogramas, con cada fotograma que contenga 20 milisegundos (MS), 1/50 veces de segundo, de contenido de voz. Un segundo valor de vídeo puede dividirse como una secuencia de 30 imágenes fijas, cada una destinada a ser vista sólo 33.3 ms (1/30 de segundo) antes de que se muestre el siguiente fotograma de vídeo. El número de tramas transmitidas o representadas por segundo se denomina la **velocidad de fotogramas**. "30fps" indica 30 fotogramas por segundo.

## <a name="audio-format"></a>Formato de audio

Cada segundo de audio se representa como **ejemplos**de 16.000, con cada ejemplo que contiene 16 bits de datos. Un marco de audio 20 MS contiene 320 ejemplos (640 bytes de datos).

## <a name="video-format"></a>Formato de vídeo

Hay varios formatos compatibles con el vídeo. Las dos propiedades clave de un formato de vídeo son el **tamaño del marco** y el **formato de color**. Los tamaños de fotograma compatibles incluyen 640 x 360 ("360p"), 1280x720 ("720p") y 1920 x 1080 ("1080p"). Los formatos de color admitidos incluyen NV12 (12 bits por píxel) y RGB24 (24 bits por píxel).

Un fotograma de vídeo "720p" contiene 921.600 píxeles (1280 veces 720). En el formato de color RGB24, cada píxel se representa como 3 bytes (24 bits), compuesto de un byte en cada uno de los componentes de color rojo, verde y azul. Por lo tanto, un solo fotograma de vídeo 720p RGB24 requiere 2.764.800 bytes de datos (921.600 píxeles multiplicados por 3 bytes/píxel). A una velocidad de fotogramas de 30fps, el envío de fotogramas de vídeo 720p RGB24 significa un procesamiento de aproximadamente 80 MB/s de contenido (que es comprimido de forma sustancial por el códec de vídeo H. 264 antes de la transmisión por red).

Una funcionalidad avanzada de la plataforma permite a un bot enviar o recibir vídeo como fotogramas H. 264 **codificado** . Esto es compatible con bots que proporcionen su propio codificador/descodificador H. 264, o no necesiten la secuencia de vídeo descodificada en RGB24 sin formato o NV12 de mapas de bits.

## <a name="active-and-dominant-speakers"></a>Altavoces activos y dominantes

Cuando se une a una reunión de Microsoft teams que consta de varios participantes, un bot puede identificar los participantes de la reunión que están hablando en ese momento. Los **altavoces activos** identifican qué participantes se escuchan en cada trama de audio recibida. Los **altavoces dominantes** identifican qué participantes están actualmente más activos (o "dominante") en la conversación de grupo, aunque su voz no se escucha en cada trama de audio. El conjunto de altavoces dominantes puede cambiar a medida que varios participantes tomen turnos.

## <a name="video-subscription"></a>Suscripción de vídeo

En una llamada de 1:1, el bot recibirá automáticamente el vídeo del autor de la llamada si el bot está habilitado para recibir vídeo. En una reunión de Microsoft Teams, el bot debe indicar a la plataforma qué participantes desea ver. Una **suscripción de vídeo** es una solicitud del bot para recibir el contenido principal de vídeo o de uso compartido de pantalla de un participante. A medida que los participantes de la reunión realizan la conversación, el bot puede modificar sus suscripciones de vídeo deseadas en función de las actualizaciones del conjunto de altavoces dominantes o de las notificaciones que indican qué participante está actualmente en uso compartido de la pantalla.

## <a name="developer-resources"></a>Recursos para desarrolladores

Para desarrollar un bot de medios hospedado en la aplicación, debe instalar el siguiente paquete de NuGet en el proyecto de Visual Studio:

- [Biblioteca de Microsoft. Graph. calls. Media .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)

Los bots de medios hospedados en aplicaciones requieren .NET/C# y Windows Server, tal y como se describe en detalle en [requisitos y consideraciones para los bots de medios hospedados en la aplicación](requirements-considerations-application-hosted-media-bots.md#application-hosted-media-bot-development-requires-cnet-and-windows-server).
