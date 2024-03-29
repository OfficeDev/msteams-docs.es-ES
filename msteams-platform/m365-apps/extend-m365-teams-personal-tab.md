---
title: Ampliar una aplicación de pestaña personal de Teams en Microsoft 365
description: Obtenga información sobre cómo actualizar la aplicación de pestaña personal para que se ejecute en Outlook y Office, además de Microsoft Teams.
ms.date: 10/10/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 910a94f34d14c8dbb8a35099d438469fea52155b
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789985"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Ampliar una pestaña personal de Teams en Microsoft 365

Las pestañas personales proporcionan una excelente manera de mejorar la experiencia de Microsoft Teams. Con las pestañas personales, puede proporcionar a un usuario acceso a su aplicación directamente en Teams, sin que el usuario tenga que salir de la experiencia ni volver a iniciar sesión. Con esta versión preliminar, las pestañas personales pueden iluminarse dentro de otras aplicaciones Microsoft 365. En este tutorial se muestra el proceso de tomar una pestaña personal de Teams existente y actualizarla para que se ejecute en las experiencias web y de escritorio de Outlook y Office, así como en la aplicación de Office para Android.

La actualización de la aplicación personal para que se ejecute en Outlook y Office implica estos pasos:

> [!div class="checklist"]
>
> * [Actualice el manifiesto de la aplicación](#update-the-app-manifest).
> * [Actualice las referencias del SDK de TeamsJS](#update-sdk-references).
> * [Modifique los encabezados de la directiva de seguridad de contenido](#configure-content-security-policy-headers).
> * Actualice el registro de aplicaciones [de Microsoft Azure Active Directory (Azure AD) para Sign-On único (SSO).](#update-azure-ad-app-registration-for-sso)
> * [Transferir localmente la aplicación actualizada en Teams](#sideload-your-app-in-teams).

El resto de esta guía le guiará por estos pasos y le mostrará cómo obtener una vista previa de la pestaña personal en otras aplicaciones de Microsoft 365.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, necesita:

* Una cuenta empresarial de espacio aislado del Programa de desarrolladores de Microsoft 365
* El inquilino de espacio aislado inscrito en *Versiones dirigidas de Office 365*
* Una máquina con aplicaciones de Office instaladas desde el *canal beta* Aplicaciones de Microsoft 365
* (Opcional) Un dispositivo Android o emulador con una aplicación de Office para Android instalada e inscrita en el *programa beta*
* (Opcional) extensión [Teams Toolkit](https://aka.ms/teams-toolkit) para Microsoft Visual Studio Code para ayudar a actualizar el código

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Preparar la pestaña personal para la actualización

Si tiene una aplicación de pestaña personal existente, realice una copia o una rama del proyecto de producción para probar y actualice el identificador de aplicación en el manifiesto de la aplicación para usar un nuevo identificador (distinto del identificador de aplicación de producción, para las pruebas).

Si desea usar código de ejemplo para completar este tutorial, siga los pasos de configuración del [ejemplo de lista de](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) tareas pendientes para compilar una aplicación de pestaña personal mediante la extensión Teams Toolkit para Visual Studio Code y, a continuación, vuelva a este artículo para actualizarla para Microsoft 365.

Como alternativa, puede usar una aplicación básica de inicio de sesión único *hola mundo* ya habilitada para Microsoft 365 en la siguiente sección [de inicio rápido](#quickstart) y, a continuación, pasar a transferir localmente [la aplicación en Teams](#sideload-your-app-in-teams).

### <a name="quickstart"></a>Inicio rápido

Para empezar con una [pestaña personal](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365) que ya esté habilitada para ejecutarse en Outlook y Office, use la extensión kit de herramientas de Teams para Visual Studio Code.

1. En Visual Studio Code, abra la paleta de comandos (`Ctrl+Shift+P`), escriba `Teams: Create a new Teams app`.
1. Seleccione la opción **Crear una nueva aplicación de Teams**.
1. Seleccione la **pestaña Personal habilitada para SSO**.

    :::image type="content" source="images/toolkit-tab-sample.png" alt-text="La captura de pantalla es un ejemplo que muestra el ejemplo lista de tareas pendientes (funciona en Teams, Outlook y Office) en el kit de herramientas de Teams.":::
1. Seleccione el lenguaje de programación preferido.
1. Seleccione una ubicación en la máquina local para la carpeta del área de trabajo y escriba el nombre de la aplicación.
1. Abra la paleta de comandos (`Ctrl+Shift+P`) y escriba `Teams: Provision in the cloud` para crear los recursos de aplicación necesarios (plan de App Service, cuenta de almacenamiento, aplicación de funciones, identidad administrada) en la cuenta de Azure.
1. Seleccione una suscripción y un grupo de recursos.
1. Seleccione **Aprovisionar**.
1. Abra la paleta de comandos (`Ctrl+Shift+P`) y escriba `Teams: Deploy to the cloud` para implementar el código de muestra en los recursos aprovisionados en Azure e iniciar la aplicación.
1. Seleccione **Implementar**.

Desde aquí, puede ir directamente a [transferir localmente la aplicación en Teams](#sideload-your-app-in-teams) y obtener una vista previa de la aplicación en Outlook y Office. (El manifiesto de la aplicación y las llamadas api de TeamsJS ya se han actualizado para Microsoft 365).

## <a name="update-the-app-manifest"></a>Actualización del manifiesto de la aplicación

Debe usar la versión `1.13` del esquema del [manifiesto para desarrolladores de Teams](../resources/schema/manifest-schema.md) para permitir que la pestaña personal de Teams se ejecute en Outlook y Office.

Tienes dos opciones para actualizar el manifiesto de la aplicación:

# <a name="teams-toolkit"></a>[Kit de herramientas de Teams](#tab/manifest-teams-toolkit)

1. Abra la paleta de comandos: `Ctrl+Shift+P`.
1. Ejecute el comando `Teams: Upgrade Teams manifest` y seleccione el archivo de manifiesto de la aplicación. Se realizarán cambios en el sitio.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abra el manifiesto de la aplicación de Teams y actualice `$schema` y `manifestVersion` con los siguientes valores:

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Si ha usado el Kit de herramientas de Teams para crear su aplicación personal, también puede usarlo para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta de comandos (`Ctrl+Shift+P`) y busque **Teams: Validar archivo de manifiesto**.

## <a name="update-sdk-references"></a>Actualizar referencias del SDK

Para ejecutarse en Outlook y Office, la aplicación debe hacer referencia al paquete `@microsoft/teams-js@2.0.0` npm (o superior). Aunque el código con versiones de nivel inferior se admite en Outlook y Office, se registran advertencias de desuso y la compatibilidad con versiones de nivel inferior de TeamsJS en Outlook y Office terminará finalmente.

Puede usar Teams Toolkit para ayudar a identificar y automatizar los cambios de código necesarios para actualizar de las versiones 1.x TeamsJS a TeamsJS versión 2.x.x. Como alternativa, puede realizar los mismos pasos manualmente; Consulte [el SDK de cliente de JavaScript de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) para obtener más información.

1. Abra la *paleta Comandos*: `Ctrl+Shift+P`.
1. Ejecute el comando `Teams: Upgrade Teams JS SDK and code references`.

Al finalizar, el archivo *package.json* hará referencia `@microsoft/teams-js@2.0.0` (o superior) y `*.js/.ts` los archivos y `*.jsx/.tsx` se actualizarán con:

> [!div class="checklist"]
>
> * Instrucciones de importación para teams-js@2.x.x
> * [Llamadas de función, enumeración e interfaz](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) para teams-js@2.x.x
> * `TODO`recordatorios de comentarios que marcan las áreas que podrían verse afectadas por los cambios en la interfaz [de contexto](../tabs/how-to/using-teams-client-sdk.md#updates-to-the-context-interface)
> * `TODO` recordatorios de comentario para [convertir las funciones de devolución de llamada a promesas](../tabs/how-to/using-teams-client-sdk.md#callbacks-converted-to-promises)

> [!IMPORTANT]
> El código dentro *de.html* archivos no es compatible con las herramientas de actualización y requiere cambios manuales.

## <a name="configure-content-security-policy-headers"></a>Configurar encabezados de directiva de seguridad de contenido

Al igual que en Microsoft Teams, las aplicaciones de tabulación se hospedan dentro de [elementos iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) en clientes web de Office y Outlook.

Si la aplicación usa encabezados de [directiva de seguridad de contenido](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP), asegúrese de permitir todos los siguientes [antecesores de marco](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) en los encabezados de CSP:

|host de Microsoft 365| permiso de antecesor de marco|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.microsoft365.com`, `*.office.com` |
| Outlook | `outlook.live.com`, `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Actualización del registro de aplicaciones de Azure AD para SSO

[El inicio de sesión único (SSO) de Azure Active Directory (AD)](../tabs/how-to/authentication/tab-sso-overview.md) para pestañas personales funciona de la misma manera en Office y Outlook que en Teams. Sin embargo, debe agregar varios identificadores de aplicación cliente al registro de aplicaciones de Azure AD de la aplicación de pestaña en el portal *de Registros de aplicaciones* del inquilino.

1. Inicie sesión en [Microsoft Azure Portal](https://portal.azure.com) con su cuenta empresarial de espacio aislado.
1. Abra la hoja **Registros de aplicaciones**.
1. Seleccione el nombre de la aplicación para abrir el registro de la aplicación.
1. Seleccione **Exponer una API** (en *Administrar*).

    :::image type="content" source="images/azure-app-registration-clients.png" alt-text="La captura de pantalla es un ejemplo que muestra los identificadores de cliente de autorización de la hoja *Registros de aplicaciones* en Azure Portal.":::

1. En la sección **Aplicaciones cliente autorizadas** asegúrese de que aparecen todos los siguientes valores `Client Id`:

    |Microsoft 365 aplicación cliente | Id. de cliente |
    |--|--|
    |Escritorio de Teams, móvil |1fec8e78-bli4-4aaf-ab1b-5451cc387264 |
    |Web de Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
    |Web de Office  |4765445b-32c6-49b0-83e6-1d93765276ca|
    |Escritorio de Office  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
    |Office Mobile  | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Escritorio de Outlook, móvil | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook web | bc59ab01-8403-45c6-8796-ac3ef710b3e3|

    > [!NOTE]
    > Algunas aplicaciones cliente de Microsoft 365 comparten identificadores de cliente.

## <a name="sideload-your-app-in-teams"></a>Transferir localmente la aplicación en Teams

El último paso para ejecutar la aplicación en Office y Outlook es transferir localmente el [paquete de aplicación](..//concepts/build-and-test/apps-package.md) de pestaña personal actualizado en Microsoft Teams.

1. Empaquete la aplicación de Teams ([manifiesto](../resources/schema/manifest-schema.md) e [iconos de aplicación](/microsoftteams/platform/resources/schema/manifest-schema#icons)) en un archivo ZIP. Si usó el Kit de herramientas de Teams para crear la aplicación, puede hacerlo fácilmente con la opción **Comprimir paquete de metadatos de Teams** en el menú de **Implementación** del Kit de herramientas de Teams.

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="&quot;La captura de pantalla es un ejemplo que muestra la opción Zip Teams metadata package&quot; (Paquete de metadatos de Zip Teams) en la extensión del kit de herramientas de Teams para Visual Studio Code.":::

1. Inicie sesión en Teams con su espacio empresarial aislado y alterne al modo *Vista previa para desarrolladores*. Seleccione el menú de los puntos suspensivos (**...**) junto al perfil de usuario y, luego, seleccione **Acerca de** > **Vista previa para desarrolladores**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="En la captura de pantalla se describe cómo seleccionar la opción &quot;Versión preliminar para desarrolladores&quot;.":::

1. Seleccione **Aplicaciones** para abrir el panel **Administrar aplicaciones**. A continuación, seleccione **Cargar una aplicación**.

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra las opciones Administrar aplicaciones y Publicar una aplicación.":::

1. Elija **la opción Cargar una aplicación personalizada** y seleccione el paquete de la aplicación.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción de cargar una aplicación en Teams.":::

Después de transferirla localmente a Teams, la pestaña personal está disponible en Outlook y Office. Debe iniciar sesión con las mismas credenciales que usó para transferir localmente la aplicación a Teams. Al ejecutar la aplicación de Office para Android, debe reiniciar la aplicación para usar la aplicación de pestaña personal desde la aplicación de Office.

Puedes anclar la aplicación para obtener acceso rápido o encontrarla en los puntos suspensivos (**...**) entre las aplicaciones recientes en la barra lateral de la izquierda. Anclar una aplicación en Teams no la ancla como una aplicación en Office o Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Obtener una vista previa de su pestaña personal en otras experiencias de Microsoft 365

Aquí se muestra cómo obtener una vista previa de la aplicación que se ejecuta en Office y Outlook, clientes de escritorio web y Windows.

> [!NOTE]
> Si usa la aplicación de ejemplo Kit de herramientas de Teams y la desinstala de Teams, se quita de los catálogos **Más aplicaciones** en Outlook y Office.

### <a name="outlook-on-windows"></a>Outlook en Windows

Para obtener una vista previa de la aplicación ejecutándose en Outlook en el escritorio de Windows:

1. Inicie Outlook e inicie sesión con su cuenta de inquilino de desarrollo.
1. En la barra lateral, seleccione  **Más aplicaciones**. El título de la aplicación de prueba aparece entre las aplicaciones instaladas.
1. Seleccione el icono de la aplicación para iniciar la aplicación en Outlook.

    :::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción puntos suspensivos (Más aplicaciones) en la barra lateral del cliente de escritorio de Outlook para ver las pestañas personales instaladas.":::

### <a name="outlook-on-the-web"></a>Outlook en la Web

Para ver la aplicación en Outlook en la Web:

1. Vaya a [Outlook en la Web](https://outlook.office.com) e inicie sesión con su cuenta de inquilino de desarrollo.
1. En la barra lateral, seleccione  **Más aplicaciones**. El título de la aplicación de prueba aparece entre las aplicaciones instaladas.
1. Seleccione el icono de la aplicación para iniciar y obtener una vista previa de la aplicación que se ejecuta en Outlook en la Web.

    :::image type="content" source="images/outlook-web-more-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción puntos suspensivos (Más aplicaciones) en la barra lateral de outlook.com para ver las pestañas personales instaladas.":::

### <a name="office-on-windows"></a>Office en Windows

Para ver la aplicación que se ejecuta en Office en el escritorio de Windows:

1. Inicie Office e inicie sesión con su cuenta de inquilino de desarrollo.
1. Seleccione el icono **Aplicaciones** en la barra lateral. El título de la aplicación de prueba aparece entre las aplicaciones instaladas.
1. Seleccione el icono de la aplicación para iniciar la aplicación en Office.

    :::image type="content" source="images/office-desktop-more-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción puntos suspensivos (Más aplicaciones) en la barra lateral del cliente de escritorio de Office para ver las pestañas personales instaladas.":::

### <a name="office-on-the-web"></a>Office en la Web

Para obtener una vista previa de la aplicación que se ejecuta en Outlook en la Web:

1. Inicie sesión en **office.com** con credenciales de inquilino de prueba.
1. Seleccione el icono **Aplicaciones** en la barra lateral. El título de la aplicación de prueba aparece entre las aplicaciones instaladas.
1. Seleccione el icono de la aplicación para iniciar la aplicación en Office en la Web.

    :::image type="content" source="images/office-web-more-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción (Más aplicaciones) en la barra lateral de office.com para ver las pestañas personales instaladas.":::

### <a name="office-app-for-android"></a>Aplicación de Office para Android

> [!NOTE]
> Antes de instalar la aplicación, realice [los pasos necesarios para instalar la versión beta de la aplicación de Office más reciente](prerequisites.md#mobile) y formar parte del programa beta.

Para ver la aplicación que se ejecuta en la aplicación de Office para Android:

1. Inicie la aplicación de Office e inicie sesión con su cuenta de inquilino de desarrollo. Si la aplicación de Office para Android ya se estaba ejecutando antes de transferir localmente la aplicación en Teams, debe reiniciarla para poder verla en las aplicaciones instaladas.
1. Seleccione el icono **Aplicaciones** . La aplicación de instalación local aparece entre las aplicaciones instaladas.
1. Seleccione el icono de la aplicación para iniciar la aplicación en la aplicación de Office para Android.

    :::image type="content" source="images/office-mobile-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción &quot;Aplicaciones&quot; en la barra lateral de la aplicación de Office para ver las pestañas personales instaladas.":::

## <a name="troubleshooting"></a>Solución de problemas

Actualmente, se admite un subconjunto de tipos y funcionalidades de aplicaciones de Teams en los clientes de Outlook y Office. Esta compatibilidad se expande con el tiempo.

Consulte [compatibilidad con Microsoft 365](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook) para comprobar la compatibilidad del host con varias funcionalidades de TeamsJS.

Para obtener un resumen general de la compatibilidad del host y la plataforma de Microsoft 365 con las aplicaciones de Teams, consulte [Extensión de aplicaciones de Teams en Microsoft 365](overview.md).

Puede comprobar la compatibilidad del host de una funcionalidad determinada en tiempo de ejecución llamando a la `isSupported()` función en esa funcionalidad (espacio de nombres) y ajustando el comportamiento de la aplicación según corresponda. Esto permite a la aplicación iluminar la interfaz de usuario y la funcionalidad en los hosts que la admiten y proporcionar una experiencia de reserva correcta en los hosts que no lo hacen. Para obtener más información, consulta [Diferenciar la experiencia de la aplicación](../tabs/how-to/using-teams-client-sdk.md#differentiate-your-app-experience).

Use los [canales de la comunidad de desarrolladores de Microsoft Teams](/microsoftteams/platform/feedback) para notificar problemas y enviar comentarios.

### <a name="debugging"></a>Depuración

Desde El kit de herramientas de Teams, puede depurar (`F5`) la aplicación de pestaña que se ejecuta en Office y Outlook, además de Teams.

:::image type="content" source="images/toolkit-debug-targets.png" alt-text="La captura de pantalla es un ejemplo que muestra el menú desplegable de depuración en Teams en el kit de herramientas de Teams.":::

Tras la primera ejecución de depuración local en Office o Outlook, se le pedirá que inicie sesión en su cuenta de inquilino de Microsoft 365 e instale un certificado de prueba autofirmado. También se le pedirá que instale Teams manualmente. Seleccione **Instalar en Teams** para abrir una ventana del explorador e instalar manualmente la aplicación. A continuación, seleccione **Continuar** para continuar con la depuración de la aplicación en Office/Outlook.

:::image type="content" source="images/toolkit-dialog-teams-install.png" alt-text="La captura de pantalla es un ejemplo que muestra el cuadro de diálogo Kit de herramientas que se va a instalar en Teams.":::

Proporcione comentarios e informe de cualquier problema con la experiencia de depuración del kit de herramientas de Teams en [Microsoft Teams Framework (TeamsFx).](https://github.com/OfficeDev/TeamsFx/issues)

#### <a name="mobile-debugging"></a>Depuración móvil

La depuración del kit de herramientas de Teams (`F5`) todavía no se admite con la aplicación de Office para Android. A continuación se muestra cómo depurar de forma remota la aplicación que se ejecuta en la aplicación de Office para Android:

1. Si depura mediante un dispositivo Android físico, conéctelo a la máquina de desarrollo y habilite la opción para la [depuración USB](https://developer.android.com/studio/debug/dev-options). Esto está habilitado de forma predeterminada con el emulador de Android.
1. Inicie la aplicación de Office desde el dispositivo Android.
1. Abra el perfil **Me > Settings (Configuración de Me >) > Allow debugging (Permitir depuración**) y active la opción **Enable remote debugging (Habilitar depuración remota**).

    :::image type="content" source="images/office-android-enable-remote-debugging.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción de alternancia Habilitar depuración remota.":::

1. Deje **Configuración**.
1. Deje la pantalla del perfil.
1. Seleccione **Aplicaciones** e inicie la aplicación de prueba para ejecutarla en la aplicación de Office.
1. Asegúrese de que el dispositivo Android está conectado a la máquina de desarrollo. Desde la máquina de desarrollo, abra el explorador en su página de inspección de DevTools. Por ejemplo, vaya a `edge://inspect/#devices` en Microsoft Edge para mostrar una lista de WebView de Android habilitado para depuración.
1. Busque con la dirección URL de la pestaña y seleccione **Inspeccionar** para iniciar la `Microsoft Teams Tab` depuración de la aplicación con DevTools.

    :::image type="content" source="images/office-android-debug.png" alt-text="La captura de pantalla es un ejemplo que muestra la lista de vistas web en devtool.":::

1. Depure la aplicación de pestaña en Android WebView. De la misma manera que [depura de forma remota](/microsoft-edge/devtools-guide-chromium/remote-debugging) un sitio web normal en un dispositivo Android.

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de ejemplo** | **Descripción** | **Node.js** |
|---------------|--------------|--------|
| Lista de tareas pendientes | Lista de tareas pendientes editable con sso creado con React y Azure Functions. Solo funciona en Teams (use esta aplicación de ejemplo para probar el proceso de actualización descrito en este tutorial). | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend)  |
| Lista de tareas pendientes (Microsoft 365) | Lista de tareas pendientes editable con sso creado con React y Azure Functions. Funciona en Teams, Outlook, Office. | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)|
| Editor de imágenes (Microsoft 365) | Cree, edite, abra y guarde imágenes mediante Microsoft Graph API. Funciona en Teams, Outlook, Office. | [View](https://github.com/OfficeDev/m365-extensibility-image-editor) |
| Página de inicio de ejemplo (Microsoft 365) | Muestra la autenticación sso y las funcionalidades del SDK de TeamsJS como disponibles en distintos hosts. Funciona en Teams, Outlook, Office. | [View](https://github.com/OfficeDev/microsoft-teams-library-js/tree/main/apps/sample-app) |
| Aplicación Northwind Orders | Muestra cómo usar el SDK de Microsoft TeamsJS V2 para ampliar la aplicación de Teams a otras aplicaciones host de Microsoft 365. Funciona en Teams, Outlook, Office. Optimizado para dispositivos móviles.| [View](https://github.com/microsoft/app-camp/tree/main/experimental/ExtendTeamsforM365) |

## <a name="next-step"></a>Paso siguiente

Publique la aplicación para que sea detectable en Teams, Outlook y Office:

> [!div class="nextstepaction"]
> [Publicar aplicaciones de Teams para Outlook y Office](publish.md)
