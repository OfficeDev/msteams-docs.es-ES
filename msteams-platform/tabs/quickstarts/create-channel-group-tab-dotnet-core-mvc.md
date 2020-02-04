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
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a>Crear una ficha de canal y de grupo personalizada con ASP.NET Core MVC

En este tutorial rápido, crearemos una pestaña de grupo/canal personalizado con C# y ASP.Net Core MVC. También usaremos [App Studio para Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) para finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtener el código fuente

Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestañas. Proporcionamos un sencillo proyecto de [pestaña de grupo de canal](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) para empezar. Para recuperar el código fuente, puede descargar la carpeta ZIP y extraer los archivos o clonar el repositorio de muestra en el nuevo directorio:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Una vez que tenga el código fuente, abra Visual Studio y seleccione **abrir un proyecto o solución**. Navegue hasta el directorio de la aplicación de la pestaña y Abra **ChannelGroupTabMVC. sln**.

Para compilar y ejecutar la aplicación, presione **F5** o elija **iniciar depuración** en el menú **depurar** . En un explorador, vaya a las siguientes direcciones URL y compruebe que la aplicación se cargó correctamente:

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

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

### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de la aplicación obligatorios:

- Un **icono de color completo** que mide 192 x 192 píxeles.
- Un **icono de contorno transparente** que mide 32 x 32 píxeles.
- Un archivo **manifest. JSON** que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de la aplicación que se usará para cargar la pestaña en Teams.

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

### <a name="models"></a>Brinda

*ChannelGroup.CS* presenta un objeto de mensaje y métodos a los que se llamará desde los controladores durante la configuración.

### <a name="views"></a>Vistas

#### <a name="home"></a>Inicio

ASP.NET Core trata los archivos denominados *index* como página principal o predeterminada del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, se mostrará **index. cshtml** como la Página principal de la aplicación.

#### <a name="shared"></a>Compartidos

La vista parcial de marcas *_Layout. cshtml* contiene la estructura de página general y los elementos visuales compartidos de la aplicación. También hará referencia a la biblioteca de Teams.

### <a name="controllers"></a>Controles

Los controladores usan la propiedad ViewBag para transferir valores de forma dinámica a las vistas.

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- Ngrok escuchará las solicitudes de Internet y las dirigirá a la aplicación cuando se ejecute en el puerto 44355.  Debe ser similar a `https://y8rCgT2b.ngrok.io/` donde *y8rCgT2b* se reemplaza por su dirección URL https alfanumérica de ngrok.

- Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL, que lo necesitará más adelante.

## <a name="update-your-application"></a>Actualizar la aplicación

Dentro de **Tab. cshtml** , la aplicación presenta al usuario dos botones de opción para mostrar la ficha con un icono rojo o gris. Al elegir el botón **seleccionar gris** o **seleccionar rojo** `saveGray()` , `saveRed()`se activa o, `settings.setValidityState(true)`respectivamente, establece y se habilita el botón **Guardar** en la página de configuración. Este código permite que los equipos sepan que ha satisfecho los requisitos de configuración y que la instalación puede continuar. Al guardar, se establecen los `settings.setSettings` parámetros de. Por último `saveEvent.notifySuccess()` , se llama a para indicar que la dirección URL del contenido se ha resuelto correctamente.

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
