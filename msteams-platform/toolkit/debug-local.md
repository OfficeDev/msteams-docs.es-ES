---
title: Depurar la aplicación de Teams localmente
author: surbhigupta
description: En este módulo, aprenderá a depurar la aplicación de Teams localmente en el kit de herramientas de Teams y las características clave del kit de herramientas de Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 730317fd6480b583d7b293a4e032589d01c99db0
ms.sourcegitcommit: 707dad21dc3cf79ac831afe05096c0341bcf2fee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68653667"
---
# <a name="debug-your-teams-app-locally"></a>Depurar la aplicación de Teams localmente

Teams Toolkit le ayuda a depurar y obtener una vista previa de la aplicación de Microsoft Teams localmente. Durante el proceso de depuración, Teams Toolkit inicia automáticamente app services, inicia depuradores y carga de forma lateral la aplicación teams. Puede obtener una vista previa de la aplicación de Teams en el cliente web de Teams localmente después de la depuración.

::: zone pivot="visual-studio-code"

## <a name="debug-your-microsoft-teams-app-locally-for-visual-studio-code"></a>Depuración local de la aplicación de Microsoft Teams para Visual Studio Code

El kit de herramientas de Teams en Visual Studio Code proporciona las características para automatizar la depuración de la aplicación de Teams localmente. Visual Studio permite depurar la pestaña, el bot y la extensión de mensaje. Debe configurar Teams Toolkit antes de depurar la aplicación.

> [!NOTE]
>
> Puede actualizar el proyecto del kit de herramientas de Teams antiguo para usar nuevas tareas. Para obtener más información, consulte [el documento de configuración de depuración](https://aka.ms/teamsfx-debug-upgrade-new-tasks).

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

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal1.png" alt-text="Inicia los servicios de las aplicaciones" lightbox="../assets/images/teams-toolkit-v2/debug/Terminal1.png":::

### <a name="launches-debug-configurations"></a>Inicia las configuraciones de depuración

Inicia las configuraciones de depuración tal como se define en `.vscode/launch.json`.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="Inicia el depurador":::

En la tabla siguiente se enumeran los nombres y tipos de configuración de depuración para el proyecto con la aplicación de extensión de pestaña, bot o mensaje y Azure Functions:

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

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-locally-using-visual-studio"></a>Depuración local de la aplicación de Teams mediante Visual Studio

Teams Toolkit le ayuda a depurar y obtener una vista previa de la aplicación de Microsoft Teams localmente. Visual Studio permite depurar la pestaña, el bot y la extensión de mensaje. Puede depurar la aplicación localmente en Visual Studio mediante el kit de herramientas de Teams realizando lo siguiente:

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Configuración de ngrok (solo para la aplicación bot y extensión de mensaje)

Use un símbolo del sistema para ejecutar este comando:

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>Configurar el kit de herramientas de Teams

Realice los pasos siguientes mediante el kit de herramientas de Teams para depurar la aplicación después de crear un proyecto:

1. Haga clic con el botón derecho en el **proyecto**.
1. Seleccione **Kit de herramientas de** >  Teams **Preparar dependencias de aplicaciones de Teams**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="Dependencias de aplicaciones de Teams para la depuración local" lightbox="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png":::

   > [!NOTE]
   > En este escenario, el nombre del proyecto es MyTeamsApp1.

   La cuenta de Microsoft 365 debe tener el permiso de carga lateral antes de iniciar sesión.  Asegúrese de que la aplicación de Teams se puede cargar en el inquilino; de lo contrario, la aplicación de Teams puede no ejecutarse en el cliente de Teams.

1. Inicie sesión en su **cuenta de Microsoft 365** y seleccione **Continuar**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="Inicio de sesión en la cuenta de Microsoft 365":::

   > [!Note]
   > Para más información sobre la transferencia local de permisos, visite <https://aka.ms/teamsfx-sideloading-option>.

1. Seleccione **Depurar** > **Iniciar depuración** o seleccione directamente **F5**.

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

::: zone-end

## <a name="see-also"></a>Vea también

* [usar el kit de herramientas de Teams para aprovisionar recursos en la nube](provision.md)
* [Agregar funcionalidades a las aplicaciones de Teams](add-capability.md)
* [Implementar en la nube](deploy.md)
* [administrar varios entornos en el kit de herramientas de Teams](TeamsFx-multi-env.md)
