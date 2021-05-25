---
title: Agregar Power Virtual Agents chatbot a Teams
author: laujan
description: integración de un Power Virtual Agents chatbot en la plataforma Teams web
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: a38b2447bba42e70d8a1c3c9dca5d92e41cfb77c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630596"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="7129d-103">Añadir un bot de chat de Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="7129d-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="7129d-104">Power Virtual Agents es una solución de interfaz gráfica guiada sin código que permite a todos los miembros del equipo crear bots de chat enriquecidos y conversacionales que se integren fácilmente con la plataforma Teams web.</span><span class="sxs-lookup"><span data-stu-id="7129d-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="7129d-105">Todo el contenido escrito en Power Virtual Agents se representa de forma natural en Teams.</span><span class="sxs-lookup"><span data-stu-id="7129d-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="7129d-106">Power Virtual Agents bots interactúan con los usuarios en el Teams de chat nativo.</span><span class="sxs-lookup"><span data-stu-id="7129d-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="7129d-107">Los administradores de TI, analistas empresariales, especialistas en dominios y desarrolladores de aplicaciones cualificados pueden diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="7129d-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="7129d-108">Pueden crear un servicio web o registrarse directamente con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="7129d-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="7129d-109">Este documento le guía sobre cómo hacer que el bot de chat esté disponible en Teams a través del portal de Power Virtual Agents y agregar el bot a Teams con App Studio.</span><span class="sxs-lookup"><span data-stu-id="7129d-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="7129d-110">Power Virtual Agents le permite crear potentes bots de chat que puedan responder a las preguntas de sus clientes, otros empleados o visitantes de su sitio web o servicio.</span><span class="sxs-lookup"><span data-stu-id="7129d-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="7129d-111">Estos bots se pueden crear fácilmente sin necesidad de científicos de datos o desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="7129d-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="7129d-112">Al agregar el bot de chat a Microsoft Teams, algunos de los datos, como el contenido del bot y el contenido de chat del usuario, se comparten con Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7129d-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="7129d-113">Significa que los datos fluyen fuera del cumplimiento de la organización y de los límites [geográficos o regionales](/power-virtual-agents/data-location).</span><span class="sxs-lookup"><span data-stu-id="7129d-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="7129d-114">Haga que el bot de chat esté disponible en Teams a través del portal Power Virtual Agents web</span><span class="sxs-lookup"><span data-stu-id="7129d-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="7129d-115">Para que el chatbot esté disponible en Teams a través del portal de Power Virtual Agents, debe realizar los siguientes pasos de proceso:</span><span class="sxs-lookup"><span data-stu-id="7129d-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="7129d-116">**Para que el bot de chat esté disponible en Teams**</span><span class="sxs-lookup"><span data-stu-id="7129d-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="7129d-117">**Publicar el contenido del bot más reciente**</span><span class="sxs-lookup"><span data-stu-id="7129d-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="7129d-118">Después de crear un bot de chat en el portal de Power Virtual Agents, debe publicar el bot antes de que Teams usuarios puedan interactuar con él.</span><span class="sxs-lookup"><span data-stu-id="7129d-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="7129d-119">Para obtener más información, [vea Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span><span class="sxs-lookup"><span data-stu-id="7129d-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![publicar en el portal de agentes virtuales de energía](../../assets/images/pva-publish.png)

1. <span data-ttu-id="7129d-121">**Configurar el canal Teams cliente**</span><span class="sxs-lookup"><span data-stu-id="7129d-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="7129d-122">Después de publicar el bot, agregue el canal Teams para que el bot esté disponible para Teams usuarios.</span><span class="sxs-lookup"><span data-stu-id="7129d-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![canales en el portal de agentes virtuales de energía](../../assets/images/pva-channels.png)

1. <span data-ttu-id="7129d-124">**Generar un identificador de aplicación para el bot de chat**</span><span class="sxs-lookup"><span data-stu-id="7129d-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="7129d-125">Después de agregar el Teams al bot de chat, se genera un **identificador** de aplicación en el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7129d-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="7129d-126">El identificador de la aplicación es un identificador único generado por Microsoft para el bot.</span><span class="sxs-lookup"><span data-stu-id="7129d-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="7129d-127">Guarda el id. de aplicación para crear un paquete de aplicación para Teams.</span><span class="sxs-lookup"><span data-stu-id="7129d-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="7129d-128">Agregar el bot a Teams con App Studio</span><span class="sxs-lookup"><span data-stu-id="7129d-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="7129d-129">Si [la carga de aplicaciones](/microsoftteams/admin-settings) personalizadas está habilitada en la instancia de Teams, puedes usar Teams App Studio para cargar directamente el chatbot y empezar a usarlo inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="7129d-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="7129d-130">Para compartir el bot de chat, puedes solicitar al administrador que haga que el bot esté disponible en el catálogo de aplicaciones de inquilino o puedes enviar el paquete de la aplicación a otros usuarios y pedirles que lo carguen de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="7129d-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="7129d-131">**Instalar App Studio en Teams**</span><span class="sxs-lookup"><span data-stu-id="7129d-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="7129d-132">App Studio es una Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="7129d-132">App Studio is a Teams app.</span></span> <span data-ttu-id="7129d-133">Instale App Studio desde la Teams que simplifica el proceso de creación y registro de bots en Teams:</span><span class="sxs-lookup"><span data-stu-id="7129d-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="7129d-134">Selecciona el icono de la tienda de aplicaciones Teams instancia y busca **App Studio**.</span><span class="sxs-lookup"><span data-stu-id="7129d-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="7129d-135">Selecciona el **icono de App Studio** y selecciona **Instalar** en el cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="7129d-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="7129d-136">**Crear el manifiesto Teams aplicación en App Studio**</span><span class="sxs-lookup"><span data-stu-id="7129d-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="7129d-137">Los bots de Teams se definen mediante un archivo JSON de manifiesto de aplicación que proporciona la información básica sobre el bot y sus capacidades.</span><span class="sxs-lookup"><span data-stu-id="7129d-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="7129d-138">En **App Studio,** selecciona **Editor de manifiestos** y **selecciona Crear una nueva aplicación.**</span><span class="sxs-lookup"><span data-stu-id="7129d-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>

    ![crear una nueva aplicación](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="7129d-140">**Agregar los detalles del bot**</span><span class="sxs-lookup"><span data-stu-id="7129d-140">**Add your bot details**</span></span>  
<span data-ttu-id="7129d-141">Complete todos los campos necesarios.</span><span class="sxs-lookup"><span data-stu-id="7129d-141">Complete all the required fields.</span></span> <span data-ttu-id="7129d-142">Para obtener una descripción completa de cada campo, vea [definición de esquema de manifiesto](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7129d-142">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>

    ![agregar detalles de la aplicación](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="7129d-144">**Configurar el bot** Para configurar el bot, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7129d-144">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="7129d-145">Abra la **pestaña Bots.**</span><span class="sxs-lookup"><span data-stu-id="7129d-145">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="7129d-146">Seleccione **Configurar**  >  **bot existente** y escriba el nombre del bot.</span><span class="sxs-lookup"><span data-stu-id="7129d-146">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   ![Configuración del bot](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="7129d-148">En la siguiente imagen se muestra cómo configurar un bot existente:</span><span class="sxs-lookup"><span data-stu-id="7129d-148">The following image depicts how to set-up an existing bot:</span></span>      

   ![configuración de bots existente](../../assets/images/get-started/existing-bot-set-up.png)
       
1. <span data-ttu-id="7129d-150">**Agregar el id. de aplicación**</span><span class="sxs-lookup"><span data-stu-id="7129d-150">**Add your App ID**</span></span>  
<span data-ttu-id="7129d-151">Para agregar el identificador de aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7129d-151">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="7129d-152">Selecciona **Conectar un identificador de bot diferente** y pega el **Id. de aplicación** que has copiado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7129d-152">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="7129d-153">Seleccione **Guardar**  >  **personal**  >  **del ámbito**.</span><span class="sxs-lookup"><span data-stu-id="7129d-153">Select **Scope** > **Personal** > **Save**.</span></span>

    ![agregar id. de aplicación](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="7129d-155">**Agregar dominios válidos para el bot**</span><span class="sxs-lookup"><span data-stu-id="7129d-155">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="7129d-156">Este paso solo es necesario si el bot requiere que el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7129d-156">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="7129d-157">Seleccione Dominios y permisos y, en el **campo Dominios** **válidos,** proporcione la siguiente entrada:</span><span class="sxs-lookup"><span data-stu-id="7129d-157">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

1. <span data-ttu-id="7129d-158">**Probar y distribuir el bot**</span><span class="sxs-lookup"><span data-stu-id="7129d-158">**Test and distribute your bot**</span></span>  
<span data-ttu-id="7129d-159">Abra **la pestaña Probar y distribuir** y seleccione **Instalar** para agregar el bot directamente a la Teams instancia.</span><span class="sxs-lookup"><span data-stu-id="7129d-159">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="7129d-160">Como alternativa, puedes descargar el paquete de la aplicación completado para compartirlo con Teams usuarios o proporcionarlo al administrador para que el bot esté disponible en el catálogo de aplicaciones de inquilino.</span><span class="sxs-lookup"><span data-stu-id="7129d-160">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

1. <span data-ttu-id="7129d-161">**Iniciar un chat** </span><span class="sxs-lookup"><span data-stu-id="7129d-161">**Start a chat** </span></span>  
<span data-ttu-id="7129d-162">El proceso de configuración para agregar el bot Power Virtual Agents chat a Teams completa.</span><span class="sxs-lookup"><span data-stu-id="7129d-162">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="7129d-163">Ahora puedes iniciar una conversación con el bot en un chat personal.</span><span class="sxs-lookup"><span data-stu-id="7129d-163">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="7129d-164">Vea también</span><span class="sxs-lookup"><span data-stu-id="7129d-164">See also</span></span>

* [<span data-ttu-id="7129d-165">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="7129d-165">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* <span data-ttu-id="7129d-166">[Crear un chatbot para Teams con Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span><span class="sxs-lookup"><span data-stu-id="7129d-166">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>  
* [<span data-ttu-id="7129d-167">Power Virtual Agents portal</span><span class="sxs-lookup"><span data-stu-id="7129d-167">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)
* [<span data-ttu-id="7129d-168">Publicar el Power Virtual Agents bot</span><span class="sxs-lookup"><span data-stu-id="7129d-168">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)
* <span data-ttu-id="7129d-169">[Seguridad y cumplimiento en Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span><span class="sxs-lookup"><span data-stu-id="7129d-169">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="7129d-170">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="7129d-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7129d-171">Crear asistente virtual</span><span class="sxs-lookup"><span data-stu-id="7129d-171">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

