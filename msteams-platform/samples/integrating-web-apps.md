---
author: heath-hamilton
description: Procedimientos recomendados o consideraciones para integrar aplicaciones web existentes con Microsoft Teams
ms.author: surbhigupta
ms.date: 08/26/2020
ms.localizationpriority: high
ms.topic: conceptual
title: Consideraciones para la integración de Teams
ms.openlocfilehash: 2e1d749a34d0dec2a38e84e57aa6147c791264c1
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111664"
---
# <a name="considerations-for-teams-integration"></a>Consideraciones para la integración de Teams

Puede hacer que las aplicaciones web se adecúen a las características sociales y colaborativas de Teams integrándolas correctamente con Teams.
  
Los distintos tipos de aplicaciones que puede integrar con Teams son los siguientes:

* **Aplicaciones independientes**: una aplicación independiente es una aplicación de una sola página o de gran tamaño y compleja. El usuario puede usar algunos aspectos de él en Teams.
* **Aplicaciones de colaboración**: una aplicación ya creada para las características sociales y colaborativas inherentes a Teams.
* **SharePoint**: una página de SharePoint que quiere que aparezca en Teams.

Puede asignar y seguir las directrices adecuadas que se aplican a su caso de integración.
En este documento se proporciona información general sobre las funcionalidades de Teams, los requisitos de punto de recurso compartido para el almacenamiento de archivos y datos, los requisitos de API, la autenticación y la vinculación en profundidad de la aplicación con Teams.

## <a name="get-to-know-teams-platform-capabilities"></a>Familiarizarse con las funcionalidades de la plataforma Teams

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

La aplicación de Teams debe incluir características de colaboración necesarias y que son de esperar. Para trabajar con la integración de aplicaciones, es importante familiarizarse con la terminología de desarrollo de Teams.

|Características comunes de la aplicación   |Funcionalidades de la plataforma de Teams   |
|----------|-----------|
|Página web integrada, página principal o vista web  |[Pestañas](../tabs/what-are-tabs.md)  |
|Uso compartido de accesos directos y extensiones  |[Extensiones de mensajes](../messaging-extensions/what-are-messaging-extensions.md)  |
|Accesos directos y extensiones de acción  |[Extensiones de mensajes](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots |[Bots](../bots/what-are-bots.md) |
|Notificaciones de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrantes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Conectores de Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Servicios externos de mensajes  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks salientes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modales  |[Módulos de tareas](../task-modules-and-cards/what-are-task-modules.md)  |
|Tarjetas enriquecidas con contenido  |[Tarjetas adaptables](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Determinar un subconjunto de funcionalidad

***Escenarios de integración**: aplicaciones independientes*

La integración de todas las características de una aplicación existente en Teams suele dar lugar a una experiencia de usuario forzada o poco natural, especialmente en aplicaciones grandes. Comience por las características que vayan a tener un mayor impacto y las que se integran de forma más natural con Teams. Puede permitir que los usuarios inicien la aplicación principal y accedan al conjunto completo de características.

Los siguientes son los requisitos previos para integrar la aplicación con Teams.

1. [Asignar los casos de uso de la aplicación a las funcionalidades de la plataforma Teams](../concepts/design/map-use-cases.md).
1. [Determinar los puntos de entrada de la aplicación](../concepts/extensibility-points.md). ¿Es para uso personal, para colaboración o para ambos?

## <a name="understand-sharepoint-requirements-and-options"></a>Descripción de los requisitos y las opciones de SharePoint

***Escenarios de integración**: SharePoint*

Para integrar una [página de SharePoint](/sharepoint/dev/general-development/overview-of-the-sharepoint-page-model) existente como pestaña de Teams, debe tener en cuenta lo siguiente:

* Debe ser una página *moderna* de SharePoint en línea.
* Solo se admiten pestañas personales. No puede integrar la página como una pestaña de canal.

Como alternativa, puede crear una pestaña de Teams [mediante SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multitenancy"></a>Poner como objetivo un multiinquilino

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Si varias organizaciones usan la aplicación, considere la posibilidad de hospedar varios inquilinos. Esto hace que el producto sea escalable y simplifica la distribución.

## <a name="review-your-apis"></a>Revisión de las API

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración*

Las API y las estructuras de datos de la aplicación deben admitir la aplicación al integrarse con Teams. Para ampliar la compatibilidad, debe aumentar las API y las estructuras de datos con información contextual sobre Teams para la [asignación de identidades](../concepts/authentication/configure-identity-provider.md), la [compatibilidad con vínculos profundos](../concepts/build-and-test/deep-links.md) y [la incorporación de Microsoft Graph](/graph/teams-concept-overview).

Consulte cómo obtener contexto para una [pestaña](../tabs/how-to/access-teams-context.md) o [bot](../bots/how-to/get-teams-context.md) de Teams.

## <a name="understand-authentication-options"></a>Descripción de las opciones de autenticación

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Azure Active Directory es el proveedor de identidades de Teams. Si la aplicación usa un proveedor de identidades diferente, debe realizar una asignación de identidades o combinar con Azure Active Directory (Azure AD) de Microsoft.

Teams tiene mecanismos de inicio de sesión único (SSO) con Azure AD para aplicaciones de terceros. También proporciona instrucciones para los flujos de autenticación a otros proveedores de identidades mediante estándares como OAuth y Open ID Connect, conocido como OIDC.

> [!IMPORTANT]
> En este momento, las aplicaciones de terceros están disponibles en Government Community Cloud (GCC), pero no están disponibles para GCC-High y el Departamento de Defensa (DOD). Las aplicaciones de terceros están desactivadas de forma predeterminada para GCC. Para activar aplicaciones de terceros en GCC, consulte [administrar directivas de permisos de aplicaciones](/microsoftteams/teams-app-permission-policies) y [administrar aplicaciones](/microsoftteams/manage-apps).

Para las páginas de SharePoint, solo se puede usar SSO y no se puede agregar otro id. de Azure AD si quiere que SSO funcione para otra aplicación, ya que el id. es la aplicación de SharePoint.

Obtenga más información sobre la [autenticación en Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Seguir las directrices de diseño de Teams

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración*

Asegúrese de seguir las [directrices de diseño de Teams](../concepts/design/understand-use-cases.md) para que la aplicación sea nativa para Teams. No puede migrar el contenido de una aplicación existente a una pestaña de Teams. Para obtener más información sobre el diseño de aplicaciones, consulte [Sistema Fluent Design](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Maximizar la vinculación en profundidad

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Puede crear vínculos a información y características en Teams. Use [vínculos profundos](../concepts/build-and-test/deep-links.md) para vincular la aplicación con Teams, ya que así se unen varias partes de una aplicación para lograr una experiencia de Teams más nativa.

## <a name="be-smart-when-messaging-users"></a>Sea inteligente al enviar mensajes a los usuarios

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Use un [bot](../bots/what-are-bots.md) en la aplicación de Teams para múltiples conversaciones encadenadas, ya que ofrece más flexibilidad que un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Los bots también permiten enviar **mensajes proactivos** a usuarios o canales. Los mensajes proactivos son mensajes no solicitados que se desencadenan por un evento externo y no por un mensaje enviado a un bot. Por ejemplo, el bot envía un mensaje de bienvenida cuando se instala o un nuevo usuario se une a un canal.

El envío de mensajes proactivos requiere identificadores específicos de Teams. Puede capturar información mediante la [captura de datos de perfil de usuario o de lista de participantes](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), la [suscripción a eventos de conversación](../bots/how-to/conversations/subscribe-to-conversation-events.md) o el uso de [Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams).

No envíe correo no deseado a los usuarios de forma excesiva. Si la funcionalidad de Teams lo admite, los usuarios pueden configurar las opciones de notificación de la aplicación.
A continuación se muestra un ejemplo de un mensaje de notificación: **No enviarme mensajes no solicitados**.

## <a name="use-sharepoint-for-file-and-data-storage"></a>Uso de SharePoint para el almacenamiento de archivos y datos

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, páginas de SharePoint*

Cuando se crea un equipo, también se aprovisiona una [colección de sitios SharePoint](/microsoftteams/sharepoint-onedrive-interact) para admitir el almacenamiento de archivos y datos para ese equipo. La aplicación debe aprovechar esta característica si interactúa con archivos. Use la colección de sitios para almacenar datos sin procesar en listas de SharePoint y Microsoft Excel.

## <a name="see-also"></a>Consulte también

* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Soluciones de código bajo y sin código para Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Compartir en Teams desde aplicaciones web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Atributos de cookies de SameSite](~/resources/samesite-cookie-update.md)
* [Integrar bots de chat de Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
