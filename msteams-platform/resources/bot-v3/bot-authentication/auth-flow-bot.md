---
title: Flujo de autenticación para bots
description: Describe el flujo de autenticación en bots.
keywords: bots de flujo de autenticación de Teams
ms.date: 03/01/2018
ms.openlocfilehash: 5230a94b23f9042d9d7753b52467fba5b2fec89e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676205"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>Flujo de autenticación de Microsoft Teams para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

OAuth 2,0 es un estándar abierto para la autenticación y autorización usado por Azure AD y muchos otros proveedores de identidades. Una descripción básica de OAuth 2,0 es un requisito previo para trabajar con la autenticación en Microsoft Teams. [esta es una buena introducción](https://aaronparecki.com/oauth-2-simplified/) que es más fácil de seguir que la [especificación formal](https://oauth.net/2/). El flujo de autenticación para fichas y bots es un poco diferente porque las pestañas son muy similares a los sitios web para que puedan usar OAuth 2,0 directamente, y los bots no son y deben hacer algunas cosas de manera diferente, pero los conceptos básicos son idénticos.

Consulte el repositorio de GitHub [ejemplo de autenticación de Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) para obtener un ejemplo que muestra el flujo de autenticación para bots mediante el uso de nodos con el [tipo de concesión de código de autorización OAuth 2,0](https://oauth.net/2/grant-types/authorization-code/).

![Diagrama de secuencia de autenticación de bot](~/assets/images/authentication/bot_auth_sequence_diagram.png)

1. El usuario envía un mensaje al bot.
2. El bot determina si el usuario tiene que iniciar sesión.
    * En este ejemplo, el bot almacena el token de acceso en su almacén de datos de usuario. Pide al usuario que inicie sesión si no tiene un token validado para el proveedor de identidad seleccionado. ([Código de vista](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. El bot crea la dirección URL de la página de inicio del flujo de autenticación y envía una tarjeta al usuario con una `signin` acción. ([Código de vista](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Al igual que otros flujos de autenticación de aplicaciones en Microsoft Teams, la página de inicio debe estar `validDomains` en un dominio de la lista y en el mismo dominio que la página de redireccionamiento posterior al inicio de sesión.
    * **Importante**: el flujo de concesión de código de autorización de OAuth `state` 2,0 llama a un parámetro en la solicitud de autenticación que contiene un token de sesión único para evitar un [ataque de falsificación de solicitud entre sitios](https://en.wikipedia.org/wiki/Cross-site_request_forgery). En el ejemplo se usa un GUID generado aleatoriamente.
4. Cuando el usuario hace clic en el botón *iniciar sesión* , Microsoft Teams abre una ventana emergente y la desplaza a la página de inicio.
5. La página de inicio redirige al usuario al punto de conexión del `authorize` proveedor de identidades. ([Código de vista](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. En el sitio del proveedor, el usuario inicia sesión y concede acceso al bot.
7. El proveedor lleva al usuario a la página de redireccionamiento de OAuth del bot, con un código de autorización.
8. El bot canjea el código de autorización para un token de acceso y, de forma **provisional** , asocia el token con el usuario que inició el flujo de inicio de sesión. A continuación, se denomina un *token provisional*.
    * En el ejemplo, el bot asocia el valor del `state` parámetro con el identificador del usuario que inició el proceso de inicio de sesión para que más adelante pueda hacerlo con el `state` valor devuelto por el proveedor de identidad. ([Código de vista](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **Importante**: el bot almacena el token que recibe del proveedor de identidad y lo asocia a un usuario específico, pero se marca como "pendiente de validación". El token provisional no se puede usar todavía: debe validarse aún más: 
      1. **Validar lo que se recibe del proveedor de identidades.** El valor del `state` parámetro debe confirmarse con respecto a lo que se guardó anteriormente. 
      1. **Validar lo que se recibe de Microsoft Teams.** Se realiza una validación de [autenticación en dos pasos](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) para garantizar que el usuario que ha autorizado el bot con el proveedor de identidades es el mismo usuario que está conversando con el bot. Esto protege contra ataques [de "Man in the Middle](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) " y de [suplantación de identidad (phishing)](https://en.wikipedia.org/wiki/Phishing) . El bot genera un código de comprobación y lo almacena, asociado al usuario. Los equipos envían automáticamente el código de comprobación como se describe más adelante en los pasos 9 y 10. ([Código de vista](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. La devolución de llamada de OAuth representa una página `notifySuccess("<verification code>")`que llama. ([Código de vista](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams cierra el elemento emergente y envía `<verification code>` el remitente `notifySuccess()` al bot. El bot recibe un mensaje de [invocación](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) con `name = signin/verifyState`.
11. El bot comprueba el código de comprobación entrante con el código de comprobación almacenado con el token provisional del usuario. ([Código de vista](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. Si coinciden, el bot marca el token como validado y listo para su uso. De lo contrario, se produce un error en el flujo de autenticación y el bot elimina el token provisional.

> [!Note]
> Si experimenta problemas con la autenticación en dispositivos móviles, asegúrese de que el SDK de JavaScript se actualiza a la versión 1.4.1 o posterior.

## <a name="samples"></a>Ejemplos

Para ver el código de ejemplo que muestra el proceso de autenticación de bot, consulte:

* [Ejemplo de autenticación de bot de Microsoft Teams (nodo)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>Más detalles

Para ver los tutoriales de implementación detallados para la autenticación de bot dirigidas a Azure Active Directory, vea:

* [Autenticar a un usuario en un bot de Microsoft Teams](~/resources/bot-v3/bot-authentication/auth-bot-AAD.md)
