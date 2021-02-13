---
title: 'Tutorial: crear la primera aplicación con C #'
description: Obtenga información sobre cómo empezar a compilar aplicaciones de Microsoft Teams con C# o .NET.
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: b37a8d555117e38383504dc99d82d564439a3ebf
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231534"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>Crear la primera aplicación de Teams con C# o .NET

Este tutorial le ayuda a crear una aplicación de Microsoft Teams con C# o .NET.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, debe obtener las siguientes herramientas:

- [Instalar Git](https://git-scm.com/downloads)
- [Instalar Visual Studio](https://www.visualstudio.com/downloads/). Puedes instalar la edición gratuita de la comunidad.

Durante la instalación, si hay una opción para agregar `git` a PATH, eligréla.

En una ventana de terminal, ejecute el siguiente comando para comprobar la `git` instalación:

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Usa una ventana de terminal adecuada en tu plataforma. Estos ejemplos usan Bash, pero se ejecutan en la mayoría de las plataformas.

Asegúrate de iniciar la versión más reciente de Visual Studio e instalar las actualizaciones.

Puede usar la misma ventana de terminal para ejecutar los comandos de este tutorial.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Descargar el ejemplo

Puedes empezar con un sencillo [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) muestra en C#. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio para](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) modificar y guardar los cambios en GitHub como referencia.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Después de clonar el repositorio, use Visual Studio para abrir el archivo de solución desde el directorio raíz del ejemplo y `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` seleccionarlo en el `Build` menú. Para ejecutar la muestra, `F5` pulse o elija en el `Start Debugging` `Debug` menú.

Cuando se inicia la aplicación, se abre una ventana del explorador con la raíz de la aplicación iniciada. Puedes navegar a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> Si recibe un `Could not find a part of the path … bin\roslyn\csc.exe` error, actualice el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Para obtener más información, [vea esta pregunta en StackOverflow](https://stackoverflow.com/questions/32780315).

## <a name="host-the-sample-app"></a>Hospedar la aplicación de ejemplo

Las aplicaciones de Microsoft Teams son aplicaciones web que proporcionan una o más funcionalidades. Para que la plataforma de Teams cargue la aplicación, debe ser accesible desde Internet. Para que la aplicación sea accesible desde Internet, debes hospedarla. Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel al proceso local en el equipo de desarrollo mediante `ngrok` . Cuando termine de hospedar la aplicación, anote su dirección URL raíz. Por ejemplo, `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Túnel con ngrok

Para realizar pruebas rápidas, puedes ejecutar la aplicación en el equipo local y crear un túnel a ella a través de un punto de conexión web. [ngrok](https://ngrok.com) es una herramienta gratuita con la que puede obtener una dirección web como `https://d0ac14a5.ngrok.io` . Puede descargar [e instalar](https://ngrok.com/download) ngrok. Asegúrese de agregarlo a una ubicación en el `PATH` archivo .

Después de instalar ngrok, abra una nueva ventana de terminal y ejecute el siguiente comando para crear un túnel:

```bash
ngrok http 44327 -host-header=localhost:44327
```

El ejemplo usa el puerto 44327 para asegurarse de especificarlo.

Ngrok escucha las solicitudes de Internet y las enruta a la aplicación que se ejecuta en el puerto 44327. Para comprobarlo, abre el explorador y ve `https://d0ac14a5.ngrok.io/hello` a cargar la página hello de la aplicación. En lugar de esta dirección URL, usa la dirección de reenvío que muestra ngrok en la sesión de la consola.

> [!NOTE]
> Si ha usado un puerto [](#build-and-run-the-sample) diferente en el paso de compilación y ejecución, asegúrese de usar el mismo número de puerto para configurar el `ngrok` túnel.

> [!TIP]
> Es una buena idea ejecutarse `ngrok` en una ventana de terminal diferente. Esto se hace para evitar que ngrok se ejecute sin interferir con la aplicación, que tienes que detener, recompilar y volver a ejecutar. La `ngrok` sesión proporciona información de depuración útil en esta ventana.

La aplicación solo está disponible durante la sesión actual en el equipo de desarrollo. Si la máquina se apaga o se queda en modo de suspensión, el servicio ya no está disponible. Recuerda esto cuando compartas la aplicación para realizar pruebas a otros usuarios. Si tienes que reiniciar el servicio, la aplicación devuelve una nueva dirección y debes actualizar cada ubicación que use esa dirección. La versión de pago de ngrok no tiene esta limitación.

### <a name="host-in-azure"></a>Host en Azure

Microsoft Azure hospeda la aplicación .NET en un nivel gratuito mediante la infraestructura compartida. Esto es suficiente para ejecutar el `Hello World` ejemplo. Para obtener más información, [vea crear una nueva cuenta gratuita.](https://azure.microsoft.com/free/)

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

Para probar la extensión de mensajería, puedes hacer clic en los tres puntos debajo del cuadro de entrada en la vista de conversación. Aparecerá un menú con la **aplicación "Hola** a todos". Al hacer clic en él, verás un montón de textos aleatorios que se muestran. Puede elegir cualquiera de ellos y se inserta en la conversación.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
