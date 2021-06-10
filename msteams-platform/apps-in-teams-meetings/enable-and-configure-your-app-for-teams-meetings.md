---
title: Habilitar y configurar las aplicaciones para Teams reuniones
author: laujan
description: Habilitar y configurar las aplicaciones para Teams reuniones
ms.topic: conceptual
ms.openlocfilehash: 3484e82f3f51a9a92da6588234744c42a86b5730
ms.sourcegitcommit: 1cc1516e71441f6f3f82b35868e21ba9933333cd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52651736"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>Habilitar y configurar las aplicaciones para Teams reuniones

Cada equipo tiene una forma diferente de comunicar y colaborar tareas. Puedes lograr estas distintas tareas personalizando Teams aplicaciones para reuniones. Para personalizar y lograr diferentes tareas, debes habilitar las aplicaciones para reuniones Teams y configurar las aplicaciones para que estén disponibles en el ámbito de la reunión dentro del manifiesto de la aplicación.

## <a name="enable-your-app-for-teams-meetings"></a>Habilitar la aplicación para Teams reuniones

Para habilitar la aplicación para Teams reuniones, debes actualizar el manifiesto de la aplicación y usar las propiedades de contexto para determinar dónde debe aparecer la aplicación.

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Las funcionalidades de la aplicación reuniones se declaran en el manifiesto de la aplicación mediante `configurableTabs` las `scopes` matrices , `context` y. El ámbito define a quién y el contexto define dónde está disponible la aplicación.

> [!NOTE]
> * Intente actualizar el manifiesto de la aplicación con el [esquema de manifiesto](../resources/schema/manifest-schema-dev-preview.md).
> * Las aplicaciones de las reuniones requieren ámbito groupchat. El ámbito de equipo solo funciona para pestañas en canales.

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

> [!NOTE]
> `meetingStage` actualmente solo está disponible en [versión preliminar del](../resources/dev-preview/developer-preview-intro.md) desarrollador.

### <a name="context-property"></a>Context (propiedad)

La propiedad determina lo que debe mostrarse cuando un usuario invoca una aplicación en una reunión en función del lugar en el que el usuario `context` invoca la aplicación. La pestaña y las propiedades te permiten determinar dónde debe aparecer `context` `scopes` la aplicación. Las pestañas del `team` ámbito or pueden tener más de un `groupchat` contexto. Estos son los valores de la propiedad desde `context` la que puede usar todos o algunos de los valores:

|Valor|Descripción|
|---|---|
| **channelTab** | Pestaña en el encabezado de un canal de grupo. |
| **privateChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios, no en el contexto de un equipo o reunión. |
| **meetingChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada. |
| **meetingDetailsTab** | Pestaña en el encabezado de la vista de detalles de la reunión del calendario. |
| **meetingSidePanel** | Un panel en la reunión abierto a través de la barra unificada (barra U). |
| **meetingStage** | Una aplicación de meetingSidePanel se puede compartir en la fase de reunión. |

> [!NOTE]
> `Context` actualmente no se admite en clientes móviles.

Después de habilitar la aplicación para Teams reuniones, debes configurar la aplicación antes de una reunión, durante una reunión y después de una reunión.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurar la aplicación para escenarios de reunión

> [!NOTE]
> * Para que la aplicación esté visible en la galería de pestañas, debe admitir pestañas configurables y el ámbito de chat de grupo.
> * Los clientes móviles solo admiten pestañas en fases de reunión previas y posteriores.
> * Las experiencias en la reunión que es el cuadro de diálogo y la pestaña en la reunión actualmente no se admiten en clientes móviles. Para obtener más información, consulta [instrucciones para pestañas en el móvil](../tabs/design/tabs-mobile.md) al crear las pestañas para móviles.

Teams reuniones proporciona una experiencia de colaboración única para su organización. Proporciona la oportunidad de configurar la aplicación para diferentes escenarios de reunión. Puedes configurar las aplicaciones para mejorar la experiencia de la reunión en función del rol de participante o el tipo de usuario. Ahora puede identificar qué acciones se pueden realizar en los siguientes escenarios de reunión:
* [Reunión previa](#pre-meeting)
* [En reunión](#in-meeting)
* [Posterior a la reunión](#post-meeting)

### <a name="pre-meeting"></a>Reunión previa

Antes de una reunión, los usuarios pueden agregar pestañas, bots y extensiones de mensajería. Los usuarios con roles de organizador y moderador pueden agregar pestañas a una reunión.

**Para agregar una pestaña a una reunión**

1. En el calendario, seleccione una reunión a la que desee agregar una pestaña.
1. Seleccione la **pestaña Detalles** y seleccione <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    ![Experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

1. En la galería de pestañas que aparece, selecciona la aplicación que quieres agregar y sigue los pasos según sea necesario. La aplicación se instala como una pestaña.

    > [!NOTE]
    > Actualmente, en la pestaña reuniones, no se admite la obtención de detalles de la reunión y la información de los participantes.

**Para agregar una extensión de mensajería a una reunión**

1. Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; ubicados en el área del mensaje de redacción en el chat.
1. Selecciona la aplicación que quieras agregar y sigue los pasos según sea necesario. La aplicación se instala como una extensión de mensajería.

**Para agregar un bot a una reunión**

En un chat de reunión, escriba la **@** clave y seleccione Obtener **bots**.

> [!NOTE]
> * La identidad del usuario debe confirmarse con [tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md). Después de la autenticación, la aplicación puede recuperar el rol de usuario mediante la `GetParticipant` API.
> * En función del rol de usuario, la aplicación tiene la capacidad de proporcionar experiencias específicas del rol. Por ejemplo, una aplicación de sondeo solo permite a los organizadores y presentadores crear un nuevo sondeo.
> * Las asignaciones de roles se pueden cambiar mientras se está en curso una reunión. Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### <a name="in-meeting"></a>En reunión

Durante una reunión, puedes usar el meetingSidePanel o el cuadro de diálogo en la reunión para crear experiencias únicas para tus aplicaciones.

#### <a name="meetingsidepanel"></a>meetingSidePanel

Con meetingSidePanel, puede personalizar las experiencias de una reunión que permitan a los organizadores y presentadores tener un conjunto diferente de vistas y acciones. En el manifiesto de la aplicación, debes agregar meetingSidePanel a la matriz de contexto. En la reunión y en todos los escenarios, la aplicación se representa en una pestaña en la reunión que tiene 320 píxeles de ancho. Para obtener más información, vea [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).

Para usar la `userContext` API para enrutar las solicitudes en consecuencia, [vea Teams SDK](../tabs/how-to/access-teams-context.md#user-context). Para obtener más información, [vea Teams de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md). El flujo de autenticación para pestañas es muy similar al flujo de autenticación para sitios web. Por lo tanto, las pestañas pueden usar OAuth 2.0 directamente. Para obtener más información, vea Plataforma de identidad de Microsoft y flujo de código de autorización [de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

La extensión de mensajería funciona según lo esperado cuando un usuario está en una vista en la reunión y el usuario puede publicar tarjetas de extensión de mensajes de redacción. AppName en la reunión es una información sobre herramientas que indica el nombre de la aplicación en la barra U de la reunión.

> [!NOTE]
> Use la versión 1.7.0 o posterior de [Teams SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)ya que las versiones anteriores no admiten el panel lateral.

#### <a name="in-meeting-dialog-box"></a>Cuadro de diálogo En la reunión

El cuadro de diálogo en la reunión se puede usar para interactuar con los participantes durante la reunión y recopilar información o comentarios durante la reunión. Use la API para indicar que se debe desencadenar [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) una notificación de burbuja. Como parte de la carga de solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.

El cuadro de diálogo en la reunión no debe usar el módulo de tareas. El módulo de tareas no se invoca en un chat de reunión. Se usa una dirección URL de recurso externo para mostrar una burbuja de contenido en una reunión. Puede usar el método `submitTask` para enviar datos en un chat de reunión.

> [!NOTE]
> * Debe invocar la [función submitTask() para](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) descartarla automáticamente después de que un usuario realiza una acción en la vista web. Este es un requisito para el envío de la aplicación. Para obtener más información, [vea Teams módulo de tareas del SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
> * Si quieres que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los metadatos de solicitud del objeto, no en `from.id` `from` los `from.aadObjectId` metadatos de la solicitud. `from.id`es el identificador de usuario `from.aadObjectId` y es el Azure Active Directory (AAD) del usuario. Para obtener más información, vea [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) y create and send the task [module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

#### <a name="share-to-stage"></a>Compartir en fase

> [!NOTE]
> * Esta funcionalidad está disponible actualmente solo en [la versión preliminar del](../resources/dev-preview/developer-preview-intro.md) desarrollador.
> * Para usar esta característica, la aplicación debe admitir una reunión en la reuniónSidePanel.

Esta funcionalidad ofrece a los desarrolladores la capacidad de compartir una aplicación en la fase de reunión. Al habilitar el recurso compartido en la fase de reunión, los participantes de la reunión pueden colaborar en tiempo real.

El contexto necesario está `meetingStage` en el manifiesto de la aplicación. Un requisito previo para ello es tener el `meetingSidePanel` contexto. Esto habilita **Compartir** en el meetingSidePanel.

![Compartir en fase durante la experiencia de reunión](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

El cambio de manifiesto necesario para habilitar esta funcionalidad es el siguiente:

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

### <a name="post-meeting"></a>Posterior a la reunión

Las configuraciones posteriores a la reunión [y previas](#pre-meeting) a la reunión son las mismas.

## <a name="code-sample"></a>Ejemplo de código

|Nombre de ejemplo | Descripción | Muestra |
|----------------|-----------------|--------------|----------------|-----------|
| Aplicación de reunión | Muestra cómo usar la aplicación Generador de tokens de reunión para solicitar un token, que se genera secuencialmente para que cada participante tenga una oportunidad equitativa de interactuar. Esto puede ser útil en situaciones como reuniones de scrum, preguntas&sesiones A, y así sucesivamente. | [View](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a>Consulte también

* [Directrices de diseño de cuadros de diálogo en la reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
