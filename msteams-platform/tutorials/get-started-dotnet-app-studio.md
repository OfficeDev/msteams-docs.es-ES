---
title: 'Tutorial: crear la primera aplicación con C #'
description: Obtén información sobre cómo empezar a crear Microsoft Teams aplicaciones con C# o .NET.
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 58e11312e61124bf09fcb55d2bcd0fc475e75a49
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114618"
---
# <a name="build-your-first-teams-app-using-c"></a><span data-ttu-id="48245-104">Crear la primera aplicación Teams con C #</span><span class="sxs-lookup"><span data-stu-id="48245-104">Build your first Teams app using C#</span></span>

<span data-ttu-id="48245-105">En este tutorial, aprenderás a crear tu primera aplicación Microsoft Teams con .NET o C#.</span><span class="sxs-lookup"><span data-stu-id="48245-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using .NET or C#.</span></span> <span data-ttu-id="48245-106">También le guiará a través de los pasos para:</span><span class="sxs-lookup"><span data-stu-id="48245-106">It also walks you through the steps to:</span></span>

1. [<span data-ttu-id="48245-107">Preparar el entorno</span><span class="sxs-lookup"><span data-stu-id="48245-107">Prepare your environment</span></span>](#prepare-your-environment)
1. [<span data-ttu-id="48245-108">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48245-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="48245-109">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="48245-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="48245-110">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="48245-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="48245-111">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="48245-111">Host the sample app</span></span>](#hostsample)
1. [<span data-ttu-id="48245-112">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="48245-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. [<span data-ttu-id="48245-113">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="48245-113">Configure the app tab</span></span>](#configureapptab)

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="48245-114">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48245-114">Get prerequisites</span></span>

<span data-ttu-id="48245-115">Para completar este tutorial, debe instalar las siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="48245-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="48245-116">Instalar Git</span><span class="sxs-lookup"><span data-stu-id="48245-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="48245-117">Instalar Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48245-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="48245-118">Puede instalar la edición de comunidad gratuita de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48245-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="48245-119">Durante la instalación, si hay una opción para agregar `git` a la ruta de acceso, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="48245-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="48245-120">En una ventana de terminal, ejecute el siguiente comando para comprobar la `git` instalación:</span><span class="sxs-lookup"><span data-stu-id="48245-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="48245-121">Usa una ventana de terminal adecuada en tu plataforma.</span><span class="sxs-lookup"><span data-stu-id="48245-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="48245-122">Estos ejemplos usan Git Bash, pero se pueden ejecutar en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="48245-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="48245-123">Abra la versión más reciente de Visual Studio e instale las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="48245-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="48245-124">Puede usar la misma ventana de terminal para ejecutar los comandos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="48245-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="48245-125">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="48245-125">Download the sample</span></span>

<span data-ttu-id="48245-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="48245-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="48245-127">muestra en C#.</span><span class="sxs-lookup"><span data-stu-id="48245-127">sample in C#.</span></span> <span data-ttu-id="48245-128">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo:</span><span class="sxs-lookup"><span data-stu-id="48245-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="48245-129">Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio para](https://github.com/OfficeDev/Microsoft-Teams-Samples) modificar y guardar los cambios en GitHub.</span><span class="sxs-lookup"><span data-stu-id="48245-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="48245-130">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="48245-130">Build and run the sample</span></span>

<span data-ttu-id="48245-131">Puede crear y ejecutar la asignación después de clonarse.</span><span class="sxs-lookup"><span data-stu-id="48245-131">You can build and run the smaple after it is cloned.</span></span> 

<span data-ttu-id="48245-132">**Para compilar y ejecutar el ejemplo clonado**</span><span class="sxs-lookup"><span data-stu-id="48245-132">**To build and run the cloned sample**</span></span>

1. <span data-ttu-id="48245-133">Abra el archivo de solución **Microsoft.Teams. Samples.HelloWorld.sln** del **directorio Microsoft-Teams-Samples/samples/app-hello-world/csharp** del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="48245-133">Open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span>
1. <span data-ttu-id="48245-134">Seleccione **Generar solución** en el **menú** Generar.</span><span class="sxs-lookup"><span data-stu-id="48245-134">Select **Build Solution** from the **Build** menu.</span></span>
1. <span data-ttu-id="48245-135">Seleccione la **tecla F5** o seleccione **Iniciar depuración** en el **menú Depurar** para ejecutar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="48245-135">Select the **F5** key, or select **Start Debugging** from the **Debug** menu to run the sample.</span></span>

<span data-ttu-id="48245-136">Cuando se inicia la aplicación, se abre una ventana del explorador con la raíz de la aplicación iniciada.</span><span class="sxs-lookup"><span data-stu-id="48245-136">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="48245-137">Puedes ir a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="48245-137">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

> [!Note]
> <span data-ttu-id="48245-138">Si recibe un `Could not find a part of the path … bin\roslyn\csc.exe` error, actualice el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="48245-138">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="48245-139">Para obtener más información, vea [esta pregunta en Stack Overflow](https://stackoverflow.com/questions/32780315).</span><span class="sxs-lookup"><span data-stu-id="48245-139">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

<a name="hostsample"></a>
## <a name="deploy-your-sample-app"></a><span data-ttu-id="48245-140">Implementar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="48245-140">Deploy your sample app</span></span>

<span data-ttu-id="48245-141">Las aplicaciones de Microsoft Teams son aplicaciones web que proporcionan una o más funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="48245-141">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="48245-142">Para que Teams plataforma para cargar la aplicación, la aplicación debe estar disponible en Internet.</span><span class="sxs-lookup"><span data-stu-id="48245-142">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="48245-143">Para ello, debes hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48245-143">To do this, you need to host your app.</span></span> <span data-ttu-id="48245-144">Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel para el proceso local en el equipo mediante `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="48245-144">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="48245-145">Después de hospedar la aplicación, anote su dirección URL raíz, como `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="48245-145">After you host your app, make a note of its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="48245-146">Tunnel con ngrok</span><span class="sxs-lookup"><span data-stu-id="48245-146">Tunnel using ngrok</span></span>

<span data-ttu-id="48245-147">Para realizar pruebas rápidas, puedes ejecutar la aplicación en el equipo y crear un túnel para ella a través de un punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="48245-147">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="48245-148">[`ngrok`](https://ngrok.com) es una herramienta gratuita con la que puede obtener una dirección web, como `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="48245-148">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="48245-149">Puede descargar [e instalar](https://ngrok.com/download) ngrok y agregarlo a una ubicación en su `PATH` .</span><span class="sxs-lookup"><span data-stu-id="48245-149">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="48245-150">Después de instalar `ngrok` , abra una nueva ventana de terminal y ejecute el siguiente comando para crear un túnel:</span><span class="sxs-lookup"><span data-stu-id="48245-150">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="48245-151">`Ngrok` responde a las solicitudes de Internet y las enruta a la aplicación que se ejecuta en el puerto 44327.</span><span class="sxs-lookup"><span data-stu-id="48245-151">`Ngrok` responds to requests from the internet and routes them to your app running on port 44327.</span></span> 

<span data-ttu-id="48245-152">**Para comprobar la respuesta**</span><span class="sxs-lookup"><span data-stu-id="48245-152">**To verify the response**</span></span>

1. <span data-ttu-id="48245-153">Abra el explorador y vaya a `https://d0ac14a5.ngrok.io/hello` .</span><span class="sxs-lookup"><span data-stu-id="48245-153">Open your browser and go to `https://d0ac14a5.ngrok.io/hello`.</span></span> <span data-ttu-id="48245-154">Esto cargará la página Hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48245-154">This will load your app's Hello page.</span></span>
1. <span data-ttu-id="48245-155">En lugar de la dirección URL mencionada en el paso 1, usa la dirección de reenvío que se muestra en `ngrok` la sesión de la consola.</span><span class="sxs-lookup"><span data-stu-id="48245-155">Instead of the URL mentioned in Step 1, use the forwarding address displayed by `ngrok` in your console session.</span></span>
    > [!NOTE]
    > <span data-ttu-id="48245-156">Si ha usado un puerto diferente en el paso [de](#build-and-run-the-sample) compilación y ejecución, asegúrese de usar el mismo número de puerto para configurar el `ngrok` túnel.</span><span class="sxs-lookup"><span data-stu-id="48245-156">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>
    > [!TIP]
    > <span data-ttu-id="48245-157">Es una buena idea ejecutarse `ngrok` en una ventana de terminal diferente.</span><span class="sxs-lookup"><span data-stu-id="48245-157">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="48245-158">Esto se hace para evitar `ngrok` que se ejecute sin interferir con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48245-158">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="48245-159">Debes detener, recompilar y volver a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48245-159">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="48245-160">La `ngrok` sesión proporciona información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="48245-160">The `ngrok` session provides useful debugging information in this window.</span></span>

    <span data-ttu-id="48245-161">La aplicación solo está disponible durante la sesión actual en el equipo.</span><span class="sxs-lookup"><span data-stu-id="48245-161">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="48245-162">Si la máquina está apagada o está en modo de suspensión, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="48245-162">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="48245-163">Recuerda esto cuando compartas la aplicación para realizar pruebas a otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="48245-163">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="48245-164">Si tienes que reiniciar el servicio, la aplicación devuelve una nueva dirección y debes actualizar cada ubicación que use esa dirección.</span><span class="sxs-lookup"><span data-stu-id="48245-164">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="48245-165">La versión de pago `ngrok` de no tiene esta limitación.</span><span class="sxs-lookup"><span data-stu-id="48245-165">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="48245-166">Host en Azure</span><span class="sxs-lookup"><span data-stu-id="48245-166">Host in Azure</span></span>

<span data-ttu-id="48245-167">Microsoft Azure hospeda la aplicación .NET en un nivel gratuito mediante infraestructura compartida.</span><span class="sxs-lookup"><span data-stu-id="48245-167">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="48245-168">Esto es suficiente para ejecutar el `Hello World` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="48245-168">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="48245-169">Para obtener más información, vea [creating a new free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="48245-169">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="48245-170">Visual Studio compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure:</span><span class="sxs-lookup"><span data-stu-id="48245-170">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

<span data-ttu-id="48245-171">**Actualizar el paquete de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="48245-171">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="48245-172">App Studio</span><span class="sxs-lookup"><span data-stu-id="48245-172">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="48245-173">Portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="48245-173">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="48245-174">**Para instalar Developer Portal (versión preliminar) en Teams**</span><span class="sxs-lookup"><span data-stu-id="48245-174">**To install Developer Portal (preview) in Teams**</span></span>


1. <span data-ttu-id="48245-175">Selecciona el **icono Aplicaciones** en la parte inferior de la barra izquierda y busca Portal **para desarrolladores.**</span><span class="sxs-lookup"><span data-stu-id="48245-175">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="48245-176">Seleccione **Portal para desarrolladores** y **seleccione Abrir**.</span><span class="sxs-lookup"><span data-stu-id="48245-176">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="48245-177">Selecciona la pestaña Aplicaciones y selecciona **Importar una aplicación existente.**</span><span class="sxs-lookup"><span data-stu-id="48245-177">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="48245-178">Seleccione **Hello World** y seleccione **Importar**.</span><span class="sxs-lookup"><span data-stu-id="48245-178">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="48245-179">La **aplicación Hello World** se importa en el Portal de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="48245-179">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="48245-180">Puedes configurar la aplicación mediante el portal Teams Developer Portal.</span><span class="sxs-lookup"><span data-stu-id="48245-180">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="48245-181">El manifiesto se encuentra en Distribuir.</span><span class="sxs-lookup"><span data-stu-id="48245-181">The Manifest is found under Distribute.</span></span> <span data-ttu-id="48245-182">Puedes usar el manifiesto para configurar las capacidades, los recursos necesarios y otros atributos importantes para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48245-182">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="48245-183">Para obtener más información sobre cómo configurar la aplicación mediante el Portal de desarrolladores, [consulta Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48245-183">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="48245-184">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="48245-184">Update the credentials for your hosted app</span></span>

<span data-ttu-id="48245-185">La aplicación de ejemplo requiere que las variables de entorno se establezcan en los valores guardados en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="48245-185">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="48245-186">**Para actualizar las credenciales de la aplicación hospedada**</span><span class="sxs-lookup"><span data-stu-id="48245-186">**To update the credentials for your hosted app**</span></span>

1. <span data-ttu-id="48245-187">Abra el archivo `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="48245-187">Open the `appsettings.json` file.</span></span> 
1. <span data-ttu-id="48245-188">Actualice el **valor de MicrosoftAppId** con el identificador de bot que guardó en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="48245-188">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> 
1. <span data-ttu-id="48245-189">Actualice **MicrosoftAppPassword** con la contraseña del bot que guardó.</span><span class="sxs-lookup"><span data-stu-id="48245-189">Update the **MicrosoftAppPassword** with the bot password that you saved.</span></span>

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    <span data-ttu-id="48245-190">Después de realizar estos cambios, recompile la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48245-190">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="48245-191">Si usa ngrok, ejecute la aplicación localmente y, si está hospedando en Azure, vuelva a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48245-191">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a><span data-ttu-id="48245-192">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="48245-192">Configure the app tab</span></span>

<span data-ttu-id="48245-193">Después de instalar la aplicación en teams, debes configurarla para mostrar el contenido.</span><span class="sxs-lookup"><span data-stu-id="48245-193">After you have installed the app into teams, you must configure it to display the content.</span></span> 

<span data-ttu-id="48245-194">**Para configurar la pestaña de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="48245-194">**To configure the app tab**</span></span>

1. <span data-ttu-id="48245-195">Ve a un canal del equipo en el que instalaste la aplicación de ejemplo y selecciona el botón **"+"** para agregar una nueva pestaña.</span><span class="sxs-lookup"><span data-stu-id="48245-195">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab.</span></span>
1. <span data-ttu-id="48245-196">Seleccione **Hello World** en la lista Agregar **una** pestaña.</span><span class="sxs-lookup"><span data-stu-id="48245-196">Select **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="48245-197">Se muestra un cuadro de diálogo de configuración que permite seleccionar la pestaña que se va a mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="48245-197">A configuration dialog box is displayed that enables you to select the tab to display in this channel.</span></span> 
1. <span data-ttu-id="48245-198">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="48245-198">Select **Save**.</span></span> <span data-ttu-id="48245-199">La `Hello World` pestaña se carga con la pestaña.</span><span class="sxs-lookup"><span data-stu-id="48245-199">The `Hello World` tab is loaded with the tab.</span></span>

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="48245-200">Pruebe el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="48245-200">Test your bot in Teams</span></span>

<span data-ttu-id="48245-201">Ahora puede probar el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="48245-201">You can now test the bot in Teams.</span></span> 

<span data-ttu-id="48245-202">**Para probar el bot**</span><span class="sxs-lookup"><span data-stu-id="48245-202">**To test your bot**</span></span>

* <span data-ttu-id="48245-203">Selecciona un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="48245-203">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="48245-204">Esto se denomina una **\@ mención**.</span><span class="sxs-lookup"><span data-stu-id="48245-204">This is called an **\@mention**.</span></span> <span data-ttu-id="48245-205">El bot responde a cualquier mensaje que envíe.</span><span class="sxs-lookup"><span data-stu-id="48245-205">The bot replies to any message that you send.</span></span>

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="48245-206">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="48245-206">Test your messaging extension</span></span>

<span data-ttu-id="48245-207">Para probar la extensión de mensajería, seleccione **...** debajo del cuadro de entrada de la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="48245-207">To test your messaging extension, select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="48245-208">Se muestra un menú con la aplicación **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="48245-208">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="48245-209">Al seleccionarlo, se muestra un conjunto de textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="48245-209">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="48245-210">Puede seleccionar uno de los textos aleatorios que se insertan en la conversación.</span><span class="sxs-lookup"><span data-stu-id="48245-210">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

<span data-ttu-id="48245-211">Seleccione uno de los textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="48245-211">Select one of the random text.</span></span> <span data-ttu-id="48245-212">Se muestra una tarjeta con formato y lista para enviar con su propio mensaje.</span><span class="sxs-lookup"><span data-stu-id="48245-212">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a><span data-ttu-id="48245-213">Vea también</span><span class="sxs-lookup"><span data-stu-id="48245-213">See also</span></span>

* [<span data-ttu-id="48245-214">Introducción a tutoriales</span><span class="sxs-lookup"><span data-stu-id="48245-214">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="48245-215">Muestras de código</span><span class="sxs-lookup"><span data-stu-id="48245-215">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)