---
title: Introducción a C#/.NET
description: Empezar a compilar excelentes aplicaciones en Microsoft Teams con C#/.NET
keywords: Introducción a .net c# CSharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c29fdde23ff6ff0e8269ccaf256c5154c0145a7b
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210697"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a><span data-ttu-id="931c6-104">Introducción a la plataforma de Microsoft Teams con C#/.NET y app Studio</span><span class="sxs-lookup"><span data-stu-id="931c6-104">Get started on the Microsoft Teams platform with C#/.NET and App Studio</span></span>

<span data-ttu-id="931c6-105">La plataforma de desarrolladores de [Microsoft Teams](/microsoftteams/) facilita la tarea de ampliar Teams e integrar sus propias aplicaciones y servicios sin problemas en el área de trabajo de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="931c6-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="931c6-106">A continuación, estas aplicaciones pueden distribuirse a su empresa o a equipos de todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="931c6-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="931c6-107">Para ampliar Microsoft Teams, tendrá que crear una aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="931c6-107">To extend Microsoft Teams, you will need to create a Microsoft Teams app.</span></span> <span data-ttu-id="931c6-108">Una aplicación de Microsoft Teams es una aplicación web que hospeda.</span><span class="sxs-lookup"><span data-stu-id="931c6-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="931c6-109">A continuación, esta aplicación se puede integrar en el área de trabajo del usuario en Teams.</span><span class="sxs-lookup"><span data-stu-id="931c6-109">This app can then be integrated into the user's workspace in Teams.</span></span>

<span data-ttu-id="931c6-110">Este tutorial le ayudará a empezar a crear una aplicación de Microsoft Teams con C# en .NET.</span><span class="sxs-lookup"><span data-stu-id="931c6-110">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span> <span data-ttu-id="931c6-111">Puede probar la aplicación cargándose en un equipo para el que tenga permisos o en un inquilino de prueba creado con el programa de desarrolladores de Office.</span><span class="sxs-lookup"><span data-stu-id="931c6-111">You can test the app by loading it into a Team that you have permissions for, or into a test tenant created using the Office Developer Program.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="931c6-112">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="931c6-112">Get prerequisites</span></span>

<span data-ttu-id="931c6-113">Para completar este tutorial, necesita obtener las siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="931c6-113">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="931c6-114">Instalar git</span><span class="sxs-lookup"><span data-stu-id="931c6-114">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="931c6-115">[Instale Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="931c6-115">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="931c6-116">Puede instalar la edición gratuita de la comunidad.</span><span class="sxs-lookup"><span data-stu-id="931c6-116">You can install the free community edition.</span></span>

<span data-ttu-id="931c6-117">Si ve una opción para agregar `git` a la ruta de acceso durante la instalación, elija esta opción.</span><span class="sxs-lookup"><span data-stu-id="931c6-117">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="931c6-118">Será útil.</span><span class="sxs-lookup"><span data-stu-id="931c6-118">It will be handy.</span></span>

<span data-ttu-id="931c6-119">`git`Ejecute lo siguiente en una ventana de terminal para comprobar la instalación:</span><span class="sxs-lookup"><span data-stu-id="931c6-119">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="931c6-120">Use la ventana de terminal que le resulte más cómoda en su plataforma.</span><span class="sxs-lookup"><span data-stu-id="931c6-120">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="931c6-121">Estos ejemplos usan Bash, pero se ejecutarán en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="931c6-121">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="931c6-122">Asegúrese de iniciar la versión más reciente de Visual Studio e instale las actualizaciones si se muestran.</span><span class="sxs-lookup"><span data-stu-id="931c6-122">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="931c6-123">Puede seguir usando esta ventana de terminal para ejecutar los comandos que se indican a continuación en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="931c6-123">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="931c6-124">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="931c6-124">Download the sample</span></span>

<span data-ttu-id="931c6-125">Hemos proporcionado un sencillo [Hola a todos.](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="931c6-125">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="931c6-126">muestra en C# para empezar.</span><span class="sxs-lookup"><span data-stu-id="931c6-126">sample in C# to get you started.</span></span> <span data-ttu-id="931c6-127">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="931c6-127">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="931c6-128">Puede [bifurcar](https://help.github.com/articles/fork-a-repo/) este [repositorio](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) si desea modificar y proteger los cambios en github para futuras referencias.</span><span class="sxs-lookup"><span data-stu-id="931c6-128">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="931c6-129">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="931c6-129">Build and run the sample</span></span>

<span data-ttu-id="931c6-130">Una vez que el repositorio se haya clonado, use Visual Studio para abrir el archivo `Microsoft.Teams.Samples.HelloWorld.sln` de solución desde el directorio raíz del ejemplo y haga clic en `Build Solution` desde el `Build` menú.</span><span class="sxs-lookup"><span data-stu-id="931c6-130">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="931c6-131">Puede ejecutar el ejemplo presionando `F5` o eligiendo `Start Debugging` en el `Debug` menú.</span><span class="sxs-lookup"><span data-stu-id="931c6-131">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="931c6-132">Cuando se inicie la aplicación, verá una ventana del explorador abierta con la raíz de la aplicación iniciada.</span><span class="sxs-lookup"><span data-stu-id="931c6-132">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="931c6-133">Puede navegar a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se cargan:</span><span class="sxs-lookup"><span data-stu-id="931c6-133">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="931c6-134">Si recibe un error como `Could not find a part of the path … bin\roslyn\csc.exe` , intente actualizar el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="931c6-134">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="931c6-135">Vea [esta pregunta en stackoverflow](https://stackoverflow.com/questions/32780315) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="931c6-135">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="931c6-136">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="931c6-136">Host the sample app</span></span>

<span data-ttu-id="931c6-137">Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más capacidades.</span><span class="sxs-lookup"><span data-stu-id="931c6-137">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="931c6-138">Para que la plataforma de Microsoft Teams cargue la aplicación, la aplicación debe ser accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="931c6-138">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="931c6-139">Para hacer que la aplicación sea accesible desde Internet, debe hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="931c6-139">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="931c6-140">Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel para el proceso local en el equipo de desarrollo mediante `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="931c6-140">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="931c6-141">Cuando termine de hospedar la aplicación, anote su dirección URL raíz.</span><span class="sxs-lookup"><span data-stu-id="931c6-141">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="931c6-142">Tendrá un aspecto similar a: `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="931c6-142">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="931c6-143">Túnel mediante ngrok</span><span class="sxs-lookup"><span data-stu-id="931c6-143">Tunnel using ngrok</span></span>

<span data-ttu-id="931c6-144">Para realizar pruebas rápidas, puede ejecutar la aplicación en el equipo local y crear un túnel a través de un punto de conexión Web.</span><span class="sxs-lookup"><span data-stu-id="931c6-144">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="931c6-145">[ngrok](https://ngrok.com) es una herramienta gratuita que le permite hacer justamente eso.</span><span class="sxs-lookup"><span data-stu-id="931c6-145">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="931c6-146">Con ngrok puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo).</span><span class="sxs-lookup"><span data-stu-id="931c6-146">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="931c6-147">Puede [Descargar e instalar](https://ngrok.com/download) ngrok para su entorno.</span><span class="sxs-lookup"><span data-stu-id="931c6-147">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="931c6-148">Asegúrese de agregarlo a una ubicación en el `PATH` .</span><span class="sxs-lookup"><span data-stu-id="931c6-148">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="931c6-149">Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel.</span><span class="sxs-lookup"><span data-stu-id="931c6-149">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="931c6-150">En el ejemplo se usa el puerto 3333, por lo que debe asegurarse de especificarlo aquí.</span><span class="sxs-lookup"><span data-stu-id="931c6-150">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="931c6-151">Ngrok escuchará solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333.</span><span class="sxs-lookup"><span data-stu-id="931c6-151">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="931c6-152">Para comprobarlo, abra el explorador y vaya a `https://d0ac14a5.ngrok.io/hello` para cargar la página Hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="931c6-152">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="931c6-153">Asegúrese de usar la dirección de reenvío que muestra ngrok en la sesión de consola en lugar de esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="931c6-153">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="931c6-154">Si ha usado un puerto diferente en el paso de [compilación y ejecutar](#build-and-run-the-sample) anterior, asegúrese de que usa el mismo número de puerto para configurar el `ngrok` túnel.</span><span class="sxs-lookup"><span data-stu-id="931c6-154">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="931c6-155">Es aconsejable ejecutar `ngrok` en una ventana de terminal diferente para mantenerla en ejecución sin interferir con la aplicación que, posteriormente, se debe detener, volver a crear y volver a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="931c6-155">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="931c6-156">La `ngrok` sesión devolverá información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="931c6-156">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="931c6-157">La aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="931c6-157">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="931c6-158">Si el equipo está apagado o entra en suspensión, el servicio dejará de estar disponible.</span><span class="sxs-lookup"><span data-stu-id="931c6-158">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="931c6-159">Recuerde esto cuando comparta la aplicación para que la prueben otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="931c6-159">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="931c6-160">Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar todos los sitios que usen esa dirección.</span><span class="sxs-lookup"><span data-stu-id="931c6-160">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="931c6-161">La versión de pago de Ngrok no tiene esta limitación.</span><span class="sxs-lookup"><span data-stu-id="931c6-161">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="931c6-162">Hospedar en Azure</span><span class="sxs-lookup"><span data-stu-id="931c6-162">Host in Azure</span></span>

<span data-ttu-id="931c6-163">Microsoft Azure le permite hospedar su aplicación .NET en un nivel gratuito mediante una infraestructura compartida.</span><span class="sxs-lookup"><span data-stu-id="931c6-163">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="931c6-164">Esto será suficiente para ejecutar este `Hello World` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="931c6-164">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="931c6-165">Consulte [creación de una nueva cuenta gratuita](https://azure.microsoft.com/free/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="931c6-165">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="931c6-166">Visual Studio tiene compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure.</span><span class="sxs-lookup"><span data-stu-id="931c6-166">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" src="~/assets/images/get-started/publishtoazure1.png" title="Visual Studio"/>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="931c6-168">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="931c6-168">Update the credentials for your hosted app</span></span>

<span data-ttu-id="931c6-169">La aplicación de ejemplo requiere que se establezcan las siguientes variables de entorno en los valores que ha anotado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="931c6-169">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="931c6-170">Abra el archivo appSettings. JSON.</span><span class="sxs-lookup"><span data-stu-id="931c6-170">Open up the appsettings.json file.</span></span> <span data-ttu-id="931c6-171">Actualice el valor *MicrosoftAppId* con el identificador de bot que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="931c6-171">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="931c6-172">Actualice *MicrosoftAppPassword* con la contraseña de bot que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="931c6-172">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" src="~/assets/images/get-started/get-started-net-azure-add-keys.png" title="configuración de las claves"/>

<span data-ttu-id="931c6-174">Una vez realizados estos cambios, reconstruya la aplicación.</span><span class="sxs-lookup"><span data-stu-id="931c6-174">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="931c6-175">Si usa ngrok, ejecute la aplicación localmente y, si hospeda en Azure, vuelva a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="931c6-175">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="931c6-176">Configurar la pestaña de la aplicación</span><span class="sxs-lookup"><span data-stu-id="931c6-176">Configure the app tab</span></span>

<span data-ttu-id="931c6-177">Una vez que haya instalado la aplicación en un equipo, tendrá que configurarla para mostrar el contenido.</span><span class="sxs-lookup"><span data-stu-id="931c6-177">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="931c6-178">Vaya a un canal del equipo en el que haya instalado la aplicación de ejemplo y haga clic en el botón **"+"** para agregar una nueva pestaña. A continuación, puede elegir `Hello World` en la lista **Agregar una pestaña** .</span><span class="sxs-lookup"><span data-stu-id="931c6-178">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="931c6-179">A continuación, se mostrará un cuadro de diálogo de configuración.</span><span class="sxs-lookup"><span data-stu-id="931c6-179">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="931c6-180">Este cuadro de diálogo le permitirá elegir la pestaña que desea mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="931c6-180">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="931c6-181">Una vez que seleccione la pestaña y haga clic en `Save` , puede ver la `Hello World` ficha cargada con la pestaña que eligió.</span><span class="sxs-lookup"><span data-stu-id="931c6-181">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" src="~/assets/images/samples-hello-world-tab-configure.png" title="Captura de pantalla de configurar" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="931c6-183">Probar el bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="931c6-183">Test your bot in Teams</span></span>

<span data-ttu-id="931c6-184">Ahora puede interactuar con el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="931c6-184">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="931c6-185">Elija un canal del equipo en el que haya registrado la aplicación y escriba `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="931c6-185">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="931c6-186">Esto se denomina una \*\* \@ mención\*\*.</span><span class="sxs-lookup"><span data-stu-id="931c6-186">This is called an **\@mention**.</span></span> <span data-ttu-id="931c6-187">Cualquier mensaje que envíe al bot se le enviará como respuesta.</span><span class="sxs-lookup"><span data-stu-id="931c6-187">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" title="Respuestas de bot" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="931c6-189">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="931c6-189">Test your messaging extension</span></span>

<span data-ttu-id="931c6-190">Para probar la extensión de mensajería, puede hacer clic en los tres puntos situados debajo del cuadro de entrada en la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="931c6-190">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="931c6-191">Se mostrará un menú con la aplicación **"Hola a todos"** .</span><span class="sxs-lookup"><span data-stu-id="931c6-191">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="931c6-192">Al hacer clic en él, verá una serie de textos aleatorios que aparecen.</span><span class="sxs-lookup"><span data-stu-id="931c6-192">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="931c6-193">Puede elegir una de ellas y se insertará en la conversación.</span><span class="sxs-lookup"><span data-stu-id="931c6-193">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" title="Menú de extensiones de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" title="Resultado de la extensión de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="931c6-196">Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="931c6-196">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" title="Envío de extensiones de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
