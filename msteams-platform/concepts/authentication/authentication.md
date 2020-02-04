---
title: Autenticar a un usuario en Microsoft Teams
description: Describe la autenticación en Microsoft Teams y cómo usarla en las aplicaciones.
keywords: autenticación de Teams SSO de OAuth para AAD
ms.openlocfilehash: d3ae57d9937c6794fb743b44ca8210a5afd181bf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675829"
---
# <a name="authentication-in-teams"></a>Autenticación en Microsoft Teams

> [!Note]
> La autenticación basada en Web en clientes móviles requiere la versión 1.4.1 o posterior del SDK de Teams para JavaScript.

Para que la aplicación tenga acceso a la información de usuario protegida con Azure Active Directory, así como el acceso a datos de otros servicios como Facebook y Twitter, la aplicación tendrá que establecer una conexión de confianza con estos proveedores. Si la aplicación necesita usar las API de Microsoft Graph en el ámbito de usuario, también necesitará autenticar al usuario para recuperar los tokens de autenticación adecuados.

En Microsoft Teams hay dos flujos de autenticación diferentes para que la aplicación aproveche. Puede realizar un flujo de autenticación tradicional basado en Web en una [Página de contenido](~/tabs/how-to/create-tab-pages/content-page.md) incrustada en una pestaña, una página de configuración o un módulo de tareas. Si la aplicación contiene un bot conversante, puede usar el flujo OAuthPrompt (y, opcionalmente, el servicio de token de Azure bot Framework) para autenticar a un usuario como parte de una conversación.

## <a name="web-based-authentication-flow"></a>Flujo de autenticación basada en Web

Deberá usar el flujo de autenticación basada en web para las [pestañas](~/tabs/what-are-tabs.md)y puede elegir usarla con [bots de conversación](~/bots/what-are-bots.md) o con extensiones de [Mensajería](~/messaging-extensions/what-are-messaging-extensions.md). Usará el SDK del [cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client) en una página de contenido web para habilitar la autenticación y, a continuación, insertar esa página de contenido en una pestaña, una página de configuración o un módulo de tareas. Si desea usar el flujo de autenticación basado en Web con un bot conversador, deberá [usar un módulo de tareas con un bot](~/task-modules-and-cards/task-modules/task-modules-bots.md).

* [Flujo de autenticación en las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) describe cómo funciona la autenticación de pestañas en Microsoft Teams. Muestra un flujo típico de autenticación basada en Web que se usa para las pestañas.
* [Autenticación de Azure ad en pestañas](~/tabs/how-to/authentication/auth-tab-AAD.md) se describe cómo conectarse a Azure Active Directory desde una pestaña de la aplicación en Microsoft Teams.
* [Autenticación silenciosa (Azure ad)](~/tabs/how-to/authentication/auth-silent-AAD.md) describe cómo reducir los mensajes de inicio de sesión/consentimiento en la aplicación con Azure Active Directory.
* Autenticación basada en Web en [dotnet/C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) o [JavaScript/node. js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flujo de OAuthPrompt para bots de conversación

El OAuthPrompt de Azure bot Framework facilita la autenticación para las aplicaciones que usan bots de conversación. Puede aprovechar el servicio de tokens de Azure bot Framework para ayudar también con el almacenamiento en caché de tokens.

Para obtener más información sobre el uso de OAuthPrompt, vea:

* [Información general sobre el flujo de autenticación de bot](~/bots/how-to/authentication/auth-flow-bot.md) describe cómo funciona la autenticación dentro de un bot en la aplicación en Teams. Muestra un flujo de autenticación no basado en Web que se usa para bots en todas las versiones de Teams (Web, aplicación de escritorio y aplicaciones móviles)
* [Autenticación de bot](~/bots/how-to/authentication/add-authentication.md)
* Ejemplo de autenticación de Bot (SDK de V3) en [dotnet/C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) o [JavaScript/node. js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth)

## <a name="configure-your-identity-provider"></a>Configurar el proveedor de identidades

Independientemente del flujo de autenticación que use (puede que incluso esté usando ambos), deberá configurar su proveedor de identidad para comunicarse con la aplicación de Teams. La mayoría de los ejemplos y tutoriales que encontrará aquí se ocuparán principalmente del uso de Azure Active Directory como proveedor de identidades. Sin embargo, los conceptos se aplican independientemente del proveedor de identidad que vaya a usar.

Para obtener más información, vea [Configuring an Identity Provider](~/concepts/authentication/configure-identity-provider.md) .
