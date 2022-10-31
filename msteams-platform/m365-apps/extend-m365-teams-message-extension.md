---
title: Ampliar una extensión de mensajería de Teams en Microsoft 365
description: Obtenga información sobre cómo actualizar la extensión de mensaje basada en búsqueda para que se ejecute en Outlook, además de Microsoft Teams.
ms.date: 10/10/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 9b153eaaaa4cf3eb59d1a7b34122b569ae0d0d1a
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789949"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Ampliar una extensión de mensajería de Teams en Microsoft 365

Las extensiones de mensajes [basadas en búsqueda](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) permiten a los usuarios buscar en un sistema externo y compartir resultados a través del área de redacción de mensajes del cliente de Microsoft Teams. Ahora puede llevar extensiones de mensajes de Teams basadas en búsqueda de producción a audiencias en versión preliminar en outlook para escritorio de Windows y outlook.com [ampliando las aplicaciones de Teams en Microsoft 365](overview.md).

El proceso para actualizar la extensión de mensaje de Teams basada en búsqueda implica los pasos siguientes:

> [!div class="checklist"]
>
> * Actualizar el manifiesto de la aplicación
> * Agregar un canal de Outlook para el bot
> * Transferir localmente la aplicación actualizada en Teams

El resto de esta guía le guiará por estos pasos y muestra cómo obtener una vista previa de la extensión de mensaje en Outlook para escritorio y web de Windows.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, necesita:

* Una cuenta empresarial de espacio aislado del Programa de desarrolladores de Microsoft 365
* Inscripción en las *Versiones dirigidas de Office 365* para su cuenta empresarial de espacio aislado
* Un entorno de prueba con aplicaciones de Office instaladas desde el *canal beta* de Aplicaciones de Microsoft 365
* Código de Microsoft Visual Studio con la extensión del Kit de herramientas de Teams (opcional)

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="link-unfurling"></a>Apertura de vínculos

Si la extensión de mensaje basada en búsqueda admite [la desplegamiento de vínculos](../messaging-extensions/how-to/link-unfurling.md) en Teams, al completar los pasos de este tutorial también se habilita la desplegamiento de vínculos en entornos de escritorio de Outlook en la Web y Windows. En [la sección Ejemplos de código](#code-sample) siguiente se proporciona una aplicación de desplegada de vínculo simple para las pruebas.

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Preparar la extensión de mensajería para la actualización

Si tiene una extensión de mensajería existente, realice una copia o una rama del proyecto de producción para probar y actualizar el id. de la aplicación en el manifiesto de la aplicación y así usar un identificador nuevo (distinto del id. de aplicación de producción usado como prueba).

Si desea usar un código de ejemplo para completar este tutorial sobre cómo configurar una aplicación de Teams, siga los pasos de configuración de [Ejemplo de búsqueda de extensión de mensajería de Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) para crear rápidamente una extensión de mensajería basada en búsqueda de Microsoft Teams.

Como alternativa, puede usar la aplicación habilitada para Outlook lista para usar en la sección siguiente y omitir la parte de [*Actualización del manifiesto de aplicación*](#update-the-app-manifest) de este tutorial.

### <a name="quickstart"></a>Inicio rápido

Para empezar con una [extensión de mensajería de muestra](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) que ya esté habilitada para ejecutarse en Outlook, use la extensión del Kit de herramientas de Teams para Visual Studio Code.

1. En Visual Studio Code, abra la paleta de comandos (`Ctrl+Shift+P`), escriba `Teams: Create a new Teams app`.
1. Seleccione la opción **Crear una nueva aplicación de Teams**.
1. Seleccione las **Extensiones de mensajería basadas en búsqueda** para descargar el código de muestra para una extensión de mensajería de Teams con el manifiesto de aplicación de Teams más reciente (versión `1.13`).

    :::image type="content" source="images/toolkit-palatte-search-sample.png" alt-text="La captura de pantalla es un ejemplo que muestra la paleta de comandos de VS Code &quot;Crear una nueva aplicación de Teams&quot; para mostrar las opciones de ejemplo de Teams.":::

    El ejemplo también está disponible como *Conector de búsqueda NPM* en la galería de ejemplos del kit de herramientas de Teams. En el panel del Kit de herramientas de Teams, seleccione *Desarrollo* > *Ver muestras* > **Conector de búsqueda NPM**.

    :::image type="content" source="images/toolkit-search-sample.png" alt-text="La captura de pantalla es un ejemplo que muestra el ejemplo de NPM Search Connector en la galería de ejemplos del kit de herramientas de Teams.":::

1. Seleccione el lenguaje de programación preferido.
1. Seleccione una ubicación en la máquina local para la carpeta del área de trabajo y escriba el nombre de la aplicación.
1. Abra la paleta de comandos (`Ctrl+Shift+P`) y escriba `Teams: Provision in the cloud` para crear los recursos de aplicación necesarios (Azure App Service, plan App Service, Azure Bot e Identidad Administrada) en su cuenta de Azure.
1. Seleccione una suscripción y un grupo de recursos.
1. Seleccione **Aprovisionar**.
1. Abra la paleta de comandos (`Ctrl+Shift+P`) y escriba `Teams: Deploy to the cloud` para implementar el código de muestra en los recursos aprovisionados en Azure e iniciar la aplicación.
1. Seleccione **Implementar**.

Desde aquí, puede ir directamente hasta [Agregar un canal de Outlook para el bot](#add-an-outlook-channel-for-your-bot) para completar el paso final de habilitar la extensión de mensajería de Teams para que funcione en Outlook. (El manifiesto de la aplicación ya hace referencia a la versión correcta, por lo que no es necesario realizar ninguna actualización).

## <a name="update-the-app-manifest"></a>Actualización del manifiesto de la aplicación

Debe usar la versión `1.13` del esquema del [manifiesto para desarrolladores de Teams](../resources/schema/manifest-schema.md) para permitir que la extensión de mensaje de Teams se ejecute en Outlook.

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

Si ha usado el Kit de herramientas de Teams para crear su aplicación de extensión de mensajería, puede usarlo para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta de comandos (`Ctrl+Shift+P`) y busque **Teams: Validar archivo de manifiesto**.

## <a name="add-an-outlook-channel-for-your-bot"></a>Agregar un canal de Outlook para el bot

En Microsoft Teams, una extensión de mensajería consta de un servicio web que usted hospeda y un manifiesto de aplicación, que define dónde se hospeda el servicio web. El servicio web aprovecha el esquema de mensajería del SDK de [Bot Framework](/azure/bot-service/bot-service-overview) y el protocolo de comunicación segura a través de un canal de Teams registrado para su bot.

Para que los usuarios interactúen con la extensión de mensaje desde Outlook, debe agregar un canal de Outlook al bot:

1. En [Microsoft Azure Portal](https://portal.azure.com) (o [en el portal de Bot Framework](https://dev.botframework.com) si se registró anteriormente allí), vaya al recurso del bot.

1. En *Configuración*, seleccione **Canales**.

1. En *Canales disponibles*, seleccione **Outlook**. Seleccione la pestaña **Extensiones de mensajería** y, a continuación, **Aplicar**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="La captura de pantalla es un ejemplo que muestra el canal &quot;Extensiones de mensaje&quot; de Outlook para el bot desde el panel Canales de bot de Azure.":::

1. Confirme que el canal de Outlook aparece junto con Teams en el panel **Canales** del bot.

    :::image type="content" source="images/azure-bot-channels.png" alt-text="La captura de pantalla es un ejemplo que muestra el panel Canales de bot de Azure que muestra los canales de Teams y Outlook.":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Actualización del registro de aplicaciones de Microsoft Azure Active Directory (Azure AD) para SSO

> [!NOTE]
> Puede omitir este paso si usa la [aplicación de ejemplo](#quickstart) proporcionada en este tutorial, ya que el escenario no implica la autenticación Sign-On única de Azure Active Directory (AAD).

El inicio de sesión único (SSO) de Azure Active Directory (AD) para extensiones de mensajes funciona de la misma manera tanto en Outlook [como en Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots). Sin embargo, debe agregar varios identificadores de aplicación cliente al registro de aplicaciones de Azure AD del bot en *el portal de Registros de aplicaciones* del inquilino.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con su cuenta empresarial de espacio aislado.
1. Abra **Registros de aplicaciones**.
1. Seleccione el nombre de la aplicación para abrir el registro de la aplicación.
1. Seleccione **Exponer una API** (en *Administrar*).
1. En la sección **Aplicaciones cliente autorizadas** asegúrese de que aparecen todos los siguientes valores `Client Id`:

   |Microsoft 365 aplicación cliente | Id. de cliente |
   |--|--|
   |Escritorio y móvil de Teams |1fec8e78-bli4-4aaf-ab1b-5451cc387264 |
   |Web de Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
   |Versión de escritorio de Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
   |Outlook Web Access | 00000002-0000-0ff1-ce00-0000000000000 |
   |Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>Transferir localmente la extensión de mensajería actualizada en Teams

El último paso es transferir localmente la extensión de mensaje actualizada ([paquete de aplicación](/microsoftteams/platform/concepts/build-and-test/apps-package)) en Teams. Una vez completado, la extensión de mensaje aparece en las *aplicaciones instaladas* desde el área de redacción del mensaje.

1. Empaquete la aplicación de Teams (iconos de [manifiesto y aplicación](/microsoftteams/platform/resources/schema/manifest-schema#icons)) en un archivo ZIP. Si usó el Kit de herramientas de Teams para crear la aplicación, puede hacerlo fácilmente con la opción **Comprimir paquete de metadatos de Teams** en el menú de *Implementación* del Kit de herramientas de Teams.

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción &quot;Zip Teams metadata package&quot; (Paquete de metadatos de Teams zip) en la extensión del kit de herramientas de Teams para Visual Studio Code.":::

1. Inicie sesión en Teams con su espacio empresarial aislado y alterne al modo *Vista previa para desarrolladores*. Seleccione el menú de los puntos suspensivos (**...**) junto al perfil de usuario y, luego, seleccione **Acerca de** > **Vista previa para desarrolladores**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción &quot;Developer Preview&quot;.":::

1. Seleccione **Aplicaciones** para abrir el panel **Administrar aplicaciones**. A continuación, seleccione **Cargar una aplicación**.

    :::image type="content" source="../assets/images/teams-manage-your-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción &quot;Cargar una aplicación&quot;.":::

1. Elija **la opción Cargar una aplicación personalizada** , seleccione el paquete de la aplicación e instálelo (*Agregar*) en el cliente de Teams.

    :::image type="content" source="../assets/images/teams-upload-custom-app.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción &quot;Cargar una aplicación personalizada&quot; en Teams.":::

Una vez que se ha cargado de forma local a través de Teams, la extensión de mensaje está disponible en Outlook para escritorio y web de Windows.

## <a name="preview-your-message-extension-in-outlook"></a>Obtener una vista previa de la extensión de mensajería en Outlook

A continuación le mostramos cómo probar la extensión de mensajería que se ejecuta en Outlook en el escritorio de Windows y en la Web.

### <a name="outlook-on-the-web"></a>Outlook en la Web

Para obtener una vista previa de la aplicación que se ejecuta en Outlook en la Web:

1. Inicie sesión en [outlook.com](https://www.outlook.com) con las credenciales del inquilino de prueba.
1. Seleccione **Nuevo mensaje**.
1. Abra el menú flotante **Más aplicaciones** en la parte inferior de la ventana de redacción.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra el menú &quot;Más aplicaciones&quot; en la parte inferior de la ventana de composición de correo para usar la extensión de mensaje.":::

Your message extension is listed. You can invoke it from there and use it just as you would while composing a message in Teams.

### <a name="outlook"></a>Outlook

Para obtener una vista previa de la aplicación ejecutándose en Outlook en el escritorio de Windows:

1. Inicie Outlook e inicie sesión con sus credenciales de inquilino de prueba.
1. Seleccione **Nuevo correo electrónico**.
1. Abra el menú flotante **Más aplicaciones** en la cinta de opciones superior.

    :::image type="content" source="images/outlook-desktop-compose-more-apps.png" alt-text="La captura de pantalla es un ejemplo que muestra &quot;Más aplicaciones&quot; en la cinta de opciones de la ventana de composición para usar la extensión de mensaje.":::

Aparece la extensión de mensajería y se abre un panel adyacente para mostrar los resultados de la búsqueda.

## <a name="troubleshooting"></a>Solución de problemas

 Aunque la extensión de mensajería actualizada seguirá ejecutándose en Teams con compatibilidad completa con [características para las extensiones de mensajería](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions), hay limitaciones en esta versión preliminar anticipada de la experiencia habilitada para Outlook que debe tener en cuenta:

* Las extensiones de mensajería en Outlook se limitan al [*contexto* redacción](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions) del correo. Incluso si la extensión de mensajería de Teams incluye `commandBox` como un *contexto* en su manifiesto, la vista previa actual se limita a la opción de redacción del correo (`compose`). No se admite la invocación de una extensión de mensajería desde el cuadro de *Búsqueda* global de Outlook.
* Los comandos [de extensión de mensajes basados en](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) acciones no se admiten en Outlook. Si la aplicación tiene comandos basados en búsquedas y acciones, aparecerá en Outlook, pero el menú de acciones no estará disponible.
* No se admite la inserción de más de cinco [Tarjetas adaptables](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) en un correo electrónico; no se admiten Tarjetas adaptables v1.4 ni versiones posteriores.
* No se admiten las [acciones de tarjeta](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) de tipo `messageBack`, `imBack`, `invoke` y `signin` para las tarjetas insertadas. La compatibilidad se limita a `openURL`: cuando se selecciona, el usuario se redirige a la dirección URL especificada en una nueva pestaña.

Use los [canales de la comunidad de desarrolladores de Microsoft Teams](/microsoftteams/platform/feedback) para notificar problemas y enviar comentarios.

### <a name="debugging"></a>Depuración

Al probar la extensión de mensaje, puede identificar el origen (que se origina en Teams frente a Outlook) de las solicitudes de bot por el [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) del objeto [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Cuando un usuario realiza una consulta, el servicio recibe un objeto Bot Framework `Activity` estándar. Una de las propiedades del objeto Activity es `channelId`, que tendrá el valor de `msteams` o `outlook`, en función de dónde se origine la solicitud del bot. Para obtener más información, consulte [El SDK de extensiones de mensaje basadas en búsquedas](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de ejemplo** | **Descripción** | **Node.js** |
|---------------|--------------|--------|
| Conector de búsqueda NPM | Use el Kit de herramientas de Teams para crear una aplicación de extensión de mensajería. Funciona en Teams, Outlook. |  [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) |
| Desplegamiento de vínculos de Teams | Aplicación sencilla de Teams para mostrar la desplegamiento de vínculos. Funciona en Teams, Outlook. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling)

## <a name="next-step"></a>Paso siguiente

Publique la aplicación para que sea detectable en Teams, Outlook y Office:

> [!div class="nextstepaction"]
> [Publicar aplicaciones de Teams para Outlook y Office](publish.md)
