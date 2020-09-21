---
title: Creación de un bot para Teams
author: heath-hamilton
description: Obtenga información sobre cómo crear un bot en su primera aplicación de Microsoft Teams.
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
ms.openlocfilehash: f1307bcc7bb864ddfa97b9297f34fa4f7d5fcb0d
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964779"
---
# <a name="create-a-bot-for-teams"></a><span data-ttu-id="ed021-103">Creación de un bot para Teams</span><span class="sxs-lookup"><span data-stu-id="ed021-103">Create a bot for Teams</span></span>

<span data-ttu-id="ed021-104">Compilará una aplicación de *Bot* básica en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ed021-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="ed021-105">Un bot actúa como intermediario entre los usuarios de Microsoft Teams y el servicio Web.</span><span class="sxs-lookup"><span data-stu-id="ed021-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="ed021-106">Los usuarios pueden chatear con un bot para obtener información o iniciar flujos de trabajo y tareas realizados por el servicio de forma rápida.</span><span class="sxs-lookup"><span data-stu-id="ed021-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="ed021-107">La asignación</span><span class="sxs-lookup"><span data-stu-id="ed021-107">Your assignment</span></span>

<span data-ttu-id="ed021-108">El área de trabajo ha estado usando [pestañas](../build-your-first-app/add-personal-tab.md) para exponer la información de contacto importante en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-108">Your workplace has been using [tabs](../build-your-first-app/add-personal-tab.md) to surface important contact information in Teams.</span></span> <span data-ttu-id="ed021-109">Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de asistencia.</span><span class="sxs-lookup"><span data-stu-id="ed021-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="ed021-110">Pero, en lugar de llamar a, ¿qué sucede si los usuarios pueden ponerse en contacto con el Departamento de soporte mediante un Chatbot?</span><span class="sxs-lookup"><span data-stu-id="ed021-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="ed021-111">Su jefe le pedirá que consulte la velocidad con la que puede poner en marcha un bot de conversación básico en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ed021-112">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="ed021-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ed021-113">Crear un proyecto de aplicación y un bot con el kit de herramientas de Microsoft Teams para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ed021-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="ed021-114">Identificar las propiedades del manifiesto de la aplicación y algunos de los scaffolding relevantes para los bots</span><span class="sxs-lookup"><span data-stu-id="ed021-114">Identify the app manifest properties and some of the scaffolding relevant to bots</span></span>
> * <span data-ttu-id="ed021-115">Hospedar un bot localmente</span><span class="sxs-lookup"><span data-stu-id="ed021-115">Host a bot locally</span></span>
> * <span data-ttu-id="ed021-116">Configurar un bot para Teams</span><span class="sxs-lookup"><span data-stu-id="ed021-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="ed021-117">Transferir localmente y probar un bot en Teams</span><span class="sxs-lookup"><span data-stu-id="ed021-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ed021-118">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ed021-118">Before you begin</span></span>

<span data-ttu-id="ed021-119">Si aún no lo ha hecho, configure la [cuenta](building-real-world-app.md#set-up-your-development-account) de desarrollo de Microsoft 365 y [las herramientas de la aplicación de Teams](building-real-world-app.md#install-your-development-tools).</span><span class="sxs-lookup"><span data-stu-id="ed021-119">If you haven't yet, set up your Microsoft 365 development [account](building-real-world-app.md#set-up-your-development-account) and [Teams app tools](building-real-world-app.md#install-your-development-tools).</span></span>

## <a name="create-your-app-project-and-bot"></a><span data-ttu-id="ed021-120">Crear un proyecto de aplicación y un bot</span><span class="sxs-lookup"><span data-stu-id="ed021-120">Create your app project and bot</span></span>

<span data-ttu-id="ed021-121">El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="ed021-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="ed021-122">**Proyecto de aplicación**: incluye el manifiesto de la aplicación y los scaffolding relevantes para los bots.</span><span class="sxs-lookup"><span data-stu-id="ed021-122">**App project**: Includes the app manifest and scaffolding relevant to bots</span></span>
* <span data-ttu-id="ed021-123">**Bot**: configura un nuevo bot y lo registra con el servicio de robots de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ed021-123">**Bot**: Configures a new bot and registers it with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="ed021-124">Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="ed021-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. <span data-ttu-id="ed021-126">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-126">Enter a name for your Teams app.</span></span> <span data-ttu-id="ed021-127">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="ed021-127">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="ed021-128">En la pantalla **Agregar funciones** , seleccione **Bot** y, a continuación, **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ed021-128">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="ed021-129">Seleccione **crear un nuevo bot** e **iniciar sesión** para iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ed021-129">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span><br/>
:::image type="content" source="../doc-links/images/vsc-create-bot.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot.":::
1. <span data-ttu-id="ed021-131">Opcional Escriba un nombre personalizado para el bot y seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="ed021-131">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="ed021-132">Recuerde que este es el nombre de su bot y no el nombre de la aplicación de teams que ya ha especificado.</span><span class="sxs-lookup"><span data-stu-id="ed021-132">(Remember, this is the name for your bot and not the name of the Teams app you already specified.)</span></span>
1. <span data-ttu-id="ed021-133">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ed021-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="ed021-134">Identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="ed021-134">Identify relevant app project components</span></span>

<span data-ttu-id="ed021-135">La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-135">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="ed021-136">Echemos un vistazo a los componentes principales para crear un bot.</span><span class="sxs-lookup"><span data-stu-id="ed021-136">Let's look at the main components for building a bot.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="ed021-137">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ed021-137">App manifest</span></span>

<span data-ttu-id="ed021-138">El siguiente fragmento de código del manifiesto de la aplicación (el `manifest.json` archivo del `.publish` directorio del proyecto) muestra las propiedades y los valores predeterminados pertinentes para los bots.</span><span class="sxs-lookup"><span data-stu-id="ed021-138">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to bots.</span></span>

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

<span data-ttu-id="ed021-139">Por ahora, vamos a centrarnos en las siguientes propiedades necesarias.</span><span class="sxs-lookup"><span data-stu-id="ed021-139">For now, let's just focus on the following required properties.</span></span> <span data-ttu-id="ed021-140">(Vea la lista completa de propiedades admitidas [`bots`](../../resources/schema/manifest-schema.md#bots) ).</span><span class="sxs-lookup"><span data-stu-id="ed021-140">(See the full list of supported [`bots`](../../resources/schema/manifest-schema.md#bots) properties.)</span></span>

* <span data-ttu-id="ed021-141">`botId`: El identificador del robot que ha creado configurando su proyecto.</span><span class="sxs-lookup"><span data-stu-id="ed021-141">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="ed021-142">(Almacenado en `{botId0}` , puede encontrar el identificador real en `Development.env` ).</span><span class="sxs-lookup"><span data-stu-id="ed021-142">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="ed021-143">`scopes`: Especifica si el bot está disponible en `personal` los `groupchat` `team` contextos,, o (por ejemplo, de canal).</span><span class="sxs-lookup"><span data-stu-id="ed021-143">`scopes`: Specifies if your bot is available in `personal`, `groupchat`, or `team` (i.e., channel) contexts.</span></span>
* <span data-ttu-id="ed021-144">`commands`: Comandos disponibles que los usuarios pueden enviar a su bot.</span><span class="sxs-lookup"><span data-stu-id="ed021-144">`commands`: Available commands users can send to your bot.</span></span>
* <span data-ttu-id="ed021-145">`title`: Un nombre de comando bot que los usuarios ven en el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-145">`title`: A bot command name users see in the Teams client.</span></span>
* <span data-ttu-id="ed021-146">`description`: Una breve descripción o un ejemplo de la sintaxis y los argumentos para ayudar a los usuarios a comprender lo que hace un comando bot.</span><span class="sxs-lookup"><span data-stu-id="ed021-146">`description`: A short description or example of the syntax and arguments to help users understand what a bot command does.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="ed021-147">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ed021-147">App scaffolding</span></span>

<span data-ttu-id="ed021-148">El scaffolding de la aplicación proporciona un `botActivityHandler.js` archivo, que se encuentra en el directorio raíz del proyecto, para controlar cómo el bot procesa las actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como "Hello").</span><span class="sxs-lookup"><span data-stu-id="ed021-148">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="ed021-149">Configurar un túnel seguro para la aplicación</span><span class="sxs-lookup"><span data-stu-id="ed021-149">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="ed021-150">Para fines de prueba, vamos a hospedar su bot en un servidor Web local (puerto 3978).</span><span class="sxs-lookup"><span data-stu-id="ed021-150">For testing purposes, let's host your bot on a local web server (port 3978).</span></span>

1. <span data-ttu-id="ed021-151">En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="ed021-151">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="ed021-152">Copie la dirección URL HTTPS en el resultado, ya que Teams requiere Conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ed021-152">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="ed021-153">En el `.publish` directorio, Abra `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="ed021-153">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="ed021-154">Reemplace el `baseUrl0` valor por la dirección URL copiada.</span><span class="sxs-lookup"><span data-stu-id="ed021-154">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="ed021-155">(Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ca5.ngrok.io` ).</span><span class="sxs-lookup"><span data-stu-id="ed021-155">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="ed021-156">El manifiesto de la aplicación apunta al lugar donde se hospeda el bot.</span><span class="sxs-lookup"><span data-stu-id="ed021-156">Your app manifest is pointing to where you're hosting the bot.</span></span>

## <a name="configuring-your-bot"></a><span data-ttu-id="ed021-157">Configurar el bot</span><span class="sxs-lookup"><span data-stu-id="ed021-157">Configuring your bot</span></span>

<span data-ttu-id="ed021-158">Para usar un bot en Teams, debe registrarlo con el servicio de bot de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed021-158">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="ed021-159">Por suerte, esto se realiza automáticamente al configurar la aplicación con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-159">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="ed021-160">Agregar la dirección de punto de conexión de bot</span><span class="sxs-lookup"><span data-stu-id="ed021-160">Add the bot endpoint address</span></span>

<span data-ttu-id="ed021-161">Debe especificar una dirección URL de punto de conexión para recibir y procesar los mensajes de usuario (por ejemplo, solicitudes) enviados al bot.</span><span class="sxs-lookup"><span data-stu-id="ed021-161">You must specify an endpoint URL to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="ed021-162">Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="ed021-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="ed021-163">Puede configurar esto rápidamente en el kit de herramientas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-163">You can configure this quickly in the Teams Toolkit.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. <span data-ttu-id="ed021-165">Vaya a **Administración de bot > registros de bot existentes** y seleccione el bot que creó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="ed021-165">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="ed021-166">En el campo **dirección de extremo del bot** , escriba el servidor Web local en el que va a hospedar el bot y agréguelo `/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="ed021-166">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot and append `/api/messages` to it.</span></span>

    :::image type="content" source="../doc-links/images/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del punto de conexión del bot en el kit de herramientas de Teams.":::

<span data-ttu-id="ed021-168">El bot podrá responder a los mensajes de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-168">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="ed021-169">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="ed021-169">Run your app</span></span>

<span data-ttu-id="ed021-170">Ha configurado una dirección URL para hospedar el bot y configurarlo para administrar mensajes.</span><span class="sxs-lookup"><span data-stu-id="ed021-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="ed021-171">Es el momento de poner el bot en marcha.</span><span class="sxs-lookup"><span data-stu-id="ed021-171">It's time to get your bot up and running.</span></span>

1. <span data-ttu-id="ed021-172">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="ed021-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="ed021-173">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="ed021-173">Run `npm start`.</span></span>

<span data-ttu-id="ed021-174">Si se ejecuta correctamente, verá algo parecido al siguiente mensaje que indica que el bot está escuchando actividades en `localhost` :</span><span class="sxs-lookup"><span data-stu-id="ed021-174">If successful, you see something like the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a><span data-ttu-id="ed021-175">Transferir localmente el bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ed021-175">Sideload your bot in Teams</span></span>

<span data-ttu-id="ed021-176">Con el bot ejecutándose, puede instalarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="ed021-177">Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="ed021-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="ed021-178">Inicie sesión en el cliente de Teams con su cuenta que permite la transferencia local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ed021-178">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="ed021-179">Seleccione **aplicaciones**y, después, elija **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="ed021-179">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="ed021-180">Vaya a la carpeta de proyecto de la aplicación `.publish` y seleccione `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="ed021-180">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="ed021-181">En el modal instalar, seleccione **Agregar** para instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed021-181">In the install modal, select **Add** to install your app.</span></span>

## <a name="test-your-bot"></a><span data-ttu-id="ed021-182">Probar el bot</span><span class="sxs-lookup"><span data-stu-id="ed021-182">Test your bot</span></span>

<span data-ttu-id="ed021-183">Ahora es la parte divertida: digamos "Hola" a su bot en un chat de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="ed021-183">Now for the fun part: Let's say "Hello" to your bot in a one-on-one chat.</span></span>

1. En Microsoft Teams, seleccione **más** :::image type="icon" source="../doc-links/images/teams-client-more.png"::: en el lado izquierdo.
1. <span data-ttu-id="ed021-185">Busque y seleccione el bot al que acaba de hacer una transtransferida localmente.</span><span class="sxs-lookup"><span data-stu-id="ed021-185">Locate and select the bot you just sideloaded.</span></span><br/>
   :::image type="content" source="../doc-links/images/bot-teams-access.png" alt-text="Ilustración que muestra dónde obtener acceso a su bot en Teams.":::
1. <span data-ttu-id="ed021-187">En el cuadro de redacción, envíe un `Hello` mensaje.</span><span class="sxs-lookup"><span data-stu-id="ed021-187">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="ed021-188">El bot responde con algo parecido al siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="ed021-188">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../doc-links/images/contoso-chatbot.png" alt-text="Una captura de pantalla que muestra un usuario diga ' Hello ' a un bot de Teams y obtenga una respuesta.":::

> [!NOTE]
> <span data-ttu-id="ed021-190">Si realiza cambios en el código después de probar el bot (por ejemplo, si actualiza `botActivityHandler.js` ) debe volver a ejecutar la aplicación para ver los cambios que se han reflejado en Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-190">If you make code changes after testing your bot—for example, you update `botActivityHandler.js`—you must run your app again to see those changes reflected in Teams.</span></span>

## <a name="well-done"></a><span data-ttu-id="ed021-191">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="ed021-191">Well done</span></span>

<span data-ttu-id="ed021-192">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ed021-192">Congratulations!</span></span> <span data-ttu-id="ed021-193">Tiene un bot básico de teams que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats).</span><span class="sxs-lookup"><span data-stu-id="ed021-193">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ed021-194">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="ed021-194">Troubleshooting</span></span>

<span data-ttu-id="ed021-195">La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ed021-195">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="ed021-196">Error en la instalación del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="ed021-196">Toolkit setup fails</span></span>

<span data-ttu-id="ed021-197">Al configurar el proyecto de la aplicación con Team Toolkit, obtiene un error después de seleccionar la opción **crear un nuevo bot** e iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ed021-197">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="ed021-198">Podría ser un problema de autenticación.</span><span class="sxs-lookup"><span data-stu-id="ed021-198">This could be an authentication issue.</span></span> <span data-ttu-id="ed021-199">Siga estos pasos para finalizar la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ed021-199">Follow these steps to finish setting up your project.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **Cerrar sesión**.
1. <span data-ttu-id="ed021-201">Vuelva a pasar por el proceso de instalación iniciando sesión con la misma cuenta y creando un nuevo bot.</span><span class="sxs-lookup"><span data-stu-id="ed021-201">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="ed021-202">Bot no está conectado a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ed021-202">Bot isn't connected to Teams</span></span>

<span data-ttu-id="ed021-203">Si ha instalado la aplicación pero el bot no funciona, asegúrese de que el bot esté [conectado al *canal*Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ed021-203">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="ed021-204">Es importante comprender que no es lo mismo que un canal en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ed021-204">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="ed021-205">En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ed021-205">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="ed021-206">Obtén más información</span><span class="sxs-lookup"><span data-stu-id="ed021-206">Learn more</span></span>

* [<span data-ttu-id="ed021-207">Ver qué otros bots de Teams pueden hacer con una de nuestras muestras (GitHub)</span><span class="sxs-lookup"><span data-stu-id="ed021-207">See what else Teams bots can do with one of our samples (GitHub)</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="ed021-208">Conceptos básicos de las conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="ed021-208">Bot conversation basics</span></span>](../../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="ed021-209">Autenticación de bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ed021-209">Bot authentication in Teams</span></span>](../../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="ed021-210">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="ed021-210">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
