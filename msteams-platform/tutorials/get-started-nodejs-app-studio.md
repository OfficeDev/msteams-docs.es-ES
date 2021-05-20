---
title: 'Tutorial : crea tu primera aplicación con Node.js'
description: Obtén información sobre cómo empezar a crear aplicaciones Microsoft Teams con Node.js.
keywords: comenzando node.js nodejs App Studio
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 46272671443e07432513b667af424b5c5be05f2e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566546"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>Crea tu primera aplicación de Microsoft Teams con Node.js

Este tutorial le ayuda a empezar a crear una aplicación Microsoft Teams mediante Node.js.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>Descarga y aloja tu aplicación

Siga estos pasos para descargar y alojar una sencilla aplicación "hello world" en Teams.

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, necesita las siguientes herramientas. Si aún no los tienes puedes instalar desde estos enlaces.

- [Git](https://git-scm.com/downloads)
- [Node.js y NPM](https://nodejs.org/)
- Obtenga cualquier editor de texto o IDE. Puede instalar y utilizar [Visual Studio Code](https://code.visualstudio.com/download) de forma gratuita.

Si ve opciones para agregar `git` , , y a la RUTA durante la `node` `npm` `code` instalación, elija hacerlo. Será útil.

Compruebe que las herramientas están disponibles ejecutando lo siguiente en una ventana de terminal:

> [!NOTE]
> Utilice la ventana del terminal con la que se sienta más cómodo en su plataforma. Estos ejemplos utilizan Bash (que se incluye en Git), pero estos scripts se ejecutarán en la mayoría de las plataformas.

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

Es posible que tenga una versión diferente de estas aplicaciones. Esto no debería ser un problema, excepto el trago. Para gulp tendrás que usar la versión 4.0.0 o posterior.

Si no tiene gulp instalado (o tiene instalada la versión incorrecta), haga esto ahora ejecutándose `npm install gulp` en la ventana del terminal.

Si ha instalado Visual Studio Code, puede comprobar la instalación ejecutando:

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

Puede seguir utilizando esta ventana de terminal para ejecutar los comandos que siguen en este tutorial.

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>Descargue el ejemplo

¡Hemos proporcionado un simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) muestra para empezar. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo local:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Puede [posicionar](https://help.github.com/articles/fork-a-repo/) este [repositorio](https://github.com/OfficeDev/Microsoft-Teams-Samples) si desea modificar y comprobar los cambios realizados en el repositorio de GitHub para futuras referencias.

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Una vez clonado el repositorio, cambie al directorio que contiene el ejemplo:

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

Para compilar el ejemplo, debe instalar todas sus dependencias. Ejecute el siguiente comando para hacer esto:

```bash
npm install
```

Debería ver un montón de dependencias que se instalan. Una vez que hayan terminado, puede ejecutar la aplicación:

```bash
npm start
```

Cuando se inicia la aplicación hello-world, se muestra `App started listening on port 3333` en la ventana del terminal.

> [!NOTE]
> Si ve un número de puerto diferente que se muestra en el mensaje anterior, es porque tiene un conjunto de variables de entorno PORT. Puede seguir utilizando ese puerto o cambiar la variable de entorno a 3333.

En este momento, puede abrir una ventana del explorador y navegar a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se están cargando:

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>Hospede la aplicación de ejemplo

Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más capacidades. Para que la plataforma Teams cargue la aplicación, la aplicación debe ser accesible desde Internet. Para que la aplicación sea accesible desde Internet, *debes alojar* tu aplicación.

Para las pruebas locales, puede ejecutar la aplicación en el equipo local y crear un túnel con un punto de conexión web. [ngrok](https://ngrok.com) es una herramienta gratuita que te permite hacer precisamente eso. Con *ngrok* puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta DIRECCIÓN URL es solo un ejemplo). Puede [descargar e instalar](https://ngrok.com/download) *ngrok* para su entorno. Asegúrese de agregarlo a una ubicación de su `PATH` archivo .

Una vez que lo instale, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel. El ejemplo utiliza el puerto 3333, así que asegúrese de especificarlo aquí:

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* escuchará las solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333. Puedes verificar abriendo tu navegador e ir a cargar la `https://d0ac14a5.ngrok.io/hello` página de saludo de tu aplicación. Asegúrese de utilizar la dirección de reenvío mostrada por *ngrok* en la sesión de la consola en lugar de esta DIRECCIÓN URL.

> [!NOTE]
> Si ha utilizado un puerto diferente en el paso [de compilación y ejecución](#build-and-run-the-sample) anterior, asegúrese de utilizar el mismo número de puerto para configurar el túnel *ngrok.*
> [!TIP]
> Es una buena idea ejecutar *ngrok* en una ventana de terminal diferente para mantenerlo en ejecución sin interferir con la aplicación de nodo que más tarde podría tener que detener, reconstruir y volver a ejecutar. La sesión *ngrok* devolverá información útil de depuración en esta ventana.

Hay una versión de pago de *ngrok* que permite nombres persistentes. Si utiliza la versión gratuita, la aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo. Si la máquina está apagada o se va a dormir, el servicio ya no estará disponible. Recuerde esto al compartir la aplicación para pruebas por otros usuarios. Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar todos los lugares que usan esa dirección.

Recuerda, toma nota de la dirección URL de la aplicación porque necesitarás esto más adelante cuando registres la aplicación con Teams mediante App Studio. Bloc de notas funciona bien para este propósito.

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>Implemente la aplicación en Microsoft Teams

En este punto tienes una aplicación alojada en Internet, pero aún no tienes forma de decirle a Teams dónde buscarla, o incluso cómo se llama tu aplicación. Para ello ahora tienes que crear un paquete de aplicación. Esto es poco más que un archivo de texto que contiene el manifiesto de la aplicación y algunos iconos que el cliente Teams usará para mostrar y marcar correctamente la aplicación. Puede crear manualmente este paquete de aplicación o puede usar App Studio, una herramienta que se ejecuta en Teams que simplificará el proceso de registro de la aplicación. App Studio es la forma recomendada de crear y actualizar el paquete de aplicación.

Para cualquiera de los métodos necesitará lo siguiente:

- La URL donde se puede encontrar la aplicación en Internet.
- Iconos que Teams usarán para marcar la aplicación. El ejemplo viene con iconos de marcador de posición ubicados en "src\static\images. App Studio también proporcionará iconos predeterminados si es necesario.

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>Actualiza tu aplicación alojada

La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores que ha tomado nota de anteriormente:

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

La forma en que lo haces difiere en función de cómo hospedaste la aplicación. Lo importante del uso de variables de entorno es que estos valores forman parte del entorno: el código de la aplicación puede acceder a ellos, pero no están expuestos a terceros que puedan examinar los archivos que componen el sitio.

Si está ejecutando la aplicación con ngrok, deberá configurar algunas variables de entorno local. Hay muchas maneras de hacerlo, pero la más fácil, si está utilizando Visual Studio Code, es agregar una [configuración de lanzamiento:](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)

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

MICROSOFT_APP_ID y MICROSOFT_APP_PASSWORD es el ID y la contraseña, respectivamente, para el bot.
NODE_DEBUG le mostrará lo que está sucediendo en el bot en la consola de depuración de Visual Studio Code.
NODE_CONFIG_DIR apunta al directorio en la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta localmente, la busca en la carpeta src).

> [!Note]
> Si no ha detenido npm desde anteriormente en el tutorial, tendrá que ejecutarse para que Visual Studio Code recogió las variables de configuración de `npm stop` lanzamiento correctamente.

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>Configurar la pestaña de la aplicación

Una vez que instale la aplicación en un equipo, deberá configurarla para mostrar contenido. Vaya a un canal del equipo y haga clic en el botón **'+'** para agregar una nueva pestaña. A continuación, puede elegir `Hello World` entre la lista Agregar una **pestaña.** A continuación, se le presentará un cuadro de diálogo de configuración. Este cuadro de diálogo le permitirá elegir qué pestaña mostrar en este canal. Una vez que seleccione la pestaña y haga clic en `Save` puede ver la pestaña cargada con la pestaña que `Hello World` eligió:

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Prueba tu bot en Teams

Ahora puede interactuar con el bot en Teams. Elige un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` , seguido de tu mensaje. Esto se denomina **\@ mención.** Cualquier mensaje que envíe al bot se le enviará de vuelta como respuesta:

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Prueba tu extensión de mensajería

Para probar la extensión de mensajería, puede hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación. Aparecerá un menú con la aplicación **'Hello World'.** Al hacer clic en él, verá una serie de textos aleatorios. Usted puede elegir cualquiera de ellos y se insertará en su conversación:

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Elija uno de los textos aleatorios, y verá una tarjeta formateada y lista para enviar con su propio mensaje en la parte inferior:

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
