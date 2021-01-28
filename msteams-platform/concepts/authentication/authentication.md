---
title: Autenticación de usuarios de aplicaciones
description: Describe la autenticación en Teams y cómo usarla en sus aplicaciones
ms.topic: conceptual
keywords: Autenticación de teams OAuth SSO AAD
ms.openlocfilehash: 6ddcd8a9e847d9216b7e2dcc12733a6cd413b48e
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014295"
---
# <a name="authenticating-users-in-microsoft-teams"></a>Autenticación de usuarios en Microsoft Teams

> [!Note]
> La autenticación basada en web en clientes móviles requiere la versión 1.4.1 o posterior del SDK de JavaScript de Teams.

Para que la aplicación tenga acceso a la información de usuario protegida por Azure Active Directory, así como a los datos de otros servicios como Facebook y Twitter, la aplicación tendrá que establecer una conexión de confianza con esos proveedores. Si la aplicación necesita usar las API de Microsoft Graph en el ámbito de usuario, también tendrá que autenticar al usuario para recuperar los tokens de autenticación adecuados.

En Microsoft Teams hay dos flujos de autenticación diferentes para que la aplicación aproveche las ventajas. Puede realizar un flujo de autenticación [](~/tabs/how-to/create-tab-pages/content-page.md) basado en web tradicional en una página de contenido incrustada en una pestaña, una página de configuración o un módulo de tareas. Si la aplicación contiene un bot de conversación, puedes usar el flujo de OAuthPrompt (y, opcionalmente, el servicio de token de Azure Bot Framework) para autenticar a un usuario como parte de una conversación.

## <a name="web-based-authentication-flow"></a>Flujo de autenticación basado en web

Necesitará usar el flujo de autenticación basado en web para las [pestañas](~/tabs/what-are-tabs.md)y puede elegir usarlo con [bots](~/bots/what-are-bots.md) de conversación o extensiones [de mensajería.](~/messaging-extensions/what-are-messaging-extensions.md) Usará el SDK de cliente [de JavaScript](/javascript/api/overview/msteams-client) de Microsoft Teams en una página de contenido web para habilitar la autenticación y, a continuación, insertar esa página de contenido en una pestaña, una página de configuración o un módulo de tareas. Si desea usar el flujo de autenticación basado en web con un bot de conversación, deberá usar un módulo de tareas [con un bot.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

* [El flujo de autenticación en las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) describe cómo funciona la autenticación de pestañas en Teams. Esto muestra un flujo de autenticación basado en web típico que se usa para las pestañas.
* [La autenticación de Azure AD en pestañas](~/tabs/how-to/authentication/auth-tab-AAD.md) describe cómo conectarse a Azure Active Directory desde dentro de una pestaña de la aplicación en Teams.
* [La autenticación silenciosa (Azure AD)](~/tabs/how-to/authentication/auth-silent-AAD.md) describe cómo reducir los mensajes de inicio de sesión o consentimiento en la aplicación con Azure Active Directory.
* Autenticación basada en web [en dotnet/C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) o [JavaScript/Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flujo de OAuthPrompt para bots de conversación

OAuthPrompt de Azure Bot Framework facilita la autenticación para las aplicaciones que usan bots de conversación. También puede aprovechar el servicio de token de Azure Bot Framework para ayudar con el almacenamiento en caché de tokens.

Para obtener más información sobre el uso de OAuthPrompt, vea:

* [Información general sobre el flujo de](~/bots/how-to/authentication/auth-flow-bot.md) autenticación de bots describe cómo funciona la autenticación dentro de un bot en su aplicación en Teams. Esto muestra un flujo de autenticación no basado en web que se usa para bots en todas las versiones de Teams (web, aplicación de escritorio y aplicaciones móviles)
* [Autenticación de bot](~/bots/how-to/authentication/add-authentication.md)
* Ejemplo de autenticación de bot (SDK v3) [en dotnet/C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) o [JavaScript/Node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth)

## <a name="configure-your-identity-provider"></a>Configurar el proveedor de identidades

Independientemente del flujo de autenticación que use la aplicación (es posible que incluso esté usando ambos), tendrá que configurar el proveedor de identidades para comunicarse con su aplicación de Teams. La mayoría de los ejemplos y tutoriales que encontrará aquí se centrarán principalmente en el uso de Azure Active Directory como proveedor de identidades. Sin embargo, los conceptos se aplican independientemente del proveedor de identidades que usará.

Para obtener más información, [vea la configuración de un proveedor de identidades](~/concepts/authentication/configure-identity-provider.md)
