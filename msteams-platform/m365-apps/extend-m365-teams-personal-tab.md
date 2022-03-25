---
title: Extender una aplicación Teams pestaña personal en Microsoft 365
description: Extender una aplicación Teams pestaña personal en Microsoft 365
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: medium
ms.openlocfilehash: 5370c9b5f273936c8afdd6c95e4e524dda3857ce
ms.sourcegitcommit: 65cea59cc0602269395a2f87e023a4057d9cc55e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2022
ms.locfileid: "63765949"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Extender una Teams personal a través de Microsoft 365

> [!NOTE]
> *La extensión de una Teams personal en Microsoft 365* está disponible solo en [la versión preliminar del desarrollador público](../resources/dev-preview/developer-preview-intro.md). Es posible que las características incluidas en la versión preliminar no estén completas y experimenten cambios antes de estar disponibles en la versión pública. Se proporcionan solo con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

Las pestañas personales proporcionan una excelente forma de mejorar la experiencia Microsoft Teams usuario. Con las pestañas personales, puede proporcionar a un usuario acceso a su aplicación dentro de Teams, sin que el usuario tenga que dejar la experiencia o volver a iniciar sesión. Con esta vista previa, las pestañas personales pueden iluminarse dentro de otras Microsoft 365 aplicaciones. En este tutorial se muestra el proceso de tomar una pestaña personal de Teams existente y actualizarla para que se ejecute en experiencias web y de escritorio Outlook, y también Office en la Web (office.com).

Actualizar la aplicación personal para que se ejecute en Outlook y Office Inicio implica estos pasos:

> [!div class="checklist"]
>
> * Actualizar el manifiesto de la aplicación
> * Actualizar las referencias del SDK de TeamsJS
> * Modificar los encabezados de la directiva de seguridad de contenido
> * Actualizar el registro Microsoft Azure Active Directory aplicación (Azure AD) para inicio de sesión único (SSO)

La prueba de la aplicación requerirá los siguientes pasos:

> [!div class="checklist"]
>
> * Inscriba Microsoft 365 inquilino en *Office 365 versiones dirigidas*
> * Configurar tu cuenta para tener acceso a las versiones preliminares de Outlook y Office aplicaciones
> * Descargar localmente la aplicación actualizada en Teams

Después de estos pasos, la aplicación debe aparecer en las versiones preliminares de Outlook y Office aplicaciones.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, necesitará:

* Inquilino Microsoft 365 espacio aislado del Programa para desarrolladores
* El inquilino de espacio aislado inscrito en *Office 365 versiones dirigidas*
* Una máquina con Office aplicaciones instaladas desde el Aplicaciones Microsoft 365 *beta*
* (Opcional) [Teams Toolkit](https://aka.ms/teams-toolkit) extensión para Microsoft Visual Studio código para ayudar a actualizar el código

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Preparar la pestaña personal para la actualización

Si tienes una aplicación de pestaña personal existente, haz una copia o una rama del proyecto de producción para probar y actualizar tu id. de aplicación en el manifiesto de la aplicación para usar un nuevo identificador (distinto del id. de aplicación de producción).

Si quieres usar código de ejemplo para completar este tutorial, sigue los pasos de configuración de Introducción a [Todo List Sample](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) para crear una aplicación de pestaña personal con la extensión Teams Toolkit para Visual Studio Code. O bien, puede empezar con el mismo ejemplo de lista [de todo actualizado para TeamsJS SDK v2 Preview](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365) y continuar con la vista previa de la pestaña personal en otras [Microsoft 365 experiencias.](#preview-your-personal-tab-in-other-microsoft-365-experiences) El ejemplo actualizado también está disponible en Teams Toolkit extensión: *DevelopmentView* >  *samplesTodo* >  **List (Funciona en Teams, Outlook y Office).**.

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Ejemplo de lista todo (funciona en Teams, Outlook y Office) en Teams Toolkit":::

## <a name="update-the-app-manifest"></a>Actualizar el manifiesto de la aplicación

Tendrás que usar el esquema de manifiesto de vista previa del desarrollador de [Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `Microsoft 365 DevPreview` y la versión del manifiesto para permitir que tu pestaña personal Teams se ejecute en Office y Outlook.

Puedes usar Teams Toolkit para actualizar el manifiesto de la aplicación o aplicar los cambios manualmente:

# <a name="teams-toolkit"></a>[Kit de herramientas de Teams](#tab/manifest-teams-toolkit)

1. Abra la *paleta Comandos*: `Ctrl+Shift+P`
1. Ejecute el `Teams: Upgrade Teams manifest to support Outlook and Office apps` comando y seleccione el archivo de manifiesto de la aplicación. Los cambios se realizarán en su lugar.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abre el Teams de la aplicación y actualiza el `$schema` y con `manifestVersion` los siguientes valores:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Si usaste Teams Toolkit para crear tu aplicación personal, también puedes usarla para validar los cambios en el archivo de manifiesto e identificar cualquier error. Abra la `Ctrl+Shift+P` paleta de comandos y busque **Teams:** validar el archivo de manifiesto o seleccione la opción en el menú Implementación del Teams Toolkit (busque el icono Teams en el lado izquierdo de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit &quot;Validar archivo de manifiesto&quot; en el menú &quot;Implementación&quot;":::

## <a name="update-sdk-references"></a>Actualizar referencias de SDK

Para ejecutar en Outlook y Office, la aplicación tendrá que depender del paquete npm `@microsoft/teams-js@2.0.0-beta.1` (o de una versión *beta* posterior). `@microsoft/teams-js` Si bien el código con versiones de nivel inferior de se admite en Outlook y Office, las advertencias `@microsoft/teams-js` de desuso se registrarán y la compatibilidad con las versiones de nivel inferior de Outlook y Office finalmente dejará de existir.

Puede usar Teams Toolkit `@microsoft/teams-js`para automatizar algunos de los cambios de código para adoptar la siguiente versión de , pero si desea realizar los pasos manualmente, consulte [Microsoft Teams JavaScript client SDK Preview](using-teams-client-sdk-preview.md) para obtener más información.

1. Abra la *paleta Comandos*: `Ctrl+Shift+P`
1. Ejecutar el comando `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Una vez completada, la utilidad habrá `package.json` actualizado el archivo con la dependencia de TeamsJS SDK Preview (`@microsoft/teams-js@2.0.0-beta.1` o posterior) `*.js/.ts` y los archivos y `*.jsx/.tsx` se actualizarán con:

> [!div class="checklist"]
>
> * `package.json` referencias a TeamsJS SDK Preview
> * Instrucciones Import para TeamsJS SDK Preview
> * [Llamadas de función, enumeración e interfaz](using-teams-client-sdk-preview.md#apis-organized-into-capabilities) a TeamsJS SDK Preview
> * `TODO` avisos de comentarios para revisar las áreas que podrían estar afectadas por los [cambios en la interfaz](using-teams-client-sdk-preview.md#updates-to-the-context-interface) de contexto
> * `TODO` avisos de comentarios para asegurarse de [que la conversión a funciones de promesas](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) de funciones de estilo de devolución de llamada ha ido bien en cada sitio de llamada que encontró la herramienta

> [!IMPORTANT]
> El código *.html* archivos no es compatible con las herramientas de actualización y requerirá cambios manuales.

> [!NOTE]
> Si quieres actualizar manualmente el código, consulta Microsoft Teams vista previa del SDK de cliente de [JavaScript](using-teams-client-sdk-preview.md) para obtener información sobre los cambios necesarios.

## <a name="configure-content-security-policy-headers"></a>Configurar encabezados de directiva de seguridad de contenido

[Al igual que Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs), las aplicaciones de tabulación se hospedan en (elementos [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)) en Office y Outlook web.

Si la aplicación usa encabezados de directiva de seguridad de [contenido (CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) ), asegúrate de permitir todos los siguientes antecesores [de fotogramas en los encabezados](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) CSP:

|Microsoft 365 host| permiso frame-ancestor|
|--|--|
| Teams | `teams.microsoft.com` |
| Oficina | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Actualizar Azure AD de aplicaciones para SSO

Azure Active Directory Inicio de sesión único (SSO) para pestañas personales funciona de la misma manera en Office y Outlook que en [Teams](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso), sin embargo, deberá agregar varios identificadores de aplicación cliente al registro de aplicación de Azure AD de la aplicación de pestaña en el portal de registros de *aplicaciones del* inquilino.

1. Inicie sesión en [Microsoft Azure portal con](https://portal.azure.com) su cuenta de espacio aislado.
1. Abra la **hoja Registros de aplicaciones** .
1. Selecciona el nombre de la aplicación de pestaña personal para abrir el registro de la aplicación.
1. Seleccione  **Exponer una API** (en *Administrar*).

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="Autorizar identificadores de cliente desde la hoja *Registros de aplicaciones* en Azure Portal":::

En la **sección Aplicaciones cliente autorizadas** , asegúrese de que se agregan todos los valores `Client Id` siguientes:

|Microsoft 365 cliente | Id. de cliente |
|--|--|
|Teams escritorio, móvil |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
|Office escritorio  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
|Versión de escritorio de Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>Transferir localmente la aplicación en Teams

El último paso es descargar localmente la pestaña personal actualizada (paquete [de](/microsoftteams/platform/concepts/build-and-test/apps-package) la aplicación) en Microsoft Teams. Una vez completada, la aplicación estará disponible para ejecutarse en Office y Outlook, además de Teams.

1. Empaqueta tu Teams (iconos de manifiesto e [aplicación](/microsoftteams/platform/resources/schema/manifest-schema#icons)) en un archivo zip. Si usó Teams Toolkit para crear la aplicación, puede hacerlo fácilmente con la opción Paquete de metadatos **Zip Teams** en el menú Implementación de Teams Toolkit  `Ctrl+Shift+P` o en la Paleta de comandos de Visual Studio Code:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Opción &quot;Paquete Teams metadatos zip&quot; en Teams Toolkit extensión para Visual Studio Code":::

1. Inicie sesión en Teams con su cuenta de espacio aislado de espacio aislado y asegúrese de que está en public Developer Preview. Puede comprobar que está en vista previa en el cliente de Teams haciendo clic en el menú de puntos suspensivos (**...**) del perfil de usuario y abriendo Acerca de comprobar  que la opción Vista previa  del programador está activa.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Desde Teams de puntos suspensivos, abra &quot;Acerca&quot; y compruebe que la opción &quot;Vista previa del programador&quot; esté activada.":::

1. Abre el *panel* Aplicaciones y haz clic **Upload una aplicación personalizada** y, a continuación **, Upload para mí o mis equipos**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Botón &quot;Upload aplicación personalizada&quot; en el panel Teams &quot;Aplicaciones&quot;":::

1. Selecciona el paquete de la aplicación y haz clic *en Abrir*.

Una vez que se haya Teams, la pestaña personal estará disponible en Outlook y Office. Asegúrese de iniciar sesión con las mismas credenciales que usó para realizar la instalación local de la aplicación en Teams.

Puedes anclar la aplicación para obtener acceso rápido o puedes encontrar la aplicación en los puntos suspensivos (**...**) que se encuentran en la barra lateral de la izquierda.

> [!NOTE]
> Anclar una aplicación en Teams anclará como una aplicación en Office.com o Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Obtener una vista previa de la pestaña personal en otras Microsoft 365 experiencias

Al actualizar la pestaña personal de Teams y cargarla localmente en Teams, también se ejecutará en Outlook clientes de escritorio y web y Office en la Web (office.com). Este es el modo de obtener una vista previa de estas Microsoft 365 experiencias.

### <a name="outlook"></a>Outlook

Para ver la aplicación que se ejecuta en Outlook en Windows escritorio:

1. Inicie Outlook e inicie sesión con su cuenta de inquilino de desarrollo.
1. Haga clic en los puntos suspensivos (**...**) de la barra lateral. El título de la aplicación de instalación local aparecerá entre las aplicaciones instaladas.
1. Haz clic en el icono de la aplicación para iniciar la aplicación en Outlook.

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Haz clic en la opción puntos suspensivos ('Más aplicaciones') en la barra lateral de Outlook cliente de escritorio para ver las pestañas personales instaladas":::

### <a name="outlook-on-the-web"></a>Outlook en la Web

Para ver la aplicación en Outlook en la Web:

1. Vaya a [Outlook en la Web](https://outlook.office.com) e inicie sesión con su cuenta de inquilino de desarrollo.
1. Haga clic en los puntos suspensivos (**...**) de la barra lateral. El título de la aplicación de instalación local aparecerá entre las aplicaciones instaladas.
1. Haz clic en el icono de la aplicación para iniciar y obtener una vista previa de la aplicación que se ejecuta en Outlook en la Web.

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="Haz clic en la opción puntos suspensivos ('Más aplicaciones') en la barra lateral de outlook.com para ver las pestañas personales instaladas":::

### <a name="office"></a>Oficina

Para ver la aplicación que se ejecuta en Office en Windows escritorio:

1. Inicie Office e inicie sesión con su cuenta de inquilino de desarrollo.
1. Haga clic en los puntos suspensivos (**...**) de la barra lateral. El título de la aplicación de instalación local aparecerá entre las aplicaciones instaladas.
1. Haz clic en el icono de la aplicación para iniciar la aplicación en Office.

:::image type="content" source="images/office-desktop-more-apps.png" alt-text="Haz clic en la opción puntos suspensivos ('Más aplicaciones') en la barra lateral de Office cliente de escritorio para ver las pestañas personales instaladas":::

### <a name="office-on-the-web"></a>Office en la web

Para obtener una vista previa de la aplicación que se ejecuta Office en la Web:

1. Inicie sesión en office.com con credenciales de inquilino de prueba.
1. Haga clic en los puntos suspensivos (**...**) de la barra lateral. El título de la aplicación de instalación local aparecerá entre las aplicaciones instaladas.
1. Haz clic en el icono de la aplicación para iniciar la aplicación en Office en la Web.

:::image type="content" source="images/office-web-more-apps.png" alt-text="Haz clic en la opción puntos suspensivos ('Más aplicaciones') en la barra lateral de office.com para ver las pestañas personales instaladas":::

## <a name="next-steps"></a>Pasos siguientes

Outlook y Office las pestañas personales habilitadas para aplicaciones están en versión preliminar y no se admiten para el uso de producción. Aquí te explicamos cómo distribuir tu aplicación de pestaña personal para obtener una vista previa de audiencias con fines de prueba.

### <a name="single-tenant-distribution"></a>Distribución de un solo inquilino

Outlook y Office pestañas personales habilitadas para la vista previa se pueden distribuir a una audiencia de vista previa en un inquilino de prueba (o producción) de tres maneras:

#### <a name="teams-client"></a>Teams cliente

En el *menú* Aplicaciones, selecciona *Administrar las aplicacionesSubmit* >  **una aplicación a tu organización**. Esto requiere la aprobación del administrador de TI.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams centro de administración

Como administrador Teams, puede cargar e instalar previamente el paquete de la aplicación para el inquilino de la organización [desde Teams administrador](https://admin.teams.microsoft.com/). Consulta [Upload aplicaciones personalizadas en el Centro Microsoft Teams administración para](/MicrosoftTeams/upload-custom-apps) obtener más información.

#### <a name="microsoft-admin-center"></a>Centro de administración de Microsoft

Como administrador global, puedes cargar e instalar previamente el paquete de la aplicación desde el administrador [de Microsoft](https://admin.microsoft.com/). Consulta [Probar e implementar Aplicaciones Microsoft 365 asociados en el portal de aplicaciones integradas](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) para obtener más información.

### <a name="multitenant-distribution"></a>Distribución multitenente

La distribución a Microsoft AppSource no se admite durante esta versión preliminar para desarrolladores de Outlook y Office pestañas personales habilitadas Teams microsoft.
