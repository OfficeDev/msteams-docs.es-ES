---
title: 'Introducción: creación de un bot'
author: heath-hamilton
description: Cree rápidamente un bot de Microsoft Teams con el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931745"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="edcb7-103">Crear un bot para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="edcb7-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="edcb7-104">Compilará una aplicación de *Bot* básica en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="edcb7-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="edcb7-105">Un bot actúa como intermediario entre los usuarios de Microsoft Teams y el servicio Web.</span><span class="sxs-lookup"><span data-stu-id="edcb7-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="edcb7-106">Los usuarios pueden chatear con un bot para obtener información o iniciar flujos de trabajo y tareas realizados por el servicio de forma rápida.</span><span class="sxs-lookup"><span data-stu-id="edcb7-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="edcb7-107">La asignación</span><span class="sxs-lookup"><span data-stu-id="edcb7-107">Your assignment</span></span>

<span data-ttu-id="edcb7-108">El área de trabajo ha creado una aplicación de Microsoft teams que usa [pestañas](../build-your-first-app/build-personal-tab.md) para exponer información de contacto importante.</span><span class="sxs-lookup"><span data-stu-id="edcb7-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="edcb7-109">Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de asistencia.</span><span class="sxs-lookup"><span data-stu-id="edcb7-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="edcb7-110">Pero, en lugar de llamar a, ¿qué sucede si los usuarios pueden ponerse en contacto con el Departamento de soporte mediante un Chatbot?</span><span class="sxs-lookup"><span data-stu-id="edcb7-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="edcb7-111">Su jefe le pedirá que consulte la velocidad con la que puede poner en marcha un bot de conversación básico en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="edcb7-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="edcb7-112">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="edcb7-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="edcb7-113">Crear un proyecto de aplicación y un bot con el kit de herramientas de Microsoft Teams para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="edcb7-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="edcb7-114">Identificar algunas de las configuraciones de aplicación y scaffolding relevantes para los bots</span><span class="sxs-lookup"><span data-stu-id="edcb7-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="edcb7-115">Hospedar una aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="edcb7-115">Host an app locally</span></span>
> * <span data-ttu-id="edcb7-116">Configurar un bot para Teams</span><span class="sxs-lookup"><span data-stu-id="edcb7-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="edcb7-117">Transferir localmente y probar un bot en Teams</span><span class="sxs-lookup"><span data-stu-id="edcb7-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="edcb7-118">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="edcb7-118">Before you begin</span></span>

<span data-ttu-id="edcb7-119">Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="edcb7-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="edcb7-120">1. crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="edcb7-120">1. Create your app project</span></span>

<span data-ttu-id="edcb7-121">El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="edcb7-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="edcb7-122">**Configuraciones de aplicación y scaffolding** relevantes para bots</span><span class="sxs-lookup"><span data-stu-id="edcb7-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="edcb7-123">**Bot** que se registra automáticamente con el servicio de robots de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="edcb7-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="edcb7-124">Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="edcb7-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. <span data-ttu-id="edcb7-126">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="edcb7-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="edcb7-127">En la pantalla **Agregar funciones** , seleccione **Bot** y, a continuación, **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="edcb7-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="edcb7-128">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="edcb7-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="edcb7-129">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="edcb7-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="edcb7-130">Vaya a **configurar bot** y seleccione **crear un nuevo bot** y, a continuación, **cree un registro de bot**.</span><span class="sxs-lookup"><span data-stu-id="edcb7-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="edcb7-131">Si se ejecuta correctamente, el nuevo bot tendrá un estado **registrado** .</span><span class="sxs-lookup"><span data-stu-id="edcb7-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="edcb7-132">Seleccione **Finalizar** en la parte inferior de la pantalla y elija una ubicación para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="edcb7-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="edcb7-133">2. identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="edcb7-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="edcb7-134">Una gran parte de la configuración de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="edcb7-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="edcb7-135">Echemos un vistazo a los componentes principales para crear un bot.</span><span class="sxs-lookup"><span data-stu-id="edcb7-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="edcb7-136">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="edcb7-136">App configurations</span></span>

<span data-ttu-id="edcb7-137">Para ver o actualizar las configuraciones de los bot, seleccione **App Studio** en el kit de herramientas y vaya a **bots**.</span><span class="sxs-lookup"><span data-stu-id="edcb7-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="edcb7-138">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="edcb7-138">App scaffolding</span></span>

<span data-ttu-id="edcb7-139">El scaffolding de la aplicación proporciona un `botActivityHandler.js` archivo, que se encuentra en el directorio raíz del proyecto, para controlar cómo el bot procesa las actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como "Hello").</span><span class="sxs-lookup"><span data-stu-id="edcb7-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="edcb7-140">3. configurar un túnel seguro a la aplicación</span><span class="sxs-lookup"><span data-stu-id="edcb7-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="edcb7-141">Para fines de prueba, vamos a hospedar la aplicación en un servidor Web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="edcb7-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="edcb7-142">Si todavía no lo ha hecho, instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="edcb7-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="edcb7-143">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="edcb7-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="edcb7-144">Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ), ya que Teams requiere conexiones https.</span><span class="sxs-lookup"><span data-stu-id="edcb7-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="edcb7-145">Con esta dirección URL, Teams (que requiere Conexiones HTTPS) podrá canalizar a donde se hospeda la aplicación ( `localhost` en el puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="edcb7-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="edcb7-146">4. configurar el bot</span><span class="sxs-lookup"><span data-stu-id="edcb7-146">4. Configure your bot</span></span>

<span data-ttu-id="edcb7-147">Para usar un bot en Teams, debe registrarlo con el servicio de bot de Azure.</span><span class="sxs-lookup"><span data-stu-id="edcb7-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="edcb7-148">Por suerte, esto se realiza automáticamente al configurar la aplicación con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="edcb7-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="edcb7-149">Todavía debe especificar una dirección de extremo para recibir y procesar los mensajes de usuario (por ejemplo, solicitudes) enviados al bot.</span><span class="sxs-lookup"><span data-stu-id="edcb7-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="edcb7-150">Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="edcb7-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="edcb7-151">Puede configurar esto rápidamente en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="edcb7-151">You can configure this quickly in the toolkit.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. <span data-ttu-id="edcb7-153">Vaya a **Bots > registros de bot existentes** y seleccione el bot que creó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="edcb7-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="edcb7-154">En el campo **dirección del extremo del bot** , escriba la dirección URL de ngrok (por ejemplo, `https://468b9ab725e9.ngrok.io` ) donde hospeda el bot y agréguelo `/api/messages` a él.</span><span class="sxs-lookup"><span data-stu-id="edcb7-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del punto de conexión del bot en el kit de herramientas de Teams.":::

<span data-ttu-id="edcb7-156">El bot podrá responder a los mensajes de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="edcb7-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="edcb7-157">5. compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="edcb7-157">5. Build and run your app</span></span>

<span data-ttu-id="edcb7-158">Ha configurado una dirección URL para hospedar el bot y configurarlo para administrar mensajes.</span><span class="sxs-lookup"><span data-stu-id="edcb7-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="edcb7-159">Es el momento de poner en marcha su aplicación.</span><span class="sxs-lookup"><span data-stu-id="edcb7-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="edcb7-160">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="edcb7-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="edcb7-161">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="edcb7-161">Run `npm start`.</span></span>

<span data-ttu-id="edcb7-162">Si se ejecuta correctamente, verá el siguiente mensaje que indica que el bot está escuchando la actividad en `localhost` :</span><span class="sxs-lookup"><span data-stu-id="edcb7-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="edcb7-163">6. transferir localmente el bot a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="edcb7-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="edcb7-164">Con el bot ejecutándose, puede instalarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="edcb7-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="edcb7-165">Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="edcb7-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="edcb7-166">En Visual Studio Code, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="edcb7-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="edcb7-167">En el cuadro de diálogo de instalación de la aplicación, seleccione **Agregar a mí**.</span><span class="sxs-lookup"><span data-stu-id="edcb7-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="edcb7-168">(Podría agregar el bot a un canal o un chat, pero es menos intrusivo para que otros puedan probar un bot en un chat único).</span><span class="sxs-lookup"><span data-stu-id="edcb7-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="edcb7-169">7. probar el bot</span><span class="sxs-lookup"><span data-stu-id="edcb7-169">7. Test your bot</span></span>

<span data-ttu-id="edcb7-170">Ahora es la parte divertida: digamos "Hola" a su bot.</span><span class="sxs-lookup"><span data-stu-id="edcb7-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="edcb7-171">En el cuadro de redacción, envíe un `Hello` mensaje.</span><span class="sxs-lookup"><span data-stu-id="edcb7-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="edcb7-172">El bot responde con algo parecido al siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="edcb7-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Una captura de pantalla que muestra un usuario diga ' Hello ' a un bot de Teams y obtenga una respuesta.":::

## <a name="well-done"></a><span data-ttu-id="edcb7-174">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="edcb7-174">Well done</span></span>

<span data-ttu-id="edcb7-175">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="edcb7-175">Congratulations!</span></span> <span data-ttu-id="edcb7-176">Tiene un bot básico de teams que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats).</span><span class="sxs-lookup"><span data-stu-id="edcb7-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="edcb7-177">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="edcb7-177">Troubleshooting</span></span>

<span data-ttu-id="edcb7-178">La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="edcb7-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="edcb7-179">Bot no está conectado a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="edcb7-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="edcb7-180">Si ha instalado la aplicación pero el bot no funciona, asegúrese de que el bot esté [conectado al *canal* Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="edcb7-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="edcb7-181">Es importante comprender que no es lo mismo que un canal en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="edcb7-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="edcb7-182">En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="edcb7-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="edcb7-183">Más información</span><span class="sxs-lookup"><span data-stu-id="edcb7-183">Learn more</span></span>

* [<span data-ttu-id="edcb7-184">Ver qué otros bots de Teams pueden hacer con una de nuestras muestras</span><span class="sxs-lookup"><span data-stu-id="edcb7-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="edcb7-185">Conceptos básicos de las conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="edcb7-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="edcb7-186">Autenticación de bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="edcb7-186">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="edcb7-187">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="edcb7-187">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="edcb7-188">Crear un bot sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="edcb7-188">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
