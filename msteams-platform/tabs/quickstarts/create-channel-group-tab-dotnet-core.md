---
title: Crear una pestaña Canal y Grupo con ASP.NET Core
author: laujan
description: Guía de inicio rápido para crear un canal personalizado y una pestaña de grupo con ASP.NET Core.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: f748335b621e9bc93272aaeb8d7e12ecc3ebbee0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52580457"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnetcore"></a><span data-ttu-id="e39ba-103">Crear un canal personalizado y una pestaña de grupo con ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="e39ba-103">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>

<span data-ttu-id="e39ba-104">En esta guía de inicio rápido, crearemos una pestaña de canal o grupo personalizada con C# y ASP.Net Core Razor.</span><span class="sxs-lookup"><span data-stu-id="e39ba-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="e39ba-105">También usaremos [App Studio](~/concepts/build-and-test/app-studio-overview.md) para Microsoft Teams finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="e39ba-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="e39ba-106">Obtener el código fuente</span><span class="sxs-lookup"><span data-stu-id="e39ba-106">Get the source code</span></span>

<span data-ttu-id="e39ba-107">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña.</span><span class="sxs-lookup"><span data-stu-id="e39ba-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="e39ba-108">Hemos proporcionado un proyecto sencillo para empezar.</span><span class="sxs-lookup"><span data-stu-id="e39ba-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="e39ba-109">Para recuperar el código fuente, puede descargar la carpeta zip y extraer los archivos o clonar el repositorio de ejemplo en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="e39ba-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="e39ba-110">Una vez que tenga el código fuente, abra Visual Studio y seleccione **Abrir un proyecto o solución**.</span><span class="sxs-lookup"><span data-stu-id="e39ba-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="e39ba-111">Vaya al directorio de la aplicación de tabulación y abra **ChannelGroupTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="e39ba-111">Navigate to the tab application directory and open **ChannelGroupTab.sln**.</span></span>

<span data-ttu-id="e39ba-112">Para compilar y ejecutar la aplicación, presione **F5** o **elija Iniciar depuración** en el **menú** Depurar.</span><span class="sxs-lookup"><span data-stu-id="e39ba-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="e39ba-113">En un explorador, vaya a las direcciones URL siguientes y compruebe que la aplicación se cargó correctamente:</span><span class="sxs-lookup"><span data-stu-id="e39ba-113">In a browser navigate to the URLs below and verify the application loaded properly:</span></span>

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="e39ba-114">Revisar el código fuente</span><span class="sxs-lookup"><span data-stu-id="e39ba-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="e39ba-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="e39ba-115">Startup.cs</span></span>

<span data-ttu-id="e39ba-116">Este proyecto se creó a partir de una plantilla vacía ASP.NET Core aplicación web 2.2 con la casilla Avanzadas *- Configurar* para HTTPS activada en el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="e39ba-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="e39ba-117">Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias.</span><span class="sxs-lookup"><span data-stu-id="e39ba-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="e39ba-118">Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método:</span><span class="sxs-lookup"><span data-stu-id="e39ba-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="e39ba-119">carpeta wwwroot</span><span class="sxs-lookup"><span data-stu-id="e39ba-119">wwwroot folder</span></span>

<span data-ttu-id="e39ba-120">En ASP.NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="e39ba-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="e39ba-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="e39ba-121">Index.cshtml</span></span>

<span data-ttu-id="e39ba-122">ASP.NET Core trata los archivos denominados *Index* como la página predeterminada/principal del sitio.</span><span class="sxs-lookup"><span data-stu-id="e39ba-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="e39ba-123">Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se mostrará como la página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e39ba-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="tabcs"></a><span data-ttu-id="e39ba-124">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="e39ba-124">Tab.cs</span></span>

<span data-ttu-id="e39ba-125">Este C# contiene un método al que se llamará desde **Tab.cshtml durante** la configuración.</span><span class="sxs-lookup"><span data-stu-id="e39ba-125">This C# file contains a method that will be called from **Tab.cshtml** during configuration.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="e39ba-126">Carpeta AppManifest</span><span class="sxs-lookup"><span data-stu-id="e39ba-126">AppManifest folder</span></span>

<span data-ttu-id="e39ba-127">Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:</span><span class="sxs-lookup"><span data-stu-id="e39ba-127">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="e39ba-128">Un **icono de color completo** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="e39ba-128">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="e39ba-129">Un **icono de esquema transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="e39ba-129">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="e39ba-130">Un **manifest.jsen** el archivo que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e39ba-130">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="e39ba-131">Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña a Teams.</span><span class="sxs-lookup"><span data-stu-id="e39ba-131">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="e39ba-132">Cuando un usuario elige agregar o actualizar la pestaña, Microsoft Teams cargará el especificado en el manifiesto, lo incrustará en un IFrame y lo representará en `configurationUrl` la pestaña.</span><span class="sxs-lookup"><span data-stu-id="e39ba-132">When a user chooses to add or update your tab, Microsoft Teams will load the `configurationUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="e39ba-133">.csproj</span><span class="sxs-lookup"><span data-stu-id="e39ba-133">.csproj</span></span>

<span data-ttu-id="e39ba-134">En la ventana Visual Studio Explorador de soluciones haga clic con el botón secundario en el proyecto y seleccione **Editar Project archivo**.</span><span class="sxs-lookup"><span data-stu-id="e39ba-134">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="e39ba-135">En la parte inferior del archivo verá el código que crea y actualiza la carpeta zip cuando se compila la aplicación:</span><span class="sxs-lookup"><span data-stu-id="e39ba-135">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="e39ba-136">Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e39ba-136">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- <span data-ttu-id="e39ba-137">Ngrok escuchará las solicitudes de Internet y las enrutará a la aplicación cuando se ejecute en el puerto 44355.</span><span class="sxs-lookup"><span data-stu-id="e39ba-137">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="e39ba-138">Debe ser similar `https://y8rCgT2b.ngrok.io/` a *donde y8rCgT2b* se reemplaza por la dirección URL HTTPS alfanumérico de ngrok.</span><span class="sxs-lookup"><span data-stu-id="e39ba-138">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="e39ba-139">Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y de tomar nota de la dirección URL; la necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="e39ba-139">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="e39ba-140">Actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="e39ba-140">Update your application</span></span>

<span data-ttu-id="e39ba-141">En *Tab.cshtml,* la aplicación presenta al usuario dos botones de opción para mostrar la pestaña con un icono rojo o gris.</span><span class="sxs-lookup"><span data-stu-id="e39ba-141">Within *Tab.cshtml* the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="e39ba-142">Al elegir el **botón Seleccionar gris** o **Seleccionar** rojo, se activa o, respectivamente, se establece y habilita el botón Guardar en la página `saveGray()` de `saveRed()` `settings.setValidityState(true)` configuración. </span><span class="sxs-lookup"><span data-stu-id="e39ba-142">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="e39ba-143">Este código permite Teams que ha cumplido los requisitos de configuración y la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="e39ba-143">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="e39ba-144">Al guardar, se establecen los `settings.setSettings` parámetros de.</span><span class="sxs-lookup"><span data-stu-id="e39ba-144">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="e39ba-145">Por último, `saveEvent.notifySuccess()` se llama para indicar que la dirección URL de contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="e39ba-145">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

## <a name="next-step"></a><span data-ttu-id="e39ba-146">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="e39ba-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e39ba-147">Crear un canal personalizado y una pestaña de grupo con ASP.NETCore MVC</span><span class="sxs-lookup"><span data-stu-id="e39ba-147">Create a Custom Channel and Group Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core-mvc.md)