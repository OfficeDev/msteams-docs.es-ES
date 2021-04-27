---
title: 'Introducción: crear un bot'
author: heath-hamilton
description: Cree rápidamente un bot de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 5dfbfa05d2f1e36bbc14bd929cb2592303081522
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020003"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="f47a0-103">Crear un bot para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f47a0-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="f47a0-104">Compilarás una *aplicación* bot básica en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f47a0-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="f47a0-105">Un bot actúa como intermediario entre los usuarios de Teams y el servicio web.</span><span class="sxs-lookup"><span data-stu-id="f47a0-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="f47a0-106">Los usuarios pueden chatear con un bot para obtener información rápidamente o iniciar flujos de trabajo y tareas realizados por el servicio.</span><span class="sxs-lookup"><span data-stu-id="f47a0-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="f47a0-107">Su asignación</span><span class="sxs-lookup"><span data-stu-id="f47a0-107">Your assignment</span></span>

<span data-ttu-id="f47a0-108">El lugar de trabajo creó una aplicación de Teams que usa [pestañas para](../build-your-first-app/build-personal-tab.md) obtener información de contacto importante.</span><span class="sxs-lookup"><span data-stu-id="f47a0-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="f47a0-109">Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de ayuda.</span><span class="sxs-lookup"><span data-stu-id="f47a0-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="f47a0-110">Pero en lugar de llamar, ¿qué ocurre si las personas pudieran ponerse en contacto con el servicio de soporte con un chatbot?</span><span class="sxs-lookup"><span data-stu-id="f47a0-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="f47a0-111">El jefe te pide que veas la rapidez con la que puedes hacer que un bot conversacional básico se ejecute en Teams.</span><span class="sxs-lookup"><span data-stu-id="f47a0-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f47a0-112">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="f47a0-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="f47a0-113">Crear un proyecto de aplicación y un bot con Microsoft Teams Toolkit for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f47a0-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="f47a0-114">Identificar algunas de las configuraciones de la aplicación y los scaffolding relevantes para bots</span><span class="sxs-lookup"><span data-stu-id="f47a0-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="f47a0-115">Hospedar una aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="f47a0-115">Host an app locally</span></span>
> * <span data-ttu-id="f47a0-116">Configurar un bot para Teams</span><span class="sxs-lookup"><span data-stu-id="f47a0-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="f47a0-117">Instalación local y prueba de un bot en Teams</span><span class="sxs-lookup"><span data-stu-id="f47a0-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f47a0-118">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f47a0-118">Before you begin</span></span>

<span data-ttu-id="f47a0-119">Si aún no lo ha hecho, asegúrese de comprender e [instalar los requisitos previos](build-first-app-overview.md#get-prerequisites)de desarrollo de Teams .</span><span class="sxs-lookup"><span data-stu-id="f47a0-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="f47a0-120">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="f47a0-120">1. Create your app project</span></span>

<span data-ttu-id="f47a0-121">Microsoft Teams Toolkit te ayuda a configurar los siguientes componentes para la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f47a0-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="f47a0-122">**Configuraciones de aplicaciones y scaffolding relevantes** para bots</span><span class="sxs-lookup"><span data-stu-id="f47a0-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="f47a0-123">**Bot** que se registra automáticamente en el Servicio de bots de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f47a0-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="f47a0-124">Si no has creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que te sea útil seguir estas instrucciones que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="f47a0-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio, selecciona **Microsoft Teams en** la barra de actividades izquierda y elige Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams**.
1. <span data-ttu-id="f47a0-126">Cuando se le pida, inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="f47a0-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="f47a0-127">En la **pantalla Agregar funcionalidades,** **seleccione Bot** y, a **continuación, Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f47a0-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="f47a0-128">Escribe un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="f47a0-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="f47a0-129">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="f47a0-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="f47a0-130">Vaya a **Configurar bot y** seleccione Crear un nuevo bot **y, a** **continuación, Cree registro de bot.**</span><span class="sxs-lookup"><span data-stu-id="f47a0-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="f47a0-131">Si se realiza correctamente, el nuevo bot tendrá un **estado Registrado.**</span><span class="sxs-lookup"><span data-stu-id="f47a0-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="f47a0-132">Seleccione **Finalizar** en la parte inferior de la pantalla y elija una ubicación para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f47a0-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="f47a0-133">2. Identificar componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="f47a0-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="f47a0-134">Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="f47a0-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="f47a0-135">Veamos los componentes principales para crear un bot.</span><span class="sxs-lookup"><span data-stu-id="f47a0-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="f47a0-136">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f47a0-136">App configurations</span></span>

<span data-ttu-id="f47a0-137">Para ver o actualizar las configuraciones del bot, seleccione **App Studio** en el kit de herramientas y vaya a **Bots**.</span><span class="sxs-lookup"><span data-stu-id="f47a0-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="f47a0-138">Scaffolding de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f47a0-138">App scaffolding</span></span>

<span data-ttu-id="f47a0-139">El scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar el modo en que el bot procesa actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como `botActivityHandler.js` "Hello").</span><span class="sxs-lookup"><span data-stu-id="f47a0-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="f47a0-140">3. Configurar un túnel seguro en la aplicación</span><span class="sxs-lookup"><span data-stu-id="f47a0-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="f47a0-141">Para realizar pruebas, vamos a hospedar la aplicación en un servidor web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="f47a0-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="f47a0-142">Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="f47a0-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="f47a0-143">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="f47a0-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="f47a0-144">Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ) ya que Teams requiere conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f47a0-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="f47a0-145">Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá realizar un túnel donde hospedas la aplicación ( en el `localhost` puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="f47a0-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="f47a0-146">4. Configurar el bot</span><span class="sxs-lookup"><span data-stu-id="f47a0-146">4. Configure your bot</span></span>

<span data-ttu-id="f47a0-147">Para usar un bot en Teams, debe registrarlo con el Servicio de bots de Azure.</span><span class="sxs-lookup"><span data-stu-id="f47a0-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="f47a0-148">Afortunadamente, esto se realiza automáticamente al configurar la aplicación con Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="f47a0-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="f47a0-149">Todavía debe especificar una dirección de extremo para recibir y procesar los mensajes de usuario (es decir, solicitudes) enviados al bot.</span><span class="sxs-lookup"><span data-stu-id="f47a0-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="f47a0-150">Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` de .</span><span class="sxs-lookup"><span data-stu-id="f47a0-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="f47a0-151">Puede configurarlo rápidamente en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="f47a0-151">You can configure this quickly in the toolkit.</span></span>

1. En Visual Studio, seleccione **Microsoft Teams en** la barra de actividades izquierda y elija Abrir Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Toolkit**.
1. <span data-ttu-id="f47a0-153">Ve a **Bots > Registros de bots existentes** y selecciona el bot que creaste durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="f47a0-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="f47a0-154">En el **campo Dirección del extremo bot,** escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.</span><span class="sxs-lookup"><span data-stu-id="f47a0-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del extremo del bot en Teams Toolkit.":::

<span data-ttu-id="f47a0-156">El bot podrá responder a mensajes en Teams.</span><span class="sxs-lookup"><span data-stu-id="f47a0-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="f47a0-157">5. Crear y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="f47a0-157">5. Build and run your app</span></span>

<span data-ttu-id="f47a0-158">Configuró una dirección URL para hospedar el bot y la configuró para controlar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="f47a0-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="f47a0-159">Es hora de que la aplicación esté en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="f47a0-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="f47a0-160">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="f47a0-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="f47a0-161">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="f47a0-161">Run `npm start`.</span></span>

<span data-ttu-id="f47a0-162">Si se realiza correctamente, verá el siguiente mensaje que indica que el bot está escuchando la actividad en su `localhost` :</span><span class="sxs-lookup"><span data-stu-id="f47a0-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="f47a0-163">6. Instalación local del bot en Teams</span><span class="sxs-lookup"><span data-stu-id="f47a0-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="f47a0-164">Con el bot en ejecución, puedes instalarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="f47a0-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="f47a0-165">Si no has descargado previamente una aplicación de Teams y tienes problemas, sigue estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="f47a0-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="f47a0-166">En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="f47a0-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="f47a0-167">En el cuadro de diálogo de instalación de la aplicación, **selecciona Agregar para mí**.</span><span class="sxs-lookup"><span data-stu-id="f47a0-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="f47a0-168">(Puede agregar el bot a un canal o chat, pero es menos intrusivo para otros probar un bot en un chat uno a uno).</span><span class="sxs-lookup"><span data-stu-id="f47a0-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="f47a0-169">7. Probar el bot</span><span class="sxs-lookup"><span data-stu-id="f47a0-169">7. Test your bot</span></span>

<span data-ttu-id="f47a0-170">Ahora, para la parte divertida: vamos a decir "Hola" al bot.</span><span class="sxs-lookup"><span data-stu-id="f47a0-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="f47a0-171">En el cuadro redacción, envíe un `Hello` mensaje.</span><span class="sxs-lookup"><span data-stu-id="f47a0-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="f47a0-172">El bot responde con algo parecido al siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="f47a0-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Captura de pantalla que muestra a un usuario decir &quot;Hola&quot; a un bot de Teams y obtener una respuesta.":::

## <a name="well-done"></a><span data-ttu-id="f47a0-174">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="f47a0-174">Well done</span></span>

<span data-ttu-id="f47a0-175">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f47a0-175">Congratulations!</span></span> <span data-ttu-id="f47a0-176">Tienes un bot básico de Teams que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats).</span><span class="sxs-lookup"><span data-stu-id="f47a0-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f47a0-177">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="f47a0-177">Troubleshooting</span></span>

<span data-ttu-id="f47a0-178">La siguiente información puede ayudar si tiene problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f47a0-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="f47a0-179">Bot no está conectado a Teams</span><span class="sxs-lookup"><span data-stu-id="f47a0-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="f47a0-180">Si has instalado la aplicación pero el bot no funciona, asegúrate de que el bot está conectado al canal teams del Servicio de [bots de Azure.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f47a0-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="f47a0-181">Es importante comprender que esto no es lo mismo que un canal en Teams.</span><span class="sxs-lookup"><span data-stu-id="f47a0-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="f47a0-182">En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones compatible con Microsoft o [de terceros.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f47a0-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="f47a0-183">Más información</span><span class="sxs-lookup"><span data-stu-id="f47a0-183">Learn more</span></span>

* [<span data-ttu-id="f47a0-184">Ver qué más pueden hacer los bots de Teams con uno de nuestros ejemplos</span><span class="sxs-lookup"><span data-stu-id="f47a0-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="f47a0-185">Conceptos básicos de las conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="f47a0-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* <span data-ttu-id="f47a0-186">Siga nuestras [directrices de diseño](../bots/design/bots.md) y cree con [plantillas de](../concepts/design/design-teams-app-ui-templates.md) interfaz de usuario preparadas para producción para crear una experiencia perfecta.</span><span class="sxs-lookup"><span data-stu-id="f47a0-186">Follow our [design guidelines](../bots/design/bots.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="f47a0-187">Autenticación de bot en Teams</span><span class="sxs-lookup"><span data-stu-id="f47a0-187">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="f47a0-188">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f47a0-188">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="f47a0-189">Crear un bot sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="f47a0-189">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)
