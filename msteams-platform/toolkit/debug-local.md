---
title: Depurar la aplicación de Teams localmente
author: surbhigupta
description: En este módulo, aprenderá a depurar la aplicación de Teams localmente en el kit de herramientas de Teams y las características clave del kit de herramientas de Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 68999351232deb60015259840147d2a1ab55681a
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616565"
---
# <a name="debug-your-microsoft-teams-app-locally"></a>Depuración local de la aplicación de Microsoft Teams

Microsoft Teams Toolkit le ayuda a depurar y obtener una vista previa de la aplicación de Teams localmente. Durante el proceso de depuración, Teams Toolkit inicia automáticamente app services, inicia depuradores y carga de forma lateral la aplicación teams. Puede obtener una vista previa de la aplicación de Teams en el cliente web de Teams localmente después de la depuración. Debe configurar Teams Toolkit antes de depurar la aplicación.

## <a name="set-up-your-teams-toolkit-for-debugging"></a>Configuración del kit de herramientas de Teams para la depuración

Los pasos siguientes le ayudan a configurar el kit de herramientas de Teams antes de iniciar el proceso de depuración:

# <a name="windows"></a>[Windows](#tab/Windows)

1. Seleccione **Depurar (Edge)** o **Depurar (Chrome)** en la barra de actividad en la lista desplegable **EJECUTAR Y DEPURAR ▷** .

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Opciones del explorador":::

1. Seleccione **Ejecutar** > **depuración de inicio (F5).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Iniciar depuración":::

3. Seleccione **iniciar sesión** con su cuenta de Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Iniciar sesión":::

   > [!TIP]
   > Puede seleccionar **Más información** para obtener información sobre el Programa de Desarrolladores de Microsoft 365. Se abre el explorador web predeterminado para que pueda iniciar sesión en su cuenta de Microsoft 365 con sus credenciales.

4. Seleccione **Instalar** para instalar el certificado de desarrollo para localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="certificado":::

   > [!TIP]
   > Puede seleccionar **Más información** para conocer el certificado de desarrollo.

5. Seleccione **Sí** en el cuadro de diálogo **Advertencia de seguridad** que aparece:

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="Entidad de certificación":::

El kit de herramientas inicia una nueva instancia del explorador Edge o Chrome en función de su selección y abre una página web para cargar el cliente de Teams.  

# <a name="macos"></a>[macOS](#tab/macOS)

1. Seleccione **Depurar Edge** o **Depurar Chrome** en la lista desplegable **EJECUTAR Y DEPURAR ▷** .

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Listas del explorador":::

1. Seleccione **Iniciar depuración (F5)** o  **Ejecutar** para ejecutar la aplicación de Teams en modo de depuración.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Depuración de la aplicación":::

3. Seleccione **iniciar sesión** con su cuenta de Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="iniciar sesión en la cuenta de M365":::

   > [!TIP]
   > Puede seleccionar **Más información** para obtener información sobre el Programa de Desarrolladores de Microsoft 365. Se abrirá el explorador web predeterminado para que pueda iniciar sesión en su cuenta de Microsoft 365 con sus credenciales.

4. Seleccione **Instalar** para instalar el certificado de desarrollo para localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="certificado":::

   > [!TIP]
   > Puede seleccionar **Más información** para conocer el certificado de desarrollo.

5. Escriba **el nombre de usuario** y **la contraseña** y, a continuación, seleccione **Actualizar configuración**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="iniciar sesión en mac":::

Teams Toolkit inicia la instancia del explorador y abre una página web para cargar el cliente de Teams.

---

## <a name="debug-your-app"></a>Depuración de la aplicación

Después del proceso de configuración inicial, Teams Toolkit inicia los procesos siguientes:

* [Inicia los servicios de aplicaciones](#starts-app-services)
* [Inicia las configuraciones de depuración](#launches-debug-configurations)
* [Instala localmente la aplicación de Teams](#sideloads-the-teams-app)

### <a name="starts-app-services"></a>Inicia los servicios de aplicaciones

Ejecuta tareas como se define en `.vscode/tasks.json`.

|  Componente |  Nombre de tarea  | Folder |
| --- | --- | --- |
|  Tab |  **Iniciar front-end** |  pestañas |
|  Bot o extensión de mensajes |  **Iniciar bot** |  Bot |
|  Azure Functions |  **Iniciar back-end** |  API |

En la imagen siguiente se muestran los nombres de las tareas en las pestañas **OUTPUT** y **TERMINAL** de la Visual Studio Code mientras se ejecuta la pestaña, el bot o la extensión de mensaje y Azure Functions.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="Inicia los servicios de las aplicaciones":::

### <a name="launches-debug-configurations"></a>Inicia las configuraciones de depuración

Inicia las configuraciones de depuración tal como se define en `.vscode/launch.json`.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="Inicia el depurador":::

En la tabla siguiente se enumeran los nombres y tipos de configuración de depuración para el proyecto con la pestaña, bot o aplicación de extensión de mensaje y Azure Functions:

|  Componente |  Nombre de la configuración de depuración  | Tipo de configuración de depuración |
| --- | --- | --- |
|  Tab |  **Adjuntar a front-end (Edge)** o  **Adjuntar a front-end (Chrome)**  |  pwa-msedge o pwa-chrome  |
|  Bot o extensión de mensajes |   **Adjuntar al bot** |  pwa-node |
| Azure Functions |   **Adjuntar al back-end** |  pwa-node |

En la tabla siguiente se enumeran los nombres y tipos de configuración de depuración para el proyecto con la aplicación bot, Azure Functions y sin aplicación de pestaña:

|  Componente |  Nombre de la configuración de depuración  | Tipo de configuración de depuración  |
| --- | --- | --- |
|  Bot o extensión de mensaje  | **Iniciar bot (Edge)** o  **Iniciar bot (Chrome)**  |   pwa-msedge o pwa-chrome  |
|  Bot o extensión de mensaje  |   **Adjuntar al bot** |  pwa-node  |
|  Azure Functions |  **Adjuntar al back-end** |  pwa-node |

### <a name="sideloads-the-teams-app"></a>Instala localmente la aplicación de Teams

La configuración **Asociar a Front-end** o **Iniciar bot** inicia una instancia del explorador Edge o Chrome para cargar el cliente de Teams en la página web. Una vez cargado el cliente de Teams, Teams carga en paralelo la aplicación de Teams controlada por la dirección URL de instalación local definida en las configuraciones de inicio [de Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}). Cuando el cliente de Teams se cargue en el explorador web, seleccione **Agregar** o seleccione una opción en la lista desplegable según sus necesidades.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="Agregar depuración local" lightbox="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png":::

   La aplicación se ha agregado a Teams.

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [Depurar procesos en segundo plano](debug-background-process.md)

## <a name="see-also"></a>Vea también

* [usar el kit de herramientas de Teams para aprovisionar recursos en la nube](provision.md)
* [Agregar funcionalidades a las aplicaciones de Teams](add-capability.md)
* [Implementar en la nube](deploy.md)
* [administrar varios entornos en el kit de herramientas de Teams](TeamsFx-multi-env.md)
