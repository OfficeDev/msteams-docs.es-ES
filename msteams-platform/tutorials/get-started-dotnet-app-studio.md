---
title: 'Tutorial: crear la primera aplicación con C #'
description: Obtén información sobre cómo empezar a crear aplicaciones de Microsoft Teams con C# o .NET.
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 99a0982a0fa453c6eb7ffeea25ba8a2607cf2d5e
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596262"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="7cd4a-104">Crear la primera aplicación de Teams con C# o .NET</span><span class="sxs-lookup"><span data-stu-id="7cd4a-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="7cd4a-105">Este tutorial te ayuda a crear una aplicación de Microsoft Teams con C# o .NET.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span> <span data-ttu-id="7cd4a-106">Para ello, debe:</span><span class="sxs-lookup"><span data-stu-id="7cd4a-106">To do this, you must:</span></span>

* <span data-ttu-id="7cd4a-107">Prepare el entorno</span><span class="sxs-lookup"><span data-stu-id="7cd4a-107">Prepare your environment</span></span>
* <span data-ttu-id="7cd4a-108">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7cd4a-108">Get prerequisites</span></span>
* <span data-ttu-id="7cd4a-109">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cd4a-109">Download the sample</span></span>
* <span data-ttu-id="7cd4a-110">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cd4a-110">Build and run the sample</span></span>
* <span data-ttu-id="7cd4a-111">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cd4a-111">Host the sample app</span></span>
* <span data-ttu-id="7cd4a-112">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="7cd4a-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="7cd4a-113">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="7cd4a-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="7cd4a-114">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7cd4a-114">Get prerequisites</span></span>

<span data-ttu-id="7cd4a-115">Para completar este tutorial, debe instalar las siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="7cd4a-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="7cd4a-116">Instalar Git</span><span class="sxs-lookup"><span data-stu-id="7cd4a-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="7cd4a-117">Instalar Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7cd4a-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="7cd4a-118">Puede instalar la edición de comunidad gratuita de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="7cd4a-119">Durante la instalación, si hay una opción para agregar `git` a la ruta de acceso, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="7cd4a-120">En una ventana de terminal, ejecute el siguiente comando para comprobar la `git` instalación:</span><span class="sxs-lookup"><span data-stu-id="7cd4a-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="7cd4a-121">Usa una ventana de terminal adecuada en tu plataforma.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="7cd4a-122">Estos ejemplos usan Git Bash, pero se pueden ejecutar en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="7cd4a-123">Abra la versión más reciente de Visual Studio e instale las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="7cd4a-124">Puede usar la misma ventana de terminal para ejecutar los comandos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="7cd4a-125">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cd4a-125">Download the sample</span></span>

<span data-ttu-id="7cd4a-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="7cd4a-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="7cd4a-127">muestra en C#.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-127">sample in C#.</span></span> <span data-ttu-id="7cd4a-128">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo:</span><span class="sxs-lookup"><span data-stu-id="7cd4a-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="7cd4a-129">Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio para](https://github.com/OfficeDev/Microsoft-Teams-Samples) modificar y guardar los cambios en GitHub.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="7cd4a-130">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cd4a-130">Build and run the sample</span></span>

<span data-ttu-id="7cd4a-131">Después de clonar el repositorio, use Visual Studio para abrir el archivo de solución **Microsoft.Teams.Samples.HelloWorld.sln** del **directorio Microsoft-Teams-Samples/samples/app-hello-world/csharp** del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="7cd4a-132">A continuación, **seleccione Generar solución** en el **menú** Generar.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="7cd4a-133">Para ejecutar el ejemplo, presione **F5** o **seleccione Iniciar depuración** en el **menú** Depurar.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="7cd4a-134">Cuando se inicia la aplicación, se abre una ventana del explorador con la raíz de la aplicación iniciada.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="7cd4a-135">Puedes ir a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7cd4a-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second](https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="7cd4a-136">Si recibe un `Could not find a part of the path … bin\roslyn\csc.exe` error, actualice el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="7cd4a-136">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="7cd4a-137">Para obtener más información, vea [esta pregunta en Stack Overflow](https://stackoverflow.com/questions/32780315).</span><span class="sxs-lookup"><span data-stu-id="7cd4a-137">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="7cd4a-138">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cd4a-138">Host the sample app</span></span>

<span data-ttu-id="7cd4a-139">Las aplicaciones de Microsoft Teams son aplicaciones web que proporcionan una o más funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-139">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="7cd4a-140">Para que la plataforma teams cargue la aplicación, la aplicación debe estar disponible en Internet.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-140">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="7cd4a-141">Para ello, debes hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-141">To do this, you need to host your app.</span></span> <span data-ttu-id="7cd4a-142">Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel para el proceso local en el equipo mediante `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="7cd4a-142">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="7cd4a-143">Después de hospedar la aplicación, anote su dirección URL raíz, como `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="7cd4a-143">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="7cd4a-144">Túnel con ngrok</span><span class="sxs-lookup"><span data-stu-id="7cd4a-144">Tunnel using ngrok</span></span>

<span data-ttu-id="7cd4a-145">Para realizar pruebas rápidas, puedes ejecutar la aplicación en el equipo y crear un túnel para ella a través de un punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-145">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="7cd4a-146">[`ngrok`](https://ngrok.com) es una herramienta gratuita con la que puede obtener una dirección web, como `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="7cd4a-146">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="7cd4a-147">Puede descargar [e instalar](https://ngrok.com/download) ngrok y agregarlo a una ubicación en su `PATH` .</span><span class="sxs-lookup"><span data-stu-id="7cd4a-147">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="7cd4a-148">Después de instalar `ngrok` , abra una nueva ventana de terminal y ejecute el siguiente comando para crear un túnel:</span><span class="sxs-lookup"><span data-stu-id="7cd4a-148">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="7cd4a-149">`Ngrok` escucha las solicitudes de Internet y las enruta a la aplicación que se ejecuta en el puerto 44327.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-149">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="7cd4a-150">Para comprobarlo, abre el explorador y ve a `https://d0ac14a5.ngrok.io/hello` cargar la página de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-150">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="7cd4a-151">En lugar de esta dirección URL, use la dirección de reenvío mostrada en `ngrok` la sesión de la consola.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-151">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="7cd4a-152">Si ha usado un puerto diferente en el paso [de](#build-and-run-the-sample) compilación y ejecución, asegúrese de usar el mismo número de puerto para configurar el `ngrok` túnel.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-152">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="7cd4a-153">Es una buena idea ejecutarse `ngrok` en una ventana de terminal diferente.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-153">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="7cd4a-154">Esto se hace para evitar `ngrok` que se ejecute sin interferir con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-154">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="7cd4a-155">Debes detener, recompilar y volver a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-155">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="7cd4a-156">La `ngrok` sesión proporciona información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-156">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="7cd4a-157">La aplicación solo está disponible durante la sesión actual en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-157">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="7cd4a-158">Si la máquina está apagada o está en modo de suspensión, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-158">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="7cd4a-159">Recuerda esto cuando compartas la aplicación para realizar pruebas a otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-159">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="7cd4a-160">Si tienes que reiniciar el servicio, la aplicación devuelve una nueva dirección y debes actualizar cada ubicación que use esa dirección.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-160">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="7cd4a-161">La versión de pago `ngrok` de no tiene esta limitación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-161">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="7cd4a-162">Host en Azure</span><span class="sxs-lookup"><span data-stu-id="7cd4a-162">Host in Azure</span></span>

<span data-ttu-id="7cd4a-163">Microsoft Azure hospeda la aplicación .NET en un nivel gratuito mediante la infraestructura compartida.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-163">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="7cd4a-164">Esto es suficiente para ejecutar el `Hello World` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-164">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="7cd4a-165">Para obtener más información, vea [creating a new free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7cd4a-165">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="7cd4a-166">Visual Studio compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-166">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="7cd4a-167">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="7cd4a-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="7cd4a-168">La aplicación de ejemplo requiere que las variables de entorno se establezcan en los valores guardados en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-168">The sample app requires the environment variables be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="7cd4a-169">Abra el archivo `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-169">Open the `appsettings.json` file.</span></span> <span data-ttu-id="7cd4a-170">Actualice el **valor de MicrosoftAppId** con el identificador de bot que guardó en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-170">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="7cd4a-171">Actualice **MicrosoftAppPassword** con la contraseña del bot que guardó.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-171">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="7cd4a-172">Después de realizar estos cambios, recompile la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-172">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="7cd4a-173">Si usa ngrok, ejecute la aplicación localmente y, si está hospedando en Azure, vuelva a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-173">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="7cd4a-174">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="7cd4a-174">Configure the app tab</span></span>

<span data-ttu-id="7cd4a-175">Una vez que instales la aplicación en un equipo, debes configurarla para que muestre contenido.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-175">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="7cd4a-176">Ve a un canal del equipo en el que instalaste la aplicación de ejemplo y selecciona el botón **"+"** para agregar una nueva pestaña. Elija **Hello World** en la lista Agregar **una** pestaña.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-176">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="7cd4a-177">Se muestra un cuadro de diálogo de configuración que permite elegir la pestaña que se va a mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-177">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="7cd4a-178">Después de seleccionar la pestaña y seleccionar **Guardar** la `Hello World` pestaña se carga con la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-178">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="7cd4a-179">Probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="7cd4a-179">Test your bot in Teams</span></span>

<span data-ttu-id="7cd4a-180">Ahora puedes probar el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-180">Now you can test the bot in Teams.</span></span> <span data-ttu-id="7cd4a-181">Selecciona un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="7cd4a-181">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="7cd4a-182">Esto se denomina una **\@ mención**.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-182">This is called an **\@mention**.</span></span> <span data-ttu-id="7cd4a-183">El bot responde a cualquier mensaje que envíe.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-183">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="7cd4a-184">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="7cd4a-184">Test your messaging extension</span></span>

<span data-ttu-id="7cd4a-185">Para probar la extensión de mensajería, puede seleccionar **...** debajo del cuadro de entrada de la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-185">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="7cd4a-186">Se muestra un menú con la aplicación **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="7cd4a-186">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="7cd4a-187">Al seleccionarlo, se muestra un conjunto de textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-187">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="7cd4a-188">Puede seleccionar uno de los textos aleatorios que se insertan en la conversación.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-188">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="7cd4a-189">Seleccione uno de los textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-189">Select one of the random text.</span></span> <span data-ttu-id="7cd4a-190">Se muestra una tarjeta con formato y lista para enviar con su propio mensaje.</span><span class="sxs-lookup"><span data-stu-id="7cd4a-190">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
