---
title: 'Tutorial: crear la primera aplicación con Node.js'
description: Obtenga información sobre cómo empezar a crear aplicaciones de Microsoft Teams con Node.js.
keywords: introducción a node.js nodejs App Studio
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 03dcf79a46266321e54c7e99bf01cdd2a87075fa
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037049"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>Crear la primera aplicación de Microsoft Teams con Node.js

Este tutorial le ayuda a empezar a crear una aplicación de Microsoft Teams con Node.js.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>Descargar y hospedar la aplicación

Siga estos pasos para descargar y hospedar una sencilla aplicación "hola a todos" en Teams.

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, necesita las siguientes herramientas. Si aún no los tiene, puede instalarlos desde estos vínculos.

- [Git](https://git-scm.com/downloads)
- [Node.js y NPM](https://nodejs.org/)
- Obtiene cualquier editor de texto o IDE. Puede instalar y usar el [código Visual Studio de](https://code.visualstudio.com/download) forma gratuita.

Si ve opciones para agregar , y a path durante la `git` `node` `npm` `code` instalación, elija hacerlo. Será útil.

Para comprobar que las herramientas están disponibles, ejecute lo siguiente en una ventana de terminal:

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

Es posible que tenga una versión diferente de estas aplicaciones. Esto no debe ser un problema, excepto para Gulp. Para Gulp tendrá que usar la versión 4.0.0 o posterior.

Si no tiene instalado Gulp (o tiene instalada la versión incorrecta), ejecítelo ahora ejecutándose `npm install gulp` en la ventana de terminal.

Si ha instalado el código Visual Studio, puede comprobar la instalación ejecutando:

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

Puede seguir usando esta ventana de terminal para ejecutar los comandos siguientes en este tutorial.

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>Descargar el ejemplo

Hemos proporcionado un saludo [sencillo, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) muestra para empezar. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio si](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) desea modificar y comprobar los cambios en el repositorio de GitHub para consultarlos en el futuro.

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Una vez clonado el repositorio, cambie al directorio que contiene el ejemplo:

```bash
cd msteams-samples-hello-world-nodejs
```

Para crear el ejemplo, debe instalar todas sus dependencias. Ejecute el siguiente comando para hacerlo:

```bash
npm install
```

Debería ver un montón de dependencias que se instalan. Una vez que terminen, puedes ejecutar la aplicación:

```bash
npm start
```

Cuando se inicia la aplicación hello-world, se muestra `App started listening on port 3333` en la ventana de terminal.

> [!NOTE]
> Si ve un número de puerto diferente en el mensaje anterior, es porque tiene una variable de entorno PORT establecida. Puede seguir usando ese puerto o cambiar la variable de entorno a 3333.

En este punto, puede abrir una ventana del explorador y navegar a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>Hospedar la aplicación de ejemplo

Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más funcionalidades. Para que la plataforma de Teams cargue la aplicación, debe ser accesible desde Internet. Para que la aplicación sea accesible desde Internet, debes *hospedarla.*

Para realizar pruebas locales, puedes ejecutar la aplicación en el equipo local y crear un túnel para ella con un punto de conexión web. [ngrok](https://ngrok.com) es una herramienta gratuita que te permite hacerlo. Con *ngrok* puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo). Puede descargar [e instalar](https://ngrok.com/download) *ngrok* para su entorno. Asegúrese de agregarlo a una ubicación en el `PATH` archivo .

Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel. El ejemplo usa el puerto 3333, así que asegúrate de especificarlo aquí.

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok escuchará* las solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333. Para comprobarlo, abre el explorador y vas a `https://d0ac14a5.ngrok.io/hello` cargar la página hello de la aplicación. Asegúrese de usar la dirección de reenvío mostrada por *ngrok* en la sesión de la consola en lugar de esta dirección URL.

> [!NOTE]
> Si ha usado un puerto [](#build-and-run-the-sample) diferente en la compilación y ejecuta el paso anterior, asegúrese de usar el mismo número de puerto para configurar el túnel *ngrok.*
> [!TIP]
> Es una buena idea ejecutar *ngrok* en una ventana de terminal diferente para mantenerlo en funcionamiento sin interferir con la aplicación de nodo que más adelante podría tener que detener, volver a compilar y volver a ejecutar. La *sesión de ngrok* devolverá información de depuración útil en esta ventana.

Hay una versión de pago de *ngrok* que permite nombres persistentes. Si usas la versión gratuita, la aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo. Si la máquina se apaga o deja de estar en modo de suspensión, el servicio ya no estará disponible. Recuerda esto al compartir la aplicación para pruebas por parte de otros usuarios. Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar cada lugar que use esa dirección.

Recuerde que debe tomar nota de la dirección URL de la aplicación porque la necesitará más adelante cuando registre la aplicación en Teams con App studio. El Bloc de notas funciona bien para este propósito.

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>Implementar la aplicación en Microsoft Teams

Llegados a este punto, tiene una aplicación hospedada en Internet, pero aún no tiene forma de decir a Teams dónde buscarla, ni siquiera cómo se llama a la aplicación. Para ello, ahora tienes que crear un paquete de la aplicación. Esto es poco más que un archivo de texto que contiene el manifiesto de la aplicación y algunos iconos que el cliente de Teams usará para mostrar y personalice correctamente la aplicación. Puede crear manualmente este paquete de la aplicación o puede usar App Studio, una herramienta que se ejecuta en Teams y que simplificará el proceso de registro de la aplicación. App Studio es la forma recomendada de crear y actualizar el paquete de la aplicación.

Para cualquiera de los dos métodos necesitará lo siguiente:

- La dirección URL en la que se encuentra la aplicación en Internet.
- Iconos que Teams usará para marcar la aplicación. El ejemplo incluye iconos de marcador de posición ubicados en "src\static\images. App Studio también proporcionará iconos predeterminados si es necesario.

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>Actualizar la aplicación hospedada

La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores que has tomado nota anteriormente.

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

La forma en que lo haces varía en función de cómo hospedaste la aplicación. Lo importante sobre el uso de variables de entorno es que estos valores forman parte del entorno: el código de la aplicación puede acceder a ellos, pero no se exponen a terceros que puedan examinar los archivos que forman el sitio.

Si ejecutas la aplicación con ngrok, tendrás que configurar algunas variables de entorno local. Hay muchas maneras de hacerlo, pero la más sencilla, si usa Visual Studio Code, es agregar una configuración [de inicio:](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)

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

MICROSOFT_APP_ID y MICROSOFT_APP_PASSWORD es el identificador y la contraseña, respectivamente, del bot.
NODE_DEBUG le mostrará lo que está sucediendo en el bot en la consola de depuración de Visual Studio código.
NODE_CONFIG_DIR apunta al directorio en la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta localmente, lo busca en la carpeta src).

> [!Note]
> Si no ha detenido npm desde antes en el tutorial, tendrá que ejecutar para que Visual Studio Code resalte correctamente las variables de configuración `npm stop` de inicio.

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>Configurar la pestaña de la aplicación

Una vez que instales la aplicación en un equipo, deberás configurarla para mostrar contenido. Vaya a un canal del equipo y haga clic en el **botón "+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir en la lista Agregar **una** pestaña. A continuación, aparecerá un cuadro de diálogo de configuración. Este cuadro de diálogo te permitirá elegir qué pestaña mostrar en este canal. Una vez que seleccione la pestaña y haga clic en esta, podrá ver la `Save` pestaña cargada con la pestaña que `Hello World` eligió.

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" alt-text="Screenshot of configure" />

### <a name="test-your-bot-in-teams"></a>Probar el bot en Teams

Ahora puede interactuar con el bot en Teams. Elija un canal en el equipo donde registró la aplicación y escriba `@your-bot-name` , seguido del mensaje. Esto se denomina una **\@ mención.** Cualquier mensaje que envíe al bot se le enviará como respuesta.

<img width="450px" alt-text="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Probar la extensión de mensajería

Para probar la extensión de mensajería, puedes hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación. Aparecerá un menú con la **aplicación "Hola** a todos". Al hacer clic en él, verá una serie de textos aleatorios. Puede elegir cualquiera de ellos y se insertará en la conversación.

<img width="430px" alt-text="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt-text="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.

<img width="430px" alt-text="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
