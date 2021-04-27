---
title: 'Tutorial: crear la primera aplicación con el generador de Yeoman'
description: Obtén información sobre cómo empezar a crear aplicaciones de Microsoft Teams con el generador de Yeoman.
keywords: introducción a node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 9efbe6f6e6502120f1afdadb9b538182f1406c56
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018435"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="0cd4c-104">Crear la primera aplicación de Microsoft Teams con el generador de Yeoman</span><span class="sxs-lookup"><span data-stu-id="0cd4c-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="0cd4c-105">Este tutorial proviene del generador [de Yeoman para la wiki de Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="0cd4c-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="0cd4c-106">En este tutorial, le mostraremos cómo crear su primera aplicación de Microsoft Teams con el generador Yeoman de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-106">In this tutorial, we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="0cd4c-107">También le guiará a través del proceso de actualización de Teams con el generador de Yeoman.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="0cd4c-108">El requisito previo para empezar con este tutorial es que tienes una cuenta de Teams que permite la [instalación local de aplicaciones.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="0cd4c-108">The prerequisite to start with this tutorial is that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![git generador de yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="0cd4c-110">Configurar y preparar el equipo</span><span class="sxs-lookup"><span data-stu-id="0cd4c-110">Setup and prepare your machine</span></span>

<span data-ttu-id="0cd4c-111">Debe instalar lo siguiente en el equipo antes de empezar a usar el generador de Yeoman.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-111">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="0cd4c-112">Instalar Node.js</span><span class="sxs-lookup"><span data-stu-id="0cd4c-112">Install Node.js</span></span>

<span data-ttu-id="0cd4c-113">Debe tener Node.js instalado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="0cd4c-114">Debe usar la versión [lts más reciente](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="0cd4c-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="0cd4c-115">Instalar un editor de código</span><span class="sxs-lookup"><span data-stu-id="0cd4c-115">Install a code editor</span></span>

<span data-ttu-id="0cd4c-116">Necesita un editor de código.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-116">You need a code editor.</span></span> <span data-ttu-id="0cd4c-117">La mayoría de esta documentación e imágenes hacen referencia al [uso de Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="0cd4c-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="0cd4c-118">Sin embargo, no dude en usar el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-118">However, feel free to use whatever text editor you prefer.</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="0cd4c-119">Instalar Yeoman y Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="0cd4c-119">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="0cd4c-120">Para scaffolding de proyectos con el generador, debe instalar la herramienta Yeoman y el administrador de tareas de la CLI de Gulp.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

<span data-ttu-id="0cd4c-121">Abra un símbolo del sistema y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0cd4c-121">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="0cd4c-122">Instalar el generador</span><span class="sxs-lookup"><span data-stu-id="0cd4c-122">Install the generator</span></span>

<span data-ttu-id="0cd4c-123">Instale el generador de Teams Yeoman con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0cd4c-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="0cd4c-124">Instale la versión preliminar del generador con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0cd4c-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="0cd4c-125">Generar el proyecto</span><span class="sxs-lookup"><span data-stu-id="0cd4c-125">Generate your project</span></span>

<span data-ttu-id="0cd4c-126">En esta sección se le guían los pasos para generar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-126">This section walks you through the steps for generating your project.</span></span>

<span data-ttu-id="0cd4c-127">**Para generar el proyecto**</span><span class="sxs-lookup"><span data-stu-id="0cd4c-127">**To generate your project**</span></span>

1. <span data-ttu-id="0cd4c-128">Abra un símbolo del sistema y cree un nuevo directorio donde desee crear el proyecto y, en ese directorio, ejecute el comando `yo teams` .</span><span class="sxs-lookup"><span data-stu-id="0cd4c-128">Open up a command prompt and create a new directory where you want to create your project, and in that directory run the command `yo teams`.</span></span> <span data-ttu-id="0cd4c-129">Se inicia el generador.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-129">The generator starts.</span></span>
1. <span data-ttu-id="0cd4c-130">Responda al conjunto de preguntas que le pida el generador.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-130">Respond to the set of questions prompted by the generator.</span></span>

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="0cd4c-132">La primera pregunta es sobre el nombre del proyecto, puede dejarlo tal como está presionando entrar.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-132">The first question is about your project name, you can leave it as is by pressing enter.</span></span>
   1. <span data-ttu-id="0cd4c-133">La siguiente pregunta le pregunta si desea crear un directorio nuevo o usar el actual.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-133">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="0cd4c-134">Como ya está en el directorio que desea, simplemente presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-134">As you are already in the directory you want, just press enter.</span></span>
   1. <span data-ttu-id="0cd4c-135">En la siguiente pregunta, escriba el título del proyecto.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-135">In the next question, type the title of your project.</span></span> <span data-ttu-id="0cd4c-136">Este título se usará en el manifiesto y la descripción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-136">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="0cd4c-137">A continuación, se le pedirá un nombre de empresa, que también se usará en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-137">Next, you will be asked for a company name, which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="0cd4c-138">La quinta pregunta le pregunta qué versión del manifiesto desea usar.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-138">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="0cd4c-139">Para este tutorial, `v1.5` seleccione , que es el esquema disponible general actual.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-139">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="0cd4c-140">A continuación, el generador le preguntará qué elementos desea agregar al proyecto.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-140">Next, the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="0cd4c-141">Puede seleccionar una sola o cualquier combinación de elementos.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-141">You can select a single one or any combination of items.</span></span> <span data-ttu-id="0cd4c-142">Para estos tutoriales, solo tiene que *seleccionar una pestaña*.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-142">For this tutorials, just select *a Tab*.</span></span>

    ![selección de elementos](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="0cd4c-144">Responda al siguiente conjunto de preguntas de seguimiento que aparecen en función de los elementos seleccionados en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-144">Respond to the next set of follow-up questions that appear based on the items you selected in step 2.</span></span>
1. <span data-ttu-id="0cd4c-145">Escriba una dirección URL de dónde hospedará la solución.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-145">Enter a URL of where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="0cd4c-146">La dirección URL puede ser cualquier dirección URL, pero de forma predeterminada el generador sugiere una dirección URL de sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-146">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="0cd4c-147">En la siguiente pregunta, confirme si desea incluir pruebas unitarias para la solución.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-147">In the next question, confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="0cd4c-148">La respuesta predeterminada es *sí*.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-148">The default response is *yes*.</span></span> <span data-ttu-id="0cd4c-149">Si decide incluir pruebas unitarias, el proyecto generado tendrá un marco de pruebas unitarias y algunas pruebas unitarias predeterminadas para los distintos elementos que se van a scaffolding.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-149">If you choose to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="0cd4c-150">Para este tutorial, elija no incluir un marco de prueba.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-150">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="0cd4c-151">El generador tiene una gran cantidad de características avanzadas integradas de las que puede participar o no participar.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-151">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="0cd4c-152">Para facilitar el inicio de sesión, también se le preguntará si desea usar Azure Application Insights para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-152">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="0cd4c-153">Si elige *Sí,* deberá proporcionar una clave de Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-153">If you choose *Yes*, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="0cd4c-154">En este tutorial no se puede usar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-154">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="0cd4c-155">El siguiente conjunto de preguntas se basará en los elementos seleccionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-155">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="0cd4c-156">Para una pestaña, solo necesita proporcionar un nombre y, opcionalmente, elegir si desea poder usar esta aplicación como un elemento web de SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-156">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="0cd4c-157">Después de proporcionar el nombre, el generador generará el proyecto e instalará todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-157">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="0cd4c-158">Esto llevará uno o dos minutos.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-158">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="0cd4c-159">Agregar código a la pestaña</span><span class="sxs-lookup"><span data-stu-id="0cd4c-159">Add some code to your tab</span></span>

<span data-ttu-id="0cd4c-160">Una vez terminado el generador, puede abrir la solución en el editor de código favorito.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-160">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="0cd4c-161">Tómese uno o dos minutos y familiarícese con cómo se organiza el código.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-161">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="0cd4c-162">Para obtener más información, consulte [documentación sobre la estructura del](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) proyecto.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-162">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="0cd4c-163">La pestaña está en el `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` archivo.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-163">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="0cd4c-164">Esta es la clase basada en TypeScript React para la pestaña. Busque el `render()` método y agregue una línea de código dentro del control para que se vea `<PanelBody>` así:</span><span class="sxs-lookup"><span data-stu-id="0cd4c-164">This is the TypeScript React-based class for your tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="0cd4c-165">Guarde el archivo y vuelva al símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-165">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="0cd4c-166">Crear una aplicación</span><span class="sxs-lookup"><span data-stu-id="0cd4c-166">Build your app</span></span>

<span data-ttu-id="0cd4c-167">Ahora puede crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-167">You can now build your project.</span></span> <span data-ttu-id="0cd4c-168">Esto se realiza en dos pasos (o un paso, vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="0cd4c-168">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="0cd4c-169">En primer lugar, debe crear el archivo de manifiesto de Teams App, que se carga o se carga localmente en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-169">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="0cd4c-170">Esto se realiza mediante la tarea Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="0cd4c-170">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="0cd4c-171">Esto validará el manifiesto y creará un archivo zip en el `./package` directorio.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-171">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="0cd4c-172">Para crear la solución, use el `gulp build` comando.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-172">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="0cd4c-173">Esto transpilará la solución en la `./dist` carpeta.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-173">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="0cd4c-174">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="0cd4c-174">Run your app</span></span>

<span data-ttu-id="0cd4c-175">Para ejecutar la aplicación, usas el `gulp serve` comando.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-175">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="0cd4c-176">Esto compilará e iniciará un servidor web local para que pruebe la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-176">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="0cd4c-177">El comando también reconstruirá la aplicación siempre que guarde un archivo en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-177">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="0cd4c-178">Ahora debería poder buscar para asegurarse de que `http://localhost:3007/myFirstAppTab/` la pestaña se está representando.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-178">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="0cd4c-179">Sin embargo, todavía no está en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-179">However, not in Microsoft Teams yet.</span></span>

![ver el sitio en un explorador](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="0cd4c-181">Ejecutar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0cd4c-181">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="0cd4c-182">Microsoft Teams no te permite hospedar la aplicación en localhost, por lo que debes publicarla en una dirección URL pública o usar un proxy como ngrok.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-182">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="0cd4c-183">Una buena noticia es que el proyecto scaffolded tiene este proyecto integrado.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-183">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="0cd4c-184">Cuando ejecute el servicio ngrok se iniciará en segundo plano, con una entrada DNS única y pública y también empaquetará el manifiesto con esa dirección URL única y, a continuación, hará exactamente lo mismo que `gulp ngrok-serve` `gulp serve` .</span><span class="sxs-lookup"><span data-stu-id="0cd4c-184">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="0cd4c-185">Después de ejecutar , cree un nuevo equipo de Microsoft Teams y cuando se cree haga clic en el nombre del equipo, vaya a la configuración de equipos y, `gulp ngrok-serve` a continuación, seleccione *Aplicaciones*.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-185">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="0cd4c-186">En la esquina inferior derecha debería ver un vínculo Cargar una aplicación personalizada, selecciónelo y, a continuación, vaya *a* la carpeta del proyecto y a la subcarpeta denominada `package` .</span><span class="sxs-lookup"><span data-stu-id="0cd4c-186">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="0cd4c-187">Seleccione el archivo zip en esa carpeta y elija abrir.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-187">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="0cd4c-188">La aplicación ahora se ha descargado localmente en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-188">Your App is now sideloaded into Microsoft Teams.</span></span>

![aplicación de sideloaded](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="0cd4c-190">Vuelva al canal *General* y seleccione *+* agregar una nueva pestaña. Debería ver la pestaña en la lista de pestañas.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-190">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![ficha configurar](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="0cd4c-192">Elija la pestaña y siga las instrucciones para agregarla.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-192">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="0cd4c-193">Tenga en cuenta que tiene un cuadro de diálogo de configuración personalizado para el que puede editar el origen.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-193">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="0cd4c-194">Seleccione *Guardar* para agregar la pestaña al canal.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-194">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="0cd4c-195">Una vez hecho esto, la pestaña debe cargarse dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-195">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![ejecutar pestaña en teams](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a><span data-ttu-id="0cd4c-197">Actualizar Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0cd4c-197">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="0cd4c-198">También puede actualizar la versión actual de Microsoft Teams a la versión más reciente con el generador Yeoman de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-198">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="0cd4c-199">**Para actualizar Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="0cd4c-199">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="0cd4c-200">Obtenga la versión actual de Teams con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0cd4c-200">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="0cd4c-201">Use el siguiente comando para seleccionar actualizar el generador:</span><span class="sxs-lookup"><span data-stu-id="0cd4c-201">Use the following command to select update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="0cd4c-202">Use las teclas de flecha para elegir **Actualizar los generadores**.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-202">Use the  arrow keys to choose **Update your Generators**.</span></span>

   ![imagen de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="0cd4c-204">Seleccione el generador que desee de la lista de generadores.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-204">Select the generator you want from the list of generators.</span></span>
   > [!NOTE]
   > <span data-ttu-id="0cd4c-205">Use la barra espaciador para seleccionar o borrar una versión de Teams seleccionada de las opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-205">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![imagen de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="0cd4c-207">La instalación de Teams tarda unos segundos y minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="0cd4c-207">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="0cd4c-208">Una vez completada la instalación, use el siguiente comando para comprobar la versión instalada:</span><span class="sxs-lookup"><span data-stu-id="0cd4c-208">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   
<span data-ttu-id="0cd4c-209">**¡Felicidades! Has creado e implementado la primera aplicación de Microsoft Teams. También ha actualizado Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="0cd4c-209">**Congrats! You built and deployed your first Microsoft Teams app. You also upgraded Microsoft Teams.**</span></span>
