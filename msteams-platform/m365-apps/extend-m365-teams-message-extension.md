---
title: Ampliar una extensión de mensajería de Teams en Microsoft 365
description: Aquí le mostramos cómo actualizar la extensión de mensajería de Teams basada en búsqueda para que se ejecute en Outlook
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 7e3a0d772367952c1726648fce2f10e1d8b885b2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111377"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Ampliar una extensión de mensajería de Teams en Microsoft 365

> [!NOTE]
> *Ampliar una extensión de mensajería de Teams en Microsoft 365* solo está disponible actualmente en [versión preliminar pública para desarrolladores](../resources/dev-preview/developer-preview-intro.md). Es posible que las características incluidas en la versión preliminar no estén completas y experimenten cambios antes de estar disponibles en la versión pública. Se proporcionan solo con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

Las extensiones de mensajes [basadas en búsqueda](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) permiten a los usuarios buscar en un sistema externo y compartir resultados a través del área de redacción de mensajes del cliente de Microsoft Teams. Al [ampliar las aplicaciones de Teams en Microsoft 365 (versión preliminar)](overview.md), ahora puede traer las extensiones de mensajes de Teams basadas en búsqueda a las experiencias de escritorio y web de Outlook para Windows.

El proceso para actualizar la extensión de mensajería de Teams basada en búsqueda para ejecutar Outlook implica estos pasos:

> [!div class="checklist"]
>
> * Actualizar el manifiesto de la aplicación
> * Agregar un canal de Outlook para el bot
> * Transferir localmente la aplicación actualizada en Teams

El resto de esta guía le guiará a través de estos pasos y le mostrará cómo obtener una vista previa de la extensión de mensajería tanto en Outlook para Windows en la web y de escritorio.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, necesitará:

* Una cuenta empresarial de espacio aislado del Programa de desarrolladores de Microsoft 365
* El inquilino de espacio aislado inscrito en *Versiones dirigidas de Office 365*
* Un entorno de prueba con aplicaciones de Office instaladas desde el *canal beta* Aplicaciones de Microsoft 365
* Código de Microsoft Visual Studio con la extensión Kit de herramientas de Teams (versión preliminar) (opcional)

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Preparar la extensión de mensajería para la actualización

Si tiene una extensión de mensajería existente, realice una copia o una rama del proyecto de producción para probar y actualizar el identificador de aplicación en el manifiesto de la aplicación para usar un identificador nuevo (distinto del identificador de aplicación de producción).

Si desea usar código de ejemplo para completar este tutorial, siga los pasos de configuración de [Ejemplo de búsqueda de extensión de mensajería de Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) para crear rápidamente una extensión de mensajería basada en búsqueda de Microsoft Teams. O bien, puede empezar con el mismo ejemplo de búsqueda de extensiones de mensajería de [Teams actualizado para la versión preliminar v2 del SDK de TeamsJS](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365) y continuar con [Vista previa de la extensión de mensajería en Outlook](#preview-your-message-extension-in-outlook). El ejemplo actualizado también está disponible en la extensión Kit de herramientas de Teams: *Desarrollo* > *Ver ejemplos* > **Conector de búsqueda NPM**.

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Ejemplo de conector de búsqueda NPM en el Kit de herramientas de Teams":::

## <a name="update-the-app-manifest"></a>Actualización del manifiesto de la aplicación

Tendrá que usar el esquema [Manifiesto de la versión preliminar para desarrolladores de Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) y la versión del manifiesto `m365DevPreview` para permitir que la extensión de mensajería de Teams se ejecute en Outlook.

Tienes dos opciones para actualizar el manifiesto de la aplicación:

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

Si ha usado el Kit de herramientas de Teams para crear su aplicación de extensión de mensajería, puede usarlo para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta de comandos `Ctrl+Shift+P` y busque **Teams: validar el archivo de manifiesto** o seleccione la opción en el menú Implementación del Kit de herramientas de Teams (busque el icono de Teams en el lado izquierdo de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="La opción &quot;Validar archivo de manifiesto&quot; del Kit de herramientas de Teams en el menú &quot;Implementación&quot;":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Agregar un canal de Outlook para el bot

En Microsoft Teams, una extensión de mensajería consta de un servicio web que usted hospeda y un manifiesto de aplicación, que define dónde se hospeda el servicio web. El servicio web aprovecha el esquema de mensajería del SDK de [Bot Framework](/azure/bot-service/bot-service-overview) y el protocolo de comunicación segura a través de un canal de Teams registrado para su bot.

Para que los usuarios interactúen con la extensión de mensajería desde Outlook, deberá agregar un canal de Outlook al bot:

1. Desde [Microsoft Azure Portal](https://portal.azure.com) (o [Bot Framework portal](https://dev.botframework.com) si se registró anteriormente allí), vaya al recurso del bot.

1. En *Configuración*, seleccione **Canales**.

1. Haga clic en **Outlook**, seleccione la pestaña **Extensiones de mensajería** y, a continuación, haga clic en **Guardar**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Agregar un canal &quot;Extensiones de mensaje&quot; de Outlook para el bot desde el panel Canales de bot de Azure":::

1. Confirme que el canal de Outlook aparece junto con Microsoft Teams en el panel **Canales del bot**:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Panel Canales de bots de Azure que enumera los canales de Microsoft Teams y Outlook":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Actualización del registro de aplicaciones de Microsoft Azure Active Directory (Azure AD) para SSO

> [!NOTE]
> Puede omitir el paso si usa el [Ejemplo de búsqueda de extensión de mensajería de Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search), ya que el escenario no implica la autenticación de inicio de sesión único de Azure Active Directory (AAD).

El inicio de sesión único (SSO) de Azure Active Directory para extensiones de mensajes funciona de la misma manera tanto en Outlook [como en Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots), sin embargo, debe agregar varios identificadores de aplicación cliente al registro de aplicación de Azure AD del bot en el portal *Registros de aplicaciones* de la cuenta empresarial.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con su cuenta empresarial de espacio aislado.
1. Abra **Registros de aplicaciones**.
1. Seleccione el nombre de la aplicación para abrir el registro de la aplicación.
1. Seleccione **Exponer una API** (en *Administrar*).

En la sección **Aplicaciones cliente autorizadas** asegúrese de que aparecen todos los siguientes valores `Client Id`:

|Microsoft 365 aplicación cliente | Id. de cliente |
|--|--|
|Escritorio y móvil de Teams |1fec8e78-bli4-4aaf-ab1b-5451cc387264 |
|Web de Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Versión de escritorio de Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-0000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>Transferir localmente la extensión de mensajería actualizada en Teams

El último paso consiste en transferir localmente la extensión de mensajería actualizada ([paquete de la aplicación](/microsoftteams/platform/concepts/build-and-test/apps-package)) en Microsoft Teams. Una vez completada, la extensión de mensajería aparecerá en *Aplicaciones* instaladas desde el área de redacción del mensaje.

1. Empaquete la aplicación de Teams (iconos de [manifiesto y aplicación](/microsoftteams/platform/resources/schema/manifest-schema#icons)) en un archivo ZIP. Si usó el Kit de herramientas de Teams para crear la aplicación, puede hacerlo fácilmente con la opción **Comprimir paquete de metadatos de Teams** en el menú de *Implementación* del Kit de herramientas de Teams:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Opción &quot;Comprimir paquete de metadatos de Teams&quot; en la extensión Kit de herramientas de Teams para Visual Studio Code":::

1. Inicie sesión en Teams con su cuenta empresarial de espacio aislado y compruebe que se encuentra en la *Versión preliminar pública para desarrolladores*; para ello, haga clic en el menú de puntos suspensivos (**...**) del perfil de usuario y abra **Acerca de** para comprobar que la opción *Vista previa de desarrollador* está activada.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="En el menú de puntos suspensivos de Teams, abra &quot;Acerca de&quot; y compruebe que la opción &quot;Vista previa de desarrollador&quot; esté activada":::

1. Abra el panel *Aplicaciones* y haga clic en **Cargar una aplicación personalizada** y, a continuación, **Cargar para mí o mis equipos**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Botón &quot;Cargar una aplicación personalizada&quot; en el panel &quot;Aplicaciones&quot; de Teams":::

1. Seleccione el paquete de la aplicación y haga clic en *Abrir*.

Una vez transferida localmente a través de Teams, la extensión de mensajería estará disponible en Outlook en la Web.

## <a name="preview-your-message-extension-in-outlook"></a>Obtener una vista previa de la extensión de mensajería en Outlook

Ahora está listo para probar la extensión de mensajería que se ejecuta en Outlook en el escritorio de Windows y en la Web. Aunque la extensión de mensajería actualizada seguirá ejecutándose en Teams con compatibilidad completa con [características para las extensiones de mensajería](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions), hay limitaciones en esta versión preliminar anticipada de la experiencia habilitada para Outlook que debe tener en cuenta:

* Las extensiones de mensajería en Outlook se limitan al [*contexto* redacción](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions) del correo. Incluso si la extensión de mensajería de Teams incluye `commandBox` como un *contexto* en su manifiesto, la vista previa actual se limita a la opción de redacción del correo (`compose`). No se admite la invocación de una extensión de mensajería desde el cuadro de *Búsqueda* global de Outlook.
* Los comandos de [extensión de mensajería basados en acciones](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) no se admiten en Outlook. Si la aplicación tiene comandos basados en búsqueda y en acciones, aparecerá en Outlook, pero el menú de acción no estará disponible.
* No se admite la inserción de más de cinco [Tarjetas adaptables](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) en un correo electrónico; Tarjetas adaptables v1.4 y versiones posteriores no se admiten.
* No se admiten [Acciones de tarjeta](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) de tipo `messageBack`, `imBack`, `invoke`y `signin` para tarjetas insertadas. La compatibilidad se limita a `openURL`: al hacer clic, se redirigirá al usuario a la dirección URL especificada en una pestaña nueva.

Al probar la extensión de mensaje, puede identificar el origen (que se origina en Teams frente a Outlook) de las solicitudes de bot por el [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) del objeto [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Cuando un usuario realiza una consulta, el servicio recibe un objeto Bot Framework `Activity` estándar. Una de las propiedades del objeto Activity es `channelId`, que tendrá el valor de `msteams` o `outlook`, dependiendo de dónde se origine la solicitud del bot. Para obtener más información, consulte  [SDK de extensiones de mensajería basadas en búsqueda](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

### <a name="outlook-on-the-web"></a>Outlook en la Web

Para obtener una vista previa de la aplicación que se ejecuta en Outlook en la Web:

1. Inicie sesión en [outlook.com](https://www.outlook.com) con credenciales para la cuenta empresarial de prueba.
1. Seleccione **Nuevo mensaje**.
1. Abra el menú flotante **Más aplicaciones** en la parte inferior de la ventana de redacción.

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Haga clic en el menú &quot;Más aplicaciones&quot; en la parte inferior de la ventana de redacción de correo para usar la extensión de mensaje":::

Se mostrará la extensión de mensajería. Puede invocarla desde allí y usarla como lo haría al redactar un mensaje en Teams.

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> Consulte las actualizaciones más recientes de [Microsoft Teams: blog de Microsoft 365 para desarrolladores](https://devblogs.microsoft.com/microsoft365dev/) para comprobar si la compatibilidad de escritorio de Outlook en Windows con aplicaciones personales de Teams está disponible para su cuenta empresarial de prueba.

Para obtener una vista previa de la aplicación ejecutándose en Outlook en el escritorio de Windows:

1. Inicie la sesión de Outlook con credenciales para la cuenta empresarial de prueba. 1. Haga clic en **Nuevo correo electrónico**.
1. Abra el menú flotante **Más aplicaciones** en la cinta de opciones superior.

Se mostrará la extensión de mensajería. Puede invocarla desde allí y usarla como lo haría al redactar un mensaje en Teams.

## <a name="next-steps"></a>Pasos siguientes

Las extensiones de mensajería de Teams habilitadas para Outlook están en versión preliminar y no se admiten para su uso en producción. Esta es la manera de distribuir la extensión de mensajería habilitada para Outlook a audiencias de vista previa con fines de prueba.

### <a name="single-tenant-distribution"></a>Distribución de cuenta empresarial única

Las pestañas personales habilitadas para Outlook y Office se pueden distribuir a una audiencia preliminar a través de una cuenta empresarial de prueba (o producción) de una de estas tres maneras:

#### <a name="teams-client"></a>Cliente de Teams

En el menú *Aplicaciones*, seleccione *Administrar las aplicaciones* > **Enviar una aplicación a la organización**. Esto requiere la aprobación del administrador de TI.

#### <a name="microsoft-teams-admin-center"></a>Centro de administración de Microsoft Teams

Como administrador de Teams, puede cargar e instalar previamente el paquete de la aplicación para la cuenta empresarial de su organización desde [Administrador de Teams](https://admin.teams.microsoft.com/). Consulte [Cargar las aplicaciones personalizadas en el Centro de administración de Microsoft Teams](/MicrosoftTeams/upload-custom-apps) para obtener más información.

#### <a name="microsoft-admin-center"></a>Centro de administración de Microsoft

Como administrador global, puede cargar e instalar previamente el paquete de la aplicación desde [Administrador de Microsoft](https://admin.microsoft.com/). Consulte [Probar e implementar aplicaciones de Microsoft 365 por asociados en el portal de aplicaciones integradas](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) para obtener más información.

### <a name="multitenant-distribution"></a>Distribución de varias cuentas empresariales

La distribución a Microsoft AppSource aún no se admite durante esta versión preliminar para desarrolladores de las extensiones de mensajería de Teams habilitadas para Outlook.
