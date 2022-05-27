---
title: Bots para llamadas y reuniones en línea
description: Obtenga información sobre cómo las aplicaciones de Microsoft Teams pueden interactuar con los usuarios mediante voz y vídeo con las API de Microsoft Graph para llamadas y reuniones en línea, y sobre las transmisiones multimedia en tiempo real.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: bot de transmisión multimedia en tiempo real para llamadas de audio y vídeo IVR de reuniones en línea.
ms.openlocfilehash: 48c5283a1552c2f04651fe67254def0e6d60a8e6
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756733"
---
# <a name="calls-and-online-meetings-bots"></a>Bots para llamadas y reuniones en línea

Los bot podrán interactúan con llamadas y reuniones de Teams mediante el uso compartido de pantalla, vídeo y voz en tiempo real. Con [Microsoft Graph API para llamadas y reuniones en línea](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), las aplicaciones de Microsoft Teams ya pueden interactuar con los usuarios mediante voz y vídeo para mejorar la experiencia. Estas API le permitirán añadir las siguientes características nuevas:

* Respuesta interactiva de voz (IVR).
* Control de llamadas.
* Acceso a transmisión de audio y vídeo en tiempo real, incluyendo el uso compartido de aplicaciones y escritorio.

Para usar estas API de Graph en una aplicación de Teams, cree un bot y especifique información y permisos adicionales.

Además, la plataforma multimedia en tiempo real permitirá a los bots interactuar con las llamadas y reuniones de Teams mediante el uso compartido de voz, vídeo y pantalla en tiempo real. Un bot que participe en llamadas de audio o vídeo y reuniones en línea se trata de un bot normal de Microsoft Teams con algunas características adicionales que se usan para registrar el bot.

El manifiesto de aplicaciones de Teams con dos configuraciones adicionales, `supportsCalling` y `supportsVideo`, los permisos de Graph para el identificador de aplicaciones de Microsoft del bot, además del consentimiento del administrador de inquilinos le permitirán registrar el bot. Al registrar un bot de llamadas y reuniones para Teams, se mencionará la dirección URL del webhook, que es el punto de conexión de webhook para todas las llamadas entrantes al bot. Un bot multimedia hospedado en la aplicación requerirá que la biblioteca Microsoft.Graph.Communications.Calls.Media de .NET acceda a los stream multimedia de audio y vídeo, y el bot deberá implementarse en un sistema operativo (OS) invitado de Windows Server o en un equipo con Windows Server en Azure. Los bots en Teams solo admiten un conjunto específico de formatos multimedia para el contenido de audio y vídeo.

Ahora deberá comprender algunos conceptos básicos, terminología y convenciones.

## <a name="terminologies"></a>Terminología

Los siguientes conceptos básicos, terminología y convenciones le guiarán a través del uso de llamadas y bots de reuniones en línea:

* Llamadas de audio o vídeo
* Tipos de llamadas
* Señales
* Llamadas y reuniones en línea
* Multimedia en tiempo real

### <a name="audio-or-video-calls"></a>Llamadas de audio o vídeo

Las llamadas en Teams podrán ser puramente audio o audio y vídeo. En lugar de audio o videollamada, se usa el término llamada.

### <a name="call-types"></a>Tipos de llamadas

Las llamadas son de punto a punto entre una persona y el bot, o bien entre varias entidades entre el bot y dos o más personas en una llamada grupal.

:::image type="content" source="~/assets/images/calls-and-meetings/call-types.png" alt-text="Tipos de llamada"border="true":::

A continuación, se muestran los distintos tipos de llamada y permisos necesarios para las llamadas:

* Un usuario podrá iniciar una llamada de punto a punto con el bot o invitar al bot a una llamada existente entre varias entidades. La llamada multiparte aún no está habilitada en la interfaz de usuario Teams.

    > [!NOTE]
    > Actualmente, las llamadas iniciadas por usuarios a un bot no se admiten en la plataforma para móviles de Microsoft Teams.

* Graph permisos no son necesarios para que un usuario inicie una llamada punto a punto con el bot. Se necesitarán permisos adicionales para que los bot participen en llamadas multiparte o para que inicien llamadas punto a punto con un usuario.
* Una llamada puede iniciarse como punto a punto y, finalmente, convertirse en una llamada multiparte. El bot podrá iniciar llamadas grupales invitando a otros usuarios, siempre que tenga permiso para iniciar llamadas de grupo. Si el bot no tiene permisos para participar en llamadas grupales y si un participante agrega otro participante a la llamada, el bot se quita de la llamada.

### <a name="signals"></a>Señales

Hay dos tipos de señales, llamada entrante y en llamada. A continuación, se muestran las distintas características de las señales:

* Para recibir una llamada entrante, escriba un punto de conexión en la configuración del bot. Este punto de conexión recibirá una notificación cuando se inicie una llamada entrante. Podrá responder a la llamada, rechazarla o redirigirla a otra persona.

     :::image type="content" source="~/assets/images/calls-and-meetings/call-handling.png" alt-text="Control de llamadas"border="true":::

* Cuando un bot esté en una llamada, existen API para silenciar y anular al bot y para iniciar o dejar de compartir contenido de vídeo o escritorio con otros participantes.
* El bot también podrá acceder a la lista de participantes, invitar a nuevos participantes y silenciarlos.

### <a name="calls-and-online-meetings"></a>Llamadas y reuniones en línea

Desde la perspectiva de un usuario de Teams, hay dos tipos de reuniones en línea, ad hoc y programadas. Desde la perspectiva de un bot, ambas reuniones en línea son iguales. Para un bot, una reunión en línea es una llamada multiparte entre un conjunto de participantes e incluye coordenadas de la reunión. Las coordenadas de la reunión son los metadatos de la reunión, incluyendo `botId` y `chatId`, asociados a la reunión, o `joinUrl`, `startTime` o `endTime`, etc.

### <a name="real-time-media"></a>Multimedia en tiempo real

Cuando un bot participe en una llamada o reunión en línea, deberá tratar con las secuencias de audio y vídeo. Cuando los usuarios hablan en una llamada, se muestran en una cámara web o presentan sus pantallas en una reunión a un bot, se muestran como secuencias de audio y vídeo. Si un bot quiere decir algo tan sencillo como, **presione 0 para llegar al operador** en un escenario de respuesta interactiva de voz (IVR), necesitará reproducir un archivo .WAV. Colectivamente, esto se conoce como multimedia o multimedia en tiempo real.

Multimedia en tiempo real se refiere a escenarios en los que los medios deberán procesarse en tiempo real, en oposición a la reproducción de audio o vídeo, que son grabados previamente. El trabajo con secuencias multimedia, especialmente los flujos de medios en tiempo real, es complejo. Microsoft ha creado la plataforma multimedia en tiempo real para controlar estos escenarios y liberar la mayor parte del trabajo pesado tradicional del procesamiento multimedia en tiempo real como sea posible. Cuando el bot responda a una llamada entrante o se una a una llamada nueva o existente, tendrá que indicarle a la plataforma multimedia en tiempo real cómo se tratarán los elementos multimedia. Si va a compilar una aplicación IVR, puede descargar el costoso procesamiento de audio a Microsoft. Como alternativa, si el bot requiriera acceso directo a flujos multimedia, también se admite ese escenario. Hay dos tipos de procesamiento multimedia:

* **Medios hospedados por el servicio**: los bot se centran en la administración del flujo de trabajo de aplicaciones, como el enrutamiento de llamadas y la descarga del procesamiento de audio a la plataforma multimedia en tiempo real de Microsoft. Con los elementos multimedia hospedados en el servicio, tiene varias opciones de implementación y organización del bot. Un bot multimedia hospedado por el servicio se puede implementar como un servicio sin estado, ya que no procesa los medios localmente. Los bot multimedia hospedados por el servicio podrán usar las siguientes API:

  * `PlayPrompt` para reproducir un clip de audio.
  * `Record` para grabar clips de audio.
  * `SubscribeToTone` para suscribirse a tonos multifrecuencia de doble tono (DTMF).

    Por ejemplo, saber cuándo un usuario ha presionado **0** para llegar al operador.

* **Elementos multimedia hospedados por la aplicación**: para que un bot obtenga acceso directo a los medios, necesitará un permiso de Graph específico. Una vez que el bot tenga el permiso, la [Biblioteca multimedia en tiempo real](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) y el [SDK de llamadas de Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) le ayudarán a crear elementos multimedia enriquecidos en tiempo real y bots de llamadas. Un bot hospedado en la aplicación debe estar hospedado en un entorno de Windows. Para obtener más información, consulte [bots multimedia hospedados en aplicaciones](./requirements-considerations-application-hosted-media-bots.md).

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **Graph** |
|---------------|----------|--------|
| Comunicación de Graph | Comunicaciones de Graph para interactuar con la plataforma de comunicaciones de Microsoft. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Llamadas y reuniones multimedia en tiempo real](~/bots/calls-and-meetings/real-time-media-concepts.md)

## <a name="see-also"></a>Consulte también

* [Referencia de las API de Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Registrar un bot que admita llamadas y reuniones en línea](./registering-calling-bot.md)
* [Permisos de Graph para llamadas y bots de reuniones en línea](./registering-calling-bot.md#add-graph-permissions)
* [Cómo desarrollar los bot de llamadas y reuniones en línea en el ordenador](./debugging-local-testing-calling-meeting-bots.md)
* [Requisitos y consideraciones sobre los bot multimedia hospedados en aplicaciones](./requirements-considerations-application-hosted-media-bots.md)
* [Información técnica sobre el control de notificaciones de llamada entrantes](./call-notifications.md)
* [Configurar un operador automático](/microsoftteams/create-a-phone-system-auto-attendant)
* [Configuración de la respuesta automática para las salas de Teams en dispositivos Android y de vídeo de teléfono Teams](/microsoftteams/set-up-auto-answer-on-teams-android)
* [Directiva de grabación de Teams](/MicrosoftTeams/teams-recording-policy)
* [Trabajar con la API de comunicaciones en Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
