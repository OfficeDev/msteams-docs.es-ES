---
title: Agregue autenticación al bot de Teams
author: clearab
description: Cómo agregar autenticación OAuth a un bot en Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 36cb6f3de6f97af1d01512175923b79f69f630ad
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566005"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="6d280-103">Agregue autenticación al bot de Teams</span><span class="sxs-lookup"><span data-stu-id="6d280-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="6d280-104">Hay ocasiones en las que es posible que deba crear bots en Microsoft Teams que puedan tener acceso a recursos en nombre del usuario, como un servicio de correo.</span><span class="sxs-lookup"><span data-stu-id="6d280-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="6d280-105">En este artículo se muestra cómo usar la autenticación del SDK de Azure Bot Service v4, basada en OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6d280-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="6d280-106">Esto facilita el desarrollo de un bot que puede usar tokens de autenticación basados en las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="6d280-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="6d280-107">La clave en todo esto es el uso de proveedores de **identidades,** como veremos más adelante.</span><span class="sxs-lookup"><span data-stu-id="6d280-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="6d280-108">OAuth 2.0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory (Azure AD) y otros muchos proveedores de identidad.</span><span class="sxs-lookup"><span data-stu-id="6d280-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="6d280-109">Una comprensión básica de OAuth 2.0 es un requisito previo para trabajar con autenticación en Teams.</span><span class="sxs-lookup"><span data-stu-id="6d280-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="6d280-110">Consulte [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) para obtener una comprensión básica y [OAuth 2.0](https://oauth.net/2/) para obtener la especificación completa.</span><span class="sxs-lookup"><span data-stu-id="6d280-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="6d280-111">Para obtener más información acerca de cómo Azure Bot Service controla la autenticación, consulte [Autenticación de usuario dentro de una conversación.](https://aka.ms/azure-bot-authentication)</span><span class="sxs-lookup"><span data-stu-id="6d280-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="6d280-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6d280-112">In this article you'll learn:</span></span>

- <span data-ttu-id="6d280-113">**Cómo crear un bot habilitado para autenticación.**</span><span class="sxs-lookup"><span data-stu-id="6d280-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="6d280-114">Usará [cs-auth-sample][teams-auth-bot-cs] para controlar las credenciales de inicio de sesión del usuario y la generación del token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6d280-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="6d280-115">**Cómo implementar el bot en Azure y asociarlo a un proveedor de identidades.**</span><span class="sxs-lookup"><span data-stu-id="6d280-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="6d280-116">El proveedor emite un token basado en credenciales de inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="6d280-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="6d280-117">El bot puede usar el token para tener acceso a recursos, como un servicio de correo, que requieren autenticación.</span><span class="sxs-lookup"><span data-stu-id="6d280-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="6d280-118">Para obtener más información, consulte [flujo de autenticación Microsoft Teams para bots.](auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="6d280-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="6d280-119">**Cómo integrar el bot dentro de Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="6d280-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="6d280-120">Una vez integrado el bot, puede iniciar sesión e intercambiar mensajes con él en un chat.</span><span class="sxs-lookup"><span data-stu-id="6d280-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d280-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6d280-121">Prerequisites</span></span>

- <span data-ttu-id="6d280-122">Conocimiento de los conceptos básicos del [bot,][concept-basics] [la administración del estado,][concept-state]la [biblioteca de cuadros de diálogo][concept-dialogs]y cómo implementar el flujo [secuencial de conversaciones.][simple-dialog]</span><span class="sxs-lookup"><span data-stu-id="6d280-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="6d280-123">Conocimiento del desarrollo de Azure y OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6d280-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="6d280-124">Las versiones actuales de Visual Studio y Git.</span><span class="sxs-lookup"><span data-stu-id="6d280-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="6d280-125">Cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d280-125">Azure account.</span></span> <span data-ttu-id="6d280-126">Si es necesario, puede crear una [cuenta gratuita de Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="6d280-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="6d280-127">La siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="6d280-127">The following sample:</span></span>

    | <span data-ttu-id="6d280-128">Muestra</span><span class="sxs-lookup"><span data-stu-id="6d280-128">Sample</span></span> | <span data-ttu-id="6d280-129">Versión de BotBuilder</span><span class="sxs-lookup"><span data-stu-id="6d280-129">BotBuilder version</span></span> | <span data-ttu-id="6d280-130">Demuestra</span><span class="sxs-lookup"><span data-stu-id="6d280-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="6d280-131">**Autenticación de bots** en [cs-auth-sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="6d280-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="6d280-132">v4</span><span class="sxs-lookup"><span data-stu-id="6d280-132">v4</span></span> | <span data-ttu-id="6d280-133">Soporte de OAuthCard</span><span class="sxs-lookup"><span data-stu-id="6d280-133">OAuthCard support</span></span> |
    | <span data-ttu-id="6d280-134">**Autenticación de bots** en [js-auth-sample][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="6d280-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="6d280-135">v4</span><span class="sxs-lookup"><span data-stu-id="6d280-135">v4</span></span>| <span data-ttu-id="6d280-136">Soporte de OAuthCard</span><span class="sxs-lookup"><span data-stu-id="6d280-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="6d280-137">**Autenticación de bots** en [py-auth-sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="6d280-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="6d280-138">v4</span><span class="sxs-lookup"><span data-stu-id="6d280-138">v4</span></span> | <span data-ttu-id="6d280-139">Soporte de OAuthCard</span><span class="sxs-lookup"><span data-stu-id="6d280-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="6d280-140">Crear el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6d280-140">Create the resource group</span></span>

<span data-ttu-id="6d280-141">El grupo de recursos y el plan de servicio no son estrictamente necesarios, pero le permiten liberar convenientemente los recursos que cree.</span><span class="sxs-lookup"><span data-stu-id="6d280-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="6d280-142">Esta es una buena práctica para mantener sus recursos organizados y manejables.</span><span class="sxs-lookup"><span data-stu-id="6d280-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="6d280-143">Utilice un grupo de recursos para crear recursos individuales para Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="6d280-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="6d280-144">Para el rendimiento, asegúrese de que estos recursos se encuentran en la misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d280-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="6d280-145">En el explorador, inicie sesión en [**Azure Portal.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="6d280-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="6d280-146">En el panel de navegación izquierdo, seleccione **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="6d280-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="6d280-147">En la parte superior izquierda de la ventana mostrada, seleccione **agregar** ficha para crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d280-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="6d280-148">Se le pedirá que proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6d280-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="6d280-149">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="6d280-149">**Subscription**.</span></span> <span data-ttu-id="6d280-150">Use su suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="6d280-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="6d280-151">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="6d280-151">**Resource group**.</span></span> <span data-ttu-id="6d280-152">Escriba el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d280-152">Enter the name for the resource group.</span></span> <span data-ttu-id="6d280-153">Un ejemplo podría ser  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="6d280-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="6d280-154">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="6d280-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="6d280-155">En el menú desplegable **Región,** seleccione *Ee. UU. occidental* o una región cercana a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6d280-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="6d280-156">Seleccione el botón **Revisar y crear.**</span><span class="sxs-lookup"><span data-stu-id="6d280-156">Select the **Review and create** button.</span></span> <span data-ttu-id="6d280-157">Debería ver un banner que lee *Validación pasada.*</span><span class="sxs-lookup"><span data-stu-id="6d280-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="6d280-158">Seleccione el botón **Crear.**</span><span class="sxs-lookup"><span data-stu-id="6d280-158">Select the **Create** button.</span></span> <span data-ttu-id="6d280-159">Puede tardar unos minutos en crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d280-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="6d280-160">Al igual que con los recursos que creará más adelante en este tutorial, es una buena idea anclar este grupo de recursos al panel para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="6d280-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="6d280-161">Si desea hacerlo, seleccione el icono de pin &#128204; en la parte superior derecha del panel.</span><span class="sxs-lookup"><span data-stu-id="6d280-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="6d280-162">Crear el plan de servicio</span><span class="sxs-lookup"><span data-stu-id="6d280-162">Create the service plan</span></span>

1. <span data-ttu-id="6d280-163">En [**Azure Portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="6d280-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="6d280-164">En el cuadro de búsqueda, escriba *Plan de App Service*.</span><span class="sxs-lookup"><span data-stu-id="6d280-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="6d280-165">Seleccione la tarjeta Plan de **App Service** en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="6d280-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="6d280-166">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6d280-166">Select **Create**.</span></span>
1. <span data-ttu-id="6d280-167">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="6d280-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="6d280-168">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="6d280-168">**Subscription**.</span></span> <span data-ttu-id="6d280-169">Puede usar una suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="6d280-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="6d280-170">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="6d280-170">**Resource Group**.</span></span> <span data-ttu-id="6d280-171">Seleccione el grupo que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6d280-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="6d280-172">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="6d280-172">**Name**.</span></span> <span data-ttu-id="6d280-173">Escriba el nombre del plan de servicio.</span><span class="sxs-lookup"><span data-stu-id="6d280-173">Enter the name for the service plan.</span></span> <span data-ttu-id="6d280-174">Un ejemplo podría ser  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="6d280-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="6d280-175">Recuerde que el nombre debe ser único, dentro del grupo.</span><span class="sxs-lookup"><span data-stu-id="6d280-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="6d280-176">**Sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="6d280-176">**Operating System**.</span></span> <span data-ttu-id="6d280-177">Seleccione *Windows* o su sistema operativo aplicable.</span><span class="sxs-lookup"><span data-stu-id="6d280-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="6d280-178">**Región**.</span><span class="sxs-lookup"><span data-stu-id="6d280-178">**Region**.</span></span> <span data-ttu-id="6d280-179">Seleccione *Oeste de EE. UU.* o una región cercana a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6d280-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="6d280-180">**Nivel de precios**.</span><span class="sxs-lookup"><span data-stu-id="6d280-180">**Pricing Tier**.</span></span> <span data-ttu-id="6d280-181">Asegúrese de que *el estándar S1* está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="6d280-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="6d280-182">Este debe ser el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="6d280-182">This should be the default value.</span></span>
    1. <span data-ttu-id="6d280-183">Seleccione el botón **Revisar y crear.**</span><span class="sxs-lookup"><span data-stu-id="6d280-183">Select the **Review and create** button.</span></span> <span data-ttu-id="6d280-184">Debería ver un banner que lee *Validación pasada.*</span><span class="sxs-lookup"><span data-stu-id="6d280-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="6d280-185">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6d280-185">Select **Create**.</span></span> <span data-ttu-id="6d280-186">Puede tardar unos minutos en crear el plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6d280-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="6d280-187">El plan aparecerá en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d280-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="6d280-188">Cree el registro de canales de bot</span><span class="sxs-lookup"><span data-stu-id="6d280-188">Create the bot channels registration</span></span>

<span data-ttu-id="6d280-189">El registro de canales de bot registra el servicio web como un bot con Bot Framework, siempre que tenga un identificador de aplicación de Microsoft y una contraseña de aplicación (secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="6d280-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d280-190">Solo debe registrar el bot si no está hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="6d280-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="6d280-191">Si [creó un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) a través de Azure Portal, ya está registrado con el servicio.</span><span class="sxs-lookup"><span data-stu-id="6d280-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="6d280-192">Si creó el bot a través de [Bot Framework](https://dev.botframework.com/bots/new) o [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) el bot no está registrado en Azure.</span><span class="sxs-lookup"><span data-stu-id="6d280-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="6d280-193">El recurso Registro de canales de bot mostrará la región **Global** incluso si seleccionó Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="6d280-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="6d280-194">Esto se espera.</span><span class="sxs-lookup"><span data-stu-id="6d280-194">This is expected.</span></span>

<span data-ttu-id="6d280-195">Para obtener más información, consulte [Crear un bot para Teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="6d280-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="6d280-196">Crear el proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="6d280-196">Create the identity provider</span></span>

<span data-ttu-id="6d280-197">Necesita un proveedor de identidades que se pueda usar para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="6d280-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="6d280-198">En este procedimiento usará un proveedor de Azure AD; también se pueden usar otros proveedores de identidades compatibles con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d280-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="6d280-199">En [**Azure Portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d280-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="6d280-200">Deberá crear y registrar este recurso de Azure AD en un inquilino en el que puede dar su consentimiento para delegar los permisos solicitados por una aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d280-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="6d280-201">Para obtener instrucciones sobre cómo crear un inquilino, consulte [Acceso al portal y crear un inquilino](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span><span class="sxs-lookup"><span data-stu-id="6d280-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="6d280-202">En el panel izquierdo, seleccione **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6d280-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="6d280-203">En el panel derecho, seleccione la pestaña **Nuevo registro,** en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="6d280-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="6d280-204">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="6d280-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="6d280-205">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="6d280-205">**Name**.</span></span> <span data-ttu-id="6d280-206">Escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d280-206">Enter the name for the application.</span></span> <span data-ttu-id="6d280-207">Un ejemplo podría ser  *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="6d280-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="6d280-208">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="6d280-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="6d280-209">Seleccione los **tipos de cuenta compatibles** para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d280-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="6d280-210">Seleccione *Cuentas en cualquier directorio de organización (cualquier directorio de Azure AD - Multitenant) y cuentas personales de Microsoft (por ejemplo, Skype, Xbox).*</span><span class="sxs-lookup"><span data-stu-id="6d280-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="6d280-211">Para el **URI de redirección**:</span><span class="sxs-lookup"><span data-stu-id="6d280-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="6d280-212">&#x2713;Seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="6d280-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="6d280-213">&#x2713; Establezca la dirección URL en `https://token.botframework.com/.auth/web/redirect` .</span><span class="sxs-lookup"><span data-stu-id="6d280-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="6d280-214">Seleccione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-214">Select **Register**.</span></span>

1. <span data-ttu-id="6d280-215">Una vez creado, Azure muestra la página **Información general de** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d280-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="6d280-216">Copie y guarde la siguiente información en un archivo:</span><span class="sxs-lookup"><span data-stu-id="6d280-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="6d280-217">El valor **del IDENTIFICADOR de aplicación (cliente).**</span><span class="sxs-lookup"><span data-stu-id="6d280-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="6d280-218">Usará este valor más adelante como *identificador de cliente* al registrar esta aplicación de identidad de Azure con el bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="6d280-219">El valor **de identificador directorio (inquilino).**</span><span class="sxs-lookup"><span data-stu-id="6d280-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="6d280-220">También usará este valor más adelante como *identificador de inquilino* para registrar esta aplicación de identidad de Azure con el bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="6d280-221">En el panel izquierdo, seleccione **Certificados & secretos** para crear un secreto de cliente para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d280-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="6d280-222">En **Secretos de cliente**, seleccione &#x2795; Nuevo secreto de **cliente**.</span><span class="sxs-lookup"><span data-stu-id="6d280-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="6d280-223">Agregue una descripción para identificar este secreto de otras personas que podría necesitar crear para esta aplicación, como *bot identity app en Teams*.</span><span class="sxs-lookup"><span data-stu-id="6d280-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="6d280-224">Establezca **Expiraciones** en la selección.</span><span class="sxs-lookup"><span data-stu-id="6d280-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="6d280-225">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-225">Select **Add**.</span></span>
   1. <span data-ttu-id="6d280-226">Antes de salir de esta página, **registre el secreto.**</span><span class="sxs-lookup"><span data-stu-id="6d280-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="6d280-227">Usará este valor más adelante como _secreto de cliente_ al registrar la aplicación de Azure AD con el bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="6d280-228">Configure la conexión del proveedor de identidades y regístrela con el bot</span><span class="sxs-lookup"><span data-stu-id="6d280-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="6d280-229">Tenga en cuenta que hay dos opciones para proveedores de servicios aquí-Azure AD V1 y Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="6d280-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="6d280-230">Las diferencias entre los dos proveedores se resumen [aquí,](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)pero en general, V2 proporciona más flexibilidad con respecto a los permisos de bot cambiantes.</span><span class="sxs-lookup"><span data-stu-id="6d280-230">The differences between the two providers are summarized [here](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="6d280-231">Graph Los permisos de API se enumeran en el campo ámbitos y, a medida que se agregan otros nuevos, los bots permitirán a los usuarios dar su consentimiento para los nuevos permisos en el siguiente inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="6d280-232">Para V1, el usuario debe eliminar el consentimiento del bot para que se soliciten nuevos permisos en el cuadro de diálogo OAuth.</span><span class="sxs-lookup"><span data-stu-id="6d280-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="6d280-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="6d280-233">Azure AD V1</span></span>

1. <span data-ttu-id="6d280-234">En [**Azure Portal,**][azure-portal]seleccione el grupo de recursos en el panel.</span><span class="sxs-lookup"><span data-stu-id="6d280-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="6d280-235">Seleccione el vínculo de registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="6d280-236">Abra la página de recursos y seleccione **Configuración** en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="6d280-236">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="6d280-237">Seleccione **Agregar Configuración de conexión de OAuth**.</span><span class="sxs-lookup"><span data-stu-id="6d280-237">Select **Add OAuth Connection Settings**.</span></span>    
<span data-ttu-id="6d280-238">La siguiente imagen muestra la selección correspondiente en la página de recursos:</span><span class="sxs-lookup"><span data-stu-id="6d280-238">The following image displays the corresponding selection in the resource page:</span></span>  
<span data-ttu-id="6d280-239">![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="6d280-239">![SampleAppDemoBot configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span>
1. <span data-ttu-id="6d280-240">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="6d280-240">Complete the form as follows:</span></span>

    1. <span data-ttu-id="6d280-241">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="6d280-241">**Name**.</span></span> <span data-ttu-id="6d280-242">Escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="6d280-242">Enter a name for the connection.</span></span> <span data-ttu-id="6d280-243">Usará este nombre en el bot del `appsettings.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="6d280-243">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="6d280-244">Por ejemplo *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="6d280-244">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="6d280-245">**Proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="6d280-245">**Service Provider**.</span></span> <span data-ttu-id="6d280-246">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d280-246">Select **Azure Active Directory**.</span></span> <span data-ttu-id="6d280-247">Una vez seleccionado esto, se mostrarán los campos específicos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d280-247">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="6d280-248">**Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="6d280-248">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="6d280-249">**Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="6d280-249">**Client secret**.</span></span> <span data-ttu-id="6d280-250">Escriba el secreto que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="6d280-250">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="6d280-251">**Tipo de concesión**.</span><span class="sxs-lookup"><span data-stu-id="6d280-251">**Grant Type**.</span></span> <span data-ttu-id="6d280-252">Escriba `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="6d280-252">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="6d280-253">**URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="6d280-253">**Login URL**.</span></span> <span data-ttu-id="6d280-254">Escriba `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="6d280-254">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="6d280-255">**Identificador de inquilino**, escriba el **identificador de directorio (inquilino)** que registró anteriormente para la aplicación de identidad de Azure o **común** en función del tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="6d280-255">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="6d280-256">Para decidir qué valor asignar sigue estos criterios:</span><span class="sxs-lookup"><span data-stu-id="6d280-256">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="6d280-257">Si seleccionó *Solo cuentas en este directorio de organización (solo Microsoft - inquilino único)* o Cuentas en cualquier directorio de organización *(directorio de Microsoft AAD - Multi tenant)* escriba el identificador de **inquilino** que registró anteriormente para la aplicación AAD.</span><span class="sxs-lookup"><span data-stu-id="6d280-257">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="6d280-258">Este será el inquilino asociado a los usuarios que se pueden autenticar.</span><span class="sxs-lookup"><span data-stu-id="6d280-258">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="6d280-259">Si seleccionó *Cuentas en cualquier directorio de organización (cualquier directorio AAD : cuentas de Microsoft multiinquilino y personales, por ejemplo, Skype, Xbox, Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="6d280-259">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="6d280-260">De lo contrario, la aplicación AAD comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6d280-260">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="6d280-261">h.</span><span class="sxs-lookup"><span data-stu-id="6d280-261">h.</span></span> <span data-ttu-id="6d280-262">En **Dirección URL de recurso**, escriba `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="6d280-262">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="6d280-263">Esto no se utiliza en el ejemplo de código actual.</span><span class="sxs-lookup"><span data-stu-id="6d280-263">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="6d280-264">i.</span><span class="sxs-lookup"><span data-stu-id="6d280-264">i.</span></span> <span data-ttu-id="6d280-265">Deje **los ámbitos** en blanco.</span><span class="sxs-lookup"><span data-stu-id="6d280-265">Leave **Scopes** blank.</span></span> <span data-ttu-id="6d280-266">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d280-266">The following image is an example:</span></span>

    ![equipos bots aplicación auth cadena de conexión adv1 vista](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="6d280-268">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-268">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="6d280-269">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="6d280-269">Azure AD V2</span></span>

1. <span data-ttu-id="6d280-270">En [**Azure Portal,**][azure-portal]seleccione el grupo de recursos en el panel.</span><span class="sxs-lookup"><span data-stu-id="6d280-270">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="6d280-271">Seleccione el vínculo de registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-271">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="6d280-272">Abra la página de recursos y seleccione **Configuración** en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="6d280-272">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="6d280-273">Seleccione **Agregar Configuración de conexión de OAuth**.</span><span class="sxs-lookup"><span data-stu-id="6d280-273">Select **Add OAuth Connection Settings**.</span></span>  
<span data-ttu-id="6d280-274">La siguiente imagen muestra la selección correspondiente en la página de recursos:</span><span class="sxs-lookup"><span data-stu-id="6d280-274">The following image displays the corresponding selection in the resource page:</span></span>        
<span data-ttu-id="6d280-275">![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="6d280-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span> 

1. <span data-ttu-id="6d280-276">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="6d280-276">Complete the form as follows:</span></span>

    1. <span data-ttu-id="6d280-277">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="6d280-277">**Name**.</span></span> <span data-ttu-id="6d280-278">Escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="6d280-278">Enter a name for the connection.</span></span> <span data-ttu-id="6d280-279">Usará este nombre en el bot del `appsettings.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="6d280-279">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="6d280-280">Por ejemplo *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="6d280-280">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="6d280-281">**Proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="6d280-281">**Service Provider**.</span></span> <span data-ttu-id="6d280-282">Seleccione **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="6d280-282">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="6d280-283">Una vez seleccionado esto, se mostrarán los campos específicos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d280-283">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="6d280-284">**Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="6d280-284">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="6d280-285">**Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="6d280-285">**Client secret**.</span></span> <span data-ttu-id="6d280-286">Escriba el secreto que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="6d280-286">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="6d280-287">**Url de Exchange de tokens**.</span><span class="sxs-lookup"><span data-stu-id="6d280-287">**Token Exchange URL**.</span></span> <span data-ttu-id="6d280-288">Deja esto en blanco.</span><span class="sxs-lookup"><span data-stu-id="6d280-288">Leave this blank.</span></span>
    1. <span data-ttu-id="6d280-289">**Identificador de inquilino**, escriba el **identificador de directorio (inquilino)** que registró anteriormente para la aplicación de identidad de Azure o **común** en función del tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="6d280-289">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="6d280-290">Para decidir qué valor asignar sigue estos criterios:</span><span class="sxs-lookup"><span data-stu-id="6d280-290">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="6d280-291">Si seleccionó *Solo cuentas en este directorio de organización (solo Microsoft - inquilino único)* o Cuentas en cualquier directorio de organización *(directorio de Microsoft AAD - Multi tenant)* escriba el identificador de **inquilino** que registró anteriormente para la aplicación AAD.</span><span class="sxs-lookup"><span data-stu-id="6d280-291">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="6d280-292">Este será el inquilino asociado a los usuarios que se pueden autenticar.</span><span class="sxs-lookup"><span data-stu-id="6d280-292">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="6d280-293">Si seleccionó *Cuentas en cualquier directorio de organización (cualquier directorio AAD : cuentas de Microsoft multiinquilino y personales, por ejemplo, Skype, Xbox, Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="6d280-293">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="6d280-294">De lo contrario, la aplicación AAD comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6d280-294">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="6d280-295">En **Scopes**, escriba una lista delimitada por espacio de permisos de gráfico que esta aplicación requiere, por ejemplo: User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="6d280-295">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="6d280-296">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-296">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="6d280-297">Probar la conexión</span><span class="sxs-lookup"><span data-stu-id="6d280-297">Test the connection</span></span>

1. <span data-ttu-id="6d280-298">Seleccione la entrada de conexión para abrir la conexión que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="6d280-298">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="6d280-299">Seleccione **Probar conexión** en la parte superior del panel Configuración de conexión del proveedor **de** servicios.</span><span class="sxs-lookup"><span data-stu-id="6d280-299">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="6d280-300">La primera vez que lo hagas abrirá una nueva ventana del navegador pidiéndote que selecciones una cuenta.</span><span class="sxs-lookup"><span data-stu-id="6d280-300">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="6d280-301">Seleccione el que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="6d280-301">Select the one you want to use.</span></span>
1. <span data-ttu-id="6d280-302">A continuación, se le pedirá que permita al proveedor de identidades usar los datos (credenciales).</span><span class="sxs-lookup"><span data-stu-id="6d280-302">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="6d280-303">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d280-303">The following image is an example:</span></span>

    ![equipos bot auth cadena de conexión adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="6d280-305">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-305">Select **Accept**.</span></span>
1. <span data-ttu-id="6d280-306">A continuación, esto debe redirigir a una conexión de prueba a la página **\<your-connection-name> correcta.**</span><span class="sxs-lookup"><span data-stu-id="6d280-306">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="6d280-307">Actualice la página si recibe un error.</span><span class="sxs-lookup"><span data-stu-id="6d280-307">Refresh the page if you get an error.</span></span> <span data-ttu-id="6d280-308">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d280-308">The following image is an example:</span></span>

    ![equipos bots aplicación auth conexión str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="6d280-310">El código de bot usa el nombre de conexión para recuperar tokens de autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="6d280-310">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="6d280-311">Prepare el código de ejemplo del bot</span><span class="sxs-lookup"><span data-stu-id="6d280-311">Prepare the bot sample code</span></span>

<span data-ttu-id="6d280-312">Con la configuración preliminar realizada, vamos a centrarnos en la creación del bot para usar en este artículo.</span><span class="sxs-lookup"><span data-stu-id="6d280-312">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6d280-313">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6d280-313">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="6d280-314">Clonar [cs-auth-sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="6d280-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="6d280-315">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d280-315">Launch Visual Studio.</span></span>
1. <span data-ttu-id="6d280-316">En la barra de herramientas, seleccione **Archivo -> Abrir -> Project/Solución** y abra el proyecto de bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-316">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="6d280-317">En C# Update **appsettings.jsactivado** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="6d280-317">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="6d280-318">Estad en `ConnectionName` el nombre de la conexión del proveedor de identidades que agregó al registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-318">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="6d280-319">El nombre que usamos en este ejemplo es *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="6d280-319">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="6d280-320">Estad en `MicrosoftAppId` el **id.**</span><span class="sxs-lookup"><span data-stu-id="6d280-320">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="6d280-321">Establezca `MicrosoftAppPassword` en el secreto de **cliente** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-321">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="6d280-322">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="6d280-322">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="6d280-323">Por ejemplo, cualquier amperaciones (&) deberá codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="6d280-323">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="6d280-324">En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta, abra `manifest.json` y establezca y en el identificador de aplicación del `id` `botId` **bot** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-324">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="6d280-325">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6d280-325">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="6d280-326">Clonar [node-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="6d280-326">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="6d280-327">En una consola, vaya al proyecto:</span><span class="sxs-lookup"><span data-stu-id="6d280-327">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="6d280-328">Instalar módulos</span><span class="sxs-lookup"><span data-stu-id="6d280-328">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="6d280-329">Actualice la configuración **.env** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="6d280-329">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="6d280-330">Estad en `MicrosoftAppId` el **id.**</span><span class="sxs-lookup"><span data-stu-id="6d280-330">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="6d280-331">Establezca `MicrosoftAppPassword` en el secreto de **cliente** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-331">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="6d280-332">Establezca el `connectionName` nombre de la conexión del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="6d280-332">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="6d280-333">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="6d280-333">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="6d280-334">Por ejemplo, cualquier amperaciones (&) deberá codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="6d280-334">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="6d280-335">En la `teamsAppManifest` carpeta, abra `manifest.json` y establezca en el IDENTIFICADOR de la aplicación de `id` **Microsoft** y en el identificador de aplicación `botId` del **bot** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-335">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="6d280-336">Python</span><span class="sxs-lookup"><span data-stu-id="6d280-336">Python</span></span>](#tab/python)

1. <span data-ttu-id="6d280-337">Clone [py-auth-sample][teams-auth-bot-py] desde el repositorio de github.</span><span class="sxs-lookup"><span data-stu-id="6d280-337">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="6d280-338">Actualizar **config.py**:</span><span class="sxs-lookup"><span data-stu-id="6d280-338">Update **config.py**:</span></span>

    - <span data-ttu-id="6d280-339">Estadúrle `ConnectionName` en el nombre de la configuración de conexión de OAuth que agregó al bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-339">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="6d280-340">Establece `MicrosoftAppId` y en el ID de aplicación y el secreto de la aplicación del `MicrosoftAppPassword` bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-340">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="6d280-341">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="6d280-341">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="6d280-342">Por ejemplo, cualquier amperaciones (&) deberá codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="6d280-342">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="6d280-343">Implementar el bot en Azure</span><span class="sxs-lookup"><span data-stu-id="6d280-343">Deploy the bot to Azure</span></span>

<span data-ttu-id="6d280-344">Para implementar el bot, siga los pasos descritos en cómo [implementar el bot en Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="6d280-344">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="6d280-345">Como alternativa, mientras está en Visual Studio, puede seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6d280-345">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="6d280-346">En Visual Studio *Explorador de soluciones,* seleccione y mantenga pulsado (o haga clic con el botón derecho) el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="6d280-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="6d280-347">En el menú desplegable, seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-347">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="6d280-348">En la ventana mostrada, seleccione el vínculo **Nuevo.**</span><span class="sxs-lookup"><span data-stu-id="6d280-348">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="6d280-349">En la ventana de diálogo, seleccione **App Service** a la izquierda y **Crear nuevo** a la derecha.</span><span class="sxs-lookup"><span data-stu-id="6d280-349">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="6d280-350">Seleccione el botón **Publicar.**</span><span class="sxs-lookup"><span data-stu-id="6d280-350">Select the **Publish** button.</span></span>
1. <span data-ttu-id="6d280-351">En la siguiente ventana de diálogo, escriba la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="6d280-351">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="6d280-352">A continuación puede ver un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d280-352">The following is an example:</span></span>

    ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="6d280-354">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6d280-354">Select **Create**.</span></span>
1. <span data-ttu-id="6d280-355">Si la implementación se completa correctamente, debería verlo reflejado en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d280-355">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="6d280-356">Por otra parte, se muestra una página en su navegador predeterminado diciendo *Su bot está listo!*.</span><span class="sxs-lookup"><span data-stu-id="6d280-356">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="6d280-357">La URL será similar a esto: `https://botteamsauth.azurewebsites.net/` .</span><span class="sxs-lookup"><span data-stu-id="6d280-357">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="6d280-358">Guárdelo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="6d280-358">Save it to a file.</span></span>
1. <span data-ttu-id="6d280-359">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6d280-359">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="6d280-360">Compruebe el grupo de recursos, el bot debe aparecer junto con los demás recursos.</span><span class="sxs-lookup"><span data-stu-id="6d280-360">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="6d280-361">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d280-361">The following image is an example:</span></span>

    ![equipos-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="6d280-363">En el grupo de recursos, seleccione el nombre de registro del canal bot (vínculo).</span><span class="sxs-lookup"><span data-stu-id="6d280-363">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="6d280-364">En el panel izquierdo, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="6d280-364">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="6d280-365">En el cuadro **Punto de conexión mensajería,** escriba la dirección URL obtenida anteriormente seguida de `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="6d280-365">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="6d280-366">Este es un ejemplo: `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="6d280-366">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="6d280-367">Seleccione el botón **Guardar** en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="6d280-367">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="6d280-368">Pruebe el bot usando el emulador</span><span class="sxs-lookup"><span data-stu-id="6d280-368">Test the bot using the Emulator</span></span>

<span data-ttu-id="6d280-369">Si aún no lo ha hecho, instale el [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="6d280-369">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="6d280-370">Vea también [Depurar con el emulador](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="6d280-370">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="6d280-371">Para que el inicio de sesión del ejemplo del bot funcione usted debe configurar el emulador.</span><span class="sxs-lookup"><span data-stu-id="6d280-371">In order for the bot sample login to work you must configure the Emulator.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="6d280-372">Configure el emulador para la autenticación</span><span class="sxs-lookup"><span data-stu-id="6d280-372">Configure the Emulator for authentication</span></span>

<span data-ttu-id="6d280-373">Si un bot requiere autenticación, debe configurar el emulador.</span><span class="sxs-lookup"><span data-stu-id="6d280-373">If a bot requires authentication, you must configure the Emulator.</span></span> <span data-ttu-id="6d280-374">Para configurar:</span><span class="sxs-lookup"><span data-stu-id="6d280-374">To configure:</span></span>

1. <span data-ttu-id="6d280-375">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="6d280-375">Start the Emulator.</span></span>
1. <span data-ttu-id="6d280-376">En el emulador, seleccione el icono de engranaje &#9881; en la parte inferior izquierda, o la pestaña **Emulador Configuración** en la parte superior derecha.</span><span class="sxs-lookup"><span data-stu-id="6d280-376">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="6d280-377">Marque la casilla Por **usar tokens de autenticación de la versión 1.0**.</span><span class="sxs-lookup"><span data-stu-id="6d280-377">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="6d280-378">Introduzca la ruta local a la herramienta **ngrok.**</span><span class="sxs-lookup"><span data-stu-id="6d280-378">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="6d280-379">*Consulte* la Bot Framework Emulator / ngrok integración de [túneles Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span><span class="sxs-lookup"><span data-stu-id="6d280-379">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="6d280-380">Para obtener más información sobre herramientas, consulte [ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="6d280-380">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="6d280-381">Marque la casilla Por **Ejecutar ngrok cuando se inicie el emulador**.</span><span class="sxs-lookup"><span data-stu-id="6d280-381">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="6d280-382">Seleccione el botón **Guardar.**</span><span class="sxs-lookup"><span data-stu-id="6d280-382">Select the **Save** button.</span></span>

<span data-ttu-id="6d280-383">Cuando el bot muestra una tarjeta de inicio de sesión y el usuario selecciona el botón de inicio de sesión, el emulador abre una página que el usuario puede usar para iniciar sesión con el proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6d280-383">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="6d280-384">Una vez que el usuario lo hace, el proveedor genera un token de usuario y lo envía al bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-384">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="6d280-385">Después de eso, el bot puede actuar en nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="6d280-385">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="6d280-386">Pruebe el bot localmente</span><span class="sxs-lookup"><span data-stu-id="6d280-386">Test the bot locally</span></span>

<span data-ttu-id="6d280-387">Después de configurar el mecanismo de autenticación, puede realizar las pruebas de bot reales.</span><span class="sxs-lookup"><span data-stu-id="6d280-387">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="6d280-388">Ejecute el ejemplo de bot localmente en el equipo, a través de Visual Studio por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6d280-388">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="6d280-389">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="6d280-389">Start the Emulator.</span></span>
1. <span data-ttu-id="6d280-390">Seleccione el botón **Abrir bot.**</span><span class="sxs-lookup"><span data-stu-id="6d280-390">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="6d280-391">En la DIRECCIÓN URL del **bot,** escriba la dirección URL local del bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-391">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="6d280-392">Por lo general, `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="6d280-392">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="6d280-393">En el **IDENTIFICADOR de aplicación de Microsoft,** escriba el identificador de aplicación del bot desde `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="6d280-393">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="6d280-394">En la contraseña de la **aplicación de Microsoft,** escriba la contraseña de la aplicación del bot desde `appsettings.json` el archivo .</span><span class="sxs-lookup"><span data-stu-id="6d280-394">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="6d280-395">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-395">Select **Connect**.</span></span>
1. <span data-ttu-id="6d280-396">Después de que el bot esté en funcionamiento, escriba cualquier texto para mostrar la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-396">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="6d280-397">Seleccione el botón **Iniciar sesión.**</span><span class="sxs-lookup"><span data-stu-id="6d280-397">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="6d280-398">Se muestra un cuadro de diálogo emergente para **confirmar la URL abierta.**</span><span class="sxs-lookup"><span data-stu-id="6d280-398">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="6d280-399">Esto es para permitir que el usuario del bot (usted) sea autenticado.</span><span class="sxs-lookup"><span data-stu-id="6d280-399">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="6d280-400">Seleccione **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-400">Select **Confirm**.</span></span>
1. <span data-ttu-id="6d280-401">Si se le solicita, seleccione la cuenta del usuario aplicable.</span><span class="sxs-lookup"><span data-stu-id="6d280-401">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="6d280-402">Dependiendo de la configuración que haya utilizado para el emulador, obtendrá una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="6d280-402">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="6d280-403">**Uso del código de verificación de inicio de sesión**</span><span class="sxs-lookup"><span data-stu-id="6d280-403">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="6d280-404">&#x2713; Se abre una ventana que muestra el código de validación.</span><span class="sxs-lookup"><span data-stu-id="6d280-404">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="6d280-405">&#x2713; Copiar e introduzca el código de validación en el cuadro de chat para completar el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-405">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="6d280-406">**Uso de tokens de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="6d280-406">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="6d280-407">&#x2713; Ha iniciado sesión en función de sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="6d280-407">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="6d280-408">La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="6d280-408">The following image is an example of the bot UI after you've logged in:</span></span>

    ![emulador de inicio de sesión de bot auth](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="6d280-410">Si selecciona **Sí** cuando el bot le pregunta *¿Desea ver el token?*, obtendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="6d280-410">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![Token de emulador de inicio de sesión de bot de autenticación](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="6d280-412">Escriba **cerrar sesión** en el cuadro de chat de entrada para cerrar sesión. Esto libera el token de usuario y el bot no podrá actuar en su nombre hasta que vuelva a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-412">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="6d280-413">La autenticación de bots requiere el uso del **servicio bot connector**.</span><span class="sxs-lookup"><span data-stu-id="6d280-413">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="6d280-414">El servicio tiene acceso a la información de registro de canales de bot para el bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-414">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="6d280-415">Pruebe el bot implementado</span><span class="sxs-lookup"><span data-stu-id="6d280-415">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="6d280-416">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6d280-416">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="6d280-417">Busque el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d280-417">Find your resource group.</span></span>
1. <span data-ttu-id="6d280-418">Seleccione el vínculo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d280-418">Select the resource link.</span></span> <span data-ttu-id="6d280-419">Se muestra la página de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d280-419">The resource page is displayed.</span></span>
1. <span data-ttu-id="6d280-420">En la página de recursos, seleccione **Probar en chat web**.</span><span class="sxs-lookup"><span data-stu-id="6d280-420">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="6d280-421">El bot se inicia y muestra los saludos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="6d280-421">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="6d280-422">Escriba cualquier cosa en el cuadro de chat.</span><span class="sxs-lookup"><span data-stu-id="6d280-422">Type anything in the chat box.</span></span>
1. <span data-ttu-id="6d280-423">Seleccione el cuadro **Iniciar sesión.**</span><span class="sxs-lookup"><span data-stu-id="6d280-423">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="6d280-424">Se muestra un cuadro de diálogo emergente para **confirmar la URL abierta.**</span><span class="sxs-lookup"><span data-stu-id="6d280-424">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="6d280-425">Esto es para permitir que el usuario del bot (usted) sea autenticado.</span><span class="sxs-lookup"><span data-stu-id="6d280-425">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="6d280-426">Seleccione **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="6d280-426">Select **Confirm**.</span></span>
1. <span data-ttu-id="6d280-427">Si se le solicita, seleccione la cuenta del usuario aplicable.</span><span class="sxs-lookup"><span data-stu-id="6d280-427">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="6d280-428">La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="6d280-428">The following image is an example of the bot UI after you have logged in:</span></span>

    ![inicio de sesión del bot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="6d280-430">.</span><span class="sxs-lookup"><span data-stu-id="6d280-430">.</span></span>

1. <span data-ttu-id="6d280-431">Seleccione el botón **Sí** para mostrar el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6d280-431">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="6d280-432">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d280-432">The following image is an example:</span></span>

    ![Token implementado de inicio de sesión del bot de autenticación](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="6d280-434">.</span><span class="sxs-lookup"><span data-stu-id="6d280-434">.</span></span>

1. <span data-ttu-id="6d280-435">Escriba cerrar sesión para cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-435">Enter logout to sign out.</span></span>

    ![auth bot desplegado cierre de sesión](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="6d280-437">Si tiene problemas para iniciar sesión, intente probar la conexión de nuevo como se describe en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="6d280-437">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="6d280-438">Esto podría volver a crear el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6d280-438">This could recreate the authentication token.</span></span>
> <span data-ttu-id="6d280-439">Con el cliente de Bot Framework Web Chat en Azure, es posible que deba iniciar sesión varias veces antes de que la autenticación se establezca correctamente.</span><span class="sxs-lookup"><span data-stu-id="6d280-439">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="6d280-440">Instale y pruebe el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="6d280-440">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="6d280-441">En el proyecto de bot, asegúrese de que la `TeamsAppManifest` carpeta contiene el junto con un archivo `manifest.json` `outline.png` `color.png` y.</span><span class="sxs-lookup"><span data-stu-id="6d280-441">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="6d280-442">En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta.</span><span class="sxs-lookup"><span data-stu-id="6d280-442">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="6d280-443">Edite `manifest.json` asignando los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="6d280-443">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="6d280-444">Asegúrese de que el **ID de aplicación** del bot que recibió en el momento del registro del canal del bot está asignado y `id` `botId` .</span><span class="sxs-lookup"><span data-stu-id="6d280-444">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="6d280-445">Asigne este valor: `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="6d280-445">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="6d280-446">Seleccione y **comprima** los `manifest.json` archivos y `outline.png` `color.png` archivos.</span><span class="sxs-lookup"><span data-stu-id="6d280-446">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="6d280-447">Abra **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="6d280-447">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="6d280-448">En el panel izquierdo, en la parte inferior, seleccione el **icono Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6d280-448">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="6d280-449">En el panel derecho, en la parte inferior, seleccione **Upload una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="6d280-449">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="6d280-450">Vaya a la `TeamsAppManifest` carpeta y cargue el manifiesto comprimido.</span><span class="sxs-lookup"><span data-stu-id="6d280-450">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="6d280-451">Se muestra el siguiente asistente:</span><span class="sxs-lookup"><span data-stu-id="6d280-451">The following wizard is displayed:</span></span>

    ![auth equipos de bots cargar](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="6d280-453">Seleccione el botón **Agregar a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="6d280-453">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="6d280-454">En la siguiente ventana, seleccione el equipo donde desea utilizar el bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-454">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="6d280-455">Seleccione el botón **Configurar un bot.**</span><span class="sxs-lookup"><span data-stu-id="6d280-455">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="6d280-456">Seleccione los tres puntos (&#x25cf;&#x25cf;&#x25cf;) en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="6d280-456">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="6d280-457">A continuación, seleccione el icono **de App Studio.**</span><span class="sxs-lookup"><span data-stu-id="6d280-457">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="6d280-458">Seleccione la pestaña **Editor de manifiestos.** Debería ver el icono del bot que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="6d280-458">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="6d280-459">Además, debería poder ver el bot que aparece como un contacto en la lista de chat que puede usar para intercambiar mensajes con el bot.</span><span class="sxs-lookup"><span data-stu-id="6d280-459">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="6d280-460">Probar el bot localmente en Teams</span><span class="sxs-lookup"><span data-stu-id="6d280-460">Testing the bot locally in Teams</span></span>

<span data-ttu-id="6d280-461">Microsoft Teams es un producto completamente basado en la nube, requiere que todos los servicios a los que accede estén disponibles desde la nube mediante puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6d280-461">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="6d280-462">Por lo tanto, para permitir que el bot (nuestro ejemplo) funcione en Teams, debe publicar el código en la nube de su elección o hacer que una instancia de ejecución local sea accesible externamente a través de una herramienta **de tunelización.**</span><span class="sxs-lookup"><span data-stu-id="6d280-462">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="6d280-463">Se recomienda  [ngrok](https://ngrok.com/download), que crea una dirección URL direccionable externamente para un puerto que se abre localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6d280-463">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="6d280-464">Para configurar ngrok en preparación para ejecutar la aplicación Microsoft Teams localmente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6d280-464">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="6d280-465">En una ventana de terminal, vaya al directorio donde ha `ngrok.exe` instalado.</span><span class="sxs-lookup"><span data-stu-id="6d280-465">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="6d280-466">Sugerimos establecer la ruta de acceso *de la variable* de entorno para que apunte a ella.</span><span class="sxs-lookup"><span data-stu-id="6d280-466">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="6d280-467">Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="6d280-467">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="6d280-468">Reemplace el número de puerto según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6d280-468">Replace the port number as needed.</span></span>
<span data-ttu-id="6d280-469">Esto inicia ngrok para escuchar en el puerto que especifique.</span><span class="sxs-lookup"><span data-stu-id="6d280-469">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="6d280-470">A cambio, le proporciona una dirección URL direccionable externamente, válida durante el tiempo que ngrok se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="6d280-470">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="6d280-471">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d280-471">The following image is an example:</span></span>

    ![equipos bot app auth cadena de conexión adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="6d280-473">.</span><span class="sxs-lookup"><span data-stu-id="6d280-473">.</span></span>

1. <span data-ttu-id="6d280-474">Copie la dirección HTTPS de reenvío.</span><span class="sxs-lookup"><span data-stu-id="6d280-474">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="6d280-475">Debe ser similar a lo siguiente: `https://dea822bf.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="6d280-475">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="6d280-476">`/api/messages`Anexar para obtener `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="6d280-476">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="6d280-477">Este es el **punto de conexión de mensajes** para el bot que se ejecuta localmente en el equipo y accesible a través de la web en un chat en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6d280-477">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="6d280-478">Un último paso a realizar es actualizar el punto de conexión de mensajes del bot implementado.</span><span class="sxs-lookup"><span data-stu-id="6d280-478">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="6d280-479">En el ejemplo, implementamos el bot en Azure.</span><span class="sxs-lookup"><span data-stu-id="6d280-479">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="6d280-480">Así que vamos a realizar estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6d280-480">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="6d280-481">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6d280-481">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="6d280-482">Seleccione el **registro del canal de bot.**</span><span class="sxs-lookup"><span data-stu-id="6d280-482">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="6d280-483">En el panel izquierdo, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="6d280-483">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="6d280-484">En el panel derecho, en el cuadro **Punto de conexión mensajería,** escriba la dirección URL de ngrok, en nuestro ejemplo, `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="6d280-484">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="6d280-485">Inicie el bot localmente, por ejemplo en Visual Studio modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="6d280-485">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="6d280-486">Pruebe el bot mientras se ejecuta localmente mediante el **chat web** de prueba del portal de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="6d280-486">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="6d280-487">Al igual que el emulador, esta prueba no le permite acceder a Teams funcionalidad específica.</span><span class="sxs-lookup"><span data-stu-id="6d280-487">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="6d280-488">En la ventana del terminal donde `ngrok` se está ejecutando puede ver el tráfico HTTP entre el bot y el cliente de chat web.</span><span class="sxs-lookup"><span data-stu-id="6d280-488">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="6d280-489">Si desea una vista más detallada, en una ventana del navegador introduzca `http://127.0.0.1:4040` la obtenida de la ventana de terminal anterior.</span><span class="sxs-lookup"><span data-stu-id="6d280-489">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="6d280-490">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d280-490">The following image is an example:</span></span>

    ![auth bot teams ngrok pruebas](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="6d280-492">.</span><span class="sxs-lookup"><span data-stu-id="6d280-492">.</span></span>

> [!NOTE]
> <span data-ttu-id="6d280-493">Si detiene y reinicia ngrok, la dirección URL cambia.</span><span class="sxs-lookup"><span data-stu-id="6d280-493">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="6d280-494">Para usar ngrok en el proyecto y, en función de las capacidades que esté utilizando, debe actualizar todas las referencias de DIRECCIÓN URL.</span><span class="sxs-lookup"><span data-stu-id="6d280-494">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="6d280-495">Información adicional</span><span class="sxs-lookup"><span data-stu-id="6d280-495">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="6d280-496">TeamsAppManifest/manifest.jsen</span><span class="sxs-lookup"><span data-stu-id="6d280-496">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="6d280-497">Este manifiesto contiene la información necesaria por Microsoft Teams para conectarse con el bot:</span><span class="sxs-lookup"><span data-stu-id="6d280-497">This manifest contains information needed by Microsoft Teams to connect with the bot:</span></span>  

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

<span data-ttu-id="6d280-498">Con la autenticación, Teams se comporta ligeramente diferente que otros canales, como se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="6d280-498">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="6d280-499">Manejo de la actividad de invocación</span><span class="sxs-lookup"><span data-stu-id="6d280-499">Handling Invoke Activity</span></span>

<span data-ttu-id="6d280-500">Una **actividad de invocación** se envía al bot en lugar de la actividad de eventos utilizada por otros canales.</span><span class="sxs-lookup"><span data-stu-id="6d280-500">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="6d280-501">Esto se hace subclasificando el **ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="6d280-501">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6d280-502">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6d280-502">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="6d280-503">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="6d280-503">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="6d280-504">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="6d280-504">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="6d280-505">La *actividad invoke* debe reenviarse al cuadro de diálogo si se utiliza **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="6d280-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="6d280-506">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="6d280-506">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="6d280-507">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6d280-507">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="6d280-508">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="6d280-508">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="6d280-509">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="6d280-509">**bots/teamsBot.js**</span></span>

<span data-ttu-id="6d280-510">La *actividad invoke* debe reenviarse al cuadro de diálogo si se utiliza **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="6d280-510">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="6d280-511">**diálogos/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="6d280-511">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="6d280-512">Dentro de un paso de diálogo, use `beginDialog` para iniciar el símbolo del sistema OAuth, que pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-512">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="6d280-513">Si el usuario ya ha iniciado sesión, esto generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="6d280-513">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="6d280-514">De lo contrario, esto pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-514">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="6d280-515">Azure Bot Service envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-515">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="6d280-516">En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="6d280-516">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="6d280-517">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="6d280-517">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="6d280-518">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="6d280-518">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="6d280-519">Python</span><span class="sxs-lookup"><span data-stu-id="6d280-519">Python</span></span>](#tab/python-sample)

<span data-ttu-id="6d280-520">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="6d280-520">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="6d280-521">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="6d280-521">**bots/teams_bot.py**</span></span>

<span data-ttu-id="6d280-522">La *actividad invoke* debe reenviarse al cuadro de diálogo si se utiliza **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="6d280-522">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="6d280-523">**diálogos/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="6d280-523">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="6d280-524">Dentro de un paso de diálogo, use `begin_dialog` para iniciar el símbolo del sistema OAuth, que pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-524">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="6d280-525">Si el usuario ya ha iniciado sesión, esto generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="6d280-525">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="6d280-526">De lo contrario, esto pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-526">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="6d280-527">Azure Bot Service envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="6d280-527">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="6d280-528">En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="6d280-528">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="6d280-529">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="6d280-529">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="6d280-530">**diálogos/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="6d280-530">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a><span data-ttu-id="6d280-531">Vea también</span><span class="sxs-lookup"><span data-stu-id="6d280-531">See also</span></span>

[<span data-ttu-id="6d280-532">Agregar autenticación a través de Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="6d280-532">Add authentication through Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
