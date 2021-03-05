---
title: 'Tutorial: crear la primera aplicación con C #'
description: Obtén información sobre cómo empezar a crear aplicaciones de Microsoft Teams con C# o .NET.
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: ededd0800c7f789469e79e2a475c125b7fc37795
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449391"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="9fe60-104">Crear la primera aplicación de Teams con C# o .NET</span><span class="sxs-lookup"><span data-stu-id="9fe60-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="9fe60-105">Este tutorial te ayuda a crear una aplicación de Microsoft Teams con C# o .NET.</span><span class="sxs-lookup"><span data-stu-id="9fe60-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span> <span data-ttu-id="9fe60-106">Para ello, debe:</span><span class="sxs-lookup"><span data-stu-id="9fe60-106">To do this, you must:</span></span>

* <span data-ttu-id="9fe60-107">Prepare el entorno</span><span class="sxs-lookup"><span data-stu-id="9fe60-107">Prepare your environment</span></span>
* <span data-ttu-id="9fe60-108">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9fe60-108">Get prerequisites</span></span>
* <span data-ttu-id="9fe60-109">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="9fe60-109">Download the sample</span></span>
* <span data-ttu-id="9fe60-110">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="9fe60-110">Build and run the sample</span></span>
* <span data-ttu-id="9fe60-111">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9fe60-111">Host the sample app</span></span>
* <span data-ttu-id="9fe60-112">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="9fe60-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="9fe60-113">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="9fe60-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="9fe60-114">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9fe60-114">Get prerequisites</span></span>

<span data-ttu-id="9fe60-115">Para completar este tutorial, debe instalar las siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="9fe60-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="9fe60-116">Instalar Git</span><span class="sxs-lookup"><span data-stu-id="9fe60-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="9fe60-117">Instalar Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9fe60-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="9fe60-118">Puede instalar la edición de comunidad gratuita de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fe60-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="9fe60-119">Durante la instalación, si hay una opción para agregar `git` a la ruta de acceso, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="9fe60-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="9fe60-120">En una ventana de terminal, ejecute el siguiente comando para comprobar la `git` instalación:</span><span class="sxs-lookup"><span data-stu-id="9fe60-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="9fe60-121">Usa una ventana de terminal adecuada en tu plataforma.</span><span class="sxs-lookup"><span data-stu-id="9fe60-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="9fe60-122">Estos ejemplos usan Git Bash, pero se pueden ejecutar en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="9fe60-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="9fe60-123">Abra la versión más reciente de Visual Studio e instale las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="9fe60-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="9fe60-124">Puede usar la misma ventana de terminal para ejecutar los comandos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9fe60-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="9fe60-125">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="9fe60-125">Download the sample</span></span>

<span data-ttu-id="9fe60-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="9fe60-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="9fe60-127">muestra en C#.</span><span class="sxs-lookup"><span data-stu-id="9fe60-127">sample in C#.</span></span> <span data-ttu-id="9fe60-128">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo:</span><span class="sxs-lookup"><span data-stu-id="9fe60-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="9fe60-129">Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio para](https://github.com/OfficeDev/Microsoft-Teams-Samples) modificar y guardar los cambios en GitHub.</span><span class="sxs-lookup"><span data-stu-id="9fe60-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="9fe60-130">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="9fe60-130">Build and run the sample</span></span>

<span data-ttu-id="9fe60-131">Después de clonar el repositorio, use Visual Studio para abrir el archivo de solución **Microsoft.Teams.Samples.HelloWorld.sln** del **directorio Microsoft-Teams-Samples/samples/app-hello-world/csharp** del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9fe60-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="9fe60-132">A continuación, **seleccione Generar solución** en el **menú** Generar.</span><span class="sxs-lookup"><span data-stu-id="9fe60-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="9fe60-133">Para ejecutar el ejemplo, presione **F5** o **seleccione Iniciar depuración** en el **menú** Depurar.</span><span class="sxs-lookup"><span data-stu-id="9fe60-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="9fe60-134">Cuando se inicia la aplicación, se abre una ventana del explorador con la raíz de la aplicación iniciada.</span><span class="sxs-lookup"><span data-stu-id="9fe60-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="9fe60-135">Puedes ir a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="9fe60-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- <span data-ttu-id="9fe60-136">[https://localhost:44327/second]https://localhost:44327/second)</span><span class="sxs-lookup"><span data-stu-id="9fe60-136">[https://localhost:44327/second]https://localhost:44327/second)</span></span>

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="9fe60-137">Si recibe un `Could not find a part of the path … bin\roslyn\csc.exe` error, actualice el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="9fe60-137">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="9fe60-138">Para obtener más información, vea [esta pregunta en Stack Overflow](https://stackoverflow.com/questions/32780315).</span><span class="sxs-lookup"><span data-stu-id="9fe60-138">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="9fe60-139">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9fe60-139">Host the sample app</span></span>

<span data-ttu-id="9fe60-140">Las aplicaciones de Microsoft Teams son aplicaciones web que proporcionan una o más funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="9fe60-140">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="9fe60-141">Para que la plataforma teams cargue la aplicación, la aplicación debe estar disponible en Internet.</span><span class="sxs-lookup"><span data-stu-id="9fe60-141">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="9fe60-142">Para ello, debes hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-142">To do this, you need to host your app.</span></span> <span data-ttu-id="9fe60-143">Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel para el proceso local en el equipo mediante `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="9fe60-143">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="9fe60-144">Después de hospedar la aplicación, anote su dirección URL raíz, como `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="9fe60-144">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="9fe60-145">Túnel con ngrok</span><span class="sxs-lookup"><span data-stu-id="9fe60-145">Tunnel using ngrok</span></span>

<span data-ttu-id="9fe60-146">Para realizar pruebas rápidas, puedes ejecutar la aplicación en el equipo y crear un túnel para ella a través de un punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="9fe60-146">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="9fe60-147">[`ngrok`](https://ngrok.com) es una herramienta gratuita con la que puede obtener una dirección web, como `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="9fe60-147">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="9fe60-148">Puede descargar [e instalar](https://ngrok.com/download) ngrok y agregarlo a una ubicación en su `PATH` .</span><span class="sxs-lookup"><span data-stu-id="9fe60-148">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="9fe60-149">Después de instalar `ngrok` , abra una nueva ventana de terminal y ejecute el siguiente comando para crear un túnel:</span><span class="sxs-lookup"><span data-stu-id="9fe60-149">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="9fe60-150">`Ngrok` escucha las solicitudes de Internet y las enruta a la aplicación que se ejecuta en el puerto 44327.</span><span class="sxs-lookup"><span data-stu-id="9fe60-150">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="9fe60-151">Para comprobarlo, abre el explorador y ve a `https://d0ac14a5.ngrok.io/hello` cargar la página de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-151">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="9fe60-152">En lugar de esta dirección URL, use la dirección de reenvío mostrada en `ngrok` la sesión de la consola.</span><span class="sxs-lookup"><span data-stu-id="9fe60-152">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="9fe60-153">Si ha usado un puerto diferente en el paso [de](#build-and-run-the-sample) compilación y ejecución, asegúrese de usar el mismo número de puerto para configurar el `ngrok` túnel.</span><span class="sxs-lookup"><span data-stu-id="9fe60-153">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="9fe60-154">Es una buena idea ejecutarse `ngrok` en una ventana de terminal diferente.</span><span class="sxs-lookup"><span data-stu-id="9fe60-154">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="9fe60-155">Esto se hace para evitar `ngrok` que se ejecute sin interferir con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-155">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="9fe60-156">Debes detener, recompilar y volver a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-156">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="9fe60-157">La `ngrok` sesión proporciona información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="9fe60-157">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="9fe60-158">La aplicación solo está disponible durante la sesión actual en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9fe60-158">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="9fe60-159">Si la máquina está apagada o está en modo de suspensión, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="9fe60-159">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="9fe60-160">Recuerda esto cuando compartas la aplicación para realizar pruebas a otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="9fe60-160">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="9fe60-161">Si tienes que reiniciar el servicio, la aplicación devuelve una nueva dirección y debes actualizar cada ubicación que use esa dirección.</span><span class="sxs-lookup"><span data-stu-id="9fe60-161">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="9fe60-162">La versión de pago `ngrok` de no tiene esta limitación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-162">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="9fe60-163">Host en Azure</span><span class="sxs-lookup"><span data-stu-id="9fe60-163">Host in Azure</span></span>

<span data-ttu-id="9fe60-164">Microsoft Azure hospeda la aplicación .NET en un nivel gratuito mediante la infraestructura compartida.</span><span class="sxs-lookup"><span data-stu-id="9fe60-164">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="9fe60-165">Esto es suficiente para ejecutar el `Hello World` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9fe60-165">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="9fe60-166">Para obtener más información, vea [creating a new free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9fe60-166">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="9fe60-167">Visual Studio compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe60-167">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="9fe60-168">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="9fe60-168">Update the credentials for your hosted app</span></span>

<span data-ttu-id="9fe60-169">La aplicación de ejemplo requiere que las variables de entorno se establezcan en los valores guardados en el [archivo de texto](~/includes/get-started/get-started-use-app-studio.md#bots).</span><span class="sxs-lookup"><span data-stu-id="9fe60-169">The sample app requires the environment variables to be set to the values that you saved in the [text file](~/includes/get-started/get-started-use-app-studio.md#bots).</span></span>

<span data-ttu-id="9fe60-170">Abra el archivo appsettings.jsen.</span><span class="sxs-lookup"><span data-stu-id="9fe60-170">Open the appsettings.json file.</span></span> <span data-ttu-id="9fe60-171">Actualice el **valor de MicrosoftAppId** con el identificador de bot que guardó en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="9fe60-171">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="9fe60-172">Actualice **MicrosoftAppPassword** con la contraseña del bot que guardó.</span><span class="sxs-lookup"><span data-stu-id="9fe60-172">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="9fe60-173">Después de realizar estos cambios, recompile la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-173">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="9fe60-174">Si usa ngrok, ejecute la aplicación localmente y, si está hospedando en Azure, vuelva a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-174">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="9fe60-175">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="9fe60-175">Configure the app tab</span></span>

<span data-ttu-id="9fe60-176">Una vez que instales la aplicación en un equipo, debes configurarla para que muestre contenido.</span><span class="sxs-lookup"><span data-stu-id="9fe60-176">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="9fe60-177">Ve a un canal del equipo en el que instalaste la aplicación de ejemplo y selecciona el botón **"+"** para agregar una nueva pestaña. Elija **Hello World** en la lista Agregar **una** pestaña.</span><span class="sxs-lookup"><span data-stu-id="9fe60-177">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="9fe60-178">Se muestra un cuadro de diálogo de configuración que permite elegir la pestaña que se va a mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="9fe60-178">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="9fe60-179">Después de seleccionar la pestaña y seleccionar **Guardar** la `Hello World` pestaña se carga con la pestaña.</span><span class="sxs-lookup"><span data-stu-id="9fe60-179">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="9fe60-180">Probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="9fe60-180">Test your bot in Teams</span></span>

<span data-ttu-id="9fe60-181">Ahora puedes probar el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="9fe60-181">Now you can test the bot in Teams.</span></span> <span data-ttu-id="9fe60-182">Selecciona un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="9fe60-182">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="9fe60-183">Esto se denomina una **\@ mención**.</span><span class="sxs-lookup"><span data-stu-id="9fe60-183">This is called an **\@mention**.</span></span> <span data-ttu-id="9fe60-184">El bot responde a cualquier mensaje que envíe.</span><span class="sxs-lookup"><span data-stu-id="9fe60-184">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="9fe60-185">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="9fe60-185">Test your messaging extension</span></span>

<span data-ttu-id="9fe60-186">Para probar la extensión de mensajería, puede seleccionar **...** debajo del cuadro de entrada de la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-186">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="9fe60-187">Se muestra un menú con la aplicación **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="9fe60-187">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="9fe60-188">Al seleccionarlo, se muestra un conjunto de textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="9fe60-188">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="9fe60-189">Puede seleccionar uno de los textos aleatorios que se insertan en la conversación.</span><span class="sxs-lookup"><span data-stu-id="9fe60-189">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="9fe60-190">Seleccione uno de los textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="9fe60-190">Select one of the random text.</span></span> <span data-ttu-id="9fe60-191">Se muestra una tarjeta con formato y lista para enviar con su propio mensaje.</span><span class="sxs-lookup"><span data-stu-id="9fe60-191">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
