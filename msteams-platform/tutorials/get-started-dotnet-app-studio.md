---
title: 'Tutorial: crear la primera aplicación con C #'
description: Obtenga información sobre cómo empezar a compilar aplicaciones de Microsoft Teams con C# o .NET.
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: b37a8d555117e38383504dc99d82d564439a3ebf
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231534"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="f7ad0-104">Crear la primera aplicación de Teams con C# o .NET</span><span class="sxs-lookup"><span data-stu-id="f7ad0-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="f7ad0-105">Este tutorial le ayuda a crear una aplicación de Microsoft Teams con C# o .NET.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="f7ad0-106">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f7ad0-106">Get prerequisites</span></span>

<span data-ttu-id="f7ad0-107">Para completar este tutorial, debe obtener las siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="f7ad0-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="f7ad0-108">Instalar Git</span><span class="sxs-lookup"><span data-stu-id="f7ad0-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="f7ad0-109">[Instalar Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f7ad0-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="f7ad0-110">Puedes instalar la edición gratuita de la comunidad.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-110">You can install the free community edition.</span></span>

<span data-ttu-id="f7ad0-111">Durante la instalación, si hay una opción para agregar `git` a PATH, eligréla.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-111">During installation, if there is an option to add `git` to the PATH, choose it.</span></span>

<span data-ttu-id="f7ad0-112">En una ventana de terminal, ejecute el siguiente comando para comprobar la `git` instalación:</span><span class="sxs-lookup"><span data-stu-id="f7ad0-112">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="f7ad0-113">Usa una ventana de terminal adecuada en tu plataforma.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-113">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="f7ad0-114">Estos ejemplos usan Bash, pero se ejecutan en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-114">These examples use Bash but run on most platforms.</span></span>

<span data-ttu-id="f7ad0-115">Asegúrate de iniciar la versión más reciente de Visual Studio e instalar las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-115">Make sure to launch the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="f7ad0-116">Puede usar la misma ventana de terminal para ejecutar los comandos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-116">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="f7ad0-117">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7ad0-117">Download the sample</span></span>

<span data-ttu-id="f7ad0-118">Puedes empezar con un sencillo [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="f7ad0-118">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="f7ad0-119">muestra en C#.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-119">sample in C#.</span></span> <span data-ttu-id="f7ad0-120">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="f7ad0-120">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="f7ad0-121">Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio para](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) modificar y guardar los cambios en GitHub como referencia.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-121">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) to modify and save your changes to GitHub for reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="f7ad0-122">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7ad0-122">Build and run the sample</span></span>

<span data-ttu-id="f7ad0-123">Después de clonar el repositorio, use Visual Studio para abrir el archivo de solución desde el directorio raíz del ejemplo y `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` seleccionarlo en el `Build` menú.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-123">After the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and select `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="f7ad0-124">Para ejecutar la muestra, `F5` pulse o elija en el `Start Debugging` `Debug` menú.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-124">To run the sample press `F5` or choose `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="f7ad0-125">Cuando se inicia la aplicación, se abre una ventana del explorador con la raíz de la aplicación iniciada.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-125">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="f7ad0-126">Puedes navegar a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f7ad0-126">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- <span data-ttu-id="f7ad0-127">[https://localhost:44327/second]https://localhost:44327/second)</span><span class="sxs-lookup"><span data-stu-id="f7ad0-127">[https://localhost:44327/second]https://localhost:44327/second)</span></span>

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="f7ad0-128">Si recibe un `Could not find a part of the path … bin\roslyn\csc.exe` error, actualice el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="f7ad0-128">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="f7ad0-129">Para obtener más información, [vea esta pregunta en StackOverflow](https://stackoverflow.com/questions/32780315).</span><span class="sxs-lookup"><span data-stu-id="f7ad0-129">For more information, see [this question on StackOverflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="f7ad0-130">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7ad0-130">Host the sample app</span></span>

<span data-ttu-id="f7ad0-131">Las aplicaciones de Microsoft Teams son aplicaciones web que proporcionan una o más funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-131">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="f7ad0-132">Para que la plataforma de Teams cargue la aplicación, debe ser accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="f7ad0-133">Para que la aplicación sea accesible desde Internet, debes hospedarla.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="f7ad0-134">Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel al proceso local en el equipo de desarrollo mediante `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="f7ad0-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="f7ad0-135">Cuando termine de hospedar la aplicación, anote su dirección URL raíz.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-135">When you finish hosting your app, note its root URL.</span></span> <span data-ttu-id="f7ad0-136">Por ejemplo, `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="f7ad0-136">For example, `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="f7ad0-137">Túnel con ngrok</span><span class="sxs-lookup"><span data-stu-id="f7ad0-137">Tunnel using ngrok</span></span>

<span data-ttu-id="f7ad0-138">Para realizar pruebas rápidas, puedes ejecutar la aplicación en el equipo local y crear un túnel a ella a través de un punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-138">For quick testing, you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="f7ad0-139">[ngrok](https://ngrok.com) es una herramienta gratuita con la que puede obtener una dirección web como `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="f7ad0-139">[ngrok](https://ngrok.com) is a free tool with which you can get a web address such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="f7ad0-140">Puede descargar [e instalar](https://ngrok.com/download) ngrok.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-140">You can [download and install](https://ngrok.com/download) ngrok.</span></span> <span data-ttu-id="f7ad0-141">Asegúrese de agregarlo a una ubicación en el `PATH` archivo .</span><span class="sxs-lookup"><span data-stu-id="f7ad0-141">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="f7ad0-142">Después de instalar ngrok, abra una nueva ventana de terminal y ejecute el siguiente comando para crear un túnel:</span><span class="sxs-lookup"><span data-stu-id="f7ad0-142">After you install ngrok, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="f7ad0-143">El ejemplo usa el puerto 44327 para asegurarse de especificarlo.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-143">The sample uses port 44327 be sure to specify it.</span></span>

<span data-ttu-id="f7ad0-144">Ngrok escucha las solicitudes de Internet y las enruta a la aplicación que se ejecuta en el puerto 44327.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-144">Ngrok listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="f7ad0-145">Para comprobarlo, abre el explorador y ve `https://d0ac14a5.ngrok.io/hello` a cargar la página hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-145">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="f7ad0-146">En lugar de esta dirección URL, usa la dirección de reenvío que muestra ngrok en la sesión de la consola.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-146">Instead of this URL, use the forwarding address displayed by ngrok in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="f7ad0-147">Si ha usado un puerto [](#build-and-run-the-sample) diferente en el paso de compilación y ejecución, asegúrese de usar el mismo número de puerto para configurar el `ngrok` túnel.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-147">If you have used a different port in the [build and run](#build-and-run-the-sample) step, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="f7ad0-148">Es una buena idea ejecutarse `ngrok` en una ventana de terminal diferente.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-148">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="f7ad0-149">Esto se hace para evitar que ngrok se ejecute sin interferir con la aplicación, que tienes que detener, recompilar y volver a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-149">This is done to keep ngrok from running without interfering with the app, which you have to stop, rebuild, and rerun.</span></span> <span data-ttu-id="f7ad0-150">La `ngrok` sesión proporciona información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-150">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="f7ad0-151">La aplicación solo está disponible durante la sesión actual en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-151">The app is only available during the current session on your development machine.</span></span> <span data-ttu-id="f7ad0-152">Si la máquina se apaga o se queda en modo de suspensión, el servicio ya no está disponible.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-152">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="f7ad0-153">Recuerda esto cuando compartas la aplicación para realizar pruebas a otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-153">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="f7ad0-154">Si tienes que reiniciar el servicio, la aplicación devuelve una nueva dirección y debes actualizar cada ubicación que use esa dirección.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-154">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="f7ad0-155">La versión de pago de ngrok no tiene esta limitación.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-155">The paid version of ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="f7ad0-156">Host en Azure</span><span class="sxs-lookup"><span data-stu-id="f7ad0-156">Host in Azure</span></span>

<span data-ttu-id="f7ad0-157">Microsoft Azure hospeda la aplicación .NET en un nivel gratuito mediante la infraestructura compartida.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-157">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="f7ad0-158">Esto es suficiente para ejecutar el `Hello World` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-158">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="f7ad0-159">Para obtener más información, [vea crear una nueva cuenta gratuita.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="f7ad0-159">For more information, see [creating a new free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="f7ad0-160">Visual Studio compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="f7ad0-161">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="f7ad0-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="f7ad0-162">La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores que has tomado nota anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="f7ad0-163">Abra el archivo appsettings.jsarchivo.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="f7ad0-164">Actualice el *valor de MicrosoftAppId* con el identificador de bot que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="f7ad0-165">Actualice *MicrosoftAppPassword* con la contraseña del bot que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="f7ad0-166">Una vez realizados estos cambios, vuelve a generar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="f7ad0-167">Si usa ngrok, ejecute la aplicación localmente y, si va a hospedarla en Azure, vuelva a implementarla.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="f7ad0-168">Configurar la pestaña de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f7ad0-168">Configure the app tab</span></span>

<span data-ttu-id="f7ad0-169">Una vez que instales la aplicación en un equipo, deberás configurarla para mostrar contenido.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="f7ad0-170">Ve a un canal del equipo donde instalaste la aplicación de muestra y haz clic en el botón **"+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir en la lista Agregar **una** pestaña.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="f7ad0-171">A continuación, aparecerá un cuadro de diálogo de configuración.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="f7ad0-172">Este cuadro de diálogo te permitirá elegir qué pestaña mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="f7ad0-173">Una vez que seleccione la pestaña y haga clic en esta, podrá ver la `Save` pestaña cargada con la pestaña que `Hello World` eligió.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="f7ad0-174">Probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="f7ad0-174">Test your bot in Teams</span></span>

<span data-ttu-id="f7ad0-175">Ahora puede interactuar con el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="f7ad0-176">Elija un canal en el equipo donde registró la aplicación y escriba `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="f7ad0-176">Choose a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="f7ad0-177">Esto se denomina una **\@ mención.**</span><span class="sxs-lookup"><span data-stu-id="f7ad0-177">This is called an **\@mention**.</span></span> <span data-ttu-id="f7ad0-178">Cualquier mensaje que envíe al bot se le enviará como respuesta.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="f7ad0-179">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="f7ad0-179">Test your messaging extension</span></span>

<span data-ttu-id="f7ad0-180">Para probar la extensión de mensajería, puedes hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="f7ad0-181">Aparecerá un menú con la **aplicación "Hola** a todos".</span><span class="sxs-lookup"><span data-stu-id="f7ad0-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="f7ad0-182">Al hacer clic en él, verás un montón de textos aleatorios que se muestran.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="f7ad0-183">Puede elegir cualquiera de ellos y se inserta en la conversación.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-183">You can choose any one of them and it is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="f7ad0-184">Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f7ad0-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
