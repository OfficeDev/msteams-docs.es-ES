---
title: Prueba y depuración del bot de manera local
author: surbhigupta
description: Obtenga información sobre cómo probar y depurar el bot localmente con un IDE en el entorno de Teams a través de una instalación de prueba, fuera de Teams mediante un emulador del bot o hablando directamente con el bot.
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 4584cc7489c931f5f02ddbb1f5dd6be529924644
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111839"
---
# <a name="test-and-debug-your-bot-locally"></a>Prueba y depuración del bot de manera local

Al probar el bot, debe tener en cuenta tanto los contextos en los que quiere que el bot ejecute como cualquier funcionalidad que haya agregado al bot que requiera datos específicos de Microsoft Teams. Asegúrese de que el método que elija para probar el bot se ajusta a su funcionalidad.

## <a name="test-by-uploading-to-teams"></a>Hacer la prueba mediante la carga en Teams

La manera más completa de probar el bot es crear un paquete de aplicación y cargarlo en Teams. Este es el único método para probar todas las funcionalidades disponibles para el bot, en todos los ámbitos.

Hay dos métodos para cargar la aplicación:

* Use [App Studio](~/concepts/build-and-test/app-studio-overview.md).
* [Cree un paquete de aplicación](~/concepts/build-and-test/apps-package.md) manualmente y, a continuación, [cargue la aplicación](~/concepts/deploy-and-publish/apps-upload.md).

> [!NOTE]
> Para modificar el manifiesto y volver a cargar la aplicación, [elimine el bot](#delete-a-bot-from-teams) antes de cargar el paquete de aplicación modificado.
> Para probar el bot, habilite la instalación de prueba en Teams. Consulte [Habilitar la instalación prueba](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

## <a name="debug-your-bot-locally"></a>Depuración del bot localmente

Si hospeda el bot localmente durante su desarrollo, debe usar un servicio de tunelización como [ngrok](https://ngrok.com/) para probar el bot. Después de descargar e instalar ngrok, agregue `ngrok` a la ruta de acceso y ejecute el siguiente comando para iniciar el servicio de tunelización:

```bash
ngrok http <port> -host-header=localhost:<port>
```

Use el punto de conexión https proporcionado por ngrok en el manifiesto de la aplicación.

> [!NOTE]
> Si cierra la ventana de comandos y la reinicia, se generará una nueva dirección URL, por lo que debe actualizar la dirección del punto de conexión del bot para usarla.

## <a name="test-your-bot-without-uploading-to-teams"></a>Probar el bot sin cargarlo en Teams

En ocasiones, puede ser necesario probar el bot sin instalarlo como una aplicación en Teams. Proporcionamos dos métodos para probar el bot. Probar el bot sin instalarlo como una aplicación puede ser útil para asegurarse de que el bot está disponible y responde, pero no le servirá para probar todas las funcionalidades de Microsoft Teams que puede haber agregado al bot. Si necesita probar el bot al completo, consulte [hacer la prueba cargándolo](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Usar Bot Emulator

Bot Framework Emulator es una aplicación de escritorio que permite a los desarrolladores de bots probar y depurar sus bots de forma local o remota. El emulador le ayuda a chatear con el bot y consultar los mensajes que el bot envía y recibe. Esto puede ser útil para comprobar que el bot está disponible y operativo. Sin embargo, el emulador no le servirá para probar ninguna funcionalidad específica de Teams que haya agregado al bot, ni para probar si las respuestas del bot son una representación visual precisa de cómo se representan en Teams. Si necesita probar cualquiera de esas cosas, es recomendable [cargar el bot](#test-by-uploading-to-teams).

Para obtener más información, consulte [instrucciones completas de Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Hable con el bot directamente por el identificador

> [!Important]
> Hablar con el bot por identificador está pensado solo para fines de prueba básicos. Cualquier funcionalidad específica de Teams que haya agregado al bot no funcionará.

También puede iniciar una conversación con el bot mediante su identificador. Cuando se ha agregado un bot a través de uno de estos métodos, no es posible dirigirse a este en las conversaciones de canal y tampoco puede aprovechar otras funcionalidades de la aplicación de Microsoft Teams, como pestañas o extensiones de mensaje. Puede iniciar una conversación de una de las siguientes maneras:

* En la página [Panel del bot](https://dev.botframework.com/bots), en **Canales**, seleccione **Agregar a Microsoft Teams**. Microsoft Teams inicia un chat personal con su bot.

* Utilice directamente el identificador de la aplicación del bot en Microsoft Teams:
   1. En la página [Panel del bot](https://dev.botframework.com/bots), en **Detalles**, copie el **identificador de la aplicación de Microsoft** para su bot.
  
      ![Obtener el AppID para el bot](~/assets/images/bots_appid_botframework.png)
  
   2. Abra Microsoft Teams, y en el panel de **Chat**, seleccione el icono **Agregar chat**. En **Para:**, pegue el identificador de aplicación de Microsoft del bot.
  
      ![Cargar bots](~/assets/images/bots_uploading.png)

      El identificador de la aplicación debe resolverse en el nombre del bot.

   3. Seleccione el bot y envíe un mensaje para iniciar una conversación.
      Como alternativa, puede pegar el identificador de la aplicación del bot en el cuadro de búsqueda de la parte superior izquierda de Microsoft Teams. En la página de resultados de la búsqueda, vaya a la pestaña **Contactos** para ver el bot e iniciar una conversación con él.

> [!Note]
> Para que Microsoft Teams haga referencia al identificador de aplicación del bot, habilite la [instalación de prueba de aplicaciones](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

El bot recibe el evento `conversationUpdate` cuando usted agregue los bots a un equipo, sin la información del equipo en el objeto `channelData`.

## <a name="block-a-bot-in-personal-chat"></a>Bloquear un bot en un chat personal

Los usuarios pueden optar por impedir que el bot envíe mensajes de chat por privado. Luego podrán modificar esto haciendo clic con el botón derecho en el bot en el canal de chat y seleccionando **Bloquear conversación con el bot**. Esto significa que los bots seguirá enviando mensajes, pero el usuario no los recibirá.

![Bloquear a un bot](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>Eliminar a un bot de un equipo

Los usuarios pueden eliminar el bot si seleccionan el icono de papelera en la lista de bots en la vista del equipo. Esto solo sirve para eliminar el bot de ese equipo y para que no se use ahí; pero los usuarios de manera individual pueden seguir interactuando con este. Los usuarios no pueden deshabilitar ni quitar los bots a nivel individual.

## <a name="disable-a-bot-in-teams"></a>Deshabilitar un bot en Teams

Para hacer que el bot deje de recibir mensajes, vaya al **Panel del bot** y edite el canal de Microsoft Teams. Desactive la opción **Habilitar en Microsoft Teams**. Esto sirve para que los usuarios dejen de interactuar con el bot. Sin embargo, se podrá seguir detectando y los usuarios podrán agregarlo a Teams.

## <a name="delete-a-bot-from-teams"></a>Eliminar un bot de Teams

Para editar el bot al completo desde Teams, vaya al **Panel del bot** y edite el canal de Microsoft Teams. Seleccione el botón **Eliminar** en la parte inferior. Esto sirve para que los usuarios dejen de detectar, agregar e interactuar con el bot. Esto no elimina al bot de las instancias de Teams de otros usuarios, pero ya no les funcionará.

## <a name="see-also"></a>Consulte también

* [Depurar el bot con el middleware de inspección](/azure/bot-service/bot-service-debug-inspection-middleware)
* [Depurar el bot de llamadas y reuniones de forma local](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
