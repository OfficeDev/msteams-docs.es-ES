---
title: Compatibilidad con SSO para las extensiones de mensaje
author: KirtiPereira
description: Obtenga información sobre cómo habilitar la compatibilidad con SSO para las extensiones de mensaje con ejemplos de código.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 4ee49b349d287325bb029aa155a61219a8656e22
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104395"
---
# <a name="single-sign-on-support-for-message-extensions"></a>Compatibilidad con el inicio de sesión único para extensiones de mensaje

La compatibilidad con el inicio de sesión único (SSO) ya está disponible para las extensiones de mensaje y la desplegamiento de vínculos. Al habilitar el inicio de sesión único para las extensiones de mensaje de forma predeterminada, se actualiza el token de autenticación, lo que minimiza el número de veces que necesita especificar las credenciales de inicio de sesión para Microsoft Teams.

Este documento le guía sobre cómo habilitar el inicio de sesión único y almacenar el token de autenticación, si es necesario.

## <a name="prerequisites"></a>Requisitos previos

El requisito previo para habilitar el inicio de sesión único para las extensiones de mensaje y la desurling de vínculos es el siguiente:

* Debe tener una cuenta de [Azure](https://azure.microsoft.com/free/) .
* Debe configurar la aplicación a través del portal de Azure AD y actualizar Teams manifiesto de aplicación el bot tal y como se define en [registrar la aplicación a través del portal de Azure AD](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal).

> [!NOTE]
> Para obtener más información sobre cómo crear una cuenta de Azure y actualizar el manifiesto de la aplicación, consulte [Compatibilidad con el inicio de sesión único (SSO) para bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-message-extensions-and-link-unfurling"></a>Habilitación del inicio de sesión único para extensiones de mensaje y desplegamiento de vínculos

Una vez completados los requisitos previos, puede habilitar el inicio de sesión único para las extensiones de mensaje y la desplegamiento de vínculos.

Para habilitar el inicio de sesión único:

1. Actualice los detalles de [conexión de OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) de los bots en el portal de Microsoft Azure.
2. Descargue el [ejemplo de extensiones de mensaje](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) y siga las instrucciones de configuración proporcionadas por el asistente.
   > [!NOTE]
   > Use la conexión de OAuth de los bots al configurar las extensiones de mensaje.
3. En el archivo [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) , actualice el valor de *auth* a *silentAuth* en `OnTeamsMessagingExtensionQueryAsync` y/o `OnTeamsAppBasedLinkQueryAsync`.  

    > [!NOTE]
    > No se admite el inicio de sesión único de otros controladores, excepto `OnTeamsMessagingExtensionQueryAsync` y `OnTeamsAppBasedLinkQueryAsync` desde el archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs.

4. Recibirá el token en `OnTeamsMessagingExtensionQueryAsync` el controlador en la `turnContext.Activity.Value` carga o en `OnTeamsAppBasedLinkQueryAsync`, en función del escenario para el que habilite el inicio de sesión único:

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    Si usa la conexión de OAuth, agregue el código siguiente al archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs para actualizar o agregar el token en el almacén:

   ```C#
   protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
            if (valueObject["authentication"] != null)
            {
                JObject authenticationObject = JObject.FromObject(valueObject["authentication"]);
                if (authenticationObject["token"] != null)
                {
                    //If the token is NOT exchangeable, then return 412 to require user consent
                    if (await TokenIsExchangeable(turnContext, cancellationToken))
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
                    }
                    else
                    {
                        var response = new InvokeResponse();
                        response.Status = 412;
                        return response;
                    }
                }
            }
            return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
        }
        private async Task<bool> TokenIsExchangeable(ITurnContext turnContext, CancellationToken cancellationToken)
        {
            TokenResponse tokenExchangeResponse = null;
            try
            {
                JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
                var tokenExchangeRequest =
                ((JObject)valueObject["authentication"])?.ToObject<TokenExchangeInvokeRequest>();
                var userTokenClient = turnContext.TurnState.Get<UserTokenClient>();
                tokenExchangeResponse = await userTokenClient.ExchangeTokenAsync(
                                turnContext.Activity.From.Id,
                                 _connectionName,
                                 turnContext.Activity.ChannelId,
                                 new TokenExchangeRequest
                 {
                     Token = tokenExchangeRequest.Token,
                 },
                  cancellationToken).ConfigureAwait(false);
            }
    #pragma warning disable CA1031 //Do not catch general exception types (ignoring, see comment below)
            catch
    #pragma warning restore CA1031 //Do not catch general exception types
            {
                //ignore exceptions
                //if token exchange failed for any reason, tokenExchangeResponse above remains null, and a failure invoke response is sent to the caller.
                //This ensures the caller knows that the invoke has failed.
            }
            if (tokenExchangeResponse == null || string.IsNullOrEmpty(tokenExchangeResponse.Token))
            {
                return false;
            }
            return true;
        }
    
    ```

## <a name="see-also"></a>Vea también

* [Adición de autenticación a las extensiones de mensaje](add-authentication.md)
* [Uso del inicio de sesión único para bots](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Apertura de vínculos](link-unfurling.md)
