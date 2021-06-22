---
title: 'Introducción: Cree su primer bot de conversación'
author: adrianhall
description: Crear un bot de conversación para Microsoft Teams con el Kit de herramientas de Microsoft Teams.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 68b266b1cf9d8f7e9b4b98611d3ba982a2e18a47
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037652"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a>Cree su primer bot de conversación para Microsoft Teams

Un bot actúa como intermediario entre un usuario de Microsoft Teams y un servicio web.  Los usuarios pueden chatear con un bot para obtener información rápidamente, iniciar flujos de trabajo o cualquier otra cosa que el servicio web pueda hacer.  En este tutorial, aprenderá a crear, ejecutar e implementar una aplicación de bot de Teams.

## <a name="before-you-begin"></a>Antes de empezar

Instale los [requisitos previos](prerequisites.md) para garantizar que su entorno de desarrollo está configurado

> [!div class="nextstepaction"]
> [Requisitos previos de la instalación](prerequisites.md)

## <a name="create-your-project"></a>Crear un proyecto

Use el Kit de herramientas de Teams para crear su primer proyecto:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abra Visual Studio Code.
1. Abra el Kit de herramientas de Teams. Para ello, seleccione el icono de Teams en la barra lateral:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Crear nuevo proyecto**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. Seleccione **Crear una nueva aplicación de Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del asistente para crear un nuevo proyecto":::

1. En el paso **Seleccionar funcionalidades**, seleccione **Bot** y anule la selección de **Pestaña**. Presione **Aceptar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. En el paso **Registro de bot**, seleccione **Crear un nuevo registro de bot**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Seleccione Crear un nuevo registro de bot":::

1. En el paso **Lenguaje de programación**, seleccione **JavaScript**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. Seleccione una carpeta de área de trabajo.  Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que esté creando.

1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo puede contener caracteres alfanuméricos.  Presione **Entrar** para continuar.

La aplicación Teams se creará en unos segundos.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

Use la CLI de `teamsfx` para crear su primer proyecto:  Comience en la carpeta en la que quiera crear la carpeta del proyecto.

``` bash
teamsfx new
```

La CLI le guiará por varias preguntas para crear el proyecto.  En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).  Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.

1. Seleccione **Crear nueva aplicación de Teams**.
1. Seleccione la funcionalidad **Bot** y anule la selección de la funcionalidad **Pestaña**.
1. Seleccione **Crear un nuevo registro de bot**
1. Seleccione **JavaScript** como lenguaje de programación.
1. Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.
1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo puede contener caracteres alfanuméricos.

Una vez que haya respondido a todas las preguntas, se creará el proyecto.

---

## <a name="take-a-tour-of-the-source-code"></a>Dar un paseo por el código fuente

Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).

Una extensión de mensajería usa [Bot Framework](https://docs.botframework.com) para permitir al usuario interactuar con el servicio a través de una conversación.  Después del scaffolding, el proyecto tendrá el siguiente aspecto:

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="Distribución de archivos de un proyecto de bot.":::

El código bot se almacena en el directorio `bot`.  El `bot/teamsBot.js` es el punto de entrada principal para el bot, y los cuadros de diálogo se almacenan en el directorio `dialogs`.

> [!Tip]
> Familiarícese con los bots fuera de Teams antes de integrar su primer bot en Teams.  Para encontrar más información sobre los bots, vea los tutoriales de [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).

## <a name="run-your-app-locally"></a>Ejecutar la aplicación localmente

El Kit de herramientas de Teams le permite hospedar la aplicación localmente.  Para ello:

- Se registra una aplicación de Azure Active Directory en el inquilino de M365.
- Se envía un manifiesto de la aplicación al Centro para desarrolladores de Microsoft Teams.
- Se ejecuta localmente una API mediante Azure Functions Core Tools para admitir la aplicación.
- Se instala [ngrok](https://ngrok.io) y se usa para proporcionar un túnel entre Teams y el código bot.

Para crear y ejecutar la aplicación localmente:

1. Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.

   > Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.  Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.  Este proceso puede tardar entre 3 o 5 minutos.

1. El explorador web comienza a ejecutar la aplicación. Si se le pide que abra Teams escritorio, seleccione **Cancelar** para permanecer en el explorador. Es posible que también se le pida que cambie a Teams escritorio en otras ocasiones; seleccione la Teams web cuando esto suceda.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Captura de pantalla que muestra cómo elegir la versión web de Teams al iniciarlo":::

1. Es posible que se le pida que inicie sesión.  Si es así, inicie sesión con su cuenta de M365.
1. Cuando se le pida que instale la aplicación en Teams, presione **Agregar**.

Una vez que se cargue la aplicación, se le redirigirá directamente a una sesión de chat con el bot.  Puede escribir `intro` para que se muestre una tarjeta de introducción, y `show` para que se muestren los detalles de Microsoft Graph.  (Esto requerirá una aprobación de permisos adicional).

La depuración funciona según lo esperado, pruébelo. Abra el archivo `bot/dialogs/rootDialog.js` y busque el método `triggerCommand(...)`.  Defina un punto de interrupción en el caso predeterminado.  Escriba alguna cosa.

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</summary>

Cuando presionó F5, el Kit de herramientas de Teams:

1. Registró la aplicación con Azure Active Directory.
1. Registró la aplicación para la "instalación de prueba" en Microsoft Teams.
1. Inició el back-end de la aplicación ejecutándose de forma local con [Azure Functions Core Tools](/azure/azure-functions/functions-run-local?#start).
1. Inició un túnel de ngrok para que Teams se comunique con la aplicación.
1. Inició Microsoft Teams con un comando para indicar a Teams que haga la instalación de prueba de la aplicación.

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</summary>

Para ejecutar correctamente la aplicación en Teams, debe tener una cuenta de desarrollo de Microsoft 365 que permita la instalación de prueba de aplicaciones. Para obtener más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).

> [!TIP]
> Antes de hacer la instalación de prueba de la aplicación, compruebe si hay algún problema con la [herramienta de validación de aplicaciones](https://dev.teams.microsoft.com/appvalidation.html), que se incluye en el kit de herramientas. Corrija los errores para hacer correctamente la instalación de prueba.
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary>Vea lo que ocurre al implementar la aplicación en Azure</summary>

Antes de la implementación, la aplicación se ejecuta de forma local:

1. El back-end se ejecuta con _Azure Functions Core Tools_.
1. El punto de conexión HTTP de la aplicación, donde Microsoft Teams carga la aplicación, se ejecuta de forma local.

La implementación implica recursos de aprovisionamiento en una suscripción activa de Azure y la implementación (carga) del back-end y del código de front-end de la aplicación en Azure. El back-end usa varios servicios de Azure, como Azure App Service y Azure Bot Service.

</details>

## <a name="see-also"></a>Ver también

- [Crear una aplicación de Teams con React](first-app-react.md)
- [Crear una aplicación de Teams con Blazor](first-app-blazor.md)
- [Crear una aplicación de Teams como elemento web de SharePoint](first-app-spfx.md) (no se necesita Azure)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una extensión de mensajería](first-message-extension.md)
