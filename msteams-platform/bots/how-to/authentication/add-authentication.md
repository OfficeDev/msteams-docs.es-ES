---
title: Agregar autenticación al bot Teams usuario
author: clearab
description: Cómo agregar la autenticación de OAuth a un bot en Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 7f171a791a9ee557e4af2e7d1e1b053046bd9db5
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101491"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="0a228-103">Agregar autenticación al bot Teams usuario</span><span class="sxs-lookup"><span data-stu-id="0a228-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="0a228-104">Hay ocasiones en las que es posible que necesite crear bots en Microsoft Teams que puedan tener acceso a recursos en nombre del usuario, como un servicio de correo.</span><span class="sxs-lookup"><span data-stu-id="0a228-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="0a228-105">En este artículo se muestra cómo usar la autenticación del SDK de Azure Bot Service v4, basada en OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0a228-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="0a228-106">Esto facilita el desarrollo de un bot que puede usar tokens de autenticación en función de las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="0a228-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="0a228-107">La clave en todo esto es el uso de proveedores **de identidades,** como veremos más adelante.</span><span class="sxs-lookup"><span data-stu-id="0a228-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="0a228-108">OAuth 2.0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory (Azure AD) y otros muchos proveedores de identidad.</span><span class="sxs-lookup"><span data-stu-id="0a228-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="0a228-109">Un conocimiento básico de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams.</span><span class="sxs-lookup"><span data-stu-id="0a228-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="0a228-110">Consulta [OAuth 2 Simplified para](https://aka.ms/oauth2-simplified) obtener una descripción básica y [OAuth 2.0](https://oauth.net/2/) para obtener la especificación completa.</span><span class="sxs-lookup"><span data-stu-id="0a228-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="0a228-111">Para obtener más información acerca de cómo el Servicio de bots de Azure controla la autenticación, vea [Autenticación de usuario en una conversación](https://aka.ms/azure-bot-authentication).</span><span class="sxs-lookup"><span data-stu-id="0a228-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="0a228-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a228-112">In this article you'll learn:</span></span>

- <span data-ttu-id="0a228-113">**Cómo crear un bot habilitado para autenticación**.</span><span class="sxs-lookup"><span data-stu-id="0a228-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="0a228-114">Usará [cs-auth-sample][teams-auth-bot-cs] para controlar las credenciales de inicio de sesión del usuario y la generación del token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="0a228-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="0a228-115">**Cómo implementar el bot en Azure y asociarlo a un proveedor de identidades.**</span><span class="sxs-lookup"><span data-stu-id="0a228-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="0a228-116">El proveedor emite un token en función de las credenciales de inicio de sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="0a228-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="0a228-117">El bot puede usar el token para obtener acceso a recursos, como un servicio de correo, que requieren autenticación.</span><span class="sxs-lookup"><span data-stu-id="0a228-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="0a228-118">Para obtener más [información, vea Microsoft Teams de autenticación para bots](auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="0a228-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="0a228-119">**Cómo integrar el bot en Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="0a228-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="0a228-120">Una vez integrado el bot, puedes iniciar sesión e intercambiar mensajes con él en un chat.</span><span class="sxs-lookup"><span data-stu-id="0a228-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a228-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0a228-121">Prerequisites</span></span>

- <span data-ttu-id="0a228-122">Conocimiento de [los conceptos básicos del bot,][concept-basics] [la administración del estado,][concept-state]la biblioteca de cuadros de diálogo [y][concept-dialogs]cómo implementar el flujo secuencial [de conversación][simple-dialog].</span><span class="sxs-lookup"><span data-stu-id="0a228-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="0a228-123">Conocimiento del desarrollo de Azure y OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0a228-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="0a228-124">Las versiones actuales de Visual Studio y Git.</span><span class="sxs-lookup"><span data-stu-id="0a228-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="0a228-125">Cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a228-125">Azure account.</span></span> <span data-ttu-id="0a228-126">Si es necesario, puede crear una cuenta [gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0a228-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="0a228-127">El ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="0a228-127">The following sample.</span></span>

    | <span data-ttu-id="0a228-128">Muestra</span><span class="sxs-lookup"><span data-stu-id="0a228-128">Sample</span></span> | <span data-ttu-id="0a228-129">Versión de BotBuilder</span><span class="sxs-lookup"><span data-stu-id="0a228-129">BotBuilder version</span></span> | <span data-ttu-id="0a228-130">Demostraciones</span><span class="sxs-lookup"><span data-stu-id="0a228-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="0a228-131">**Autenticación de** [bot en cs-auth-sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="0a228-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="0a228-132">v4</span><span class="sxs-lookup"><span data-stu-id="0a228-132">v4</span></span> | <span data-ttu-id="0a228-133">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="0a228-133">OAuthCard support</span></span> |
    | <span data-ttu-id="0a228-134">**Autenticación de** bot [en js-auth-sample][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="0a228-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="0a228-135">v4</span><span class="sxs-lookup"><span data-stu-id="0a228-135">v4</span></span>| <span data-ttu-id="0a228-136">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="0a228-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="0a228-137">**Autenticación de bot** [en py-auth-sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="0a228-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="0a228-138">v4</span><span class="sxs-lookup"><span data-stu-id="0a228-138">v4</span></span> | <span data-ttu-id="0a228-139">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="0a228-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="0a228-140">Crear el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0a228-140">Create the resource group</span></span>

<span data-ttu-id="0a228-141">El grupo de recursos y el plan de servicio no son estrictamente necesarios, pero permiten liberar cómodamente los recursos que cree.</span><span class="sxs-lookup"><span data-stu-id="0a228-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="0a228-142">Este es un buen procedimiento para mantener los recursos organizados y manejables.</span><span class="sxs-lookup"><span data-stu-id="0a228-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="0a228-143">Se usa un grupo de recursos para crear recursos individuales para Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0a228-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="0a228-144">Para obtener rendimiento, asegúrese de que estos recursos se encuentran en la misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a228-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="0a228-145">En el explorador, inicie sesión en [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="0a228-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="0a228-146">En el panel de navegación izquierdo, seleccione **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="0a228-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="0a228-147">En la parte superior izquierda de la ventana mostrada, seleccione **La** pestaña Agregar para crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a228-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="0a228-148">Se le pedirá que proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a228-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="0a228-149">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="0a228-149">**Subscription**.</span></span> <span data-ttu-id="0a228-150">Use la suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="0a228-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="0a228-151">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="0a228-151">**Resource group**.</span></span> <span data-ttu-id="0a228-152">Escriba el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a228-152">Enter the name for the resource group.</span></span> <span data-ttu-id="0a228-153">Un ejemplo podría ser  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0a228-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="0a228-154">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="0a228-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="0a228-155">En el **menú** desplegable Región, seleccione *Oeste de EE.* UU. o una región cercana a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0a228-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="0a228-156">Seleccione el **botón Revisar y** crear.</span><span class="sxs-lookup"><span data-stu-id="0a228-156">Select the **Review and create** button.</span></span> <span data-ttu-id="0a228-157">Debería ver un banner que lee *Validación pasada*.</span><span class="sxs-lookup"><span data-stu-id="0a228-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="0a228-158">Seleccione el **botón** Crear.</span><span class="sxs-lookup"><span data-stu-id="0a228-158">Select the **Create** button.</span></span> <span data-ttu-id="0a228-159">Puede tardar unos minutos en crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a228-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="0a228-160">Al igual que con los recursos que crearás más adelante en este tutorial, es buena idea anclar este grupo de recursos al panel para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="0a228-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="0a228-161">Si desea hacerlo, seleccione el icono de patilla &#128204; en la parte superior derecha del panel.</span><span class="sxs-lookup"><span data-stu-id="0a228-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="0a228-162">Crear el plan de servicio</span><span class="sxs-lookup"><span data-stu-id="0a228-162">Create the service plan</span></span>

1. <span data-ttu-id="0a228-163">En [**Azure Portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="0a228-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="0a228-164">En el cuadro de búsqueda, escriba *Plan de App Service*.</span><span class="sxs-lookup"><span data-stu-id="0a228-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="0a228-165">Seleccione la **tarjeta Plan de App Service** en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0a228-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="0a228-166">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0a228-166">Select **Create**.</span></span>
1. <span data-ttu-id="0a228-167">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="0a228-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="0a228-168">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="0a228-168">**Subscription**.</span></span> <span data-ttu-id="0a228-169">Puede usar una suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="0a228-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="0a228-170">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="0a228-170">**Resource Group**.</span></span> <span data-ttu-id="0a228-171">Seleccione el grupo que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0a228-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="0a228-172">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="0a228-172">**Name**.</span></span> <span data-ttu-id="0a228-173">Escriba el nombre del plan de servicio.</span><span class="sxs-lookup"><span data-stu-id="0a228-173">Enter the name for the service plan.</span></span> <span data-ttu-id="0a228-174">Un ejemplo podría ser  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="0a228-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="0a228-175">Recuerde que el nombre debe ser único, dentro del grupo.</span><span class="sxs-lookup"><span data-stu-id="0a228-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="0a228-176">**Sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="0a228-176">**Operating System**.</span></span> <span data-ttu-id="0a228-177">Seleccione *Windows* o el sistema operativo aplicable.</span><span class="sxs-lookup"><span data-stu-id="0a228-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="0a228-178">**Región**.</span><span class="sxs-lookup"><span data-stu-id="0a228-178">**Region**.</span></span> <span data-ttu-id="0a228-179">Seleccione *Oeste de EE. UU.* o una región cercana a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0a228-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="0a228-180">**Plan de precios**.</span><span class="sxs-lookup"><span data-stu-id="0a228-180">**Pricing Tier**.</span></span> <span data-ttu-id="0a228-181">Asegúrese de que *standard S1* está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="0a228-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="0a228-182">Este debe ser el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0a228-182">This should be the default value.</span></span>
    1. <span data-ttu-id="0a228-183">Seleccione el **botón Revisar y** crear.</span><span class="sxs-lookup"><span data-stu-id="0a228-183">Select the **Review and create** button.</span></span> <span data-ttu-id="0a228-184">Debería ver un banner que lee *Validación pasada*.</span><span class="sxs-lookup"><span data-stu-id="0a228-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="0a228-185">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0a228-185">Select **Create**.</span></span> <span data-ttu-id="0a228-186">Puede tardar unos minutos en crear el plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0a228-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="0a228-187">El plan se enumerará en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a228-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="0a228-188">Crear el registro de canales de bot</span><span class="sxs-lookup"><span data-stu-id="0a228-188">Create the bot channels registration</span></span>

<span data-ttu-id="0a228-189">El registro de canales de bot registra el servicio web como un bot con Bot Framework, siempre que tenga un identificador de aplicación de Microsoft y una contraseña de aplicación (secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="0a228-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a228-190">Solo necesita registrar el bot si no está hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="0a228-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="0a228-191">Si [creó un bot a](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) través de Azure Portal, ya está registrado en el servicio.</span><span class="sxs-lookup"><span data-stu-id="0a228-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="0a228-192">Si creó el bot a través de [Bot Framework](https://dev.botframework.com/bots/new) o [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) el bot no está registrado en Azure.</span><span class="sxs-lookup"><span data-stu-id="0a228-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="0a228-193">El recurso Registro de canales bot mostrará la región **Global** incluso si seleccionó Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="0a228-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="0a228-194">Esto se espera.</span><span class="sxs-lookup"><span data-stu-id="0a228-194">This is expected.</span></span>

<span data-ttu-id="0a228-195">Para obtener más información, vea [Create a bot for Teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="0a228-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="0a228-196">Crear el proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="0a228-196">Create the identity provider</span></span>

<span data-ttu-id="0a228-197">Necesita un proveedor de identidades que se pueda usar para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="0a228-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="0a228-198">En este procedimiento, usará un proveedor de Azure AD; También se pueden usar otros proveedores de identidad compatibles con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a228-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="0a228-199">En [**azure portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a228-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="0a228-200">Deberá crear y registrar este recurso de Azure AD en un espacio empresarial en el que pueda dar su consentimiento para delegar los permisos solicitados por una aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a228-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="0a228-201">Para obtener instrucciones sobre cómo crear un inquilino, vea [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span><span class="sxs-lookup"><span data-stu-id="0a228-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="0a228-202">En el panel izquierdo, seleccione **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0a228-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="0a228-203">En el panel derecho, seleccione la **pestaña Nuevo registro,** en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="0a228-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="0a228-204">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="0a228-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="0a228-205">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="0a228-205">**Name**.</span></span> <span data-ttu-id="0a228-206">Escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a228-206">Enter the name for the application.</span></span> <span data-ttu-id="0a228-207">Un ejemplo podría ser  *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="0a228-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="0a228-208">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="0a228-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="0a228-209">Seleccione los **tipos de cuenta admitidos** para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a228-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="0a228-210">Selecciona Cuentas en cualquier directorio de la organización (cualquier directorio de Azure AD - Multitenant) y cuentas personales de *Microsoft (por ejemplo, Skype, Xbox).*</span><span class="sxs-lookup"><span data-stu-id="0a228-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="0a228-211">Para el **URI de redireccionamiento**:</span><span class="sxs-lookup"><span data-stu-id="0a228-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="0a228-212">&#x2713;Seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="0a228-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="0a228-213">&#x2713; Establezca la dirección URL en `https://token.botframework.com/.auth/web/redirect` .</span><span class="sxs-lookup"><span data-stu-id="0a228-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="0a228-214">Seleccione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-214">Select **Register**.</span></span>

1. <span data-ttu-id="0a228-215">Una vez creado, Azure muestra la **página Información** general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a228-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="0a228-216">Copie y guarde la siguiente información en un archivo:</span><span class="sxs-lookup"><span data-stu-id="0a228-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="0a228-217">Valor **de id. de aplicación (cliente).**</span><span class="sxs-lookup"><span data-stu-id="0a228-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="0a228-218">Este valor se usará más adelante como *identificador* de cliente al registrar esta aplicación de identidad de Azure con el bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="0a228-219">Valor **del id. de directorio (espacio** empresarial).</span><span class="sxs-lookup"><span data-stu-id="0a228-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="0a228-220">También usarás este valor más adelante como identificador *de* inquilino para registrar esta aplicación de identidad de Azure con el bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="0a228-221">En el panel izquierdo, seleccione **Certificados & secretos para** crear un secreto de cliente para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a228-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="0a228-222">En **Secretos de** cliente, &#x2795; **Nuevo secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="0a228-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="0a228-223">Agrega una descripción para identificar este secreto de otros usuarios que podrías necesitar crear para esta aplicación, como la aplicación de identidad bot *en Teams*.</span><span class="sxs-lookup"><span data-stu-id="0a228-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="0a228-224">Establece **Expira en** la selección.</span><span class="sxs-lookup"><span data-stu-id="0a228-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="0a228-225">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-225">Select **Add**.</span></span>
   1. <span data-ttu-id="0a228-226">Antes de salir de esta página, **registre el secreto**.</span><span class="sxs-lookup"><span data-stu-id="0a228-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="0a228-227">Este valor se usará más adelante como _secreto_ de cliente al registrar la aplicación de Azure AD con el bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="0a228-228">Configurar la conexión del proveedor de identidades y registrarla con el bot</span><span class="sxs-lookup"><span data-stu-id="0a228-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="0a228-229">Nota: hay dos opciones para los proveedores de servicios aquí:Azure AD V1 y Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="0a228-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="0a228-230">Las diferencias entre los dos proveedores se resumen [aquí,](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)pero, en general, V2 proporciona más flexibilidad con respecto a cambiar los permisos del bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="0a228-231">Graph Los permisos de API se enumeran en el campo ámbitos y, a medida que se agregan los nuevos, los bots permitirán a los usuarios dar su consentimiento a los nuevos permisos en el siguiente inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="0a228-232">Para V1, el usuario debe eliminar el consentimiento del bot para que se pidan nuevos permisos en el cuadro de diálogo OAuth.</span><span class="sxs-lookup"><span data-stu-id="0a228-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="0a228-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="0a228-233">Azure AD V1</span></span>

1. <span data-ttu-id="0a228-234">En [**Azure Portal,**][azure-portal]seleccione el grupo de recursos en el panel.</span><span class="sxs-lookup"><span data-stu-id="0a228-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="0a228-235">Seleccione el vínculo de registro del canal de bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="0a228-236">Abra la página de recursos y seleccione **Configuración** **en Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0a228-236">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="0a228-237">Seleccione **Agregar conexión de OAuth Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0a228-237">Select **Add OAuth Connection Settings**.</span></span>    
<span data-ttu-id="0a228-238">La siguiente imagen muestra la selección correspondiente en la página de recursos:</span><span class="sxs-lookup"><span data-stu-id="0a228-238">The following image displays the corresponding selection in the resource page:</span></span>  
<span data-ttu-id="0a228-239">![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="0a228-239">![SampleAppDemoBot configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span>
1. <span data-ttu-id="0a228-240">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="0a228-240">Complete the form as follows:</span></span>

    1. <span data-ttu-id="0a228-241">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="0a228-241">**Name**.</span></span> <span data-ttu-id="0a228-242">Escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="0a228-242">Enter a name for the connection.</span></span> <span data-ttu-id="0a228-243">Usarás este nombre en el bot en el `appsettings.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="0a228-243">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="0a228-244">Por ejemplo *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="0a228-244">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="0a228-245">**Proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="0a228-245">**Service Provider**.</span></span> <span data-ttu-id="0a228-246">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a228-246">Select **Azure Active Directory**.</span></span> <span data-ttu-id="0a228-247">Una vez seleccionado, se mostrarán los campos específicos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a228-247">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="0a228-248">**Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="0a228-248">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="0a228-249">**Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="0a228-249">**Client secret**.</span></span> <span data-ttu-id="0a228-250">Escriba el secreto que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="0a228-250">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="0a228-251">**Tipo de concesión**.</span><span class="sxs-lookup"><span data-stu-id="0a228-251">**Grant Type**.</span></span> <span data-ttu-id="0a228-252">Escriba `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="0a228-252">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="0a228-253">**Dirección URL de inicio de** sesión .</span><span class="sxs-lookup"><span data-stu-id="0a228-253">**Login URL**.</span></span> <span data-ttu-id="0a228-254">Escriba `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="0a228-254">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="0a228-255">**Identificador de inquilino**, escriba el id. de directorio  **(espacio empresarial)** que registró anteriormente para la aplicación de identidad de Azure o común según el tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="0a228-255">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="0a228-256">Para decidir qué valor asignar, siga estos criterios:</span><span class="sxs-lookup"><span data-stu-id="0a228-256">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="0a228-257">Si seleccionó Cuentas solo en este directorio de la organización *(Solo Microsoft -* Inquilino único) o  Cuentas en cualquier directorio de la organización *(directorio de Microsoft AAD - Inquilino múltiple)* escriba el identificador de inquilino que registró anteriormente para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="0a228-257">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="0a228-258">Este será el espacio empresarial asociado con los usuarios que se pueden autenticar.</span><span class="sxs-lookup"><span data-stu-id="0a228-258">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="0a228-259">Si seleccionó Cuentas en cualquier directorio de la organización (cualquier directorio de AAD: cuentas de Microsoft multiinquilino y personales, por *ejemplo, Skype, Xbox, Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="0a228-259">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="0a228-260">De lo contrario, la aplicación de AAD comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a228-260">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="0a228-261">h.</span><span class="sxs-lookup"><span data-stu-id="0a228-261">h.</span></span> <span data-ttu-id="0a228-262">En **Dirección URL de** recurso , escriba `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="0a228-262">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="0a228-263">Esto no se usa en el ejemplo de código actual.</span><span class="sxs-lookup"><span data-stu-id="0a228-263">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="0a228-264">i.</span><span class="sxs-lookup"><span data-stu-id="0a228-264">i.</span></span> <span data-ttu-id="0a228-265">Deje **ámbitos en** blanco.</span><span class="sxs-lookup"><span data-stu-id="0a228-265">Leave **Scopes** blank.</span></span> <span data-ttu-id="0a228-266">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a228-266">The following image is an example:</span></span>

    ![vista de cadena de conexión de la aplicación de bots de teams adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="0a228-268">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-268">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="0a228-269">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="0a228-269">Azure AD V2</span></span>

1. <span data-ttu-id="0a228-270">En [**Azure Portal,**][azure-portal]seleccione el grupo de recursos en el panel.</span><span class="sxs-lookup"><span data-stu-id="0a228-270">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="0a228-271">Seleccione el vínculo de registro del canal de bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-271">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="0a228-272">Abra la página de recursos y seleccione **Configuración** **en Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0a228-272">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="0a228-273">Seleccione **Agregar conexión de OAuth Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0a228-273">Select **Add OAuth Connection Settings**.</span></span>  
<span data-ttu-id="0a228-274">La siguiente imagen muestra la selección correspondiente en la página de recursos:</span><span class="sxs-lookup"><span data-stu-id="0a228-274">The following image displays the corresponding selection in the resource page:</span></span>        
<span data-ttu-id="0a228-275">![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="0a228-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span> 

1. <span data-ttu-id="0a228-276">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="0a228-276">Complete the form as follows:</span></span>

    1. <span data-ttu-id="0a228-277">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="0a228-277">**Name**.</span></span> <span data-ttu-id="0a228-278">Escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="0a228-278">Enter a name for the connection.</span></span> <span data-ttu-id="0a228-279">Usarás este nombre en el bot en el `appsettings.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="0a228-279">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="0a228-280">Por ejemplo *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="0a228-280">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="0a228-281">**Proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="0a228-281">**Service Provider**.</span></span> <span data-ttu-id="0a228-282">Seleccione **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="0a228-282">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="0a228-283">Una vez seleccionado, se mostrarán los campos específicos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a228-283">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="0a228-284">**Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="0a228-284">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="0a228-285">**Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="0a228-285">**Client secret**.</span></span> <span data-ttu-id="0a228-286">Escriba el secreto que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="0a228-286">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="0a228-287">**Dirección URL Exchange token**.</span><span class="sxs-lookup"><span data-stu-id="0a228-287">**Token Exchange URL**.</span></span> <span data-ttu-id="0a228-288">Deje esto en blanco.</span><span class="sxs-lookup"><span data-stu-id="0a228-288">Leave this blank.</span></span>
    1. <span data-ttu-id="0a228-289">**Identificador de inquilino**, escriba el id. de directorio  **(espacio empresarial)** que registró anteriormente para la aplicación de identidad de Azure o común según el tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="0a228-289">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="0a228-290">Para decidir qué valor asignar, siga estos criterios:</span><span class="sxs-lookup"><span data-stu-id="0a228-290">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="0a228-291">Si seleccionó Cuentas solo en este directorio de la organización *(Solo Microsoft -* Inquilino único) o  Cuentas en cualquier directorio de la organización *(directorio de Microsoft AAD - Inquilino múltiple)* escriba el identificador de inquilino que registró anteriormente para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="0a228-291">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="0a228-292">Este será el espacio empresarial asociado con los usuarios que se pueden autenticar.</span><span class="sxs-lookup"><span data-stu-id="0a228-292">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="0a228-293">Si seleccionó Cuentas en cualquier directorio de la organización (cualquier directorio de AAD: cuentas de Microsoft multiinquilino y personales, por *ejemplo, Skype, Xbox, Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="0a228-293">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="0a228-294">De lo contrario, la aplicación de AAD comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a228-294">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="0a228-295">Para **Ámbitos,** escriba una lista delimitada por espacios de permisos de gráfico que esta aplicación requiere, por ejemplo: User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="0a228-295">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="0a228-296">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-296">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="0a228-297">Probar la conexión</span><span class="sxs-lookup"><span data-stu-id="0a228-297">Test the connection</span></span>

1. <span data-ttu-id="0a228-298">Seleccione la entrada de conexión para abrir la conexión que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="0a228-298">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="0a228-299">Seleccione **Probar conexión en** la parte superior del panel Configuración de conexión del proveedor **de** servicios.</span><span class="sxs-lookup"><span data-stu-id="0a228-299">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="0a228-300">La primera vez que lo hagas, se abrirá una nueva ventana del explorador que te pedirá que selecciones una cuenta.</span><span class="sxs-lookup"><span data-stu-id="0a228-300">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="0a228-301">Seleccione la que desea usar.</span><span class="sxs-lookup"><span data-stu-id="0a228-301">Select the one you want to use.</span></span>
1. <span data-ttu-id="0a228-302">A continuación, se le pedirá que permita al proveedor de identidades usar sus datos (credenciales).</span><span class="sxs-lookup"><span data-stu-id="0a228-302">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="0a228-303">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a228-303">The following image is an example:</span></span>

    ![cadena de conexión de autenticación de bots de teams adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="0a228-305">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-305">Select **Accept**.</span></span>
1. <span data-ttu-id="0a228-306">A continuación, debería redirigirle a una **página Conexión de prueba a \<your-connection-name> Correcta.**</span><span class="sxs-lookup"><span data-stu-id="0a228-306">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="0a228-307">Actualice la página si recibe un error.</span><span class="sxs-lookup"><span data-stu-id="0a228-307">Refresh the page if you get an error.</span></span> <span data-ttu-id="0a228-308">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a228-308">The following image is an example:</span></span>

  ![teams bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="0a228-310">El código de bot usa el nombre de conexión para recuperar tokens de autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="0a228-310">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="0a228-311">Preparar el código de ejemplo del bot</span><span class="sxs-lookup"><span data-stu-id="0a228-311">Prepare the bot sample code</span></span>

<span data-ttu-id="0a228-312">Una vez realizada la configuración preliminar, vamos a centrarnos en la creación del bot que se va a usar en este artículo.</span><span class="sxs-lookup"><span data-stu-id="0a228-312">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0a228-313">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0a228-313">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="0a228-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="0a228-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="0a228-315">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0a228-315">Launch Visual Studio.</span></span>
1. <span data-ttu-id="0a228-316">En la barra de **herramientas, seleccione Archivo -> Abrir -> Project/Solución** y abra el proyecto de bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-316">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="0a228-317">En C# actualizar **appsettings.jsde la** siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="0a228-317">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="0a228-318">Establezca `ConnectionName` el nombre de la conexión del proveedor de identidades que agregó al registro del canal de bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-318">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="0a228-319">El nombre que se usa en este ejemplo es *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="0a228-319">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="0a228-320">Se `MicrosoftAppId` establece en el identificador de aplicación del **bot** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-320">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="0a228-321">Se `MicrosoftAppPassword` establece en el secreto de **cliente** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-321">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="0a228-322">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML.</span><span class="sxs-lookup"><span data-stu-id="0a228-322">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="0a228-323">Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="0a228-323">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="0a228-324">En el Explorador de soluciones, vaya a la carpeta, abra y establezca y al identificador de aplicación del bot que guardó en el momento del registro `TeamsAppManifest` `manifest.json` del canal del `id` `botId` bot. </span><span class="sxs-lookup"><span data-stu-id="0a228-324">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="0a228-325">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0a228-325">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="0a228-326">Clone [node-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="0a228-326">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="0a228-327">En una consola, vaya al proyecto:</span><span class="sxs-lookup"><span data-stu-id="0a228-327">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="0a228-328">Instalar módulos</span><span class="sxs-lookup"><span data-stu-id="0a228-328">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="0a228-329">Actualice la **configuración .env** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="0a228-329">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="0a228-330">Se `MicrosoftAppId` establece en el identificador de aplicación del **bot** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-330">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="0a228-331">Se `MicrosoftAppPassword` establece en el secreto de **cliente** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-331">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="0a228-332">Establezca el `connectionName` valor en el nombre de la conexión del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="0a228-332">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="0a228-333">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML.</span><span class="sxs-lookup"><span data-stu-id="0a228-333">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="0a228-334">Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="0a228-334">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="0a228-335">En la carpeta, abra y establezca el id. de la aplicación de Microsoft y el id. de la aplicación bot que guardó en el momento del registro `teamsAppManifest` `manifest.json` del canal del `id`  `botId` bot. </span><span class="sxs-lookup"><span data-stu-id="0a228-335">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="0a228-336">Python</span><span class="sxs-lookup"><span data-stu-id="0a228-336">Python</span></span>](#tab/python)

1. <span data-ttu-id="0a228-337">Clone [py-auth-sample][teams-auth-bot-py] desde el repositorio de github.</span><span class="sxs-lookup"><span data-stu-id="0a228-337">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="0a228-338">Actualizar **config.py**:</span><span class="sxs-lookup"><span data-stu-id="0a228-338">Update **config.py**:</span></span>

    - <span data-ttu-id="0a228-339">Establezca el nombre de la configuración de conexión `ConnectionName` de OAuth que agregó al bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-339">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="0a228-340">Set `MicrosoftAppId` and to your `MicrosoftAppPassword` bot's app ID and app secret.</span><span class="sxs-lookup"><span data-stu-id="0a228-340">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="0a228-341">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML.</span><span class="sxs-lookup"><span data-stu-id="0a228-341">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="0a228-342">Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="0a228-342">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="0a228-343">Implementar el bot en Azure</span><span class="sxs-lookup"><span data-stu-id="0a228-343">Deploy the bot to Azure</span></span>

<span data-ttu-id="0a228-344">Para implementar el bot, siga los pasos descritos en el procedimiento para [implementar el bot en Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="0a228-344">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="0a228-345">Como alternativa, mientras esté Visual Studio, puede seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0a228-345">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="0a228-346">En Visual Studio *Explorador de soluciones,* seleccione y mantenga presionado (o haga clic con el botón secundario) en el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="0a228-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="0a228-347">En el menú desplegable, seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-347">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="0a228-348">En la ventana mostrada, seleccione el **vínculo** Nuevo.</span><span class="sxs-lookup"><span data-stu-id="0a228-348">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="0a228-349">En la ventana de diálogo, seleccione **App Service** a la izquierda y **Crear nuevo** a la derecha.</span><span class="sxs-lookup"><span data-stu-id="0a228-349">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="0a228-350">Seleccione el **botón** Publicar.</span><span class="sxs-lookup"><span data-stu-id="0a228-350">Select the **Publish** button.</span></span>
1. <span data-ttu-id="0a228-351">En la siguiente ventana de diálogo, escriba la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="0a228-351">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="0a228-352">A continuación puede ver un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a228-352">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="0a228-354">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0a228-354">Select **Create**.</span></span>
1. <span data-ttu-id="0a228-355">Si la implementación se completa correctamente, debería verlo reflejado en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0a228-355">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="0a228-356">Además, se muestra una página en el explorador predeterminado que dice *Que el bot está listo.*</span><span class="sxs-lookup"><span data-stu-id="0a228-356">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="0a228-357">La dirección URL será similar a esta: `https://botteamsauth.azurewebsites.net/` .</span><span class="sxs-lookup"><span data-stu-id="0a228-357">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="0a228-358">Guárdelo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="0a228-358">Save it to a file.</span></span>
1. <span data-ttu-id="0a228-359">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="0a228-359">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="0a228-360">Compruebe el grupo de recursos, el bot debe aparecer junto con los demás recursos.</span><span class="sxs-lookup"><span data-stu-id="0a228-360">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="0a228-361">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a228-361">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="0a228-363">En el grupo de recursos, seleccione el nombre de registro del canal bot (vínculo).</span><span class="sxs-lookup"><span data-stu-id="0a228-363">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="0a228-364">En el panel izquierdo, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0a228-364">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="0a228-365">En el **cuadro Punto de conexión** de mensajería, escriba la dirección URL obtenida anteriormente seguida de `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="0a228-365">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="0a228-366">Este es un ejemplo: `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="0a228-366">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="0a228-367">Seleccione el **botón** Guardar en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="0a228-367">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="0a228-368">Probar el bot con el emulador</span><span class="sxs-lookup"><span data-stu-id="0a228-368">Test the bot using the Emulator</span></span>

<span data-ttu-id="0a228-369">Si aún no lo ha hecho, instale el [archivo Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="0a228-369">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="0a228-370">Vea también [Depurar con el emulador](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="0a228-370">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="0a228-371">Para que el inicio de sesión de ejemplo del bot funcione, debe configurar el emulador como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0a228-371">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="0a228-372">Configurar el emulador para la autenticación</span><span class="sxs-lookup"><span data-stu-id="0a228-372">Configure the Emulator for authentication</span></span>

<span data-ttu-id="0a228-373">Si un bot requiere autenticación, debe configurar el emulador como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0a228-373">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="0a228-374">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="0a228-374">Start the Emulator.</span></span>
1. <span data-ttu-id="0a228-375">En el emulador, seleccione el icono de engranaje &#9881; en la parte inferior izquierda o la pestaña Configuración **emulador** en la parte superior derecha.</span><span class="sxs-lookup"><span data-stu-id="0a228-375">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="0a228-376">Active la casilla **usar tokens de autenticación de la versión 1.0**.</span><span class="sxs-lookup"><span data-stu-id="0a228-376">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="0a228-377">Escriba la ruta de acceso local a la **herramienta ngrok.**</span><span class="sxs-lookup"><span data-stu-id="0a228-377">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="0a228-378">*Vea* el wiki Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span><span class="sxs-lookup"><span data-stu-id="0a228-378">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="0a228-379">Para obtener más información sobre la herramienta, [vea ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="0a228-379">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="0a228-380">Active la casilla **Ejecutar ngrok cuando se inicie el emulador**.</span><span class="sxs-lookup"><span data-stu-id="0a228-380">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="0a228-381">Seleccione el **botón** Guardar.</span><span class="sxs-lookup"><span data-stu-id="0a228-381">Select the **Save** button.</span></span>

<span data-ttu-id="0a228-382">Cuando el bot muestra una tarjeta de inicio de sesión y el usuario selecciona el botón de inicio de sesión, el emulador abre una página que el usuario puede usar para iniciar sesión con el proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="0a228-382">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="0a228-383">Una vez que el usuario lo hace, el proveedor genera un token de usuario y lo envía al bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-383">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="0a228-384">Después, el bot puede actuar en nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="0a228-384">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="0a228-385">Probar el bot localmente</span><span class="sxs-lookup"><span data-stu-id="0a228-385">Test the bot locally</span></span>

<span data-ttu-id="0a228-386">Después de configurar el mecanismo de autenticación, puede realizar las pruebas de bot reales.</span><span class="sxs-lookup"><span data-stu-id="0a228-386">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="0a228-387">Ejecute el ejemplo de bot localmente en el equipo, por Visual Studio por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0a228-387">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="0a228-388">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="0a228-388">Start the Emulator.</span></span>
1. <span data-ttu-id="0a228-389">Seleccione el **botón Abrir bot.**</span><span class="sxs-lookup"><span data-stu-id="0a228-389">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="0a228-390">En la **dirección URL del bot,** escriba la dirección URL local del bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-390">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="0a228-391">Normalmente, `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="0a228-391">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="0a228-392">En el **Id. de aplicación de Microsoft,** escriba el identificador de aplicación del bot desde `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="0a228-392">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="0a228-393">En la **contraseña de Microsoft App,** escriba la contraseña de la aplicación del bot desde `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="0a228-393">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="0a228-394">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-394">Select **Connect**.</span></span>
1. <span data-ttu-id="0a228-395">Después de que el bot esté en funcionamiento, escriba cualquier texto para mostrar la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-395">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="0a228-396">Seleccione el **botón Iniciar sesión.**</span><span class="sxs-lookup"><span data-stu-id="0a228-396">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="0a228-397">Se muestra un cuadro de diálogo emergente para **Confirmar dirección URL abierta.**</span><span class="sxs-lookup"><span data-stu-id="0a228-397">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="0a228-398">Esto permite que el usuario del bot (usted) se autentique.</span><span class="sxs-lookup"><span data-stu-id="0a228-398">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="0a228-399">Seleccione **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-399">Select **Confirm**.</span></span>
1. <span data-ttu-id="0a228-400">Si se le pide, seleccione la cuenta del usuario aplicable.</span><span class="sxs-lookup"><span data-stu-id="0a228-400">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="0a228-401">Según la configuración que usó para el emulador, se obtiene una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="0a228-401">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="0a228-402">**Uso del código de verificación de inicio de sesión**</span><span class="sxs-lookup"><span data-stu-id="0a228-402">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="0a228-403">&#x2713; Se abre una ventana que muestra el código de validación.</span><span class="sxs-lookup"><span data-stu-id="0a228-403">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="0a228-404">&#x2713; copiar y escribir el código de validación en el cuadro de chat para completar el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-404">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="0a228-405">**Uso de tokens de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="0a228-405">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="0a228-406">&#x2713; Ha iniciado sesión en función de sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="0a228-406">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="0a228-407">La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="0a228-407">The following image is an example of the bot UI after you've logged in:</span></span>

    ![Emulador de inicio de sesión del bot de autenticación](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="0a228-409">Si selecciona **Sí cuando** el bot le pregunta ¿Le gustaría ver el *token?*, tendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a228-409">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![Token de emulador de inicio de sesión del bot de autenticación](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="0a228-411">Escriba **cerrar sesión en** el cuadro de chat de entrada para cerrar la sesión. Esto libera el token de usuario y el bot no podrá actuar en su nombre hasta que inicie sesión de nuevo.</span><span class="sxs-lookup"><span data-stu-id="0a228-411">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="0a228-412">La autenticación de bots requiere el uso del **servicio Bot Connector**.</span><span class="sxs-lookup"><span data-stu-id="0a228-412">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="0a228-413">El servicio tiene acceso a la información de registro de canales del bot para el bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-413">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="0a228-414">Probar el bot implementado</span><span class="sxs-lookup"><span data-stu-id="0a228-414">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="0a228-415">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="0a228-415">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="0a228-416">Busque el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a228-416">Find your resource group.</span></span>
1. <span data-ttu-id="0a228-417">Seleccione el vínculo de recurso.</span><span class="sxs-lookup"><span data-stu-id="0a228-417">Select the resource link.</span></span> <span data-ttu-id="0a228-418">Se muestra la página de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a228-418">The resource page is displayed.</span></span>
1. <span data-ttu-id="0a228-419">En la página de recursos, seleccione **Probar en chat web**.</span><span class="sxs-lookup"><span data-stu-id="0a228-419">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="0a228-420">El bot se inicia y muestra los saludos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="0a228-420">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="0a228-421">Escriba cualquier cosa en el cuadro de chat.</span><span class="sxs-lookup"><span data-stu-id="0a228-421">Type anything in the chat box.</span></span>
1. <span data-ttu-id="0a228-422">Seleccione el **cuadro Iniciar sesión.**</span><span class="sxs-lookup"><span data-stu-id="0a228-422">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="0a228-423">Se muestra un cuadro de diálogo emergente para **Confirmar dirección URL abierta.**</span><span class="sxs-lookup"><span data-stu-id="0a228-423">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="0a228-424">Esto permite que el usuario del bot (usted) se autentique.</span><span class="sxs-lookup"><span data-stu-id="0a228-424">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="0a228-425">Seleccione **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="0a228-425">Select **Confirm**.</span></span>
1. <span data-ttu-id="0a228-426">Si se le pide, seleccione la cuenta del usuario aplicable.</span><span class="sxs-lookup"><span data-stu-id="0a228-426">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="0a228-427">La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="0a228-427">The following image is an example of the bot UI after you have logged in:</span></span>

    ![Inicio de sesión del bot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="0a228-429">.</span><span class="sxs-lookup"><span data-stu-id="0a228-429">.</span></span>

1. <span data-ttu-id="0a228-430">Seleccione el **botón Sí** para mostrar el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="0a228-430">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="0a228-431">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a228-431">The following image is an example:</span></span>

    ![Token de inicio de sesión del bot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="0a228-433">.</span><span class="sxs-lookup"><span data-stu-id="0a228-433">.</span></span>

1. <span data-ttu-id="0a228-434">Escriba cerrar sesión para cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-434">Enter logout to sign out.</span></span>

    ![Inicio de sesión implementado por el bot de autenticación](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="0a228-436">Si tiene problemas para iniciar sesión, intente probar la conexión de nuevo como se describe en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="0a228-436">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="0a228-437">Esto podría volver a crear el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="0a228-437">This could recreate the authentication token.</span></span>
> <span data-ttu-id="0a228-438">Con el cliente de Chat web de Bot Framework en Azure, es posible que deba iniciar sesión varias veces antes de que la autenticación se establezca correctamente.</span><span class="sxs-lookup"><span data-stu-id="0a228-438">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="0a228-439">Instalar y probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="0a228-439">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="0a228-440">En el proyecto de bot, asegúrese de que la carpeta contiene la junto `TeamsAppManifest` con un y los `manifest.json` `outline.png` `color.png` archivos.</span><span class="sxs-lookup"><span data-stu-id="0a228-440">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="0a228-441">En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta.</span><span class="sxs-lookup"><span data-stu-id="0a228-441">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="0a228-442">Para `manifest.json` editar, asigne los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="0a228-442">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="0a228-443">Asegúrese de que **el identificador de aplicación del bot** que recibió en el momento del registro del canal del bot está asignado y `id` `botId` .</span><span class="sxs-lookup"><span data-stu-id="0a228-443">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="0a228-444">Asigne este valor: `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="0a228-444">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="0a228-445">Seleccione y **zip** los `manifest.json` archivos , `outline.png` `color.png` y.</span><span class="sxs-lookup"><span data-stu-id="0a228-445">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="0a228-446">Abra **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="0a228-446">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="0a228-447">En el panel izquierdo, en la parte inferior, seleccione el **icono Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0a228-447">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="0a228-448">En el panel derecho, en la parte inferior, **selecciona Upload una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="0a228-448">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="0a228-449">Vaya a la `TeamsAppManifest` carpeta y cargue el manifiesto comprimido.</span><span class="sxs-lookup"><span data-stu-id="0a228-449">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="0a228-450">Se muestra el siguiente asistente:</span><span class="sxs-lookup"><span data-stu-id="0a228-450">The following wizard is displayed:</span></span>

    ![Carga de equipos de bots de autenticación](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="0a228-452">Seleccione el botón **Agregar a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="0a228-452">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="0a228-453">En la siguiente ventana, seleccione el equipo donde desea usar el bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-453">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="0a228-454">Seleccione el **botón Configurar un bot.**</span><span class="sxs-lookup"><span data-stu-id="0a228-454">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="0a228-455">Seleccione los tres puntos (&#x25cf;&#x25cf;&#x25cf;) en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="0a228-455">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="0a228-456">A continuación, **selecciona el icono de App Studio.**</span><span class="sxs-lookup"><span data-stu-id="0a228-456">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="0a228-457">Seleccione la **pestaña Editor de manifiestos.** Debería ver el icono del bot que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="0a228-457">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="0a228-458">Además, deberías poder ver el bot como un contacto en la lista de chat que puedes usar para intercambiar mensajes con el bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-458">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="0a228-459">Probar el bot localmente en Teams</span><span class="sxs-lookup"><span data-stu-id="0a228-459">Testing the bot locally in Teams</span></span>

<span data-ttu-id="0a228-460">Microsoft Teams es un producto totalmente basado en la nube, requiere que todos los servicios a los que tiene acceso estén disponibles desde la nube mediante puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0a228-460">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="0a228-461">Por lo tanto, para permitir que el bot (nuestro ejemplo) funcione en Teams, debe publicar el código en la nube  de su elección o hacer que una instancia en ejecución local sea accesible externamente a través de una herramienta de túnel.</span><span class="sxs-lookup"><span data-stu-id="0a228-461">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="0a228-462">Se recomienda  [ngrok](https://ngrok.com/download), que crea una dirección URL direccionable externamente para un puerto que se abre localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0a228-462">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="0a228-463">Para configurar ngrok en preparación para ejecutar la aplicación Microsoft Teams localmente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0a228-463">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="0a228-464">En una ventana de terminal, vaya al directorio donde ha `ngrok.exe` instalado.</span><span class="sxs-lookup"><span data-stu-id="0a228-464">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="0a228-465">Se recomienda establecer la *ruta de acceso de la variable* de entorno para que apunte a ella.</span><span class="sxs-lookup"><span data-stu-id="0a228-465">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="0a228-466">Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="0a228-466">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="0a228-467">Reemplace el número de puerto según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0a228-467">Replace the port number as needed.</span></span>
<span data-ttu-id="0a228-468">Esto inicia ngrok para escuchar en el puerto especificado.</span><span class="sxs-lookup"><span data-stu-id="0a228-468">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="0a228-469">A cambio, le proporciona una dirección URL direccionable externamente, válida durante el tiempo que ngrok se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="0a228-469">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="0a228-470">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a228-470">The following image is an example:</span></span>

    ![cadena de conexión de la aplicación bot de teams adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="0a228-472">.</span><span class="sxs-lookup"><span data-stu-id="0a228-472">.</span></span>

1. <span data-ttu-id="0a228-473">Copie la dirección HTTPS de reenvío.</span><span class="sxs-lookup"><span data-stu-id="0a228-473">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="0a228-474">Debe ser similar a lo siguiente: `https://dea822bf.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="0a228-474">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="0a228-475">Anexar `/api/messages` para obtener `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="0a228-475">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="0a228-476">Este es el punto **de conexión** de mensajes para el bot que se ejecuta localmente en el equipo y al que se puede acceder a través de la web en un chat en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0a228-476">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="0a228-477">Un último paso para realizar es actualizar el extremo de mensajes del bot implementado.</span><span class="sxs-lookup"><span data-stu-id="0a228-477">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="0a228-478">En el ejemplo, implementamos el bot en Azure.</span><span class="sxs-lookup"><span data-stu-id="0a228-478">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="0a228-479">Así que \*\*vamos a realizar estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0a228-479">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="0a228-480">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="0a228-480">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="0a228-481">Seleccione el **registro del canal bot**.</span><span class="sxs-lookup"><span data-stu-id="0a228-481">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="0a228-482">En el panel izquierdo, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0a228-482">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="0a228-483">En el panel derecho, en el cuadro **Extremo** de mensajería, escriba la dirección URL de ngrok, en nuestro ejemplo, `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="0a228-483">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="0a228-484">Inicie el bot localmente, por ejemplo, en Visual Studio modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="0a228-484">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="0a228-485">Pruebe el bot mientras se ejecuta localmente con el chat web de prueba del portal **de** Bot Framework .</span><span class="sxs-lookup"><span data-stu-id="0a228-485">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="0a228-486">Al igual que el emulador, esta prueba no permite tener acceso a Teams funcionalidad específica.</span><span class="sxs-lookup"><span data-stu-id="0a228-486">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="0a228-487">En la ventana de terminal donde se ejecuta puede ver el tráfico `ngrok` HTTP entre el bot y el cliente de chat web.</span><span class="sxs-lookup"><span data-stu-id="0a228-487">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="0a228-488">Si desea una vista más detallada, en una ventana del explorador escriba que obtuvo `http://127.0.0.1:4040` de la ventana de terminal anterior.</span><span class="sxs-lookup"><span data-stu-id="0a228-488">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="0a228-489">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a228-489">The following image is an example:</span></span>

    ![Pruebas de auth bot teams ngrok](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="0a228-491">.</span><span class="sxs-lookup"><span data-stu-id="0a228-491">.</span></span>

> [!NOTE]
> <span data-ttu-id="0a228-492">Si detiene y reinicia ngrok, la dirección URL cambia.</span><span class="sxs-lookup"><span data-stu-id="0a228-492">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="0a228-493">Para usar ngrok en el proyecto y según las capacidades que use, debe actualizar todas las referencias de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="0a228-493">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="0a228-494">Información adicional</span><span class="sxs-lookup"><span data-stu-id="0a228-494">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="0a228-495">TeamsAppManifest/manifest.json</span><span class="sxs-lookup"><span data-stu-id="0a228-495">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="0a228-496">Este manifiesto contiene la información necesaria Microsoft Teams para conectarse con el bot.</span><span class="sxs-lookup"><span data-stu-id="0a228-496">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

<span data-ttu-id="0a228-497">Con la autenticación, Teams se comporta de forma ligeramente diferente que otros canales, como se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="0a228-497">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="0a228-498">Controlar actividad de invocación</span><span class="sxs-lookup"><span data-stu-id="0a228-498">Handling Invoke Activity</span></span>

<span data-ttu-id="0a228-499">Se **envía una actividad Invoke** al bot en lugar de a la actividad de evento usada por otros canales.</span><span class="sxs-lookup"><span data-stu-id="0a228-499">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="0a228-500">Para ello, se subclase **activityHandler**.</span><span class="sxs-lookup"><span data-stu-id="0a228-500">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0a228-501">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0a228-501">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="0a228-502">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="0a228-502">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="0a228-503">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="0a228-503">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="0a228-504">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="0a228-504">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="0a228-505">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="0a228-505">TeamsActivityHandler.cs</span></span>

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[<span data-ttu-id="0a228-506">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0a228-506">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="0a228-507">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="0a228-507">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="0a228-508">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="0a228-508">**bots/teamsBot.js**</span></span>

<span data-ttu-id="0a228-509">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="0a228-509">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="0a228-510">**cuadros de diálogo/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="0a228-510">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="0a228-511">En un paso de cuadro de diálogo, use para iniciar el mensaje `beginDialog` de OAuth, que pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-511">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="0a228-512">Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="0a228-512">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="0a228-513">De lo contrario, se pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-513">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="0a228-514">El Servicio de bots de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-514">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="0a228-515">En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="0a228-515">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="0a228-516">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="0a228-516">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="0a228-517">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="0a228-517">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="0a228-518">Python</span><span class="sxs-lookup"><span data-stu-id="0a228-518">Python</span></span>](#tab/python-sample)

<span data-ttu-id="0a228-519">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="0a228-519">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="0a228-520">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="0a228-520">**bots/teams_bot.py**</span></span>

<span data-ttu-id="0a228-521">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="0a228-521">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="0a228-522">**dialogs/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="0a228-522">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="0a228-523">En un paso de cuadro de diálogo, use para iniciar el mensaje `begin_dialog` de OAuth, que pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-523">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="0a228-524">Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="0a228-524">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="0a228-525">De lo contrario, se pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-525">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="0a228-526">El Servicio de bots de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="0a228-526">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="0a228-527">En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="0a228-527">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="0a228-528">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="0a228-528">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="0a228-529">**dialogs/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="0a228-529">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a228-530">Obtenga información sobre cómo agregar autenticación a través del servicio bot de Azure</span><span class="sxs-lookup"><span data-stu-id="0a228-530">Learn about adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
