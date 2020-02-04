---
title: Crear una pestaña personal con ASP.NET Core
author: laujan
description: Una guía de inicio rápido para crear una ficha personal personalizada con ASP.NET Core.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: b279c96f47265fe1928ae90d661e7dc042085b39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676174"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core"></a>Crear una ficha personal personalizada con ASP.NET Core

En este tutorial rápido, vamos a crear una pestaña personal personalizada con páginas de Razor principales de C# y ASP.Net. También usaremos [App Studio para Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) para finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtener el código fuente

Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestañas. Proporcionamos un proyecto sencillo para empezar. Para recuperar el código fuente, puede descargar la carpeta ZIP y extraer los archivos o clonar el repositorio de muestra en el nuevo directorio:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Una vez que tenga el código fuente, abra Visual Studio y seleccione **abrir un proyecto o solución**. Navegue hasta el directorio de la aplicación de la pestaña y Abra **PersonalTab. sln**.

Para compilar y ejecutar la aplicación, presione **F5** o elija **iniciar depuración** en el menú **depurar** . En un explorador, navegue a las siguientes direcciones URL para comprobar que la aplicación se cargó correctamente:

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

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

### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de la aplicación obligatorios:

- Un **icono de color completo** que mide 192 x 192 píxeles.
- Un **icono de contorno transparente** que mide 32 x 32 píxeles.
- Un archivo **manifest. JSON** que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de la aplicación que se usará para cargar la pestaña en Teams. Microsoft Teams cargará `contentUrl` el especificado en el manifiesto, lo incrustará en un iframe y lo representará en la pestaña.

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

[!INCLUDE  [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- Ngrok escuchará las solicitudes de Internet y las dirigirá a la aplicación cuando se ejecute en el puerto 44325.  Debe ser similar a `https://y8rPrT2b.ngrok.io/` donde *y8rPrT2b* se reemplaza por su dirección URL https alfanumérica de ngrok.

- Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL, que lo necesitará más adelante.

- Compruebe que *ngrok* se está ejecutando y que funciona correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL https ngrok que se proporcionó en la ventana del símbolo del sistema.

>[!TIP]
>Debe tener la aplicación en Visual Studio y ngrok en ejecución para completar este inicio rápido. Si necesita detener la ejecución de la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**. Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio. Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar todos los sitios que usen esa dirección URL.

### <a name="run-your-application"></a>Ejecutar la aplicación

- En Visual Studio, presione **F5** o elija **iniciar depuración** en el menú **depurar** de la aplicación.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
