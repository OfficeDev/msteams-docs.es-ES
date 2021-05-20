---
title: Pruebe y depure el bot
description: Describe cómo probar bots en Microsoft Teams
keywords: equipos bots pruebas
ms.topic: how-to
localization_priority: Normal
ms.date: 03/20/2019
ms.openlocfilehash: 269b0680e45d764cf4cb0269c40d3d202145edb8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566463"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Prueba y depura el bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Al probar el bot, debe tener en cuenta tanto los contextos en los que desea que se ejecute el bot, como cualquier funcionalidad que haya agregado al bot que requiera datos específicos de Microsoft Teams. Asegúrese de que el método que eligió para probar el bot se alinea con su funcionalidad.

## <a name="test-by-uploading-to-teams"></a>Prueba subiendo a Teams

La forma más completa de probar el bot es creando un paquete de aplicación y cargándolo en Teams. Este es el único método para probar la funcionalidad completa disponible para el bot, en todos los ámbitos.

Hay dos métodos para cargar la aplicación. Puedes usar [App Studio](~/concepts/build-and-test/app-studio-overview.md) para ayudarte o puedes crear manualmente [un paquete de aplicación](~/concepts/build-and-test/apps-package.md) y cargar la [aplicación.](~/concepts/deploy-and-publish/apps-upload.md) Si necesitas modificar el manifiesto y volver a cargar la aplicación, [debes eliminar el bot](#deleting-a-bot-from-teams) antes de cargar el paquete de aplicación modificado.

## <a name="debug-your-bot-locally"></a>Depurar el bot localmente

Si está alojando su bot localmente durante el desarrollo, deberá utilizar un servicio de tunelización como [ngrok](https://ngrok.com/) para probar el bot. Una vez que haya descargado e instalado ngrok, ejecute el siguiente comando para iniciar el servicio de tunelización. Es posible que deba agregar ngrok a su ruta de acceso.

```bash
ngrok http <port> -host-header=localhost:<port>
```

Use el punto de conexión https proporcionado por ngrok en el manifiesto de la aplicación. Si cierra la ventana de comandos y reinicia, obtendrá una nueva dirección URL y deberá actualizar la dirección del punto de conexión del bot para usarla también.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Probar el bot sin cargarlo en Teams

Ocasionalmente puede ser necesario probar el bot sin instalarlo como una aplicación en Teams. Proporcionamos dos métodos para hacerlo a continuación. Probar el bot sin instalarlo como una aplicación puede ser útil para garantizar que el bot esté disponible y respondiendo, sin embargo, no le permitirá probar toda la amplitud de Microsoft Teams funcionalidad que puede haber agregado a su bot. Si necesita probar completamente su bot, siga las instrucciones para [las pruebas cargando](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utilice el emulador de bots

La Bot Framework Emulator es una aplicación de escritorio que permite a los desarrolladores de bots probar y depurar sus bots, ya sea localmente o de forma remota. Con el emulador, puede chatear con su bot e inspeccionar los mensajes que el bot envía y recibe. Esto puede ser útil para comprobar que el bot está disponible y responder, sin embargo, el emulador no le permitirá probar ninguna funcionalidad específica de Teams que haya agregado al bot, ni las respuestas de su bot serán una representación visual precisa de cómo se representarán en Teams. Si necesita probar cualquiera de esas cosas es mejor [cargar su bot](#test-by-uploading-to-teams).

Puede encontrar instrucciones completas sobre el Bot Framework Emulator [aquí.](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)

### <a name="talk-to-your-bot-directly-by-id"></a>Hable con su bot directamente por Id

>[!Important]
>Hablar con su bot por id está destinado únicamente a fines de prueba.

También puede iniciar una conversación con su bot mediante su id. A continuación se indican dos métodos para hacerlo. Cuando se ha agregado un bot a través de uno de estos métodos, no se puede abordar en las conversaciones de canal y no puede aprovechar otras capacidades de Microsoft Teams aplicación, como pestañas o extensiones de mensajería.

1. En la página [Bot Dashboard del](https://dev.botframework.com/bots) bot, en **Canales**, seleccione Agregar **a Microsoft Teams**. Microsoft Teams se iniciará con un chat personal con su bot.
2. Haga referencia directamente al ID de aplicación del bot desde Microsoft Teams:
   * En la página [Panel de bots del](https://dev.botframework.com/bots) bot, en **Detalles**, copie el identificador de aplicación **de Microsoft** para el bot.
  
     ![Obtener el AppID para el bot](~/assets/images/bots_appid_botframework.png)
  
   * En Microsoft Teams, en el panel **Chat,** seleccione el icono **Agregar chat.** **Para:**, pegue el IDENTIFICADOR de microsoft app del bot.
  
     ![Carga del AppID para el bot](~/assets/images/bots_uploading.png)

     El identificador de aplicación debe resolverse con el nombre del bot.

   * Seleccione el bot y envíe un mensaje para iniciar una conversación.
   * Como alternativa, puede pegar el IDENTIFICADOR de aplicación del bot en el cuadro de búsqueda en la parte superior izquierda de Microsoft Teams. En la página de resultados de búsqueda, vaya a la pestaña Personas para ver el bot y empezar a chatear con él.

El bot recibirá el `conversationUpdate` evento al igual que los bots agregados a un equipo, pero sin la información del equipo en el `channelData` objeto.

## <a name="blocking-a-bot-in-personal-chat"></a>Bloqueo de un bot en el chat personal

Tenga en cuenta que los usuarios pueden elegir bloquear el envío de mensajes de chat personales por parte del bot. Pueden alternar esto haciendo clic con el botón derecho en el bot en el canal de chat y eligiendo **Bloquear conversación de bot.** Esto significa que los bots seguirán enviando mensajes, pero el usuario no recibirá esos mensajes.

![Bloqueo de un bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Extracción de un bot de un equipo

Los usuarios pueden eliminar el bot eligiendo el icono de papelera en la lista de bots en la vista de sus equipos. Tenga en cuenta que esto solo elimina el bot del uso de ese equipo; los usuarios individuales todavía podrán interactuar en contexto personal.

Los bots en contexto personal no pueden ser deshabilitados o eliminados por un usuario, a falta de eliminar completamente el bot de Teams.

## <a name="disabling-a-bot-in-teams"></a>Deshabilitar un bot en Teams

Para evitar que el bot reciba mensajes, vaya al Panel de bots y edite el canal de Microsoft Teams. Desactive la opción **Habilitar en Microsoft Teams.** Esto impide que los usuarios interactúen con el bot, pero seguirá siendo detectable y los usuarios podrán agregarlo a los equipos.

## <a name="deleting-a-bot-from-teams"></a>Eliminación de un bot de Teams

Para eliminar el bot por completo de Teams, ve al Panel de bots y edita el canal de Microsoft Teams. Elija el botón **Eliminar** en la parte inferior. Esto impide que los usuarios descubran, agreguen o interactúen con el bot. Tenga en cuenta que esto no quita el bot de las instancias de Teams de otros usuarios, aunque también dejará de funcionar para ellos.

## <a name="removing-your-bot-from-appsource"></a>Eliminación del bot de AppSource

Si quieres quitar el bot de la aplicación Teams en AppSource (anteriormente Office Store), debes quitar el bot del manifiesto de la aplicación y volver a enviar la aplicación para su validación. Para obtener más información, consulte [Publicar la aplicación Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md).
