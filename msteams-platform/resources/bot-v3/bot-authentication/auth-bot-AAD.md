---
title: Autenticación para bots que usan Azure Active Directory
description: Describe la autenticación de Azure AD en Teams y cómo usarla en los bots
keywords: Bots de autenticación de teams AAD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: c3f2f7fe3eb6b10faef2b24b3212081a881d6f8f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020691"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Autenticar un usuario en un bot de Microsoft Teams de autenticación

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Es posible que desee usar muchos servicios dentro de la aplicación Teams y la mayoría de esos servicios requieren autenticación y autorización para obtener acceso al servicio. Los servicios incluyen Facebook, Twitter y, por supuesto, Teams. Los usuarios de Teams tienen información de perfil de usuario almacenada en Azure Active Directory (Azure AD) mediante Microsoft Graph. Este artículo se centrará en la autenticación con Azure AD para obtener acceso a esta información.

OAuth 2.0 es un estándar abierto para la autenticación usada por Azure AD y muchos otros proveedores de servicios. Comprender OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams y Azure AD. Los ejemplos siguientes usan el flujo de concesión implícita de OAuth 2.0 con el objetivo de leer finalmente la información de perfil del usuario de Azure AD y Microsoft Graph.

El flujo de autenticación descrito en este artículo es muy similar al de las pestañas, excepto que las pestañas pueden usar el flujo de autenticación basado en web y los bots requieren que la autenticación se controle desde el código. Los conceptos de este artículo también serán útiles al implementar la autenticación desde la plataforma móvil.

Para obtener información general sobre el flujo de autenticación para bots, vea el tema [Flujo de autenticación en bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

## <a name="configuring-identity-providers"></a>Configuración de proveedores de identidades

Consulte el tema [Configurar](~/concepts/authentication/configure-identity-provider.md) proveedores de identidades para obtener pasos detallados sobre cómo configurar las direcciones URL de redireccionamiento de devolución de llamada de OAuth 2.0 al usar Azure Active Directory como proveedor de identidades.

## <a name="initiate-authentication-flow"></a>Iniciar flujo de autenticación

El flujo de autenticación debe desencadenarse mediante una acción del usuario. No debe abrir la ventana emergente de autenticación automáticamente porque es probable que esto desencadene el bloqueador de elementos emergentes del explorador y confunda al usuario.

## <a name="add-ui-to-start-authentication"></a>Agregar interfaz de usuario para iniciar la autenticación

Agrega la interfaz de usuario al bot para permitir que el usuario inicie sesión cuando sea necesario. Aquí se hace desde una tarjeta miniatura, en TypeScript:

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

Se han agregado tres botones a la tarjeta de héroe: Iniciar sesión, Mostrar perfil y Cerrar sesión.

## <a name="sign-the-user-in"></a>Iniciar sesión en el usuario

Debido a la validación que debe realizarse por motivos de seguridad y la compatibilidad con las versiones móviles de Teams, el código no se muestra aquí, pero este es un ejemplo del código que inicia el proceso cuando el usuario presiona el botón Iniciar [sesión.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).

La validación y la compatibilidad móvil se explican en el tema [Flujo de autenticación en bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

Asegúrese de agregar el dominio de la dirección URL de redireccionamiento de autenticación a la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) sección del manifiesto. Si no lo hace, no aparecerá el elemento emergente de inicio de sesión.

## <a name="showing-user-profile-information"></a>Mostrar información de perfil de usuario

Aunque obtener un token de acceso es difícil debido a todas las transiciones de ida y vuelta en diferentes sitios web y a los problemas de seguridad que deben solucionarse, una vez que tenga un token, obtener información de Azure Active Directory es sencillo. El bot realiza una llamada al punto Graph `me` con el token de acceso. Graph responde con la información del usuario de la persona que inició sesión. La información de la respuesta se usa para construir una tarjeta bot y se envía.

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

## <a name="other-samples"></a>Otras muestras

Para ver el código de ejemplo que muestra el proceso de autenticación del bot, vea:

* [Microsoft Teams ejemplo de autenticación de bots](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
