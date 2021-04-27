---
title: 'Introducción: crear un bot'
author: heath-hamilton
description: Cree rápidamente un bot de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 5dfbfa05d2f1e36bbc14bd929cb2592303081522
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020003"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

Compilarás una *aplicación* bot básica en este tutorial. Un bot actúa como intermediario entre los usuarios de Teams y el servicio web. Los usuarios pueden chatear con un bot para obtener información rápidamente o iniciar flujos de trabajo y tareas realizados por el servicio.

## <a name="your-assignment"></a>Su asignación

El lugar de trabajo creó una aplicación de Teams que usa [pestañas para](../build-your-first-app/build-personal-tab.md) obtener información de contacto importante. Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de ayuda. Pero en lugar de llamar, ¿qué ocurre si las personas pudieran ponerse en contacto con el servicio de soporte con un chatbot? El jefe te pide que veas la rapidez con la que puedes hacer que un bot conversacional básico se ejecute en Teams.

## <a name="what-youll-learn"></a>Lo que aprenderás

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación y un bot con Microsoft Teams Toolkit for Visual Studio Code
> * Identificar algunas de las configuraciones de la aplicación y los scaffolding relevantes para bots
> * Hospedar una aplicación localmente
> * Configurar un bot para Teams
> * Instalación local y prueba de un bot en Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese de comprender e [instalar los requisitos previos](build-first-app-overview.md#get-prerequisites)de desarrollo de Teams .

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

Microsoft Teams Toolkit te ayuda a configurar los siguientes componentes para la aplicación:

* **Configuraciones de aplicaciones y scaffolding relevantes** para bots
* **Bot** que se registra automáticamente en el Servicio de bots de Microsoft Azure

> [!TIP]
> Si no has creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que te sea útil seguir estas instrucciones que explican los proyectos con más detalle.

1. En Visual Studio, selecciona **Microsoft Teams en** la barra de actividades izquierda y elige Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams**.
1. Cuando se le pida, inicie sesión con su cuenta de desarrollo de Microsoft 365.
1. En la **pantalla Agregar funcionalidades,** **seleccione Bot** y, a **continuación, Siguiente**.
1. Escribe un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).
1. Vaya a **Configurar bot y** seleccione Crear un nuevo bot **y, a** **continuación, Cree registro de bot.** Si se realiza correctamente, el nuevo bot tendrá un **estado Registrado.**
1. Seleccione **Finalizar** en la parte inferior de la pantalla y elija una ubicación para crear el proyecto.

## <a name="2-identify-relevant-app-project-components"></a>2. Identificar componentes relevantes del proyecto de aplicación

Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit. Veamos los componentes principales para crear un bot.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

Para ver o actualizar las configuraciones del bot, seleccione **App Studio** en el kit de herramientas y vaya a **Bots**.

### <a name="app-scaffolding"></a>Scaffolding de aplicaciones

El scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar el modo en que el bot procesa actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como `botActivityHandler.js` "Hello").

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurar un túnel seguro en la aplicación

Para realizar pruebas, vamos a hospedar la aplicación en un servidor web local (puerto 3978).

1. Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).
1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ) ya que Teams requiere conexiones HTTPS.

Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá realizar un túnel donde hospedas la aplicación ( en el `localhost` puerto 3978).

## <a name="4-configure-your-bot"></a>4. Configurar el bot

Para usar un bot en Teams, debe registrarlo con el Servicio de bots de Azure. Afortunadamente, esto se realiza automáticamente al configurar la aplicación con Teams Toolkit.

Todavía debe especificar una dirección de extremo para recibir y procesar los mensajes de usuario (es decir, solicitudes) enviados al bot. Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` de . Puede configurarlo rápidamente en el kit de herramientas.

1. En Visual Studio, seleccione **Microsoft Teams en** la barra de actividades izquierda y elija Abrir Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Toolkit**.
1. Ve a **Bots > Registros de bots existentes** y selecciona el bot que creaste durante la instalación.
1. En el **campo Dirección del extremo bot,** escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del extremo del bot en Teams Toolkit.":::

El bot podrá responder a mensajes en Teams.

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

1. En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.
1. En el cuadro de diálogo de instalación de la aplicación, **selecciona Agregar para mí**. (Puede agregar el bot a un canal o chat, pero es menos intrusivo para otros probar un bot en un chat uno a uno).

## <a name="7-test-your-bot"></a>7. Probar el bot

Ahora, para la parte divertida: vamos a decir "Hola" al bot.

1. En el cuadro redacción, envíe un `Hello` mensaje.

El bot responde con algo parecido al siguiente mensaje.

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Captura de pantalla que muestra a un usuario decir &quot;Hola&quot; a un bot de Teams y obtener una respuesta.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tienes un bot básico de Teams que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats).

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede ayudar si tiene problemas para completar este tutorial.

### <a name="bot-isnt-connected-to-teams"></a>Bot no está conectado a Teams

Si has instalado la aplicación pero el bot no funciona, asegúrate de que el bot está conectado al canal teams del Servicio de [bots de Azure.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Es importante comprender que esto no es lo mismo que un canal en Teams. En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones compatible con Microsoft o [de terceros.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="learn-more"></a>Más información

* [Ver qué más pueden hacer los bots de Teams con uno de nuestros ejemplos](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Conceptos básicos de las conversaciones de bot](../bots/how-to/conversations/conversation-basics.md)
* Siga nuestras [directrices de diseño](../bots/design/bots.md) y cree con [plantillas de](../concepts/design/design-teams-app-ui-templates.md) interfaz de usuario preparadas para producción para crear una experiencia perfecta.
* [Autenticación de bot en Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [Crear un bot sin el kit de herramientas](../resources/bot-v3/bots-create.md)
