---
title: Flujo de autenticación para bots
description: Describe el flujo de autenticación en bots
keywords: bots de flujo de autenticación de Teams
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: 4930edcef81fca60f45ecdfd9bab863eb4524753
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757209"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>Microsoft Teams flujo de autenticación para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

OAuth 2.0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory (Azure AD) y otros muchos proveedores de identidad. Se requiere una comprensión básica de OAuth 2.0 para trabajar con la autenticación en Teams; [aquí hay introducción](https://aaronparecki.com/oauth-2-simplified/) más fácil de seguir que la [especificación formal](https://oauth.net/2/). El flujo de autenticación para pestañas y bots es diferente porque las pestañas son similares a los sitios web para que puedan usar OAuth 2.0 directamente, y los bots no son y deben hacer algunas cosas de forma diferente, pero los conceptos básicos son idénticos.

Consulte el repositorio de GitHub [Microsoft Teams ejemplo de autenticación](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) para obtener un ejemplo que muestre el flujo de autenticación para bots que usan Node mediante el [tipo de concesión de código de autorización de OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/).

![Diagrama de secuencia de autenticación de bots](~/assets/images/authentication/bot_auth_sequence_diagram.png)

1. El usuario envía un mensaje al bot.
2. El bot determina si el usuario necesita iniciar sesión.
    * En este ejemplo, el bot almacena el token de acceso en su almacén de datos de usuario. Pide al usuario que inicie sesión si no tiene un token validado para el proveedor de identidades seleccionado. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. El bot construye la dirección URL a la página de inicio del flujo de autenticación y envía una tarjeta al usuario con una acción `signin`. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Al igual que otros flujos de autenticación de aplicación en Teams, la página de inicio debe estar en un dominio que esté en la `validDomains` lista y en el mismo dominio que la página de redirección posterior al inicio de sesión.
    * **IMPORTANTE**: El flujo de concesión de código de autorización de OAuth 2.0 llama a un `state` parámetro en la solicitud de autenticación, que contiene un token de sesión único para evitar un [ataque de falsificación de solicitud entre sitios](https://en.wikipedia.org/wiki/Cross-site_request_forgery). En el ejemplo se usa un GUID generado aleatoriamente.
4. Cuando el usuario selecciona el botón *de inicio de sesión*, Teams abre una ventana emergente y la desplaza a la página de inicio.
5. La página de inicio redirige al usuario al punto de conexión `authorize` del proveedor de identidad. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. En el sitio web del proveedor, el usuario inicia sesión y concede acceso al bot.
7. El proveedor lleva al usuario a la página de redirección de OAuth del bot, con un código de autorización.
8. El bot canjea el código de autorización por un token de acceso y asocia **provisionalmente** el token al usuario que inició el flujo de inicio de sesión. En adelante llamaremos a esto *token provisional*.
    * En el ejemplo, el bot asocia el valor del `state` parámetro con el identificador del usuario que inició el proceso de inicio de sesión para que pueda coincidir más adelante con el `state` valor devuelto por el proveedor de identidades. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **IMPORTANTE**: El bot almacena el token que recibe del proveedor de identidades y lo asocia a un usuario específico, pero se marca como "validación pendiente". Todavía no se puede usar el token provisional: debe validarse aún más:
      1. **Valide lo que se recibió del proveedor de identidad.** El valor del parámetro `state` debe compararse con lo que se guardó anteriormente.
      1. **Valide lo que se recibió de Teams.** Se realiza una validación de [autenticación en dos pasos](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) para comprobar que el usuario que autorizó el bot con el proveedor de identidad es el mismo usuario que está chateando con el bot. Esto protege contra los ataques de [intermediario](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) y [phishing](https://en.wikipedia.org/wiki/Phishing). El bot genera un código de verificación asociado al usuario y lo almacena. El código de verificación se envía automáticamente por Teams como se describe a continuación en los pasos 9 y 10. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. La devolución de llamada de OAuth genera una página que llama a `notifySuccess("<verification code>")`. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams cierra el elemento emergente y envía el `<verification code>` objeto enviado al `notifySuccess()` bot. El bot recibe un mensaje de [invoke](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) con `name = signin/verifyState`.
11. El bot compara el código de verificación entrante con el código de verificación almacenado con el token provisional del usuario. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. Si coinciden, el bot marca el token como validado y listo para su uso. De lo contrario, se produce un error en el flujo de autenticación y el bot elimina el token provisional.

> [!Note]
> Si experimenta problemas con la autenticación en dispositivos móviles, asegúrese de que el SDK de Javascript está actualizado a la versión 1.4.1 o posterior.

## <a name="samples"></a>Muestras

Para obtener código de ejemplo que muestra el proceso de autenticación del bot, consulte:

* [Microsoft Teams ejemplo de autenticación de bot (Node)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>Más detalles

Para ver tutoriales detallados de implementación para la autenticación de bots destinada a Azure Active Directory, consulte:

* [Autenticación de un usuario en un bot de Microsoft Teams](~/resources/bot-v3/bot-authentication/auth-bot-AAD.md)
