---
title: Habilitar y configurar las aplicaciones para Teams reuniones
author: surbhigupta
description: Habilitar y configurar las aplicaciones para reuniones de Teams y diferentes escenarios de reunión, actualizar el manifiesto de la aplicación, configurar características, como, cuadro de diálogo en la reunión, fase de reunión compartida, panel lateral de reunión, etc.
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 0211cb1458b13a0727fce9915d1a50d227ed1a53
ms.sourcegitcommit: ca902f505a125641c379a917ee745ab418bd1ce6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/14/2022
ms.locfileid: "63464362"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>Habilitar y configurar las aplicaciones para Teams reuniones

Cada equipo tiene una forma diferente de comunicar y colaborar tareas. Para lograr estas diferentes tareas, personalice Teams con aplicaciones para reuniones. Habilita las aplicaciones para Teams reuniones y configura las aplicaciones para que estén disponibles en el ámbito de la reunión dentro del manifiesto de la aplicación.

## <a name="prerequisites"></a>Requisitos previos

Con aplicaciones para Teams reuniones, puedes expandir las capacidades de tus aplicaciones en todo el ciclo de vida de la reunión. Antes de trabajar con aplicaciones para Teams reuniones, debes cumplir los siguientes requisitos previos:

* Sepa cómo desarrollar Teams aplicaciones. Para obtener más información sobre cómo desarrollar Teams aplicación, consulta [Teams desarrollo de aplicaciones.](../overview.md)

* Usa la aplicación que admite pestañas configurables en el ámbito groupchat. Para obtener más información, vea [ámbito de chat de grupo](../resources/schema/manifest-schema.md#configurabletabs) [y cree una pestaña de grupo](../build-your-first-app/build-channel-tab.md).

* Siga las directrices [generales Teams de diseño de pestañas](../tabs/design/tabs.md) para escenarios previos y posteriores a la reunión. Para obtener experiencias durante las reuniones, consulte las directrices de diseño de [pestañas](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) en la reunión y las directrices de diseño de [cuadros de diálogo en la reunión](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).

* Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión. Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión. Para el cuadro de diálogo en la reunión, vea `completionBotId` el parámetro en [la carga de notificación en la reunión](API-references.md#send-an-in-meeting-notification).

## <a name="enable-your-app-for-teams-meetings"></a>Habilitar la aplicación para Teams reuniones

Para habilitar la aplicación para Teams reuniones, actualiza el manifiesto de la aplicación y usa las propiedades de contexto para determinar dónde debe aparecer la aplicación.

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Las funcionalidades de la aplicación reuniones se declaran en el manifiesto de la aplicación mediante `configurableTabs`las matrices , `scopes`y `context` . El ámbito define quién puede tener acceso y el contexto define dónde está disponible la aplicación.

> [!NOTE]
>
> * Debes actualizar el manifiesto de la aplicación con el [esquema de manifiesto](../resources/schema/manifest-schema-dev-preview.md).
> * Las aplicaciones de las reuniones requieren ámbito `groupchat` . El `team` ámbito solo funciona para pestañas en canales.

El manifiesto de la aplicación debe incluir el siguiente fragmento de código:

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

La `context` propiedad determina lo que debe mostrarse cuando un usuario invoca una aplicación en una reunión en función del lugar en el que el usuario invoca la aplicación. La pestaña `context` y las `scopes` propiedades te permiten determinar dónde debe aparecer la aplicación. Las pestañas del `team` ámbito or `groupchat` pueden tener más de un contexto.

Admite el `groupchat` ámbito para habilitar la aplicación en chats previos y posteriores a la reunión. Con la experiencia de la aplicación antes de la reunión, puedes encontrar y agregar aplicaciones de reunión y realizar las tareas previas a la reunión. Con la experiencia de la aplicación posterior a la reunión, puedes ver los resultados de la reunión, como los resultados de la encuesta o la tarifa.

 Estos son los valores de la `context` propiedad desde la que puede usar todos o algunos de los valores:

|Valor|Descripción|
|---|---|
| **channelTab** | Pestaña en el encabezado de un canal de grupo. |
| **privateChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios, no en el contexto de un equipo o reunión. |
| **meetingChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios para una reunión programada. Puede especificar **meetingChatTab** o **meetingDetailsTab** para asegurarse de que las aplicaciones funcionan en dispositivos móviles. |
| **meetingDetailsTab** | Pestaña en el encabezado de la vista de detalles de la reunión del calendario. Puede especificar **meetingChatTab** o **meetingDetailsTab** para asegurarse de que las aplicaciones funcionan en dispositivos móviles. |
| **meetingSidePanel** | Un panel en la reunión abierto a través de la barra unificada (barra U). |
| **meetingStage** | Una aplicación de la puede `meetingSidePanel` compartirse en la fase de reunión. No puedes usar esta aplicación en dispositivos móviles ni en clientes de sala de Teams. |

Después de habilitar la aplicación para Teams reuniones, debes configurar la aplicación antes de una reunión, durante una reunión y después de una reunión.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurar la aplicación para escenarios de reunión

Teams reuniones proporcionan una experiencia de colaboración para su organización. Configura la aplicación para diferentes escenarios de reunión y para mejorar la experiencia de la reunión. Ahora puede identificar qué acciones se pueden realizar en los siguientes escenarios de reunión:

* [Antes de una reunión](#before-a-meeting)
* [Durante una reunión](#during-a-meeting)
* [Después de una reunión](#after-a-meeting)

### <a name="before-a-meeting"></a>Antes de una reunión

Antes de una reunión, los usuarios pueden agregar pestañas, bots y extensiones de mensajería. Los usuarios con roles de organizador y moderador pueden agregar pestañas a una reunión.

Para agregar una pestaña a una reunión:

1. En el calendario, seleccione una reunión a la que desee agregar una pestaña.
1. Seleccione la **pestaña Detalles** y seleccione <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting.png" alt="Pre-meeting experience" width="900"/>

1. En la galería de pestañas que aparece, selecciona la aplicación que quieres agregar y sigue los pasos según sea necesario. La aplicación se instala como una pestaña.

Para agregar una extensión de mensajería a una reunión:

1. Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; ubicados en el área del mensaje de redacción en el chat.
1. Selecciona la aplicación que quieras agregar y sigue los pasos según sea necesario. La aplicación se instala como una extensión de mensajería.

Para agregar un bot a una reunión:

En un chat de reunión, escriba la clave **@** y seleccione **Obtener bots**.

> [!NOTE]
>
> * La burbuja de contenido publica una tarjeta adaptable o una tarjeta simultáneamente en el chat de reunión al que pueden acceder los usuarios. Esto ayuda a los usuarios cuando se minimiza la reunión o Teams aplicación.
> * La identidad del usuario debe confirmarse con [SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md). Después de la autenticación, la aplicación puede recuperar el rol de usuario mediante la `GetParticipant` API.
> * En función del rol de usuario, la aplicación tiene la capacidad de proporcionar experiencias específicas del rol. Por ejemplo, una aplicación de sondeo solo permite a los organizadores y presentadores crear un nuevo sondeo.
> * Las asignaciones de roles se pueden cambiar mientras se está en curso una reunión. Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### <a name="during-a-meeting"></a>Durante una reunión

Durante una reunión, puedes usar la `meetingSidePanel` notificación o en la reunión para crear experiencias únicas para tus aplicaciones.

#### <a name="meeting-sidepanel"></a>Meeting SidePanel

Permite `meetingSidePanel` personalizar experiencias en una reunión que permiten a los organizadores y presentadores tener un conjunto diferente de vistas y acciones. En el manifiesto de la aplicación, debes agregar a `meetingSidePanel` la matriz de contexto. En la reunión y en todos los escenarios, la aplicación se representa en una pestaña en la reunión que tiene 320 píxeles de ancho. Para obtener más información, vea [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).

Para usar la `userContext` API para enrutar solicitudes, [consulte Teams SDK](../tabs/how-to/access-teams-context.md#user-context). Para obtener más información, [vea Teams de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md). El flujo de autenticación de las pestañas es similar al flujo de autenticación de los sitios web. Por lo tanto, las pestañas pueden usar OAuth 2.0 directamente. Para obtener más información, [vea Plataforma de identidad de Microsoft y flujo de código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

La extensión de mensajería funciona según lo esperado cuando un usuario está en una vista en la reunión. El usuario puede publicar tarjetas de extensión de mensaje de redacción. AppName en la reunión es una información sobre herramientas que indica el nombre de la aplicación en la barra U de la reunión.

> [!NOTE]
> Use la versión 1.7.0 o posterior de [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), ya que las versiones anteriores no admiten el panel lateral.

#### <a name="in-meeting-notification"></a>Notificación en la reunión

La notificación en la reunión se usa para interactuar con los participantes durante la reunión y recopilar información o comentarios durante la reunión. Use una [carga de notificación en la](API-references.md#send-an-in-meeting-notification) reunión para desencadenar una notificación en la reunión. Como parte de la carga de solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.

La notificación en reunión no debe usar el módulo de tareas. El módulo de tareas no se invoca en un chat de reunión. Se usa una dirección URL de recurso externo para mostrar la notificación en la reunión. Puede usar el método para `submitTask` enviar datos en un chat de reunión.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="En el ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión." border="true":::

#### <a name="shared-meeting-stage"></a>Escena de reunión compartida

La fase de reunión compartida permite a los participantes de la reunión interactuar y colaborar en el contenido de la aplicación en tiempo real. Puedes compartir tus aplicaciones en la fase de reunión de colaboración de las siguientes maneras:

* [Compartir toda la aplicación en fase](#share-entire-app-to-stage) mediante el botón compartir a fase en Teams cliente.
* [Compartir partes específicas de la aplicación para faser](#share-specific-parts-of-the-app-to-stage) el uso de API en el SDK Teams cliente.

##### <a name="share-entire-app-to-stage"></a>Compartir toda la aplicación en fase

Los participantes pueden compartir toda la aplicación en la fase de reunión de colaboración con el botón compartir a fase desde el panel lateral de la aplicación.

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

Para compartir toda la aplicación en fase, en el manifiesto de la aplicación debes configurar `meetingStage` `meetingSidePanel` y como contextos de marco. Por ejemplo:

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

Para obtener más información, consulta [manifiesto de la aplicación](../resources/schema/manifest-schema-dev-preview.md#configurabletabs).

##### <a name="share-specific-parts-of-the-app-to-stage"></a>Compartir partes específicas de la aplicación en fase

Los participantes pueden compartir partes específicas de la aplicación a la fase de reunión de colaboración mediante el uso del recurso compartido para configurar las API. Las API están disponibles en el SDK Teams cliente y se invocan desde el panel del lado de la aplicación.

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

Para compartir partes específicas de la aplicación en fase, debes invocar las API relacionadas en la Teams SDK de cliente. Para obtener más información, vea [Referencia de API](API-references.md).

Si quieres que la aplicación admita usuarios anónimos, `from.id` `from` la carga inicial de la solicitud de invocación debe basarse en los metadatos de la solicitud en el objeto, no en los metadatos `from.aadObjectId` de la solicitud. `from.id`es el identificador de usuario y `from.aadObjectId` es el Azure AD del usuario. Para obtener más información, vea [usar módulos de tareas en pestañas](../task-modules-and-cards/task-modules/task-modules-tabs.md) [y crear y enviar el módulo de tareas](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### <a name="after-a-meeting"></a>Después de una reunión

Las configuraciones de las reuniones después [y antes](#before-a-meeting) son las mismas.

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Aplicación de reunión | Muestra cómo usar la aplicación Generador de tokens de reunión para solicitar un token. El token se genera secuencialmente para que cada participante tenga una oportunidad equitativa de contribuir en una reunión. El token es útil en situaciones como reuniones de scrum y preguntas&sesiones A. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|Ejemplo de fase de reunión | Aplicación de ejemplo para mostrar una pestaña en la fase de reunión para la colaboración | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|Panel lateral de la reunión | Aplicación de ejemplo para mostrar cómo agregar agenda en un panel del lado de la reunión | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>Guías paso a paso

* Siga la [guía paso a paso para](../sbs-meeting-token-generator.yml) generar token de reunión en su Teams reunión.
* Siga la [guía paso a paso para](../sbs-meetings-sidepanel.yml) generar un panel lateral de reunión en su Teams reunión.
* Siga la [guía paso a paso para](../sbs-meetings-stage-view.yml) generar una vista de fase de reunión en su Teams reunión.
* Siga la [guía paso a paso para](../sbs-meeting-content-bubble.yml) generar una burbuja de contenido de reunión en su Teams reunión.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Referencias API de aplicaciones de reuniones](API-references.md)

## <a name="see-also"></a>Vea también

* [Directrices de diseño de cuadros de diálogo en la reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
* [Directrices de diseño de la experiencia de fase de reunión compartida](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Agregar aplicaciones a reuniones a través de Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
