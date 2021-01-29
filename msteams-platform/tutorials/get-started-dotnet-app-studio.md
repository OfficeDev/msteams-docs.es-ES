---
title: 'Tutorial: crear la primera aplicación con C #'
description: Obtenga información sobre cómo empezar a compilar aplicaciones de Microsoft Teams con C#/.NET.
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037042"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a><span data-ttu-id="bff32-104">Crear la primera aplicación de Microsoft Teams con C #</span><span class="sxs-lookup"><span data-stu-id="bff32-104">Create your first Microsoft Teams app using C#</span></span>

<span data-ttu-id="bff32-105">Este tutorial le ayuda a empezar a crear una aplicación de Microsoft Teams con C# en .NET.</span><span class="sxs-lookup"><span data-stu-id="bff32-105">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="bff32-106">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bff32-106">Get prerequisites</span></span>

<span data-ttu-id="bff32-107">Para completar este tutorial, debe obtener las siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="bff32-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="bff32-108">Instalar Git</span><span class="sxs-lookup"><span data-stu-id="bff32-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="bff32-109">[Instalar Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bff32-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bff32-110">Puedes instalar la edición gratuita de la comunidad.</span><span class="sxs-lookup"><span data-stu-id="bff32-110">You can install the free community edition.</span></span>

<span data-ttu-id="bff32-111">Si ve una opción para agregar a PATH durante la `git` instalación, elija hacerlo.</span><span class="sxs-lookup"><span data-stu-id="bff32-111">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="bff32-112">Será útil.</span><span class="sxs-lookup"><span data-stu-id="bff32-112">It will be handy.</span></span>

<span data-ttu-id="bff32-113">Compruebe la `git` instalación ejecutando lo siguiente en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="bff32-113">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="bff32-114">Usa la ventana de terminal con la que te sientas más cómodo en tu plataforma.</span><span class="sxs-lookup"><span data-stu-id="bff32-114">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="bff32-115">Estos ejemplos usan Bash, pero se ejecutarán en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="bff32-115">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="bff32-116">Asegúrate de iniciar la versión más reciente de Visual Studio e instalar las actualizaciones si se muestran.</span><span class="sxs-lookup"><span data-stu-id="bff32-116">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="bff32-117">Puede seguir usando esta ventana de terminal para ejecutar los comandos siguientes en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bff32-117">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="bff32-118">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="bff32-118">Download the sample</span></span>

<span data-ttu-id="bff32-119">Hemos proporcionado un saludo [sencillo, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="bff32-119">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="bff32-120">muestra en C# para empezar.</span><span class="sxs-lookup"><span data-stu-id="bff32-120">sample in C# to get you started.</span></span> <span data-ttu-id="bff32-121">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="bff32-121">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="bff32-122">Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio si](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) desea modificar y comprobar los cambios en GitHub para consultarlos en el futuro.</span><span class="sxs-lookup"><span data-stu-id="bff32-122">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="bff32-123">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="bff32-123">Build and run the sample</span></span>

<span data-ttu-id="bff32-124">Una vez clonado el repositorio, use Visual Studio para abrir el archivo de solución desde el directorio raíz del ejemplo y haga clic `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` en el `Build` menú.</span><span class="sxs-lookup"><span data-stu-id="bff32-124">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="bff32-125">Puede ejecutar la muestra presionando `F5` o eligiendo `Start Debugging` en el `Debug` menú.</span><span class="sxs-lookup"><span data-stu-id="bff32-125">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="bff32-126">Cuando se inicia la aplicación, verás una ventana del explorador abierta con la raíz de la aplicación iniciada.</span><span class="sxs-lookup"><span data-stu-id="bff32-126">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="bff32-127">Puedes navegar a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="bff32-127">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="bff32-128">Si recibe un error como `Could not find a part of the path … bin\roslyn\csc.exe` , pruebe a actualizar el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="bff32-128">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="bff32-129">Consulta [esta pregunta en StackOverflow para](https://stackoverflow.com/questions/32780315) obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="bff32-129">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="bff32-130">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bff32-130">Host the sample app</span></span>

<span data-ttu-id="bff32-131">Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="bff32-131">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="bff32-132">Para que la plataforma de Teams cargue la aplicación, debe ser accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="bff32-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="bff32-133">Para que la aplicación sea accesible desde Internet, debes hospedarla.</span><span class="sxs-lookup"><span data-stu-id="bff32-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="bff32-134">Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel al proceso local en el equipo de desarrollo mediante `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="bff32-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="bff32-135">Cuando termines de hospedar la aplicación, toma nota de su dirección URL raíz.</span><span class="sxs-lookup"><span data-stu-id="bff32-135">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="bff32-136">Tendrá un aspecto como: `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="bff32-136">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="bff32-137">Túnel con ngrok</span><span class="sxs-lookup"><span data-stu-id="bff32-137">Tunnel using ngrok</span></span>

<span data-ttu-id="bff32-138">Para realizar pruebas rápidas, puedes ejecutar la aplicación en el equipo local y crear un túnel a ella a través de un punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="bff32-138">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="bff32-139">[ngrok](https://ngrok.com) es una herramienta gratuita que te permite hacerlo.</span><span class="sxs-lookup"><span data-stu-id="bff32-139">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="bff32-140">Con ngrok puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo).</span><span class="sxs-lookup"><span data-stu-id="bff32-140">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="bff32-141">Puede descargar [e instalar](https://ngrok.com/download) ngrok para su entorno.</span><span class="sxs-lookup"><span data-stu-id="bff32-141">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="bff32-142">Asegúrese de agregarlo a una ubicación en el `PATH` archivo .</span><span class="sxs-lookup"><span data-stu-id="bff32-142">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="bff32-143">Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel.</span><span class="sxs-lookup"><span data-stu-id="bff32-143">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="bff32-144">El ejemplo usa el puerto 3333, así que asegúrate de especificarlo aquí.</span><span class="sxs-lookup"><span data-stu-id="bff32-144">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="bff32-145">Ngrok escuchará las solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333.</span><span class="sxs-lookup"><span data-stu-id="bff32-145">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="bff32-146">Para comprobarlo, abre el explorador y vas a `https://d0ac14a5.ngrok.io/hello` cargar la página hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bff32-146">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="bff32-147">Asegúrese de usar la dirección de reenvío mostrada por ngrok en la sesión de la consola en lugar de esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="bff32-147">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="bff32-148">Si ha usado un puerto [](#build-and-run-the-sample) diferente en la compilación y ejecuta el paso anterior, asegúrese de usar el mismo número de puerto para configurar el `ngrok` túnel.</span><span class="sxs-lookup"><span data-stu-id="bff32-148">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="bff32-149">Es una buena idea ejecutarse en una ventana de terminal diferente para mantenerla en funcionamiento sin interferir con la aplicación que más adelante podría tener que detener, recompilar y `ngrok` volver a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="bff32-149">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="bff32-150">La `ngrok` sesión devolverá información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="bff32-150">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="bff32-151">La aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="bff32-151">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="bff32-152">Si la máquina se apaga o deja de estar en modo de suspensión, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="bff32-152">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="bff32-153">Recuerda esto al compartir la aplicación para pruebas por parte de otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="bff32-153">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="bff32-154">Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar cada lugar que use esa dirección.</span><span class="sxs-lookup"><span data-stu-id="bff32-154">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="bff32-155">La versión de pago de Ngrok no tiene esta limitación.</span><span class="sxs-lookup"><span data-stu-id="bff32-155">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="bff32-156">Host en Azure</span><span class="sxs-lookup"><span data-stu-id="bff32-156">Host in Azure</span></span>

<span data-ttu-id="bff32-157">Microsoft Azure le permite hospedar la aplicación .NET en un nivel gratuito mediante la infraestructura compartida.</span><span class="sxs-lookup"><span data-stu-id="bff32-157">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="bff32-158">Esto será suficiente para ejecutar este `Hello World` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bff32-158">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="bff32-159">Vea [la creación de una nueva cuenta gratuita](https://azure.microsoft.com/free/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="bff32-159">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="bff32-160">Visual Studio compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure.</span><span class="sxs-lookup"><span data-stu-id="bff32-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="bff32-161">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="bff32-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="bff32-162">La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores que has tomado nota anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bff32-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="bff32-163">Abra el archivo appsettings.jsarchivo.</span><span class="sxs-lookup"><span data-stu-id="bff32-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="bff32-164">Actualice el *valor de MicrosoftAppId* con el identificador de bot que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bff32-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="bff32-165">Actualice *MicrosoftAppPassword* con la contraseña del bot que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bff32-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="bff32-166">Una vez realizados estos cambios, vuelve a generar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bff32-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="bff32-167">Si usa ngrok, ejecute la aplicación localmente y, si va a hospedarla en Azure, vuelva a implementarla.</span><span class="sxs-lookup"><span data-stu-id="bff32-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="bff32-168">Configurar la pestaña de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bff32-168">Configure the app tab</span></span>

<span data-ttu-id="bff32-169">Una vez que instales la aplicación en un equipo, deberás configurarla para mostrar contenido.</span><span class="sxs-lookup"><span data-stu-id="bff32-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="bff32-170">Ve a un canal del equipo donde instalaste la aplicación de muestra y haz clic en el botón **"+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir en la lista Agregar **una** pestaña.</span><span class="sxs-lookup"><span data-stu-id="bff32-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="bff32-171">A continuación, aparecerá un cuadro de diálogo de configuración.</span><span class="sxs-lookup"><span data-stu-id="bff32-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="bff32-172">Este cuadro de diálogo te permitirá elegir qué pestaña mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="bff32-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="bff32-173">Una vez que seleccione la pestaña y haga clic en esta, podrá ver la `Save` pestaña cargada con la pestaña que `Hello World` eligió.</span><span class="sxs-lookup"><span data-stu-id="bff32-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="bff32-174">Probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="bff32-174">Test your bot in Teams</span></span>

<span data-ttu-id="bff32-175">Ahora puede interactuar con el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="bff32-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="bff32-176">Elija un canal en el equipo donde registró la aplicación y escriba `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="bff32-176">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="bff32-177">Esto se denomina una **\@ mención.**</span><span class="sxs-lookup"><span data-stu-id="bff32-177">This is called an **\@mention**.</span></span> <span data-ttu-id="bff32-178">Cualquier mensaje que envíe al bot se le enviará como respuesta.</span><span class="sxs-lookup"><span data-stu-id="bff32-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="bff32-179">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="bff32-179">Test your messaging extension</span></span>

<span data-ttu-id="bff32-180">Para probar la extensión de mensajería, puedes hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="bff32-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="bff32-181">Aparecerá un menú con la **aplicación "Hola** a todos".</span><span class="sxs-lookup"><span data-stu-id="bff32-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="bff32-182">Al hacer clic en él, verás un montón de textos aleatorios que se muestran.</span><span class="sxs-lookup"><span data-stu-id="bff32-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="bff32-183">Puede elegir cualquiera de ellos y se insertará en la conversación.</span><span class="sxs-lookup"><span data-stu-id="bff32-183">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="bff32-184">Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="bff32-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
