---
title: 'Introducción: creación de su primera aplicación de Teams con React'
author: adrianhall
description: Cree rápidamente una aplicación de Microsoft Teams en la que se muestre un mensaje de "Hola a todos" con el kit de herramientas de Microsoft Teams y React.
ms.author: adhal
ms.date: 05/18/2021
ms.topic: quickstart
ms.openlocfilehash: 4560e332834fec7b681a6b2babf3e881b5e472f7
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2021
ms.locfileid: "52698153"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a>Compilar y ejecutar su primera aplicación de Microsoft Teams con React

En este tutorial, creará una nueva aplicación de Microsoft Teams en React que implementa una aplicación personal simple para obtener información de Microsoft Graph. (Una *aplicación personal* incluye un conjunto de pestañas con ámbito para uso individual). Durante el tutorial, aprenderá sobre la estructura de una aplicación de Teams, cómo ejecutar una aplicación localmente y cómo implementar la aplicación en Azure.

La aplicación que se crea muestra información básica del usuario para el usuario actual.  Cuando se conceda permiso, la aplicación se conectará a Microsoft Graph como el usuario actual para obtener el perfil completo.

## <a name="before-you-begin"></a>Antes de empezar

Instale los [requisitos previos](prerequisites.md) para garantizar que su entorno de desarrollo está configurado

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="create-your-project"></a>Crear un proyecto

Use el Kit de herramientas de Teams para crear su primer proyecto:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abra Visual Studio Code.
1. Abra el Kit de herramientas de Teams. Para ello, seleccione el icono de Teams en la barra lateral:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Crear nuevo proyecto**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. Seleccione **Crear una nueva aplicación de Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. En el paso **Seleccionar funcionalidades**, ya estará seleccionada la funcionalidad de **Pestaña**.  Pulse **Aceptar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. En el paso **Tipo de hospedaje del front-end**, seleccione **Azure**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje para la nueva aplicación.":::

1. En el paso **Recursos de nube**, pulse **Aceptar**.  No necesitamos recursos de nube adicionales para este tutorial.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Captura de pantalla que muestra cómo agregar recursos de nube para la nueva aplicación.":::

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

1. Seleccione **Crear una nueva aplicación de Teams**.
1. Seleccione la funcionalidad de **Pestaña**.
1. Seleccione el hospedaje de front-end de **Azure**.
1. No seleccione ningún recurso de nube.
1. Seleccione **JavaScript** como lenguaje de programación.
1. Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.
1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo puede contener caracteres alfanuméricos.

Una vez que haya respondido a todas las preguntas, se creará el proyecto.

---

## <a name="take-a-tour-of-the-source-code"></a>Dar un paseo por el código fuente

Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).

Una vez que el Kit de herramientas de Teams configure el proyecto, tendrá los componentes para crear una aplicación personal básica para Teams. Los archivos y directorios del proyecto se muestran en el área del Explorador de Visual Studio Code.

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio Code.":::

El kit de herramientas crea automáticamente el scaffolding en el directorio del proyecto en función de las funcionalidades que ha agregado durante la configuración. El Kit de herramientas de Teams mantiene el estado para la aplicación en el directorio `.fx`.  Entre otros elementos de este directorio:

- Los iconos de aplicación se almacenan como archivos PNG en `color.png` y `outline.png`.
- El manifiesto de la aplicación para la publicación en el Portal de desarrolladores para Teams se almacena en `manifest.source.json`.
- La configuración que eligió al crear el proyecto se almacena en `settings.json`.

Después de seleccionar la funcionalidad de pestaña durante la configuración, el kit de herramientas de Microsoft Teams seleccionará todo el código necesario para crear una pestaña básica en el directorio `tabs`. En este directorio hay varios archivos importantes:

- `tabs/src/index.jsx` es el punto de entrada de la aplicación front-end, donde el componente `App` principal se representa con `ReactDOM.render()`.
- `tabs/src/components/App.jsx` controla el enrutamiento de URL en la aplicación. Llama al [SDK del cliente de JavaScript de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y Teams.
- `tabs/src/components/Tab.jsx` contiene el código para implementar la interfaz de usuario de la aplicación.
- `tabs/src/components/TabConfig.jsx` contiene el código para implementar la interfaz de usuario que configura la aplicación.

El tiempo de ejecución de Teams necesita varias pestañas, incluidos el aviso de privacidad, los términos de uso y las pestañas de configuración.  El código del aviso de privacidad y los términos de uso se encuentran en el mismo directorio.

Al agregar funcionalidad de nube, se agregan directorios adicionales al proyecto.  En particular, el directorio `api` contiene el código para cualquier función de Azure que escriba.

## <a name="run-your-app-locally"></a>Ejecutar la aplicación localmente

El Kit de herramientas de Teams le permite ejecutar la aplicación localmente.  Se compone de varias partes que son necesarias para proporcionar la infraestructura correcta que espera Teams:

- Una aplicación se registra con Azure Active Directory.  Esta aplicación tiene permisos asociados a la ubicación desde la que se carga la aplicación y a cualquier recurso del back-end al que accede.
- Una API web se hospeda para ayudar con las tareas de autenticación, actúa como un proxy entre la aplicación y Azure Active Directory.  Esto lo ejecuta Azure Functions Core Tools.  Se puede acceder en la dirección URL `https://localhost:5000`.
- Los recursos HTML, CSS y JavaScript que configuran el front-end de la aplicación se hospedan en un servicio local. Se puede acceder en `https://localhost:3000`.
- Se genera un manifiesto de aplicación y existe en el Portal de desarrolladores para Teams.  Teams usa el manifiesto de la aplicación para decir a los clientes conectados desde dónde cargar la aplicación.

Una vez hecho, la aplicación se puede cargar en el cliente de Teams.  Usamos el cliente web de Teams para poder ver el código HTML, CSS y JavaScript en un entorno de desarrollo web estándar.

[!INCLUDE [Adjust your browser launch settings](~/includes/get-started/browser-private-launch.md)]

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>Compilar y ejecutar la aplicación de forma local en Visual Studio Code

Para crear y ejecutar la aplicación localmente:

1. Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.

   > Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.  Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.  Este proceso puede tardar entre 3 o 5 minutos.

   El Kit de herramientas le pedirá que instale un certificado local si es necesario. Este certificado permite a Teams cargar la aplicación desde `https://localhost`. Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. Se inicia el explorador web para ejecutar la aplicación. Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador. Cuando se le pida, seleccione **Usar la aplicación web en su lugar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Captura de pantalla que muestra cómo elegir la versión web de Teams al iniciarlo":::

1. Es posible que se le pida que inicie sesión.  Si es así, inicie sesión con su cuenta de M365.
1. Cuando se le pida que instale la aplicación en Teams, presione **Agregar**.

Ahora se mostrará su aplicación:

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="Captura de pantalla de la aplicación completada":::

Puede realizar actividades de depuración normales como si se tratase de cualquier otra aplicación web (como establecer puntos de interrupción). La aplicación es compatible con "hot reloading".  Si cambia cualquier archivo dentro del proyecto, la página se volverá a cargar.

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</summary>

Cuando presionó F5, el Kit de herramientas de Teams:

1. Registró la aplicación con Azure Active Directory.
1. *Realizó la transferencia local* de la aplicación en Teams.
1. Inició el back-end de la aplicación ejecutándose de forma local con [Azure Functions Core Tools](/azure/azure-functions/functions-run-local?#start).
1. Inició el front-end de la aplicación hospedada localmente.
1. Inició Microsoft Teams en un explorador web con un comando para indicar a Teams que transfiera localmente la aplicación desde `https://localhost:3000/tab` (la dirección URL está registrada dentro del manifiesto de la aplicación).

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</summary>

Para ejecutar correctamente la aplicación en Teams, debe tener una cuenta de Teams que permita la instalación de prueba de aplicaciones. Para más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea lo que ocurre al implementar la aplicación en Azure</summary>

Antes de la implementación, la aplicación se ejecuta de forma local:

1. El back-end se ejecuta con _Azure Functions Core Tools_.
1. El punto de conexión HTTP de la aplicación, donde Microsoft Teams carga la aplicación, se ejecuta de forma local.

La implementación implica recursos de aprovisionamiento en una suscripción activa de Azure y la implementación (carga) del back-end y del código de front-end de la aplicación en Azure.

1. El back-end (si se configura) usa varios servicios de Azure, como Azure App Service y Azure Storage.
1. La aplicación front-end se implementará en una cuenta de Azure Storage configurada para hospedaje web estático.

</details>

## <a name="next-steps"></a>Siguientes pasos

Vea otros métodos para crear aplicaciones de Teams:

- [Crear una aplicación de Teams con Blazor](first-app-blazor.md)
- [Crear una aplicación de Teams como elemento web de SharePoint](first-app-spfx.md) (no se necesita Azure)
- [Crear una aplicación de bots de conversación](first-app-bot.md)
- [Crear una extensión de mensajería](first-message-extension.md)
