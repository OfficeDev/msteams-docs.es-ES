---
title: Introducción a App Studio y node. js
description: Empezar a compilar excelentes aplicaciones en Microsoft Teams con node. js y app Studio
keywords: nodo introducción. js NodeJS App Studio
ms.date: 11/09/2018
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 92fbbdd30e9cdaf54644b42bf642ca5825bcec51
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034053"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a>Introducción a la plataforma de Microsoft Teams con node. js y app Studio

La plataforma de desarrolladores de [Microsoft Teams](/microsoftteams/) facilita la tarea de ampliar Teams e integrar sus propias aplicaciones y servicios sin problemas en el área de trabajo de Microsoft Teams. A continuación, estas aplicaciones pueden distribuirse a su empresa o a equipos de todo el mundo.

Para ampliar Microsoft Teams, debe crear una aplicación de Microsoft Teams. Una aplicación de Microsoft Teams es una aplicación web que hospeda. A continuación, esta aplicación se puede integrar en el área de trabajo del usuario en Teams.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>Descargar y hospedar la aplicación

Siga estos pasos para descargar y hospedar una aplicación "Hola a todos" sencilla en Microsoft Teams.

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, necesitará las siguientes herramientas. Si todavía no los tiene, puede instalarlas desde estos vínculos.

- [Git](https://git-scm.com/downloads)
- [Node. js y NPM](https://nodejs.org/)
- Obtenga cualquier editor de texto o IDE. Puede instalar y usar [Visual Studio Code](https://code.visualstudio.com/download) de forma gratuita.

Si ve opciones para `git`agregar, `node`, `npm`y `code` a la ruta de acceso durante la instalación, elija esta opción. Será útil.

Compruebe que las herramientas están disponibles al ejecutar lo siguiente en una ventana de terminal:

> [!NOTE]
> Use la ventana de terminal que le resulte más cómoda en su plataforma. En estos ejemplos se usa Bash (que se incluye en Git), pero estos scripts se ejecutarán en la mayoría de las plataformas.

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 4.0.2
```

Es posible que tenga una versión diferente de estas aplicaciones. Esto no debería ser un problema, excepto para Gulp. Para Gulp tendrá que usar la versión 4.0.0 o posterior.

Si no tiene Gulp instalado (o tiene instalada una versión incorrecta), hágalo ahora ejecutando `npm install gulp` en la ventana de terminal.

Si ha instalado Visual Studio Code, puede comprobar la instalación ejecutando:

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

Puede seguir usando esta ventana de terminal para ejecutar los comandos que se indican a continuación en este tutorial.

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>Descargar el ejemplo

Hemos proporcionado un sencillo [Hola a todos.](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) muestra que le ayuda a empezar. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> Puede [bifurcar](https://help.github.com/articles/fork-a-repo/) este [repositorio](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) si desea modificar y proteger los cambios en el repositorio de github para futuras referencias.

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Una vez que se clona el repositorio, cambie al directorio que contiene el ejemplo:

```bash
cd msteams-samples-hello-world-nodejs
```

Para poder compilar el ejemplo, debe instalar todas sus dependencias. Ejecute el siguiente comando para hacerlo:

```bash
npm install
```

Debe ver un conjunto de dependencias que se van a instalar. Una vez que hayan finalizado, puede ejecutar la aplicación:

```bash
npm start
```

Cuando se inicia la aplicación Hello World, se muestra `App started listening on port 3333` en la ventana de terminal.

> [!NOTE]
> Si ve que aparece un número de puerto diferente en el mensaje anterior, es porque tiene establecida una variable de entorno PORT. Puede seguir usando ese puerto o cambiar la variable de entorno a 3333.

En este punto, puede abrir una ventana del explorador y navegar a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se cargan:

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>Hospedar la aplicación de ejemplo

Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más capacidades. Para que la plataforma de Microsoft Teams cargue la aplicación, la aplicación debe ser accesible desde Internet. Para hacer que la aplicación sea accesible desde Internet, debe *hospedar* la aplicación.

Para las pruebas locales, puede ejecutar la aplicación en el equipo local y crear un túnel con un punto de conexión Web. [ngrok](https://ngrok.com) es una herramienta gratuita que le permite hacer justamente eso. Con *ngrok* puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo). Puede [Descargar e instalar](https://ngrok.com/download) *ngrok* para su entorno. Asegúrese de agregarlo a una ubicación en el `PATH`.

Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel. En el ejemplo se usa el puerto 3333, por lo que debe asegurarse de especificarlo aquí.

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* escuchará solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333. `https://d0ac14a5.ngrok.io/hello` Para comprobarlo, abra el explorador y vaya a para cargar la página Hello de la aplicación. Asegúrese de usar la dirección de reenvío que muestra *ngrok* en la sesión de consola en lugar de esta dirección URL.

> [!NOTE]
> Si ha usado un puerto diferente en el paso de [compilación y ejecutar](#build-and-run-the-sample) anterior, asegúrese de usar el mismo número de puerto para configurar el túnel *ngrok* .
> [!TIP]
> Es buena idea ejecutar *ngrok* en una ventana de terminal diferente para mantenerla en ejecución sin interferir con la aplicación de nodo que, posteriormente, se debe detener, volver a crear y volver a ejecutar. La sesión de *ngrok* devolverá información de depuración útil en esta ventana.

Hay una versión de pago de *ngrok* que permite nombres persistentes. Si usa la versión gratuita, la aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo. Si el equipo está apagado o entra en suspensión, el servicio dejará de estar disponible. Recuerde esto cuando comparta la aplicación para que la prueben otros usuarios. Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar todos los sitios que usen esa dirección.

Recuerde que anote la dirección URL de la aplicación, ya que la necesitará más adelante cuando registre la aplicación con Teams mediante App Studio. El Bloc de notas funciona bien para este propósito.

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>Implementar la aplicación en Microsoft Teams

En este punto, tiene una aplicación hospedada en Internet, pero todavía no tiene ninguna manera de indicar a teams dónde buscarla, o incluso qué se llama a la aplicación. Para ello, ahora tiene que crear un paquete de la aplicación. Esto es algo más que un archivo de texto que contiene el manifiesto de la aplicación y algunos iconos que usará el cliente de Microsoft Teams para mostrar y marcar correctamente la aplicación. Puede crear manualmente este paquete de la aplicación o puede usar App Studio, una herramienta que se ejecuta en Microsoft teams que simplificará el proceso de registro de la aplicación. App Studio es la forma recomendada de crear y actualizar el paquete de la aplicación.

Para cualquiera de los dos métodos, necesitará lo siguiente:

- La dirección URL en la que se puede encontrar la aplicación en Internet.
- Iconos que los equipos usarán para personalizar la aplicación. El ejemplo incluye iconos de marcador de posición ubicados en "src\static\images. App Studio también proporcionará los iconos predeterminados, si es necesario.

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>Actualizar la aplicación hospedada

La aplicación de ejemplo requiere que se establezcan las siguientes variables de entorno en los valores que ha anotado anteriormente.

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

La forma de hacerlo varía en función de cómo hospedaste la aplicación. Lo más importante sobre el uso de variables de entorno es que estos valores forman parte de su entorno: se puede acceder a ellos mediante el código de la aplicación, pero no están expuestos a terceros que puedan examinar los archivos que componen el sitio.

Si está ejecutando la aplicación con ngrok, tendrá que configurar algunas variables de entorno local. Hay muchas formas de hacerlo, pero la más sencilla, si usa Visual Studio Code, es agregar una [configuración de inicio](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):

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
NODE_DEBUG le mostrarán lo que está sucediendo en su bot en la consola de depuración de Visual Studio Code.
NODE_CONFIG_DIR apunta al directorio de la raíz del repositorio (de forma predeterminada, cuando la aplicación se ejecuta de forma local, la busca en la carpeta src).

> [!Note]
> Si no ha detenido NPM de anteriormente en el tutorial, deberá ejecutar `npm stop` para que Visual Studio Code devuelva las variables de configuración de inicio correctamente.

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>Configurar la pestaña de la aplicación

Una vez que haya instalado la aplicación en un equipo, tendrá que configurarla para mostrar el contenido. Vaya a un canal del equipo y haga clic en el botón **"+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir en la lista **Agregar una pestaña** . A continuación, se mostrará un cuadro de diálogo de configuración. Este cuadro de diálogo le permitirá elegir la pestaña que desea mostrar en este canal. Una vez que seleccione la pestaña y haga `Save` clic en, puede `Hello World` ver la ficha cargada con la pestaña que eligió.

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" title="Captura de pantalla de configurar" />

### <a name="test-your-bot-in-teams"></a>Probar el bot en Microsoft Teams

Ahora puede interactuar con el bot en Teams. Elija un canal del equipo en el que haya registrado la aplicación y escriba `@your-bot-name`, seguido del mensaje. Esto se denomina una ** \@mención**. Cualquier mensaje que envíe al bot se le enviará como respuesta.

<img width="450px" title="Respuestas de bot" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Probar la extensión de mensajería

Para probar la extensión de mensajería, puede hacer clic en los tres puntos situados debajo del cuadro de entrada en la vista de conversación. Se mostrará un menú con la aplicación **"Hola a todos"** . Al hacer clic en él, verá un número de textos aleatorios. Puede elegir una de ellas y se insertará en la conversación.

<img width="430px" title="Menú de extensiones de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" title="Resultado de la extensión de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.

<img width="430px" title="Envío de extensiones de mensajería" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
