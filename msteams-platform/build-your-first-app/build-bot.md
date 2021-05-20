---
title: Empezar - Crear un bot
author: girliemac
description: Cree rápidamente un bot Microsoft Teams utilizando el Microsoft Teams Toolkit.
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: 2cbd90b293e8ac8343febc7b3d23278d5bb5bf82
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565889"
---
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="9b1f6-103">Crea tu primer bot para Teams</span><span class="sxs-lookup"><span data-stu-id="9b1f6-103">Create your first bot for Teams</span></span>

<span data-ttu-id="9b1f6-104">En este tutorial se le enseña a crear una aplicación de bot básica.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="9b1f6-105">Un bot actúa como intermediario entre los usuarios Teams y la aplicación web o servicio con una interfaz conversacional.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="9b1f6-106">Las personas pueden chatear con un bot para obtener información rápidamente o iniciar flujos de trabajo y tareas realizadas por su servicio.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="9b1f6-107">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="9b1f6-107">What you'll learn</span></span>

* <span data-ttu-id="9b1f6-108">Cree un proyecto de aplicación y un bot con la Microsoft Teams Toolkit para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="9b1f6-109">Comprender las configuraciones de Teams aplicación relevantes para los bots.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="9b1f6-110">Hospede y ejecute una aplicación localmente mediante una solución de tunelización localhost.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="9b1f6-111">Descargue lateralmente y pruebe un bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b1f6-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b1f6-112">Prerequisites</span></span>

<span data-ttu-id="9b1f6-113">Asegúrese de comprender cómo configurar y crear una aplicación de Teams sencilla.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="9b1f6-114">Para obtener más información, consulta [crear tu primera aplicación Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="9b1f6-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="9b1f6-115">1. Cree el proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9b1f6-115">1. Create your app project</span></span>

<span data-ttu-id="9b1f6-116">El Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para la aplicación:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="9b1f6-117">**Configuraciones de aplicaciones y andamios** relevantes para bots.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-117">**App configurations and scaffolding** relevant to bots.</span></span>
* <span data-ttu-id="9b1f6-118">**Bot** que se registra automáticamente con el servicio de bots de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="9b1f6-119">**Para crear el proyecto de aplicación**</span><span class="sxs-lookup"><span data-stu-id="9b1f6-119">**To create your app project**</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividades izquierda y elija Crear una nueva aplicación **de Teams**.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Captura de pantalla que muestra cómo crear una aplicación en el Teams Toolkit.":::

1. <span data-ttu-id="9b1f6-122">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="9b1f6-123">En la pantalla Seleccionar proyecto, seleccione Bots de conversación:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Captura de pantalla que muestra cómo crear un nuevo bot en el Teams Toolkit.":::

1. <span data-ttu-id="9b1f6-125">En la pantalla **Configurar proyecto,** escriba un nombre para el bot.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="9b1f6-126">Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="9b1f6-127">Seleccione **Crear un nuevo registro** de  >  **bots de creación de bots** como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Captura de pantalla que muestra el nombre de nuevo bot en el Teams Toolkit.":::

    <span data-ttu-id="9b1f6-129">Si se realiza correctamente, el nuevo bot tendrá un estado **Registrado.**</span><span class="sxs-lookup"><span data-stu-id="9b1f6-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="9b1f6-130">Ahora el bot se registra automáticamente con el servicio de bots de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Captura de pantalla que muestra el registro de nuevo bot en el Teams Toolkit.":::

1. <span data-ttu-id="9b1f6-132">Seleccione **Finalizar** en la parte inferior de la pantalla y guarde el proyecto en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="9b1f6-133">2. Comprender los componentes del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9b1f6-133">2. Understand your app project components</span></span>

<span data-ttu-id="9b1f6-134">Gran parte de las configuraciones de la aplicación y los andamios se configuran automáticamente al crear el proyecto con el Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="9b1f6-135">Echemos un vistazo a los componentes principales para crear un bot:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Captura de pantalla que muestra un andamio de proyecto en el Teams Toolkit.":::

<span data-ttu-id="9b1f6-137">Si creó una pestaña en otro tutorial, el andamiaje de la aplicación para el bot es diferente.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="9b1f6-138">A diferencia de las pestañas, el desarrollo de bots no requiere que cree ningún componente web front-end ni utilice el SDK de cliente de JavaScript Teams.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="9b1f6-139">En su lugar, el andamio utiliza el [Microsoft Bot Framework](https://dev.botframework.com/), que es un SDK de código abierto para crear bots inteligentes de nivel empresarial que pueden funcionar en la web, móvil y, por supuesto, Teams!</span><span class="sxs-lookup"><span data-stu-id="9b1f6-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="9b1f6-140">El `botActivityHandler.js` archivo, ubicado en el directorio raíz del proyecto, es el controlador específico de Teams que controla las actividades del bot, como cómo responde el bot a mensajes específicos.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-140">The `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities, such as how the bot responds to specific messages.</span></span> <span data-ttu-id="9b1f6-141">El andamiaje de la aplicación proporciona un `botActivityHandler.js` archivo ubicado en el directorio raíz del proyecto, es el controlador específico Teams que controla las actividades del bot, como cómo responde el bot a mensajes específicos.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-141">The app scaffolding provides a `botActivityHandler.js` file located in the root directory of your project, is the Teams specific handler that handles bot activities such as how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="9b1f6-142">3. Exponga de forma segura su localhost a Internet</span><span class="sxs-lookup"><span data-stu-id="9b1f6-142">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="9b1f6-143">Eche un vistazo al `index.js` archivo, que crea un servidor HTTP y controla el enrutamiento para escuchar las solicitudes entrantes al bot.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-143">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="9b1f6-144">La `/api/messages` dirección URL del punto de conexión de la aplicación es la que responde a las solicitudes de cliente:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-144">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="9b1f6-145">Para reenviar las solicitudes a la lógica del bot, debe configurar una dirección URL de acceso público, como `https://example.com/api/messages` , en lugar de `https://localhost` .</span><span class="sxs-lookup"><span data-stu-id="9b1f6-145">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="9b1f6-146">Dado que la aplicación se está ejecutando desde el localhost actualmente, debe hacer *un túnel de* la red.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-146">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="9b1f6-147">La tunelización es un protocolo que le permite transportar datos a través de una red.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-147">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="9b1f6-148">Y la tunelización localhost le ofrece una conexión entre su máquina local y una conexión remota.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-148">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="9b1f6-149">Para exponer de forma segura su localhost a Internet, le recomendamos que utilice la herramienta 3rd party llamada **ngrok**.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-149">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="9b1f6-150">Esto le dará una URL segura.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-150">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="9b1f6-151">Vaya al sitio [de ngrok.com](https://ngrok.com/download) y siga las instrucciones para instalar y configurar ngrok en su entorno.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-151">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="9b1f6-152">Agregue la ruta completa al archivo ngrok.exe que instaló en la variable de entorno PATH del sistema.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-152">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="9b1f6-153">Los pasos exactos son específicos del shell que está utilizando.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-153">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="9b1f6-154">Una vez que haya terminado de configurarlo, abra un terminal y ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="9b1f6-154">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="9b1f6-155">Ahora ngrok le proporciona una dirección URL pública y segura que reenvía a su localhost en el puerto 3978, así que copie la dirección URL HTTPS, por ejemplo, `https://287a4f4223bc.ngrok.io` como se muestra en la captura de pantalla siguiente, ya que Teams requiere conexiones HTTPS:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-155">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Captura de pantalla que muestra la tunelización de localhost con ngrok.":::

1. <span data-ttu-id="9b1f6-157">Registre la dirección URL en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-157">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="9b1f6-158">4. Registre el punto final del bot</span><span class="sxs-lookup"><span data-stu-id="9b1f6-158">4. Register your bot endpoint</span></span>

<span data-ttu-id="9b1f6-159">Para usar un bot en Teams, debe registrarlo en Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-159">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="9b1f6-160">Esto se hace automáticamente cuando configuras la aplicación con la Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-160">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="9b1f6-161">Todavía debe especificar una dirección de punto de conexión para recibir y procesar mensajes de usuario o solicitudes enviadas al bot.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-161">You must still specify an endpoint address to receive and process user messages, or requests sent to the bot.</span></span> <span data-ttu-id="9b1f6-162">Normalmente, la dirección URL se parece `https://HOST_URL/api/messages` a .</span><span class="sxs-lookup"><span data-stu-id="9b1f6-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="9b1f6-163">Puede configurarlo en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-163">You can configure this in the toolkit.</span></span>

1. <span data-ttu-id="9b1f6-164">En Visual Studio Code, abra **Microsoft Teams Toolkit**.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-164">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="9b1f6-165">Seleccione **Bots**  >  **Registros de bots existentes** y seleccione el bot que creó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-165">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="9b1f6-166">En el campo **Dirección del punto de conexión del bot,** escriba la dirección URL de ngrok, por ejemplo, donde hospeda el bot y `https://287a4f4223bc.ngrok.io` `/api/messages` anexe a él:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-166">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Captura de pantalla que muestra cómo hacer un túnel localhost con ngrok.":::

    <span data-ttu-id="9b1f6-168">El bot podrá responder a los mensajes de Teams, después de configurar el punto de conexión correctamente.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-168">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="9b1f6-169">5. Compile y ejecute la aplicación</span><span class="sxs-lookup"><span data-stu-id="9b1f6-169">5. Build and run your app</span></span>

<span data-ttu-id="9b1f6-170">Ha configurado una dirección URL para hospedar el bot y lo ha configurado para controlar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="9b1f6-171">Es hora de poner en marcha la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-171">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="9b1f6-172">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="9b1f6-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="9b1f6-173">Ejecute `npm start`.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-173">Run `npm start`.</span></span>

   <span data-ttu-id="9b1f6-174">Si se realiza correctamente, verá el siguiente mensaje que indica que el bot está escuchando la actividad `localhost` en:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-174">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="9b1f6-175">6. Descargue su bot en Teams</span><span class="sxs-lookup"><span data-stu-id="9b1f6-175">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="9b1f6-176">Con el bot en ejecución, puede instalarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="9b1f6-177">Si no has descargado una aplicación Teams antes y te has quedado con problemas, sigue estas [instrucciones.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="9b1f6-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="9b1f6-178">En Visual Studio Code, seleccione la clave **F5** para iniciar un cliente web Teams.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-178">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="9b1f6-179">En el cuadro de diálogo de instalación de la aplicación, seleccione **Agregar para mí.**</span><span class="sxs-lookup"><span data-stu-id="9b1f6-179">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="9b1f6-180">De forma predeterminada, la aplicación se agrega a su mensaje de chat directo 1:1, sin embargo, puede optar por instalarlo en un equipo o chat haciendo clic en la pequeña flecha junto a **Agregar para mí.**</span><span class="sxs-lookup"><span data-stu-id="9b1f6-180">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="9b1f6-181">En este tutorial, vamos a hacer clic en Agregar.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-181">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Captura de pantalla que muestra túnel localhost con ngrok.":::

## <a name="7-test-your-bot"></a><span data-ttu-id="9b1f6-183">7. Pruebe su bot</span><span class="sxs-lookup"><span data-stu-id="9b1f6-183">7. Test your bot</span></span>

<span data-ttu-id="9b1f6-184">Digamos "Hola" a tu bot.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-184">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="9b1f6-185">En el cuadro de composición, envíe un `Hello` mensaje.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-185">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="9b1f6-186">El bot responde con algo como el siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="9b1f6-186">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Una captura de pantalla que muestra a un usuario decir 'Hola' a un bot de Teams y obtener una respuesta.":::

    <span data-ttu-id="9b1f6-188">Ahora ha creado un bot Teams básico que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats) 🎉.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-188">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉.</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="9b1f6-189">Solución de problemas del bot</span><span class="sxs-lookup"><span data-stu-id="9b1f6-189">Troubleshoot your bot</span></span>

<span data-ttu-id="9b1f6-190">La siguiente información puede ayudar si tuvo problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-190">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="9b1f6-191">Bot no está conectado a Teams</span><span class="sxs-lookup"><span data-stu-id="9b1f6-191">Bot isn't connected to Teams</span></span>


<span data-ttu-id="9b1f6-192">Si instaló la aplicación pero el bot no funciona, asegúrese de que el bot esté [conectado al *canal* de Teams del Servicio de bots de Azure.](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9b1f6-192">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="9b1f6-193">Es importante entender que esto no es lo mismo que un canal en Teams.</span><span class="sxs-lookup"><span data-stu-id="9b1f6-193">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="9b1f6-194">En este caso, un canal es cómo Azure Bot Service conecta el bot a Teams u otra [aplicación de comunicaciones compatible con Microsoft o de terceros.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9b1f6-194">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="9b1f6-195">Vea también</span><span class="sxs-lookup"><span data-stu-id="9b1f6-195">See also</span></span>

* [<span data-ttu-id="9b1f6-196">Conceptos básicos del bot</span><span class="sxs-lookup"><span data-stu-id="9b1f6-196">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="9b1f6-197">Construir una pestaña personal para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9b1f6-197">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="9b1f6-198">Vea qué más pueden hacer Teams bots con una de nuestras muestras</span><span class="sxs-lookup"><span data-stu-id="9b1f6-198">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="9b1f6-199">Conceptos básicos de las conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="9b1f6-199">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="9b1f6-200">Directrices de diseño</span><span class="sxs-lookup"><span data-stu-id="9b1f6-200">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="9b1f6-201">Plantillas de interfaz de usuario listas para producción</span><span class="sxs-lookup"><span data-stu-id="9b1f6-201">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="9b1f6-202">Autenticación de bots en Teams</span><span class="sxs-lookup"><span data-stu-id="9b1f6-202">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="9b1f6-203">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9b1f6-203">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="9b1f6-204">Crear un bot sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="9b1f6-204">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="9b1f6-205">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="9b1f6-205">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9b1f6-206">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="9b1f6-206">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
