---
title: Extender una extensión Teams mensaje a través de Microsoft 365
description: Este es el modo de actualizar la extensión de mensajería de Teams basada en búsqueda para que se ejecute en Outlook
ms.date: 11/15/2021
ms.topic: tutorial
ms.openlocfilehash: 6adde57b6c5f59d28234afaacc721fba3812bd24
ms.sourcegitcommit: f77750f2e60f63d1e2f66a96c169119683c66950
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2021
ms.locfileid: "60960395"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Extender una extensión Teams mensaje a través de Microsoft 365

> [!NOTE]
> *La extensión de una Teams de mensaje en Microsoft 365* está disponible actualmente solo en la versión preliminar del desarrollador [público.](../resources/dev-preview/developer-preview-intro.md) Es posible que las características incluidas en la versión preliminar no estén completas y que se someten a cambios antes de estar disponibles en la versión pública. Solo se proporcionan con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

Las extensiones de [mensajería basadas](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) en búsquedas permiten a los usuarios buscar en un sistema externo y compartir resultados a través del área de mensajes de redacción del Microsoft Teams cliente. Al extender las aplicaciones de Teams en [Microsoft 365 (versión preliminar),](overview.md)ahora puede llevar las extensiones de mensaje de Teams basadas en búsqueda a Outlook para Windows de escritorio y web.

El proceso para actualizar la extensión de mensaje basada en Teams búsqueda para que se ejecute Outlook implica estos pasos:

> [!div class="checklist"]
> * Actualizar el manifiesto de la aplicación
> * Agregar un canal Outlook para el bot
> * Instalación local de la aplicación actualizada en Teams

El resto de esta guía le guiará por estos pasos y le mostrará cómo obtener una vista previa de la extensión de mensaje en Outlook para Windows escritorio y web.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, necesitará:

 - Inquilino Microsoft 365 espacio aislado del Programa para desarrolladores
 - El inquilino de espacio aislado inscrito en *Office 365 versiones dirigidas*
 - Un entorno de prueba con Office aplicaciones instaladas desde el Aplicaciones Microsoft 365 *beta*
 - Visual Studio Code con la Teams Toolkit (versión preliminar) (opcional)

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="prepare-your-messaging-extension-for-the-upgrade"></a>Preparar la extensión de mensajería para la actualización

Si tienes una extensión de mensajería existente, haz una copia o una rama del proyecto de producción para probar y actualizar tu id. de aplicación en el manifiesto de la aplicación para usar un nuevo identificador (distinto del id. de aplicación de producción).

Si quieres usar código de ejemplo para completar este tutorial, sigue los pasos de configuración de Teams [ejemplo](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) de búsqueda de extensión de mensajería para crear y registrar rápidamente un bot.

## <a name="update-the-app-manifest"></a>Actualizar el manifiesto de la aplicación

Deberá usar el esquema [](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) de manifiesto de vista previa de Teams desarrollador y la versión del manifiesto para permitir que la extensión de mensajería Teams se ejecute en `m365DevPreview` Outlook.

Tienes dos opciones para actualizar el manifiesto de la aplicación:

# <a name="teams-toolkit"></a>[Teams Toolkit](#tab/manifest-teams-toolkit)

1. Abra la *paleta Comandos*: `Ctrl+Shift+P`
1. Ejecute el `Teams: Upgrade Teams manifest to support Outlook and Office apps` comando y seleccione el archivo de manifiesto de la aplicación. Los cambios se realizarán en su lugar.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abre el Teams de la aplicación y actualiza `$schema` el y con los siguientes `manifestVersion` valores:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

Si usó Teams Toolkit para crear la aplicación de extensión de mensajería, puede usarla para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta de comandos y busque Teams: validar el archivo de manifiesto o seleccione la opción en el menú Implementación del Teams Toolkit (busque el icono Teams a la izquierda de `Ctrl+Shift+P` Visual Studio Code). 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit &quot;Validar archivo de manifiesto&quot; en el menú &quot;Implementación&quot;":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Agregar un canal Outlook para el bot

En Microsoft Teams, una extensión de mensajería consta de un servicio web que hospeda y un manifiesto de aplicación, que define dónde se hospeda el servicio web. El servicio web aprovecha el esquema de mensajería del SDK de [Bot Framework](/azure/bot-service/bot-service-overview) y el protocolo de comunicación segura a través de un canal Teams registrado para el bot.

Para que los usuarios interactúen con la extensión de mensajería desde Outlook, deberá agregar un canal de Outlook al bot:

1. Desde [Azure Portal](https://portal.azure.com) (o el portal de Bot [Framework](https://dev.botframework.com) si se registró anteriormente allí), vaya al recurso bot.

1. En *Configuración*, seleccione **Canales**.

1. Haga clic **en Outlook**, seleccione la pestaña Extensiones **de mensaje** y, a continuación, haga clic en **Guardar**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Agregar un Outlook de extensiones de mensaje para el bot desde el panel Canales del bot de Azure":::

1. Confirme que el canal Outlook aparece junto con Microsoft Teams en el panel Canales **del** bot:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Panel Canales del bot de Azure que enumera Microsoft Teams y Outlook canales":::

## <a name="sideload-your-updated-messaging-extension-in-teams"></a>Descargar localmente la extensión de mensajería actualizada en Teams

El último paso es cargar localmente la extensión de mensajería actualizada ([paquete](/microsoftteams/platform/concepts/build-and-test/apps-package)de la aplicación ) en Microsoft Teams. Una vez completada, la extensión de mensajería aparecerá en las aplicaciones instaladas *desde* el área del mensaje de redacción.

1. Empaqueta la Teams (iconos de manifiesto e [aplicación)](/microsoftteams/platform/resources/schema/manifest-schema#icons)en un archivo zip. Si usó Teams Toolkit para crear la aplicación, puede hacerlo fácilmente con la opción Paquete  de metadatos **zip Teams** en el menú Implementación de Teams Toolkit:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Opción &quot;Paquete Teams metadatos zip&quot; en Teams Toolkit extensión para Visual Studio Code":::

1. Inicie sesión en Teams con su cuenta de espacio aislado de espacio aislado y compruebe que está en la vista  previa del  desarrollador público haciendo clic en el menú de puntos suspensivos (**...**) junto al perfil de usuario y abriendo Acerca de para comprobar que la opción Vista previa del desarrollador está activa. 

    :::image type="content" source="images/teams-dev-preview.png" alt-text="En Teams de puntos suspensivos, abra &quot;Acerca&quot; y compruebe que la opción &quot;Vista previa del programador&quot; esté activada.":::

1. Abra el *panel* Aplicaciones y haga clic **Upload una aplicación personalizada** y, a continuación, Upload para mí o **mis equipos**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Botón &quot;Upload una aplicación personalizada&quot; en el panel Teams &quot;Aplicaciones&quot;":::

1. Selecciona el paquete de la aplicación y haz clic *en Abrir*.

Una vez que se haya Teams, la extensión de mensajería estará disponible en Outlook en la Web.

## <a name="preview-your-message-extension-in-outlook"></a>Vista previa de la extensión de mensaje en Outlook

Ya está listo para probar la extensión de mensajería que se ejecuta en Outlook en Windows escritorio y la web. Aunque la extensión de mensajería actualizada seguirá funcionando en Teams con compatibilidad completa de características para extensiones de [mensajería,](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)hay limitaciones en esta versión preliminar de la experiencia habilitada para Outlook para tener en cuenta:

* Las extensiones de mensajería Outlook están limitadas al contexto de [ *redacción de* correo](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Incluso si la extensión Teams mensaje incluye como contexto en su manifiesto, la vista previa actual se limita a la opción de composición de `commandBox` correo (  `compose` ). No se admite invocar una extensión de mensaje desde el cuadro Outlook *búsqueda* global.
* [Los comandos de extensión de mensajería basada](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) en acciones no se admiten en Outlook. Si la aplicación tiene comandos basados en búsqueda y en acción, aparecerá en Outlook pero el menú de acción no estará disponible.
* [La autenticación silenciosa de inicio de](/microsoftteams/platform/messaging-extensions/how-to/enable-sso-auth-me) sesión único no es compatible con las extensiones de mensajería en Outlook.
* No se admite la inserción de más de cinco [tarjetas](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) adaptables en un correo electrónico; No se admiten las tarjetas adaptables v1.4 y posteriores.
* [Las acciones de](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) tarjeta `messageBack` de tipo , , y no se `imBack` `invoke` `signin` admiten para tarjetas insertadas. La compatibilidad se limita a: al hacer clic, se redirigirá al usuario a la dirección URL especificada `openURL` en una nueva pestaña.

Al probar la extensión de mensajería, puede identificar el origen (que se origina de Teams frente a Outlook) de las solicitudes de bot mediante [el channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) del [objeto Activity.](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) Cuando un usuario realiza una consulta, el servicio recibe un objeto Bot Framework `Activity` estándar. Una de las propiedades del objeto Activity es , que tendrá el valor de o , según el origen de la `channelId` `msteams` solicitud del `outlook` bot. Para obtener más información,  [vea Search based messaging extensions SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

### <a name="outlook"></a>Outlook

Para obtener una vista previa de la aplicación que se ejecuta Outlook en Windows escritorio, Outlook ha iniciado sesión con las credenciales del inquilino de prueba. Haga clic en **Nuevo correo electrónico**. Abre el **menú desplegable Más aplicaciones** en la cinta de opciones superior. Se mostrará la extensión de mensaje. Puede invocarlo desde allí y usarlo tal como lo haría al redactar un mensaje en Teams.

### <a name="outlook-on-the-web"></a>Outlook en la Web

Para obtener una vista previa de la aplicación que se Outlook en la Web, inicie sesión [en outlook.com](https://www.outlook.com) con las credenciales del inquilino de prueba. Haga clic en **Nuevo mensaje**. Abre el **menú desplegable Más aplicaciones** en la parte inferior de la ventana de composición. Se mostrará la extensión de mensaje. Puede invocarlo desde allí y usarlo tal como lo haría al redactar un mensaje en Teams.

## <a name="next-steps"></a>Pasos siguientes

Outlook habilitadas para Teams de mensajería están en versión preliminar y no son compatibles con el uso de producción. Este es el modo de distribuir la extensión de Outlook de mensajería habilitada para obtener una vista previa de audiencias con fines de prueba.

### <a name="single-tenant-distribution"></a>Distribución de un solo inquilino

Outlook y Office pestañas personales habilitadas para la vista previa se pueden distribuir a una audiencia de vista previa en un inquilino de prueba (o producción) de tres maneras:

#### <a name="teams-client"></a>Teams cliente

En el *menú* Aplicaciones, selecciona *Administrar tus aplicaciones* Enviar una aplicación a tu  >  **organización.** Esto requiere la aprobación del administrador de TI.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams de administración

Como administrador Teams, puede cargar e instalar previamente el paquete de la aplicación para el inquilino de la organización desde https://admin.teams.microsoft.com/ . Consulta [Upload aplicaciones personalizadas en el Centro Microsoft Teams administración para](/MicrosoftTeams/upload-custom-apps) obtener más información.

#### <a name="microsoft-admin-center"></a>Centro de administración de Microsoft

Como administrador global, puedes cargar e instalar previamente el paquete de la aplicación desde https://admin.microsoft.com/ . Consulta [Probar e implementar Aplicaciones Microsoft 365 asociados en el portal de aplicaciones integradas](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) para obtener más información.

### <a name="multi-tenant-distribution"></a>Distribución multiinquilino

La distribución a Microsoft AppSource aún no se admite durante esta versión preliminar de desarrolladores de Outlook aplicaciones habilitadas Teams de mensajes.
