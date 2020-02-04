---
title: Introducción al generador de Yeoman para Microsoft Teams
description: Empezar a compilar excelentes aplicaciones con el generador de Yeoman para Microsoft Teams
keywords: nodo introducción. js NodeJS Yeoman
ms.openlocfilehash: b0a9ae8d526286790d266e4291ef95d4ed7ce90f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675895"
---
# <a name="build-your-first-microsoft-teams-app"></a><span data-ttu-id="d76c5-104">Compilar la primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d76c5-104">Build your First Microsoft Teams App</span></span>

>[!Note]
><span data-ttu-id="d76c5-105">Este tutorial proviene del [generador de Yeoman para Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="d76c5-105">This tutorial comes from the [yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span></span>

<span data-ttu-id="d76c5-106">En este tutorial, veremos cómo crear su primera aplicación de Microsoft Teams con el generador de Yeoman de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d76c5-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="d76c5-107">Se da por hecho que ha [habilitado la carga del lado de las aplicaciones de Microsoft Teams](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d76c5-107">It assumes that you have [enabled side-loading of Microsoft Teams apps](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![git del generador de Yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="d76c5-109">Configurar y preparar el equipo</span><span class="sxs-lookup"><span data-stu-id="d76c5-109">Setup and prepare your machine</span></span>

<span data-ttu-id="d76c5-110">Debe instalar lo siguiente en su equipo antes de empezar a usar el generador de equipos.</span><span class="sxs-lookup"><span data-stu-id="d76c5-110">You need to install the following on your machine before starting to use the Teams Generator.</span></span>

### <a name="install-node"></a><span data-ttu-id="d76c5-111">Nodo de instalación</span><span class="sxs-lookup"><span data-stu-id="d76c5-111">Install Node</span></span>

<span data-ttu-id="d76c5-112">Debe tener NodeJS instalado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d76c5-112">You need to have NodeJS installed on your machine.</span></span> <span data-ttu-id="d76c5-113">Debe usar la última [versión de lts](https://nodejs.org/dist/latest-v8.x/).</span><span class="sxs-lookup"><span data-stu-id="d76c5-113">You should use the latest [LTS version](https://nodejs.org/dist/latest-v8.x/).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="d76c5-114">Instalar un editor de código</span><span class="sxs-lookup"><span data-stu-id="d76c5-114">Install a code editor</span></span>

<span data-ttu-id="d76c5-115">También necesita un editor de código, no dude en usar el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="d76c5-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="d76c5-116">Sin embargo, la mayoría de esta documentación y capturas de pantallas hacen referencia al uso de [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d76c5-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="d76c5-117">Instalar Yeoman y CLI de Gulp</span><span class="sxs-lookup"><span data-stu-id="d76c5-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="d76c5-118">Para poder aplicar scaffolding a los proyectos con el generador de Teams, debe instalar la herramienta Yeoman y el administrador de tareas de Gulp CLI.</span><span class="sxs-lookup"><span data-stu-id="d76c5-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="d76c5-119">Abra un símbolo del sistema y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d76c5-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-microsoft-teams-apps-generator---yo-teams"></a><span data-ttu-id="d76c5-120">Instalar el generador de aplicaciones de Microsoft Teams-yo Teams</span><span class="sxs-lookup"><span data-stu-id="d76c5-120">Install the Microsoft Teams Apps generator - Yo Teams</span></span>

<span data-ttu-id="d76c5-121">El generador de Yeoman para las aplicaciones de Microsoft Teams se instala con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d76c5-121">The Yeoman generator for Microsoft Teams apps are installed with the following command:</span></span>

```bash
npm install generator-teams --global
```

#### <a name="install-preview-versions"></a><span data-ttu-id="d76c5-122">Instalar versiones preliminares</span><span class="sxs-lookup"><span data-stu-id="d76c5-122">Install preview versions</span></span>

<span data-ttu-id="d76c5-123">Si desea instalar versiones preliminares del generador de equipos con este comando:</span><span class="sxs-lookup"><span data-stu-id="d76c5-123">If you want to install preview versions of the Teams generator with this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="d76c5-124">Generar el proyecto</span><span class="sxs-lookup"><span data-stu-id="d76c5-124">Generate your project</span></span>

<span data-ttu-id="d76c5-125">Abra un símbolo del sistema y cree un nuevo directorio donde desee crear el proyecto y, en ese directorio, escriba el comando `yo teams`.</span><span class="sxs-lookup"><span data-stu-id="d76c5-125">Open up a command prompt and create a new directory where you want to create your project and in that directory type the command `yo teams`.</span></span> <span data-ttu-id="d76c5-126">Se iniciará el generador de aplicaciones de Microsoft Teams y se le preguntará un conjunto de preguntas.</span><span class="sxs-lookup"><span data-stu-id="d76c5-126">This will start the Teams Apps generator and you will be asked a set of questions.</span></span>

![Yo Teams](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="d76c5-128">La primera pregunta trata sobre el nombre del proyecto, puede dejarlo como está presionando entrar.</span><span class="sxs-lookup"><span data-stu-id="d76c5-128">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="d76c5-129">La siguiente pregunta le preguntará si desea crear un nuevo directorio o usar el actual.</span><span class="sxs-lookup"><span data-stu-id="d76c5-129">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="d76c5-130">Como ya se encuentra en el directorio que queremos, simplemente se presiona la tecla entrar.</span><span class="sxs-lookup"><span data-stu-id="d76c5-130">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="d76c5-131">En el paso siguiente se solicita un título del proyecto, este título se utilizará en el manifiesto y la descripción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d76c5-131">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="d76c5-132">Y, a continuación, se le pedirá el nombre de la compañía, que también se usará en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="d76c5-132">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="d76c5-133">La quinta pregunta le pregunta qué versión del manifiesto desea usar.</span><span class="sxs-lookup"><span data-stu-id="d76c5-133">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="d76c5-134">Para este tutorial, `v1.5`seleccione, que es el esquema actual disponible en general.</span><span class="sxs-lookup"><span data-stu-id="d76c5-134">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="d76c5-135">Después de esto, el generador le pedirá qué elementos desea agregar a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="d76c5-135">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="d76c5-136">Puede seleccionar una sola combinación de elementos o una combinación de ellos.</span><span class="sxs-lookup"><span data-stu-id="d76c5-136">You can select a single one or any combination of items.</span></span> <span data-ttu-id="d76c5-137">Por ahora, solo tiene que seleccionar *una pestaña*.</span><span class="sxs-lookup"><span data-stu-id="d76c5-137">For now, just select *a Tab*.</span></span>

![selección de elementos](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="d76c5-139">En función de los elementos que seleccione, se le preguntará un conjunto de preguntas de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="d76c5-139">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="d76c5-140">Ahora debe escribir una dirección URL donde hospedará la solución.</span><span class="sxs-lookup"><span data-stu-id="d76c5-140">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="d76c5-141">Puede ser cualquier dirección URL, pero, de forma predeterminada, el generador sugiere una dirección URL de sitios web de Azure.</span><span class="sxs-lookup"><span data-stu-id="d76c5-141">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="d76c5-142">El generador tiene muchas características avanzadas integradas que puede incluir o excluir de ellas.</span><span class="sxs-lookup"><span data-stu-id="d76c5-142">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="d76c5-143">Tras la pregunta de dirección URL se le preguntará si desea incluir pruebas unitarias para su solución, de forma predeterminada es sí.</span><span class="sxs-lookup"><span data-stu-id="d76c5-143">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="d76c5-144">Si elige esta opción, el proyecto generado tendrá un marco de pruebas unitarias y algunas pruebas unitarias predeterminadas para los distintos elementos que se van a scaffolding.</span><span class="sxs-lookup"><span data-stu-id="d76c5-144">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="d76c5-145">Para este tutorial, elija no incluir un marco de prueba.</span><span class="sxs-lookup"><span data-stu-id="d76c5-145">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="d76c5-146">Para que el registro sea más fácil, también se le preguntará si quiere usar Azure Application Insights para el registro.</span><span class="sxs-lookup"><span data-stu-id="d76c5-146">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="d76c5-147">Si elige sí, tendrá que proporcionar una clave de Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d76c5-147">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="d76c5-148">Para este tutorial, rechace la utilización de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d76c5-148">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="d76c5-149">El siguiente conjunto de preguntas se basará en la selección de elementos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d76c5-149">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="d76c5-150">Para una pestaña solo tiene que proporcionar un nombre y, opcionalmente, elegir si desea poder usar esta aplicación como un elemento Web de SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d76c5-150">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="d76c5-151">Una vez que haya proporcionado el nombre, el generador generará el proyecto e instalará todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="d76c5-151">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="d76c5-152">Esto tardará un minuto o dos.</span><span class="sxs-lookup"><span data-stu-id="d76c5-152">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="d76c5-153">Agregar código a la pestaña</span><span class="sxs-lookup"><span data-stu-id="d76c5-153">Add some code to your tab</span></span>

<span data-ttu-id="d76c5-154">Una vez que el generador haya finalizado, podrá abrir la solución en su editor de código favorito.</span><span class="sxs-lookup"><span data-stu-id="d76c5-154">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="d76c5-155">Tómese un minuto o dos y familiarícese con cómo se organiza el código: puede obtener más información sobre esto en la documentación sobre la [estructura del proyecto](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) .</span><span class="sxs-lookup"><span data-stu-id="d76c5-155">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="d76c5-156">La pestaña se ubicará en el `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` archivo.</span><span class="sxs-lookup"><span data-stu-id="d76c5-156">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="d76c5-157">Esta es la clase basada en TypeScript reAct para su pestaña. busque `render()` el método y agregue una línea de código dentro `<PanelBody>` del control para que tenga el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="d76c5-157">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="d76c5-158">Guarde el archivo y vuelva a la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d76c5-158">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="d76c5-159">Crear una aplicación</span><span class="sxs-lookup"><span data-stu-id="d76c5-159">Build your app</span></span>

<span data-ttu-id="d76c5-160">Ahora puede compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d76c5-160">You can now build your project.</span></span> <span data-ttu-id="d76c5-161">Esto se realiza en dos pasos (o un paso, vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="d76c5-161">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="d76c5-162">En primer lugar, debe crear el archivo de manifiesto de la aplicación Teams, que carga o transferir localmente a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d76c5-162">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="d76c5-163">Esto se realiza mediante la tarea `gulp manifest`de Gulp.</span><span class="sxs-lookup"><span data-stu-id="d76c5-163">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="d76c5-164">Se validará el manifiesto y se creará un archivo zip `./package` en el directorio.</span><span class="sxs-lookup"><span data-stu-id="d76c5-164">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="d76c5-165">Para compilar la solución, `gulp build` use el comando.</span><span class="sxs-lookup"><span data-stu-id="d76c5-165">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="d76c5-166">Se transpilará la solución a la `./dist` carpeta.</span><span class="sxs-lookup"><span data-stu-id="d76c5-166">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="d76c5-167">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="d76c5-167">Run your app</span></span>

<span data-ttu-id="d76c5-168">Para ejecutar la aplicación, use el `gulp serve` comando.</span><span class="sxs-lookup"><span data-stu-id="d76c5-168">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="d76c5-169">Se compilará e iniciará un servidor Web local para que pueda probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d76c5-169">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="d76c5-170">El comando también volverá a generar la aplicación cada vez que guarde un archivo en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d76c5-170">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="d76c5-171">Ahora debería poder ir a `http://localhost:3007/myFirstAppTab/` para asegurarse de que la pestaña está en representación.</span><span class="sxs-lookup"><span data-stu-id="d76c5-171">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="d76c5-172">Sin embargo, aún no en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d76c5-172">However, not in Microsoft Teams yet.</span></span>

![ver el sitio en un explorador](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="d76c5-174">Ejecutar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d76c5-174">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="d76c5-175">Microsoft Teams no le permite hospedar la aplicación en localhost, por lo que debe publicarla en una dirección URL pública o usar un proxy como ngrok.</span><span class="sxs-lookup"><span data-stu-id="d76c5-175">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="d76c5-176">Una buena noticia es que el proyecto con scaffolding tiene esta integrado.</span><span class="sxs-lookup"><span data-stu-id="d76c5-176">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="d76c5-177">Al ejecutar `gulp ngrok-serve` el servicio ngrok, se iniciará en segundo plano, con un único y una entrada DNS pública, y también empaquetará el manifiesto con esa dirección URL única y, a continuación, hará `gulp serve`exactamente lo mismo que.</span><span class="sxs-lookup"><span data-stu-id="d76c5-177">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unqiue and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="d76c5-178">Una vez `gulp ngrok-serve`ejecutado, cree un nuevo equipo de Microsoft Teams y, cuando se haya creado, haga clic en el nombre del equipo, vaya a la configuración de Microsoft Teams y seleccione *aplicaciones*.</span><span class="sxs-lookup"><span data-stu-id="d76c5-178">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="d76c5-179">En la esquina inferior derecha, debería ver un vínculo *cargar una aplicación personalizada*, seleccionarla y, a continuación, buscar la carpeta del proyecto y la `package`subcarpeta denominada.</span><span class="sxs-lookup"><span data-stu-id="d76c5-179">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="d76c5-180">Seleccione el archivo zip en esa carpeta y elija Abrir.</span><span class="sxs-lookup"><span data-stu-id="d76c5-180">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="d76c5-181">La aplicación ahora se transferirá a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d76c5-181">Your App is now sideloaded into Microsoft Teams.</span></span>

![aplicación transferida localmente](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="d76c5-183">Vuelva al canal *General* y seleccione *+* agregar una nueva pestaña. Debe ver la ficha en la lista de pestañas.</span><span class="sxs-lookup"><span data-stu-id="d76c5-183">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![pestaña configurar](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="d76c5-185">Elija su pestaña y siga las instrucciones para agregarlo.</span><span class="sxs-lookup"><span data-stu-id="d76c5-185">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="d76c5-186">Tenga en cuenta que tiene un cuadro de diálogo de configuración personalizada, para el que puede editar el origen.</span><span class="sxs-lookup"><span data-stu-id="d76c5-186">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="d76c5-187">Seleccione *Guardar* para agregar su pestaña al canal.</span><span class="sxs-lookup"><span data-stu-id="d76c5-187">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="d76c5-188">Una vez que haya terminado, la pestaña debe estar cargada en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d76c5-188">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![pestaña en ejecución en Microsoft Teams](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="d76c5-190">**Congrats! Ha compilado e implementado su primera aplicación de Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="d76c5-190">**Congrats! You built and deployed your first Microsoft Teams App**</span></span>
