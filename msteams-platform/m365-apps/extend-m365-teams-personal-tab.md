---
title: Ampliar una aplicación de pestaña personal de Teams en Microsoft 365
description: Ampliar una aplicación de pestaña personal de Teams en Microsoft 365
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: high
ms.openlocfilehash: 873a6fa6207d122581e18cef0ae922ffca87762f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111524"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Ampliar una pestaña personal de Teams en Microsoft 365

> [!NOTE]
> *Ampliar una extensión de mensajería de Teams en Microsoft 365* solo está disponible actualmente en [versión preliminar pública para desarrolladores](../resources/dev-preview/developer-preview-intro.md). Es posible que las características incluidas en la versión preliminar no estén completas y experimenten cambios antes de estar disponibles en la versión pública. Se proporcionan solo con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

Las pestañas personales proporcionan una excelente manera de mejorar la experiencia de Microsoft Teams. Con las pestañas personales, puede proporcionar a un usuario acceso a su aplicación directamente en Teams, sin que el usuario tenga que salir de la experiencia ni volver a iniciar sesión. Con esta versión preliminar, las pestañas personales pueden iluminarse dentro de otras aplicaciones Microsoft 365. En este tutorial se muestra el proceso de tomar una pestaña personal de Teams existente y actualizarla para que se ejecute en las experiencias de escritorio y web de Outlook, así como en Office en la Web (office.com).

La actualización de la aplicación personal para que se ejecute en Outlook y Office Hogar implica estos pasos:

> [!div class="checklist"]
>
> * Actualizar el manifiesto de la aplicación
> * Actualizar las referencias del SDK de TeamsJS
> * Modificar los encabezados de la directiva de seguridad de contenido
> * Actualización del registro de aplicaciones de Microsoft Azure Active Directory (Azure AD) para el inicio de sesión único (SSO)

La prueba de la aplicación requerirá los pasos siguientes:

> [!div class="checklist"]
>
> * Inscribir el espacio empresarial de Microsoft 365 en *Lanzamientos específicos de Office 365*
> * Configurar su cuenta para acceder a las versiones preliminares de Outlook y las aplicaciones de Office
> * Transferir localmente la aplicación actualizada en Teams

Después de estos pasos, la aplicación debe aparecer en las versiones preliminares de las aplicaciones de Outlook y Office.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, necesitará:

* Una cuenta empresarial de espacio aislado del Programa de desarrolladores de Microsoft 365
* El inquilino de espacio aislado inscrito en *Versiones dirigidas de Office 365*
* Una máquina con aplicaciones de Office instaladas desde el *canal beta* Aplicaciones de Microsoft 365
* (Opcional) extensión [Teams Toolkit](https://aka.ms/teams-toolkit) para Microsoft Visual Studio Code para ayudar a actualizar el código

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Preparar la pestaña personal para la actualización

Si tiene una extensión de mensajería existente, realice una copia o una rama del proyecto de producción para probar y actualizar el identificador de aplicación en el manifiesto de la aplicación para usar un identificador nuevo (distinto del identificador de aplicación de producción).

Si desea usar código de ejemplo para completar este tutorial, siga los pasos de configuración de [Introducción con el ejemplo lista de tareas pendientes](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) para crear una aplicación de pestaña personal con la extensión Kit de herramientas de Teams para Visual Studio Code. O bien, puede empezar con el mismo [Todo List Sample actualizado para la versión preliminar del SDK de TeamsJS v2](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365) y continuar con [Preview your personal tab in other Microsoft 365 experiences](#preview-your-personal-tab-in-other-microsoft-365-experiences). La muestra actualizada también está disponible en la extensión Teams Toolkit: *Desarrollo* > *Ver muestras* > **de la lista de tareas (funciona en Teams, Outlook y Office)**.

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Se muestra lista completa (funciona en Teams, Outlook y Office) en el kit de herramientas de Teams":::

## <a name="update-the-app-manifest"></a>Actualización del manifiesto de la aplicación

Tendrá que usar el esquema [Manifiesto de la versión preliminar para desarrolladores de Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) y la versión del manifiesto `Microsoft 365 DevPreview` para permitir que la extensión de pestaña personal de Teams se ejecute en Office y Outlook.

Puede usar el kit de herramientas de Teams para actualizar el manifiesto de la aplicación o aplicar los cambios manualmente:

# <a name="teams-toolkit"></a>[Kit de herramientas de Teams](#tab/manifest-teams-toolkit)

1. Abra la *Paleta de comandos*: `Ctrl+Shift+P`
1. Ejecute el comando `Teams: Upgrade Teams manifest to support Outlook and Office apps` y seleccione el archivo de manifiesto de la aplicación. Se realizarán cambios en el sitio.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abra el manifiesto de la aplicación de Teams y actualice `$schema` y `manifestVersion` con los siguientes valores:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Si ha usado el Kit de herramientas de Teams para crear su aplicación personal, también puede usarlo para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta de comandos `Ctrl+Shift+P` y busque **Teams: validar el archivo de manifiesto** o seleccione la opción en el menú Implementación del Kit de herramientas de Teams (busque el icono de Teams en el lado izquierdo de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="La opción &quot;Validar archivo de manifiesto&quot; del Kit de herramientas de Teams en el menú &quot;Implementación&quot;":::

## <a name="update-sdk-references"></a>Actualizar referencias del SDK

Para ejecutarse en Outlook y Office, la aplicación tendrá que depender del paquete npm `@microsoft/teams-js@2.0.0-beta.1` (o una versión *beta* posterior). Aunque el código con versiones de nivel inferior de `@microsoft/teams-js` se admite en Outlook y Office, se registrarán advertencias de desuso y la compatibilidad con las versiones de nivel inferior de `@microsoft/teams-js` en Outlook y Office terminará finalmente.

Puede usar el Kit de herramientas de Teams para ayudar a automatizar algunos de los cambios de código para adoptar la próxima versión de `@microsoft/teams-js`, pero si desea realizar los pasos manualmente, consulte [Preview del SDK de cliente JavaScript de Microsoft Teams](using-teams-client-sdk-preview.md) para obtener más información.

1. Abra la *Paleta de comandos*: `Ctrl+Shift+P`
1. Ejecute el comando `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Después de la finalización, la utilidad habrá actualizado el archivo `package.json` con la dependencia de la versión preliminar v2 del SDK de TeamsJS (`@microsoft/teams-js@2.0.0-beta.1` o posterior) y los archivos de `*.js/.ts` y `*.jsx/.tsx` se actualizarán con:

> [!div class="checklist"]
>
> * referencias de `package.json` a la versión preliminar v2 del SDK de TeamsJS
> * Instrucciones de importación para la versión preliminar v2 del SDK de TeamsJS
> * [Llamadas de funciones, enumeraciones e interfaces](using-teams-client-sdk-preview.md#apis-organized-into-capabilities) a la versión preliminar v2 del SDK de TeamsJS
> * Comentarios `TODO` de recordatorios para revisar las áreas que podrían verse afectadas por los cambios en la interfaz [Context](using-teams-client-sdk-preview.md#updates-to-the-context-interface)
> * Comentarios `TODO` de recordatorios para garantizar la [conversión de funciones de tipo callback a promises](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) ha ido bien en cada sitio de llamada que encontró la herramienta

> [!IMPORTANT]
> Las herramientas de actualización no admiten el código dentro de archivos *HTML* y requerirán cambios manuales.

> [!NOTE]
> Si desea actualizar manualmente el código, consulte [Preview del SDK de cliente javaScript de Microsoft Teams](using-teams-client-sdk-preview.md) para obtener información sobre los cambios necesarios.

## <a name="configure-content-security-policy-headers"></a>Configurar encabezados de directiva de seguridad de contenido

[Ajustar como en Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs), las aplicaciones de pestañas se hospedan en ([iframe elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)) en clientes web de Office y Outlook.

Si la aplicación usa los encabezados [Directiva de seguridad de contenido](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP), asegúrate de permitir todas las siguientes [antecesor de marco](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) en los encabezados de CSP:

|host de Microsoft 365| permiso de antecesor de marco|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Actualización del registro de aplicaciones de Azure AD para SSO

El inicio de sesión único (SSO) de Azure Active Directory para extensiones de mensajes funciona de la misma manera tanto en Outlook [como en Teams](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso), sin embargo, debe agregar varios identificadores de aplicación cliente al registro de aplicación de Azure AD del bot en el portal *Registros de aplicaciones* de la cuenta empresarial.

1. Inicie sesión en [Microsoft Azure Portal](https://portal.azure.com) con su cuenta empresarial de espacio aislado.
1. Abra la hoja **Registros de aplicaciones**.
1. Seleccione el nombre de la aplicación para abrir el registro de la aplicación.
1. Seleccione **Exponer una API** (en *Administrar*).

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="Autorizar los Ids de los clientes desde la hoja *Registros de aplicaciones* en el portal de Azure":::

En la sección **Aplicaciones cliente autorizadas** asegúrese de que aparecen todos los siguientes valores `Client Id`:

|Microsoft 365 aplicación cliente | Id. de cliente |
|--|--|
|Escritorio de Teams, móvil |1fec8e78-bli4-4aaf-ab1b-5451cc387264 |
|Web de Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
|Escritorio de Office  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
|Versión de escritorio de Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-0000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>Transferir localmente la aplicación en Teams

El último paso consiste en transferir localmente la extensión de mensajería actualizada ([paquete de la aplicación](/microsoftteams/platform/concepts/build-and-test/apps-package)) en Microsoft Teams. Una vez completada, la aplicación estará disponible para ejecutarse en Office y Outlook, además de en Teams.

1. Empaquete la aplicación de Teams (iconos de [manifiesto y aplicación](/microsoftteams/platform/resources/schema/manifest-schema#icons)) en un archivo ZIP. Si ha utilizado Teams Toolkit para crear su aplicación, puede hacerlo fácilmente utilizando la opción de **paquete de metadatos Zip Teams** en el menú de *despliegue* de Teams Toolkit o en la paleta `Ctrl+Shift+P` de comandos de Visual Studio Code:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Opción &quot;Comprimir paquete de metadatos de Teams&quot; en la extensión Kit de herramientas de Teams para Visual Studio Code":::

1. Inicie sesión en Teams con su cuenta de inquilino de espacio aislado y asegúrese de que se encuentra en la versión preliminar pública para desarrolladores. Para comprobar que se encuentra en la versión preliminar en el cliente de Teams, haga clic en los puntos suspensivos (**...**) por su perfil de usuario y abrir **Acerca de** para comprobar que la opción *Vista preliminar de desarrollador* está activada.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="En el menú de puntos suspensivos de Teams, abra &quot;Acerca de&quot; y compruebe que la opción &quot;Vista previa de desarrollador&quot; esté activada":::

1. Abra el panel *Aplicaciones* y haga clic en **Cargar una aplicación personalizada** y, a continuación, **Cargar para mí o mis equipos**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Botón &quot;Cargar una aplicación personalizada&quot; en el panel &quot;Aplicaciones&quot; de Teams":::

1. Seleccione el paquete de la aplicación y haga clic en *Abrir*.

Una vez transferida localmente a través de Teams, su pestaña personal estará disponible en Outlook y Office. Asegúrese de iniciar sesión con las mismas credenciales que usó para transferir localmente la aplicación en Teams.

Puedes anclar la aplicación para obtener acceso rápido o encontrarla en los puntos suspensivos (**...**) entre las aplicaciones recientes en la barra lateral de la izquierda.

> [!NOTE]
> Anclar una aplicación en Teams no se anclará como una aplicación en Office.com o Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Obtener una vista previa de su pestaña personal en otras experiencias de Microsoft 365

Al actualizar la pestaña personal de Teams y transferirla localmente en Teams, se ejecuta en Outlook en Windows, en la web, Office en Windows y en la Web (office.com). Aquí le mostramos cómo obtener una vista previa de esas experiencias de Microsoft 365.

### <a name="outlook-on-windows"></a>Outlook en Windows

Para obtener una vista previa de la aplicación ejecutándose en Outlook en el escritorio de Windows:

1. Inicie Outlook e inicie sesión con su cuenta de inquilino de desarrollo.
1. Haga clic en los puntos suspensivos (**...**) en la barra lateral. El título de la aplicación transferida localmente aparecerá entre las aplicaciones instaladas.
1. Haga clic en el icono de la aplicación para iniciar la aplicación en Outlook.

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Haga clic en la opción de puntos suspensivos (&quot;Más aplicaciones&quot;) de la barra lateral del cliente de escritorio de Outlook para ver las pestañas personales instaladas":::

### <a name="outlook-on-the-web"></a>Outlook en la Web

Para ver la aplicación en Outlook en la Web:

1. Vaya a [Outlook en la Web](https://outlook.office.com) e inicie sesión con su cuenta de inquilino de desarrollo.
1. Haga clic en los puntos suspensivos (**...**) en la barra lateral. El título de la aplicación transferida localmente aparecerá entre las aplicaciones instaladas.
1. Haga clic en el icono de la aplicación para iniciar y obtener una vista previa de la aplicación que se ejecuta en Outlook en la Web.

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="Haga clic en la opción de puntos suspensivos (&quot;Más aplicaciones&quot;) de la barra lateral de outlook.com para ver las pestañas personales instaladas":::

### <a name="office-on-windows"></a>Office en Windows

Para ver la aplicación que se ejecuta en Office en el escritorio de Windows:

1. Inicie Office e inicie sesión con su cuenta de inquilino de desarrollo.
1. Haga clic en los puntos suspensivos (**...**) en la barra lateral. El título de la aplicación transferida localmente aparecerá entre las aplicaciones instaladas.
1. Haga clic en el icono de la aplicación para iniciar la aplicación en Office.

:::image type="content" source="images/office-desktop-more-apps.png" alt-text="Haga clic en la opción de puntos suspensivos (&quot;Más aplicaciones&quot;) de la barra lateral del cliente de escritorio de Office para ver las pestañas personales instaladas":::

### <a name="office-on-the-web"></a>Office en la Web

Para obtener una vista previa de la aplicación que se ejecuta en Outlook en la Web:

1. Inicie sesión en office.com con credenciales de espacio empresarial de prueba.
1. Haga clic en los puntos suspensivos (**...**) en la barra lateral. El título de la aplicación transferida localmente aparecerá entre las aplicaciones instaladas.
1. Haga clic en el icono de la aplicación para iniciar la aplicación en Office en la web.

:::image type="content" source="images/office-web-more-apps.png" alt-text="Haga clic en la opción de puntos suspensivos (&quot;Más aplicaciones&quot;) de la barra lateral de office.com para ver las pestañas personales instaladas":::

## <a name="next-steps"></a>Pasos siguientes

Las pestañas personales habilitadas para Outlook y Office están en versión preliminar y no se admiten para su uso en producción. Aquí te mostramos cómo distribuir tu aplicación de pestaña personal a audiencias de vista previa con fines de prueba.

### <a name="single-tenant-distribution"></a>Distribución de cuenta empresarial única

Las pestañas personales habilitadas para Outlook y Office se pueden distribuir a una audiencia preliminar a través de una cuenta empresarial de prueba (o producción) de una de estas tres maneras:

#### <a name="teams-client"></a>Cliente de Teams

En el menú *Aplicaciones*, seleccione *Administrar las aplicaciones* > **Enviar una aplicación a la organización**. Esto requiere la aprobación del administrador de TI.

#### <a name="microsoft-teams-admin-center"></a>Centro de administración de Microsoft Teams

Como administrador de Teams, puede cargar e instalar previamente el paquete de la aplicación para la cuenta empresarial de su organización desde [Administrador de Teams](https://admin.teams.microsoft.com/). Consulte [Cargar las aplicaciones personalizadas en el Centro de administración de Microsoft Teams](/MicrosoftTeams/upload-custom-apps) para obtener más información.

#### <a name="microsoft-admin-center"></a>Centro de administración de Microsoft

Como administrador global, puede cargar e instalar previamente el paquete de la aplicación desde [Administrador de Microsoft](https://admin.microsoft.com/). Consulte [Probar e implementar Aplicaciones de Microsoft 365 por asociados en el portal de aplicaciones integradas](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) para obtener más información.

### <a name="multitenant-distribution"></a>Distribución de varias cuentas empresariales

La distribución a Microsoft AppSource no se admite durante esta vista previa para desarrolladores de las pestañas personales de Teams habilitadas para Outlook y Office.
