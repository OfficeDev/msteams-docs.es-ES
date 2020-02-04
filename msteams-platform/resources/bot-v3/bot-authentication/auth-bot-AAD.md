---
title: Autenticación para bots con Azure Active Directory
description: Describe la autenticación de Azure AD en Microsoft Teams y cómo usarla en los bots.
keywords: bots de autenticación de Teams AAD
ms.date: 03/01/2018
ms.openlocfilehash: 268af02c51b21b65214bce4673b54ac564a125ae
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676016"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Autenticar a un usuario en un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Hay muchos servicios que puede que desee consumir dentro de la aplicación de Teams y la mayoría de esos servicios requieren autenticación y autorización para obtener acceso al servicio. Los servicios incluyen Facebook, Twitter y los equipos del curso. Los usuarios de Microsoft Teams tienen información de Perfil de usuario almacenada en Azure Active Directory (Azure AD) con Microsoft Graph. Este artículo se centra en la autenticación mediante Azure AD para obtener acceso a esta información.

OAuth 2,0 es un estándar abierto para la autenticación que usa Azure AD y muchos otros proveedores de servicios. La comprensión de OAuth 2,0 es un requisito previo para trabajar con la autenticación en Microsoft Teams y Azure AD. En los ejemplos siguientes se usa el flujo de concesión implícita de OAuth 2,0 con el objetivo de leer eventualmente la información de perfil del usuario de Azure AD y Microsoft Graph.

El flujo de autenticación que se describe en este artículo es muy similar al de las pestañas, excepto en que las pestañas pueden usar el flujo de autenticación basada en Web, y los bots requieren autenticación para poder controlarlos desde el código. Los conceptos de este artículo también serán útiles al implementar la autenticación desde la plataforma móvil.

Para obtener información general sobre el flujo de autenticación para bots, vea el tema sobre el [flujo de autenticación en bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

## <a name="configuring-identity-providers"></a>Configuración de proveedores de identidad

Vea el tema [configuración de proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para obtener pasos detallados sobre cómo configurar las direcciones URL de redireccionamiento de devolución de llamada de OAuth 2,0 al usar Azure Active Directory como proveedor de identidades.

## <a name="initiate-authentication-flow"></a>Iniciar el flujo de autenticación

El flujo de autenticación debe activarse mediante una acción del usuario. No debe abrir la ventana emergente de autenticación automáticamente porque es probable que desencadene el bloqueador de ventanas emergentes del explorador, así como confundir al usuario.

## <a name="add-ui-to-start-authentication"></a>Agregar la interfaz de usuario para iniciar la autenticación

Agregue la interfaz de usuario al bot para permitir que el usuario inicie sesión cuando sea necesario. Aquí se realiza desde una tarjeta de miniaturas, en TypeScript:

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

Se han agregado tres botones a la tarjeta Hero: iniciar sesión, Mostrar perfil y cerrar sesión.

## <a name="sign-the-user-in"></a>Iniciar sesión del usuario

Debido a la validación que debe realizarse por motivos de seguridad y por la compatibilidad con las versiones móviles de Teams, el código no se muestra aquí, pero [este es un ejemplo del código que inicia el proceso cuando el usuario presiona el botón de inicio de sesión.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).

La validación y la compatibilidad con móviles se explican en el tema sobre el [flujo de autenticación en bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

Asegúrese de agregar el dominio de la dirección URL de redireccionamiento de [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) autenticación a la sección del manifiesto. Si no lo hace, el elemento emergente de inicio de sesión no aparecerá.

## <a name="showing-user-profile-information"></a>Mostrar información de Perfil de usuario

Aunque es difícil obtener un token de acceso debido a todas las transiciones entre sitios web y los problemas de seguridad que se deben solucionar, una vez que se tiene un token, obtener información de Azure Active Directory es sencillo. El bot realiza una llamada al punto `me` de conexión del grafo con el token de acceso. Graph responde con la información de usuario de la persona que inició la sesión. La información de la respuesta se usa para crear una tarjeta de Bot y enviarla.

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

Para ver el código de ejemplo que muestra el proceso de autenticación de bot, consulte:

* [Ejemplo de autenticación de bot de Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
