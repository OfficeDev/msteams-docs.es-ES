---
title: Agregar autenticación a su bot de Teams
author: clearab
description: Cómo agregar la autenticación OAuth a un bot en Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 63d06100f69a5dc3777bdfb20b3231a85dce1f04
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675870"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="831d1-103">Agregar autenticación a su bot de Teams</span><span class="sxs-lookup"><span data-stu-id="831d1-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="831d1-104">En ocasiones, es posible que necesite crear bots en Microsoft teams que puedan tener acceso a recursos en nombre del usuario, como un servicio de correo.</span><span class="sxs-lookup"><span data-stu-id="831d1-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="831d1-105">En este artículo se muestra cómo usar la autenticación de SDK de Azure bot Service V4, basada en OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="831d1-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="831d1-106">Esto hace que sea más fácil desarrollar un bot que puede usar tokens de autenticación en función de las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="831d1-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="831d1-107">La clave en todo esto es el uso de **proveedores de identidades**, como veremos más adelante.</span><span class="sxs-lookup"><span data-stu-id="831d1-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="831d1-108">OAuth 2,0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory (Azure AD) y muchos otros proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="831d1-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="831d1-109">Una descripción básica de OAuth 2,0 es un requisito previo para trabajar con la autenticación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="831d1-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="831d1-110">Consulte [OAuth 2 simplificado](https://aka.ms/oauth2-simplified) para conocer los conocimientos básicos y [OAuth 2,0](https://oauth.net/2/) para la especificación completa.</span><span class="sxs-lookup"><span data-stu-id="831d1-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="831d1-111">Para obtener más información sobre cómo administra el servicio de robots de Azure la autenticación, vea [autenticación de usuario en una conversación](https://aka.ms/azure-bot-authentication).</span><span class="sxs-lookup"><span data-stu-id="831d1-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="831d1-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="831d1-112">In this article you'll learn:</span></span>

- <span data-ttu-id="831d1-113">**Cómo crear un bot habilitado para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="831d1-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="831d1-114">Usar [CS-auth-Sample][teams-auth-bot] para controlar las credenciales de inicio de sesión de usuario y la generación del token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="831d1-114">You'll use [cs-auth-sample][teams-auth-bot] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="831d1-115">**Cómo implementar el bot en Azure y asociarlo con un proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="831d1-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="831d1-116">El proveedor emite un token en función de las credenciales de inicio de sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="831d1-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="831d1-117">El bot puede usar el token para obtener acceso a los recursos, como un servicio de correo, que requieren autenticación.</span><span class="sxs-lookup"><span data-stu-id="831d1-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="831d1-118">Para obtener más información, vea [flujo de autenticación de Microsoft Teams para bots](auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="831d1-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="831d1-119">**Cómo integrar el bot en Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="831d1-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="831d1-120">Una vez que se ha integrado el bot, puede iniciar sesión y intercambiar mensajes con él en un chat.</span><span class="sxs-lookup"><span data-stu-id="831d1-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="831d1-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="831d1-121">Prerequisites</span></span>

- <span data-ttu-id="831d1-122">Información sobre los [aspectos básicos][concept-basics]de los bot, la [Administración del estado][concept-state], la biblioteca de cuadros de [diálogo][concept-dialogs]y cómo implementar un [flujo de conversación secuencial][simple-dialog].</span><span class="sxs-lookup"><span data-stu-id="831d1-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="831d1-123">Conocimientos del desarrollo de Azure y OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="831d1-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="831d1-124">Visual Studio 2017 o posterior y git.</span><span class="sxs-lookup"><span data-stu-id="831d1-124">Visual Studio 2017 or later and Git.</span></span>
- <span data-ttu-id="831d1-125">Cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="831d1-125">Azure account.</span></span> <span data-ttu-id="831d1-126">Si es necesario, puede crear una [cuenta gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="831d1-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="831d1-127">El siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="831d1-127">The following sample.</span></span>

    | <span data-ttu-id="831d1-128">Muestra</span><span class="sxs-lookup"><span data-stu-id="831d1-128">Sample</span></span> | <span data-ttu-id="831d1-129">Versión de BotBuilder</span><span class="sxs-lookup"><span data-stu-id="831d1-129">BotBuilder version</span></span> | <span data-ttu-id="831d1-130">Muestre</span><span class="sxs-lookup"><span data-stu-id="831d1-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="831d1-131">**Autenticación de bot** en [CS-auth-Sample][teams-auth-bot]</span><span class="sxs-lookup"><span data-stu-id="831d1-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot]</span></span> | <span data-ttu-id="831d1-132">IPv4</span><span class="sxs-lookup"><span data-stu-id="831d1-132">v4</span></span> | <span data-ttu-id="831d1-133">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="831d1-133">OAuthCard support</span></span> |
    | <span data-ttu-id="831d1-134">**Autenticación de bot** en [Python-auth-Sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="831d1-134">**Bot authentication** in [python-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="831d1-135">IPv4</span><span class="sxs-lookup"><span data-stu-id="831d1-135">v4</span></span> | <span data-ttu-id="831d1-136">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="831d1-136">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="831d1-137">Crear el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="831d1-137">Create the resource group</span></span>

<span data-ttu-id="831d1-138">El grupo de recursos y el plan de servicio no son estrictamente necesarios, pero le permiten liberar de forma cómoda los recursos que cree.</span><span class="sxs-lookup"><span data-stu-id="831d1-138">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="831d1-139">Esta es una buena práctica para mantener los recursos organizados y fáciles de administrar.</span><span class="sxs-lookup"><span data-stu-id="831d1-139">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="831d1-140">Puede usar un grupo de recursos para crear recursos individuales para el marco de robots.</span><span class="sxs-lookup"><span data-stu-id="831d1-140">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="831d1-141">Para el rendimiento, asegúrese de que estos recursos se encuentran en el mismo área de Azure.</span><span class="sxs-lookup"><span data-stu-id="831d1-141">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="831d1-142">En el explorador, inicie sesión en [**Azure portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="831d1-142">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="831d1-143">En el panel de navegación izquierdo, seleccione **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="831d1-143">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="831d1-144">En la esquina superior izquierda de la ventana que se muestra, seleccione **Agregar** ficha para crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="831d1-144">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="831d1-145">Se le pedirá que proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="831d1-145">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="831d1-146">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="831d1-146">**Subscription**.</span></span> <span data-ttu-id="831d1-147">Use la suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="831d1-147">Use your existing subscription.</span></span>
    1. <span data-ttu-id="831d1-148">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="831d1-148">**Resource group**.</span></span> <span data-ttu-id="831d1-149">Escriba el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="831d1-149">Enter the name for the resource group.</span></span> <span data-ttu-id="831d1-150">Un ejemplo podría ser *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="831d1-150">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="831d1-151">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="831d1-151">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="831d1-152">En el menú desplegable **región** , seleccione *oeste de EE. UU.* o una región cercana a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="831d1-152">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="831d1-153">Seleccione el botón **revisar y crear** .</span><span class="sxs-lookup"><span data-stu-id="831d1-153">Select the **Review and create** button.</span></span> <span data-ttu-id="831d1-154">Debería ver un banner que lee la *validación pasada*.</span><span class="sxs-lookup"><span data-stu-id="831d1-154">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="831d1-155">Seleccione el botón **crear** .</span><span class="sxs-lookup"><span data-stu-id="831d1-155">Select the **Create** button.</span></span> <span data-ttu-id="831d1-156">La creación del grupo de recursos puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="831d1-156">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="831d1-157">Como con los recursos que creará más adelante en este tutorial, es una buena idea anclar este grupo de recursos en el panel para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="831d1-157">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="831d1-158">Si quiere hacerlo, seleccione el icono PIN & # 128204; en la esquina superior derecha del panel.</span><span class="sxs-lookup"><span data-stu-id="831d1-158">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="831d1-159">Crear el plan de servicio</span><span class="sxs-lookup"><span data-stu-id="831d1-159">Create the service plan</span></span>

1. <span data-ttu-id="831d1-160">En el panel de navegación izquierdo de [**Azure portal**][azure-portal], seleccione **crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="831d1-160">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="831d1-161">En el cuadro de búsqueda, escriba *plan de App Service*.</span><span class="sxs-lookup"><span data-stu-id="831d1-161">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="831d1-162">Seleccione la tarjeta de **planeación de App Service** en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="831d1-162">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="831d1-163">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="831d1-163">Select **Create**.</span></span>
1. <span data-ttu-id="831d1-164">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="831d1-164">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="831d1-165">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="831d1-165">**Subscription**.</span></span> <span data-ttu-id="831d1-166">Puede usar una suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="831d1-166">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="831d1-167">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="831d1-167">**Resource Group**.</span></span> <span data-ttu-id="831d1-168">Seleccione el grupo que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="831d1-168">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="831d1-169">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="831d1-169">**Name**.</span></span> <span data-ttu-id="831d1-170">Escriba el nombre del plan de servicio.</span><span class="sxs-lookup"><span data-stu-id="831d1-170">Enter the name for the service plan.</span></span> <span data-ttu-id="831d1-171">Un ejemplo podría ser *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="831d1-171">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="831d1-172">Recuerde que el nombre debe ser único dentro del grupo.</span><span class="sxs-lookup"><span data-stu-id="831d1-172">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="831d1-173">**Sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="831d1-173">**Operating System**.</span></span> <span data-ttu-id="831d1-174">Seleccione *Windows* o su sistema operativo aplicable.</span><span class="sxs-lookup"><span data-stu-id="831d1-174">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="831d1-175">**Región**.</span><span class="sxs-lookup"><span data-stu-id="831d1-175">**Region**.</span></span> <span data-ttu-id="831d1-176">Seleccione *oeste de EE. UU.* o una región cercana a sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="831d1-176">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="831d1-177">**Plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="831d1-177">**Pricing Tier**.</span></span> <span data-ttu-id="831d1-178">Asegúrese de que está seleccionado el *estándar S1* .</span><span class="sxs-lookup"><span data-stu-id="831d1-178">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="831d1-179">Este debe ser el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="831d1-179">This should be the default value.</span></span>
    1. <span data-ttu-id="831d1-180">Seleccione el botón **revisar y crear** .</span><span class="sxs-lookup"><span data-stu-id="831d1-180">Select the **Review and create** button.</span></span> <span data-ttu-id="831d1-181">Debería ver un banner que lee la *validación pasada*.</span><span class="sxs-lookup"><span data-stu-id="831d1-181">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="831d1-182">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="831d1-182">Select **Create**.</span></span> <span data-ttu-id="831d1-183">Puede tardar unos minutos en crear el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="831d1-183">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="831d1-184">El plan se mostrará en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="831d1-184">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="831d1-185">Crear el registro de los canales de bot</span><span class="sxs-lookup"><span data-stu-id="831d1-185">Create the bot channels registration</span></span>

<span data-ttu-id="831d1-186">El registro de los canales de bot registra el servicio web como un bot con bot Framework, siempre que tenga un identificador de aplicación de Microsoft y una contraseña de aplicación (secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="831d1-186">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="831d1-187">Solo tiene que registrar el bot si no está hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="831d1-187">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="831d1-188">Si ha [creado un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) a través de Azure portal, ya está registrado con el servicio.</span><span class="sxs-lookup"><span data-stu-id="831d1-188">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="831d1-189">Si ha creado el bot a través del [marco de robots](https://dev.botframework.com/bots/new) o [AppStudio](~/concepts/build-and-test/app-studio-overview.md) , el bot no está registrado en Azure.</span><span class="sxs-lookup"><span data-stu-id="831d1-189">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="831d1-190">Una vez que Azure haya creado el recurso de registro, se incluirá en la lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="831d1-190">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![Grupo de registro de canales de aplicación de bot](../../../assets/images/authentication/auth-bot-channels-registration-group.PNG)

> [!NOTE]
> <span data-ttu-id="831d1-192">El recurso de registro de los canales de bot mostrará la región **global** aunque haya seleccionado oeste de EE. UU..</span><span class="sxs-lookup"><span data-stu-id="831d1-192">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="831d1-193">Esto es lo que se espera.</span><span class="sxs-lookup"><span data-stu-id="831d1-193">This is expected.</span></span>

<span data-ttu-id="831d1-194">Para obtener más información, consulte [crear un bot para Teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="831d1-194">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="831d1-195">Crear el proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="831d1-195">Create the identity provider</span></span>

<span data-ttu-id="831d1-196">Necesita un proveedor de identidad que se pueda usar para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="831d1-196">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="831d1-197">En este procedimiento, usará un proveedor de Azure AD; también se pueden usar otros proveedores de identidades compatibles con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="831d1-197">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="831d1-198">En el panel de navegación izquierdo de [**Azure portal**][azure-portal], seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="831d1-198">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="831d1-199">Deberá crear y registrar este recurso de Azure AD en un espacio empresarial en el que pueda dar su consentimiento para delegar permisos solicitados por una aplicación.</span><span class="sxs-lookup"><span data-stu-id="831d1-199">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="831d1-200">Para obtener instrucciones sobre cómo crear un inquilino, vea [obtener acceso al portal y crear un inquilino](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span><span class="sxs-lookup"><span data-stu-id="831d1-200">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="831d1-201">En el panel izquierdo, seleccione **registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="831d1-201">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="831d1-202">En el panel derecho, seleccione la pestaña **registro nuevo** , en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="831d1-202">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="831d1-203">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="831d1-203">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="831d1-204">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="831d1-204">**Name**.</span></span> <span data-ttu-id="831d1-205">Escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="831d1-205">Enter the name for the application.</span></span> <span data-ttu-id="831d1-206">Un ejemplo podría ser *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="831d1-206">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="831d1-207">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="831d1-207">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="831d1-208">Seleccione los **tipos de cuenta admitidos** para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="831d1-208">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="831d1-209">Seleccione *cuentas en cualquier directorio de la organización (cualquier directorio de Azure ad-multiinquilino) y cuentas personales de Microsoft (por ejemplo, Skype, Xbox)*.</span><span class="sxs-lookup"><span data-stu-id="831d1-209">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="831d1-210">Para el **URI de redireccionamiento**:</span><span class="sxs-lookup"><span data-stu-id="831d1-210">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="831d1-211">&#x2713;seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="831d1-211">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="831d1-212">&#x2713; establece la dirección URL `https://token.botframework.com/.auth/web/redirect`en.</span><span class="sxs-lookup"><span data-stu-id="831d1-212">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="831d1-213">Seleccione **registrar**.</span><span class="sxs-lookup"><span data-stu-id="831d1-213">Select **Register**.</span></span>

1. <span data-ttu-id="831d1-214">Una vez creado, Azure muestra la página de **información general** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="831d1-214">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="831d1-215">Copie y guarde la siguiente información en un archivo:</span><span class="sxs-lookup"><span data-stu-id="831d1-215">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="831d1-216">Valor del identificador de la **aplicación (cliente)** .</span><span class="sxs-lookup"><span data-stu-id="831d1-216">The **Application (client) ID** value.</span></span> <span data-ttu-id="831d1-217">Este valor se usará más adelante como *identificador de cliente* al registrar esta aplicación de identidad de Azure en el bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-217">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="831d1-218">El valor del **identificador de directorio (tenant)** .</span><span class="sxs-lookup"><span data-stu-id="831d1-218">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="831d1-219">También usará este valor más adelante como identificador de *inquilino* para registrar esta aplicación de identidad de Azure en su bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-219">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="831d1-220">En el panel izquierdo, seleccione **certificados & secretos** para crear un secreto de cliente para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="831d1-220">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="831d1-221">En **Client Secrets**, seleccione &#x2795; **nuevo secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="831d1-221">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="831d1-222">Agregue una descripción para identificar este secreto con respecto a otros que puede que necesite crear para esta aplicación, como *aplicación de identidad de bot en Teams*.</span><span class="sxs-lookup"><span data-stu-id="831d1-222">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="831d1-223">El valor establecido **expira** en la selección.</span><span class="sxs-lookup"><span data-stu-id="831d1-223">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="831d1-224">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="831d1-224">Select **Add**.</span></span>
   1. <span data-ttu-id="831d1-225">Antes de salir de esta página, **Anote el secreto**.</span><span class="sxs-lookup"><span data-stu-id="831d1-225">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="831d1-226">Este valor se usará más adelante como _secreto de cliente_ al registrar la aplicación de Azure ad en el bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-226">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="831d1-227">Configurar la conexión del proveedor de identidad y registrarla con el bot</span><span class="sxs-lookup"><span data-stu-id="831d1-227">Configure the identity provider connection and register it with the bot</span></span>

1. <span data-ttu-id="831d1-228">En el [**portal de Azure**][azure-portal], seleccione su grupo de recursos en el panel.</span><span class="sxs-lookup"><span data-stu-id="831d1-228">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="831d1-229">Seleccione el vínculo de registro del canal de bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-229">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="831d1-230">En la página recurso, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="831d1-230">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="831d1-231">En **configuración de conexión de OAuth** cerca de la parte inferior de la página, seleccione **Agregar configuración**.</span><span class="sxs-lookup"><span data-stu-id="831d1-231">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="831d1-232">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="831d1-232">Complete the form as follows:</span></span>

    1. <span data-ttu-id="831d1-233">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="831d1-233">**Name**.</span></span> <span data-ttu-id="831d1-234">Escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="831d1-234">Enter a name for the connection.</span></span> <span data-ttu-id="831d1-235">Usará este nombre en el bot en el `appsettings.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="831d1-235">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="831d1-236">Por ejemplo *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="831d1-236">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="831d1-237">**Proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="831d1-237">**Service Provider**.</span></span> <span data-ttu-id="831d1-238">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="831d1-238">Select **Azure Active Directory**.</span></span> <span data-ttu-id="831d1-239">Una vez que seleccione esto, se mostrarán los campos específicos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="831d1-239">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="831d1-240">**Identificador de cliente**. Escriba el identificador de la aplicación (cliente) que anotó para su aplicación de proveedor de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="831d1-240">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="831d1-241">**Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="831d1-241">**Client secret**.</span></span> <span data-ttu-id="831d1-242">Escriba el secreto que anotó para su aplicación de proveedor de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="831d1-242">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="831d1-243">**Tipo de concesión**.</span><span class="sxs-lookup"><span data-stu-id="831d1-243">**Grant Type**.</span></span> <span data-ttu-id="831d1-244">Entrar `authorization_code`.</span><span class="sxs-lookup"><span data-stu-id="831d1-244">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="831d1-245">**Dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="831d1-245">**Login URL**.</span></span> <span data-ttu-id="831d1-246">Entrar `https://login.microsoftonline.com`.</span><span class="sxs-lookup"><span data-stu-id="831d1-246">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="831d1-247">**Identificador de inquilino**, escriba el **identificador de directorio (inquilino)** que anotó anteriormente para la aplicación de identidad de Azure o **Common** , según el tipo de cuenta compatible que se haya seleccionado cuando se creó la aplicación de proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="831d1-247">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="831d1-248">Para decidir qué valor asignar, siga estos criterios:</span><span class="sxs-lookup"><span data-stu-id="831d1-248">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="831d1-249">Si seleccionó *solo cuentas en este directorio de la organización (solo Microsoft-inquilino único)* o *cuentas en cualquier directorio de la organización (Microsoft AAD Directory-multiinquilino)* , escriba el **identificador de inquilino** que ha registrado anteriormente para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="831d1-249">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="831d1-250">Este será el inquilino asociado con los usuarios que se pueden autenticar.</span><span class="sxs-lookup"><span data-stu-id="831d1-250">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="831d1-251">Si seleccionó *cuentas en cualquier directorio de la organización (cualquier espacio empresarial de AAD y cuentas personales de Microsoft, por ejemplo, Skype, Xbox, Outlook),* escriba la palabra **Common** en lugar de un identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="831d1-251">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="831d1-252">De lo contrario, la aplicación de AAD comprobará en el inquilino cuyo identificador se haya seleccionado y excluya las cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="831d1-252">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="831d1-253">h.</span><span class="sxs-lookup"><span data-stu-id="831d1-253">h.</span></span> <span data-ttu-id="831d1-254">En **dirección URL**del recurso `https://graph.microsoft.com/`, escriba.</span><span class="sxs-lookup"><span data-stu-id="831d1-254">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="831d1-255">No se usa en el ejemplo de código actual.</span><span class="sxs-lookup"><span data-stu-id="831d1-255">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="831d1-256">sigo.</span><span class="sxs-lookup"><span data-stu-id="831d1-256">i.</span></span> <span data-ttu-id="831d1-257">Deje los **ámbitos** en blanco.</span><span class="sxs-lookup"><span data-stu-id="831d1-257">Leave **Scopes** blank.</span></span> <span data-ttu-id="831d1-258">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="831d1-258">The following image is an example:</span></span>

    ![la cadena de conexión de autenticación de la aplicación bots de Microsoft Teams Adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="831d1-260">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="831d1-260">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="831d1-261">Probar la conexión</span><span class="sxs-lookup"><span data-stu-id="831d1-261">Test the connection</span></span>

1. <span data-ttu-id="831d1-262">Seleccione la entrada de conexión para abrir la conexión que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="831d1-262">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="831d1-263">Seleccione **probar conexión** en la parte superior del panel **configuración de conexión del proveedor de servicios** .</span><span class="sxs-lookup"><span data-stu-id="831d1-263">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="831d1-264">La primera vez que lo haga, se abrirá una nueva ventana del explorador en la que se le pedirá que seleccione una cuenta.</span><span class="sxs-lookup"><span data-stu-id="831d1-264">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="831d1-265">Seleccione el que desee usar.</span><span class="sxs-lookup"><span data-stu-id="831d1-265">Select the one you want to use.</span></span>
1. <span data-ttu-id="831d1-266">A continuación, se le pedirá que lo permita al proveedor de identidades para usar sus datos (credenciales).</span><span class="sxs-lookup"><span data-stu-id="831d1-266">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="831d1-267">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="831d1-267">The following image is an example:</span></span>

    ![la cadena de conexión de autenticación de la aplicación bots de Microsoft Teams Adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="831d1-269">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="831d1-269">Select **Accept**.</span></span>
1. <span data-ttu-id="831d1-270">Esto debería redirigirlo a una **conexión de prueba con \<el nombre de-conexión-nombre> Página realizada correctamente** .</span><span class="sxs-lookup"><span data-stu-id="831d1-270">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="831d1-271">Actualice la página si recibe un error.</span><span class="sxs-lookup"><span data-stu-id="831d1-271">Refresh the page if you get an error.</span></span> <span data-ttu-id="831d1-272">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="831d1-272">The following image is an example:</span></span>

  ![la cadena de conexión de autenticación de la aplicación bots de Microsoft Teams Adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="831d1-274">El código de bot usa el nombre de la conexión para recuperar los tokens de autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="831d1-274">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="831d1-275">Preparar el código de ejemplo de bot</span><span class="sxs-lookup"><span data-stu-id="831d1-275">Prepare the bot sample code</span></span>

<span data-ttu-id="831d1-276">Una vez finalizada la configuración preliminar, vamos a centrarse en la creación del bot que se va a usar en este artículo.</span><span class="sxs-lookup"><span data-stu-id="831d1-276">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="831d1-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="831d1-277">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="831d1-278">Clone [CS-auth-Sample][teams-auth-bot].</span><span class="sxs-lookup"><span data-stu-id="831d1-278">Clone [cs-auth-sample][teams-auth-bot].</span></span>
1. <span data-ttu-id="831d1-279">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="831d1-279">Launch Visual Studio.</span></span>
1. <span data-ttu-id="831d1-280">En la barra de herramientas **, seleccione archivo > abrir > proyecto/solución** y abra el proyecto de bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-280">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="831d1-281">En C#, actualice **appSettings. JSON** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="831d1-281">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="831d1-282">Establezca `ConnectionName` el nombre de la conexión del proveedor de identidad que agregó al registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-282">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="831d1-283">El nombre usado en este ejemplo es *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="831d1-283">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="831d1-284">Establezca `MicrosoftAppId` el identificador de la **aplicación de bot** que guardó en el momento del registro del canal de bot? n.</span><span class="sxs-lookup"><span data-stu-id="831d1-284">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="831d1-285">Establezca `MicrosoftAppPassword` el **secreto de cliente** que guardó en el momento del registro del canal de bot?</span><span class="sxs-lookup"><span data-stu-id="831d1-285">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="831d1-286">Establezca el `ConnectionName` como el nombre de la conexión del proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="831d1-286">Set the `ConnectionName` to the name of the identity provider connection.</span></span> 

    <span data-ttu-id="831d1-287">Según los caracteres del secreto de bot, es posible que deba omitir la contraseña XML.</span><span class="sxs-lookup"><span data-stu-id="831d1-287">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="831d1-288">Por ejemplo, cualquier "y" comercial (&) tendrá que codificarse como `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="831d1-288">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="831d1-289">En el explorador de soluciones, vaya a `TeamsAppManifest` la carpeta, `manifest.json` abra y `id` defina `botId` y el **identificador** de la aplicación de bot que guardó en el momento del registro del canal de bot? n.</span><span class="sxs-lookup"><span data-stu-id="831d1-289">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="pythontabpython"></a>[<span data-ttu-id="831d1-290">Python</span><span class="sxs-lookup"><span data-stu-id="831d1-290">Python</span></span>](#tab/python)

1. <span data-ttu-id="831d1-291">Clonar la autenticación de robot de muestra de [Teams][teams-auth-bot-py] desde el repositorio de github.</span><span class="sxs-lookup"><span data-stu-id="831d1-291">Clone the sample [Teams bot authentication][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="831d1-292">Actualizar **config.py**:</span><span class="sxs-lookup"><span data-stu-id="831d1-292">Update **config.py**:</span></span>

    - <span data-ttu-id="831d1-293">Establezca `ConnectionName` el nombre de la configuración de conexión OAuth que ha agregado a su bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-293">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="831d1-294">Establezca `MicrosoftAppId` el `MicrosoftAppPassword` identificador de aplicación y el secreto de la aplicación en el bot? n.</span><span class="sxs-lookup"><span data-stu-id="831d1-294">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="831d1-295">Según los caracteres del secreto de bot, es posible que deba omitir la contraseña XML.</span><span class="sxs-lookup"><span data-stu-id="831d1-295">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="831d1-296">Por ejemplo, cualquier "y" comercial (&) tendrá que codificarse como `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="831d1-296">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="831d1-297">Implementar el bot en Azure</span><span class="sxs-lookup"><span data-stu-id="831d1-297">Deploy the bot to Azure</span></span>

<span data-ttu-id="831d1-298">Para implementar el bot, siga los pasos descritos en How to [deploy Your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="831d1-298">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="831d1-299">Como alternativa, en Visual Studio, puede seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="831d1-299">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="831d1-300">En el *Explorador de soluciones* de Visual Studio, seleccione y mantenga presionado (o haga clic con el botón derecho) en el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="831d1-300">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="831d1-301">En el menú desplegable, seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="831d1-301">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="831d1-302">En la ventana que se muestra, seleccione el **nuevo** vínculo.</span><span class="sxs-lookup"><span data-stu-id="831d1-302">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="831d1-303">En la ventana de diálogo, seleccione **servicio de aplicaciones** a la izquierda y **crear nuevo** a la derecha.</span><span class="sxs-lookup"><span data-stu-id="831d1-303">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="831d1-304">Seleccione el botón **publicar** .</span><span class="sxs-lookup"><span data-stu-id="831d1-304">Select the **Publish** button.</span></span>
1. <span data-ttu-id="831d1-305">En la siguiente ventana de diálogo, escriba la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="831d1-305">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="831d1-306">A continuación puede ver un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="831d1-306">The following is an example:</span></span>

   ![auth-App-Service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="831d1-308">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="831d1-308">Select **Create**.</span></span>
1. <span data-ttu-id="831d1-309">Si la implementación se completa correctamente, debería verse reflejada en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="831d1-309">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="831d1-310">Además, se muestra una página en el explorador predeterminado que indica que *su bot está listo*.</span><span class="sxs-lookup"><span data-stu-id="831d1-310">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="831d1-311">La dirección URL será similar a esta: `https://botteamsauth.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="831d1-311">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="831d1-312">Guárdelo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="831d1-312">Save it to a file.</span></span>
1. <span data-ttu-id="831d1-313">En el explorador, vaya a [**Azure portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="831d1-313">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="831d1-314">Compruebe el grupo de recursos, el bot debe aparecer junto con los otros recursos.</span><span class="sxs-lookup"><span data-stu-id="831d1-314">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="831d1-315">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="831d1-315">The following image is an example:</span></span>

    ![Teams-bot-auth-App-Service-Group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="831d1-317">En el grupo de recursos, seleccione el nombre de registro del canal del bot (vínculo).</span><span class="sxs-lookup"><span data-stu-id="831d1-317">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="831d1-318">En el panel izquierdo, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="831d1-318">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="831d1-319">En el cuadro **extremo de mensajería** , escriba la dirección URL que se `api/messages`ha obtenido anteriormente y, a continuación,.</span><span class="sxs-lookup"><span data-stu-id="831d1-319">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="831d1-320">Este es un ejemplo: `https://botteamsauth.azurewebsites.net/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="831d1-320">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="831d1-321">Seleccione el botón **Guardar** en la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="831d1-321">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="831d1-322">Probar el bot con el emulador</span><span class="sxs-lookup"><span data-stu-id="831d1-322">Test the bot using the Emulator</span></span>

<span data-ttu-id="831d1-323">Si aún no lo ha hecho, instale el [emulador de Microsoft bot Framework](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="831d1-323">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="831d1-324">Vea también [depurar con el emulador](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="831d1-324">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="831d1-325">Para que el inicio de sesión de ejemplo de bot funcione, debe configurar el emulador como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="831d1-325">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="831d1-326">Configurar el emulador para la autenticación</span><span class="sxs-lookup"><span data-stu-id="831d1-326">Configure the Emulator for authentication</span></span>

<span data-ttu-id="831d1-327">Si un bot requiere autenticación, debe configurar el emulador tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="831d1-327">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="831d1-328">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="831d1-328">Start the Emulator.</span></span>
1. <span data-ttu-id="831d1-329">En el emulador, seleccione el icono de engranaje &#9881; en la parte inferior izquierda o la pestaña **configuración del emulador** en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="831d1-329">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="831d1-330">Active la casilla para **usar los tokens de autenticación de la versión 1,0**.</span><span class="sxs-lookup"><span data-stu-id="831d1-330">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="831d1-331">Escriba la ruta de acceso local a la herramienta **ngrok** .</span><span class="sxs-lookup"><span data-stu-id="831d1-331">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="831d1-332">*Consulte* el [wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))del emulador/ngrok de la integración de túneles de bot Framework.</span><span class="sxs-lookup"><span data-stu-id="831d1-332">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="831d1-333">Para obtener más información sobre herramientas, consulte [ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="831d1-333">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="831d1-334">Para activar la casilla, **ejecute ngrok cuando se inicie el emulador**.</span><span class="sxs-lookup"><span data-stu-id="831d1-334">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="831d1-335">Seleccione el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="831d1-335">Select the **Save** button.</span></span>

<span data-ttu-id="831d1-336">Cuando el bot muestra una tarjeta de inicio de sesión y el usuario selecciona el botón de inicio de sesión, el emulador abre una página que el usuario puede usar para iniciar sesión con el proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="831d1-336">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="831d1-337">Una vez que el usuario lo hace, el proveedor genera un token de usuario y lo envía al bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-337">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="831d1-338">Después de eso, el bot puede actuar en nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="831d1-338">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="831d1-339">Probar el bot localmente</span><span class="sxs-lookup"><span data-stu-id="831d1-339">Test the bot locally</span></span>

<span data-ttu-id="831d1-340">Una vez que haya configurado el mecanismo de autenticación, puede realizar las pruebas de bot reales.</span><span class="sxs-lookup"><span data-stu-id="831d1-340">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="831d1-341">Ejecute el ejemplo de bot de forma local en el equipo, a través de Visual Studio, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="831d1-341">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="831d1-342">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="831d1-342">Start the Emulator.</span></span>
1. <span data-ttu-id="831d1-343">Seleccione el botón **abrir bot** .</span><span class="sxs-lookup"><span data-stu-id="831d1-343">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="831d1-344">En la **dirección URL del bot**, escriba la dirección URL local del bot? n.</span><span class="sxs-lookup"><span data-stu-id="831d1-344">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="831d1-345">Normalmente, `http://localhost:3978/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="831d1-345">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="831d1-346">En el **identificador de aplicación de Microsoft** , escriba el identificador de `appsettings.json`aplicación del bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-346">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="831d1-347">En la **contraseña de aplicación de Microsoft** , escriba la contraseña de aplicación `appsettings.json`del bot desde el.</span><span class="sxs-lookup"><span data-stu-id="831d1-347">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="831d1-348">Seleccione **conectar**.</span><span class="sxs-lookup"><span data-stu-id="831d1-348">Select **Connect**.</span></span>
1. <span data-ttu-id="831d1-349">Una vez que el bot esté funcionando, escriba el texto para mostrar la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="831d1-349">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="831d1-350">Seleccione el botón **iniciar sesión** .</span><span class="sxs-lookup"><span data-stu-id="831d1-350">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="831d1-351">Se muestra un cuadro de diálogo emergente para **confirmar la dirección URL abierta**.</span><span class="sxs-lookup"><span data-stu-id="831d1-351">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="831d1-352">Esto permite que el usuario del bot (usted) se autentique.</span><span class="sxs-lookup"><span data-stu-id="831d1-352">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="831d1-353">Seleccione **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="831d1-353">Select **Confirm**.</span></span>
1. <span data-ttu-id="831d1-354">Si se le solicita, seleccione la cuenta de usuario correspondiente.</span><span class="sxs-lookup"><span data-stu-id="831d1-354">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="831d1-355">En función de la configuración que haya usado para el emulador, puede obtener una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="831d1-355">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="831d1-356">**Usar el código de comprobación de inicio de sesión**</span><span class="sxs-lookup"><span data-stu-id="831d1-356">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="831d1-357">&#x2713; se abre una ventana en la que se muestra el código de validación.</span><span class="sxs-lookup"><span data-stu-id="831d1-357">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="831d1-358">&#x2713; copiar y escriba el código de validación en el cuadro chat para completar el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="831d1-358">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="831d1-359">**Uso de tokens de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="831d1-359">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="831d1-360">&#x2713; ha iniciado sesión en función de sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="831d1-360">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="831d1-361">La siguiente imagen es un ejemplo de la interfaz de usuario de bot una vez que ha iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="831d1-361">The following image is an example of the bot UI after you've logged in:</span></span>

    ![emulador de inicio de sesión de bot auth](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="831d1-363">Si selecciona **sí** cuando el robot le pregunta si desea *ver el token?*, obtendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="831d1-363">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![token del emulador de inicio de sesión del robot de auth](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="831d1-365">Escriba **Logout** en el cuadro chat de entrada para cerrar la sesión. Esto libera el token de usuario y el bot no podrá actuar en su nombre hasta que vuelva a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="831d1-365">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="831d1-366">La autenticación de bot requiere el uso del **servicio de conector de bot**.</span><span class="sxs-lookup"><span data-stu-id="831d1-366">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="831d1-367">El servicio tiene acceso a la información de registro de los canales de bot para el bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-367">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="831d1-368">Probar el bot implementado</span><span class="sxs-lookup"><span data-stu-id="831d1-368">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="831d1-369">En el explorador, vaya a [**Azure portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="831d1-369">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="831d1-370">Busque su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="831d1-370">Find your resource group.</span></span>
1. <span data-ttu-id="831d1-371">Seleccione el vínculo de recursos.</span><span class="sxs-lookup"><span data-stu-id="831d1-371">Select the resource link.</span></span> <span data-ttu-id="831d1-372">Se muestra la página recurso.</span><span class="sxs-lookup"><span data-stu-id="831d1-372">The resource page is displayed.</span></span>
1. <span data-ttu-id="831d1-373">En la página recurso, seleccione **probar en chat web**.</span><span class="sxs-lookup"><span data-stu-id="831d1-373">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="831d1-374">El bot se inicia y muestra los saludos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="831d1-374">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="831d1-375">Escriba cualquier cosa en el cuadro chat.</span><span class="sxs-lookup"><span data-stu-id="831d1-375">Type anything in the chat box.</span></span>
1. <span data-ttu-id="831d1-376">Seleccione el cuadro **iniciar sesión** .</span><span class="sxs-lookup"><span data-stu-id="831d1-376">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="831d1-377">Se muestra un cuadro de diálogo emergente para **confirmar la dirección URL abierta**.</span><span class="sxs-lookup"><span data-stu-id="831d1-377">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="831d1-378">Esto permite que el usuario del bot (usted) se autentique.</span><span class="sxs-lookup"><span data-stu-id="831d1-378">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="831d1-379">Seleccione **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="831d1-379">Select **Confirm**.</span></span>
1. <span data-ttu-id="831d1-380">Si se le solicita, seleccione la cuenta de usuario correspondiente.</span><span class="sxs-lookup"><span data-stu-id="831d1-380">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="831d1-381">La siguiente imagen es un ejemplo de la interfaz de usuario de bot una vez que ha iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="831d1-381">The following image is an example of the bot UI after you have logged in:</span></span>

    ![Inicio de sesión de robot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="831d1-383">.</span><span class="sxs-lookup"><span data-stu-id="831d1-383">.</span></span>

1. <span data-ttu-id="831d1-384">Seleccione el botón **sí** para mostrar el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="831d1-384">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="831d1-385">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="831d1-385">The following image is an example:</span></span>

    ![token de inicio de sesión de robot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="831d1-387">.</span><span class="sxs-lookup"><span data-stu-id="831d1-387">.</span></span>

1. <span data-ttu-id="831d1-388">Escriba Logout para cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="831d1-388">Enter logout to sign out.</span></span>

    ![cierre de sesión de auth bot](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="831d1-390">Si tiene problemas para iniciar sesión, intente probar la conexión de nuevo tal como se describe en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="831d1-390">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="831d1-391">Esto podría volver a crear el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="831d1-391">This could recreate the authentication token.</span></span>
> <span data-ttu-id="831d1-392">Con el cliente de chat Web de bot Framework en Azure, es posible que deba iniciar sesión varias veces antes de que la autenticación se establezca correctamente.</span><span class="sxs-lookup"><span data-stu-id="831d1-392">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="831d1-393">Instalar y probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="831d1-393">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="831d1-394">En el proyecto de bot, asegúrese de `TeamsAppManifest` que la carpeta `manifest.json` contiene el junto `outline.png` con `color.png` los archivos y.</span><span class="sxs-lookup"><span data-stu-id="831d1-394">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="831d1-395">En el explorador de soluciones, desplácese hasta la `TeamsAppManifest` carpeta.</span><span class="sxs-lookup"><span data-stu-id="831d1-395">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="831d1-396">Modifique `manifest.json` asignando los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="831d1-396">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="831d1-397">Asegúrese de que el identificador de la **aplicación de bot** que ha recibido en el momento del registro del `id` canal `botId`de bot esté asignado a y.</span><span class="sxs-lookup"><span data-stu-id="831d1-397">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="831d1-398">Asigne este valor: `validDomains: [ "token.botframework.com" ]`.</span><span class="sxs-lookup"><span data-stu-id="831d1-398">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="831d1-399">Seleccione y **zip** los `manifest.json`archivos `outline.png`, y `color.png` .</span><span class="sxs-lookup"><span data-stu-id="831d1-399">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="831d1-400">Abra **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="831d1-400">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="831d1-401">En el panel izquierdo, en la parte inferior, seleccione el **icono aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="831d1-401">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="831d1-402">En el panel derecho, en la parte inferior, seleccione **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="831d1-402">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="831d1-403">Desplácese a `TeamsAppManifest` la carpeta y cargue el manifiesto comprimido.</span><span class="sxs-lookup"><span data-stu-id="831d1-403">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="831d1-404">Se muestra el siguiente asistente:</span><span class="sxs-lookup"><span data-stu-id="831d1-404">The following wizard is displayed:</span></span>

    ![cargar equipos de robot de autenticación](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="831d1-406">Seleccione el botón **Agregar a un equipo** .</span><span class="sxs-lookup"><span data-stu-id="831d1-406">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="831d1-407">En la siguiente ventana, seleccione el equipo en el que desea usar el bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-407">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="831d1-408">Seleccione el botón **configurar un bot** .</span><span class="sxs-lookup"><span data-stu-id="831d1-408">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="831d1-409">Seleccione los puntos suspensivos (&#x25cf;&#x25cf;&#x25cf;) en el panel de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="831d1-409">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="831d1-410">A continuación, selecciona el icono de **App Studio** .</span><span class="sxs-lookup"><span data-stu-id="831d1-410">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="831d1-411">Seleccione la pestaña **Editor de manifiestos** . Debe ver el icono del bot que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="831d1-411">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="831d1-412">Además, debería poder ver el bot enumerado como un contacto en la lista de chats que puede usar para intercambiar mensajes con el bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-412">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="831d1-413">Probar el bot localmente en Teams</span><span class="sxs-lookup"><span data-stu-id="831d1-413">Testing the bot locally in Teams</span></span>

<span data-ttu-id="831d1-414">Microsoft Teams es un producto basado en la nube completamente, por lo que todos los servicios a los que tiene acceso se encuentran disponibles desde la nube con puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="831d1-414">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="831d1-415">Por lo tanto, para habilitar el bot (nuestro ejemplo) para trabajar en Microsoft Teams, debe publicar el código en la nube que prefiera, o bien hacer que una instancia de ejecución local sea accesible externamente mediante una herramienta de **túnel** .</span><span class="sxs-lookup"><span data-stu-id="831d1-415">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="831d1-416">Se recomienda [ngrok](https://ngrok.com/download), que crea una dirección URL externamente direccionable para un puerto que se abre de forma local en el equipo.</span><span class="sxs-lookup"><span data-stu-id="831d1-416">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="831d1-417">Para configurar ngrok en preparación para la ejecución local de la aplicación de Microsoft Teams, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="831d1-417">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="831d1-418">En una ventana de terminal, vaya al directorio en el `ngrok.exe` que ha instalado.</span><span class="sxs-lookup"><span data-stu-id="831d1-418">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="831d1-419">Se recomienda establecer la ruta de la *variable de entorno* para que apunte a ella.</span><span class="sxs-lookup"><span data-stu-id="831d1-419">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="831d1-420">Ejecutar, por ejemplo, `ngrok http 3978 --host-header=localhost:3978`.</span><span class="sxs-lookup"><span data-stu-id="831d1-420">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="831d1-421">Reemplace el número de Puerto según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="831d1-421">Replace the port number as needed.</span></span>
<span data-ttu-id="831d1-422">Se inicia ngrok para escuchar en el puerto especificado.</span><span class="sxs-lookup"><span data-stu-id="831d1-422">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="831d1-423">A cambio, le proporciona una dirección URL que se puede direccionar externamente, válida durante el tiempo que se ejecute ngrok.</span><span class="sxs-lookup"><span data-stu-id="831d1-423">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="831d1-424">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="831d1-424">The following image is an example:</span></span>

    ![la cadena de conexión de autenticación de la aplicación bots de Microsoft Teams Adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="831d1-426">.</span><span class="sxs-lookup"><span data-stu-id="831d1-426">.</span></span>

1. <span data-ttu-id="831d1-427">Copie la dirección HTTPS de reenvío.</span><span class="sxs-lookup"><span data-stu-id="831d1-427">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="831d1-428">Debe ser similar a la siguiente: `https://dea822bf.ngrok.io/`.</span><span class="sxs-lookup"><span data-stu-id="831d1-428">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="831d1-429">Anexe `/api/messages` para obtener `https://dea822bf.ngrok.io/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="831d1-429">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="831d1-430">Este es el **punto de conexión de mensajes** para que el bot se ejecute localmente en el equipo y sea accesible a través de la web en un chat en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="831d1-430">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="831d1-431">Un último paso para realizar es actualizar el punto de conexión de mensajes del componente implementado.</span><span class="sxs-lookup"><span data-stu-id="831d1-431">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="831d1-432">En el ejemplo, implementamos el bot en Azure.</span><span class="sxs-lookup"><span data-stu-id="831d1-432">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="831d1-433">Por lo tanto, \* \* vamos a realizar estos pasos:</span><span class="sxs-lookup"><span data-stu-id="831d1-433">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="831d1-434">En el explorador, navegue a [**Azure portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="831d1-434">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="831d1-435">Seleccione el **registro del canal del bot**.</span><span class="sxs-lookup"><span data-stu-id="831d1-435">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="831d1-436">En el panel izquierdo, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="831d1-436">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="831d1-437">En el panel derecho, en el cuadro **extremo de mensajería** , escriba la dirección URL de ngrok, en `https://dea822bf.ngrok.io/api/messages`nuestro ejemplo.</span><span class="sxs-lookup"><span data-stu-id="831d1-437">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="831d1-438">Inicie el bot de forma local, por ejemplo, en el modo de depuración de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="831d1-438">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="831d1-439">Pruebe el bot mientras se ejecuta de forma local mediante el **chat web**del portal de bot Framework.</span><span class="sxs-lookup"><span data-stu-id="831d1-439">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="831d1-440">Al igual que en el emulador, esta prueba no permite el acceso a funciones específicas de Teams.</span><span class="sxs-lookup"><span data-stu-id="831d1-440">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="831d1-441">En la ventana de terminal `ngrok` donde se está ejecutando, puede ver el tráfico HTTP entre el bot y el cliente de chat Web.</span><span class="sxs-lookup"><span data-stu-id="831d1-441">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="831d1-442">Si desea una vista más detallada, en una ventana del explorador, `http://127.0.0.1:4040` escriba lo que obtuvo en la ventana de terminal anterior.</span><span class="sxs-lookup"><span data-stu-id="831d1-442">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="831d1-443">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="831d1-443">The following image is an example:</span></span>

    ![autenticación Team bot ngrok pruebas](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="831d1-445">.</span><span class="sxs-lookup"><span data-stu-id="831d1-445">.</span></span>

> [!NOTE]
> <span data-ttu-id="831d1-446">Si detiene y reinicia ngrok, la dirección URL cambia.</span><span class="sxs-lookup"><span data-stu-id="831d1-446">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="831d1-447">Para usar ngrok en su proyecto, y según las capacidades que use, debe actualizar todas las referencias a direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="831d1-447">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>

## <a name="additional-information"></a><span data-ttu-id="831d1-448">Información adicional</span><span class="sxs-lookup"><span data-stu-id="831d1-448">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="831d1-449">TeamsAppManifest/manifest. JSON</span><span class="sxs-lookup"><span data-stu-id="831d1-449">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="831d1-450">Este manifiesto contiene la información que Microsoft Teams necesita para conectarse con el bot.</span><span class="sxs-lookup"><span data-stu-id="831d1-450">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

<span data-ttu-id="831d1-451">Con la autenticación, Teams se comporta de forma ligeramente distinta a otros canales, tal como se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="831d1-451">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="831d1-452">Controlar la actividad de invocación</span><span class="sxs-lookup"><span data-stu-id="831d1-452">Handling Invoke Activity</span></span>

<span data-ttu-id="831d1-453">Se envía una **actividad Invoke** al bot en lugar de a la actividad de evento usada por otros canales.</span><span class="sxs-lookup"><span data-stu-id="831d1-453">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="831d1-454">Esto se realiza mediante la subclase de **ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="831d1-454">This is done by sub-classing the **ActivityHandler**.</span></span>

<span data-ttu-id="831d1-455">**Bots/DialogBot. CS**</span><span class="sxs-lookup"><span data-stu-id="831d1-455">**Bots/DialogBot.cs**</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="831d1-456">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="831d1-456">C#/.NET</span></span>](#tab/dotnet)

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="831d1-457">**Bots/TeamsBot. CS**</span><span class="sxs-lookup"><span data-stu-id="831d1-457">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="831d1-458">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa la **OAuthPrompt** .</span><span class="sxs-lookup"><span data-stu-id="831d1-458">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="831d1-459">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="831d1-459">TeamsActivityHandler.cs</span></span>

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

# <a name="pythontabpython"></a>[<span data-ttu-id="831d1-460">Python</span><span class="sxs-lookup"><span data-stu-id="831d1-460">Python</span></span>](#tab/python)

<span data-ttu-id="831d1-461">**bots/dialog_bot. py**</span><span class="sxs-lookup"><span data-stu-id="831d1-461">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="831d1-462">**bots/teams_bot. py**</span><span class="sxs-lookup"><span data-stu-id="831d1-462">**bots/teams_bot.py**</span></span>

<span data-ttu-id="831d1-463">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa la **OAuthPrompt** .</span><span class="sxs-lookup"><span data-stu-id="831d1-463">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)] 

<span data-ttu-id="831d1-464">**cuadros de diálogo/main_dialog. py**</span><span class="sxs-lookup"><span data-stu-id="831d1-464">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="831d1-465">En un paso de diálogo, `begin_dialog` use para iniciar el símbolo del sistema de OAuth, que le pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="831d1-465">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="831d1-466">Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="831d1-466">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="831d1-467">De lo contrario, se le pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="831d1-467">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="831d1-468">El servicio de bot de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="831d1-468">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="831d1-469">En el siguiente paso de cuadro de diálogo, compruebe si existe un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="831d1-469">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="831d1-470">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="831d1-470">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=54-65)]

<span data-ttu-id="831d1-471">**cuadros de diálogo/logout_dialog. py**</span><span class="sxs-lookup"><span data-stu-id="831d1-471">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="further-reading"></a><span data-ttu-id="831d1-472">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="831d1-472">Further reading</span></span>

- [<span data-ttu-id="831d1-473">Agregar autenticación a su bot a través del servicio de bot de Azure</span><span class="sxs-lookup"><span data-stu-id="831d1-473">Add authentication to your bot via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
