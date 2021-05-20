---
author: heath-hamilton
description: Prácticas recomendadas para integrar aplicaciones web existentes con Microsoft Teams
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Aplicaciones web
ms.openlocfilehash: 6783a05079f876cf3c2475a0ad5ca0e1f6687fc4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566225"
---
# <a name="web-apps"></a>Aplicaciones web 

Puede hacer que las aplicaciones web sean adecuadas con las funciones sociales y colaborativas de Teams, integrándolas adecuadamente con Teams.
  
Los diferentes tipos de aplicaciones que puede integrar con Teams son los siguientes:
* **Aplicaciones independientes:** una aplicación independiente es una aplicación grande o de una sola página y compleja. El usuario puede utilizar algunos aspectos de la misma en Teams.
* **Aplicaciones de colaboración**: Una aplicación ya creada para las características sociales y colaborativas inherentes a Teams.
* **SharePoint**: Una página de SharePoint que desea salir a la superficie en Teams.

Puede asignar y seguir las directrices adecuadas aplicables a su escenario de integración.
Este documento proporciona una visión general de Teams capacidades, requisitos de punto compartido para almacenamiento de archivos y datos, requisitos de API, autenticación y vinculación profunda de la aplicación con Teams.
 
## <a name="get-to-know-teams-platform-capabilities"></a>Conozca las capacidades de Teams plataforma

***Escenarios de integración**: Aplicaciones independientes, aplicaciones de colaboración, SharePoint*

La aplicación Teams debe incluir las características de colaboración necesarias y esperadas. Para trabajar con la integración de aplicaciones, es importante familiarizarse con Teams terminología de desarrollo.

|Características comunes de la aplicación   |capacidades de plataforma Teams   |
|----------|-----------|
|Página web, página de inicio o vista web integradas  |[Pestañas](../tabs/what-are-tabs.md)  |
|Compartir accesos directos y extensiones  |[Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)  |
|Accesos directos y extensiones de acción  |[Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[Bots](../bots/what-are-bots.md) |
|Notificaciones de canales  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrantes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Conectores de Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Mensajes servicios externos  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks salientes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modales  |[Módulos de tareas](../task-modules-and-cards/what-are-task-modules.md)  |
|Tarjetas ricas en contenido  |[Tarjetas adaptables](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Determinar un subconjunto de funcionalidad

***Escenarios de integración**: Aplicaciones independientes*

La integración de todas las características de una aplicación existente en Teams a menudo conduce a una experiencia de usuario forzada o antinatural, especialmente en aplicaciones más grandes. Comience con las características más impactantes y aquellas que se integran más naturalmente con Teams. Puede permitir que los usuarios inicien la aplicación principal y accedan a su conjunto completo de características.

**Requisitos previos para integrar la aplicación con Teams** A continuación se indican los requisitos previos para integrar la aplicación con Teams. 

1. [Asigna los casos de uso de la aplicación a Teams capacidades de la plataforma.](../concepts/design/map-use-cases.md)
1. [Determina los puntos de entrada de la aplicación.](../concepts/extensibility-points.md) ¿Es para uso personal, colaboración o ambos?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprender SharePoint requisitos y opciones

***Escenarios de integración**: SharePoint*

Para integrar una [página de SharePoint](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) existente como una pestaña de Teams, debe tener en cuenta lo siguiente:

* Debe ser una página *moderna* SharePoint en línea.
* Solo se admiten pestañas personales. No puede integrar la página como una pestaña de canal.

Como alternativa, puede crear una pestaña Teams [mediante la SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multi-tenancy"></a>Apunta hacia la multiinquilino

***Escenarios de integración**: Aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Si varias organizaciones usan la aplicación, considere la posibilidad de hospedaje multiinquilino que hace que el producto sea escalable y simplifique en gran medida la distribución.

## <a name="review-your-apis"></a>Revise sus API

***Escenarios de integración**: Aplicaciones independientes, aplicaciones de colaboración*

Debe hacer que las API y estructuras de datos existentes de la aplicación admitan la aplicación al integrarse con Teams. Para ampliar la compatibilidad, debe aumentar las API y estructuras de datos con información contextual sobre Teams para [la asignación de identidades,](../concepts/authentication/configure-identity-provider.md)compatibilidad con [vínculos profundos](../concepts/build-and-test/deep-links.md)e [incorporar Microsoft Graph](/graph/teams-concept-overview).

Obtén más información sobre cómo obtener contexto para tu [pestaña](../tabs/how-to/access-teams-context.md) o [bot](../bots/how-to/get-teams-context.md)de Teams.

## <a name="understand-authentication-options"></a>Comprender las opciones de autenticación

***Escenarios de integración**: Aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Azure Active Directory (AD) es el proveedor de identidades para Teams. Si la aplicación usa un proveedor de identidades diferente, debe realizar un ejercicio de asignación de identidad o combinarse con Azure AD.

Teams tiene mecanismos de inicio de sesión único (SSO) con Azure AD para aplicaciones de terceros. También proporciona la guía para los flujos de autenticación a otros proveedores de identidades mediante estándares como OAuth y Open ID Conectar, conocido como OIDC.

Para SharePoint páginas, solo puede usar SSO y no puede agregar otro identificador de Azure AD si desea que SSO funcione para otra aplicación, ya que el identificador es la aplicación SharePoint.

Obtenga más información sobre [la autenticación en Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Siga las directrices de diseño Teams

***Escenarios de integración**: Aplicaciones independientes, aplicaciones de colaboración*

Asegúrese de seguir [las directrices de diseño Teams](../concepts/design/understand-use-cases.md) para que la aplicación sea nativa de Teams. No puede migrar el contenido de una aplicación existente a una pestaña Teams. Para obtener más información sobre el diseño de aplicaciones, consulte [Sistema de diseño fluido.](https://fluentsite.z22.web.core.windows.net/)

## <a name="maximize-deep-linking"></a>Maximizar la vinculación profunda

***Escenarios de integración**: Aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Puede crear vínculos a información y entidades dentro de Teams. Usa [vínculos profundos](../concepts/build-and-test/deep-links.md) para vincular tu aplicación con Teams mientras unen varias piezas de una aplicación para una experiencia de Teams más nativa.

## <a name="be-smart-when-messaging-users"></a>Sea inteligente al enviar mensajes a los usuarios

***Escenarios de integración**: Aplicaciones independientes, aplicaciones de colaboración, SharePoint*

Utilice un [bot](../bots/what-are-bots.md) en la aplicación Teams para conversaciones multiproceso, ya que ofrece más flexibilidad que un [webhook.](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

Los bots también le permiten enviar **mensajes proactivos** a usuarios o canales individuales. Los mensajes proactivos son mensajes no probados desencadenados por un evento externo y no por un mensaje enviado a un bot. Por ejemplo, el bot envía un mensaje de bienvenida cuando está instalado o un nuevo usuario se une a un canal. 

El envío de mensajes proactivos requiere identificadores específicos de Teams. Puede capturar la información [recuperando datos de perfil de usuario o lista,](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile) [suscribiéndose a eventos de conversación](../bots/how-to/conversations/subscribe-to-conversation-events.md)o utilizando Microsoft [Graph](/graph/teams-proactive-messaging).

No spam usuarios con mensajes excesivos. Si la funcionalidad Teams lo admite, los usuarios pueden configurar la configuración de notificaciones para la aplicación.   
A continuación se muestra un ejemplo de un mensaje de notificación: **No me envíe mensajes sin probar.**

## <a name="use-sharepoint-for-file-and-data-storage"></a>Usar SharePoint para el almacenamiento de archivos y datos

***Escenarios de integración:** Aplicaciones independientes, aplicaciones de colaboración, páginas de SharePoint*

Cuando se crea un equipo, también se aprovisiona una [colección de sitios SharePoint](/microsoftteams/sharepoint-onedrive-interact) para admitir el almacenamiento de archivos y datos para ese equipo. La aplicación debe aprovechar esta característica si interactúa con los archivos. Utilice la colección de sitios para almacenar datos sin procesar en listas de SharePoint y Excel.

## <a name="see-also"></a>Vea también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
