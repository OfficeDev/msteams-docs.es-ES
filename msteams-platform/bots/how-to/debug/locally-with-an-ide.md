---
title: Probar y depurar el bot localmente
author: clearab
description: Probar y depurar el bot localmente con un IDE
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8494302b41e33910cb33f8c6889d82505b703577
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675844"
---
# <a name="test-and-debug-your-bot-locally"></a>Probar y depurar el bot localmente

Al probar el bot, debe tener en cuenta los contextos en los que desea que se ejecute el bot, así como cualquier funcionalidad que haya agregado a su bot que requiera datos específicos de Microsoft Teams. Asegúrese de que el método que eligió para probar el bot se alinee con su funcionalidad.

## <a name="test-by-uploading-to-teams"></a>Realizar pruebas mediante la carga a teams

La forma más completa de probar el bot es crear un paquete de la aplicación y cargarlo en Teams. Este es el único método para probar la funcionalidad completa disponible para el bot en todos los ámbitos.

Hay dos métodos para cargar la aplicación. Puede usar [App Studio](~/concepts/build-and-test/app-studio-overview.md) para ayudarle, o puede [crear manualmente un paquete](~/concepts/build-and-test/apps-package.md) de la aplicación y [cargar la aplicación](~/concepts/deploy-and-publish/apps-upload.md). Si necesita modificar el manifiesto y volver a cargar la aplicación, debe [eliminar el bot](#deleting-a-bot-from-teams) antes de cargar el paquete de la aplicación que ha modificado.

## <a name="debug-your-bot-locally"></a>Depurar el bot localmente

Si hospeda el bot localmente durante el desarrollo, deberá usar un servicio de túnel como [ngrok](https://ngrok.com/) para probar el bot. Una vez que haya descargado e instalado ngrok, ejecute el siguiente comando para iniciar el servicio de túnel (es posible que deba agregar ngrok a la ruta de acceso).

```bash
ngrok http <port> -host-header=localhost:<port>
```

Use el punto de conexión HTTPS proporcionado por ngrok en el manifiesto de la aplicación. Si cierra la ventana de comandos y reinicia, obtendrá una nueva dirección URL y tendrá que actualizar la dirección de su punto de conexión de bot para usar también esta.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Probar el bot sin cargar a teams

En ocasiones, puede ser necesario probar el bot sin instalarlo como una aplicación en Microsoft Teams. A continuación se ofrecen dos métodos para hacerlo. Probar el bot sin instalarlo como una aplicación puede ser útil para asegurarse de que su bot está disponible y responde, pero no le permitirá probar toda la funcionalidad de Microsoft teams que haya agregado a su bot. Si necesita probar completamente el bot, siga las instrucciones para [realizar las pruebas mediante la carga](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Usar el emulador de bot

Bot Framework Emulator es una aplicación de escritorio que permite a los programadores de robots probar y depurar los bots, ya sea de forma local o remota. Mediante el emulador, puede chatear con su bot e inspeccionar los mensajes que envía y recibe el bot. Esto puede ser útil para comprobar que el bot está disponible y responde, pero el emulador no le permitirá probar ninguna funcionalidad específica de teams que haya agregado a su bot, ni las respuestas del bot serán una representación visual precisa de cómo se se puede representar en Microsoft Teams. Si necesita probar cualquiera de esas cosas, es mejor [cargar el bot](#test-by-uploading-to-teams).

Encontrará instrucciones completas en el emulador de bot Framework [.](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0)

### <a name="talk-to-your-bot-directly-by-id"></a>Hable directamente con su bot mediante el identificador

>[!Important]
>La comunicación con el bot mediante el identificador está pensada solo para fines de pruebas básicas. Las funcionalidades específicas de teams que haya agregado a su bot no funcionarán.

También puede iniciar una conversación con el bot mediante su identificador. A continuación se indican dos métodos para hacerlo. Cuando se ha agregado un bot a través de uno de estos métodos, no será direccionable en conversaciones de canal y no podrá aprovechar otras funciones de la aplicación Microsoft Teams, como pestañas o extensiones de mensajería.

1. En la página [Panel de bot](https://dev.botframework.com/bots) de su bot, en **canales**, seleccione **Agregar a Microsoft Teams**. Microsoft Teams se iniciará con un chat personal con su bot.
2. Haga referencia directamente al identificador de aplicación de su bot desde Microsoft Teams:
   * En la página de [Panel de bot](https://dev.botframework.com/bots) ? n de su bot, en **detalles**, copie el identificador de **aplicación de Microsoft** para su bot? n.
  
     ![Obtener el AppID del bot](~/assets/images/bots_appid_botframework.png)
  
   * En Microsoft Teams, en el panel **chat** , haga clic en el icono **Agregar chat** . Para **para:**, pegue el identificador de aplicación de Microsoft de bot.
  
     ![Obtener el AppID del bot](~/assets/images/bots_uploading.png)

     El identificador de la aplicación debe resolverse en el nombre del bot.

   * Seleccione el bot y envíe un mensaje para iniciar una conversación.
   * Como alternativa, puede pegar el identificador de aplicación de bot en el cuadro de búsqueda de la parte superior izquierda en Microsoft Teams. En la página de resultados de búsqueda, vaya a la pestaña personas para ver el bot y empezar a chatear con él.

El bot recibirá el `conversationUpdate` evento del mismo modo que los bots agregados a un equipo, pero sin la `channelData` información del equipo en el objeto.

## <a name="blocking-a-bot-in-personal-chat"></a>Bloqueo de un bot en chat personal

Tenga en cuenta que los usuarios pueden optar por bloquear el bot para que no envíe mensajes de chat personal. Pueden alternar esto haciendo clic con el botón secundario en el bot en el canal de chat y eligiendo **bloquear conversación de robot**. Esto significa que los bots seguirán enviando mensajes, pero el usuario no recibirá esos mensajes.

![Bloqueo de un bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Quitar un bot de un equipo

Los usuarios pueden eliminar el bot seleccionando el icono de la papelera de la lista bots en la vista de Teams. Tenga en cuenta que esto solo quita el bot del uso de ese equipo; los usuarios individuales seguirán pudiendo interactuar en el contexto personal.

Los bots en el contexto personal no se pueden deshabilitar ni quitar por un usuario, es decir, quitar completamente el bot de Teams.

## <a name="disabling-a-bot-in-teams"></a>Deshabilitar un bot en Teams

Para detener la recepción de mensajes del bot, vaya a su panel de Bot? y edite el canal de Microsoft Teams. Desactive la opción **Habilitar en Microsoft Teams** . Esto evita que los usuarios interactúen con el bot, pero seguirá siendo reconocible y los usuarios podrán agregarlo a teams.

## <a name="deleting-a-bot-from-teams"></a>Eliminación de un bot de Teams

Para quitar su bot completamente de Microsoft Teams, vaya a su panel de Bot? y edite el canal de Microsoft Teams. Elija el botón **eliminar** en la parte inferior. Esto evita que los usuarios detecten, agreguen o interaccionen con el bot. Tenga en cuenta que esto no quita el bot de las instancias de los equipos de otros usuarios, aunque también dejará de funcionar para ellos.
