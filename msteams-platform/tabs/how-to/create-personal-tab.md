---
title: Crear una pestaña personal
author: laujan
description: 'Una guía de inicio rápido para crear una pestaña personal con el Generador de Yeoman, ASP.NET Core o ASP.NET Core MVC para Microsoft Teams usar Node.js y actualizar el manifiesto de la aplicación.'
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET almacén de permisos de dominio de conversación de aplicación de paquete MVC
zone_pivot_groups: teams-app-environment
---

# <a name="create-a-personal-tab"></a>Crear una pestaña personal

Pestañas personales, junto con los bots de ámbito personal, forman parte de las aplicaciones personales y se limitan a un solo usuario. Se pueden anclar al panel izquierdo para facilitar el acceso. También puede [reordenar](#reorder-static-personal-tabs) y agregar [`registerOnFocused` api para](#add-registeronfocused-api-for-tabs-or-personal-apps) pestañas personales.

Asegúrese de que tiene todos los [prerequisitos para](~/tabs/how-to/tab-requirements.md) crear la pestaña personal.

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Crear una pestaña personal con Node.js

1. En el símbolo del sistema, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) especificando el siguiente comando después de instalar el Node.js:

    ```cmd
    npm install yo gulp-cli --global
    ```

1. En el símbolo del sistema, Microsoft Teams generador de aplicaciones especificando el siguiente comando:

    ```cmd
    npm install generator-teams --global
    ```

A continuación se indican los pasos para crear una pestaña personal:

1. [Generar la aplicación con una pestaña personal](#generate-your-application-with-a-personal-tab)
1. [Agregar una página de contenido a la pestaña personal](#add-a-content-page-to-the-personal-tab)
1. [Crear el paquete de aplicación](#create-your-app-package)
1. [Compilar y ejecutar la aplicación](#build-and-run-your-application)
1. [Establecer un túnel seguro en la pestaña personal](#establish-a-secure-tunnel-to-your-tab)
1. [Upload la aplicación a Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Generar la aplicación con una pestaña personal

1. En el símbolo del sistema, cree un nuevo directorio para la pestaña personal.

1. Escriba el siguiente comando en el nuevo directorio para iniciar el generador Microsoft Teams aplicación:

    ```cmd
    yo teams
    ```

1. Proporcione los valores a una serie de preguntas que Microsoft Teams generador de aplicaciones para actualizar el **archivo manifest.json**.

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Teams generador de Teams de datos" border="true":::

    <details>
    <summary><b>Serie de preguntas para actualizar el archivo manifest.json</b></summary>

    * **¿Cómo se llama su solución?**

      El nombre de la solución es el nombre del proyecto. Puede aceptar el nombre sugerido seleccionando **Entrar**.

    * **¿Dónde desea ubicar los archivos?**

      Actualmente está en el directorio del proyecto. Seleccione **Entrar**.

    * **¿Título del proyecto Microsoft Teams aplicación?**

      El título es el nombre del paquete de la aplicación y se usa en el manifiesto y la descripción de la aplicación. Escriba un título o **seleccione Entrar** para aceptar el nombre predeterminado.

    * **¿Su nombre (empresa)? (máximo 32 caracteres)**

      El nombre de la empresa se usará en el manifiesto de la aplicación. Escriba un nombre de empresa o **seleccione Entrar** para aceptar el nombre predeterminado.

    * **¿Qué versión de manifiesto le gustaría usar?**

      Seleccione el esquema predeterminado.

    * **¿Scaffolding rápido? (Y/n)**

      El valor predeterminado es sí; escriba **n** para escribir su id. de partner de Microsoft.

    * **Escriba su id. de partner de Microsoft, si tiene uno. (Dejar en blanco para omitir)**

      Este campo no es necesario y debe usarse solo si ya forma parte de la [Red de partners de Microsoft](https://partner.microsoft.com).

    * **¿Qué desea agregar al proyecto?**

      Seleccione **( &ast; ) Una pestaña**.

    * **¿La dirección URL donde hospedará esta solución?**

      De forma predeterminada, el generador sugiere una dirección URL de sitios web de Azure. Solo estás probando la aplicación localmente, por lo que no es necesaria una dirección URL válida.

    * **¿Desea mostrar un indicador de carga cuando se carga la aplicación o pestaña?**

      Elige **no incluir** un indicador de carga cuando se cargue la aplicación o la pestaña. El valor predeterminado es no, escriba **n**.

    * **¿Desea que las aplicaciones personales se representen sin una barra de encabezado de pestaña?**

      Elige **no incluir** aplicaciones personales que se representarán sin una barra de encabezado de pestaña. El valor predeterminado es no, escriba **n**.

    * **¿Desea incluir el marco de pruebas y las pruebas iniciales? (y/N)**

      Elija **no incluir** un marco de prueba para este proyecto. El valor predeterminado es no, escriba **n**.

    * **¿Desea incluir la compatibilidad con ESLint? (y/N)**

      Elija no incluir la compatibilidad con ESLint. El valor predeterminado es no, escriba **n**.

    * **¿Desea usar azure applications Ideas para telemetría? (y/N)**

      Elija **no** [incluir Aplicación de Azure Ideas](/azure/azure-monitor/app/app-insights-overview). El valor predeterminado es no; escriba **n**.

    * **Nombre de tabulación predeterminado (máximo 16 caracteres)?**

      Asigne un nombre a la pestaña. Este nombre de pestaña se usa en todo el proyecto como un componente de ruta de acceso de dirección URL o archivo.

    * **¿Qué tipo de tab le gustaría crear?**

      Use las teclas de flecha para **seleccionar Personal (estático).**.

    * **¿Necesita Microsoft Azure Active Directory (Azure AD) de inicio de sesión único para la pestaña?**

      Elija **no** incluir la Azure AD inicio de sesión único para la pestaña. El valor predeterminado es sí, escriba **n**.

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>Agregar una página de contenido a la pestaña personal

Cree una página de contenido y actualice los archivos existentes de la aplicación de pestaña personal:

1. Cree un nuevo **archivopersonal.html** en su Visual Studio Code con el siguiente marcado:

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

1. Guarde **personal.html** en la **carpeta pública de** la aplicación en la siguiente ubicación:

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. Abra **manifest.json** desde la siguiente ubicación en su Visual Studio Code:

    ```
     ./src/manifest/manifest.json
    ```

1. Agregue lo siguiente a la matriz `staticTabs` vacía (`staticTabs":[]`) y agregue el siguiente objeto JSON:

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{PUBLIC_HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{PUBLIC_HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

    > [!IMPORTANT]
    > El componente de **ruta de acceso yourDefaultTabNameTab** es el valor que escribió en el generador **para Nombre de tabulación** predeterminado más la palabra **Tab**.
    >
    > Por ejemplo: DefaultTabName es **MyTab** y **luego /MyTabTab/**

1. Actualice el **componente de ruta de acceso contentURL** **yourDefaultTabNameTab** con el nombre de pestaña real.

1. Guarde el archivo **manifest.json** actualizado.

1. Abra **Tab.ts** en su Visual Studio Code de la siguiente ruta de acceso para proporcionar la página de contenido en un IFrame:

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Agregue lo siguiente a la lista de decoradores de IFrame:

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. Guarde el archivo actualizado. El código de pestaña se ha completado.

### <a name="create-your-app-package"></a>Crear el paquete de aplicación

Debes tener un paquete de aplicación para compilar y ejecutar la aplicación en Teams. El paquete de la aplicación se crea a través de una tarea gulp que valida el archivo **manifest.json** y genera la carpeta zip en el **directorio ./package** . En el símbolo del sistema, escriba el comando siguiente:

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

#### <a name="build-your-application"></a>Compilar la aplicación

Escriba el siguiente comando en el símbolo del sistema para transpilar la solución en la **carpeta ./dist** :

```cmd
gulp build
```

#### <a name="run-your-application"></a>Ejecutar la aplicación

1. En el símbolo del sistema, escriba el siguiente comando para iniciar un servidor web local:

    ```cmd
    gulp serve
    ```

1. Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador para ver la página principal de la aplicación.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Ficha predeterminada" border="true":::

1. Examinar `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`, para ver la pestaña personal.

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="Pestaña html predeterminada" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

En el símbolo del sistema, salga del localhost y escriba el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Después de cargar la pestaña en Microsoft Teams a través de **ngrok** y guardarla correctamente, puede verlo en Teams hasta que finalice la sesión del túnel.

### <a name="upload-your-application-to-teams"></a>Upload la aplicación a Teams

1. Ve a Microsoft Teams y selecciona **Store**&nbsp; :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Selecciona **Administrar aplicaciones**
1. Selecciona **Publicar una aplicación** **y Upload una aplicación personalizada**.

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="Upload aplicación personalizada" border="true":::

1. Vaya al directorio del proyecto, vaya a **la carpeta ./package** , seleccione la carpeta zip y elija **Abrir**.

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="Agregar la pestaña personal" border="true":::

1. Seleccione **Agregar** en el cuadro de diálogo. La pestaña se carga en Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="Pestaña personal cargada" border="true":::

1. En el panel izquierdo de Teams, selecciona puntos suspensivos &#x25CF;&#x25CF;&#x25CF; y, a continuación, elige la aplicación cargada para ver tu pestaña personal.

   Ahora ha creado correctamente y agregado su pestaña personal en Teams.
  
   Al tener la pestaña personal en Teams, también puede [reordenar](#reorder-static-personal-tabs) y agregar [`registerOnFocused` API](#add-registeronfocused-api-for-tabs-or-personal-apps) para su pestaña personal.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>Crear una pestaña personal con ASP.NET Core

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio con el siguiente comando o puede descargar el código [fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

A continuación se indican los pasos para crear una pestaña personal:

1. [Generar la aplicación con una pestaña personal](#generate-your-application-with-a-personal-tab-1)
1. [Actualizar y ejecutar la aplicación](#update-and-run-your-application)
1. [Establecer un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab-1)
1. [Actualizar el paquete de la aplicación con el Portal de desarrolladores](#update-your-app-package-with-developer-portal)
1. [Vista previa de la aplicación en Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Generar la aplicación con una pestaña personal

1. Abra Visual Studio y seleccione **Abrir un proyecto o solución**.

1. Vaya a **la carpeta Microsoft-Teams-Samplessamplestab-personalrazor-csharp** >  >  >  y abra **PersonalTab.sln**.

1. En Visual Studio, seleccione **F5** o elija Iniciar depuración en el menú Depurar **de** la aplicación para  comprobar si la aplicación se ha cargado correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Revisar el código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto se creó a partir ASP.NET Core plantilla vacía de una aplicación web 3.1 con la casilla Avanzadas **- Configurar para HTTPS** activada en el programa de instalación. Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware `Configure()` de archivos estáticos se agrega al método con el código siguiente:

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

ASP.NET Core trata los archivos denominados **Index** como la página predeterminada o principal del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se muestra como la página principal de la aplicación.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono de color completo** que mide 192 x 192 píxeles.
* Un **icono de esquema transparente** que mide 32 x 32 píxeles.
* Un **archivo manifest.json** que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de la aplicación para usarlos al cargar la pestaña a Teams. Microsoft Teams carga el `contentUrl` especificado en el manifiesto, lo inserta en un iframe\> <y lo representa en la pestaña.

#### <a name="csproj"></a>.csproj

En Visual Studio Explorador de soluciones, haga clic con el botón secundario en el proyecto y seleccione **Editar Project archivo**. Al final del archivo, puede ver el siguiente código que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

### <a name="update-and-run-your-application"></a>Actualizar y ejecutar la aplicación

1. Abra Visual Studio Explorador de soluciones y vaya a La carpeta **PagesShared** > , abra **_Layout.cshtml** y agregue lo siguiente a la sección `<head>` etiquetas:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. En Visual Studio Explorador de soluciones **abra PersonalTab.cshtml** desde la carpeta **Pages** y agregue `microsoftTeams.initialize()` las etiquetas `<script>` y guarde.

1. En Visual Studio, seleccione **F5** o **elija Iniciar depuración** en el menú **Depurar de la** aplicación.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Actualizar el paquete de la aplicación con el Portal de desarrolladores

1. Vaya a [**Portal de desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abre **Aplicaciones y** selecciona **Importar aplicación**.

1. El nombre del paquete de la **aplicación estab.zip**. Está disponible en la siguiente ruta de acceso:

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Seleccione **tab.zip** y ábralo en el Portal de desarrolladores.

1. Se crea **un identificador de** aplicación predeterminado y se rellena en **la sección Información** básica.

1. Agrega la descripción corta y larga de la aplicación en **Descripciones**.

1. En **Información para desarrolladores**, agrega los detalles necesarios y en **Sitio web (debe** ser una dirección URL HTTPS válida) proporciona la dirección URL HTTPS de ngrok.

1. En **las direcciones URL de la** aplicación, actualice la directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso para `https://<yourngrokurl>/tou` guardar y guardar.

1. En **Características de la** aplicación, **selecciona Aplicación personalCrear** >  la **primera pestaña de la aplicación personal** y escribe el nombre y actualiza la **dirección URL de** contenido con `https://<yourngrokurl>/personalTab`. Deje el campo Dirección URL del sitio web en blanco y seleccione **Contexto** como personalTab de la lista desplegable y **Agregar**.

1. Seleccione **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Selecciona **Vista previa en Teams** de la barra de herramientas del Portal de desarrolladores, Portal para desarrolladores te informa de que la aplicación se ha descargado correctamente. La **página** Agregar aparece para la aplicación en Teams.

1. Seleccione **Agregar** para cargar la pestaña en Teams. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="Ficha predeterminada" border="true":::

   Ahora ha creado correctamente y agregado su pestaña personal en Teams.
  
   Al tener la pestaña personal en Teams, también puede [reordenar](#reorder-static-personal-tabs) y agregar [`registerOnFocused` API](#add-registeronfocused-api-for-tabs-or-personal-apps) para su pestaña personal.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>Crear una pestaña personal con ASP.NET Core MVC

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio con el siguiente comando o puede descargar el código [fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

A continuación se indican los pasos para crear una pestaña personal:

1. [Generar la aplicación con una pestaña personal](#generate-your-application-with-a-personal-tab-2)
1. [Actualizar y ejecutar aplicación](#update-and-run-your-application-1)
1. [Establecer un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab-2)
1. [Actualizar el paquete de la aplicación con el Portal de desarrolladores](#update-your-app-package-with-developer-portal-1)
1. [Vista previa de la aplicación en Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>Generar la aplicación con una pestaña personal

1. Abra Visual Studio y seleccione **Abrir un proyecto o solución**.

1. Vaya a **la carpeta Microsoft-Teams-Samplessamplestab-personalmvc-csharp** >  >  >  y abra **PersonalTabMVC.sln** en Visual Studio.

1. En Visual Studio, seleccione **F5** o elija Iniciar depuración en el menú Depurar **de** la aplicación para  comprobar si la aplicación se ha cargado correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Revisar el código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto se creó a partir ASP.NET Core plantilla vacía de una aplicación web 3.1 con la casilla Avanzadas **- Configurar para HTTPS** activada en el programa de instalación. Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware `Configure()` de archivos estáticos se agrega al método con el código siguiente:

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

#### <a name="wwwroot-folder"></a>carpeta wwwroot

En ASP.NET Core, la carpeta raíz web es donde la aplicación busca archivos estáticos.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono de color completo** que mide 192 x 192 píxeles.
* Un **icono de esquema transparente** que mide 32 x 32 píxeles.
* Un **archivo manifest.json** que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de la aplicación para usarlos al cargar la pestaña a Teams. Microsoft Teams carga el `contentUrl` especificado en el manifiesto, lo inserta en un IFrame y lo representa en la pestaña.

#### <a name="csproj"></a>.csproj

En el Visual Studio Explorador de soluciones, haga clic con el botón secundario en el proyecto y seleccione **Editar Project archivo**. Al final del archivo, verá el siguiente código que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

#### <a name="models"></a>Modelos

**PersonalTab.cs** presenta un objeto de mensaje y métodos a los que se llama desde **PersonalTabController** cuando un usuario selecciona un botón en la **vista PersonalTab** .

#### <a name="views"></a>Vistas

Estas vistas son las diferentes vistas de ASP.NET Core MVC:

* Inicio: ASP.NET Core trata los archivos denominados **Index** como la página predeterminada o principal del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se muestra como la página principal de la aplicación.

* Shared: el marcado de vista **parcial _Layout.cshtml** contiene la estructura de página general de la aplicación y los elementos visuales compartidos. También hace referencia a la Teams biblioteca.

#### <a name="controllers"></a>Controladores

Los controladores usan la propiedad `ViewBag` para transferir valores dinámicamente a las vistas.

</details>

### <a name="update-and-run-your-application"></a>Actualizar y ejecutar la aplicación

1. Abra Visual Studio Explorador de soluciones vaya a **la carpeta** **ViewsShared** >  y **abra _Layout.cshtml** y agregue lo siguiente a la sección `<head>` etiquetas:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. En Visual Studio Explorador de soluciones **abra PersonalTab.cshtml** desde **la carpeta** **ViewsPersonalTab** >  y agregue `microsoftTeams.initialize()` dentro de las etiquetas `<script>` y guarde.

1. En Visual Studio, seleccione **F5** o **elija Iniciar depuración** en el menú **Depurar de la** aplicación.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Actualizar el paquete de la aplicación con el Portal de desarrolladores

1. Vaya a [**Portal de desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abre **Aplicaciones y** selecciona **Importar aplicación**.

1. El nombre del paquete de la **aplicación estab.zip**. Está disponible en la siguiente ruta de acceso:

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Seleccione **tab.zip** y ábralo en el Portal de desarrolladores.

1. Se crea **un identificador de** aplicación predeterminado y se rellena en **la sección Información** básica.

1. Agrega la descripción corta y larga de la aplicación en **Descripciones**.

1. En **Información para desarrolladores**, agrega los detalles necesarios y en **Sitio web (debe** ser una dirección URL HTTPS válida) proporciona la dirección URL HTTPS de ngrok.

1. En **las direcciones URL de la** aplicación, actualice la directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso para `https://<yourngrokurl>/tou` guardar y guardar.

1. En **Características de la** aplicación, **selecciona Aplicación personalCrear** >  la **primera pestaña de la aplicación personal** y escribe el nombre y actualiza la **dirección URL de** contenido con `https://<yourngrokurl>/personalTab`. Deje el campo Dirección URL del sitio web en blanco y seleccione **Contexto** como personalTab de la lista desplegable y **Agregar**.

1. Seleccione **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Selecciona **Vista previa en Teams** de la barra de herramientas del Portal de desarrolladores, Portal para desarrolladores te informa de que la aplicación se ha descargado correctamente. La **página** Agregar aparece para la aplicación en Teams.

1. Seleccione **Agregar** para cargar la pestaña en Teams. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="Pestaña personal" border="true":::
  
   Ahora ha creado correctamente y agregado su pestaña personal en Teams.

   Al tener la pestaña personal en Teams, también puede [reordenar](#reorder-static-personal-tabs) y agregar [`registerOnFocused` API](#add-registeronfocused-api-for-tabs-or-personal-apps) para su pestaña personal.

::: zone-end

## <a name="reorder-static-personal-tabs"></a>Reordenar pestañas personales estáticas

A partir de la versión 1.7 del manifiesto, los desarrolladores pueden reorganizar todas las pestañas de su aplicación personal. En concreto, un desarrollador puede mover la pestaña de **chat del bot** , que siempre se sitúa de forma predeterminada en la primera posición, en cualquier lugar del encabezado de pestaña de la aplicación personal. Se declaran dos palabras `entityId` clave de tabulación reservadas, **conversaciones** y **acerca de.**

Si creas un bot con un **ámbito personal** , aparece en la primera posición de pestaña de una aplicación personal de forma predeterminada. Si desea moverlo a otra posición, debe agregar un objeto tab estático al manifiesto con la palabra clave reservada, **conversaciones**. La **pestaña de** conversación aparece en la web o en el escritorio en función de dónde agregue la **pestaña de** conversación en la `staticTabs` matriz.

``` JSON

{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}

```

## <a name="add-registeronfocused-api-for-tabs-or-personal-apps"></a>Agregar `registerOnFocused` API para pestañas o aplicaciones personales

La `registerOnFocused` API del SDK le permite usar un teclado en Teams. Puedes volver a una aplicación personal y mantener el foco en una pestaña o aplicación personal con la ayuda de las teclas Ctrl, Mayús y F6. Por ejemplo, puedes alejarte de la aplicación personal para buscar algo y luego volver a la aplicación personal o usar Ctrl+F6 para desplazarte por los lugares requeridos.

El código siguiente proporciona un ejemplo de definición de controlador en `registerFocusEnterHandler` SDK cuando el foco debe devolverse a la pestaña o a la aplicación personal:

``` C#

export function registerFocusEnterHandler(handler: (navigateForward: boolean) => void): 
void {
  HandlersPrivate.focusEnterHandler = handler;
  handler && sendMessageToParent('registerHandler', ['focusEnter']);
}
function handleFocusEnter(navigateForward: boolean): void
 {
  if (HandlersPrivate.focusEnterHandler)
   {
    HandlersPrivate.focusEnterHandler(navigateForward);
  }
}

```

Después de que el controlador se desencadene con la palabra `focusEnter`clave , `registerFocusEnterHandler` el controlador se invoca con una función de `focusEnterHandler` devolución de llamada que toma un parámetro denominado `navigateForward`. El valor de `navigateForward` determina el tipo de eventos. Ctrl `focusEnterHandler` +F6 invoca el valor solo y no la tecla de tabulación.
Las claves útiles para mover eventos dentro Teams son las siguientes:

* Evento Forward: Ctrl+F6 keys
* Evento Backward: Teclas Ctrl+Mayús+F6

``` C#

case 'focusEnter':     
this.registerFocusEnterHandler((navigateForward: boolean = true) => {
this.sdkWindowMessageHandler.sendRequestMessage(this.frame, this.constants.SdkMessageTypes.focusEnter, [navigateForward]);
// Set focus on iframe or webview
if (this.frame && this.frame.sourceElem) {
  this.frame.sourceElem.focus();
}
return true;
});
}

// callback function to be passed to the handler
private focusEnterHandler: (navigateForward: boolean) => boolean;

// function that gets invoked after handler is registered.
private registerFocusEnterHandler(focusEnterHandler: (navigateForward: boolean) => boolean): void {
this.focusEnterHandler = focusEnterHandler;
this.layoutService.registerAppFocusEnterCallback(this.focusEnterHandler);
}

```

### <a name="personal-app"></a>Aplicación personal

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="En el ejemplo se muestran las opciones para agregar la API registerOnFocussed" border="true":::

#### <a name="personal-app-forward-event"></a>Aplicación personal: evento Forward

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="En el ejemplo se muestran las opciones para agregar el movimiento hacia delante de la API registerOnFocussed" border="true":::

#### <a name="personal-app-backward-event"></a>Aplicación personal: evento Backward

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="En el ejemplo se muestran las opciones para agregar el movimiento hacia atrás de la API registerOnFocussed" border="true":::

### <a name="tab"></a>Pestaña

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="En el ejemplo se muestran las opciones para agregar la API registerOnFocussed para la pestaña" border="true":::

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Vea también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Crear pestañas de conversación](~/tabs/how-to/conversational-tabs.md)
