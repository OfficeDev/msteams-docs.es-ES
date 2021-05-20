---
title: 'Tutorial - Crea tu primera aplicación usando C #'
description: Obtén información sobre cómo empezar a crear aplicaciones Microsoft Teams con C# o .NET.
keywords: comenzando .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: eaa37f1ccb7944ee18bb62ae47882dc4a715b165
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566890"
---
# <a name="create-your-first-teams-app-using-c"></a><span data-ttu-id="6faba-104">Crea tu primera aplicación de Teams usando C #</span><span class="sxs-lookup"><span data-stu-id="6faba-104">Create your first Teams app using C#</span></span>

<span data-ttu-id="6faba-105">Este tutorial le ayuda a crear una aplicación Microsoft Teams mediante C#.</span><span class="sxs-lookup"><span data-stu-id="6faba-105">This tutorial helps you to create a Microsoft Teams app using C#.</span></span> <span data-ttu-id="6faba-106">Para ello, debe:</span><span class="sxs-lookup"><span data-stu-id="6faba-106">To do this, you must:</span></span>

* <span data-ttu-id="6faba-107">Prepare el entorno</span><span class="sxs-lookup"><span data-stu-id="6faba-107">Prepare your environment</span></span>
* <span data-ttu-id="6faba-108">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6faba-108">Get prerequisites</span></span>
* <span data-ttu-id="6faba-109">Descargue el ejemplo</span><span class="sxs-lookup"><span data-stu-id="6faba-109">Download the sample</span></span>
* <span data-ttu-id="6faba-110">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="6faba-110">Build and run the sample</span></span>
* <span data-ttu-id="6faba-111">Hospede la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6faba-111">Host the sample app</span></span>
* <span data-ttu-id="6faba-112">Actualice las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="6faba-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="6faba-113">Configurar la pestaña de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6faba-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="6faba-114">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6faba-114">Get prerequisites</span></span>

<span data-ttu-id="6faba-115">Para completar este tutorial, debe instalar las siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="6faba-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="6faba-116">Instalar Git</span><span class="sxs-lookup"><span data-stu-id="6faba-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="6faba-117">Instalar Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6faba-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="6faba-118">Puede instalar la edición gratuita de la comunidad de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6faba-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="6faba-119">Durante la instalación, si hay una opción para agregar `git` a la ruta de acceso, selecciónela.</span><span class="sxs-lookup"><span data-stu-id="6faba-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="6faba-120">En una ventana de terminal, ejecute el siguiente comando para comprobar la `git` instalación:</span><span class="sxs-lookup"><span data-stu-id="6faba-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="6faba-121">Utilice una ventana de terminal adecuada en su plataforma.</span><span class="sxs-lookup"><span data-stu-id="6faba-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="6faba-122">Estos ejemplos utilizan Git Bash, pero se pueden ejecutar en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="6faba-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="6faba-123">Abra la versión más reciente de Visual Studio e instale cualquier actualización.</span><span class="sxs-lookup"><span data-stu-id="6faba-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="6faba-124">Puede utilizar la misma ventana de terminal para ejecutar los comandos en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6faba-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="6faba-125">Descargue el ejemplo</span><span class="sxs-lookup"><span data-stu-id="6faba-125">Download the sample</span></span>

<span data-ttu-id="6faba-126">¡Puedes empezar con un simple [Hola, Mundo!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="6faba-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="6faba-127">muestra en C#.</span><span class="sxs-lookup"><span data-stu-id="6faba-127">sample in C#.</span></span> <span data-ttu-id="6faba-128">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo:</span><span class="sxs-lookup"><span data-stu-id="6faba-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="6faba-129">Puede [posicionar](https://help.github.com/articles/fork-a-repo/) este [repositorio](https://github.com/OfficeDev/Microsoft-Teams-Samples) para modificar y guardar los cambios en GitHub.</span><span class="sxs-lookup"><span data-stu-id="6faba-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="6faba-130">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="6faba-130">Build and run the sample</span></span>

<span data-ttu-id="6faba-131">Después de clonar el repositorio, use Visual Studio para abrir el archivo de solución **Microsoft.Teams. Samples.HelloWorld.sln** del directorio **Microsoft-Teams-Samples/samples/app-hello-world/csharp** del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6faba-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="6faba-132">A continuación, seleccione **Compilar solución** en el menú **Compilar.**</span><span class="sxs-lookup"><span data-stu-id="6faba-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="6faba-133">Para ejecutar el ejemplo, presione **F5** o seleccione **Iniciar depuración** en el menú **Depurar.**</span><span class="sxs-lookup"><span data-stu-id="6faba-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="6faba-134">Cuando se inicia la aplicación, se abre una ventana del explorador con la raíz de la aplicación iniciada.</span><span class="sxs-lookup"><span data-stu-id="6faba-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="6faba-135">Puede ir a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se están cargando:</span><span class="sxs-lookup"><span data-stu-id="6faba-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="6faba-136">Si recibe un `Could not find a part of the path … bin\roslyn\csc.exe` error, actualice el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="6faba-136">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="6faba-137">Para obtener más información, consulte [esta pregunta sobre Desbordamiento de pila](https://stackoverflow.com/questions/32780315).</span><span class="sxs-lookup"><span data-stu-id="6faba-137">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="6faba-138">Hospede la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6faba-138">Host the sample app</span></span>

<span data-ttu-id="6faba-139">Las aplicaciones en Microsoft Teams son aplicaciones web que proporcionan una o más capacidades.</span><span class="sxs-lookup"><span data-stu-id="6faba-139">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="6faba-140">Para que la plataforma Teams cargue la aplicación, la aplicación debe estar disponible en Internet.</span><span class="sxs-lookup"><span data-stu-id="6faba-140">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="6faba-141">Para ello, debe hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6faba-141">To do this, you need to host your app.</span></span> <span data-ttu-id="6faba-142">Puede alojarlo en Microsoft Azure de forma gratuita o crear un túnel al proceso local en su ordenador mediante `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="6faba-142">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="6faba-143">Después de hospedar la aplicación, anote su DIRECCIÓN URL raíz, como `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="6faba-143">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="6faba-144">Tunnel usando ngrok</span><span class="sxs-lookup"><span data-stu-id="6faba-144">Tunnel using ngrok</span></span>

<span data-ttu-id="6faba-145">Para realizar pruebas rápidas, puede ejecutar la aplicación en el equipo y crear un túnel a través de un punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="6faba-145">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="6faba-146">[`ngrok`](https://ngrok.com) es una herramienta gratuita con la que se puede obtener una dirección web, como `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="6faba-146">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="6faba-147">Puede [descargar e instalar](https://ngrok.com/download) ngrok y agregarlo a una ubicación en su `PATH` archivo .</span><span class="sxs-lookup"><span data-stu-id="6faba-147">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="6faba-148">Después de instalar `ngrok` , abra una nueva ventana de terminal y ejecute el siguiente comando para crear un túnel:</span><span class="sxs-lookup"><span data-stu-id="6faba-148">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="6faba-149">`Ngrok` escucha las solicitudes de Internet y las enruta a la aplicación que se ejecuta en el puerto 44327.</span><span class="sxs-lookup"><span data-stu-id="6faba-149">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="6faba-150">Para comprobarlo, abre el navegador y ve a cargar la `https://d0ac14a5.ngrok.io/hello` página de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6faba-150">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="6faba-151">En lugar de esta dirección URL, utilice la dirección de reenvío que se muestra `ngrok` en la sesión de consola.</span><span class="sxs-lookup"><span data-stu-id="6faba-151">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="6faba-152">Si ha utilizado un puerto diferente en el paso [de compilación y ejecución,](#build-and-run-the-sample) asegúrese de utilizar el mismo número de puerto para configurar el `ngrok` túnel.</span><span class="sxs-lookup"><span data-stu-id="6faba-152">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="6faba-153">Es una buena idea correr `ngrok` en una ventana de terminal diferente.</span><span class="sxs-lookup"><span data-stu-id="6faba-153">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="6faba-154">Esto se hace para evitar `ngrok` que se ejecute sin interferir con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6faba-154">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="6faba-155">Tienes que detener, reconstruir y volver a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6faba-155">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="6faba-156">La `ngrok` sesión proporciona información útil de depuración en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="6faba-156">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="6faba-157">La aplicación solo está disponible durante la sesión actual en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6faba-157">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="6faba-158">Si la máquina está apagada o se va a dormir, el servicio ya no está disponible.</span><span class="sxs-lookup"><span data-stu-id="6faba-158">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="6faba-159">Recuerde esto cuando comparta la aplicación para realizar pruebas a otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="6faba-159">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="6faba-160">Si tiene que reiniciar el servicio, la aplicación devuelve una nueva dirección y debe actualizar todas las ubicaciones que usan esa dirección.</span><span class="sxs-lookup"><span data-stu-id="6faba-160">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="6faba-161">La versión de pago `ngrok` de no tiene esta limitación.</span><span class="sxs-lookup"><span data-stu-id="6faba-161">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="6faba-162">Host en Azure</span><span class="sxs-lookup"><span data-stu-id="6faba-162">Host in Azure</span></span>

<span data-ttu-id="6faba-163">Microsoft Azure hospeda la aplicación .NET en un nivel gratuito mediante la infraestructura compartida.</span><span class="sxs-lookup"><span data-stu-id="6faba-163">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="6faba-164">Esto es suficiente para ejecutar el `Hello World` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6faba-164">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="6faba-165">Para obtener más información, consulte [Creación de una nueva cuenta gratuita de Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="6faba-165">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="6faba-166">Visual Studio tiene compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure:</span><span class="sxs-lookup"><span data-stu-id="6faba-166">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="6faba-167">Actualice las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="6faba-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="6faba-168">La aplicación de ejemplo requiere que las variables de entorno se establezcan en los valores que guardó en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="6faba-168">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="6faba-169">Abra el archivo `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="6faba-169">Open the `appsettings.json` file.</span></span> <span data-ttu-id="6faba-170">Actualice el valor **de MicrosoftAppId** con el identificador de bot que guardó en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="6faba-170">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="6faba-171">Actualice **MicrosoftAppPassword** con la contraseña del bot que guardó.</span><span class="sxs-lookup"><span data-stu-id="6faba-171">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="6faba-172">Una vez realizados estos cambios, vuelva a generar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6faba-172">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="6faba-173">Si usa ngrok, ejecute la aplicación localmente y, si hospeda en Azure, vuelva a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6faba-173">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="6faba-174">Configurar la pestaña de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6faba-174">Configure the app tab</span></span>

<span data-ttu-id="6faba-175">Una vez que instale la aplicación en un equipo, debe configurarla para mostrar contenido.</span><span class="sxs-lookup"><span data-stu-id="6faba-175">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="6faba-176">Vaya a un canal del equipo donde instaló la aplicación de ejemplo y seleccione el botón **'+'** para agregar una nueva pestaña. Elija **Hello World** en la lista Agregar una **pestaña.**</span><span class="sxs-lookup"><span data-stu-id="6faba-176">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="6faba-177">Se muestra un cuadro de diálogo de configuración que le permite elegir la pestaña que se va a mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="6faba-177">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="6faba-178">Después de seleccionar la pestaña y seleccionar **Guardar** la `Hello World` pestaña se carga con la pestaña.</span><span class="sxs-lookup"><span data-stu-id="6faba-178">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="6faba-179">Prueba tu bot en Teams</span><span class="sxs-lookup"><span data-stu-id="6faba-179">Test your bot in Teams</span></span>

<span data-ttu-id="6faba-180">Ahora puede probar el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="6faba-180">Now you can test the bot in Teams.</span></span> <span data-ttu-id="6faba-181">Seleccione un canal en el equipo donde registró la aplicación y escriba `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="6faba-181">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="6faba-182">Esto se denomina **\@ mención.**</span><span class="sxs-lookup"><span data-stu-id="6faba-182">This is called an **\@mention**.</span></span> <span data-ttu-id="6faba-183">El bot responde a cualquier mensaje que envíe.</span><span class="sxs-lookup"><span data-stu-id="6faba-183">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="6faba-184">Prueba tu extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="6faba-184">Test your messaging extension</span></span>

<span data-ttu-id="6faba-185">Para probar la extensión de mensajería, puede seleccionar **...** debajo del cuadro de entrada en su vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="6faba-185">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="6faba-186">Se muestra un menú con la aplicación **'Hello World'.**</span><span class="sxs-lookup"><span data-stu-id="6faba-186">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="6faba-187">Al seleccionarlo, se muestra un conjunto de textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="6faba-187">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="6faba-188">Puede seleccionar uno de los textos aleatorios y que se inserta en su conversación.</span><span class="sxs-lookup"><span data-stu-id="6faba-188">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="6faba-189">Seleccione uno de los textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="6faba-189">Select one of the random text.</span></span> <span data-ttu-id="6faba-190">Se muestra una tarjeta formateada y lista para enviar con su propio mensaje.</span><span class="sxs-lookup"><span data-stu-id="6faba-190">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
