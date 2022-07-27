---
title: Autenticación para bots mediante Azure Active Directory
description: Describe la autenticación de Azure AD en Teams y cómo usarla en los bots
keywords: bots de autenticación de teams en Azure AD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: 2b467f6a7b4678110dece3b54a67227df6beeaf7
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035166"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Autenticación de un usuario en un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Es posible que desee consumir muchos servicios dentro de la aplicación de Teams, y la mayoría de esos servicios requieren autenticación y autorización para obtener acceso. Los servicios incluyen Facebook, Twitter y Teams. Los usuarios de Teams tienen información de perfil de usuario almacenada en Azure Active Directory mediante Microsoft Graph. Este tema se centra en la autenticación mediante Azure AD para obtener acceso.
OAuth 2.0 es un estándar abierto para la autenticación usado por Azure Active Directory (Azure AD) y muchos otros proveedores de identidad. Comprender OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams y Azure AD. En los ejemplos siguientes se usa el flujo de concesión implícita de OAuth 2.0 para leer eventualmente la información de perfil del usuario de Azure AD y Microsoft Graph.

El flujo de autenticación descrito en este tema es similar a las pestañas, salvo que las pestañas pueden usar el flujo de autenticación basado en web y los bots requieren que la autenticación se controle desde el código. Los conceptos de este tema también serán útiles al implementar la autenticación desde la plataforma móvil.

Para obtener información general sobre el flujo de autenticación para bots, consulte el tema [Flujo de autenticación en bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

## <a name="configuring-identity-providers"></a>Configuración de proveedores de identidades

Consulte el tema [Configuración de proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para obtener pasos detallados sobre cómo configurar las direcciones URL de redireccionamiento de devolución de llamada de OAuth 2.0 al usar Azure Active Directory como proveedor de identidades.

## <a name="initiate-authentication-flow"></a>Iniciar el flujo de autenticación

El flujo de autenticación debe desencadenarse mediante una acción del usuario. No abra el elemento emergente de autenticación automáticamente, ya que podría desencadenar el bloqueador emergente del explorador y confundir al usuario.

## <a name="add-ui-to-start-authentication"></a>Agregar interfaz de usuario para iniciar la autenticación

Agregue la interfaz de usuario al bot para permitir que el usuario inicie sesión cuando sea necesario. Aquí se hace a partir de una tarjeta en miniatura, en TypeScript:

```typescript
// Show prompt of options
protected async promptForAction(session: builder.Session): Promise<void> {
    let msg = new builder.Message(session)
        .addAttachment(new builder.ThumbnailCard(session)
            .title(this.providerDisplayName)
            .buttons([
                 builder.CardAction.messageBack(session, "{}", "Sign in")
                     .text("SignIn")
                     .displayText("Sign in"),
                  builder.CardAction.messageBack(session, "{}", "Show profile")
                     .text("ShowProfile")
                     .displayText("Show profile"),
                  builder.CardAction.messageBack(session, "{}", "Sign out")
                     .text("SignOut")
                     .displayText("Sign out"),
            ]));
    session.send(msg);
}
```

Se han agregado tres botones a la tarjeta principal: Iniciar sesión, Mostrar perfil y Cerrar sesión.

## <a name="sign-the-user-in"></a>Inicio de sesión del usuario

Debido a la validación que se debe realizar por motivos de seguridad y la compatibilidad con las versiones móviles de Teams, el código no se muestra aquí, pero [este es un ejemplo del código que inicia el proceso cuando el usuario presiona el botón Iniciar sesión.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)

La validación y la compatibilidad móvil se explican en el tema [Flujo de autenticación en bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

Asegúrese de agregar el dominio de la dirección URL de redireccionamiento de autenticación a la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) sección del manifiesto. Si no inicia sesión, no aparecerá el elemento emergente.

## <a name="showing-user-profile-information"></a>Mostrar información de perfil de usuario

Aunque la obtención de un token de acceso es difícil debido a todas las transiciones entre diferentes sitios web y los problemas de seguridad que se deben solucionar, una vez que tenga un token, la obtención de información de Azure Active Directory es sencilla. El bot realiza una llamada al punto de conexión de `me` Graph con el token de acceso. Graph responde con la información del usuario de la persona que inició sesión. La información de la respuesta se usa para construir una tarjeta de bot y enviarla.

```typescript
// Show user profile
protected async showUserProfile(session: builder.Session): Promise<void> {
    let azureADApi = this.authProvider as AzureADv1Provider;
    let userToken = this.getUserToken(session);

    if (userToken) {
        let profile = await azureADApi.getProfileAsync(userToken.accessToken);
        let profileCard = new builder.ThumbnailCard()
            .title(profile.displayName)
            .subtitle(profile.mail)
            .text(`${profile.jobTitle}<br/> ${profile.officeLocation}`);
        session.send(new builder.Message().addAttachment(profileCard));
    } else {
        session.send("Please sign in to AzureAD so I can access your profile.");
    }

    await this.promptForAction(session);
}

// Helper function to make the Graph API call
public async getProfileAsync(accessToken: string): Promise<any> {
    let options = {
        url: "https://graph.microsoft.com/v1.0/me",
        json: true,
        headers: {
            "Authorization": `Bearer ${accessToken}`,
        },
    };
    return await request.get(options);
}
```

Si el usuario no ha iniciado sesión, se le pedirá que lo haga.

## <a name="sign-the-user-out"></a>Cerrar la sesión del usuario

```typescript
// Handle user logout request
private async handleLogout(session: builder.Session): Promise<void> {
    if (!utils.getUserToken(session, this.providerName)) {
        session.send(`You're already signed out of ${this.providerDisplayName}.`);
    } else {
        utils.setUserToken(session, this.providerName, null);
        session.send(`You're now signed out of ${this.providerDisplayName}.`);
    }

    await this.promptForAction(session);
}
```

## <a name="other-samples"></a>Otros ejemplos

Para obtener código de ejemplo que muestra el proceso de autenticación del bot, consulte:

* [Ejemplo de autenticación de bot de Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
