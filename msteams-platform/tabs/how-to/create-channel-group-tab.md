---
title: Crear una pestaña de canal
author: laujan
description: Cree un canal personalizado, una pestaña de grupo con Node.js, ASP.NET Core, ASP.NET Core MVC. Generación de una aplicación, creación de un paquete, compilación y ejecución de aplicaciones, túnel secreto, carga en Teams
ms.localizationpriority: high
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 0febbd535f5375f03599009d32d9b613cf5af6d6
ms.sourcegitcommit: e4ccbbdce620418c129689c0ba6ad246a81068c0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2022
ms.locfileid: "68329087"
---
# <a name="create-a-channel-tab"></a>Crear una pestaña de canal

Pestañas de canal o grupo entregar contenido a canales y chats grupales, y son una excelente manera de crear espacios de colaboración en torno a contenido dedicado basado en web.

Asegúrese de que tiene todos los [requisitos previos](~/tabs/how-to/tab-requirements.md) para compilar el canal o la pestaña de grupo.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Crear una pestaña personalizada de canal o grupo con Node.js

1. En el símbolo del sistema, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) introduciendo el siguiente comando después de instalar **Node.js**:

    ```cmd
    npm install yo gulp-cli --global
    ```

2. En el símbolo del sistema, instale el generador de aplicaciones de Microsoft Teams escribiendo el siguiente comando:

    ```cmd
    npm install generator-teams --global
    ```

Estos son los pasos para crear una pestaña de canal o grupo:

* [Generar la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab)
* [Crear el paquete de aplicación](#create-your-app-package)
* [Compilar y ejecutar la aplicación](#build-and-run-your-application)
* [Establecer un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab)
* [Cargar la aplicación en Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generar la aplicación con una pestaña de canal o grupo

1. En el símbolo del sistema, cree un nuevo directorio para la pestaña de canal o grupo.

1. Escriba el siguiente comando en el nuevo directorio para iniciar el generador de aplicaciones de Microsoft Teams:

    ```cmd
    yo teams
    ```

1. Proporcione sus valores a una serie de preguntas solicitadas por el generador de aplicaciones de Microsoft Teams para actualizar el archivo `manifest.json`:

    ![captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <details>
    <summary><b>serie de preguntas para actualizar el archivo manifest.json</b></summary>

    * **¿Cómo se llama su solución?**

        El nombre de la solución es el nombre del proyecto. Puede aceptar el nombre sugerido seleccionando **Introducir**.

    * **¿Dónde desea ubicar los archivos?**

        Actualmente está en el directorio del proyecto. Seleccione **Introducir**.

    * **¿Título del proyecto de su aplicación de Microsoft Teams?**

        El título es el nombre del paquete de la aplicación y se usa en el manifiesto y en la descripción de la aplicación. Escriba un título o seleccione **Introducir** para aceptar el nombre predeterminado.

    * **¿Nombre (de su empresa)? (Máximo 32 caracteres)**

        El nombre de la empresa se usará en el manifiesto de la aplicación. Escriba un nombre de empresa o seleccione **Introducir** para aceptar el nombre predeterminado.

    * **¿Qué versión del manifiesto desea usar?**

        Seleccione el esquema predeterminado.

    * **¿Scaffolding rápido? (S/n)**

        El valor predeterminado es sí; escriba **n** para introducir su Id. de partner de Microsoft.

    * **Introduzca su Id. de partner de Microsoft, si lo tiene (deje el espacio en blanco para omitir esta respuesta)**

        Este campo no es obligatorio y solo debe usarse si ya forma parte de la [Microsoft Partner Network](https://partner.microsoft.com).

    * **¿Qué desea agregar al proyecto?**

        Seleccione **( &ast; ) Una pestaña**.

    * **¿Cuál es la dirección URL en donde hospedará esta solución?**

        De forma predeterminada, el generador sugiere una dirección URL de sitios web de Azure. Solo está probando la aplicación localmente, por lo que no es necesaria ninguna dirección URL válida.

    * **¿Quiere mostrar un indicador de carga cuando se cargue la aplicación o la pestaña?**

        Elija **no** incluir ningún indicador de carga cuando se cargue la aplicación o la pestaña. El valor predeterminado es no, escriba **n**.

    * **¿Desea que las aplicaciones personales se representen sin una barra de encabezado de pestaña?**

        Elija **no** incluir aplicaciones personales que se van a representar sin una barra de encabezado de pestaña. El valor predeterminado es no, escriba **n**.

    * **¿Desea incluir un marco de prueba y pruebas iniciales? (s/N)**

        Elija **no** incluir ningún marco de prueba para este proyecto. El valor predeterminado es no, escriba **n**.

    * **¿Desea incluir la compatibilidad con ESLint? (s/N)**

        Elija no incluir compatibilidad con ESLint. El valor predeterminado es no, escriba **n**.

    * **¿Desea usar Azure Applications Insights para la telemetría? (s/N)**

        Elija **no** incluir [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview). El valor predeterminado es no; escriba **n**.

    * **¿Nombre de pestaña predeterminado? (Máximo 16 caracteres)**

        Asigne un nombre a la pestaña. Este nombre de pestaña se usará en todo el proyecto como un componente de ruta de acceso del archivo o la dirección URL.

    * **¿Qué tipo de pestaña quiere crear?**

        Use las teclas de dirección para seleccionar la pestaña **Configurable**.

    * **¿Qué ámbitos va a usar para la pestaña?**

        Puede seleccionar un equipo o un chat de grupo.

    * **¿Necesita compatibilidad con el inicio de sesión único de Microsoft Azure Active Directory (Azure AD) para la pestaña?**

        Elija **no** incluir compatibilidad con el inicio de sesión único de Microsoft Azure Active Directory (Azure AD) para la pestaña. El valor predeterminado es sí, introduzca **n**.

    * **¿Quiere que esta pestaña esté disponible en SharePoint Online? (S/n)**

        Introduzca **n**.

    </details>

> [!IMPORTANT]
> El componente de ruta **yourDefaultTabNameTab** es el valor que especificó en el generador para **Nombre de pestaña predeterminado** más la palabra **Tab**. Por ejemplo, `DefaultTabName` es **MyTab** y **luego /MyTabTab/**.

<!--- TBD: this info seems removed from the main branch.
* A **full color icon** measuring 192 x 192 pixels.
* A **transparent outline icon** measuring 32 x 32 pixels.
* A `manifest.json` file that specifies the attributes of your app.
--->

### <a name="create-your-app-package"></a>Crear el paquete de aplicación

Debe tener un paquete de aplicación para compilar y ejecutar la aplicación en Teams. El paquete de la aplicación se crea a través de una tarea de Gulp que valida el archivo `manifest.json` y genera la carpeta ZIP en el directorio `./package`. En el símbolo del sistema, escriba el comando siguiente:

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

#### <a name="build-your-application"></a>Compilar la aplicación

Escriba el siguiente comando en el símbolo del sistema para transpilar la solución en la carpeta `./dist`:

```cmd
gulp build
```

#### <a name="run-your-application"></a>Ejecutar la aplicación

1. En el símbolo del sistema, escriba el siguiente comando para iniciar un servidor web local:

    ```bash
    gulp serve
    ```

1. Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador para ver la página principal de la aplicación.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Pestaña predeterminada":::

1. Para ver la página de configuración de la pestaña, vaya a `http://localhost:3007/<yourDefaultAppNameTab>/config.html`. Se muestra lo siguiente:

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="Página de configuración de la pestaña":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

Para establecer un túnel seguro en la pestaña, salga de localhost e introduzca el siguiente comando:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Una vez que la pestaña se carga en Microsoft Teams a través de **ngrok** y se guarda correctamente, puede verla en Teams hasta que finalice la sesión del túnel. Si reinicia la sesión de ngrok, debe actualizar la aplicación con la nueva dirección URL.

### <a name="upload-your-application-to-teams"></a>Cargar la aplicación en Teams

1. Vaya a Teams y seleccione **Aplicaciones**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Tienda de Teams":::.
1. Seleccione **Administrar las aplicaciones** > **Cargar una aplicación** > **Carga de una aplicación personalizada**.
1. Vaya al directorio del proyecto, desplácese hasta la carpeta **./package**, seleccione la carpeta ZIP del paquete de la aplicación y elija **Abrir**.

    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="Pestaña del canal cargada":::

1. Seleccione **Agregar** en el cuadro de diálogo. La pestaña se carga en Teams.

    > [!NOTE]
    > Si no se muestra **Agregar** en el cuadro de diálogo, quite el código siguiente del manifiesto de la carpeta ZIP del paquete de la aplicación cargada. Vuelva a comprimir la carpeta y cárguela en Teams.
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. Siga las instrucciones para agregar una pestaña. Hay un cuadro de diálogo de configuración personalizado para la pestaña de canal o grupo.
1. Seleccione **Guardar** y la pestaña se agregará a la barra de pestañas del canal.

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="Pestaña de canal cargada":::

    Ahora ha creado y agregado correctamente la pestaña de canal o grupo en Teams.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>Crear una pestaña personalizada de canal o grupo con ASP.NET Core

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de la pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio con el siguiente comando o puede descargar el [ código fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Estos son los pasos para crear una pestaña de canal o grupo:

* [Generar la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab-1)
* [Establecer un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab-1)
* [Actualizar la aplicación](#update-your-application)
* [Compilar y ejecutar la aplicación](#build-and-run-your-application-1)
* [Actualizar el paquete de la aplicación con el portal para desarrolladores](#update-your-app-package-with-developer-portal)
* [Vista previa de la aplicación en Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generar la aplicación con una pestaña de canal o grupo

1. Abra Visual Studio y seleccione **Abrir un proyecto o solución**.

1. Vaya a la carpeta **Microsoft-Teams-Samples** > **samples** > **tab-channel-group** > **razor-csharp** y abra **channelGroupTab.sln**.

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar** de la aplicación para comprobar si la aplicación se ha cargado correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * `https://localhost:3978/`
    * `https://localhost:3978/privacy`
    * `https://localhost:3978/tou`

<details>
<summary><b>Revisar el código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto se creó a partir de una plantilla vacía de aplicación web ASP.NET Core 3.1 con la casilla de verificación **Avanzado * Configurar para HTTPS** seleccionada en la configuración. Los servicios de MVC se registran mediante el método `ConfigureServices()` del marco de inserción de dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de los archivos estáticos se agrega al método `Configure()` mediante el código siguiente:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options => options.EnableEndpointRouting = false);
}

public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();
    app.UseMvc();
}
```

#### <a name="wwwroot-folder"></a>carpeta wwwroot

En ASP.NET Core, la carpeta raíz web es en donde la aplicación busca los archivos estáticos.

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core trata los archivos llamados **Index** como la página principal o predeterminada del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se muestra como la página principal de la aplicación.

#### <a name="tabcs"></a>Tab.cs

Este archivo de C# contiene un método al que se llama desde **Tab.cshtml** durante la configuración.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono a todo color** de 192 x 192 píxeles.
* Un **icono de contorno transparente** de 32 x 32 píxeles.
* Un archivo `manifest.json` que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña en Teams. Cuando un usuario elige agregar o actualizar la pestaña, Teams carga el especificado en el `configurationUrl` manifiesto, lo inserta en un IFrame y lo representa en la pestaña.

#### <a name="csproj"></a>.csproj

En la ventana Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto y seleccione **Editar archivo de proyecto**. Al final del archivo, verá el código siguiente que crea y actualiza la carpeta ZIP cuando se compila la aplicación:

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

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL.

### <a name="update-your-application"></a>Actualizar la aplicación

1. Abra el Explorador de soluciones de Visual Studio, vaya a la carpeta **Pages** > **Shared** y abra **_Layout.cshtml** y agregue lo siguiente a <head> la sección de etiquetas:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js"></script>
    ```

    > [!IMPORTANT]
    > No copie ni pegue las direcciones URL `<script src="...">` de esta página, ya que no representan la versión más reciente. Para obtener la versión más reciente del SDK, vaya siempre a la [API de JavaScript de Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js).

1. Inserte una llamada a `microsoftTeams.app.initialize();` en la etiqueta `script`.

1. En el Explorador de soluciones de Visual Studio vaya a la carpeta **Pages** y abra **Tab.cshtml**.

    En **Tab.cshtml** , la aplicación presenta al usuario dos opciones para mostrar la pestaña con un icono rojo o gris. El botón **Seleccionar gris** o **Seleccionar rojo** desencadena `saveGray()` o `saveRed()` , respectivamente, establece `pages.config.setValidityState(true)`y habilita **Guardar** en la página de configuración. Este código permite a Teams saber que ha completado la configuración de requisitos y puede continuar con la instalación. Se establecen los parámetros de `pages.config.setConfig`. Por último, se llama a `saveEvent.notifySuccess()` para indicar que la dirección URL de contenido se ha resuelto correctamente.

1. Actualice los valores `websiteUrl` y `contentUrl` en cada función con la dirección URL de ngrok HTTPS en la pestaña.

    El código ahora debe incluir lo siguiente con **y8rCgT2b** reemplazado por la dirección URL de ngrok:

    ```javascript
        
        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl: ""
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl: ""
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. Guarde el archivo **tab.cshtml** actualizado.

### <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar**.

1. Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

    > [!TIP]
    > Debe tener la aplicación en Visual Studio y ngrok en ejecución para completar los pasos proporcionados en este artículo. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**. Escucha y reanuda el enrutamiento de la solicitud de la aplicación cuando se reinicia en Visual Studio. Si tiene que reiniciar el servicio ngrok, devuelve una nueva dirección URL y tiene que actualizar la aplicación con la nueva dirección URL.

<!--- TBD: This note seems to be removed from main. Commenting it for now.
> [!NOTE]
> App Studio can be used to edit your `manifest.json` file and upload the completed package to Teams. You can also manually edit the `manifest.json` file. If you do, ensure that you build the solution again to create the `tab.zip` file to upload.
--->

### <a name="update-your-app-package-with-developer-portal"></a>Actualizar el paquete de la aplicación con el portal para desarrolladores

1. Vaya a Teams. Si usa la [versión basada en la Web](https://teams.microsoft.com), puede inspeccionar el código front-end mediante las [herramientas para desarrolladores](~/tabs/how-to/developer-tools.md) del explorador.

1. Vaya al [**portal para desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abra **Aplicaciones** y seleccione **Importar aplicación**.

<!--- TBD: This steps seems to be removed from main now so commenting it for now.

1. Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest. The name of your app package is `tab.zip`. It is available from the following path:
--->

1. El nombre del paquete de la aplicación es `tab.zip`. Está disponible en la siguiente ruta:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Seleccione `tab.zip` y ábralo en el portal para desarrolladores.

1. Se crea y rellena un **identificador de aplicación** predeterminado en la sección **Información básica**.

1. Agregue la descripción corta y larga de la aplicación en **Descripciones**.

1. En **Información del desarrollador**, agregue los detalles necesarios y, en **Sitio web (debe ser una dirección URL HTTPS válida)** proporcione la dirección URL HTTPS de ngrok.

1. En **Direcciones URL de la aplicación**, actualice la Directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso a `https://<yourngrokurl>/tou` y seleccione Guardar.

1. En **Características de la aplicación**, seleccione **Grupo y aplicación de canal**. Actualice la **Dirección URL de configuración** con `https://<yourngrokurl>/tab` y seleccione la pestaña **Ámbito**.

1. Seleccione **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Seleccione **Vista previa en Teams** desde la barra de herramientas del Portal para desarrolladores. El Portal para desarrolladores le informará que la aplicación fue transferida localmente de forma correcta. La página **Agregar** aparece para la aplicación en Teams.

1. Seleccione **Agregar al equipo** para configurar la pestaña en un equipo. Configure la pestaña y seleccione **Guardar**. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Pestaña de canal ASPNET cargada":::

    Ahora ha creado y agregado correctamente la pestaña de canal o grupo en Teams.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>Crear una pestaña personalizada de canal o grupo con ASP.NET Core MVC

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de la pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio con el siguiente comando o puede descargar el [ código fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Estos son los pasos para crear una pestaña de canal o grupo:

* [Generar la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab-2)
* [Establecer un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab-2)
* [Actualizar la aplicación](#update-your-application-1)
* [Compilar y ejecutar la aplicación](#build-and-run-your-application-2)
* [Actualizar el paquete de la aplicación con el portal para desarrolladores](#update-your-app-package-with-developer-portal-1)
* [Vista previa de la aplicación en Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generar la aplicación con una pestaña de canal o grupo

1. Abra Visual Studio y seleccione **Abrir un proyecto o solución**.

1. Vaya a la carpeta **Microsoft-Teams-Samples** > **samples** > **tab-channel-group** > **mvc-csharp** y abra **ChannelGroupTabMVC.sln**.

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar** de la aplicación para comprobar si la aplicación se ha cargado correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * `https://localhost:3978/`
    * `https://localhost:3978/privacy`
    * `https://localhost:3978/tou`

<details>
<summary><b>Revisar el código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto fue creado a partir de una plantilla de aplicación web vacía de ASP.NET Core 3.1 con la casilla **Avanzado - Configurar para HTTPS** seleccionada durante la configuración. Los servicios de MVC se registran mediante el método `ConfigureServices()` del marco de inserción de dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de los archivos estáticos se agrega al método `Configure()` mediante el código siguiente:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options => options.EnableEndpointRouting = false);
}

public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();
    app.UseMvc();
}
```

#### <a name="wwwroot-folder"></a>carpeta wwwroot

En ASP.NET Core, la carpeta raíz web es en donde la aplicación busca los archivos estáticos.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono a todo color** de 192 x 192 píxeles.
* Un **icono de contorno transparente** de 32 x 32 píxeles.
* Un archivo `manifest.json` que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña en Teams.

#### <a name="csproj"></a>.csproj

En la ventana Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto y seleccione **Editar archivo de proyecto**. Al final del archivo, verá el código siguiente que crea y actualiza la carpeta ZIP cuando se compila la aplicación:

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

Los controladores usan la propiedad `ViewBag` para transferir valores dinámicamente a las vistas.

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y tome nota de la dirección URL.

### <a name="update-your-application"></a>Actualizar la aplicación

1. Abra el Explorador de soluciones de Visual Studio, vaya a la carpeta **Views** > **Shared** y abra **_Layout.cshtml** y agregue lo siguiente a <head> la sección de etiquetas:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js"></script>
    ```

    > [!IMPORTANT]
    > No copie ni pegue las direcciones URL `<script src="...">` de esta página, ya que no representan la versión más reciente. Para obtener la versión más reciente del SDK, vaya siempre a la [API de JavaScript de Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js).

1. Inserte una llamada a `microsoftTeams.app.initialize();` en la etiqueta `script`.

1. En el Explorador de soluciones de Visual Studio vaya a la carpeta **Tab** y abra **Tab.cshtml**.

    En **Tab.cshtml** , la aplicación presenta al usuario dos opciones para mostrar la pestaña con un icono rojo o gris. El botón **Seleccionar gris** o **Seleccionar rojo** desencadena `saveGray()` o `saveRed()` , respectivamente, establece `pages.config.setValidityState(true)`y habilita **Guardar** en la página de configuración. Este código permite a Teams saber que ha completado la configuración de requisitos y puede continuar con la instalación. Se establecen los parámetros de `pages.config.setConfig`. Por último, se llama a `saveEvent.notifySuccess()` para indicar que la dirección URL de contenido se ha resuelto correctamente.

1. Actualice los valores `websiteUrl` y `contentUrl` en cada función con la dirección URL de ngrok HTTPS en la pestaña.

    El código ahora debe incluir lo siguiente con **y8rCgT2b** reemplazado por la dirección URL de ngrok:

    ```javascript

        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl:""
                });
                saveEvent.notifySuccess();
            });
        }
    
        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl:""
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. Asegúrese de guardar el archivo **Tab.cshtml** actualizado.

### <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar**.

1. Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

    > [!TIP]
    > Debe tener la aplicación en Visual Studio y ngrok en ejecución para completar los pasos proporcionados en este artículo. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**. Escucha y reanuda el enrutamiento de la solicitud de la aplicación cuando se reinicia en Visual Studio. Si tiene que reiniciar el servicio ngrok, devuelve una nueva dirección URL y tiene que actualizar la aplicación con la nueva dirección URL.

### <a name="update-your-app-package-with-developer-portal"></a>Actualizar el paquete de la aplicación con el portal para desarrolladores

1. Vaya a Teams. Si usa la [versión basada en la Web](https://teams.microsoft.com), puede inspeccionar el código front-end mediante las [herramientas para desarrolladores](~/tabs/how-to/developer-tools.md) del explorador.

1. Vaya al [**portal para desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abra **Aplicaciones** y seleccione **Importar aplicación**.

1. El nombre del paquete de la aplicación es **tab.zip**. Está disponible en la siguiente ruta:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Seleccione **tab.zip** y ábralo en el Portal para desarrolladores.

1. Se creará y se rellenará un **Id. de aplicación** predeterminado en la sección **Información básica**.

1. Agregue una Descripción corta y una Descripción larga para la aplicación en **Descripciones**.

1. En **Información del desarrollador**, agregue los detalles necesarios y en **Sitio web (debe ser una dirección URL HTTPS válida)**, proporcione la dirección URL HTTPS de ngrok.

1. En **Direcciones URL de la aplicación**, actualice la Directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso a `https://<yourngrokurl>/tou` y seleccione Guardar.

1. En **Características de la aplicación**, seleccione **Grupo y aplicación de canal**. Actualice la **Dirección URL de configuración** con `https://<yourngrokurl>/tab` y seleccione la pestaña **Ámbito**.

1. Seleccione **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Seleccione **Vista previa en Teams** desde la barra de herramientas del Portal para desarrolladores. El Portal para desarrolladores le informará que la aplicación fue transferida localmente de forma correcta. La página **Agregar** aparece para la aplicación en Teams.

1. Seleccione **Agregar al equipo** para configurar la pestaña en un equipo. Configure la pestaña y seleccione **Guardar**. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Pestaña de canal ASPNET MVC cargada":::

    Ahora ha creado y agregado correctamente la pestaña de canal o grupo en Teams.

::: zone-end

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Creación de una página de contenido](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>Consulte también

* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Crear una página de eliminación](~/tabs/how-to/create-tab-pages/removal-page.md)
* [Agregar una página de SharePoint como pestaña en Teams](https://support.microsoft.com/en-us/office/add-a-sharepoint-page-list-or-document-library-as-a-tab-in-teams-131edef1-455f-4c67-a8ce-efa2ebf25f0b)
