---
title: Crear una pestaña personal con ASP. NET Core MVC
author: laujan
description: Guía de inicio rápido para crear una pestaña personal personalizada con ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 01418adb32335660bb20f74ecfaa0e7e27230c93
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566634"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="c999a-105">Crear una pestaña personal personalizada con ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="c999a-105">Create a Custom Personal Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="c999a-106">En esta guía de inicio rápido, crearemos una pestaña personal personalizada con C# y ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="c999a-106">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="c999a-107">También usaremos [App Studio](~/concepts/build-and-test/app-studio-overview.md) para Microsoft Teams finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="c999a-107">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="c999a-108">Obtener el código fuente</span><span class="sxs-lookup"><span data-stu-id="c999a-108">Get the source code</span></span>

<span data-ttu-id="c999a-109">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña.</span><span class="sxs-lookup"><span data-stu-id="c999a-109">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="c999a-110">Hemos proporcionado un proyecto sencillo para empezar.</span><span class="sxs-lookup"><span data-stu-id="c999a-110">We have provided a simple project to get you started.</span></span> <span data-ttu-id="c999a-111">Para recuperar el código fuente, puede descargar la carpeta zip y extraer los archivos o clonar el repositorio de ejemplo en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="c999a-111">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="c999a-112">Una vez que tenga el código fuente, abra Visual Studio y seleccione **Abrir un proyecto o solución**.</span><span class="sxs-lookup"><span data-stu-id="c999a-112">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="c999a-113">Vaya al directorio de la aplicación de tabulación y abra **PersonalTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="c999a-113">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="c999a-114">Para compilar y ejecutar la aplicación, presione **F5** o **elija Iniciar depuración** en el **menú** Depurar.</span><span class="sxs-lookup"><span data-stu-id="c999a-114">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="c999a-115">En un explorador, vaya a las direcciones URL siguientes para comprobar que la aplicación se cargó correctamente:</span><span class="sxs-lookup"><span data-stu-id="c999a-115">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="c999a-116">Revisar el código fuente</span><span class="sxs-lookup"><span data-stu-id="c999a-116">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="c999a-117">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="c999a-117">Startup.cs</span></span>

<span data-ttu-id="c999a-118">Este proyecto se creó a partir de una ASP.</span><span class="sxs-lookup"><span data-stu-id="c999a-118">This project was created from an ASP.</span></span> <span data-ttu-id="c999a-119">Aplicación web de NET Core 2.2 plantilla vacía con la casilla Avanzadas *- Configurar* para HTTPS activada en el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="c999a-119">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="c999a-120">Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias.</span><span class="sxs-lookup"><span data-stu-id="c999a-120">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="c999a-121">Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método:</span><span class="sxs-lookup"><span data-stu-id="c999a-121">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="c999a-122">carpeta wwwroot</span><span class="sxs-lookup"><span data-stu-id="c999a-122">wwwroot folder</span></span>

<span data-ttu-id="c999a-123">En ASP.</span><span class="sxs-lookup"><span data-stu-id="c999a-123">In ASP.</span></span> <span data-ttu-id="c999a-124">NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="c999a-124">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="c999a-125">Carpeta AppManifest</span><span class="sxs-lookup"><span data-stu-id="c999a-125">AppManifest folder</span></span>

<span data-ttu-id="c999a-126">Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:</span><span class="sxs-lookup"><span data-stu-id="c999a-126">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="c999a-127">Un **icono de color completo** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="c999a-127">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="c999a-128">Un **icono de esquema transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="c999a-128">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="c999a-129">Un **manifest.jsen** el archivo que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c999a-129">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="c999a-130">Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña a Teams.</span><span class="sxs-lookup"><span data-stu-id="c999a-130">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="c999a-131">Microsoft Teams cargará el especificado en el manifiesto, lo incrustará en un IFrame y lo `contentUrl` representará en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="c999a-131">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="c999a-132">.csproj</span><span class="sxs-lookup"><span data-stu-id="c999a-132">.csproj</span></span>

<span data-ttu-id="c999a-133">En la ventana Visual Studio Explorador de soluciones haga clic con el botón secundario en el proyecto y seleccione **Editar Project archivo**.</span><span class="sxs-lookup"><span data-stu-id="c999a-133">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="c999a-134">En la parte inferior del archivo verá el código que crea y actualiza la carpeta zip cuando se compila la aplicación:</span><span class="sxs-lookup"><span data-stu-id="c999a-134">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="c999a-135">Modelos</span><span class="sxs-lookup"><span data-stu-id="c999a-135">Models</span></span>

<span data-ttu-id="c999a-136">**PersonalTab.cs** presenta un objeto Message y métodos a los que se llamará desde *PersonalTabController* cuando un usuario seleccione un botón en la **vista PersonalTab.**</span><span class="sxs-lookup"><span data-stu-id="c999a-136">**PersonalTab.cs** presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the **PersonalTab** View.</span></span>

### <a name="views"></a><span data-ttu-id="c999a-137">Views</span><span class="sxs-lookup"><span data-stu-id="c999a-137">Views</span></span>

#### <a name="home"></a><span data-ttu-id="c999a-138">Inicio</span><span class="sxs-lookup"><span data-stu-id="c999a-138">Home</span></span>

<span data-ttu-id="c999a-139">ASP.</span><span class="sxs-lookup"><span data-stu-id="c999a-139">ASP.</span></span> <span data-ttu-id="c999a-140">NET Core trata los archivos denominados **Index** como la página predeterminada o principal del sitio.</span><span class="sxs-lookup"><span data-stu-id="c999a-140">NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="c999a-141">Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se mostrará como la página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c999a-141">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="c999a-142">Compartido</span><span class="sxs-lookup"><span data-stu-id="c999a-142">Shared</span></span>

<span data-ttu-id="c999a-143">El marcado de vista *parcial _Layout.cshtml* contiene la estructura de página general de la aplicación y los elementos visuales compartidos.</span><span class="sxs-lookup"><span data-stu-id="c999a-143">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="c999a-144">También hará referencia a la Teams biblioteca.</span><span class="sxs-lookup"><span data-stu-id="c999a-144">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="c999a-145">Controladores</span><span class="sxs-lookup"><span data-stu-id="c999a-145">Controllers</span></span>

<span data-ttu-id="c999a-146">Los controladores usan la propiedad ViewBag para transferir valores dinámicamente a las vistas.</span><span class="sxs-lookup"><span data-stu-id="c999a-146">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="c999a-147">Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c999a-147">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* <span data-ttu-id="c999a-148">Ngrok escuchará las solicitudes de Internet y las enrutará a la aplicación cuando se ejecute en el puerto 44325.</span><span class="sxs-lookup"><span data-stu-id="c999a-148">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="c999a-149">Debe ser similar `https://y8rPrT2b.ngrok.io/` a *donde y8rPrT2b* se reemplaza por la dirección URL HTTPS alfanumérico de ngrok.</span><span class="sxs-lookup"><span data-stu-id="c999a-149">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="c999a-150">Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y de tomar nota de la dirección URL, la necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="c999a-150">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="c999a-151">Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="c999a-151">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="c999a-152">Debe tener la aplicación en ejecución Visual Studio y ngrok para completar esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="c999a-152">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="c999a-153">Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**.</span><span class="sxs-lookup"><span data-stu-id="c999a-153">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="c999a-154">Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c999a-154">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="c999a-155">Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar cada lugar que use esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="c999a-155">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="c999a-156">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="c999a-156">Run your application</span></span>

* <span data-ttu-id="c999a-157">En Visual Studio presione **F5** o **elija Iniciar depuración** en el menú **Depurar de la** aplicación.</span><span class="sxs-lookup"><span data-stu-id="c999a-157">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="c999a-158">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="c999a-158">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c999a-159">Cree una pestaña de canal y grupo personalizada con Node.js y el generador de Yeoman para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c999a-159">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
