---
title: Llamadas y bots de reuniones en línea
description: Obtenga información sobre cómo las aplicaciones de Microsoft Teams pueden interactuar con los usuarios mediante voz y vídeo mediante las API de Microsoft Graph para las llamadas y las reuniones en línea.
keywords: llamar llamadas audio video IVR Voice online reuniones
ms.openlocfilehash: fa31bc55221befab1ac1b6b77e116f3fc2e1a935
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552433"
---
# <a name="calls-and-online-meetings-bots"></a>Llamadas y bots de reuniones en línea

> [!NOTE]
> Actualmente, la plataforma móvil de Microsoft Teams no admite la compatibilidad con las llamadas y los bots de reuniones en línea. 

Con la adición de las [API de Microsoft Graph para las llamadas y las reuniones en línea](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecidas mediante voz y vídeo. Estas API permiten agregar nuevas características, como la respuesta interactiva de voz (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.

Para usar estas API de Microsoft Graph en una aplicación de Microsoft Teams, debe crear un bot y especificar información y permisos adicionales que se describirán en otra parte, pero, en primer lugar, es importante comprender algunos conceptos básicos, terminología y convenciones:

* **Llamadas de audio y vídeo.** Las llamadas en Microsoft Teams pueden ser puramente de audio o audio + vídeo. Por razones de brevedad, no decimos "llamada de audio y vídeo" en todas partes; simplemente decimos "llamar".
* **Tipos de llamadas.** Las llamadas son de punto a punto (entre una persona y su bot) o varias partes (el bot y dos o más personas en una llamada de grupo).
  ![CallingTypes ](~/assets/images/calls-and-meetings/call-types.png) :
  * Un usuario puede iniciar una llamada punto a punto con su bot o invitar a su bot a una llamada entre varias personas existente (aunque esta última todavía no está habilitada en la interfaz de usuario de Microsoft Teams).
  * Los permisos de Microsoft Graph no son necesarios para que un usuario inicie una llamada punto a punto con el bot, pero se necesitan permisos adicionales para que el bot participe en una llamada entre varias personas o para que el bot inicie una llamada punto a punto con un usuario.
  * Una llamada puede empezar a ser de punto a punto y escalarse a varios elementos. El bot puede iniciar esta escalación invitando a otros, siempre que el bot tenga los permisos adecuados. Si el bot no tiene permisos para participar en llamadas de grupo y un participante agrega a otra parte, el bot desaparecerá de la llamada.
* **Señalización.** Hay dos tipos de señales: llamada entrante y llamada:
  * Para recibir una llamada entrante, debe especificar un extremo en la configuración de bot; este extremo recibe una notificación cuando llega una llamada entrante. Puede responder a la llamada, rechazarla o redirigirla a algún sitio o a otra persona.
  ![Tipos de llamadas](~/assets/images/calls-and-meetings/call-handling.png)
  * Cuando un bot está en una llamada, hay varias API para silenciar y deshacer el desactivación del audio y comenzar o dejar de compartir contenido de vídeo y escritorio con los demás participantes.
  * El bot también puede tener acceso a la lista de participantes, invitar a nuevos participantes y silenciarlos.
* **Llamadas y reuniones en línea.** Desde el punto de vista de un usuario de Teams, hay dos tipos de reuniones en línea: ad hoc y programadas. Sin embargo, desde el punto de vista de un bot, ambos son iguales. Para un bot, una reunión en línea es solo una llamada entre varias partes (el conjunto de participantes) más "coordenadas de la reunión", que puede considerar como los metadatos de la reunión: `botId` , `chatId` asociado con la reunión,, `joinUrl` `startTime` / `endTime` y más.
* **Medios en tiempo real.** Cuando un bot participa en una llamada o una reunión en línea, debe ocuparse de las secuencias de audio y vídeo. Cuando los usuarios hablan en una llamada, se muestran en una cámara web o presentan sus pantallas en una reunión, un bot "ve" como secuencias de audio o vídeo. Si un bot desea decir algo o presentar contenido de la pantalla, es necesario un flujo de audio o vídeo. Incluso algo tan sencillo como el bot que dice: "presione 0 para llegar al operador" en un escenario IVR (respuesta interactiva de voz) que reproduce un. Archivo WAV. De forma colectiva, nos referimos a esto como medios en _tiempo real_ o _medios_ (al hacer referencia a escenarios en los que los medios deben procesarse en tiempo real, en lugar de la reproducción de audio/vídeo grabados previamente). Históricamente, trabajar con flujos de medios, sobre todo en flujos de medios en tiempo real, ha sido extremadamente complejo para los programadores. Microsoft ha creado la _plataforma de medios en tiempo real_ para administrar estos casos de uso y descargar tanto como sea posible la mayor parte del "levantamiento" más tradicional del procesamiento de medios en tiempo real.  Cuando el bot responde a una llamada entrante o se une a una llamada nueva o existente, tiene que indicarle a la plataforma Real-time Media cómo se tratarán los elementos multimedia. Si está creando una aplicación IVR, puede descargar el procesamiento de audio caro para Microsoft. Como alternativa, si el bot requiere acceso directo a los flujos de medios, también admitimos ese escenario. Hay dos tipos de procesamiento de medios:
  * **Medios hospedados en el servicio.** Los bots se centran en administrar el flujo de trabajo de la aplicación (por ejemplo, las llamadas de enrutamiento) y descargar el procesamiento de audio a la plataforma multimedia en tiempo real de Microsoft. Con los medios hospedados en el servicio, tiene varias opciones para implementar y hospedar el bot. Un bot? n de medios hospedado por el servicio se puede implementar como un servicio sin estado, ya que no procesa los medios de forma local. Los bots de medios hospedados en el servicio pueden usar API como `PlayPrompt` para reproducir un clip de audio, `Record` para grabar clips de audio o `SubscribeToTone` para suscribirse a tonos DTMF (por ejemplo, saber cuándo un usuario presionó 0 para llegar al operador).
  * **Medios hospedados en la aplicación.** Para que un bot obtenga acceso directo a los medios, necesita un permiso específico de Graph, pero una vez que su bot lo tenga, la [biblioteca multimedia en tiempo real](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) y el [SDK de llamadas de Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) le ayudarán a crear multimedia en tiempo real enriquecida, llamando a bots. Un bot hospedado por la aplicación debe alojarse en un entorno Windows, tal y como se describe [aquí](./requirements-considerations-application-hosted-media-bots.md)con más detalle.

## <a name="further-reading"></a>Lecturas adicionales

Aquí encontrará más información sobre cómo crear y probar llamadas y los bots de reuniones en línea:

* [Referencia de la API de Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Registro de un bot que admite llamadas y reuniones en línea](./registering-calling-bot.md) y [permisos de Microsoft Graph para las llamadas y los bots de reuniones en línea](./registering-calling-bot.md#add-microsoft-graph-permissions)
* [Cómo desarrollar los bots de llamada y reunión en línea en su equipo local](./debugging-local-testing-calling-meeting-bots.md)
* [Más información sobre el procesamiento de medios en tiempo real](./real-time-media-concepts.md)y [lo que se necesita para admitir medios hospedados en la aplicación](./requirements-considerations-application-hosted-media-bots.md)
* [Información técnica sobre el control de las notificaciones de llamadas entrantes](./call-notifications.md)
