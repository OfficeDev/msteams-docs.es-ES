---
title: Recibir todos los mensajes de canal con RSC
author: surbhigupta12
description: Recibir todos los mensajes de canal con permisos de RSC
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 6c509475a94d7f161dd6fb26c46ecb669c4059a1
ms.sourcegitcommit: f77750f2e60f63d1e2f66a96c169119683c66950
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2021
ms.locfileid: "60960232"
---
# <a name="receive-all-channel-messages-with-rsc"></a>Recibir todos los mensajes de canal con RSC

El modelo de permisos de consentimiento específico de recursos (RSC), desarrollado originalmente para Teams Graph API, se extiende a escenarios de bots.

Con RSC, ahora puedes solicitar a los propietarios del equipo que consienten que un bot reciba mensajes de usuario en los canales estándar de un equipo sin que se @mentioned. Esta funcionalidad se habilita especificando el permiso en el `ChannelMessage.Read.Group` manifiesto de una aplicación Teams RSC habilitada. Después de la configuración, los propietarios del equipo pueden conceder su consentimiento durante el proceso de instalación de la aplicación.

Para obtener más información acerca de cómo habilitar RSC para tu aplicación, consulta el consentimiento específico de los [recursos en Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).

## <a name="enable-bots-to-receive-all-channel-messages"></a>Habilitar bots para recibir todos los mensajes de canal

El `ChannelMessage.Read.Group` permiso RSC se extiende a los bots. Con el consentimiento del usuario, este permiso permite que las aplicaciones de gráficos obtengan todos los mensajes de una conversación y que los bots reciban todos los mensajes de canal sin que se @mentioned.

> [!NOTE]
> * Los servicios que necesitan acceso a todos los Teams de mensajes deben usar las API de Graph que también proporcionan acceso a los datos archivados en canales y chats.
> * Los bots deben usar el permiso RSC adecuadamente para crear y mejorar la experiencia atractiva para los usuarios del equipo o no aprobarán `ChannelMessage.Read.Group` la aprobación de la tienda. La descripción de la aplicación debe incluir cómo el bot usa los datos que lee.
> * Los bots no pueden usar el permiso RSC como una forma de extraer `ChannelMessage.Read.Group` grandes cantidades de datos de clientes. 

## <a name="update-app-manifest"></a>Actualizar manifiesto de la aplicación

Para que el bot reciba todos los mensajes de canal, RSC debe configurarse en el manifiesto Teams aplicación con el permiso `ChannelMessage.Read.Group` especificado en la `webApplicationInfo` propiedad.
![Actualizar manifiesto de la aplicación](~/bots/how-to/conversations/Media/appmanifest.png)

A continuación se muestra un ejemplo del `webApplicationInfo` objeto:

* **id:** El identificador Azure Active Directory aplicación (AAD). Puede ser el mismo que el identificador del bot.
* **resource**: Any string. Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar la respuesta de error.
* **applicationPermissions:** se deben especificar los permisos de RSC para `ChannelMessage.Read.Group` la aplicación con. Para obtener más información, [consulte resource-specific permissions](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).

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

## <a name="sideload-in-a-team"></a>Instalación local en un equipo

Para realizar la instalación local en un equipo para probar, si todos los mensajes de canal de un equipo con RSC se reciben sin que se @mentioned:

1. Seleccione o cree un equipo.
1. Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; en el panel izquierdo. Aparece el menú desplegable.
1. Seleccione **Administrar equipo** en el menú desplegable. Aparecen los detalles.

   ![Administración de aplicaciones en equipo](~/bots/how-to/conversations/Media/managingteam.png)

1. Seleccione **Aplicaciones**. Aparecen varias aplicaciones.
1. Selecciona **Upload una aplicación personalizada** en la esquina inferior derecha.

    ![Cargar una aplicación personalizada](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. Selecciona el paquete de la aplicación en el **cuadro de diálogo** Abrir.
1. Seleccione **Abrir**.

    ![Selección del paquete de la aplicación](~/bots/how-to/conversations/Media/selectapppackage.png)

1. Selecciona **Agregar** en la ventana emergente detalles de la aplicación para agregar el bot al equipo seleccionado.

    ![Agregar el bot](~/bots/how-to/conversations/Media/addingbot.png)

1. Seleccione un canal e introduzca un mensaje en el canal del bot.

    El bot recibe el mensaje sin que se @mentioned.

    ![Bot recibe mensaje](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C # |Node.js|
|-------------|-------------|------|----|
|Mensajes de canal con permisos RSC| Microsoft Teams aplicación de ejemplo que muestra cómo un bot puede recibir todos los mensajes de canal con RSC sin que se @mentioned.|  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) |    [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>Consulte también

* [Conversaciones de bot](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Consentimiento específico del recurso](/microsoftteams/resource-specific-consent)
* [Probar el consentimiento específico de los recursos](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Upload aplicación personalizada en Teams](~/concepts/deploy-and-publish/apps-upload.md)
