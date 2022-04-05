---
title: Crear una pestaña de canal o grupo
author: laujan
description: 'Guía de inicio rápido para crear una pestaña de canal y grupo con el Generador de Yeoman para Microsoft Teams, incluida la revisión del código fuente con ejemplos de código.'
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
---

# <a name="channel-or-group-tab"></a>Pestaña Canal o grupo

Pestañas de canal o grupo entregar contenido a canales y chats grupales, y son una excelente manera de crear espacios de colaboración en torno a contenido dedicado basado en web.

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Crear una pestaña de canal o grupo personalizada con Node.js

1. En el símbolo del sistema, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) especificando el siguiente comando después de instalar el **Node.js**:

    ```cmd
    npm install yo gulp-cli --global
    ```

2. En el símbolo del sistema, Microsoft Teams generador de aplicaciones especificando el siguiente comando:

    ```cmd
    npm install generator-teams --global
    ```

A continuación se indican los pasos para crear una pestaña de canal o grupo:

* [Generar la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab)
* [Crear el paquete de aplicación](#create-your-app-package)
* [Compilar y ejecutar la aplicación](#build-and-run-your-application)
* [Establecer un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab)
* [Upload la aplicación a Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generar la aplicación con una pestaña de canal o grupo

1. En el símbolo del sistema, cree un nuevo directorio para la pestaña canal o grupo.

1. Escriba el siguiente comando en el nuevo directorio para iniciar el generador Microsoft Teams aplicación:

    ```cmd
    yo teams
    ```

1. Proporcione los valores a una serie de preguntas que Microsoft Teams generador de aplicaciones para actualizar el **archivo manifest.json**:

    ![captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

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

        Use las teclas de flecha para seleccionar **Ficha Configurable** .

    * **¿Qué ámbitos tiene previsto usar para la pestaña?**

        Puede seleccionar un equipo o un chat de grupo.

    * **¿Necesita Microsoft Azure Active Directory (Azure AD) de inicio de sesión único para la pestaña?**

        Elija **no** incluir la Microsoft Azure Active Directory inicio de sesión único (Azure AD) para la pestaña. El valor predeterminado es sí, escriba **n**.

    * **¿Desea que esta pestaña esté disponible en SharePoint Online? (Y/n)**

        Escriba **n**.

    </details>

> [!IMPORTANT]
> El componente de **ruta de acceso yourDefaultTabNameTab** es el valor que escribió en el generador **para Nombre de tabulación** predeterminado más la palabra **Tab**.
>
> Por ejemplo: DefaultTabName es **MyTab** y **luego /MyTabTab/**

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

    ```bash
    gulp serve
    ```

1. Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador para ver la página principal de la aplicación.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Ficha predeterminada" border="true":::

1. Para ver la página de configuración de pestañas, vaya a `http://localhost:3007/<yourDefaultAppNameTab>/config.html`. Se muestra lo siguiente:

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="Página de configuración de tabulación" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

Para establecer un túnel seguro en la pestaña, salga del localhost y escriba el siguiente comando:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Después de cargar la pestaña en Microsoft Teams a través de **ngrok** y guardarla correctamente, puede verlo en Teams hasta que finalice la sesión del túnel. Si reinicias la sesión de ngrok, debes actualizar la aplicación con la nueva dirección URL.

### <a name="upload-your-application-to-teams"></a>Upload la aplicación a Teams

1. Ve a Microsoft Teams y selecciona **Store**&nbsp; :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Selecciona **Administrar aplicaciones**.
1. Selecciona **Publicar una aplicación** **y Upload una aplicación personalizada**.

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="Upload aplicación personalizada" border="true":::

1. Vaya al directorio del proyecto, vaya a **la carpeta ./package** , seleccione la carpeta zip del paquete de la aplicación y elija **Abrir**.
    
    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="Pestaña Canal cargado" border="true":::

1. Seleccione **Agregar** en el cuadro de diálogo. La pestaña se carga en Teams.
    
    > [!NOTE]
    > Si  **Add** no se muestra en el cuadro de diálogo, quite el siguiente código del manifiesto de la carpeta zip del paquete de la aplicación cargada. Vuelva a comprimir la carpeta y cargarla en Teams.
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. Siga las instrucciones para agregar una pestaña. Hay un cuadro de diálogo de configuración personalizado para la pestaña canal o grupo.
1. Selecciona **Guardar** y la pestaña se agrega a la barra de pestañas del canal.

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="Pestaña Canal cargada" border="true":::
    
    Ahora ha creado y agregado correctamente la pestaña canal o grupo en Teams.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>Crear una pestaña de canal o grupo personalizada con ASP.NET Core

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio con el siguiente comando o puede descargar el código [fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

A continuación se indican los pasos para crear una pestaña de canal o grupo:

* [Generar la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab-1)
* [Establecer un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab-1)
* [Actualizar la aplicación](#update-your-application)
* [Compilar y ejecutar la aplicación](#build-and-run-your-application-1)
* [Actualizar el paquete de la aplicación con el Portal de desarrolladores](#update-your-app-package-with-developer-portal)
* [Vista previa de la aplicación en Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generar la aplicación con una pestaña de canal o grupo

1. Abra Visual Studio y seleccione **Abrir un proyecto o solución**.

1. Vaya a **la carpeta Microsoft-Teams-Samplessamplestab-channel-grouprazor-csharp** >  >  >  y **abra channelGroupTab.sln**.

1. En Visual Studio, seleccione **F5** o elija Iniciar depuración en el menú Depurar **de** la aplicación para  comprobar si la aplicación se ha cargado correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Revisar el código fuente</b></summary>

#### <a name="startupcs"></a>Startup.cs

Este proyecto se creó a partir de una plantilla vacía ASP.NET Core aplicación web 3.1 con la casilla Configuración avanzada *** para HTTPS** activada en el programa de instalación. Los servicios MVC están registrados por el método del marco de inserción de `ConfigureServices()` dependencias. Además, la plantilla vacía no habilita el servicio de contenido estático de forma predeterminada, por lo que el middleware `Configure()` de archivos estáticos se agrega al método con el código siguiente:

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

#### <a name="tabcs"></a>Tab.cs

Este C# contiene un método al que se llama desde **Tab.cshtml durante** la configuración.

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono de color completo** que mide 192 x 192 píxeles.
* Un **icono de esquema transparente** que mide 32 x 32 píxeles.
* Un **archivo manifest.json** que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña en Teams. Cuando un usuario elige agregar o actualizar la pestaña, Microsoft Teams `configurationUrl` carga el especificado en el manifiesto, lo inserta en un IFrame y lo representa en la pestaña.

#### <a name="csproj"></a>.csproj

En la Visual Studio Explorador de soluciones, haga clic con el botón secundario en el proyecto y seleccione **Editar Project archivo**. Al final del archivo, verá el siguiente código que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y de tomar nota de la dirección URL.

### <a name="update-your-application"></a>Actualizar la aplicación

1. Abra Visual Studio Explorador de soluciones vaya a la **carpeta** **PagesShared** >  y **abra _Layout.cshtml** y agregue lo siguiente a la <head> sección de etiquetas:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > No copie ni pegue las direcciones `<script src="...">` URL de esta página, ya que no representan la versión más reciente. Para obtener la versión más reciente del SDK, siempre vaya a Microsoft Teams [API de JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. Inserte una llamada a `microsoftTeams.initialize();` en la `script` etiqueta.

1. En Visual Studio Explorador de soluciones vaya a la **carpeta Pages** y abra **Tab.cshtml**

    En **Tab.cshtml** , la aplicación presenta al usuario dos botones de opción para mostrar la pestaña con un icono rojo o gris. Al elegir los **desencadenadores de los**  `saveGray()` `saveRed()`botones Seleccionar gris o Seleccionar rojo o , respectivamente, `settings.setValidityState(true)`se establece y se habilita el **botón** Guardar en la página de configuración. Este código permite Teams que ha completado los requisitos de configuración y la instalación puede continuar. Los parámetros de `settings.setSettings` se establecen. Por último, `saveEvent.notifySuccess()` se llama para indicar que la dirección URL de contenido se ha resuelto correctamente.

1. Actualice los `websiteUrl` valores y `contentUrl` de cada función con la dirección URL de https ngrok a la pestaña.

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

1. Guarde el **tab.cshtml actualizado**.

### <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

1. En Visual Studio, seleccione **F5** o **elija Iniciar depuración** en el **menú** Depurar.

1. Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

    > [!TIP]
    > Debe tener la aplicación en ejecución Visual Studio y ngrok para completar los pasos proporcionados en este artículo. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**. Escucha y reanuda el enrutamiento de la solicitud de la aplicación cuando se reinicia en Visual Studio. Si tiene que reiniciar el servicio ngrok, devuelve una nueva dirección URL y tiene que actualizar la aplicación con la nueva dirección URL.

### <a name="update-your-app-package-with-developer-portal"></a>Actualizar el paquete de la aplicación con el Portal de desarrolladores

1. Vaya a Microsoft Teams. Si usa la versión [basada en web](https://teams.microsoft.com), puede inspeccionar el código front-end con las herramientas para [desarrolladores del explorador](~/tabs/how-to/developer-tools.md).

1. Vaya a [**Portal de desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abre **Aplicaciones y** selecciona **Importar aplicación**.

1. El nombre del paquete de la **aplicación estab.zip**. Está disponible en la siguiente ruta de acceso:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Seleccione **tab.zip** y ábralo en el Portal de desarrolladores.

1. Se crea **un identificador de** aplicación predeterminado y se rellena en **la sección Información** básica.

1. Agrega la descripción corta y larga de la aplicación en **Descripciones**.

1. En **Información para desarrolladores**, agrega los detalles necesarios y en **Sitio web (debe** ser una dirección URL HTTPS válida) proporciona la dirección URL HTTPS de ngrok.

1. En **las direcciones URL de la** aplicación, actualice la directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso para `https://<yourngrokurl>/tou` guardar y guardar.

1. En **Características de la** aplicación, selecciona Agrupar y canalizar aplicación. Actualice la **dirección URL de configuración** con `https://<yourngrokurl>/tab` y seleccione la pestaña **Ámbito**.

1. Seleccione **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Selecciona **Vista previa en Teams** de la barra de herramientas del Portal de desarrolladores, Portal para desarrolladores te informa de que la aplicación se ha descargado correctamente. La **página** Agregar aparece para la aplicación en Teams.

1. Seleccione **Agregar al equipo** para configurar la pestaña en un equipo. Configure la pestaña y seleccione **Guardar**. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Pestaña canal ASPNET cargada" border="true":::
    
    Ahora ha creado y agregado correctamente la pestaña canal o grupo en Teams.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>Crear una pestaña de grupo o canal personalizado con ASP.NET Core MVC

1. En el símbolo del sistema, cree un nuevo directorio para el proyecto de pestaña.

1. Clone el repositorio de ejemplo en el nuevo directorio con el siguiente comando o puede descargar el código [fuente](https://github.com/OfficeDev/Microsoft-Teams-Samples) y extraer los archivos:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

A continuación se indican los pasos para crear una pestaña de canal o grupo:

* [Generar la aplicación con una pestaña de canal o grupo](#generate-your-application-with-a-channel-or-group-tab-2)
* [Establecer un túnel seguro en la pestaña](#establish-a-secure-tunnel-to-your-tab-2)
* [Actualizar la aplicación](#update-your-application-1)
* [Compilar y ejecutar la aplicación](#build-and-run-your-application-2)
* [Actualizar el paquete de la aplicación con el Portal de desarrolladores](#update-your-app-package-with-developer-portal-1)
* [Vista previa de la aplicación en Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Generar la aplicación con una pestaña de canal o grupo

1. Abra Visual Studio y seleccione **Abrir un proyecto o solución**.

1. Vaya a **la carpeta Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp** >  >  >  y abra **ChannelGroupTabMVC.sln**.

1. En Visual Studio, seleccione **F5** o elija Iniciar depuración en el menú Depurar **de** la aplicación para  comprobar si la aplicación se ha cargado correctamente. En un explorador, vaya a las siguientes direcciones URL:

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

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

#### <a name="appmanifest-folder"></a>Carpeta AppManifest

Esta carpeta contiene los siguientes archivos de paquete de aplicación necesarios:

* Un **icono de color completo** que mide 192 x 192 píxeles.
* Un **icono de esquema transparente** que mide 32 x 32 píxeles.
* Un **archivo manifest.json** que especifica los atributos de la aplicación.

Estos archivos deben comprimirse en un paquete de aplicación para usarlos al cargar la pestaña en Teams.

#### <a name="csproj"></a>.csproj

En la Visual Studio Explorador de soluciones, haga clic con el botón secundario en el proyecto y seleccione **Editar Project archivo**. Al final del archivo, verá el siguiente código que crea y actualiza la carpeta zip cuando se compila la aplicación:

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

Estas son las diferentes vistas de ASP.NET Core MVC:

* Inicio: ASP.NET Core trata los archivos denominados **Index** como la página predeterminada o principal del sitio. Cuando la dirección URL del explorador apunta a la raíz del sitio, **Index.cshtml** se mostrará como la página principal de la aplicación.

* Shared: el marcado de vista **parcial _Layout.cshtml** contiene la estructura de página general de la aplicación y los elementos visuales compartidos. También hará referencia a la Teams biblioteca.

#### <a name="controllers"></a>Controladores

Los controladores usan la propiedad `ViewBag` para transferir valores dinámicamente a las vistas.

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

En el símbolo del sistema de la raíz del directorio del proyecto, ejecute el siguiente comando para establecer un túnel seguro en la pestaña:

```cmd
ngrok http 3978 --host-header=localhost
```

Asegúrese de mantener el símbolo del sistema con ngrok en ejecución y de tomar nota de la dirección URL.

### <a name="update-your-application"></a>Actualizar la aplicación

1. Abra Visual Studio Explorador de soluciones vaya a la **carpeta** **ViewsShared** >  y **abra _Layout.cshtml** y agregue lo siguiente a la <head> sección de etiquetas:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > No copie ni pegue las direcciones `<script src="...">` URL de esta página, ya que no representan la versión más reciente. Para obtener la versión más reciente del SDK, siempre vaya a Microsoft Teams [API de JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. Inserte una llamada a `microsoftTeams.initialize();` en la `script` etiqueta.

1. En Visual Studio Explorador de soluciones vaya a la **carpeta Tab** y abra **Tab.cshtml**

    En **Tab.cshtml** , la aplicación presenta al usuario dos botones de opción para mostrar la pestaña con un icono rojo o gris. Al elegir los **desencadenadores de los**  `saveGray()` `saveRed()`botones Seleccionar gris o Seleccionar rojo o , respectivamente, `settings.setValidityState(true)`se establece y se habilita el **botón** Guardar en la página de configuración. Este código permite Teams que ha completado los requisitos de configuración y la instalación puede continuar. Los parámetros de `settings.setSettings` se establecen. Por último, `saveEvent.notifySuccess()` se llama para indicar que la dirección URL de contenido se ha resuelto correctamente. 

1. Actualice los `websiteUrl` valores y `contentUrl` de cada función con la dirección URL de https ngrok a la pestaña.

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

1. Asegúrese de guardar el **tab.cshtml actualizado**.

### <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

1. En Visual Studio, seleccione **F5** o **elija Iniciar depuración** en el **menú** Depurar.

1. Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

    > [!TIP]
    > Debe tener la aplicación en ejecución Visual Studio y ngrok para completar los pasos proporcionados en este artículo. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**. Escucha y reanuda el enrutamiento de la solicitud de la aplicación cuando se reinicia en Visual Studio. Si tiene que reiniciar el servicio ngrok, devuelve una nueva dirección URL y tiene que actualizar la aplicación con la nueva dirección URL.

### <a name="update-your-app-package-with-developer-portal"></a>Actualizar el paquete de la aplicación con el Portal de desarrolladores

1. Vaya a Microsoft Teams. Si usa la versión [basada en web](https://teams.microsoft.com), puede inspeccionar el código front-end con las herramientas para [desarrolladores del explorador](~/tabs/how-to/developer-tools.md).

1. Vaya a [**Portal de desarrolladores**](https://dev.teams.microsoft.com/home).

1. Abre **Aplicaciones y** selecciona **Importar aplicación**.

1. El nombre del paquete de la **aplicación estab.zip**. Está disponible en la siguiente ruta de acceso:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Seleccione **tab.zip** y ábralo en el Portal de desarrolladores.

1. Se crea **un identificador de** aplicación predeterminado y se rellena en **la sección Información** básica.

1. Agrega la descripción corta y larga de la aplicación en **Descripciones**.

1. En **Información para desarrolladores**, agrega los detalles necesarios y en **Sitio web (debe** ser una dirección URL HTTPS válida) proporciona la dirección URL HTTPS de ngrok.

1. En **las direcciones URL de la** aplicación, actualice la directiva de privacidad a `https://<yourngrokurl>/privacy` y los Términos de uso para `https://<yourngrokurl>/tou` guardar y guardar.

1. En **Características de la** aplicación, selecciona Agrupar y canalizar aplicación. Actualice la **dirección URL de configuración** con `https://<yourngrokurl>/tab` y seleccione la pestaña **Ámbito**.

1. Seleccione **Guardar**.

1. En la sección Dominios, los dominios de las pestañas deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Vista previa de la aplicación en Teams

1. Selecciona **Vista previa en Teams** de la barra de herramientas del Portal de desarrolladores, Portal para desarrolladores te informa de que la aplicación se ha descargado correctamente. La **página** Agregar aparece para la aplicación en Teams.

1. Seleccione **Agregar al equipo** para configurar la pestaña en un equipo. Configure la pestaña y seleccione **Guardar**. La pestaña ya está disponible en Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Pestaña canal ASPNET MVC cargada" border="true":::
    
    Ahora ha creado y agregado correctamente la pestaña canal o grupo en Teams.

::: zone-end

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Creación de una página de contenido](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>Vea también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Crear una página de eliminación](~/tabs/how-to/create-tab-pages/removal-page.md)
