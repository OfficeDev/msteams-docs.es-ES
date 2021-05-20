---
title: Empezar - Crear un bot
author: girliemac
description: Cree rápidamente un bot Microsoft Teams utilizando el Microsoft Teams Toolkit.
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: 2cbd90b293e8ac8343febc7b3d23278d5bb5bf82
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565889"
---
# <a name="create-your-first-bot-for-teams"></a>Crea tu primer bot para Teams

En este tutorial se le enseña a crear una aplicación de bot básica. Un bot actúa como intermediario entre los usuarios Teams y la aplicación web o servicio con una interfaz conversacional. Las personas pueden chatear con un bot para obtener información rápidamente o iniciar flujos de trabajo y tareas realizadas por su servicio.

## <a name="what-youll-learn"></a>Lo que aprenderás

* Cree un proyecto de aplicación y un bot con la Microsoft Teams Toolkit para Visual Studio Code.
* Comprender las configuraciones de Teams aplicación relevantes para los bots.
* Hospede y ejecute una aplicación localmente mediante una solución de tunelización localhost.
* Descargue lateralmente y pruebe un bot en Teams.

## <a name="prerequisites"></a>Requisitos previos

Asegúrese de comprender cómo configurar y crear una aplicación de Teams sencilla. Para obtener más información, consulta [crear tu primera aplicación Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md) 

## <a name="1-create-your-app-project"></a>1. Cree el proyecto de la aplicación

El Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para la aplicación: 

* **Configuraciones de aplicaciones y andamios** relevantes para bots.
* **Bot** que se registra automáticamente con el servicio de bots de Microsoft Azure.

**Para crear el proyecto de aplicación**

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividades izquierda y elija Crear una nueva aplicación **de Teams**.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Captura de pantalla que muestra cómo crear una aplicación en el Teams Toolkit.":::

1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365. 
1. En la pantalla Seleccionar proyecto, seleccione Bots de conversación: 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Captura de pantalla que muestra cómo crear un nuevo bot en el Teams Toolkit.":::

1. En la pantalla **Configurar proyecto,** escriba un nombre para el bot. Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.
1. Seleccione **Crear un nuevo registro** de  >  **bots de creación de bots** como se muestra en la siguiente imagen:

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Captura de pantalla que muestra el nombre de nuevo bot en el Teams Toolkit.":::

    Si se realiza correctamente, el nuevo bot tendrá un estado **Registrado.** Ahora el bot se registra automáticamente con el servicio de bots de Microsoft Azure. 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Captura de pantalla que muestra el registro de nuevo bot en el Teams Toolkit.":::

1. Seleccione **Finalizar** en la parte inferior de la pantalla y guarde el proyecto en el equipo.  

## <a name="2-understand-your-app-project-components"></a>2. Comprender los componentes del proyecto de la aplicación

Gran parte de las configuraciones de la aplicación y los andamios se configuran automáticamente al crear el proyecto con el Teams Toolkit. Echemos un vistazo a los componentes principales para crear un bot:

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Captura de pantalla que muestra un andamio de proyecto en el Teams Toolkit.":::

Si creó una pestaña en otro tutorial, el andamiaje de la aplicación para el bot es diferente. A diferencia de las pestañas, el desarrollo de bots no requiere que cree ningún componente web front-end ni utilice el SDK de cliente de JavaScript Teams.  En su lugar, el andamio utiliza el [Microsoft Bot Framework](https://dev.botframework.com/), que es un SDK de código abierto para crear bots inteligentes de nivel empresarial que pueden funcionar en la web, móvil y, por supuesto, Teams! 

El `botActivityHandler.js` archivo, ubicado en el directorio raíz del proyecto, es el controlador específico de Teams que controla las actividades del bot, como cómo responde el bot a mensajes específicos. El andamiaje de la aplicación proporciona un `botActivityHandler.js` archivo ubicado en el directorio raíz del proyecto, es el controlador específico Teams que controla las actividades del bot, como cómo responde el bot a mensajes específicos.

## <a name="3-securely-expose-your-localhost-to-the-internet"></a>3. Exponga de forma segura su localhost a Internet

Eche un vistazo al `index.js` archivo, que crea un servidor HTTP y controla el enrutamiento para escuchar las solicitudes entrantes al bot. La `/api/messages` dirección URL del punto de conexión de la aplicación es la que responde a las solicitudes de cliente: 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

Para reenviar las solicitudes a la lógica del bot, debe configurar una dirección URL de acceso público, como `https://example.com/api/messages` , en lugar de `https://localhost` . Dado que la aplicación se está ejecutando desde el localhost actualmente, debe hacer *un túnel de* la red.

La tunelización es un protocolo que le permite transportar datos a través de una red. Y la tunelización localhost le ofrece una conexión entre su máquina local y una conexión remota. Para exponer de forma segura su localhost a Internet, le recomendamos que utilice la herramienta 3rd party llamada **ngrok**. Esto le dará una URL segura. 

1. Vaya al sitio [de ngrok.com](https://ngrok.com/download) y siga las instrucciones para instalar y configurar ngrok en su entorno. 
    
    Agregue la ruta completa al archivo ngrok.exe que instaló en la variable de entorno PATH del sistema. Los pasos exactos son específicos del shell que está utilizando.

1.  Una vez que haya terminado de configurarlo, abra un terminal y ejecute `ngrok http -host-header=rewrite 3978` . 

    Ahora ngrok le proporciona una dirección URL pública y segura que reenvía a su localhost en el puerto 3978, así que copie la dirección URL HTTPS, por ejemplo, `https://287a4f4223bc.ngrok.io` como se muestra en la captura de pantalla siguiente, ya que Teams requiere conexiones HTTPS: 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Captura de pantalla que muestra la tunelización de localhost con ngrok.":::

1. Registre la dirección URL en el manifiesto de la aplicación. 

## <a name="4-register-your-bot-endpoint"></a>4. Registre el punto final del bot

Para usar un bot en Teams, debe registrarlo en Azure Bot Service. Esto se hace automáticamente cuando configuras la aplicación con la Teams Toolkit.

Todavía debe especificar una dirección de punto de conexión para recibir y procesar mensajes de usuario o solicitudes enviadas al bot. Normalmente, la dirección URL se parece `https://HOST_URL/api/messages` a . Puede configurarlo en el kit de herramientas.

1. En Visual Studio Code, abra **Microsoft Teams Toolkit**.
1. Seleccione **Bots**  >  **Registros de bots existentes** y seleccione el bot que creó durante la instalación. 
1. En el campo **Dirección del punto de conexión del bot,** escriba la dirección URL de ngrok, por ejemplo, donde hospeda el bot y `https://287a4f4223bc.ngrok.io` `/api/messages` anexe a él:

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Captura de pantalla que muestra cómo hacer un túnel localhost con ngrok.":::

    El bot podrá responder a los mensajes de Teams, después de configurar el punto de conexión correctamente. 

## <a name="5-build-and-run-your-app"></a>5. Compile y ejecute la aplicación

Ha configurado una dirección URL para hospedar el bot y lo ha configurado para controlar los mensajes. Es hora de poner en marcha la aplicación.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecute `npm start`.

   Si se realiza correctamente, verá el siguiente mensaje que indica que el bot está escuchando la actividad `localhost` en:

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Descargue su bot en Teams

Con el bot en ejecución, puede instalarlo en Teams.

> [!TIP]
> Si no has descargado una aplicación Teams antes y te has quedado con problemas, sigue estas [instrucciones.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. En Visual Studio Code, seleccione la clave **F5** para iniciar un cliente web Teams.
1. En el cuadro de diálogo de instalación de la aplicación, seleccione **Agregar para mí.** 

   > [!Note]
   > De forma predeterminada, la aplicación se agrega a su mensaje de chat directo 1:1, sin embargo, puede optar por instalarlo en un equipo o chat haciendo clic en la pequeña flecha junto a **Agregar para mí.** En este tutorial, vamos a hacer clic en Agregar.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Captura de pantalla que muestra túnel localhost con ngrok.":::

## <a name="7-test-your-bot"></a>7. Pruebe su bot

Digamos "Hola" a tu bot.

* En el cuadro de composición, envíe un `Hello` mensaje.
    El bot responde con algo como el siguiente mensaje:

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Una captura de pantalla que muestra a un usuario decir 'Hola' a un bot de Teams y obtener una respuesta.":::

    Ahora ha creado un bot Teams básico que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats) 🎉.

## <a name="troubleshoot-your-bot"></a>Solución de problemas del bot

La siguiente información puede ayudar si tuvo problemas para completar este tutorial.

### <a name="bot-isnt-connected-to-teams"></a>Bot no está conectado a Teams


Si instaló la aplicación pero el bot no funciona, asegúrese de que el bot esté [conectado al *canal* de Teams del Servicio de bots de Azure.](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Es importante entender que esto no es lo mismo que un canal en Teams. En este caso, un canal es cómo Azure Bot Service conecta el bot a Teams u otra [aplicación de comunicaciones compatible con Microsoft o de terceros.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="see-also"></a>Vea también

* [Conceptos básicos del bot](../bots/bot-basics.md)
* [Construir una pestaña personal para Microsoft Teams](../build-your-first-app/build-personal-tab.md)
* [Vea qué más pueden hacer Teams bots con una de nuestras muestras](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Conceptos básicos de las conversaciones de bot](../bots/how-to/conversations/conversation-basics.md)
* [Directrices de diseño](../bots/design/bots.md) 
* [Plantillas de interfaz de usuario listas para producción](../concepts/design/design-teams-app-ui-templates.md)
* [Autenticación de bots en Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [Crear un bot sin el kit de herramientas](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una extensión de mensajería](../build-your-first-app/build-messaging-extension.md)
