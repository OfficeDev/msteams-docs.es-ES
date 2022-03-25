---
title: Depurar la aplicación de Teams
description: Depurar la aplicación de Teams localmente con el kit de herramientas de Teams
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 25a851f0dcc956139551a46b713dc2e7df3f626d
ms.sourcegitcommit: 5e5d2d3fb621bcbd9d792a5b450f95167ec8548b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2022
ms.locfileid: "63731861"
---
# <a name="debug-your-teams-app-locally"></a>Depurar la aplicación de Teams localmente

El kit de herramientas de Teams le ayuda a depurar y obtener una vista previa de la aplicación de Teams localmente. La depuración es el proceso de comprobar, detectar y corregir problemas o errores para asegurarse de que el programa se ejecuta correctamente. Visual Studio Code permite depurar pestañas, bots, extensiones de mensajería y Azure Functions. El kit de herramientas de Teams admite las siguientes características de depuración:

* [Iniciar depuración](#start-debugging)
* [ Depuración de varios destinos](#multi-target-debugging)
* [Alternar puntos de interrupción](#toggle-breakpoints)
* [Recarga activa ](#hot-reload)
* [Detener depuración](#stop-debugging)  


Durante el proceso de depuración, el kit de herramientas de Teams inicia automáticamente los servicios de aplicaciones, inicia depuradores y realiza la instalación de prueba de la aplicación Teams. La aplicación de Teams está disponible para la versión preliminar en el cliente web de Teams localmente después de la depuración. También puede personalizar la configuración de depuración para usar los puntos de conexión del bot, el certificado de desarrollo o el componente parcial de depuración para cargar la aplicación configurada.

## <a name="prerequisite"></a>Requisito previo

Instale la versión [más reciente del kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## <a name="key-features-of-teams-toolkit"></a>Características clave del kit de herramientas de Teams

#### <a name="start-debugging"></a>Iniciar depuración

Puede realizar una sola operación, seleccionar **F5** para iniciar la depuración. El kit de herramientas de Teams empieza a comprobar los requisitos previos, registrar la aplicación Azure Active Directory, registrar la aplicación de Teams, registrar el bot, iniciar servicios e iniciar el explorador.

#### <a name="multi-target-debugging"></a>Depuración de varios destinos

El kit de herramientas de Teams usa la característica de depuración de varios destinos para depurar pestañas, bots, extensiones de mensajería y Azure Functions al mismo tiempo.

#### <a name="toggle-breakpoints"></a>Alternar puntos de interrupción

Puede alternar los puntos de interrupción en los códigos fuente de pestañas, bots, extensiones de mensajería y Azure Functions. Los puntos de interrupción se ejecutan al interactuar con la aplicación Teams en un explorador web. En la imagen siguiente se muestran la alternancia de puntos de interrupción:

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="Alternar puntos de interrupción":::

#### <a name="hot-reload"></a>Recarga activa

Puede actualizar y guardar los códigos fuente de la pestaña, el bot, la extensión de mensajería y Azure Functions al mismo tiempo que depura la aplicación de Teams. La aplicación se vuelve a cargar y el depurador vuelve a asociarse a los lenguajes de programación.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="recarga activa para códigos fuente":::

#### <a name="stop-debugging"></a>Detener depuración

Al completar la depuración local, puede seleccionar **Detener** o **Desconectar** de la barra de herramientas de depuración flotante para detener todas las sesiones de depuración y finalizar las tareas. En la imagen siguiente se muestra la acción de detención de depuración:

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="detener depuración":::

## <a name="debug-your-teams-app-locally"></a>Depurar la aplicación de Teams localmente

#### <a name="1-set-up-your-teams-toolkit"></a>1. Configurar el kit de herramientas de Teams

Complete los pasos siguientes para depurar la aplicación después de crear una nueva aplicación con el kit de herramientas de Teams:

<br>

<details>
<summary><b>Windows</b></summary>

1. Seleccione **Depurar Edge** o **Depurar Chrome** en **Ejecución y depuración** desde la barra de actividades.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Opciones del explorador" border="false":::

1. Seleccione **Iniciar depuración (F5)** o  **Ejecutar** para ejecutar la aplicación de Teams en modo de depuración.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Iniciar depuración" border="false":::

3. Seleccione **iniciar sesión** con su cuenta de Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Iniciar sesión" border="true":::


   > [!TIP]
   > Puede seleccionar **Más información** para obtener información sobre el Programa de Desarrolladores de Microsoft 365. Se abrirá el explorador web predeterminado para que pueda iniciar sesión en su cuenta de Microsoft 365 con sus credenciales.

4. Seleccione **Instalar** para instalar el certificado de desarrollo para localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="certificado" border="true":::

   > [!TIP]
   > Puede seleccionar **Más información** para conocer el certificado de desarrollo.

5. Seleccione **Sí** si aparece el siguiente cuadro de diálogo:

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="Entidad de certificación" border="true":::

El kit de herramientas inicia una nueva instancia del explorador Edge o Chrome en función de su selección y abre una página web para cargar el cliente de Teams.  

</details>

<details>
<summary><b>macOS</b></summary>

1. Seleccione **Depurar Edge** o **Depurar Chrome** en **Ejecución y depuración** desde la barra de actividades.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Listas del explorador" border="false":::

1. Seleccione **Iniciar depuración (F5)** o  **Ejecutar** para ejecutar la aplicación de Teams en modo de depuración.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Depuración de la aplicación" border="false":::

3. Seleccione **iniciar sesión** con su cuenta de Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="iniciar sesión en la cuenta de M365" border="true":::

   > [!TIP]
   > Puede seleccionar **Más información** para obtener información sobre el Programa de Desarrolladores de Microsoft 365. Se abrirá el explorador web predeterminado para que pueda iniciar sesión en su cuenta de Microsoft 365 con sus credenciales.

4. Seleccione **Instalar** para instalar el certificado de desarrollo para localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="certificado" border="true":::

   > [!TIP]
   > Puede seleccionar **Más información** para conocer el certificado de desarrollo.

5. Escriba su **Nombre de usuario** y **Contraseña** y, a continuación, seleccione **Actualizar configuración** en el cuadro de diálogo siguiente:

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="iniciar sesión en mac" border="true":::

El kit de herramientas inicia una nueva instancia del explorador Edge o Chrome en función de su selección y abre una página web para cargar el cliente de Teams. 

</details>


#### <a name="2-debug-your-app"></a>2. Depurar la aplicación 

Después del proceso de configuración inicial, el kit de herramientas de Teams inicia los siguientes procesos:

  a. [Inicia los servicios de aplicaciones](#starts-app-services) </br>
  b. [inicia los depuradores](#launches-debuggers)   </br>
  c. [Instala localmente la aplicación de Teams](#sideloads-the-teams-app)
        
#### <a name="starts-app-services"></a>Inicia los servicios de aplicaciones

Ejecuta las tareas definidas en `.vscode/tasks.json` como se indica a continuación:

|  Componente |  Nombre de tarea  | Folder |
| --- | --- | --- |
|  Tab |  **Iniciar front-end** |  pestañas |
|  Extensiones de bot o mensajería |  **Iniciar bot** |  Bot |
|  Azure Functions |  **Iniciar back-end** |  api |

En la imagen siguiente se muestran los nombres de las tareas en la pestaña **Terminal** **de salida** de Visual Studio Code mientras se ejecuta la pestaña, bot o extensión de mensajería y Azure Functions.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="Inicia los servicios de las aplicaciones":::

#### <a name="launches-debuggers"></a>Inicia los depuradores

Inicia las configuraciones de depuración definidas en `.vscode/launch.json` como se indica a continuación:

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="Inicia el depurador":::

En la tabla siguiente se enumeran los tipos y nombres de configuración de depuración para el proyecto con aplicación de pestaña y aplicación de bot:

|  Componente |  Nombre de la configuración de depuración  | Tipo de configuración de depuración |
| --- | --- | --- |
|  Tab |  **Adjuntar a front-end (Edge)** o  **Adjuntar a front-end (Chrome)**  |  pwa-msedge o pwa-chrome  |
|  Extensiones de bot o mensajería |   **Adjuntar al bot** |  pwa-node |
| Azure Functions |   **Adjuntar al back-end** |  pwa-node |

En la tabla siguiente se enumeran los tipos y nombres de configuración de depuración para el proyecto con la aplicación de bot y sin la aplicación de pestaña:

|  Componente |  Nombre de la configuración de depuración  | Tipo de configuración de depuración  |
| --- | --- | --- |
|  Bot, extensión de mensajería  | **Iniciar bot (Edge)** o  **Iniciar bot (Chrome)**  |   pwa-msedge o pwa-chrome  |
|  Bot, extensión de mensajería  |   **Adjuntar al bot** |  pwa-node  |
|  Azure Functions |  **Adjuntar al back-end** |  pwa-node |

#### <a name="sideloads-the-teams-app"></a>Instala localmente la aplicación de Teams

La configuración **Adjuntar a front-end** o **Iniciar Bot** inicia una nueva instancia del explorador Edge o Chrome y abre una página web para cargar el cliente de Teams. Una vez cargado el cliente de Teams, Teams transferirá localmente la aplicación de Teams controlada por la dirección URL de instalación de prueba definida en las configuraciones de inicio [Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}).  Cuando el cliente de Teams se cargue en el explorador web, seleccione **Agregar** o seleccione uno de la lista desplegable según sus necesidades.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="depuración local" border="true":::

   La aplicación se ha agregado a Teams.

## <a name="customize-debug-settings"></a>Personalizar la configuración de depuración

El kit de herramientas de Teams le permite personalizar la configuración de depuración para crear su pestaña o bot desactivando algunos requisitos previos:

<br>

<details>
<summary><b>Use el punto de conexión del bot</b></summary>

1. En la configuración de Visual Studio Code desactive **Asegúrese de que Ngrok está instalado e iniciado (ngrok)**.

1. Establezca la configuración de botDomain y botEndpoint en `.fx/configs/localSettings.json` el dominio y en el punto de conexión.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/bot-endpoint.png" alt-text="Personaiize bot endpoint":::

</details>

<details>
<summary><b>Use el certificado de desarrollo</b></summary>

1. En la configuración de Visual Studio Code, desactive **Asegurarse de que el certificado de desarrollo es de confianza (devCert)**.

1. Establezca la configuración de sslCertFile y sslKeyFile en `.fx/configs/localSettings.json` a la ruta de acceso del archivo de certificado y la ruta de acceso del archivo de clave.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate-customize.png" alt-text="Personalizar el certificado":::

</details>

<details>
<summary><b>Use los scripts de inicio para iniciar los servicios de aplicaciones</b></summary>

1. Para la pestaña, actualice el `dev:teamsfx`script en `tabs/package.json`.

1. Para la extensión de bot o mensajería, actualice el `dev:teamsfx` script en `bot/package.json`.

1. Para Azure Functions, actualice el `dev:teamsfx` script en `api/package.json` y para TypeScript actualice el `watch:teamsfx` script.

   > [!NOTE]
   > Actualmente, la pestaña, el bot, las aplicaciones de extensión de mensajería y los puertos de Azure Functions no admiten la personalización.

</details>

<details>
<summary><b>Agregar variables de entorno</b></summary>

Puede agregar variables de entorno a `.env.teamsfx.local` archivo para pestaña, bot, extensión de mensajería y Azure Functions. Teams Toolkit carga las variables de entorno que agregó para iniciar los servicios durante la depuración local.

 > [!NOTE]
 > Asegúrese de iniciar una nueva depuración local después de agregar nuevas variables de entorno, ya que las variables de entorno no admiten la recarga activa.

</details>

<details>
<summary><b>Depurar componente parcial</b></summary>


Teams Toolkit usa la depuración de varios destinos de Visual Studio Code para depurar la pestaña, el bot, la extensión de mensajería y Azure Functions al mismo tiempo. Puede actualizar `.vscode/launch.json` y `.vscode/tasks.json` para depurar componentes parciales. Si desea depurar la pestaña solo en una pestaña más un bot con un proyecto de Azure Functions, siga estos pasos:

1. Comentario **Asociar a bot** y **Asociar a** back-end desde el compuesto de depuración en `.vscode/launch.json`

   ```json
   {
       "name": "Debug (Edge)",
        "configurations": [
           "Attach to Frontend (Edge)",
           // "Attach to Bot",
           // "Attach to Backend""
           ],
           "preLaunchTask": "Pre Debug Check & Start All",
           "presentation": {
               "group": "all",
               "order": 1
           },
           "stopAll": true

   }
   ```

2. Comentario **Iniciar** back-end e Iniciar bot desde la tarea Iniciar todo en .vscode/tasks.json

   ```json
   {
                                           
       "label": "Start All",
       "dependsOn": [
           "Start Frontend",
             // "Start Backend",
             // "Start Bot"

         ]
              
   }
   ```

</details>


## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Depurar procesos en segundo plano](debug-background-process.md).

## <a name="see-also"></a>Vea también

* [usar el kit de herramientas de Teams para aprovisionar recursos en la nube](provision.md)
* [Agregar funcionalidades a las aplicaciones de Teams](add-capability.md)
* [Implementar en la nube](deploy.md)
* [administrar varios entornos en el kit de herramientas de Teams](TeamsFx-multi-env.md)