---
title: 'Introducción: compilación de una extensión de mensajería'
author: heath-hamilton
description: Cree rápidamente una extensión de mensajería de Microsoft Teams con el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: b19856eacee866ebbc89f21ac12575f1392918b3
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452837"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="3488a-103">Crear una extensión de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3488a-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="3488a-104">Hay dos tipos de extensiones de *Mensajería*de Teams: [comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) y [comandos de acciones](../messaging-extensions/how-to/action-commands/define-action-command.md).</span><span class="sxs-lookup"><span data-stu-id="3488a-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="3488a-105">En esta lección, creará un *comando de búsqueda* (también conocido como *extensión de mensajería basada en búsquedas*), que es un método abreviado para buscar contenido externo y compartirlo en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="3488a-106">Los usuarios pueden tener acceso a los comandos de búsqueda desde el [cuadro redactar o comando de Teams](../messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="3488a-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="3488a-107">La asignación</span><span class="sxs-lookup"><span data-stu-id="3488a-107">Your assignment</span></span>

<span data-ttu-id="3488a-108">El Departamento de soporte técnico de su organización se comunica con los usuarios a través de Microsoft Teams, pero los vales residen en un sistema independiente.</span><span class="sxs-lookup"><span data-stu-id="3488a-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="3488a-109">Esto significa que el personal de soporte técnico debe volver y avanzar entre las aplicaciones constantemente.</span><span class="sxs-lookup"><span data-stu-id="3488a-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="3488a-110">Investigará cómo se puede reducir este gran cambio de contexto mediante la creación de una extensión de mensajería sencilla basada en búsquedas para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="3488a-111">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="3488a-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="3488a-112">Crear un bot de extensión de mensajería y un proyecto de aplicación con el kit de herramientas de Microsoft Teams para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3488a-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="3488a-113">Identificar las propiedades del manifiesto de la aplicación y algunos de los scaffolding relevantes para las extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="3488a-113">Identify the app manifest properties and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="3488a-114">Hospedar una aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="3488a-114">Host an app locally</span></span>
> * <span data-ttu-id="3488a-115">Configurar el bot para la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3488a-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="3488a-116">Transferir localmente y probar una extensión de mensajería en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3488a-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3488a-117">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3488a-117">Before you begin</span></span>

<span data-ttu-id="3488a-118">Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="3488a-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="3488a-119">1. crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="3488a-119">1. Create your app project</span></span>

<span data-ttu-id="3488a-120">El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes para su extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="3488a-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="3488a-121">**Manifiesto de la aplicación y scaffolding** relevantes para las extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="3488a-121">**App manifest and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="3488a-122">**Bot** para la extensión de mensajería que se registra automáticamente con el servicio de robots de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3488a-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="3488a-123">Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="3488a-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. <span data-ttu-id="3488a-125">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="3488a-126">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="3488a-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="3488a-127">En la pantalla **Agregar funcionalidad** , seleccione **extensión de mensajería** y, a continuación, **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3488a-127">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="3488a-128">En la pantalla **configurar la extensión de mensajería** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3488a-128">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="3488a-129">Elija solo la opción **basada en búsquedas** para el tipo de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3488a-129">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="3488a-130">Seleccione **crear un nuevo bot** e **iniciar sesión** para iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3488a-130">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span>
    1. <span data-ttu-id="3488a-131">Almacene el identificador y la contraseña de su Bot (necesita esto un poco más adelante).</span><span class="sxs-lookup"><span data-stu-id="3488a-131">Store your bot ID and password (you need this a little later).</span></span>
    1. <span data-ttu-id="3488a-132">Opcional Escriba un nombre personalizado para el bot y seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="3488a-132">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="3488a-133">(No es el nombre de la aplicación de teams que ya ha especificado.)</span><span class="sxs-lookup"><span data-stu-id="3488a-133">(This is not the name of the Teams app you already specified.)</span></span>
    1. <span data-ttu-id="3488a-134">Por ahora, seleccione **no** para la opción vincular unfurling.</span><span class="sxs-lookup"><span data-stu-id="3488a-134">For now, select **No** for the link unfurling option.</span></span></br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot para la extensión de mensajería.":::
1. <span data-ttu-id="3488a-136">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3488a-136">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="3488a-137">2. identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="3488a-137">2. Identify relevant app project components</span></span>

<span data-ttu-id="3488a-138">La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-138">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="3488a-139">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3488a-139">App manifest</span></span>

<span data-ttu-id="3488a-140">El siguiente fragmento de código del manifiesto de la aplicación (el `manifest.json` archivo del `.publish` directorio del proyecto) muestra las propiedades y los valores predeterminados relevantes para las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3488a-140">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to messaging extensions.</span></span>

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

<span data-ttu-id="3488a-141">Vamos a comprender algunas de las propiedades creadas por el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="3488a-141">Let's understand some of the properties the toolkit created for you.</span></span> <span data-ttu-id="3488a-142">(Vea la lista completa de propiedades admitidas [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) ).</span><span class="sxs-lookup"><span data-stu-id="3488a-142">(See the full list of supported [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) properties.)</span></span>

* <span data-ttu-id="3488a-143">`botId`: El identificador del robot que ha creado configurando su proyecto.</span><span class="sxs-lookup"><span data-stu-id="3488a-143">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="3488a-144">(Almacenado en `{botId0}` , puede encontrar el identificador real en `Development.env` ).</span><span class="sxs-lookup"><span data-stu-id="3488a-144">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="3488a-145">`commands`: Comandos disponibles para la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3488a-145">`commands`: Available commands for the messaging extension.</span></span> <span data-ttu-id="3488a-146">El kit de herramientas le proporciona scaffolding para un comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3488a-146">The toolkit provided you scaffolding for a search command.</span></span>
* <span data-ttu-id="3488a-147">`context`: Donde los usuarios pueden invocar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3488a-147">`context`: Where users can invoke the messaging extension.</span></span> <span data-ttu-id="3488a-148">En este caso, puede iniciar la extensión de mensajería desde el cuadro redactar o comando de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-148">In this case, you can launch the messaging extension from the Teams compose or command box.</span></span>
* <span data-ttu-id="3488a-149">`description`: Texto de la ayuda de la interfaz de usuario que indica lo que hace el comando o cómo usarlo.</span><span class="sxs-lookup"><span data-stu-id="3488a-149">`description`: UI help text indicating what the command does or how to use it.</span></span>
* <span data-ttu-id="3488a-150">`parameters`: Incluye todos los parámetros que acepta un comando (debe tener al menos un y puede tener hasta cinco).</span><span class="sxs-lookup"><span data-stu-id="3488a-150">`parameters`: Includes all parameters a command accepts (you must have at least one and can have up to five).</span></span>
* <span data-ttu-id="3488a-151">`parameters.description`: Texto de ayuda de interfaz de usuario que describe el propósito del parámetro o la entrada de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3488a-151">`parameters.description`: UI help text describing the parameter's purpose or example input.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="3488a-152">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3488a-152">App scaffolding</span></span>

<span data-ttu-id="3488a-153">La aplicación scaffolding incluye un `.env` archivo, ubicado en el directorio raíz del proyecto, que almacena el identificador y la contraseña del bot de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3488a-153">The app scaffolding includes a `.env` file, located in the root directory of your project, which stores the ID and password of your messaging extension's bot.</span></span>

<span data-ttu-id="3488a-154">También en el directorio raíz hay un `botActivityHandler.js` archivo para controlar cómo su extensión de mensajería (técnicamente, el [Bot de la extensión de mensajería](#4-configure-the-bot-for-your-messaging-extension)) responde a las consultas de búsqueda en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-154">Also in the root directory, there's a `botActivityHandler.js` file for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="3488a-155">3. configurar un túnel seguro a la aplicación</span><span class="sxs-lookup"><span data-stu-id="3488a-155">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="3488a-156">Para fines de prueba, vamos a hospedar su extensión de mensajería en un servidor Web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="3488a-156">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="3488a-157">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="3488a-157">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="3488a-158">Copie la dirección URL HTTPS en el resultado, ya que Teams requiere Conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3488a-158">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="3488a-159">En el `.publish` directorio, Abra `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="3488a-159">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="3488a-160">Reemplace el `baseUrl0` valor por la dirección URL copiada.</span><span class="sxs-lookup"><span data-stu-id="3488a-160">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="3488a-161">(Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ca5.ngrok.io` ).</span><span class="sxs-lookup"><span data-stu-id="3488a-161">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="3488a-162">El manifiesto de la aplicación apunta al lugar donde se hospeda el bot usado por la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3488a-162">Your app manifest is pointing to where you're hosting the bot used by the messaging extension.</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="3488a-163">4. configurar el bot para la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3488a-163">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="3488a-164">Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario de Microsoft Teams en el servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="3488a-164">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span>

<span data-ttu-id="3488a-165">El bot debe estar registrado en el servicio de bot de Azure, que se ha realizado al configurar la aplicación con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-165">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

### <a name="specify-your-bot-id-and-password"></a><span data-ttu-id="3488a-166">Especificar el identificador de robot y la contraseña</span><span class="sxs-lookup"><span data-stu-id="3488a-166">Specify your bot ID and password</span></span>

<span data-ttu-id="3488a-167">Cuando se registra el bot con el servicio de robots de Azure, se le asigna un identificador y una contraseña que la aplicación de Teams debe conocer.</span><span class="sxs-lookup"><span data-stu-id="3488a-167">When your bot is registered with the Azure Bot Service, it's assigned an ID and password that your Teams app must know about.</span></span>

1. <span data-ttu-id="3488a-168">Busque el identificador de robot y la contraseña que almacenó durante la instalación del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="3488a-168">Locate the bot ID and password you stored during toolkit setup.</span></span>
1. <span data-ttu-id="3488a-169">En el directorio raíz, abra el `.env` archivo.</span><span class="sxs-lookup"><span data-stu-id="3488a-169">In your root directory, open the `.env` file.</span></span>
1. <span data-ttu-id="3488a-170">Establezca el identificador y la contraseña de bot en las `BotId` `BotPassword` propiedades y, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="3488a-170">Set your bot ID and password to the `BotId` and `BotPassword` properties, respectively.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="3488a-171">Agregar la dirección de punto de conexión de bot</span><span class="sxs-lookup"><span data-stu-id="3488a-171">Add the bot endpoint address</span></span>

<span data-ttu-id="3488a-172">Debe especificar una dirección URL de punto de conexión de bot para recibir y procesar consultas de búsqueda en su extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3488a-172">You must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="3488a-173">Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="3488a-173">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="3488a-174">Puede configurar esto rápidamente en el kit de herramientas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-174">You can configure this quickly in the Teams Toolkit.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. <span data-ttu-id="3488a-176">Vaya a **Administración de bot > registros de bot existentes** y seleccione el bot que creó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="3488a-176">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="3488a-177">En el campo **dirección de extremo del bot** , escriba el servidor Web local en el que hospeda el bot ( `baseUrl10` valor) y agréguelo `/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="3488a-177">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot (`baseUrl10` value) and append `/api/messages` to it.</span></span>

<span data-ttu-id="3488a-178">El bot podrá controlar las consultas en su extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3488a-178">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-run-your-app"></a><span data-ttu-id="3488a-179">5. ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="3488a-179">5. Run your app</span></span>

<span data-ttu-id="3488a-180">Configuró una dirección URL para hospedar la extensión de mensajería y configurarla para controlar las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="3488a-180">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="3488a-181">Es el momento de poner en marcha su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3488a-181">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="3488a-182">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="3488a-182">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="3488a-183">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="3488a-183">Run `npm start`.</span></span>

<span data-ttu-id="3488a-184">Si se ejecuta correctamente, verá algo parecido al siguiente mensaje que indica que el servicio de extensiones de mensajería está escuchando la actividad en `localhost` :</span><span class="sxs-lookup"><span data-stu-id="3488a-184">If successful, you see something like the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="3488a-185">6. transferir localmente la extensión de mensajería en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3488a-185">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="3488a-186">Con la extensión de mensajería en ejecución, puede instalarla en Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-186">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="3488a-187">Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="3488a-187">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="3488a-188">Inicie sesión en el cliente de Teams con su cuenta que permite la transferencia local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3488a-188">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="3488a-189">Seleccione **aplicaciones**y, después, elija **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="3488a-189">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="3488a-190">Vaya a la carpeta de proyecto de la aplicación `.publish` y seleccione `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="3488a-190">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="3488a-191">En el modal instalar, seleccione **Agregar** para instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3488a-191">In the install modal, select **Add** to install your app.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="3488a-192">7. probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3488a-192">7. Test your messaging extension</span></span>

<span data-ttu-id="3488a-193">Obtenga información sobre cómo funcionan las extensiones de mensajería en un chat de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-193">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="3488a-194">Inicie un nuevo chat.</span><span class="sxs-lookup"><span data-stu-id="3488a-194">Start a new chat.</span></span> En el cuadro de redacción, seleccione **más** :::image type="icon" source="../assets/icons/teams-client-more.png"::: y elija la aplicación de extensión de mensajería que acaba de transferirá localmente.<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot para la extensión de mensajería.":::
1. <span data-ttu-id="3488a-197">Intente buscar algo (por ejemplo, "vales").</span><span class="sxs-lookup"><span data-stu-id="3488a-197">Try searching for something (for example, "Tickets").</span></span> <span data-ttu-id="3488a-198">Si la aplicación funciona, verá los resultados de la búsqueda de ejemplo (puede Agregar los suyos propios más adelante).</span><span class="sxs-lookup"><span data-stu-id="3488a-198">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot para la extensión de mensajería.":::

## <a name="well-done"></a><span data-ttu-id="3488a-200">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="3488a-200">Well done</span></span>

<span data-ttu-id="3488a-201">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="3488a-201">Congratulations!</span></span> <span data-ttu-id="3488a-202">Tiene una extensión de mensajería básica de teams que está configurada para buscar contenido externo en el cuadro de redacción o comando.</span><span class="sxs-lookup"><span data-stu-id="3488a-202">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3488a-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3488a-203">Next steps</span></span>

<span data-ttu-id="3488a-204">Vea las siguientes páginas para continuar y crear una extensión de mensajería con características completas:</span><span class="sxs-lookup"><span data-stu-id="3488a-204">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="3488a-205">[Definir los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) relevantes para el servicio.</span><span class="sxs-lookup"><span data-stu-id="3488a-205">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="3488a-206">Configurar el servicio para que [responda a las búsquedas de los usuarios](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="3488a-206">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3488a-207">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="3488a-207">Troubleshooting</span></span>

<span data-ttu-id="3488a-208">La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3488a-208">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="3488a-209">Error en la instalación del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="3488a-209">Toolkit setup fails</span></span>

<span data-ttu-id="3488a-210">Al configurar el proyecto de la aplicación con Team Toolkit, obtiene un error después de seleccionar la opción **crear un nuevo bot** e iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3488a-210">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="3488a-211">Podría ser un problema de autenticación.</span><span class="sxs-lookup"><span data-stu-id="3488a-211">This could be an authentication issue.</span></span> <span data-ttu-id="3488a-212">Siga estos pasos para finalizar la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3488a-212">Follow these steps to finish setting up your project.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **Cerrar sesión**.
1. <span data-ttu-id="3488a-214">Vuelva a pasar por el proceso de instalación iniciando sesión con la misma cuenta y creando un nuevo bot.</span><span class="sxs-lookup"><span data-stu-id="3488a-214">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="3488a-215">Bot no está conectado a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3488a-215">Bot isn't connected to Teams</span></span>

<span data-ttu-id="3488a-216">Si ha instalado la aplicación pero no funciona, asegúrese de que el bot de la extensión de mensajería esté [conectado al *canal*de Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="3488a-216">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="3488a-217">Es importante comprender que no es lo mismo que un canal en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3488a-217">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="3488a-218">En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="3488a-218">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="3488a-219">Más información</span><span class="sxs-lookup"><span data-stu-id="3488a-219">Learn more</span></span>

* [<span data-ttu-id="3488a-220">Incluir una característica de unfurling de vínculos</span><span class="sxs-lookup"><span data-stu-id="3488a-220">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="3488a-221">Agregar autenticación</span><span class="sxs-lookup"><span data-stu-id="3488a-221">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="3488a-222">Crear una extensión de mensajería basada en acciones</span><span class="sxs-lookup"><span data-stu-id="3488a-222">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="3488a-223">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="3488a-223">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
