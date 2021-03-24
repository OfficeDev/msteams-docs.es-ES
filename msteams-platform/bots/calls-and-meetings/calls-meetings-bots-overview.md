---
title: Bots de llamadas y reuniones en línea
description: Obtén información sobre cómo las aplicaciones de Microsoft Teams pueden interactuar con los usuarios mediante voz y vídeo con las API de Microsoft Graph para llamadas y reuniones en línea.
keywords: llamadas de audio vídeo IVR reuniones en línea de voz
ms.openlocfilehash: 0fcf420ba8d698404d00bb2cab3d61cab2245f40
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034645"
---
# <a name="calls-and-online-meetings-bots"></a>Bots de llamadas y reuniones en línea

Con la adición de API de [Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)para llamadas y reuniones en línea, las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecciones mediante voz y vídeo. Estas API te permiten agregar nuevas características, como la respuesta de voz interactiva (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.

Para usar estas API de Microsoft Graph en una aplicación de Microsoft Teams, crea un bot y especifica información y permisos adicionales que describiremos en otro lugar, pero en primer lugar, es importante comprender algunos conceptos básicos, terminología y convenciones:

* **Llamadas de audio y vídeo.** Las llamadas en Teams pueden ser puramente audio o audio+vídeo. Por razones de brevedad, no decimos "llamada de audio y vídeo" en todas partes; simplemente decimos "llamar".
* **Tipos de llamadas.** Las llamadas son punto a punto (entre una persona y el bot) o multipartes (el bot y dos o más personas en una llamada de grupo).
  ![CallingTypes ](~/assets/images/calls-and-meetings/call-types.png) :
  * Un usuario puede iniciar una llamada punto a punto con el bot o invitar al bot a una llamada multiparte existente (aunque esta última aún no está habilitada en la interfaz de usuario de Microsoft Teams).
  
  > [!NOTE]
  > Actualmente, las llamadas iniciadas por el usuario a un bot no se admiten en la plataforma móvil de Microsoft Teams. 
  
  * Los permisos de Microsoft Graph no son necesarios para que un usuario inicie una llamada punto a punto con el bot, pero se necesitan permisos adicionales para que el bot participe en una llamada multipartid o para que el bot inicie una llamada punto a punto con un usuario.
  * Una llamada puede comenzar como punto a punto y escalar a varias partes. El bot puede iniciar esta escalada invitando a otros usuarios, siempre que el bot tenga los permisos adecuados. Si el bot no tiene permisos para participar en llamadas de grupo y un participante agrega otra parte, el bot se descarta de la llamada.
* **Señalización.** Hay dos tipos de señales: llamadas entrantes y llamadas entrantes:
  * Para recibir una llamada entrante, especifique un extremo en la configuración del bot; este extremo recibe una notificación cuando llega una llamada entrante. Puedes responder a la llamada, rechazarla o redirigirla a otro lugar o a otra persona.
  ![Tipos de llamadas](~/assets/images/calls-and-meetings/call-handling.png)
  * Cuando un bot está en una llamada, hay API para silenciar y desmutarse a sí mismo y para iniciar o dejar de compartir contenido de vídeo/escritorio con los demás participantes.
  * El bot también puede acceder a la lista de participantes, invitar a nuevos participantes y silenciarlos.
* **Llamadas y reuniones en línea.** Desde la perspectiva de un usuario de Teams, hay dos tipos de reuniones en línea: ad hoc y programadas. Sin embargo, desde la perspectiva de un bot, ambos son los mismos. Para un bot, una reunión en línea es solo una llamada multiparte (el conjunto de participantes) más "coordenadas de reunión", que puede ser los metadatos de la reunión: , asociados con la reunión, , y mucho `botId` `chatId` `joinUrl` `startTime` / `endTime` más.
* **Medios en tiempo real.** Cuando un bot participa en una llamada o reunión en línea, debe tratar con secuencias de audio y vídeo. Cuando los usuarios hablan en una llamada, se muestran en una cámara web o presentan sus pantallas en una reunión, un bot "ve" esto como secuencias de audio y/o vídeo. Si un bot quiere decir algo o presentar contenido de pantalla, eso requiere una secuencia de audio o vídeo. Incluso algo tan simple como el bot que dice "presione 0 para llegar al operador" en un escenario de IVR (respuesta de voz interactiva) significa reproducir un . ARCHIVO WAV. Colectivamente, nos referimos  a esto como medios o medios en tiempo _real_ (al hacer referencia a escenarios en los que los medios deben procesarse en tiempo real, en lugar de reproducir audio o vídeo grabados anteriormente). Históricamente, tratar con secuencias multimedia, especialmente las secuencias multimedia en tiempo real, ha sido extremadamente compleja para los desarrolladores. Microsoft ha creado la Plataforma multimedia en tiempo _real_ para controlar estos casos de uso y descargar la mayor parte del tradicional "trabajo pesado" del procesamiento multimedia en tiempo real como sea posible.  Cuando el bot responde a una llamada entrante o se une a una llamada nueva o existente, tiene que indicarle a la plataforma Real-time Media cómo se tratarán los elementos multimedia. Si está creando una aplicación IVR, puede descargar el costoso procesamiento de audio a Microsoft. Como alternativa, si el bot requiere acceso directo a las secuencias multimedia, también se admite ese escenario. Existen los dos tipos de procesamiento de medios:
  * **Medios hospedados en el servicio.** Los bots se centran en administrar el flujo de trabajo de aplicaciones (por ejemplo, las llamadas de enrutamiento) y en descargar el procesamiento de audio en la Plataforma multimedia en tiempo real de Microsoft. Con los medios hospedados en el servicio, tiene varias opciones para implementar y hospedar el bot. Un bot de medios hospedado por el servicio se puede implementar como un servicio sin estado, ya que no procesa los medios localmente. Los bots multimedia hospedados en el servicio pueden usar API como reproducir un clip de audio, grabar clips de audio o suscribirse a tonos `PlayPrompt` `Record` DTMF (por ejemplo, saber cuándo un usuario ha presionado 0 para llegar al `SubscribeToTone` operador).
  * **Medios hospedados en aplicaciones.** Para que un bot obtenga acceso directo a los medios, necesita un permiso específico de Graph, pero una vez que el bot lo tiene, la Biblioteca multimedia en tiempo [real](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) y el SDK de llamadas de [Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) le ayudan a crear medios enriquecidos en tiempo real y llamar a bots. Un bot hospedado por la aplicación debe hospedarse en un entorno windows, como se describe con más [detalle aquí](./requirements-considerations-application-hosted-media-bots.md).

## <a name="further-reading"></a>Lectura adicional

A continuación, encontrará más información sobre cómo crear y probar llamadas y bots de reuniones en línea:

* [Referencia de la API de Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Registro de un bot que admite llamadas](./registering-calling-bot.md) y reuniones en línea y permisos de Microsoft Graph para [bots](./registering-calling-bot.md#add-microsoft-graph-permissions) de llamadas y reuniones en línea
* [Cómo desarrollar bots de llamadas y reuniones en línea en el equipo local](./debugging-local-testing-calling-meeting-bots.md)
* [Más información sobre el procesamiento de medios](./real-time-media-concepts.md)en tiempo real y lo que se necesita para admitir medios [hospedados en aplicaciones](./requirements-considerations-application-hosted-media-bots.md)
* [Información técnica sobre cómo controlar las notificaciones de llamadas entrantes](./call-notifications.md)
