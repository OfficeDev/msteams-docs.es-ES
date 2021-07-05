---
title: 'Tutorial: crear la primera aplicación con el generador de Yeoman'
description: Obtén información sobre cómo empezar a crear Microsoft Teams aplicaciones con el generador de Yeoman.
keywords: introducción a node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: a3519da1495dc51a811f4e95bc4ada9b11aa8292
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254358"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="84efb-104">Crear la primera aplicación Microsoft Teams con el generador de Yeoman</span><span class="sxs-lookup"><span data-stu-id="84efb-104">Build your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="84efb-105">Este tutorial proviene del generador [de Yeoman para Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="84efb-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="84efb-106">En este tutorial, aprenderás a crear la primera aplicación Microsoft Teams con el generador de Yeoman Microsoft Teams de Yeoman.</span><span class="sxs-lookup"><span data-stu-id="84efb-106">In this tutorial, you will learn how to build your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="84efb-107">También le guiará a través del proceso de actualización de su Teams mediante el generador de Yeoman.</span><span class="sxs-lookup"><span data-stu-id="84efb-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="84efb-108">Antes de comenzar, debes tener una cuenta Teams que permita la [instalación local de la aplicación](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="84efb-108">Before you begin, you must have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![git generador de yeoman](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="84efb-110">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="84efb-110">Get Prerequisites</span></span>

<span data-ttu-id="84efb-111">Debe instalar lo siguiente en el equipo antes de empezar a usar el generador de Yeoman:</span><span class="sxs-lookup"><span data-stu-id="84efb-111">You need to install the following on your machine before starting to use the Yeoman generator:</span></span>

* <span data-ttu-id="84efb-112">Node.js</span><span class="sxs-lookup"><span data-stu-id="84efb-112">Node.js</span></span>

   <span data-ttu-id="84efb-113">Debe tener Node.js instalado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="84efb-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="84efb-114">Debe usar la versión [lts más reciente](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="84efb-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

* <span data-ttu-id="84efb-115">Un editor de código</span><span class="sxs-lookup"><span data-stu-id="84efb-115">A code editor</span></span>

   <span data-ttu-id="84efb-116">Necesita un editor de código.</span><span class="sxs-lookup"><span data-stu-id="84efb-116">You need a code editor.</span></span> <span data-ttu-id="84efb-117">La mayoría de esta documentación e imágenes hacen referencia al [uso de Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="84efb-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="84efb-118">Sin embargo, no dude en usar el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="84efb-118">However, feel free to use whatever text editor you prefer.</span></span>

* <span data-ttu-id="84efb-119">CLI de Yeoman y Gulp</span><span class="sxs-lookup"><span data-stu-id="84efb-119">Yeoman and Gulp CLI</span></span>

   <span data-ttu-id="84efb-120">Para scaffolding de proyectos con el generador, debe instalar la herramienta Yeoman y el administrador de tareas de la CLI de Gulp.</span><span class="sxs-lookup"><span data-stu-id="84efb-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

   <span data-ttu-id="84efb-121">Abra un símbolo del sistema y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="84efb-121">Open up a command prompt and type the following:</span></span>

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a><span data-ttu-id="84efb-122">Instalar el generador</span><span class="sxs-lookup"><span data-stu-id="84efb-122">Install the generator</span></span>

<span data-ttu-id="84efb-123">Instale el Teams Yeoman con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="84efb-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm init yo teams
```

<span data-ttu-id="84efb-124">Instale la versión preliminar del generador con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="84efb-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a><span data-ttu-id="84efb-125">Generar el proyecto</span><span class="sxs-lookup"><span data-stu-id="84efb-125">Generate your project</span></span>

<span data-ttu-id="84efb-126">Esta sección le guiará por los pasos para generar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="84efb-126">This section walks you through the steps to generate your project.</span></span>

<span data-ttu-id="84efb-127">**Para generar el proyecto**</span><span class="sxs-lookup"><span data-stu-id="84efb-127">**To generate your project**</span></span>

1. <span data-ttu-id="84efb-128">Abra un símbolo del sistema y cree un nuevo directorio donde desee crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="84efb-128">Open a command prompt and create a new directory where you want to create your project.</span></span>
1. <span data-ttu-id="84efb-129">Vaya al directorio y ejecute el comando `yo teams` .</span><span class="sxs-lookup"><span data-stu-id="84efb-129">Go to the directory, and run the command `yo teams`.</span></span> <span data-ttu-id="84efb-130">Se inicia el generador.</span><span class="sxs-lookup"><span data-stu-id="84efb-130">The generator starts.</span></span>
1. <span data-ttu-id="84efb-131">Responda al conjunto de preguntas que le pida el generador:</span><span class="sxs-lookup"><span data-stu-id="84efb-131">Respond to the set of questions prompted by the generator:</span></span>

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="84efb-133">Escriba un nombre para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="84efb-133">Enter a name for your project.</span></span> <span data-ttu-id="84efb-134">Puede dejarla tal como está presionando Entrar.</span><span class="sxs-lookup"><span data-stu-id="84efb-134">You can leave it as is by pressing Enter.</span></span>
   1. <span data-ttu-id="84efb-135">Escriba una ruta de acceso para el nuevo directorio si desea crear un directorio nuevo.</span><span class="sxs-lookup"><span data-stu-id="84efb-135">Enter a path for the new directory if you want to create a new directory.</span></span> <span data-ttu-id="84efb-136">Como ya está en el directorio que desea, simplemente presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="84efb-136">As you are already in the directory you want, just press Enter.</span></span>
   1. <span data-ttu-id="84efb-137">Escriba el título del proyecto.</span><span class="sxs-lookup"><span data-stu-id="84efb-137">Enter the title of your project.</span></span> <span data-ttu-id="84efb-138">Este título se usará en el manifiesto y la descripción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="84efb-138">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="84efb-139">Escriba un nombre de empresa que también se usará en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="84efb-139">Enter a company name which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="84efb-140">Escriba la versión del manifiesto que desea usar.</span><span class="sxs-lookup"><span data-stu-id="84efb-140">Enter the version of the manifest you want to use.</span></span> <span data-ttu-id="84efb-141">Para este tutorial, `v1.5` seleccione , que es el esquema disponible general actual.</span><span class="sxs-lookup"><span data-stu-id="84efb-141">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="84efb-142">Seleccione los elementos que desea agregar al proyecto.</span><span class="sxs-lookup"><span data-stu-id="84efb-142">Select the items you want to add to your project.</span></span> <span data-ttu-id="84efb-143">Puede seleccionar una sola o cualquier combinación de elementos.</span><span class="sxs-lookup"><span data-stu-id="84efb-143">You can select a single one or any combination of items.</span></span> <span data-ttu-id="84efb-144">Para estos tutoriales, solo tienes *que seleccionar una pestaña*:</span><span class="sxs-lookup"><span data-stu-id="84efb-144">For this tutorials, just select *a Tab*:</span></span>

    ![selección de elementos](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="84efb-146">Responda al siguiente conjunto de preguntas de seguimiento que aparecen en función de los elementos seleccionados en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="84efb-146">Respond to the next set of follow-up questions that appear based on the items you selected in Step 2.</span></span>
1. <span data-ttu-id="84efb-147">Escriba una dirección URL para la ubicación donde hospedará la solución.</span><span class="sxs-lookup"><span data-stu-id="84efb-147">Enter a URL for the location where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="84efb-148">La dirección URL puede ser cualquier dirección URL, pero de forma predeterminada el generador sugiere una dirección URL de sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="84efb-148">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="84efb-149">Confirme si desea incluir pruebas unitarias para la solución.</span><span class="sxs-lookup"><span data-stu-id="84efb-149">Confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="84efb-150">La respuesta predeterminada es **Sí**.</span><span class="sxs-lookup"><span data-stu-id="84efb-150">The default response is **Yes**.</span></span> <span data-ttu-id="84efb-151">Si opta por incluir pruebas unitarias, el proyecto generado tendrá un marco de pruebas unitarias y algunas pruebas unitarias predeterminadas para los distintos elementos que se van a scaffolding.</span><span class="sxs-lookup"><span data-stu-id="84efb-151">If you opt to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="84efb-152">Para este tutorial, elija no incluir un marco de prueba.</span><span class="sxs-lookup"><span data-stu-id="84efb-152">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="84efb-153">El generador tiene una gran cantidad de características avanzadas integradas de las que puede participar o no participar.</span><span class="sxs-lookup"><span data-stu-id="84efb-153">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="84efb-154">Para facilitar el inicio de sesión, también se le preguntará si desea usar Azure Application Ideas para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="84efb-154">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="84efb-155">Si selecciona **Sí**, tendrá que proporcionar una clave de Ideas Azure Application.</span><span class="sxs-lookup"><span data-stu-id="84efb-155">If you select **Yes**, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="84efb-156">En este tutorial no se puede usar application Ideas.</span><span class="sxs-lookup"><span data-stu-id="84efb-156">For this tutorial opt-out of using Application Insights.</span></span>

   <span data-ttu-id="84efb-157">El siguiente conjunto de preguntas se basará en los elementos seleccionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="84efb-157">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="84efb-158">Para una pestaña solo tienes que proporcionar un nombre y, opcionalmente, elegir si quieres poder usar esta aplicación como un elemento web SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="84efb-158">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="84efb-159">Después de proporcionar el nombre, el generador generará el proyecto e instalará todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="84efb-159">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="84efb-160">Esto llevará uno o dos minutos.</span><span class="sxs-lookup"><span data-stu-id="84efb-160">This will take a minute or two.</span></span>

## <a name="add-code-to-your-tab"></a><span data-ttu-id="84efb-161">Agregar código a la pestaña</span><span class="sxs-lookup"><span data-stu-id="84efb-161">Add code to your tab</span></span>

<span data-ttu-id="84efb-162">Una vez terminado el generador, puede abrir la solución en el editor de código favorito.</span><span class="sxs-lookup"><span data-stu-id="84efb-162">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="84efb-163">Tómese uno o dos minutos y familiarícese con cómo se organiza el código.</span><span class="sxs-lookup"><span data-stu-id="84efb-163">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="84efb-164">Para obtener más información, [vea Project structure.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)</span><span class="sxs-lookup"><span data-stu-id="84efb-164">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="84efb-165">La pestaña está en el `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` archivo.</span><span class="sxs-lookup"><span data-stu-id="84efb-165">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="84efb-166">Esta es la clase basada React TypeScript para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="84efb-166">This is the TypeScript React-based class for your tab.</span></span> 

1. <span data-ttu-id="84efb-167">Busque el `render()` método y agregue una línea de código dentro del control para que se vea `<PanelBody>` así:</span><span class="sxs-lookup"><span data-stu-id="84efb-167">Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. <span data-ttu-id="84efb-168">Guarde el archivo y vuelva al símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="84efb-168">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="84efb-169">Crear una aplicación</span><span class="sxs-lookup"><span data-stu-id="84efb-169">Build your app</span></span>

<span data-ttu-id="84efb-170">Ahora puede crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="84efb-170">You can now build your project.</span></span> <span data-ttu-id="84efb-171">Esto se realiza en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="84efb-171">This is done in two steps.</span></span>

1. <span data-ttu-id="84efb-172">Crea el Teams de manifiesto de la aplicación para la aplicación que has cargado en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="84efb-172">Create the Teams App manifest file for the app that you uploaded into Microsoft Teams.</span></span> <span data-ttu-id="84efb-173">Esto se realiza mediante la tarea Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="84efb-173">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="84efb-174">Esto validará el manifiesto y creará un archivo zip en el `./package` directorio.</span><span class="sxs-lookup"><span data-stu-id="84efb-174">This will validate the manifest and create a zip file in the `./package` directory.</span></span>
1. <span data-ttu-id="84efb-175">Ejecute el `gulp build` comando para compilar la solución.</span><span class="sxs-lookup"><span data-stu-id="84efb-175">Run the `gulp build` command to build the solution.</span></span> <span data-ttu-id="84efb-176">Esto transpilará la solución en la `./dist` carpeta.</span><span class="sxs-lookup"><span data-stu-id="84efb-176">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="84efb-177">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="84efb-177">Run your app</span></span>

<span data-ttu-id="84efb-178">Para ejecutar la aplicación, usa el `gulp serve` comando.</span><span class="sxs-lookup"><span data-stu-id="84efb-178">To run your app, use the `gulp serve` command.</span></span> <span data-ttu-id="84efb-179">Esto compilará e iniciará un servidor web local para que pruebe la aplicación.</span><span class="sxs-lookup"><span data-stu-id="84efb-179">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="84efb-180">El comando también reconstruirá la aplicación siempre que guarde un archivo en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="84efb-180">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="84efb-181">Ahora debe ir a y `http://localhost:3007/myFirstAppTab/` asegurarse de que la pestaña se está representando.</span><span class="sxs-lookup"><span data-stu-id="84efb-181">You should now be go to `http://localhost:3007/myFirstAppTab/` and ensure that your tab is rendering.</span></span> <span data-ttu-id="84efb-182">Sin embargo, aún no está Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="84efb-182">However, it is not in Microsoft Teams yet.</span></span> 

<span data-ttu-id="84efb-183">**Para representar la pestaña en Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="84efb-183">**To render your tab in Microsoft Teams**</span></span>

![ver el sitio en un explorador](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="84efb-185">Ejecute la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="84efb-185">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="84efb-186">Microsoft Teams no te permite tener la aplicación hospedada en localhost, por lo que debes publicarla en una dirección URL pública o usar un proxy como ngrok.</span><span class="sxs-lookup"><span data-stu-id="84efb-186">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span> <span data-ttu-id="84efb-187">Una buena noticia es que el proyecto scaffolded tiene este proyecto integrado.</span><span class="sxs-lookup"><span data-stu-id="84efb-187">Good news is that the scaffolded project has this built-in.</span></span> 

<span data-ttu-id="84efb-188">**Para ejecutar la aplicación en Teams**</span><span class="sxs-lookup"><span data-stu-id="84efb-188">**To run your app in Teams**</span></span>

1. <span data-ttu-id="84efb-189">Ejecutar `gulp ngrok-serve` en terminal.</span><span class="sxs-lookup"><span data-stu-id="84efb-189">Run `gulp ngrok-serve` in Terminal.</span></span> <span data-ttu-id="84efb-190">Cuando ejecute el servicio ngrok se iniciará en segundo plano, con una entrada DNS única y pública y también empaquetará el manifiesto con esa dirección URL única y, a continuación, hará exactamente lo mismo que `gulp ngrok-serve` `gulp serve` .</span><span class="sxs-lookup"><span data-stu-id="84efb-190">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>
1. <span data-ttu-id="84efb-191">Cree un nuevo Microsoft Teams equipo.</span><span class="sxs-lookup"><span data-stu-id="84efb-191">Create a new Microsoft Teams team.</span></span>
1. <span data-ttu-id="84efb-192">Seleccione el nombre del equipo > Teams Configuración > Aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="84efb-192">Select the Team name > Teams Settings > Apps.</span></span>
1. <span data-ttu-id="84efb-193">En la esquina inferior derecha, **selecciona Upload una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="84efb-193">From the lower right corner, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="84efb-194">Vaya a la `package` carpeta de la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="84efb-194">Go to the `package` folder under your project folder.</span></span> 
1. <span data-ttu-id="84efb-195">Seleccione el archivo zip de esa carpeta y seleccione Abrir.</span><span class="sxs-lookup"><span data-stu-id="84efb-195">Select the zip file in that folder and select open.</span></span> 
   <span data-ttu-id="84efb-196">La aplicación ahora se ha descargado localmente en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="84efb-196">Your App is now sideloaded into Microsoft Teams:</span></span>

   ![aplicación de sideloaded](~/assets/yeoman-images/teams-first-app-4.png)
1. <span data-ttu-id="84efb-198">Vuelva al canal **General** y seleccione **+** agregar una nueva pestaña. Debería ver la pestaña en la lista de pestañas: ![ configurar ficha](~/assets/yeoman-images/teams-first-app-5.png)</span><span class="sxs-lookup"><span data-stu-id="84efb-198">Go back to the **General** channel and select **+** to add a new Tab. You should see your tab in the list of tabs: ![configure tab](~/assets/yeoman-images/teams-first-app-5.png)</span></span>
1. <span data-ttu-id="84efb-199">Seleccione la pestaña y siga las instrucciones para agregarla.</span><span class="sxs-lookup"><span data-stu-id="84efb-199">Select your tab and follow the instructions to add it.</span></span> <span data-ttu-id="84efb-200">Tenga en cuenta que tiene un cuadro de diálogo de configuración personalizado para el que puede editar el origen.</span><span class="sxs-lookup"><span data-stu-id="84efb-200">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="84efb-201">Seleccione *Guardar* para agregar la pestaña al canal.</span><span class="sxs-lookup"><span data-stu-id="84efb-201">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="84efb-202">La pestaña se carga ahora dentro de Microsoft Teams!</span><span class="sxs-lookup"><span data-stu-id="84efb-202">Your tab is now loaded inside Microsoft Teams!</span></span>

   ![ejecutar pestaña en teams](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a><span data-ttu-id="84efb-204">Actualizar Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="84efb-204">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="84efb-205">También puede actualizar la versión Microsoft Teams actual a la versión más reciente mediante el generador de Yeoman Microsoft Teams de Yeoman.</span><span class="sxs-lookup"><span data-stu-id="84efb-205">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="84efb-206">**Para actualizar Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="84efb-206">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="84efb-207">Obtenga la versión actual de Teams con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="84efb-207">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="84efb-208">Use el siguiente comando para seleccionar y actualizar el generador:</span><span class="sxs-lookup"><span data-stu-id="84efb-208">Use the following command to select and update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="84efb-209">Use las teclas de flecha para **seleccionar Actualizar los generadores:**</span><span class="sxs-lookup"><span data-stu-id="84efb-209">Use the  arrow keys to select **Update your Generators**:</span></span>

   ![imagen de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="84efb-211">Seleccione el generador que desee de la lista de generadores:</span><span class="sxs-lookup"><span data-stu-id="84efb-211">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="84efb-212">Use la barra espaciador para seleccionar o borrar una versión Teams seleccionada de las opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="84efb-212">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![imagen de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="84efb-214">Se tardan unos segundos y minutos en completarse Teams instalación.</span><span class="sxs-lookup"><span data-stu-id="84efb-214">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="84efb-215">Una vez completada la instalación, use el siguiente comando para comprobar la versión instalada:</span><span class="sxs-lookup"><span data-stu-id="84efb-215">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   <span data-ttu-id="84efb-216">¡Felicidades!</span><span class="sxs-lookup"><span data-stu-id="84efb-216">Congrats!</span></span> <span data-ttu-id="84efb-217">Has creado e implementado la primera Microsoft Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="84efb-217">You built and deployed your first Microsoft Teams app.</span></span> <span data-ttu-id="84efb-218">También ha actualizado Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="84efb-218">You also upgraded Microsoft Teams.</span></span>

 ## <a name="see-also"></a><span data-ttu-id="84efb-219">Vea también</span><span class="sxs-lookup"><span data-stu-id="84efb-219">See also</span></span>

* [<span data-ttu-id="84efb-220">Introducción a tutoriales</span><span class="sxs-lookup"><span data-stu-id="84efb-220">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="84efb-221">Crear una aplicación de bots de conversación</span><span class="sxs-lookup"><span data-stu-id="84efb-221">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="84efb-222">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="84efb-222">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="84efb-223">Muestras de código</span><span class="sxs-lookup"><span data-stu-id="84efb-223">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)