---
title: 'Introducción: compilación de una extensión de mensajería'
author: heath-hamilton
description: Cree rápidamente una extensión de mensajería de Microsoft Teams con el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 160878d92969d57680e6fa25eb6fc13e82bf2a82
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931753"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="1e622-103">Crear una extensión de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1e622-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="1e622-104">Hay dos tipos de *extensiones de mensajería* de la aplicación Teams: [comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) y comandos de [acciones](../messaging-extensions/how-to/action-commands/define-action-command.md).</span><span class="sxs-lookup"><span data-stu-id="1e622-104">There are two types of Teams app *messaging extensions* : [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="1e622-105">En esta lección, creará un *comando de búsqueda* (también conocido como *extensión de mensajería basada en búsquedas* ), que es un método abreviado para buscar contenido externo y compartirlo en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension* ), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="1e622-106">Los usuarios pueden tener acceso a los comandos de búsqueda desde el [cuadro redactar o comando de Teams](../messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="1e622-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="1e622-107">La asignación</span><span class="sxs-lookup"><span data-stu-id="1e622-107">Your assignment</span></span>

<span data-ttu-id="1e622-108">El Departamento de soporte técnico de su organización se comunica con los usuarios a través de Microsoft Teams, pero los vales residen en un sistema independiente.</span><span class="sxs-lookup"><span data-stu-id="1e622-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="1e622-109">Esto significa que el personal de soporte técnico debe volver y avanzar entre las aplicaciones constantemente.</span><span class="sxs-lookup"><span data-stu-id="1e622-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="1e622-110">Investigará cómo se puede reducir este gran cambio de contexto mediante la creación de una extensión de mensajería sencilla basada en búsquedas para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="1e622-111">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="1e622-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1e622-112">Crear un bot de extensión de mensajería y un proyecto de aplicación con el kit de herramientas de Microsoft Teams para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1e622-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="1e622-113">Identificar las configuraciones de la aplicación y algunos de los scaffolding relevantes para las extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="1e622-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="1e622-114">Hospedar una aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="1e622-114">Host an app locally</span></span>
> * <span data-ttu-id="1e622-115">Configurar el bot para la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="1e622-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="1e622-116">Transferir localmente y probar una extensión de mensajería en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1e622-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1e622-117">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="1e622-117">Before you begin</span></span>

<span data-ttu-id="1e622-118">Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="1e622-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="1e622-119">1. crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="1e622-119">1. Create your app project</span></span>

<span data-ttu-id="1e622-120">El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes para su extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="1e622-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="1e622-121">**Configuraciones de aplicación y scaffolding** relevantes para las extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="1e622-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="1e622-122">**Bot** para la extensión de mensajería que se registra automáticamente con el servicio de robots de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1e622-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="1e622-123">Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="1e622-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. <span data-ttu-id="1e622-125">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e622-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="1e622-126">En la pantalla **Agregar funcionalidad** , seleccione **extensión de mensajería** y, a continuación, **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e622-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="1e622-127">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="1e622-128">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="1e622-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="1e622-129">En la pantalla **configurar la extensión de mensajería** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1e622-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="1e622-130">Elija solo la opción **basada en búsquedas** para el tipo de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1e622-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="1e622-131">Seleccione **crear un nuevo bot** y, a continuación, **cree un registro de bot**.</span><span class="sxs-lookup"><span data-stu-id="1e622-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="1e622-132">Si se ejecuta correctamente, el nuevo bot tendrá un estado **registrado** .</span><span class="sxs-lookup"><span data-stu-id="1e622-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="1e622-133">Por ahora, seleccione **no** para la opción vincular unfurling.</span><span class="sxs-lookup"><span data-stu-id="1e622-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="1e622-134">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e622-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="1e622-135">2. identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="1e622-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="1e622-136">Una gran parte de la configuración de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="1e622-137">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1e622-137">App configurations</span></span>

<span data-ttu-id="1e622-138">Para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a **extensiones de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="1e622-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="1e622-139">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1e622-139">App scaffolding</span></span>

<span data-ttu-id="1e622-140">El scaffolding de la aplicación proporciona un `botActivityHandler.js` archivo, que se encuentra en el directorio raíz del proyecto, para controlar cómo su extensión de mensajería (técnicamente, el [Bot de la extensión de mensajería](#4-configure-the-bot-for-your-messaging-extension)) responde a las consultas de búsqueda en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="1e622-141">3. configurar un túnel seguro a la aplicación</span><span class="sxs-lookup"><span data-stu-id="1e622-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="1e622-142">Para fines de prueba, vamos a hospedar su extensión de mensajería en un servidor Web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="1e622-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="1e622-143">Si todavía no lo ha hecho, instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="1e622-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="1e622-144">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="1e622-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="1e622-145">Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ), ya que Teams requiere conexiones https.</span><span class="sxs-lookup"><span data-stu-id="1e622-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="1e622-146">Con esta dirección URL, Teams (que requiere Conexiones HTTPS) podrá canalizar a donde se hospeda la aplicación ( `localhost` en el puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="1e622-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="1e622-147">4. configurar el bot para la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="1e622-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="1e622-148">Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario de Microsoft Teams en el servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="1e622-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="1e622-149">El bot debe estar registrado en el servicio de bot de Azure, que se ha realizado al configurar la aplicación con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="1e622-150">Todavía debe especificar una dirección URL de punto de conexión de bot para recibir y procesar consultas de búsqueda en su extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1e622-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="1e622-151">Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="1e622-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="1e622-152">Puede configurar esto rápidamente en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="1e622-152">You can configure this quickly in the toolkit.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. <span data-ttu-id="1e622-154">Vaya a **Bots > registros de bot existentes** y seleccione el bot que creó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="1e622-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="1e622-155">En el campo **dirección del extremo del bot** , escriba la dirección URL de ngrok (por ejemplo, `https://468b9ab725e9.ngrok.io` ) donde hospeda el bot y agréguelo `/api/messages` a él.</span><span class="sxs-lookup"><span data-stu-id="1e622-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="1e622-156">El bot podrá controlar las consultas en su extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1e622-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="1e622-157">5. compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="1e622-157">5. Build and run your app</span></span>

<span data-ttu-id="1e622-158">Configuró una dirección URL para hospedar la extensión de mensajería y configurarla para controlar las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="1e622-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="1e622-159">Es el momento de poner en marcha su aplicación.</span><span class="sxs-lookup"><span data-stu-id="1e622-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="1e622-160">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="1e622-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="1e622-161">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="1e622-161">Run `npm start`.</span></span>

<span data-ttu-id="1e622-162">Si se ejecuta correctamente, verá el siguiente mensaje que indica que el servicio de extensiones de mensajería está escuchando la actividad en `localhost` :</span><span class="sxs-lookup"><span data-stu-id="1e622-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="1e622-163">6. transferir localmente la extensión de mensajería en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1e622-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="1e622-164">Con la extensión de mensajería en ejecución, puede instalarla en Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="1e622-165">Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="1e622-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="1e622-166">En Visual Studio Code, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="1e622-167">En el cuadro de diálogo de instalación de la aplicación, seleccione **Agregar a mí**.</span><span class="sxs-lookup"><span data-stu-id="1e622-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="1e622-168">7. probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="1e622-168">7. Test your messaging extension</span></span>

<span data-ttu-id="1e622-169">Obtenga información sobre cómo funcionan las extensiones de mensajería en un chat de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="1e622-170">Inicie un nuevo chat.</span><span class="sxs-lookup"><span data-stu-id="1e622-170">Start a new chat.</span></span> En el cuadro redactar, seleccione **más** :::image type="icon" source="../assets/icons/teams-client-more.png"::: y elija la aplicación de extensión de mensajería que acaba de transferirá localmente.
1. <span data-ttu-id="1e622-172">Intente buscar algo (por ejemplo, **vales** ).</span><span class="sxs-lookup"><span data-stu-id="1e622-172">Try searching for something (for example, **Tickets** ).</span></span> <span data-ttu-id="1e622-173">Si la aplicación funciona, verá los resultados de la búsqueda de ejemplo (puede Agregar los suyos propios más adelante).</span><span class="sxs-lookup"><span data-stu-id="1e622-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Una captura de pantalla que muestra cómo se usa una extensión de mensajería basada en búsquedas en el cuadro de redacción de Teams.":::

## <a name="well-done"></a><span data-ttu-id="1e622-175">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="1e622-175">Well done</span></span>

<span data-ttu-id="1e622-176">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="1e622-176">Congratulations!</span></span> <span data-ttu-id="1e622-177">Tiene una extensión de mensajería básica de teams que está configurada para buscar contenido externo en el cuadro de redacción o comando.</span><span class="sxs-lookup"><span data-stu-id="1e622-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e622-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e622-178">Next steps</span></span>

<span data-ttu-id="1e622-179">Vea las siguientes páginas para continuar y crear una extensión de mensajería con características completas:</span><span class="sxs-lookup"><span data-stu-id="1e622-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="1e622-180">[Definir los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) relevantes para el servicio.</span><span class="sxs-lookup"><span data-stu-id="1e622-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="1e622-181">Configurar el servicio para que [responda a las búsquedas de los usuarios](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="1e622-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1e622-182">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="1e622-182">Troubleshooting</span></span>

<span data-ttu-id="1e622-183">La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1e622-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="1e622-184">Bot no está conectado a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1e622-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="1e622-185">Si ha instalado la aplicación pero no funciona, asegúrese de que el bot de la extensión de mensajería esté [conectado al *canal* de Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="1e622-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="1e622-186">Es importante comprender que no es lo mismo que un canal en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1e622-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="1e622-187">En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="1e622-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="1e622-188">Más información</span><span class="sxs-lookup"><span data-stu-id="1e622-188">Learn more</span></span>

* [<span data-ttu-id="1e622-189">Incluir una característica de unfurling de vínculos</span><span class="sxs-lookup"><span data-stu-id="1e622-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="1e622-190">Agregar autenticación</span><span class="sxs-lookup"><span data-stu-id="1e622-190">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="1e622-191">Crear una extensión de mensajería basada en acciones</span><span class="sxs-lookup"><span data-stu-id="1e622-191">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="1e622-192">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="1e622-192">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
