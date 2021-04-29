---
title: 'Introducción: crear un bot'
author: girliemac
description: Cree rápidamente un bot de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: dbb6f0a2497a0914d8e14473f1dbd6b2b225fc96
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068633"
---
# <a name="create-your-first-bot-for-teams"></a>Crear el primer bot para Teams

Este tutorial te enseña a crear una aplicación básica de bot. Un bot actúa como intermediario entre los usuarios de Teams y su aplicación web o servicio con una interfaz de conversación. Los usuarios pueden chatear con un bot para obtener información rápidamente o iniciar flujos de trabajo y tareas realizados por el servicio.

## <a name="what-youll-learn"></a>Lo que aprenderás

* Crea un proyecto de aplicación y un bot con Microsoft Teams Toolkit para Visual Studio código.
* Comprender las configuraciones de la aplicación de Teams relevantes para los bots.
* Host and run an app locally using a localhost tunneling solution.
* Descarga local y prueba un bot en Teams.

## <a name="prerequisites"></a>Requisitos previos

Asegúrate de comprender cómo configurar y crear una aplicación sencilla de Teams. Para obtener más información, consulta crear la primera aplicación de [Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md) 

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

Microsoft Teams Toolkit te ayuda a configurar los siguientes componentes para la aplicación: 

* **Configuraciones de aplicaciones y scaffolding relevantes** para bots
* **Bot** que se registra automáticamente en el Servicio de bots de Microsoft Azure

**Para crear el proyecto de aplicación**

1. En Visual Studio, selecciona **Microsoft Teams en** la barra de actividades izquierda y elige Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams**.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Captura de pantalla que muestra cómo crear una aplicación en Teams Toolkit.":::

1. Cuando se le pida, inicie sesión con su cuenta de desarrollo de Microsoft 365. 
1. En la pantalla Seleccionar proyecto, seleccione Bots de conversación: 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Captura de pantalla que muestra cómo crear un nuevo bot en Teams Toolkit.":::

1. En la **pantalla Configurar proyecto,** escriba un nombre para el bot. Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.
1. Seleccione **Crear un nuevo registro de bot** crear  >  **bot** como se muestra en la siguiente imagen:

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Captura de pantalla que muestra el nombre del nuevo bot en teams Toolkit.":::

    Si se realiza correctamente, el nuevo bot tendrá un **estado Registrado.** Ahora, el bot se registra automáticamente en el Servicio de bots de Microsoft Azure. 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Captura de pantalla que muestra el registro de nuevo bot en Teams Toolkit.":::

1. Selecciona **Finalizar** en la parte inferior de la pantalla y guarda el proyecto en el equipo.  

## <a name="2-understand-your-app-project-components"></a>2. Comprender los componentes del proyecto de la aplicación

Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit. Veamos los componentes principales para crear un bot:

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Captura de pantalla que muestra un scaffolding de proyecto en Teams Toolkit.":::

Si creaste una pestaña en otro tutorial, el scaffolding de la aplicación para el bot es diferente. A diferencia de las pestañas, el desarrollo de bots no requiere que cree ningún componente web front-end ni use el SDK de cliente de JavaScript de Teams.  En su lugar, el scaffolding usa [Microsoft Bot Framework](https://dev.botframework.com/), que es un SDK de código abierto para crear bots inteligentes de nivel empresarial que pueden funcionar en la web, en dispositivos móviles y, por supuesto, en Teams. 

El archivo, ubicado en el directorio raíz del proyecto, es el controlador específico de Teams que controla las actividades del bot, como la forma en que el bot responde a `botActivityHandler.js` mensajes específicos. El scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, es el controlador específico de Teams que controla las actividades del bot, como la forma en que el bot responde a mensajes `botActivityHandler.js` específicos.

## <a name="3-securely-expose-your-localhost-to-the-internet"></a>3. Exponer de forma segura el localhost a Internet

Echa un vistazo al archivo, que crea un servidor HTTP y controla el enrutamiento para escuchar las solicitudes `index.js` entrantes al bot. Es la dirección URL del punto de conexión de la `/api/messages` aplicación para responder a las solicitudes de cliente: 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

Para reenviar las solicitudes a la lógica del bot, debe configurar una dirección URL accesible públicamente, como `https://example.com/api/messages` , en lugar de `https://localhost` . Dado que la aplicación se está ejecutando desde el localhost actualmente, debes *túnel de* la red.

El túnel es un protocolo que permite transportar datos a través de una red. Además, la tunelización de localhost proporciona una conexión entre la máquina local y una conexión remota. Para exponer de forma segura el localhost a Internet, se recomienda usar la herramienta de terceros denominada **ngrok**. Esto le dará una dirección URL segura. 

1. Vaya al [sitio ngrok.com](https://ngrok.com/download) y siga las instrucciones para instalar y configurar ngrok en su entorno. 
    
    Agregue la ruta de acceso completa al ngrok.exe archivo que instaló en la variable de entorno PATH del sistema. Los pasos exactos son específicos del shell que está usando.

1.  Una vez que haya terminado de configurarlo, abra un terminal y ejecute `ngrok http -host-header=rewrite 3978` . 

    Ahora ngrok le proporciona una dirección URL pública y segura que reenvía a su host local en el puerto 3978, por lo que copie la dirección URL HTTPS, por ejemplo, como se muestra en la captura de pantalla siguiente, ya que Teams requiere conexiones `https://287a4f4223bc.ngrok.io` HTTPS: 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Captura de pantalla que muestra el túnel de localhost con ngrok.":::

1. Registra la dirección URL en el manifiesto de la aplicación. 

## <a name="4-register-your-bot-endpoint"></a>4. Registrar el extremo del bot

Para usar un bot en Teams, debe registrarlo con el Servicio de bots de Azure. Esto se realiza automáticamente al configurar la aplicación con Teams Toolkit.

Todavía debe especificar una dirección de extremo para recibir y procesar mensajes de usuario, o solicitudes, enviados al bot. Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` de . Puede configurarlo rápidamente en el kit de herramientas.

1. En Visual Studio code, abra **Microsoft Teams Toolkit**.
1. Seleccione **Bots**  >  **Registros de bots existentes** y seleccione el bot que creó durante la instalación. 
1. En el **campo Dirección del extremo bot,** escriba la dirección URL de ngrok, por ejemplo, , donde hospeda el bot y `https://287a4f4223bc.ngrok.io` `/api/messages` anexe a él:

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Captura de pantalla que muestra cómo túnel localhost con ngrok.":::

    El bot podrá responder a los mensajes en Teams, después de configurar el punto de conexión correctamente. 

## <a name="5-build-and-run-your-app"></a>5. Crear y ejecutar la aplicación

Configuró una dirección URL para hospedar el bot y la configuró para controlar los mensajes. Es hora de que la aplicación esté en funcionamiento.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecute `npm start` .

   Si se realiza correctamente, verá el siguiente mensaje que indica que el bot está escuchando la actividad en su `localhost` :

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Instalación local del bot en Teams

Con el bot en ejecución, puedes instalarlo en Teams.

> [!TIP]
> Si no has descargado previamente una aplicación de Teams y tienes problemas, sigue estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).

1. En Visual Studio, seleccione la **tecla F5** para iniciar un cliente web de Teams.
1. En el cuadro de diálogo de instalación de la aplicación, **selecciona Agregar para mí**. 

   > [!Note]
   > De forma predeterminada, la aplicación se agrega a tu mensaje de chat directo 1:1, pero puedes elegir instalarla en un equipo o chat haciendo clic en la pequeña flecha junto a Agregar **para mí**. En este tutorial, vamos a hacer clic en Agregar.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Captura de pantalla que muestra el túnel localhost con ngrok.":::

## <a name="7-test-your-bot"></a>7. Probar el bot

Vamos a decir "Hola" al bot.

* En el cuadro redacción, envíe un `Hello` mensaje.
    El bot responde con algo parecido al siguiente mensaje:

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Captura de pantalla que muestra a un usuario decir &quot;Hola&quot; a un bot de Teams y obtener una respuesta.":::

    Ahora ha creado un bot básico de Teams que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats) 🎉

## <a name="troubleshoot-your-bot"></a>Solucionar problemas del bot

La siguiente información puede ayudar si tiene problemas para completar este tutorial.

### <a name="bot-isnt-connected-to-teams"></a>Bot no está conectado a Teams


Si has instalado la aplicación pero el bot no funciona, asegúrate de que el bot está conectado al canal teams del Servicio de [bots de Azure.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Es importante comprender que esto no es lo mismo que un canal en Teams. En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones compatible con Microsoft o [de terceros.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="see-also"></a>Consulte también

* [Conceptos básicos del bot](../bots/bot-basics.md)
* [Crear una pestaña personal para Microsoft Teams](../build-your-first-app/build-personal-tab.md)
* [Ver qué más pueden hacer los bots de Teams con uno de nuestros ejemplos](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Conceptos básicos de las conversaciones de bot](../bots/how-to/conversations/conversation-basics.md)
* [Directrices de diseño](../bots/design/bots.md) 
* [Plantillas de interfaz de usuario listas para producción](../concepts/design/design-teams-app-ui-templates.md)
* [Autenticación de bot en Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [Crear un bot sin el kit de herramientas](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una extensión de mensajería](../build-your-first-app/build-messaging-extension.md)
