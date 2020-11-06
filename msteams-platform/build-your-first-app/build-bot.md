---
title: 'Introducción: creación de un bot'
author: heath-hamilton
description: Cree rápidamente un bot de Microsoft Teams con el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931745"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

Compilará una aplicación de *Bot* básica en este tutorial. Un bot actúa como intermediario entre los usuarios de Microsoft Teams y el servicio Web. Los usuarios pueden chatear con un bot para obtener información o iniciar flujos de trabajo y tareas realizados por el servicio de forma rápida.

## <a name="your-assignment"></a>La asignación

El área de trabajo ha creado una aplicación de Microsoft teams que usa [pestañas](../build-your-first-app/build-personal-tab.md) para exponer información de contacto importante. Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de asistencia. Pero, en lugar de llamar a, ¿qué sucede si los usuarios pueden ponerse en contacto con el Departamento de soporte mediante un Chatbot? Su jefe le pedirá que consulte la velocidad con la que puede poner en marcha un bot de conversación básico en Microsoft Teams.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación y un bot con el kit de herramientas de Microsoft Teams para Visual Studio Code
> * Identificar algunas de las configuraciones de aplicación y scaffolding relevantes para los bots
> * Hospedar una aplicación localmente
> * Configurar un bot para Teams
> * Transferir localmente y probar un bot en Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).

## <a name="1-create-your-app-project"></a>1. crear un proyecto de aplicación

El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes de la aplicación:

* **Configuraciones de aplicación y scaffolding** relevantes para bots
* **Bot** que se registra automáticamente con el servicio de robots de Microsoft Azure

> [!TIP]
> Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de 365 de Microsoft.
1. En la pantalla **Agregar funciones** , seleccione **Bot** y, a continuación, **siguiente**.
1. Escriba un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).
1. Vaya a **configurar bot** y seleccione **crear un nuevo bot** y, a continuación, **cree un registro de bot**. Si se ejecuta correctamente, el nuevo bot tendrá un estado **registrado** .
1. Seleccione **Finalizar** en la parte inferior de la pantalla y elija una ubicación para crear el proyecto.

## <a name="2-identify-relevant-app-project-components"></a>2. identificar los componentes relevantes del proyecto de aplicación

Una gran parte de la configuración de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams. Echemos un vistazo a los componentes principales para crear un bot.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

Para ver o actualizar las configuraciones de los bot, seleccione **App Studio** en el kit de herramientas y vaya a **bots**.

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

El scaffolding de la aplicación proporciona un `botActivityHandler.js` archivo, que se encuentra en el directorio raíz del proyecto, para controlar cómo el bot procesa las actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como "Hello").

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. configurar un túnel seguro a la aplicación

Para fines de prueba, vamos a hospedar la aplicación en un servidor Web local (puerto 3978).

1. Si todavía no lo ha hecho, instale [ngrok](https://ngrok.com/download).
1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ), ya que Teams requiere conexiones https.

Con esta dirección URL, Teams (que requiere Conexiones HTTPS) podrá canalizar a donde se hospeda la aplicación ( `localhost` en el puerto 3978).

## <a name="4-configure-your-bot"></a>4. configurar el bot

Para usar un bot en Teams, debe registrarlo con el servicio de bot de Azure. Por suerte, esto se realiza automáticamente al configurar la aplicación con el kit de herramientas de Teams.

Todavía debe especificar una dirección de extremo para recibir y procesar los mensajes de usuario (por ejemplo, solicitudes) enviados al bot. Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` . Puede configurar esto rápidamente en el kit de herramientas.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. Vaya a **Bots > registros de bot existentes** y seleccione el bot que creó durante la instalación.
1. En el campo **dirección del extremo del bot** , escriba la dirección URL de ngrok (por ejemplo, `https://468b9ab725e9.ngrok.io` ) donde hospeda el bot y agréguelo `/api/messages` a él.<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del punto de conexión del bot en el kit de herramientas de Teams.":::

El bot podrá responder a los mensajes de Microsoft Teams.

## <a name="5-build-and-run-your-app"></a>5. compilar y ejecutar la aplicación

Ha configurado una dirección URL para hospedar el bot y configurarlo para administrar mensajes. Es el momento de poner en marcha su aplicación.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecutar `npm start` .

Si se ejecuta correctamente, verá el siguiente mensaje que indica que el bot está escuchando la actividad en `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. transferir localmente el bot a Microsoft Teams

Con el bot ejecutándose, puede instalarlo en Teams.

> [!TIP]
> Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).

1. En Visual Studio Code, presione la tecla **F5** para iniciar un cliente web de Teams.
1. En el cuadro de diálogo de instalación de la aplicación, seleccione **Agregar a mí**. (Podría agregar el bot a un canal o un chat, pero es menos intrusivo para que otros puedan probar un bot en un chat único).

## <a name="7-test-your-bot"></a>7. probar el bot

Ahora es la parte divertida: digamos "Hola" a su bot.

1. En el cuadro de redacción, envíe un `Hello` mensaje.

El bot responde con algo parecido al siguiente mensaje.

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Una captura de pantalla que muestra un usuario diga ' Hello ' a un bot de Teams y obtenga una respuesta.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene un bot básico de teams que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats).

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.

### <a name="bot-isnt-connected-to-teams"></a>Bot no está conectado a Microsoft Teams

Si ha instalado la aplicación pero el bot no funciona, asegúrese de que el bot esté [conectado al *canal* Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Es importante comprender que no es lo mismo que un canal en Microsoft Teams. En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>Más información

* [Ver qué otros bots de Teams pueden hacer con una de nuestras muestras](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Conceptos básicos de las conversaciones de bot](../bots/how-to/conversations/conversation-basics.md)
* [Autenticación de bot en Microsoft Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
* [Crear un bot sin el kit de herramientas](../bots/how-to/create-a-bot-for-teams.md)
