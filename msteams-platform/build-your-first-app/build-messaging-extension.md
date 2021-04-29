---
title: 'Introducción: crear una extensión de mensajería'
author: girliemac
description: Cree rápidamente una extensión de mensajería de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: 91a5a15697163ee9103607511047a6411a5acf1a
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068762"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="c5122-103">Crear la primera extensión de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c5122-103">Build your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="c5122-104">Hay dos tipos de extensiones de *mensajería de* Teams: comandos [de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) y comandos [de acción](../messaging-extensions/how-to/action-commands/define-action-command.md).</span><span class="sxs-lookup"><span data-stu-id="c5122-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="c5122-105">Este tutorial le enseña *a* crear un comando de búsqueda (también conocido como una extensión de mensajería basada en *búsqueda),* que es un acceso directo para buscar contenido externo y compartirlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-105">This tutorial teaches you to create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="c5122-106">Los usuarios pueden tener acceso a los comandos de búsqueda desde el cuadro de redacción o comando de Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-106">Users can access search commands from the Teams compose or command box.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c5122-107">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="c5122-107">What you'll learn</span></span>

* <span data-ttu-id="c5122-108">Crea un proyecto de aplicación y un bot de extensión de mensajería con Microsoft Teams Toolkit para Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="c5122-108">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="c5122-109">Comprenda las configuraciones de la aplicación y los scaffolding relevantes para las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c5122-109">Understand the app configurations and the scaffolding relevant to messaging extensions.</span></span>
* <span data-ttu-id="c5122-110">Hospedar una aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="c5122-110">Host an app locally.</span></span>
* <span data-ttu-id="c5122-111">Configure el bot para la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c5122-111">Configure the bot for your messaging extension.</span></span>
* <span data-ttu-id="c5122-112">Descarga local y prueba una extensión de mensajería en Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-112">Sideload and test a messaging extension in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5122-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c5122-113">Prerequisites</span></span>

<span data-ttu-id="c5122-114">Asegúrate de comprender cómo configurar y crear una aplicación sencilla de Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-114">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="c5122-115">Para obtener más información, consulta crear la primera aplicación de [Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="c5122-115">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="c5122-116">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="c5122-116">1. Create your app project</span></span>

<span data-ttu-id="c5122-117">Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="c5122-117">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="c5122-118">**Configuraciones de aplicaciones y scaffolding relevantes** para extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="c5122-118">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="c5122-119">**Bot** para la extensión de mensajería que se registra automáticamente en el Servicio de bots de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c5122-119">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

<span data-ttu-id="c5122-120">**Para crear el proyecto de aplicación**</span><span class="sxs-lookup"><span data-stu-id="c5122-120">**To create your app project**</span></span>

1. En Visual Studio, selecciona **Microsoft Teams en** la barra de actividades izquierda y elige Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams**.
1. <span data-ttu-id="c5122-122">Cuando se le pida, inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="c5122-122">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="c5122-123">En la **pantalla Seleccionar proyecto,** en **Búsqueda de extensiones de**  >  mensajería, haga clic en **JS (JavaScript).**</span><span class="sxs-lookup"><span data-stu-id="c5122-123">On the **Select project** screen, at **Messaging Extensions** > **Search**, click **JS (JavaScript)**.</span></span> 
1. <span data-ttu-id="c5122-124">Escribe un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-124">Enter a name for your Teams app.</span></span> <span data-ttu-id="c5122-125">Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="c5122-125">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="c5122-126">Seleccione **Crear un nuevo bot y, a** continuación, haga clic en El botón Crear registro **del** bot.</span><span class="sxs-lookup"><span data-stu-id="c5122-126">Select **Create a new Bot** then click **Create Bot Registration** button.</span></span> <span data-ttu-id="c5122-127">Si se realiza correctamente, el nuevo bot tendrá un *estado Registrado.*</span><span class="sxs-lookup"><span data-stu-id="c5122-127">If successful, your new bot will have a *Registered* status.</span></span> <span data-ttu-id="c5122-128">Ahora, el bot se registra automáticamente en el Servicio de bots de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c5122-128">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 
1. <span data-ttu-id="c5122-129">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto y guardar el proyecto en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="c5122-129">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="c5122-130">2. Comprender los componentes del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c5122-130">2. Understand your app project components</span></span>

<span data-ttu-id="c5122-131">Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="c5122-131">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

* <span data-ttu-id="c5122-132">Configuraciones de aplicaciones: para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a Extensiones **de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="c5122-132">App configurations: To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>
* <span data-ttu-id="c5122-133">Scaffolding de aplicaciones: el scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar cómo responde la extensión de mensajería (o técnicamente, el bot de la extensión de mensajería) a las consultas de búsqueda en `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="c5122-133">App scaffolding: The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="c5122-134">3. Configurar un túnel seguro en la aplicación</span><span class="sxs-lookup"><span data-stu-id="c5122-134">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="c5122-135">Para realizar pruebas, vamos a hospedar la extensión de mensajería en un servidor web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="c5122-135">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span> <span data-ttu-id="c5122-136">Va a usar [ngrok](https://ngrok.com/download) para configurar un túnel seguro para localhost.</span><span class="sxs-lookup"><span data-stu-id="c5122-136">You are going to use [ngrok](https://ngrok.com/download) to set up a secure tunnel to localhost.</span></span> <span data-ttu-id="c5122-137">Vea [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c5122-137">See [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) for details.</span></span> 

1. <span data-ttu-id="c5122-138">Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="c5122-138">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="c5122-139">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="c5122-139">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="c5122-140">Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ) ya que Teams requiere conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c5122-140">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

   <span data-ttu-id="c5122-141">Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá realizar un túnel donde hospedas la aplicación ( en el `localhost` puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="c5122-141">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="c5122-142">4. Configurar el bot para la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c5122-142">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="c5122-143">Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario de Teams al servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="c5122-143">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="c5122-144">El bot debe estar registrado en el Servicio de bots de Azure, que se hizo al configurar la aplicación con Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="c5122-144">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="c5122-145">Todavía debe especificar una dirección URL de extremo de bot para recibir y procesar consultas de búsqueda en la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c5122-145">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="c5122-146">Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` de .</span><span class="sxs-lookup"><span data-stu-id="c5122-146">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="c5122-147">Puede configurarlo rápidamente en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="c5122-147">You can configure this quickly in the toolkit.</span></span>

1. En Visual Studio, seleccione **Microsoft Teams en** la barra de actividades izquierda y elija Abrir Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Toolkit**.
1. <span data-ttu-id="c5122-149">Ve a **Bots > Registros de bots existentes** y selecciona el bot que creaste durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="c5122-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="c5122-150">En el **campo Dirección del extremo bot,** escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.</span><span class="sxs-lookup"><span data-stu-id="c5122-150">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

   <span data-ttu-id="c5122-151">El bot podrá controlar las consultas de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c5122-151">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="c5122-152">5. Crear y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="c5122-152">5. Build and run your app</span></span>

<span data-ttu-id="c5122-153">Ha configurado una dirección URL para hospedar la extensión de mensajería y la ha configurado para controlar las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="c5122-153">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="c5122-154">Es hora de que la aplicación esté en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="c5122-154">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="c5122-155">Abra el terminal y vaya al directorio raíz del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c5122-155">Open terminal and go to the root directory of your app project</span></span>
1. <span data-ttu-id="c5122-156">Ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="c5122-156">Run `npm install`.</span></span>
1. <span data-ttu-id="c5122-157">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="c5122-157">Run `npm start`.</span></span>

   <span data-ttu-id="c5122-158">Si se realiza correctamente, verá el siguiente mensaje que indica que el servicio de extensión de mensajería está escuchando la actividad en su `localhost` :</span><span class="sxs-lookup"><span data-stu-id="c5122-158">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="c5122-159">6. Instalación local de la extensión de mensajería en Teams</span><span class="sxs-lookup"><span data-stu-id="c5122-159">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="c5122-160">Con la extensión de mensajería en ejecución, puede instalarla en Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-160">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="c5122-161">Si no has descargado previamente una aplicación de Teams y tienes problemas, sigue estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="c5122-161">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="c5122-162">En Visual Studio, seleccione la **tecla F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-162">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="c5122-163">En el cuadro de diálogo de instalación de la aplicación, **selecciona Agregar para mí**.</span><span class="sxs-lookup"><span data-stu-id="c5122-163">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="c5122-164">7. Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c5122-164">7. Test your messaging extension</span></span>

<span data-ttu-id="c5122-165">Obtenga información sobre cómo funcionan las extensiones de mensajería en un chat de Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-165">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="c5122-166">Inicie un nuevo chat.</span><span class="sxs-lookup"><span data-stu-id="c5122-166">Start a new chat.</span></span> En el cuadro redacción, selecciona **Más** y selecciona la aplicación de extensión de :::image type="icon" source="../assets/icons/teams-client-more.png"::: mensajería que acaba de instalar.
1. <span data-ttu-id="c5122-168">Intente buscar algo (por ejemplo, **Tickets**).</span><span class="sxs-lookup"><span data-stu-id="c5122-168">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="c5122-169">Si la aplicación funciona, verás resultados de búsqueda de ejemplo (puedes agregar los tuyos más adelante).</span><span class="sxs-lookup"><span data-stu-id="c5122-169">If your app is working, you'll see sample search results (you can add your own later).</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Captura de pantalla que muestra cómo se usa una extensión de mensajería basada en búsqueda en el cuadro de redacción de Teams.":::

## <a name="troubleshooting"></a><span data-ttu-id="c5122-171">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="c5122-171">Troubleshooting</span></span>

<span data-ttu-id="c5122-172">La siguiente información puede ayudar si tiene problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c5122-172">The following information may help if you had issues completing this tutorial.</span></span>

<span data-ttu-id="c5122-173">**Bot no está conectado a Teams**</span><span class="sxs-lookup"><span data-stu-id="c5122-173">**Bot isn't connected to Teams**</span></span>

<span data-ttu-id="c5122-174">Si has instalado la aplicación pero no funciona, asegúrate de que el bot de la extensión de mensajería esté conectado al canal de Teams del servicio de bot [de Azure. ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c5122-174">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="c5122-175">Es importante comprender que esto no es lo mismo que un canal en Teams.</span><span class="sxs-lookup"><span data-stu-id="c5122-175">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="c5122-176">En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones compatible con Microsoft o [de terceros.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c5122-176">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="c5122-177">Consulte también</span><span class="sxs-lookup"><span data-stu-id="c5122-177">See also</span></span>

* [<span data-ttu-id="c5122-178">Cuadro de redacción o comando de Teams</span><span class="sxs-lookup"><span data-stu-id="c5122-178">Teams compose or command box</span></span>](../messaging-extensions/what-are-messaging-extensions.md) 
* [<span data-ttu-id="c5122-179">Incluir una característica de desamuestra de vínculos</span><span class="sxs-lookup"><span data-stu-id="c5122-179">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="c5122-180">Directrices de diseño</span><span class="sxs-lookup"><span data-stu-id="c5122-180">Design guidelines</span></span>](../messaging-extensions/design/messaging-extension-design.md) 
* [<span data-ttu-id="c5122-181">Plantillas de interfaz de usuario listas para producción</span><span class="sxs-lookup"><span data-stu-id="c5122-181">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="c5122-182">Añadir autenticación</span><span class="sxs-lookup"><span data-stu-id="c5122-182">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="c5122-183">Crear una extensión de mensajería basada en acciones</span><span class="sxs-lookup"><span data-stu-id="c5122-183">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="c5122-184">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c5122-184">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

## <a name="next-steps"></a><span data-ttu-id="c5122-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5122-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c5122-186">Definición de comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="c5122-186">Define search commands</span></span>](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c5122-187">Responder a las búsquedas de los usuarios</span><span class="sxs-lookup"><span data-stu-id="c5122-187">Respond to users' searches</span></span>](../messaging-extensions/how-to/search-commands/respond-to-search.md)