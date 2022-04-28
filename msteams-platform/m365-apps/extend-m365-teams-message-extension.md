---
title: Extensión de una extensión de mensaje de Teams entre Microsoft 365
description: A continuación se muestra cómo actualizar la extensión de mensaje de Teams basada en búsqueda para que se ejecute en Outlook
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 3bab70d85d071763ffbbae7cb1dae11534d0e812
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104542"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Extensión de una extensión de mensaje de Teams entre Microsoft 365

> [!NOTE]
> *La extensión de una extensión de mensaje de Teams entre Microsoft 365* solo está disponible actualmente en la [versión preliminar del desarrollador público](../resources/dev-preview/developer-preview-intro.md). Es posible que las características incluidas en la versión preliminar no estén completas y experimenten cambios antes de estar disponibles en la versión pública. Se proporcionan solo con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

Las [extensiones de mensajes basadas](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) en búsqueda permiten a los usuarios buscar en un sistema externo y compartir resultados a través del área de mensajes de redacción del cliente de Microsoft Teams. Al [ampliar las aplicaciones de Teams entre Microsoft 365 (versión preliminar),](overview.md) ahora puede llevar las extensiones de mensajes de Teams basadas en búsqueda a Outlook para Windows experiencias de escritorio y web.

El proceso para actualizar la extensión de mensaje de Teams basada en búsqueda para ejecutar Outlook implica estos pasos:

> [!div class="checklist"]
>
> * Actualización del manifiesto de la aplicación
> * Adición de un canal de Outlook para el bot
> * Transferir localmente la aplicación actualizada en Teams

El resto de esta guía le guiará por estos pasos y le mostrará cómo obtener una vista previa de la extensión de mensaje en Outlook para Windows escritorio y web.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, necesitará lo siguiente:

* Un inquilino de espacio aislado del Programa para desarrolladores de Microsoft 365
* El inquilino del espacio aislado inscrito en *Office 365 versiones dirigidas*
* Un entorno de prueba con aplicaciones Office instaladas desde el *canal beta* de Aplicaciones Microsoft 365
* Microsoft Visual Studio Código con la extensión Teams Toolkit (versión preliminar) (opcional)

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Preparación de la extensión de mensaje para la actualización

Si tiene una extensión de mensaje existente, realice una copia o una rama del proyecto de producción para probar y actualice el identificador de aplicación en el manifiesto de la aplicación para usar un nuevo identificador (distinto del identificador de aplicación de producción).

Si desea usar código de ejemplo para completar este tutorial, siga los pasos de configuración de [Teams ejemplo de búsqueda de extensión de mensaje](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) para crear rápidamente una extensión de mensaje basada en búsqueda de Microsoft Teams. O bien, puede empezar con el mismo [Teams ejemplo de búsqueda de extensiones de mensaje actualizado para la versión preliminar del SDK de TeamsJS v2](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365) y continuar con [la vista previa de la extensión de mensaje en Outlook](#preview-your-message-extension-in-outlook). El ejemplo actualizado también está disponible dentro de Teams Toolkit extensión: *DevelopmentView* >  *samplesNPM* >  **Search Connector**.

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Ejemplo de npm search connector en Teams Toolkit":::

## <a name="update-the-app-manifest"></a>Actualización del manifiesto de aplicación

Tendrá que usar el esquema de [manifiesto de Teams versión preliminar del desarrollador](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) y la versión del `m365DevPreview` manifiesto para permitir que la extensión de mensaje de Teams se ejecute en Outlook.

Tiene dos opciones para actualizar el manifiesto de la aplicación:

# <a name="teams-toolkit"></a>[Kit de herramientas de Teams](#tab/manifest-teams-toolkit)

1. Abra la *paleta Comandos*: `Ctrl+Shift+P`
1. Ejecute el comando y seleccione el `Teams: Upgrade Teams manifest to support Outlook and Office apps` archivo de manifiesto de la aplicación. Los cambios se realizarán en su lugar.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abra el manifiesto de la aplicación de Teams y actualice `$schema` y `manifestVersion` con los valores siguientes:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Si usó Teams Toolkit para crear la aplicación de extensión de mensaje, puede usarla para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta `Ctrl+Shift+P` de comandos y busque **Teams: Validar archivo de manifiesto** o seleccione la opción en el menú Implementación de la Teams Toolkit (busque el icono de Teams en el lado izquierdo de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit opción &quot;Validar archivo de manifiesto&quot; en el menú &quot;Implementación&quot;":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Adición de un canal de Outlook para el bot

En Microsoft Teams, una extensión de mensaje consta de un servicio web que se hospeda y un manifiesto de aplicación, que define dónde se hospeda el servicio web. El servicio web aprovecha el esquema de mensajería del [SDK de Bot Framework](/azure/bot-service/bot-service-overview) y protege el protocolo de comunicación a través de un canal de Teams registrado para el bot.

Para que los usuarios interactúen con la extensión de mensaje desde Outlook, deberá agregar un canal de Outlook al bot:

1. En [Microsoft Azure portal](https://portal.azure.com) (o [portal de Bot Framework](https://dev.botframework.com) si se registró anteriormente allí), vaya al recurso del bot.

1. En *Configuración*, seleccione **Canales**.

1. Haga clic en **Outlook**, seleccione la pestaña **Extensiones de mensaje** y, a continuación, haga clic en **Guardar**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Agregue un canal de Outlook &quot;Extensiones de mensaje&quot; para el bot desde el panel Canales de bot de Azure":::

1. Confirme que el canal de Outlook aparece junto con Microsoft Teams en el panel **Canales** del bot:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Panel Canales de bot de Azure en el que se enumeran los canales Microsoft Teams y Outlook":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Actualización del registro de aplicaciones de Microsoft Azure Active Directory (Azure AD) para sso

> [!NOTE]
> Puede omitir el paso si usa [Teams ejemplo de búsqueda de extensión de mensaje](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search), ya que el escenario no implica la autenticación Azure Active Directory (AAD) Sign-On única.

Azure Active Directory inicio de sesión único (SSO) para las extensiones de mensaje funciona de la misma manera en Outlook [que en Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots), sin embargo, debe agregar varios identificadores de aplicación cliente al registro de la aplicación Azure AD del bot en el inquilino.*Registros de aplicaciones* portal.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con su cuenta de inquilino de espacio aislado.
1. Abra **Registros de aplicaciones**.
1. Seleccione el nombre de la aplicación para abrir el registro de la aplicación.
1. Seleccione  **Exponer una API** (en *Administrar*).

En la sección **Aplicaciones cliente autorizadas** , asegúrese de que aparecen todos los valores siguientes `Client Id` :

|Microsoft 365 aplicación cliente | Id. de cliente |
|--|--|
|Teams escritorio y móvil |1fec8e78-bli4-4aaf-ab1b-5451cc387264 |
|Web de Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Versión de escritorio de Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-0000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>Transferir localmente la extensión de mensaje actualizada en Teams

El último paso consiste en transferir localmente la extensión de mensaje actualizada ([paquete de aplicación](/microsoftteams/platform/concepts/build-and-test/apps-package)) en Microsoft Teams. Una vez completada, la extensión de mensaje aparecerá en las *aplicaciones instaladas* desde el área de redacción del mensaje.

1. Empaquete la aplicación de Teams ([manifiesto e iconos](/microsoftteams/platform/resources/schema/manifest-schema#icons) de aplicación) en un archivo ZIP. Si usó Teams Toolkit para crear la aplicación, puede hacerlo fácilmente mediante la opción **Zip Teams metadata package** del menú *Implementación* de Teams Toolkit:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Opción &quot;Zip Teams metadata package&quot; en Teams Toolkit extensión para Visual Studio Code":::

1. Inicie sesión en Teams con su cuenta de inquilino de espacio aislado y compruebe que está en la *versión preliminar del desarrollador público* haciendo clic en el menú de puntos suspensivos (**...**) del perfil de usuario y abriendo **Acerca de** para comprobar que la opción *Vista previa del desarrollador* está activada.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="En Teams menú de puntos suspensivos, abra &quot;Acerca de&quot; y compruebe que la opción &quot;Developer Preview&quot; está activada.":::

1. Abra el panel *Aplicaciones* y haga clic en **Upload una aplicación personalizada** y, a continuación, **Upload para mí o mis equipos**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Botón &quot;Upload una aplicación personalizada&quot; en el panel &quot;Aplicaciones&quot; de Teams":::

1. Seleccione el paquete de la aplicación y haga clic en *Abrir*.

Una vez que se haya cargado de forma local a través de Teams, la extensión de mensaje estará disponible en Outlook en la Web.

## <a name="preview-your-message-extension-in-outlook"></a>Vista previa de la extensión de mensaje en Outlook

Ya está listo para probar la extensión de mensaje que se ejecuta en Outlook en Windows escritorio y en la web. Aunque la extensión de mensaje actualizada seguirá ejecutándose en Teams con compatibilidad completa con [características para extensiones de mensaje](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions), hay limitaciones en esta versión preliminar temprana de la experiencia habilitada para Outlook que debe tener en cuenta:

* Las extensiones de mensaje de Outlook se limitan al contexto de [*redacción*](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions) de correo. Incluso si la extensión de mensaje de Teams incluye `commandBox` como *contexto* en su manifiesto, la versión preliminar actual se limita a la opción de composición de correo (`compose`). No se admite la invocación de una extensión de mensaje desde el cuadro *de búsqueda* de Outlook global.
* Los comandos [de extensión de mensajes basados en](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) acciones no se admiten en Outlook. Si la aplicación tiene comandos basados en búsqueda y acción, aparecerá en Outlook, pero el menú de acciones no estará disponible.
* No se admite la inserción de más de cinco [tarjetas adaptables](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) en un correo electrónico; No se admiten las tarjetas adaptables v1.4 y posteriores.
* [Las acciones de tarjeta](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) de tipo `messageBack`, `imBack`, `invoke`y `signin` no se admiten para las tarjetas insertadas. La compatibilidad se limita a `openURL`: al hacer clic, el usuario se redirigirá a la dirección URL especificada en una nueva pestaña.

Al probar la extensión de mensaje, puede identificar el origen (que se origina en Teams frente a Outlook) de las solicitudes de bot por el [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) del objeto [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Cuando un usuario realiza una consulta, el servicio recibe un objeto estándar de Bot Framework `Activity` . Una de las propiedades del objeto Activity es `channelId`, que tendrá el valor de `msteams` o `outlook`, en función de dónde se origine la solicitud del bot. Para obtener más información, consulte  [El SDK de extensiones de mensaje basadas en búsquedas](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

### <a name="outlook-on-the-web"></a>Outlook en la Web

Para obtener una vista previa de la aplicación que se ejecuta en Outlook en la Web:

1. Inicie sesión en [outlook.com](https://www.outlook.com) con las credenciales del inquilino de prueba.
1. Seleccione **Nuevo mensaje**.
1. Abra el menú flotante **Más aplicaciones** en la parte inferior de la ventana de composición.

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Haga clic en el menú &quot;Más aplicaciones&quot; en la parte inferior de la ventana de composición de correo para usar la extensión de mensaje.":::

Se mostrará la extensión de mensaje. Puede invocarlo desde allí y usarlo como lo haría al redactar un mensaje en Teams.

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> Consulte las actualizaciones más recientes de [Microsoft Teams- Microsoft 365 Blog para desarrolladores](https://devblogs.microsoft.com/microsoft365dev/) para comprobar si Outlook en Windows soporte técnico de escritorio para Teams aplicaciones personales está disponible para el inquilino de prueba.

Para obtener una vista previa de la aplicación que se ejecuta en Outlook en Windows escritorio:

1. Inicie Outlook haya iniciado sesión con las credenciales del inquilino de prueba. 1. Haga clic en **Nuevo correo electrónico**.
1. Abra el menú flotante **Más aplicaciones** en la cinta de opciones superior.

Se mostrará la extensión de mensaje. Puede invocarlo desde allí y usarlo como lo haría al redactar un mensaje en Teams.

## <a name="next-steps"></a>Siguientes pasos

las extensiones de mensaje de Teams habilitadas para Outlook están en versión preliminar y no se admiten para su uso en producción. A continuación se muestra cómo distribuir la extensión de mensaje habilitada para Outlook para obtener una vista previa de las audiencias con fines de prueba.

### <a name="single-tenant-distribution"></a>Distribución de un solo inquilino

las pestañas personales habilitadas para Office y Outlook se pueden distribuir a un público en versión preliminar a través de un inquilino de prueba (o producción) de una de estas tres maneras:

#### <a name="teams-client"></a>Cliente de Teams

En el menú *Aplicaciones*, seleccione *Administrar las aplicacionesSumisión* >  **de una aplicación a su organización**. Esto requiere la aprobación del administrador de TI.

#### <a name="microsoft-teams-admin-center"></a>Centro de administración de Microsoft Teams

Como administrador de Teams, puede cargar y preinstalar el paquete de la aplicación para el inquilino de la organización desde [Teams administrador](https://admin.teams.microsoft.com/). Consulte [Upload las aplicaciones personalizadas en el Centro de administración de Microsoft Teams](/MicrosoftTeams/upload-custom-apps) para obtener más información.

#### <a name="microsoft-admin-center"></a>Centro de administración de Microsoft

Como administrador global, puede cargar y preinstalar el paquete de la aplicación desde el [administrador de Microsoft](https://admin.microsoft.com/). Consulte [Prueba e implementación de Aplicaciones Microsoft 365 por asociados en el portal de aplicaciones integradas](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) para obtener más información.

### <a name="multitenant-distribution"></a>Distribución multiinquilino

La distribución a Microsoft AppSource aún no se admite durante esta versión preliminar para desarrolladores de extensiones de mensaje de Teams habilitadas para Outlook.
