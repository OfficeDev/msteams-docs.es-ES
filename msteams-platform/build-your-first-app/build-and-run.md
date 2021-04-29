---
title: 'Introducción: compilación y ejecución de la primera aplicación'
author: girliemac
description: Crea rápidamente una aplicación de Microsoft Teams que muestre un "¡Hola, mundo!" con Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068804"
---
# <a name="create-your-first-microsoft-teams-app"></a><span data-ttu-id="1d82a-104">Crear la primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1d82a-104">Create your first Microsoft Teams app</span></span>

<span data-ttu-id="1d82a-105">Esta guía de inicio rápido te enseña a crear y ejecutar la aplicación de Microsoft Teams que muestra "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="1d82a-105">This quickstart teaches you to build and run Microsoft Teams app that displays "Hello, World!"</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d82a-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1d82a-106">Prerequisites</span></span>

<span data-ttu-id="1d82a-107">Antes de comenzar, debe configurar el inquilino de desarrollo de [Teams](#set-up-your-teams-development-tenant) e [instalar las herramientas de desarrollo de Teams.](#install-your-development-tools)</span><span class="sxs-lookup"><span data-stu-id="1d82a-107">Before you begin, you need to [set up your Teams development tenant](#set-up-your-teams-development-tenant) and [install your Teams development tools](#install-your-development-tools).</span></span>

### <a name="set-up-your-teams-development-tenant"></a><span data-ttu-id="1d82a-108">Configurar el inquilino de desarrollo de Teams</span><span class="sxs-lookup"><span data-stu-id="1d82a-108">Set up your Teams development tenant</span></span>

<span data-ttu-id="1d82a-109">Un **inquilino** es como un contenedor para una organización.</span><span class="sxs-lookup"><span data-stu-id="1d82a-109">A **tenant** is like a container for an organization.</span></span> <span data-ttu-id="1d82a-110">En términos de Teams, un inquilino es donde los usuarios de esa organización chat, comparten archivos y ejecutan reuniones.</span><span class="sxs-lookup"><span data-stu-id="1d82a-110">In Teams terms, a tenant is where people from that org chat, share files, and run meetings.</span></span> <span data-ttu-id="1d82a-111">Como desarrollador, necesita un inquilino para realizar la instalación local y probar las aplicaciones de Teams que está creando.</span><span class="sxs-lookup"><span data-stu-id="1d82a-111">As a developer, you need a tenant to sideload and test the Teams apps that you are building.</span></span>  

# <a name="do-not-have-a-tenant"></a>[<span data-ttu-id="1d82a-112">No tener un inquilino</span><span class="sxs-lookup"><span data-stu-id="1d82a-112">Do not have a tenant</span></span>](#tab/do-not-have-a-tenant)

<span data-ttu-id="1d82a-113">Puedes obtener una cuenta de prueba gratuita de Teams, que incluye un inquilino que permite la instalación local de aplicaciones, uniéndose al programa para desarrolladores de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="1d82a-113">You can get a free Teams test account, which includes a tenant that allows app sideloading, by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="1d82a-114">El proceso de registro tarda aproximadamente dos minutos.</span><span class="sxs-lookup"><span data-stu-id="1d82a-114">The registration process takes approximately two minutes.</span></span>

<span data-ttu-id="1d82a-115">**Para obtener un inquilino**</span><span class="sxs-lookup"><span data-stu-id="1d82a-115">**To get a tenant**</span></span>

1. <span data-ttu-id="1d82a-116">Vaya al programa para desarrolladores de [Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="1d82a-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="1d82a-117">Selecciona **Unirse ahora** y sigue las instrucciones en pantalla.</span><span class="sxs-lookup"><span data-stu-id="1d82a-117">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="1d82a-118">En la pantalla de bienvenida, seleccione **Configurar suscripción E5**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-118">In the Welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="1d82a-119">Configura tu cuenta de desarrollador de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="1d82a-119">Set up your Microsoft 365 developer account.</span></span> 
   <span data-ttu-id="1d82a-120">Después de finalizar, aparecerá la siguiente pantalla:</span><span class="sxs-lookup"><span data-stu-id="1d82a-120">After you finish, the following screen appears:</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa para desarrolladores de Microsoft 365.":::

1. <span data-ttu-id="1d82a-122">Inicie sesión en Teams con su nueva cuenta.</span><span class="sxs-lookup"><span data-stu-id="1d82a-122">Sign in to Teams with your new account.</span></span>
1. <span data-ttu-id="1d82a-123">En el cliente de Teams, seleccione **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-123">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="1d82a-124">Comprueba que puedes ver la opción **Cargar una aplicación** personalizada.</span><span class="sxs-lookup"><span data-stu-id="1d82a-124">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="1d82a-125">Si lo haces, esto significa que puedes realizar la instalación local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1d82a-125">If you do, this means you can sideload apps.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde se puede cargar una aplicación personalizada en Teams.":::

# <a name="have-a-tenant"></a>[<span data-ttu-id="1d82a-127">Tener un inquilino</span><span class="sxs-lookup"><span data-stu-id="1d82a-127">Have a tenant</span></span>](#tab/have-a-tenant)

<span data-ttu-id="1d82a-128">Si ya tienes un inquilino, comprueba si puedes realizar la instalación local de aplicaciones en Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-128">If you already have a tenant, verify if you can sideload apps in Teams.</span></span>

<span data-ttu-id="1d82a-129">**Comprobar que puedes realizar la instalación local de las aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="1d82a-129">**Verify that you can sideload your apps**</span></span> 

1. <span data-ttu-id="1d82a-130">En el cliente de Teams, seleccione **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-130">In the Teams Client, select **Apps**.</span></span> 
1.  <span data-ttu-id="1d82a-131">Comprueba que puedes ver la opción **Cargar una aplicación** personalizada.</span><span class="sxs-lookup"><span data-stu-id="1d82a-131">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="1d82a-132">Si lo haces, esto significa que puedes realizar la instalación local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1d82a-132">If you do, this means you can sideload apps.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde se puede cargar una aplicación personalizada en Teams.":::

---

### <a name="install-your-development-tools"></a><span data-ttu-id="1d82a-134">Instalar las herramientas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="1d82a-134">Install your development tools</span></span>

<span data-ttu-id="1d82a-135">Para crear esta aplicación, usarás teams Toolkit for Visual Studio Code para empezar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="1d82a-135">To build this app, you'll use the Teams Toolkit for Visual Studio Code to quickly get started.</span></span> <span data-ttu-id="1d82a-136">También puedes crear aplicaciones de Teams con cualquiera de tus herramientas predefinidas.</span><span class="sxs-lookup"><span data-stu-id="1d82a-136">You can also build Teams apps with any ofyour preffered tools.</span></span> 

> [!NOTE]
> <span data-ttu-id="1d82a-137">Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1d82a-137">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="1d82a-138">Para depurar ciertos tipos de aplicaciones localmente, como un bot, aprenderás a usar ngrok para configurar un túnel seguro entre Teams y tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d82a-138">To debug certain types of apps locally, such as a bot, you'll learn how to use ngrok to set up a secure tunnel between Teams and your app.</span></span>
> 
> <span data-ttu-id="1d82a-139">Las aplicaciones de Production Teams se hospedan en la nube.</span><span class="sxs-lookup"><span data-stu-id="1d82a-139">Production Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="1d82a-140">**Para instalar herramientas de Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="1d82a-140">**To install Microsoft Teams tools**</span></span>

1. <span data-ttu-id="1d82a-141">Instale [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="1d82a-141">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="1d82a-142">Si planea crear un bot o una extensión de mensajería, instale [ngrok](https://ngrok.com/download) y exponga el localhost a [Internet con ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span><span class="sxs-lookup"><span data-stu-id="1d82a-142">If you plan to build a bot or messaging extension, install [ngrok](https://ngrok.com/download) and [expose your localhost to the Internet using ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="1d82a-143">Instale la versión más reciente [de Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="1d82a-143">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="1d82a-144">El kit de herramientas no admite versiones anteriores de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1d82a-144">The toolkit does not support earlier versions of Visual Studio Code.</span></span>

1. En la barra de actividad izquierda, seleccione **Extensiones** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: .
1. <span data-ttu-id="1d82a-146">En **Microsoft Teams Toolkit,** seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-146">In **Microsoft Teams Toolkit**, select **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración que muestra dónde en Visual Studio código puede instalar la extensión microsoft Teams Toolkit.":::

## <a name="1-create-your-app-project"></a><span data-ttu-id="1d82a-148">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="1d82a-148">1. Create your app project</span></span>

1. <span data-ttu-id="1d82a-149">Abra Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="1d82a-149">Open Visual Studio Code.</span></span>
1. Selecciona **Microsoft Teams Toolkit** Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Teams**.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Captura de pantalla que muestra cómo crear el proyecto de la aplicación con Visual Studio Kit de herramientas de Code Teams.":::
   
1. <span data-ttu-id="1d82a-152">Inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="1d82a-152">Sign in with your Microsoft 365 development account.</span></span> <span data-ttu-id="1d82a-153">Ya sea la que acaba de crear o la cuenta que ya tenía que permite la instalación local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1d82a-153">Either the one you just created or the account you already had that allows app sideloading.</span></span>
1. <span data-ttu-id="1d82a-154">En la **pantalla Seleccionar proyecto,** vaya a **Aplicación personal** y seleccione **JS** (JavaScript) > **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-154">On the **Select project** screen, go to **Personal app** and select **JS** (JavaScript) > **Next**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de la aplicación con Visual Studio Code Teams Toolkit.":::

1. <span data-ttu-id="1d82a-156">Escribe un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-156">Enter a name for your Teams app.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Captura de pantalla que muestra cómo agregar un nombre al proyecto de la aplicación con Visual Studio Kit de herramientas de Code Teams.":::

1. <span data-ttu-id="1d82a-158">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-158">Select **Finish**.</span></span> 
   <span data-ttu-id="1d82a-159">El proyecto ya está configurado.</span><span class="sxs-lookup"><span data-stu-id="1d82a-159">Your project is now configured.</span></span> 

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="1d82a-160">2. Comprender los componentes del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1d82a-160">2. Understand your app project components</span></span>

<span data-ttu-id="1d82a-161">Una vez que el kit de herramientas configura el proyecto de la aplicación, tienes los componentes para crear tu "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="1d82a-161">After the toolkit configures your app project, you have the components to build your "Hello, World!"</span></span> <span data-ttu-id="1d82a-162">Aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-162">Teams app.</span></span> <span data-ttu-id="1d82a-163">Los directorios y archivos del proyecto se encuentran en el Explorador Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="1d82a-163">The project's directories and files are located in the Visual Studio Code Explorer.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Captura de pantalla que muestra el scaffolding en el proyecto de la aplicación con Visual Studio Code Teams Toolkit.":::

<span data-ttu-id="1d82a-165">El kit de herramientas crea automáticamente scaffolding de aplicaciones en el directorio en función de `src` las capacidades que agregó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="1d82a-165">The toolkit automatically creates app scaffolding in the `src` directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="1d82a-166">Desde que creaste una pestaña durante la instalación, el archivo del directorio controla la inicialización `App.js` y el enrutamiento de la `src/components` aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d82a-166">Since you created a tab during setup, the `App.js` file in the `src/components` directory handles the initialization and routing of your app.</span></span> <span data-ttu-id="1d82a-167">El archivo también llama al SDK de cliente de JavaScript de Microsoft Teams para establecer la comunicación entre la aplicación y Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-167">The file also calls the Microsoft Teams JavaScript client SDK to establish communication between your app and Teams.</span></span> 

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="1d82a-168">3. Crear y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="1d82a-168">3. Build and run your app</span></span>

<span data-ttu-id="1d82a-169">Compila y ejecuta la aplicación localmente para ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="1d82a-169">Build and run your app locally to save time.</span></span> 

<span data-ttu-id="1d82a-170">**Para compilar y ejecutar la aplicación**</span><span class="sxs-lookup"><span data-stu-id="1d82a-170">**To build and run your app**</span></span>

1. <span data-ttu-id="1d82a-171">En Visual Studio, seleccione **Ver**  >  **terminal**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-171">In Visual Studio Code, select **View** > **Terminal**.</span></span>
1. <span data-ttu-id="1d82a-172">Ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="1d82a-172">Run `npm install`.</span></span>
1. <span data-ttu-id="1d82a-173">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="1d82a-173">Run `npm start`.</span></span>
  
  <span data-ttu-id="1d82a-174">Un **compilado correctamente.**</span><span class="sxs-lookup"><span data-stu-id="1d82a-174">A **Compiled successfully!**</span></span> <span data-ttu-id="1d82a-175">mensaje aparece en el terminal.</span><span class="sxs-lookup"><span data-stu-id="1d82a-175">message appears in the terminal.</span></span> <span data-ttu-id="1d82a-176">La aplicación se está ejecutando en el localhost en `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="1d82a-176">Your app is now running on your localhost at `https://localhost:3000`.</span></span> 

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="1d82a-177">4. Instalación local de la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="1d82a-177">4. Sideload your app in Teams</span></span>

<span data-ttu-id="1d82a-178">La instalación local es el proceso de instalación de una aplicación en Teams que no ha sido aprobada por el administrador o Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1d82a-178">Sideloading is the process of installing an app in Teams that hasn't been approved by your admin or Microsoft.</span></span> <span data-ttu-id="1d82a-179">La instalación local es común al probar y depurar aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-179">Sideloading is common when testing and debugging Teams apps.</span></span>

<span data-ttu-id="1d82a-180">De forma predeterminada, Teams no permite la instalación local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1d82a-180">By default, Teams doesn't allow app sideloading.</span></span> <span data-ttu-id="1d82a-181">Puedes cambiar esta configuración en el Centro de administración de Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-181">You can change this setting in the Teams admin center.</span></span>

<span data-ttu-id="1d82a-182">**Para habilitar la instalación local de aplicaciones en Teams**</span><span class="sxs-lookup"><span data-stu-id="1d82a-182">**To enable app sideloading in Teams**</span></span>

1. <span data-ttu-id="1d82a-183">Inicie sesión en el [Centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="1d82a-183">Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>  
1. <span data-ttu-id="1d82a-184">Seleccione **Mostrar todos los**  >  **equipos**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-184">Select **Show All** > **Teams**.</span></span> 

   ![imagen del menú del Centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > <span data-ttu-id="1d82a-186">La opción **Teams** puede tardar hasta 24 horas en aparecer.</span><span class="sxs-lookup"><span data-stu-id="1d82a-186">It can take up to 24 hours for the **Teams** option to appear.</span></span> 

1. <span data-ttu-id="1d82a-187">Ve a **Directivas de instalación de aplicaciones** de Teams  >    >  **Global** (configuración predeterminada para toda la organización).</span><span class="sxs-lookup"><span data-stu-id="1d82a-187">Go to **Teams apps** > **Setup policies** > **Global** (Org-wide default).</span></span>

   ![Activar la vista de instalación local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. <span data-ttu-id="1d82a-189">Activa la **alternancia cargar aplicaciones personalizadas.**</span><span class="sxs-lookup"><span data-stu-id="1d82a-189">Turn on the **upload custom apps** toggle.</span></span>

1. <span data-ttu-id="1d82a-190">Seleccione **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="1d82a-190">Select **Save** to save the changes.</span></span>

   <span data-ttu-id="1d82a-191">El inquilino de prueba ahora permite la instalación local de aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="1d82a-191">Your test tenant now allows custom app sideloading.</span></span>

   > [!Note]
   > <span data-ttu-id="1d82a-192">Comprueba si hay problemas antes de descargar localmente la aplicación con la característica de validación de App Studio, que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="1d82a-192">Check for issues before sideloading your app using the validation feature in App Studio, which is included in the toolkit.</span></span> <span data-ttu-id="1d82a-193">Se corrigen los errores para que la aplicación se desacargue correctamente.</span><span class="sxs-lookup"><span data-stu-id="1d82a-193">Fix the errors to successfully sideload the app.</span></span>


### <a name="sideload-your-app"></a><span data-ttu-id="1d82a-194">Instalación local de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1d82a-194">Sideload your app</span></span>

1. <span data-ttu-id="1d82a-195">En Visual Studio, abra el Kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-195">In Visual Studio Code, open the Teams Toolkit.</span></span>
1. <span data-ttu-id="1d82a-196">Vaya a **App Studio**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-196">Go to **App Studio**.</span></span>  
1. <span data-ttu-id="1d82a-197">Seleccione **Probar y distribuir**  >  **instalar**.</span><span class="sxs-lookup"><span data-stu-id="1d82a-197">Select **Test and Distribute** > **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Captura de pantalla que muestra cómo descargar localmente la aplicación en el cliente de Teams con Visual Studio Code Teams Toolkit.":::

<span data-ttu-id="1d82a-199">**Como alternativa**</span><span class="sxs-lookup"><span data-stu-id="1d82a-199">**Alternatively**</span></span>

1. <span data-ttu-id="1d82a-200">Seleccione la **tecla F5** para abrir la ventana del explorador que desea instalar.</span><span class="sxs-lookup"><span data-stu-id="1d82a-200">Select the **F5** key to open browser window to install.</span></span> <span data-ttu-id="1d82a-201">Esto omitirá el proceso de instalación en **App Studio** y lajerá Teams en el explorador.</span><span class="sxs-lookup"><span data-stu-id="1d82a-201">This will skip the installation process in the **App Studio** and lauch Teams in your browser.</span></span>
1. <span data-ttu-id="1d82a-202">En el cuadro de diálogo de instalación, selecciona **Agregar** para instalar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-202">In the installation dialog, select **Add** to install your app to Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="Captura de pantalla que muestra cómo descargar localmente la aplicación en el cliente de Teams.":::

   > [!Note]
   > <span data-ttu-id="1d82a-204">App Studio también está disponible como una aplicación independiente para el cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="1d82a-204">App Studio is also available as a stand-alone app for Teams client.</span></span>

### <a name="troubleshoot-sideloading-issues"></a><span data-ttu-id="1d82a-205">Solucionar problemas de instalación local</span><span class="sxs-lookup"><span data-stu-id="1d82a-205">Troubleshoot sideloading issues</span></span>

<span data-ttu-id="1d82a-206">**Error en la instalación**</span><span class="sxs-lookup"><span data-stu-id="1d82a-206">**Installation failed**</span></span>

<span data-ttu-id="1d82a-207">Si aparece el mensaje de error al instalar la aplicación, comprueba que la información de `Manifest parsing has failed` la aplicación se ha escrito correctamente.</span><span class="sxs-lookup"><span data-stu-id="1d82a-207">If the `Manifest parsing has failed` error message appears while installing your app, verify that the app information is correctly entered.</span></span>

<span data-ttu-id="1d82a-208">**Para comprobar la información de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="1d82a-208">**To verify the app information**</span></span>

* <span data-ttu-id="1d82a-209">En Teams Toolkit, ve a Detalles de **App Studio** App y comprueba que toda la información  >   necesaria se haya escrito correctamente.</span><span class="sxs-lookup"><span data-stu-id="1d82a-209">In the Teams Toolkit, go to **App Studio** > **App details** and verify that all the required information is correctly entered.</span></span>
*  <span data-ttu-id="1d82a-210">Si editó manualmente el archivo, compruebe que el JSON está bien definido en la herramienta Manifiesto de la aplicación `manifest.json` en App Studio. </span><span class="sxs-lookup"><span data-stu-id="1d82a-210">If you manually edited the `manifest.json` file, verify that the JSON is well-defined in the **App Manifest** tool in App Studio.</span></span>

<span data-ttu-id="1d82a-211">**Contenido de tabulación no mostrado**</span><span class="sxs-lookup"><span data-stu-id="1d82a-211">**Tab content not displayed**</span></span>

<span data-ttu-id="1d82a-212">Comprueba que la aplicación se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="1d82a-212">Verify that your app is running.</span></span> <span data-ttu-id="1d82a-213">Si no es así, vaya al terminal y ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="1d82a-213">If it isn't, go to the terminal and run `npm start`.</span></span>

## <a name="see-also"></a><span data-ttu-id="1d82a-214">Consulte también</span><span class="sxs-lookup"><span data-stu-id="1d82a-214">See also</span></span>

* [<span data-ttu-id="1d82a-215">Preparar el espacio empresarial de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="1d82a-215">Prepare your Microsoft 365 tenant</span></span>](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [<span data-ttu-id="1d82a-216">Elegir una configuración para probar y depurar la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1d82a-216">Choosing a setup to test and debug your Microsoft Teams app</span></span>](../concepts/build-and-test/debug.md)
* [<span data-ttu-id="1d82a-217">Creación de pestañas y otras experiencias hospedadas con el SDK de cliente de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1d82a-217">Building tabs and other hosted experiences with the Microsoft Teams JavaScript client SDK</span></span>](../tabs/how-to/using-teams-client-sdk.md)
* [<span data-ttu-id="1d82a-218">Preparar el envío de AppSource</span><span class="sxs-lookup"><span data-stu-id="1d82a-218">Prepare for AppSource submission</span></span>](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [<span data-ttu-id="1d82a-219">Desarrolle aplicaciones rápidamente con App Studio para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1d82a-219">Quickly develop apps with App Studio for Microsoft Teams</span></span>](../concepts/build-and-test/app-studio-overview.md)
* [<span data-ttu-id="1d82a-220">Crear una pestaña de canal</span><span class="sxs-lookup"><span data-stu-id="1d82a-220">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a><span data-ttu-id="1d82a-221">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1d82a-221">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d82a-222">Crear una pestaña personal para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1d82a-222">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
