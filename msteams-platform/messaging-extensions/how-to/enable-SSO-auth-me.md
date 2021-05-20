---
title: Compatibilidad con SSO para sus extensiones de mensajería
author: KirtiPereira
description: Cómo habilitar la compatibilidad con SSO para las extensiones de mensajería
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 02d08506a07e955693531908f4f3cf16573a02c0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566204"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a><span data-ttu-id="91f90-103">Compatibilidad con inicio de sesión único (SSO) para extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="91f90-103">Single sign-on (SSO) support for messaging extensions</span></span>
 
<span data-ttu-id="91f90-104">La compatibilidad con inicio de sesión único ya está disponible para las extensiones de mensajería y la despliegación de vínculos.</span><span class="sxs-lookup"><span data-stu-id="91f90-104">Single sign-on support is now available for messaging extensions and link unfurling.</span></span> <span data-ttu-id="91f90-105">Habilitar el inicio de sesión único (SSO) para las extensiones de mensajería actualiza silenciosamente el token de autenticación, lo que minimiza el número de veces que debe escribir las credenciales de inicio de sesión para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="91f90-105">Enabling Single sign-on (SSO) for messaging extensions silently refreshes the authentication token, which minimizes the number of times you need to enter your sign in credentials for Microsoft Teams.</span></span>

<span data-ttu-id="91f90-106">Este documento le guía sobre cómo habilitar el SSO y almacenar su token de autenticación, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="91f90-106">This document guides you on how to enable the SSO and store your authentication token, if required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91f90-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="91f90-107">Prerequisites</span></span>

<span data-ttu-id="91f90-108">El requisito previo para habilitar SSO para las extensiones de mensajería y el despliegue de vínculos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="91f90-108">The prerequisite to enable SSO for messaging extensions and link unfurling are as follows:</span></span>
* <span data-ttu-id="91f90-109">Debe tener una cuenta [de Azure.](https://azure.microsoft.com/en-us/free/)</span><span class="sxs-lookup"><span data-stu-id="91f90-109">You must have an [Azure](https://azure.microsoft.com/en-us/free/) account.</span></span>
* <span data-ttu-id="91f90-110">Debe configurar la aplicación a través del portal de AAD y actualizar el manifiesto de aplicación Teams para el bot tal como se define en [registrar la aplicación a través del portal de AAD.](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="91f90-110">You must configure your app through the AAD portal, and update your Teams application manifest for your bot as defined in [register your app through the AAD portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span></span>

> [!NOTE]
> <span data-ttu-id="91f90-111">Para obtener más información sobre cómo crear una cuenta de Azure y actualizar el manifiesto de la aplicación, consulte [Compatibilidad con inicio de sesión único (SSO) para bots.](../../bots/how-to/authentication/auth-aad-sso-bots.md)</span><span class="sxs-lookup"><span data-stu-id="91f90-111">For more information on creating an Azure account and updating your app manifest, see [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span></span>

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a><span data-ttu-id="91f90-112">Habilitar SSO para extensiones de mensajería y despliegue de enlaces</span><span class="sxs-lookup"><span data-stu-id="91f90-112">Enable SSO for messaging extensions and link unfurling</span></span>

<span data-ttu-id="91f90-113">Una vez completados los requisitos previos, puede habilitar SSO para las extensiones de mensajería y la despliegación de vínculos.</span><span class="sxs-lookup"><span data-stu-id="91f90-113">After the prerequisites are completed, you can enable SSO for messaging extensions and link unfurling.</span></span>

<span data-ttu-id="91f90-114">**Para habilitar SSO**</span><span class="sxs-lookup"><span data-stu-id="91f90-114">**To enable SSO**</span></span>
1. <span data-ttu-id="91f90-115">Actualice los detalles [de conexión de OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) de los bots en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="91f90-115">Update your bots [OAuth connection](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) details in the Azure portal.</span></span>
2. <span data-ttu-id="91f90-116">Descargue el [ejemplo de extensiones de mensajería](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) y siga las instrucciones de configuración proporcionadas por el asistente.</span><span class="sxs-lookup"><span data-stu-id="91f90-116">Download the [messaging extensions sample](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) and follow the setup instructions provided by the wizard.</span></span>
   > [!NOTE]
   > <span data-ttu-id="91f90-117">Utilice la conexión OAuth de bots al configurar las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="91f90-117">Use your bots OAuth connection when setting up your messaging extensions.</span></span>
3. <span data-ttu-id="91f90-118">En el archivo [TeamsMessagingExtensionsSearchAuthConfigBot.cs,](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) actualice el valor del *autenticación* a *silentAuth* en el `OnTeamsMessagingExtensionQueryAsync` archivo and/o `OnTeamsAppBasedLinkQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="91f90-118">In the [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) file, update the value from *auth* to *silentAuth* in the `OnTeamsMessagingExtensionQueryAsync` and / or `OnTeamsAppBasedLinkQueryAsync`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="91f90-119">No somos compatibles con otros controladores SSO, excepto `OnTeamsMessagingExtensionQueryAsync` y `OnTeamsAppBasedLinkQueryAsync` desde el TeamsMessagingExtensionsSearchAuthConfigBot.cs archivo.</span><span class="sxs-lookup"><span data-stu-id="91f90-119">We do not support other handlers SSO, except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the TeamsMessagingExtensionsSearchAuthConfigBot.cs file.</span></span>
   
4. <span data-ttu-id="91f90-120">Recibirá el token en `OnTeamsMessagingExtensionQueryAsync` el controlador en la carga útil o en el , dependiendo del escenario que esté `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync` habilitando el SSO para:</span><span class="sxs-lookup"><span data-stu-id="91f90-120">You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you are enabling the SSO for:</span></span>

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    <span data-ttu-id="91f90-121">Si usa la conexión OAuth, agregue el código siguiente al archivo TeamsMessagingExtensionsSearchAuthConfigBot.cs para actualizar o agregar el token en el almacén:</span><span class="sxs-lookup"><span data-stu-id="91f90-121">If you are using the OAuth connection, add the following code to the TeamsMessagingExtensionsSearchAuthConfigBot.cs file to update or add the token in the store:</span></span>
    
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

## <a name="see-also"></a><span data-ttu-id="91f90-122">Vea también</span><span class="sxs-lookup"><span data-stu-id="91f90-122">See also</span></span>

* [<span data-ttu-id="91f90-123">Agregue autenticación a las extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="91f90-123">Add authentication to your messaging extensions</span></span>](add-authentication.md)
* [<span data-ttu-id="91f90-124">Usar SSO para bots</span><span class="sxs-lookup"><span data-stu-id="91f90-124">Use SSO for bots</span></span>](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [<span data-ttu-id="91f90-125">Apertura de vínculos</span><span class="sxs-lookup"><span data-stu-id="91f90-125">Link unfurling</span></span>](link-unfurling.md)

