---
title: Crear una pestaña personal con ASP. NET Core MVC
author: laujan
description: Una guía de inicio rápido para crear una ficha personal personalizada con ASP. NET Core MVC.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 3bdd23692eca5ff3f6fc3f82cdaa233d34d4c69f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675709"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a><span data-ttu-id="5f169-105">Cree una ficha personal personalizada con ASP.</span><span class="sxs-lookup"><span data-stu-id="5f169-105">Create a Custom Personal Tab with ASP.</span></span> <span data-ttu-id="5f169-106">NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="5f169-106">NET Core MVC</span></span>

<span data-ttu-id="5f169-107">En este tutorial rápido, vamos a crear una pestaña personal personalizada con C# y ASP.</span><span class="sxs-lookup"><span data-stu-id="5f169-107">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.</span></span> <span data-ttu-id="5f169-108">Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="5f169-108">Net Core MVC.</span></span> <span data-ttu-id="5f169-109">También usaremos [App Studio para Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) para finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="5f169-109">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="5f169-110">Obtener el código fuente</span><span class="sxs-lookup"><span data-stu-id="5f169-110">Get the source code</span></span>

<span data-ttu-id="5f169-111">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestañas.</span><span class="sxs-lookup"><span data-stu-id="5f169-111">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="5f169-112">Proporcionamos un proyecto sencillo para empezar.</span><span class="sxs-lookup"><span data-stu-id="5f169-112">We have provided a simple project to get you started.</span></span> <span data-ttu-id="5f169-113">Para recuperar el código fuente, puede descargar la carpeta ZIP y extraer los archivos o clonar el repositorio de muestra en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="5f169-113">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="5f169-114">Una vez que tenga el código fuente, abra Visual Studio y seleccione **abrir un proyecto o solución**.</span><span class="sxs-lookup"><span data-stu-id="5f169-114">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="5f169-115">Navegue hasta el directorio de la aplicación de la pestaña y Abra **PersonalTabMVC. sln**.</span><span class="sxs-lookup"><span data-stu-id="5f169-115">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="5f169-116">Para compilar y ejecutar la aplicación, presione **F5** o elija **iniciar depuración** en el menú **depurar** .</span><span class="sxs-lookup"><span data-stu-id="5f169-116">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="5f169-117">En un explorador, navegue a las siguientes direcciones URL para comprobar que la aplicación se cargó correctamente:</span><span class="sxs-lookup"><span data-stu-id="5f169-117">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="5f169-118">Revisar el código fuente</span><span class="sxs-lookup"><span data-stu-id="5f169-118">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="5f169-119">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="5f169-119">Startup.cs</span></span>

<span data-ttu-id="5f169-120">Este proyecto se creó a partir de un ASP.</span><span class="sxs-lookup"><span data-stu-id="5f169-120">This project was created from an ASP.</span></span> <span data-ttu-id="5f169-121">Plantilla de la aplicación web NET Core 2,2 con la casilla de verificación *avanzadas-configurar para https* seleccionada en la instalación.</span><span class="sxs-lookup"><span data-stu-id="5f169-121">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="5f169-122">Los servicios MVC se registran mediante el método del marco `ConfigureServices()` de inserción de dependencias.</span><span class="sxs-lookup"><span data-stu-id="5f169-122">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="5f169-123">Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de `Configure()` archivos estáticos se agrega al método:</span><span class="sxs-lookup"><span data-stu-id="5f169-123">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

``` csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

### <a name="wwwroot-folder"></a><span data-ttu-id="5f169-124">carpeta wwwroot</span><span class="sxs-lookup"><span data-stu-id="5f169-124">wwwroot folder</span></span>

<span data-ttu-id="5f169-125">En ASP.</span><span class="sxs-lookup"><span data-stu-id="5f169-125">In ASP.</span></span> <span data-ttu-id="5f169-126">NET Core, la carpeta raíz Web es donde la aplicación busca archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="5f169-126">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="5f169-127">Carpeta AppManifest</span><span class="sxs-lookup"><span data-stu-id="5f169-127">AppManifest folder</span></span>

<span data-ttu-id="5f169-128">Esta carpeta contiene los siguientes archivos de paquete de la aplicación obligatorios:</span><span class="sxs-lookup"><span data-stu-id="5f169-128">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="5f169-129">Un **icono de color completo** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="5f169-129">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="5f169-130">Un **icono de contorno transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="5f169-130">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="5f169-131">Un archivo **manifest. JSON** que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f169-131">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="5f169-132">Estos archivos deben comprimirse en un paquete de la aplicación que se usará para cargar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="5f169-132">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="5f169-133">Microsoft Teams cargará `contentUrl` el especificado en el manifiesto, lo incrustará en un iframe y lo representará en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="5f169-133">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="5f169-134">. csproj</span><span class="sxs-lookup"><span data-stu-id="5f169-134">.csproj</span></span>

<span data-ttu-id="5f169-135">En la ventana Explorador de soluciones de Visual Studio, haga clic con el botón secundario en el proyecto y seleccione **Editar archivo de proyecto**.</span><span class="sxs-lookup"><span data-stu-id="5f169-135">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="5f169-136">En la parte inferior del archivo, verá el código que crea y actualiza la carpeta ZIP cuando se genera la aplicación:</span><span class="sxs-lookup"><span data-stu-id="5f169-136">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

``` xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

### <a name="models"></a><span data-ttu-id="5f169-137">Brinda</span><span class="sxs-lookup"><span data-stu-id="5f169-137">Models</span></span>

<span data-ttu-id="5f169-138">*PersonalTab.CS* presenta un objeto de mensaje y los métodos que se llamarán desde *PersonalTabController* cuando un usuario selecciona un botón en la vista de *PersonalTab* .</span><span class="sxs-lookup"><span data-stu-id="5f169-138">*PersonalTab.cs* presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the *PersonalTab* View.</span></span>

### <a name="views"></a><span data-ttu-id="5f169-139">Vistas</span><span class="sxs-lookup"><span data-stu-id="5f169-139">Views</span></span>

#### <a name="home"></a><span data-ttu-id="5f169-140">Inicio</span><span class="sxs-lookup"><span data-stu-id="5f169-140">Home</span></span>

<span data-ttu-id="5f169-141">Páginas.</span><span class="sxs-lookup"><span data-stu-id="5f169-141">ASP.</span></span> <span data-ttu-id="5f169-142">NET Core trata los archivos denominados *index* como página principal o predeterminada del sitio.</span><span class="sxs-lookup"><span data-stu-id="5f169-142">NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="5f169-143">Cuando la dirección URL del explorador apunta a la raíz del sitio, se mostrará *index. cshtml* como la Página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f169-143">When your browser URL points to the root of the site, *Index.cshtml* will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="5f169-144">Compartidos</span><span class="sxs-lookup"><span data-stu-id="5f169-144">Shared</span></span>

<span data-ttu-id="5f169-145">La vista parcial de marcas *_Layout. cshtml* contiene la estructura de página general y los elementos visuales compartidos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f169-145">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="5f169-146">También hará referencia a la biblioteca de Teams.</span><span class="sxs-lookup"><span data-stu-id="5f169-146">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="5f169-147">Controles</span><span class="sxs-lookup"><span data-stu-id="5f169-147">Controllers</span></span>

<span data-ttu-id="5f169-148">Los controladores usan la propiedad ViewBag para transferir valores de forma dinámica a las vistas.</span><span class="sxs-lookup"><span data-stu-id="5f169-148">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="5f169-149">Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5f169-149">Open a command prompt in the root of your project directory and run the following command:</span></span>

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* <span data-ttu-id="5f169-150">Ngrok escuchará las solicitudes de Internet y las dirigirá a la aplicación cuando se ejecute en el puerto 44325.</span><span class="sxs-lookup"><span data-stu-id="5f169-150">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="5f169-151">Debe ser similar a `https://y8rPrT2b.ngrok.io/` donde *y8rPrT2b* se reemplaza por su dirección URL https alfanumérica de ngrok.</span><span class="sxs-lookup"><span data-stu-id="5f169-151">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="5f169-152">Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL, que lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="5f169-152">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="5f169-153">Compruebe que *ngrok* se está ejecutando y que funciona correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL https ngrok que se proporcionó en la ventana del símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="5f169-153">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> <span data-ttu-id="5f169-154">[!</span><span class="sxs-lookup"><span data-stu-id="5f169-154">[!</span></span> <span data-ttu-id="5f169-155">SUGERENCIA] debe tener la aplicación en Visual Studio y ngrok en ejecución para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5f169-155">TIP] You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="5f169-156">Si necesita detener la ejecución de la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**.</span><span class="sxs-lookup"><span data-stu-id="5f169-156">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="5f169-157">Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f169-157">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="5f169-158">Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar todos los sitios que usen esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="5f169-158">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="5f169-159">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="5f169-159">Run your application</span></span>

* <span data-ttu-id="5f169-160">En Visual Studio, presione **F5** o elija **iniciar depuración** en el menú **depurar** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f169-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
