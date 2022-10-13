---
title: Crear una pestaña personal
author: laujan
description: Aprenda a crear una pestaña personal. Seleccione el entorno Node.js, ASP.NET Core o ASP.NET Core MVC. Genere la aplicación, agregue contenido, cree un paquete, compile y ejecute la aplicación.
ms.localizationpriority: high
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 187f1b40c60d8f7d88b75e6f666239ab70717cf6
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560739"
---
# <a name="create-a-personal-tab"></a>Crear una pestaña personal

Pestañas personales, junto con los bots de ámbito personal, forman parte de las aplicaciones personales y se limitan a un solo usuario. Se pueden anclar al panel izquierdo para facilitar su acceso. También puede [reordenar](#reorder-static-personal-tabs) sus pestañas personales.

Asegúrese de cumplir con todos los [requisitos previos](~/tabs/how-to/tab-requirements.md) para crear una pestaña personal.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Creación de una pestaña personal con Node.js

1. En el símbolo del sistema, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) escribiendo el siguiente comando después de instalar Node.js:

    ```cmd
    npm install yo gulp-cli --global
    ```

1. En el símbolo del sistema, instale el generador de aplicaciones de Microsoft Teams; para ello, escriba el siguiente comando:

    ```cmd
    npm install generator-teams --global
    ```

Estos son los pasos para crear una pestaña personal:

1. [Generar la aplicación con una pestaña personal](#generate-your-application-with-a-personal-tab)
1. [Agregar una página de contenido a la pestaña personal](#add-a-content-page-to-the-personal-tab)
1. [Crear el paquete de aplicación](#create-your-app-package)
1. [Compilar y ejecutar la aplicación](#build-and-run-your-application)
1. [Establezca un túnel seguro a la pestaña personal](#establish-a-secure-tunnel-to-your-tab)
1. [Cargar la aplicación en Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Generar la aplicación con una pestaña personal

1. En el símbolo del sistema, cree un directorio nuevo para su pestaña personal.

1. Escriba el siguiente comando en el nuevo directorio para iniciar el generador de aplicaciones de Microsoft Teams:

    ```cmd
    yo teams
    ```

1. Proporcione los valores a una serie de preguntas que le pide el generador de aplicaciones de Microsoft Teams para actualizar el `manifest.json` archivo.

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Generador de Teams":::

    <details>
    <summary><b>Serie de preguntas para actualizar el archivo manifest.json</b></summary>

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

      De forma predeterminada, el generador sugiere una dirección URL del sitio web de Azure. Solo está probando la aplicación localmente, por lo que no es necesaria ninguna dirección URL válida.

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

      Use las teclas de dirección para seleccionar **Personal (estático)**.

    * **¿Necesita compatibilidad con el inicio de sesión único de Microsoft Azure Active Directory (Azure AD) para la pestaña?**

      Elija **no** incluir compatibilidad con el inicio de sesión único de Azure AD para la pestaña. El valor predeterminado es sí, escriba **n**.
    > [!NOTE]
    > En una pestaña, la página principal de la pestaña aparece solo cuando el usuario selecciona el botón Atrás (o se mueve fuera de la pestaña) y vuelve a la página principal. La pestaña no mantiene ni conserva el estado anterior por diseño.
    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>Agregar una página de contenido a la pestaña personal

Cree una página de contenido y actualice los archivos existentes de la aplicación de la pestaña personal:

1. Cree un nuevo archivo **personal.html** en Visual Studio Code con la siguiente revisión:

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

1. Guarde **personal.html** en la carpeta **pública** de la aplicación en la siguiente ubicación:

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. Abra `manifest.json` desde la siguiente ubicación de Visual Studio Code:

    ```
     ./src/manifest/manifest.json
    ```

1. Agregue lo siguiente a la matriz vacía `staticTabs` (`staticTabs":[]`) y agregue el siguiente objeto JSON:

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
    > El componente de la ruta de acceso **yourDefaultTabNameTab** es el valor que especificó en el generador para el **Nombre de pestaña predeterminado** más la palabra **Tab**.
    >
    > Por ejemplo: DefaultTabName es **MyTab** luego, **/MyTabTab/**

1. Actualice el componente de la ruta de acceso **contentURL** **yourDefaultTabNameTab** con el nombre real de la pestaña.

1. Guarde el archivo `manifest.json` actualizado.

1. Abra **Tab.ts en el** Visual Studio Code desde la siguiente ruta de acceso para proporcionar la página de contenido en un iFrame:

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Agregue lo siguiente a la lista de decoradores de iFrame:

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. Guarde el archivo actualizado. El código de la pestaña se ha completado.

### <a name="create-your-app-package"></a>Crear el paquete de aplicación

Debe tener un paquete de aplicación para compilar y ejecutar la aplicación en Teams. El paquete de aplicación se crea a través de una tarea de Gulp que valida el archivo `manifest.json` y genera la carpeta zip en el directorio `./package`. En el símbolo del sistema, use el comando `gulp manifest`.

### <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

#### <a name="build-your-application"></a>Compilar la aplicación

Escriba el siguiente comando en el símbolo del sistema para transpilar la solución en la carpeta **./dist**:

```cmd
gulp build
```

#### <a name="run-your-application"></a>Ejecutar la aplicación

1. En el símbolo del sistema, escriba el siguiente comando para iniciar un servidor web local:

    ```cmd
    gulp serve
    ```

1. Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador para ver la página principal de la aplicación.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Pestaña predeterminada":::

1. Examine `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` para ver su pestaña personal.

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="Pestaña HTML predeterminada":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro a la pestaña

En el símbolo del sistema, salga del localhost y escriba el siguiente comando para establecer un túnel seguro a la pestaña:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Después de cargar la pestaña en Microsoft Teams a través de **ngrok** y una vez guardada correctamente, podrá verla en Teams hasta que finalice la sesión del túnel.

### <a name="upload-your-application-to-teams"></a>Cargar la aplicación en Teams

1. Vaya a Teams y seleccione **Aplicaciones**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Tienda de Teams":::.
1. Seleccione **Administrar las aplicaciones** > **Cargar una aplicación** > **Carga de una aplicación personalizada**.
1. Vaya al directorio del proyecto, examine la carpeta **./package**, seleccione la carpeta zip y elija **Abrir**.

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="Agregar la pestaña personal":::

1. Seleccione **Agregar** en el cuadro de diálogo. La pestaña se cargará en Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="Pestaña personal cargada":::

1. En el panel izquierdo de Teams, seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; y, a continuación, elija la aplicación cargada para ver su pestaña personal.

   Ahora ha creado y agregado correctamente su pestaña personal en Teams.
  
   Ahora que tiene su pestaña personal en Teams, también puede [reordenar](#reorder-static-personal-tabs) dicha pestaña.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>Crear una pestaña personal con ASP.NET Core

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio usando el siguiente comando o puede descargar el [código fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Estos son los pasos para crear una pestaña personal:

1. [Generar la aplicación con una pestaña personal](#generate-your-application-with-a-personal-tab-1)
1. [Actualizar y ejecutar la aplicación](#update-and-run-your-application)
1. [Establecer un túnel seguro a la pestaña](#establish-a-secure-tunnel-to-your-tab-1)
1. [Actualizar el paquete de la aplicación con el Portal para desarrolladores](#update-your-app-package-with-developer-portal)
1. [Vista previa de la aplicación en Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Generar la aplicación con una pestaña personal

1. Abra Visual Studio y seleccione **Abrir un proyecto o una solución**.

1. Vaya a la carpeta **Microsoft-Teams-Samples** > **samples** > **tab-personal** > **razor-csharp** y abra **PersonalTab.sln**.

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar** de la aplicación para comprobar si se cargó correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * `<http://localhost:3978/>`
    * `<http://localhost:3978/personalTab>`
    * `<http://localhost:3978/privacy>`
    * `<http://localhost:3978/tou>`

<details>
<summary><b>Revisar el código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto fue creado a partir de una plantilla de aplicación web vacía de ASP.NET Core 3.1 con la casilla **Avanzado - Configurar para HTTPS** seleccionada durante la configuración. Los servicios de MVC se registran mediante el método `ConfigureServices()` del marco de inserción de dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de los archivos estáticos se agrega al método `Configure()` mediante el código siguiente:

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

En ASP.NET Core, la carpeta raíz web es en donde la aplicación busca los archivos estáticos.

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core trata los archivos llamados **Index** como la página principal o predeterminada del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se muestra como la página principal de la aplicación.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un icono a todo color de 192 x 192 píxeles.
* Un icono de contorno transparente de 32 x 32 píxeles.
* Un archivo `manifest.json` que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos en la carga de la pestaña en Teams. Teams carga el `contentUrl` especificado en el manifiesto, lo inserta en un <iframe\> y lo representa en la pestaña.

#### <a name="csproj"></a>.csproj

En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto y seleccione **Editar archivo del proyecto**. Al final del archivo, verá el código siguiente que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

1. Abra el Explorador de soluciones de Visual Studio y vaya a la carpeta **Páginas** > **Compartido**, abra **_Layout.cshtml** y agregue lo siguiente a la sección de etiquetas `<head>`:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-QtTBFeFlfRDZBfwHJHYQp7MdLJ2C3sfAEB1Qpy+YblvjavBye+q87TELpTnvlXw4" crossorigin="anonymous"></script>
    ```

1. En Visual Studio Explorador de soluciones, abra **personalTab.cshtml desde la** carpeta **Pages** y agregue `microsoftTeams.app.initialize()` las `<script>` etiquetas.

1. Seleccione **Guardar**.

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar** de la aplicación.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro a la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Actualizar el paquete de la aplicación con el Portal para desarrolladores

1. Vaya al [**Portal para desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abra **Aplicaciones** y seleccione **Importar aplicación**.

1. El nombre del archivo del paquete de la aplicación es `tab.zip` y está disponible en la `/bin/Debug/netcoreapp3.1/tab.zip` ruta de acceso.

1. Seleccione `tab.zip` y ábralo en el Portal para desarrolladores.

1. Se creará y se rellenará un **Id. de aplicación** predeterminado en la sección **Información básica**.

1. Agregue una Descripción corta y una Descripción larga para la aplicación en **Descripciones**.

1. En **Información del desarrollador**, agregue los detalles necesarios y en **Sitio web (debe ser una dirección URL HTTPS válida)**, proporcione la dirección URL HTTPS de ngrok.

1. En **Direcciones URL de la aplicación**, actualice la directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso para `https://<yourngrokurl>/tou` y seleccione **Guardar**.

1. En **Características de la aplicación**, seleccione **Personal app** > **Create your first personal app tab (Creación de la primera pestaña de aplicación personal** ), escriba el nombre y actualice la **dirección URL de contenido** con `https://<yourngrokurl>/personalTab`. Deje el campo Url del sitio web en blanco, seleccione **Contexto** como personalTab en la lista desplegable y seleccione **Confirmar**.

1. Seleccione **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Seleccione **Vista previa en Teams** desde la barra de herramientas del Portal para desarrolladores. El Portal para desarrolladores le informará que la aplicación fue transferida localmente de forma correcta. La página **Agregar** aparecerá para la aplicación en Teams.

1. Seleccione **Agregar** para cargar la pestaña en Teams. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="Pestaña predeterminada":::

   Ahora ha creado y agregado correctamente su pestaña personal en Teams.
  
   Ahora que tiene su pestaña personal en Teams, también puede [reordenar](#reorder-static-personal-tabs) dicha pestaña.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>Crear una pestaña personal con ASP.NET Core MVC

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio usando el siguiente comando o puede descargar el [código fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Estos son los pasos para crear una pestaña personal:

1. [Generar la aplicación con una pestaña personal](#generate-your-application-with-a-personal-tab-2)
1. [Actualizar y ejecutar la aplicación](#update-and-run-your-application-1)
1. [Establecer un túnel seguro a la pestaña](#establish-a-secure-tunnel-to-your-tab-2)
1. [Actualizar el paquete de la aplicación con el Portal para desarrolladores](#update-your-app-package-with-developer-portal-1)
1. [Vista previa de la aplicación en Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>Generar la aplicación con una pestaña personal

1. Abra Visual Studio y seleccione **Abrir un proyecto o una solución**.

1. Vaya a la carpeta **Microsoft-Teams-Samples** > **samples** > **tab-personal** > **mvc-csharp** y abra **PersonalTabMVC.sln** en Visual Studio.

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar** de la aplicación para comprobar si se cargó correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * `<http://localhost:3978>`
    * `<http://localhost:3978/personalTab>`
    * `<http://localhost:3978/privacy>`
    * `<http://localhost:3978/tou>`

<details>
<summary><b>Revisar el código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto fue creado a partir de una plantilla de aplicación web vacía de ASP.NET Core 3.1 con la casilla **Avanzado - Configurar para HTTPS** seleccionada durante la configuración. Los servicios de MVC se registran mediante el método `ConfigureServices()` del marco de inserción de dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware de los archivos estáticos se agrega al método `Configure()` mediante el código siguiente:

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

En ASP.NET Core, la carpeta raíz web es en donde la aplicación busca los archivos estáticos.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono a todo color** de 192 x 192 píxeles.
* Un **icono de contorno transparente** de 32 x 32 píxeles.
* Un archivo `manifest.json` que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos en la carga de la pestaña en Teams. Teams carga el especificado en el `contentUrl` manifiesto, lo inserta en un iFrame y lo representa en la pestaña.

#### <a name="csproj"></a>.csproj

En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto y seleccione **Editar archivo del proyecto**. Al final del archivo, verá el código siguiente que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

**PersonalTab.cs** presenta un objeto de mensaje y métodos a los que se llama desde **PersonalTabController** cuando un usuario selecciona un botón en la vista **PersonalTab**.

#### <a name="views"></a>Vistas

Estas son las diferentes vistas de ASP.NET Core MVC:

* Inicio: ASP.NET Core trata los archivos llamados **Index** como la página principal o predeterminada del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se muestra como la página principal de la aplicación.

* Compartido: La revisión de vista parcial **_Layout.cshtml** contiene la estructura general de la página de la aplicación y los elementos visuales compartidos. También hace referencia a la biblioteca de Teams.

#### <a name="controllers"></a>Controladores

Los controladores usan la propiedad `ViewBag` para transferir valores dinámicamente a las Vistas.

</details>

### <a name="update-and-run-your-application"></a>Actualizar y ejecutar la aplicación

1. Abra el Explorador de soluciones de Visual Studio, vaya a la carpeta **Vistas** > **Compartido**, abra **_Layout.cshtml** y agregue lo siguiente a la sección de etiquetas `<head>`:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-QtTBFeFlfRDZBfwHJHYQp7MdLJ2C3sfAEB1Qpy+YblvjavBye+q87TELpTnvlXw4" crossorigin="anonymous"></script>
    ```

1. En Visual Studio Explorador de soluciones, abra **PersonalTab.cshtml** desde la carpeta **Views** > **PersonalTab** y agregue `microsoftTeams.app.initialize()` dentro de las `<script>` etiquetas.

1. Seleccione **Guardar**.

1. En Visual Studio, seleccione **F5** o elija **Iniciar depuración** en el menú **Depurar** de la aplicación.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro a la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Actualizar el paquete de la aplicación con el Portal para desarrolladores

1. Vaya al [**Portal para desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abra **Aplicaciones** y seleccione **Importar aplicación**.

1. El nombre del paquete de la aplicación es **tab.zip**. Está disponible en la siguiente ruta:

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Seleccione **tab.zip** y ábralo en el Portal para desarrolladores.

1. Se creará y se rellenará un **Id. de aplicación** predeterminado en la sección **Información básica**.

1. Agregue una Descripción corta y una Descripción larga para la aplicación en **Descripciones**.

1. En **Información del desarrollador**, agregue los detalles necesarios y, en **Sitio web (debe ser una dirección URL HTTPS válida),** proporcione la dirección URL HTTPS de ngrok.

1. En **Direcciones URL de la aplicación**, actualice la directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso para `https://<yourngrokurl>/tou` y seleccione **Guardar**.

1. En **Características de la aplicación**, seleccione **Personal app** > **Create your first personal app tab (Creación de la primera pestaña de aplicación personal** ), escriba el nombre y actualice la **dirección URL de contenido** con `https://<yourngrokurl>/personalTab`. Deje el campo Url del sitio web en blanco, seleccione **Contexto** como personalTab en la lista desplegable y seleccione **Confirmar**.

1. Seleccione **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Seleccione **Vista previa en Teams** desde la barra de herramientas del Portal para desarrolladores. El Portal para desarrolladores le informará que la aplicación fue transferida localmente de forma correcta. La página **Agregar** aparecerá para la aplicación en Teams.

1. Seleccione **Agregar** para cargar la pestaña en Teams. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="Pestaña personal":::
  
   Ahora ha creado y agregado correctamente su pestaña personal en Teams.

   Ahora que tiene su pestaña personal en Teams, también puede [reordenar](#reorder-static-personal-tabs) dicha pestaña.

::: zone-end

## <a name="reorder-static-personal-tabs"></a>Reordenar las pestañas personales estáticas

A partir de la versión 1.7 del manifiesto, los desarrolladores podrán reorganizar todas las pestañas de su aplicación personal. Puede mover la pestaña **de chat del bot** , que siempre se establece de forma predeterminada en la primera posición, en cualquier lugar del encabezado de la pestaña de la aplicación personal. Se declaran dos palabras clave `entityId` reservadas para la pestaña, **conversaciones** y **Acerca de**.

Si crea un bot con un ámbito **personal**, aparecerá en la primera posición de pestaña de la aplicación personal de forma predeterminada. Si desea moverlo a otra posición, debe agregar un objeto de pestaña estática al manifiesto con la palabra clave reservada, **conversaciones**. La pestaña **conversación** aparecerá en la web o en el escritorio en función de dónde agregue la pestaña de **conversación** en la matriz `staticTabs`.

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

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una pestaña de grupo o de canal](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Consulte también

* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Crear pestañas de conversación](~/tabs/how-to/conversational-tabs.md)
* [Compartir en Teams desde una aplicación personal o una pestaña](~/concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md)
