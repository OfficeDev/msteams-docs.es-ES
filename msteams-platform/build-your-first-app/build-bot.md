---
title: Crear un bot de Teams
author: heath-hamilton
description: Obtenga información sobre cómo crear un bot para su primera aplicación de Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: 7d3d1b63aace7fda971fb6ccaddddf631b4b2ad9
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210305"
---
# <a name="build-a-teams-bot"></a>Crear un bot de Teams

Compilará una aplicación de *Bot* básica en este tutorial. Un bot actúa como intermediario entre los usuarios de Microsoft Teams y el servicio Web. Los usuarios pueden chatear con un bot para obtener información o iniciar flujos de trabajo y tareas realizados por el servicio de forma rápida.

## <a name="your-assignment"></a>La asignación

El área de trabajo ha estado usando [pestañas](../build-your-first-app/build-personal-tab.md) para exponer la información de contacto importante en Microsoft Teams. Por ejemplo, los compañeros tienen acceso rápido al número de teléfono del servicio de asistencia. Pero, en lugar de llamar a, ¿qué sucede si los usuarios pueden ponerse en contacto con el Departamento de soporte mediante un Chatbot? Su jefe le pedirá que consulte la velocidad con la que puede poner en marcha un bot de conversación básico en Microsoft Teams.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación y un bot con el kit de herramientas de Microsoft Teams para Visual Studio Code
> * Identificar algunas de las propiedades del manifiesto de la aplicación y los scaffolding relevantes para los bots
> * Hospedar una aplicación localmente
> * Configurar un bot para Teams
> * Transferir localmente y probar un bot en Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).

## <a name="create-your-app-project"></a>Crear el proyecto de la aplicación

El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes de la aplicación:

* **Manifiesto de la aplicación y scaffolding** relevantes para bots
* **Bot** que se registra automáticamente con el servicio de robots de Microsoft Azure

> [!TIP]
> Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. Escriba un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).
1. En la pantalla **Agregar funciones** , seleccione **Bot** y, a continuación, **siguiente**.
1. Seleccione **crear un nuevo bot** e **iniciar sesión** para iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.<br/>
:::image type="content" source="../assets/images/build-your-first-app/vsc-create-bot.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot.":::
1. Almacene el identificador y la contraseña de su Bot (necesita esto un poco más adelante).
1. Opcional Escriba un nombre personalizado para el bot y seleccione **crear**. Recuerde que este es el nombre de su bot y no el nombre de la aplicación de teams que ya ha especificado.
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="identify-relevant-app-project-components"></a>Identificar los componentes relevantes del proyecto de aplicación

La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams. Echemos un vistazo a los componentes principales para crear un bot.

### <a name="app-manifest"></a>Manifiesto de la aplicación

El siguiente fragmento de código del manifiesto de la aplicación (el `manifest.json` archivo del `.publish` directorio del proyecto) muestra las propiedades y los valores predeterminados pertinentes para los bots.

```JSON
"bots": [
    {
        "botId": "{botId0}",
        "scopes": [
            "personal",
            "groupchat",
            "team"
        ],
        "supportsFiles": false,
        "isNotificationOnly": false,
        "commandLists": [
            {
                "scopes": [
                    "personal",
                    "groupchat",
                    "team"
                ],
                "commands": [
                    {
                        "title": "Hello",
                        "description": "Sends a hello message and @mention the sender"
                    }
                ]
            }
        ]
    }
],
```

Por ahora, vamos a centrarnos en las siguientes propiedades necesarias. (Vea la lista completa de propiedades admitidas [`bots`](../resources/schema/manifest-schema.md#bots) ).

* `botId`: El identificador del robot que ha creado configurando su proyecto. (Almacenado en `{botId0}` , puede encontrar el identificador real en `Development.env` ).
* `scopes`: Especifica si el bot está disponible en `personal` los `groupchat` `team` contextos,, o (por ejemplo, de canal).
* `commands`: Comandos disponibles que los usuarios pueden enviar a su bot.
* `title`: Nombre del comando bot que se muestra en el cliente de Microsoft Teams.
* `description`: Una breve descripción o un ejemplo de la sintaxis y los argumentos para ayudar a los usuarios a comprender lo que hace un comando bot.

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

El scaffolding de la aplicación proporciona un `botActivityHandler.js` archivo, que se encuentra en el directorio raíz del proyecto, para controlar cómo el bot procesa las actividades en Teams (por ejemplo, cómo responde el bot a mensajes específicos como "Hello").

El `.env` archivo, también en el directorio raíz, almacena el identificador de Bot y la contraseña.

## <a name="set-up-a-secure-tunnel-to-your-app"></a>Configurar un túnel seguro para la aplicación

Para fines de prueba, vamos a hospedar su bot en un servidor Web local (puerto 3978).

1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado, ya que Teams requiere Conexiones HTTPS.
1. En el `.publish` directorio, Abra `Development.env` .
1. Reemplace el `baseUrl0` valor por la dirección URL copiada. (Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ca5.ngrok.io` ).

El manifiesto de la aplicación apunta al lugar donde se hospeda el bot.

## <a name="configuring-your-bot"></a>Configurar el bot

Para usar un bot en Teams, debe registrarlo con el servicio de bot de Azure. Por suerte, esto se realiza automáticamente al configurar la aplicación con el kit de herramientas de Teams.

### <a name="specify-your-bot-id-and-password"></a>Especificar el identificador de robot y la contraseña

Cuando se registra el bot con el servicio de robots de Azure, se le asigna un identificador y una contraseña que la aplicación de Teams debe conocer.

1. Busque el identificador de robot y la contraseña que almacenó durante la instalación del kit de herramientas.
1. En el directorio raíz, abra el `.env` archivo.
1. Agregue el identificador de Bot y la contraseña a `BotId` y `BotPassword` , respectivamente.

### <a name="add-the-bot-endpoint-address"></a>Agregar la dirección de punto de conexión de bot

Debe especificar una dirección URL de punto de conexión para recibir y procesar los mensajes de usuario (por ejemplo, solicitudes) enviados al bot. Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` . Puede configurar esto rápidamente en el kit de herramientas de Microsoft Teams.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. Vaya a **Administración de bot > registros de bot existentes** y seleccione el bot que creó durante la instalación.
1. En el campo **dirección de extremo del bot** , escriba el servidor Web local en el que hospeda el bot ( `baseUrl10` valor) y agréguelo `/api/messages` .

    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Ilustración que muestra dónde puede configurar la dirección URL del punto de conexión del bot en el kit de herramientas de Teams.":::

El bot podrá responder a los mensajes de Microsoft Teams.

## <a name="run-your-app"></a>Ejecutar la aplicación

Ha configurado una dirección URL para hospedar el bot y configurarlo para administrar mensajes. Es el momento de poner el bot en marcha.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecutar `npm start` .

Si se ejecuta correctamente, verá algo parecido al siguiente mensaje que indica que el bot está escuchando actividades en `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a>Transferir localmente el bot en Microsoft Teams

Con el bot ejecutándose, puede instalarlo en Teams.

> [!TIP]
> Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).

1. Inicie sesión en el cliente de Teams con su cuenta que permite la transferencia local de aplicaciones.
1. Seleccione **aplicaciones**y, después, elija **cargar una aplicación personalizada**.
1. Vaya a la carpeta de proyecto de la aplicación `.publish` y seleccione `Development.zip` .
1. En el modal instalar, seleccione **Agregar** para instalar la aplicación.

## <a name="test-your-bot"></a>Probar el bot

Ahora es la parte divertida: digamos "Hola" a su bot en un chat de uno a uno.

1. En Microsoft Teams, seleccione **más** :::image type="icon" source="../assets/icons/teams-client-more.png"::: en el lado izquierdo.
1. Busque y seleccione el bot al que acaba de hacer una transtransferida localmente.<br/>
   :::image type="content" source="../assets/images/build-your-first-app/bot-teams-access.png" alt-text="Ilustración que muestra dónde obtener acceso a su bot en Teams.":::
1. En el cuadro de redacción, envíe un `Hello` mensaje.

El bot responde con algo parecido al siguiente mensaje.

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Una captura de pantalla que muestra un usuario diga ' Hello ' a un bot de Teams y obtenga una respuesta.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene un bot básico de teams que puede comunicarse con los usuarios uno a uno o en la configuración de grupo (canales y chats).

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.

### <a name="toolkit-setup-fails"></a>Error en la instalación del kit de herramientas

Al configurar el proyecto de la aplicación con Team Toolkit, obtiene un error después de seleccionar la opción **crear un nuevo bot** e iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.

Podría ser un problema de autenticación. Siga estos pasos para finalizar la configuración del proyecto.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **Cerrar sesión**.
1. Vuelva a pasar por el proceso de instalación iniciando sesión con la misma cuenta y creando un nuevo bot.

### <a name="bot-isnt-connected-to-teams"></a>Bot no está conectado a Microsoft Teams

Si ha instalado la aplicación pero el bot no funciona, asegúrese de que el bot esté [conectado al *canal*Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Es importante comprender que no es lo mismo que un canal en Microsoft Teams. En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>Obtén más información

* [Ver qué otros bots de Teams pueden hacer con una de nuestras muestras](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Conceptos básicos de las conversaciones de bot](../bots/how-to/conversations/conversation-basics.md)
* [Autenticación de bot en Microsoft Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
* [Crear un bot sin el kit de herramientas](../bots/how-to/create-a-bot-for-teams.md)
