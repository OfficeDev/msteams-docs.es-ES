---
title: Compatibilidad del SSO con las extensiones de mensajes
author: KirtiPereira
description: Aprenda a habilitar la compatibilidad con el SSO para las extensiones de mensajería con ejemplos de código.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: bba2a8a225a75c21c46a242dec8acc55dcc0e8b5
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2022
ms.locfileid: "65296948"
---
# <a name="single-sign-on-support-for-message-extensions"></a>Compatibilidad con el inicio de sesión único para las extensiones de mensajes

Las extensiones de mensajes y el despliegue de vínculos ya admiten el inicio de sesión único (SSO). Al habilitar el inicio de sesión único para las extensiones de mensajes de forma predeterminada, se actualiza el token de autenticación, lo que minimiza el número de veces que necesita escribir las credenciales de inicio de sesión en Microsoft Teams.

En este documento se explica cómo habilitar el inicio de sesión único y almacenar el token de autenticación, si es necesario.

## <a name="prerequisites"></a>Requisitos previos

Los requisitos previos para habilitar el SSO para las extensiones de mensajes y la apertura de vínculos son los siguientes:

* Debe tener una cuenta de [Azure](https://azure.microsoft.com/free/).
* Debe configurar la aplicación a través del portal Azure AD y actualizar el manifiesto de la aplicación Teams tal como se define en [Registrar la aplicación a través del portal Azure AD](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal).

> [!NOTE]
> Para más información sobre cómo crear una cuenta Azure y actualizar el manifiesto de su aplicación, consulte [Compatibilidad con el inicio de sesión único (SSO) para los bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-message-extensions-and-link-unfurling"></a>Habilitar el inicio de sesión único para las extensiones de mensajes y la apertura de vínculos

Una vez completados los requisitos previos, puede habilitar el SSO para las extensiones de mensajes y la apertura de vínculos.

Para habilitar el SSO:

1. Actualice los detalles de [conexión OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) de sus bots en el portal Microsoft Azure.
2. Descargue el [ejemplo de extensiones de mensajes](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) y siga las instrucciones de configuración proporcionadas por el asistente.
   > [!NOTE]
   > Use la conexión OAuth de bots al configurar las extensiones de mensajes.
3. En el archivo [TeamsMessagingExtensionsSearchAuthConfigBot.cs,](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) actualice el valor de *auth* a *silentAuth* en el `OnTeamsMessagingExtensionQueryAsync` y/o `OnTeamsAppBasedLinkQueryAsync`.  

    > [!NOTE]
    > No se admite el SSO de otros controladores, excepto de `OnTeamsMessagingExtensionQueryAsync` y `OnTeamsAppBasedLinkQueryAsync` del archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs.

4. Recibirá el token en el controlador `OnTeamsMessagingExtensionQueryAsync` en la carga `turnContext.Activity.Value` o en el `OnTeamsAppBasedLinkQueryAsync`, en función del escenario para el que esté habilitando el inicio de sesión único:

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    Si usa la conexión OAuth, agregue el código siguiente al archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs para actualizar o agregar el token en el almacén:

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

## <a name="see-also"></a>Consulte también

* [Agregar autenticación a las extensiones de mensajes](add-authentication.md)
* [Usar el SSO para los bots](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Apertura de vínculos](link-unfurling.md)
