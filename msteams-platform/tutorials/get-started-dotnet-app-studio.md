---
title: 'Tutorial: crear la primera aplicación con C #'
description: Obtenga información sobre cómo empezar a compilar aplicaciones de Microsoft Teams con C#/.NET.
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037042"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a>Crear la primera aplicación de Microsoft Teams con C #

Este tutorial le ayuda a empezar a crear una aplicación de Microsoft Teams con C# en .NET.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, debe obtener las siguientes herramientas:

- [Instalar Git](https://git-scm.com/downloads)
- [Instalar Visual Studio](https://www.visualstudio.com/downloads/). Puedes instalar la edición gratuita de la comunidad.

Si ve una opción para agregar a PATH durante la `git` instalación, elija hacerlo. Será útil.

Compruebe la `git` instalación ejecutando lo siguiente en una ventana de terminal:
> [!NOTE]
> Usa la ventana de terminal con la que te sientas más cómodo en tu plataforma. Estos ejemplos usan Bash, pero se ejecutarán en la mayoría de las plataformas.

```bash
$ git --version
git version 2.17.1.windows.2

```

Asegúrate de iniciar la versión más reciente de Visual Studio e instalar las actualizaciones si se muestran.

Puede seguir usando esta ventana de terminal para ejecutar los comandos siguientes en este tutorial.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Descargar el ejemplo

Hemos proporcionado un saludo [sencillo, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) muestra en C# para empezar. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio si](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) desea modificar y comprobar los cambios en GitHub para consultarlos en el futuro.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Una vez clonado el repositorio, use Visual Studio para abrir el archivo de solución desde el directorio raíz del ejemplo y haga clic `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` en el `Build` menú. Puede ejecutar la muestra presionando `F5` o eligiendo `Start Debugging` en el `Debug` menú.

Cuando se inicia la aplicación, verás una ventana del explorador abierta con la raíz de la aplicación iniciada. Puedes navegar a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> Si recibe un error como `Could not find a part of the path … bin\roslyn\csc.exe` , pruebe a actualizar el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Consulta [esta pregunta en StackOverflow para](https://stackoverflow.com/questions/32780315) obtener más detalles.

## <a name="host-the-sample-app"></a>Hospedar la aplicación de ejemplo

Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más funcionalidades. Para que la plataforma de Teams cargue la aplicación, debe ser accesible desde Internet. Para que la aplicación sea accesible desde Internet, debes hospedarla. Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel al proceso local en el equipo de desarrollo mediante `ngrok` . Cuando termines de hospedar la aplicación, toma nota de su dirección URL raíz. Tendrá un aspecto como: `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Túnel con ngrok

Para realizar pruebas rápidas, puedes ejecutar la aplicación en el equipo local y crear un túnel a ella a través de un punto de conexión web. [ngrok](https://ngrok.com) es una herramienta gratuita que te permite hacerlo. Con ngrok puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo). Puede descargar [e instalar](https://ngrok.com/download) ngrok para su entorno. Asegúrese de agregarlo a una ubicación en el `PATH` archivo .

Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel. El ejemplo usa el puerto 3333, así que asegúrate de especificarlo aquí.

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok escuchará las solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333. Para comprobarlo, abre el explorador y vas a `https://d0ac14a5.ngrok.io/hello` cargar la página hello de la aplicación. Asegúrese de usar la dirección de reenvío mostrada por ngrok en la sesión de la consola en lugar de esta dirección URL.

> [!NOTE]
> Si ha usado un puerto [](#build-and-run-the-sample) diferente en la compilación y ejecuta el paso anterior, asegúrese de usar el mismo número de puerto para configurar el `ngrok` túnel.
> [!TIP]
> Es una buena idea ejecutarse en una ventana de terminal diferente para mantenerla en funcionamiento sin interferir con la aplicación que más adelante podría tener que detener, recompilar y `ngrok` volver a ejecutar. La `ngrok` sesión devolverá información de depuración útil en esta ventana.

La aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo. Si la máquina se apaga o deja de estar en modo de suspensión, el servicio ya no estará disponible. Recuerda esto al compartir la aplicación para pruebas por parte de otros usuarios. Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar cada lugar que use esa dirección. La versión de pago de Ngrok no tiene esta limitación.

### <a name="host-in-azure"></a>Host en Azure

Microsoft Azure le permite hospedar la aplicación .NET en un nivel gratuito mediante la infraestructura compartida. Esto será suficiente para ejecutar este `Hello World` ejemplo. Vea [la creación de una nueva cuenta gratuita](https://azure.microsoft.com/free/) para obtener más información.

Visual Studio compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure.

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Actualizar las credenciales de la aplicación hospedada

La aplicación de ejemplo requiere que las siguientes variables de entorno se establezcan en los valores que has tomado nota anteriormente.

Abra el archivo appsettings.jsarchivo. Actualice el *valor de MicrosoftAppId* con el identificador de bot que guardó anteriormente. Actualice *MicrosoftAppPassword* con la contraseña del bot que guardó anteriormente.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

Una vez realizados estos cambios, vuelve a generar la aplicación. Si usa ngrok, ejecute la aplicación localmente y, si va a hospedarla en Azure, vuelva a implementarla.

## <a name="configure-the-app-tab"></a>Configurar la pestaña de la aplicación

Una vez que instales la aplicación en un equipo, deberás configurarla para mostrar contenido. Ve a un canal del equipo donde instalaste la aplicación de muestra y haz clic en el botón **"+"** para agregar una nueva pestaña. A continuación, puede `Hello World` elegir en la lista Agregar **una** pestaña. A continuación, aparecerá un cuadro de diálogo de configuración. Este cuadro de diálogo te permitirá elegir qué pestaña mostrar en este canal. Una vez que seleccione la pestaña y haga clic en esta, podrá ver la `Save` pestaña cargada con la pestaña que `Hello World` eligió.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Probar el bot en Teams

Ahora puede interactuar con el bot en Teams. Elija un canal en el equipo donde registró la aplicación y escriba `@your-bot-name` . Esto se denomina una **\@ mención.** Cualquier mensaje que envíe al bot se le enviará como respuesta.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Probar la extensión de mensajería

Para probar la extensión de mensajería, puedes hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación. Aparecerá un menú con la **aplicación "Hola** a todos". Al hacer clic en él, verás un montón de textos aleatorios que se muestran. Puede elegir cualquiera de ellos y se insertará en la conversación.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
