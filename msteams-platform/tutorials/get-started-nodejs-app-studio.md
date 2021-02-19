---
title: 'Tutorial: crea la primera aplicación con Node.js'
description: Obtén información sobre cómo empezar a crear aplicaciones de Microsoft Teams con Node.js.
keywords: introducción a node.js nodejs App Studio
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 61be1056a07952c6cf166dbe183fa257ceaf7227
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294764"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>Crear la primera aplicación de Microsoft Teams con Node.js

Este tutorial te ayuda a empezar a crear una aplicación de Microsoft Teams con Node.js.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>Descargar y hospedar la aplicación

Sigue estos pasos para descargar y hospedar una aplicación sencilla de "hello world" en Teams.

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, necesita las siguientes herramientas. Si aún no las tiene, puede instalarlas desde estos vínculos.

- [Git](https://git-scm.com/downloads)
- [Node.js y NPM](https://nodejs.org/)
- Obtener cualquier editor de texto o IDE. Puede instalar y usar Visual Studio [code](https://code.visualstudio.com/download) de forma gratuita.

Si ve opciones para agregar , , y a PATH durante la `git` `node` `npm` `code` instalación, elija hacerlo. Será útil.

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

Si ha instalado Visual Studio code, puede comprobar la instalación ejecutando:

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

Puede seguir usando esta ventana de terminal para ejecutar los comandos que se siguen en este tutorial.

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>Descargar el ejemplo

Hemos proporcionado un hello [simple, world!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) muestra para empezar. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo local:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Puedes [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio](https://github.com/OfficeDev/Microsoft-Teams-Samples) si quieres modificar y comprobar los cambios realizados en el repositorio de GitHub para obtener una referencia futura.

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Una vez clonado el repositorio, cambie al directorio que contiene el ejemplo:

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

Para crear el ejemplo, debe instalar todas sus dependencias. Ejecute el siguiente comando para hacerlo:

```bash
npm install
```

Debería ver un montón de dependencias que se instalan. Una vez que terminen, puedes ejecutar la aplicación:

```bash
npm start
```

Cuando se inicia la aplicación hello-world, se muestra `App started listening on port 3333` en la ventana del terminal.

> [!NOTE]
> Si ve un número de puerto diferente que se muestra en el mensaje anterior, es porque tiene un conjunto de variables de entorno PORT. Puede seguir usando ese puerto o cambiar la variable de entorno a 3333.

En este punto, puede abrir una ventana del explorador y navegar a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se están cargando:

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>Hospedar la aplicación de ejemplo

Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más funcionalidades. Para que la plataforma teams cargue la aplicación, la aplicación debe ser accesible desde Internet. Para que la aplicación sea accesible desde Internet, debes *hospedar* la aplicación.

Para las pruebas locales, puedes ejecutar la aplicación en el equipo local y crear un túnel para ella con un punto de conexión web. [ngrok](https://ngrok.com) es una herramienta gratuita que te permite hacerlo. Con *ngrok* puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo). Puede descargar [e instalar](https://ngrok.com/download) *ngrok* para su entorno. Asegúrese de agregarlo a una ubicación en el `PATH` archivo .

Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel. El ejemplo usa el puerto 3333, así que asegúrese de especificarlo aquí.

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* escuchará las solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333. Para comprobarlo, abra el explorador y vaya `https://d0ac14a5.ngrok.io/hello` a cargar la página de saludo de la aplicación. Asegúrese de usar la dirección de reenvío mostrada por *ngrok* en la sesión de la consola en lugar de esta dirección URL.

> [!NOTE]
> Si ha usado un puerto [](#build-and-run-the-sample) diferente en la compilación y ejecuta el paso anterior, asegúrese de usar el mismo número de puerto para configurar el túnel *ngrok.*
> [!TIP]
> Es una buena idea ejecutar *ngrok* en una ventana de terminal diferente para mantenerla en funcionamiento sin interferir con la aplicación de nodo que más adelante podría tener que detener, volver a compilar y volver a ejecutar. La *sesión ngrok* devolverá información de depuración útil en esta ventana.

Hay una versión de pago de *ngrok* que permite nombres persistentes. Si usas la versión gratuita, la aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo. Si la máquina se apaga o se queda en modo de suspensión, el servicio ya no estará disponible. Recuerda esto al compartir la aplicación para pruebas por otros usuarios. Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar cada lugar que use esa dirección.

Recuerda, toma nota de la dirección URL de la aplicación porque necesitarás esto más adelante cuando registres la aplicación con Teams mediante App studio. Bloc de notas funciona bien para este propósito.

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>Implementar la aplicación en Microsoft Teams

En este momento tienes una aplicación hospedada en Internet, pero aún no tienes forma de decir a Teams dónde buscarla, ni siquiera cómo se llama a la aplicación. Para ello, ahora tienes que crear un paquete de aplicación. Esto es poco más que un archivo de texto que contiene el manifiesto de la aplicación y algunos iconos que el cliente de Teams usará para mostrar y marcar correctamente la aplicación. Puedes crear manualmente este paquete de aplicación o puedes usar App Studio, una herramienta que se ejecuta en Teams que simplificará el proceso de registro de la aplicación. App Studio es la forma recomendada de crear y actualizar el paquete de la aplicación.

Para cualquiera de los dos métodos, necesitará lo siguiente:

- La dirección URL en la que se puede encontrar la aplicación en Internet.
- Iconos que Teams usará para crear una marca de la aplicación. El ejemplo incluye iconos de marcador de posición ubicados en "src\static\images. App Studio también proporcionará iconos predeterminados si es necesario.

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>Actualizar la aplicación hospedada

La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores de los que has tomado nota anteriormente.

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
NODE_DEBUG le mostrará lo que está sucediendo en el bot en la consola de depuración Visual Studio código.
NODE_CONFIG_DIR apunta al directorio en la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta localmente, lo busca en la carpeta src).

> [!Note]
> Si no has detenido npm desde antes en el tutorial, tendrás que ejecutar para que Visual Studio Code resalte correctamente las variables de `npm stop` configuración de inicio.

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>Configurar la pestaña aplicación

Una vez que instales la aplicación en un equipo, deberás configurarla para mostrar contenido. Vaya a un canal del equipo y haga clic en el **botón "+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir entre la lista Agregar **una** pestaña. A continuación, se le mostrará un cuadro de diálogo de configuración. Este cuadro de diálogo le permitirá elegir qué pestaña mostrar en este canal. Una vez que seleccione la pestaña y haga clic `Save` en, puede ver la `Hello World` pestaña cargada con la pestaña que eligió.

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Probar el bot en Teams

Ahora puedes interactuar con el bot en Teams. Elige un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` , seguido del mensaje. Esto se denomina una **\@ mención**. Cualquier mensaje que envíes al bot se te enviará como respuesta.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Probar la extensión de mensajería

Para probar la extensión de mensajería, puedes hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación. Aparecerá un menú con la **aplicación "Hello World".** Al hacer clic en él, verá una serie de textos aleatorios. Puede elegir cualquiera de ellos y se insertará en la conversación.

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
