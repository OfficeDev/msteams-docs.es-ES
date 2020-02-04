---
title: Crear una pestaña de canal y de grupo con ASP.NET Core MVC
author: laujan
description: Una guía de inicio rápido para crear una ficha de canal y de grupo personalizada con ASP.NET Core MVC.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 57c22d10414eb8ec93249584219488397f0b6b33
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675926"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="7f139-103">Crear una ficha de canal y de grupo personalizada con ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="7f139-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="7f139-104">En este tutorial rápido, crearemos una pestaña de grupo/canal personalizado con C# y ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="7f139-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="7f139-105">También usaremos [App Studio para Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) para finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="7f139-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="7f139-106">Obtener el código fuente</span><span class="sxs-lookup"><span data-stu-id="7f139-106">Get the source code</span></span>

<span data-ttu-id="7f139-107">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestañas.</span><span class="sxs-lookup"><span data-stu-id="7f139-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="7f139-108">Proporcionamos un sencillo proyecto de [pestaña de grupo de canal](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) para empezar.</span><span class="sxs-lookup"><span data-stu-id="7f139-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="7f139-109">Para recuperar el código fuente, puede descargar la carpeta ZIP y extraer los archivos o clonar el repositorio de muestra en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="7f139-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="7f139-110">Una vez que tenga el código fuente, abra Visual Studio y seleccione **abrir un proyecto o solución**.</span><span class="sxs-lookup"><span data-stu-id="7f139-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="7f139-111">Navegue hasta el directorio de la aplicación de la pestaña y Abra **ChannelGroupTabMVC. sln**.</span><span class="sxs-lookup"><span data-stu-id="7f139-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="7f139-112">Para compilar y ejecutar la aplicación, presione **F5** o elija **iniciar depuración** en el menú **depurar** .</span><span class="sxs-lookup"><span data-stu-id="7f139-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="7f139-113">En un explorador, vaya a las siguientes direcciones URL y compruebe que la aplicación se cargó correctamente:</span><span class="sxs-lookup"><span data-stu-id="7f139-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="7f139-114">Revisar el código fuente</span><span class="sxs-lookup"><span data-stu-id="7f139-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="7f139-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="7f139-115">Startup.cs</span></span>

<span data-ttu-id="7f139-116">Este proyecto se creó a partir de una plantilla vacía de la aplicación Web de ASP.NET Core 2,2 con la casilla de verificación *Advanced-configure for https* seleccionada en la instalación.</span><span class="sxs-lookup"><span data-stu-id="7f139-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="7f139-117">Los servicios MVC se registran mediante el método del marco `ConfigureServices()` de inserción de dependencias.</span><span class="sxs-lookup"><span data-stu-id="7f139-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="7f139-118">Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de `Configure()` archivos estáticos se agrega al método:</span><span class="sxs-lookup"><span data-stu-id="7f139-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="7f139-119">carpeta wwwroot</span><span class="sxs-lookup"><span data-stu-id="7f139-119">wwwroot folder</span></span>

<span data-ttu-id="7f139-120">En ASP.NET Core, la carpeta Web raíz es donde la aplicación busca archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="7f139-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="7f139-121">Carpeta AppManifest</span><span class="sxs-lookup"><span data-stu-id="7f139-121">AppManifest folder</span></span>

<span data-ttu-id="7f139-122">Esta carpeta contiene los siguientes archivos de paquete de la aplicación obligatorios:</span><span class="sxs-lookup"><span data-stu-id="7f139-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="7f139-123">Un **icono de color completo** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="7f139-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="7f139-124">Un **icono de contorno transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="7f139-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="7f139-125">Un archivo **manifest. JSON** que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f139-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="7f139-126">Estos archivos deben comprimirse en un paquete de la aplicación que se usará para cargar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="7f139-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="7f139-127">. csproj</span><span class="sxs-lookup"><span data-stu-id="7f139-127">.csproj</span></span>

<span data-ttu-id="7f139-128">En la ventana Explorador de soluciones de Visual Studio, haga clic con el botón secundario en el proyecto y seleccione **Editar archivo de proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7f139-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="7f139-129">En la parte inferior del archivo, verá el código que crea y actualiza la carpeta ZIP cuando se genera la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7f139-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="7f139-130">Brinda</span><span class="sxs-lookup"><span data-stu-id="7f139-130">Models</span></span>

<span data-ttu-id="7f139-131">*ChannelGroup.CS* presenta un objeto de mensaje y métodos a los que se llamará desde los controladores durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="7f139-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="7f139-132">Vistas</span><span class="sxs-lookup"><span data-stu-id="7f139-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="7f139-133">Inicio</span><span class="sxs-lookup"><span data-stu-id="7f139-133">Home</span></span>

<span data-ttu-id="7f139-134">ASP.NET Core trata los archivos denominados *index* como página principal o predeterminada del sitio.</span><span class="sxs-lookup"><span data-stu-id="7f139-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="7f139-135">Cuando la dirección URL del explorador apunta a la raíz del sitio, se mostrará **index. cshtml** como la Página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f139-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="7f139-136">Compartidos</span><span class="sxs-lookup"><span data-stu-id="7f139-136">Shared</span></span>

<span data-ttu-id="7f139-137">La vista parcial de marcas *_Layout. cshtml* contiene la estructura de página general y los elementos visuales compartidos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f139-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="7f139-138">También hará referencia a la biblioteca de Teams.</span><span class="sxs-lookup"><span data-stu-id="7f139-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="7f139-139">Controles</span><span class="sxs-lookup"><span data-stu-id="7f139-139">Controllers</span></span>

<span data-ttu-id="7f139-140">Los controladores usan la propiedad ViewBag para transferir valores de forma dinámica a las vistas.</span><span class="sxs-lookup"><span data-stu-id="7f139-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="7f139-141">Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7f139-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- <span data-ttu-id="7f139-142">Ngrok escuchará las solicitudes de Internet y las dirigirá a la aplicación cuando se ejecute en el puerto 44355.</span><span class="sxs-lookup"><span data-stu-id="7f139-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="7f139-143">Debe ser similar a `https://y8rCgT2b.ngrok.io/` donde *y8rCgT2b* se reemplaza por su dirección URL https alfanumérica de ngrok.</span><span class="sxs-lookup"><span data-stu-id="7f139-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="7f139-144">Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL, que lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="7f139-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="7f139-145">Actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="7f139-145">Update your application</span></span>

<span data-ttu-id="7f139-146">Dentro de **Tab. cshtml** , la aplicación presenta al usuario dos botones de opción para mostrar la ficha con un icono rojo o gris.</span><span class="sxs-lookup"><span data-stu-id="7f139-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="7f139-147">Al elegir el botón **seleccionar gris** o **seleccionar rojo** `saveGray()` , `saveRed()`se activa o, `settings.setValidityState(true)`respectivamente, establece y se habilita el botón **Guardar** en la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="7f139-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="7f139-148">Este código permite que los equipos sepan que ha satisfecho los requisitos de configuración y que la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="7f139-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="7f139-149">Al guardar, se establecen los `settings.setSettings` parámetros de.</span><span class="sxs-lookup"><span data-stu-id="7f139-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="7f139-150">Por último `saveEvent.notifySuccess()` , se llama a para indicar que la dirección URL del contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="7f139-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
