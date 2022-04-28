---
title: Prueba y depuración del bot
description: Describe cómo probar bots en Microsoft Teams
keywords: pruebas de bots de teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: df403343aab60ebd802b4da0e871649ded8b8a7e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103435"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Prueba y depuración del bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Al probar el bot, debe tener en cuenta los contextos en los que quiere que se ejecute el bot, así como cualquier funcionalidad que haya agregado al bot que requiera datos específicos de Microsoft Teams. Asegúrese de que el método que eligió para probar el bot se alinea con su funcionalidad.

## <a name="test-by-uploading-to-teams"></a>Pruebe mediante la carga en Teams

La manera más completa de probar el bot es crear un paquete de aplicación y cargarlo en Teams. Este es el único método para probar la funcionalidad completa disponible para el bot en todos los ámbitos.

Hay dos métodos para cargar la aplicación. Puede usar [App Studio](~/concepts/build-and-test/app-studio-overview.md) o puede [crear manualmente un paquete de aplicación](~/concepts/build-and-test/apps-package.md) y [cargar la aplicación](~/concepts/deploy-and-publish/apps-upload.md). Si necesita modificar el manifiesto y volver a cargar la aplicación, debe [eliminar el bot](#deleting-a-bot-from-teams) antes de cargar el paquete de aplicación modificado.

## <a name="debug-your-bot-locally"></a>Depuración local del bot

Si va a hospedar el bot localmente durante el desarrollo, deberá usar un servicio de tunelización como [ngrok](https://ngrok.com/) para probar el bot. Una vez que haya descargado e instalado ngrok, ejecute el siguiente comando para iniciar el servicio de tunelización. Es posible que tenga que agregar ngrok a la ruta de acceso.

```bash
ngrok http <port> -host-header=localhost:<port>
```

Use el punto de conexión https proporcionado por ngrok en el manifiesto de la aplicación. Si cierra la ventana de comandos y se reinicia, obtendrá una nueva dirección URL y deberá actualizar la dirección del punto de conexión del bot para usarla también.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Probar el bot sin cargarlo en Teams

En ocasiones, es necesario probar el bot sin instalarlo como una aplicación en Teams. Proporcionamos dos métodos para las pruebas. Probar el bot sin instalarlo como una aplicación puede ser útil para asegurarse de que el bot está disponible y responder, pero no le permitirá probar toda la amplitud de Microsoft Teams funcionalidad que puede haber agregado al bot. Si necesita probar el bot por completo, siga las instrucciones para [realizar pruebas mediante la carga](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Uso del bot Emulator

El Bot Framework Emulator es una aplicación de escritorio que permite a los desarrolladores de bots probar y depurar sus bots, ya sea de forma local o remota. Con el emulador, puede chatear con el bot e inspeccionar los mensajes que el bot envía y recibe. Esto puede ser útil para comprobar que el bot está disponible y responder, pero el emulador no le permitirá probar ninguna funcionalidad específica de Teams que haya agregado al bot, ni las respuestas del bot serán una representación visual precisa de cómo se representan en Teams. Si necesita probar cualquiera de estas cosas, no es mejor [cargar el bot](#test-by-uploading-to-teams).

Puede encontrar instrucciones completas sobre la Bot Framework Emulator [aquí](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Hable con el bot directamente por identificador.

>[!Important]
>La comunicación con el bot por identificador está pensada solo para fines de prueba.

También puede iniciar una conversación con el bot mediante su identificador. A continuación se proporcionan dos métodos para hacerlo. Cuando se ha agregado un bot a través de uno de estos métodos, no será direccionable en las conversaciones de canal y no podrá aprovechar otras funcionalidades de Microsoft Teams aplicación, como pestañas o extensiones de mensajes.

1. En la página [Bot Dashboard](https://dev.botframework.com/bots) del bot, en **Canales**, seleccione **Agregar a Microsoft Teams**. Microsoft Teams se iniciará con un chat personal con el bot.
2. Haga referencia directamente al identificador de aplicación del bot desde dentro de Microsoft Teams:
   * En la página [Bot Dashboard](https://dev.botframework.com/bots) del bot, en **Detalles**, copie el **identificador de aplicación de Microsoft** para el bot.
  
     ![Obtención del AppID para el bot](~/assets/images/bots_appid_botframework.png)
  
   * En Microsoft Teams, en el panel **Chat**, seleccione el icono **Agregar chat**. En **To:**, pegue el identificador de aplicación de Microsoft del bot.
  
     ![Carga del AppID para el bot](~/assets/images/bots_uploading.png)

     El identificador de la aplicación debe resolverse en el nombre del bot.

   * Seleccione el bot y envíe un mensaje para iniciar una conversación.
   * Como alternativa, puede pegar el identificador de aplicación del bot en el cuadro de búsqueda de la parte superior izquierda de Microsoft Teams. En la página de resultados de búsqueda, vaya a la pestaña Personas para ver el bot y empezar a chatear con él.

El bot recibirá el evento igual `conversationUpdate` que los bots agregados a un equipo, pero sin la información del equipo en el `channelData` objeto.

## <a name="blocking-a-bot-in-personal-chat"></a>Bloqueo de un bot en el chat personal

Tenga en cuenta que los usuarios pueden optar por impedir que el bot envíe mensajes de chat personales. Para alternar esto, haga clic con el botón derecho en el bot en el canal de chat y elija **Bloquear conversación de bot**. Esto significa que los bots seguirán enviando mensajes, pero el usuario no recibirá esos mensajes.

![Bloqueo de un bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Eliminación de un bot de un equipo

Los usuarios pueden eliminar el bot eligiendo el icono de papelera en la lista de bots en la vista de equipos. Tenga en cuenta que esto solo quita el bot del uso de ese equipo, ya que los usuarios individuales pueden interactuar en el contexto personal.

Los bots en el contexto personal no pueden ser deshabilitados o eliminados por un usuario, en lugar de quitar completamente el bot de Teams.

## <a name="disabling-a-bot-in-teams"></a>Deshabilitación de un bot en Teams

Para detener la recepción de mensajes del bot, vaya al panel de bots y edite el canal de Microsoft Teams. Desactive la opción **Habilitar en Microsoft Teams**. Esto impide que los usuarios interactúen con el bot, pero todavía se podrá detectar y los usuarios podrán agregarlo a los equipos.

## <a name="deleting-a-bot-from-teams"></a>Eliminación de un bot de Teams

Para quitar completamente el bot de Teams, vaya al panel de bots y edite el canal de Microsoft Teams. Elija el botón **Eliminar** en la parte inferior. Esto impide que los usuarios detecten, agreguen o interactúen con el bot. Tenga en cuenta que esto no quita el bot de las instancias de Teams de otros usuarios, aunque dejará de funcionar para ellos también.

## <a name="removing-your-bot-from-appsource"></a>Eliminación del bot de AppSource

Si desea quitar el bot de la aplicación de Teams en AppSource (anteriormente Office Store), debe quitar el bot del manifiesto de la aplicación y volver a enviar la aplicación para su validación. Para obtener más información, consulte [Publicación de la aplicación Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md).
