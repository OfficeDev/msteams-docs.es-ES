---
title: Bots de llamadas y reuniones en línea
description: Obtén información sobre cómo las aplicaciones de Microsoft Teams pueden interactuar con los usuarios mediante voz y vídeo con las API de Microsoft Graph para llamadas y reuniones en línea.
ms.topic: conceptual
localization_priority: Normal
keywords: llamadas de audio vídeo IVR reuniones en línea de voz
ms.openlocfilehash: 52a7e1e24fdc0a2c17264087e4f4461b7c43a50a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020172"
---
# <a name="calls-and-online-meetings-bots"></a>Bots de llamadas y reuniones en línea

> [!NOTE]
> Actualmente, la compatibilidad con llamadas y bots de reunión en línea no se admite en la plataforma móvil de Microsoft Teams.

Los bots pueden interactuar con las llamadas y reuniones de Teams mediante el uso compartido de pantalla, vídeo y voz en tiempo real. Con [las API de Microsoft Graph para](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)llamadas y reuniones en línea, las aplicaciones de Teams ahora pueden interactuar con usuarios que usan voz y vídeo para mejorar la experiencia. Estas API le permiten agregar las siguientes características nuevas:

* Respuesta de voz interactiva (IVR).
* Control de llamadas.
* Acceso a secuencias de audio y vídeo en tiempo real, incluido el uso compartido de aplicaciones y escritorio.

Para usar estas API de Graph en una aplicación de Teams, creas un bot y especificas información y permisos adicionales.

Además, la Plataforma multimedia en tiempo real permite a los bots interactuar con las llamadas y reuniones de Teams mediante el uso compartido de voz, vídeo y pantalla en tiempo real. Un bot que participa en llamadas de audio o vídeo y reuniones en línea es un bot de Microsoft Teams normal con pocas características adicionales usadas para registrar el bot.

El manifiesto de la aplicación de Teams con dos configuraciones adicionales y , los permisos graph para el identificador de aplicación de Microsoft del bot y el consentimiento de administrador de inquilinos permiten `supportsCalling` `supportsVideo` registrar el bot. Al registrar un bot de llamadas y reuniones para Teams, se menciona la dirección URL de webhook, que es el extremo de webhook para todas las llamadas entrantes al bot. Un bot multimedia hospedado por la aplicación requiere que la biblioteca microsoft.Graph.Communications.Calls.Media .NET tenga acceso a las secuencias multimedia de audio y vídeo, y el bot debe implementarse en un equipo de Windows Server o en un sistema operativo invitado (OS) de Windows Server en Azure. Los bots de Teams solo admiten un conjunto específico de formatos multimedia para el contenido de audio y vídeo.

Ahora, debe comprender algunos conceptos básicos, terminología y convenciones.

## <a name="terminologies"></a>Terminologías

Los siguientes conceptos básicos, terminología y convenciones le guían a través del uso de bots de llamadas y reuniones en línea:

* Llamadas de audio o vídeo
* Tipos de llamadas
* Señales
* Llamadas y reuniones en línea
* Medios en tiempo real

### <a name="audio-or-video-calls"></a>Llamadas de audio o vídeo

Las llamadas en Teams pueden ser puramente audio o audio y vídeo. En lugar de llamada de audio o vídeo, se usa el término llamada.

### <a name="call-types"></a>Tipos de llamadas

Las llamadas son punto a punto entre una persona y el bot, o varias partes entre el bot y dos o más personas en una llamada de grupo.

![Tipos de llamadas](~/assets/images/calls-and-meetings/call-types.png)

A continuación se enumeran los distintos tipos de llamadas y permisos necesarios para la llamada:

* Un usuario puede iniciar una llamada punto a punto con el bot o invitar al bot a una llamada multiparte existente. La llamada multiparte aún no está habilitada en la interfaz de usuario de Teams.
* Los permisos de gráfico no son necesarios para que un usuario inicie una llamada punto a punto con el bot. Se necesitan permisos adicionales para que el bot participe en una llamada multiparte o para que el bot inicie una llamada punto a punto con un usuario.
* Una llamada puede iniciarse como punto a punto y, finalmente, convertirse en una llamada multipartid. El bot puede iniciar llamadas multipartes invitando a otras personas, siempre que el bot tenga los permisos adecuados. Si el bot no tiene permisos para participar en llamadas de grupo y si un participante agrega otro participante a la llamada, el bot se descarta de la llamada.

### <a name="signals"></a>Señales

Hay dos tipos de señales, llamadas entrantes y llamadas entrantes. A continuación se incluyen las diferentes características de las señales:

* Para recibir una llamada entrante, escriba un punto de conexión en la configuración del bot. Este extremo recibe una notificación cuando se inicia una llamada entrante. Puedes responder a la llamada, rechazarla o redirigirla a otra persona.

    ![Control de llamadas](~/assets/images/calls-and-meetings/call-handling.png)

* Cuando un bot está en una llamada, hay API para silenciar y desmutar el bot y para iniciar o detener el uso compartido de contenido de escritorio o vídeo con otros participantes.
* El bot también puede acceder a la lista de participantes, invitar a nuevos participantes y silenciarlos.

### <a name="calls-and-online-meetings"></a>Llamadas y reuniones en línea

Desde la perspectiva de un usuario de Teams, hay dos tipos de reuniones en línea, ad hoc y programadas. Desde la perspectiva de un bot, ambas reuniones en línea son las mismas. Para un bot, una reunión en línea es una llamada multipartid entre un conjunto de participantes e incluye coordenadas de reunión. Las coordenadas de reunión son los metadatos de la reunión, incluidos , asociados con la `botId` `chatId` reunión, `joinUrl` o , y `startTime` así `endTime` sucesivamente.

### <a name="real-time-media"></a>Medios en tiempo real

Cuando un bot participa en una llamada o reunión en línea, debe tratar con secuencias de audio y vídeo. Cuando los usuarios hablan en una llamada, se muestran en una cámara web o presentan sus pantallas en una reunión, a un bot que se muestra como secuencias de audio y vídeo. Si un bot quiere decir algo tan simple como presionar **0** para llegar al operador en un escenario de respuesta de voz interactiva (IVR), requiere reproducir un . ARCHIVO WAV. Colectivamente, esto se conoce como medios o medios en tiempo real.

Los medios en tiempo real se refieren a escenarios en los que los medios deben procesarse en tiempo real, en lugar de reproducir audio o vídeo grabados anteriormente. Tratar con secuencias multimedia, especialmente en tiempo real, es extremadamente complejo. Microsoft ha creado la Plataforma multimedia en tiempo real para controlar estos escenarios y descargar la mayor parte del trabajo pesado tradicional del procesamiento multimedia en tiempo real como sea posible. Cuando el bot responde a una llamada entrante o se une a una llamada nueva o existente, debe decir a la Plataforma multimedia en tiempo real cómo se administran los medios. Si está creando una aplicación IVR, puede descargar el costoso procesamiento de audio a Microsoft. Como alternativa, si el bot requiere acceso directo a las secuencias multimedia, también se admite ese escenario. Hay dos tipos de procesamiento de medios:

* **Medios hospedados en** el servicio: los bots se centran en administrar el flujo de trabajo de aplicaciones, como el enrutamiento de llamadas y la descarga de procesamiento de audio en la Plataforma multimedia en tiempo real de Microsoft. Con los medios hospedados en el servicio, tiene varias opciones para implementar y hospedar el bot. Puede implementar un bot de elementos multimedia hospedados en el servicio como servicio sin estado puesto que no procesa los elementos multimedia localmente. Los bots multimedia hospedados en el servicio pueden usar las siguientes API:

    * `PlayPrompt` para reproducir un clip de audio.
    * `Record` para grabar clips de audio.
    * `SubscribeToTone` para suscribirse a tonos de frecuencia múltiple de tono dual (DTMF).

    Por ejemplo, saber cuándo un usuario ha presionado **0** para llegar al operador.

* **Medios hospedados en aplicaciones:** para que un bot obtenga acceso directo a los medios, necesita un permiso de Graph específico. Después de que el bot tenga el permiso, la Biblioteca multimedia en tiempo [real](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)y el SDK de llamadas de [Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) le ayudarán a crear bots de llamadas y medios enriquecidos en tiempo real. Un bot hospedado en la aplicación debe estar hospedado en un entorno de Windows. Para obtener más información, [vea bots multimedia hospedados en aplicaciones](./requirements-considerations-application-hosted-media-bots.md).

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de ejemplo** | **Description** | **Graph** |
|---------------|----------|--------|
| Comunicación de gráficos | Gráfico de comunicaciones para interactuar con la plataforma de comunicaciones de Microsoft. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Referencia de la API de Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
> [!div class="nextstepaction"]
> [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
> [!div class="nextstepaction"]
> [Registro de un bot que admite llamadas y reuniones en línea](./registering-calling-bot.md)
> [!div class="nextstepaction"]
> [Permisos de Graph para bots de llamadas y reuniones en línea](./registering-calling-bot.md#add-graph-permissions)
> [!div class="nextstepaction"]
> [Cómo desarrollar bots de llamadas y reuniones en línea en el equipo](./debugging-local-testing-calling-meeting-bots.md)
> [!div class="nextstepaction"]
> [Requisitos y consideraciones para bots multimedia hospedados en aplicaciones](./requirements-considerations-application-hosted-media-bots.md)
> [!div class="nextstepaction"]
> [Información técnica sobre cómo controlar las notificaciones de llamadas entrantes](./call-notifications.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Llamadas y reuniones multimedia en tiempo real](~/bots/calls-and-meetings/real-time-media-concepts.md)
