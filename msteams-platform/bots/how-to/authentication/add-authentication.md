---
title: Agregar autenticación a su bot de Teams
author: clearab
description: Cómo agregar la autenticación OAuth a un bot en Microsoft Teams.
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: f5eae27de45cd0932e4d2ed62fa954429a48aa6d
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550983"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="98f3b-103">Agregar autenticación a su bot de Teams</span><span class="sxs-lookup"><span data-stu-id="98f3b-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="98f3b-104">En ocasiones, es posible que necesite crear bots en Microsoft teams que puedan tener acceso a recursos en nombre del usuario, como un servicio de correo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="98f3b-105">En este artículo se muestra cómo usar la autenticación de SDK de Azure bot Service V4, basada en OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="98f3b-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="98f3b-106">Esto hace que sea más fácil desarrollar un bot que puede usar tokens de autenticación en función de las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="98f3b-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="98f3b-107">La clave en todo esto es el uso de **proveedores de identidades**, como veremos más adelante.</span><span class="sxs-lookup"><span data-stu-id="98f3b-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="98f3b-108">OAuth 2,0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory (Azure AD) y muchos otros proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="98f3b-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="98f3b-109">Una descripción básica de OAuth 2,0 es un requisito previo para trabajar con la autenticación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="98f3b-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="98f3b-110">Consulte [OAuth 2 simplificado](https://aka.ms/oauth2-simplified) para conocer los conocimientos básicos y [OAuth 2,0](https://oauth.net/2/) para la especificación completa.</span><span class="sxs-lookup"><span data-stu-id="98f3b-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="98f3b-111">Para obtener más información sobre cómo administra el servicio de robots de Azure la autenticación, vea [autenticación de usuario en una conversación](https://aka.ms/azure-bot-authentication).</span><span class="sxs-lookup"><span data-stu-id="98f3b-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="98f3b-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="98f3b-112">In this article you'll learn:</span></span>

- <span data-ttu-id="98f3b-113">**Cómo crear un bot habilitado para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="98f3b-114">Usar [CS-auth-Sample][teams-auth-bot-cs] para controlar las credenciales de inicio de sesión de usuario y la generación del token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="98f3b-115">**Cómo implementar el bot en Azure y asociarlo con un proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="98f3b-116">El proveedor emite un token en función de las credenciales de inicio de sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="98f3b-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="98f3b-117">El bot puede usar el token para obtener acceso a los recursos, como un servicio de correo, que requieren autenticación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="98f3b-118">Para obtener más información, vea [flujo de autenticación de Microsoft Teams para bots](auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="98f3b-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="98f3b-119">**Cómo integrar el bot en Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="98f3b-120">Una vez que se ha integrado el bot, puede iniciar sesión y intercambiar mensajes con él en un chat.</span><span class="sxs-lookup"><span data-stu-id="98f3b-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98f3b-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="98f3b-121">Prerequisites</span></span>

- <span data-ttu-id="98f3b-122">Información sobre los [aspectos básicos][concept-basics]de los bot, la [Administración del estado][concept-state], la biblioteca de cuadros de [diálogo][concept-dialogs]y cómo implementar un [flujo de conversación secuencial][simple-dialog].</span><span class="sxs-lookup"><span data-stu-id="98f3b-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="98f3b-123">Conocimientos del desarrollo de Azure y OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="98f3b-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="98f3b-124">Las versiones actuales de Visual Studio y git.</span><span class="sxs-lookup"><span data-stu-id="98f3b-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="98f3b-125">Cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="98f3b-125">Azure account.</span></span> <span data-ttu-id="98f3b-126">Si es necesario, puede crear una [cuenta gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="98f3b-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="98f3b-127">El siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-127">The following sample.</span></span>

    | <span data-ttu-id="98f3b-128">Muestra</span><span class="sxs-lookup"><span data-stu-id="98f3b-128">Sample</span></span> | <span data-ttu-id="98f3b-129">Versión de BotBuilder</span><span class="sxs-lookup"><span data-stu-id="98f3b-129">BotBuilder version</span></span> | <span data-ttu-id="98f3b-130">Muestre</span><span class="sxs-lookup"><span data-stu-id="98f3b-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="98f3b-131">**Autenticación de bot** en [CS-auth-Sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="98f3b-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="98f3b-132">IPv4</span><span class="sxs-lookup"><span data-stu-id="98f3b-132">v4</span></span> | <span data-ttu-id="98f3b-133">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="98f3b-133">OAuthCard support</span></span> |
    | <span data-ttu-id="98f3b-134">**Autenticación de bot** en [JS-auth-Sample][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="98f3b-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="98f3b-135">IPv4</span><span class="sxs-lookup"><span data-stu-id="98f3b-135">v4</span></span>| <span data-ttu-id="98f3b-136">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="98f3b-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="98f3b-137">**Autenticación de bot** en [py-auth-Sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="98f3b-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="98f3b-138">IPv4</span><span class="sxs-lookup"><span data-stu-id="98f3b-138">v4</span></span> | <span data-ttu-id="98f3b-139">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="98f3b-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="98f3b-140">Crear el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="98f3b-140">Create the resource group</span></span>

<span data-ttu-id="98f3b-141">El grupo de recursos y el plan de servicio no son estrictamente necesarios, pero le permiten liberar de forma cómoda los recursos que cree.</span><span class="sxs-lookup"><span data-stu-id="98f3b-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="98f3b-142">Esta es una buena práctica para mantener los recursos organizados y fáciles de administrar.</span><span class="sxs-lookup"><span data-stu-id="98f3b-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="98f3b-143">Puede usar un grupo de recursos para crear recursos individuales para el marco de robots.</span><span class="sxs-lookup"><span data-stu-id="98f3b-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="98f3b-144">Para el rendimiento, asegúrese de que estos recursos se encuentran en el mismo área de Azure.</span><span class="sxs-lookup"><span data-stu-id="98f3b-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="98f3b-145">En el explorador, inicie sesión en [**Azure portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="98f3b-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="98f3b-146">En el panel de navegación izquierdo, seleccione **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="98f3b-147">En la esquina superior izquierda de la ventana que se muestra, seleccione **Agregar** ficha para crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="98f3b-148">Se le pedirá que proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="98f3b-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="98f3b-149">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-149">**Subscription**.</span></span> <span data-ttu-id="98f3b-150">Use la suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="98f3b-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="98f3b-151">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-151">**Resource group**.</span></span> <span data-ttu-id="98f3b-152">Escriba el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-152">Enter the name for the resource group.</span></span> <span data-ttu-id="98f3b-153">Un ejemplo podría ser *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="98f3b-154">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="98f3b-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="98f3b-155">En el menú desplegable **región** , seleccione *oeste de EE. UU.* o una región cercana a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="98f3b-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="98f3b-156">Seleccione el botón **revisar y crear** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-156">Select the **Review and create** button.</span></span> <span data-ttu-id="98f3b-157">Debería ver un banner que lee la *validación pasada*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="98f3b-158">Seleccione el botón **crear** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-158">Select the **Create** button.</span></span> <span data-ttu-id="98f3b-159">La creación del grupo de recursos puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="98f3b-160">Como con los recursos que creará más adelante en este tutorial, es una buena idea anclar este grupo de recursos en el panel para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="98f3b-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="98f3b-161">Si quiere hacerlo, seleccione el icono PIN & # 128204; en la esquina superior derecha del panel.</span><span class="sxs-lookup"><span data-stu-id="98f3b-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="98f3b-162">Crear el plan de servicio</span><span class="sxs-lookup"><span data-stu-id="98f3b-162">Create the service plan</span></span>

1. <span data-ttu-id="98f3b-163">En el panel de navegación izquierdo de [**Azure portal**][azure-portal], seleccione **crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="98f3b-164">En el cuadro de búsqueda, escriba *plan de App Service*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="98f3b-165">Seleccione la tarjeta de **planeación de App Service** en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="98f3b-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="98f3b-166">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-166">Select **Create**.</span></span>
1. <span data-ttu-id="98f3b-167">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="98f3b-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="98f3b-168">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-168">**Subscription**.</span></span> <span data-ttu-id="98f3b-169">Puede usar una suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="98f3b-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="98f3b-170">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-170">**Resource Group**.</span></span> <span data-ttu-id="98f3b-171">Seleccione el grupo que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="98f3b-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="98f3b-172">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-172">**Name**.</span></span> <span data-ttu-id="98f3b-173">Escriba el nombre del plan de servicio.</span><span class="sxs-lookup"><span data-stu-id="98f3b-173">Enter the name for the service plan.</span></span> <span data-ttu-id="98f3b-174">Un ejemplo podría ser *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="98f3b-175">Recuerde que el nombre debe ser único dentro del grupo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="98f3b-176">**Sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-176">**Operating System**.</span></span> <span data-ttu-id="98f3b-177">Seleccione *Windows* o su sistema operativo aplicable.</span><span class="sxs-lookup"><span data-stu-id="98f3b-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="98f3b-178">**Región**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-178">**Region**.</span></span> <span data-ttu-id="98f3b-179">Seleccione *oeste de EE. UU.* o una región cercana a sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="98f3b-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="98f3b-180">**Plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-180">**Pricing Tier**.</span></span> <span data-ttu-id="98f3b-181">Asegúrese de que está seleccionado el *estándar S1* .</span><span class="sxs-lookup"><span data-stu-id="98f3b-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="98f3b-182">Este debe ser el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="98f3b-182">This should be the default value.</span></span>
    1. <span data-ttu-id="98f3b-183">Seleccione el botón **revisar y crear** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-183">Select the **Review and create** button.</span></span> <span data-ttu-id="98f3b-184">Debería ver un banner que lee la *validación pasada*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="98f3b-185">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-185">Select **Create**.</span></span> <span data-ttu-id="98f3b-186">Puede tardar unos minutos en crear el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="98f3b-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="98f3b-187">El plan se mostrará en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="98f3b-188">Crear el registro de los canales de bot</span><span class="sxs-lookup"><span data-stu-id="98f3b-188">Create the bot channels registration</span></span>

<span data-ttu-id="98f3b-189">El registro de los canales de bot registra el servicio web como un bot con bot Framework, siempre que tenga un identificador de aplicación de Microsoft y una contraseña de aplicación (secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="98f3b-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98f3b-190">Solo tiene que registrar el bot si no está hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="98f3b-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="98f3b-191">Si ha [creado un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) a través de Azure portal, ya está registrado con el servicio.</span><span class="sxs-lookup"><span data-stu-id="98f3b-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="98f3b-192">Si ha creado el bot a través del [marco de robots](https://dev.botframework.com/bots/new) o [AppStudio](~/concepts/build-and-test/app-studio-overview.md) , el bot no está registrado en Azure.</span><span class="sxs-lookup"><span data-stu-id="98f3b-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="98f3b-193">Una vez que Azure haya creado el recurso de registro, se incluirá en la lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-193">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![Grupo de registro de canales de aplicación de bot](../../../assets/images/authentication/auth-bot-channels-registration-group.PNG)

> [!NOTE]
> <span data-ttu-id="98f3b-195">El recurso de registro de los canales de bot mostrará la región **global** aunque haya seleccionado oeste de EE. UU..</span><span class="sxs-lookup"><span data-stu-id="98f3b-195">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="98f3b-196">Esto es lo que se espera.</span><span class="sxs-lookup"><span data-stu-id="98f3b-196">This is expected.</span></span>

<span data-ttu-id="98f3b-197">Para obtener más información, consulte [crear un bot para Teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="98f3b-197">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="98f3b-198">Crear el proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="98f3b-198">Create the identity provider</span></span>

<span data-ttu-id="98f3b-199">Necesita un proveedor de identidad que se pueda usar para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-199">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="98f3b-200">En este procedimiento, usará un proveedor de Azure AD; también se pueden usar otros proveedores de identidades compatibles con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98f3b-200">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="98f3b-201">En el panel de navegación izquierdo de [**Azure portal**][azure-portal], seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-201">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="98f3b-202">Deberá crear y registrar este recurso de Azure AD en un espacio empresarial en el que pueda dar su consentimiento para delegar permisos solicitados por una aplicación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-202">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="98f3b-203">Para obtener instrucciones sobre cómo crear un inquilino, vea [obtener acceso al portal y crear un inquilino](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span><span class="sxs-lookup"><span data-stu-id="98f3b-203">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="98f3b-204">En el panel izquierdo, seleccione **registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-204">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="98f3b-205">En el panel derecho, seleccione la pestaña **registro nuevo** , en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="98f3b-205">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="98f3b-206">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="98f3b-206">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="98f3b-207">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-207">**Name**.</span></span> <span data-ttu-id="98f3b-208">Escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-208">Enter the name for the application.</span></span> <span data-ttu-id="98f3b-209">Un ejemplo podría ser *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-209">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="98f3b-210">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="98f3b-210">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="98f3b-211">Seleccione los **tipos de cuenta admitidos** para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-211">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="98f3b-212">Seleccione *cuentas en cualquier directorio de la organización (cualquier directorio de Azure ad-multiinquilino) y cuentas personales de Microsoft (por ejemplo, Skype, Xbox)*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-212">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="98f3b-213">Para el **URI de redireccionamiento**:</span><span class="sxs-lookup"><span data-stu-id="98f3b-213">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="98f3b-214">&#x2713;seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-214">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="98f3b-215">&#x2713; establece la dirección URL `https://token.botframework.com/.auth/web/redirect`en.</span><span class="sxs-lookup"><span data-stu-id="98f3b-215">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="98f3b-216">Seleccione **registrar**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-216">Select **Register**.</span></span>

1. <span data-ttu-id="98f3b-217">Una vez creado, Azure muestra la página de **información general** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-217">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="98f3b-218">Copie y guarde la siguiente información en un archivo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-218">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="98f3b-219">Valor del identificador de la **aplicación (cliente)** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-219">The **Application (client) ID** value.</span></span> <span data-ttu-id="98f3b-220">Este valor se usará más adelante como *identificador de cliente* al registrar esta aplicación de identidad de Azure en el bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-220">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="98f3b-221">El valor del **identificador de directorio (tenant)** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-221">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="98f3b-222">También usará este valor más adelante como identificador de *inquilino* para registrar esta aplicación de identidad de Azure en su bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-222">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="98f3b-223">En el panel izquierdo, seleccione **certificados & secretos** para crear un secreto de cliente para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-223">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="98f3b-224">En **Client Secrets**, seleccione &#x2795; **nuevo secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-224">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="98f3b-225">Agregue una descripción para identificar este secreto con respecto a otros que puede que necesite crear para esta aplicación, como *aplicación de identidad de bot en Teams*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-225">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="98f3b-226">El valor establecido **expira** en la selección.</span><span class="sxs-lookup"><span data-stu-id="98f3b-226">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="98f3b-227">Elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-227">Select **Add**.</span></span>
   1. <span data-ttu-id="98f3b-228">Antes de salir de esta página, **Anote el secreto**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-228">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="98f3b-229">Este valor se usará más adelante como _secreto de cliente_ al registrar la aplicación de Azure ad en el bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-229">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="98f3b-230">Configurar la conexión del proveedor de identidad y registrarla con el bot</span><span class="sxs-lookup"><span data-stu-id="98f3b-230">Configure the identity provider connection and register it with the bot</span></span>

1. <span data-ttu-id="98f3b-231">En el [**portal de Azure**][azure-portal], seleccione su grupo de recursos en el panel.</span><span class="sxs-lookup"><span data-stu-id="98f3b-231">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="98f3b-232">Seleccione el vínculo de registro del canal de bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-232">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="98f3b-233">En la página recurso, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-233">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="98f3b-234">En **configuración de conexión de OAuth** cerca de la parte inferior de la página, seleccione **Agregar configuración**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-234">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="98f3b-235">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="98f3b-235">Complete the form as follows:</span></span>

    1. <span data-ttu-id="98f3b-236">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-236">**Name**.</span></span> <span data-ttu-id="98f3b-237">Escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-237">Enter a name for the connection.</span></span> <span data-ttu-id="98f3b-238">Usará este nombre en el bot en el `appsettings.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-238">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="98f3b-239">Por ejemplo *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-239">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="98f3b-240">**Proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-240">**Service Provider**.</span></span> <span data-ttu-id="98f3b-241">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-241">Select **Azure Active Directory**.</span></span> <span data-ttu-id="98f3b-242">Una vez que seleccione esto, se mostrarán los campos específicos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98f3b-242">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="98f3b-243">**Identificador de cliente**. Escriba el identificador de la aplicación (cliente) que anotó para su aplicación de proveedor de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="98f3b-243">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="98f3b-244">**Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-244">**Client secret**.</span></span> <span data-ttu-id="98f3b-245">Escriba el secreto que anotó para su aplicación de proveedor de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="98f3b-245">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="98f3b-246">**Tipo de concesión**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-246">**Grant Type**.</span></span> <span data-ttu-id="98f3b-247">Entrar `authorization_code`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-247">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="98f3b-248">**Dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-248">**Login URL**.</span></span> <span data-ttu-id="98f3b-249">Entrar `https://login.microsoftonline.com`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-249">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="98f3b-250">**Identificador de inquilino**, escriba el **identificador de directorio (inquilino)** que anotó anteriormente para la aplicación de identidad de Azure o **Common** , según el tipo de cuenta compatible que se haya seleccionado cuando se creó la aplicación de proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="98f3b-250">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="98f3b-251">Para decidir qué valor asignar, siga estos criterios:</span><span class="sxs-lookup"><span data-stu-id="98f3b-251">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="98f3b-252">Si seleccionó *solo cuentas en este directorio de la organización (solo Microsoft-inquilino único)* o *cuentas en cualquier directorio de la organización (Microsoft AAD Directory-multiinquilino)* , escriba el **identificador de inquilino** que ha registrado anteriormente para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="98f3b-252">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="98f3b-253">Este será el inquilino asociado con los usuarios que se pueden autenticar.</span><span class="sxs-lookup"><span data-stu-id="98f3b-253">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="98f3b-254">Si seleccionó *cuentas en cualquier directorio de la organización (cualquier espacio empresarial de AAD y cuentas personales de Microsoft, por ejemplo, Skype, Xbox, Outlook),* escriba la palabra **Common** en lugar de un identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="98f3b-254">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="98f3b-255">De lo contrario, la aplicación de AAD comprobará en el inquilino cuyo identificador se haya seleccionado y excluya las cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98f3b-255">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="98f3b-256">h.</span><span class="sxs-lookup"><span data-stu-id="98f3b-256">h.</span></span> <span data-ttu-id="98f3b-257">En **dirección URL**del recurso `https://graph.microsoft.com/`, escriba.</span><span class="sxs-lookup"><span data-stu-id="98f3b-257">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="98f3b-258">No se usa en el ejemplo de código actual.</span><span class="sxs-lookup"><span data-stu-id="98f3b-258">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="98f3b-259">sigo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-259">i.</span></span> <span data-ttu-id="98f3b-260">Deje los **ámbitos** en blanco.</span><span class="sxs-lookup"><span data-stu-id="98f3b-260">Leave **Scopes** blank.</span></span> <span data-ttu-id="98f3b-261">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-261">The following image is an example:</span></span>

    ![la cadena de conexión de autenticación de la aplicación bots de Microsoft Teams Adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="98f3b-263">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-263">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="98f3b-264">Probar la conexión</span><span class="sxs-lookup"><span data-stu-id="98f3b-264">Test the connection</span></span>

1. <span data-ttu-id="98f3b-265">Seleccione la entrada de conexión para abrir la conexión que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="98f3b-265">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="98f3b-266">Seleccione **probar conexión** en la parte superior del panel **configuración de conexión del proveedor de servicios** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-266">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="98f3b-267">La primera vez que lo haga, se abrirá una nueva ventana del explorador en la que se le pedirá que seleccione una cuenta.</span><span class="sxs-lookup"><span data-stu-id="98f3b-267">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="98f3b-268">Seleccione el que desee usar.</span><span class="sxs-lookup"><span data-stu-id="98f3b-268">Select the one you want to use.</span></span>
1. <span data-ttu-id="98f3b-269">A continuación, se le pedirá que lo permita al proveedor de identidades para usar sus datos (credenciales).</span><span class="sxs-lookup"><span data-stu-id="98f3b-269">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="98f3b-270">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-270">The following image is an example:</span></span>

    ![la cadena de conexión de autenticación de la aplicación bots de Microsoft Teams Adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="98f3b-272">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-272">Select **Accept**.</span></span>
1. <span data-ttu-id="98f3b-273">Esto debería redirigirlo a una **conexión de prueba con \<el nombre de-conexión-nombre> Página realizada correctamente** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-273">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="98f3b-274">Actualice la página si recibe un error.</span><span class="sxs-lookup"><span data-stu-id="98f3b-274">Refresh the page if you get an error.</span></span> <span data-ttu-id="98f3b-275">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-275">The following image is an example:</span></span>

  ![la cadena de conexión de autenticación de la aplicación bots de Microsoft Teams Adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="98f3b-277">El código de bot usa el nombre de la conexión para recuperar los tokens de autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="98f3b-277">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="98f3b-278">Preparar el código de ejemplo de bot</span><span class="sxs-lookup"><span data-stu-id="98f3b-278">Prepare the bot sample code</span></span>

<span data-ttu-id="98f3b-279">Una vez finalizada la configuración preliminar, vamos a centrarse en la creación del bot que se va a usar en este artículo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-279">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="98f3b-280">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="98f3b-280">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="98f3b-281">Clone [CS-auth-Sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="98f3b-281">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="98f3b-282">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98f3b-282">Launch Visual Studio.</span></span>
1. <span data-ttu-id="98f3b-283">En la barra de herramientas **, seleccione archivo > abrir > proyecto/solución** y abra el proyecto de bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-283">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="98f3b-284">En C#, actualice **appSettings. JSON** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="98f3b-284">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="98f3b-285">Establezca `ConnectionName` el nombre de la conexión del proveedor de identidad que agregó al registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-285">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="98f3b-286">El nombre usado en este ejemplo es *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-286">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="98f3b-287">Establezca `MicrosoftAppId` el identificador de la **aplicación de bot** que guardó en el momento del registro del canal de bot? n.</span><span class="sxs-lookup"><span data-stu-id="98f3b-287">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="98f3b-288">Establezca `MicrosoftAppPassword` el **secreto de cliente** que guardó en el momento del registro del canal de bot?</span><span class="sxs-lookup"><span data-stu-id="98f3b-288">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="98f3b-289">Establezca el `ConnectionName` como el nombre de la conexión del proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="98f3b-289">Set the `ConnectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="98f3b-290">Según los caracteres del secreto de bot, es posible que deba omitir la contraseña XML.</span><span class="sxs-lookup"><span data-stu-id="98f3b-290">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="98f3b-291">Por ejemplo, cualquier "y" comercial (&) tendrá que codificarse como `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-291">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="98f3b-292">En el explorador de soluciones, vaya a `TeamsAppManifest` la carpeta, `manifest.json` abra y `id` defina `botId` y el **identificador** de la aplicación de bot que guardó en el momento del registro del canal de bot? n.</span><span class="sxs-lookup"><span data-stu-id="98f3b-292">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="98f3b-293">JavaScript</span><span class="sxs-lookup"><span data-stu-id="98f3b-293">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="98f3b-294">Clone [node-auth-Sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="98f3b-294">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="98f3b-295">En una consola, vaya al proyecto:</span><span class="sxs-lookup"><span data-stu-id="98f3b-295">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="98f3b-296">Módulos de instalación</span><span class="sxs-lookup"><span data-stu-id="98f3b-296">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="98f3b-297">Actualice la configuración de **. env** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="98f3b-297">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="98f3b-298">Establezca `MicrosoftAppId` el identificador de la **aplicación de bot** que guardó en el momento del registro del canal de bot? n.</span><span class="sxs-lookup"><span data-stu-id="98f3b-298">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="98f3b-299">Establezca `MicrosoftAppPassword` el **secreto de cliente** que guardó en el momento del registro del canal de bot?</span><span class="sxs-lookup"><span data-stu-id="98f3b-299">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="98f3b-300">Establezca el `connectionName` como el nombre de la conexión del proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="98f3b-300">Set the `connectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="98f3b-301">Según los caracteres del secreto de bot, es posible que deba omitir la contraseña XML.</span><span class="sxs-lookup"><span data-stu-id="98f3b-301">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="98f3b-302">Por ejemplo, cualquier "y" comercial (&) tendrá que codificarse como `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-302">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="98f3b-303">En la `teamsAppManifest` carpeta, Abra `manifest.json` y establezca `id` su **identificador de aplicación** de Microsoft `botId` y el **identificador** de la aplicación de bot que guardó en el momento del registro del canal de bot? n.</span><span class="sxs-lookup"><span data-stu-id="98f3b-303">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="98f3b-304">Python</span><span class="sxs-lookup"><span data-stu-id="98f3b-304">Python</span></span>](#tab/python)

1. <span data-ttu-id="98f3b-305">Clone [py-auth-Sample][teams-auth-bot-py] desde el repositorio de github.</span><span class="sxs-lookup"><span data-stu-id="98f3b-305">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="98f3b-306">Actualizar **config.py**:</span><span class="sxs-lookup"><span data-stu-id="98f3b-306">Update **config.py**:</span></span>

    - <span data-ttu-id="98f3b-307">Establezca `ConnectionName` el nombre de la configuración de conexión OAuth que ha agregado a su bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-307">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="98f3b-308">Establezca `MicrosoftAppId` el `MicrosoftAppPassword` identificador de aplicación y el secreto de la aplicación en el bot? n.</span><span class="sxs-lookup"><span data-stu-id="98f3b-308">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="98f3b-309">Según los caracteres del secreto de bot, es posible que deba omitir la contraseña XML.</span><span class="sxs-lookup"><span data-stu-id="98f3b-309">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="98f3b-310">Por ejemplo, cualquier "y" comercial (&) tendrá que codificarse como `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-310">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="98f3b-311">Implementar el bot en Azure</span><span class="sxs-lookup"><span data-stu-id="98f3b-311">Deploy the bot to Azure</span></span>

<span data-ttu-id="98f3b-312">Para implementar el bot, siga los pasos descritos en How to [deploy Your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="98f3b-312">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="98f3b-313">Como alternativa, en Visual Studio, puede seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98f3b-313">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="98f3b-314">En el *Explorador de soluciones* de Visual Studio, seleccione y mantenga presionado (o haga clic con el botón derecho) en el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="98f3b-314">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="98f3b-315">En el menú desplegable, seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-315">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="98f3b-316">En la ventana que se muestra, seleccione el **nuevo** vínculo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-316">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="98f3b-317">En la ventana de diálogo, seleccione **servicio de aplicaciones** a la izquierda y **crear nuevo** a la derecha.</span><span class="sxs-lookup"><span data-stu-id="98f3b-317">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="98f3b-318">Seleccione el botón **publicar** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-318">Select the **Publish** button.</span></span>
1. <span data-ttu-id="98f3b-319">En la siguiente ventana de diálogo, escriba la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="98f3b-319">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="98f3b-320">A continuación puede ver un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-320">The following is an example:</span></span>

   ![auth-App-Service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="98f3b-322">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-322">Select **Create**.</span></span>
1. <span data-ttu-id="98f3b-323">Si la implementación se completa correctamente, debería verse reflejada en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98f3b-323">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="98f3b-324">Además, se muestra una página en el explorador predeterminado que indica que *su bot está listo*.</span><span class="sxs-lookup"><span data-stu-id="98f3b-324">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="98f3b-325">La dirección URL será similar a esta: `https://botteamsauth.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-325">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="98f3b-326">Guárdelo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-326">Save it to a file.</span></span>
1. <span data-ttu-id="98f3b-327">En el explorador, vaya a [**Azure portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="98f3b-327">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="98f3b-328">Compruebe el grupo de recursos, el bot debe aparecer junto con los otros recursos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-328">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="98f3b-329">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-329">The following image is an example:</span></span>

    ![Teams-bot-auth-App-Service-Group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="98f3b-331">En el grupo de recursos, seleccione el nombre de registro del canal del bot (vínculo).</span><span class="sxs-lookup"><span data-stu-id="98f3b-331">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="98f3b-332">En el panel izquierdo, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-332">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="98f3b-333">En el cuadro **extremo de mensajería** , escriba la dirección URL que se `api/messages`ha obtenido anteriormente y, a continuación,.</span><span class="sxs-lookup"><span data-stu-id="98f3b-333">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="98f3b-334">Este es un ejemplo: `https://botteamsauth.azurewebsites.net/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-334">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="98f3b-335">Seleccione el botón **Guardar** en la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="98f3b-335">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="98f3b-336">Probar el bot con el emulador</span><span class="sxs-lookup"><span data-stu-id="98f3b-336">Test the bot using the Emulator</span></span>

<span data-ttu-id="98f3b-337">Si aún no lo ha hecho, instale el [emulador de Microsoft bot Framework](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="98f3b-337">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="98f3b-338">Vea también [depurar con el emulador](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="98f3b-338">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="98f3b-339">Para que el inicio de sesión de ejemplo de bot funcione, debe configurar el emulador como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-339">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="98f3b-340">Configurar el emulador para la autenticación</span><span class="sxs-lookup"><span data-stu-id="98f3b-340">Configure the Emulator for authentication</span></span>

<span data-ttu-id="98f3b-341">Si un bot requiere autenticación, debe configurar el emulador tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-341">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="98f3b-342">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="98f3b-342">Start the Emulator.</span></span>
1. <span data-ttu-id="98f3b-343">En el emulador, seleccione el icono de engranaje &#9881; en la parte inferior izquierda o la pestaña **configuración del emulador** en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="98f3b-343">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="98f3b-344">Active la casilla para **usar los tokens de autenticación de la versión 1,0**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-344">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="98f3b-345">Escriba la ruta de acceso local a la herramienta **ngrok** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-345">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="98f3b-346">*Consulte* el [wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))del emulador/ngrok de la integración de túneles de bot Framework.</span><span class="sxs-lookup"><span data-stu-id="98f3b-346">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="98f3b-347">Para obtener más información sobre herramientas, consulte [ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="98f3b-347">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="98f3b-348">Para activar la casilla, **ejecute ngrok cuando se inicie el emulador**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-348">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="98f3b-349">Seleccione el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-349">Select the **Save** button.</span></span>

<span data-ttu-id="98f3b-350">Cuando el bot muestra una tarjeta de inicio de sesión y el usuario selecciona el botón de inicio de sesión, el emulador abre una página que el usuario puede usar para iniciar sesión con el proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-350">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="98f3b-351">Una vez que el usuario lo hace, el proveedor genera un token de usuario y lo envía al bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-351">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="98f3b-352">Después de eso, el bot puede actuar en nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="98f3b-352">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="98f3b-353">Probar el bot localmente</span><span class="sxs-lookup"><span data-stu-id="98f3b-353">Test the bot locally</span></span>

<span data-ttu-id="98f3b-354">Una vez que haya configurado el mecanismo de autenticación, puede realizar las pruebas de bot reales.</span><span class="sxs-lookup"><span data-stu-id="98f3b-354">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="98f3b-355">Ejecute el ejemplo de bot de forma local en el equipo, a través de Visual Studio, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-355">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="98f3b-356">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="98f3b-356">Start the Emulator.</span></span>
1. <span data-ttu-id="98f3b-357">Seleccione el botón **abrir bot** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-357">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="98f3b-358">En la **dirección URL del bot**, escriba la dirección URL local del bot? n.</span><span class="sxs-lookup"><span data-stu-id="98f3b-358">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="98f3b-359">Normalmente, `http://localhost:3978/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-359">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="98f3b-360">En el **identificador de aplicación de Microsoft** , escriba el identificador de `appsettings.json`aplicación del bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-360">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="98f3b-361">En la **contraseña de aplicación de Microsoft** , escriba la contraseña de aplicación `appsettings.json`del bot desde el.</span><span class="sxs-lookup"><span data-stu-id="98f3b-361">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="98f3b-362">Seleccione **conectar**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-362">Select **Connect**.</span></span>
1. <span data-ttu-id="98f3b-363">Una vez que el bot esté funcionando, escriba el texto para mostrar la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-363">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="98f3b-364">Seleccione el botón **iniciar sesión** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-364">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="98f3b-365">Se muestra un cuadro de diálogo emergente para **confirmar la dirección URL abierta**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-365">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="98f3b-366">Esto permite que el usuario del bot (usted) se autentique.</span><span class="sxs-lookup"><span data-stu-id="98f3b-366">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="98f3b-367">Seleccione **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-367">Select **Confirm**.</span></span>
1. <span data-ttu-id="98f3b-368">Si se le solicita, seleccione la cuenta de usuario correspondiente.</span><span class="sxs-lookup"><span data-stu-id="98f3b-368">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="98f3b-369">En función de la configuración que haya usado para el emulador, puede obtener una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="98f3b-369">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="98f3b-370">**Usar el código de comprobación de inicio de sesión**</span><span class="sxs-lookup"><span data-stu-id="98f3b-370">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="98f3b-371">&#x2713; se abre una ventana en la que se muestra el código de validación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-371">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="98f3b-372">&#x2713; copiar y escriba el código de validación en el cuadro chat para completar el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-372">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="98f3b-373">**Uso de tokens de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-373">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="98f3b-374">&#x2713; ha iniciado sesión en función de sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="98f3b-374">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="98f3b-375">La siguiente imagen es un ejemplo de la interfaz de usuario de bot una vez que ha iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="98f3b-375">The following image is an example of the bot UI after you've logged in:</span></span>

    ![emulador de inicio de sesión de bot auth](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="98f3b-377">Si selecciona **sí** cuando el robot le pregunta si desea *ver el token?*, obtendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="98f3b-377">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![token del emulador de inicio de sesión del robot de auth](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="98f3b-379">Escriba **Logout** en el cuadro chat de entrada para cerrar la sesión. Esto libera el token de usuario y el bot no podrá actuar en su nombre hasta que vuelva a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-379">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="98f3b-380">La autenticación de bot requiere el uso del **servicio de conector de bot**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-380">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="98f3b-381">El servicio tiene acceso a la información de registro de los canales de bot para el bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-381">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="98f3b-382">Probar el bot implementado</span><span class="sxs-lookup"><span data-stu-id="98f3b-382">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="98f3b-383">En el explorador, vaya a [**Azure portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="98f3b-383">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="98f3b-384">Busque su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-384">Find your resource group.</span></span>
1. <span data-ttu-id="98f3b-385">Seleccione el vínculo de recursos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-385">Select the resource link.</span></span> <span data-ttu-id="98f3b-386">Se muestra la página recurso.</span><span class="sxs-lookup"><span data-stu-id="98f3b-386">The resource page is displayed.</span></span>
1. <span data-ttu-id="98f3b-387">En la página recurso, seleccione **probar en chat web**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-387">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="98f3b-388">El bot se inicia y muestra los saludos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="98f3b-388">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="98f3b-389">Escriba cualquier cosa en el cuadro chat.</span><span class="sxs-lookup"><span data-stu-id="98f3b-389">Type anything in the chat box.</span></span>
1. <span data-ttu-id="98f3b-390">Seleccione el cuadro **iniciar sesión** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-390">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="98f3b-391">Se muestra un cuadro de diálogo emergente para **confirmar la dirección URL abierta**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-391">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="98f3b-392">Esto permite que el usuario del bot (usted) se autentique.</span><span class="sxs-lookup"><span data-stu-id="98f3b-392">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="98f3b-393">Seleccione **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-393">Select **Confirm**.</span></span>
1. <span data-ttu-id="98f3b-394">Si se le solicita, seleccione la cuenta de usuario correspondiente.</span><span class="sxs-lookup"><span data-stu-id="98f3b-394">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="98f3b-395">La siguiente imagen es un ejemplo de la interfaz de usuario de bot una vez que ha iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="98f3b-395">The following image is an example of the bot UI after you have logged in:</span></span>

    ![Inicio de sesión de robot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="98f3b-397">.</span><span class="sxs-lookup"><span data-stu-id="98f3b-397">.</span></span>

1. <span data-ttu-id="98f3b-398">Seleccione el botón **sí** para mostrar el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-398">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="98f3b-399">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-399">The following image is an example:</span></span>

    ![token de inicio de sesión de robot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="98f3b-401">.</span><span class="sxs-lookup"><span data-stu-id="98f3b-401">.</span></span>

1. <span data-ttu-id="98f3b-402">Escriba Logout para cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-402">Enter logout to sign out.</span></span>

    ![cierre de sesión de auth bot](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="98f3b-404">Si tiene problemas para iniciar sesión, intente probar la conexión de nuevo tal como se describe en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="98f3b-404">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="98f3b-405">Esto podría volver a crear el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-405">This could recreate the authentication token.</span></span>
> <span data-ttu-id="98f3b-406">Con el cliente de chat Web de bot Framework en Azure, es posible que deba iniciar sesión varias veces antes de que la autenticación se establezca correctamente.</span><span class="sxs-lookup"><span data-stu-id="98f3b-406">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="98f3b-407">Instalar y probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="98f3b-407">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="98f3b-408">En el proyecto de bot, asegúrese de `TeamsAppManifest` que la carpeta `manifest.json` contiene el junto `outline.png` con `color.png` los archivos y.</span><span class="sxs-lookup"><span data-stu-id="98f3b-408">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="98f3b-409">En el explorador de soluciones, desplácese hasta la `TeamsAppManifest` carpeta.</span><span class="sxs-lookup"><span data-stu-id="98f3b-409">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="98f3b-410">Modifique `manifest.json` asignando los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="98f3b-410">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="98f3b-411">Asegúrese de que el identificador de la **aplicación de bot** que ha recibido en el momento del registro del `id` canal `botId`de bot esté asignado a y.</span><span class="sxs-lookup"><span data-stu-id="98f3b-411">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="98f3b-412">Asigne este valor: `validDomains: [ "token.botframework.com" ]`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-412">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="98f3b-413">Seleccione y **zip** los `manifest.json`archivos `outline.png`, y `color.png` .</span><span class="sxs-lookup"><span data-stu-id="98f3b-413">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="98f3b-414">Abra **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-414">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="98f3b-415">En el panel izquierdo, en la parte inferior, seleccione el **icono aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-415">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="98f3b-416">En el panel derecho, en la parte inferior, seleccione **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-416">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="98f3b-417">Desplácese a `TeamsAppManifest` la carpeta y cargue el manifiesto comprimido.</span><span class="sxs-lookup"><span data-stu-id="98f3b-417">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="98f3b-418">Se muestra el siguiente asistente:</span><span class="sxs-lookup"><span data-stu-id="98f3b-418">The following wizard is displayed:</span></span>

    ![cargar equipos de robot de autenticación](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="98f3b-420">Seleccione el botón **Agregar a un equipo** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-420">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="98f3b-421">En la siguiente ventana, seleccione el equipo en el que desea usar el bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-421">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="98f3b-422">Seleccione el botón **configurar un bot** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-422">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="98f3b-423">Seleccione los puntos suspensivos (&#x25cf;&#x25cf;&#x25cf;) en el panel de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="98f3b-423">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="98f3b-424">A continuación, selecciona el icono de **App Studio** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-424">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="98f3b-425">Seleccione la pestaña **Editor de manifiestos** . Debe ver el icono del bot que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="98f3b-425">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="98f3b-426">Además, debería poder ver el bot enumerado como un contacto en la lista de chats que puede usar para intercambiar mensajes con el bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-426">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="98f3b-427">Probar el bot localmente en Teams</span><span class="sxs-lookup"><span data-stu-id="98f3b-427">Testing the bot locally in Teams</span></span>

<span data-ttu-id="98f3b-428">Microsoft Teams es un producto basado en la nube completamente, por lo que todos los servicios a los que tiene acceso se encuentran disponibles desde la nube con puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="98f3b-428">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="98f3b-429">Por lo tanto, para habilitar el bot (nuestro ejemplo) para trabajar en Microsoft Teams, debe publicar el código en la nube que prefiera, o bien hacer que una instancia de ejecución local sea accesible externamente mediante una herramienta de **túnel** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-429">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="98f3b-430">Se recomienda [ngrok](https://ngrok.com/download), que crea una dirección URL externamente direccionable para un puerto que se abre de forma local en el equipo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-430">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="98f3b-431">Para configurar ngrok en preparación para la ejecución local de la aplicación de Microsoft Teams, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98f3b-431">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="98f3b-432">En una ventana de terminal, vaya al directorio en el `ngrok.exe` que ha instalado.</span><span class="sxs-lookup"><span data-stu-id="98f3b-432">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="98f3b-433">Se recomienda establecer la ruta de la *variable de entorno* para que apunte a ella.</span><span class="sxs-lookup"><span data-stu-id="98f3b-433">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="98f3b-434">Ejecutar, por ejemplo, `ngrok http 3978 --host-header=localhost:3978`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-434">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="98f3b-435">Reemplace el número de Puerto según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="98f3b-435">Replace the port number as needed.</span></span>
<span data-ttu-id="98f3b-436">Se inicia ngrok para escuchar en el puerto especificado.</span><span class="sxs-lookup"><span data-stu-id="98f3b-436">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="98f3b-437">A cambio, le proporciona una dirección URL que se puede direccionar externamente, válida durante el tiempo que se ejecute ngrok.</span><span class="sxs-lookup"><span data-stu-id="98f3b-437">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="98f3b-438">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-438">The following image is an example:</span></span>

    ![la cadena de conexión de autenticación de la aplicación bots de Microsoft Teams Adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="98f3b-440">.</span><span class="sxs-lookup"><span data-stu-id="98f3b-440">.</span></span>

1. <span data-ttu-id="98f3b-441">Copie la dirección HTTPS de reenvío.</span><span class="sxs-lookup"><span data-stu-id="98f3b-441">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="98f3b-442">Debe ser similar a la siguiente: `https://dea822bf.ngrok.io/`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-442">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="98f3b-443">Anexe `/api/messages` para obtener `https://dea822bf.ngrok.io/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="98f3b-443">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="98f3b-444">Este es el **punto de conexión de mensajes** para que el bot se ejecute localmente en el equipo y sea accesible a través de la web en un chat en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="98f3b-444">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="98f3b-445">Un último paso para realizar es actualizar el punto de conexión de mensajes del componente implementado.</span><span class="sxs-lookup"><span data-stu-id="98f3b-445">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="98f3b-446">En el ejemplo, implementamos el bot en Azure.</span><span class="sxs-lookup"><span data-stu-id="98f3b-446">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="98f3b-447">Por lo tanto, \* \* vamos a realizar estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98f3b-447">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="98f3b-448">En el explorador, navegue a [**Azure portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="98f3b-448">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="98f3b-449">Seleccione el **registro del canal del bot**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-449">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="98f3b-450">En el panel izquierdo, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-450">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="98f3b-451">En el panel derecho, en el cuadro **extremo de mensajería** , escriba la dirección URL de ngrok, en `https://dea822bf.ngrok.io/api/messages`nuestro ejemplo.</span><span class="sxs-lookup"><span data-stu-id="98f3b-451">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="98f3b-452">Inicie el bot de forma local, por ejemplo, en el modo de depuración de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98f3b-452">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="98f3b-453">Pruebe el bot mientras se ejecuta de forma local mediante el **chat web**del portal de bot Framework.</span><span class="sxs-lookup"><span data-stu-id="98f3b-453">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="98f3b-454">Al igual que en el emulador, esta prueba no permite el acceso a funciones específicas de Teams.</span><span class="sxs-lookup"><span data-stu-id="98f3b-454">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="98f3b-455">En la ventana de terminal `ngrok` donde se está ejecutando, puede ver el tráfico HTTP entre el bot y el cliente de chat Web.</span><span class="sxs-lookup"><span data-stu-id="98f3b-455">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="98f3b-456">Si desea una vista más detallada, en una ventana del explorador, `http://127.0.0.1:4040` escriba lo que obtuvo en la ventana de terminal anterior.</span><span class="sxs-lookup"><span data-stu-id="98f3b-456">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="98f3b-457">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98f3b-457">The following image is an example:</span></span>

    ![autenticación Team bot ngrok pruebas](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="98f3b-459">.</span><span class="sxs-lookup"><span data-stu-id="98f3b-459">.</span></span>

> [!NOTE]
> <span data-ttu-id="98f3b-460">Si detiene y reinicia ngrok, la dirección URL cambia.</span><span class="sxs-lookup"><span data-stu-id="98f3b-460">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="98f3b-461">Para usar ngrok en su proyecto, y según las capacidades que use, debe actualizar todas las referencias a direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="98f3b-461">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>

## <a name="additional-information"></a><span data-ttu-id="98f3b-462">Información adicional</span><span class="sxs-lookup"><span data-stu-id="98f3b-462">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="98f3b-463">TeamsAppManifest/manifest. JSON</span><span class="sxs-lookup"><span data-stu-id="98f3b-463">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="98f3b-464">Este manifiesto contiene la información que Microsoft Teams necesita para conectarse con el bot.</span><span class="sxs-lookup"><span data-stu-id="98f3b-464">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

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

<span data-ttu-id="98f3b-465">Con la autenticación, Teams se comporta de forma ligeramente distinta a otros canales, tal como se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="98f3b-465">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="98f3b-466">Controlar la actividad de invocación</span><span class="sxs-lookup"><span data-stu-id="98f3b-466">Handling Invoke Activity</span></span>

<span data-ttu-id="98f3b-467">Se envía una **actividad Invoke** al bot en lugar de a la actividad de evento usada por otros canales.</span><span class="sxs-lookup"><span data-stu-id="98f3b-467">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="98f3b-468">Esto se realiza mediante la subclase de **ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="98f3b-468">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="98f3b-469">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="98f3b-469">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="98f3b-470">**Bots/DialogBot. CS**</span><span class="sxs-lookup"><span data-stu-id="98f3b-470">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="98f3b-471">**Bots/TeamsBot. CS**</span><span class="sxs-lookup"><span data-stu-id="98f3b-471">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="98f3b-472">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa la **OAuthPrompt** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-472">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="98f3b-473">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="98f3b-473">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="98f3b-474">JavaScript</span><span class="sxs-lookup"><span data-stu-id="98f3b-474">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="98f3b-475">**bots/dialogBot. js**</span><span class="sxs-lookup"><span data-stu-id="98f3b-475">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="98f3b-476">**bots/teamsBot. js**</span><span class="sxs-lookup"><span data-stu-id="98f3b-476">**bots/teamsBot.js**</span></span>

<span data-ttu-id="98f3b-477">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa la **OAuthPrompt** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-477">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="98f3b-478">**Dialogs/mainDialog. js**</span><span class="sxs-lookup"><span data-stu-id="98f3b-478">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="98f3b-479">En un paso de diálogo, `beginDialog` use para iniciar el símbolo del sistema de OAuth, que le pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-479">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="98f3b-480">Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="98f3b-480">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="98f3b-481">De lo contrario, se le pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-481">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="98f3b-482">El servicio de bot de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-482">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="98f3b-483">En el siguiente paso de cuadro de diálogo, compruebe si existe un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="98f3b-483">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="98f3b-484">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="98f3b-484">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="98f3b-485">**bots/logoutDialog. js**</span><span class="sxs-lookup"><span data-stu-id="98f3b-485">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="98f3b-486">Python</span><span class="sxs-lookup"><span data-stu-id="98f3b-486">Python</span></span>](#tab/python-sample)

<span data-ttu-id="98f3b-487">**bots/dialog_bot. py**</span><span class="sxs-lookup"><span data-stu-id="98f3b-487">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="98f3b-488">**bots/teams_bot. py**</span><span class="sxs-lookup"><span data-stu-id="98f3b-488">**bots/teams_bot.py**</span></span>

<span data-ttu-id="98f3b-489">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa la **OAuthPrompt** .</span><span class="sxs-lookup"><span data-stu-id="98f3b-489">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="98f3b-490">**cuadros de diálogo/main_dialog. py**</span><span class="sxs-lookup"><span data-stu-id="98f3b-490">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="98f3b-491">En un paso de diálogo, `begin_dialog` use para iniciar el símbolo del sistema de OAuth, que le pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-491">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="98f3b-492">Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="98f3b-492">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="98f3b-493">De lo contrario, se le pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-493">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="98f3b-494">El servicio de bot de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="98f3b-494">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="98f3b-495">En el siguiente paso de cuadro de diálogo, compruebe si existe un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="98f3b-495">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="98f3b-496">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="98f3b-496">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="98f3b-497">**cuadros de diálogo/logout_dialog. py**</span><span class="sxs-lookup"><span data-stu-id="98f3b-497">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="98f3b-498">Obtenga información sobre cómo agregar la autenticación mediante el servicio de robots de Azure</span><span class="sxs-lookup"><span data-stu-id="98f3b-498">Learn about adding adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
