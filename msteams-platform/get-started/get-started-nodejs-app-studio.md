---
title: 'Tutorial: crea la primera aplicación con Node.js'
description: Obtén información sobre cómo empezar a crear Microsoft Teams aplicaciones con Node.js.
keywords: introducción a node.js nodejs App Studio
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 5abde3b1866556ff20e9ee145e761915f88f7288c581556460f5e0e3f3386ecb
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704689"
---
# <a name="build-your-first-microsoft-teams-app-using-nodejs"></a>Crea tu primera Microsoft Teams con Node.js

En este tutorial, aprenderás a crear la primera aplicación Microsoft Teams con Node.js. También le guiará a través de los pasos para: 

1. [Preparar el entorno](#prepare-environment)
1. [Obtener requisitos previos](#GetPrerequisites)
1. [Descargar el ejemplo](#DownloadSample)
1. [Compilar y ejecutar el ejemplo](#BuildRun)
1. [Hospedar la aplicación de ejemplo](#HostSample)
1. [Actualizar las credenciales de la aplicación hospedada](#updatecredentials)
1. [Configurar la pestaña aplicación](#ConfigureTheAppTab)

<a name="prepare-environment"></a>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

### <a name="download-and-host-your-app"></a>Descargar y hospedar la aplicación

Siga estos pasos para descargar y hospedar una aplicación sencilla de "hello world" en Teams.

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, necesita las siguientes herramientas. Si aún no las tiene, puede instalarlas desde estos vínculos.

- [Git](https://git-scm.com/downloads)
- [Node.js y NPM](https://nodejs.org/)
- Obtener cualquier editor de texto o IDE. Puede instalar y [usar](https://code.visualstudio.com/download) Visual Studio Code de forma gratuita.

Si ve opciones para agregar , , y a PATH durante la `git` `node` `npm` `code` instalación, seleccione las opciones. 

Compruebe que las herramientas están disponibles ejecutando lo siguiente en una ventana de terminal:

> [!NOTE]
> Usa la ventana de terminal con la que te sientas más cómodo en tu plataforma. Estos ejemplos usan Bash (que se incluye en Git), pero estos scripts se ejecutarán en la mayoría de las plataformas.

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

Es posible que tenga una versión diferente de estas aplicaciones. Esto no debe ser un problema, excepto gulp. Para gulp tendrás que usar la versión 4.0.0 o posterior.

Si no tiene gulp instalado (o tiene instalada la versión incorrecta), ahora ejecutándose `npm install gulp` en la ventana de terminal.

Si ha instalado Visual Studio Code, puede comprobar la instalación ejecutando:

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

Puede seguir usando esta ventana de terminal para ejecutar los comandos que se siguen en este tutorial.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Descargar el ejemplo

Hemos proporcionado un hello [simple, world!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) muestra para empezar. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo local:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio](https://github.com/OfficeDev/Microsoft-Teams-Samples) si desea modificar y comprobar los cambios realizados en el repositorio de GitHub para su referencia futura.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Después de clonar el repositorio, ejecute el comando cambiar directorio en el terminal para cambiar el directorio al ejemplo:

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

Para crear el ejemplo, debe instalar todas sus dependencias. Ejecute el siguiente comando para hacerlo:

```bash
npm install
```

Debería ver un montón de dependencias que se instalan. Después de la instalación, puedes ejecutar la aplicación con el siguiente comando:

```bash
npm start
```

Cuando se inicia la aplicación hello-world, se muestra `App started listening on port 3333` en la ventana del terminal.

> [!NOTE]
> Si ve un número de puerto diferente que se muestra en el mensaje anterior, es porque tiene un conjunto de variables de entorno PORT. Puede seguir usando ese puerto o cambiar la variable de entorno a 3333.

En este punto, puede abrir una ventana del explorador y navegar a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

## <a name="deploy-your-sample-app"></a>Implementar la aplicación de ejemplo

Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más funcionalidades. Para que Teams plataforma para cargar la aplicación, la aplicación debe ser accesible desde Internet. Para que la aplicación sea accesible desde Internet, debes *hospedar* la aplicación.

Para las pruebas locales, puedes ejecutar la aplicación en el equipo local y crear un túnel para ella con un punto de conexión web. [ngrok](https://ngrok.com) es una herramienta gratuita que te permite hacerlo. Con *ngrok* puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo). Puede descargar [e instalar](https://ngrok.com/download) *ngrok* para su entorno. Asegúrese de agregarlo a una ubicación en el `PATH` archivo .

Después de instalarlo, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel. El ejemplo usa el puerto 3333, así que asegúrese de especificarlo aquí:

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* escuchará las solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333. Para comprobarlo, abra el explorador y vaya `https://d0ac14a5.ngrok.io/hello` a cargar la página de saludo de la aplicación. Asegúrese de usar la dirección de reenvío mostrada por *ngrok* en la sesión de la consola en lugar de esta dirección URL.

> [!NOTE]
> Si ha usado un puerto [](#build-and-run-the-sample) diferente en la compilación y ejecuta el paso anterior, asegúrese de usar el mismo número de puerto para configurar el túnel *ngrok.*
> [!TIP]
> Es una buena idea ejecutar *ngrok* en una ventana de terminal diferente para mantenerla en funcionamiento sin interferir con la aplicación de nodo que más adelante podría tener que detener, volver a compilar y volver a ejecutar. La *sesión ngrok* devolverá información de depuración útil en esta ventana.

Hay una versión de pago de *ngrok* que permite nombres persistentes. Si usas la versión gratuita, la aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo. Si la máquina se apaga o se queda en modo de suspensión, el servicio ya no estará disponible. Recuerda esto al compartir la aplicación para pruebas por otros usuarios. Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar cada lugar que use esa dirección.

Anote la dirección URL de la aplicación. Necesitarás esto más adelante cuando registres la aplicación con Teams con App studio o Portal para desarrolladores.

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>Implementar la aplicación en Microsoft Teams

En este momento tienes una aplicación hospedada en Internet, pero aún no tienes forma de decir Teams dónde buscarla, ni siquiera cómo se llama a la aplicación. Para ello, ahora tienes que crear un paquete de aplicación. Esto es poco más que un archivo de texto que contiene el manifiesto de la aplicación y algunos iconos que el cliente de Teams usará para mostrar y marcar correctamente la aplicación. Puedes crear manualmente este paquete de aplicación, o puedes usar App Studio o Developer Portal, herramientas que se ejecutan en Teams, que simplificarán el proceso de registro de la aplicación. App Studio y Developer Portal son las formas recomendadas de crear y actualizar el paquete de la aplicación.

Para cualquiera de los dos métodos, necesitará lo siguiente:

- La dirección URL en la que se puede encontrar la aplicación en Internet.
- Iconos que Teams usarán para crear una marca de la aplicación. El ejemplo incluye iconos de marcador de posición ubicados en "src\static\images. App Studio también proporcionará iconos predeterminados si es necesario.

**Actualizar el paquete de la aplicación**

# <a name="app-studio"></a>[App Studio](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[Portal para desarrolladores](#tab/DP)

**Para instalar Developer Portal (versión preliminar) en Teams**

1. Selecciona el **icono Aplicaciones** en la parte inferior de la barra izquierda y busca Portal **para desarrolladores.**

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. Seleccione **Portal para desarrolladores** y **seleccione Abrir**.

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. Selecciona la pestaña Aplicaciones y selecciona **Importar una aplicación existente.**

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. Seleccione **Hello World** y seleccione **Importar**. La **aplicación Hello World** se importa en el Portal de desarrolladores. 

    Puedes configurar la aplicación mediante el portal Teams Developer Portal. El manifiesto se encuentra en Distribuir. Puedes usar el manifiesto para configurar las capacidades, los recursos necesarios y otros atributos importantes para la aplicación. Para obtener más información sobre cómo configurar la aplicación mediante el Portal de desarrolladores, [consulta Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>

---
<a name="updatecredentials"></a>

## <a name="update-the-credentials-for-your-hosted-app"></a>Actualizar las credenciales de la aplicación hospedada

La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores de los que has tomado nota anteriormente:

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

La forma en que lo haces varía en función de cómo hospedaste la aplicación. Lo importante sobre el uso de variables de entorno es que estos valores forman parte del entorno: el código de la aplicación puede acceder a ellos, pero no se exponen a terceros que podrían examinar los archivos que forman el sitio.

Si ejecutas la aplicación con ngrok, tendrás que configurar algunas variables de entorno local. Hay muchas maneras de hacerlo, pero lo más fácil, si usa Visual Studio Code, es agregar una configuración [de inicio:](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)

``` 
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

MICROSOFT_APP_ID y MICROSOFT_APP_PASSWORD es el identificador y la contraseña, respectivamente, para el bot.
NODE_DEBUG le mostrará lo que está sucediendo en el bot en la Visual Studio Code de depuración.
NODE_CONFIG_DIR apunta al directorio en la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta localmente, lo busca en la carpeta src).

> [!Note]
> Si no has detenido npm desde antes en el tutorial, tendrás que ejecutar para que Visual Studio Code las variables de configuración de `npm stop` inicio correctamente.

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>Configurar la pestaña aplicación

Después de instalar la aplicación en un equipo, deberás configurarla para mostrar contenido. Vaya a un canal del equipo y haga clic en el **botón "+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir entre la lista Agregar **una** pestaña. A continuación, se le mostrará un cuadro de diálogo de configuración. Este cuadro de diálogo le permitirá elegir qué pestaña mostrar en este canal. Después de seleccionar la pestaña y hacer clic en **Guardar,** puede ver la `Hello World` pestaña cargada con la pestaña que eligió:

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Pruebe el bot en Teams

Ahora puede interactuar con el bot en Teams. Elige un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` , seguido del mensaje. Esto se denomina una **\@ mención**. Cualquier mensaje que envíes al bot se te enviará como respuesta:

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Probar la extensión de mensajería

**Para probar la extensión de mensajería**
1. Seleccione los tres puntos debajo del cuadro de entrada en la vista de conversación. Se muestra un menú con la aplicación **"Hello World".**
1. Seleccione el menú. Se muestra un conjunto de textos aleatorios. Puede seleccionar uno de los textos aleatorios que se insertan en la conversación.

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Seleccione uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior:

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

 ## <a name="see-also"></a>Vea también

* [Introducción a tutoriales](code-samples.md)
* [Crear una aplicación de bots de conversación](first-app-bot.md)
* [Crear una extensión de mensajería](first-message-extension.md)
* [Muestras de código](https://github.com/OfficeDev/Microsoft-Teams-Samples)