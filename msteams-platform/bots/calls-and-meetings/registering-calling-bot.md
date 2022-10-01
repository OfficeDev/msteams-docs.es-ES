---
title: Registro de llamadas y bots de reuniones para Microsoft teams
description: Obtenga información sobre cómo registrar un nuevo bot de llamadas de audio y vídeo para Microsoft Teams, crear un nuevo bot o agregar funcionalidad de llamadas, agregar permisos de grafos. Ejemplo para crear una llamada, unirse a una reunión y una llamada de transferencia.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 3fe8d0adde45242738b8023c5478c24769561d1c
ms.sourcegitcommit: 53818e55dfe0dbdf874d578a40982f7db444f89b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2022
ms.locfileid: "68319940"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>Registro de llamadas y bots de reuniones para Microsoft teams

Un bot que participe en llamadas de audio o vídeo y reuniones en línea se trata de un bot normal de Microsoft Teams con algunas características adicionales que se usan para registrar el bot:

* Hay una nueva versión del manifiesto de aplicación de Teams con dos configuraciones adicionales, `supportsCalling` y `supportsVideo`. Esta configuración se incluye en el esquema [Manifest para Microsoft Teams](../../resources/schema/manifest-schema.md).
* [Microsoft Graph permisos](./registering-calling-bot.md#add-graph-permissions) deben configurarse para el identificador de aplicación de Microsoft del bot.
* Los permisos de las API de llamadas y reuniones en línea de Graph requieren el consentimiento del administrador de inquilinos.

## <a name="new-manifest-settings"></a>Nueva configuración del manifiesto

Los bots de llamadas y reuniones en línea tienen las dos opciones adicionales siguientes en manifest.json que habilitan el audio o el vídeo para el bot en Teams.

* `bots[0].supportsCalling`. If present and set to `true`, Teams allows your bot to participate in calls and online meetings.
* `bots[0].supportsVideo`. If present and set to `true`, Teams knows that your bot supports video.

Si quiere que el IDE valide correctamente el esquema manifest.json de los bots de llamadas y reuniones para estos valores, puede cambiar el atributo `$schema` de la siguiente manera:

```json
"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
```

La siguiente sección le permite crear un nuevo bot o agregar funcionalidades de llamada al bot existente.

## <a name="create-new-bot-or-add-calling-capabilities"></a>Creación de un nuevo bot o adición de funcionalidades de llamada

Para obtener información sobre cómo crear bots, consulte [cree un bot para Teams](../how-to/create-a-bot-for-teams.md).

Para crear un nuevo bot para Teams:

1. Use this link to create a new bot, `https://dev.botframework.com/bots/new`. Alternately, if you select the **Create a bot** button in the Bot Framework portal, you create your bot in Microsoft Azure, for which you must have an Azure account.
1. En el canal de Teams:
1. Seleccione la pestaña **Llamada** en la página del canal de Teams. Seleccione **Permitir llamada**, y, a continuación, actualice **Webhook (para llamar)** con la dirección URL HTTPS donde recibirá las notificaciones entrantes, por ejemplo, `https://contoso.com/teamsapp/api/calling`. Para obtener más información, vea [configurar canales](/bot-framework/portal-configure-channels).

    ![Configurar la información del canal de Teams](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

En la sección siguiente se proporciona una lista de los permisos de aplicación admitidos para llamadas y reuniones en línea.

## <a name="add-graph-permissions"></a>Conceder permisos de Graph

Graph proporciona permisos granulares para controlar el acceso que las aplicaciones tienen a los recursos. Usted decide qué permisos de Graph solicita la aplicación. Las API de llamada de Graph admiten permisos de aplicación, que usan las aplicaciones que se ejecutan sin un usuario que ha iniciado sesión presente. Un administrador de inquilinos debe conceder consentimiento a los permisos de aplicación.

### <a name="application-permissions-for-calls"></a>Permisos de aplicación para llamadas

En la tabla siguiente se proporciona una lista de permisos de aplicación para las llamadas:

|Permiso    |Mostrar cadena   |Descripción |Se requiere el consentimiento del administrador |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |Iniciar llamadas salientes de 1:1 desde la aplicación versión preliminar |Permite a la aplicación realizar llamadas a un único usuario y transferir las llamadas a usuarios en el directorio de su organización, sin que el usuario haya iniciado sesión en la aplicación.|Sí|
| Calls.InitiateGroupCall.All |Inicie las llamadas salientes 1:1 y agrupar desde la versión preliminar de la aplicación. |Permite a la aplicación realizar llamadas salientes a un único usuario, varios usuarios, transferir llamadas y agregar participantes a reuniones de su organización, sin que un usuario haya iniciado sesión.|Sí|
| Calls.JoinGroupCall.All |Unirse a llamadas y reuniones de grupo como una aplicación versión preliminar |Permite a la aplicación unirse a llamadas de grupo y reuniones programadas de la organización, sin que el usuario haya iniciado sesión en la aplicación. La aplicación se combinará con los privilegios de un usuario del directorio a las reuniones en su espacio empresarial.|Sí|
| Calls.JoinGroupCallasGuest.All |Unirse a llamadas y reuniones de grupo como invitado versión preliminar |Permite a la aplicación unirse a llamadas de grupo y reuniones programadas de la organización de forma anónima, sin que el usuario haya iniciado sesión en la aplicación. La aplicación se unirá como invitado a las reuniones de su espacio empresarial.|Sí|
| Calls.AccessMedia.All |Accede a los flujos de medios en una llamada como aplicación versión preliminar |Permite a la aplicación obtener acceso directo a los flujos de medios en una llamada, sin que el usuario haya iniciado sesión en la aplicación.|Sí|

> [!IMPORTANT]
> No puede usar la API de acceso multimedia para grabar o conservar contenido multimedia de llamadas o reuniones a las que la aplicación tenga acceso o derive datos de ese registro o grabación de contenido multimedia. Primero debe llamar al [`updateRecordingStatus` API](/graph/api/call-updaterecordingstatus) para indicar que la grabación ha comenzado y recibir una respuesta correcta de esa API. Si la aplicación comienza a grabar cualquier reunión o llamada, debe finalizar la grabación antes de llamar a la API `updateRecordingStatus` para indicar que la grabación ha finalizado.

### <a name="application-permissions-for-online-meetings"></a>Permisos de aplicación para reuniones en línea

En la tabla siguiente se proporciona una lista de permisos de aplicación para reuniones en línea:

|Permiso    |Mostrar cadena   |Descripción |Se requiere el consentimiento del administrador |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |Leer detalles de la reunión en línea desde la aplicación versión preliminar|Permite a la aplicación leer los detalles de las reuniones en línea de la organización, sin que un usuario haya iniciado sesión.|Sí|
| OnlineMeetings.ReadWrite.All |Leer y crear reuniones en línea desde la aplicación versión preliminar en nombre de un usuario|Permite a la aplicación crear reuniones en línea dentro de la organización en nombre de un usuario, sin que un usuario haya iniciado sesión.|Sí|

### <a name="assign-permissions"></a>Asignar permisos

Debe configurar los permisos de aplicación para el bot de antemano mediante el [Microsoft Azure Portal](https://portal.azure.com) si prefiere usar el punto de conexión [Microsoft Azure Active Directory (Azure AD) V1](/azure/active-directory/develop/azure-ad-endpoint-comparison).

### <a name="get-tenant-administrator-consent"></a>Obtención del consentimiento del administrador de inquilinos

For apps using the Azure AD V1 endpoint, a tenant administrator can consent to the application permissions using the [Microsoft Azure portal](https://portal.azure.com) when your app is installed in their organization. Alternately, you can provide a sign-up experience in your app through which administrators can consent to the permissions you configured. Once administrator consent is recorded by Azure AD, your app can request tokens without having to request consent again.

You can rely on an administrator to grant the permissions your app needs at the [Microsoft Azure portal](https://portal.azure.com). A better option is to provide a sign-up experience for administrators by using the Azure AD V2 `/adminconsent` endpoint. For more information, see [instructions on constructing an Admin consent URL](/graph/auth-v2-service#3-get-administrator-consent).

> [!NOTE]
> Para construir la dirección URL de consentimiento del administrador del inquilino, se requiere un URI de redireccionamiento configurado o una dirección URL de respuesta en el [ portal de registro de aplicaciones](https://apps.dev.microsoft.com/). Para agregar direcciones URL de respuesta para el bot, acceda al registro del bot, elija **Opciones avanzadas** > **Edit Application Manifest**. Agregue la dirección URL de redireccionamiento a la colección `replyUrls`.

> [!IMPORTANT]
> Cada vez que realice un cambio en los permisos de la aplicación, también debe repetir el proceso de consentimiento del administrador. Los cambios realizados en el portal de registro de la aplicación no se reflejarán hasta que el administrador del espacio empresarial haya vuelto a aplicar el consentimiento.

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **C#** |
|---------------|----------|--------|
| Bots de llamadas y reuniones | La aplicación de ejemplo muestra cómo el bot puede crear una llamada, unirse a una reunión y transferirla. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |
| Eventos de reunión en tiempo real |La aplicación de ejemplo muestra cómo bot puede recibir eventos de reunión en tiempo real.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la guía [paso a paso](../../sbs-calling-and-meeting.yml) para configurar llamadas y reuniones en un bot.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Notificaciones de llamadas entrantes](~/bots/calls-and-meetings/call-notifications.md)

## <a name="see-also"></a>Vea también

* [Notificaciones de llamadas entrantes](~/bots/calls-and-meetings/call-notifications.md)
* [Desarrollar bots de llamadas y reuniones en línea en su PC local](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
* [Ver permisos de aplicación y conceder consentimiento del administrador](/MicrosoftTeams/app-permissions-admin-center).
* [Uso de la API de comunicaciones en Microsoft Graph](/graph/api/resources/communications-api-overview)
