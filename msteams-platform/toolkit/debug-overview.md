---
title: Depurar la aplicación de Teams
author: surbhigupta
description: En este módulo, aprenderá a depurar la aplicación de Teams en teams Toolkit y las características clave del kit de herramientas de Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 8545d4bbd97a6a4c5065c279368505f18dd5a14a
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617270"
---
# <a name="debug-your-microsoft-teams-app"></a>Depuración de la aplicación de Microsoft Teams

Microsoft Teams Toolkit le ayuda a depurar y obtener una vista previa de la aplicación de Teams. La depuración es el proceso de comprobar, detectar y corregir problemas o errores para garantizar que el programa se ejecuta correctamente en Teams.

Durante el proceso de depuración:

* El kit de herramientas de Teams inicia automáticamente los servicios de aplicaciones, inicia depuradores y descarga localmente la aplicación de Teams.
* Teams Toolkit comprueba los requisitos previos durante el proceso en segundo plano de depuración.
* La aplicación de Teams está disponible para la versión preliminar en el cliente web de Teams localmente después de la depuración.
* También puede personalizar la configuración de depuración para usar los puntos de conexión del bot, el certificado de desarrollo o el componente parcial de depuración para cargar la aplicación configurada.
* Microsoft Visual Studio Code permite depurar pestañas, bots, extensiones de mensajes y Azure Functions.

## <a name="key-debug-features-of-teams-toolkit"></a>Características clave de depuración del kit de herramientas de Teams

El kit de herramientas de Teams admite las siguientes características de depuración:

* [Iniciar depuración](#start-debugging)
* [ Depuración de varios destinos](#multi-target-debugging)
* [Alternar puntos de interrupción](#toggle-breakpoints)
* [Recarga activa ](#hot-reload)
* [Detener depuración](#stop-debugging)

Teams Toolkit realiza funciones en segundo plano durante el proceso de depuración, que incluyen la comprobación de los requisitos previos necesarios para la depuración. Puede ver el progreso del proceso de verificación en el canal de salida del kit de herramientas de Teams. En el proceso de instalación, puede registrar y configurar la aplicación de Teams.

### <a name="start-debugging"></a>Iniciar depuración

Puede presionar **F5** como una sola operación para iniciar la depuración. El kit de herramientas de Teams empieza a comprobar los requisitos previos, registra la aplicación de Azure AD, la aplicación de Teams, registra el bot, inicia los servicios e inicia el explorador.

### <a name="multi-target-debugging"></a>Depuración de varios destinos

El kit de herramientas de Teams usa la característica de depuración de varios destinos para depurar pestañas, bots, extensiones de mensajes y Azure Functions al mismo tiempo.

### <a name="toggle-breakpoints"></a>Alternar puntos de interrupción

Los puntos de interrupción en los códigos fuente de pestañas, bots, extensiones de mensajes y Azure Functions se pueden alternar. Los puntos de interrupción se ejecutan al interactuar con la aplicación Teams en un explorador web. En la imagen siguiente se muestra el punto de interrupción de alternancia:

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="Alternar puntos de interrupción" lightbox="../assets/images/teams-toolkit-v2/debug/toggle-points.png":::

### <a name="hot-reload"></a>Recarga activa

Puede actualizar y guardar los códigos de origen de tabulación, bot, extensión de mensaje y Azure Functions al mismo tiempo que depura la aplicación teams. La aplicación se vuelve a cargar y el depurador vuelve a asociarse a los lenguajes de programación.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="recarga activa para códigos fuente" lightbox="../assets/images/teams-toolkit-v2/debug/hot-reload.png":::

### <a name="stop-debugging"></a>Detener depuración

Cuando complete la depuración local, puede seleccionar **Detener (Mayús+F5)** o **[Alt] Desconectar (Mayús+F5)** en la barra de herramientas de depuración flotante para detener todas las sesiones de depuración y finalizar las tareas. En la imagen siguiente se muestra la acción de detención de depuración:

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="detener depuración":::

## <a name="prepare-for-debug"></a>Preparación para la depuración

Los pasos siguientes le ayudan a prepararse para la depuración:

### <a name="sign-in-to-microsoft-365"></a>Iniciar sesión en Microsoft 365

Si ya se ha registrado en Microsoft 365, inicie sesión en Microsoft 365. Para obtener más información, consulte [Programa para desarrolladores de Microsoft 365](tools-prerequisites.md#microsoft-365-developer-program).

### <a name="toggle-breakpoints"></a>Alternar puntos de interrupción

Asegúrese de que puede alternar los puntos de interrupción en los códigos de origen de pestañas, bots, extensiones de mensaje y Azure Functions para obtener más información, consulte [Alternar puntos de interrupción](#toggle-breakpoints).

## <a name="customize-debug-settings"></a>Personalizar la configuración de depuración

El kit de herramientas de Teams desactiva algunos requisitos previos y le permite personalizar la configuración de depuración para crear su pestaña o bot:

<br>

<details>
<summary><b>Use el punto de conexión del bot</b></summary>

1. En Visual Studio Code configuración, debe desactivar **Asegurarse de que Ngrok está instalado e iniciado (ngrok)**.

1. Puede establecer la `siteEndpoint` configuración en en el `.fx/configs/config.local.json` punto de conexión.

```json
{
    "bot": {
        "siteEndpoint": "https://your-bot-tunneling-url"
    }
}

```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/bot-endpoint.png" alt-text="Personalice el punto de conexión del bot":::

</details>

<details>
<summary><b>Use el certificado de desarrollo</b></summary>

1. En Visual Studio Code configuración, debe desactivar **Asegurarse de que el certificado de desarrollo es de confianza (devCert).**

1. Puede establecer `sslCertFile` y `sslKeyFile` configurar en la ruta de acceso del archivo de certificado y la `.fx/configs/config.local.json` ruta de acceso del archivo de clave.

```json
{
    "frontend": {
        "sslCertFile": "",
        "sslKeyFile": ""
    }
}
```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate-customize.png" alt-text="Personalizar el certificado":::

</details>

<details>
<summary><b>Use los scripts de inicio para iniciar los servicios de aplicaciones</b></summary>

1. Para la pestaña , debe actualizar `dev:teamsfx` el script en `tabs/package.json`.

1. Para la extensión de bot o mensaje, debe actualizar `dev:teamsfx` el script en `bot/package.json`.

1. Para Azure Functions, debe actualizar `dev:teamsfx` el script en `api/package.json` y para el script de actualización `watch:teamsfx` de TypeScript.

   > [!NOTE]
   > Actualmente, la pestaña, el bot, las aplicaciones de extensión de mensajes y los puertos de Azure Functions no admiten la personalización.

</details>

<details>
<summary><b>Agregar variables de entorno</b></summary>

Puede agregar variables de entorno al archivo `.env.teamsfx.local` para pestañas, bots, extensión de mensajes y Azure Functions. Teams Toolkit carga las variables de entorno que agregó para iniciar los servicios durante la depuración local.

 > [!NOTE]
 > Asegúrese de iniciar una nueva depuración local después de agregar nuevas variables de entorno, ya que las variables de entorno no admiten la recarga activa.

</details>

<details>
<summary><b>Depurar componente parcial</b></summary>

El kit de herramientas de Teams usa la depuración de varios destinos de Visual Studio Code para depurar la pestaña, el bot, la extensión de mensajes y Azure Functions al mismo tiempo. Puede actualizar `.vscode/launch.json` y `.vscode/tasks.json` para depurar componentes parciales. Si desea depurar la pestaña solo en una pestaña más un bot con un proyecto de Azure Functions, siga estos pasos:

1. Comentario **`Attach to Bot`** y **`Attach to Backend`** del compuesto de depuración en `.vscode/launch.json`.

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

2. Comentario **`Start Backend`** e inicio del bot desde la tarea Iniciar todo en .vscode/tasks.json.

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

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [Depurar la aplicación localmente](debug-local.md)

## <a name="see-also"></a>Vea también

* [Depurar procesos en segundo plano](debug-background-process.md)
* [usar el kit de herramientas de Teams para aprovisionar recursos en la nube](provision.md)
* [Implementar en la nube](deploy.md)
* [Vista previa y personalización del manifiesto de la aplicación de Teams](TeamsFx-preview-and-customize-app-manifest.md)
