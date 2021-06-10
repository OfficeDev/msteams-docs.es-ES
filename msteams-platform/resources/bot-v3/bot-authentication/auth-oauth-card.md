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
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Uso del servicio de bot de Azure para la autenticación en Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Sin la OAuthCard del servicio de bot de Azure, es complicado implementar la autenticación en un bot. Es un desafío de pila completa que implica la creación de una experiencia web, la integración con proveedores externos de OAuth, la administración de tokens y el tratamiento de las llamadas de API de servidor a servidor correctas para completar el flujo de autenticación de forma segura. Esto puede dar lugar a experiencias desordenada que requieren la entrada de "números mágicos".

Con OAuthCard del servicio de bot de Azure, es más fácil que el bot de Teams inicie sesión en los usuarios y acceda a proveedores de datos externos. Tanto si ya has implementado la autenticación como si quieres cambiar a algo más sencillo, o si estás buscando agregar autenticación al servicio de bots por primera vez, OAuthCard puede facilitarlo.

Otros temas [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) de autenticación describen la autenticación sin usar OAuthCard, por lo que si desea comprender la autenticación en Teams más profundamente o tener una situación en la que no puede usar la OAuthCard, todavía puede hacer referencia a esos temas.

## <a name="support-for-the-oauthcard"></a>Compatibilidad con OAuthCard

Actualmente hay algunas restricciones para usar la OAuthCard. Entre ellas se incluyen:

* La tarjeta no funcionará con el [acceso de invitado](/MicrosoftTeams/guest-access)
* No funcionará con Microsoft Teams [gratis](https://products.office.com/microsoft-teams/free)
* Solo se puede usar para la autenticación de bots
* Solo funciona para bots registrados en el [Servicio de bots de Azure](https://azure.microsoft.com/services/bot-service/)

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>¿Cómo me ayuda el Servicio de bots de Azure a realizar la autenticación?

La documentación completa con OAuthCard está disponible en el tema: Agregar autenticación al bot a través [del Servicio de bots de Azure](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true). Tenga en cuenta que este tema se encuentra en el conjunto de documentación de Azure Bot Framework y no es específico de Teams.

En las secciones siguientes se explica cómo usar OAuthCard en Teams.

## <a name="main-benefits-for-teams-developers"></a>Principales ventajas para Teams desarrolladores

OAuthCard ayuda con la autenticación de las siguientes maneras:

* Proporciona un flujo de autenticación basado en web de forma integrada: ya no es necesario escribir y hospedar una página web para dirigir a experiencias de inicio de sesión externas o proporcionar un redireccionamiento.
* Es perfecto para los usuarios finales: completa la experiencia de inicio de sesión completa dentro de Teams.
* Incluye una administración de tokens sencilla: ya no es necesario implementar un sistema de almacenamiento de tokens; en su lugar, el Servicio de bots se encarga del almacenamiento en caché de tokens y proporciona un mecanismo seguro para capturar esos tokens.
* Es compatible con SDK completos: fáciles de integrar y consumir desde el servicio de bots.
* Tiene compatibilidad lista para muchos proveedores populares de OAuth, como Azure AD/MSA, Facebook y Google.

## <a name="when-should-i-implement-my-own-solution"></a>¿Cuándo debo implementar mi propia solución?

Dado que los tokens de acceso son información confidencial, es posible que no desee que se almacenen en un servicio externo. En este caso, puede optar por implementar su propio sistema de administración de tokens y la experiencia de inicio de sesión en Teams, tal como se describe en el resto de los temas de autenticación Teams [token.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)

## <a name="getting-started-with-oauthcard-in-teams"></a>Introducción a OAuthCard en Teams

> [!NOTE]
> Esta guía usa el SDK de Bot Framework v3. Puede encontrar la implementación de v4 [aquí](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true). Todavía tendrá que crear un manifiesto e incluir token.botframework.com en la sección, porque de lo contrario el botón Iniciar sesión no `validDomains` abrirá la ventana de autenticación. Usa [App Studio](~/concepts/build-and-test/app-studio-overview.md) para generar el manifiesto.

Primero tendrá que configurar el servicio de bots de Azure para configurar proveedores de autenticación externos. Lea [Configurar proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para conocer los pasos detallados.

Para habilitar la autenticación con el Servicio de bots de Azure, debe realizar estas adiciones al código:

1. Incluye token.botframework.com en la sección del manifiesto de la aplicación porque Teams insertará la página de inicio `validDomains` de sesión del servicio bot.
2. Recupera el token del Servicio de bots siempre que el bot necesite obtener acceso a los recursos autenticados. Si no hay ningún token disponible, envíe un mensaje con una OAuthCard al usuario que le solicite que inicie sesión en el servicio externo.
3. Controlar la actividad de finalización de inicio de sesión. Esto garantiza que la solicitud de autenticación y el token estén asociados con el usuario que interactúa actualmente con el bot.
4. Recupere el token siempre que el bot necesite realizar acciones autenticadas, como llamar a API de REST externas.

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

Si no existe un token de acceso, el código enviará un mensaje con una OAuthCard al usuario:

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Para controlar la actividad completa de inicio de sesión, deberá procesar esta invocación:

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

En el código de diálogo, puede recuperar el token del servicio de autenticación bot:

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

También puede usar el Servicio de bots de Azure para conectar proveedores de terceros a la extensión de mensajería. El flujo es el mismo que con un bot, excepto que en lugar de devolver una OAuthCard, el servicio devolverá un mensaje de inicio de sesión.

El siguiente fragmento de código (C#) ilustra cómo crear la respuesta de inicio de sesión:

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

Tenga en cuenta que en el ejemplo anterior debe realizar la llamada `GetSignInLinkAsync` directamente en la `client.OAuthApi` propiedad.

Cuando el usuario complete correctamente la secuencia de inicio de sesión, el servicio recibirá otra solicitud Invoke que contenga la consulta de usuario original, junto con una cadena de parámetro de estado que contenga el "código mágico". Ahora puede capturar el token con esta cadena, junto con el identificador de usuario y el nombre de conexión.

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
