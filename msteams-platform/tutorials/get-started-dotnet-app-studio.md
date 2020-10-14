---
title: Introducción a C#/.NET
description: Empezar a compilar excelentes aplicaciones en Microsoft Teams con C#/.NET
keywords: Introducción a .net c# CSharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 3aca72a43765036c0014a9e16fa585575fe97b2e
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452851"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a>Introducción a la plataforma de Microsoft Teams con C#/.NET y app Studio

La plataforma de desarrolladores de [Microsoft Teams](/microsoftteams/) facilita la tarea de ampliar Teams e integrar sus propias aplicaciones y servicios sin problemas en el área de trabajo de Microsoft Teams. A continuación, estas aplicaciones pueden distribuirse a su empresa o a equipos de todo el mundo.

Para ampliar Microsoft Teams, tendrá que crear una aplicación de Microsoft Teams. Una aplicación de Microsoft Teams es una aplicación web que hospeda. A continuación, esta aplicación se puede integrar en el área de trabajo del usuario en Teams.

Este tutorial le ayudará a empezar a crear una aplicación de Microsoft Teams con C# en .NET. Puede probar la aplicación cargándose en un equipo para el que tenga permisos o en un inquilino de prueba creado con el programa de desarrolladores de Office.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, necesita obtener las siguientes herramientas:

- [Instalar git](https://git-scm.com/downloads)
- [Instale Visual Studio](https://www.visualstudio.com/downloads/). Puede instalar la edición gratuita de la comunidad.

Si ve una opción para agregar `git` a la ruta de acceso durante la instalación, elija esta opción. Será útil.

`git`Ejecute lo siguiente en una ventana de terminal para comprobar la instalación:
> [!NOTE]
> Use la ventana de terminal que le resulte más cómoda en su plataforma. Estos ejemplos usan Bash, pero se ejecutarán en la mayoría de las plataformas.

```bash
$ git --version
git version 2.17.1.windows.2

```

Asegúrese de iniciar la versión más reciente de Visual Studio e instale las actualizaciones si se muestran.

Puede seguir usando esta ventana de terminal para ejecutar los comandos que se indican a continuación en este tutorial.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Descargar el ejemplo

Hemos proporcionado un sencillo [Hola a todos.](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) muestra en C# para empezar. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de muestra en el equipo local:

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> Puede [bifurcar](https://help.github.com/articles/fork-a-repo/) este [repositorio](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) si desea modificar y proteger los cambios en github para futuras referencias.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Una vez que el repositorio se haya clonado, use Visual Studio para abrir el archivo `Microsoft.Teams.Samples.HelloWorld.sln` de solución desde el directorio raíz del ejemplo y haga clic en `Build Solution` desde el `Build` menú. Puede ejecutar el ejemplo presionando `F5` o eligiendo `Start Debugging` en el `Debug` menú.

Cuando se inicie la aplicación, verá una ventana del explorador abierta con la raíz de la aplicación iniciada. Puede navegar a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se cargan:

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> Si recibe un error como `Could not find a part of the path … bin\roslyn\csc.exe` , intente actualizar el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Vea [esta pregunta en stackoverflow](https://stackoverflow.com/questions/32780315) para obtener más información.

## <a name="host-the-sample-app"></a>Hospedar la aplicación de ejemplo

Recuerde que las aplicaciones de Microsoft Teams son aplicaciones web que exponen una o más capacidades. Para que la plataforma de Microsoft Teams cargue la aplicación, la aplicación debe ser accesible desde Internet. Para hacer que la aplicación sea accesible desde Internet, debe hospedar la aplicación. Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel para el proceso local en el equipo de desarrollo mediante `ngrok` . Cuando termine de hospedar la aplicación, anote su dirección URL raíz. Tendrá un aspecto similar a: `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Túnel mediante ngrok

Para realizar pruebas rápidas, puede ejecutar la aplicación en el equipo local y crear un túnel a través de un punto de conexión Web. [ngrok](https://ngrok.com) es una herramienta gratuita que le permite hacer justamente eso. Con ngrok puede obtener una dirección web como `https://d0ac14a5.ngrok.io` (esta dirección URL es solo un ejemplo). Puede [Descargar e instalar](https://ngrok.com/download) ngrok para su entorno. Asegúrese de agregarlo a una ubicación en el `PATH` .

Una vez instalado, puede abrir una nueva ventana de terminal y ejecutar el siguiente comando para crear un túnel. En el ejemplo se usa el puerto 3333, por lo que debe asegurarse de especificarlo aquí.

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok escuchará solicitudes de Internet y las enrutará a la aplicación que se ejecuta en el puerto 3333. Para comprobarlo, abra el explorador y vaya a `https://d0ac14a5.ngrok.io/hello` para cargar la página Hello de la aplicación. Asegúrese de usar la dirección de reenvío que muestra ngrok en la sesión de consola en lugar de esta dirección URL.

> [!NOTE]
> Si ha usado un puerto diferente en el paso de [compilación y ejecutar](#build-and-run-the-sample) anterior, asegúrese de que usa el mismo número de puerto para configurar el `ngrok` túnel.
> [!TIP]
> Es aconsejable ejecutar `ngrok` en una ventana de terminal diferente para mantenerla en ejecución sin interferir con la aplicación que, posteriormente, se debe detener, volver a crear y volver a ejecutar. La `ngrok` sesión devolverá información de depuración útil en esta ventana.

La aplicación solo estará disponible durante la sesión actual en el equipo de desarrollo. Si el equipo está apagado o entra en suspensión, el servicio dejará de estar disponible. Recuerde esto cuando comparta la aplicación para que la prueben otros usuarios. Si tiene que reiniciar el servicio, devolverá una nueva dirección y tendrá que actualizar todos los sitios que usen esa dirección. La versión de pago de Ngrok no tiene esta limitación.

### <a name="host-in-azure"></a>Hospedar en Azure

Microsoft Azure le permite hospedar su aplicación .NET en un nivel gratuito mediante una infraestructura compartida. Esto será suficiente para ejecutar este `Hello World` ejemplo. Consulte [creación de una nueva cuenta gratuita](https://azure.microsoft.com/free/) para obtener más información.

Visual Studio tiene compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure.

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Actualizar las credenciales de la aplicación hospedada

La aplicación de ejemplo requiere que se establezcan las siguientes variables de entorno en los valores que ha anotado anteriormente.

Abra el appsettings.jsen el archivo. Actualice el valor *MicrosoftAppId* con el identificador de bot que guardó anteriormente. Actualice *MicrosoftAppPassword* con la contraseña de bot que guardó anteriormente.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

Una vez realizados estos cambios, reconstruya la aplicación. Si usa ngrok, ejecute la aplicación localmente y, si hospeda en Azure, vuelva a implementar la aplicación.

## <a name="configure-the-app-tab"></a>Configurar la pestaña de la aplicación

Una vez que haya instalado la aplicación en un equipo, tendrá que configurarla para mostrar el contenido. Vaya a un canal del equipo en el que haya instalado la aplicación de ejemplo y haga clic en el botón **"+"** para agregar una nueva pestaña. A continuación, puede elegir `Hello World` en la lista **Agregar una pestaña** . A continuación, se mostrará un cuadro de diálogo de configuración. Este cuadro de diálogo le permitirá elegir la pestaña que desea mostrar en este canal. Una vez que seleccione la pestaña y haga clic en `Save` , puede ver la `Hello World` ficha cargada con la pestaña que eligió.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Probar el bot en Microsoft Teams

Ahora puede interactuar con el bot en Teams. Elija un canal del equipo en el que haya registrado la aplicación y escriba `@your-bot-name` . Esto se denomina una ** \@ mención**. Cualquier mensaje que envíe al bot se le enviará como respuesta.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Probar la extensión de mensajería

Para probar la extensión de mensajería, puede hacer clic en los tres puntos situados debajo del cuadro de entrada en la vista de conversación. Se mostrará un menú con la aplicación **"Hola a todos"** . Al hacer clic en él, verá una serie de textos aleatorios que aparecen. Puede elegir una de ellas y se insertará en la conversación.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Elija uno de los textos aleatorios y verá una tarjeta con formato y lista para enviar con su propio mensaje en la parte inferior.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
