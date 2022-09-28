---
title: Webhooks y conectores
author: clearab
description: Obtenga información sobre cómo los webhooks y los conectores ayudan a conectar los servicios web a los canales y equipos de Microsoft Teams. Obtenga información sobre los webhooks entrantes, salientes y los conectores de Office 365.
ms.localizationpriority: high
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 94c84b577dfb20cb823167d3af84f5460bb87554
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100451"
---
# <a name="webhooks-and-connectors"></a>Webhooks y conectores

Los webhooks y conectores ayudan a conectar los servicios web a canales y equipos en Microsoft Teams. Los webhooks son devoluciones de llamada HTTP definidas por el usuario que notifican a los usuarios cualquier acción que haya tenido lugar en el canal de Teams. Es una manera de que una aplicación obtenga datos en tiempo real. Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Exponen un punto de conexión HTTPS para que el servicio publique mensajes en forma de tarjetas.

> [!IMPORTANT]
> Puede elegir crear una aplicación de Teams del bot de notificación que no sea webhooks entrantes. Se realizan de forma similar, pero el bot de notificación tiene más funcionalidades. Para obtener más información, consulte [Compilación de un bot de notificación con JavaScript](../sbs-gs-notificationbot.yml) o [un ejemplo de notificación de webhook entrante](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification). Para empezar, descargue [Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) ahora y explore. Para obtener más información, vea [Documentos del kit de herramientas de Teams](../toolkit/teams-toolkit-fundamentals.md).

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks ayudan a Teams a integrarse con aplicaciones externas. Los webhooks salientes permiten que los usuarios envíen mensajes de texto desde un canal a los servicios web. Después de configurar los webhooks salientes, los usuarios pueden @mention webhook saliente y enviar un mensaje a los servicios web. El servicio responde en un plazo de 10 segundos al mensaje con un texto o una tarjeta.

> [!NOTE]
> Los webhooks salientes se configuran por equipo y no se pueden incluir como parte de una aplicación de Teams normal.

## <a name="connectors"></a>Conectores

Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Exponen el punto de conexión HTTPS para que el servicio publique mensajes en canales de Teams, normalmente en forma de tarjetas.

### <a name="incoming-webhooks"></a>Webhooks entrantes

Los webhooks entrantes ayudan a publicar mensajes de aplicaciones en Teams. Si los webhooks entrantes están habilitados para un equipo en cualquier canal, exponen el punto de conexión HTTPS, que acepta el archivo JSON con el formato correcto e inserta los mensajes en ese canal. Por ejemplo, puede crear un webhook entrante en el canal de DevOps, configurar la compilación e implementar y supervisar servicios simultáneamente para enviar alertas.

#### <a name="notification-bot-or-incoming-webhook---choose-the-right-one"></a>Bot de notificación o webhook entrante: elija el correcto.

Antes de empezar a aprender a crear webhooks entrantes, es posible que también quiera saber que puede crear un bot de notificación mediante el kit de herramientas de Teams. Los bots de notificación pueden habilitar una experiencia más personalizable para satisfacer diferentes escenarios empresariales.

Obtenga más información sobre las diferencias entre el bot de notificación y el webhook entrante para que pueda elegir soluciones correctas para sus escenarios:

| &nbsp; | Bot de notificación |  Webhook entrante |
| --- | --- | --- |
| ¿Qué es? | Una aplicación de Teams | Una característica de Teams |
| Instalación necesaria | Sí | No |
| Escenarios adecuados | • Recibir notificaciones y mensajes periódicamente, por ejemplo, recibir notificaciones diarias de tareas del equipo. <br>  • Recibir notificaciones y mensajes basados en eventos reales. Por ejemplo, una vez que los compañeros de equipo cargan archivos, recibe notificaciones. | Comunicarse con aplicaciones externas y recibir notificaciones y mensajes de otras aplicaciones. |
| Configuración del ámbito | • Canal de Teams <br> • Chat en grupo <br> • Chat personal | Canal de Teams |
| Proceso de mensaje | Un bot de notificación funciona como una aplicación de Teams. Puede definir la lógica de negocios para procesar datos y mostrar datos en un formato personalizado. | Webhook es una característica de Teams en lugar de una aplicación de Teams, por lo que solo recibe y muestra datos sin procesamiento. |
| Recuperación del contexto de Teams | El bot de notificación puede recuperar el contexto de Teams, como el canal o la información del usuario, los mensajes, etc. | No |
| Enviar tarjeta adaptable | Sí | Sí |
| Enviar un mensaje de bienvenida | Puede enviar un mensaje de bienvenida | Sin mensaje de bienvenida |
| Desencadenador admitido | Todos los desencadenadores admitidos. Si usa Teams Toolkit, puede obtener rápidamente proyectos de plantilla con los siguientes desencadenadores: <br> • Desencadenador de tiempo hospedado en funciones de Azure. <br> • Restify HTTP trigger hosted on Azure App Service (Restify HTTP trigger hospedado en Azure App Service) <br> • Desencadenador HTTP hospedado en Azure Functions | Todos los desencadenadores admitidos |
| Herramientas de compilación | • [Introducción al kit de herramientas de Teams para Visual Studio Code](../toolkit/teams-toolkit-fundamentals.md) <br> • [Introducción al kit de herramientas de Teams para Visual Studio](../toolkit/teams-toolkit-fundamentals.md) <br> • [Biblioteca TeamsFx](../toolkit/TeamsFx-CLI.md) <br> • [SDK de TeamsFx](../toolkit/TeamsFx-SDK.md) | No se requiere ninguna herramienta |
| Recurso en la nube necesario | Azure Bot Framework | No se requieren recursos |
| Tutorial | [Crear un bot de notificaciones con JavaScript](../sbs-gs-notificationbot.yml) | [ejemplo de notificación de webhook entrante](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification) |

### <a name="office-365-connectors"></a>Conectores de Office 365

Los conectores de Office 365 le permiten crear una página de configuración personalizada para el webhook entrante y empaquetarlas como parte de una aplicación de Teams. Los mensajes se envían principalmente mediante tarjetas del Conector de Office 365 y tienen la capacidad de agregar un conjunto limitado de acciones de tarjeta. Por ejemplo, un conector meteorológico que permite a los usuarios seleccionar una ubicación y cualquier hora del día para recibir actualizaciones sobre el clima de mañana. Se configuran en el nivel de canal, pero se instalan en el nivel de equipo.

> [!NOTE]
> Puede distribuir la aplicación de Teams de Conector de Office 365 a nuestra AppStore.

## <a name="create-and-send-messages"></a>Crear y enviar mensajes

Los mensajes que requieren acción permiten a los usuarios tomar medidas sin salir de su cliente de correo electrónico, lo que aumenta la involucración del usuario. Con Office 365 y los webhooks entrantes, puede enviar mensajes publicando una carga JSON en la dirección URL del webhook.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="see-also"></a>Vea también

* [Creación de un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Crear un bot de notificaciones con JavaScript](../sbs-gs-notificationbot.yml)
* [Cree su primera aplicación de bot con JavaScript](../sbs-gs-bot.yml)
