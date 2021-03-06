---
author: heath-hamilton
description: Procedimientos recomendados para integrar aplicaciones web existentes con Microsoft Teams
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Aplicaciones web
ms.openlocfilehash: b7f530198a8e1c240e3cf4b227d786af94f6c89e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630435"
---
# <a name="web-apps"></a>Aplicaciones web 

Puede hacer que las aplicaciones web se ajusten a las características sociales y de colaboración de Teams, integrándolos correctamente con Teams.
  
Los diferentes tipos de aplicaciones que puedes integrar con Teams son los siguientes:
* **Aplicaciones independientes:** una aplicación independiente es una aplicación de una sola página o grande y compleja. El usuario puede usar algunos aspectos de Teams.
* **Aplicaciones de colaboración:** una aplicación ya creada para las características sociales y de colaboración inherentes a Teams.
* **SharePoint:** una página SharePoint que desea que se desaocie en Teams.

Puede asignar y seguir las instrucciones adecuadas aplicables a su escenario de integración.
En este documento se proporciona información general sobre las funcionalidades de Teams, los requisitos de punto compartido para el almacenamiento de archivos y datos, los requisitos de api, la autenticación y la vinculación profunda de la aplicación con Teams.
 
## <a name="get-to-know-teams-platform-capabilities"></a>Conozca las funcionalidades Teams plataforma

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

La aplicación Teams debe incluir características de colaboración necesarias y esperadas. Para trabajar con la integración de aplicaciones, es importante familiarizarse con Teams terminología de desarrollo.

|Características comunes de la aplicación   |Teams de plataforma   |
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

La integración de todas las características de una aplicación existente en Teams a menudo conduce a una experiencia de usuario forzada o no natural, especialmente en aplicaciones más grandes. Comience con las características más impactantes y las que se integran de forma más natural con Teams. Puedes permitir que los usuarios inicien la aplicación principal y accedan a su conjunto completo de características.

**Requisitos previos para integrar la aplicación con Teams** A continuación se indican los requisitos previos para integrar la aplicación con Teams. 

1. [Asigna los casos de uso de la aplicación a Teams funcionalidades de plataforma.](../concepts/design/map-use-cases.md)
1. [Determinar los puntos de entrada de la aplicación](../concepts/extensibility-points.md). ¿Es para uso personal, colaboración o ambos?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprender SharePoint requisitos y opciones

***Escenarios de integración:** SharePoint*

Para integrar una página [de SharePoint existente](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) como una Teams, debe tener en cuenta lo siguiente:

* Debe ser una página *moderna* SharePoint en línea.
* Solo se admiten pestañas personales. No puede integrar la página como una pestaña de canal.

Como alternativa, puede crear una pestaña Teams [con el SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multi-tenancy"></a>Apuntar a multiinquilino

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Si la aplicación la usan varias organizaciones, considera el hospedaje multiinquilino que haga que el producto sea escalable y simplifique enormemente la distribución.

## <a name="review-your-apis"></a>Revisar las API

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración*

Debes hacer que las API y estructuras de datos existentes de la aplicación admitan la aplicación al integrarla con Teams. Para ampliar la compatibilidad, debe aumentar las API y estructuras de datos [](../concepts/build-and-test/deep-links.md)con información contextual sobre Teams para la asignación de identidades, [](../concepts/authentication/configure-identity-provider.md)compatibilidad con vínculos profundos e incorporación de Microsoft [Graph](/graph/teams-concept-overview).

Obtenga más información sobre cómo obtener contexto para su Teams [o](../tabs/how-to/access-teams-context.md) [bot](../bots/how-to/get-teams-context.md).

## <a name="understand-authentication-options"></a>Comprender las opciones de autenticación

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Azure Active Directory (AD) es el proveedor de identidades para Teams. Si la aplicación usa un proveedor de identidades diferente, debe realizar un ejercicio de asignación de identidades o combinarlo con Azure AD.

Teams tiene mecanismos de inicio de sesión único (SSO) con Azure AD para aplicaciones de terceros. También proporciona instrucciones para flujos de autenticación a otros proveedores de identidades mediante estándares como OAuth y Open ID Conectar, conocidos como OIDC.

Para SharePoint, solo puedes usar SSO y no puedes agregar otro identificador de Azure AD si quieres que SSO funcione para otra aplicación, ya que el identificador es la SharePoint aplicación.

Obtenga más información [sobre la autenticación en Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Seguir Teams de diseño

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración*

Asegúrate de seguir [las Teams de diseño para](../concepts/design/understand-use-cases.md) que tu aplicación sea nativa de Teams. No puedes migrar un contenido de la aplicación existente a una Teams pestaña. Para obtener más información sobre el diseño de aplicaciones, consulta [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Maximizar la vinculación profunda

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Puede crear vínculos a información y características dentro de Teams. Usa [vínculos profundos](../concepts/build-and-test/deep-links.md) para vincular la aplicación con Teams a medida que unen varias partes de una aplicación para una experiencia Teams nativa.

## <a name="be-smart-when-messaging-users"></a>Ser inteligente cuando los usuarios de mensajería

***Escenarios de integración:** aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Usa un [bot](../bots/what-are-bots.md) en tu aplicación Teams para conversaciones multiproceso, ya que ofrece más flexibilidad que un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Los bots también permiten enviar mensajes **proactivos** a usuarios o canales individuales. Los mensajes proactivos son mensajes no proactivos desencadenados por un evento externo y no un mensaje enviado a un bot. Por ejemplo, el bot envía un mensaje de bienvenida cuando está instalado o un nuevo usuario se une a un canal. 

El envío de mensajes proactivos requiere Teams identificadores específicos. Puede capturar la información mediante [la captura de](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)datos de lista o perfil de usuario, la suscripción a eventos de conversación o el uso de Microsoft [Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams). [](../bots/how-to/conversations/subscribe-to-conversation-events.md)

No enviar correo no deseado a los usuarios con mensajes excesivos. Si la Teams la admite, los usuarios pueden configurar las opciones de notificación para la aplicación.   
A continuación se muestra un ejemplo de un mensaje de notificación: **No me envíe mensajes no probados.**

## <a name="use-sharepoint-for-file-and-data-storage"></a>Usar SharePoint para el almacenamiento de archivos y datos

***Escenarios de integración:** Aplicaciones independientes, aplicaciones de colaboración, SharePoint páginas*

Cuando se crea un equipo, también [se aprovisiona SharePoint](/microsoftteams/sharepoint-onedrive-interact) colección de sitios para admitir el almacenamiento de archivos y datos para ese equipo. La aplicación debe aprovechar esta característica si interactúa con archivos. Use la colección de sitios para almacenar datos sin procesar en SharePoint listas y Excel.

## <a name="see-also"></a>Consulte también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
