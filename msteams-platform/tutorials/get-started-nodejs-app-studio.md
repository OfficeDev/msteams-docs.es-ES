---
title: 'Tutorial: crea la primera aplicación con Node.js'
description: Obtén información sobre cómo empezar a crear Microsoft Teams aplicaciones con Node.js.
keywords: introducción a node.js nodejs App Studio
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: bbb2e50592eaa8a69a2cd9abda6a17ba2aa0e6bc
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114520"
---
# <a name="build-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="48367-104">Crea tu primera Microsoft Teams con Node.js</span><span class="sxs-lookup"><span data-stu-id="48367-104">Build your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="48367-105">En este tutorial, aprenderás a crear la primera aplicación Microsoft Teams con Node.js.</span><span class="sxs-lookup"><span data-stu-id="48367-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using Node.js.</span></span> <span data-ttu-id="48367-106">También le guiará a través de los pasos para:</span><span class="sxs-lookup"><span data-stu-id="48367-106">It also walks you through the steps to:</span></span> 

1. [<span data-ttu-id="48367-107">Preparar el entorno</span><span class="sxs-lookup"><span data-stu-id="48367-107">Prepare your environment</span></span>](#prepare-environment)
1. [<span data-ttu-id="48367-108">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48367-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="48367-109">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="48367-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="48367-110">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="48367-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="48367-111">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="48367-111">Host the sample app</span></span>](#HostSample)
1. [<span data-ttu-id="48367-112">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="48367-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. [<span data-ttu-id="48367-113">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="48367-113">Configure the app tab</span></span>](#ConfigureTheAppTab)

<a name="prepare-environment"></a>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

### <a name="download-and-host-your-app"></a><span data-ttu-id="48367-114">Descargar y hospedar la aplicación</span><span class="sxs-lookup"><span data-stu-id="48367-114">Download and host your app</span></span>

<span data-ttu-id="48367-115">Siga estos pasos para descargar y hospedar una aplicación sencilla de "hello world" en Teams.</span><span class="sxs-lookup"><span data-stu-id="48367-115">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="48367-116">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48367-116">Get prerequisites</span></span>

<span data-ttu-id="48367-117">Para completar este tutorial, necesita las siguientes herramientas.</span><span class="sxs-lookup"><span data-stu-id="48367-117">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="48367-118">Si aún no las tiene, puede instalarlas desde estos vínculos.</span><span class="sxs-lookup"><span data-stu-id="48367-118">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="48367-119">Git</span><span class="sxs-lookup"><span data-stu-id="48367-119">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="48367-120">Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="48367-120">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="48367-121">Obtener cualquier editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="48367-121">Get any text editor or IDE.</span></span> <span data-ttu-id="48367-122">Puede instalar y [usar](https://code.visualstudio.com/download) Visual Studio Code de forma gratuita.</span><span class="sxs-lookup"><span data-stu-id="48367-122">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="48367-123">Si ve opciones para agregar , , y a PATH durante la `git` `node` `npm` `code` instalación, seleccione las opciones.</span><span class="sxs-lookup"><span data-stu-id="48367-123">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, select the options.</span></span> 

<span data-ttu-id="48367-124">Compruebe que las herramientas están disponibles ejecutando lo siguiente en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="48367-124">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="48367-125">Usa la ventana de terminal con la que te sientas más cómodo en tu plataforma.</span><span class="sxs-lookup"><span data-stu-id="48367-125">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="48367-126">Estos ejemplos usan Bash (que se incluye en Git), pero estos scripts se ejecutarán en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="48367-126">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

<span data-ttu-id="48367-127">Es posible que tenga una versión diferente de estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="48367-127">You may have a different version of these applications.</span></span> <span data-ttu-id="48367-128">Esto no debe ser un problema, excepto gulp.</span><span class="sxs-lookup"><span data-stu-id="48367-128">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="48367-129">Para gulp tendrás que usar la versión 4.0.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="48367-129">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="48367-130">Si no tiene gulp instalado (o tiene instalada la versión incorrecta), ahora ejecutándose `npm install gulp` en la ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="48367-130">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="48367-131">Si ha instalado Visual Studio Code, puede comprobar la instalación ejecutando:</span><span class="sxs-lookup"><span data-stu-id="48367-131">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="48367-132">Puede seguir usando esta ventana de terminal para ejecutar los comandos que se siguen en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="48367-132">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="48367-133">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="48367-133">Download the sample</span></span>

<span data-ttu-id="48367-134">Hemos proporcionado un hello [simple, world!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span><span class="sxs-lookup"><span data-stu-id="48367-134">We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span></span> <span data-ttu-id="48367-135">muestra para empezar.</span><span class="sxs-lookup"><span data-stu-id="48367-135">sample to get you started.</span></span> <span data-ttu-id="48367-136">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="48367-136">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="48367-137">Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio](https://github.com/OfficeDev/Microsoft-Teams-Samples) si desea modificar y comprobar los cambios realizados en el repositorio de GitHub para su referencia futura.</span><span class="sxs-lookup"><span data-stu-id="48367-137">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="48367-138">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="48367-138">Build and run the sample</span></span>

<span data-ttu-id="48367-139">Después de clonar el repositorio, ejecute el comando cambiar directorio en el terminal para cambiar el directorio al ejemplo:</span><span class="sxs-lookup"><span data-stu-id="48367-139">After the repository is cloned, run the change directory command in terminal to change the directory to the sample:</span></span>

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

<span data-ttu-id="48367-140">Para crear el ejemplo, debe instalar todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="48367-140">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="48367-141">Ejecute el siguiente comando para hacerlo:</span><span class="sxs-lookup"><span data-stu-id="48367-141">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="48367-142">Debería ver un montón de dependencias que se instalan.</span><span class="sxs-lookup"><span data-stu-id="48367-142">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="48367-143">Después de la instalación, puedes ejecutar la aplicación con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="48367-143">After installation you can run the app with the following command:</span></span>

```bash
npm start
```

<span data-ttu-id="48367-144">Cuando se inicia la aplicación hello-world, se muestra `App started listening on port 3333` en la ventana del terminal.</span><span class="sxs-lookup"><span data-stu-id="48367-144">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="48367-145">Si ve un número de puerto diferente que se muestra en el mensaje anterior, es porque tiene un conjunto de variables de entorno PORT.</span><span class="sxs-lookup"><span data-stu-id="48367-145">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="48367-146">Puede seguir usando ese puerto o cambiar la variable de entorno a 3333.</span><span class="sxs-lookup"><span data-stu-id="48367-146">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="48367-147">En este punto, puede abrir una ventana del explorador y navegar a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="48367-147">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

## <a name="deploy-your-sample-app"></a><span data-ttu-id="48367-148">Implementar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="48367-148">Deploy your sample app</span></span>

<span data-ttu-id="48367-149">Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="48367-149">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="48367-150">Para que Teams plataforma para cargar la aplicación, la aplicación debe ser accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="48367-150">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="48367-151">Para que la aplicación sea accesible desde Internet, debes *hospedar* la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-151">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="48367-152">Para las pruebas locales, puedes ejecutar la aplicación en el equipo local y crear un túnel para ella con un punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="48367-152">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="48367-153">[ngrok](https://ngrok.com) es una herramienta gratuita que te permite hacerlo.</span><span class="sxs-lookup"><span data-stu-id="48367-153">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="48367-154">Con *ngrok* puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo).</span><span class="sxs-lookup"><span data-stu-id="48367-154">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="48367-155">Puede descargar [e instalar](https://ngrok.com/download) *ngrok* para su entorno.</span><span class="sxs-lookup"><span data-stu-id="48367-155">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="48367-156">Asegúrese de agregarlo a una ubicación en el `PATH` archivo .</span><span class="sxs-lookup"><span data-stu-id="48367-156">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="48367-157">Después de instalarlo, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel.</span><span class="sxs-lookup"><span data-stu-id="48367-157">After you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="48367-158">El ejemplo usa el puerto 3333, así que asegúrese de especificarlo aquí:</span><span class="sxs-lookup"><span data-stu-id="48367-158">The sample uses port 3333, so be sure to specify it here:</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="48367-159">*Ngrok* escuchará las solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333.</span><span class="sxs-lookup"><span data-stu-id="48367-159">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="48367-160">Para comprobarlo, abra el explorador y vaya `https://d0ac14a5.ngrok.io/hello` a cargar la página de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-160">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="48367-161">Asegúrese de usar la dirección de reenvío mostrada por *ngrok* en la sesión de la consola en lugar de esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="48367-161">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="48367-162">Si ha usado un puerto [](#build-and-run-the-sample) diferente en la compilación y ejecuta el paso anterior, asegúrese de usar el mismo número de puerto para configurar el túnel *ngrok.*</span><span class="sxs-lookup"><span data-stu-id="48367-162">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="48367-163">Es una buena idea ejecutar *ngrok* en una ventana de terminal diferente para mantenerla en funcionamiento sin interferir con la aplicación de nodo que más adelante podría tener que detener, volver a compilar y volver a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="48367-163">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="48367-164">La *sesión ngrok* devolverá información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="48367-164">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="48367-165">Hay una versión de pago de *ngrok* que permite nombres persistentes.</span><span class="sxs-lookup"><span data-stu-id="48367-165">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="48367-166">Si usas la versión gratuita, la aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="48367-166">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="48367-167">Si la máquina se apaga o se queda en modo de suspensión, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="48367-167">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="48367-168">Recuerda esto al compartir la aplicación para pruebas por otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="48367-168">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="48367-169">Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar cada lugar que use esa dirección.</span><span class="sxs-lookup"><span data-stu-id="48367-169">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="48367-170">Anote la dirección URL de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-170">Make a note of the URL of your app.</span></span> <span data-ttu-id="48367-171">Necesitarás esto más adelante cuando registres la aplicación con Teams con App studio o Portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="48367-171">You will need this later when you register the app with Teams using App studio or Developer Portal.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="48367-172">Implementar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="48367-172">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="48367-173">En este momento tienes una aplicación hospedada en Internet, pero aún no tienes forma de decir Teams dónde buscarla, ni siquiera cómo se llama a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-173">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="48367-174">Para ello, ahora tienes que crear un paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-174">To do this you now have to create an app package.</span></span> <span data-ttu-id="48367-175">Esto es poco más que un archivo de texto que contiene el manifiesto de la aplicación y algunos iconos que el cliente de Teams usará para mostrar y marcar correctamente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-175">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="48367-176">Puedes crear manualmente este paquete de aplicación, o puedes usar App Studio o Developer Portal, herramientas que se ejecutan en Teams, que simplificarán el proceso de registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-176">You can manually create this app package, or you can use App Studio or Developer Portal, tools that run in Teams, that will simplify the process of registering the app.</span></span> <span data-ttu-id="48367-177">App Studio y Developer Portal son las formas recomendadas de crear y actualizar el paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-177">App Studio and Developer Portal are the recommended ways of creating and updating the app package.</span></span>

<span data-ttu-id="48367-178">Para cualquiera de los dos métodos, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="48367-178">For either method you will need the following:</span></span>

- <span data-ttu-id="48367-179">La dirección URL en la que se puede encontrar la aplicación en Internet.</span><span class="sxs-lookup"><span data-stu-id="48367-179">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="48367-180">Iconos que Teams usarán para crear una marca de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-180">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="48367-181">El ejemplo incluye iconos de marcador de posición ubicados en "src\static\images.</span><span class="sxs-lookup"><span data-stu-id="48367-181">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="48367-182">App Studio también proporcionará iconos predeterminados si es necesario.</span><span class="sxs-lookup"><span data-stu-id="48367-182">App Studio also will provide default icons if needed.</span></span>

<span data-ttu-id="48367-183">**Actualizar el paquete de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="48367-183">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="48367-184">App Studio</span><span class="sxs-lookup"><span data-stu-id="48367-184">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="48367-185">Portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="48367-185">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="48367-186">**Para instalar Developer Portal (versión preliminar) en Teams**</span><span class="sxs-lookup"><span data-stu-id="48367-186">**To install Developer Portal (preview) in Teams**</span></span>

1. <span data-ttu-id="48367-187">Selecciona el **icono Aplicaciones** en la parte inferior de la barra izquierda y busca Portal **para desarrolladores.**</span><span class="sxs-lookup"><span data-stu-id="48367-187">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="48367-188">Seleccione **Portal para desarrolladores** y **seleccione Abrir**.</span><span class="sxs-lookup"><span data-stu-id="48367-188">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="48367-189">Selecciona la pestaña Aplicaciones y selecciona **Importar una aplicación existente.**</span><span class="sxs-lookup"><span data-stu-id="48367-189">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="48367-190">Seleccione **Hello World** y seleccione **Importar**.</span><span class="sxs-lookup"><span data-stu-id="48367-190">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="48367-191">La **aplicación Hello World** se importa en el Portal de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="48367-191">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="48367-192">Puedes configurar la aplicación mediante el portal Teams Developer Portal.</span><span class="sxs-lookup"><span data-stu-id="48367-192">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="48367-193">El manifiesto se encuentra en Distribuir.</span><span class="sxs-lookup"><span data-stu-id="48367-193">The Manifest is found under Distribute.</span></span> <span data-ttu-id="48367-194">Puedes usar el manifiesto para configurar las capacidades, los recursos necesarios y otros atributos importantes para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-194">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="48367-195">Para obtener más información sobre cómo configurar la aplicación mediante el Portal de desarrolladores, [consulta Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48367-195">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>

---
<a name="updatecredentials"></a>

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="48367-196">Actualizar las credenciales de la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="48367-196">Update the credentials for your hosted app</span></span>

<span data-ttu-id="48367-197">La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores de los que has tomado nota anteriormente:</span><span class="sxs-lookup"><span data-stu-id="48367-197">The sample app requires the following environment variables to be set to the values you made a note of earlier:</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="48367-198">La forma en que lo haces varía en función de cómo hospedaste la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48367-198">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="48367-199">Lo importante sobre el uso de variables de entorno es que estos valores forman parte del entorno: el código de la aplicación puede acceder a ellos, pero no se exponen a terceros que podrían examinar los archivos que forman el sitio.</span><span class="sxs-lookup"><span data-stu-id="48367-199">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="48367-200">Si ejecutas la aplicación con ngrok, tendrás que configurar algunas variables de entorno local.</span><span class="sxs-lookup"><span data-stu-id="48367-200">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="48367-201">Hay muchas maneras de hacerlo, pero lo más fácil, si usa Visual Studio Code, es agregar una configuración [de inicio:](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)</span><span class="sxs-lookup"><span data-stu-id="48367-201">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

<span data-ttu-id="48367-202">Donde:</span><span class="sxs-lookup"><span data-stu-id="48367-202">Where:</span></span>

<span data-ttu-id="48367-203">MICROSOFT_APP_ID y MICROSOFT_APP_PASSWORD es el identificador y la contraseña, respectivamente, para el bot.</span><span class="sxs-lookup"><span data-stu-id="48367-203">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="48367-204">NODE_DEBUG le mostrará lo que está sucediendo en el bot en la Visual Studio Code de depuración.</span><span class="sxs-lookup"><span data-stu-id="48367-204">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="48367-205">NODE_CONFIG_DIR apunta al directorio en la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta localmente, lo busca en la carpeta src).</span><span class="sxs-lookup"><span data-stu-id="48367-205">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="48367-206">Si no has detenido npm desde antes en el tutorial, tendrás que ejecutar para que Visual Studio Code las variables de configuración de `npm stop` inicio correctamente.</span><span class="sxs-lookup"><span data-stu-id="48367-206">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="48367-207">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="48367-207">Configure the app tab</span></span>

<span data-ttu-id="48367-208">Después de instalar la aplicación en un equipo, deberás configurarla para mostrar contenido.</span><span class="sxs-lookup"><span data-stu-id="48367-208">After you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="48367-209">Vaya a un canal del equipo y haga clic en el **botón "+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir entre la lista Agregar **una** pestaña.</span><span class="sxs-lookup"><span data-stu-id="48367-209">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="48367-210">A continuación, se le mostrará un cuadro de diálogo de configuración.</span><span class="sxs-lookup"><span data-stu-id="48367-210">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="48367-211">Este cuadro de diálogo le permitirá elegir qué pestaña mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="48367-211">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="48367-212">Después de seleccionar la pestaña y hacer clic en **Guardar,** puede ver la `Hello World` pestaña cargada con la pestaña que eligió:</span><span class="sxs-lookup"><span data-stu-id="48367-212">After you select the tab and click **Save** you can see the `Hello World` tab loaded with the tab you chose:</span></span>

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="48367-213">Pruebe el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="48367-213">Test your bot in Teams</span></span>

<span data-ttu-id="48367-214">Ahora puede interactuar con el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="48367-214">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="48367-215">Elige un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` , seguido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="48367-215">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="48367-216">Esto se denomina una **\@ mención**.</span><span class="sxs-lookup"><span data-stu-id="48367-216">This is called an **\@mention**.</span></span> <span data-ttu-id="48367-217">Cualquier mensaje que envíes al bot se te enviará como respuesta:</span><span class="sxs-lookup"><span data-stu-id="48367-217">Whatever message you send to the bot will be sent back to you as a reply:</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="48367-218">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="48367-218">Test your messaging extension</span></span>

<span data-ttu-id="48367-219">Para probar la extensión de mensajería, puedes hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="48367-219">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="48367-220">Aparecerá un menú con la **aplicación "Hello World".**</span><span class="sxs-lookup"><span data-stu-id="48367-220">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="48367-221">Al hacer clic en él, verá una serie de textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="48367-221">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="48367-222">Puede elegir cualquiera de ellos y se insertará en la conversación:</span><span class="sxs-lookup"><span data-stu-id="48367-222">You can choose any one of them and it will be inserted it into your conversation:</span></span>

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

<span data-ttu-id="48367-223">Seleccione uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior:</span><span class="sxs-lookup"><span data-stu-id="48367-223">Select one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom:</span></span>

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

 ## <a name="see-also"></a><span data-ttu-id="48367-224">Vea también</span><span class="sxs-lookup"><span data-stu-id="48367-224">See also</span></span>

* [<span data-ttu-id="48367-225">Introducción a tutoriales</span><span class="sxs-lookup"><span data-stu-id="48367-225">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="48367-226">Muestras de código</span><span class="sxs-lookup"><span data-stu-id="48367-226">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)