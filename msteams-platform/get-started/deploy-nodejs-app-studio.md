---
title: Implementación de la primera aplicación con Node.js en App Studio
description: Aprenda a implementar aplicaciones Microsoft Teams con Node.js en App Studio
keywords: introducción node.js App Studio
ms.custom: scenarios:getting-started; languages:ASP,Node.js
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 15b5837fb8155d8b34b2c337a550ecbaaae9d86a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142524"
---
# <a name="update-nodejs-app-package-in-app-studio"></a>Actualización Node.js paquete de la aplicación en App Studio

> [!TIP]
> **Pruebe el Portal para desarrolladores**: App Studio ha evolucionado. Configurar, distribuir y administrar las aplicaciones de Teams con el nuevo [Portal para desarrolladores](https://dev.teams.microsoft.com/).

App Studio es una aplicación Teams que puedes instalar desde la tienda de Teams. Simplifica la creación y el registro de una aplicación.

Complete los pasos siguientes para actualizar el paquete de la aplicación:

1. Para instalar App Studio en Teams, seleccione el icono **Aplicaciones** en la parte inferior de la barra izquierda y busque **App Studio**:

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. Seleccione el icono **de App Studio** y elija **Instalar**. App Studio está instalado:

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. Para crear el paquete de la aplicación para la aplicación de Teams, seleccione la pestaña **Editor de manifiestos** en **App Studio**:

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    El ejemplo viene con su propio manifiesto y está diseñado para compilar un paquete de aplicación cuando se compila el proyecto. En Node.js, para ello, escriba `gulp` en la línea de comandos del directorio raíz del proyecto.

    Puede compilar el paquete de la aplicación en Node.js escribiendo `gulp` en la línea de comandos del directorio raíz del proyecto.

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

    El nombre del paquete de aplicación generado es `helloworldapp.zip`. Puede buscar este archivo si la ubicación no está clara en la herramienta que está usando.

1. Ahora, para modificar este paquete de aplicación, seleccione **Importar una aplicación existente** en el **editor de manifiestos**:

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. Seleccione el icono **Hola mundo** de la aplicación recién importada:

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    En la imagen siguiente se muestra el paquete de la aplicación importada en App Studio:

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    En el lado izquierdo del editor de manifiestos hay una lista de pasos. En el lado derecho hay una lista de propiedades que deben rellenarse para cada paso. Al empezar con una aplicación de ejemplo, gran parte de la información ya se ha completado. Los pasos siguientes le permiten actualizar las propiedades de la aplicación Hola mundo.

## <a name="app-details"></a>Detalles de la aplicación

Seleccione **Detalles de la aplicación** en **Detalles**. Seleccione el botón **Generar** para crear un nuevo identificador de aplicación.

El nuevo identificador de aplicación es similar a `2322041b-72bf-459d-b107-f4f335bc35bd`.

Consulte los detalles de la aplicación en el panel derecho, incluida **la información del desarrollador** y los detalles **de personalización de marca** . Estos detalles son importantes si está escribiendo una nueva aplicación para su distribución.

## <a name="tabs"></a>Pestañas

Es sencillo agregar pestañas a una aplicación Teams. La aplicación de ejemplo ya admite varias pestañas y puede habilitarlas.

### <a name="team-tab"></a>Pestaña Equipo

La aplicación solo puede tener una pestaña Equipo:

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

En este ejemplo, la pestaña Equipo es donde se muestra la página de configuración. Seleccione el **símbolo ...** de la **dirección URL de configuración de la pestaña** y elija **Editar** en el menú desplegable. Cambie la dirección URL a `https://yourteamsapp.ngrok.io/configure` donde `yourteamsapp.ngrok.io` se debe reemplazar por la dirección URL que usó al hospedar la aplicación.

### <a name="personal-tabs"></a>Pestañas personales

La aplicación puede tener hasta 16 pestañas, incluida la pestaña Equipo.

Las pestañas personales son diferentes de la pestaña Equipo. **Hello Tab** ya aparece en la lista de pestañas personales con un valor `com.contoso.helloworld.hellotab`de marcador de posición . Seleccione el **símbolo ...** de la **dirección URL de configuración de la pestaña** y elija **Editar** en el menú desplegable. Aparece el siguiente cuadro de diálogo:

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Actualice los siguientes cuadros con la dirección URL de la aplicación:

* Cambie el cuadro **Dirección URL de contenido** a `https://yourteamsapp.ngrok.io/hello`
* Cambie el cuadro **Dirección URL del sitio web** a `https://yourteamsapp.ngrok.io/hello`

Reemplace `yourteamsapp.ngrok.io` por la dirección URL que usó al hospedar la aplicación.

#### <a name="bots"></a>Bots

Es fácil agregar la funcionalidad de bots a la aplicación. La **aplicación de ejemplo Hola mundo** ya tiene un bot como parte del ejemplo, pero debe registrarlo con Microsoft:

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

El bot que se importó desde el ejemplo no tiene un identificador de aplicación asociado. Debe crear un nuevo bot para que App Studio pueda crear un nuevo identificador de aplicación y registrarlo en Microsoft.

> [!NOTE]
> El identificador de aplicación creado por App Studio para el bot es diferente del id. de aplicación creado para la aplicación. Cada bot de una aplicación requiere su propio identificador de aplicación.

Complete los pasos siguientes para configurar el bot:

1. Seleccione **Eliminar** junto al bot importado en la lista de bots. Ahora no queda ningún bot que mostrar.
1. Seleccione **Configurar** para mostrar el cuadro de diálogo **Configurar un bot** .

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. Agregue un bot con el nombre **contoso bot** y seleccione las tres casillas en **Ámbito**.
1. Elija **Guardar** para salir del cuadro de diálogo. App Studio registra el bot con Microsoft y muestra el nuevo bot en la lista de bots.
1. Ahora abra un archivo de texto en el Bloc de notas y copie y pegue el nuevo identificador de bot en él.
1. Haga clic en **Generar nueva contraseña** y anote la contraseña en el mismo archivo de texto que anotó en el identificador de la aplicación del bot.
1. Actualice la **dirección del punto de conexión del bot** a `https://yourteamsapp.ngrok.io/api/messages`y reemplace por `yourteamsapp.ngrok.io` la dirección URL que usó al hospedar la aplicación.
1. Ahora guarde el archivo de texto, ya que debe agregar la información del archivo a la aplicación hospedada para permitir una comunicación segura con el bot.

#### <a name="messaging-extensions"></a>Extensiones de mensajería

Las extensiones de mensajería permiten a los usuarios solicitar información del servicio y publicar esa información. La información se publica en forma de tarjetas en la conversación del canal. Las extensiones de mensajería aparecen en la parte inferior del cuadro de redacción.

Complete los pasos siguientes para configurar la extensión de mensajería:

1. Seleccione **Extensiones de mensajería** en **Funcionalidades** en el panel izquierdo de App Studio para configurar la extensión de mensajería:

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    La extensión de mensajería de ejemplo se muestra en el panel **Extensiones de mensajería** .

1. Seleccione **Eliminar** para quitar la extensión de mensajería, seleccione **Configurar** y siga los mismos pasos que se usan para [los bots](#bots). Se muestra el cuadro **de diálogo Extensión de mensajería** .
1. Seleccione la pestaña **Usar bot existente** y **Seleccione uno de mis bots existentes**.
1. Seleccione el bot que creó en el menú desplegable. Agregue un **nombre de bot** y seleccione **Guardar** para cerrar el cuadro de diálogo.
1. En la sección **Comando** , seleccione **Agregar**. Para agregar un comando basado en búsqueda, seleccione la opción **Permitir a los usuarios consultar el servicio para obtener información e insertarla en un mensaje** .
1. En el cuadro de diálogo **Nuevo comando** , escriba los valores siguientes:

    En **Nuevo comando**:

    * **Identificador de comando**: escriba texto aleatorio
    * **Título**: escriba un título aleatorio
    * **Descripción**: escriba una descripción aleatoria.

    En **Parámetro**:

    * **Nombre**: escriba el nombre del parámetro.
    * **Título**: escriba el título de la tarjeta
    * **Descripción**: escriba la descripción de la tarjeta.

1. Después de escribir la información, seleccione **Guardar** para cerrar el cuadro de diálogo.

#### <a name="register-your-app-in-teams"></a>Registrar la aplicación en Teams

Después de escribir los detalles de la aplicación, complete los pasos siguientes para registrar la aplicación en Teams:

1. Use **Probar y distribuir** App Studio para instalar la aplicación en Teams.
1. Actualice la aplicación hospedada con el identificador de aplicación y la contraseña del bot. Para la aplicación de ejemplo, use el mismo identificador de aplicación y contraseña para el bot y la extensión de mensajería.
1. Seleccione **Probar y distribuir**  en **Finalizar** en el panel izquierdo de App Studio:

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. Para cargar la aplicación en Teams, seleccione el botón **Instalar** en **Probar y distribuir**:

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

    > [!NOTE]
    > Si no puede transferir localmente la aplicación, compruebe si ha [habilitado la carga de aplicaciones personalizadas](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option).

1. Seleccione el cuadro **Buscar** de la sección **Agregar a un equipo** y seleccione un equipo para agregar la aplicación de ejemplo. Puede configurar un equipo especial para las pruebas.
1. Seleccione el botón **Instalar** en la parte inferior del cuadro de diálogo.

    La aplicación ya está disponible en Teams. Sin embargo, el bot y la extensión de mensajería no funcionarán hasta que actualice el entorno de aplicaciones hospedadas con los identificadores de aplicación y las contraseñas.

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>

## <a name="update-the-credentials-for-your-hosted-app"></a>Actualización de las credenciales de la aplicación hospedada

La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores que anotó anteriormente:

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

Las variables de entorno forman parte del entorno. Solo el código de la aplicación puede acceder a ellos. No están expuestos a terceros.

Si ejecuta la aplicación mediante ngrok, deberá configurar variables de entorno locales. Puede usar Visual Studio Code para agregar una [configuración de inicio](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):

```json
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

Donde:

* Las credenciales de autorización del bot son las siguientes:
  * MICROSOFT_APP_ID es id.
  * MICROSOFT_APP_PASSWORD es contraseña.
* NODE_DEBUG mostrar lo que sucede en el bot en la consola de depuración de Visual Studio Code
* NODE_CONFIG_DIR apunta al directorio en la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta localmente, busca el directorio raíz en la `src` carpeta).

> [!Note]
> Si no ha detenido npm anteriormente en el tutorial, tendrá que ejecutarse `npm stop` para que Visual Studio Code recoga correctamente las variables de configuración de inicio.

<a name="ConfigureTheAppTab"></a>

## <a name="test-the-app-capabilities-in-teams"></a>Probar las funcionalidades de la aplicación en Teams

Después de instalar la aplicación en Teams, debe configurarla para mostrar el contenido.

### <a name="test-your-tab-in-teams"></a>Pruebe la pestaña en Teams

1. Vaya a un canal de Teams y seleccione el botón **"+"** para agregar una nueva pestaña.
1. A continuación, puede elegir en `Hello World` la lista **Agregar una pestaña** .
1. En el cuadro de diálogo de configuración, seleccione la pestaña que desea mostrar en el canal. A continuación, seleccione **Guardar**.

Puede ver la `Hello World` pestaña cargada con la pestaña que eligió:

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Pruebe el bot en Teams

Ahora puede interactuar con el bot en Teams. Elija un canal en el equipo donde registró la aplicación y escriba `@your-bot-name`, seguido del mensaje. Este tipo de mensaje se denomina **mención\@**. Cualquier mensaje que envíe al bot se le devolverá como respuesta:

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Prueba de la extensión de mensajería

Para probar la extensión de mensajería:

1. Seleccione los tres puntos debajo del cuadro de entrada de la vista de conversación. Se muestra un menú con la aplicación **"Hola mundo"**.
1. Seleccione el menú. Se muestra un conjunto de textos aleatorios. Puede seleccionar uno de los textos aleatorios que se insertan en la conversación.

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Seleccione uno de los textos aleatorios. La tarjeta con formato aparece lista para enviarse con su propio mensaje incluido en la parte inferior:

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

| &nbsp; | &nbsp; |
|:--- | ---:|
|[Back](get-started-overview.md) | &nbsp; |
|
