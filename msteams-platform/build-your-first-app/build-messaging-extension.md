---
title: 'Introducción: compilación de una extensión de mensajería'
author: heath-hamilton
description: Cree rápidamente una extensión de mensajería de Microsoft Teams con el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: b19856eacee866ebbc89f21ac12575f1392918b3
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452837"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>Crear una extensión de mensajería para Microsoft Teams

Hay dos tipos de extensiones de *Mensajería*de Teams: [comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) y [comandos de acciones](../messaging-extensions/how-to/action-commands/define-action-command.md).

En esta lección, creará un *comando de búsqueda* (también conocido como *extensión de mensajería basada en búsquedas*), que es un método abreviado para buscar contenido externo y compartirlo en Microsoft Teams. Los usuarios pueden tener acceso a los comandos de búsqueda desde el [cuadro redactar o comando de Teams](../messaging-extensions/what-are-messaging-extensions.md).

## <a name="your-assignment"></a>La asignación

El Departamento de soporte técnico de su organización se comunica con los usuarios a través de Microsoft Teams, pero los vales residen en un sistema independiente. Esto significa que el personal de soporte técnico debe volver y avanzar entre las aplicaciones constantemente. Investigará cómo se puede reducir este gran cambio de contexto mediante la creación de una extensión de mensajería sencilla basada en búsquedas para Microsoft Teams.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
>
> * Crear un bot de extensión de mensajería y un proyecto de aplicación con el kit de herramientas de Microsoft Teams para Visual Studio Code
> * Identificar las propiedades del manifiesto de la aplicación y algunos de los scaffolding relevantes para las extensiones de mensajería
> * Hospedar una aplicación localmente
> * Configurar el bot para la extensión de mensajería
> * Transferir localmente y probar una extensión de mensajería en Microsoft Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).

## <a name="1-create-your-app-project"></a>1. crear un proyecto de aplicación

El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes para su extensión de mensajería:

* **Manifiesto de la aplicación y scaffolding** relevantes para las extensiones de mensajería
* **Bot** para la extensión de mensajería que se registra automáticamente con el servicio de robots de Microsoft Azure

> [!TIP]
> Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. Escriba un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).
1. En la pantalla **Agregar funcionalidad** , seleccione **extensión de mensajería** y, a continuación, **siguiente**.
1. En la pantalla **configurar la extensión de mensajería** , haga lo siguiente:
    1. Elija solo la opción **basada en búsquedas** para el tipo de extensión de mensajería.
    1. Seleccione **crear un nuevo bot** e **iniciar sesión** para iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.
    1. Almacene el identificador y la contraseña de su Bot (necesita esto un poco más adelante).
    1. Opcional Escriba un nombre personalizado para el bot y seleccione **crear**. (No es el nombre de la aplicación de teams que ya ha especificado.)
    1. Por ahora, seleccione **no** para la opción vincular unfurling.</br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot para la extensión de mensajería.":::
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="2-identify-relevant-app-project-components"></a>2. identificar los componentes relevantes del proyecto de aplicación

La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.

### <a name="app-manifest"></a>Manifiesto de la aplicación

El siguiente fragmento de código del manifiesto de la aplicación (el `manifest.json` archivo del `.publish` directorio del proyecto) muestra las propiedades y los valores predeterminados relevantes para las extensiones de mensajería.

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

Vamos a comprender algunas de las propiedades creadas por el kit de herramientas. (Vea la lista completa de propiedades admitidas [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) ).

* `botId`: El identificador del robot que ha creado configurando su proyecto. (Almacenado en `{botId0}` , puede encontrar el identificador real en `Development.env` ).
* `commands`: Comandos disponibles para la extensión de mensajería. El kit de herramientas le proporciona scaffolding para un comando de búsqueda.
* `context`: Donde los usuarios pueden invocar la extensión de mensajería. En este caso, puede iniciar la extensión de mensajería desde el cuadro redactar o comando de Microsoft Teams.
* `description`: Texto de la ayuda de la interfaz de usuario que indica lo que hace el comando o cómo usarlo.
* `parameters`: Incluye todos los parámetros que acepta un comando (debe tener al menos un y puede tener hasta cinco).
* `parameters.description`: Texto de ayuda de interfaz de usuario que describe el propósito del parámetro o la entrada de ejemplo.

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

La aplicación scaffolding incluye un `.env` archivo, ubicado en el directorio raíz del proyecto, que almacena el identificador y la contraseña del bot de la extensión de mensajería.

También en el directorio raíz hay un `botActivityHandler.js` archivo para controlar cómo su extensión de mensajería (técnicamente, el [Bot de la extensión de mensajería](#4-configure-the-bot-for-your-messaging-extension)) responde a las consultas de búsqueda en Microsoft Teams.

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. configurar un túnel seguro a la aplicación

Para fines de prueba, vamos a hospedar su extensión de mensajería en un servidor Web local (puerto 3978).

1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado, ya que Teams requiere Conexiones HTTPS.
1. En el `.publish` directorio, Abra `Development.env` .
1. Reemplace el `baseUrl0` valor por la dirección URL copiada. (Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ca5.ngrok.io` ).

El manifiesto de la aplicación apunta al lugar donde se hospeda el bot usado por la extensión de mensajería.

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. configurar el bot para la extensión de mensajería

Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario de Microsoft Teams en el servicio hospedado.

El bot debe estar registrado en el servicio de bot de Azure, que se ha realizado al configurar la aplicación con el kit de herramientas de Teams.

### <a name="specify-your-bot-id-and-password"></a>Especificar el identificador de robot y la contraseña

Cuando se registra el bot con el servicio de robots de Azure, se le asigna un identificador y una contraseña que la aplicación de Teams debe conocer.

1. Busque el identificador de robot y la contraseña que almacenó durante la instalación del kit de herramientas.
1. En el directorio raíz, abra el `.env` archivo.
1. Establezca el identificador y la contraseña de bot en las `BotId` `BotPassword` propiedades y, respectivamente.

### <a name="add-the-bot-endpoint-address"></a>Agregar la dirección de punto de conexión de bot

Debe especificar una dirección URL de punto de conexión de bot para recibir y procesar consultas de búsqueda en su extensión de mensajería. Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` . Puede configurar esto rápidamente en el kit de herramientas de Microsoft Teams.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. Vaya a **Administración de bot > registros de bot existentes** y seleccione el bot que creó durante la instalación.
1. En el campo **dirección de extremo del bot** , escriba el servidor Web local en el que hospeda el bot ( `baseUrl10` valor) y agréguelo `/api/messages` .

El bot podrá controlar las consultas en su extensión de mensajería.

## <a name="5-run-your-app"></a>5. ejecutar la aplicación

Configuró una dirección URL para hospedar la extensión de mensajería y configurarla para controlar las búsquedas. Es el momento de poner en marcha su aplicación.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecutar `npm start` .

Si se ejecuta correctamente, verá algo parecido al siguiente mensaje que indica que el servicio de extensiones de mensajería está escuchando la actividad en `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. transferir localmente la extensión de mensajería en Microsoft Teams

Con la extensión de mensajería en ejecución, puede instalarla en Teams.

> [!TIP]
> Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).

1. Inicie sesión en el cliente de Teams con su cuenta que permite la transferencia local de aplicaciones.
1. Seleccione **aplicaciones**y, después, elija **cargar una aplicación personalizada**.
1. Vaya a la carpeta de proyecto de la aplicación `.publish` y seleccione `Development.zip` .
1. En el modal instalar, seleccione **Agregar** para instalar la aplicación.

## <a name="7-test-your-messaging-extension"></a>7. probar la extensión de mensajería

Obtenga información sobre cómo funcionan las extensiones de mensajería en un chat de Microsoft Teams.

1. Inicie un nuevo chat. En el cuadro de redacción, seleccione **más** :::image type="icon" source="../assets/icons/teams-client-more.png"::: y elija la aplicación de extensión de mensajería que acaba de transferirá localmente.<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot para la extensión de mensajería.":::
1. Intente buscar algo (por ejemplo, "vales"). Si la aplicación funciona, verá los resultados de la búsqueda de ejemplo (puede Agregar los suyos propios más adelante).<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Ilustración que muestra cómo, en Team Toolkit, iniciar sesión en su cuenta de Microsoft 365 para crear un nuevo bot para la extensión de mensajería.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una extensión de mensajería básica de teams que está configurada para buscar contenido externo en el cuadro de redacción o comando.

## <a name="next-steps"></a>Pasos siguientes

Vea las siguientes páginas para continuar y crear una extensión de mensajería con características completas:

1. [Definir los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) relevantes para el servicio.
1. Configurar el servicio para que [responda a las búsquedas de los usuarios](../messaging-extensions/how-to/search-commands/respond-to-search.md).

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.

### <a name="toolkit-setup-fails"></a>Error en la instalación del kit de herramientas

Al configurar el proyecto de la aplicación con Team Toolkit, obtiene un error después de seleccionar la opción **crear un nuevo bot** e iniciar sesión con su cuenta de desarrollo de 365 de Microsoft.

Podría ser un problema de autenticación. Siga estos pasos para finalizar la configuración del proyecto.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **Cerrar sesión**.
1. Vuelva a pasar por el proceso de instalación iniciando sesión con la misma cuenta y creando un nuevo bot.

### <a name="bot-isnt-connected-to-teams"></a>Bot no está conectado a Microsoft Teams

Si ha instalado la aplicación pero no funciona, asegúrese de que el bot de la extensión de mensajería esté [conectado al *canal*de Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Es importante comprender que no es lo mismo que un canal en Microsoft Teams. En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>Más información

* [Incluir una característica de unfurling de vínculos](../messaging-extensions/how-to/link-unfurling.md)
* [Agregar autenticación](../messaging-extensions/how-to/add-authentication.md)
* [Crear una extensión de mensajería basada en acciones](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
