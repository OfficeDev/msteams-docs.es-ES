---
title: Crear un bot de Teams
author: heath-hamilton
description: Obtenga información sobre cómo crear un bot para su primera aplicación de Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: cc004bd0d86eca1e4e63c2a96a72f9c11d2269db
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237828"
---
# <a name="build-a-teams-bot"></a><span data-ttu-id="71aef-103">Crear un bot de Teams</span><span class="sxs-lookup"><span data-stu-id="71aef-103">Build a Teams bot</span></span>

<span data-ttu-id="71aef-104">Compilará una aplicación de *Bot* básica en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="71aef-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="71aef-105">Un bot actúa como intermediario entre los usuarios de Microsoft Teams y el servicio Web.</span><span class="sxs-lookup"><span data-stu-id="71aef-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="71aef-106">Los usuarios pueden chatear con un bot para obtener información o iniciar flujos de trabajo y tareas realizados por el servicio de forma rápida.</span><span class="sxs-lookup"><span data-stu-id="71aef-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="71aef-107">La asignación</span><span class="sxs-lookup"><span data-stu-id="71aef-107">Your assignment</span></span>

<span data-ttu-id="71aef-108">El área de trabajo ha estado usando [pestañas](../build-your-first-app/build-personal-tab.md) para exponer la información de contacto importante en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-108">Your workplace has been using [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information in Teams.</span></span> <span data-ttu-id="71aef-109">Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de asistencia.</span><span class="sxs-lookup"><span data-stu-id="71aef-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="71aef-110">Pero, en lugar de llamar a, ¿qué sucede si los usuarios pueden ponerse en contacto con el Departamento de soporte mediante un Chatbot?</span><span class="sxs-lookup"><span data-stu-id="71aef-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="71aef-111">Su jefe le pedirá que consulte la velocidad con la que puede poner en marcha un bot de conversación básico en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="71aef-112">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="71aef-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="71aef-113">Crear un proyecto de aplicación y un bot con el kit de herramientas de Microsoft Teams para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="71aef-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="71aef-114">Identificar algunas de las propiedades del manifiesto de la aplicación y los scaffolding relevantes para los bots</span><span class="sxs-lookup"><span data-stu-id="71aef-114">Identify some of the app manifest properties and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="71aef-115">Hospedar una aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="71aef-115">Host an app locally</span></span>
> * <span data-ttu-id="71aef-116">Configurar un bot para Teams</span><span class="sxs-lookup"><span data-stu-id="71aef-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="71aef-117">Transferir localmente y probar un bot en Teams</span><span class="sxs-lookup"><span data-stu-id="71aef-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="71aef-118">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="71aef-118">Before you begin</span></span>

<span data-ttu-id="71aef-119">Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="71aef-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="71aef-120">1. crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="71aef-120">1. Create your app project</span></span>

<span data-ttu-id="71aef-121">El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="71aef-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="71aef-122">**Manifiesto de la aplicación y scaffolding** relevantes para bots</span><span class="sxs-lookup"><span data-stu-id="71aef-122">**App manifest and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="71aef-123">**Bot** que se registra automáticamente con el servicio de robots de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="71aef-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="71aef-124">Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="71aef-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. <span data-ttu-id="71aef-126">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-126">Enter a name for your Teams app.</span></span> <span data-ttu-id="71aef-127">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="71aef-127">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="71aef-128">En la pantalla **Agregar funciones** , seleccione **Bot** y, a continuación, **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="71aef-128">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="71aef-129">Seleccione **crear un nuevo bot** e **iniciar sesión** para iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="71aef-129">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span><br/>
:::image type="content" source="../assets/images/build-your-first-app/vsc-create-bot.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot.":::
1. <span data-ttu-id="71aef-131">Almacene el identificador y la contraseña de su Bot (necesita esto un poco más adelante).</span><span class="sxs-lookup"><span data-stu-id="71aef-131">Store your bot ID and password (you need this a little later).</span></span>
1. <span data-ttu-id="71aef-132">Opcional Escriba un nombre personalizado para el bot y seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="71aef-132">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="71aef-133">Recuerde que este es el nombre de su bot y no el nombre de la aplicación de teams que ya ha especificado.</span><span class="sxs-lookup"><span data-stu-id="71aef-133">(Remember, this is the name for your bot and not the name of the Teams app you already specified.)</span></span>
1. <span data-ttu-id="71aef-134">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="71aef-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="71aef-135">2. identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="71aef-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="71aef-136">La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-136">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="71aef-137">Echemos un vistazo a los componentes principales para crear un bot.</span><span class="sxs-lookup"><span data-stu-id="71aef-137">Let's look at the main components for building a bot.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="71aef-138">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="71aef-138">App manifest</span></span>

<span data-ttu-id="71aef-139">El siguiente fragmento de código del manifiesto de la aplicación (el `manifest.json` archivo del `.publish` directorio del proyecto) muestra las propiedades y los valores predeterminados pertinentes para los bots.</span><span class="sxs-lookup"><span data-stu-id="71aef-139">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to bots.</span></span>

```JSON
"bots": [
    {
        "botId": "{botId0}",
        "scopes": [
            "personal",
            "groupchat",
            "team"
        ],
        "supportsFiles": false,
        "isNotificationOnly": false,
        "commandLists": [
            {
                "scopes": [
                    "personal",
                    "groupchat",
                    "team"
                ],
                "commands": [
                    {
                        "title": "Hello",
                        "description": "Sends a hello message and @mention the sender"
                    }
                ]
            }
        ]
    }
],
```

<span data-ttu-id="71aef-140">Por ahora, vamos a centrarnos en las siguientes propiedades necesarias.</span><span class="sxs-lookup"><span data-stu-id="71aef-140">For now, let's just focus on the following required properties.</span></span> <span data-ttu-id="71aef-141">(Vea la lista completa de propiedades admitidas [`bots`](../resources/schema/manifest-schema.md#bots) ).</span><span class="sxs-lookup"><span data-stu-id="71aef-141">(See the full list of supported [`bots`](../resources/schema/manifest-schema.md#bots) properties.)</span></span>

* <span data-ttu-id="71aef-142">`botId`: El identificador del robot que ha creado configurando su proyecto.</span><span class="sxs-lookup"><span data-stu-id="71aef-142">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="71aef-143">(Almacenado en `{botId0}` , puede encontrar el identificador real en `Development.env` ).</span><span class="sxs-lookup"><span data-stu-id="71aef-143">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="71aef-144">`scopes`: Especifica si el bot está disponible en `personal` los `groupchat` `team` contextos,, o (por ejemplo, de canal).</span><span class="sxs-lookup"><span data-stu-id="71aef-144">`scopes`: Specifies if your bot is available in `personal`, `groupchat`, or `team` (i.e., channel) contexts.</span></span>
* <span data-ttu-id="71aef-145">`commands`: Comandos disponibles que los usuarios pueden enviar a su bot.</span><span class="sxs-lookup"><span data-stu-id="71aef-145">`commands`: Available commands users can send to your bot.</span></span>
* <span data-ttu-id="71aef-146">`title`: Nombre del comando bot que se muestra en el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-146">`title`: Bot command name that displays in the Teams client.</span></span>
* <span data-ttu-id="71aef-147">`description`: Una breve descripción o un ejemplo de la sintaxis y los argumentos para ayudar a los usuarios a comprender lo que hace un comando bot.</span><span class="sxs-lookup"><span data-stu-id="71aef-147">`description`: A short description or example of the syntax and arguments to help users understand what a bot command does.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="71aef-148">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="71aef-148">App scaffolding</span></span>

<span data-ttu-id="71aef-149">El scaffolding de la aplicación proporciona un `botActivityHandler.js` archivo, que se encuentra en el directorio raíz del proyecto, para controlar cómo el bot procesa las actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como "Hello").</span><span class="sxs-lookup"><span data-stu-id="71aef-149">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

<span data-ttu-id="71aef-150">El `.env` archivo, también en el directorio raíz, almacena el identificador de Bot y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="71aef-150">The `.env` file, also in the root directory, stores your bot ID and password.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="71aef-151">3. configurar un túnel seguro a la aplicación</span><span class="sxs-lookup"><span data-stu-id="71aef-151">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="71aef-152">Para fines de prueba, vamos a hospedar su bot en un servidor Web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="71aef-152">For testing purposes, let's host your bot on a local web server (port 3978).</span></span>

1. <span data-ttu-id="71aef-153">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="71aef-153">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="71aef-154">Copie la dirección URL HTTPS en el resultado, ya que Teams requiere Conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="71aef-154">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="71aef-155">En el `.publish` directorio, Abra `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="71aef-155">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="71aef-156">Reemplace el `baseUrl0` valor por la dirección URL copiada.</span><span class="sxs-lookup"><span data-stu-id="71aef-156">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="71aef-157">(Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ca5.ngrok.io` ).</span><span class="sxs-lookup"><span data-stu-id="71aef-157">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="71aef-158">El manifiesto de la aplicación apunta al lugar donde se hospeda el bot.</span><span class="sxs-lookup"><span data-stu-id="71aef-158">Your app manifest is pointing to where you're hosting the bot.</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="71aef-159">4. configurar el bot</span><span class="sxs-lookup"><span data-stu-id="71aef-159">4. Configure your bot</span></span>

<span data-ttu-id="71aef-160">Para usar un bot en Teams, debe registrarlo con el servicio de bot de Azure.</span><span class="sxs-lookup"><span data-stu-id="71aef-160">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="71aef-161">Por suerte, esto se realiza automáticamente al configurar la aplicación con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-161">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

### <a name="specify-your-bot-id-and-password"></a><span data-ttu-id="71aef-162">Especificar el identificador de robot y la contraseña</span><span class="sxs-lookup"><span data-stu-id="71aef-162">Specify your bot ID and password</span></span>

<span data-ttu-id="71aef-163">Cuando se registra el bot con el servicio de robots de Azure, se le asigna un identificador y una contraseña que la aplicación de Teams debe conocer.</span><span class="sxs-lookup"><span data-stu-id="71aef-163">When your bot is registered with the Azure Bot Service, it's assigned an ID and password that your Teams app must know about.</span></span>

1. <span data-ttu-id="71aef-164">Busque el identificador de robot y la contraseña que almacenó durante la instalación del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="71aef-164">Locate the bot ID and password you stored during toolkit setup.</span></span>
1. <span data-ttu-id="71aef-165">En el directorio raíz, abra el `.env` archivo.</span><span class="sxs-lookup"><span data-stu-id="71aef-165">In your root directory, open the `.env` file.</span></span>
1. <span data-ttu-id="71aef-166">Agregue el identificador de Bot y la contraseña a `BotId` y `BotPassword` , respectivamente.</span><span class="sxs-lookup"><span data-stu-id="71aef-166">Add your bot ID and password to `BotId` and `BotPassword`, respectively.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="71aef-167">Agregar la dirección de punto de conexión de bot</span><span class="sxs-lookup"><span data-stu-id="71aef-167">Add the bot endpoint address</span></span>

<span data-ttu-id="71aef-168">Debe especificar una dirección URL de punto de conexión para recibir y procesar los mensajes de usuario (por ejemplo, solicitudes) enviados al bot.</span><span class="sxs-lookup"><span data-stu-id="71aef-168">You must specify an endpoint URL to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="71aef-169">Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="71aef-169">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="71aef-170">Puede configurar esto rápidamente en el kit de herramientas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-170">You can configure this quickly in the Teams Toolkit.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. <span data-ttu-id="71aef-172">Vaya a **Administración de bot > registros de bot existentes** y seleccione el bot que creó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="71aef-172">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="71aef-173">En el campo **dirección de extremo del bot** , escriba el servidor Web local en el que hospeda el bot ( `baseUrl10` valor) y agréguelo `/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="71aef-173">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot (`baseUrl10` value) and append `/api/messages` to it.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del punto de conexión del bot en el kit de herramientas de Teams.":::

<span data-ttu-id="71aef-175">El bot podrá responder a los mensajes de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-175">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-run-your-app"></a><span data-ttu-id="71aef-176">5. ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="71aef-176">5. Run your app</span></span>

<span data-ttu-id="71aef-177">Ha configurado una dirección URL para hospedar el bot y configurarlo para administrar mensajes.</span><span class="sxs-lookup"><span data-stu-id="71aef-177">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="71aef-178">Es el momento de poner el bot en marcha.</span><span class="sxs-lookup"><span data-stu-id="71aef-178">It's time to get your bot up and running.</span></span>

1. <span data-ttu-id="71aef-179">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="71aef-179">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="71aef-180">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="71aef-180">Run `npm start`.</span></span>

<span data-ttu-id="71aef-181">Si se ejecuta correctamente, verá algo parecido al siguiente mensaje que indica que el bot está escuchando actividades en `localhost` :</span><span class="sxs-lookup"><span data-stu-id="71aef-181">If successful, you see something like the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="71aef-182">6. transferir localmente el bot a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="71aef-182">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="71aef-183">Con el bot ejecutándose, puede instalarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-183">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="71aef-184">Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="71aef-184">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="71aef-185">Inicie sesión en el cliente de Teams con su cuenta que permite la transferencia local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="71aef-185">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="71aef-186">Seleccione **aplicaciones**y, después, elija **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="71aef-186">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="71aef-187">Vaya a la carpeta de proyecto de la aplicación `.publish` y seleccione `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="71aef-187">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="71aef-188">En el modal instalar, seleccione **Agregar** para instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71aef-188">In the install modal, select **Add** to install your app.</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="71aef-189">7. probar el bot</span><span class="sxs-lookup"><span data-stu-id="71aef-189">7. Test your bot</span></span>

<span data-ttu-id="71aef-190">Ahora es la parte divertida: digamos "Hola" a su bot en un chat de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="71aef-190">Now for the fun part: Let's say "Hello" to your bot in a one-on-one chat.</span></span>

1. En Microsoft Teams, seleccione **más** :::image type="icon" source="../assets/icons/teams-client-more.png"::: en el lado izquierdo.
1. <span data-ttu-id="71aef-192">Busque y seleccione el bot al que acaba de hacer una transtransferida localmente.</span><span class="sxs-lookup"><span data-stu-id="71aef-192">Locate and choose the bot you just sideloaded.</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/bot-teams-access.png" alt-text="Ilustración que muestra dónde obtener acceso a su bot en Teams.":::
1. <span data-ttu-id="71aef-194">En el cuadro de redacción, envíe un `Hello` mensaje.</span><span class="sxs-lookup"><span data-stu-id="71aef-194">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="71aef-195">El bot responde con algo parecido al siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="71aef-195">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Una captura de pantalla que muestra un usuario diga ' Hello ' a un bot de Teams y obtenga una respuesta.":::

## <a name="well-done"></a><span data-ttu-id="71aef-197">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="71aef-197">Well done</span></span>

<span data-ttu-id="71aef-198">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="71aef-198">Congratulations!</span></span> <span data-ttu-id="71aef-199">Tiene un bot básico de teams que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats).</span><span class="sxs-lookup"><span data-stu-id="71aef-199">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="71aef-200">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="71aef-200">Troubleshooting</span></span>

<span data-ttu-id="71aef-201">La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="71aef-201">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="71aef-202">Error en la instalación del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="71aef-202">Toolkit setup fails</span></span>

<span data-ttu-id="71aef-203">Al configurar el proyecto de la aplicación con Team Toolkit, obtiene un error después de seleccionar la opción **crear un nuevo bot** e iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="71aef-203">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="71aef-204">Podría ser un problema de autenticación.</span><span class="sxs-lookup"><span data-stu-id="71aef-204">This could be an authentication issue.</span></span> <span data-ttu-id="71aef-205">Siga estos pasos para finalizar la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="71aef-205">Follow these steps to finish setting up your project.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **Cerrar sesión**.
1. <span data-ttu-id="71aef-207">Vuelva a pasar por el proceso de instalación iniciando sesión con la misma cuenta y creando un nuevo bot.</span><span class="sxs-lookup"><span data-stu-id="71aef-207">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="71aef-208">Bot no está conectado a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="71aef-208">Bot isn't connected to Teams</span></span>

<span data-ttu-id="71aef-209">Si ha instalado la aplicación pero el bot no funciona, asegúrese de que el bot esté [conectado al *canal*Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="71aef-209">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="71aef-210">Es importante comprender que no es lo mismo que un canal en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="71aef-210">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="71aef-211">En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="71aef-211">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="71aef-212">Más información</span><span class="sxs-lookup"><span data-stu-id="71aef-212">Learn more</span></span>

* [<span data-ttu-id="71aef-213">Ver qué otros bots de Teams pueden hacer con una de nuestras muestras</span><span class="sxs-lookup"><span data-stu-id="71aef-213">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="71aef-214">Conceptos básicos de las conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="71aef-214">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="71aef-215">Autenticación de bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="71aef-215">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="71aef-216">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="71aef-216">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="71aef-217">Crear un bot sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="71aef-217">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
