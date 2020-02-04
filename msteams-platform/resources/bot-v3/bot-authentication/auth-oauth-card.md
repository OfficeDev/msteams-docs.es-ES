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
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Uso del servicio de bot de Azure para la autenticación en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Sin el OAuthCard del servicio de robots de Azure, es complicado implementar la autenticación en un bot. Se trata de un desafío completo que implica la creación de una experiencia web, la integración con proveedores externos de OAuth, la administración de tokens y el control de las llamadas de API de servidor a servidor adecuadas para completar de forma segura el flujo de autenticación. Esto puede dar lugar a experiencias de Clunky que requieran la entrada de "números mágicos".

Con el OAuthCard del servicio de robots de Azure, es más fácil para su equipo bot iniciar sesión en los usuarios y tener acceso a proveedores de datos externos. Tanto si ya ha implementado auth como si desea cambiar a algo más sencillo o si está buscando agregar autenticación a su servicio de bot por primera vez, el OAuthCard puede hacerlo más fácil.

Otros temas de [autenticación](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describen la autenticación sin usar la OAuthCard, por lo que si desea comprender la autenticación en Teams más profundamente o si tiene alguna situación en la que no puede usar el OAuthCard, puede hacer referencia a esos temas.

## <a name="support-for-the-oauthcard"></a>Compatibilidad con OAuthCard

Actualmente hay algunas restricciones en donde puede usar el OAuthCard. Entre ellos se incluyen:

* La tarjeta no funcionará con [acceso de invitado](/MicrosoftTeams/guest-access)
* No funcionará con [Microsoft Teams](https://products.office.com/microsoft-teams/free) de forma gratuita
* Solo se puede usar para la autenticación de bot.
* Solo funciona con bots registrados en el [servicio de robots de Azure](https://azure.microsoft.com/services/bot-service/) .

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>¿Cómo me ayuda el servicio de robots de Azure a realizar la autenticación?

La documentación completa sobre el uso de OAuthCard está disponible en el tema sobre cómo [Agregar autenticación a su bot a través del servicio de bot de Azure](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0). Tenga en cuenta que este tema se encuentra en el conjunto de documentación de Azure bot Framework y no es específico para Microsoft Teams.

En las secciones siguientes se explica cómo usar OAuthCard en Microsoft Teams.

## <a name="main-benefits-for-teams-developers"></a>Principales ventajas para los desarrolladores de Microsoft Teams

La OAuthCard ayuda con la autenticación de las siguientes maneras:

* Proporciona un flujo de autenticación basado en Web, ya que ya no es necesario escribir ni hospedar una página web para dirigirse a experiencias de inicio de sesión externo ni proporcionar un redireccionamiento.
* Es perfecta para los usuarios finales: complete la experiencia de inicio de sesión completa en Teams.
* Incluye administración de tokens sencilla: ya no tiene que implementar un sistema de almacenamiento de tokens: en su lugar, el servicio de bot se encarga del almacenamiento en caché de tokens y proporciona un mecanismo seguro para recuperar dichos tokens.
* Es compatible con los SDK completos: fácil de integrar y consumir desde el servicio de bot.
* Tiene compatibilidad para muchos proveedores de OAuth populares, como Azure AD/MSA, Facebook y Google.

## <a name="when-should-i-implement-my-own-solution"></a>¿Cuándo debo implementar mi propia solución?

Como los tokens de acceso son información confidencial, es posible que no desee que se almacenen en un servicio externo. En este caso, puede optar por implementar su propio sistema de administración de tokens y la experiencia de inicio de sesión dentro de Teams, tal como se describe en el resto de los temas de [autenticación](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) de Teams.

## <a name="getting-started-with-oauthcard-in-teams"></a>Introducción a OAuthCard en Microsoft Teams

> [!NOTE]
> Esta guía está usando el SDK de bot Framework V3. [Aquí](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp)puede encontrar la implementación de V4. Todavía tendrá que crear un manifiesto e incluir token.botframework.com en la `validDomains` sección, ya que, de lo contrario, el botón de inicio de sesión no abrirá la ventana de autenticación. Use [App Studio](~/concepts/build-and-test/app-studio-overview.md) para generar el manifiesto.

Primero necesita configurar el servicio de bot de Azure para configurar los proveedores de autenticación externa. Leer la [configuración de proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para conocer los pasos detallados.

Para habilitar la autenticación con el servicio de bot de Azure, debe realizar estas adiciones al código:

1. Incluya token.botframework.com en la `validDomains` sección del manifiesto de la aplicación, ya que Microsoft Teams incrustará la página de inicio de sesión del servicio de bot.
2. Recupere el token del servicio de bot siempre que el bot necesite tener acceso a los recursos autenticados. Si no hay ningún token disponible, envíe un mensaje con un OAuthCard al usuario para solicitarle que inicie sesión en el servicio externo.
3. Controlar la actividad de finalización de inicio de sesión. Esto garantiza que la solicitud de autenticación y el token están asociados con el usuario que interactúa actualmente con el bot.
4. Recupere el token siempre que su bot necesite realizar acciones autenticadas, como llamar a las API de REST externas.

En el código del cuadro de diálogo, deberá agregar este fragmento de código (C#), que comprueba si existe un token de acceso:

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

Si no existe ningún token de acceso, el código enviará un mensaje con un OAuthCard al usuario:

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Para controlar la actividad completa de inicio de sesión, debe procesar esta Invocación:

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

En el código del cuadro de diálogo, puede recuperar el token del servicio de autenticación de bot:

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

También puede usar el servicio de robots de Azure para conectar proveedores de terceros a su extensión de mensajería. El flujo es el mismo que con un bot, excepto en lugar de devolver un OAuthCard, el servicio devolverá un mensaje de inicio de sesión.

El siguiente fragmento de código (C#) ilustra cómo diseñar la respuesta de inicio de sesión:

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

Tenga en cuenta que en el ejemplo anterior necesita realizar la llamada directamente `GetSignInLinkAsync` a la `client.OAuthApi` propiedad.

Cuando el usuario complete correctamente la secuencia de inicio de sesión, el servicio recibirá otra solicitud de invocación que contiene la consulta de usuario original, junto con una cadena de parámetro de estado que contiene el "Magic Code". Ahora puede capturar el token con esta cadena, junto con el identificador de usuario y el nombre de conexión.

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
