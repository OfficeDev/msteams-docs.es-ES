---
author: heath-hamilton
description: Procedimientos recomendados para integrar aplicaciones web existentes con Microsoft Teams
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Integrar una aplicación web con Microsoft Teams
ms.openlocfilehash: 4671d2277d5eb7c035421c51b1714eccaac06a31
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696489"
---
# <a name="integrate-web-apps-with-teams"></a>Integrar aplicaciones web con Teams

¿Tienes una aplicación web que crees que encajaría de forma natural con las características sociales y de colaboración de Teams? Estas directrices pueden ayudarle a comprender cómo integrar los siguientes tipos de aplicaciones:

* **Aplicaciones independientes:** puede ser una aplicación de una sola página o una aplicación grande y compleja de la que quieres que los usuarios usen algunos aspectos de Teams.
* **Aplicaciones de colaboración:** una aplicación ya creada para las características sociales y de colaboración inherentes a Teams.
* **SharePoint:** una página de SharePoint que desea que se despunte en Teams.

Para cada directriz, puede ver si es aplicable al escenario de integración.

## <a name="get-to-know-teams-platform-capabilities"></a>Conocer las capacidades de la plataforma de Teams

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

La aplicación de Teams puede incluir características que los usuarios desean y pueden esperar al colaborar, pero es posible que no esté familiarizado con la terminología de desarrollo de Teams.

|Características comunes de la aplicación   |Capacidades de la plataforma de Teams   |
|----------|-----------|
|Página web incrustada, página principal o vista web  |[Pestañas](../tabs/what-are-tabs.md)  |
|Compartir accesos directos y extensiones  |[Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)  |
|Accesos directos y extensiones de acción  |[Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[Bots](../bots/what-are-bots.md) |
|Notificaciones de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrantes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Conectores de Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Servicios externos de mensajes  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks salientes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modales  |[Módulos de tareas](../task-modules-and-cards/what-are-task-modules.md)  |
|Tarjetas enriquecciones de contenido  |[Tarjetas adaptables](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Determinar un subconjunto de funciones

***Escenarios de integración:** aplicaciones independientes*

La integración de todas las características de una aplicación existente en Teams suele dar lugar a una experiencia de usuario forzada o no natural, especialmente en aplicaciones más grandes. Considera empezar con las características más impactantes y aquellas que se integrarán de forma más natural con Teams. Recuerda que siempre puedes permitir que los usuarios inicien la aplicación principal y accedan a su conjunto completo de características.

Antes de comenzar cualquier trabajo técnico, haga algo de planeación para la aplicación de Teams:

1. [Asigne los casos de uso de la aplicación a las capacidades de la plataforma de Teams.](../concepts/design/map-use-cases.md)
1. [Determinar los puntos de entrada de la aplicación](../concepts/extensibility-points.md). ¿Es para uso personal, colaboración o ambos?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprender los requisitos y opciones de SharePoint

***Escenarios de integración:** SharePoint*

Puede integrar una página de [SharePoint existente como](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) una pestaña de Teams. Recuerde lo siguiente:

* Debe ser una página *moderna de* SharePoint Online
* Solo se admiten pestañas personales (no se puede integrar la página como pestaña de canal)

Como alternativa, puede crear una pestaña de Teams [con SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multi-tenancy"></a>Apuntar a multiinquilino

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Si la aplicación la usan varias organizaciones, considera el hospedaje multiinquilino que haría que el producto sea escalable y simplificaría enormemente la distribución.

## <a name="review-your-apis"></a>Revisar las API

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración*

No supongas que las API y estructuras de datos existentes de la aplicación son totalmente compatibles con la aplicación cuando se integran con Teams. Es posible que deba aumentarlos con información [](../concepts/build-and-test/deep-links.md)contextual sobre Teams para la asignación de [identidades,](../concepts/authentication/configure-identity-provider.md)compatibilidad con vínculos profundos e [incorporación de Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).

Obtenga más información sobre cómo obtener contexto para la [pestaña](../tabs/how-to/access-teams-context.md) o [bot](../bots/how-to/get-teams-context.md)de Teams .

## <a name="understand-authentication-options"></a>Comprender las opciones de autenticación

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Azure Active Directory (AD) es el proveedor de identidades de Teams. Si la aplicación usa un proveedor de identidades diferente, debe realizar un ejercicio de asignación de identidades o federar con Azure AD.

Teams tiene mecanismos de inicio de sesión único (SSO) con Azure AD para aplicaciones de terceros y instrucciones para flujos de autenticación a otros proveedores de identidades mediante estándares como OAuth y Open ID Connect (OIDC).

Para las páginas de SharePoint, solo puede usar SSO y no puede agregar otro identificador de Azure AD si desea que SSO funcione para otra aplicación (ya que el identificador es la aplicación de SharePoint).

Obtenga más información sobre [la autenticación en Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Seguir las directrices de diseño de Teams

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración*

En general, la aplicación debe sentirse natural en Teams. Es posible que pienses que la migración del contenido de la aplicación existente a una pestaña de Teams es suficiente, pero te recomendamos encarecidamente que la aplicación siga las directrices de diseño [de Teams.](../concepts/design/understand-use-cases.md) Vea también: [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Maximizar la vinculación profunda

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Casi todo en Teams se puede vincular directamente con un [vínculo profundo.](../concepts/build-and-test/deep-links.md) La aplicación debe maximizar el uso de estos, incluidos los vínculos a y desde mensajes específicos y contenido de pestañas. Los vínculos profundos realmente pueden unir varias partes de una aplicación para una experiencia de Teams más nativa.

## <a name="be-smart-when-messaging-users"></a>Ser inteligente cuando los usuarios de mensajería

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Ten en cuenta los tipos de mensajes que la aplicación de Teams puede enviar ahora y a largo plazo. Si crees que la aplicación alguna vez tendrá una conversación multiproceso, un [bot](../bots/what-are-bots.md) puede ofrecer más flexibilidad que un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Los bots también permiten enviar mensajes *proactivos* a usuarios o canales individuales. Estos son mensajes no probados desencadenados por un evento externo y no un mensaje enviado a un bot. (Por ejemplo, el bot puede enviar un mensaje de bienvenida cuando está instalado o un nuevo usuario se une a un canal).

El envío de mensajes proactivos requiere identificadores específicos de Teams: [](../bots/how-to/conversations/subscribe-to-conversation-events.md)puede capturar esta información mediante la captura de datos de lista o perfil de [usuario,](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)la suscripción a eventos de conversación o el uso de [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).

Tenga cuidado de no enviar correo no deseado a los usuarios con mensajes excesivos. Si la funcionalidad de Teams lo admite, considere la posibilidad de permitir que los usuarios configuren las opciones de notificación para la aplicación (por ejemplo, "No me envíes mensajes no probados").

## <a name="use-sharepoint-for-file-and-data-storage"></a>Usar SharePoint para el almacenamiento de archivos y datos

***Escenarios de integración:** Aplicaciones independientes, aplicaciones de colaboración, páginas de SharePoint*

Cuando se crea un equipo, también se aprovisiona una colección de sitios de [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) para admitir el almacenamiento de archivos y datos para ese equipo. La aplicación puede y debe aprovechar esta característica si interactúa con archivos. También puede usar la colección de sitios para almacenar datos sin procesar en Listas de SharePoint y Excel.
