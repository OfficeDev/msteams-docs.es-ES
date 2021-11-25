---
title: Compatibilidad con SSO para las extensiones de mensajería
author: KirtiPereira
description: Obtenga información sobre cómo habilitar la compatibilidad con SSO para las extensiones de mensajería con ejemplos de código.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 3da2c19debd3275266b4f96ce62bdfb0c85c353b
ms.sourcegitcommit: ba911ce3de7d096514f876faf00e4174444e2285
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2021
ms.locfileid: "61178254"
---
# <a name="single-sign-on-support-for-messaging-extensions"></a>Compatibilidad con inicio de sesión único para extensiones de mensajería
 
La compatibilidad con inicio de sesión único (SSO) ya está disponible para extensiones de mensajería y desamuesar vínculos. Al habilitar el inicio de sesión único para las extensiones de mensajería de forma predeterminada, se actualiza el token de autenticación, lo que minimiza el número de veces que necesita escribir las credenciales de inicio de sesión para Microsoft Teams.

Este documento le guía sobre cómo habilitar el SSO y almacenar el token de autenticación, si es necesario.

## <a name="prerequisites"></a>Requisitos previos

Los requisitos previos para habilitar SSO para extensiones de mensajería y desafutización de vínculos son los siguientes:
* Debe tener una [cuenta de Azure.](https://azure.microsoft.com/free/)
* Debes configurar la aplicación a través del portal de AAD y actualizar el manifiesto de la aplicación Teams tu bot tal como se define en registrar la aplicación AAD [portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).

> [!NOTE]
> Para obtener más información sobre cómo crear una cuenta de Azure y actualizar el manifiesto de la aplicación, consulte [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>Habilitar SSO para extensiones de mensajería y desafutización de vínculos

Una vez completados los requisitos previos, puede habilitar SSO para extensiones de mensajería y deshacer vínculos.

**Para habilitar SSO**
1. Actualice los detalles de conexión [de OAuth de](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) bots en Azure Portal.
2. Descargue el [ejemplo de extensiones de mensajería](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) y siga las instrucciones de configuración proporcionadas por el asistente.
   > [!NOTE]
   > Usa la conexión OAuth de bots al configurar las extensiones de mensajería.
3. En el [archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs,](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) actualice el valor de *auth* a *silentAuth* en `OnTeamsMessagingExtensionQueryAsync` y/ o `OnTeamsAppBasedLinkQueryAsync` .  

    > [!NOTE]
    > No se admiten otros controladores SSO, excepto el archivo `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` TeamsMessagingExtensionsSearchAuthConfigBot.cs.
   
4. El token se recibe en el controlador en la carga o en el , según el escenario en el que se habilita `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` el SSO `OnTeamsAppBasedLinkQueryAsync` para:

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    Si usa la conexión OAuth, agregue el siguiente código al archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs para actualizar o agregar el token en el almacén:
    
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

* [Agregar autenticación a las extensiones de mensajería](add-authentication.md)
* [Usar SSO para bots](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Apertura de vínculos](link-unfurling.md)
