---
title: Flujo de autenticación de Microsoft Teams para bots
description: En este módulo, aprenderá a realizar el flujo de autenticación para bots en Microsoft Teams y su ejemplo de código.
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: de263a75b7b8077570dca2f94bf6937d9d339bbe
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143238"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Flujo de autenticación para bots en Microsoft Teams

OAuth 2.0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory y otros muchos proveedores de identidad. Se requiere una comprensión básica de OAuth 2.0 para trabajar con la autenticación en Teams; [aquí hay introducción](https://aaronparecki.com/oauth-2-simplified/) más fácil de seguir que la [especificación formal](https://oauth.net/2/). El flujo de autenticación para pestañas y bots es un poco diferente: las pestañas son similares a los sitios web para que puedan usar OAuth 2.0 directamente, mientras que los bots no son y deben hacer algunas cosas de forma diferente, pero los conceptos básicos son idénticos.

Consulte el repositorio de GitHub de [ejemplos de autenticación de Microsoft Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) para ver un ejemplo del flujo de autenticación para bots usando Node.js y el [tipo de concesión de código de autorización OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/).

![Diagrama de secuencia de autenticación de bots](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. El usuario envía un mensaje al bot.
2. El bot determina si el usuario necesita iniciar sesión.
   En este ejemplo, el bot almacena el token de acceso en su almacén de datos de usuario. Pide al usuario que inicie sesión si no tiene un token validado para el proveedor de identidad seleccionado. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. El bot construye la dirección URL a la página de inicio del flujo de autenticación y envía una tarjeta al usuario con una acción `signin`. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Al igual que sucede con otros flujos de autenticación de aplicación en Teams, la página de inicio debe estar en un dominio que esté en su lista `validDomains` y en el mismo dominio que la página de redireccionamiento tras el inicio de sesión.
    > [!IMPORTANT]
    > El flujo de concesión de código de autorización de OAuth 2.0 llama a un parámetro `state` en la solicitud de autenticación que contiene un token de sesión único para prevenir un ataque de [falsificación de solicitud entre sitios](https://en.wikipedia.org/wiki/Cross-site_request_forgery). En el ejemplo se usa un GUID generado aleatoriamente.
4. Cuando el usuario selecciona el botón de *inicio de sesión*, Teams abre una ventana emergente y va a la página de inicio.
   > [!NOTE]
   > El tamaño de la ventana emergente puede controlarse mediante los parámetros width y height de la cadena de consulta en la URL. Por ejemplo, si añade width=600 y height=600, el tamaño de la ventana emergente es de 600 x 600 píxeles. El tamaño real de la ventana emergente se limita a un porcentaje del tamaño de la ventana principal Teams. Si la ventana Teams es pequeña, la ventana emergente es menor que las dimensiones especificadas.

5. La página de inicio redirige al usuario al punto de conexión `authorize` del proveedor de identidad. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. En el sitio web del proveedor, el usuario inicia sesión y concede acceso al bot.
7. El proveedor lleva al usuario a la página de redirección de OAuth del bot con un código de autorización.
8. El bot canjea el código de autorización por un token de acceso y asocia **provisionalmente** el token al usuario que inició el flujo de inicio de sesión. En adelante llamaremos a esto *token provisional*.
    * En el ejemplo, el bot asocia el valor del parámetro `state` con la Id. del usuario que ha iniciado el proceso de identificación para poder compararlo más tarde con el valor `state` devuelto por el proveedor de identidad. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT]
      > El bot almacena el token que recibe del proveedor de identidad y lo asocia con un usuario determinado, pero se marca como “pendiente de validación”.
    * El token provisional no se puede usar sin una validación adicional.
      1. **Valide lo que se recibió del proveedor de identidad.** El valor del parámetro `state` debe compararse con lo que se guardó anteriormente.
      1. **Valide lo que se recibió de Teams.** Se realiza una validación de [autenticación en dos pasos](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) para comprobar que el usuario que autorizó el bot con el proveedor de identidad es el mismo usuario que está chateando con el bot. Esto protege contra los ataques de [intermediario](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) y [phishing](https://en.wikipedia.org/wiki/Phishing). El bot genera un código de verificación asociado al usuario y lo almacena. El código de verificación se envía automáticamente por Teams como se describe a continuación. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. La devolución de llamada de OAuth genera una página que llama a `notifySuccess("<verification code>")`. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams cierra la ventana emergente y envía el `<verification code>` enviado a `notifySuccess()` de vuelta al bot. El bot recibe un mensaje de [invoke](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) con `name = signin/verifyState`.
11. El bot compara el código de verificación entrante con el código de verificación almacenado con el token provisional del usuario. ([Ver código](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. Si coinciden, el bot marca el token como validado y listo para su uso. De lo contrario, se produce un error en el flujo de autenticación y el bot elimina el token provisional.

    > [!NOTE]
    > Si experimenta problemas con la autenticación en dispositivos móviles, asegúrese de que el SDK de JavaScript esté actualizado a la versión 1.4.1 o posterior.

## <a name="code-sample"></a>Ejemplo de código

Código de ejemplo que muestra el proceso de autenticación del bot:

| **Ejemplo de nombre** | **Descripción** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Autenticación de Teams | En este ejemplo, se muestra la autenticación en las aplicaciones de Microsoft Teams. | [View](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| Autenticación del bot | En este ejemplo se muestra cómo usar la autenticación para un bot que se ejecuta en Microsoft Teams | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>Consulte también

[Agregar autenticación al bot de Teams](add-authentication.md)
