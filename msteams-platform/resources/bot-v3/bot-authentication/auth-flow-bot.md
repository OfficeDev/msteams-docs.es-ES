---
title: Flujo de autenticación para bots
description: Describe el flujo de autenticación en bots
keywords: bots de flujo de autenticación de teams
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: fe7e528be98a0b58334535952327b6026b30a87d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019807"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>Microsoft Teams de autenticación para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

OAuth 2.0 es un estándar abierto para la autenticación y autorización que usa Azure AD y muchos otros proveedores de identidades. Un conocimiento básico de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams; [esta es una buena introducción](https://aaronparecki.com/oauth-2-simplified/) que es más fácil de seguir que la [especificación formal](https://oauth.net/2/). El flujo de autenticación para pestañas y bots es un poco diferente porque las pestañas son muy similares a los sitios web para que puedan usar OAuth 2.0 directamente, y los bots no son y deben hacer algunas cosas de forma diferente, pero los conceptos básicos son idénticos.

Consulte el ejemplo Microsoft Teams [](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) de autenticación de GitHub de repositorio de GitHub para ver un ejemplo que muestra el flujo de autenticación para bots que usan Node mediante el tipo de concesión de código de autorización [de OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/).

![Diagrama de secuencia de autenticación de bot](~/assets/images/authentication/bot_auth_sequence_diagram.png)

1. El usuario envía un mensaje al bot.
2. El bot determina si el usuario debe iniciar sesión.
    * En este ejemplo, el bot almacena el token de acceso en su almacén de datos de usuario. Se pide al usuario que inicie sesión si no tiene un token validado para el proveedor de identidades seleccionado. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. El bot construye la dirección URL en la página de inicio del flujo de autenticación y envía una tarjeta al usuario con una `signin` acción. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Al igual que otros flujos de autenticación de aplicación en Teams, la página de inicio debe estar en un dominio que esté en la lista y en el mismo dominio que la página de redireccionamiento posterior `validDomains` al inicio de sesión.
    * **IMPORTANTE:** El flujo de concesión de código de autorización de OAuth 2.0 llama a un parámetro de la solicitud de autenticación que contiene un token de sesión único para evitar un ataque de falsificación de solicitudes entre `state` [sitios](https://en.wikipedia.org/wiki/Cross-site_request_forgery). En el ejemplo se usa un GUID generado aleatoriamente.
4. Cuando el usuario hace clic en el botón *de* inicio de sesión, Teams abre una ventana emergente y la navega a la página de inicio.
5. La página de inicio redirige al usuario al extremo del proveedor de `authorize` identidades. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. En el sitio del proveedor, el usuario inicia sesión y concede acceso al bot.
7. El proveedor lleva al usuario a la página de redireccionamiento de OAuth del bot, con un código de autorización.
8. El bot canjea el código de autorización de un token de acceso y **asocia provisionalmente** el token con el usuario que inició el flujo de inicio de sesión. A continuación, le llamamos un *token provisional*.
    * En el ejemplo, el bot asocia el valor del parámetro con el identificador del usuario que inició el proceso de inicio de sesión para que posteriormente pueda coincidir con el valor devuelto por el proveedor de `state` `state` identidades. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **IMPORTANTE:** el bot almacena el token que recibe del proveedor de identidades y lo asocia con un usuario específico, pero se marca como "validación pendiente". El token provisional no se puede usar todavía: debe validarse aún más: 
      1. **Valide lo que se recibe del proveedor de identidades.** El valor del `state` parámetro debe confirmarse con respecto a lo que se guardó anteriormente. 
      1. **Valide lo que se recibe de Teams.** Se [realiza una validación de](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) autenticación en dos pasos para garantizar que el usuario que autorizó el bot con el proveedor de identidades sea el mismo usuario que está chateando con el bot. Esto protege contra ataques de suplantación de identidad [(phishing) y](https://en.wikipedia.org/wiki/Phishing) de [man-in-the-middle.](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) El bot genera un código de verificación y lo almacena, asociado con el usuario. El código de verificación se envía automáticamente Teams como se describe a continuación en los pasos 9 y 10. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. La devolución de llamada de OAuth representa una página que llama a `notifySuccess("<verification code>")` . ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams cierra el elemento emergente y envía el `<verification code>` enviado `notifySuccess()` al bot. El bot recibe un [mensaje de invocación](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) con `name = signin/verifyState` .
11. El bot comprueba el código de comprobación entrante con el código de verificación almacenado con el token provisional del usuario. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. Si coinciden, el bot marca el token como validado y listo para su uso. De lo contrario, se produce un error en el flujo de autenticación y el bot elimina el token provisional.

> [!Note]
> Si tienes problemas con la autenticación en dispositivos móviles, asegúrate de que el SDK de Javascript se actualice a la versión 1.4.1 o posterior.

## <a name="samples"></a>Ejemplos

Para ver el código de ejemplo que muestra el proceso de autenticación del bot, vea:

* [Microsoft Teams ejemplo de autenticación de bots (Node)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>Más detalles

Para obtener tutoriales de implementación detallados para la autenticación de bots Azure Active Directory vea:

* [Autenticar un usuario en un bot de Microsoft Teams de autenticación](~/resources/bot-v3/bot-authentication/auth-bot-AAD.md)
