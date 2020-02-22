---
title: Crear una ficha de canal y de grupo con ASP.NET Core
author: laujan
description: Una guía de inicio rápido para crear una ficha de canal y de grupo personalizada con ASP.NET Core.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 47a0c98d630501944c7a5f4baf4620dbb70cdbcd
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228013"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a>Crear una ficha de canal y de grupo personalizada con ASP.NET Core

En este tutorial rápido, vamos a crear una pestaña de canal o de grupo personalizada con C# y página de Razor ASP.Net Core. También usaremos [App Studio para Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) para finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtener el código fuente

Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestañas. Proporcionamos un proyecto sencillo para empezar. Para recuperar el código fuente, puede descargar la carpeta ZIP y extraer los archivos o clonar el repositorio de muestra en el nuevo directorio:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Una vez que tenga el código fuente, abra Visual Studio y seleccione **abrir un proyecto o solución**. Navegue hasta el directorio de la aplicación de la pestaña y Abra **ChannelGroupTab. sln**.

Para compilar y ejecutar la aplicación, presione **F5** o elija **iniciar depuración** en el menú **depurar** . En un explorador, navegue a las direcciones URL que aparecen a continuación y compruebe que la aplicación se cargó correctamente:

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a>Revisar el código fuente

### <a name="startupcs"></a>Startup.cs

Este proyecto se creó a partir de una plantilla vacía de la aplicación Web de ASP.NET Core 2,2 con la casilla de verificación *Advanced-configure for https* seleccionada en la instalación. Los servicios MVC se registran mediante el método del marco `ConfigureServices()` de inserción de dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de `Configure()` archivos estáticos se agrega al método:

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

### <a name="wwwroot-folder"></a>carpeta wwwroot

En ASP.NET Core, la carpeta Web raíz es donde la aplicación busca archivos estáticos.

### <a name="indexcshtml"></a>Index. cshtml

ASP.NET Core trata los archivos denominados *index* como página principal o predeterminada del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, se mostrará **index. cshtml** como la Página principal de la aplicación.

### <a name="tabcs"></a>Tab.cs

Este archivo de C# contiene un método al que se llamará desde **Tab. cshtml** durante la configuración.

### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de la aplicación obligatorios:

- Un **icono de color completo** que mide 192 x 192 píxeles.
- Un **icono de contorno transparente** que mide 32 x 32 píxeles.
- Un archivo **manifest. JSON** que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de la aplicación que se usará para cargar la pestaña en Teams. Cuando un usuario elige agregar o actualizar la pestaña, Microsoft Teams cargará los especificados en el manifiesto, los `configurationUrl` incrustará en un iframe y los representará en la pestaña.

### <a name="csproj"></a>. csproj

En la ventana Explorador de soluciones de Visual Studio, haga clic con el botón secundario en el proyecto y seleccione **Editar archivo de proyecto**. En la parte inferior del archivo, verá el código que crea y actualiza la carpeta ZIP cuando se genera la aplicación:

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

- Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- Ngrok escuchará las solicitudes de Internet y las dirigirá a la aplicación cuando se ejecute en el puerto 44355. Debe ser similar a `https://y8rCgT2b.ngrok.io/` donde *y8rCgT2b* se reemplaza por su dirección URL https alfanumérica de ngrok.

- Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL, que lo necesitará más adelante.

## <a name="update-your-application"></a>Actualizar la aplicación

Dentro de *Tab. cshtml* , la aplicación presenta al usuario dos botones de opción para mostrar la ficha con un icono rojo o gris. Al elegir el botón **seleccionar gris** o **seleccionar rojo** `saveGray()` , `saveRed()`se activa o, `settings.setValidityState(true)`respectivamente, establece y se habilita el botón **Guardar** en la página de configuración. Este código permite que los equipos sepan que ha satisfecho los requisitos de configuración y que la instalación puede continuar. Al guardar, se establecen los `settings.setSettings` parámetros de. Por último `saveEvent.notifySuccess()` , se llama a para indicar que la dirección URL del contenido se ha resuelto correctamente.

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

