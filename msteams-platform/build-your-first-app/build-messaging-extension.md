---
title: 'Introducción: crear una extensión de mensajería'
author: heath-hamilton
description: Cree rápidamente una extensión de mensajería de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 86d44740feaa2cd33aff0e1dde14d757420d90d6
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911922"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="4e274-103">Crear una extensión de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4e274-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="4e274-104">Hay dos tipos de extensiones de mensajería *de aplicaciones de* Teams: comandos de búsqueda [y](../messaging-extensions/how-to/search-commands/define-search-command.md) comandos [de acción.](../messaging-extensions/how-to/action-commands/define-action-command.md)</span><span class="sxs-lookup"><span data-stu-id="4e274-104">There are two types of Teams app *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="4e274-105">En esta lección, creará un comando de búsqueda *(también* conocido como extensión de mensajería basada en *búsquedas),* que es un acceso directo para buscar contenido externo y compartirlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="4e274-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="4e274-106">Los usuarios pueden obtener acceso a los comandos de búsqueda desde el cuadro [de redacción o comando de Teams.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="4e274-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="4e274-107">Su asignación</span><span class="sxs-lookup"><span data-stu-id="4e274-107">Your assignment</span></span>

<span data-ttu-id="4e274-108">El servicio de ayuda de su organización se comunica con los usuarios a través de Teams, pero los vales residen en un sistema independiente.</span><span class="sxs-lookup"><span data-stu-id="4e274-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="4e274-109">Esto significa que el personal de soporte técnico debe ir de una aplicación a otra constantemente.</span><span class="sxs-lookup"><span data-stu-id="4e274-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="4e274-110">Investigará cómo puede reducir este cambio de contexto creando una extensión de mensajería sencilla basada en búsquedas para Teams.</span><span class="sxs-lookup"><span data-stu-id="4e274-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="4e274-111">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="4e274-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="4e274-112">Crear un proyecto de aplicación y un bot de extensión de mensajería con Microsoft Teams Toolkit para Visual Studio código</span><span class="sxs-lookup"><span data-stu-id="4e274-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="4e274-113">Identificar las configuraciones de la aplicación y algunos de los scaffolding relevantes para las extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="4e274-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="4e274-114">Hospedar una aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="4e274-114">Host an app locally</span></span>
> * <span data-ttu-id="4e274-115">Configurar el bot para la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="4e274-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="4e274-116">Instalación de prueba y instalación de prueba de una extensión de mensajería en Teams</span><span class="sxs-lookup"><span data-stu-id="4e274-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4e274-117">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4e274-117">Before you begin</span></span>

<span data-ttu-id="4e274-118">Si aún no lo ha hecho, asegúrese de comprender [e instalar los requisitos previos de](build-first-app-overview.md#get-prerequisites)desarrollo de Teams.</span><span class="sxs-lookup"><span data-stu-id="4e274-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="4e274-119">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="4e274-119">1. Create your app project</span></span>

<span data-ttu-id="4e274-120">Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="4e274-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="4e274-121">**Configuraciones de aplicaciones y scaffolding relevantes** para extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="4e274-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="4e274-122">**Bot** para la extensión de mensajería que se registra automáticamente con el servicio de bots de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4e274-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="4e274-123">Si no ha creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que le sea útil seguir estas instrucciones que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="4e274-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Crear una nueva aplicación :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: de **Teams.**
1. <span data-ttu-id="4e274-125">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="4e274-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="4e274-126">En la pantalla **Agregar funcionalidades,** seleccione **Extensión de mensajería y,** a **continuación, Siguiente.**</span><span class="sxs-lookup"><span data-stu-id="4e274-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="4e274-127">Escriba un nombre para su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="4e274-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="4e274-128">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="4e274-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="4e274-129">En la **pantalla Configurar extensión de** mensajería, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4e274-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="4e274-130">Elija solo la **opción basada en** búsqueda para el tipo de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="4e274-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="4e274-131">Seleccione **Crear un nuevo bot y,** a **continuación, crear registro de bot.**</span><span class="sxs-lookup"><span data-stu-id="4e274-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="4e274-132">Si se realiza correctamente, el nuevo bot tendrá el **estado Registrado.**</span><span class="sxs-lookup"><span data-stu-id="4e274-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="4e274-133">Por ahora, seleccione **No para** la opción de desenlazaje de vínculos.</span><span class="sxs-lookup"><span data-stu-id="4e274-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="4e274-134">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4e274-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="4e274-135">2. Identificar componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="4e274-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="4e274-136">Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="4e274-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="4e274-137">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4e274-137">App configurations</span></span>

<span data-ttu-id="4e274-138">Para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a Extensiones **de mensajería.**</span><span class="sxs-lookup"><span data-stu-id="4e274-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="4e274-139">Scaffolding de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4e274-139">App scaffolding</span></span>

<span data-ttu-id="4e274-140">El scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar cómo responde la extensión de mensajería (o técnicamente, el bot de la extensión de mensajería) a las consultas de búsqueda en `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="4e274-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="4e274-141">3. Configurar un túnel seguro para la aplicación</span><span class="sxs-lookup"><span data-stu-id="4e274-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="4e274-142">Para realizar pruebas, vamos a hospedar la extensión de mensajería en un servidor web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="4e274-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="4e274-143">Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="4e274-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="4e274-144">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="4e274-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="4e274-145">Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ), ya que Teams requiere conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4e274-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="4e274-146">Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá túnel hasta donde hospeda la aplicación ( en el puerto `localhost` 3978).</span><span class="sxs-lookup"><span data-stu-id="4e274-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="4e274-147">4. Configurar el bot para la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="4e274-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="4e274-148">Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario de Teams a su servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="4e274-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="4e274-149">El bot debe estar registrado con el Servicio de bots de Azure, que se ha realizado al configurar la aplicación con Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="4e274-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="4e274-150">Debe especificar una dirección URL de extremo de bot para recibir y procesar consultas de búsqueda en la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="4e274-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="4e274-151">Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="4e274-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="4e274-152">Puedes configurarlo rápidamente en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="4e274-152">You can configure this quickly in the toolkit.</span></span>

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Abrir Microsoft :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: Teams **Toolkit.**
1. <span data-ttu-id="4e274-154">Vaya a **Bots > registros de bots existentes** y seleccione el bot que creó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="4e274-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="4e274-155">En el **campo de dirección** del extremo del bot, escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.</span><span class="sxs-lookup"><span data-stu-id="4e274-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="4e274-156">El bot podrá controlar las consultas en la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="4e274-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="4e274-157">5. Compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="4e274-157">5. Build and run your app</span></span>

<span data-ttu-id="4e274-158">Ha configurado una dirección URL para hospedar la extensión de mensajería y la ha configurado para controlar las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="4e274-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="4e274-159">Es el momento de que la aplicación esté en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="4e274-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="4e274-160">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="4e274-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="4e274-161">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="4e274-161">Run `npm start`.</span></span>

<span data-ttu-id="4e274-162">Si se realiza correctamente, verá el siguiente mensaje que indica que el servicio de extensión de mensajería está escuchando la actividad en `localhost` su:</span><span class="sxs-lookup"><span data-stu-id="4e274-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="4e274-163">6. Instalación local de la extensión de mensajería en Teams</span><span class="sxs-lookup"><span data-stu-id="4e274-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="4e274-164">Con la extensión de mensajería en ejecución, puede instalarla en Teams.</span><span class="sxs-lookup"><span data-stu-id="4e274-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="4e274-165">Si no ha descargado localmente una aplicación de Teams antes y tiene problemas, siga estas [instrucciones.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="4e274-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="4e274-166">En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="4e274-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="4e274-167">En el cuadro de diálogo de instalación de la aplicación, **seleccione Agregar para mí.**</span><span class="sxs-lookup"><span data-stu-id="4e274-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="4e274-168">7. Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="4e274-168">7. Test your messaging extension</span></span>

<span data-ttu-id="4e274-169">Obtenga información sobre cómo funcionan las extensiones de mensajería en un chat de Teams.</span><span class="sxs-lookup"><span data-stu-id="4e274-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="4e274-170">Inicie un nuevo chat.</span><span class="sxs-lookup"><span data-stu-id="4e274-170">Start a new chat.</span></span> En el cuadro de redacción, seleccione **Más** y elija la aplicación de extensión de :::image type="icon" source="../assets/icons/teams-client-more.png"::: mensajería que acaba de instalar localmente.
1. <span data-ttu-id="4e274-172">Intente buscar algo (por ejemplo, **Vales).**</span><span class="sxs-lookup"><span data-stu-id="4e274-172">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="4e274-173">Si la aplicación funciona, verá resultados de búsqueda de ejemplo (puede agregar los suyos más adelante).</span><span class="sxs-lookup"><span data-stu-id="4e274-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Captura de pantalla que muestra cómo se usa una extensión de mensajería basada en búsquedas en el cuadro de redacción de Teams.":::

## <a name="well-done"></a><span data-ttu-id="4e274-175">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="4e274-175">Well done</span></span>

<span data-ttu-id="4e274-176">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="4e274-176">Congratulations!</span></span> <span data-ttu-id="4e274-177">Tiene una extensión de mensajería básica de Teams que está configurada para buscar contenido externo en el cuadro de redacción o comando.</span><span class="sxs-lookup"><span data-stu-id="4e274-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e274-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e274-178">Next steps</span></span>

<span data-ttu-id="4e274-179">Vea las páginas siguientes para continuar y crear una extensión de mensajería completa:</span><span class="sxs-lookup"><span data-stu-id="4e274-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="4e274-180">[Defina los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) que sean relevantes para su servicio.</span><span class="sxs-lookup"><span data-stu-id="4e274-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="4e274-181">Configure el servicio para [que responda a las búsquedas de los usuarios.](../messaging-extensions/how-to/search-commands/respond-to-search.md)</span><span class="sxs-lookup"><span data-stu-id="4e274-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4e274-182">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="4e274-182">Troubleshooting</span></span>

<span data-ttu-id="4e274-183">La siguiente información puede resultar útil si tiene problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4e274-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="4e274-184">El bot no está conectado a Teams</span><span class="sxs-lookup"><span data-stu-id="4e274-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="4e274-185">Si ha instalado la aplicación pero no funciona, asegúrese de que el bot de la extensión de mensajería está conectado al canal de Teams del servicio de bot [de Azure. ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="4e274-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="4e274-186">Es importante comprender que esto no es lo mismo que un canal en Teams.</span><span class="sxs-lookup"><span data-stu-id="4e274-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="4e274-187">En este caso, un canal es cómo el servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones de Microsoft o de [terceros compatible.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="4e274-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="4e274-188">Más información</span><span class="sxs-lookup"><span data-stu-id="4e274-188">Learn more</span></span>

* [<span data-ttu-id="4e274-189">Incluir una característica de desenlazaje de vínculos</span><span class="sxs-lookup"><span data-stu-id="4e274-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* <span data-ttu-id="4e274-190">Sigue nuestras [directrices de diseño](../messaging-extensions/design/messaging-extension-design.md) y compila con [plantillas de interfaz](../concepts/design/design-teams-app-ui-templates.md) de usuario listas para producción para crear una experiencia sin problemas.</span><span class="sxs-lookup"><span data-stu-id="4e274-190">Follow our [design guidelines](../messaging-extensions/design/messaging-extension-design.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="4e274-191">Añadir autenticación</span><span class="sxs-lookup"><span data-stu-id="4e274-191">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="4e274-192">Crear una extensión de mensajería basada en acciones</span><span class="sxs-lookup"><span data-stu-id="4e274-192">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="4e274-193">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4e274-193">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
