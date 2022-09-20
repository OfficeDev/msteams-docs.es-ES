---
title: Habilitar y configurar las aplicaciones para reuniones de Teams
author: surbhigupta
description: Aprenderá a habilitar y configurar las aplicaciones para reuniones de Teams y diferentes escenarios de reunión, actualice el manifiesto de la aplicación, configure características como, por ejemplo, el cuadro de diálogo en la reunión, la fase de reunión compartida, el panel lateral de la reunión, etc.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: b01155abe9ec421310b169c7a2b50c49e211b4b7
ms.sourcegitcommit: 08bd7f1b9c654b95d3639ca88052c9ca9a8c3f67
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/20/2022
ms.locfileid: "67833711"
---
# <a name="enable-and-configure-apps-for-meetings"></a>Habilitar y configurar las aplicaciones para reuniones

Cada equipo tiene una manera diferente de comunicarse y colaborar con las tareas. Para lograr estas tareas diferentes, personalice Teams con aplicaciones para reuniones. Habilite las aplicaciones para reuniones de Teams y configure las aplicaciones para que estén disponibles en el ámbito de la reunión dentro de su manifiesto de aplicación.

## <a name="prerequisites"></a>Requisitos previos

Con las aplicaciones para reuniones de Teams puede expandir las funcionalidades de las aplicaciones a lo largo del ciclo de vida de la reunión. Antes de trabajar con aplicaciones para reuniones de Teams debe cumplir los siguientes requisitos previos:

* Saber cómo desarrollar aplicaciones de Teams. Para obtener más información sobre cómo desarrollar una aplicación de Teams, consulte [desarrollo de aplicaciones de Teams](../overview.md).

* Usa la aplicación que admite pestañas configurables en el ámbito de grupo o de grupo. Para obtener más información, consulte [Ámbitos](../resources/schema/manifest-schema.md#configurabletabs) y [compilación de la primera aplicación de pestaña](../build-your-first-app/build-channel-tab.md).

* Cumpla con las [directrices generales de diseño de pestañas de Teams](../tabs/design/tabs.md) para escenarios previos y posteriores a la reunión. Para obtener experiencias durante las reuniones, consulte las [directrices de diseño de la pestaña en la reunión](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) y [las directrices de diseño del cuadro de diálogo en la reunión](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).

* Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión. Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras fases a lo largo del ciclo de vida de la reunión. Para ver el cuadro de diálogo en la reunión, consulte el parámetro `completionBotId` en [la carga de notificaciones en la reunión](API-references.md#send-an-in-meeting-notification).

## <a name="enable-your-app-for-teams-meetings"></a>Habilitación de la aplicación para reuniones de Teams

Para habilitar la aplicación para reuniones de Teams, actualice el manifiesto de la aplicación y use las propiedades de contexto para determinar dónde debe aparecer la aplicación.

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Las funcionalidades de la aplicación de reuniones se declaran en el manifiesto de la aplicación mediante las matrices `configurableTabs`, `scopes` y `context`. El ámbito define quién puede acceder y el contexto define dónde está disponible la aplicación.

> [!NOTE]
>
> * Las aplicaciones en reuniones requieren `groupchat` o `team` ámbito. El `team` ámbito funciona para pestañas en canales o reuniones de canales.
> * Para admitir la adición de pestañas en reuniones de canal programadas, especifique el ámbito del **equipo** en **la sección ámbitos** del manifiesto de la aplicación. Sin el ámbito del **equipo** , la aplicación no aparecería en el control flotante para las reuniones de canal.
> * Las aplicaciones de las reuniones pueden usar los siguientes contextos: `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` y `meetingStage`.

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

### <a name="context-property"></a>Context (propiedad)

La propiedad `context` determina lo que se debe mostrar cuando un usuario invoca una aplicación en una reunión en función del lugar en el que el usuario invoca la aplicación. Las propiedades de pestaña `context` y `scopes` permiten determinar dónde debe aparecer la aplicación. Las pestañas del ámbito `team` o `groupchat` pueden tener más de un contexto.

Admita el ámbito `groupchat` para habilitar la aplicación en chats previos y posteriores a la reunión. Con la experiencia de la aplicación previa a la reunión, se pueden buscar y agregar aplicaciones de reunión y hacer tareas previas a la reunión. Con la experiencia de la aplicación posterior a la reunión, los usuarios pueden ver los resultados de la reunión, como son los resultados de la encuesta de sondeo o costo.

 A continuación se muestran los valores de la propiedad `context` desde la que puede usar todos o algunos de los valores:

|Valor|Descripción|
|---|---|
| **channelTab** | Pestaña en el encabezado de un canal de equipo. |
| **privateChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios, no en el contexto de un equipo o reunión. |
| **meetingChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios para una reunión programada. Puede especificar **meetingChatTab** o **meetingDetailsTab** para asegurarse de que las aplicaciones funcionen en dispositivos móviles. |
| **meetingDetailsTab** | Pestaña en el encabezado de la vista de detalles de la reunión del calendario. Puede especificar **meetingChatTab** o **meetingDetailsTab** para asegurarse de que las aplicaciones funcionen en dispositivos móviles. |
| **meetingSidePanel** | Un panel durante la reunión abierto a través de la barra unificada (barra-U). |
| **meetingStage** | Una aplicación desde la que `meetingSidePanel` se puede compartir a la escena de reunión. No puedes usar esta aplicación en dispositivos móviles ni en clientes de sala de Teams. |

Después de habilitar la aplicación para reuniones de Teams, debe configurarla antes de una reunión, durante una reunión y después de una reunión.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configuración de la aplicación para escenarios de reunión

Las reuniones de Teams proporcionan una experiencia de colaboración para su organización. Configure la aplicación para diferentes escenarios de reunión y mejore la experiencia de la reunión. Ahora puede identificar qué acciones se pueden realizar en los siguientes escenarios de reunión:

* [Antes de una reunión](#before-a-meeting)
* [Durante una reunión](#during-a-meeting)
* [Después de una reunión](#after-a-meeting)

### <a name="before-a-meeting"></a>Antes de una reunión

Antes de una reunión, los usuarios pueden agregar pestañas, bots y extensiones de mensaje. Los usuarios con roles de organizador y moderador pueden agregar pestañas a una reunión.

Para agregar una pestaña a una reunión:

1. En el calendario, seleccione una reunión a la que quiera agregar una pestaña.
1. Seleccione la pestaña **Detalles** y seleccione <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting1.png" alt="Pre-meeting experience" width="900"/>

1. En la galería de pestañas que aparece, seleccione la aplicación que desea agregar y siga los pasos necesarios. La aplicación se instala como una pestaña.

Para agregar una extensión de mensaje a una reunión:

1. Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; ubicados en el área de redacción del mensaje en el chat.
1. Seleccione la aplicación que desea agregar y siga los pasos necesarios. La aplicación se instala como una extensión de mensaje.

Para agregar un bot a una reunión:

En un chat de reunión, escriba la clave **@** y seleccione **Obtener bots**.

> [!NOTE]
>
> * El cuadro de diálogo en la reunión muestra un cuadro de diálogo en una reunión y publica simultáneamente una tarjeta adaptable en el chat de reunión al que los usuarios pueden acceder. La tarjeta adaptable del chat de reunión ayuda a los usuarios mientras asisten a la reunión o si la aplicación Teams está minimizada.
> * La identidad del usuario debe confirmarse mediante [el inicio de sesión único de Tabs](../tabs/how-to/authentication/tab-sso-overview.md). Después de la autenticación, la aplicación puede recuperar el rol de usuario mediante la API `GetParticipant`.
> * En función del rol de usuario, la aplicación tiene la capacidad de proporcionar experiencias específicas para cada rol. Por ejemplo, una aplicación de sondeo solo permite a los organizadores y moderadores crear un nuevo sondeo.
> * Las asignaciones de roles se pueden cambiar mientras una reunión está en curso. Para obtener más información, consulte [roles en una reunión de Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### <a name="during-a-meeting"></a>Durante una reunión

Durante una reunión, puede usar el `meetingSidePanel` o la notificación durante la reunión para crear experiencias únicas para las aplicaciones.

#### <a name="meeting-sidepanel"></a>Panel lateral de reunión

El `meetingSidePanel` permite personalizar experiencias en una reunión que permiten a los organizadores y moderadores tener un conjunto diferente de vistas y acciones. En el manifiesto de la aplicación debe agregar `meetingSidePanel` a la matriz de contexto. En la reunión y en todos los escenarios, la aplicación se representa en una pestaña en la reunión que tiene un ancho de 320 píxeles. Para obtener más información, consulte la [interfaz de FrameInfo](/javascript/api/@microsoft/teams-js/frameinfo) (conocida como `FrameContext` antes de TeamsJS v.2.0.0).

Puede [usar el contexto de usuario para redirigir las solicitudes](../tabs/how-to/access-teams-context.md#user-context). Para obtener más información, vea [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md). El flujo de autenticación de las pestañas es similar al flujo de autenticación de los sitios web. Las pestañas pueden usar OAuth 2.0 directamente. Para obtener más información, consulte [Plataforma de identidad de Microsoft y flujo del código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

La extensión de mensaje funciona según lo esperado cuando un usuario está en una vista en la reunión. El usuario puede publicar tarjetas de extensión de mensaje de redacción. AppName en la reunión es una información sobre herramientas que indica el nombre de la aplicación en la barra U de la reunión.

> [!NOTE]
> Use la versión 1.7.0 o posterior de [SDK de Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), ya que las versiones anteriores no admiten el panel lateral.

#### <a name="in-meeting-notification"></a>Notificación en la reunión

La notificación en la reunión se usa para interactuar con los participantes durante la reunión y recopilar información o comentarios durante la reunión. Use una [carga de notificación en la reunión](API-references.md#send-an-in-meeting-notification) para desencadenar una notificación en la reunión. Como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.

La notificación en la reunión no debe usar el módulo de tareas. El módulo de tareas no se invoca en un chat de reunión. Se usa una dirección URL de recurso externo para mostrar la notificación en la reunión. Puede usar el método `submitTask` para enviar datos en un chat de reunión.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="En el ejemplo se muestra cómo puede usar un cuadro de diálogo en la reunión.":::

Además, puede agregar la imagen de visualización de Teams y la tarjeta de contactos del usuario a la notificación de la reunión basada en el `onBehalfOf`token con el MRI del usuario y el nombre para mostrar pasado en la carga útil. A continuación se muestra una carga útil de ejemplo:

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="En el ejemplo se muestra cómo Teams muestra la imagen y la tarjeta de personas con el cuadro de diálogo en la reunión." border="true":::

#### <a name="shared-meeting-stage"></a>Escena de reunión compartida

La fase de reunión compartida permite a los participantes de la reunión interactuar con el contenido de la aplicación y colaborar en él en tiempo real. Puede compartir sus aplicaciones en la fase de reunión colaborativa de las siguientes maneras:

* [Comparta toda la aplicación en fase](#share-entire-app-to-stage) mediante el botón compartir en fase en el cliente de Teams.
* [Comparta partes específicas de la aplicación en fase](#share-specific-parts-of-the-app-to-stage) mediante API en el SDK de cliente de Teams.

##### <a name="share-entire-app-to-stage"></a>Compartir toda la aplicación en fase

Los participantes pueden compartir toda la aplicación en la fase de reunión de colaboración mediante el botón compartir en fase desde el panel lateral de la aplicación.

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

Para compartir toda la aplicación en fase, debe configurar `meetingStage` y `meetingSidePanel` como contextos de marco en el manifiesto de la aplicación. Por ejemplo:

```json
"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

Para obtener más información, vea [manifiesto de aplicación](../resources/schema/manifest-schema-dev-preview.md#configurabletabs).

##### <a name="share-specific-parts-of-the-app-to-stage"></a>Compartir partes específicas de la aplicación en fase

Los participantes pueden compartir partes específicas de la aplicación en la fase de reunión de colaboración mediante las API de compartir en fase. Las API están disponibles en el SDK de cliente de Teams y se invocan desde el panel lateral de la aplicación.

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

Para compartir partes específicas de la aplicación en fase debe invocar las API relacionadas en la biblioteca del SDK de cliente de Teams. Para obtener más información, vea [referencia de API](API-references.md).

> [!NOTE]
>
> * Para compartir partes específicas de la aplicación en fase use la versión de manifiesto 1.12 o posterior de Teams.
> * Puede compartir partes específicas de la aplicación en la fase de reunión solo en los clientes de escritorio de Teams. Los usuarios móviles pueden compartir partes específicas de la aplicación para almacenar provisionalmente el uso del [recurso compartido en la API de fase](API-references.md#share-app-content-to-stage-api).

### <a name="after-a-meeting"></a>Después de una reunión

Las configuraciones de después y [antes de las reuniones](#before-a-meeting) son las mismas.

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Aplicación Meeting | Muestra cómo usar la aplicación Generador de token de reunión para solicitar un token. El token se genera secuencialmente para que cada participante tenga las mismas oportunidades que los demás de contribuir en una reunión. El token es útil en situaciones como reuniones de scrum y sesiones de Preguntas y respuestas. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|Ejemplo de fase de reunión | Aplicación de ejemplo para mostrar una pestaña en la fase de reunión para la colaboración | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|Panel lateral de la reunión | Aplicación de ejemplo para mostrar cómo agregar una agenda en un panel lateral de la reunión | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>Guías paso a paso

* Siga la [guía paso a paso](../sbs-meeting-token-generator.yml) para generar el token de reunión en la reunión de Teams.
* Siga la [guía paso a paso](../sbs-meetings-sidepanel.yml) para generar el panel lateral de la reunión en la reunión de Teams.
* Siga la [guía paso a paso](../sbs-meetings-stage-view.yml) para compartir la vista de la fase de reunión en la reunión de Teams.
* Siga la [guía paso a paso](../sbs-meeting-content-bubble.yml) para generar la burbuja de contenido de la reunión en la reunión de Teams.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Referencias API de aplicaciones de reuniones](API-references.md)

## <a name="see-also"></a>Consulte también

* [Directrices de diseño del cuadro de diálogo en la reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
* [Directrices de diseño de la experiencia de la fase de reunión compartida](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Agregar aplicaciones a reuniones a través de Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
