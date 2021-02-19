---
title: 'Tutorial: crea la primera aplicación con Node.js'
description: Obtén información sobre cómo empezar a crear aplicaciones de Microsoft Teams con Node.js.
keywords: introducción a node.js nodejs App Studio
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 61be1056a07952c6cf166dbe183fa257ceaf7227
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294764"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="f7320-104">Crear la primera aplicación de Microsoft Teams con Node.js</span><span class="sxs-lookup"><span data-stu-id="f7320-104">Create your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="f7320-105">Este tutorial te ayuda a empezar a crear una aplicación de Microsoft Teams con Node.js.</span><span class="sxs-lookup"><span data-stu-id="f7320-105">This tutorial helps you get started creating a Microsoft Teams app using Node.js.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="f7320-106">Descargar y hospedar la aplicación</span><span class="sxs-lookup"><span data-stu-id="f7320-106">Download and host your app</span></span>

<span data-ttu-id="f7320-107">Sigue estos pasos para descargar y hospedar una aplicación sencilla de "hello world" en Teams.</span><span class="sxs-lookup"><span data-stu-id="f7320-107">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="f7320-108">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f7320-108">Get prerequisites</span></span>

<span data-ttu-id="f7320-109">Para completar este tutorial, necesita las siguientes herramientas.</span><span class="sxs-lookup"><span data-stu-id="f7320-109">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="f7320-110">Si aún no las tiene, puede instalarlas desde estos vínculos.</span><span class="sxs-lookup"><span data-stu-id="f7320-110">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="f7320-111">Git</span><span class="sxs-lookup"><span data-stu-id="f7320-111">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="f7320-112">Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="f7320-112">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="f7320-113">Obtener cualquier editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="f7320-113">Get any text editor or IDE.</span></span> <span data-ttu-id="f7320-114">Puede instalar y usar Visual Studio [code](https://code.visualstudio.com/download) de forma gratuita.</span><span class="sxs-lookup"><span data-stu-id="f7320-114">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="f7320-115">Si ve opciones para agregar , , y a PATH durante la `git` `node` `npm` `code` instalación, elija hacerlo.</span><span class="sxs-lookup"><span data-stu-id="f7320-115">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="f7320-116">Será útil.</span><span class="sxs-lookup"><span data-stu-id="f7320-116">It will be handy.</span></span>

<span data-ttu-id="f7320-117">Compruebe que las herramientas están disponibles ejecutando lo siguiente en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="f7320-117">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="f7320-118">Usa la ventana de terminal con la que te sientas más cómodo en tu plataforma.</span><span class="sxs-lookup"><span data-stu-id="f7320-118">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="f7320-119">Estos ejemplos usan Bash (que se incluye en Git), pero estos scripts se ejecutarán en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="f7320-119">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

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

<span data-ttu-id="f7320-120">Es posible que tenga una versión diferente de estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f7320-120">You may have a different version of these applications.</span></span> <span data-ttu-id="f7320-121">Esto no debe ser un problema, excepto gulp.</span><span class="sxs-lookup"><span data-stu-id="f7320-121">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="f7320-122">Para gulp tendrás que usar la versión 4.0.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f7320-122">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="f7320-123">Si no tiene gulp instalado (o tiene instalada la versión incorrecta), ahora ejecutándose `npm install gulp` en la ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="f7320-123">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="f7320-124">Si ha instalado Visual Studio code, puede comprobar la instalación ejecutando:</span><span class="sxs-lookup"><span data-stu-id="f7320-124">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="f7320-125">Puede seguir usando esta ventana de terminal para ejecutar los comandos que se siguen en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f7320-125">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="f7320-126">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7320-126">Download the sample</span></span>

<span data-ttu-id="f7320-127">Hemos proporcionado un hello [simple, world!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span><span class="sxs-lookup"><span data-stu-id="f7320-127">We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span></span> <span data-ttu-id="f7320-128">muestra para empezar.</span><span class="sxs-lookup"><span data-stu-id="f7320-128">sample to get you started.</span></span> <span data-ttu-id="f7320-129">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="f7320-129">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="f7320-130">Puedes [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio](https://github.com/OfficeDev/Microsoft-Teams-Samples) si quieres modificar y comprobar los cambios realizados en el repositorio de GitHub para obtener una referencia futura.</span><span class="sxs-lookup"><span data-stu-id="f7320-130">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="f7320-131">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7320-131">Build and run the sample</span></span>

<span data-ttu-id="f7320-132">Una vez clonado el repositorio, cambie al directorio que contiene el ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f7320-132">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

<span data-ttu-id="f7320-133">Para crear el ejemplo, debe instalar todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f7320-133">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="f7320-134">Ejecute el siguiente comando para hacerlo:</span><span class="sxs-lookup"><span data-stu-id="f7320-134">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="f7320-135">Debería ver un montón de dependencias que se instalan.</span><span class="sxs-lookup"><span data-stu-id="f7320-135">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="f7320-136">Una vez que terminen, puedes ejecutar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f7320-136">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="f7320-137">Cuando se inicia la aplicación hello-world, se muestra `App started listening on port 3333` en la ventana del terminal.</span><span class="sxs-lookup"><span data-stu-id="f7320-137">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="f7320-138">Si ve un número de puerto diferente que se muestra en el mensaje anterior, es porque tiene un conjunto de variables de entorno PORT.</span><span class="sxs-lookup"><span data-stu-id="f7320-138">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="f7320-139">Puede seguir usando ese puerto o cambiar la variable de entorno a 3333.</span><span class="sxs-lookup"><span data-stu-id="f7320-139">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="f7320-140">En este punto, puede abrir una ventana del explorador y navegar a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se están cargando:</span><span class="sxs-lookup"><span data-stu-id="f7320-140">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="f7320-141">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7320-141">Host the sample app</span></span>

<span data-ttu-id="f7320-142">Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="f7320-142">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="f7320-143">Para que la plataforma teams cargue la aplicación, la aplicación debe ser accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="f7320-143">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="f7320-144">Para que la aplicación sea accesible desde Internet, debes *hospedar* la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-144">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="f7320-145">Para las pruebas locales, puedes ejecutar la aplicación en el equipo local y crear un túnel para ella con un punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="f7320-145">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="f7320-146">[ngrok](https://ngrok.com) es una herramienta gratuita que te permite hacerlo.</span><span class="sxs-lookup"><span data-stu-id="f7320-146">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="f7320-147">Con *ngrok* puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo).</span><span class="sxs-lookup"><span data-stu-id="f7320-147">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="f7320-148">Puede descargar [e instalar](https://ngrok.com/download) *ngrok* para su entorno.</span><span class="sxs-lookup"><span data-stu-id="f7320-148">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="f7320-149">Asegúrese de agregarlo a una ubicación en el `PATH` archivo .</span><span class="sxs-lookup"><span data-stu-id="f7320-149">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="f7320-150">Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel.</span><span class="sxs-lookup"><span data-stu-id="f7320-150">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="f7320-151">El ejemplo usa el puerto 3333, así que asegúrese de especificarlo aquí.</span><span class="sxs-lookup"><span data-stu-id="f7320-151">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="f7320-152">*Ngrok* escuchará las solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333.</span><span class="sxs-lookup"><span data-stu-id="f7320-152">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="f7320-153">Para comprobarlo, abra el explorador y vaya `https://d0ac14a5.ngrok.io/hello` a cargar la página de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-153">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="f7320-154">Asegúrese de usar la dirección de reenvío mostrada por *ngrok* en la sesión de la consola en lugar de esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="f7320-154">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="f7320-155">Si ha usado un puerto [](#build-and-run-the-sample) diferente en la compilación y ejecuta el paso anterior, asegúrese de usar el mismo número de puerto para configurar el túnel *ngrok.*</span><span class="sxs-lookup"><span data-stu-id="f7320-155">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="f7320-156">Es una buena idea ejecutar *ngrok* en una ventana de terminal diferente para mantenerla en funcionamiento sin interferir con la aplicación de nodo que más adelante podría tener que detener, volver a compilar y volver a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="f7320-156">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="f7320-157">La *sesión ngrok* devolverá información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="f7320-157">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="f7320-158">Hay una versión de pago de *ngrok* que permite nombres persistentes.</span><span class="sxs-lookup"><span data-stu-id="f7320-158">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="f7320-159">Si usas la versión gratuita, la aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f7320-159">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="f7320-160">Si la máquina se apaga o se queda en modo de suspensión, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="f7320-160">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="f7320-161">Recuerda esto al compartir la aplicación para pruebas por otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="f7320-161">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="f7320-162">Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar cada lugar que use esa dirección.</span><span class="sxs-lookup"><span data-stu-id="f7320-162">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="f7320-163">Recuerda, toma nota de la dirección URL de la aplicación porque necesitarás esto más adelante cuando registres la aplicación con Teams mediante App studio.</span><span class="sxs-lookup"><span data-stu-id="f7320-163">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="f7320-164">Bloc de notas funciona bien para este propósito.</span><span class="sxs-lookup"><span data-stu-id="f7320-164">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="f7320-165">Implementar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f7320-165">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="f7320-166">En este momento tienes una aplicación hospedada en Internet, pero aún no tienes forma de decir a Teams dónde buscarla, ni siquiera cómo se llama a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-166">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="f7320-167">Para ello, ahora tienes que crear un paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-167">To do this you now have to create an app package.</span></span> <span data-ttu-id="f7320-168">Esto es poco más que un archivo de texto que contiene el manifiesto de la aplicación y algunos iconos que el cliente de Teams usará para mostrar y marcar correctamente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-168">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="f7320-169">Puedes crear manualmente este paquete de aplicación o puedes usar App Studio, una herramienta que se ejecuta en Teams que simplificará el proceso de registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-169">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="f7320-170">App Studio es la forma recomendada de crear y actualizar el paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-170">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="f7320-171">Para cualquiera de los dos métodos, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f7320-171">For either method you will need the following:</span></span>

- <span data-ttu-id="f7320-172">La dirección URL en la que se puede encontrar la aplicación en Internet.</span><span class="sxs-lookup"><span data-stu-id="f7320-172">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="f7320-173">Iconos que Teams usará para crear una marca de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-173">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="f7320-174">El ejemplo incluye iconos de marcador de posición ubicados en "src\static\images.</span><span class="sxs-lookup"><span data-stu-id="f7320-174">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="f7320-175">App Studio también proporcionará iconos predeterminados si es necesario.</span><span class="sxs-lookup"><span data-stu-id="f7320-175">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="f7320-176">Actualizar la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="f7320-176">Update your hosted app</span></span>

<span data-ttu-id="f7320-177">La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores de los que has tomado nota anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f7320-177">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="f7320-178">La forma en que lo haces varía en función de cómo hospedaste la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7320-178">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="f7320-179">Lo importante sobre el uso de variables de entorno es que estos valores forman parte del entorno: el código de la aplicación puede acceder a ellos, pero no se exponen a terceros que podrían examinar los archivos que forman el sitio.</span><span class="sxs-lookup"><span data-stu-id="f7320-179">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="f7320-180">Si ejecutas la aplicación con ngrok, tendrás que configurar algunas variables de entorno local.</span><span class="sxs-lookup"><span data-stu-id="f7320-180">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="f7320-181">Hay muchas maneras de hacerlo, pero lo más fácil, si usa Visual Studio Code, es agregar una configuración [de inicio:](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)</span><span class="sxs-lookup"><span data-stu-id="f7320-181">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="f7320-182">Donde:</span><span class="sxs-lookup"><span data-stu-id="f7320-182">Where:</span></span>

<span data-ttu-id="f7320-183">MICROSOFT_APP_ID y MICROSOFT_APP_PASSWORD es el identificador y la contraseña, respectivamente, para el bot.</span><span class="sxs-lookup"><span data-stu-id="f7320-183">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="f7320-184">NODE_DEBUG le mostrará lo que está sucediendo en el bot en la consola de depuración Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="f7320-184">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="f7320-185">NODE_CONFIG_DIR apunta al directorio en la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta localmente, lo busca en la carpeta src).</span><span class="sxs-lookup"><span data-stu-id="f7320-185">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="f7320-186">Si no has detenido npm desde antes en el tutorial, tendrás que ejecutar para que Visual Studio Code resalte correctamente las variables de `npm stop` configuración de inicio.</span><span class="sxs-lookup"><span data-stu-id="f7320-186">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="f7320-187">Configurar la pestaña aplicación</span><span class="sxs-lookup"><span data-stu-id="f7320-187">Configure the app tab</span></span>

<span data-ttu-id="f7320-188">Una vez que instales la aplicación en un equipo, deberás configurarla para mostrar contenido.</span><span class="sxs-lookup"><span data-stu-id="f7320-188">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="f7320-189">Vaya a un canal del equipo y haga clic en el **botón "+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir entre la lista Agregar **una** pestaña.</span><span class="sxs-lookup"><span data-stu-id="f7320-189">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="f7320-190">A continuación, se le mostrará un cuadro de diálogo de configuración.</span><span class="sxs-lookup"><span data-stu-id="f7320-190">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="f7320-191">Este cuadro de diálogo le permitirá elegir qué pestaña mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="f7320-191">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="f7320-192">Una vez que seleccione la pestaña y haga clic `Save` en, puede ver la `Hello World` pestaña cargada con la pestaña que eligió.</span><span class="sxs-lookup"><span data-stu-id="f7320-192">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="f7320-193">Probar el bot en Teams</span><span class="sxs-lookup"><span data-stu-id="f7320-193">Test your bot in Teams</span></span>

<span data-ttu-id="f7320-194">Ahora puedes interactuar con el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="f7320-194">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="f7320-195">Elige un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` , seguido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="f7320-195">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="f7320-196">Esto se denomina una **\@ mención**.</span><span class="sxs-lookup"><span data-stu-id="f7320-196">This is called an **\@mention**.</span></span> <span data-ttu-id="f7320-197">Cualquier mensaje que envíes al bot se te enviará como respuesta.</span><span class="sxs-lookup"><span data-stu-id="f7320-197">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="f7320-198">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="f7320-198">Test your messaging extension</span></span>

<span data-ttu-id="f7320-199">Para probar la extensión de mensajería, puedes hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="f7320-199">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="f7320-200">Aparecerá un menú con la **aplicación "Hello World".**</span><span class="sxs-lookup"><span data-stu-id="f7320-200">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="f7320-201">Al hacer clic en él, verá una serie de textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="f7320-201">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="f7320-202">Puede elegir cualquiera de ellos y se insertará en la conversación.</span><span class="sxs-lookup"><span data-stu-id="f7320-202">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="f7320-203">Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f7320-203">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
