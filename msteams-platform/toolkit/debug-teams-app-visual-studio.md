---
author: surbhigupta
title: Depuración de la aplicación de Teams para Visual Studio
description: En este módulo, aprenderá a depurar la aplicación de Teams localmente en Visual Studio mediante el kit de herramientas de Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: cff0b3e18f63bc7943a7fc16875294f41257a37c
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027478"
---
# <a name="debug-your-teams-app-locally-using-visual-studio"></a>Depuración local de la aplicación de Teams mediante Visual Studio

Teams Toolkit le ayuda a depurar y obtener una vista previa de la aplicación de Microsoft Teams localmente. La depuración es un proceso de creación, comprobación, detección y corrección de problemas o errores en la aplicación. La depuración garantiza que el programa se ejecuta correctamente. Visual Studio permite depurar la pestaña, el bot y la extensión de mensaje. El kit de herramientas de Teams admite las siguientes características de depuración:

* Preparación de dependencias de aplicaciones de Teams
* Iniciar depuración
* Alternar puntos de interrupción
* Recarga activa
* Detener depuración

Durante el proceso de depuración, el kit de herramientas de Teams inicia automáticamente app services, inicia la depuración y carga en paralelo la aplicación Teams. Después de la depuración, puede obtener una vista previa de la aplicación de Teams en el cliente web de Teams. También puede personalizar la configuración de depuración para usar los puntos de conexión del bot o las variables de entorno para cargar la aplicación configurada.

## <a name="prerequisites"></a>Requisitos previos

| &nbsp; | Instalar | Para usar... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022, versión 17.3 | Puede instalar la edición enterprise de Visual Studio e instalar la carga de trabajo "ASP.NET" y las herramientas de desarrollo de Microsoft Teams. |
| &nbsp; | Kit de herramientas de Teams | Extensión de Visual Studio que crea un scaffolding de proyecto para la aplicación. Use la versión más reciente. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams para colaborar con todos los usuarios con los que trabaja a través de aplicaciones de chat, reuniones, llamadas, todo en un solo lugar. |
| &nbsp; | [Preparar el espacio empresarial de Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Acceso a la cuenta de Teams con los permisos adecuados para instalar una aplicación. |
| &nbsp; | [Cuenta de desarrollador de Microsoft 365](/../concepts/build-and-test/prepare-your-o365-tenant) | Acceso a la cuenta de Teams con los permisos adecuados para instalar una aplicación. |
| &nbsp; | Herramientas de Azure y [cli de Microsoft Azure](/cli/azure/install-azure-cli) | Herramientas de Azure para acceder a datos almacenados o para implementar un back-end basado en la nube para la aplicación de Teams en Azure. |
|&nbsp;  | **Optional** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok se usa para reenviar mensajes externos de Azure Bot Framework a la máquina local.|

## <a name="debug-your-app-locally"></a>Depurar la aplicación localmente

Puede depurar la aplicación localmente en Visual Studio mediante el kit de herramientas de Teams realizando lo siguiente:

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Configuración de ngrok (solo para la aplicación bot y extensión de mensaje)

Use un símbolo del sistema para ejecutar este comando:

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>Configurar el kit de herramientas de Teams

Realice los pasos siguientes mediante el kit de herramientas de Teams para depurar la aplicación después de crear un proyecto:

1. Haga clic con el botón derecho en el **proyecto**.
1. Seleccione **Kit de herramientas de Teams**.
1. Seleccione **Preparar dependencias de aplicaciones de Teams**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="Dependencias de aplicaciones de Teams para la depuración local":::

   > [!NOTE]
   > En este escenario, el nombre del proyecto es MyTeamsApp1.

   La cuenta de Microsoft 365 debe tener el permiso de carga lateral antes de iniciar sesión.  Asegúrese de que la aplicación de Teams se puede cargar en el inquilino; de lo contrario, la aplicación de Teams puede no ejecutarse en el cliente de Teams.

1. Inicie sesión en su **cuenta de Microsoft 365**.
1. Seleccione **Continue**:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="Sign in to Microsoft 365 account (Continuar inicio de sesión en la cuenta de Microsoft 365).":::
   

   > [!Note]
   > Para más información sobre la transferencia local de permisos, visite <https://aka.ms/teamsfx-sideloading-option>.

1. Seleccione **Depurar**.
1. Seleccione **Iniciar depuración** o seleccione directamente **F5**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="Iniciar depuración":::

   Visual Studio inicia la aplicación de Teams dentro del cliente de Microsoft Teams en el explorador.

   > [!Note]
   > Para más información, visite <https://aka.ms/teamsfx-vs-debug>.

1. Una vez cargado Microsoft Teams, seleccione **Agregar** para instalar la aplicación en Teams.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="Seleccione Agregar para cargar la aplicación.":::

   > [!TIP]
   > También puede usar la función de recarga activa de Visual Studio durante la depuración. Para más información, visite <https://aka.ms/teamsfx-vs-hotreload>.

   > [!NOTE]
   > Asegúrese de publicar la solicitud HTTP en "<http://localhost:5130/api/notification>" para desencadenar la notificación cuando esté depurando la aplicación del bot de notificación. Si ha seleccionado el desencadenador HTTP al crear el proyecto, puede usar cualquier herramienta de API, como curl (símbolo del sistema de Windows), Postman, etc.

   > [!TIP]
   > Si realiza algún cambio en el archivo de manifiesto de aplicación de Teams (/templates/appPackage/manifest.template.json), asegúrese de realizar el comando Preparar dependencias de aplicaciones de Teams. Antes de intentar ejecutar la aplicación de Teams de nuevo localmente.

## <a name="key-features-of-teams-toolkit"></a>Características clave del kit de herramientas de Teams

Puede ver las siguientes características clave del kit de herramientas de Teams, que automatizan el proceso de depuración local de la aplicación de Teams:

### <a name="prepare-teams-app-dependencies"></a>Preparación de dependencias de aplicaciones de Teams

Teams Toolkit prepara dependencias de depuración local y registra la aplicación de Teams en el inquilino de la cuenta. En el caso de las aplicaciones bot y extensión de mensajes, Teams Toolkit registrará y configurará el bot.

### <a name="start-debugging"></a>Iniciar depuración

Puede realizar la depuración con una sola operación, presione **F5** para iniciar la depuración. Teams Toolkit compila código, inicia servicios y la aplicación se inicia en el explorador.

### <a name="toggle-breakpoints"></a>Alternar puntos de interrupción

Puede alternar los puntos de interrupción en los códigos de origen de pestañas, bots, extensiones de mensaje y funciones de Azure. Los puntos de interrupción se ejecutan al interactuar con la aplicación Teams en el explorador web.
En la imagen siguiente se muestran la alternancia de puntos de interrupción:

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="Puntos de interrupción de alternancia de depuración local":::

### <a name="hot-reload"></a>Recarga activa

Seleccione **Recarga activa** para aplicar los cambios en la aplicación de Teams cuando quiera actualizar y guardar los códigos de origen simultáneamente durante la depuración.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="Seleccionar icono de recarga activa":::

Seleccione la opción **Recarga activa en Guardar** archivo en la lista desplegable para habilitar la recarga activa automática.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="Seleccionar recarga activa al guardar archivos":::
  
   > [!Tip]
   > Para obtener más información sobre Recarga activa función de Visual Studio durante la depuración, puede visitar <https://aka.ms/teamsfx-vs-hotreload>.

### <a name="stop-debugging"></a>Detener depuración

Seleccione **Detener depuración** cuando se complete la depuración local.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="Seleccionar icono de detención de depuración":::

## <a name="customize-debug-settings"></a>Personalizar la configuración de depuración

Puede personalizar la configuración de depuración para que la aplicación de Teams use los puntos de conexión del bot y agregue variables de entorno:

### <a name="use-your-bot-endpoint"></a>Use el punto de conexión del bot

Puede establecer la configuración de siteEndpoint en **.fx/configs/config.local.json** en el punto de conexión.

```
"bot": {
    "siteEndpoint": "https://baidu.com"
}
```

### <a name="add-environment-variables"></a>Agregar variables de entorno

Puede agregar **environmentVariables** al archivo **launchSettings.json** .

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-environment-variables.png" alt-text="Adición de variables de entorno personalizadas":::

### <a name="launch-teams-app-as-a-web-app"></a>Inicio de una aplicación de Teams como una aplicación web

Puede iniciar la aplicación de Teams como una aplicación web en lugar de ejecutarse en el cliente de Teams.

1. Seleccione **Propiedades** > **launchSettings.json** en Explorador de soluciones panel del proyecto.
1. Quite " **launchUrl"** del archivo.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="Iniciar equipos como una aplicación web mediante la eliminación de launchurl":::

1. Haga clic con el botón derecho en **Solución**.
1. Seleccione **Propiedades**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="Haga clic con el botón derecho en la solución y seleccione las propiedades":::

1. Seleccione **Configuración de propiedades** > **de** configuración en el cuadro de diálogo.
1. Seleccione la casilla **Implementar** proceso.
1. Seleccione **Aceptar**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="Desactivar la implementación en las propiedades de configuración ":::

## <a name="see-also"></a>Vea también

* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)
* [Edición del manifiesto de aplicación de Teams mediante Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
