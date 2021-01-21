---
title: 'Introducción: crear un bot'
author: heath-hamilton
description: Cree rápidamente un bot de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: fbabd5130f0b7eb648a980f5f143792cc4c17933
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911950"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="3d482-103">Crear un bot para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3d482-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="3d482-104">En este tutorial, compilarás una *aplicación de bot* básica.</span><span class="sxs-lookup"><span data-stu-id="3d482-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="3d482-105">Un bot actúa como intermediario entre los usuarios de Teams y su servicio web.</span><span class="sxs-lookup"><span data-stu-id="3d482-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="3d482-106">Los usuarios pueden chatear con un bot para obtener rápidamente información o iniciar flujos de trabajo y tareas realizadas por el servicio.</span><span class="sxs-lookup"><span data-stu-id="3d482-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="3d482-107">Su asignación</span><span class="sxs-lookup"><span data-stu-id="3d482-107">Your assignment</span></span>

<span data-ttu-id="3d482-108">Su lugar de trabajo creó una aplicación de Teams que usa [pestañas](../build-your-first-app/build-personal-tab.md) para destacar información de contacto importante.</span><span class="sxs-lookup"><span data-stu-id="3d482-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="3d482-109">Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de ayuda.</span><span class="sxs-lookup"><span data-stu-id="3d482-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="3d482-110">Pero en lugar de llamar, ¿qué ocurre si los contactos pudieran ponerse en contacto con el servicio de soporte con un chatbot?</span><span class="sxs-lookup"><span data-stu-id="3d482-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="3d482-111">Su jefe le pide que vea la rapidez con la que puede obtener un bot de conversación básico en Funcionamiento en Teams.</span><span class="sxs-lookup"><span data-stu-id="3d482-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="3d482-112">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="3d482-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="3d482-113">Crear un proyecto de aplicación y un bot con Microsoft Teams Toolkit for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3d482-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="3d482-114">Identificar algunas de las configuraciones de aplicaciones y scaffolding relevantes para los bots</span><span class="sxs-lookup"><span data-stu-id="3d482-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="3d482-115">Hospedar una aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="3d482-115">Host an app locally</span></span>
> * <span data-ttu-id="3d482-116">Configurar un bot para Teams</span><span class="sxs-lookup"><span data-stu-id="3d482-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="3d482-117">Instalación de prueba y instalación de prueba de un bot en Teams</span><span class="sxs-lookup"><span data-stu-id="3d482-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3d482-118">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3d482-118">Before you begin</span></span>

<span data-ttu-id="3d482-119">Si aún no lo ha hecho, asegúrese de comprender [e instalar los requisitos previos de](build-first-app-overview.md#get-prerequisites)desarrollo de Teams.</span><span class="sxs-lookup"><span data-stu-id="3d482-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="3d482-120">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="3d482-120">1. Create your app project</span></span>

<span data-ttu-id="3d482-121">Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para su aplicación:</span><span class="sxs-lookup"><span data-stu-id="3d482-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="3d482-122">**Configuraciones de aplicaciones y scaffolding relevantes** para bots</span><span class="sxs-lookup"><span data-stu-id="3d482-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="3d482-123">**Bot** que se registra automáticamente con el servicio de bot de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3d482-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="3d482-124">Si no ha creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que le sea útil seguir estas instrucciones que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="3d482-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Crear una nueva aplicación :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: de **Teams.**
1. <span data-ttu-id="3d482-126">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="3d482-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="3d482-127">En la **pantalla Agregar funcionalidades,** seleccione **Bot** y, a **continuación, Siguiente.**</span><span class="sxs-lookup"><span data-stu-id="3d482-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="3d482-128">Escriba un nombre para su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="3d482-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="3d482-129">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="3d482-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="3d482-130">Vaya a **Configurar bot y** seleccione Crear un nuevo bot **y, a** continuación, cree el registro del **bot.**</span><span class="sxs-lookup"><span data-stu-id="3d482-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="3d482-131">Si se realiza correctamente, el nuevo bot tendrá el **estado Registrado.**</span><span class="sxs-lookup"><span data-stu-id="3d482-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="3d482-132">Seleccione **Finalizar** en la parte inferior de la pantalla y elija una ubicación para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3d482-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="3d482-133">2. Identificar componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="3d482-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="3d482-134">Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="3d482-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="3d482-135">Veamos los componentes principales para crear un bot.</span><span class="sxs-lookup"><span data-stu-id="3d482-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="3d482-136">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3d482-136">App configurations</span></span>

<span data-ttu-id="3d482-137">Para ver o actualizar las configuraciones del bot, seleccione **App Studio** en el kit de herramientas y vaya **a Bots.**</span><span class="sxs-lookup"><span data-stu-id="3d482-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="3d482-138">Scaffolding de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3d482-138">App scaffolding</span></span>

<span data-ttu-id="3d482-139">El scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar cómo el bot procesa las actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como `botActivityHandler.js` "Hola").</span><span class="sxs-lookup"><span data-stu-id="3d482-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="3d482-140">3. Configurar un túnel seguro para la aplicación</span><span class="sxs-lookup"><span data-stu-id="3d482-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="3d482-141">Con fines de prueba, vamos a hospedar la aplicación en un servidor web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="3d482-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="3d482-142">Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="3d482-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="3d482-143">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="3d482-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="3d482-144">Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ), ya que Teams requiere conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3d482-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="3d482-145">Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá túnel hasta donde hospeda la aplicación (en el puerto `localhost` 3978).</span><span class="sxs-lookup"><span data-stu-id="3d482-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="3d482-146">4. Configurar el bot</span><span class="sxs-lookup"><span data-stu-id="3d482-146">4. Configure your bot</span></span>

<span data-ttu-id="3d482-147">Para usar un bot en Teams, debe registrarlo con el servicio de bots de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d482-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="3d482-148">Para usted, esto se realiza automáticamente al configurar la aplicación con el Kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="3d482-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="3d482-149">Debe especificar una dirección de extremo para recibir y procesar mensajes de usuario (es decir, solicitudes) enviados al bot.</span><span class="sxs-lookup"><span data-stu-id="3d482-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="3d482-150">Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="3d482-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="3d482-151">Puedes configurarlo rápidamente en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="3d482-151">You can configure this quickly in the toolkit.</span></span>

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Abrir Microsoft :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: Teams **Toolkit.**
1. <span data-ttu-id="3d482-153">Vaya a **Bots > registros de bots existentes** y seleccione el bot que creó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="3d482-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="3d482-154">En el **campo de dirección** del extremo del bot, escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.</span><span class="sxs-lookup"><span data-stu-id="3d482-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del punto de conexión del bot en el Kit de herramientas de Teams.":::

<span data-ttu-id="3d482-156">El bot podrá responder a los mensajes en Teams.</span><span class="sxs-lookup"><span data-stu-id="3d482-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="3d482-157">5. Compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="3d482-157">5. Build and run your app</span></span>

<span data-ttu-id="3d482-158">Ha configurado una dirección URL para hospedar el bot y la ha configurado para que controle los mensajes.</span><span class="sxs-lookup"><span data-stu-id="3d482-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="3d482-159">Es el momento de que la aplicación esté en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="3d482-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="3d482-160">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="3d482-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="3d482-161">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="3d482-161">Run `npm start`.</span></span>

<span data-ttu-id="3d482-162">Si se realiza correctamente, verá el siguiente mensaje que indica que el bot está escuchando la actividad en `localhost` su:</span><span class="sxs-lookup"><span data-stu-id="3d482-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="3d482-163">6. Instalación local del bot en Teams</span><span class="sxs-lookup"><span data-stu-id="3d482-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="3d482-164">Con el bot en ejecución, puede instalarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="3d482-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="3d482-165">Si no ha descargado localmente una aplicación de Teams antes y tiene problemas, siga estas [instrucciones.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="3d482-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="3d482-166">En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="3d482-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="3d482-167">En el cuadro de diálogo de instalación de la aplicación, **seleccione Agregar para mí.**</span><span class="sxs-lookup"><span data-stu-id="3d482-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="3d482-168">(Puede agregar el bot a un canal o chat, pero es menos intrusivo para otros probar un bot en un chat uno a uno).</span><span class="sxs-lookup"><span data-stu-id="3d482-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="3d482-169">7. Probar el bot</span><span class="sxs-lookup"><span data-stu-id="3d482-169">7. Test your bot</span></span>

<span data-ttu-id="3d482-170">Ahora para la parte divertida: vamos a decir "Hola" al bot.</span><span class="sxs-lookup"><span data-stu-id="3d482-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="3d482-171">En el cuadro de redacción, envíe un `Hello` mensaje.</span><span class="sxs-lookup"><span data-stu-id="3d482-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="3d482-172">El bot responde con algo parecido al siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="3d482-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Captura de pantalla que muestra a un usuario decir &quot;Hola&quot; a un bot de Teams y obtener una respuesta.":::

## <a name="well-done"></a><span data-ttu-id="3d482-174">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="3d482-174">Well done</span></span>

<span data-ttu-id="3d482-175">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="3d482-175">Congratulations!</span></span> <span data-ttu-id="3d482-176">Tiene un bot básico de Teams que puede comunicarse con usuarios de uno en uno o en la configuración de grupo (canales y chats).</span><span class="sxs-lookup"><span data-stu-id="3d482-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3d482-177">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="3d482-177">Troubleshooting</span></span>

<span data-ttu-id="3d482-178">La siguiente información puede resultar útil si tiene problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3d482-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="3d482-179">El bot no está conectado a Teams</span><span class="sxs-lookup"><span data-stu-id="3d482-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="3d482-180">Si ha instalado la aplicación pero el bot no funciona, asegúrese de que el bot está conectado al canal de Teams del Servicio de [bots de Azure.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="3d482-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="3d482-181">Es importante comprender que esto no es lo mismo que un canal en Teams.</span><span class="sxs-lookup"><span data-stu-id="3d482-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="3d482-182">En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones de Microsoft o de [terceros compatible.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="3d482-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="3d482-183">Más información</span><span class="sxs-lookup"><span data-stu-id="3d482-183">Learn more</span></span>

* [<span data-ttu-id="3d482-184">Ver qué más pueden hacer los bots de Teams con uno de nuestros ejemplos</span><span class="sxs-lookup"><span data-stu-id="3d482-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="3d482-185">Conceptos básicos de las conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="3d482-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* <span data-ttu-id="3d482-186">Sigue nuestras [directrices de diseño](../bots/design/bots.md) y compila con [plantillas de interfaz](../concepts/design/design-teams-app-ui-templates.md) de usuario listas para producción para crear una experiencia sin problemas.</span><span class="sxs-lookup"><span data-stu-id="3d482-186">Follow our [design guidelines](../bots/design/bots.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="3d482-187">Autenticación de bots en Teams</span><span class="sxs-lookup"><span data-stu-id="3d482-187">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="3d482-188">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3d482-188">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="3d482-189">Crear un bot sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="3d482-189">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
