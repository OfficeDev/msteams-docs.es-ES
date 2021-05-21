---
title: 'Introducción: crear una extensión de mensajería'
author: girliemac
description: Cree rápidamente una Microsoft Teams de mensajería mediante el Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: c120a5b5d878c549cde008c3e1ccc71743a4e24f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566064"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="0a90f-103">Crear la primera extensión de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0a90f-103">Build your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="0a90f-104">Hay dos tipos de extensiones Teams *mensajería:* [comandos de](../messaging-extensions/how-to/search-commands/define-search-command.md) búsqueda y [comandos de acción](../messaging-extensions/how-to/action-commands/define-action-command.md).</span><span class="sxs-lookup"><span data-stu-id="0a90f-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="0a90f-105">Este tutorial le enseña *a* crear un comando de búsqueda (también conocido como una extensión de mensajería basada en *búsqueda),* que es un acceso directo para buscar contenido externo y compartirlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="0a90f-105">This tutorial teaches you to create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="0a90f-106">Los usuarios pueden tener acceso a los comandos de búsqueda desde Teams cuadro de redacción o comando.</span><span class="sxs-lookup"><span data-stu-id="0a90f-106">Users can access search commands from the Teams compose or command box.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0a90f-107">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="0a90f-107">What you'll learn</span></span>

* <span data-ttu-id="0a90f-108">Crea un proyecto de aplicación y un bot de extensión de mensajería con el Microsoft Teams Toolkit para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0a90f-108">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="0a90f-109">Comprenda las configuraciones de la aplicación y los scaffolding relevantes para las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0a90f-109">Understand the app configurations and the scaffolding relevant to messaging extensions.</span></span>
* <span data-ttu-id="0a90f-110">Hospedar una aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="0a90f-110">Host an app locally.</span></span>
* <span data-ttu-id="0a90f-111">Configure el bot para la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0a90f-111">Configure the bot for your messaging extension.</span></span>
* <span data-ttu-id="0a90f-112">Descarga local y prueba una extensión de mensajería en Teams.</span><span class="sxs-lookup"><span data-stu-id="0a90f-112">Sideload and test a messaging extension in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a90f-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0a90f-113">Prerequisites</span></span>

<span data-ttu-id="0a90f-114">Asegúrate de comprender cómo configurar y crear una aplicación Teams sencilla.</span><span class="sxs-lookup"><span data-stu-id="0a90f-114">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="0a90f-115">Para obtener más información, consulta [crear la primera aplicación Microsoft Teams "Hello, World!"](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="0a90f-115">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="0a90f-116">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="0a90f-116">1. Create your app project</span></span>

<span data-ttu-id="0a90f-117">La Microsoft Teams Toolkit ayuda a configurar los siguientes componentes para la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="0a90f-117">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="0a90f-118">**Configuraciones de aplicaciones y scaffolding relevantes** para extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0a90f-118">**App configurations and scaffolding** relevant to messaging extensions.</span></span>
* <span data-ttu-id="0a90f-119">**Bot** para la extensión de mensajería que se registra automáticamente con el servicio Microsoft Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="0a90f-119">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="0a90f-120">**Para crear el proyecto de aplicación**</span><span class="sxs-lookup"><span data-stu-id="0a90f-120">**To create your app project**</span></span>

1. En Visual Studio Code, selecciona **Microsoft Teams** en la barra de actividades izquierda y :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: elige Crear una nueva aplicación Teams **.**
1. <span data-ttu-id="0a90f-122">Cuando se le pida, inicie sesión con su Microsoft 365 de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="0a90f-122">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="0a90f-123">En la **pantalla Seleccionar proyecto,** en **Búsqueda de extensiones de**  >  mensajería, haga clic en **JS (JavaScript).**</span><span class="sxs-lookup"><span data-stu-id="0a90f-123">On the **Select project** screen, at **Messaging Extensions** > **Search**, click **JS (JavaScript)**.</span></span> 
1. <span data-ttu-id="0a90f-124">Escribe un nombre para la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a90f-124">Enter a name for your Teams app.</span></span> <span data-ttu-id="0a90f-125">Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="0a90f-125">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="0a90f-126">Seleccione **Crear un nuevo bot y, a** continuación, haga clic en El botón Crear registro **del** bot.</span><span class="sxs-lookup"><span data-stu-id="0a90f-126">Select **Create a new Bot** then click **Create Bot Registration** button.</span></span> <span data-ttu-id="0a90f-127">Si se realiza correctamente, el nuevo bot tendrá un *estado Registrado.*</span><span class="sxs-lookup"><span data-stu-id="0a90f-127">If successful, your new bot will have a *Registered* status.</span></span> <span data-ttu-id="0a90f-128">Ahora, el bot se registra automáticamente con el servicio Microsoft Azure bot.</span><span class="sxs-lookup"><span data-stu-id="0a90f-128">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 
1. <span data-ttu-id="0a90f-129">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto y guardar el proyecto en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="0a90f-129">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="0a90f-130">2. Comprender los componentes del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0a90f-130">2. Understand your app project components</span></span>

<span data-ttu-id="0a90f-131">Gran parte de las configuraciones de la aplicación y los scaffolding se establecen automáticamente al crear el proyecto con el Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="0a90f-131">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

* <span data-ttu-id="0a90f-132">Configuraciones de aplicaciones: para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a Extensiones **de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="0a90f-132">App configurations: To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>
* <span data-ttu-id="0a90f-133">Scaffolding de aplicaciones: el scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar cómo la extensión de mensajería (o técnicamente, el bot de la extensión de mensajería) responde a las consultas de búsqueda en `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="0a90f-133">App scaffolding: The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="0a90f-134">3. Configurar un túnel seguro en la aplicación</span><span class="sxs-lookup"><span data-stu-id="0a90f-134">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="0a90f-135">Para realizar pruebas, vamos a hospedar la extensión de mensajería en un servidor web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="0a90f-135">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span> <span data-ttu-id="0a90f-136">Va a usar [ngrok](https://ngrok.com/download) para configurar un túnel seguro para localhost.</span><span class="sxs-lookup"><span data-stu-id="0a90f-136">You are going to use [ngrok](https://ngrok.com/download) to set up a secure tunnel to localhost.</span></span> <span data-ttu-id="0a90f-137">Consulta [crear el primer bot para obtener Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0a90f-137">See [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) for details.</span></span> 

1. <span data-ttu-id="0a90f-138">Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="0a90f-138">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="0a90f-139">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="0a90f-139">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="0a90f-140">Copie la dirección URL HTTPS en el resultado (por ejemplo, ) ya que `https://468b9ab725e9.ngrok.io` Teams requiere conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0a90f-140">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

   <span data-ttu-id="0a90f-141">Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá realizar un túnel donde hospedas la aplicación ( en el `localhost` puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="0a90f-141">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="0a90f-142">4. Configurar el bot para la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="0a90f-142">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="0a90f-143">Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario desde Teams al servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="0a90f-143">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="0a90f-144">El bot debe estar registrado en el Servicio de bots de Azure, que se ha realizado al configurar la aplicación mediante el Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="0a90f-144">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="0a90f-145">Todavía debe especificar una dirección URL de extremo de bot para recibir y procesar consultas de búsqueda en la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0a90f-145">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="0a90f-146">Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` de .</span><span class="sxs-lookup"><span data-stu-id="0a90f-146">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="0a90f-147">Puede configurarlo rápidamente en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="0a90f-147">You can configure this quickly in the toolkit.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** en la barra de actividades izquierda :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: y elija Abrir **Microsoft Teams Toolkit**.
1. <span data-ttu-id="0a90f-149">Ve a **Bots > Registros de bots existentes** y selecciona el bot que creaste durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="0a90f-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="0a90f-150">En el **campo Dirección del extremo bot,** escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.</span><span class="sxs-lookup"><span data-stu-id="0a90f-150">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

   <span data-ttu-id="0a90f-151">El bot podrá controlar las consultas de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0a90f-151">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="0a90f-152">5. Crear y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="0a90f-152">5. Build and run your app</span></span>

<span data-ttu-id="0a90f-153">Ha configurado una dirección URL para hospedar la extensión de mensajería y la ha configurado para controlar las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="0a90f-153">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="0a90f-154">Es hora de que la aplicación esté en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="0a90f-154">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="0a90f-155">Abre el terminal y ve al directorio raíz del proyecto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a90f-155">Open terminal and go to the root directory of your app project.</span></span>
1. <span data-ttu-id="0a90f-156">Ejecute `npm install`.</span><span class="sxs-lookup"><span data-stu-id="0a90f-156">Run `npm install`.</span></span>
1. <span data-ttu-id="0a90f-157">Ejecute `npm start`.</span><span class="sxs-lookup"><span data-stu-id="0a90f-157">Run `npm start`.</span></span>

   <span data-ttu-id="0a90f-158">Si se realiza correctamente, verá el siguiente mensaje que indica que el servicio de extensión de mensajería está escuchando la actividad en su `localhost` :</span><span class="sxs-lookup"><span data-stu-id="0a90f-158">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="0a90f-159">6. Cargar localmente la extensión de mensajería en Teams</span><span class="sxs-lookup"><span data-stu-id="0a90f-159">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="0a90f-160">Con la extensión de mensajería en ejecución, puede instalarla en Teams.</span><span class="sxs-lookup"><span data-stu-id="0a90f-160">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="0a90f-161">Si no has descargado localmente una aplicación Teams antes y te encuentras con problemas, sigue estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="0a90f-161">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="0a90f-162">En Visual Studio Code, seleccione la clave **F5** para iniciar un Teams web.</span><span class="sxs-lookup"><span data-stu-id="0a90f-162">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="0a90f-163">En el cuadro de diálogo de instalación de la aplicación, **selecciona Agregar para mí**.</span><span class="sxs-lookup"><span data-stu-id="0a90f-163">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="0a90f-164">7. Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="0a90f-164">7. Test your messaging extension</span></span>

<span data-ttu-id="0a90f-165">Obtenga información sobre cómo funcionan las extensiones de mensajería en un Teams chat.</span><span class="sxs-lookup"><span data-stu-id="0a90f-165">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="0a90f-166">Inicie un nuevo chat.</span><span class="sxs-lookup"><span data-stu-id="0a90f-166">Start a new chat.</span></span> En el cuadro redacción, selecciona **Más** y selecciona la aplicación de extensión de :::image type="icon" source="../assets/icons/teams-client-more.png"::: mensajería que acaba de instalar.
1. <span data-ttu-id="0a90f-168">Intente buscar algo (por ejemplo, **Tickets**).</span><span class="sxs-lookup"><span data-stu-id="0a90f-168">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="0a90f-169">Si la aplicación funciona, verás resultados de búsqueda de ejemplo (puedes agregar los tuyos más adelante).</span><span class="sxs-lookup"><span data-stu-id="0a90f-169">If your app is working, you'll see sample search results (you can add your own later).</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Captura de pantalla que muestra cómo se usa una extensión de mensajería basada en búsqueda en el Teams cuadro de redacción.":::

## <a name="troubleshooting"></a><span data-ttu-id="0a90f-171">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="0a90f-171">Troubleshooting</span></span>

<span data-ttu-id="0a90f-172">La siguiente información puede ayudar si tiene problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0a90f-172">The following information may help if you had issues completing this tutorial.</span></span>

<span data-ttu-id="0a90f-173">**Bot no está conectado a Teams**</span><span class="sxs-lookup"><span data-stu-id="0a90f-173">**Bot isn't connected to Teams**</span></span>

<span data-ttu-id="0a90f-174">Si instalaste la aplicación pero no funciona, asegúrate de que el bot de la extensión de mensajería esté conectado al canal de Teams [ *bot de* Azure](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="0a90f-174">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="0a90f-175">Es importante comprender que esto no es lo mismo que un canal en Teams.</span><span class="sxs-lookup"><span data-stu-id="0a90f-175">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="0a90f-176">En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones compatible con Microsoft o [de terceros.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="0a90f-176">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="0a90f-177">Consulte también</span><span class="sxs-lookup"><span data-stu-id="0a90f-177">See also</span></span>

* [<span data-ttu-id="0a90f-178">Teams comando o redacción</span><span class="sxs-lookup"><span data-stu-id="0a90f-178">Teams compose or command box</span></span>](../messaging-extensions/what-are-messaging-extensions.md) 
* [<span data-ttu-id="0a90f-179">Incluir una característica de desamuestra de vínculos</span><span class="sxs-lookup"><span data-stu-id="0a90f-179">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="0a90f-180">Directrices de diseño</span><span class="sxs-lookup"><span data-stu-id="0a90f-180">Design guidelines</span></span>](../messaging-extensions/design/messaging-extension-design.md) 
* [<span data-ttu-id="0a90f-181">Plantillas de interfaz de usuario listas para producción</span><span class="sxs-lookup"><span data-stu-id="0a90f-181">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="0a90f-182">Añadir autenticación</span><span class="sxs-lookup"><span data-stu-id="0a90f-182">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="0a90f-183">Crear una extensión de mensajería basada en acciones</span><span class="sxs-lookup"><span data-stu-id="0a90f-183">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="0a90f-184">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0a90f-184">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

## <a name="next-steps"></a><span data-ttu-id="0a90f-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a90f-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a90f-186">Definición de comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="0a90f-186">Define search commands</span></span>](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a90f-187">Responder a las búsquedas de los usuarios</span><span class="sxs-lookup"><span data-stu-id="0a90f-187">Respond to users' searches</span></span>](../messaging-extensions/how-to/search-commands/respond-to-search.md)
