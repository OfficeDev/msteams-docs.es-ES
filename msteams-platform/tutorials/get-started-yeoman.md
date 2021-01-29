---
title: 'Tutorial: crear la primera aplicación con el generador de Yeoman'
description: Obtenga información sobre cómo empezar a compilar aplicaciones de Microsoft Teams con el generador de Yeoman.
keywords: introducción a node.js nodejs yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037007"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="fc004-104">Crear la primera aplicación de Microsoft Teams con el generador de Yeoman</span><span class="sxs-lookup"><span data-stu-id="fc004-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

>[!Note]
><span data-ttu-id="fc004-105">Este tutorial procede del generador [de Yeoman para la wiki de Teams.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="fc004-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="fc004-106">En este tutorial, le mostraremos cómo crear su primera aplicación de Microsoft Teams con el generador de Yeoman de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fc004-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="fc004-107">Se supone que tiene una cuenta de Teams que permite [la instalación de prueba de la aplicación.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="fc004-107">It assumes that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![yeoman generator git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="fc004-109">Configurar y preparar el equipo</span><span class="sxs-lookup"><span data-stu-id="fc004-109">Setup and prepare your machine</span></span>

<span data-ttu-id="fc004-110">Debes instalar lo siguiente en el equipo antes de empezar a usar el generador de Yeoman.</span><span class="sxs-lookup"><span data-stu-id="fc004-110">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="fc004-111">Instalar Node.js</span><span class="sxs-lookup"><span data-stu-id="fc004-111">Install Node.js</span></span>

<span data-ttu-id="fc004-112">Debes tener Node.js instalado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fc004-112">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="fc004-113">Debe usar la versión más reciente [de LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="fc004-113">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="fc004-114">Instalar un editor de código</span><span class="sxs-lookup"><span data-stu-id="fc004-114">Install a code editor</span></span>

<span data-ttu-id="fc004-115">También necesitas un editor de código, no dudes en usar el editor de texto que prefieras.</span><span class="sxs-lookup"><span data-stu-id="fc004-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="fc004-116">Sin embargo, la mayoría de esta documentación y capturas de pantalla hacen referencia al [uso Visual Studio código.](https://code.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="fc004-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="fc004-117">Instalar la CLI de Yeoman y Gulp</span><span class="sxs-lookup"><span data-stu-id="fc004-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="fc004-118">Para poder realizar scaffolding en proyectos con el generador de Teams, debe instalar la herramienta Yeoman, así como el administrador de tareas de la CLI de Gulp.</span><span class="sxs-lookup"><span data-stu-id="fc004-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="fc004-119">Abra un símbolo del sistema y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fc004-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="fc004-120">Instalar el generador</span><span class="sxs-lookup"><span data-stu-id="fc004-120">Install the generator</span></span>

<span data-ttu-id="fc004-121">Instale el generador de Yeoman de Teams con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fc004-121">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="fc004-122">Para instalar versiones preliminares del generador, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="fc004-122">To install preview versions of the generator, run this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="fc004-123">Generar el proyecto</span><span class="sxs-lookup"><span data-stu-id="fc004-123">Generate your project</span></span>

<span data-ttu-id="fc004-124">Abra un símbolo del sistema y cree un directorio donde quiera crear el proyecto y, en ese directorio, ejecute el `yo teams` comando.</span><span class="sxs-lookup"><span data-stu-id="fc004-124">Open up a command prompt and create a new directory where you want to create your project and in that directory run the command `yo teams`.</span></span>

<span data-ttu-id="fc004-125">Esto inicia el generador, que le pedirá un conjunto de preguntas.</span><span class="sxs-lookup"><span data-stu-id="fc004-125">This starts the generator, which prompts you with a set of questions.</span></span>

![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="fc004-127">La primera pregunta es sobre el nombre del proyecto, puede dejarlo tal como está presionando ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="fc004-127">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="fc004-128">La siguiente pregunta le pregunta si desea crear un nuevo directorio o usar el actual.</span><span class="sxs-lookup"><span data-stu-id="fc004-128">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="fc004-129">Como ya estamos en el directorio que queremos, simplemente presionamos ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="fc004-129">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="fc004-130">En el siguiente paso se pide un título del proyecto, este título se usará en el manifiesto y la descripción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fc004-130">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="fc004-131">Y, a continuación, se le pedirá un nombre de compañía, que también se usará en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="fc004-131">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="fc004-132">La quinta pregunta le pregunta qué versión del manifiesto desea usar.</span><span class="sxs-lookup"><span data-stu-id="fc004-132">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="fc004-133">Para este tutorial, seleccione `v1.5` , que es el esquema disponible general actual.</span><span class="sxs-lookup"><span data-stu-id="fc004-133">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="fc004-134">Después, el generador le preguntará qué elementos desea agregar a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="fc004-134">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="fc004-135">Puede seleccionar una sola o cualquier combinación de elementos.</span><span class="sxs-lookup"><span data-stu-id="fc004-135">You can select a single one or any combination of items.</span></span> <span data-ttu-id="fc004-136">Por ahora, solo tiene que *seleccionar una pestaña*.</span><span class="sxs-lookup"><span data-stu-id="fc004-136">For now, just select *a Tab*.</span></span>

![selección de elemento](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="fc004-138">En función de los elementos que seleccione, se le hará un conjunto de preguntas de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="fc004-138">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="fc004-139">Ahora debe escribir una dirección URL donde hospedará la solución.</span><span class="sxs-lookup"><span data-stu-id="fc004-139">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="fc004-140">Puede ser cualquier dirección URL, pero de forma predeterminada el generador sugiere una dirección URL de Sitios web de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc004-140">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="fc004-141">El generador tiene una gran cantidad de características avanzadas integradas que puede optar por participar o no participar.</span><span class="sxs-lookup"><span data-stu-id="fc004-141">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="fc004-142">Si sigue la pregunta de dirección URL que se le hará si desea incluir pruebas unitarias para la solución, el valor predeterminado es sí.</span><span class="sxs-lookup"><span data-stu-id="fc004-142">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="fc004-143">Si eliges esto, el proyecto generado tendrá un marco de pruebas unitarias y algunas pruebas unitarias predeterminadas para los distintos elementos que se van a scaffolding.</span><span class="sxs-lookup"><span data-stu-id="fc004-143">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="fc004-144">Para este tutorial, elija no incluir un marco de prueba.</span><span class="sxs-lookup"><span data-stu-id="fc004-144">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="fc004-145">Para facilitar el registro, también se le preguntará si desea usar Azure Application Insights para el registro.</span><span class="sxs-lookup"><span data-stu-id="fc004-145">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="fc004-146">Si elige Sí, deberá proporcionar una clave de Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fc004-146">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="fc004-147">En este tutorial no se puede usar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fc004-147">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="fc004-148">El siguiente conjunto de preguntas se basará en la selección de elementos previamente.</span><span class="sxs-lookup"><span data-stu-id="fc004-148">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="fc004-149">Para una pestaña solo necesita proporcionar un nombre y, opcionalmente, elegir si desea poder usar esta aplicación como un elemento web de SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="fc004-149">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="fc004-150">Una vez que haya proporcionado este nombre, el generador generará el proyecto e instalará todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="fc004-150">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="fc004-151">Esto puede tardar uno o dos minutos.</span><span class="sxs-lookup"><span data-stu-id="fc004-151">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="fc004-152">Agregar código a la pestaña</span><span class="sxs-lookup"><span data-stu-id="fc004-152">Add some code to your tab</span></span>

<span data-ttu-id="fc004-153">Una vez que haya terminado el generador, puede abrir la solución en su editor de código favorito.</span><span class="sxs-lookup"><span data-stu-id="fc004-153">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="fc004-154">Tómese uno o dos minutos y familiarícese con cómo se organiza el código; puede leer más sobre esto en la documentación de la estructura [del](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) proyecto.</span><span class="sxs-lookup"><span data-stu-id="fc004-154">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="fc004-155">La pestaña se encontrará en el `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` archivo.</span><span class="sxs-lookup"><span data-stu-id="fc004-155">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="fc004-156">Esta es la clase basada en TypeScript React para la pestaña. Busque el método y agregue una línea de código dentro del control para que se vea `render()` `<PanelBody>` así:</span><span class="sxs-lookup"><span data-stu-id="fc004-156">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="fc004-157">Guarde el archivo y vuelva al símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="fc004-157">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="fc004-158">Crear una aplicación</span><span class="sxs-lookup"><span data-stu-id="fc004-158">Build your app</span></span>

<span data-ttu-id="fc004-159">Ahora puede compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="fc004-159">You can now build your project.</span></span> <span data-ttu-id="fc004-160">Esto se realiza en dos pasos (o un paso, consulta a continuación).</span><span class="sxs-lookup"><span data-stu-id="fc004-160">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="fc004-161">En primer lugar, debe crear el archivo de manifiesto de la aplicación de Teams que cargue o cargue localmente en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fc004-161">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="fc004-162">Esto se realiza mediante la tarea de Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="fc004-162">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="fc004-163">Esto validará el manifiesto y creará un archivo zip en el `./package` directorio.</span><span class="sxs-lookup"><span data-stu-id="fc004-163">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="fc004-164">Para crear la solución, use el `gulp build` comando.</span><span class="sxs-lookup"><span data-stu-id="fc004-164">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="fc004-165">Esto transpilará la solución en la `./dist` carpeta.</span><span class="sxs-lookup"><span data-stu-id="fc004-165">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="fc004-166">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="fc004-166">Run your app</span></span>

<span data-ttu-id="fc004-167">Para ejecutar la aplicación, usas el `gulp serve` comando.</span><span class="sxs-lookup"><span data-stu-id="fc004-167">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="fc004-168">Esto compilará e iniciará un servidor web local para que pruebe la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fc004-168">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="fc004-169">El comando también volverá a generar la aplicación siempre que guarde un archivo en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="fc004-169">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="fc004-170">Ahora debería poder explorar para asegurarse de `http://localhost:3007/myFirstAppTab/` que se está representando la pestaña.</span><span class="sxs-lookup"><span data-stu-id="fc004-170">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="fc004-171">Sin embargo, aún no está en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fc004-171">However, not in Microsoft Teams yet.</span></span>

![ver el sitio en un explorador](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="fc004-173">Ejecutar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fc004-173">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="fc004-174">Microsoft Teams no le permite tener la aplicación hospedada en localhost, por lo que necesita publicarla en una dirección URL pública o usar un proxy como ngrok.</span><span class="sxs-lookup"><span data-stu-id="fc004-174">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="fc004-175">Una buena noticia es que el proyecto con scaffolding tiene esto integrado.</span><span class="sxs-lookup"><span data-stu-id="fc004-175">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="fc004-176">Cuando ejecute el servicio ngrok se iniciará en segundo plano, con una entrada DNS única y pública, y también empaquetará el manifiesto con esa dirección URL única y, a continuación, hará exactamente lo mismo que `gulp ngrok-serve` `gulp serve` .</span><span class="sxs-lookup"><span data-stu-id="fc004-176">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="fc004-177">Después de ejecutar , cree un nuevo equipo de Microsoft Teams y, cuando se cree, haga clic en el nombre del equipo, para ir a la configuración de teams y, `gulp ngrok-serve` a continuación, *seleccione Aplicaciones.*</span><span class="sxs-lookup"><span data-stu-id="fc004-177">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="fc004-178">En la esquina inferior derecha debería ver un vínculo Cargar una aplicación personalizada, selecciónelo y, a continuación, vaya *a* la carpeta del proyecto y a la subcarpeta llamada `package` .</span><span class="sxs-lookup"><span data-stu-id="fc004-178">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="fc004-179">Seleccione el archivo zip de esa carpeta y elija Abrir.</span><span class="sxs-lookup"><span data-stu-id="fc004-179">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="fc004-180">La aplicación ahora se ha instalado localmente en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fc004-180">Your App is now sideloaded into Microsoft Teams.</span></span>

![aplicación de instalación de local](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="fc004-182">Vuelva al canal *General* y seleccione *+* agregar una nueva pestaña. Debería ver la pestaña en la lista de pestañas.</span><span class="sxs-lookup"><span data-stu-id="fc004-182">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![pestaña configurar](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="fc004-184">Elija la pestaña y siga las instrucciones para agregarla.</span><span class="sxs-lookup"><span data-stu-id="fc004-184">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="fc004-185">Observe que tiene un cuadro de diálogo de configuración personalizado para el que puede editar el origen.</span><span class="sxs-lookup"><span data-stu-id="fc004-185">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="fc004-186">Seleccione *Guardar* para agregar la pestaña al canal.</span><span class="sxs-lookup"><span data-stu-id="fc004-186">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="fc004-187">Una vez que haya terminado, la pestaña debe cargarse dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fc004-187">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![ejecutar pestaña en teams](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="fc004-189">**¡Congraciaciones! Ha creado e implementado su primera aplicación de Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="fc004-189">**Congrats! You built and deployed your first Microsoft Teams app**</span></span>
