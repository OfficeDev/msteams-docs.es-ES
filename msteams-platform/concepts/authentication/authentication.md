---
title: Autenticación de usuarios de aplicaciones
description: Describe la autenticación en Teams y cómo usarla en las aplicaciones
ms.topic: conceptual
localization_priority: Normal
keywords: Autenticación de teams OAuth SSO AAD
ms.openlocfilehash: 73d85fed57caff410e2f4986f208b868c228777deade8a5a2a0a1ce0e35d7cd3
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705597"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Autenticar usuarios en Microsoft Teams

> [!Note]
> La autenticación basada en web en clientes móviles requiere la versión 1.4.1 o posterior del SDK de cliente Teams JavaScript.

Para obtener acceso a la información de usuario protegida por Azure Active Directory (AAD) y acceder a datos de servicios como Facebook y Twitter, la aplicación establece una conexión de confianza con esos proveedores. Si la aplicación usa las API Graph Microsoft en el ámbito de usuario, autentique al usuario para recuperar los tokens de autenticación adecuados.

En Teams, hay dos flujos de autenticación diferentes para la aplicación. Realice un flujo de autenticación basado en web tradicional en [una](~/tabs/how-to/create-tab-pages/content-page.md) página de contenido incrustada en una pestaña, una página de configuración o un módulo de tareas. Si la aplicación contiene un bot de conversación, use el flujo de OAuthPrompt y, opcionalmente, el servicio de tokens de Azure Bot Framework para autenticar a un usuario como parte de una conversación.

## <a name="web-based-authentication-flow"></a>Flujo de autenticación basado en web

Use el flujo de autenticación basado en web para las [pestañas](~/tabs/what-are-tabs.md) y elija usarlo con [bots de](~/bots/what-are-bots.md) conversación o extensiones [de mensajería.](~/messaging-extensions/what-are-messaging-extensions.md) Use el [SDK Microsoft Teams cliente de JavaScript](/javascript/api/overview/msteams-client) en una página de contenido web para habilitar la autenticación. Después de habilitar la autenticación, inserte la página de contenido en una pestaña, una página de configuración o un módulo de tareas. Para obtener más información sobre el flujo de autenticación basado en web, vea:

* [Agregar autenticación al bot Teams describe](~/bots/how-to/authentication/add-authentication.md) cómo usar el flujo de autenticación basado en web con un bot de conversación.
* [El flujo de autenticación en las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) describe cómo funciona la autenticación de pestañas en Teams. Esto muestra un flujo de autenticación basado en web típico usado para las pestañas.
* [La autenticación de AAD](~/tabs/how-to/authentication/auth-tab-AAD.md) en pestañas describe cómo conectarse a AAD desde dentro de una pestaña de la aplicación en Teams.
* [La autenticación silenciosa AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) describe cómo reducir los mensajes de inicio de sesión o de consentimiento en la aplicación mediante AAD.
* [.Net o C#,](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript o Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) proporciona ejemplos para la autenticación basada en web.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flujo OAuthPrompt para bots conversacionales

OAuthPrompt de Azure Bot Framework facilita la autenticación para las aplicaciones que usan bots de conversación. Use el servicio de token de Azure Bot Framework para ayudar con el almacenamiento en caché de tokens.

Para obtener más información sobre el uso de OAuthPrompt, vea:

* [Información general sobre el flujo](~/bots/how-to/authentication/auth-flow-bot.md) de autenticación de bots describe cómo funciona la autenticación dentro de un bot en la aplicación en Teams. Esto muestra un flujo de autenticación no basado en web que se usa para bots Teams web, aplicaciones de escritorio y aplicaciones móviles.
* [La autenticación](~/bots/how-to/authentication/add-authentication.md) de bots describe cómo agregar la autenticación de OAuth al Teams bot.

## <a name="code-sample"></a>Ejemplo de código

proporciona un ejemplo de SDK de autenticación de bot v3.

| **Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Autenticación de bot | En este ejemplo se muestra cómo empezar con la autenticación en un bot para Microsoft Teams. | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Sso de pestaña, bot y mensajería (ME) | En este ejemplo se muestra SSO para Tab, Bot y ME: búsqueda, acción, linkunfurl. |  [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | No disponible |


## <a name="configure-the-identity-provider"></a>Configurar el proveedor de identidades

Independientemente del flujo de autenticación de la aplicación, configure el proveedor de identidades para que se comunique con la Teams aplicación. La mayoría de los ejemplos y tutoriales tratan principalmente con el uso de AAD como proveedor de identidades. Sin embargo, los conceptos se aplican independientemente del proveedor de identidades.

Para obtener más información, vea [configuring an identity provider](~/concepts/authentication/configure-identity-provider.md).
