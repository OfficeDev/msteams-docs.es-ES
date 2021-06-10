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
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="b310b-104">Autenticar un usuario en un bot de Microsoft Teams de autenticación</span><span class="sxs-lookup"><span data-stu-id="b310b-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="b310b-105">Es posible que desee usar muchos servicios dentro de la aplicación Teams y la mayoría de esos servicios requieren autenticación y autorización para obtener acceso al servicio.</span><span class="sxs-lookup"><span data-stu-id="b310b-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="b310b-106">Los servicios incluyen Facebook, Twitter y, por supuesto, Teams.</span><span class="sxs-lookup"><span data-stu-id="b310b-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="b310b-107">Los usuarios de Teams tienen información de perfil de usuario almacenada en Azure Active Directory (Azure AD) mediante Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b310b-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="b310b-108">Este artículo se centrará en la autenticación con Azure AD para obtener acceso a esta información.</span><span class="sxs-lookup"><span data-stu-id="b310b-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="b310b-109">OAuth 2.0 es un estándar abierto para la autenticación usada por Azure AD y muchos otros proveedores de servicios.</span><span class="sxs-lookup"><span data-stu-id="b310b-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="b310b-110">Comprender OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b310b-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="b310b-111">Los ejemplos siguientes usan el flujo de concesión implícita de OAuth 2.0 con el objetivo de leer finalmente la información de perfil del usuario de Azure AD y Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b310b-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="b310b-112">El flujo de autenticación descrito en este artículo es muy similar al de las pestañas, excepto que las pestañas pueden usar el flujo de autenticación basado en web y los bots requieren que la autenticación se controle desde el código.</span><span class="sxs-lookup"><span data-stu-id="b310b-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="b310b-113">Los conceptos de este artículo también serán útiles al implementar la autenticación desde la plataforma móvil.</span><span class="sxs-lookup"><span data-stu-id="b310b-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="b310b-114">Para obtener información general sobre el flujo de autenticación para bots, vea el tema [Flujo de autenticación en bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="b310b-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="b310b-115">Configuración de proveedores de identidades</span><span class="sxs-lookup"><span data-stu-id="b310b-115">Configuring identity providers</span></span>

<span data-ttu-id="b310b-116">Consulte el tema [Configurar](~/concepts/authentication/configure-identity-provider.md) proveedores de identidades para obtener pasos detallados sobre cómo configurar las direcciones URL de redireccionamiento de devolución de llamada de OAuth 2.0 al usar Azure Active Directory como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="b310b-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="b310b-117">Iniciar flujo de autenticación</span><span class="sxs-lookup"><span data-stu-id="b310b-117">Initiate authentication flow</span></span>

<span data-ttu-id="b310b-118">El flujo de autenticación debe desencadenarse mediante una acción del usuario.</span><span class="sxs-lookup"><span data-stu-id="b310b-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="b310b-119">No debe abrir la ventana emergente de autenticación automáticamente porque es probable que esto desencadene el bloqueador de elementos emergentes del explorador y confunda al usuario.</span><span class="sxs-lookup"><span data-stu-id="b310b-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="b310b-120">Agregar interfaz de usuario para iniciar la autenticación</span><span class="sxs-lookup"><span data-stu-id="b310b-120">Add UI to start authentication</span></span>

<span data-ttu-id="b310b-121">Agrega la interfaz de usuario al bot para permitir que el usuario inicie sesión cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b310b-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="b310b-122">Aquí se hace desde una tarjeta miniatura, en TypeScript:</span><span class="sxs-lookup"><span data-stu-id="b310b-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

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

<span data-ttu-id="b310b-123">Se han agregado tres botones a la tarjeta de héroe: Iniciar sesión, Mostrar perfil y Cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="b310b-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="b310b-124">Iniciar sesión en el usuario</span><span class="sxs-lookup"><span data-stu-id="b310b-124">Sign the user in</span></span>

<span data-ttu-id="b310b-125">Debido a la validación que debe realizarse por motivos de seguridad y la compatibilidad con las versiones móviles de Teams, el código no se muestra aquí, pero este es un ejemplo del código que inicia el proceso cuando el usuario presiona el botón Iniciar [sesión.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span><span class="sxs-lookup"><span data-stu-id="b310b-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="b310b-126">La validación y la compatibilidad móvil se explican en el tema [Flujo de autenticación en bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="b310b-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="b310b-127">Asegúrese de agregar el dominio de la dirección URL de redireccionamiento de autenticación a la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) sección del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b310b-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="b310b-128">Si no lo hace, no aparecerá el elemento emergente de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b310b-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="b310b-129">Mostrar información de perfil de usuario</span><span class="sxs-lookup"><span data-stu-id="b310b-129">Showing user profile information</span></span>

<span data-ttu-id="b310b-130">Aunque obtener un token de acceso es difícil debido a todas las transiciones de ida y vuelta en diferentes sitios web y a los problemas de seguridad que deben solucionarse, una vez que tenga un token, obtener información de Azure Active Directory es sencillo.</span><span class="sxs-lookup"><span data-stu-id="b310b-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="b310b-131">El bot realiza una llamada al punto Graph `me` con el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="b310b-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="b310b-132">Graph responde con la información del usuario de la persona que inició sesión.</span><span class="sxs-lookup"><span data-stu-id="b310b-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="b310b-133">La información de la respuesta se usa para construir una tarjeta bot y se envía.</span><span class="sxs-lookup"><span data-stu-id="b310b-133">Information from the response is used to construct a bot card and sent.</span></span>

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

<span data-ttu-id="b310b-134">Si el usuario no ha iniciado sesión, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="b310b-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="b310b-135">Cerrar la sesión del usuario</span><span class="sxs-lookup"><span data-stu-id="b310b-135">Sign the user out</span></span>

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

## <a name="other-samples"></a><span data-ttu-id="b310b-136">Otras muestras</span><span class="sxs-lookup"><span data-stu-id="b310b-136">Other samples</span></span>

<span data-ttu-id="b310b-137">Para ver el código de ejemplo que muestra el proceso de autenticación del bot, vea:</span><span class="sxs-lookup"><span data-stu-id="b310b-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="b310b-138">Microsoft Teams ejemplo de autenticación de bots</span><span class="sxs-lookup"><span data-stu-id="b310b-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
