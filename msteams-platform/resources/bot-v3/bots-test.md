---
title: Probar y depurar el bot
description: Describe cómo probar bots en Microsoft Teams
keywords: pruebas de bots de teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: 71d70aef3adeb3d351223e918aec21d0d2dea440
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720123"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Probar y depurar el Microsoft Teams bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Al probar el bot, debes tener en cuenta los contextos en los que quieres que se ejecute el bot, así como cualquier funcionalidad que haya agregado al bot que requiera datos específicos para Microsoft Teams. Asegúrese de que el método elegido para probar el bot se alinea con su funcionalidad.

## <a name="test-by-uploading-to-teams"></a>Pruebe cargando en Teams

La forma más completa de probar el bot es crear un paquete de aplicación y cargarlo en Teams. Este es el único método para probar la funcionalidad completa disponible para el bot, en todos los ámbitos.

Hay dos métodos para cargar la aplicación. Puedes usar [App Studio](~/concepts/build-and-test/app-studio-overview.md) o puedes crear manualmente un paquete [de aplicación](~/concepts/build-and-test/apps-package.md) y cargar [la aplicación](~/concepts/deploy-and-publish/apps-upload.md). Si necesitas modificar el manifiesto y volver a cargar la aplicación, debes eliminar el [bot](#deleting-a-bot-from-teams) antes de cargar el paquete de la aplicación modificado.

## <a name="debug-your-bot-locally"></a>Depurar el bot localmente

Si hospedas el bot localmente durante el desarrollo, tendrás que usar un servicio de túnel como [ngrok](https://ngrok.com/) para probar el bot. Una vez que haya descargado e instalado ngrok, ejecute el siguiente comando para iniciar el servicio de túnel. Es posible que deba agregar ngrok a la ruta de acceso.

```bash
ngrok http <port> -host-header=localhost:<port>
```

Usa el punto de conexión https proporcionado por ngrok en el manifiesto de la aplicación. Si cierras la ventana de comandos y reinicias, tendrás una nueva dirección URL y tendrás que actualizar la dirección del extremo del bot para usarla también.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Probar el bot sin cargarlo en Teams

En ocasiones, es necesario probar el bot sin instalarlo como una aplicación en Teams. Proporcionamos dos métodos para las pruebas. Probar el bot sin instalarlo como una aplicación puede ser útil para garantizar que el bot esté disponible y responda, pero no te permitirá probar toda la amplitud de la funcionalidad de Microsoft Teams que puedas haber agregado al bot. Si necesita probar el bot completamente, siga las instrucciones para [realizar pruebas cargando](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Use el bot Emulator

El Bot Framework Emulator es una aplicación de escritorio que permite a los desarrolladores de bots probar y depurar sus bots, ya sea de forma local o remota. Con el emulador, puedes chatear con el bot e inspeccionar los mensajes que el bot envía y recibe. Esto puede ser útil para comprobar que el bot está disponible y responde, pero el emulador no le permitirá probar ninguna funcionalidad específica de Teams que haya agregado al bot, ni las respuestas del bot serán una representación visual precisa de cómo se representan en Teams. Si necesita probar cualquiera de estas cosas, no es mejor cargar [el bot](#test-by-uploading-to-teams).

Aquí se pueden encontrar Bot Framework Emulator instrucciones [completas en el archivo](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Hablar con el bot directamente por id.

>[!Important]
>La conversación con el bot por id. está diseñada únicamente para fines de prueba.

También puedes iniciar una conversación con el bot mediante su identificador. A continuación se indican dos métodos para hacerlo. Cuando un bot se ha agregado a través de uno de estos métodos, no será direccionable en conversaciones de canal y no puedes aprovechar otras funcionalidades de aplicaciones de Microsoft Teams como pestañas o extensiones de mensajería.

1. En la [página Panel de bots](https://dev.botframework.com/bots) del bot, en **Canales,** seleccione Agregar **a Microsoft Teams**. Microsoft Teams se iniciará con un chat personal con el bot.
2. Haga referencia directamente al identificador de aplicación del bot desde dentro Microsoft Teams:
   * En la [página Panel de bots](https://dev.botframework.com/bots) del bot, en **Detalles,** copie el identificador de **aplicación de Microsoft** para el bot.
  
     ![Obtener el AppID para el bot](~/assets/images/bots_appid_botframework.png)
  
   * Desde dentro Microsoft Teams, en el **panel Chat,** seleccione el **icono Agregar chat.** For **To:**, paste your bot's Microsoft App ID.
  
     ![Cargar el AppID para el bot](~/assets/images/bots_uploading.png)

     El identificador de la aplicación debe resolverse en el nombre del bot.

   * Seleccione el bot y envíe un mensaje para iniciar una conversación.
   * Como alternativa, puedes pegar el identificador de la aplicación del bot en el cuadro de búsqueda de la parte superior izquierda de Microsoft Teams. En la página de resultados de búsqueda, vaya a la pestaña Personas para ver el bot y empezar a chatear con él.

El bot recibirá el evento igual que los bots agregados a un equipo, pero sin la `conversationUpdate` información del equipo en el `channelData` objeto.

## <a name="blocking-a-bot-in-personal-chat"></a>Bloqueo de un bot en chat personal

Ten en cuenta que los usuarios pueden elegir bloquear el bot para que no envíe mensajes de chat personales. Pueden alternar esto haciendo clic con el botón secundario en el bot en el canal de chat y eligiendo **Bloquear conversación de bot**. Esto significa que los bots seguirán mandando mensajes, pero el usuario no los recibirá.

![Bloqueo de un bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Quitar un bot de un equipo

Los usuarios pueden eliminar el bot eligiendo el icono de papelera en la lista de bots de la vista equipos. Tenga en cuenta que esto solo quita el bot del uso de ese equipo, los usuarios individuales pueden interactuar en contexto personal.

Los bots en contexto personal no pueden deshabilitarse ni quitarse por un usuario, a falta de quitar completamente el bot de Teams.

## <a name="disabling-a-bot-in-teams"></a>Deshabilitar un bot en Teams

Para detener la recepción de mensajes del bot, vaya al Panel de bots y edite el Microsoft Teams. Desactive la **opción Habilitar en Microsoft Teams.** Esto impide que los usuarios interactúen con el bot, pero seguirá siendo detectable y los usuarios pueden agregarlo a teams.

## <a name="deleting-a-bot-from-teams"></a>Eliminar un bot de Teams

Para quitar el bot completamente de Teams, vaya al Panel del bot y edite el Microsoft Teams. Elija el **botón** Eliminar en la parte inferior. Esto impide que los usuarios detecten, agreguen o interactúen con el bot. Tenga en cuenta que esto no quita el bot de las instancias Teams usuarios, aunque también dejará de funcionar para ellos.

## <a name="removing-your-bot-from-appsource"></a>Quitar el bot de AppSource

Si quieres quitar el bot de la aplicación Teams en AppSource (anteriormente Office Store), debes quitar el bot del manifiesto de la aplicación y volver a enviar la aplicación para su validación. Para obtener más información, vea [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).
