---
title: Recibir todos los mensajes de canal con RSC
author: surbhigupta12
description: Recibir todos los mensajes de canal con permisos RSC
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 6b4c2add73c54aadd068c16171a0d340a0c79075
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111209"
---
# <a name="receive-all-channel-messages-with-rsc"></a>Recibir todos los mensajes de canal con RSC

El modelo de permisos de consentimiento específico del recurso (RSC), desarrollado originalmente para Graph API de Teams, se extiende a escenarios de bot.

Con RSC, ahora puede solicitar a los propietarios del equipo que den su consentimiento para que un bot reciba mensajes de usuario a través de los canales estándar de un equipo sin ser @mentioned. Esta funcionalidad se habilita especificando el `ChannelMessage.Read.Group` permiso en el manifiesto de una aplicación de Teams habilitada para RSC. Después de la configuración, los propietarios del equipo pueden conceder consentimiento durante el proceso de instalación de la aplicación.

Para obtener más información sobre cómo habilitar RSC para su aplicación, consulte [consentimiento específico del recurso en Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).

## <a name="enable-bots-to-receive-all-channel-messages"></a>Permitir que los bots reciban todos los mensajes del canal

El `ChannelMessage.Read.Group` permiso RSC se extiende a los bots. Con el consentimiento del usuario, este permiso permite que las aplicaciones de grafos obtengan todos los mensajes de una conversación y que los bots reciban todos los mensajes del canal sin ser @mentioned.

> [!NOTE]
>
> * Los servicios que necesitan acceso a todos los datos de mensajes de Teams deben usar las API de Graph que también proporcionan acceso a los datos archivados en canales y chats.
> * Los bots deben usar el `ChannelMessage.Read.Group` permiso RSC adecuadamente para crear y mejorar una experiencia que sea atractiva para los usuarios del equipo o no pasarán la aprobación de la tienda. La descripción de la aplicación debe incluir cómo usa el bot los datos que lee.
> * Los bots no pueden usar el permiso `ChannelMessage.Read.Group` RSC como una manera de extraer grandes cantidades de datos de clientes.

## <a name="update-app-manifest"></a>Actualizar el manifiesto de la aplicación

Para que el bot reciba todos los mensajes del canal, RSC debe configurarse en el manifiesto de la aplicación de Teams con el permiso de `ChannelMessage.Read.Group` especificado en la propiedad `webApplicationInfo`.

![Actualizar el manifiesto de la aplicación](~/bots/how-to/conversations/Media/appmanifest.png)


A continuación se muestra un ejemplo del objeto `webApplicationInfo` :

* **id**: Su identificador de la aplicación Microsoft Azure Active Directory (Azure AD). Puede ser el mismo que el identificador del bot.
* **recurso**: cualquier cadena. Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error.
* **applicationPermissions**: se deben especificar los permisos de RSC para su aplicación con `ChannelMessage.Read.Group`. Para obtener más información, vea [permisos específicos del recurso](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).

El código siguiente proporciona un ejemplo del manifiesto de la aplicación:

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team"></a>Transferir localmente en un equipo

Para transferir localmente en un equipo para probar si todos los mensajes de canal de un equipo con RSC se reciben sin ser @mentioned:

1. Seleccione o cree un equipo.
1. Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; en el panel izquierdo. Aparece el menú desplegable.
1. Seleccione **Administrar el equipo** en el menú desplegable. Aparecen los detalles.

   ![Administración de aplicaciones en el equipo](~/bots/how-to/conversations/Media/managingteam.png)

      :::image type="content" source="Media/managingteam.png" alt-text="equipo de administración"border="true":::

1. Seleccione **Aplicaciones**. Aparecen varias aplicaciones.
1. Seleccione **Cargar una aplicación personalizada** en la esquina inferior derecha.

      :::image type="content" source="Media/uploadingcustomapp.png" alt-text="carga de una aplicación personalizada":::
  
1. Seleccione el paquete de la aplicación en el cuadro de diálogo **Abrir**.
1. Seleccione **Abrir**.

      :::image type="content" source="Media/selectapppackage.png" alt-text="Seleccionar el paquete de la aplicación"lightbox="Media/selectapppackage.png"border="true":::

1. Seleccione **Agregar** en la ventana emergente de detalles de la aplicación para agregar el bot al equipo seleccionado.

      :::image type="content" source="Media/addingbot.png" alt-text="Agregar bot"lightbox="Media/addingbot.png"border="true":::

1. Seleccione un canal y escriba un mensaje en el canal del bot.

    El bot recibe el mensaje sin ser @mentioned.

      :::image type="content" source="Media/botreceivingmessage.png" alt-text="Bot recibiendo mensaje"lightbox="Media/botreceivingmessage.png"border="true":::

## <a name="code-snippets"></a>Fragmentos de código

El código siguiente proporciona un ejemplo de permisos de RSC:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text("Using RSC the bot can recieve messages across channels in team without being @mentioned."));
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
this.onMessage(async (context, next) => {
   await context.sendActivity(MessageFactory.text("Using RSC the bot can recieve messages across channles in team without being @mentioned."))
   await next();
});
```

---

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Mensajes de canal con permisos RSC| Aplicación de ejemplo de Microsoft Teams que muestra cómo un bot puede recibir todos los mensajes de canal con RSC sin ser @mentioned.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>Consulte también

* [Conversaciones de bot](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Consentimiento específico del recurso](/microsoftteams/resource-specific-consent)
* [Probar el consentimiento específico del recurso](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Cargar aplicación personalizada en Teams](~/concepts/deploy-and-publish/apps-upload.md)
