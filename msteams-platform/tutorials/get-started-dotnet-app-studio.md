---
title: 'Tutorial - Crea tu primera aplicación usando C #'
description: Obtén información sobre cómo empezar a crear aplicaciones Microsoft Teams con C# o .NET.
keywords: comenzando .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: eaa37f1ccb7944ee18bb62ae47882dc4a715b165
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566890"
---
# <a name="create-your-first-teams-app-using-c"></a>Crea tu primera aplicación de Teams usando C #

Este tutorial le ayuda a crear una aplicación Microsoft Teams mediante C#. Para ello, debe:

* Prepare el entorno
* Obtener requisitos previos
* Descargue el ejemplo
* Compilar y ejecutar el ejemplo
* Hospede la aplicación de ejemplo
* Actualice las credenciales de la aplicación hospedada
* Configurar la pestaña de la aplicación

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtener requisitos previos

Para completar este tutorial, debe instalar las siguientes herramientas:

- [Instalar Git](https://git-scm.com/downloads)
- [Instalar Visual Studio](https://www.visualstudio.com/downloads/)

Puede instalar la edición gratuita de la comunidad de Visual Studio. Durante la instalación, si hay una opción para agregar `git` a la ruta de acceso, selecciónela. En una ventana de terminal, ejecute el siguiente comando para comprobar la `git` instalación:

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Utilice una ventana de terminal adecuada en su plataforma. Estos ejemplos utilizan Git Bash, pero se pueden ejecutar en la mayoría de las plataformas.

Abra la versión más reciente de Visual Studio e instale cualquier actualización.

Puede utilizar la misma ventana de terminal para ejecutar los comandos en este tutorial.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Descargue el ejemplo

¡Puedes empezar con un simple [Hola, Mundo!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) muestra en C#. En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de ejemplo en el equipo:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Puede [posicionar](https://help.github.com/articles/fork-a-repo/) este [repositorio](https://github.com/OfficeDev/Microsoft-Teams-Samples) para modificar y guardar los cambios en GitHub.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Compilar y ejecutar el ejemplo

Después de clonar el repositorio, use Visual Studio para abrir el archivo de solución **Microsoft.Teams. Samples.HelloWorld.sln** del directorio **Microsoft-Teams-Samples/samples/app-hello-world/csharp** del ejemplo. A continuación, seleccione **Compilar solución** en el menú **Compilar.** Para ejecutar el ejemplo, presione **F5** o seleccione **Iniciar depuración** en el menú **Depurar.**

Cuando se inicia la aplicación, se abre una ventana del explorador con la raíz de la aplicación iniciada. Puede ir a las siguientes direcciones URL para comprobar que todas las direcciones URL de la aplicación se están cargando:

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> Si recibe un `Could not find a part of the path … bin\roslyn\csc.exe` error, actualice el paquete con el comando `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Para obtener más información, consulte [esta pregunta sobre Desbordamiento de pila](https://stackoverflow.com/questions/32780315).

## <a name="host-the-sample-app"></a>Hospede la aplicación de ejemplo

Las aplicaciones en Microsoft Teams son aplicaciones web que proporcionan una o más capacidades. Para que la plataforma Teams cargue la aplicación, la aplicación debe estar disponible en Internet. Para ello, debe hospedar la aplicación. Puede alojarlo en Microsoft Azure de forma gratuita o crear un túnel al proceso local en su ordenador mediante `ngrok` . Después de hospedar la aplicación, anote su DIRECCIÓN URL raíz, como `https://yourteamsapp.ngrok.io` o `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel usando ngrok

Para realizar pruebas rápidas, puede ejecutar la aplicación en el equipo y crear un túnel a través de un punto de conexión web. [`ngrok`](https://ngrok.com) es una herramienta gratuita con la que se puede obtener una dirección web, como `https://d0ac14a5.ngrok.io` . Puede [descargar e instalar](https://ngrok.com/download) ngrok y agregarlo a una ubicación en su `PATH` archivo .

Después de instalar `ngrok` , abra una nueva ventana de terminal y ejecute el siguiente comando para crear un túnel:

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` escucha las solicitudes de Internet y las enruta a la aplicación que se ejecuta en el puerto 44327. Para comprobarlo, abre el navegador y ve a cargar la `https://d0ac14a5.ngrok.io/hello` página de saludo de la aplicación. En lugar de esta dirección URL, utilice la dirección de reenvío que se muestra `ngrok` en la sesión de consola.

> [!NOTE]
> Si ha utilizado un puerto diferente en el paso [de compilación y ejecución,](#build-and-run-the-sample) asegúrese de utilizar el mismo número de puerto para configurar el `ngrok` túnel.

> [!TIP]
> Es una buena idea correr `ngrok` en una ventana de terminal diferente. Esto se hace para evitar `ngrok` que se ejecute sin interferir con la aplicación. Tienes que detener, reconstruir y volver a ejecutar la aplicación. La `ngrok` sesión proporciona información útil de depuración en esta ventana.

La aplicación solo está disponible durante la sesión actual en el equipo. Si la máquina está apagada o se va a dormir, el servicio ya no está disponible. Recuerde esto cuando comparta la aplicación para realizar pruebas a otros usuarios. Si tiene que reiniciar el servicio, la aplicación devuelve una nueva dirección y debe actualizar todas las ubicaciones que usan esa dirección. La versión de pago `ngrok` de no tiene esta limitación.

### <a name="host-in-azure"></a>Host en Azure

Microsoft Azure hospeda la aplicación .NET en un nivel gratuito mediante la infraestructura compartida. Esto es suficiente para ejecutar el `Hello World` ejemplo. Para obtener más información, consulte [Creación de una nueva cuenta gratuita de Azure.](https://azure.microsoft.com/free/)

Visual Studio tiene compatibilidad integrada para la implementación de aplicaciones en diferentes proveedores, incluido Azure:

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Actualice las credenciales de la aplicación hospedada

La aplicación de ejemplo requiere que las variables de entorno se establezcan en los valores que guardó en el archivo de texto.

Abra el archivo `appsettings.json`. Actualice el valor **de MicrosoftAppId** con el identificador de bot que guardó en el archivo de texto. Actualice **MicrosoftAppPassword** con la contraseña del bot que guardó.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

Una vez realizados estos cambios, vuelva a generar la aplicación. Si usa ngrok, ejecute la aplicación localmente y, si hospeda en Azure, vuelva a implementar la aplicación.

## <a name="configure-the-app-tab"></a>Configurar la pestaña de la aplicación

Una vez que instale la aplicación en un equipo, debe configurarla para mostrar contenido. Vaya a un canal del equipo donde instaló la aplicación de ejemplo y seleccione el botón **'+'** para agregar una nueva pestaña. Elija **Hello World** en la lista Agregar una **pestaña.** Se muestra un cuadro de diálogo de configuración que le permite elegir la pestaña que se va a mostrar en este canal. Después de seleccionar la pestaña y seleccionar **Guardar** la `Hello World` pestaña se carga con la pestaña.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Prueba tu bot en Teams

Ahora puede probar el bot en Teams. Seleccione un canal en el equipo donde registró la aplicación y escriba `@your-bot-name` . Esto se denomina **\@ mención.** El bot responde a cualquier mensaje que envíe.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Prueba tu extensión de mensajería

Para probar la extensión de mensajería, puede seleccionar **...** debajo del cuadro de entrada en su vista de conversación. Se muestra un menú con la aplicación **'Hello World'.** Al seleccionarlo, se muestra un conjunto de textos aleatorios. Puede seleccionar uno de los textos aleatorios y que se inserta en su conversación.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Seleccione uno de los textos aleatorios. Se muestra una tarjeta formateada y lista para enviar con su propio mensaje.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
