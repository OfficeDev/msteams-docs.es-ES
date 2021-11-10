---
title: Probar y depurar el bot localmente
author: surbhigupta
description: Obtenga información sobre cómo probar y depurar el bot localmente con un IDE en un entorno de Teams mediante la instalación local, fuera de Teams mediante el emulador bot y hablando directamente con el bot.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 9ac6e2f7bf173e68e111b0d792ec89ba266c188f
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888233"
---
# <a name="test-and-debug-your-bot-locally"></a>Probar y depurar el bot localmente

Al probar el bot, debes tener en cuenta los contextos en los que quieres que se ejecute el bot y cualquier funcionalidad que haya agregado al bot que requiera datos específicos para Microsoft Teams. Asegúrese de que el método que elija para probar el bot se alinee con su funcionalidad.

## <a name="test-by-uploading-to-teams"></a>Pruebe cargando en Teams

La forma más completa de probar el bot es crear un paquete de aplicación y cargarlo en Teams. Este es el único método para probar la funcionalidad completa disponible para el bot, en todos los ámbitos.

Hay dos métodos para cargar la aplicación:
* Use [App Studio](~/concepts/build-and-test/app-studio-overview.md).
* [Crea un paquete de aplicación](~/concepts/build-and-test/apps-package.md) manualmente y, a continuación, carga la [aplicación](~/concepts/deploy-and-publish/apps-upload.md).

> [!NOTE]
> Si necesitas modificar el manifiesto y volver a cargar la aplicación, debes eliminar el [bot](#delete-a-bot-from-teams) antes de cargar el paquete de la aplicación modificado.

## <a name="debug-your-bot-locally"></a>Depurar el bot localmente

Si hospeda el bot localmente durante el desarrollo, debe usar un servicio de túnel como [ngrok](https://ngrok.com/) para probar el bot. Después de descargar e instalar ngrok, agregue a la ruta de acceso y ejecute el `ngrok` siguiente comando para iniciar el servicio de túnel:

```bash
ngrok http <port> -host-header=localhost:<port>
```

Usa el punto de conexión https proporcionado por ngrok en el manifiesto de la aplicación. 

> [!NOTE]
> Si cierra la ventana de comandos y se reinicia, se genera una nueva dirección URL y necesita actualizar la dirección del extremo del bot para usarla.

## <a name="test-your-bot-without-uploading-to-teams"></a>Pruebe el bot sin cargarlo en Teams

En ocasiones, es posible que sea necesario probar el bot sin instalarlo como una aplicación en Teams. Proporcionamos dos métodos para probar el bot. Probar el bot sin instalarlo como una aplicación puede ser útil para garantizar que el bot esté disponible y responda, pero no te permitirá probar toda la amplitud de la funcionalidad de Microsoft Teams que puedas haber agregado al bot. Si necesita probar completamente el bot, consulte [testing by uploading](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Use el bot Emulator

El Bot Framework Emulator es una aplicación de escritorio que permite a los desarrolladores de bots probar y depurar sus bots de forma local o remota. El emulador te ayuda a chatear con el bot e inspeccionar los mensajes que el bot envía y recibe. Esto puede ser útil para comprobar que el bot está disponible y responde. Sin embargo, el emulador no permite probar ninguna funcionalidad específica de Teams que haya agregado al bot, ni las respuestas del bot son una representación visual precisa de cómo se representan en Teams. Si necesita probar cualquiera de esos aspectos, es mejor [cargar el bot](#test-by-uploading-to-teams).

Para obtener más información, [vea instrucciones completas en el Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Hablar con el bot directamente por id.

> [!Important]
> La conversación con el bot por identificador está diseñada únicamente para fines de prueba básicos. Cualquier Teams funcionalidad específica que haya agregado al bot no funcionará.

También puedes iniciar una conversación con el bot mediante su identificador. Cuando un bot se ha agregado a través de uno de estos métodos, no es direccionable en conversaciones de canal y no puedes aprovechar otras funcionalidades de la aplicación Microsoft Teams como pestañas o extensiones de mensajería. Puede iniciar una conversación de una de las siguientes maneras:

* En la [página Panel de bots](https://dev.botframework.com/bots) del bot, en **Canales,** seleccione Agregar **a Microsoft Teams**. Microsoft Teams inicia un chat personal con el bot.

* Haga referencia directamente al identificador de aplicación del bot desde dentro Microsoft Teams:
   1. En la [página Panel de bots](https://dev.botframework.com/bots) del bot, en **Detalles,** copie el identificador de **aplicación de Microsoft** para el bot.
  
      ![Obtener el AppID para el bot](~/assets/images/bots_appid_botframework.png)
  
   2. Abra Microsoft Teams, en el **panel Chat,** seleccione el **icono Agregar chat.** En **Para:**, pegue el identificador de la aplicación de Microsoft del bot.
  
      ![Cargar bots](~/assets/images/bots_uploading.png)

      El identificador de la aplicación debe resolverse en el nombre del bot.

   3. Seleccione el bot y envíe un mensaje para iniciar una conversación.
      Como alternativa, puedes pegar el identificador de la aplicación del bot en el cuadro de búsqueda de la parte superior izquierda de Microsoft Teams. En la página de resultados de búsqueda, vaya a la **pestaña** Personas para ver el bot y empezar a chatear con él.

El bot recibe el `conversationUpdate` evento al agregar los bots a un equipo, sin la información del equipo en el `channelData` objeto.

## <a name="block-a-bot-in-personal-chat"></a>Bloquear un bot en el chat personal

Los usuarios pueden elegir bloquear el bot para no enviar mensajes de chat personales. Pueden alternar esto haciendo clic con el botón secundario en el bot en el canal de chat y eligiendo **Bloquear conversación de bot**. Esto significa que los bots siguen mandando mensajes, pero el usuario no recibe los mensajes.

![Bloqueo de un bot](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>Quitar un bot de un equipo

Los usuarios pueden eliminar el bot eligiendo el icono de papelera en la lista de bots en la vista de su equipo. Esto solo quita el bot del uso de ese equipo, los usuarios individuales aún pueden interactuar en contexto personal. Los usuarios no pueden deshabilitar ni quitar bots en contexto personal.

## <a name="disable-a-bot-in-teams"></a>Deshabilitar un bot en Teams

Para impedir que el bot reciba mensajes, vaya al **Panel de bots** y edite el Microsoft Teams canal. Desactive la **opción Habilitar en Microsoft Teams.** Esto impide que los usuarios interactúen con el bot, sin embargo, seguirá siendo detectable y los usuarios podrán agregarlo a Teams.

## <a name="delete-a-bot-from-teams"></a>Eliminar un bot de Teams

Para quitar el bot completamente de Teams, vaya al **Panel de bots** y edite el Microsoft Teams. Elija el **botón** Eliminar en la parte inferior. Esto evita que los usuarios detecten, agreguen e interactúen con el bot. Esto no quita el bot de las instancias de Teams de otro usuario, pero también deja de funcionar para ellas.

## <a name="see-also"></a>Consulte también

* [Depurar el bot con el middleware de inspección](/azure/bot-service/bot-service-debug-inspection-middleware)
* [Depurar el bot de llamadas y reuniones de forma local](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
