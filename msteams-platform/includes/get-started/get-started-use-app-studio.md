### <a name="use-app-studio-to-update-the-app-package"></a>Usar App Studio para actualizar el paquete de la aplicación

App Studio es una aplicación de Microsoft teams que se puede instalar desde la tienda Teams. Simplifica la creación y el registro de una aplicación.

Para instalar App Studio en Teams, haga clic en el icono App Store situado en la parte inferior de la barra izquierda y busque App Studio.

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

Una vez que encuentre el icono de App Studio, haga clic en él y elija *instalar* en el cuadro de diálogo que aparece.

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

Una vez instalado App Studio, haga clic en la pestaña del editor de manifiestos para empezar a crear el paquete de la aplicación para la aplicación de Teams.

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

El ejemplo incluye su propio manifiesto predefinido y está diseñado para compilar un paquete de la aplicación cuando se crea el proyecto. En .NET esto se hace en Visual Studio y en el nodo JS esto se hace escribiendo `gulp` en la línea de comandos en el directorio raíz del proyecto.

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

El nombre del paquete de la aplicación generado es *helloworldapp.zip*. Puede buscar este archivo si la ubicación no está clara en la herramienta que está usando.

En la siguiente parte de este tutorial, va a modificar este paquete de la aplicación seleccionando el icono *importar una aplicación existente* en el editor de manifiestos.

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

Una vez que se ha importado el paquete de la aplicación, App Studio debería tener el siguiente aspecto:

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

Haga clic en el icono de la aplicación recién importada, *Hello World*.

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

Hay una lista de pasos en el lado izquierdo del editor de manifiestos y, a la derecha, una lista de propiedades que deben rellenarse para cada uno de estos pasos. Desde que empezó con una aplicación de muestra, gran parte de la información ya se ha rellenado. Los pasos siguientes le guiarán por el cambio de las partes que todavía deben actualizarse.

#### <a name="app-details"></a>Detalles de la aplicación

Haga clic en la entrada detalles de la *aplicación* en *detalles*. Haga clic en el botón *generar* para crear un nuevo identificador de aplicación.

El nuevo identificador de la aplicación debe tener un aspecto similar al siguiente: `2322041b-72bf-459d-b107-f4f335bc35bd` .

Mire el resto de los detalles de la aplicación en el panel de la derecha y familiarícese con algunas de las entradas, como *información de desarrolladores* y *Personalización de marca*. Estas secciones son importantes si está escribiendo una nueva aplicación para la distribución.

#### <a name="capabilities-tabs"></a>Capacidades: pestañas

Las pestañas se encuentran entre los elementos más simples para agregar a una aplicación de Teams. La aplicación de ejemplo ya admite varias pestañas y puede habilitarlas de la siguiente manera.

##### <a name="team-tab"></a>Ficha equipo

La aplicación solo puede tener una pestaña de equipo.

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

En este ejemplo, la ficha equipo es donde se encuentra la página de configuración. Haga clic en el símbolo *...* al final de la entrada y elija *Editar* en la lista desplegable. Cambie la dirección URL a `https://yourteamsapp.ngrok.io/configure` donde `yourteamsapp.ngrok.io` se debe reemplazar la dirección URL que usó al hospedar la aplicación.

##### <a name="personal-tabs"></a>Pestañas personales

La aplicación puede tener hasta 16 pestañas, incluida la pestaña equipo.

Las pestañas personales se representan de forma diferente a la ficha equipo. Debe ver la *ficha Hello* que ya aparece en la lista de pestañas personales. En el momento tiene un valor de marcador de posición `com.contoso.helloworld.hellotab` . Haga clic en el símbolo *...* al final de la entrada y elija *Editar* en la lista desplegable. Aparecerá el siguiente cuadro de diálogo.

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Hay dos campos que debe actualizar con la dirección URL de la aplicación.

- Cambiar la dirección URL del contenido a `https://yourteamsapp.ngrok.io/hello`
- Cambiar la dirección URL del sitio web a `https://yourteamsapp.ngrok.io/hello`

Donde `yourteamsapp.ngrok.io` se debe reemplazar por la dirección URL que ha usado anteriormente al hospedar la aplicación.

#### <a name="bots"></a>Bots

Los bots son la forma más común de agregar funcionalidad a la aplicación. La muestra Hello World ya tiene un bot como parte de la muestra, pero todavía no se ha registrado con Microsoft.

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

El bot que se importó desde el ejemplo no tiene un identificador de aplicación asociado todavía. Tendrá que crear un nuevo bot para que App Studio pueda crear un nuevo identificador de aplicación y registrarlo en Microsoft. Tenga en cuenta que este es el identificador de la aplicación para bot, que es diferente del identificador de aplicación que se ha creado para la aplicación en un paso anterior. Cada bot en una aplicación requiere su propio identificador de aplicación.

Haga clic en el botón *eliminar* situado junto al *Bot importado* en la lista de robots.

Ahora no quedan bots para mostrar. Haga clic en *configurar*. Se mostrará el cuadro de diálogo *configurar un bot* .

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

Agregue un nombre de bot, por ejemplo `Contoso bot` , y seleccione los tres botones bajo *ámbito*.

Elija *crear bot* para salir del cuadro de diálogo. App Studio dedicará un momento a registrar el bot con Microsoft y, a continuación, deberá mostrar el nuevo bot en la lista de robots. Ahora sería un buen momento para abrir un archivo de texto en el Bloc de notas y copiar y pegar el nuevo identificador de bot en él. Necesitará este identificador más adelante.

Haga clic en *generar nueva contraseña*y anote la contraseña en el mismo archivo de texto que anotó con el identificador de la aplicación de bot en. Esta es la única vez que se mostrará su contraseña, por lo que debe asegurarse de hacerlo ahora.

Actualice la *dirección del punto de conexión del bot* con `https://yourteamsapp.ngrok.io/api/messages` , donde `yourteamsapp.ngrok.io` debe reemplazarse por la dirección URL que usó al hospedar la aplicación.

Ahora sería un buen momento para guardar el archivo de texto si todavía no lo ha hecho. Esta información se agregará a la aplicación hospedada más adelante en este tutorial, lo que permitirá la comunicación segura con el bot.

#### <a name="messaging-extensions"></a>Extensiones de mensajería

Las extensiones de mensajería permiten a los usuarios solicitar información de su servicio y publicarla, en forma de tarjetas, directamente en la conversación del canal. Las extensiones de mensajería aparecen a lo largo de la parte inferior del cuadro de redacción.

Haga clic en *extensiones de mensajería* en *funcionalidades* en la columna izquierda de App Studio para comenzar a configurar la extensión de mensajería.

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

La extensión de mensajería de muestra aparece en el panel de la derecha, en *extensiones de mensajería*. Haga clic en *eliminar* de nuevo para quitar esta entrada y, a continuación, haga clic en el botón *configurar* siguiendo los mismos pasos que siguió para los bots. Se mostrará el cuadro de diálogo de la *extensión de mensajería* .

Seleccione la pestaña *usar bot existente* y, a continuación, *Seleccione uno de los bots existentes*. En el menú desplegable, seleccione el bot que creó en la sección anterior. Agregue un *nombre de bot* y haga clic en *Guardar* para cerrar el cuadro de diálogo.

En la sección *comando* , haga clic en *Agregar*. Estamos agregando un comando basado en la búsqueda, por lo que debe elegir la opción *permitir que los usuarios consulten su servicio...*

En el cuadro de diálogo *nuevo comando* , escriba los siguientes valores.

En *nuevo comando*:

- *Identificador de comando*  = getRandomText
- *Title*       = obtener texto aleatorio para divertirse
- *Description* = obtiene texto e imágenes aleatorios

En *parámetro*:

- *Name*        = cardTitle
- *Title*       = título de la tarjeta
- *Description* = título de la tarjeta para usar

Una vez que haya introducido la información, haga clic en *Guardar* para cerrar el cuadro de diálogo.

#### <a name="register-your-app-in-teams"></a>Registrar la aplicación en Microsoft Teams

Ya ha completado la especificación de los detalles de la aplicación, pero quedan dos pasos. En primer lugar, debe usar la sección probar y distribuir de App Studio para instalar la aplicación en Teams y, en segundo lugar, debe actualizar la aplicación hospedada con el identificador de aplicación y la contraseña de su bot. Recuerde que el ejemplo espera usar el mismo identificador de aplicación y la misma contraseña para el bot y la extensión de mensajería.

Haga clic en el elemento *probar y distribuir* en *Finalizar* en la columna izquierda de App Studio.

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

Para cargar la aplicación en Teams, haga clic en el botón *instalar* en *probar y distribuir*.

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

Haga clic en el cuadro de *búsqueda* en la sección *Agregar a un equipo* y seleccione un equipo al que desee agregar la aplicación de ejemplo. Normalmente querrá configurar un equipo especial para realizar las pruebas.

Haga clic en el botón *instalar* situado en la parte inferior del cuadro de diálogo.

Esto finaliza la parte de App Studio de este tutorial. Ahora debería ver que la aplicación se está ejecutando en Teams, pero el bot y la extensión de mensajería no funcionarán hasta que actualice el entorno de aplicaciones hospedadas para conocer los identificadores de aplicación y las contraseñas.

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
