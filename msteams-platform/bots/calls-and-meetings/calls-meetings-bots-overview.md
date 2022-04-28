---
title: Llamadas y bots de reuniones en línea
description: Obtenga información sobre cómo las aplicaciones de Microsoft Teams pueden interactuar con los usuarios mediante voz y vídeo mediante las API de Microsoft Graph para llamadas y reuniones en línea, y obtenga información sobre los flujos multimedia en tiempo real.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: llamadas a llamadas de vídeo de audio IVR voice online meetings real-time media streams bot
ms.openlocfilehash: a7b9dbe81304e2556b8b8b868f1f9e29f8bba284
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102510"
---
# <a name="calls-and-online-meetings-bots"></a>Llamadas y bots de reuniones en línea

Los bots pueden interactuar con Teams llamadas y reuniones mediante el uso compartido de voz, vídeo y pantalla en tiempo real. Con [las API de Microsoft Graph para llamadas y reuniones en línea](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), las aplicaciones Teams ahora pueden interactuar con los usuarios mediante voz y vídeo para mejorar la experiencia. Estas API le permiten agregar las siguientes características nuevas:

* Respuesta de voz interactiva (IVR).
* Control de llamadas.
* Acceso a secuencias de audio y vídeo en tiempo real, incluido el uso compartido de aplicaciones y escritorio.

Para usar estas API de Graph en una aplicación de Teams, cree un bot y especifique información y permisos adicionales.

Además, la Plataforma de medios en tiempo real permite a los bots interactuar con Teams llamadas y reuniones mediante el uso compartido de voz, vídeo y pantalla en tiempo real. Un bot que participa en audio o videollamadas y reuniones en línea es un bot de Microsoft Teams normal con algunas características adicionales que se usan para registrar el bot.

El manifiesto de aplicación Teams con dos configuraciones `supportsCalling` adicionales y `supportsVideo`, Graph permisos para el identificador de aplicación de Microsoft del bot y el consentimiento del administrador de inquilinos le permiten registrar el bot. Al registrar un bot de llamadas y reuniones para Teams, se menciona la dirección URL del webhook, que es el punto de conexión de webhook para todas las llamadas entrantes al bot. Un bot multimedia hospedado en la aplicación requiere Microsoft. Graph. Biblioteca de .NET Communications.Calls.Media para acceder a las secuencias multimedia de audio y vídeo, y el bot debe implementarse en una máquina Windows Server o en Windows Sistema operativo invitado (SO) del servidor en Azure. Los bots en Teams solo admiten un conjunto específico de formatos multimedia para el contenido de audio y vídeo.

Ahora, debe comprender algunos conceptos básicos, terminología y convenciones.

## <a name="terminologies"></a>Terminologías

Los siguientes conceptos básicos, terminología y convenciones le guían a través del uso de llamadas y bots de reuniones en línea:

* Llamadas de audio o vídeo
* Tipos de llamadas
* Señales
* Llamadas y reuniones en línea
* Medios en tiempo real

### <a name="audio-or-video-calls"></a>Llamadas de audio o vídeo

Las llamadas en Teams pueden ser puramente audio o audio y vídeo. En lugar de audio o videollamada, se usa el término llamada.

### <a name="call-types"></a>Tipos de llamadas

Las llamadas son punto a punto entre una persona y el bot o varias partes entre el bot y dos o más personas en una llamada de grupo.

:::image type="content" source="~/assets/images/calls-and-meetings/call-types.png" alt-text="Tipos de llamada"border="true":::

A continuación se muestran los distintos tipos de llamada y permisos necesarios para la llamada:

* Un usuario puede iniciar una llamada punto a punto con el bot o invitar al bot a una llamada multiparte existente. La llamada multiparte aún no está habilitada en la interfaz de usuario Teams.

    > [!NOTE]
    > Actualmente, las llamadas iniciadas por el usuario a un bot no se admiten en Microsoft Teams plataforma móvil.

* Graph permisos no son necesarios para que un usuario inicie una llamada punto a punto con el bot. Se necesitan permisos adicionales para que el bot participe en una llamada multiparte o para que el bot inicie una llamada punto a punto con un usuario.
* Una llamada puede iniciarse como punto a punto y, finalmente, convertirse en una llamada multiparte. El bot puede iniciar llamadas multiparte si invita a otros usuarios, siempre que el bot tenga los permisos adecuados. Si el bot no tiene permisos para participar en llamadas grupales y si un participante agrega otro participante a la llamada, el bot se quita de la llamada.

### <a name="signals"></a>Señales

Hay dos tipos de señales, llamada entrante y en llamada. A continuación se muestran las distintas características de las señales:

* Para recibir una llamada entrante, escriba un punto de conexión en la configuración del bot. Este punto de conexión recibe una notificación cuando se inicia una llamada entrante. Puede responder a la llamada, rechazarla o redirigirla a otra persona.

     :::image type="content" source="~/assets/images/calls-and-meetings/call-handling.png" alt-text="Control de llamadas"border="true":::

* Cuando un bot está en una llamada, hay API para silenciar y anular la conmutación por el bot y para iniciar o dejar de compartir contenido de vídeo o escritorio con otros participantes.
* El bot también puede acceder a la lista de participantes, invitar a nuevos participantes y silenciarlos.

### <a name="calls-and-online-meetings"></a>Llamadas y reuniones en línea

Desde la perspectiva de un usuario Teams, hay dos tipos de reuniones en línea, ad hoc y programadas. Desde la perspectiva de un bot, ambas reuniones en línea son las mismas. Para un bot, una reunión en línea es una llamada multiparte entre un conjunto de participantes e incluye coordenadas de reunión. Las coordenadas de reunión son los metadatos de la reunión, incluidos `botId`, `chatId` asociados a la reunión, `joinUrl`, `startTime` o `endTime`, etc.

### <a name="real-time-media"></a>Medios en tiempo real

Cuando un bot participa en una llamada o reunión en línea, debe tratar con las secuencias de audio y vídeo. Cuando los usuarios hablan en una llamada, se muestran en una cámara web o presentan sus pantallas en una reunión a un bot, se muestran como secuencias de audio y vídeo. Si un bot quiere decir algo tan sencillo como, **presione 0 para llegar al operador** en un escenario de respuesta de voz interactiva (IVR), requiere reproducir . Archivo WAV. Colectivamente, esto se conoce como medios de comunicación o medios en tiempo real.

Los medios en tiempo real se refieren a escenarios en los que los medios deben procesarse en tiempo real, en lugar de la reproducción de audio o vídeo grabados previamente. El trabajo con los flujos multimedia, especialmente los flujos de medios en tiempo real, es extremadamente complejo. Microsoft ha creado la Plataforma de medios en tiempo real para controlar estos escenarios y descargar la mayor parte del trabajo pesado tradicional del procesamiento de medios en tiempo real como sea posible. Cuando el bot responde a una llamada entrante o se une a una llamada nueva o existente, debe indicar a La Plataforma multimedia en tiempo real cómo se administran los medios. Si va a compilar una aplicación IVR, puede descargar el costoso procesamiento de audio a Microsoft. Como alternativa, si el bot requiere acceso directo a flujos multimedia, también se admite ese escenario. Hay dos tipos de procesamiento multimedia:

* **Medios hospedados por el servicio**: los bots se centran en la administración del flujo de trabajo de la aplicación, como el enrutamiento de llamadas y la descarga del procesamiento de audio a la plataforma multimedia en tiempo real de Microsoft. Con los medios hospedados por el servicio, tiene varias opciones para implementar y hospedar el bot. Puede implementar un bot de elementos multimedia hospedados en el servicio como servicio sin estado puesto que no procesa los elementos multimedia localmente. Los bots multimedia hospedados por el servicio pueden usar las siguientes API:

  * `PlayPrompt` para reproducir un clip de audio.
  * `Record` para grabar clips de audio.
  * `SubscribeToTone` para suscribirse a tonos de frecuencia múltiple de tono dual (DTMF).

    Por ejemplo, saber cuándo un usuario ha presionado **0** para llegar al operador.

* **Medios hospedados por la aplicación**: para que un bot obtenga acceso directo a los medios, necesita un permiso de Graph específico. Una vez que el bot tiene el permiso, la [Biblioteca multimedia en tiempo real](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) y el [SDK de llamadas de Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) le ayudan a crear elementos multimedia enriquecidos en tiempo real y bots de llamada. Un bot hospedado en la aplicación debe estar hospedado en un entorno de Windows. Para obtener más información, consulte [Bots multimedia hospedados en aplicaciones](./requirements-considerations-application-hosted-media-bots.md).

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **Graph** |
|---------------|----------|--------|
| comunicación Graph | Graph comunicaciones para interactuar con la plataforma de comunicaciones de Microsoft. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Llamadas y reuniones multimedia en tiempo real](~/bots/calls-and-meetings/real-time-media-concepts.md)

## <a name="see-also"></a>Vea también

* [referencia de Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Registro de un bot que admite llamadas y reuniones en línea](./registering-calling-bot.md)
* [Graph permisos para llamadas y bots de reuniones en línea](./registering-calling-bot.md#add-graph-permissions)
* [Cómo desarrollar bots de llamadas y reuniones en línea en el equipo](./debugging-local-testing-calling-meeting-bots.md)
* [Requisitos y consideraciones para los bots multimedia hospedados en aplicaciones](./requirements-considerations-application-hosted-media-bots.md)
* [Información técnica sobre el control de notificaciones de llamada entrantes](./call-notifications.md)
* [Configurar un operador automático](/microsoftteams/create-a-phone-system-auto-attendant)
* [Configuración de la respuesta automática para Salas de Microsoft Teams en dispositivos Android y Teams video phone](/microsoftteams/set-up-auto-answer-on-teams-android)
* [Teams directiva de grabación](/MicrosoftTeams/teams-recording-policy)