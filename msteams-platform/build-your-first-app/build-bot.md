---
title: 'Introducción: crear un bot'
author: heath-hamilton
description: Cree rápidamente un bot de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: fbabd5130f0b7eb648a980f5f143792cc4c17933
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911950"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

En este tutorial, compilarás una *aplicación de bot* básica. Un bot actúa como intermediario entre los usuarios de Teams y su servicio web. Los usuarios pueden chatear con un bot para obtener rápidamente información o iniciar flujos de trabajo y tareas realizadas por el servicio.

## <a name="your-assignment"></a>Su asignación

Su lugar de trabajo creó una aplicación de Teams que usa [pestañas](../build-your-first-app/build-personal-tab.md) para destacar información de contacto importante. Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de ayuda. Pero en lugar de llamar, ¿qué ocurre si los contactos pudieran ponerse en contacto con el servicio de soporte con un chatbot? Su jefe le pide que vea la rapidez con la que puede obtener un bot de conversación básico en Funcionamiento en Teams.

## <a name="what-youll-learn"></a>Lo que aprenderás

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación y un bot con Microsoft Teams Toolkit for Visual Studio Code
> * Identificar algunas de las configuraciones de aplicaciones y scaffolding relevantes para los bots
> * Hospedar una aplicación localmente
> * Configurar un bot para Teams
> * Instalación de prueba y instalación de prueba de un bot en Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese de comprender [e instalar los requisitos previos de](build-first-app-overview.md#get-prerequisites)desarrollo de Teams.

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para su aplicación:

* **Configuraciones de aplicaciones y scaffolding relevantes** para bots
* **Bot** que se registra automáticamente con el servicio de bot de Microsoft Azure

> [!TIP]
> Si no ha creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que le sea útil seguir estas instrucciones que explican los proyectos con más detalle.

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Crear una nueva aplicación :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: de **Teams.**
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.
1. En la **pantalla Agregar funcionalidades,** seleccione **Bot** y, a **continuación, Siguiente.**
1. Escriba un nombre para su aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).
1. Vaya a **Configurar bot y** seleccione Crear un nuevo bot **y, a** continuación, cree el registro del **bot.** Si se realiza correctamente, el nuevo bot tendrá el **estado Registrado.**
1. Seleccione **Finalizar** en la parte inferior de la pantalla y elija una ubicación para crear el proyecto.

## <a name="2-identify-relevant-app-project-components"></a>2. Identificar componentes relevantes del proyecto de aplicación

Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit. Veamos los componentes principales para crear un bot.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

Para ver o actualizar las configuraciones del bot, seleccione **App Studio** en el kit de herramientas y vaya **a Bots.**

### <a name="app-scaffolding"></a>Scaffolding de aplicaciones

El scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar cómo el bot procesa las actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como `botActivityHandler.js` "Hola").

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurar un túnel seguro para la aplicación

Con fines de prueba, vamos a hospedar la aplicación en un servidor web local (puerto 3978).

1. Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).
1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ), ya que Teams requiere conexiones HTTPS.

Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá túnel hasta donde hospeda la aplicación (en el puerto `localhost` 3978).

## <a name="4-configure-your-bot"></a>4. Configurar el bot

Para usar un bot en Teams, debe registrarlo con el servicio de bots de Azure. Para usted, esto se realiza automáticamente al configurar la aplicación con el Kit de herramientas de Teams.

Debe especificar una dirección de extremo para recibir y procesar mensajes de usuario (es decir, solicitudes) enviados al bot. Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` . Puedes configurarlo rápidamente en el kit de herramientas.

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Abrir Microsoft :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: Teams **Toolkit.**
1. Vaya a **Bots > registros de bots existentes** y seleccione el bot que creó durante la instalación.
1. En el **campo de dirección** del extremo del bot, escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del punto de conexión del bot en el Kit de herramientas de Teams.":::

El bot podrá responder a los mensajes en Teams.

## <a name="5-build-and-run-your-app"></a>5. Compilar y ejecutar la aplicación

Ha configurado una dirección URL para hospedar el bot y la ha configurado para que controle los mensajes. Es el momento de que la aplicación esté en funcionamiento.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecute `npm start` .

Si se realiza correctamente, verá el siguiente mensaje que indica que el bot está escuchando la actividad en `localhost` su:

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Instalación local del bot en Teams

Con el bot en ejecución, puede instalarlo en Teams.

> [!TIP]
> Si no ha descargado localmente una aplicación de Teams antes y tiene problemas, siga estas [instrucciones.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.
1. En el cuadro de diálogo de instalación de la aplicación, **seleccione Agregar para mí.** (Puede agregar el bot a un canal o chat, pero es menos intrusivo para otros probar un bot en un chat uno a uno).

## <a name="7-test-your-bot"></a>7. Probar el bot

Ahora para la parte divertida: vamos a decir "Hola" al bot.

1. En el cuadro de redacción, envíe un `Hello` mensaje.

El bot responde con algo parecido al siguiente mensaje.

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Captura de pantalla que muestra a un usuario decir &quot;Hola&quot; a un bot de Teams y obtener una respuesta.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene un bot básico de Teams que puede comunicarse con usuarios de uno en uno o en la configuración de grupo (canales y chats).

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede resultar útil si tiene problemas para completar este tutorial.

### <a name="bot-isnt-connected-to-teams"></a>El bot no está conectado a Teams

Si ha instalado la aplicación pero el bot no funciona, asegúrese de que el bot está conectado al canal de Teams del Servicio de [bots de Azure.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Es importante comprender que esto no es lo mismo que un canal en Teams. En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones de Microsoft o de [terceros compatible.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="learn-more"></a>Más información

* [Ver qué más pueden hacer los bots de Teams con uno de nuestros ejemplos](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Conceptos básicos de las conversaciones de bot](../bots/how-to/conversations/conversation-basics.md)
* Sigue nuestras [directrices de diseño](../bots/design/bots.md) y compila con [plantillas de interfaz](../concepts/design/design-teams-app-ui-templates.md) de usuario listas para producción para crear una experiencia sin problemas.
* [Autenticación de bots en Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [Crear un bot sin el kit de herramientas](../bots/how-to/create-a-bot-for-teams.md)
