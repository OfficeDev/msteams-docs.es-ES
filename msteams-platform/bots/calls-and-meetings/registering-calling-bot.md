---
title: Registro de un bot de llamada y reunión para Microsoft Teams
description: Obtenga información sobre cómo registrar un nuevo bot de llamada de audio y vídeo para Microsoft Teams
keywords: llamar a medios de audio y vídeo audio de bot
ms.openlocfilehash: 9a246c9b1a5aae230881b468afef6c205d5bdecf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676123"
---
# <a name="registering-a-calling-bot-for-microsoft-teams"></a>Registro de un bot de llamada para Microsoft Teams

Un bot que participa en llamadas de audio y vídeo y en reuniones en línea es un bot de Microsoft Teams ordinario con algunas características adicionales:

* Hay una nueva versión del manifiesto de la aplicación de Microsoft Teams con dos `supportsCalling` opciones `supportsVideo`de configuración adicionales y. Esta configuración se incluye en la versión de [vista previa para desarrolladores](../../resources/dev-preview/developer-preview-intro.md) del manifiesto de la aplicación Microsoft Teams.
* [Los permisos de Microsoft Graph](./registering-calling-bot.md#add-microsoft-graph-permissions) deben estar configurados para el identificador de aplicación de Microsoft de bot.
* Los permisos llamadas de Microsoft Graph y las API de reuniones en línea requieren el consentimiento del administrador de inquilinos.

Hablemos sobre lo anterior con más detalle.

## <a name="new-manifest-settings"></a>Nueva configuración del manifiesto

Los bots de llamadas y reuniones en línea tienen dos opciones de configuración adicionales en el manifiesto. JSON que habilitan el audio y vídeo para el bot en Teams.

* `bots[0].supportsCalling`. Si está presente y establecido `true`en, Microsoft Teams permitirá que el bot participe en las llamadas y las reuniones en línea.
* `bots[0].supportsVideo`. Si está presente y establecido `true`en, Teams sabe que su bot admite vídeo.

Si desea que el IDE valide correctamente el esquema manifest. JSON para el bot de llamadas y reuniones para estos valores, puede cambiar el atributo `$schema` de la siguiente manera:

```json
"$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
```

## <a name="creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot"></a>Creación de un nuevo bot o adición de capacidades de llamada a un bot existente

La creación de un nuevo bot se describe con más detalle en el tema [crear un bot para Microsoft Teams](../how-to/create-a-bot-for-teams.md) , pero repetiremos parte de él:

1. Use este vínculo para crear un nuevo bot: `https://dev.botframework.com/bots/new`. Si, en su lugar, selecciona el botón *crear un bot* en el portal de la plataforma de bot, creará su bot en Microsoft Azure, en el que necesitará una cuenta de Azure.
1. Agregue el canal de Microsoft Teams. Haga clic en la pestaña "llamada" en la página de canal de Microsoft Teams y seleccione **Habilitar llamada**y, a continuación, actualizar **webhook (para llamar)** con la dirección URL https donde recibirá`https://contoso.com/teamsapp/api/calling`las notificaciones entrantes; por ejemplo,. Consulte [Configuring Channels](/bot-framework/portal-configure-channels) para obtener más información sobre cómo configurar los canales.
  ![Configurar información de canal de Microsoft Teams](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

## <a name="add-microsoft-graph-permissions"></a>Agregar permisos de Microsoft Graph

Microsoft Graph expone permisos granulares que controlan el acceso de las aplicaciones a los recursos. Como desarrollador, usted decide qué permisos de Microsoft Graph solicita la aplicación.  Las API de llamada de Microsoft Graph admiten _permisos de aplicación_, que son usados por aplicaciones que se ejecutan sin la presencia de un usuario que ha iniciado sesión.  Un administrador de inquilinos debe conceder consentimiento a los permisos de la aplicación. A continuación se muestra una lista de los permisos:

### <a name="application-permissions-calls"></a>Permisos de aplicación: llamadas

|Permiso    |Cadena para mostrar   |Descripción |Se requiere el consentimiento del administrador |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
|_Calls.Initiate.All_|Iniciar llamadas salientes de 1:1 desde la aplicación (versión preliminar)|Permite a la aplicación realizar llamadas a un único usuario y transferir las llamadas a usuarios en el directorio de su organización, sin que el usuario haya iniciado sesión en la aplicación.|Sí|
|_Calls.InitiateGroupCall.All_|Iniciar llamadas de grupo salientes desde la aplicación (versión preliminar)|Permite a la aplicación realizar llamadas a varios usuarios y agregar a participantes a las reuniones de su organización, sin que el usuario haya iniciado sesión en la aplicación.|Sí|
|_Calls.JoinGroupCall.All_|Unirse a llamadas y reuniones de grupo como una aplicación (versión preliminar)|Permite a la aplicación unirse a llamadas de grupo y reuniones programadas de la organización, sin que el usuario haya iniciado sesión en la aplicación. La aplicación se combinará con los privilegios de un usuario del directorio a las reuniones en su espacio empresarial.|Sí|
|_Calls.JoinGroupCallasGuest.All_|Unirse a llamadas y reuniones de grupo como invitado (versión preliminar)|Permite a la aplicación unirse a llamadas de grupo y reuniones programadas de la organización de forma anónima, sin que el usuario haya iniciado sesión en la aplicación. La aplicación se unirá como invitado a las reuniones de su espacio empresarial.|Sí|
|_Calls. AccessMedia. All_ <sup> _vea más adelante_</sup>|Accede a los flujos de medios en una llamada como aplicación (versión preliminar)|Permite a la aplicación obtener acceso directo a los flujos de medios en una llamada, sin que el usuario haya iniciado sesión en la aplicación.|Sí|

> [!IMPORTANT]
> **No puede** usar la API Microsoft. Graph. calls. media para grabar o conservar el contenido multimedia de las llamadas o reuniones a las que tiene acceso el bot.

### <a name="application-permissions-online-meetings"></a>Permisos de aplicación: reuniones en línea

|Permiso    |Cadena para mostrar   |Descripción |Se requiere el consentimiento del administrador |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
|_OnlineMeetings.Read.All_|Leer detalles de la reunión en línea desde la aplicación (versión preliminar)|Permite a la aplicación leer los detalles de las reuniones en línea de la organización, sin que un usuario haya iniciado sesión.|Sí|
|_OnlineMeetings.ReadWrite.All_|Leer y crear reuniones en línea desde la aplicación (versión preliminar) en nombre de un usuario|Permite a la aplicación crear reuniones en línea dentro de la organización en nombre de un usuario, sin que un usuario haya iniciado sesión.|Sí|

### <a name="assigning-permissions"></a>Asignación de permisos

Debe configurar los permisos de la aplicación para su bot de antemano. Se recomienda usar el [portal de registro de aplicaciones de Microsoft](https://apps.dev.microsoft.com/) , tal y como se describe [aquí](/graph/docs/concepts/auth_register_app_v2) porque ahí es donde se configuró el bot; sin embargo, puede seguir usando [Azure portal](https://aka.ms/aadapplist) si prefiere usar el [punto de conexión de Azure ad v1](/azure/active-directory/develop/azure-ad-endpoint-comparison).

### <a name="getting-tenant-administrator-consent"></a>Obtener el consentimiento del administrador de inquilinos

Para las aplicaciones que usan el punto de conexión de Azure AD v1, un administrador de inquilinos puede dar su consentimiento a los permisos de la aplicación mediante el [portal de Azure](https://portal.azure.com) cuando la aplicación está instalada en la organización, o puede proporcionar una experiencia de suscripción en su aplicación a través de la cual los administradores pueden dar su consentimiento a los permisos configurados. Una vez que Azure AD registra el consentimiento del administrador, la aplicación puede solicitar tokens sin tener que volver a solicitar el consentimiento.

Puede confiar en un administrador para conceder los permisos que necesita la aplicación en [Azure portal](https://portal.azure.com); pero, a menudo, una mejor opción es proporcionar una experiencia de suscripción a los administradores mediante el punto de conexión de `/adminconsent` Azure ad V2.  Para obtener más información, consulte las [instrucciones sobre cómo crear una dirección URL de consentimiento de administrador](https://developer.microsoft.com/graph/docs/concepts/auth_v2_service#3-get-administrator-consent) .

> [!NOTE]
> La construcción de la dirección URL de consentimiento del administrador del espacio empresarial requiere una URL de respuesta/URI de redireccionamiento configurada en el [portal de registro](https://apps.dev.microsoft.com/)de la aplicación. Para agregar direcciones URL de respuesta para el bot, obtenga acceso al registro de los robots, elija Opciones avanzadas: > editar manifiesto de la aplicación.  Agregue la dirección URL de redireccionamiento a la `replyUrls` colección.

> [!IMPORTANT]
> Siempre que realice un cambio en los permisos de la aplicación, también debe repetir el proceso de consentimiento del administrador. Los cambios realizados en el portal de registro de la aplicación no se reflejarán hasta que el administrador del inquilino haya vuelto a aplicar el consentimiento.
