---
title: Cómo crear su primera extensión de mensajería
author: adrianhall
description: Cree una extensión de mensajería para Microsoft Teams con el Kit de herramientas de Teams.
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: ad341c386cc9e1bf03cf6e25c0d8be8add0880c6
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2021
ms.locfileid: "52698124"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a>Crear y ejecutar la primera extensión de mensajería para Microsoft Teams

Hay dos tipos de extensiones de mensajería **Teams**:

- [Los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) le permiten buscar sistemas externos e insertar los resultados de esa búsqueda en un mensaje con forma de tarjeta.
- Los [comandos de acción](../messaging-extensions/how-to/action-commands/define-action-command.md) le permiten presentar a los usuarios una ventana emergente modal para recopilar o mostrar información y, a continuación, procesar su interacción y enviar información de nuevo a Teams.

En este tutorial, creará un *comando de búsqueda* para buscar datos externos e insertar los resultados en un mensaje.  

## <a name="before-you-begin"></a>Antes de empezar

Instale los [requisitos previos](prerequisites.md) para garantizar que su entorno de desarrollo está configurado

> [!div class="nextstepaction"]
> [Requisitos previos de la instalación](prerequisites.md)

## <a name="create-your-project"></a>Crear un proyecto

Usar el Kit de herramientas de Teams para crear su primer proyecto:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abrir Visual Studio Code.
1. Abra el Kit de herramientas de Microsoft Teams. Para ello, seleccione el icono de Teams en la barra lateral:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="El icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Crear un nuevo proyecto**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. Seleccione **Crear una nueva aplicación de Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. En el paso **Seleccionar funcionalidades**, seleccione **Extensión de mensajería** y desmarque la opción **Pestaña**. Presione **Aceptar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. En el paso **Registro de bot**, seleccione **Crear un nuevo registro de bot**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Seleccione Crear un nuevo registro de bot":::

   > [!NOTE]
   > Las extensiones de mensajería dependen de los bots para proporcionar un diálogo entre el usuario y el código.

1. En el paso **Lenguaje de programación**, seleccione **JavaScript**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. Seleccione una carpeta (opcional).  Se creará una carpeta en la carpeta del área de trabajo para el proyecto que esté creando.

1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo puede contener caracteres alfanuméricos.  Presione **Entrar** para continuar.

La aplicación Teams se creará en unos segundos.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

Use la CLI `teamsfx` para crear su primer proyecto:  Comience en la carpeta en la que quiera crear la carpeta del proyecto.

``` bash
teamsfx new
```

La CLI le guiará por varias preguntas para crear el proyecto.  En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).  Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.

1. Seleccione **Crear una nueva aplicación de Teams**.
1. Seleccione la funcionalidad **Extensión de mensajería** y anule la selección de la funcionalidad **Pestaña**.
1. Seleccione **Crear un nuevo registro de bot**.
1. Seleccione **JavaScript** como lenguaje de programación.
1. Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.
1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo puede contener caracteres alfanuméricos.

Una vez que haya respondido a todas las preguntas, se creará el proyecto.

---

## <a name="take-a-tour-of-the-source-code"></a>Dar un paseo por el código fuente

Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).

Una extensión de mensajería usa [Bot Framework](https://docs.botframework.com) para permitir al usuario interactuar con el servicio a través de una conversación.  Después del scaffolding, el proyecto tendrá el siguiente aspecto:

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="Distribución de archivos de un proyecto de bot.":::

El código bot se almacena en el directorio `bot`.  `bots/messageExtensionBot.js` es el punto de entrada principal de la extensión de mensajería.

> [!Tip]
> Familiarícese con los bots fuera de Teams antes de integrar su primer bot en Teams.  Para encontrar más información sobre los bots, vea los tutoriales de [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).

## <a name="run-your-app-locally"></a>Ejecute la aplicación localmente

El Kit de herramientas de Teams le permite hospedar la aplicación localmente.  Para ello:

- Se registra una aplicación de Azure Active Directory en el inquilino de M365.
- Se envía un manifiesto de la aplicación al Portal para desarrolladores de Microsoft Teams.
- Se ejecuta localmente una API mediante Azure Functions Core Tools para admitir la aplicación.
- Se instala [ngrok](https://ngrok.io) y se usa para proporcionar un túnel entre Teams y la extensión de mensajería.

Para crear y ejecutar la aplicación localmente:

1. Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.

   > Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.  Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.  Este proceso puede tardar entre 3 o 5 minutos.

1. Se cargará Teams en un explorador web y se le pedirá que inicie sesión. Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador. Inicie sesión con su cuenta de M365.

1. Presione **Agregar** para agregar la aplicación a su cuenta.

Una vez que se cargue la aplicación, se le redirigirá directamente a un diálogo de búsqueda:

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="Su extensión de mensajería basada en búsquedas en acción":::

Escriba texto en el cuadro de búsqueda y, después, seleccione una de las opciones.  Se agregará una tarjeta adaptable al cuadro de entrada.

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

## <a name="next-steps"></a>Siguientes pasos

Vea otros métodos para crear aplicaciones de Teams:

- [Crear una aplicación de Teams con React](first-app-react.md)
- [Crear una aplicación de Teams con Blazor](first-app-blazor.md)
- [Crear una aplicación de Teams como elemento web de SharePoint](first-app-spfx.md) (no se necesita Azure)
- [Crear un bot de conversación](first-app-bot.md)