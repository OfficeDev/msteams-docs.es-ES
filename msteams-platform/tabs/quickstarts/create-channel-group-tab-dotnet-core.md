---
title: Crear una ficha de canal y de grupo con ASP.NET Core
author: laujan
description: Una guía de inicio rápido para crear una ficha de canal y de grupo personalizada con ASP.NET Core.
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 6a21d40d4d474fd587b43760d818082b4ab2502d
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818923"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a><span data-ttu-id="ccfcd-103">Crear una ficha de canal y de grupo personalizada con ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ccfcd-103">Create a Custom Channel and Group Tab with ASP.NET Core</span></span>

<span data-ttu-id="ccfcd-104">En este tutorial rápido, vamos a crear una pestaña de canal o de grupo personalizada con C# y página de Razor ASP.Net Core.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="ccfcd-105">También usaremos [App Studio para Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) para finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="ccfcd-106">Obtener el código fuente</span><span class="sxs-lookup"><span data-stu-id="ccfcd-106">Get the source code</span></span>

<span data-ttu-id="ccfcd-107">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestañas.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="ccfcd-108">Proporcionamos un proyecto sencillo para empezar.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="ccfcd-109">Para recuperar el código fuente, puede descargar la carpeta ZIP y extraer los archivos o clonar el repositorio de muestra en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="ccfcd-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="ccfcd-110">Una vez que tenga el código fuente, abra Visual Studio y seleccione **abrir un proyecto o solución**.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="ccfcd-111">Navegue hasta el directorio de la aplicación de la pestaña y Abra **ChannelGroupTab. sln**.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-111">Navigate to the tab application directory and open **ChannelGroupTab.sln**.</span></span>

<span data-ttu-id="ccfcd-112">Para compilar y ejecutar la aplicación, presione **F5** o elija **iniciar depuración** en el menú **depurar** .</span><span class="sxs-lookup"><span data-stu-id="ccfcd-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="ccfcd-113">En un explorador, navegue a las direcciones URL que aparecen a continuación y compruebe que la aplicación se cargó correctamente:</span><span class="sxs-lookup"><span data-stu-id="ccfcd-113">In a browser navigate to the URLs below and verify the application loaded properly:</span></span>

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="ccfcd-114">Revisar el código fuente</span><span class="sxs-lookup"><span data-stu-id="ccfcd-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="ccfcd-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ccfcd-115">Startup.cs</span></span>

<span data-ttu-id="ccfcd-116">Este proyecto se creó a partir de una plantilla vacía de la aplicación Web de ASP.NET Core 2,2 con la casilla de verificación *Advanced-configure for https* seleccionada en la instalación.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="ccfcd-117">Los servicios MVC se registran mediante el método del marco de inserción de dependencias `ConfigureServices()` .</span><span class="sxs-lookup"><span data-stu-id="ccfcd-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="ccfcd-118">Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método:</span><span class="sxs-lookup"><span data-stu-id="ccfcd-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="ccfcd-119">carpeta wwwroot</span><span class="sxs-lookup"><span data-stu-id="ccfcd-119">wwwroot folder</span></span>

<span data-ttu-id="ccfcd-120">En ASP.NET Core, la carpeta Web raíz es donde la aplicación busca archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="ccfcd-121">Index. cshtml</span><span class="sxs-lookup"><span data-stu-id="ccfcd-121">Index.cshtml</span></span>

<span data-ttu-id="ccfcd-122">ASP.NET Core trata los archivos denominados *index* como página principal o predeterminada del sitio.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="ccfcd-123">Cuando la dirección URL del explorador apunta a la raíz del sitio, se mostrará **index. cshtml** como la Página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="tabcs"></a><span data-ttu-id="ccfcd-124">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="ccfcd-124">Tab.cs</span></span>

<span data-ttu-id="ccfcd-125">Este archivo de C# contiene un método al que se llamará desde **Tab. cshtml** durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-125">This C# file contains a method that will be called from **Tab.cshtml** during configuration.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="ccfcd-126">Carpeta AppManifest</span><span class="sxs-lookup"><span data-stu-id="ccfcd-126">AppManifest folder</span></span>

<span data-ttu-id="ccfcd-127">Esta carpeta contiene los siguientes archivos de paquete de la aplicación obligatorios:</span><span class="sxs-lookup"><span data-stu-id="ccfcd-127">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="ccfcd-128">Un **icono de color completo** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-128">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="ccfcd-129">Un **icono de contorno transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-129">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="ccfcd-130">Un **manifest.jsen** archivo que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-130">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ccfcd-131">Estos archivos deben comprimirse en un paquete de la aplicación que se usará para cargar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-131">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="ccfcd-132">Cuando un usuario elige agregar o actualizar la pestaña, Microsoft Teams cargará los `configurationUrl` especificados en el manifiesto, los incrustará en un iframe y los representará en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-132">When a user chooses to add or update your tab, Microsoft Teams will load the `configurationUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="ccfcd-133">. csproj</span><span class="sxs-lookup"><span data-stu-id="ccfcd-133">.csproj</span></span>

<span data-ttu-id="ccfcd-134">En la ventana Explorador de soluciones de Visual Studio, haga clic con el botón secundario en el proyecto y seleccione **Editar archivo de proyecto**.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-134">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="ccfcd-135">En la parte inferior del archivo, verá el código que crea y actualiza la carpeta ZIP cuando se genera la aplicación:</span><span class="sxs-lookup"><span data-stu-id="ccfcd-135">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="ccfcd-136">Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ccfcd-136">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- <span data-ttu-id="ccfcd-137">Ngrok escuchará las solicitudes de Internet y las dirigirá a la aplicación cuando se ejecute en el puerto 44355.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-137">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="ccfcd-138">Debe ser similar `https://y8rCgT2b.ngrok.io/` a donde *y8rCgT2b* se reemplaza por su dirección URL https alfanumérica de ngrok.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-138">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="ccfcd-139">Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL, que lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-139">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="ccfcd-140">Actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="ccfcd-140">Update your application</span></span>

<span data-ttu-id="ccfcd-141">Dentro de *Tab. cshtml* , la aplicación presenta al usuario dos botones de opción para mostrar la ficha con un icono rojo o gris.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-141">Within *Tab.cshtml* the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="ccfcd-142">Al elegir el botón **seleccionar gris** o **seleccionar rojo** , se activa `saveGray()` o `saveRed()` , respectivamente, establece `settings.setValidityState(true)` y se habilita el botón **Guardar** en la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-142">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="ccfcd-143">Este código permite que los equipos sepan que ha satisfecho los requisitos de configuración y que la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-143">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="ccfcd-144">Al guardar, se establecen los parámetros de `settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="ccfcd-144">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="ccfcd-145">Por último, `saveEvent.notifySuccess()` se llama a para indicar que la dirección URL del contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-145">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

