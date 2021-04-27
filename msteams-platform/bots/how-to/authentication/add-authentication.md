---
title: Agregar autenticación al bot de Teams
author: clearab
description: Cómo agregar la autenticación de OAuth a un bot en Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: d54d7fadb13626bb38de3a907b966f026cc6c485
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020953"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="99fec-103">Agregar autenticación al bot de Teams</span><span class="sxs-lookup"><span data-stu-id="99fec-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="99fec-104">Hay ocasiones en las que es posible que necesite crear bots en Microsoft Teams que puedan tener acceso a recursos en nombre del usuario, como un servicio de correo.</span><span class="sxs-lookup"><span data-stu-id="99fec-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="99fec-105">En este artículo se muestra cómo usar la autenticación del SDK de Azure Bot Service v4, basada en OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="99fec-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="99fec-106">Esto facilita el desarrollo de un bot que puede usar tokens de autenticación en función de las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="99fec-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="99fec-107">La clave en todo esto es el uso de proveedores **de identidades,** como veremos más adelante.</span><span class="sxs-lookup"><span data-stu-id="99fec-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="99fec-108">OAuth 2.0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory (Azure AD) y otros muchos proveedores de identidad.</span><span class="sxs-lookup"><span data-stu-id="99fec-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="99fec-109">Una comprensión básica de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams.</span><span class="sxs-lookup"><span data-stu-id="99fec-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="99fec-110">Consulta [OAuth 2 Simplified para](https://aka.ms/oauth2-simplified) obtener una descripción básica y [OAuth 2.0](https://oauth.net/2/) para obtener la especificación completa.</span><span class="sxs-lookup"><span data-stu-id="99fec-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="99fec-111">Para obtener más información acerca de cómo el Servicio de bots de Azure controla la autenticación, vea [Autenticación de usuario en una conversación](https://aka.ms/azure-bot-authentication).</span><span class="sxs-lookup"><span data-stu-id="99fec-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="99fec-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="99fec-112">In this article you'll learn:</span></span>

- <span data-ttu-id="99fec-113">**Cómo crear un bot habilitado para autenticación**.</span><span class="sxs-lookup"><span data-stu-id="99fec-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="99fec-114">Usará [cs-auth-sample][teams-auth-bot-cs] para controlar las credenciales de inicio de sesión del usuario y la generación del token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="99fec-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="99fec-115">**Cómo implementar el bot en Azure y asociarlo a un proveedor de identidades.**</span><span class="sxs-lookup"><span data-stu-id="99fec-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="99fec-116">El proveedor emite un token en función de las credenciales de inicio de sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="99fec-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="99fec-117">El bot puede usar el token para obtener acceso a recursos, como un servicio de correo, que requieren autenticación.</span><span class="sxs-lookup"><span data-stu-id="99fec-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="99fec-118">Para obtener más información,  [vea Flujo de autenticación de Microsoft Teams para bots](auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="99fec-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="99fec-119">**Cómo integrar el bot en Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="99fec-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="99fec-120">Una vez integrado el bot, puedes iniciar sesión e intercambiar mensajes con él en un chat.</span><span class="sxs-lookup"><span data-stu-id="99fec-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99fec-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99fec-121">Prerequisites</span></span>

- <span data-ttu-id="99fec-122">Conocimiento de [los conceptos básicos del bot,][concept-basics] [la administración del estado,][concept-state]la biblioteca de cuadros de diálogo [y][concept-dialogs]cómo implementar el flujo secuencial [de conversación][simple-dialog].</span><span class="sxs-lookup"><span data-stu-id="99fec-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="99fec-123">Conocimiento del desarrollo de Azure y OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="99fec-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="99fec-124">Las versiones actuales de Visual Studio y Git.</span><span class="sxs-lookup"><span data-stu-id="99fec-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="99fec-125">Cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="99fec-125">Azure account.</span></span> <span data-ttu-id="99fec-126">Si es necesario, puede crear una cuenta [gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="99fec-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="99fec-127">El ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="99fec-127">The following sample.</span></span>

    | <span data-ttu-id="99fec-128">Muestra</span><span class="sxs-lookup"><span data-stu-id="99fec-128">Sample</span></span> | <span data-ttu-id="99fec-129">Versión de BotBuilder</span><span class="sxs-lookup"><span data-stu-id="99fec-129">BotBuilder version</span></span> | <span data-ttu-id="99fec-130">Demostraciones</span><span class="sxs-lookup"><span data-stu-id="99fec-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="99fec-131">**Autenticación de** [bot en cs-auth-sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="99fec-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="99fec-132">v4</span><span class="sxs-lookup"><span data-stu-id="99fec-132">v4</span></span> | <span data-ttu-id="99fec-133">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="99fec-133">OAuthCard support</span></span> |
    | <span data-ttu-id="99fec-134">**Autenticación de** bot [en js-auth-sample][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="99fec-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="99fec-135">v4</span><span class="sxs-lookup"><span data-stu-id="99fec-135">v4</span></span>| <span data-ttu-id="99fec-136">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="99fec-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="99fec-137">**Autenticación de bot** [en py-auth-sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="99fec-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="99fec-138">v4</span><span class="sxs-lookup"><span data-stu-id="99fec-138">v4</span></span> | <span data-ttu-id="99fec-139">Compatibilidad con OAuthCard</span><span class="sxs-lookup"><span data-stu-id="99fec-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="99fec-140">Crear el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="99fec-140">Create the resource group</span></span>

<span data-ttu-id="99fec-141">El grupo de recursos y el plan de servicio no son estrictamente necesarios, pero permiten liberar cómodamente los recursos que cree.</span><span class="sxs-lookup"><span data-stu-id="99fec-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="99fec-142">Este es un buen procedimiento para mantener los recursos organizados y manejables.</span><span class="sxs-lookup"><span data-stu-id="99fec-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="99fec-143">Se usa un grupo de recursos para crear recursos individuales para Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="99fec-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="99fec-144">Para obtener rendimiento, asegúrese de que estos recursos se encuentran en la misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="99fec-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="99fec-145">En el explorador, inicie sesión en [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="99fec-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="99fec-146">En el panel de navegación izquierdo, seleccione **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="99fec-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="99fec-147">En la parte superior izquierda de la ventana mostrada, seleccione **La** pestaña Agregar para crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99fec-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="99fec-148">Se le pedirá que proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="99fec-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="99fec-149">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="99fec-149">**Subscription**.</span></span> <span data-ttu-id="99fec-150">Use la suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="99fec-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="99fec-151">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="99fec-151">**Resource group**.</span></span> <span data-ttu-id="99fec-152">Escriba el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99fec-152">Enter the name for the resource group.</span></span> <span data-ttu-id="99fec-153">Un ejemplo podría ser  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="99fec-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="99fec-154">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="99fec-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="99fec-155">En el **menú** desplegable Región, seleccione *Oeste de EE.* UU. o una región cercana a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="99fec-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="99fec-156">Seleccione el **botón Revisar y** crear.</span><span class="sxs-lookup"><span data-stu-id="99fec-156">Select the **Review and create** button.</span></span> <span data-ttu-id="99fec-157">Debería ver un banner que lee *Validación pasada*.</span><span class="sxs-lookup"><span data-stu-id="99fec-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="99fec-158">Seleccione el **botón** Crear.</span><span class="sxs-lookup"><span data-stu-id="99fec-158">Select the **Create** button.</span></span> <span data-ttu-id="99fec-159">Puede tardar unos minutos en crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99fec-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="99fec-160">Al igual que con los recursos que crearás más adelante en este tutorial, es buena idea anclar este grupo de recursos al panel para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="99fec-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="99fec-161">Si desea hacerlo, seleccione el icono de patilla &#128204; en la parte superior derecha del panel.</span><span class="sxs-lookup"><span data-stu-id="99fec-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="99fec-162">Crear el plan de servicio</span><span class="sxs-lookup"><span data-stu-id="99fec-162">Create the service plan</span></span>

1. <span data-ttu-id="99fec-163">En [**Azure Portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="99fec-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="99fec-164">En el cuadro de búsqueda, escriba *Plan de App Service*.</span><span class="sxs-lookup"><span data-stu-id="99fec-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="99fec-165">Seleccione la **tarjeta Plan de App Service** en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="99fec-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="99fec-166">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="99fec-166">Select **Create**.</span></span>
1. <span data-ttu-id="99fec-167">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="99fec-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="99fec-168">**Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="99fec-168">**Subscription**.</span></span> <span data-ttu-id="99fec-169">Puede usar una suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="99fec-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="99fec-170">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="99fec-170">**Resource Group**.</span></span> <span data-ttu-id="99fec-171">Seleccione el grupo que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="99fec-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="99fec-172">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="99fec-172">**Name**.</span></span> <span data-ttu-id="99fec-173">Escriba el nombre del plan de servicio.</span><span class="sxs-lookup"><span data-stu-id="99fec-173">Enter the name for the service plan.</span></span> <span data-ttu-id="99fec-174">Un ejemplo podría ser  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="99fec-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="99fec-175">Recuerde que el nombre debe ser único, dentro del grupo.</span><span class="sxs-lookup"><span data-stu-id="99fec-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="99fec-176">**Sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="99fec-176">**Operating System**.</span></span> <span data-ttu-id="99fec-177">Selecciona *Windows* o el sistema operativo aplicable.</span><span class="sxs-lookup"><span data-stu-id="99fec-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="99fec-178">**Región**.</span><span class="sxs-lookup"><span data-stu-id="99fec-178">**Region**.</span></span> <span data-ttu-id="99fec-179">Seleccione *Oeste de EE. UU.* o una región cercana a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="99fec-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="99fec-180">**Plan de precios**.</span><span class="sxs-lookup"><span data-stu-id="99fec-180">**Pricing Tier**.</span></span> <span data-ttu-id="99fec-181">Asegúrese de que *standard S1* está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="99fec-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="99fec-182">Este debe ser el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="99fec-182">This should be the default value.</span></span>
    1. <span data-ttu-id="99fec-183">Seleccione el **botón Revisar y** crear.</span><span class="sxs-lookup"><span data-stu-id="99fec-183">Select the **Review and create** button.</span></span> <span data-ttu-id="99fec-184">Debería ver un banner que lee *Validación pasada*.</span><span class="sxs-lookup"><span data-stu-id="99fec-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="99fec-185">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="99fec-185">Select **Create**.</span></span> <span data-ttu-id="99fec-186">Puede tardar unos minutos en crear el plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="99fec-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="99fec-187">El plan se enumerará en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99fec-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="99fec-188">Crear el registro de canales de bot</span><span class="sxs-lookup"><span data-stu-id="99fec-188">Create the bot channels registration</span></span>

<span data-ttu-id="99fec-189">El registro de canales de bot registra el servicio web como un bot con Bot Framework, siempre que tenga un identificador de aplicación de Microsoft y una contraseña de aplicación (secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="99fec-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99fec-190">Solo necesita registrar el bot si no está hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="99fec-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="99fec-191">Si [creó un bot a](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) través de Azure Portal, ya está registrado en el servicio.</span><span class="sxs-lookup"><span data-stu-id="99fec-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="99fec-192">Si creó el bot a través de [Bot Framework](https://dev.botframework.com/bots/new) o [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) el bot no está registrado en Azure.</span><span class="sxs-lookup"><span data-stu-id="99fec-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="99fec-193">El recurso Registro de canales bot mostrará la región **Global** incluso si seleccionó Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="99fec-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="99fec-194">Esto se espera.</span><span class="sxs-lookup"><span data-stu-id="99fec-194">This is expected.</span></span>

<span data-ttu-id="99fec-195">Para obtener más información, vea [Create a bot for Teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="99fec-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="99fec-196">Crear el proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="99fec-196">Create the identity provider</span></span>

<span data-ttu-id="99fec-197">Necesita un proveedor de identidades que se pueda usar para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="99fec-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="99fec-198">En este procedimiento, usará un proveedor de Azure AD; También se pueden usar otros proveedores de identidad compatibles con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99fec-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="99fec-199">En [**Azure Portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99fec-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="99fec-200">Deberá crear y registrar este recurso de Azure AD en un espacio empresarial en el que pueda dar su consentimiento para delegar los permisos solicitados por una aplicación.</span><span class="sxs-lookup"><span data-stu-id="99fec-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="99fec-201">Para obtener instrucciones sobre cómo crear un inquilino, vea [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span><span class="sxs-lookup"><span data-stu-id="99fec-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="99fec-202">En el panel izquierdo, seleccione **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="99fec-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="99fec-203">En el panel derecho, seleccione la **pestaña Nuevo registro,** en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="99fec-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="99fec-204">Se le pedirá que proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="99fec-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="99fec-205">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="99fec-205">**Name**.</span></span> <span data-ttu-id="99fec-206">Escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99fec-206">Enter the name for the application.</span></span> <span data-ttu-id="99fec-207">Un ejemplo podría ser  *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="99fec-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="99fec-208">Recuerde que el nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="99fec-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="99fec-209">Seleccione los **tipos de cuenta admitidos** para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99fec-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="99fec-210">Seleccione Cuentas en cualquier directorio de la organización (cualquier directorio de Azure AD - Multitenant) y cuentas personales de *Microsoft (por ejemplo, Skype, Xbox).*</span><span class="sxs-lookup"><span data-stu-id="99fec-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="99fec-211">Para el **URI de redireccionamiento**:</span><span class="sxs-lookup"><span data-stu-id="99fec-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="99fec-212">&#x2713;Seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="99fec-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="99fec-213">&#x2713; Establezca la dirección URL en `https://token.botframework.com/.auth/web/redirect` .</span><span class="sxs-lookup"><span data-stu-id="99fec-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="99fec-214">Seleccione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-214">Select **Register**.</span></span>

1. <span data-ttu-id="99fec-215">Una vez creado, Azure muestra la **página Información** general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99fec-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="99fec-216">Copie y guarde la siguiente información en un archivo:</span><span class="sxs-lookup"><span data-stu-id="99fec-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="99fec-217">Valor **de id. de aplicación (cliente).**</span><span class="sxs-lookup"><span data-stu-id="99fec-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="99fec-218">Este valor se usará más adelante como *identificador* de cliente al registrar esta aplicación de identidad de Azure con el bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="99fec-219">Valor **del id. de directorio (espacio** empresarial).</span><span class="sxs-lookup"><span data-stu-id="99fec-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="99fec-220">También usarás este valor más adelante como identificador *de* inquilino para registrar esta aplicación de identidad de Azure con el bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="99fec-221">En el panel izquierdo, seleccione **Certificados & secretos para** crear un secreto de cliente para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99fec-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="99fec-222">En **Secretos de** cliente, &#x2795; **Nuevo secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="99fec-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="99fec-223">Agrega una descripción para identificar este secreto de otras personas que podrías tener que crear para esta aplicación, como *Bot identity app en Teams*.</span><span class="sxs-lookup"><span data-stu-id="99fec-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="99fec-224">Establece **Expira en** la selección.</span><span class="sxs-lookup"><span data-stu-id="99fec-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="99fec-225">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-225">Select **Add**.</span></span>
   1. <span data-ttu-id="99fec-226">Antes de salir de esta página, **registre el secreto**.</span><span class="sxs-lookup"><span data-stu-id="99fec-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="99fec-227">Este valor se usará más adelante como _secreto_ de cliente al registrar la aplicación de Azure AD con el bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="99fec-228">Configurar la conexión del proveedor de identidades y registrarla con el bot</span><span class="sxs-lookup"><span data-stu-id="99fec-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="99fec-229">Nota: hay dos opciones para los proveedores de servicios aquí:Azure AD V1 y Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="99fec-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="99fec-230">Las diferencias entre los dos proveedores se resumen [aquí,](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)pero, en general, V2 proporciona más flexibilidad con respecto a cambiar los permisos del bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="99fec-231">Los permisos de la API de Graph se enumeran en el campo ámbitos y, a medida que se agregan nuevos, los bots permitirán a los usuarios dar su consentimiento a los nuevos permisos en el siguiente inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="99fec-232">Para V1, el usuario debe eliminar el consentimiento del bot para que se pidan nuevos permisos en el cuadro de diálogo OAuth.</span><span class="sxs-lookup"><span data-stu-id="99fec-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="99fec-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="99fec-233">Azure AD V1</span></span>

1. <span data-ttu-id="99fec-234">En [**Azure Portal,**][azure-portal]seleccione el grupo de recursos en el panel.</span><span class="sxs-lookup"><span data-stu-id="99fec-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="99fec-235">Seleccione el vínculo de registro del canal de bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="99fec-236">En la página de recursos, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="99fec-236">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="99fec-237">En **Configuración de conexión de OAuth** cerca de la parte inferior de la página, seleccione Agregar **configuración**.</span><span class="sxs-lookup"><span data-stu-id="99fec-237">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="99fec-238">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="99fec-238">Complete the form as follows:</span></span>

    1. <span data-ttu-id="99fec-239">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="99fec-239">**Name**.</span></span> <span data-ttu-id="99fec-240">Escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="99fec-240">Enter a name for the connection.</span></span> <span data-ttu-id="99fec-241">Usarás este nombre en el bot en el `appsettings.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="99fec-241">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="99fec-242">Por ejemplo *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="99fec-242">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="99fec-243">**Proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="99fec-243">**Service Provider**.</span></span> <span data-ttu-id="99fec-244">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99fec-244">Select **Azure Active Directory**.</span></span> <span data-ttu-id="99fec-245">Una vez seleccionado, se mostrarán los campos específicos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99fec-245">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="99fec-246">**Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="99fec-246">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="99fec-247">**Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="99fec-247">**Client secret**.</span></span> <span data-ttu-id="99fec-248">Escriba el secreto que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="99fec-248">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="99fec-249">**Tipo de concesión**.</span><span class="sxs-lookup"><span data-stu-id="99fec-249">**Grant Type**.</span></span> <span data-ttu-id="99fec-250">Escriba `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="99fec-250">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="99fec-251">**Dirección URL de inicio de** sesión .</span><span class="sxs-lookup"><span data-stu-id="99fec-251">**Login URL**.</span></span> <span data-ttu-id="99fec-252">Escriba `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="99fec-252">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="99fec-253">**Identificador de inquilino**, escriba el id. de directorio  **(espacio empresarial)** que registró anteriormente para la aplicación de identidad de Azure o común según el tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="99fec-253">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="99fec-254">Para decidir qué valor asignar, siga estos criterios:</span><span class="sxs-lookup"><span data-stu-id="99fec-254">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="99fec-255">Si seleccionó Cuentas solo en este directorio de la organización *(Solo Microsoft -* Inquilino único) o  Cuentas en cualquier directorio de la organización *(directorio de Microsoft AAD - Inquilino múltiple)* escriba el identificador de inquilino que registró anteriormente para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="99fec-255">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="99fec-256">Este será el espacio empresarial asociado con los usuarios que se pueden autenticar.</span><span class="sxs-lookup"><span data-stu-id="99fec-256">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="99fec-257">Si seleccionó Cuentas en cualquier directorio de la organización (cualquier directorio de AAD: cuentas de Microsoft multiinquilino y personales, por *ejemplo, Skype, Xbox y Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="99fec-257">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="99fec-258">De lo contrario, la aplicación de AAD comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="99fec-258">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="99fec-259">h.</span><span class="sxs-lookup"><span data-stu-id="99fec-259">h.</span></span> <span data-ttu-id="99fec-260">En **Dirección URL de** recurso , escriba `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="99fec-260">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="99fec-261">Esto no se usa en el ejemplo de código actual.</span><span class="sxs-lookup"><span data-stu-id="99fec-261">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="99fec-262">i.</span><span class="sxs-lookup"><span data-stu-id="99fec-262">i.</span></span> <span data-ttu-id="99fec-263">Deje **ámbitos en** blanco.</span><span class="sxs-lookup"><span data-stu-id="99fec-263">Leave **Scopes** blank.</span></span> <span data-ttu-id="99fec-264">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99fec-264">The following image is an example:</span></span>

    ![vista de cadena de conexión de la aplicación de bots de teams adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="99fec-266">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-266">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="99fec-267">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="99fec-267">Azure AD V2</span></span>

1. <span data-ttu-id="99fec-268">En [**Azure Portal,**][azure-portal]seleccione el grupo de recursos en el panel.</span><span class="sxs-lookup"><span data-stu-id="99fec-268">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="99fec-269">Seleccione el vínculo de registro del canal de bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-269">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="99fec-270">En la página de recursos, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="99fec-270">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="99fec-271">En **Configuración de conexión de OAuth** cerca de la parte inferior de la página, seleccione Agregar **configuración**.</span><span class="sxs-lookup"><span data-stu-id="99fec-271">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="99fec-272">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="99fec-272">Complete the form as follows:</span></span>

    1. <span data-ttu-id="99fec-273">**Nombre**.</span><span class="sxs-lookup"><span data-stu-id="99fec-273">**Name**.</span></span> <span data-ttu-id="99fec-274">Escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="99fec-274">Enter a name for the connection.</span></span> <span data-ttu-id="99fec-275">Usarás este nombre en el bot en el `appsettings.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="99fec-275">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="99fec-276">Por ejemplo *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="99fec-276">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="99fec-277">**Proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="99fec-277">**Service Provider**.</span></span> <span data-ttu-id="99fec-278">Seleccione **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="99fec-278">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="99fec-279">Una vez seleccionado, se mostrarán los campos específicos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99fec-279">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="99fec-280">**Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="99fec-280">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="99fec-281">**Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="99fec-281">**Client secret**.</span></span> <span data-ttu-id="99fec-282">Escriba el secreto que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="99fec-282">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="99fec-283">**Dirección URL de Exchange de token**.</span><span class="sxs-lookup"><span data-stu-id="99fec-283">**Token Exchange URL**.</span></span> <span data-ttu-id="99fec-284">Deje esto en blanco.</span><span class="sxs-lookup"><span data-stu-id="99fec-284">Leave this blank.</span></span>
    1. <span data-ttu-id="99fec-285">**Identificador de inquilino**, escriba el id. de directorio  **(espacio empresarial)** que registró anteriormente para la aplicación de identidad de Azure o común según el tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="99fec-285">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="99fec-286">Para decidir qué valor asignar, siga estos criterios:</span><span class="sxs-lookup"><span data-stu-id="99fec-286">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="99fec-287">Si seleccionó Cuentas solo en este directorio de la organización *(Solo Microsoft -* Inquilino único) o  Cuentas en cualquier directorio de la organización *(directorio de Microsoft AAD - Inquilino múltiple)* escriba el identificador de inquilino que registró anteriormente para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="99fec-287">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="99fec-288">Este será el espacio empresarial asociado con los usuarios que se pueden autenticar.</span><span class="sxs-lookup"><span data-stu-id="99fec-288">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="99fec-289">Si seleccionó Cuentas en cualquier directorio de la organización (cualquier directorio de AAD: cuentas de Microsoft multiinquilino y personales, por *ejemplo, Skype, Xbox y Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="99fec-289">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="99fec-290">De lo contrario, la aplicación de AAD comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="99fec-290">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="99fec-291">Para **Ámbitos,** escriba una lista delimitada por espacios de permisos de gráfico que esta aplicación requiere, por ejemplo: User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="99fec-291">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="99fec-292">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-292">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="99fec-293">Probar la conexión</span><span class="sxs-lookup"><span data-stu-id="99fec-293">Test the connection</span></span>

1. <span data-ttu-id="99fec-294">Seleccione la entrada de conexión para abrir la conexión que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="99fec-294">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="99fec-295">Seleccione **Probar conexión en** la parte superior del panel Configuración de conexión del proveedor **de** servicios.</span><span class="sxs-lookup"><span data-stu-id="99fec-295">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="99fec-296">La primera vez que lo hagas, se abrirá una nueva ventana del explorador que te pedirá que selecciones una cuenta.</span><span class="sxs-lookup"><span data-stu-id="99fec-296">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="99fec-297">Seleccione la que desea usar.</span><span class="sxs-lookup"><span data-stu-id="99fec-297">Select the one you want to use.</span></span>
1. <span data-ttu-id="99fec-298">A continuación, se le pedirá que permita al proveedor de identidades usar sus datos (credenciales).</span><span class="sxs-lookup"><span data-stu-id="99fec-298">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="99fec-299">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99fec-299">The following image is an example:</span></span>

    ![cadena de conexión de autenticación de bots de teams adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="99fec-301">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-301">Select **Accept**.</span></span>
1. <span data-ttu-id="99fec-302">A continuación, debería redirigirle a una **página Conexión de prueba a \<your-connection-name> Correcta.**</span><span class="sxs-lookup"><span data-stu-id="99fec-302">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="99fec-303">Actualice la página si recibe un error.</span><span class="sxs-lookup"><span data-stu-id="99fec-303">Refresh the page if you get an error.</span></span> <span data-ttu-id="99fec-304">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99fec-304">The following image is an example:</span></span>

  ![teams bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="99fec-306">El código de bot usa el nombre de conexión para recuperar tokens de autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="99fec-306">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="99fec-307">Preparar el código de ejemplo del bot</span><span class="sxs-lookup"><span data-stu-id="99fec-307">Prepare the bot sample code</span></span>

<span data-ttu-id="99fec-308">Una vez realizada la configuración preliminar, vamos a centrarnos en la creación del bot que se va a usar en este artículo.</span><span class="sxs-lookup"><span data-stu-id="99fec-308">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="99fec-309">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="99fec-309">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="99fec-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="99fec-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="99fec-311">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99fec-311">Launch Visual Studio.</span></span>
1. <span data-ttu-id="99fec-312">En la barra de herramientas, **seleccione Archivo -> Abrir -> Project/Solution** y abra el proyecto de bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-312">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="99fec-313">En C# actualizar **appsettings.jsde la** siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="99fec-313">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="99fec-314">Establezca `ConnectionName` el nombre de la conexión del proveedor de identidades que agregó al registro del canal de bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-314">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="99fec-315">El nombre que se usa en este ejemplo es *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="99fec-315">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="99fec-316">Se `MicrosoftAppId` establece en el identificador de aplicación del **bot** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-316">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="99fec-317">Se `MicrosoftAppPassword` establece en el secreto de **cliente** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-317">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="99fec-318">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML.</span><span class="sxs-lookup"><span data-stu-id="99fec-318">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="99fec-319">Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="99fec-319">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="99fec-320">En el Explorador de soluciones, vaya a la carpeta, abra y establezca y al identificador de aplicación del bot que guardó en el momento del registro `TeamsAppManifest` `manifest.json` del canal del `id` `botId` bot. </span><span class="sxs-lookup"><span data-stu-id="99fec-320">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="99fec-321">JavaScript</span><span class="sxs-lookup"><span data-stu-id="99fec-321">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="99fec-322">Clone [node-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="99fec-322">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="99fec-323">En una consola, vaya al proyecto:</span><span class="sxs-lookup"><span data-stu-id="99fec-323">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="99fec-324">Instalar módulos</span><span class="sxs-lookup"><span data-stu-id="99fec-324">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="99fec-325">Actualice la **configuración .env** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="99fec-325">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="99fec-326">Se `MicrosoftAppId` establece en el identificador de aplicación del **bot** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-326">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="99fec-327">Se `MicrosoftAppPassword` establece en el secreto de **cliente** que guardó en el momento del registro del canal del bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-327">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="99fec-328">Establezca el `connectionName` valor en el nombre de la conexión del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="99fec-328">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="99fec-329">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML.</span><span class="sxs-lookup"><span data-stu-id="99fec-329">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="99fec-330">Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="99fec-330">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="99fec-331">En la carpeta, abra y establezca el id. de la aplicación de Microsoft y el id. de la aplicación bot que guardó en el momento del registro `teamsAppManifest` `manifest.json` del canal del `id`  `botId` bot. </span><span class="sxs-lookup"><span data-stu-id="99fec-331">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="99fec-332">Python</span><span class="sxs-lookup"><span data-stu-id="99fec-332">Python</span></span>](#tab/python)

1. <span data-ttu-id="99fec-333">Clone [py-auth-sample][teams-auth-bot-py] desde el repositorio de github.</span><span class="sxs-lookup"><span data-stu-id="99fec-333">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="99fec-334">Actualizar **config.py**:</span><span class="sxs-lookup"><span data-stu-id="99fec-334">Update **config.py**:</span></span>

    - <span data-ttu-id="99fec-335">Establezca el nombre de la configuración de conexión `ConnectionName` de OAuth que agregó al bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-335">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="99fec-336">Set `MicrosoftAppId` and to your `MicrosoftAppPassword` bot's app ID and app secret.</span><span class="sxs-lookup"><span data-stu-id="99fec-336">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="99fec-337">Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML.</span><span class="sxs-lookup"><span data-stu-id="99fec-337">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="99fec-338">Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="99fec-338">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="99fec-339">Implementar el bot en Azure</span><span class="sxs-lookup"><span data-stu-id="99fec-339">Deploy the bot to Azure</span></span>

<span data-ttu-id="99fec-340">Para implementar el bot, siga los pasos descritos en el procedimiento para [implementar el bot en Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="99fec-340">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="99fec-341">Como alternativa, mientras esté Visual Studio, puede seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="99fec-341">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="99fec-342">En Visual Studio *Explorador de soluciones,* seleccione y mantenga presionado (o haga clic con el botón secundario) en el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="99fec-342">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="99fec-343">En el menú desplegable, seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-343">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="99fec-344">En la ventana mostrada, seleccione el **vínculo** Nuevo.</span><span class="sxs-lookup"><span data-stu-id="99fec-344">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="99fec-345">En la ventana de diálogo, seleccione **App Service** a la izquierda y **Crear nuevo** a la derecha.</span><span class="sxs-lookup"><span data-stu-id="99fec-345">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="99fec-346">Seleccione el **botón** Publicar.</span><span class="sxs-lookup"><span data-stu-id="99fec-346">Select the **Publish** button.</span></span>
1. <span data-ttu-id="99fec-347">En la siguiente ventana de diálogo, escriba la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="99fec-347">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="99fec-348">A continuación puede ver un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99fec-348">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="99fec-350">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="99fec-350">Select **Create**.</span></span>
1. <span data-ttu-id="99fec-351">Si la implementación se completa correctamente, debería verlo reflejado en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99fec-351">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="99fec-352">Además, se muestra una página en el explorador predeterminado que dice *Que el bot está listo.*</span><span class="sxs-lookup"><span data-stu-id="99fec-352">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="99fec-353">La dirección URL será similar a esta: `https://botteamsauth.azurewebsites.net/` .</span><span class="sxs-lookup"><span data-stu-id="99fec-353">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="99fec-354">Guárdelo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="99fec-354">Save it to a file.</span></span>
1. <span data-ttu-id="99fec-355">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="99fec-355">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="99fec-356">Compruebe el grupo de recursos, el bot debe aparecer junto con los demás recursos.</span><span class="sxs-lookup"><span data-stu-id="99fec-356">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="99fec-357">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99fec-357">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="99fec-359">En el grupo de recursos, seleccione el nombre de registro del canal bot (vínculo).</span><span class="sxs-lookup"><span data-stu-id="99fec-359">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="99fec-360">En el panel izquierdo, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="99fec-360">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="99fec-361">En el **cuadro Punto de conexión** de mensajería, escriba la dirección URL obtenida anteriormente seguida de `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="99fec-361">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="99fec-362">Este es un ejemplo: `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="99fec-362">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="99fec-363">Seleccione el **botón** Guardar en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="99fec-363">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="99fec-364">Probar el bot con el emulador</span><span class="sxs-lookup"><span data-stu-id="99fec-364">Test the bot using the Emulator</span></span>

<span data-ttu-id="99fec-365">Si aún no lo ha hecho, instale el emulador [de Microsoft Bot Framework](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="99fec-365">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="99fec-366">Vea también [Depurar con el emulador](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="99fec-366">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="99fec-367">Para que el inicio de sesión de ejemplo del bot funcione, debe configurar el emulador como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="99fec-367">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="99fec-368">Configurar el emulador para la autenticación</span><span class="sxs-lookup"><span data-stu-id="99fec-368">Configure the Emulator for authentication</span></span>

<span data-ttu-id="99fec-369">Si un bot requiere autenticación, debe configurar el emulador como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="99fec-369">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="99fec-370">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="99fec-370">Start the Emulator.</span></span>
1. <span data-ttu-id="99fec-371">En el emulador, selecciona el icono de engranaje &#9881; en la parte inferior izquierda o la pestaña Configuración del **emulador** en la parte superior derecha.</span><span class="sxs-lookup"><span data-stu-id="99fec-371">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="99fec-372">Active la casilla **usar tokens de autenticación de la versión 1.0**.</span><span class="sxs-lookup"><span data-stu-id="99fec-372">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="99fec-373">Escriba la ruta de acceso local a la **herramienta ngrok.**</span><span class="sxs-lookup"><span data-stu-id="99fec-373">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="99fec-374">*Consulta* el Wiki de integración de túneles de Bot Framework [Emulator](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))/ngrok .</span><span class="sxs-lookup"><span data-stu-id="99fec-374">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="99fec-375">Para obtener más información sobre la herramienta, [vea ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="99fec-375">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="99fec-376">Active la casilla **Ejecutar ngrok cuando se inicie el emulador**.</span><span class="sxs-lookup"><span data-stu-id="99fec-376">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="99fec-377">Seleccione el **botón** Guardar.</span><span class="sxs-lookup"><span data-stu-id="99fec-377">Select the **Save** button.</span></span>

<span data-ttu-id="99fec-378">Cuando el bot muestra una tarjeta de inicio de sesión y el usuario selecciona el botón de inicio de sesión, el emulador abre una página que el usuario puede usar para iniciar sesión con el proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="99fec-378">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="99fec-379">Una vez que el usuario lo hace, el proveedor genera un token de usuario y lo envía al bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-379">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="99fec-380">Después, el bot puede actuar en nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="99fec-380">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="99fec-381">Probar el bot localmente</span><span class="sxs-lookup"><span data-stu-id="99fec-381">Test the bot locally</span></span>

<span data-ttu-id="99fec-382">Después de configurar el mecanismo de autenticación, puede realizar las pruebas de bot reales.</span><span class="sxs-lookup"><span data-stu-id="99fec-382">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="99fec-383">Ejecute el ejemplo de bot localmente en el equipo, a través Visual Studio por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="99fec-383">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="99fec-384">Inicie el emulador.</span><span class="sxs-lookup"><span data-stu-id="99fec-384">Start the Emulator.</span></span>
1. <span data-ttu-id="99fec-385">Seleccione el **botón Abrir bot.**</span><span class="sxs-lookup"><span data-stu-id="99fec-385">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="99fec-386">En la **dirección URL del bot,** escriba la dirección URL local del bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-386">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="99fec-387">Normalmente, `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="99fec-387">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="99fec-388">En el **Id. de aplicación de Microsoft,** escriba el identificador de aplicación del bot desde `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="99fec-388">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="99fec-389">En la **contraseña de Microsoft App,** escriba la contraseña de la aplicación del bot desde `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="99fec-389">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="99fec-390">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-390">Select **Connect**.</span></span>
1. <span data-ttu-id="99fec-391">Después de que el bot esté en funcionamiento, escriba cualquier texto para mostrar la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-391">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="99fec-392">Seleccione el **botón Iniciar sesión.**</span><span class="sxs-lookup"><span data-stu-id="99fec-392">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="99fec-393">Se muestra un cuadro de diálogo emergente para **Confirmar dirección URL abierta.**</span><span class="sxs-lookup"><span data-stu-id="99fec-393">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="99fec-394">Esto permite que el usuario del bot (usted) se autentique.</span><span class="sxs-lookup"><span data-stu-id="99fec-394">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="99fec-395">Seleccione **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-395">Select **Confirm**.</span></span>
1. <span data-ttu-id="99fec-396">Si se le pide, seleccione la cuenta del usuario aplicable.</span><span class="sxs-lookup"><span data-stu-id="99fec-396">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="99fec-397">Según la configuración que usó para el emulador, se obtiene una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="99fec-397">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="99fec-398">**Uso del código de verificación de inicio de sesión**</span><span class="sxs-lookup"><span data-stu-id="99fec-398">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="99fec-399">&#x2713; Se abre una ventana que muestra el código de validación.</span><span class="sxs-lookup"><span data-stu-id="99fec-399">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="99fec-400">&#x2713; copiar y escribir el código de validación en el cuadro de chat para completar el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-400">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="99fec-401">**Uso de tokens de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="99fec-401">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="99fec-402">&#x2713; Ha iniciado sesión en función de sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="99fec-402">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="99fec-403">La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="99fec-403">The following image is an example of the bot UI after you've logged in:</span></span>

    ![Emulador de inicio de sesión del bot de autenticación](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="99fec-405">Si selecciona **Sí cuando** el bot le pregunta ¿Le gustaría ver el *token?*, tendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="99fec-405">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![Token de emulador de inicio de sesión del bot de autenticación](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="99fec-407">Escriba **cerrar sesión en** el cuadro de chat de entrada para cerrar la sesión. Esto libera el token de usuario y el bot no podrá actuar en su nombre hasta que inicie sesión de nuevo.</span><span class="sxs-lookup"><span data-stu-id="99fec-407">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="99fec-408">La autenticación de bots requiere el uso del **servicio Bot Connector**.</span><span class="sxs-lookup"><span data-stu-id="99fec-408">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="99fec-409">El servicio tiene acceso a la información de registro de canales del bot para el bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-409">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="99fec-410">Probar el bot implementado</span><span class="sxs-lookup"><span data-stu-id="99fec-410">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="99fec-411">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="99fec-411">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="99fec-412">Busque el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99fec-412">Find your resource group.</span></span>
1. <span data-ttu-id="99fec-413">Seleccione el vínculo de recurso.</span><span class="sxs-lookup"><span data-stu-id="99fec-413">Select the resource link.</span></span> <span data-ttu-id="99fec-414">Se muestra la página de recursos.</span><span class="sxs-lookup"><span data-stu-id="99fec-414">The resource page is displayed.</span></span>
1. <span data-ttu-id="99fec-415">En la página de recursos, seleccione **Probar en chat web**.</span><span class="sxs-lookup"><span data-stu-id="99fec-415">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="99fec-416">El bot se inicia y muestra los saludos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="99fec-416">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="99fec-417">Escriba cualquier cosa en el cuadro de chat.</span><span class="sxs-lookup"><span data-stu-id="99fec-417">Type anything in the chat box.</span></span>
1. <span data-ttu-id="99fec-418">Seleccione el **cuadro Iniciar sesión.**</span><span class="sxs-lookup"><span data-stu-id="99fec-418">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="99fec-419">Se muestra un cuadro de diálogo emergente para **Confirmar dirección URL abierta.**</span><span class="sxs-lookup"><span data-stu-id="99fec-419">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="99fec-420">Esto permite que el usuario del bot (usted) se autentique.</span><span class="sxs-lookup"><span data-stu-id="99fec-420">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="99fec-421">Seleccione **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="99fec-421">Select **Confirm**.</span></span>
1. <span data-ttu-id="99fec-422">Si se le pide, seleccione la cuenta del usuario aplicable.</span><span class="sxs-lookup"><span data-stu-id="99fec-422">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="99fec-423">La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:</span><span class="sxs-lookup"><span data-stu-id="99fec-423">The following image is an example of the bot UI after you have logged in:</span></span>

    ![Inicio de sesión del bot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="99fec-425">.</span><span class="sxs-lookup"><span data-stu-id="99fec-425">.</span></span>

1. <span data-ttu-id="99fec-426">Seleccione el **botón Sí** para mostrar el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="99fec-426">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="99fec-427">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99fec-427">The following image is an example:</span></span>

    ![Token de inicio de sesión del bot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="99fec-429">.</span><span class="sxs-lookup"><span data-stu-id="99fec-429">.</span></span>

1. <span data-ttu-id="99fec-430">Escriba cerrar sesión para cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-430">Enter logout to sign out.</span></span>

    ![Inicio de sesión implementado por el bot de autenticación](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="99fec-432">Si tiene problemas para iniciar sesión, intente probar la conexión de nuevo como se describe en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="99fec-432">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="99fec-433">Esto podría volver a crear el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="99fec-433">This could recreate the authentication token.</span></span>
> <span data-ttu-id="99fec-434">Con el cliente de Chat web de Bot Framework en Azure, es posible que deba iniciar sesión varias veces antes de que la autenticación se establezca correctamente.</span><span class="sxs-lookup"><span data-stu-id="99fec-434">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="99fec-435">Instalar y probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="99fec-435">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="99fec-436">En el proyecto de bot, asegúrese de que la carpeta contiene la junto `TeamsAppManifest` con un y los `manifest.json` `outline.png` `color.png` archivos.</span><span class="sxs-lookup"><span data-stu-id="99fec-436">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="99fec-437">En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta.</span><span class="sxs-lookup"><span data-stu-id="99fec-437">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="99fec-438">Para `manifest.json` editar, asigne los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="99fec-438">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="99fec-439">Asegúrese de que **el identificador de aplicación del bot** que recibió en el momento del registro del canal del bot está asignado y `id` `botId` .</span><span class="sxs-lookup"><span data-stu-id="99fec-439">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="99fec-440">Asigne este valor: `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="99fec-440">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="99fec-441">Seleccione y **zip** los `manifest.json` archivos , `outline.png` `color.png` y.</span><span class="sxs-lookup"><span data-stu-id="99fec-441">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="99fec-442">Abra **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="99fec-442">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="99fec-443">En el panel izquierdo, en la parte inferior, seleccione el **icono Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="99fec-443">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="99fec-444">En el panel derecho, en la parte inferior, selecciona **Cargar una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="99fec-444">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="99fec-445">Vaya a la `TeamsAppManifest` carpeta y cargue el manifiesto comprimido.</span><span class="sxs-lookup"><span data-stu-id="99fec-445">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="99fec-446">Se muestra el siguiente asistente:</span><span class="sxs-lookup"><span data-stu-id="99fec-446">The following wizard is displayed:</span></span>

    ![Carga de equipos de bots de autenticación](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="99fec-448">Seleccione el botón **Agregar a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="99fec-448">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="99fec-449">En la siguiente ventana, seleccione el equipo donde desea usar el bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-449">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="99fec-450">Seleccione el **botón Configurar un bot.**</span><span class="sxs-lookup"><span data-stu-id="99fec-450">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="99fec-451">Seleccione los tres puntos (&#x25cf;&#x25cf;&#x25cf;) en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="99fec-451">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="99fec-452">A continuación, **selecciona el icono de App Studio.**</span><span class="sxs-lookup"><span data-stu-id="99fec-452">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="99fec-453">Seleccione la **pestaña Editor de manifiestos.** Debería ver el icono del bot que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="99fec-453">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="99fec-454">Además, deberías poder ver el bot como un contacto en la lista de chat que puedes usar para intercambiar mensajes con el bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-454">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="99fec-455">Probar el bot localmente en Teams</span><span class="sxs-lookup"><span data-stu-id="99fec-455">Testing the bot locally in Teams</span></span>

<span data-ttu-id="99fec-456">Microsoft Teams es un producto totalmente basado en la nube, que requiere que todos los servicios a los que tiene acceso estén disponibles desde la nube mediante puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="99fec-456">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="99fec-457">Por lo tanto, para permitir que el bot (nuestro ejemplo) funcione en Teams, debe publicar el código en la nube de su elección o hacer que una instancia en ejecución local sea accesible externamente **a** través de una herramienta de túnel.</span><span class="sxs-lookup"><span data-stu-id="99fec-457">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="99fec-458">Se recomienda  [ngrok](https://ngrok.com/download), que crea una dirección URL direccionable externamente para un puerto que se abre localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="99fec-458">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="99fec-459">Para configurar ngrok en preparación para ejecutar la aplicación de Microsoft Teams localmente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="99fec-459">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="99fec-460">En una ventana de terminal, vaya al directorio donde ha `ngrok.exe` instalado.</span><span class="sxs-lookup"><span data-stu-id="99fec-460">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="99fec-461">Se recomienda establecer la *ruta de acceso de la variable* de entorno para que apunte a ella.</span><span class="sxs-lookup"><span data-stu-id="99fec-461">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="99fec-462">Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="99fec-462">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="99fec-463">Reemplace el número de puerto según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="99fec-463">Replace the port number as needed.</span></span>
<span data-ttu-id="99fec-464">Esto inicia ngrok para escuchar en el puerto especificado.</span><span class="sxs-lookup"><span data-stu-id="99fec-464">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="99fec-465">A cambio, le proporciona una dirección URL direccionable externamente, válida durante el tiempo que ngrok se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="99fec-465">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="99fec-466">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99fec-466">The following image is an example:</span></span>

    ![cadena de conexión de la aplicación bot de teams adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="99fec-468">.</span><span class="sxs-lookup"><span data-stu-id="99fec-468">.</span></span>

1. <span data-ttu-id="99fec-469">Copie la dirección HTTPS de reenvío.</span><span class="sxs-lookup"><span data-stu-id="99fec-469">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="99fec-470">Debe ser similar a lo siguiente: `https://dea822bf.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="99fec-470">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="99fec-471">Anexar `/api/messages` para obtener `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="99fec-471">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="99fec-472">Este es el punto **de conexión de** mensajes para el bot que se ejecuta localmente en el equipo y al que se puede acceder a través de la web en un chat de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="99fec-472">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="99fec-473">Un último paso para realizar es actualizar el extremo de mensajes del bot implementado.</span><span class="sxs-lookup"><span data-stu-id="99fec-473">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="99fec-474">En el ejemplo, implementamos el bot en Azure.</span><span class="sxs-lookup"><span data-stu-id="99fec-474">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="99fec-475">Así que \*\*vamos a realizar estos pasos:</span><span class="sxs-lookup"><span data-stu-id="99fec-475">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="99fec-476">En el explorador, vaya a [**Azure Portal**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="99fec-476">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="99fec-477">Seleccione el **registro del canal bot**.</span><span class="sxs-lookup"><span data-stu-id="99fec-477">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="99fec-478">En el panel izquierdo, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="99fec-478">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="99fec-479">En el panel derecho, en el cuadro **Extremo** de mensajería, escriba la dirección URL de ngrok, en nuestro ejemplo, `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="99fec-479">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="99fec-480">Inicie el bot localmente, por ejemplo, en Visual Studio modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="99fec-480">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="99fec-481">Pruebe el bot mientras se ejecuta localmente con el chat web de prueba del portal **de** Bot Framework .</span><span class="sxs-lookup"><span data-stu-id="99fec-481">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="99fec-482">Al igual que el emulador, esta prueba no permite tener acceso a la funcionalidad específica de Teams.</span><span class="sxs-lookup"><span data-stu-id="99fec-482">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="99fec-483">En la ventana de terminal donde se ejecuta puede ver el tráfico `ngrok` HTTP entre el bot y el cliente de chat web.</span><span class="sxs-lookup"><span data-stu-id="99fec-483">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="99fec-484">Si desea una vista más detallada, en una ventana del explorador escriba que obtuvo `http://127.0.0.1:4040` de la ventana de terminal anterior.</span><span class="sxs-lookup"><span data-stu-id="99fec-484">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="99fec-485">La siguiente imagen es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99fec-485">The following image is an example:</span></span>

    ![Pruebas de auth bot teams ngrok](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="99fec-487">.</span><span class="sxs-lookup"><span data-stu-id="99fec-487">.</span></span>

> [!NOTE]
> <span data-ttu-id="99fec-488">Si detiene y reinicia ngrok, la dirección URL cambia.</span><span class="sxs-lookup"><span data-stu-id="99fec-488">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="99fec-489">Para usar ngrok en el proyecto y según las capacidades que use, debe actualizar todas las referencias de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="99fec-489">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="99fec-490">Información adicional</span><span class="sxs-lookup"><span data-stu-id="99fec-490">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="99fec-491">TeamsAppManifest/manifest.json</span><span class="sxs-lookup"><span data-stu-id="99fec-491">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="99fec-492">Este manifiesto contiene la información necesaria para que Microsoft Teams se conecte con el bot.</span><span class="sxs-lookup"><span data-stu-id="99fec-492">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

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

<span data-ttu-id="99fec-493">Con la autenticación, Teams se comporta de forma ligeramente diferente que otros canales, como se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="99fec-493">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="99fec-494">Controlar actividad de invocación</span><span class="sxs-lookup"><span data-stu-id="99fec-494">Handling Invoke Activity</span></span>

<span data-ttu-id="99fec-495">Se **envía una actividad Invoke** al bot en lugar de a la actividad de evento usada por otros canales.</span><span class="sxs-lookup"><span data-stu-id="99fec-495">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="99fec-496">Para ello, se subclase **activityHandler**.</span><span class="sxs-lookup"><span data-stu-id="99fec-496">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="99fec-497">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="99fec-497">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="99fec-498">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="99fec-498">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="99fec-499">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="99fec-499">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="99fec-500">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="99fec-500">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="99fec-501">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="99fec-501">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="99fec-502">JavaScript</span><span class="sxs-lookup"><span data-stu-id="99fec-502">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="99fec-503">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="99fec-503">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="99fec-504">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="99fec-504">**bots/teamsBot.js**</span></span>

<span data-ttu-id="99fec-505">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="99fec-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="99fec-506">**cuadros de diálogo/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="99fec-506">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="99fec-507">En un paso de cuadro de diálogo, use para iniciar el mensaje `beginDialog` de OAuth, que pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-507">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="99fec-508">Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="99fec-508">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="99fec-509">De lo contrario, se pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-509">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="99fec-510">El Servicio de bots de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-510">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="99fec-511">En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="99fec-511">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="99fec-512">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="99fec-512">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="99fec-513">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="99fec-513">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="99fec-514">Python</span><span class="sxs-lookup"><span data-stu-id="99fec-514">Python</span></span>](#tab/python-sample)

<span data-ttu-id="99fec-515">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="99fec-515">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="99fec-516">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="99fec-516">**bots/teams_bot.py**</span></span>

<span data-ttu-id="99fec-517">La *actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt.**</span><span class="sxs-lookup"><span data-stu-id="99fec-517">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="99fec-518">**dialogs/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="99fec-518">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="99fec-519">En un paso de cuadro de diálogo, use para iniciar el mensaje `begin_dialog` de OAuth, que pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-519">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="99fec-520">Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.</span><span class="sxs-lookup"><span data-stu-id="99fec-520">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="99fec-521">De lo contrario, se pedirá al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-521">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="99fec-522">El Servicio de bots de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="99fec-522">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="99fec-523">En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="99fec-523">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="99fec-524">Si no es null, el usuario ha iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="99fec-524">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="99fec-525">**dialogs/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="99fec-525">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="99fec-526">Obtenga información sobre cómo agregar autenticación a través del servicio bot de Azure</span><span class="sxs-lookup"><span data-stu-id="99fec-526">Learn about adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

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
