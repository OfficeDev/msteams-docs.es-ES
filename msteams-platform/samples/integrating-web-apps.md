---
author: heath-hamilton
description: Procedimientos recomendados para la integración de aplicaciones Web existentes con Microsoft Teams
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Integración de una aplicación web con Microsoft Teams
ms.openlocfilehash: e7d4f74526f7a71fe33d5a70d9ed60be960adefc
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210355"
---
# <a name="integrate-web-apps-with-teams"></a>Integración de aplicaciones web con Microsoft Teams

¿Tiene una aplicación web que cree que quepa de forma natural con las características sociales y de colaboración de Microsoft Teams? Estas instrucciones pueden ayudarle a comprender cómo integrar los siguientes tipos de aplicaciones:

* **Aplicaciones independientes**: puede ser una aplicación de una sola página o una aplicación grande y compleja en la que desea que los usuarios usen algunos aspectos de en Teams.
* **Aplicaciones de colaboración**: una aplicación ya creada para las características sociales y de colaboración inherentes a teams.
* **SharePoint**: una página de SharePoint que desea exponer en Microsoft Teams.

Para cada directriz, puede ver si es aplicable a su escenario de integración.

## <a name="get-to-know-teams-platform-capabilities"></a>Familiarizarse con las capacidades de la plataforma de Microsoft Teams

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint *

La aplicación de Microsoft Teams puede incluir características que los usuarios desean y podrían esperar al colaborar, pero puede que no esté familiarizado con la terminología de desarrollo de Teams.

|Características comunes de la aplicación   |Capacidades de la plataforma de Microsoft Teams   |
|----------|-----------|
|Página Web, Página principal o vista previa insertada  |[Pestañas](../tabs/what-are-tabs.md)  |
|Compartir accesos directos y extensiones  |[Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)  |
|Extensiones y métodos abreviados de acciones  |[Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[Bots](../bots/what-are-bots.md) |
|Notificaciones de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrantes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Conectores de Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Servicios externos de mensajes  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks salientes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modales  |[Módulos de tareas](../task-modules-and-cards/what-are-task-modules.md)  |
|Tarjetas de contenido enriquecido  |[Tarjetas adaptables](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Determinación de un subconjunto de funciones

***Escenarios de integración**: aplicaciones independientes *

La integración de todas las características de una aplicación existente en Teams a menudo conduce a una experiencia de usuario forzada o poco natural, especialmente en aplicaciones de mayor tamaño. Considere la posibilidad de empezar con las características más impactantes y las que se integrarán de forma más natural con Microsoft Teams. Recuerde que siempre puede permitir a los usuarios que inicien la aplicación principal y obtengan acceso a su conjunto completo de características.

Antes de empezar con un trabajo técnico, realice alguna planeación de la aplicación de Microsoft Teams:

1. [Asigne los casos de uso de la aplicación a las capacidades de la plataforma de Teams](../concepts/design/map-use-cases.md).
1. [Determine los puntos de entrada de la aplicación](../concepts/extensibility-points.md). ¿Se trata de uso personal, colaboración o ambos?

## <a name="understand-sharepoint-requirements-and-options"></a>Descripción de los requisitos y las opciones de SharePoint

***Escenarios de integración**: SharePoint *

Puede integrar una página de [SharePoint](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) existente como una pestaña de Microsoft Teams. Recuerde lo siguiente:

* Debe ser una página *moderna* de SharePoint Online
* Solo se admiten las pestañas personales (no puede integrar la página como una ficha de canal)

Como alternativa, puede crear una pestaña de Microsoft Teams [con SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multi-tenancy"></a>Objetivo hacia la multiempresa

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint *

Si la aplicación se usa en varias organizaciones, tenga en cuenta el hospedaje de varios inquilinos que hará que el producto sea escalable y simplifique la distribución.

## <a name="review-your-apis"></a>Revisar las API

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración *

No asuma que las API y las estructuras de datos existentes de la aplicación son compatibles completamente con la aplicación cuando se integra con Microsoft Teams. Es posible que necesite aumentarlos con información contextual sobre Microsoft Teams para la [asignación de identidades](../concepts/authentication/configure-identity-provider.md), [compatibilidad con vínculos profundos y la](../concepts/build-and-test/deep-links.md)incorporación de [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).

Obtenga más información sobre cómo obtener contexto para la [pestaña](../tabs/how-to/access-teams-context.md) o el [Bot](../bots/how-to/get-teams-context.md)de Teams.

## <a name="understand-authentication-options"></a>Descripción de las opciones de autenticación

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint *

Azure Active Directory (AD) es el proveedor de identidades para Microsoft Teams. Si la aplicación usa un proveedor de identidades diferente, debe realizar un ejercicio de asignación de identidades o federarse con Azure AD.

Microsoft Teams tiene mecanismos de inicio de sesión único (SSO) con Azure AD para aplicaciones de terceros y guía para los flujos de autenticación a otros proveedores de identidades que usan estándares como OAuth y Open ID Connect (OIDC).

En el caso de las páginas de SharePoint, solo puede usar SSO y no puede agregar otro identificador de Azure AD si desea que SSO funcione para otra aplicación (ya que el identificador es la aplicación de SharePoint).

Obtenga más información sobre la [autenticación en Microsoft Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Seguir las instrucciones de diseño de Teams

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración *

En general, la aplicación debe sentirse natural en Teams. Puede creer que la migración del contenido de la aplicación existente a una pestaña de Microsoft Teams es suficiente, pero se recomienda encarecidamente que la aplicación siga las [directrices de diseño de Teams](../concepts/design/understand-use-cases.md). Vea también: [sistema de diseño de Fluent](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Maximizar la vinculación profunda

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint *

Casi todo en Microsoft Teams se puede vincular directamente a un [vínculo profundo](../concepts/build-and-test/deep-links.md). La aplicación debe maximizar el uso de estos, lo que incluye la vinculación a y desde determinados mensajes y contenido de la pestaña. En realidad, los vínculos profundos pueden vincular varias partes de una aplicación para una experiencia más nativa de Microsoft Teams.

## <a name="be-smart-when-messaging-users"></a>Ser inteligente cuando los usuarios de mensajería

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint *

Considere los tipos de mensajes que la aplicación de Teams puede enviar ahora y a largo plazo. Si cree que su aplicación tendrá una conversación multiproceso, es posible que un [Bot](../bots/what-are-bots.md) ofrezca más flexibilidad que un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Los bots también permiten enviar *mensajes proactivos* a usuarios individuales o canales. Se trata de mensajes sin pedir desencadenados por un evento externo y no de un mensaje enviado a un bot. (Por ejemplo, el bot puede enviar un mensaje de bienvenida cuando está instalado o un nuevo usuario se une a un canal). 

El envío de mensajes proactivos requiere identificadores específicos de Microsoft Teams: puede capturar esta información buscando la [lista o los datos de perfiles de usuario](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile), [suscribirse a eventos de conversación](../bots/how-to/conversations/subscribe-to-conversation-events.md)o usar [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).

Tenga cuidado de no enviar correo no deseado a los usuarios con demasiados mensajes. Si la funcionalidad de Teams lo admite, considere la posibilidad de permitir que los usuarios configuren la configuración de notificaciones para la aplicación (por ejemplo, "no enviar mensajes sin pedir").

## <a name="use-sharepoint-for-file-and-data-storage"></a>Uso de SharePoint para el almacenamiento de archivos y datos

***Escenarios de integración:** Aplicaciones independientes, aplicaciones de colaboración, páginas de SharePoint*

Cuando se crea un equipo, también se aprovisiona una [colección de sitios de SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) para admitir el almacenamiento de datos y archivos de ese equipo. La aplicación puede y debe aprovechar esta característica si interactúa con los archivos. También puede usar la colección de sitios para almacenar datos sin procesar en listas de SharePoint y Excel.
