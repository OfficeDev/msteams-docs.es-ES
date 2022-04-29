---
title: Autenticación de usuarios de aplicaciones
description: Describe la autenticación en Teams y cómo usarla en las aplicaciones
ms.topic: conceptual
ms.localizationpriority: high
keywords: autenticación de teams Microsoft Azure Active Directory SSO de OAuth (Azure AD)
ms.openlocfilehash: f5aecf2791d03795229d3b37c5fc8784de992326
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111405"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Autenticar usuarios en Microsoft Teams

> [!Note]
> La autenticación basada en web en clientes móviles requiere la versión 1.4.1 o posterior del SDK de cliente de JavaScript de Teams.

Para acceder a la información de usuario protegida por Azure AD y para acceder a datos de servicios como Facebook y Twitter, la aplicación establece una conexión de confianza con esos proveedores. Si la aplicación usa Microsoft Graph API en el ámbito de usuario, autentique al usuario para recuperar los tokens de autenticación adecuados.

En Microsoft Teams, hay dos flujos de autenticación diferentes para la aplicación. Realice un flujo de autenticación tradicional basado en web en una [página de contenido](~/tabs/how-to/create-tab-pages/content-page.md) incrustada en una pestaña, una página de configuración o un módulo de tareas. Si la aplicación contiene un bot de conversación, use el flujo de OAuthPrompt y, opcionalmente, el servicio de tokens de Azure Bot Framework para autenticar a un usuario como parte de una conversación.

## <a name="web-based-authentication-flow"></a>Flujo de autenticación basado en web

Use el flujo de autenticación basado en web para [pestañas](~/tabs/what-are-tabs.md) y elija usarlo con [bots de conversación](~/bots/what-are-bots.md) o [extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md). Use el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client) en una página de contenido web para habilitar la autenticación. Después de habilitar la autenticación, inserte la página de contenido en una pestaña, una página de configuración o un módulo de tareas. Para obtener más información sobre el flujo de autenticación basado en web, consulte:

* [Agregar autenticación al bot de Teams](~/bots/how-to/authentication/add-authentication.md) describe cómo usar el flujo de autenticación basado en web con un bot conversacional.
* [Flujo de autenticación en pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) describe cómo funciona la autenticación de pestañas en Teams. Esto muestra un flujo de autenticación basado en web típico que se usa para las pestañas.
* [Azure AD autenticación en pestañas](~/tabs/how-to/authentication/auth-tab-AAD.md) describe cómo conectarse a Azure AD desde una pestaña de la aplicación en Teams.
* [Autenticación silenciosa de Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md) describe cómo reducir las solicitudes de inicio de sesión o consentimiento en la aplicación mediante Azure AD.
* [.Net o C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) o [JavaScript o Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) proporciona ejemplos de autenticación basada en web.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flujo de OAuthPrompt para bots de conversación

OAuthPrompt de Azure Bot Framework facilita la autenticación para las aplicaciones que usan bots de conversación. Use el servicio de token de Azure Bot Framework para ayudar con el almacenamiento en caché de tokens.

Para obtener más información sobre el uso de OAuthPrompt, consulte:

* [Vista general del flujo de autenticación de bots](~/bots/how-to/authentication/auth-flow-bot.md) describe cómo funciona la autenticación dentro de un bot en la aplicación en Teams. Esto muestra un flujo de autenticación no basado en web que se usa para bots en Teams web, aplicación de escritorio y aplicaciones móviles.
* [Autenticación](~/bots/how-to/authentication/add-authentication.md) describe cómo agregar la autenticación de OAuth al bot de Teams.

## <a name="code-sample"></a>Ejemplo de código

proporciona un ejemplo de SDK de autenticación de bot v3.

| **Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Autenticación del bot | En este ejemplo se muestra cómo empezar a usar la autenticación en un bot para Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Inicio de sesión único (SSO) de pestaña, bot y extensión de mensajes (ME) | En este ejemplo se muestra SSO para pestaña, Bot y ME: búsqueda, acción, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | No disponible |

## <a name="configure-the-identity-provider"></a>Configurar el proveedor de identidades

Independientemente del flujo de autenticación de la aplicación, configure el proveedor de identidades para comunicarse con la aplicación de Teams. La mayoría de los ejemplos y recorridos se centran principalmente en el uso de Azure AD como proveedor de identidades. Sin embargo, los conceptos se aplican independientemente del proveedor de identidades.

Para obtener más información, vea [configurar un proveedor de identidades](~/concepts/authentication/configure-identity-provider.md).

## <a name="third-party-cookies-on-ios"></a>Cookies de terceros en iOS

Después de la actualización de iOS 14, Apple ha bloqueado el acceso a esta [cookie de terceros](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) para todas las aplicaciones de forma predeterminada. Por lo tanto, las aplicaciones que aprovechan las cookies de terceros para la autenticación en sus pestañas de canal o chat y las aplicaciones personales no podrán completar sus flujos de trabajo de autenticación en clientes iOS de Teams. Para cumplir con los requisitos de privacidad y seguridad, debe pasar a un sistema basado en tokens o usar cookies propias para los flujos de trabajo de autenticación de usuario.

## <a name="see-also"></a>Vea también

* [Flujo de autenticación de Microsoft Teams para pestañas](~/tabs/how-to/authentication/auth-flow-tab.md)
* [Compatibilidad con inicio de sesión único para bots](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [Agregar autenticación a la extensión de mensaje](~/messaging-extensions/how-to/add-authentication.md)
