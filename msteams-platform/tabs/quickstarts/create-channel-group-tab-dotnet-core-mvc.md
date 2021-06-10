---
title: Crear una pestaña Canal y Grupo con ASP.NET Core MVC
author: laujan
description: Guía de inicio rápido para crear un canal personalizado y una pestaña de grupo con ASP.NET Core MVC
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: bac406f22e9273b6cca5d1d5f576b03d295b875f
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630358"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="72b91-103">Crear un canal personalizado y una pestaña de grupo con ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="72b91-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="72b91-104">En esta guía de inicio rápido, crearemos una pestaña de canal o grupo personalizada con C# y ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="72b91-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="72b91-105">También usaremos [App Studio](~/concepts/build-and-test/app-studio-overview.md) para Microsoft Teams finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="72b91-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="72b91-106">Obtener el código fuente</span><span class="sxs-lookup"><span data-stu-id="72b91-106">Get the source code</span></span>

<span data-ttu-id="72b91-107">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña.</span><span class="sxs-lookup"><span data-stu-id="72b91-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="72b91-108">Hemos proporcionado un proyecto de pestaña de [grupo de canales](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) sencillo para empezar.</span><span class="sxs-lookup"><span data-stu-id="72b91-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="72b91-109">Para recuperar el código fuente, puede descargar la carpeta zip y extraer los archivos o clonar el repositorio de ejemplo en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="72b91-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="72b91-110">Una vez que tenga el código fuente, abra Visual Studio y seleccione **Abrir un proyecto o solución**.</span><span class="sxs-lookup"><span data-stu-id="72b91-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="72b91-111">Vaya al directorio de la aplicación de tabulación y abra **ChannelGroupTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="72b91-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="72b91-112">Para compilar y ejecutar la aplicación, presione **F5** o **elija Iniciar depuración** en el **menú** Depurar.</span><span class="sxs-lookup"><span data-stu-id="72b91-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="72b91-113">En un explorador, vaya a las direcciones URL siguientes y compruebe que la aplicación se cargó correctamente:</span><span class="sxs-lookup"><span data-stu-id="72b91-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="72b91-114">Revisar el código fuente</span><span class="sxs-lookup"><span data-stu-id="72b91-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="72b91-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="72b91-115">Startup.cs</span></span>

<span data-ttu-id="72b91-116">Este proyecto se creó a partir de una plantilla vacía ASP.NET Core aplicación web 2.2 con la casilla Avanzadas *- Configurar* para HTTPS activada en el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="72b91-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="72b91-117">Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias.</span><span class="sxs-lookup"><span data-stu-id="72b91-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="72b91-118">Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método:</span><span class="sxs-lookup"><span data-stu-id="72b91-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="72b91-119">carpeta wwwroot</span><span class="sxs-lookup"><span data-stu-id="72b91-119">wwwroot folder</span></span>

<span data-ttu-id="72b91-120">En ASP.NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="72b91-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="72b91-121">Carpeta AppManifest</span><span class="sxs-lookup"><span data-stu-id="72b91-121">AppManifest folder</span></span>

<span data-ttu-id="72b91-122">Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:</span><span class="sxs-lookup"><span data-stu-id="72b91-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="72b91-123">Un **icono de color completo** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="72b91-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="72b91-124">Un **icono de esquema transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="72b91-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="72b91-125">Un **manifest.jsen** el archivo que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="72b91-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="72b91-126">Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña a Teams.</span><span class="sxs-lookup"><span data-stu-id="72b91-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="72b91-127">.csproj</span><span class="sxs-lookup"><span data-stu-id="72b91-127">.csproj</span></span>

<span data-ttu-id="72b91-128">En la ventana Visual Studio Explorador de soluciones haga clic con el botón secundario en el proyecto y seleccione **Editar Project archivo**.</span><span class="sxs-lookup"><span data-stu-id="72b91-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="72b91-129">En la parte inferior del archivo verá el código que crea y actualiza la carpeta zip cuando se compila la aplicación:</span><span class="sxs-lookup"><span data-stu-id="72b91-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="72b91-130">Modelos</span><span class="sxs-lookup"><span data-stu-id="72b91-130">Models</span></span>

<span data-ttu-id="72b91-131">*ChannelGroup.cs* presenta un objeto Message y métodos a los que se llamará desde los controladores durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="72b91-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="72b91-132">Views</span><span class="sxs-lookup"><span data-stu-id="72b91-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="72b91-133">Inicio</span><span class="sxs-lookup"><span data-stu-id="72b91-133">Home</span></span>

<span data-ttu-id="72b91-134">ASP.NET Core trata los archivos denominados *Index* como la página predeterminada/principal del sitio.</span><span class="sxs-lookup"><span data-stu-id="72b91-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="72b91-135">Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se mostrará como la página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="72b91-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="72b91-136">Compartido</span><span class="sxs-lookup"><span data-stu-id="72b91-136">Shared</span></span>

<span data-ttu-id="72b91-137">El marcado de vista *parcial _Layout.cshtml* contiene la estructura de página general de la aplicación y los elementos visuales compartidos.</span><span class="sxs-lookup"><span data-stu-id="72b91-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="72b91-138">También hará referencia a la Teams biblioteca.</span><span class="sxs-lookup"><span data-stu-id="72b91-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="72b91-139">Controladores</span><span class="sxs-lookup"><span data-stu-id="72b91-139">Controllers</span></span>

<span data-ttu-id="72b91-140">Los controladores usan la propiedad ViewBag para transferir valores dinámicamente a las vistas.</span><span class="sxs-lookup"><span data-stu-id="72b91-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="72b91-141">Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="72b91-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:443560 -host-header="localhost:44360"
    ```

- <span data-ttu-id="72b91-142">Ngrok escuchará las solicitudes de Internet y las enrutará a la aplicación cuando se ejecute en el puerto 44355.</span><span class="sxs-lookup"><span data-stu-id="72b91-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="72b91-143">Debe ser similar `https://y8rCgT2b.ngrok.io/` a *donde y8rCgT2b* se reemplaza por la dirección URL HTTPS alfanumérico de ngrok.</span><span class="sxs-lookup"><span data-stu-id="72b91-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="72b91-144">Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y de tomar nota de la dirección URL; la necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="72b91-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="72b91-145">Actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="72b91-145">Update your application</span></span>

<span data-ttu-id="72b91-146">En **Tab.cshtml,** la aplicación presenta al usuario dos botones de opción para mostrar la pestaña con un icono rojo o gris.</span><span class="sxs-lookup"><span data-stu-id="72b91-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="72b91-147">Al elegir el **botón Seleccionar gris** o **Seleccionar** rojo, se activa o, respectivamente, se establece y habilita el botón Guardar en la página `saveGray()` de `saveRed()` `settings.setValidityState(true)` configuración. </span><span class="sxs-lookup"><span data-stu-id="72b91-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="72b91-148">Este código permite Teams que ha cumplido los requisitos de configuración y la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="72b91-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="72b91-149">Al guardar, se establecen los `settings.setSettings` parámetros de.</span><span class="sxs-lookup"><span data-stu-id="72b91-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="72b91-150">Por último, `saveEvent.notifySuccess()` se llama para indicar que la dirección URL de contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="72b91-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]
