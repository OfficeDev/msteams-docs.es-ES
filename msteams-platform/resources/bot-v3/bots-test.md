---
title: Prueba y depuración de la aplicación
description: En este artículo, sabrá cómo probar y depurar los bots en Microsoft Teams y probar el bot sin cargarlo en Teams.
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: e1b1921b3a51731a67ddfeee78f38c2f6f3a9c83
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312040"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Probar y depurar la el bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Al probar el bot, debe tener en cuenta tanto los contextos en los que quiere que se ejecute el bot como cualquier funcionalidad que haya agregado al bot que requiera datos específicos de Microsoft Teams. Asegúrese de que el método que eligió para probar el bot se alinea con su funcionalidad.

## <a name="test-by-uploading-to-teams"></a>Prueba mediante la carga en Teams

La manera más completa de probar el bot es crear un paquete de aplicación y cargarlo en Teams. Cargar la aplicación en Teams es el único método para probar la funcionalidad completa disponible para el bot, en todos los ámbitos.

Hay dos métodos para cargar la aplicación. Puede usar [el Portal para desarrolladores para Teams](~/concepts/build-and-test/teams-developer-portal.md) o puede [crear manualmente un paquete de aplicación](~/concepts/build-and-test/apps-package.md) y [cargar la aplicación](~/concepts/deploy-and-publish/apps-upload.md). Si necesita modificar el manifiesto y volver a cargar la aplicación, debe [eliminar el bot](#deleting-a-bot-from-teams) antes de cargar el paquete de aplicación modificado.

## <a name="debug-your-bot-locally"></a>Depuración del bot localmente

Si va a hospedar el bot localmente durante el desarrollo, deberá usar un servicio de tunelización como [ngrok](https://ngrok.com/) para probar el bot. Una vez que haya descargado e instalado ngrok, ejecute el siguiente comando para iniciar el servicio de tunelización. Es posible que tenga que agregar ngrok a la ruta de acceso.

```bash
ngrok http <port> --host-header=localhost:<port>
```

Use el punto de conexión https proporcionado por ngrok en el manifiesto de la aplicación. Si cierra la ventana de comandos y se reinicia, obtendrá una nueva dirección URL y tendrá que actualizar la dirección del punto de conexión del bot para usarla también.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Probar el bot sin cargarlo en Teams

En ocasiones, es necesario probar el bot sin instalarlo como una aplicación en Teams. Proporcionamos dos métodos para las pruebas. Probar el bot sin instalarlo como una aplicación puede ser útil para asegurarse de que el bot está disponible y responder, pero no le permitirá probar toda la amplitud de la funcionalidad de Teams que puede haber agregado al bot. Si necesita probar completamente el bot, siga las instrucciones de [Prueba mediante carga](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Uso del emulador de bots

La Bot Framework Emulator es una aplicación de escritorio que permite a los desarrolladores de bots probar y depurar sus bots, ya sea de forma local o remota. Con el emulador, puede chatear con el bot e inspeccionar los mensajes que el bot envía y recibe. Esto puede ser útil para comprobar que el bot está disponible y responder, pero el emulador no le permitirá probar ninguna funcionalidad específica de Teams que haya agregado al bot, ni las respuestas del bot serán una representación visual precisa de cómo se representan en Teams. Si necesita probar cualquiera de estas cosas, no es mejor [cargar el bot](#test-by-uploading-to-teams).

Encontrará instrucciones completas sobre el Bot Framework Emulator [aquí](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Hable con el bot directamente por identificador

>[!Important]
>Hablar con el bot por identificador está pensado solo con fines de prueba.

También puede iniciar una conversación con el bot mediante su identificador. A continuación se proporcionan dos métodos para hacerlo. Cuando se agrega un bot a través de uno de estos métodos, no será direccionable en las conversaciones de canal y no podrá aprovechar otras funcionalidades de aplicaciones de Microsoft Teams, como pestañas o extensiones de mensajes.

1. En la página [Panel del bot](https://dev.botframework.com/bots), en **Canales**, seleccione **Agregar a Microsoft Teams**. Teams se iniciará con un chat personal con el bot.
2. Haga referencia directamente al identificador de aplicación del bot desde Teams:
   * En la página [ Panel de control del bot](https://dev.botframework.com/bots), en **Details**, copie el **Id. de aplicación de Microsoft** del bot.
  
      :::image type="content" source="../../assets/images/bots_appid_botframework.png" alt-text="Panel del bot":::
  
   * En Teams, en el panel **Chat** , seleccione el icono **Agregar chat** . Para **Para:**, pegue el identificador de aplicación de Microsoft del bot.
  
      :::image type="content" source="../../assets/images/bots_uploading.png" alt-text="Carga del AppID para el bot"border="true":::

     El identificador de la aplicación debe resolverse en el nombre del bot.

   * Seleccione el bot y envíe un mensaje para iniciar una conversación.

   * Como alternativa, puede pegar el identificador de la aplicación del bot en el cuadro de búsqueda de la parte superior izquierda de Microsoft Teams. En la página de resultados de la búsqueda, vaya a la pestaña Contactos para ver el bot e iniciar una conversación con él.

El bot recibirá el evento `conversationUpdate` igual que los bots agregados a un equipo, pero sin la información del equipo en el objeto `channelData`.

## <a name="blocking-a-bot-in-personal-chat"></a>Bloquear un bot en un chat personal

Los usuarios pueden optar por impedir que el bot envíe mensajes de chat por privado. Luego podrán modificar esto haciendo clic con el botón derecho en el bot en el canal de chat y seleccionando **Bloquear conversación con el bot**. Esto significa que los bots seguirán enviando mensajes, pero el usuario no los recibirá.

  :::image type="content" source="../../assets/images/bots/botdisable.png" alt-text="Bloqueo de un bot"border="true":::

## <a name="removing-a-bot-from-a-team"></a>Eliminación de un bot de un equipo

Los usuarios pueden eliminar el bot eligiendo el icono de papelera en la lista de bots en la vista de equipos. Tenga en cuenta que esto solo quita el bot del uso de ese equipo; los usuarios individuales pueden interactuar en el contexto personal.

Un usuario no puede deshabilitar ni quitar bots en el contexto personal, en lugar de quitar completamente el bot de Teams.

## <a name="disabling-a-bot-in-teams"></a>Deshabilitar un bot en Teams

Para detener la recepción de mensajes del bot, vaya al Panel de bots y edite el canal de Microsoft Teams. Desactive la opción **Permitir en Microsoft Teams**. Deshabilitar un bot en Teams impide que los usuarios interactúen con el bot, pero seguirá siendo reconocible y los usuarios podrán agregarlo a los equipos.

## <a name="deleting-a-bot-from-teams"></a>Eliminación de un bot de Teams

Para quitar completamente el bot de Teams, vaya al Panel de bots y edite el canal de Microsoft Teams. Elija el botón **Borrar** en la parte inferior. La eliminación de un bot de Teams impide que los usuarios detecten, agreguen o interactúen con el bot. La eliminación de un bot de Teams no quita el bot de las instancias de Teams de otros usuarios, aunque dejará de funcionar para ellos también.

## <a name="removing-your-bot-from-appsource"></a>Eliminación del bot de AppSource

Si desea quitar el bot de la aplicación de Teams en AppSource (anteriormente, la Tienda Office), debe quitar el bot del manifiesto de la aplicación y volver a enviar la aplicación para su validación. Para obtener más información, vea [Publicar la aplicación de Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md).
