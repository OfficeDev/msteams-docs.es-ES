---
title: Compatibilidad con SSO para las extensiones de mensajería
author: KirtiPereira
description: Cómo habilitar la compatibilidad con SSO para las extensiones de mensajería
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: f7dc689da3f0e3e06b8f9c68836b6449c2ae9120
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020705"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a><span data-ttu-id="8be77-103">Compatibilidad con inicio de sesión único (SSO) para extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="8be77-103">Single sign-on (SSO) support for messaging extensions</span></span>
 
<span data-ttu-id="8be77-104">La compatibilidad con el inicio de sesión único ya está disponible para extensiones de mensajería y desamuesar vínculos.</span><span class="sxs-lookup"><span data-stu-id="8be77-104">Single sign-on support is now available for messaging extensions and link unfurling.</span></span> <span data-ttu-id="8be77-105">Al habilitar el inicio de sesión único (SSO) para las extensiones de mensajería, se actualiza silenciosamente el token de autenticación, lo que minimiza el número de veces que necesita escribir las credenciales de inicio de sesión para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8be77-105">Enabling Single sign-on (SSO) for messaging extensions silently refreshes the authentication token, which minimizes the number of times you need to enter your sign in credentials for Microsoft Teams.</span></span>

<span data-ttu-id="8be77-106">Este documento le guía sobre cómo habilitar el SSO y almacenar el token de autenticación, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="8be77-106">This document guides you on how to enable the SSO and store your authentication token, if required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8be77-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8be77-107">Prerequisites</span></span>

<span data-ttu-id="8be77-108">Los requisitos previos para habilitar SSO para extensiones de mensajería y desafutización de vínculos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="8be77-108">The prerequisite to enable SSO for messaging extensions and link unfurling are as follows:</span></span>
* <span data-ttu-id="8be77-109">Debe tener una [cuenta de Azure.](https://azure.microsoft.com/en-us/free/)</span><span class="sxs-lookup"><span data-stu-id="8be77-109">You must have an [Azure](https://azure.microsoft.com/en-us/free/) account.</span></span>
* <span data-ttu-id="8be77-110">Debes configurar la aplicación a través del portal de AAD y actualizar el manifiesto de la aplicación de Teams para el bot tal como se define en registrar la aplicación a través [del portal de AAD](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span><span class="sxs-lookup"><span data-stu-id="8be77-110">You must configure your app through the AAD portal, and update your Teams application manifest for your bot as defined in [register your app through the AAD portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span></span>

> [!NOTE]
> <span data-ttu-id="8be77-111">Para obtener más información sobre cómo crear una cuenta de Azure y actualizar el manifiesto de la aplicación, consulte [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span><span class="sxs-lookup"><span data-stu-id="8be77-111">For more information on creating an Azure account and updating your app manifest, see [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span></span>

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a><span data-ttu-id="8be77-112">Habilitar SSO para extensiones de mensajería y desafutización de vínculos</span><span class="sxs-lookup"><span data-stu-id="8be77-112">Enable SSO for messaging extensions and link unfurling</span></span>

<span data-ttu-id="8be77-113">Una vez completados los requisitos previos, puede habilitar SSO para extensiones de mensajería y deshacer vínculos.</span><span class="sxs-lookup"><span data-stu-id="8be77-113">After the prerequisites are completed, you can enable SSO for messaging extensions and link unfurling.</span></span>

<span data-ttu-id="8be77-114">**Para habilitar SSO**</span><span class="sxs-lookup"><span data-stu-id="8be77-114">**To enable SSO**</span></span>
1. <span data-ttu-id="8be77-115">Actualice los detalles de conexión [de OAuth de](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) bots en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8be77-115">Update your bots [OAuth connection](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) details in the Azure portal.</span></span>
2. <span data-ttu-id="8be77-116">Descargue el [ejemplo de extensiones de mensajería](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) y siga las instrucciones de configuración proporcionadas por el asistente.</span><span class="sxs-lookup"><span data-stu-id="8be77-116">Download the [messaging extensions sample](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) and follow the setup instructions provided by the wizard.</span></span>
   > [!NOTE]
   > <span data-ttu-id="8be77-117">Usa la conexión OAuth de bots al configurar las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8be77-117">Use your bots OAuth connection when setting up your messaging extensions.</span></span>
3. <span data-ttu-id="8be77-118">En el [archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs,](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) actualice el valor de *auth* a *silentAuth* en `OnTeamsMessagingExtensionQueryAsync` y/ o `OnTeamsAppBasedLinkQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="8be77-118">In the [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) file, update the value from *auth* to *silentAuth* in the `OnTeamsMessagingExtensionQueryAsync` and / or `OnTeamsAppBasedLinkQueryAsync`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="8be77-119">No se admiten otros controladores SSO, excepto el archivo `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` TeamsMessagingExtensionsSearchAuthConfigBot.cs.</span><span class="sxs-lookup"><span data-stu-id="8be77-119">We do not support other handlers SSO, except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the TeamsMessagingExtensionsSearchAuthConfigBot.cs file.</span></span>
   
4. <span data-ttu-id="8be77-120">El token se recibe en el controlador en la carga o en el , según el escenario en el que se habilita `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` el SSO `OnTeamsAppBasedLinkQueryAsync` para:</span><span class="sxs-lookup"><span data-stu-id="8be77-120">You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you are enabling the SSO for:</span></span>

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    <span data-ttu-id="8be77-121">Si usa la conexión OAuth, agregue el siguiente código al archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs para actualizar o agregar el token en el almacén:</span><span class="sxs-lookup"><span data-stu-id="8be77-121">If you are using the OAuth connection, add the following code to the TeamsMessagingExtensionsSearchAuthConfigBot.cs file to update or add the token in the store:</span></span>
    
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
                tokenExchangeResponse = await (turnContext.Adapter as IExtendedUserTokenProvider).ExchangeTokenAsync(
                 turnContext,
                 _connectionName,
                 turnContext.Activity.From.Id,
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

## <a name="see-also"></a><span data-ttu-id="8be77-122">Consulte también</span><span class="sxs-lookup"><span data-stu-id="8be77-122">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8be77-123">Agregar autenticación a las extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="8be77-123">Add authentication to your messaging extensions</span></span>](add-authentication.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="8be77-124">Usar SSO para bots</span><span class="sxs-lookup"><span data-stu-id="8be77-124">Use SSO for bots</span></span>](../../bots/how-to/authentication/auth-aad-sso-bots.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="8be77-125">Apertura de vínculos</span><span class="sxs-lookup"><span data-stu-id="8be77-125">Link unfurling</span></span>](link-unfurling.md)

