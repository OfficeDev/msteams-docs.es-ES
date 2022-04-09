---
title: Crear una pestaña de canal o grupo
author: laujan
description: Guía de inicio rápido para crear una pestaña de canal y grupo con el generador de Yeoman para Microsoft Teams, incluida la revisión del código fuente con ejemplos de código.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: bc7cb1fceef586959be44ba680874914c4f07cc1
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737045"
---
# <a name="channel-or-group-tab"></a>Pestaña Canal o grupo

Pestañas de canal o grupo entregar contenido a canales y chats grupales, y son una excelente manera de crear espacios de colaboración en torno a contenido dedicado basado en web.

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Cree una pestaña de grupo o canal personalizado con Node.js

1. En el símbolo del sistema, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) escribiendo el siguiente comando después de instalar el **Node.js**:

    ```cmd
    npm install yo gulp-cli --global
    ```

2. En el símbolo del sistema, instale Microsoft Teams generador de aplicaciones; para ello, escriba el siguiente comando:

    ```cmd
    npm install generator-teams --global
    ```

A continuación se indican los pasos para crear una pestaña de canal o grupo:

* [Generación de la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab)
* [Crear el paquete de aplicación](#create-your-app-package)
* [Compilación y ejecución de la aplicación](#build-and-run-your-application)
* [Establecimiento de un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab)
* [Upload la aplicación a Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generación de la aplicación con una pestaña de canal o grupo

1. En el símbolo del sistema, cree un nuevo directorio para la pestaña de canal o grupo.

1. Escriba el siguiente comando en el nuevo directorio para iniciar el generador de aplicaciones de Microsoft Teams:

    ```cmd
    yo teams
    ```

1. Proporcione los valores a una serie de preguntas que le pide Microsoft Teams generador de aplicaciones para actualizar el `manifest.json` archivo:

    ![Captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <details>
    <summary><b>Serie de preguntas para actualizar el archivo manifest.json</b></summary>

    * **¿Cómo se llama su solución?**

        El nombre de la solución es el nombre del proyecto. Para aceptar el nombre sugerido, seleccione **Entrar**.

    * **¿Dónde desea ubicar los archivos?**

        Actualmente se encuentra en el directorio del proyecto. Seleccione **Entrar**.

    * **¿Título del proyecto de aplicación de Microsoft Teams?**

        El título es el nombre del paquete de la aplicación y se usa en el manifiesto y la descripción de la aplicación. Escriba un título o seleccione **Entrar** para aceptar el nombre predeterminado.

    * **¿Su nombre (de empresa)? (máximo 32 caracteres)**

        El nombre de la empresa se usará en el manifiesto de la aplicación. Escriba un nombre de empresa o seleccione **Entrar** para aceptar el nombre predeterminado.

    * **¿Qué versión del manifiesto desea usar?**

        Seleccione el esquema predeterminado.

    * **¿Scaffolding rápido? (Y/n)**

        El valor predeterminado es sí; escriba **n** para escribir el identificador de asociado de Microsoft.

    * **Escriba su id. de partner de Microsoft, si tiene uno. (Deje en blanco para omitir)**

        Este campo no es necesario y solo se debe usar si ya forma parte de [Microsoft Partner Network](https://partner.microsoft.com).

    * **¿Qué desea agregar al proyecto?**

        Seleccione **( &ast; ) Una pestaña**.

    * **¿La dirección URL donde hospedará esta solución?**

        De forma predeterminada, el generador sugiere una dirección URL de sitios web de Azure. Solo está probando la aplicación localmente, por lo que no es necesaria una dirección URL válida.

    * **¿Desea mostrar un indicador de carga cuando se cargue la aplicación o la pestaña?**

        Elija **no** incluir un indicador de carga cuando se cargue la aplicación o la pestaña. El valor predeterminado es no, escriba **n**.

    * **¿Desea que las aplicaciones personales se representen sin una barra de encabezado de pestaña?**

        Elija **no** incluir aplicaciones personales que se van a representar sin una barra de encabezado de pestaña. El valor predeterminado es no, escriba **n**.

    * **¿Desea incluir el marco de pruebas y las pruebas iniciales? (y/N)**

        Elija **no** incluir un marco de prueba para este proyecto. El valor predeterminado es no, escriba **n**.

    * **¿Desea incluir compatibilidad con ESLint? (y/N)**

        Elija no incluir compatibilidad con ESLint. El valor predeterminado es no, escriba **n**.

    * **¿Desea usar azure applications Ideas para telemetría? (y/N)**

        Elija **no** incluir [Aplicación de Azure Ideas](/azure/azure-monitor/app/app-insights-overview). El valor predeterminado es no; escriba **n**.

    * **Nombre de tabulación predeterminado (máximo de 16 caracteres)?**

        Asigne un nombre a la pestaña. Este nombre de pestaña se usa en todo el proyecto como un componente de ruta de acceso de archivo o dirección URL.

    * **¿Qué tipo de pestaña le gustaría crear?**

        Use las teclas de dirección para seleccionar **la pestaña Configurable** .

    * **¿Qué ámbitos tiene previsto usar para la pestaña?**

        Puede seleccionar un equipo o un chat de grupo.

    * **¿Necesita compatibilidad con el inicio de sesión único de Microsoft Azure Active Directory (Azure AD) para la pestaña?**

        Elija **no** incluir compatibilidad con el inicio de sesión único de Microsoft Azure Active Directory (Azure AD) para la pestaña. El valor predeterminado es sí, escriba **n**.

    * **¿Desea que esta pestaña esté disponible en SharePoint Online? (Y/n)**

        Escriba **n**.

    </details>

> [!IMPORTANT]
> El componente de ruta **de acceso yourDefaultTabNameTab** es el valor que especificó en el generador para **Nombre de tabulación predeterminado** más la palabra **Tab**. Por ejemplo, `DefaultTabName` es **MyTab** y **luego /MyTabTab/**.

<!--- TBD: this info seems removed from the main branch.
* A **full color icon** measuring 192 x 192 pixels.
* A **transparent outline icon** measuring 32 x 32 pixels.
* A `manifest.json` file that specifies the attributes of your app.
--->

### <a name="create-your-app-package"></a>Crear el paquete de aplicación

Debe tener un paquete de aplicación para compilar y ejecutar la aplicación en Teams. El paquete de la aplicación se crea a través de una tarea gulp que valida el `manifest.json` archivo y genera la carpeta zip en el `./package` directorio. En el símbolo del sistema, escriba el comando siguiente:

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>Compilación y ejecución de la aplicación

#### <a name="build-your-application"></a>Compilación de la aplicación

Escriba el siguiente comando en el símbolo del sistema para transpilar la solución en la `./dist` carpeta :

```cmd
gulp build
```

#### <a name="run-your-application"></a>Ejecución de la aplicación

1. En el símbolo del sistema, escriba el siguiente comando para iniciar un servidor web local:

    ```bash
    gulp serve
    ```

1. Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador para ver la página principal de la aplicación.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Pestaña predeterminada" border="true":::

1. Para ver la página de configuración de la pestaña, vaya a `http://localhost:3007/<yourDefaultAppNameTab>/config.html`. Se muestra lo siguiente:

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="Página de configuración de tabulación" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecimiento de un túnel seguro en la pestaña

Para establecer un túnel seguro en la pestaña, salga de localhost y escriba el siguiente comando:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Una vez que la pestaña se carga en Microsoft Teams a través de **ngrok** y se guarda correctamente, puede verla en Teams hasta que finalice la sesión del túnel. Si reinicia la sesión de ngrok, debe actualizar la aplicación con la nueva dirección URL.

### <a name="upload-your-application-to-teams"></a>Upload la aplicación a Teams

1. Vaya a Microsoft Teams y seleccione **Aplicaciones**&nbsp; :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Tienda":::.
1. Seleccione **Administrar las aplicaciones** y **Upload una aplicación personalizada**.
1. Vaya al directorio del proyecto, vaya a la carpeta **./package** , seleccione la carpeta zip del paquete de aplicación y elija **Abrir**.

    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="Pestaña Canal cargado" border="true":::

1. Seleccione **Agregar** en el cuadro de diálogo. La pestaña se carga en Teams.

    > [!NOTE]
    > Si  **Agregar** no se muestra en el cuadro de diálogo, quite el código siguiente del manifiesto de la carpeta zip del paquete de la aplicación cargada. Vuelva a comprimir la carpeta y cárguela en Teams.
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. Siga las instrucciones para agregar una pestaña. Hay un cuadro de diálogo de configuración personalizado para la pestaña de canal o grupo.
1. Seleccione **Guardar** y la pestaña se agregará a la barra de pestañas del canal.

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="Pestaña de canal cargada" border="true":::

    Ahora ha creado y agregado correctamente el canal o la pestaña de grupo en Teams.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>Cree una pestaña de grupo o canal personalizado con ASP.NET Core

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio mediante el siguiente comando o puede descargar el [código fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

A continuación se indican los pasos para crear una pestaña de canal o grupo:

* [Generación de la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab-1)
* [Establecimiento de un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab-1)
* [Actualización de la aplicación](#update-your-application)
* [Compilación y ejecución de la aplicación](#build-and-run-your-application-1)
* [Actualización del paquete de la aplicación con el Portal para desarrolladores](#update-your-app-package-with-developer-portal)
* [Vista previa de la aplicación en Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generación de la aplicación con una pestaña de canal o grupo

1. Abra Visual Studio y seleccione **Abrir un proyecto o solución**.

1. Vaya a la carpeta Microsoft-Teams-Samplessamplestab-channel-grouprazor-csharp  >  >  >  y abra **channelGroupTab.sln**.

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar** de la aplicación para comprobar si la aplicación se ha cargado correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Revisión del código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto se creó a partir de una plantilla vacía de aplicación web ASP.NET Core 3.1 con la casilla **Advanced * Configure for HTTPS (Opciones avanzadas * Configurar para HTTPS**) seleccionada en el programa de instalación. El método del `ConfigureServices()` marco de inserción de dependencias registra los servicios MVC. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método mediante el código siguiente:

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

#### <a name="wwwroot-folder"></a>carpeta wwwroot

En ASP.NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core trata los archivos denominados **Index** como la página principal o predeterminada del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se muestra como la página principal de la aplicación.

#### <a name="tabcs"></a>Tab.cs

Este archivo de C# contiene un método al que se llama desde **Tab.cshtml** durante la configuración.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono de color completo** que mide 192 x 192 píxeles.
* Icono **de contorno transparente** que mide 32 x 32 píxeles.
* Archivo `manifest.json` que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña en Teams. Cuando un usuario elige agregar o actualizar la pestaña, Microsoft Teams carga el especificado en el `configurationUrl` manifiesto, lo inserta en un IFrame y lo representa en la pestaña.

#### <a name="csproj"></a>.csproj

En la ventana Visual Studio Explorador de soluciones, haga clic con el botón derecho en el proyecto y seleccione **Editar archivo Project**. Al final del archivo, verá el código siguiente que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecimiento de un túnel seguro en la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL.

### <a name="update-your-application"></a>Actualización de la aplicación

1. Abra Visual Studio Explorador de soluciones, vaya a la carpeta **PagesShared**  >  y abra **_Layout.cshtml** y agregue lo siguiente a <head> Sección de etiquetas:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > No copie ni pegue las `<script src="...">` direcciones URL de esta página, ya que no representan la versión más reciente. Para obtener la versión más reciente del SDK, vaya siempre a [Microsoft Teams API de JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. Inserte una llamada a `microsoftTeams.initialize();` en la `script` etiqueta .

1. En Visual Studio Explorador de soluciones vaya a la carpeta **Pages** y abra **Tab.cshtml**.

    En **Tab.cshtml** , la aplicación presenta al usuario dos botones de opción para mostrar la pestaña con un icono rojo o gris. Al elegir los desencadenadores de los botones `saveGray()` **Seleccionar gris** o **Seleccionar rojo** o `saveRed()`, respectivamente, establece `settings.setValidityState(true)`y habilita el botón **Guardar** en la página de configuración. Este código permite Teams saber que ha completado los requisitos de configuración y que la instalación puede continuar. Se establecen los parámetros de `settings.setSettings` . Por último, `saveEvent.notifySuccess()` se llama a para indicar que la dirección URL de contenido se ha resuelto correctamente.

1. Actualice los `websiteUrl` valores y `contentUrl` de cada función con la dirección URL de ngrok HTTPS a la pestaña.

    El código ahora debe incluir lo siguiente con **y8rCgT2b** reemplazado por la dirección URL de ngrok:

    ```javascript
        
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
        });
        }
    ```

1. Guarde el **archivo Tab.cshtml** actualizado.

### <a name="build-and-run-your-application"></a>Compilación y ejecución de la aplicación

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar**.

1. Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

    > [!TIP]
    > Debe tener la aplicación en Visual Studio y ngrok en ejecución para completar los pasos proporcionados en este artículo. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**. Escucha y reanuda el enrutamiento de la solicitud de la aplicación cuando se reinicia en Visual Studio. Si tiene que reiniciar el servicio ngrok, devuelve una nueva dirección URL y tiene que actualizar la aplicación con la nueva dirección URL.

<!--- TBD: This note seems to be removed from main. Commenting it for now.
> [!NOTE]
> App Studio can be used to edit your `manifest.json` file and upload the completed package to Teams. You can also manually edit the `manifest.json` file. If you do, ensure that you build the solution again to create the `tab.zip` file to upload.
--->

### <a name="update-your-app-package-with-developer-portal"></a>Actualización del paquete de la aplicación con el Portal para desarrolladores

1. Ve a Microsoft Teams. Si usa la [versión basada en web](https://teams.microsoft.com), puede inspeccionar el código front-end mediante [las herramientas para desarrolladores](~/tabs/how-to/developer-tools.md) del explorador.

1. Vaya al [**portal para desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abra **Aplicaciones** y seleccione **Importar aplicación**.

<!--- TBD: This steps seems to be removed from main now so commenting it for now.

1. Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest. The name of your app package is `tab.zip`. It is available from the following path:
--->

1. El nombre del paquete de la aplicación es `tab.zip`. Está disponible en la ruta de acceso siguiente:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Selecciónelo `tab.zip` y ábralo en el Portal para desarrolladores.

1. Se crea y rellena un **identificador de aplicación** predeterminado en la sección **Información básica** .

1. Agregue la descripción corta y larga de la aplicación en **Descripciones**.

1. En **Información del desarrollador**, agregue los detalles necesarios y, en **Sitio web (debe ser una dirección URL HTTPS válida),** proporcione la dirección URL HTTPS de ngrok.

1. En **Direcciones URL de la aplicación**, actualice la directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso en `https://<yourngrokurl>/tou` y guárdelo.

1. En **Características de la aplicación**, seleccione Grupo y aplicación de canal. Actualice la **dirección URL de configuración** con `https://<yourngrokurl>/tab` y seleccione la pestaña **Ámbito**.

1. Haga clic en **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo `<yourngrokurl>.ngrok.io`HTTPS .

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Seleccione **Vista previa en Teams** en la barra de herramientas del Portal para desarrolladores; portal para desarrolladores le informa de que la aplicación se ha cargado de forma local correctamente. La página **Agregar** aparece para la aplicación en Teams.

1. Seleccione **Agregar al equipo** para configurar la pestaña en un equipo. Configure la pestaña y seleccione **Guardar**. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Pestaña Canal ASPNET cargada" border="true":::
    
    Ahora ha creado y agregado correctamente el canal o la pestaña de grupo en Teams.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>Creación de un canal personalizado o una pestaña de grupo con ASP.NET Core MVC

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio mediante el siguiente comando o puede descargar el [código fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

A continuación se indican los pasos para crear una pestaña de canal o grupo:

* [Generación de la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab-2)
* [Establecimiento de un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab-2)
* [Actualización de la aplicación](#update-your-application-1)
* [Compilación y ejecución de la aplicación](#build-and-run-your-application-2)
* [Actualización del paquete de la aplicación con el Portal para desarrolladores](#update-your-app-package-with-developer-portal-1)
* [Vista previa de la aplicación en Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generación de la aplicación con una pestaña de canal o grupo

1. Abra Visual Studio y seleccione **Abrir un proyecto o solución**.

1. Vaya a la carpeta Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp  >  >  >  y abra **ChannelGroupTabMVC.sln**.

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar** de la aplicación para comprobar si la aplicación se ha cargado correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Revisión del código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto se creó a partir de una plantilla vacía de aplicación web de ASP.NET Core 3.1 con la casilla **Avanzadas - Configurar para HTTPS** seleccionada en la instalación. El método del `ConfigureServices()` marco de inserción de dependencias registra los servicios MVC. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de archivos estáticos se agrega al `Configure()` método mediante el código siguiente:

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

#### <a name="wwwroot-folder"></a>carpeta wwwroot

En ASP.NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono de color completo** que mide 192 x 192 píxeles.
* Icono **de contorno transparente** que mide 32 x 32 píxeles.
* Archivo `manifest.json` que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña en Teams.

#### <a name="csproj"></a>.csproj

En la ventana Visual Studio Explorador de soluciones, haga clic con el botón derecho en el proyecto y seleccione **Editar archivo Project**. Al final del archivo, verá el código siguiente que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

#### <a name="models"></a>Modelos

**ChannelGroup.cs** presenta un objeto Message y métodos a los que se llamará desde los controladores durante la configuración.

#### <a name="views"></a>Vistas

Estas son las distintas vistas de ASP.NET Core MVC:

* Inicio: ASP.NET Core trata los archivos denominados **Index** como la página principal o predeterminada del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se mostrará como la página principal de la aplicación.

* Compartido: el marcado de vista parcial **_Layout.cshtml** contiene la estructura general de la página de la aplicación y los elementos visuales compartidos. También hará referencia a la biblioteca de Teams.

#### <a name="controllers"></a>Controladores

Los controladores usan la `ViewBag` propiedad para transferir valores dinámicamente a las vistas.

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecimiento de un túnel seguro en la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL.

### <a name="update-your-application"></a>Actualización de la aplicación

1. Abra Visual Studio Explorador de soluciones, vaya a la carpeta **ViewsShared** > , abra **_Layout.cshtml** y agregue lo siguiente a <head> Sección de etiquetas:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > No copie ni pegue las `<script src="...">` direcciones URL de esta página, ya que no representan la versión más reciente. Para obtener la versión más reciente del SDK, vaya siempre a [Microsoft Teams API de JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. Inserte una llamada a `microsoftTeams.initialize();` en la `script` etiqueta .

1. En Visual Studio Explorador de soluciones vaya a la carpeta **Tab** y abra **Tab.cshtml**.

    En **Tab.cshtml** , la aplicación presenta al usuario dos botones de opción para mostrar la pestaña con un icono rojo o gris. Al elegir los desencadenadores de los botones `saveGray()` **Seleccionar gris** o **Seleccionar rojo** o `saveRed()`, respectivamente, establece `settings.setValidityState(true)`y habilita el botón **Guardar** en la página de configuración. Este código permite Teams saber que ha completado los requisitos de configuración y que la instalación puede continuar. Se establecen los parámetros de `settings.setSettings` . Por último, `saveEvent.notifySuccess()` se llama a para indicar que la dirección URL de contenido se ha resuelto correctamente. 

1. Actualice los `websiteUrl` valores y `contentUrl` de cada función con la dirección URL de ngrok HTTPS a la pestaña.

    El código ahora debe incluir lo siguiente con **y8rCgT2b** reemplazado por la dirección URL de ngrok:

    ```javascript

        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. Asegúrese de guardar el **archivo Tab.cshtml** actualizado.

### <a name="build-and-run-your-application"></a>Compilación y ejecución de la aplicación

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar**.

1. Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

    > [!TIP]
    > Debe tener la aplicación en Visual Studio y ngrok en ejecución para completar los pasos proporcionados en este artículo. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**. Escucha y reanuda el enrutamiento de la solicitud de la aplicación cuando se reinicia en Visual Studio. Si tiene que reiniciar el servicio ngrok, devuelve una nueva dirección URL y tiene que actualizar la aplicación con la nueva dirección URL.

### <a name="update-your-app-package-with-developer-portal"></a>Actualización del paquete de la aplicación con el Portal para desarrolladores

1. Ve a Microsoft Teams. Si usa la [versión basada en web](https://teams.microsoft.com), puede inspeccionar el código front-end mediante [las herramientas para desarrolladores](~/tabs/how-to/developer-tools.md) del explorador.

1. Vaya al [**portal para desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abra **Aplicaciones** y seleccione **Importar aplicación**.

1. El nombre del paquete de la aplicación es **tab.zip**. Está disponible en la ruta de acceso siguiente:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Seleccione **tab.zip** y ábralo en el Portal para desarrolladores.

1. Se crea y rellena un **identificador de aplicación** predeterminado en la sección **Información básica** .

1. Agregue la descripción corta y larga de la aplicación en **Descripciones**.

1. En **Información del desarrollador**, agregue los detalles necesarios y, en **Sitio web (debe ser una dirección URL HTTPS válida),** proporcione la dirección URL HTTPS de ngrok.

1. En **Direcciones URL de la aplicación**, actualice la directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso en `https://<yourngrokurl>/tou` y guárdelo.

1. En **Características de la aplicación**, seleccione Grupo y aplicación de canal. Actualice la **dirección URL de configuración** con `https://<yourngrokurl>/tab` y seleccione la pestaña **Ámbito**.

1. Haga clic en **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo `<yourngrokurl>.ngrok.io`HTTPS .

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Seleccione **Vista previa en Teams** en la barra de herramientas del Portal para desarrolladores; portal para desarrolladores le informa de que la aplicación se ha cargado de forma local correctamente. La página **Agregar** aparece para la aplicación en Teams.

1. Seleccione **Agregar al equipo** para configurar la pestaña en un equipo. Configure la pestaña y seleccione **Guardar**. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Pestaña Canal de ASPNET MVC cargada" border="true":::
    
    Ahora ha creado y agregado correctamente el canal o la pestaña de grupo en Teams.

::: zone-end

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Creación de una página de contenido](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>Consulte también

* [pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Crear una página de eliminación](~/tabs/how-to/create-tab-pages/removal-page.md)
