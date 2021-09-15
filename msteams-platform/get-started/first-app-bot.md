---
title: 'Introducción: crear el primer bot'
author: adrianhall
description: Cree un bot para Microsoft Teams mediante el Teams Toolkit.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.localizationpriority: none
ms.openlocfilehash: 7e41de915e63b509da1db5b1cbe8e018be4d586d
ms.sourcegitcommit: 72de146d11e81fd9777374dd3915ad290fd07d82
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2021
ms.locfileid: "59360608"
---
# <a name="build-your-first-bot-for-microsoft-teams"></a>Cree el primer bot para Microsoft Teams

En este tutorial, aprenderá a crear, ejecutar e implementar una aplicación de bot de Teams. Un bot actúa como intermediario entre un usuario de Microsoft Teams y un servicio web. Los usuarios pueden chatear con un bot para obtener información rápidamente, iniciar flujos de trabajo o cualquier otra cosa que el servicio web pueda hacer. 

> [!IMPORTANT]
> Actualmente, los bots están disponibles en Government Community Cloud (GCC) pero no están disponibles en GCC-High departamento de defensa (DOD).

## <a name="before-you-begin"></a>Antes de empezar

Asegúrese de que el entorno de desarrollo está configurado mediante la instalación de los requisitos previos.

> [!div class="nextstepaction"]
> [Requisitos previos de la instalación](prerequisites.md)

## <a name="create-your-project"></a>Crear un proyecto

Use el Kit de herramientas de Teams para crear su primer proyecto:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abra Visual Studio Code.
1. Seleccione el Teams en la barra lateral para abrir el Teams Toolkit.

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Crear nuevo proyecto**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. Seleccione **Crear una nueva aplicación de Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. En la **sección Seleccionar capacidades,** **seleccione Bot**, anule la selección de **Tab** y seleccione **Aceptar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. En la **sección Registro del bot,** seleccione **Crear un nuevo registro de bot.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Seleccione Crear un nuevo registro de bot":::

1. En la **sección Lenguaje de programación,** seleccione **JavaScript**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. Seleccione una carpeta de área de trabajo.  Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que esté creando.

1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo debe contener caracteres alfanuméricos.  Presione **Entrar** para continuar.

La aplicación Teams se creará en unos segundos.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

Use la CLI de `teamsfx` para crear su primer proyecto:  Comience en la carpeta en la que quiera crear la carpeta del proyecto.

``` bash
teamsfx new
```

La CLI le guiará por varias preguntas para crear el proyecto.  En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).  Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.

1. Seleccione **Crear una nueva aplicación de Teams**.
1. Seleccione **Bot** y anule la selección de **Tab**.
1. Seleccione **Crear un nuevo registro de bot**.
1. Seleccione **JavaScript** como lenguaje de programación.
1. Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.
1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo puede contener caracteres alfanuméricos.

Una vez contestadas todas las preguntas, se crea el proyecto.

---

## <a name="take-a-tour-of-the-source-code"></a>Dar un paseo por el código fuente

Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).

Una extensión de mensajería usa [Bot Framework](https://docs.botframework.com) para permitir al usuario interactuar con el servicio a través de una conversación.  Después del scaffolding, el proyecto tendrá el siguiente aspecto:

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="Distribución de archivos de un proyecto de bot.":::

El código bot se almacena en el directorio `bot`.  Es `bot/teamsBot.js` el punto de entrada principal del bot.

> [!Tip]
> Familiarícese con los bots fuera de Teams antes de integrar su primer bot en Teams.  Para encontrar más información sobre los bots, vea los tutoriales de [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).

## <a name="run-your-app-locally"></a>Ejecutar la aplicación localmente

El Kit de herramientas de Teams le permite hospedar la aplicación localmente.  Para ello:

- Se registra una aplicación de Azure Active Directory en el inquilino de M365.
- Se envía un manifiesto de la aplicación al Centro para desarrolladores de Microsoft Teams.
- Se instala [ngrok](https://ngrok.io) y se usa para proporcionar un túnel entre Teams y el código bot.

Para crear y ejecutar la aplicación localmente:

1. Desde Visual Studio Code, presione la **tecla F5** para ejecutar la aplicación en modo de depuración.

   > Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.  Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.  Este proceso puede tardar entre 3 o 5 minutos.

1. El explorador web comienza a ejecutar la aplicación. Si se le pide que abra Teams escritorio, seleccione **Cancelar** para permanecer en el explorador. Es posible que también se le pida que cambie a Teams escritorio en otras ocasiones; seleccione la Teams web cuando esto suceda.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Captura de pantalla que muestra cómo elegir la versión web de Teams al iniciarlo":::

1. Es posible que se le pida que inicie sesión.  Si es así, inicie sesión con su cuenta de M365.
1. Cuando se le pida que instale la aplicación en Teams, seleccione **Agregar**.

   Después de cargar la aplicación, se te llevará directamente a una sesión de chat con el bot.  Puede escribir para mostrar una tarjeta de introducción y para ir a la documentación de comandos de bot y `welcome` `learn` tarjeta adaptable. 

   La depuración funciona según lo esperado, pruébelo. Abra el archivo `bot/teamsBot.js` y busque el método `onMessage()`.  Establecer un punto de interrupción en cualquier caso.  Escriba alguna cosa.

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</summary>

Al presionar la tecla **F5,** el Teams Toolkit:

1. Registra la aplicación con Azure Active Directory.
1. Registra la aplicación para la "carga lateral" en Microsoft Teams.
1. Inicia un túnel ngrok para Teams comunicarse con la aplicación.
1. Inicia Microsoft Teams con un comando para indicar a Teams que desacargue la aplicación.

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</summary>

Para ejecutar correctamente la aplicación en Teams, debe tener una cuenta de desarrollo de Microsoft 365 que permita la instalación de prueba de aplicaciones. Para obtener más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).

> [!IMPORTANT]
> Actualmente, las aplicaciones de instalación local están disponibles en Government Community Cloud (GCC), GCC-High y DOD.

> [!TIP]
> Antes de hacer la instalación de prueba de la aplicación, compruebe si hay algún problema con la [herramienta de validación de aplicaciones](https://dev.teams.microsoft.com/appvalidation.html), que se incluye en el kit de herramientas. Corrija los errores para hacer correctamente la instalación de prueba.
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary>Vea lo que ocurre al implementar la aplicación en Azure</summary>

Antes de la implementación, la aplicación se ejecuta de forma local:

1. El punto de conexión HTTP de la aplicación, donde Microsoft Teams carga la aplicación, se ejecuta de forma local.

   La implementación implica recursos de aprovisionamiento en una suscripción activa de Azure y la implementación (carga) del back-end y del código de front-end de la aplicación en Azure. El back-end usa varios servicios de Azure, como Azure App Service y Azure Bot Service.

</details>

## <a name="see-also"></a>Consulte también

* [Introducción a tutoriales](code-samples.md) 
* [Crear una aplicación con React](first-app-react.md)
* [Crear una aplicación con Blazor](first-app-blazor.md)
* [Crear una aplicación con SPFx](first-app-spfx.md)
* [Crear una aplicación con C# o .NET](get-started-dotnet-app-studio.md)
* [Crear una aplicación con Node.js](get-started-nodejs-app-studio.md)
* [Crear una aplicación con el generador de Yeoman](get-started-yeoman.md)
* [Crear una extensión de mensajería](first-message-extension.md)
* [Muestras de código](https://github.com/OfficeDev/Microsoft-Teams-Samples)
