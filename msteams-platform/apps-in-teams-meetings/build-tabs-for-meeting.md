---
title: Pestañas de compilación para la reunión
author: surbhigupta
description: Obtenga información sobre cómo crear pestañas para un chat de reunión, un panel lateral de reunión y una fase de reunión en una reunión de Microsoft Teams.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: d86f0931cb6338ef331f2afe3a4a5fdb217bb316
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615491"
---
# <a name="build-tabs-for-meeting"></a>Pestañas de compilación para la reunión

Cada equipo tiene una manera diferente de comunicarse y colaborar con las tareas. Para lograr estas tareas diferentes, personalice Teams con aplicaciones para reuniones. Habilite las aplicaciones para las reuniones de Teams y configure las aplicaciones para que estén disponibles en el ámbito de la reunión dentro de su manifiesto de aplicación.

## <a name="tabs-in-teams-meetings"></a>Pestañas en reuniones de Teams

Las pestañas permiten a los participantes de la reunión acceder a los servicios y al contenido de un espacio específico dentro de una reunión. Si no está familiarizado con el desarrollo de pestañas de Microsoft Teams, consulte [Compilación de pestañas para Teams](/microsoftteams/platform/tabs/what-are-tabs).

Antes de crear una pestaña de reunión, es importante obtener información sobre las superficies que están disponibles para dirigirse a la vista de chat de reunión, la vista de detalles de la reunión, la vista del panel lateral de la reunión y la vista de la fase de reunión.

### <a name="meeting-details-view"></a>Vista de detalles de la reunión

1. En el calendario, seleccione una reunión a la que quiera agregar una pestaña.
1. Seleccione la pestaña **Detalles** y seleccione :::image type="icon" source="../assets/icons/add-icon.png" Border = "false":::. Aparece la galería de aplicaciones.

   :::image type="content" source="~/assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="En esta captura de pantalla se muestra la experiencia de la aplicación previa a la reunión en la reunión de Teams.":::

1. En la galería de aplicaciones, seleccione la aplicación que desea agregar y siga los pasos necesarios. La pestaña se agrega a la página de detalles de la reunión.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

En la imagen siguiente se muestra una pestaña agregada a la página de detalles de la reunión en el cliente de escritorio de Teams:

   :::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="En la captura de pantalla se muestran las pestañas de Teams de escritorio en la vista de detalles de la reunión de Teams.":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

En la imagen siguiente se muestra una pestaña agregada a la página de detalles de la reunión en el cliente móvil de Teams:

   :::image type="content" source="../assets/images/mobile-tab.png" alt-text="En la captura de pantalla se muestran las pestañas móviles de Teams en la vista de detalles de la reunión de Teams.":::

---

### <a name="meeting-chat-view"></a>Vista de chat de reunión

1. En el panel de chat de Teams, seleccione la vista de chat de reunión.

1. Seleccione :::image type="icon" source="../assets/icons/add-icon.png" Border = "false"::: y aparecerá la galería de aplicaciones.

1. En la galería de aplicaciones, seleccione la aplicación que desea agregar y siga los pasos necesarios. La pestaña se agrega al chat de reunión.

   :::image type="content" source="../assets/images/apps-in-meetings/meeting-chat-view.png" alt-text="En la captura de pantalla se muestra la vista de chat de reunión en la reunión de Teams.":::

### <a name="meeting-side-panel-view"></a>Vista del panel lateral de la reunión

1. Durante una reunión, puede seleccionar :::image type="icon" source="../assets/icons/add-icon.png" Border = "false"::: **Aplicaciones** en la ventana de reunión de Teams para agregar aplicaciones a la reunión.

   :::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="En esta captura de pantalla se muestra cómo agregar una aplicación en la ventana de reunión de Teams.":::

1. En la galería de aplicaciones, seleccione la aplicación que desea agregar y siga los pasos necesarios. La aplicación se agrega al panel lateral de la reunión.

   :::image type="content" source="../assets/images/side-panel-view.png" alt-text="En esta captura de pantalla se muestra la vista del panel lateral con la lista de aplicaciones.":::

### <a name="meeting-stage-view"></a>Vista de la fase de reunión

1. Después de agregar una pestaña al panel del lado de la reunión, ahora puede optar por participar en el uso compartido global de aplicaciones.

1. Esto da como resultado una pestaña de representación en la fase para cada participante de la reunión.

   :::image type="content" source="../assets/images/meeting-stage-view.png" alt-text="En esta captura de pantalla se muestra la vista de la fase de reunión de la aplicación que ha compartido con la reunión.":::

### <a name="apps-in-channel-meeting"></a>Aplicaciones en la reunión del canal

Una reunión de canal programada pública tiene la misma lista de aplicaciones que su equipo primario. La instalación de una aplicación en una reunión de canal también hace que esté disponible en el equipo primario y viceversa.

Sin embargo, las instancias de tabulación de una reunión de canal son independientes de las pestañas del propio canal. Por ejemplo, supongamos que un canal *de desarrollo* tiene una pestaña *Polly* . Si crea una reunión *standup* en ese canal, esa reunión no tendría una pestaña *Polly* hasta que agregue explícitamente [la pestaña a la reunión](#meeting-details-view).

En las reuniones de canal programadas públicas, después de agregar una pestaña de reunión, puede seleccionar el objeto de reunión en la página de detalles de la reunión para acceder a la pestaña.

:::image type="content" source="~/assets/images/apps-in-meetings/after-a-meeting1.png" alt-text="Después de una reunión":::

> [!NOTE]
> En dispositivos móviles, los usuarios anónimos no pueden acceder a las aplicaciones de las reuniones programadas del canal público.

### <a name="app-manifest-settings-for-tabs-in-meeting"></a>Configuración del manifiesto de la aplicación para pestañas en la reunión

Actualice el [manifiesto de la aplicación](/microsoftteams/platform/resources/schema/manifest-schema) con la propiedad de contexto pertinente para configurar las distintas vistas de pestaña. Las funcionalidades de la aplicación de reuniones se declaran en el manifiesto de la aplicación mediante los ámbitos y las matrices de contexto de la sección configurableTabs.

#### <a name="scope"></a>Ámbito

El ámbito define quién puede acceder a las aplicaciones.

* `groupchat` ámbito hace que la aplicación esté disponible en un ámbito de grupo y permite que la aplicación se agregue en una llamada o reunión (reunión privada programada o reuniones instantáneas).

* `team` ámbito hace que la aplicación esté disponible en un ámbito de equipo y permite que la aplicación se agregue en equipo o canal o en una reunión de canal programada.

#### <a name="context"></a>Contexto

La `context` propiedad determina si la aplicación está disponible en una vista específica después de la instalación y configuración. A continuación se muestran los valores de la propiedad desde la `context` que puede usar todos o algunos de los valores:

|Valor|Descripción|
|---|---|
| **channelTab** | Pestaña en el encabezado de un canal de equipo. |
| **privateChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios, no en el contexto de un equipo o reunión. |
| **meetingChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios para una reunión programada. Puede especificar **meetingChatTab** o **meetingDetailsTab** para asegurarse de que las aplicaciones funcionen en dispositivos móviles. |
| **meetingDetailsTab** | Pestaña en el encabezado de la vista de detalles de la reunión del calendario. Puede especificar **meetingChatTab** o **meetingDetailsTab** para asegurarse de que las aplicaciones funcionen en dispositivos móviles. |
| **meetingSidePanel** | Un panel durante la reunión abierto a través de la barra unificada (barra-U). |
| **meetingStage** | Una aplicación desde la que `meetingSidePanel` se puede compartir a la escena de reunión. No puedes usar esta aplicación en dispositivos móviles ni en clientes de sala de Teams. |

#### <a name="configure-tab-app-for-a-meeting"></a>Configuración de una aplicación de pestaña para una reunión

Las aplicaciones de las reuniones pueden usar los siguientes contextos: `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` y `meetingStage`. Después de que un participante de la reunión instala una aplicación y configura la pestaña en la reunión, todos los demás contextos de destino de la aplicación para la reunión determinada comienzan a representar la pestaña.

El siguiente fragmento de código es un ejemplo de una pestaña configurable que se usa en una aplicación para reuniones de Teams:

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

---

#### <a name="other-examples"></a>Otros ejemplos

El contexto predeterminado de las pestañas (si no se especifica) es:  

```json
"context":[ 
  "channelTab", 
  "privateChatTab", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

Para evitar que una aplicación se muestre en chats de grupos que no sean de reunión, debe establecer el contexto siguiente:

```json
"context":[ 
  "meetingSidePanel", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

Solo para la experiencia del panel lateral en la reunión:  

```json
"context":[ 
  "meetingSidePanel" 
     ] 
```

### <a name="advanced-tab-sdk-apis"></a>API avanzadas del SDK de pestañas

El SDK de cliente de JavaScript de Microsoft Teams es un SDK enriquecido que se usa para crear pestañas mediante JavaScript. Use la versión más reciente de TeamsJS (V.2.0 o posterior) para trabajar en Teams, Office y Outlook. Para obtener más información, vea [SDK de cliente de JavaScript de Teams](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk?tabs=javascript%2Cmanifest-teams-toolkit).

### <a name="frame-context"></a>Contexto de marco

La biblioteca JavaScript de Microsoft Teams expone el frameContext en el que se carga la dirección URL de la pestaña de reunión en la API getContext. Los valores posibles de frameContext son content, task, setting, remove, sidePanel y meetingStage. Esto le permite crear experiencias personalizadas en función de dónde se represente la aplicación. Por ejemplo, mostrar una interfaz de usuario específica centrada en la `meetingStage` colaboración cuando se encuentra en y una interfaz de usuario de preparación de reuniones diferente en la pestaña de chat (`content`). Para obtener más información, consulte [getContext API](/microsoftteams/platform/tabs/how-to/access-teams-context?tabs=teamsjs-v2).

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Aplicación Meeting | Muestra cómo usar la aplicación Generador de token de reunión para solicitar un token. El token se genera secuencialmente para que cada participante tenga las mismas oportunidades que los demás de contribuir en una reunión. El token es útil en situaciones como reuniones de scrum y sesiones de Preguntas y respuestas. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Ejemplo de fase de reunión | Aplicación de ejemplo para mostrar una pestaña en la fase de reunión para la colaboración | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| Panel lateral de la reunión | Aplicación de ejemplo para mostrar cómo agregar una agenda en un panel lateral de la reunión | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|
| Notificación en la reunión | Muestra cómo implementar la notificación en la reunión mediante el bot. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| Firma de documentos en la reunión | Muestra cómo implementar una aplicación de Teams de firma de documentos. Incluye el uso compartido de contenido específico de la aplicación para la fase, el inicio de sesión único de Teams y la vista de fase específica del usuario. | [View](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | ND |

> [!NOTE]
>
> * Las aplicaciones de reunión (panel lateral y fase de reunión) se admiten en el cliente de escritorio de Teams.
> * Las aplicaciones de reunión (panel lateral y fase de reunión) en el cliente web de Teams solo se admiten cuando [la versión preliminar del desarrollador está habilitada](/microsoftteams/platform/resources/dev-preview/developer-preview-intro#enable-developer-preview).

## <a name="step-by-step-guides"></a>Guías paso a paso

* Siga la [guía paso a paso](../sbs-meeting-token-generator.yml) para generar el token de reunión en la reunión de Teams.
* Siga la [guía paso a paso](../sbs-meetings-sidepanel.yml) para generar el panel lateral de la reunión en la reunión de Teams.
* Siga la [guía paso a paso](../sbs-meetings-stage-view.yml) para compartir la vista de la fase de reunión en la reunión de Teams.
* Siga la [guía paso a paso](../sbs-meeting-content-bubble.yml) para generar una notificación en la reunión de Teams.

## <a name="see-also"></a>Vea también

* [Directrices de diseño de notificaciones en la reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
* [Directrices de diseño de la experiencia de la fase de reunión compartida](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Agregar aplicaciones a reuniones a través de Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
