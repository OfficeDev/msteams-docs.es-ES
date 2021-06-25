### <a name="use-app-studio-to-update-the-app-package"></a>Usar App Studio para actualizar el paquete de la aplicación

> [!TIP]
> **Pruebe el Portal para desarrolladores:** App Studio pronto se depricará. Configure, distribuya y administre las aplicaciones Teams con el nuevo [Portal de desarrolladores.](https://dev.teams.microsoft.com/)

App Studio es una Teams que puedes instalar desde la Teams tienda. Simplifica la creación y el registro de una aplicación.

Siga estos pasos para actualizar el paquete de la aplicación:

1. Para instalar App Studio en Teams,  selecciona el icono Aplicaciones en la parte inferior de la barra izquierda y busca **App Studio**:

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. Selecciona el **icono de App Studio** y elige **Instalar**. App Studio está instalado:

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. Para crear el paquete de la aplicación para Teams aplicación, selecciona la pestaña Editor de **manifiestos** en **App Studio**:

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>


    El ejemplo viene con su propio manifiesto y está diseñado para crear un paquete de aplicación cuando se crea el proyecto. En .NET, el archivo manifest.json se puede encontrar en Visual Studio en Manifiesto en ```Microsoft.Teams.Samples.HelloWorld.Web``` . En Node.js, esto se realiza escribiendo en la línea `gulp` de comandos del directorio raíz del proyecto.

     En Visual Studio, el manifest.jsel archivo on se encuentra en **en Manifiesto** en `Microsoft.Teams.Samples.HelloWorld.Web` . Este paso se describe en la siguiente imagen:  
    
    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>
    
    Puedes crear el paquete de la aplicación en Node.js escribiendo en la línea `gulp` de comandos en el directorio raíz del proyecto.


    ```bash
    $ gulp
    [13:39:27] Using gulpfile ~\documents\github\msteams-samples-hello-world-nodejs\gulpfile.js
    [13:39:27] Starting 'clean'...
    [13:39:27] Starting 'generate-manifest'...
    [13:39:27] Finished 'generate-manifest' after 11 ms
    [13:39:27] Finished 'clean' after 21 ms
    [13:39:27] Starting 'default'...
    Build completed. Output in manifest folder
    [13:39:27] Finished 'default' after 62 μs
    ```

    El nombre del paquete de aplicación generado es **helloworldapp.zip**. Puede buscar este archivo si la ubicación no está clara en la herramienta que está usando.

1. Ahora, para modificar este paquete de aplicación, selecciona **Importar una aplicación existente** en el editor de **manifiestos:**

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. Selecciona el **icono Hello World** para la aplicación recién importada:

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    La siguiente imagen muestra el paquete de aplicación importado en App Studio:

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    En el lado izquierdo del editor de manifiesto hay una lista de pasos. En el lado derecho hay una lista de propiedades que deben rellenarse para cada paso. Al empezar con una aplicación de ejemplo, gran parte de la información ya se ha completado. Los siguientes pasos te permiten actualizar las propiedades de la aplicación Hello World.

#### <a name="app-details"></a>Detalles de la aplicación

Seleccione **Detalles de la aplicación** en **Detalles**. Selecciona el **botón** Generar para crear un nuevo identificador de aplicación.

El nuevo identificador de aplicación es similar a `2322041b-72bf-459d-b107-f4f335bc35bd` .

Consulta los detalles de la aplicación en el panel derecho, incluida la información del **desarrollador** y los **detalles de personal** de marca. Estos detalles son importantes si vas a escribir una nueva aplicación para su distribución.

#### <a name="tabs"></a>Pestañas

Es sencillo agregar pestañas a una Teams aplicación. La aplicación de ejemplo ya admite varias pestañas y puedes habilitarlas.

##### <a name="team-tab"></a>Ficha Equipo

La aplicación solo puede tener una pestaña Equipo:

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

En este ejemplo, la pestaña Equipo es donde se muestra la página de configuración. Seleccione el **símbolo ...** de la dirección URL de **configuración tab** y elija **Editar** en el menú desplegable. Cambie la dirección URL a `https://yourteamsapp.ngrok.io/configure` donde `yourteamsapp.ngrok.io` debe reemplazarse por la dirección URL que usó al hospedar la aplicación.

##### <a name="personal-tabs"></a>Pestañas personales

La aplicación puede tener hasta 16 pestañas, incluida la pestaña Equipo.

Las pestañas personales son diferentes de la pestaña Equipo. **Hello Tab** ya aparece en la lista de pestañas personales con un valor de marcador de posición `com.contoso.helloworld.hellotab` . Seleccione el **símbolo ...** de la dirección URL de **configuración tab** y elija **Editar** en el menú desplegable. Aparece el siguiente cuadro de diálogo:

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Actualice los siguientes cuadros con la dirección URL de la aplicación:

- Cambiar el **cuadro Dirección URL de** contenido a `https://yourteamsapp.ngrok.io/hello`
- Cambiar el **cuadro Dirección URL del** sitio web a `https://yourteamsapp.ngrok.io/hello`

Reemplace `yourteamsapp.ngrok.io` por la dirección URL que usó al hospedar la aplicación.

#### <a name="bots"></a>Bots

Es fácil agregar la funcionalidad de bots a la aplicación. La aplicación de ejemplo **Hello World** ya tiene un bot como parte de la muestra, pero debes registrarlo con Microsoft:

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

El bot que se importó desde el ejemplo no tiene un identificador de aplicación asociado. Debes crear un bot nuevo para que App Studio pueda crear un nuevo id. de aplicación y registrarlo con Microsoft.

> [!NOTE]
> El id. de aplicación creado por App Studio para el bot es diferente del id. de aplicación creado para la aplicación. Cada bot de una aplicación requiere su propio identificador de aplicación.

Siga estos pasos para configurar el bot:

1. Seleccione **Eliminar** junto al bot importado en la lista de bots. Ahora no quedan bots que mostrar. 
1. Seleccione **Configurar** para mostrar el cuadro de diálogo Configurar **un bot.**

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. Agregue un bot name **Contoso bot** y active las tres casillas en **Scope**.
1. Elija **Guardar** para salir del cuadro de diálogo. App Studio registra el bot con Microsoft y muestra el nuevo bot en la lista de bots. 
1. Ahora abra un archivo de texto en el bloc de notas y copie y pegue el nuevo identificador de bot en él.
1. Haga **clic en Generar nueva contraseña** y anote la contraseña en el mismo archivo de texto que anotó el id. de la aplicación del bot.
1. Actualice la **dirección del extremo bot** a y reemplace por la dirección URL que `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` usó al hospedar la aplicación.
1. Ahora guarda el archivo de texto, ya que debes agregar la información del archivo a la aplicación hospedada para permitir una comunicación segura con el bot.

#### <a name="messaging-extensions"></a>Extensiones de mensajería

Las extensiones de mensajería permiten a los usuarios solicitar información del servicio y publicar esa información. La información se publica en forma de tarjetas en la conversación del canal. Las extensiones de mensajería aparecen en la parte inferior del cuadro de redacción.

Siga estos pasos para configurar la extensión de mensajería:

1. Seleccione **Extensiones de mensajería en** **Funcionalidades** en el panel izquierdo de App Studio para configurar la extensión de mensajería:

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    La extensión de mensajería de ejemplo se muestra en el panel **Extensiones de** mensajería.

1. Seleccione **Eliminar** para quitar la extensión de mensajería, **seleccione Configurar** y siga los mismos pasos usados para [bots](#bots). Se **muestra el cuadro de diálogo** Extensión de mensajería.
1. Seleccione la **pestaña Usar bot existente** y Seleccionar de uno de mis **bots existentes**.
1. Selecciona el bot que creaste en el menú desplegable. Agregue un **nombre bot y** seleccione **Guardar** para cerrar el cuadro de diálogo.
1. En la **sección Comando,** seleccione **Agregar**. Para agregar un comando basado en búsqueda, seleccione la opción Permitir a los usuarios consultar su servicio para obtener información e **insertarla en un mensaje.**
1. En el **cuadro de diálogo Nuevo** comando, escriba los siguientes valores:

    En **Nuevo comando**:

    - **Identificador de comando:** escriba texto aleatorio
    - **Title**: Enter random title
    - **Descripción:** escriba una descripción aleatoria

    En **Parámetro**:

    - **Nombre:** escriba el nombre del parámetro
    - **Título:** escriba el título de la tarjeta
    - **Descripción:** escriba la descripción de la tarjeta

1. Después de escribir la información, seleccione **Guardar** para cerrar el cuadro de diálogo.

#### <a name="register-your-app-in-teams"></a>Registrar la aplicación en Teams

Después de especificar los detalles de la aplicación, siga estos pasos para registrar la aplicación en Teams:

1. Usa **Probar y distribuir** App Studio para instalar la aplicación en Teams. 
1. Actualice la aplicación hospedada con el identificador de aplicación y la contraseña del bot. Para la aplicación de ejemplo, usa el mismo id. de la aplicación y la misma contraseña para bot y extensión de mensajería. 
1. Seleccione **Probar y distribuir en** **Finalizar** en el panel izquierdo de App Studio:

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. Para cargar la aplicación en Teams, selecciona el botón **Instalar** en **Probar y distribuir**:

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. Selecciona el **cuadro** Buscar en la **sección Agregar a un** equipo y selecciona un equipo para agregar la aplicación de ejemplo. Puede configurar un equipo especial para las pruebas.
1. Seleccione el **botón** Instalar en la parte inferior del cuadro de diálogo.

    La aplicación ya está disponible en Teams. Sin embargo, el bot y la extensión de mensajería no funcionarán hasta que actualice el entorno de aplicaciones hospedadas con los IDs y contraseñas de la aplicación.

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
