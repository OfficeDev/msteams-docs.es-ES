---
title: Uso del servicio de bot de Azure para la autenticación en Teams
description: Describe la OAuthCard del servicio de bot de Azure y cómo se usa para la autenticación
ms.topic: conceptual
localization_priority: Normal
keywords: OAuthCard OAuth card Azure Bot Service de autenticación de teams
ms.openlocfilehash: 3d0df4f04625c5be3468d12319b54096ae06de90
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020684"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="4d295-104">Uso del servicio de bot de Azure para la autenticación en Teams</span><span class="sxs-lookup"><span data-stu-id="4d295-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="4d295-105">Sin la OAuthCard del servicio de bot de Azure, es complicado implementar la autenticación en un bot.</span><span class="sxs-lookup"><span data-stu-id="4d295-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="4d295-106">Es un desafío de pila completa que implica la creación de una experiencia web, la integración con proveedores externos de OAuth, la administración de tokens y el tratamiento de las llamadas de API de servidor a servidor correctas para completar el flujo de autenticación de forma segura.</span><span class="sxs-lookup"><span data-stu-id="4d295-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="4d295-107">Esto puede dar lugar a experiencias desordenada que requieren la entrada de "números mágicos".</span><span class="sxs-lookup"><span data-stu-id="4d295-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="4d295-108">Con OAuthCard del servicio de bot de Azure, es más fácil que el bot de Teams inicie sesión en los usuarios y acceda a proveedores de datos externos.</span><span class="sxs-lookup"><span data-stu-id="4d295-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="4d295-109">Tanto si ya has implementado la autenticación como si quieres cambiar a algo más sencillo, o si estás buscando agregar autenticación al servicio de bots por primera vez, OAuthCard puede facilitarlo.</span><span class="sxs-lookup"><span data-stu-id="4d295-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="4d295-110">Otros temas [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) de Autenticación describen la autenticación sin usar OAuthCard, por lo que si desea comprender la autenticación en Teams más profundamente o tener una situación en la que no puede usar la OAuthCard, todavía puede hacer referencia a esos temas.</span><span class="sxs-lookup"><span data-stu-id="4d295-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="4d295-111">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="4d295-111">Support for the OAuthCard</span></span>

<span data-ttu-id="4d295-112">Actualmente hay algunas restricciones para usar la OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="4d295-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="4d295-113">Entre ellos se incluyen:</span><span class="sxs-lookup"><span data-stu-id="4d295-113">These include:</span></span>

* <span data-ttu-id="4d295-114">La tarjeta no funcionará con el [acceso de invitado](/MicrosoftTeams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="4d295-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="4d295-115">No funcionará con [Microsoft Teams gratis](https://products.office.com/microsoft-teams/free)</span><span class="sxs-lookup"><span data-stu-id="4d295-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="4d295-116">Solo se puede usar para la autenticación de bots</span><span class="sxs-lookup"><span data-stu-id="4d295-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="4d295-117">Solo funciona para bots registrados en el [Servicio de bots de Azure](https://azure.microsoft.com/services/bot-service/)</span><span class="sxs-lookup"><span data-stu-id="4d295-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="4d295-118">¿Cómo me ayuda el Servicio de bots de Azure a realizar la autenticación?</span><span class="sxs-lookup"><span data-stu-id="4d295-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="4d295-119">La documentación completa con OAuthCard está disponible en el tema: Agregar autenticación al bot a través [del Servicio de bots de Azure](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="4d295-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="4d295-120">Tenga en cuenta que este tema está en el conjunto de documentación de Azure Bot Framework y no es específico de Teams.</span><span class="sxs-lookup"><span data-stu-id="4d295-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="4d295-121">En las secciones siguientes se explica cómo usar OAuthCard en Teams.</span><span class="sxs-lookup"><span data-stu-id="4d295-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="4d295-122">Principales ventajas para desarrolladores de Teams</span><span class="sxs-lookup"><span data-stu-id="4d295-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="4d295-123">OAuthCard ayuda con la autenticación de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="4d295-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="4d295-124">Proporciona un flujo de autenticación basado en web de forma integrada: ya no es necesario escribir y hospedar una página web para dirigir a experiencias de inicio de sesión externas o proporcionar un redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="4d295-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="4d295-125">Es perfecto para los usuarios finales: completa la experiencia de inicio de sesión completa en Teams.</span><span class="sxs-lookup"><span data-stu-id="4d295-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="4d295-126">Incluye una administración de tokens sencilla: ya no es necesario implementar un sistema de almacenamiento de tokens; en su lugar, el Servicio de bots se encarga del almacenamiento en caché de tokens y proporciona un mecanismo seguro para capturar esos tokens.</span><span class="sxs-lookup"><span data-stu-id="4d295-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="4d295-127">Es compatible con SDK completos: fáciles de integrar y consumir desde el servicio de bots.</span><span class="sxs-lookup"><span data-stu-id="4d295-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="4d295-128">Tiene compatibilidad lista para muchos proveedores populares de OAuth, como Azure AD/MSA, Facebook y Google.</span><span class="sxs-lookup"><span data-stu-id="4d295-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="4d295-129">¿Cuándo debo implementar mi propia solución?</span><span class="sxs-lookup"><span data-stu-id="4d295-129">When should I implement my own solution?</span></span>

<span data-ttu-id="4d295-130">Dado que los tokens de acceso son información confidencial, es posible que no desee que se almacenen en un servicio externo.</span><span class="sxs-lookup"><span data-stu-id="4d295-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="4d295-131">En este caso, puede optar por implementar su propio sistema de administración de tokens y la experiencia de inicio de sesión en Teams, como se describe en el resto de los temas de autenticación [de](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) Teams.</span><span class="sxs-lookup"><span data-stu-id="4d295-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="4d295-132">Introducción a OAuthCard en Teams</span><span class="sxs-lookup"><span data-stu-id="4d295-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="4d295-133">Esta guía usa el SDK de Bot Framework v3.</span><span class="sxs-lookup"><span data-stu-id="4d295-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="4d295-134">Puede encontrar la implementación de v4 [aquí](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="4d295-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span> <span data-ttu-id="4d295-135">Todavía tendrá que crear un manifiesto e incluir token.botframework.com en la sección, porque de lo contrario el botón Iniciar sesión no `validDomains` abrirá la ventana de autenticación.</span><span class="sxs-lookup"><span data-stu-id="4d295-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="4d295-136">Usa [App Studio](~/concepts/build-and-test/app-studio-overview.md) para generar el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="4d295-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="4d295-137">Primero tendrá que configurar el servicio de bots de Azure para configurar proveedores de autenticación externos.</span><span class="sxs-lookup"><span data-stu-id="4d295-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="4d295-138">Lea [Configurar proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para conocer los pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="4d295-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="4d295-139">Para habilitar la autenticación con el Servicio de bots de Azure, debe realizar estas adiciones al código:</span><span class="sxs-lookup"><span data-stu-id="4d295-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="4d295-140">Incluye token.botframework.com en la sección del manifiesto de la aplicación porque Teams insertará la página de inicio `validDomains` de sesión del servicio bot.</span><span class="sxs-lookup"><span data-stu-id="4d295-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="4d295-141">Recupera el token del Servicio de bots siempre que el bot necesite obtener acceso a los recursos autenticados.</span><span class="sxs-lookup"><span data-stu-id="4d295-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="4d295-142">Si no hay ningún token disponible, envíe un mensaje con una OAuthCard al usuario que le solicite que inicie sesión en el servicio externo.</span><span class="sxs-lookup"><span data-stu-id="4d295-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="4d295-143">Controlar la actividad de finalización de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4d295-143">Handle the login completion activity.</span></span> <span data-ttu-id="4d295-144">Esto garantiza que la solicitud de autenticación y el token estén asociados con el usuario que interactúa actualmente con el bot.</span><span class="sxs-lookup"><span data-stu-id="4d295-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="4d295-145">Recupere el token siempre que el bot necesite realizar acciones autenticadas, como llamar a API de REST externas.</span><span class="sxs-lookup"><span data-stu-id="4d295-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="4d295-146">En el código de diálogo, deberá agregar este fragmento de código (C#), que comprueba si hay un token de acceso existente:</span><span class="sxs-lookup"><span data-stu-id="4d295-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

```CSharp
// First ask Bot Service if it already has a token for this user
var token = await context.GetUserTokenAsync(ConnectionName).ConfigureAwait(false);
if (token != null)
{
    // use the token to do exciting things!
}
else
{
    // If Bot Service does not have a token, send an OAuth card to sign in 
    await SendOAuthCardAsync(context, (Activity)context.Activity);
}
```

<span data-ttu-id="4d295-147">Si no existe un token de acceso, el código enviará un mensaje con una OAuthCard al usuario:</span><span class="sxs-lookup"><span data-stu-id="4d295-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="4d295-148">Para controlar la actividad completa de inicio de sesión, deberá procesar esta invocación:</span><span class="sxs-lookup"><span data-stu-id="4d295-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

```CSharp
if (activity.Name == "signin/verifyState")
{
  // We do this so that we can pass handling to the right logic in the dialog. You can
  // set this to be whatever string you want.
  activity.Text = "loginComplete";
  await Conversation.SendAsync(activity, () => new Dialogs.RootDialog());

  return Request.CreateResponse(HttpStatusCode.OK);
}
```

<span data-ttu-id="4d295-149">En el código de diálogo, puede recuperar el token del servicio de autenticación bot:</span><span class="sxs-lookup"><span data-stu-id="4d295-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

```CSharp
if (text.Contains("loginComplete"))
  {
    // Handle login completion event.
    JObject ctx = activity.Value as JObject;

    if (ctx != null)
    {
      string code = ctx["state"].ToString();

      var oauthClient = activity.GetOAuthClient();
      var token = await oauthClient.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, magicCode: code).ConfigureAwait(false);
      if (token != null)
      {
        // Make whatever API calls here you want
        await context.PostAsync($"Success! You are now signed in.");
      }
    }
  // Need to respond to the Invoke.
  return;
}
```

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="4d295-150">Uso de OAuthCard con extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="4d295-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="4d295-151">También puede usar el Servicio de bots de Azure para conectar proveedores de terceros a la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="4d295-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="4d295-152">El flujo es el mismo que con un bot, excepto que en lugar de devolver una OAuthCard, el servicio devolverá un mensaje de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4d295-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="4d295-153">El siguiente fragmento de código (C#) ilustra cómo crear la respuesta de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="4d295-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

```CSharp
var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName).ConfigureAwait(false);

if (token == null)
{
  // Send the login response with the auth link.
  string link = await client.OAuthApi.GetSignInLinkAsync(activity, ConnectionName);

  response = new ComposeExtensionResponse()
  {
    ComposeExtension = new ComposeExtensionResult()
  };
  response.ComposeExtension.Type = "auth";
  response.ComposeExtension.SuggestedActions = new ComposeExtensionSuggestedAction()
  {
    Actions = new List<CardAction>()
      {
        new CardAction(ActionTypes.OpenUrl, title: "Sign into this app", value: link)
      }
    };
  return response;
}
```

<span data-ttu-id="4d295-154">Tenga en cuenta que en el ejemplo anterior debe realizar la llamada `GetSignInLinkAsync` directamente en la `client.OAuthApi` propiedad.</span><span class="sxs-lookup"><span data-stu-id="4d295-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="4d295-155">Cuando el usuario complete correctamente la secuencia de inicio de sesión, el servicio recibirá otra solicitud Invoke que contenga la consulta de usuario original, junto con una cadena de parámetro de estado que contenga el "código mágico".</span><span class="sxs-lookup"><span data-stu-id="4d295-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="4d295-156">Ahora puede capturar el token con esta cadena, junto con el identificador de usuario y el nombre de conexión.</span><span class="sxs-lookup"><span data-stu-id="4d295-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

```CSharp
var query = activity.GetComposeExtensionQueryData();
JObject data = activity.Value as JObject;

var client = activity.GetOAuthClient();

// Check if the request comes with login state
if (data != null && data["state"] != null)
{
  var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, data["state"].ToString());

  // Do stuff with the token here.

}
```
