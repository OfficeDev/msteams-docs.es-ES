---
title: 'Empezar : cree una extensión de mensajería'
author: girliemac
description: Cree rápidamente una extensión de mensajería Microsoft Teams mediante la Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: c120a5b5d878c549cde008c3e1ccc71743a4e24f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566064"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a>Cree su primera extensión de mensajería para Microsoft Teams

Hay dos tipos de extensiones de *mensajería* Teams: [comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) y comandos de [acción.](../messaging-extensions/how-to/action-commands/define-action-command.md)

En este tutorial se le enseña a crear un *comando de búsqueda* (también conocido como extensión de mensajería basada en *búsqueda),* que es un acceso directo para encontrar contenido externo y compartirlo en Teams. Los usuarios pueden acceder a comandos de búsqueda desde el cuadro de comando Teams compose o.

## <a name="what-youll-learn"></a>Lo que aprenderás

* Cree un proyecto de aplicación y un bot de extensión de mensajería mediante la Microsoft Teams Toolkit para Visual Studio Code.
* Comprender las configuraciones de la aplicación y el andamiaje relevante para las extensiones de mensajería.
* Hospede una aplicación localmente.
* Configure el bot para la extensión de mensajería.
* Descargue lateralmente y pruebe una extensión de mensajería en Teams.

## <a name="prerequisites"></a>Requisitos previos

Asegúrese de comprender cómo configurar y crear una aplicación de Teams sencilla. Para obtener más información, consulta [crear tu primera aplicación Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)

## <a name="1-create-your-app-project"></a>1. Cree el proyecto de la aplicación

El Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para la extensión de mensajería:

* **Configuraciones de aplicaciones y andamios** relevantes para las extensiones de mensajería.
* **Bot** para la extensión de mensajería que se registra automáticamente con el servicio de bots Microsoft Azure.

**Para crear el proyecto de aplicación**

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividades izquierda y elija Crear una nueva aplicación **de Teams**.
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.
1. En la pantalla **Seleccionar proyecto,** en Búsqueda **de extensiones de mensajería,** haga clic en  >   **JS (JavaScript).** 
1. Escriba un nombre para la aplicación Teams. Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.
1. Seleccione **Crear un nuevo bot** y, a continuación, haga clic en el botón Crear registro de **bots.** Si se realiza correctamente, el nuevo bot tendrá un estado *Registrado.* Ahora el bot se registra automáticamente con el servicio de bots de Microsoft Azure. 
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto y guardar el proyecto en el equipo local.

## <a name="2-understand-your-app-project-components"></a>2. Comprender los componentes del proyecto de la aplicación

Gran parte de las configuraciones de la aplicación y los andamios se configuran automáticamente al crear el proyecto con el Teams Toolkit.

* Configuraciones de aplicaciones: para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a Extensiones **de mensajería.**
* Andamios de aplicaciones: el andamiaje de la aplicación proporciona un `botActivityHandler.js` archivo, ubicado en el directorio raíz del proyecto, para controlar cómo responde la extensión de mensajería (o técnicamente, el bot de la [extensión de mensajería)](#4-configure-the-bot-for-your-messaging-extension)a las consultas de búsqueda en Teams.

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configure un túnel seguro a su aplicación

Para fines de prueba, vamos a hospedar la extensión de mensajería en un servidor web local (puerto 3978). Va a utilizar [ngrok](https://ngrok.com/download) para configurar un túnel seguro a localhost. Consulte [la compilación del primer bot para obtener Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) para obtener más información. 

1. Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).
1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en la salida (por ejemplo, `https://468b9ab725e9.ngrok.io` ) ya que Teams requiere conexiones HTTPS.

   Con esta DIRECCIÓN URL, Teams (que requiere conexiones HTTPS) podrán llegar a donde hospedas la aplicación `localhost` (en el puerto 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. Configure el bot para su extensión de mensajería

Las extensiones de mensajería se basan en bots para enviar y procesar solicitudes de usuario desde Teams al servicio hospedado. El bot debe registrarse en Azure Bot Service, que se realizó al configurar la aplicación mediante la Teams Toolkit.

Todavía debe especificar una dirección URL de punto de conexión de bot para recibir y procesar consultas de búsqueda en la extensión de mensajería. Normalmente, la dirección URL se parece `https://HOST_URL/api/messages` a . Puede configurar esto rápidamente en el kit de herramientas.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividades izquierda y elija Abrir **Microsoft Teams Toolkit**.
1. Vaya a **Bots > Registros de bots existentes** y seleccione el bot que creó durante la instalación.
1. En el campo **Dirección del punto de conexión del bot,** escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.

   El bot podrá controlar las consultas de la extensión de mensajería.

## <a name="5-build-and-run-your-app"></a>5. Compile y ejecute la aplicación

Ha configurado una dirección URL para hospedar la extensión de mensajería y la ha configurado para controlar las búsquedas. Es hora de poner en marcha la aplicación.

1. Abra el terminal y vaya al directorio raíz del proyecto de aplicación.
1. Ejecute `npm install`.
1. Ejecute `npm start`.

   Si se realiza correctamente, verá el siguiente mensaje que indica que el servicio de extensión de mensajería está escuchando la actividad `localhost` en:

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Descargue su extensión de mensajería en Teams

Con la extensión de mensajería en ejecución, puede instalarla en Teams.

> [!TIP]
> Si no has descargado una aplicación Teams antes y te has quedado con problemas, sigue estas [instrucciones.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. En Visual Studio Code, seleccione la clave **F5** para iniciar un cliente web Teams.
1. En el cuadro de diálogo de instalación de la aplicación, seleccione **Agregar para mí.**

## <a name="7-test-your-messaging-extension"></a>7. Pruebe su extensión de mensajería

Obtén información sobre cómo funcionan las extensiones de mensajería en un chat Teams.

1. Inicia un nuevo chat. En el cuadro de composición, seleccione **Más** :::image type="icon" source="../assets/icons/teams-client-more.png"::: y seleccione la aplicación de extensión de mensajería que acaba de descargar.
1. Intente buscar algo (por ejemplo, **Tickets).** Si la aplicación funciona, verás resultados de búsqueda de ejemplo (puedes agregar los tuyos más adelante).

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Una captura de pantalla que muestra cómo se utiliza una extensión de mensajería basada en búsqueda en el cuadro de composición Teams.":::

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede ayudar si tuvo problemas para completar este tutorial.

**Bot no está conectado a Teams**

Si instaló la aplicación pero no funciona, asegúrese de que el bot de la extensión de mensajería esté [conectado al canal de Teams del Servicio de *bots* de Azure.](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Es importante entender que esto no es lo mismo que un canal en Teams. En este caso, un canal es cómo Azure Bot Service conecta el bot a Teams u otra [aplicación de comunicaciones compatible con Microsoft o de terceros.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="see-also"></a>Vea también

* [Teams componer o cuadro de mando](../messaging-extensions/what-are-messaging-extensions.md) 
* [Incluir una función de despliegue de enlaces](../messaging-extensions/how-to/link-unfurling.md)
* [Directrices de diseño](../messaging-extensions/design/messaging-extension-design.md) 
* [Plantillas de interfaz de usuario listas para producción](../concepts/design/design-teams-app-ui-templates.md) 
* [Añadir autenticación](../messaging-extensions/how-to/add-authentication.md)
* [Crear una extensión de mensajería basada en acciones](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Definición de comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [Responder a las búsquedas de los usuarios](../messaging-extensions/how-to/search-commands/respond-to-search.md)
