### <a name="use-app-studio-to-update-the-app-package"></a>Usar App Studio para actualizar el paquete de la aplicación

App Studio es una aplicación de Teams que puede instalar desde la tienda de Teams. Simplifica la creación y el registro de una aplicación.

Para instalar App Studio en  Teams, seleccione el icono Aplicaciones en la parte inferior de la barra izquierda y busque **App Studio.**

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

Seleccione el **icono de App Studio** y elija **Instalar**. App Studio está instalado.

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

Seleccione la **pestaña Editor de manifiestos** para crear el paquete de la aplicación para su aplicación de Teams.

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

El ejemplo viene con su propio manifiesto predefinido y está diseñado para crear un paquete de la aplicación cuando se crea el proyecto. En .NET, esto se realiza en Visual Studio y, en Node JS, esto se realiza escribiendo en la línea de comandos del directorio `gulp` raíz del proyecto.

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

El nombre del paquete de la aplicación generado **eshelloworldapp.zip**. Puedes buscar este archivo si la ubicación no está clara en la herramienta que estás usando.

Ahora, para modificar este paquete de la aplicación, seleccione el icono Importar **una aplicación** existente en el editor **de manifiestos.**

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

Haz clic **en el icono Hola** a todos para la aplicación recién importada.

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

La siguiente imagen muestra el paquete de la aplicación importado en App Studio:

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

Hay una lista de pasos en el lado izquierdo del editor de manifiestos y, en el lado derecho, una lista de propiedades que deben rellenarse para cada uno de esos pasos. Desde que empezaste con una aplicación de ejemplo, gran parte de la información ya está rellenada. Los pasos siguientes le ayudarán a cambiar los elementos que aún deben actualizarse.

#### <a name="app-details"></a>Detalles de la aplicación

Haga clic en la *entrada detalles de la* aplicación en *Detalles.* Haz clic *en el botón* Generar para crear un nuevo identificador de aplicación.

El nuevo id. de aplicación debe tener un aspecto parecido a: `2322041b-72bf-459d-b107-f4f335bc35bd` .

Consulte el resto de los detalles de la aplicación en el panel derecho y  familiarícese con algunas de las entradas, como información de desarrollador y *personalización de marca.* Estas secciones son importantes si estás escribiendo una nueva aplicación para su distribución.

#### <a name="capabilities-tabs"></a>Funcionalidades: pestañas

Las pestañas son uno de los elementos más sencillos para agregar a una aplicación de Teams. La aplicación de ejemplo ya admite varias pestañas y puedes habilitarlas de la siguiente manera.

##### <a name="team-tab"></a>Pestaña Equipo

La aplicación solo puede tener una pestaña equipo.

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

En este ejemplo, la pestaña Equipo es donde va la página de configuración. Haga clic en *el símbolo ...* al final de la entrada y elija *Editar* en la lista desplegable. Cambie la dirección URL a la dirección URL en la que debe reemplazarse por la dirección URL que `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` usó anteriormente al hospedar la aplicación.

##### <a name="personal-tabs"></a>Pestañas personales

La aplicación puede tener hasta 16 pestañas, incluida la pestaña de equipo.

Las pestañas personales se representan de forma diferente a la pestaña de equipo. Debería ver la *pestaña Hello* ya en la lista de pestañas personales. En este momento tiene un valor de marcador de `com.contoso.helloworld.hellotab` posición. Haga clic en *el símbolo ...* al final de la entrada y elija *Editar* en la lista desplegable. Aparecerá el siguiente cuadro de diálogo.

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Hay dos campos que debes actualizar con la dirección URL de la aplicación.

- Cambiar la dirección URL de contenido a `https://yourteamsapp.ngrok.io/hello`
- Cambiar la dirección URL del sitio web a `https://yourteamsapp.ngrok.io/hello`

Dónde `yourteamsapp.ngrok.io` debe reemplazarse por la dirección URL que usó anteriormente al hospedar la aplicación.

#### <a name="bots"></a>Bots

Los bots son la forma más común de agregar funcionalidad a la aplicación. La muestra hello world ya tiene un bot como parte de la muestra, pero aún no se ha registrado con Microsoft.

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

El bot que se importó de la muestra aún no tiene asociado un id. de aplicación. Tendrá que crear un nuevo bot para que App Studio pueda crear un nuevo id. de aplicación y registrarlo con Microsoft. Ten en cuenta que este es el id. de aplicación del bot, que es diferente del id. de aplicación creado para la aplicación. Cada bot de una aplicación requiere su propio identificador de aplicación.

Haga clic *en el botón* Eliminar situado junto al bot *importado* en la lista de bots.

Ahora no quedan bots para mostrar. Haga clic *en Instalación.* Se mostrará el cuadro *de diálogo Configurar un bot.*

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

Agregue un nombre de bot como `Contoso bot` , y seleccione los tres botones en **Ámbito**.

Elija *Crear bot para* salir del cuadro de diálogo. App Studio registra el bot con Microsoft y muestra el nuevo bot en la lista de bots. Ahora sería un buen momento para abrir un archivo de texto en el bloc de notas y copiar y pegar el nuevo identificador de bot en él. Necesitará este identificador más adelante.

Haga *clic en Generar nueva* contraseña y anote la contraseña en el mismo archivo de texto en el que anotó el id. de la aplicación bot. Esta es la única vez que se mostrará la contraseña, así que asegúrate de hacerlo ahora.

Actualice la *dirección del punto de conexión del bot* a , donde debe reemplazarse por la dirección URL que usó anteriormente al hospedar la `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` aplicación.

Ahora sería un buen momento para guardar el archivo de texto si aún no lo ha hecho. Agregará esta información a la aplicación hospedada más adelante en este tutorial, lo que permitirá una comunicación segura con el bot.

#### <a name="messaging-extensions"></a>Extensiones de mensajería

Las extensiones de mensajería permiten a los usuarios solicitar información de su servicio y publicar esa información, en forma de tarjetas, directamente en la conversación del canal. Las extensiones de mensajería aparecen en la parte inferior del cuadro de redacción.

Seleccione **Extensiones de mensajería en** **Funcionalidades** de la columna izquierda de App Studio para configurar la extensión de mensajería.

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

La extensión de mensajería de ejemplo aparece en el panel derecho en **Extensiones de mensajería.** Seleccione **Eliminar** de nuevo para quitar  esta entrada y, a continuación, haga clic en el botón Configurar siguiendo los mismos pasos que siguió para los bots. Se mostrará el cuadro *de diálogo Extensión de* mensajería.

Seleccione la *pestaña Usar bot existente* y, a continuación, seleccione uno de mis *bots existentes.* En el menú desplegable, seleccione el bot que creó en la sección anterior. Agregue un *nombre de bot y* haga clic en *Guardar* para cerrar el cuadro de diálogo.

En la *sección Comando,* haga clic *en Agregar*. We're adding a search-based command, so choose the *Allow users to query your service...* option.

En el **cuadro de diálogo Nuevo** comando, escriba los siguientes valores.

En *Nuevo comando:*

- *Identificador de comando*  = getRandomText
- *Title*       = Obtener texto aleatorio para la diversión
- *Description* = Obtiene texto e imágenes aleatorios

En *Parámetro*:

- *Name*        = cardTitle
- *Título*       = Título de la tarjeta
- *Descripción* = título de la tarjeta que se usará

Una vez que haya escrito la información, haga clic *en Guardar* para cerrar el cuadro de diálogo.

#### <a name="register-your-app-in-teams"></a>Registrar la aplicación en Teams

Ya has completado la especificación de los detalles de la aplicación, pero quedan los dos pasos siguientes:
1. Use la sección Probar y distribuir de App Studio para instalar la aplicación en Teams.
1. Actualice la aplicación hospedada con el identificador de aplicación y la contraseña del bot. Recuerde que el ejemplo espera usar el mismo id. de aplicación y contraseña tanto para el bot como para la extensión de mensajería.

Selecciona el **elemento Probar y distribuir en** **Finalizar** en la columna izquierda de App Studio.

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

Para cargar la aplicación en Teams, haga clic en el botón Instalar en *Probar y distribuir.* 

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

Seleccione el **cuadro** de búsqueda en la sección Agregar **a un** equipo y seleccione un equipo al que agregar la aplicación de ejemplo. Por lo general, puede configurar un equipo especial para realizar pruebas.

Seleccione el **botón** Instalar en la parte inferior del cuadro de diálogo.

Esto finaliza la parte de App Studio de este tutorial. Ahora debería ver que la aplicación se ejecuta en Teams, pero el bot y la extensión de mensajería no funcionarán hasta que actualice el entorno de aplicaciones hospedadas para saber cuáles son los IDs y las contraseñas de la aplicación.

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
