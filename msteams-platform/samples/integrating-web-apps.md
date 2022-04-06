---
author: heath-hamilton
description: Procedimientos recomendados o consideraciones para integrar aplicaciones web existentes con Microsoft Teams
ms.author: surbhigupta
ms.date: 08/26/2020
ms.localizationpriority: medium
ms.topic: conceptual
title: Consideraciones para la integración de Teams
ms.openlocfilehash: eb278d078c7b195ff5d2d2a2f980ffc9db74f748
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685600"
---
# <a name="considerations-for-teams-integration"></a>Consideraciones para la integración de Teams

Puede hacer que las aplicaciones web sean adecuadas con las características sociales y colaborativas de Teams, integrándolas correctamente con Teams.
  
Los diferentes tipos de aplicaciones que puede integrar con Teams son los siguientes:

* **Aplicaciones independientes**: una aplicación independiente es una aplicación de una sola página o grande y compleja. El usuario puede usar algunos aspectos de él en Teams.
* **Aplicaciones de colaboración**: una aplicación ya creada para las características sociales y colaborativas inherentes a Teams.
* **SharePoint**: página de SharePoint que desea mostrar en Teams.

Puede asignar y seguir la guía adecuada aplicable al escenario de integración.
En este documento se proporciona información general sobre las funcionalidades de Teams, los requisitos de punto de recurso compartido para el almacenamiento de archivos y datos, los requisitos de API, la autenticación y la vinculación profunda de la aplicación con Teams.

## <a name="get-to-know-teams-platform-capabilities"></a>Conocer las funcionalidades de la plataforma Teams

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

La aplicación Teams debe incluir las características de colaboración necesarias y esperadas. Para trabajar con la integración de aplicaciones, es importante familiarizarse con Teams terminología de desarrollo.

|Características comunes de la aplicación   |Funcionalidades de la plataforma de Teams   |
|----------|-----------|
|Página web incrustada, página principal o vista web  |[Pestañas](../tabs/what-are-tabs.md)  |
|Uso compartido de accesos directos y extensiones  |[Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)  |
|Accesos directos y extensiones de acción  |[Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots |[Bots](../bots/what-are-bots.md) |
|Notificaciones de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrantes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Conectores de Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Servicios externos de mensajes  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks salientes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modals  |[Módulos de tareas](../task-modules-and-cards/what-are-task-modules.md)  |
|Tarjetas enriquecidas con contenido  |[Tarjetas adaptables](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Determinación de un subconjunto de funciones

***Escenarios de integración**: aplicaciones independientes*

La integración de todas las características de una aplicación existente en Teams a menudo conduce a una experiencia de usuario forzada o no natural, especialmente en aplicaciones más grandes. Comience con las características más impactantes y las que se integran de forma más natural con Teams. Puede permitir que los usuarios inicien la aplicación principal y accedan a su conjunto completo de características.

Los siguientes son los requisitos previos para integrar la aplicación con Teams.

1. [Asigne los casos de uso de la aplicación a las funcionalidades de la plataforma de Teams](../concepts/design/map-use-cases.md).
1. [Determine los puntos de entrada de la aplicación](../concepts/extensibility-points.md). ¿Es para uso personal, para colaboración o para ambos?

## <a name="understand-sharepoint-requirements-and-options"></a>Descripción de los requisitos y las opciones de SharePoint

***Escenarios de integración**: SharePoint*

Para integrar una [página de SharePoint](/sharepoint/dev/general-development/overview-of-the-sharepoint-page-model) existente como una pestaña de Teams, debe tener en cuenta lo siguiente:

* Debe ser una página *moderna* SharePoint en línea.
* Solo se admiten pestañas personales. No puede integrar la página como una pestaña de canal.

Como alternativa, puede crear una pestaña de Teams [mediante el SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multitenancy"></a>Objetivo hacia la multiinquilino

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Si varias organizaciones usan la aplicación, considere la posibilidad de hospedar varios inquilinos. Hace que el producto sea escalable y simplifica la distribución.

## <a name="review-your-apis"></a>Revisión de las API

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración*

Las API y estructuras de datos de la aplicación deben admitir la aplicación al integrarla con Teams. Para ampliar la compatibilidad, debe aumentar las API y las estructuras de datos con información contextual sobre Teams para la [asignación de identidades](../concepts/authentication/configure-identity-provider.md), la [compatibilidad con vínculos profundos](../concepts/build-and-test/deep-links.md) y [la incorporación de Microsoft Graph](/graph/teams-concept-overview).

Consulte cómo obtener el contexto de la [pestaña](../tabs/how-to/access-teams-context.md) o [bot](../bots/how-to/get-teams-context.md) de Teams.

## <a name="understand-authentication-options"></a>Descripción de las opciones de autenticación

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Azure Active Directory es el proveedor de identidades de Teams. Si la aplicación usa un proveedor de identidades diferente, debe realizar un ejercicio de asignación de identidades o combinar con Microsoft Azure Active Directory (Azure AD).

Teams tiene mecanismos de inicio de sesión único (SSO) con Azure AD para aplicaciones de terceros. También proporciona las instrucciones para los flujos de autenticación a otros proveedores de identidades mediante estándares como OAuth y Open ID Conectar, conocidos como OIDC.

> [!IMPORTANT]
> Actualmente, las aplicaciones de terceros están disponibles en Government Community Cloud (GCC), pero no están disponibles para GCC-High y el Departamento de Defensa (DOD). Las aplicaciones de terceros están desactivadas de forma predeterminada para GCC. Para activar aplicaciones de terceros para GCC, consulte [Administración de directivas de permisos de aplicaciones](/microsoftteams/teams-app-permission-policies) y [administración de aplicaciones](/microsoftteams/manage-apps).

En SharePoint páginas, solo puede usar sso y no puede agregar otro identificador de Azure AD si desea que el inicio de sesión único funcione para otra aplicación, ya que el identificador es la aplicación SharePoint.

Obtenga más información sobre [la autenticación en Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Siga las instrucciones de diseño de Teams

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración*

Asegúrese de seguir [Teams directrices de diseño](../concepts/design/understand-use-cases.md) para que la aplicación sea nativa para Teams. No se puede migrar un contenido de aplicación existente a una pestaña de Teams. Para obtener más información sobre el diseño de aplicaciones, consulte [Sistema Fluent Design](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Maximizar la vinculación profunda

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Puede crear vínculos a información y características en Teams. Usa [vínculos profundos](../concepts/build-and-test/deep-links.md) para vincular la aplicación con Teams, ya que unen varias partes de una aplicación para una experiencia de Teams más nativa.

## <a name="be-smart-when-messaging-users"></a>Ser inteligente cuando los usuarios de mensajería

***Escenarios de integración**: aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Use un [bot](../bots/what-are-bots.md) en la aplicación Teams para la conversación multiproceso, ya que ofrece más flexibilidad que un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Los bots también permiten enviar **mensajes proactivos** a usuarios o canales individuales. Los mensajes proactivos son mensajes no proprompidos desencadenados por un evento externo y no un mensaje enviado a un bot. Por ejemplo, el bot envía un mensaje de bienvenida cuando está instalado o un nuevo usuario se une a un canal.

El envío de mensajes proactivos requiere identificadores específicos de Teams. Puede capturar la información mediante la [captura de datos de perfil de usuario o de lista](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [la suscripción a eventos de conversación](../bots/how-to/conversations/subscribe-to-conversation-events.md) o el uso [de Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams).

No envíe correo no deseado a los usuarios con mensajes excesivos. Si la funcionalidad Teams la admite, los usuarios pueden configurar las opciones de notificación para la aplicación.
A continuación se muestra un ejemplo de un mensaje de notificación: **No me envíe mensajes no probados**.

## <a name="use-sharepoint-for-file-and-data-storage"></a>Uso de SharePoint para el almacenamiento de archivos y datos

***Escenarios de integración:** Aplicaciones independientes, aplicaciones de colaboración, páginas de SharePoint*

Cuando se crea un equipo, también se aprovisiona una [colección de sitios SharePoint](/microsoftteams/sharepoint-onedrive-interact) para admitir el almacenamiento de archivos y datos para ese equipo. La aplicación debe aprovechar esta característica si interactúa con archivos. Use la colección de sitios para almacenar datos sin procesar en listas de SharePoint y Microsoft Excel.

## <a name="see-also"></a>Consulte también

* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Soluciones de código bajo y sin código para Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Uso compartido en Teams desde aplicaciones web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Atributos de cookies de SameSite](~/resources/samesite-cookie-update.md)
* [Integrar Power Virtual Agents bot de chat](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
