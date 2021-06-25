---
title: 'Tutorial: crear la primera aplicación con C #'
description: Obtén información sobre cómo empezar a crear Microsoft Teams aplicaciones con C# o .NET.
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 58e11312e61124bf09fcb55d2bcd0fc475e75a49
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114618"
---
# <a name="build-your-first-teams-app-using-c"></a>Crear la primera aplicación Teams con C #

En este tutorial, aprenderás a crear tu primera aplicación Microsoft Teams con .NET o C#. También le guiará a través de los pasos para:

1. [Preparar el entorno](#prepare-your-environment)
1. [Obtener requisitos previos](#GetPrerequisites)
1. [Descargar el ejemplo](#DownloadSample)
1. [Compilar y ejecutar el ejemplo](#BuildRun)
1. [Hospedar la aplicación de ejemplo](#hostsample)
1. [Actualizar las credenciales de la aplicación hospedada](#updatecredentials)
1. [Configurar la pestaña aplicación](#configureapptab)

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, debe instalar las siguientes herramientas:

- [Instalar Git](https://git-scm.com/downloads)
- [Instalar Visual Studio](https://www.visualstudio.com/downloads/)

Puede instalar la edición de comunidad gratuita de Visual Studio. Durante la instalación, si hay una opción para agregar `git` a la ruta de acceso, selecciónelo. En una ventana de terminal, ejecute el siguiente comando para comprobar la `git` instalación:

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Usa una ventana de terminal adecuada en tu plataforma. Estos ejemplos usan Git Bash, pero se pueden ejecutar en la mayoría de las plataformas.

Abra la versión más reciente de Visual Studio e instale las actualizaciones.

Puede usar la misma ventana de terminal para ejecutar los comandos de este tutorial.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Descargar el ejemplo

You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) muestra en C#. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Puede [bifurcar este](https://help.github.com/articles/fork-a-repo/) [repositorio para](https://github.com/OfficeDev/Microsoft-Teams-Samples) modificar y guardar los cambios en GitHub.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Puede crear y ejecutar la asignación después de clonarse. 

**Para compilar y ejecutar el ejemplo clonado**

1. Abra el archivo de solución **Microsoft.Teams. Samples.HelloWorld.sln** del **directorio Microsoft-Teams-Samples/samples/app-hello-world/csharp** del ejemplo.
1. Seleccione **Generar solución** en el **menú** Generar.
1. Seleccione la **tecla F5** o seleccione **Iniciar depuración** en el **menú Depurar** para ejecutar el ejemplo.

Cuando se inicia la aplicación, se abre una ventana del explorador con la raíz de la aplicación iniciada. Puedes ir a las siguientes direcciones URL para comprobar que se están cargando todas las direcciones URL de la aplicación:

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

> [!Note]
> Si recibe un `Could not find a part of the path … bin\roslyn\csc.exe` error, actualice el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Para obtener más información, vea [esta pregunta en Stack Overflow](https://stackoverflow.com/questions/32780315).

<a name="hostsample"></a>
## <a name="deploy-your-sample-app"></a>Implementar la aplicación de ejemplo

Las aplicaciones de Microsoft Teams son aplicaciones web que proporcionan una o más funcionalidades. Para que Teams plataforma para cargar la aplicación, la aplicación debe estar disponible en Internet. Para ello, debes hospedar la aplicación. Puede hospedarlo en Microsoft Azure de forma gratuita o crear un túnel para el proceso local en el equipo mediante `ngrok` . Después de hospedar la aplicación, anote su dirección URL raíz, como `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel con ngrok

Para realizar pruebas rápidas, puedes ejecutar la aplicación en el equipo y crear un túnel para ella a través de un punto de conexión web. [`ngrok`](https://ngrok.com) es una herramienta gratuita con la que puede obtener una dirección web, como `https://d0ac14a5.ngrok.io` . Puede descargar [e instalar](https://ngrok.com/download) ngrok y agregarlo a una ubicación en su `PATH` .

Después de instalar `ngrok` , abra una nueva ventana de terminal y ejecute el siguiente comando para crear un túnel:

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` responde a las solicitudes de Internet y las enruta a la aplicación que se ejecuta en el puerto 44327. 

**Para comprobar la respuesta**

1. Abra el explorador y vaya a `https://d0ac14a5.ngrok.io/hello` . Esto cargará la página Hello de la aplicación.
1. En lugar de la dirección URL mencionada en el paso 1, usa la dirección de reenvío que se muestra en `ngrok` la sesión de la consola.
    > [!NOTE]
    > Si ha usado un puerto diferente en el paso [de](#build-and-run-the-sample) compilación y ejecución, asegúrese de usar el mismo número de puerto para configurar el `ngrok` túnel.
    > [!TIP]
    > Es una buena idea ejecutarse `ngrok` en una ventana de terminal diferente. Esto se hace para evitar `ngrok` que se ejecute sin interferir con la aplicación. Debes detener, recompilar y volver a ejecutar la aplicación. La `ngrok` sesión proporciona información de depuración útil en esta ventana.

    La aplicación solo está disponible durante la sesión actual en el equipo. Si la máquina está apagada o está en modo de suspensión, el servicio ya no estará disponible. Recuerda esto cuando compartas la aplicación para realizar pruebas a otros usuarios. Si tienes que reiniciar el servicio, la aplicación devuelve una nueva dirección y debes actualizar cada ubicación que use esa dirección. La versión de pago `ngrok` de no tiene esta limitación.

### <a name="host-in-azure"></a>Host en Azure

Microsoft Azure hospeda la aplicación .NET en un nivel gratuito mediante infraestructura compartida. Esto es suficiente para ejecutar el `Hello World` ejemplo. Para obtener más información, vea [creating a new free Azure account](https://azure.microsoft.com/free/).

Visual Studio compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure:

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

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

La aplicación de ejemplo requiere que las variables de entorno se establezcan en los valores guardados en el archivo de texto.

**Para actualizar las credenciales de la aplicación hospedada**

1. Abra el archivo `appsettings.json`. 
1. Actualice el **valor de MicrosoftAppId** con el identificador de bot que guardó en el archivo de texto. 
1. Actualice **MicrosoftAppPassword** con la contraseña del bot que guardó.

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    Después de realizar estos cambios, recompile la aplicación. Si usa ngrok, ejecute la aplicación localmente y, si está hospedando en Azure, vuelva a implementar la aplicación.

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a>Configurar la pestaña aplicación

Después de instalar la aplicación en teams, debes configurarla para mostrar el contenido. 

**Para configurar la pestaña de la aplicación**

1. Ve a un canal del equipo en el que instalaste la aplicación de ejemplo y selecciona el botón **"+"** para agregar una nueva pestaña.
1. Seleccione **Hello World** en la lista Agregar **una** pestaña. Se muestra un cuadro de diálogo de configuración que permite seleccionar la pestaña que se va a mostrar en este canal. 
1. Seleccione **Guardar**. La `Hello World` pestaña se carga con la pestaña.

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Pruebe el bot en Teams

Ahora puede probar el bot en Teams. 

**Para probar el bot**

* Selecciona un canal en el equipo donde registraste la aplicación y escribe `@your-bot-name` . Esto se denomina una **\@ mención**. El bot responde a cualquier mensaje que envíe.

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Probar la extensión de mensajería

Para probar la extensión de mensajería, seleccione **...** debajo del cuadro de entrada de la vista de conversación. Se muestra un menú con la aplicación **"Hello World".** Al seleccionarlo, se muestra un conjunto de textos aleatorios. Puede seleccionar uno de los textos aleatorios que se insertan en la conversación.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

Seleccione uno de los textos aleatorios. Se muestra una tarjeta con formato y lista para enviar con su propio mensaje.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a>Vea también

* [Introducción a tutoriales](code-samples.md)
* [Muestras de código](https://github.com/OfficeDev/Microsoft-Teams-Samples)