---
title: Prueba y depuración del bot localmente
author: surbhigupta
description: Obtenga información sobre cómo probar y depurar el bot localmente con un IDE dentro de Teams entorno a través de la instalación local, fuera de Teams mediante bot emulator y hablando directamente con el bot.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a673f1cd260c9b53de477cdd5084bd521c79bd41
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103989"
---
# <a name="test-and-debug-your-bot-locally"></a>Prueba y depuración del bot localmente

Al probar el bot, debe tener en cuenta tanto los contextos en los que desea que se ejecute el bot como cualquier funcionalidad que haya agregado al bot que requiera datos específicos de Microsoft Teams. Asegúrese de que el método que elija para probar el bot se alinea con su funcionalidad.

## <a name="test-by-uploading-to-teams"></a>Pruebe mediante la carga en Teams

La manera más completa de probar el bot es crear un paquete de aplicación y cargarlo en Teams. Este es el único método para probar la funcionalidad completa disponible para el bot en todos los ámbitos.

Hay dos métodos para cargar la aplicación:

* Use [App Studio](~/concepts/build-and-test/app-studio-overview.md).
* [Cree manualmente un paquete de aplicación](~/concepts/build-and-test/apps-package.md) y, a continuación, [cargue la aplicación](~/concepts/deploy-and-publish/apps-upload.md).

> [!NOTE]
> Para modificar el manifiesto y volver a cargar la aplicación, [elimine el bot](#delete-a-bot-from-teams) antes de cargar el paquete de aplicación modificado.
> Para probar el bot, habilite la instalación local en Teams. Consulte [Habilitación de la instalación local](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

## <a name="debug-your-bot-locally"></a>Depuración local del bot

Si hospeda el bot localmente durante el desarrollo, debe usar un servicio de tunelización como [ngrok](https://ngrok.com/) para probar el bot. Después de descargar e instalar ngrok, agregue `ngrok` a la ruta de acceso y ejecute el siguiente comando para iniciar el servicio de tunelización:

```bash
ngrok http <port> -host-header=localhost:<port>
```

Use el punto de conexión https proporcionado por ngrok en el manifiesto de la aplicación.

> [!NOTE]
> Si cierra la ventana de comandos y se reinicia, se genera una nueva dirección URL y debe actualizar la dirección del punto de conexión del bot para usarla.

## <a name="test-your-bot-without-uploading-to-teams"></a>Pruebe el bot sin cargarlo en Teams

En ocasiones, es posible que sea necesario probar el bot sin instalarlo como una aplicación en Teams. Proporcionamos dos métodos para probar el bot. Probar el bot sin instalarlo como una aplicación puede ser útil para asegurarse de que el bot está disponible y responder, pero no le permitirá probar toda la amplitud de Microsoft Teams funcionalidad que puede haber agregado al bot. Si necesita probar completamente el bot, consulte [pruebas mediante la carga](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Uso del bot Emulator

El Bot Framework Emulator es una aplicación de escritorio que permite a los desarrolladores de bots probar y depurar sus bots de forma local o remota. El emulador le ayuda a chatear con el bot e inspeccionar los mensajes que el bot envía y recibe. Esto puede ser útil para comprobar que el bot está disponible y responder. Sin embargo, el emulador no permite probar ninguna funcionalidad específica de Teams que haya agregado al bot, ni las respuestas del bot son una representación visual precisa de cómo se representan en Teams. Si necesita probar cualquiera de esas cosas, es mejor [cargar el bot](#test-by-uploading-to-teams).

Para obtener más información, consulte [instrucciones completas sobre el Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Hable con el bot directamente por identificador.

> [!Important]
> La comunicación con el bot por identificador está pensada solo para fines de pruebas básicas. Cualquier funcionalidad específica de Teams que haya agregado al bot no funcionará.

También puede iniciar una conversación con el bot mediante su identificador. Cuando se ha agregado un bot a través de uno de estos métodos, no es direccionable en las conversaciones de canal y no se pueden aprovechar otras funcionalidades de Microsoft Teams aplicación, como pestañas o extensiones de mensajes. Puede iniciar una conversación de una de las siguientes maneras:

* En la página [Bot Dashboard](https://dev.botframework.com/bots) del bot, en **Canales**, seleccione **Agregar a Microsoft Teams**. Microsoft Teams inicia un chat personal con el bot.

* Haga referencia directamente al identificador de aplicación del bot desde dentro de Microsoft Teams:
   1. En la página [Bot Dashboard](https://dev.botframework.com/bots) del bot, en **Detalles**, copie el **identificador de aplicación de Microsoft** para el bot.
  
      ![Obtención del AppID para el bot](~/assets/images/bots_appid_botframework.png)
  
   2. Abra Microsoft Teams, en el panel **Chat**, seleccione el icono **Agregar chat**. En **To:**, pegue el identificador de aplicación de Microsoft del bot.
  
      ![Carga de bots](~/assets/images/bots_uploading.png)

      El identificador de la aplicación debe resolverse en el nombre del bot.

   3. Seleccione el bot y envíe un mensaje para iniciar una conversación.
      Como alternativa, puede pegar el identificador de aplicación del bot en el cuadro de búsqueda de la parte superior izquierda de Microsoft Teams. En la página de resultados de búsqueda, vaya a la pestaña **Personas** para ver el bot y empezar a chatear con él.

> [!Note]
> Para que Microsoft Teams consulte el identificador de aplicación del bot, habilite [la instalación local de aplicaciones](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

El bot recibe el `conversationUpdate` evento a medida que agrega los bots a un equipo, sin la información del equipo en el `channelData` objeto .

## <a name="block-a-bot-in-personal-chat"></a>Bloquear un bot en el chat personal

Los usuarios pueden optar por impedir que el bot envíe mensajes de chat personales. Para alternar esto, haga clic con el botón derecho en el bot en el canal de chat y elija **Bloquear conversación de bot**. Esto significa que los bots siguen enviando mensajes; sin embargo, el usuario no recibe los mensajes.

![Bloqueo de un bot](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>Eliminación de un bot de un equipo

Los usuarios pueden eliminar el bot eligiendo el icono de papelera en la lista de bots en la vista de su equipo. Esto solo quita el bot del uso de ese equipo; los usuarios individuales todavía pueden interactuar en el contexto personal. Los usuarios no pueden deshabilitar ni quitar bots en el contexto personal.

## <a name="disable-a-bot-in-teams"></a>Deshabilitación de un bot en Teams

Para evitar que el bot reciba mensajes, vaya al **panel del bot** y edite el canal de Microsoft Teams. Desactive la opción **Habilitar en Microsoft Teams**. Esto impide que los usuarios interactúen con el bot; sin embargo, seguirá siendo reconocible y los usuarios podrán agregarlo a Teams.

## <a name="delete-a-bot-from-teams"></a>Eliminación de un bot de Teams

Para quitar completamente el bot de Teams, vaya al **panel de bots** y edite el canal de Microsoft Teams. Elija el botón **Eliminar** en la parte inferior. Esto impide que los usuarios detecten, agreguen e interactúen con el bot. Esto no quita el bot de las instancias de Teams de otro usuario; sin embargo, también deja de funcionar para ellos.

## <a name="see-also"></a>Vea también

* [Depurar el bot con el middleware de inspección](/azure/bot-service/bot-service-debug-inspection-middleware)
* [Depurar el bot de llamadas y reuniones de forma local](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
