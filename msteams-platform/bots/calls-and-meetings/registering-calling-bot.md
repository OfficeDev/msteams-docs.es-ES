---
title: Registrar un bot de llamadas y reuniones para Microsoft Teams
description: Obtenga información sobre cómo registrar un nuevo bot de llamadas de audio y vídeo para Microsoft Teams
ms.topic: conceptual
keywords: llamar a los medios de audio y vídeo de audio y vídeo del bot
ms.openlocfilehash: 6cbba3f63a97e47fd9cca6dbeea6595cc3bdc9d7
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696362"
---
# <a name="register-a-calls-and-meetings-bot-for-microsoft-teams"></a>Registrar un bot de llamadas y reuniones para Microsoft Teams

Un bot que participa en llamadas de audio o vídeo y reuniones en línea es un bot de Microsoft Teams normal con las siguientes características adicionales usadas para registrar el bot:

* Hay una nueva versión del manifiesto de la aplicación de Teams con dos configuraciones `supportsCalling` adicionales y `supportsVideo` . Esta configuración se incluye en la versión [preliminar](../../resources/dev-preview/developer-preview-intro.md) del desarrollador del manifiesto de la aplicación de Teams.
* [Los permisos de Microsoft Graph](./registering-calling-bot.md#add-graph-permissions) deben configurarse para el identificador de aplicación de Microsoft del bot.
* Los permisos de las API de llamadas y reuniones en línea de Graph requieren el consentimiento del administrador de inquilinos.

## <a name="new-manifest-settings"></a>Nueva configuración del manifiesto

Los bots de llamadas y reuniones en línea tienen las siguientes dos opciones de configuración adicionales en el manifest.jsque habilitan audio o vídeo para el bot en Teams.

* `bots[0].supportsCalling`. Si está presente y se establece en `true` , Teams permite que el bot participe en llamadas y reuniones en línea.
* `bots[0].supportsVideo`. Si está presente y se establece en `true` , Teams sabe que el bot admite vídeo.

Si desea que el IDE valide correctamente el manifest.jsen el esquema para el bot de llamadas y reuniones para estos valores, puede cambiar el atributo de la `$schema` siguiente manera:

```json
"$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
```

La siguiente sección le permite crear un nuevo bot o agregar funcionalidades de llamada al bot existente.

## <a name="create-new-bot-or-add-calling-capabilities"></a>Crear nuevo bot o agregar funcionalidades de llamada

Para obtener información sobre la creación de bots, [vea create a bot for Teams](../how-to/create-a-bot-for-teams.md).

**Para crear un nuevo bot para Teams**

1. Use este vínculo para crear un nuevo bot, `https://dev.botframework.com/bots/new` . Como alternativa, si selecciona el botón Crear un **bot** en el portal de Bot Framework, cree el bot en Microsoft Azure, para el que debe tener una cuenta de Azure.
1. Agregue el canal de Teams.
1. Seleccione la **pestaña Llamar** en la página canal de Teams. Seleccione **Habilitar llamada** y, a continuación, actualice **Webhook (para llamar)** con la dirección URL HTTPS donde recibe notificaciones entrantes, por ejemplo `https://contoso.com/teamsapp/api/calling` . Para obtener más información, vea [configuring channels](/bot-framework/portal-configure-channels).

    ![Configurar la información del canal de Teams](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

En la siguiente sección se proporciona una lista de los permisos de aplicación admitidos para llamadas y reuniones en línea.

## <a name="add-graph-permissions"></a>Agregar permisos de Graph

Graph proporciona permisos granulares para controlar el acceso que las aplicaciones tienen a los recursos. Decides qué permisos para Graph solicitas tu aplicación. Las API de llamadas de Graph admiten permisos de aplicación, que usan las aplicaciones que se ejecutan sin que haya un usuario que haya iniciado sesión. Un administrador de inquilinos debe conceder el consentimiento a los permisos de la aplicación.

### <a name="application-permissions-for-calls"></a>Permisos de aplicación para llamadas

En la tabla siguiente se proporciona una lista de permisos de aplicación para llamadas:

|Permiso    |Cadena de presentación   |Descripción |Se requiere el consentimiento de administrador |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |Inicia llamadas salientes 1:1 desde la vista previa de la aplicación. |Permite a la aplicación realizar llamadas a un único usuario y transferir las llamadas a usuarios en el directorio de su organización, sin que el usuario haya iniciado sesión en la aplicación.|Sí|
| Calls.InitiateGroupCall.All |Iniciar llamadas de grupo salientes desde la vista previa de la aplicación. |Permite a la aplicación realizar llamadas a varios usuarios y agregar a participantes a las reuniones de su organización, sin que el usuario haya iniciado sesión en la aplicación.|Sí|
| Calls.JoinGroupCall.All |Unirse a llamadas de grupo y reuniones como una vista previa de la aplicación. |Permite a la aplicación unirse a llamadas de grupo y reuniones programadas de la organización, sin que el usuario haya iniciado sesión en la aplicación. La aplicación se une con los privilegios de un usuario de directorio a las reuniones de su inquilino.|Sí|
| Calls.JoinGroupCallasGuest.All |Unirse a llamadas de grupo y reuniones como una vista previa de invitado. |Permite a la aplicación unirse a llamadas de grupo y reuniones programadas de la organización de forma anónima, sin que el usuario haya iniciado sesión en la aplicación. La aplicación se une como invitado a reuniones en el espacio empresarial.|Sí|
| Calls.AccessMedia.All |Acceder a secuencias multimedia en una llamada como una vista previa de la aplicación. |Permite a la aplicación obtener acceso directo a los flujos de medios en una llamada, sin que el usuario haya iniciado sesión en la aplicación.|Sí|

> [!IMPORTANT]
> No puede usar la API de Acceso a medios para registrar o conservar contenido multimedia de llamadas o reuniones a las que la aplicación tiene acceso ni derivar datos de ese registro o grabación de contenido multimedia. Primero debe llamar a la [ `updateRecordingStatus` API para](/graph/api/call-updaterecordingstatus) indicar que la grabación ha comenzado y recibir una respuesta correcta de esa API. Si la aplicación comienza a grabar cualquier reunión o llamada, debe finalizar la grabación antes de llamar a la API para indicar `updateRecordingStatus` que la grabación ha finalizado.

### <a name="application-permissions-for-online-meetings"></a>Permisos de aplicación para reuniones en línea

En la tabla siguiente se proporciona una lista de permisos de aplicación para reuniones en línea:

|Permiso    |Cadena de presentación   |Descripción |Se requiere el consentimiento de administrador |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |Leer los detalles de la reunión en línea desde la vista previa de la aplicación|Permite que la aplicación lea los detalles de la reunión en línea en su organización, sin que un usuario haya iniciado sesión.|Sí|
| OnlineMeetings.ReadWrite.All |Leer y crear reuniones en línea desde la vista previa de la aplicación en nombre de un usuario|Permite que la aplicación cree reuniones en línea en su organización en nombre de un usuario, sin que un usuario haya iniciado sesión.|Sí|

### <a name="assign-permissions"></a>Asignar permisos

Debe configurar los permisos de aplicación para el bot por adelantado mediante [Azure Portal](https://aka.ms/aadapplist) si prefiere usar el extremo V1 de Azure Active [Directory (AAD).](/azure/active-directory/develop/azure-ad-endpoint-comparison)

### <a name="get-tenant-administrator-consent"></a>Obtener el consentimiento del administrador de inquilinos

Para las aplicaciones que usan el punto de conexión de AAD V1, un administrador de inquilinos puede dar su consentimiento a los permisos de la aplicación mediante [Azure Portal](https://portal.azure.com) cuando la aplicación está instalada en su organización. Como alternativa, puedes proporcionar una experiencia de registro en la aplicación a través de la cual los administradores pueden dar su consentimiento a los permisos configurados. Una vez que AAD registra el consentimiento de administrador, la aplicación puede solicitar tokens sin tener que volver a solicitar el consentimiento.

Puede confiar en un administrador para conceder los permisos que necesita la aplicación en [Azure Portal](https://portal.azure.com). Una mejor opción es proporcionar una experiencia de registro para los administradores mediante el punto de conexión de AAD `/adminconsent` V2. Para obtener más información, vea [instrucciones sobre cómo crear una dirección URL de consentimiento de administrador](https://developer.microsoft.com/graph/docs/concepts/auth_v2_service#3-get-administrator-consent).

> [!NOTE]
> Para crear la dirección URL de consentimiento de administrador del espacio empresarial, se requiere un URI de redireccionamiento configurado o una dirección URL de respuesta en el [portal de registro de](https://apps.dev.microsoft.com/) aplicaciones. Para agregar direcciones URL de respuesta para el bot, acceda al registro del bot, elija **Opciones avanzadas** Editar manifiesto  >  **de aplicación**. Agregue la dirección URL de redireccionamiento a la `replyUrls` colección.

> [!IMPORTANT]
> Cada vez que realice un cambio en los permisos de la aplicación, también debe repetir el proceso de consentimiento de administrador. Los cambios realizados en el portal de registro de aplicaciones no se reflejan hasta que el administrador del espacio empresarial haya proporcionado el consentimiento.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Notificaciones de llamadas entrantes](~/bots/calls-and-meetings/call-notifications.md)
