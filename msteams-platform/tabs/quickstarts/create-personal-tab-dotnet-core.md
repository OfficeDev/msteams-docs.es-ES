---
title: Crea una pestaña personal con ASP.NET Core
author: laujan
description: Una guía de inicio rápido para crear una pestaña personal personalizada con ASP.NET Core.
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 41aa916f4c69d50e48254d0f4934109429dab83c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566897"
---
# <a name="create-a-personal-tab-using-aspnetcore"></a><span data-ttu-id="7ef20-103">Cree una pestaña personal con ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="7ef20-103">Create a personal tab using ASP.NETCore</span></span>

<span data-ttu-id="7ef20-104">En esta guía de inicio rápido, crearemos una pestaña personal personalizada con las páginas C# y ASP.Net Core Razor.</span><span class="sxs-lookup"><span data-stu-id="7ef20-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="7ef20-105">También usaremos [App Studio para Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) para finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="7ef20-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="7ef20-106">Obtener el código fuente</span><span class="sxs-lookup"><span data-stu-id="7ef20-106">Get the source code</span></span>

<span data-ttu-id="7ef20-107">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña.</span><span class="sxs-lookup"><span data-stu-id="7ef20-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="7ef20-108">Hemos proporcionado un proyecto sencillo para que comiences.</span><span class="sxs-lookup"><span data-stu-id="7ef20-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="7ef20-109">Para recuperar el código fuente, puede descargar la carpeta zip y extraer los archivos o clonar el repositorio de ejemplo en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="7ef20-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="7ef20-110">Una vez que tenga el código fuente, abra Visual Studio y seleccione **Abrir un proyecto o solución.**</span><span class="sxs-lookup"><span data-stu-id="7ef20-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="7ef20-111">Vaya al directorio de la aplicación de pestañas y abra **PersonalTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="7ef20-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="7ef20-112">Para compilar y ejecutar la aplicación, presione **F5** o elija **Iniciar depuración** en el menú **Depurar.**</span><span class="sxs-lookup"><span data-stu-id="7ef20-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="7ef20-113">En un explorador, vaya a las direcciones URL a continuación para comprobar la aplicación cargada correctamente:</span><span class="sxs-lookup"><span data-stu-id="7ef20-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="7ef20-114">Revise el código fuente</span><span class="sxs-lookup"><span data-stu-id="7ef20-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="7ef20-115">Inicio.cs</span><span class="sxs-lookup"><span data-stu-id="7ef20-115">Startup.cs</span></span>

<span data-ttu-id="7ef20-116">Este proyecto se creó a partir de una plantilla vacía de aplicación web ASP.NET Core 2.2 con la casilla **Avanzadas - Configurar para HTTPS** activada en la configuración.</span><span class="sxs-lookup"><span data-stu-id="7ef20-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="7ef20-117">Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias.</span><span class="sxs-lookup"><span data-stu-id="7ef20-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="7ef20-118">Además, la plantilla vacía no habilita la publicación de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método:</span><span class="sxs-lookup"><span data-stu-id="7ef20-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

```csharp
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

### <a name="wwwroot-folder"></a><span data-ttu-id="7ef20-119">carpeta wwwroot</span><span class="sxs-lookup"><span data-stu-id="7ef20-119">wwwroot folder</span></span>

<span data-ttu-id="7ef20-120">En ASP.NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="7ef20-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="7ef20-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="7ef20-121">Index.cshtml</span></span>

<span data-ttu-id="7ef20-122">ASP.NET Core trata los archivos denominados *Índice* como la página predeterminada/página de inicio del sitio.</span><span class="sxs-lookup"><span data-stu-id="7ef20-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="7ef20-123">Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se mostrará como la página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7ef20-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="7ef20-124">Carpeta AppManifest</span><span class="sxs-lookup"><span data-stu-id="7ef20-124">AppManifest folder</span></span>

<span data-ttu-id="7ef20-125">Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:</span><span class="sxs-lookup"><span data-stu-id="7ef20-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="7ef20-126">Un **icono a todo color** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="7ef20-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="7ef20-127">Un **icono de contorno transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="7ef20-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="7ef20-128">Un **manifest.jsen el** archivo que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7ef20-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="7ef20-129">Estos archivos deben estar comprimidos en un paquete de aplicación para su uso en la carga de la pestaña a Teams.</span><span class="sxs-lookup"><span data-stu-id="7ef20-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="7ef20-130">Microsoft Teams cargará lo especificado en el `contentUrl` manifiesto, lo incrustará en un <iframe \> y lo representará en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7ef20-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="7ef20-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="7ef20-131">.csproj</span></span>

<span data-ttu-id="7ef20-132">En la ventana Explorador de soluciones Visual Studio, haga clic con el botón derecho en el proyecto y seleccione **Editar Project archivo**.</span><span class="sxs-lookup"><span data-stu-id="7ef20-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="7ef20-133">En la parte inferior del archivo verá el código que crea y actualiza la carpeta zip cuando se compila la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7ef20-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

```xml
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

[!INCLUDE  [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="7ef20-134">Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7ef20-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- <span data-ttu-id="7ef20-135">Ngrok escuchará las solicitudes de Internet y las enrutará a su aplicación cuando se ejecute en el puerto 44325.</span><span class="sxs-lookup"><span data-stu-id="7ef20-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="7ef20-136">Debe ser similar `https://y8rPrT2b.ngrok.io/` a donde *y8rPrT2b* es reemplazado por su URL HTTPS alfanumérica ngrok.</span><span class="sxs-lookup"><span data-stu-id="7ef20-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="7ef20-137">Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y de tomar nota de la dirección URL: la necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="7ef20-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="7ef20-138">Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador e yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7ef20-138">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="7ef20-139">Debe tener la aplicación en Visual Studio y ngrok ejecutándose para completar esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="7ef20-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="7ef20-140">Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución.**</span><span class="sxs-lookup"><span data-stu-id="7ef20-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="7ef20-141">Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ef20-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="7ef20-142">Si tienes que reiniciar el servicio ngrok devolverá una nueva dirección URL y tendrás que actualizar cada lugar que use esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="7ef20-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="7ef20-143">Ejecute la aplicación</span><span class="sxs-lookup"><span data-stu-id="7ef20-143">Run your application</span></span>

- <span data-ttu-id="7ef20-144">En Visual Studio presione **F5** o elija **Iniciar depuración** en el menú **Depurar de** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7ef20-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="7ef20-145">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="7ef20-145">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ef20-146">Cree una pestaña personal personalizada con ASP.NETCore MVC</span><span class="sxs-lookup"><span data-stu-id="7ef20-146">Create a Custom Personal Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
