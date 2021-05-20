---
title: Cree una pestaña personal con ASP. NET Core MVC
author: laujan
description: Una guía de inicio rápido para crear una pestaña personal personalizada con ASP. MVC de NET Core.
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
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a>Cree una pestaña personal personalizada con ASP.NET Core MVC

En esta guía de inicio rápido, crearemos una pestaña personal personalizada con C# y ASP.Net Core MVC. También usaremos [App Studio para Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) para finalizar el manifiesto de la aplicación e implementar la pestaña en Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtener el código fuente

Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña. Hemos proporcionado un proyecto sencillo para que comiences. Para recuperar el código fuente, puede descargar la carpeta zip y extraer los archivos o clonar el repositorio de ejemplo en el nuevo directorio:

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Una vez que tenga el código fuente, abra Visual Studio y seleccione **Abrir un proyecto o solución.** Vaya al directorio de la aplicación de tabulación y abra **PersonalTabMVC.sln**.

Para compilar y ejecutar la aplicación, presione **F5** o elija **Iniciar depuración** en el menú **Depurar.** En un explorador, vaya a las direcciones URL a continuación para comprobar que la aplicación se cargó correctamente:

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a>Revise el código fuente

### <a name="startupcs"></a>Inicio.cs

Este proyecto se creó a partir de un ASP. Plantilla vacía de aplicación web de NET Core 2.2 con la casilla *Avanzadas - Configurar para HTTPS* activada en el programa de instalación. Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias. Además, la plantilla vacía no habilita la publicación de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método:

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

### <a name="wwwroot-folder"></a>carpeta wwwroot

En ASP. NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.

### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono a todo color** que mide 192 x 192 píxeles.
* Un **icono de contorno transparente** que mide 32 x 32 píxeles.
* Un **manifest.jsen el** archivo que especifica los atributos de la aplicación.

Estos archivos deben estar comprimidos en un paquete de aplicación para su uso en la carga de la pestaña a Teams. Microsoft Teams cargará lo especificado en el `contentUrl` manifiesto, lo incrustará en un IFrame y lo representará en la pestaña.

### <a name="csproj"></a>.csproj

En la ventana explorador de soluciones Visual Studio haga clic con el botón derecho en el proyecto y seleccione **Editar Project archivo**. En la parte inferior del archivo verá el código que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

### <a name="models"></a>Modelos

**PersonalTab.cs** presenta un objeto Message y métodos a los que se llamará desde *PersonalTabController* cuando un usuario selecciona un botón en la vista **PersonalTab.**

### <a name="views"></a>Views

#### <a name="home"></a>Inicio

áspid. NET Core trata los archivos denominados **Índice** como predeterminado o página de inicio del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se mostrará como la página principal de la aplicación.

#### <a name="shared"></a>Compartido

El marcado de vista parcial *_Layout.cshtml* contiene la estructura general de páginas de la aplicación y los elementos visuales compartidos. También hará referencia a la Biblioteca Teams.

### <a name="controllers"></a>Controladores

Los controladores utilizan la propiedad ViewBag para transferir valores dinámicamente a vistas.

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* Abra un símbolo del sistema en la raíz del directorio del proyecto y ejecute el siguiente comando:

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* Ngrok escuchará las solicitudes de Internet y las enrutará a su aplicación cuando se ejecute en el puerto 44325.  Debe ser similar `https://y8rPrT2b.ngrok.io/` a donde *y8rPrT2b* es reemplazado por su URL HTTPS alfanumérica ngrok.

* Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y de tomar nota de la dirección URL: la necesitará más adelante.

* Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador e yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

> [!TIP]
> Debe tener la aplicación en Visual Studio y ngrok ejecutándose para completar esta guía de inicio rápido. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución.** Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio. Si tienes que reiniciar el servicio ngrok devolverá una nueva dirección URL y tendrás que actualizar cada lugar que use esa dirección URL.

### <a name="run-your-application"></a>Ejecute la aplicación

* En Visual Studio presione **F5** o elija **Iniciar depuración** en el menú **Depurar de** la aplicación.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Cree una pestaña de canal y grupo personalizada con Node.js y el generador Yeoman para Microsoft Teams](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
