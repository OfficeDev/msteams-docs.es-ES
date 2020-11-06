---
title: 'Introducción: compilación de una extensión de mensajería'
author: heath-hamilton
description: Cree rápidamente una extensión de mensajería de Microsoft Teams con el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 160878d92969d57680e6fa25eb6fc13e82bf2a82
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931753"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>Crear una extensión de mensajería para Microsoft Teams

Hay dos tipos de *extensiones de mensajería* de la aplicación Teams: [comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) y comandos de [acciones](../messaging-extensions/how-to/action-commands/define-action-command.md).

En esta lección, creará un *comando de búsqueda* (también conocido como *extensión de mensajería basada en búsquedas* ), que es un método abreviado para buscar contenido externo y compartirlo en Microsoft Teams. Los usuarios pueden tener acceso a los comandos de búsqueda desde el [cuadro redactar o comando de Teams](../messaging-extensions/what-are-messaging-extensions.md).

## <a name="your-assignment"></a>La asignación

El Departamento de soporte técnico de su organización se comunica con los usuarios a través de Microsoft Teams, pero los vales residen en un sistema independiente. Esto significa que el personal de soporte técnico debe volver y avanzar entre las aplicaciones constantemente. Investigará cómo se puede reducir este gran cambio de contexto mediante la creación de una extensión de mensajería sencilla basada en búsquedas para Microsoft Teams.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
>
> * Crear un bot de extensión de mensajería y un proyecto de aplicación con el kit de herramientas de Microsoft Teams para Visual Studio Code
> * Identificar las configuraciones de la aplicación y algunos de los scaffolding relevantes para las extensiones de mensajería
> * Hospedar una aplicación localmente
> * Configurar el bot para la extensión de mensajería
> * Transferir localmente y probar una extensión de mensajería en Microsoft Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).

## <a name="1-create-your-app-project"></a>1. crear un proyecto de aplicación

El kit de herramientas de Microsoft Teams le ayudará a configurar los siguientes componentes para su extensión de mensajería:

* **Configuraciones de aplicación y scaffolding** relevantes para las extensiones de mensajería
* **Bot** para la extensión de mensajería que se registra automáticamente con el servicio de robots de Microsoft Azure

> [!TIP]
> Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de 365 de Microsoft.
1. En la pantalla **Agregar funcionalidad** , seleccione **extensión de mensajería** y, a continuación, **siguiente**.
1. Escriba un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).
1. En la pantalla **configurar la extensión de mensajería** , haga lo siguiente:
    1. Elija solo la opción **basada en búsquedas** para el tipo de extensión de mensajería.
    1. Seleccione **crear un nuevo bot** y, a continuación, **cree un registro de bot**. Si se ejecuta correctamente, el nuevo bot tendrá un estado **registrado** .
    1. Por ahora, seleccione **no** para la opción vincular unfurling.
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="2-identify-relevant-app-project-components"></a>2. identificar los componentes relevantes del proyecto de aplicación

Una gran parte de la configuración de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

Para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a **extensiones de mensajería**.

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

El scaffolding de la aplicación proporciona un `botActivityHandler.js` archivo, que se encuentra en el directorio raíz del proyecto, para controlar cómo su extensión de mensajería (técnicamente, el [Bot de la extensión de mensajería](#4-configure-the-bot-for-your-messaging-extension)) responde a las consultas de búsqueda en Microsoft Teams.

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. configurar un túnel seguro a la aplicación

Para fines de prueba, vamos a hospedar su extensión de mensajería en un servidor Web local (puerto 3978).

1. Si todavía no lo ha hecho, instale [ngrok](https://ngrok.com/download).
1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ), ya que Teams requiere conexiones https.

Con esta dirección URL, Teams (que requiere Conexiones HTTPS) podrá canalizar a donde se hospeda la aplicación ( `localhost` en el puerto 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. configurar el bot para la extensión de mensajería

Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario de Microsoft Teams en el servicio hospedado. El bot debe estar registrado en el servicio de bot de Azure, que se ha realizado al configurar la aplicación con el kit de herramientas de Teams.

Todavía debe especificar una dirección URL de punto de conexión de bot para recibir y procesar consultas de búsqueda en su extensión de mensajería. Normalmente, la dirección URL tiene el aspecto siguiente `https://HOST_URL/api/messages` . Puede configurar esto rápidamente en el kit de herramientas.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **abrir el kit de herramientas de Microsoft Teams**.
1. Vaya a **Bots > registros de bot existentes** y seleccione el bot que creó durante la instalación.
1. En el campo **dirección del extremo del bot** , escriba la dirección URL de ngrok (por ejemplo, `https://468b9ab725e9.ngrok.io` ) donde hospeda el bot y agréguelo `/api/messages` a él.

El bot podrá controlar las consultas en su extensión de mensajería.

## <a name="5-build-and-run-your-app"></a>5. compilar y ejecutar la aplicación

Configuró una dirección URL para hospedar la extensión de mensajería y configurarla para controlar las búsquedas. Es el momento de poner en marcha su aplicación.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecutar `npm start` .

Si se ejecuta correctamente, verá el siguiente mensaje que indica que el servicio de extensiones de mensajería está escuchando la actividad en `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. transferir localmente la extensión de mensajería en Microsoft Teams

Con la extensión de mensajería en ejecución, puede instalarla en Teams.

> [!TIP]
> Si no ha transferido localmente una aplicación de Microsoft Teams y tiene problemas, siga estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).

1. En Visual Studio Code, presione la tecla **F5** para iniciar un cliente web de Teams.
1. En el cuadro de diálogo de instalación de la aplicación, seleccione **Agregar a mí**.

## <a name="7-test-your-messaging-extension"></a>7. probar la extensión de mensajería

Obtenga información sobre cómo funcionan las extensiones de mensajería en un chat de Microsoft Teams.

1. Inicie un nuevo chat. En el cuadro redactar, seleccione **más** :::image type="icon" source="../assets/icons/teams-client-more.png"::: y elija la aplicación de extensión de mensajería que acaba de transferirá localmente.
1. Intente buscar algo (por ejemplo, **vales** ). Si la aplicación funciona, verá los resultados de la búsqueda de ejemplo (puede Agregar los suyos propios más adelante).<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Una captura de pantalla que muestra cómo se usa una extensión de mensajería basada en búsquedas en el cuadro de redacción de Teams.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una extensión de mensajería básica de teams que está configurada para buscar contenido externo en el cuadro de redacción o comando.

## <a name="next-steps"></a>Pasos siguientes

Vea las siguientes páginas para continuar y crear una extensión de mensajería con características completas:

1. [Definir los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) relevantes para el servicio.
1. Configurar el servicio para que [responda a las búsquedas de los usuarios](../messaging-extensions/how-to/search-commands/respond-to-search.md).

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede resultarle útil si tuvo problemas para completar este tutorial.

### <a name="bot-isnt-connected-to-teams"></a>Bot no está conectado a Microsoft Teams

Si ha instalado la aplicación pero no funciona, asegúrese de que el bot de la extensión de mensajería esté [conectado al *canal* de Teams del servicio de robots de Azure](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Es importante comprender que no es lo mismo que un canal en Microsoft Teams. En este caso, un canal es cómo el servicio bot de Azure conecta su bot con Teams u otra [aplicación de comunicaciones de terceros o de Microsoft compatible](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>Más información

* [Incluir una característica de unfurling de vínculos](../messaging-extensions/how-to/link-unfurling.md)
* [Agregar autenticación](../messaging-extensions/how-to/add-authentication.md)
* [Crear una extensión de mensajería basada en acciones](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
