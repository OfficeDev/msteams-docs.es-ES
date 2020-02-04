---
title: Introducción a App Studio y node. js
description: Empezar a compilar excelentes aplicaciones en Microsoft Teams con node. js y app Studio
keywords: nodo introducción. js NodeJS App Studio
ms.date: 11/09/2018
ms.openlocfilehash: 36da6d7445ad7780f6bbbf52ccce3e558c76be72
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676142"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a><span data-ttu-id="0037e-104">Introducción a la plataforma de Microsoft Teams con node. js y app Studio</span><span class="sxs-lookup"><span data-stu-id="0037e-104">Get started on the Microsoft Teams platform with Node.js and App Studio</span></span>

<span data-ttu-id="0037e-105">La plataforma de desarrolladores de [Microsoft Teams](/microsoftteams/) facilita la tarea de ampliar Teams e integrar sus propias aplicaciones y servicios sin problemas en el área de trabajo de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0037e-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="0037e-106">A continuación, estas aplicaciones pueden distribuirse a su empresa o a equipos de todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="0037e-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="0037e-107">Para ampliar Microsoft Teams, debe crear una aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0037e-107">To extend Microsoft Teams, you need to create a Microsoft Teams app.</span></span> <span data-ttu-id="0037e-108">Una aplicación de Microsoft Teams es una aplicación web que hospeda.</span><span class="sxs-lookup"><span data-stu-id="0037e-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="0037e-109">A continuación, esta aplicación se puede integrar en el área de trabajo del usuario en Teams.</span><span class="sxs-lookup"><span data-stu-id="0037e-109">This app can then be integrated into the user's workspace in Teams.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="0037e-110">Descargar y hospedar la aplicación</span><span class="sxs-lookup"><span data-stu-id="0037e-110">Download and host your app</span></span>

<span data-ttu-id="0037e-111">Siga estos pasos para descargar y hospedar una aplicación "Hola a todos" sencilla en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0037e-111">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="0037e-112">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0037e-112">Get prerequisites</span></span>

<span data-ttu-id="0037e-113">Para completar este tutorial, necesitará las siguientes herramientas.</span><span class="sxs-lookup"><span data-stu-id="0037e-113">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="0037e-114">Si todavía no los tiene, puede instalarlas desde estos vínculos.</span><span class="sxs-lookup"><span data-stu-id="0037e-114">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="0037e-115">Git</span><span class="sxs-lookup"><span data-stu-id="0037e-115">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="0037e-116">Node. js y NPM</span><span class="sxs-lookup"><span data-stu-id="0037e-116">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="0037e-117">Obtenga cualquier editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="0037e-117">Get any text editor or IDE.</span></span> <span data-ttu-id="0037e-118">Puede instalar y usar [Visual Studio Code](https://code.visualstudio.com/download) de forma gratuita.</span><span class="sxs-lookup"><span data-stu-id="0037e-118">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="0037e-119">Si ve opciones para `git`agregar, `node`, `npm`y `code` a la ruta de acceso durante la instalación, elija esta opción.</span><span class="sxs-lookup"><span data-stu-id="0037e-119">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="0037e-120">Será útil.</span><span class="sxs-lookup"><span data-stu-id="0037e-120">It will be handy.</span></span>

<span data-ttu-id="0037e-121">Compruebe que las herramientas están disponibles al ejecutar lo siguiente en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="0037e-121">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="0037e-122">Use la ventana de terminal que le resulte más cómoda en su plataforma.</span><span class="sxs-lookup"><span data-stu-id="0037e-122">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="0037e-123">En estos ejemplos se usa Bash (que se incluye en Git), pero estos scripts se ejecutarán en la mayoría de las plataformas.</span><span class="sxs-lookup"><span data-stu-id="0037e-123">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 4.0.2
```

<span data-ttu-id="0037e-124">Es posible que tenga una versión diferente de estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0037e-124">You may have a different version of these applications.</span></span> <span data-ttu-id="0037e-125">Esto no debería ser un problema, excepto para Gulp.</span><span class="sxs-lookup"><span data-stu-id="0037e-125">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="0037e-126">Para Gulp tendrá que usar la versión 4.0.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0037e-126">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="0037e-127">Si no tiene Gulp instalado (o tiene instalada una versión incorrecta), hágalo ahora ejecutando `npm install gulp` en la ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="0037e-127">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="0037e-128">Si ha instalado Visual Studio Code, puede comprobar la instalación ejecutando:</span><span class="sxs-lookup"><span data-stu-id="0037e-128">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="0037e-129">Puede seguir usando esta ventana de terminal para ejecutar los comandos que se indican a continuación en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0037e-129">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="0037e-130">Descargar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="0037e-130">Download the sample</span></span>

<span data-ttu-id="0037e-131">Hemos proporcionado un sencillo [Hola a todos.](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="0037e-131">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span></span> <span data-ttu-id="0037e-132">muestra que le ayuda a empezar.</span><span class="sxs-lookup"><span data-stu-id="0037e-132">sample to get you started.</span></span> <span data-ttu-id="0037e-133">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="0037e-133">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> <span data-ttu-id="0037e-134">Puede [bifurcar](https://help.github.com/articles/fork-a-repo/) este [repositorio](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) si desea modificar y proteger los cambios en el repositorio de github para futuras referencias.</span><span class="sxs-lookup"><span data-stu-id="0037e-134">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="0037e-135">Compilar y ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="0037e-135">Build and run the sample</span></span>

<span data-ttu-id="0037e-136">Una vez que se clona el repositorio, cambie al directorio que contiene el ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0037e-136">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd msteams-samples-hello-world-nodejs
```

<span data-ttu-id="0037e-137">Para poder compilar el ejemplo, debe instalar todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="0037e-137">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="0037e-138">Ejecute el siguiente comando para hacerlo:</span><span class="sxs-lookup"><span data-stu-id="0037e-138">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="0037e-139">Debe ver un conjunto de dependencias que se van a instalar.</span><span class="sxs-lookup"><span data-stu-id="0037e-139">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="0037e-140">Una vez que hayan finalizado, puede ejecutar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="0037e-140">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="0037e-141">Cuando se inicia la aplicación Hello World, se muestra `App started listening on port 3333` en la ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="0037e-141">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="0037e-142">Si ve que aparece un número de puerto diferente en el mensaje anterior, es porque tiene establecida una variable de entorno PORT.</span><span class="sxs-lookup"><span data-stu-id="0037e-142">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="0037e-143">Puede seguir usando ese puerto o cambiar la variable de entorno a 3333.</span><span class="sxs-lookup"><span data-stu-id="0037e-143">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="0037e-144">En este punto, puede abrir una ventana del explorador y navegar a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se cargan:</span><span class="sxs-lookup"><span data-stu-id="0037e-144">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="0037e-145">Hospedar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0037e-145">Host the sample app</span></span>

<span data-ttu-id="0037e-146">Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más capacidades.</span><span class="sxs-lookup"><span data-stu-id="0037e-146">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="0037e-147">Para que la plataforma de Microsoft Teams cargue la aplicación, la aplicación debe ser accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="0037e-147">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="0037e-148">Para hacer que la aplicación sea accesible desde Internet, debe *hospedar* la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-148">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="0037e-149">Para las pruebas locales, puede ejecutar la aplicación en el equipo local y crear un túnel con un punto de conexión Web.</span><span class="sxs-lookup"><span data-stu-id="0037e-149">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="0037e-150">[ngrok](https://ngrok.com) es una herramienta gratuita que le permite hacer justamente eso.</span><span class="sxs-lookup"><span data-stu-id="0037e-150">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="0037e-151">Con *ngrok* puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo).</span><span class="sxs-lookup"><span data-stu-id="0037e-151">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="0037e-152">Puede [Descargar e instalar](https://ngrok.com/download) *ngrok* para su entorno.</span><span class="sxs-lookup"><span data-stu-id="0037e-152">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="0037e-153">Asegúrese de agregarlo a una ubicación en el `PATH`.</span><span class="sxs-lookup"><span data-stu-id="0037e-153">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="0037e-154">Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel.</span><span class="sxs-lookup"><span data-stu-id="0037e-154">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="0037e-155">En el ejemplo se usa el puerto 3333, por lo que debe asegurarse de especificarlo aquí.</span><span class="sxs-lookup"><span data-stu-id="0037e-155">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="0037e-156">*Ngrok* escuchará solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333.</span><span class="sxs-lookup"><span data-stu-id="0037e-156">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="0037e-157">`https://d0ac14a5.ngrok.io/hello` Para comprobarlo, abra el explorador y vaya a para cargar la página Hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-157">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="0037e-158">Asegúrese de usar la dirección de reenvío que muestra *ngrok* en la sesión de consola en lugar de esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="0037e-158">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="0037e-159">Si ha usado un puerto diferente en el paso de [compilación y ejecutar](#build-and-run-the-sample) anterior, asegúrese de usar el mismo número de puerto para configurar el túnel *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="0037e-159">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="0037e-160">Es buena idea ejecutar *ngrok* en una ventana de terminal diferente para mantenerla en ejecución sin interferir con la aplicación de nodo que, posteriormente, se debe detener, volver a crear y volver a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="0037e-160">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="0037e-161">La sesión de *ngrok* devolverá información de depuración útil en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="0037e-161">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="0037e-162">Hay una versión de pago de *ngrok* que permite nombres persistentes.</span><span class="sxs-lookup"><span data-stu-id="0037e-162">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="0037e-163">Si usa la versión gratuita, la aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="0037e-163">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="0037e-164">Si el equipo está apagado o entra en suspensión, el servicio dejará de estar disponible.</span><span class="sxs-lookup"><span data-stu-id="0037e-164">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="0037e-165">Recuerde esto cuando comparta la aplicación para que la prueben otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="0037e-165">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="0037e-166">Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar todos los sitios que usen esa dirección.</span><span class="sxs-lookup"><span data-stu-id="0037e-166">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="0037e-167">Recuerde que anote la dirección URL de la aplicación, ya que la necesitará más adelante cuando registre la aplicación con Teams mediante App Studio.</span><span class="sxs-lookup"><span data-stu-id="0037e-167">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="0037e-168">El Bloc de notas funciona bien para este propósito.</span><span class="sxs-lookup"><span data-stu-id="0037e-168">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="0037e-169">Implementar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0037e-169">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="0037e-170">En este punto, tiene una aplicación hospedada en Internet, pero todavía no tiene ninguna manera de indicar a teams dónde buscarla, o incluso qué se llama a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-170">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="0037e-171">Para ello, ahora tiene que crear un paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-171">To do this you now have to create an app package.</span></span> <span data-ttu-id="0037e-172">Esto es algo más que un archivo de texto que contiene el manifiesto de la aplicación y algunos iconos que usará el cliente de Microsoft Teams para mostrar y marcar correctamente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-172">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="0037e-173">Puede crear manualmente este paquete de la aplicación o puede usar App Studio, una herramienta que se ejecuta en Microsoft teams que simplificará el proceso de registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-173">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="0037e-174">App Studio es la forma recomendada de crear y actualizar el paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-174">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="0037e-175">Para cualquiera de los dos métodos, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0037e-175">For either method you will need the following:</span></span>

- <span data-ttu-id="0037e-176">La dirección URL en la que se puede encontrar la aplicación en Internet.</span><span class="sxs-lookup"><span data-stu-id="0037e-176">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="0037e-177">Iconos que los equipos usarán para personalizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-177">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="0037e-178">El ejemplo incluye iconos de marcador de posición ubicados en "src\static\images.</span><span class="sxs-lookup"><span data-stu-id="0037e-178">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="0037e-179">App Studio también proporcionará los iconos predeterminados, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="0037e-179">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="0037e-180">Actualizar la aplicación hospedada</span><span class="sxs-lookup"><span data-stu-id="0037e-180">Update your hosted app</span></span>

<span data-ttu-id="0037e-181">La aplicación de ejemplo requiere que se establezcan las siguientes variables de entorno en los valores que ha anotado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0037e-181">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="0037e-182">La forma de hacerlo varía en función de cómo hospedaste la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0037e-182">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="0037e-183">Lo más importante sobre el uso de variables de entorno es que estos valores forman parte de su entorno: se puede acceder a ellos mediante el código de la aplicación, pero no están expuestos a terceros que puedan examinar los archivos que componen el sitio.</span><span class="sxs-lookup"><span data-stu-id="0037e-183">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="0037e-184">Si está ejecutando la aplicación con ngrok, tendrá que configurar algunas variables de entorno local.</span><span class="sxs-lookup"><span data-stu-id="0037e-184">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="0037e-185">Hay muchas formas de hacerlo, pero la más sencilla, si usa Visual Studio Code, es agregar una [configuración de inicio](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span><span class="sxs-lookup"><span data-stu-id="0037e-185">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="0037e-186">Donde:</span><span class="sxs-lookup"><span data-stu-id="0037e-186">Where:</span></span>

<span data-ttu-id="0037e-187">MICROSOFT_APP_ID y MICROSOFT_APP_PASSWORD es el identificador y la contraseña, respectivamente, para el bot.</span><span class="sxs-lookup"><span data-stu-id="0037e-187">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="0037e-188">NODE_DEBUG le mostrarán lo que está sucediendo en su bot en la consola de depuración de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0037e-188">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="0037e-189">NODE_CONFIG_DIR apunta al directorio de la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta de forma local, la busca en la carpeta src).</span><span class="sxs-lookup"><span data-stu-id="0037e-189">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="0037e-190">Si no ha detenido NPM de anteriormente en el tutorial, deberá ejecutar `npm stop` para que Visual Studio Code devuelva las variables de configuración de inicio correctamente.</span><span class="sxs-lookup"><span data-stu-id="0037e-190">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="0037e-191">Configurar la pestaña de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0037e-191">Configure the app tab</span></span>

<span data-ttu-id="0037e-192">Una vez que haya instalado la aplicación en un equipo, tendrá que configurarla para mostrar el contenido.</span><span class="sxs-lookup"><span data-stu-id="0037e-192">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="0037e-193">Vaya a un canal del equipo y haga clic en el botón **"+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir en la lista **Agregar una pestaña** .</span><span class="sxs-lookup"><span data-stu-id="0037e-193">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="0037e-194">A continuación, se mostrará un cuadro de diálogo de configuración.</span><span class="sxs-lookup"><span data-stu-id="0037e-194">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="0037e-195">Este cuadro de diálogo le permitirá elegir la pestaña que desea mostrar en este canal.</span><span class="sxs-lookup"><span data-stu-id="0037e-195">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="0037e-196">Una vez que seleccione la pestaña y haga `Save` clic en, puede `Hello World` ver la ficha cargada con la pestaña que eligió.</span><span class="sxs-lookup"><span data-stu-id="0037e-196">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" title="Captura de pantalla de configurar" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="0037e-198">Probar el bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0037e-198">Test your bot in Teams</span></span>

<span data-ttu-id="0037e-199">Ahora puede interactuar con el bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="0037e-199">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="0037e-200">Elija un canal del equipo en el que haya registrado la aplicación y escriba `@your-bot-name`, seguido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="0037e-200">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="0037e-201">Esto se denomina una \*\* \@mención\*\*.</span><span class="sxs-lookup"><span data-stu-id="0037e-201">This is called an **\@mention**.</span></span> <span data-ttu-id="0037e-202">Cualquier mensaje que envíe al bot se le enviará como respuesta.</span><span class="sxs-lookup"><span data-stu-id="0037e-202">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" title="Respuestas de bot" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="0037e-204">Probar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="0037e-204">Test your messaging extension</span></span>

<span data-ttu-id="0037e-205">Para probar la extensión de mensajería, puede hacer clic en los tres puntos situados debajo del cuadro de entrada en la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="0037e-205">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="0037e-206">Se mostrará un menú con la aplicación **"Hola a todos"** .</span><span class="sxs-lookup"><span data-stu-id="0037e-206">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="0037e-207">Al hacer clic en él, verá un número de textos aleatorios.</span><span class="sxs-lookup"><span data-stu-id="0037e-207">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="0037e-208">Puede elegir una de ellas y se insertará en la conversación.</span><span class="sxs-lookup"><span data-stu-id="0037e-208">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" title="Menú de extensiones de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" title="Resultado de la extensión de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="0037e-211">Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0037e-211">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" title="Envío de extensiones de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
