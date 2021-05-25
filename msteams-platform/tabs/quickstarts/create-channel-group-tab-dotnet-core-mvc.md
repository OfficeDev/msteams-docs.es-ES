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
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a>Crear un canal personalizado y una pestaña de grupo con ASP.NET Core MVC

En esta guía de inicio rápido, crearemos una pestaña de canal o grupo personalizada con C# y ASP.Net Core MVC. También usaremos [App Studio](~/concepts/build-and-test/app-studio-overview.md) para Microsoft Teams finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtener el código fuente

Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña. Hemos proporcionado un proyecto de pestaña de [grupo de canales](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) sencillo para empezar. Para recuperar el código fuente, puede descargar la carpeta zip y extraer los archivos o clonar el repositorio de ejemplo en el nuevo directorio:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Una vez que tenga el código fuente, abra Visual Studio y seleccione **Abrir un proyecto o solución**. Vaya al directorio de la aplicación de tabulación y abra **ChannelGroupTabMVC.sln**.

Para compilar y ejecutar la aplicación, presione **F5** o **elija Iniciar depuración** en el **menú** Depurar. En un explorador, vaya a las direcciones URL siguientes y compruebe que la aplicación se cargó correctamente:

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a>Revisar el código fuente

### <a name="startupcs"></a>Startup.cs

Este proyecto se creó a partir de una plantilla vacía ASP.NET Core aplicación web 2.2 con la casilla Avanzadas *- Configurar* para HTTPS activada en el programa de instalación. Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método:

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

En ASP.NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.

### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

- Un **icono de color completo** que mide 192 x 192 píxeles.
- Un **icono de esquema transparente** que mide 32 x 32 píxeles.
- Un **manifest.jsen** el archivo que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña a Teams.

### <a name="csproj"></a>.csproj

En la ventana Visual Studio Explorador de soluciones haga clic con el botón secundario en el proyecto y seleccione **Editar Project archivo**. En la parte inferior del archivo verá el código que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

### <a name="models"></a>Modelos

*ChannelGroup.cs* presenta un objeto Message y métodos a los que se llamará desde los controladores durante la configuración.

### <a name="views"></a>Views

#### <a name="home"></a>Inicio

ASP.NET Core trata los archivos denominados *Index* como la página predeterminada/principal del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se mostrará como la página principal de la aplicación.

#### <a name="shared"></a>Compartido

El marcado de vista *parcial _Layout.cshtml* contiene la estructura de página general de la aplicación y los elementos visuales compartidos. También hará referencia a la Teams biblioteca.

### <a name="controllers"></a>Controladores

Los controladores usan la propiedad ViewBag para transferir valores dinámicamente a las vistas.

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:

    ```bash
    ngrok http https://localhost:443560 -host-header="localhost:44360"
    ```

- Ngrok escuchará las solicitudes de Internet y las enrutará a la aplicación cuando se ejecute en el puerto 44355.  Debe ser similar `https://y8rCgT2b.ngrok.io/` a *donde y8rCgT2b* se reemplaza por la dirección URL HTTPS alfanumérico de ngrok.

- Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y de tomar nota de la dirección URL; la necesitará más adelante.

## <a name="update-your-application"></a>Actualizar la aplicación

En **Tab.cshtml,** la aplicación presenta al usuario dos botones de opción para mostrar la pestaña con un icono rojo o gris. Al elegir el **botón Seleccionar gris** o **Seleccionar** rojo, se activa o, respectivamente, se establece y habilita el botón Guardar en la página `saveGray()` de `saveRed()` `settings.setValidityState(true)` configuración.  Este código permite Teams que ha cumplido los requisitos de configuración y la instalación puede continuar. Al guardar, se establecen los `settings.setSettings` parámetros de. Por último, `saveEvent.notifySuccess()` se llama para indicar que la dirección URL de contenido se ha resuelto correctamente.

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]
