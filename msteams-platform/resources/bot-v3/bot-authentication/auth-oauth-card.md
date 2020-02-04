---
title: Uso del servicio de bot de Azure para la autenticación en Microsoft Teams
description: Describe la OAuthCard del servicio de bot de Azure y cómo se usa para la autenticación
keywords: Servicios de autenticación de OAuthCard servicio de bot de Azure en la tarjeta OAuth
ms.openlocfilehash: 0397c45b39470d97c1158b2681462038de618a39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676017"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="341e3-104">Uso del servicio de bot de Azure para la autenticación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="341e3-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="341e3-105">Sin el OAuthCard del servicio de robots de Azure, es complicado implementar la autenticación en un bot.</span><span class="sxs-lookup"><span data-stu-id="341e3-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="341e3-106">Se trata de un desafío completo que implica la creación de una experiencia web, la integración con proveedores externos de OAuth, la administración de tokens y el control de las llamadas de API de servidor a servidor adecuadas para completar de forma segura el flujo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="341e3-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="341e3-107">Esto puede dar lugar a experiencias de Clunky que requieran la entrada de "números mágicos".</span><span class="sxs-lookup"><span data-stu-id="341e3-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="341e3-108">Con el OAuthCard del servicio de robots de Azure, es más fácil para su equipo bot iniciar sesión en los usuarios y tener acceso a proveedores de datos externos.</span><span class="sxs-lookup"><span data-stu-id="341e3-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="341e3-109">Tanto si ya ha implementado auth como si desea cambiar a algo más sencillo o si está buscando agregar autenticación a su servicio de bot por primera vez, el OAuthCard puede hacerlo más fácil.</span><span class="sxs-lookup"><span data-stu-id="341e3-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="341e3-110">Otros temas de [autenticación](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describen la autenticación sin usar la OAuthCard, por lo que si desea comprender la autenticación en Teams más profundamente o si tiene alguna situación en la que no puede usar el OAuthCard, puede hacer referencia a esos temas.</span><span class="sxs-lookup"><span data-stu-id="341e3-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="341e3-111">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="341e3-111">Support for the OAuthCard</span></span>

<span data-ttu-id="341e3-112">Actualmente hay algunas restricciones en donde puede usar el OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="341e3-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="341e3-113">Entre ellos se incluyen:</span><span class="sxs-lookup"><span data-stu-id="341e3-113">These include:</span></span>

* <span data-ttu-id="341e3-114">La tarjeta no funcionará con [acceso de invitado](/MicrosoftTeams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="341e3-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="341e3-115">No funcionará con [Microsoft Teams](https://products.office.com/microsoft-teams/free) de forma gratuita</span><span class="sxs-lookup"><span data-stu-id="341e3-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="341e3-116">Solo se puede usar para la autenticación de bot.</span><span class="sxs-lookup"><span data-stu-id="341e3-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="341e3-117">Solo funciona con bots registrados en el [servicio de robots de Azure](https://azure.microsoft.com/services/bot-service/) .</span><span class="sxs-lookup"><span data-stu-id="341e3-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="341e3-118">¿Cómo me ayuda el servicio de robots de Azure a realizar la autenticación?</span><span class="sxs-lookup"><span data-stu-id="341e3-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="341e3-119">La documentación completa sobre el uso de OAuthCard está disponible en el tema sobre cómo [Agregar autenticación a su bot a través del servicio de bot de Azure](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="341e3-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="341e3-120">Tenga en cuenta que este tema se encuentra en el conjunto de documentación de Azure bot Framework y no es específico para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="341e3-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="341e3-121">En las secciones siguientes se explica cómo usar OAuthCard en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="341e3-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="341e3-122">Principales ventajas para los desarrolladores de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="341e3-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="341e3-123">La OAuthCard ayuda con la autenticación de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="341e3-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="341e3-124">Proporciona un flujo de autenticación basado en Web, ya que ya no es necesario escribir ni hospedar una página web para dirigirse a experiencias de inicio de sesión externo ni proporcionar un redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="341e3-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="341e3-125">Es perfecta para los usuarios finales: complete la experiencia de inicio de sesión completa en Teams.</span><span class="sxs-lookup"><span data-stu-id="341e3-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="341e3-126">Incluye administración de tokens sencilla: ya no tiene que implementar un sistema de almacenamiento de tokens: en su lugar, el servicio de bot se encarga del almacenamiento en caché de tokens y proporciona un mecanismo seguro para recuperar dichos tokens.</span><span class="sxs-lookup"><span data-stu-id="341e3-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="341e3-127">Es compatible con los SDK completos: fácil de integrar y consumir desde el servicio de bot.</span><span class="sxs-lookup"><span data-stu-id="341e3-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="341e3-128">Tiene compatibilidad para muchos proveedores de OAuth populares, como Azure AD/MSA, Facebook y Google.</span><span class="sxs-lookup"><span data-stu-id="341e3-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="341e3-129">¿Cuándo debo implementar mi propia solución?</span><span class="sxs-lookup"><span data-stu-id="341e3-129">When should I implement my own solution?</span></span>

<span data-ttu-id="341e3-130">Como los tokens de acceso son información confidencial, es posible que no desee que se almacenen en un servicio externo.</span><span class="sxs-lookup"><span data-stu-id="341e3-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="341e3-131">En este caso, puede optar por implementar su propio sistema de administración de tokens y la experiencia de inicio de sesión dentro de Teams, tal como se describe en el resto de los temas de [autenticación](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) de Teams.</span><span class="sxs-lookup"><span data-stu-id="341e3-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="341e3-132">Introducción a OAuthCard en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="341e3-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="341e3-133">Esta guía está usando el SDK de bot Framework V3.</span><span class="sxs-lookup"><span data-stu-id="341e3-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="341e3-134">[Aquí](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp)puede encontrar la implementación de V4.</span><span class="sxs-lookup"><span data-stu-id="341e3-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp).</span></span> <span data-ttu-id="341e3-135">Todavía tendrá que crear un manifiesto e incluir token.botframework.com en la `validDomains` sección, ya que, de lo contrario, el botón de inicio de sesión no abrirá la ventana de autenticación.</span><span class="sxs-lookup"><span data-stu-id="341e3-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="341e3-136">Use [App Studio](~/concepts/build-and-test/app-studio-overview.md) para generar el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="341e3-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="341e3-137">Primero necesita configurar el servicio de bot de Azure para configurar los proveedores de autenticación externa.</span><span class="sxs-lookup"><span data-stu-id="341e3-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="341e3-138">Leer la [configuración de proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para conocer los pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="341e3-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="341e3-139">Para habilitar la autenticación con el servicio de bot de Azure, debe realizar estas adiciones al código:</span><span class="sxs-lookup"><span data-stu-id="341e3-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="341e3-140">Incluya token.botframework.com en la `validDomains` sección del manifiesto de la aplicación, ya que Microsoft Teams incrustará la página de inicio de sesión del servicio de bot.</span><span class="sxs-lookup"><span data-stu-id="341e3-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="341e3-141">Recupere el token del servicio de bot siempre que el bot necesite tener acceso a los recursos autenticados.</span><span class="sxs-lookup"><span data-stu-id="341e3-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="341e3-142">Si no hay ningún token disponible, envíe un mensaje con un OAuthCard al usuario para solicitarle que inicie sesión en el servicio externo.</span><span class="sxs-lookup"><span data-stu-id="341e3-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="341e3-143">Controlar la actividad de finalización de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="341e3-143">Handle the login completion activity.</span></span> <span data-ttu-id="341e3-144">Esto garantiza que la solicitud de autenticación y el token están asociados con el usuario que interactúa actualmente con el bot.</span><span class="sxs-lookup"><span data-stu-id="341e3-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="341e3-145">Recupere el token siempre que su bot necesite realizar acciones autenticadas, como llamar a las API de REST externas.</span><span class="sxs-lookup"><span data-stu-id="341e3-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="341e3-146">En el código del cuadro de diálogo, deberá agregar este fragmento de código (C#), que comprueba si existe un token de acceso:</span><span class="sxs-lookup"><span data-stu-id="341e3-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

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

<span data-ttu-id="341e3-147">Si no existe ningún token de acceso, el código enviará un mensaje con un OAuthCard al usuario:</span><span class="sxs-lookup"><span data-stu-id="341e3-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="341e3-148">Para controlar la actividad completa de inicio de sesión, debe procesar esta Invocación:</span><span class="sxs-lookup"><span data-stu-id="341e3-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

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

<span data-ttu-id="341e3-149">En el código del cuadro de diálogo, puede recuperar el token del servicio de autenticación de bot:</span><span class="sxs-lookup"><span data-stu-id="341e3-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

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

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="341e3-150">Uso de OAuthCard con extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="341e3-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="341e3-151">También puede usar el servicio de robots de Azure para conectar proveedores de terceros a su extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="341e3-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="341e3-152">El flujo es el mismo que con un bot, excepto en lugar de devolver un OAuthCard, el servicio devolverá un mensaje de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="341e3-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="341e3-153">El siguiente fragmento de código (C#) ilustra cómo diseñar la respuesta de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="341e3-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

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

<span data-ttu-id="341e3-154">Tenga en cuenta que en el ejemplo anterior necesita realizar la llamada directamente `GetSignInLinkAsync` a la `client.OAuthApi` propiedad.</span><span class="sxs-lookup"><span data-stu-id="341e3-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="341e3-155">Cuando el usuario complete correctamente la secuencia de inicio de sesión, el servicio recibirá otra solicitud de invocación que contiene la consulta de usuario original, junto con una cadena de parámetro de estado que contiene el "Magic Code".</span><span class="sxs-lookup"><span data-stu-id="341e3-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="341e3-156">Ahora puede capturar el token con esta cadena, junto con el identificador de usuario y el nombre de conexión.</span><span class="sxs-lookup"><span data-stu-id="341e3-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

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
