---
title: Uso de Azure Bot Service para la autenticación en Teams
description: Describe azure Bot Service OAuthCard y cómo se usa para la autenticación
ms.topic: conceptual
localization_priority: Normal
keywords: autenticación de teams OAuthCard OAuth card Azure Bot Service
ms.openlocfilehash: 7731e4d1148e50c748d9c5e1b55371628a78dea7
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143168"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Uso de Azure Bot Service para la autenticación en Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Sin la OAuthCard de Azure Bot Service es complicado implementar la autenticación en un bot. Es un desafío de pila completa que implica la creación de una experiencia web, la integración con proveedores externos de OAuth, la administración de tokens y el control de las llamadas API de servidor a servidor adecuadas para completar el flujo de autenticación de forma segura. Esto puede dar lugar a experiencias torpes que requieren la entrada de "números mágicos".

Con OAuthCard de Azure Bot Service, es más fácil que el bot de Teams inicie sesión en los usuarios y acceda a proveedores de datos externos. Tanto si ya ha implementado la autenticación como si desea cambiar a algo más sencillo o si quiere agregar autenticación al servicio bot por primera vez, OAuthCard puede facilitarla.

Otros temas de [Autenticación](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describen la autenticación sin usar OAuthCard, por lo que si desea comprender la autenticación en Teams más profundamente, o si tiene una situación en la que no puede usar OAuthCard, puede seguir haciendo referencia a esos temas.

## <a name="support-for-the-oauthcard"></a>Compatibilidad con OAuthCard

Actualmente hay algunas restricciones en las que puede usar OAuthCard. Incluyen:

* La tarjeta no funcionará con [el acceso de invitado](/MicrosoftTeams/guest-access).
* No funcionará con [Microsoft Teams gratuito](https://products.office.com/microsoft-teams/free).
* Solo se puede usar para la autenticación de bots.
* Solo funciona para los bots registrados en [azure Bot Service](https://azure.microsoft.com/services/bot-service/).

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>¿Cómo me ayuda Azure Bot Service a realizar la autenticación?

La documentación completa con OAuthCard está disponible en el tema: [Adición de autenticación al bot a través de Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true). Tenga en cuenta que este tema se encuentra en el conjunto de documentación de Azure Bot Framework y no es específico de Teams.

En las secciones siguientes se indica cómo usar OAuthCard en Teams.

## <a name="main-benefits-for-teams-developers"></a>Principales ventajas para desarrolladores de Teams

OAuthCard ayuda con la autenticación de las siguientes maneras:

* Proporciona un flujo de autenticación basado en web integrado: ya no tiene que escribir ni hospedar una página web para dirigirse a experiencias de inicio de sesión externas o proporcionar una redirección.
* Es perfecta para los usuarios finales: complete la experiencia de inicio de sesión completa justo dentro de Teams.
* Incluye una administración de tokens sencilla: ya no tiene que implementar un sistema de almacenamiento de tokens; en su lugar, el Bot Service se encarga del almacenamiento en caché de tokens y proporciona un mecanismo seguro para capturar esos tokens.
* Es compatible con SDK completos: fácil de integrar y consumir desde el servicio de bot.
* Tiene compatibilidad integrada con muchos proveedores de OAuth populares, como Azure AD/MSA, Facebook y Google.

## <a name="when-should-i-implement-my-own-solution"></a>¿Cuándo debo implementar mi propia solución?

Dado que los tokens de acceso son información confidencial, es posible que no desee almacenarlos en un servicio externo. En este caso, puede optar por seguir implementando su propio sistema de administración de tokens y su experiencia de inicio de sesión dentro de Teams, como se describe en el resto de los temas de [autenticación](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) de Teams.

## <a name="getting-started-with-oauthcard-in-teams"></a>Introducción a OAuthCard en Teams

> [!NOTE]
> En esta guía se usa el SDK de Bot Framework v3. Puede encontrar la implementación v4 [aquí](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true). Tendrá que crear un manifiesto e incluir token.botframework.com en la `validDomains` sección, ya que de lo contrario, el botón Iniciar sesión no abrirá la ventana de autenticación. Use [App Studio](~/concepts/build-and-test/app-studio-overview.md) para generar el manifiesto.

Primero tendrá que configurar el servicio bot de Azure para configurar proveedores de autenticación externos. Lea [Configuración de proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para obtener pasos detallados.

Para habilitar la autenticación mediante azure Bot Service, debe realizar estas adiciones al código:

1. Incluya token.botframework.com en la `validDomains` sección del manifiesto de la aplicación porque Teams insertará la página de inicio de sesión del Bot Service.
2. Capture el token de la Bot Service siempre que el bot necesite acceder a los recursos autenticados. Si no hay ningún token disponible, envíe un mensaje con una OAuthCard al usuario que le solicite que inicie sesión en el servicio externo.
3. Controlar la actividad de finalización de inicio de sesión. Esto garantiza que la solicitud de autenticación y el token están asociados al usuario que interactúa actualmente con el bot.
4. Recupere el token siempre que el bot necesite realizar acciones autenticadas, como llamar a API REST externas.

En el código de diálogo, deberá agregar este fragmento de código (C#), que comprueba si hay un token de acceso existente:

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

Si no existe un token de acceso, el código enviará un mensaje con un OAuthCard al usuario:

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Para controlar la actividad de inicio de sesión completo, deberá procesar esta invocación:

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

En el código de diálogo, puede recuperar el token del servicio de autenticación de bots:

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

## <a name="using-oauthcard-with-messaging-extensions"></a>Uso de OAuthCard con extensiones de mensajería

También puede usar Azure Bot Service para conectar proveedores de terceros a la extensión de mensajería. El flujo es el mismo que con un bot, salvo que, en lugar de devolver una OAuthCard, el servicio devolverá un símbolo del sistema de inicio de sesión.

El siguiente fragmento de código (C#) muestra cómo crear la respuesta de inicio de sesión:

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

Tenga en cuenta que en el ejemplo anterior debe realizar la llamada a `GetSignInLinkAsync` directamente en la `client.OAuthApi` propiedad .

Cuando el usuario complete correctamente la secuencia de inicio de sesión, el servicio recibirá otra solicitud Invoke que contiene la consulta de usuario original, junto con una cadena de parámetro de estado que contiene el "código mágico". Ahora puede capturar el token mediante esta cadena, junto con el identificador de usuario y el nombre de conexión.

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
