---
title: Extender una extensión Teams de mensajería a través de Microsoft 365
description: Este es el modo de actualizar la extensión de mensajería de Teams basada en búsqueda para que se ejecute en Outlook
ms.date: 11/15/2021
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 5c37eff384f3aa9d2d5f615272ec7a5518de4e8d
ms.sourcegitcommit: 6e33289c55a1a83adb9b7b38c42d781c699786f7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2022
ms.locfileid: "62345383"
---
# <a name="extend-a-teams-messaging-extension-across-microsoft-365"></a>Extender una extensión Teams de mensajería a través de Microsoft 365

> [!NOTE]
> *La extensión de una Teams de mensajería entre Microsoft 365* está disponible actualmente solo en [la versión preliminar del desarrollador público](../resources/dev-preview/developer-preview-intro.md). Es posible que las características incluidas en la versión preliminar no estén completas y experimenten cambios antes de estar disponibles en la versión pública. Se proporcionan solo con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

Las extensiones de [mensajería basadas en búsquedas](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) permiten a los usuarios buscar en un sistema externo y compartir resultados a través del área de mensajes de redacción del Microsoft Teams cliente. Al [extender las aplicaciones de Teams en Microsoft 365 (](overview.md)versión preliminar), ahora puede llevar las extensiones de mensajería de Teams basadas en búsquedas Outlook para Windows experiencias de escritorio y web.

El proceso para actualizar la extensión de mensajería de Teams basada en búsqueda para Outlook implica estos pasos:

> [!div class="checklist"]
> * Actualizar el manifiesto de la aplicación
> * Agregar un canal Outlook para el bot
> * Instalación local de la aplicación actualizada en Teams

El resto de esta guía le guiará por estos pasos y le mostrará cómo obtener una vista previa de la extensión de mensajería en Outlook para Windows escritorio y web.

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

Si desea usar código de ejemplo para completar este tutorial, siga los pasos de configuración de Teams [ejemplo](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) de búsqueda de extensión de mensajería para crear rápidamente una extensión de mensajería basada en Microsoft Teams búsqueda. O bien, puede empezar con el mismo ejemplo de búsqueda de extensiones de mensajería de Teams actualizado para [TeamsJS SDK v2 Preview](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365) y continuar con Vista previa de la extensión de mensajería [en Outlook](#preview-your-messaging-extension-in-outlook). El ejemplo actualizado también está disponible en la Teams Toolkit: *DevelopmentView* >  *samplesNPM* >  **Search Connector**.

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Ejemplo de NPM Search Connector en Teams Toolkit":::

## <a name="update-the-app-manifest"></a>Actualizar el manifiesto de la aplicación

Tendrás que usar el esquema de [](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `m365DevPreview` manifiesto de vista previa de Teams desarrollador y la versión del manifiesto para permitir que la extensión de mensajería Teams se ejecute en Outlook.

Tienes dos opciones para actualizar el manifiesto de la aplicación:

# <a name="teams-toolkit"></a>[Kit de herramientas de Teams](#tab/manifest-teams-toolkit)

1. Abra la *paleta Comandos*: `Ctrl+Shift+P`
1. Ejecute el `Teams: Upgrade Teams manifest to support Outlook and Office apps` comando y seleccione el archivo de manifiesto de la aplicación. Los cambios se realizarán en su lugar.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abre el Teams de la aplicación y actualiza el `$schema` y `manifestVersion` con los siguientes valores:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

Si usó Teams Toolkit para crear la aplicación de extensión de mensajería, puede usarla para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la `Ctrl+Shift+P` paleta de comandos y busque **Teams:** validar el archivo de manifiesto o seleccione la opción en el menú Implementación del Teams Toolkit (busque el icono Teams en el lado izquierdo de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit &quot;Validar archivo de manifiesto&quot; en el menú &quot;Implementación&quot;":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Agregar un canal Outlook para el bot

En Microsoft Teams, una extensión de mensajería consta de un servicio web que hospeda y un manifiesto de aplicación, que define dónde se hospeda el servicio web. El servicio web aprovecha el esquema de mensajería [del SDK de Bot Framework](/azure/bot-service/bot-service-overview) y el protocolo de comunicación segura a través de un canal Teams registrado para el bot.

Para que los usuarios interactúen con la extensión de mensajería desde Outlook, deberá agregar un canal de Outlook al bot:

1. Desde [Azure Portal](https://portal.azure.com) (o [el portal de Bot Framework](https://dev.botframework.com) si se registró anteriormente allí), vaya al recurso bot.

1. En *Configuración*, seleccione **Canales**.

1. Haga clic **en Outlook**, seleccione la pestaña **Extensiones de mensaje** y, a continuación, haga clic en **Guardar**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Agregar un Outlook de extensiones de mensaje para el bot desde el panel Canales del bot de Azure":::

1. Confirme que el canal Outlook aparece junto con Microsoft Teams en el panel Canales **del** bot:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Panel Canales del bot de Azure que enumera Microsoft Teams y Outlook canales":::

## <a name="update-azure-ad-app-registration-for-sso"></a>Actualizar Azure AD de aplicaciones para SSO

> [!NOTE]
> Puedes omitir el paso si usas un ejemplo de búsqueda de extensión de mensajería de [Teams, ya](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) que el escenario no implica Azure Active Directory (AAD) autenticación de Sign-On única.

Azure Active Directory Inicio de sesión único (SSO) para extensiones de mensajería funciona de la misma manera en Outlook que en [Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots), sin embargo, debe agregar varios identificadores de aplicación cliente al registro de aplicaciones de Azure AD del bot en *el portal de* registros de aplicaciones del inquilino.

1. Inicie sesión en [Azure Portal con](https://portal.azure.com) su cuenta de espacio aislado.
1. Abra **Registros de aplicaciones**.
1. Seleccione el nombre de la aplicación para abrir el registro de la aplicación.
1. Seleccione  **Exponer una API** (en *Administrar*).

En la **sección Aplicaciones cliente autorizadas** , asegúrese de que se enumeran todos los valores `Client Id` siguientes:

|Microsoft 365 cliente | Id. de cliente |
|--|--|
|Teams escritorio y móvil |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Versión de escritorio de Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-messaging-extension-in-teams"></a>Descargar localmente la extensión de mensajería actualizada en Teams

El último paso es cargar localmente la extensión de mensajería actualizada (paquete [de](/microsoftteams/platform/concepts/build-and-test/apps-package) la aplicación) en Microsoft Teams. Una vez completada, la extensión de mensajería aparecerá en las aplicaciones *instaladas desde el* área del mensaje de redacción.

1. Empaqueta tu Teams (iconos de manifiesto e [aplicación](/microsoftteams/platform/resources/schema/manifest-schema#icons)) en un archivo zip. Si usó Teams Toolkit para crear la aplicación, puede hacerlo fácilmente con la opción Paquete de metadatos **zip Teams** en el menú Implementación de Teams Toolkit:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Opción &quot;Paquete Teams metadatos zip&quot; en Teams Toolkit extensión para Visual Studio Code":::

1. Inicie sesión en Teams con su cuenta de espacio aislado de espacio aislado y compruebe que está en la  vista previa del desarrollador público haciendo clic en el menú de puntos suspensivos (**...**) del perfil  de usuario y abriendo Acerca  de para comprobar que la opción Vista previa del desarrollador está activa.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="En Teams de puntos suspensivos, abra &quot;Acerca&quot; y compruebe que la opción &quot;Vista previa del programador&quot; esté activada.":::

1. Abre el *panel* Aplicaciones y haz clic **Upload una aplicación personalizada** y, a continuación **, Upload para mí o mis equipos**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Botón &quot;Upload una aplicación personalizada&quot; en el panel Teams &quot;Aplicaciones&quot;":::

1. Selecciona el paquete de la aplicación y haz clic *en Abrir*.

Una vez que se haya Teams, la extensión de mensajería estará disponible en Outlook en la Web.

## <a name="preview-your-messaging-extension-in-outlook"></a>Obtener una vista previa de la extensión de mensajería en Outlook

Ya está listo para probar la extensión de mensajería que se ejecuta en Outlook en Windows escritorio y la web. Aunque la extensión de mensajería actualizada seguirá en ejecución en Teams con compatibilidad completa con características para extensiones de [mensajería, hay](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) limitaciones en esta versión preliminar de la experiencia habilitada para Outlook para tener en cuenta:

* Las extensiones de mensajería Outlook se limitan al contexto de [*redacción de* correo](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Incluso si la Teams de `commandBox` mensajería incluye como contexto en su manifiesto, la vista previa actual se *limita a la* opción de composición de correo (`compose`). No se admite invocar una extensión de mensajería desde el cuadro *Outlook búsqueda global*.
* [Los comandos de extensión de mensajería basada](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) en acciones no se admiten en Outlook. Si la aplicación tiene comandos basados en búsqueda y en acción, aparecerá en Outlook pero el menú de acción no estará disponible.
* No se admite la inserción de más de cinco [tarjetas](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) adaptables en un correo electrónico; No se admiten las tarjetas adaptables v1.4 y posteriores.
* [Las acciones de](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) tarjeta de `messageBack`tipo , `imBack`, `invoke`y no `signin` se admiten para tarjetas insertadas. La compatibilidad se limita a `openURL`: al hacer clic, se redirigirá al usuario a la dirección URL especificada en una nueva pestaña.

Al probar la extensión de mensajería, puede identificar el origen (procedente de Teams frente a Outlook) de las solicitudes de bot por el [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) del [objeto Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Cuando un usuario realiza una consulta, el servicio recibe un objeto Bot Framework `Activity` estándar. Una de las propiedades del objeto Activity es `channelId`, que tendrá el valor de `msteams` o `outlook`, según el origen de la solicitud del bot. Para obtener más información,  [consulte Search based messaging extensions SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

### <a name="outlook"></a>Outlook

Para obtener una vista previa de la aplicación que se ejecuta Outlook en Windows escritorio, Outlook ha iniciado sesión con las credenciales del inquilino de prueba. Haga clic en **Nuevo correo electrónico**. Abre el **menú desplegable Más aplicaciones** en la cinta de opciones superior. Aparecerá la extensión de mensajería. Puede invocarlo desde allí y usarlo tal como lo haría al redactar un mensaje en Teams.

### <a name="outlook-on-the-web"></a>Outlook en la Web

Para obtener una vista previa de la aplicación que se Outlook en la Web, inicie sesión [en outlook.com](https://www.outlook.com) con las credenciales del inquilino de prueba. Haga clic en **Nuevo mensaje**. Abre el **menú desplegable Más aplicaciones** en la parte inferior de la ventana de composición. Aparecerá la extensión de mensajería. Puede invocarlo desde allí y usarlo tal como lo haría al redactar un mensaje en Teams.

## <a name="next-steps"></a>Siguientes pasos

Outlook habilitadas para Teams de mensajería están en versión preliminar y no son compatibles con el uso de producción. Este es el modo de distribuir la extensión de Outlook de mensajería habilitada para obtener una vista previa de audiencias con fines de prueba.

### <a name="single-tenant-distribution"></a>Distribución de un solo inquilino

Outlook y Office pestañas personales habilitadas para la vista previa se pueden distribuir a una audiencia de vista previa en un inquilino de prueba (o producción) de tres maneras:

#### <a name="teams-client"></a>Teams cliente

En el *menú* Aplicaciones, selecciona *Administrar las aplicacionesSubmit* >  **una aplicación a tu organización**. Esto requiere la aprobación del administrador de TI.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams de administración

Como administrador Teams, puede cargar e instalar previamente el paquete de la aplicación para el inquilino de la organización desde https://admin.teams.microsoft.com/. Consulta [Upload aplicaciones personalizadas en el Centro Microsoft Teams administración para](/MicrosoftTeams/upload-custom-apps) obtener más información.

#### <a name="microsoft-admin-center"></a>Centro de administración de Microsoft

Como administrador global, puedes cargar e instalar previamente el paquete de la aplicación desde https://admin.microsoft.com/. Consulta [Probar e implementar Aplicaciones Microsoft 365 asociados en el portal de aplicaciones integradas](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) para obtener más información.

### <a name="multi-tenant-distribution"></a>Distribución multiinquilino

La distribución a Microsoft AppSource aún no se admite durante esta versión preliminar del desarrollador de Outlook de mensajería Teams habilitadas.
