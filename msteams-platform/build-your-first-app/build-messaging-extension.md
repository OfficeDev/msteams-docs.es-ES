---
title: 'Introducción: crear una extensión de mensajería'
author: girliemac
description: Cree rápidamente una Microsoft Teams de mensajería mediante el Microsoft Teams Toolkit.
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
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a>Crear la primera extensión de mensajería para Microsoft Teams

Hay dos tipos de extensiones Teams *mensajería:* [comandos de](../messaging-extensions/how-to/search-commands/define-search-command.md) búsqueda y [comandos de acción](../messaging-extensions/how-to/action-commands/define-action-command.md).

Este tutorial le enseña *a* crear un comando de búsqueda (también conocido como una extensión de mensajería basada en *búsqueda),* que es un acceso directo para buscar contenido externo y compartirlo en Teams. Los usuarios pueden tener acceso a los comandos de búsqueda desde Teams cuadro de redacción o comando.

## <a name="what-youll-learn"></a>Lo que aprenderás

* Crea un proyecto de aplicación y un bot de extensión de mensajería con el Microsoft Teams Toolkit para Visual Studio Code.
* Comprenda las configuraciones de la aplicación y los scaffolding relevantes para las extensiones de mensajería.
* Hospedar una aplicación localmente.
* Configure el bot para la extensión de mensajería.
* Descarga local y prueba una extensión de mensajería en Teams.

## <a name="prerequisites"></a>Requisitos previos

Asegúrate de comprender cómo configurar y crear una aplicación Teams sencilla. Para obtener más información, consulta [crear la primera aplicación Microsoft Teams "Hello, World!"](../build-your-first-app/build-and-run.md).

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

La Microsoft Teams Toolkit ayuda a configurar los siguientes componentes para la extensión de mensajería:

* **Configuraciones de aplicaciones y scaffolding relevantes** para extensiones de mensajería.
* **Bot** para la extensión de mensajería que se registra automáticamente con el servicio Microsoft Azure Bot.

**Para crear el proyecto de aplicación**

1. En Visual Studio Code, selecciona **Microsoft Teams** en la barra de actividades izquierda y :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: elige Crear una nueva aplicación Teams **.**
1. Cuando se le pida, inicie sesión con su Microsoft 365 de desarrollo.
1. En la **pantalla Seleccionar proyecto,** en **Búsqueda de extensiones de**  >  mensajería, haga clic en **JS (JavaScript).** 
1. Escribe un nombre para la Teams aplicación. Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.
1. Seleccione **Crear un nuevo bot y, a** continuación, haga clic en El botón Crear registro **del** bot. Si se realiza correctamente, el nuevo bot tendrá un *estado Registrado.* Ahora, el bot se registra automáticamente con el servicio Microsoft Azure bot. 
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto y guardar el proyecto en el equipo local.

## <a name="2-understand-your-app-project-components"></a>2. Comprender los componentes del proyecto de la aplicación

Gran parte de las configuraciones de la aplicación y los scaffolding se establecen automáticamente al crear el proyecto con el Teams Toolkit.

* Configuraciones de aplicaciones: para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a Extensiones **de mensajería**.
* Scaffolding de aplicaciones: el scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar cómo la extensión de mensajería (o técnicamente, el bot de la extensión de mensajería) responde a las consultas de búsqueda en `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurar un túnel seguro en la aplicación

Para realizar pruebas, vamos a hospedar la extensión de mensajería en un servidor web local (puerto 3978). Va a usar [ngrok](https://ngrok.com/download) para configurar un túnel seguro para localhost. Consulta [crear el primer bot para obtener Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) para obtener más información. 

1. Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).
1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado (por ejemplo, ) ya que `https://468b9ab725e9.ngrok.io` Teams requiere conexiones HTTPS.

   Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá realizar un túnel donde hospedas la aplicación ( en el `localhost` puerto 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. Configurar el bot para la extensión de mensajería

Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario desde Teams al servicio hospedado. El bot debe estar registrado en el Servicio de bots de Azure, que se ha realizado al configurar la aplicación mediante el Teams Toolkit.

Todavía debe especificar una dirección URL de extremo de bot para recibir y procesar consultas de búsqueda en la extensión de mensajería. Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` de . Puede configurarlo rápidamente en el kit de herramientas.

1. En Visual Studio Code, seleccione **Microsoft Teams** en la barra de actividades izquierda :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: y elija Abrir **Microsoft Teams Toolkit**.
1. Ve a **Bots > Registros de bots existentes** y selecciona el bot que creaste durante la instalación.
1. En el **campo Dirección del extremo bot,** escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.

   El bot podrá controlar las consultas de la extensión de mensajería.

## <a name="5-build-and-run-your-app"></a>5. Crear y ejecutar la aplicación

Ha configurado una dirección URL para hospedar la extensión de mensajería y la ha configurado para controlar las búsquedas. Es hora de que la aplicación esté en funcionamiento.

1. Abre el terminal y ve al directorio raíz del proyecto de la aplicación.
1. Ejecute `npm install`.
1. Ejecute `npm start`.

   Si se realiza correctamente, verá el siguiente mensaje que indica que el servicio de extensión de mensajería está escuchando la actividad en su `localhost` :

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Cargar localmente la extensión de mensajería en Teams

Con la extensión de mensajería en ejecución, puede instalarla en Teams.

> [!TIP]
> Si no has descargado localmente una aplicación Teams antes y te encuentras con problemas, sigue estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).

1. En Visual Studio Code, seleccione la clave **F5** para iniciar un Teams web.
1. En el cuadro de diálogo de instalación de la aplicación, **selecciona Agregar para mí**.

## <a name="7-test-your-messaging-extension"></a>7. Probar la extensión de mensajería

Obtenga información sobre cómo funcionan las extensiones de mensajería en un Teams chat.

1. Inicie un nuevo chat. En el cuadro redacción, selecciona **Más** y selecciona la aplicación de extensión de :::image type="icon" source="../assets/icons/teams-client-more.png"::: mensajería que acaba de instalar.
1. Intente buscar algo (por ejemplo, **Tickets**). Si la aplicación funciona, verás resultados de búsqueda de ejemplo (puedes agregar los tuyos más adelante).

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Captura de pantalla que muestra cómo se usa una extensión de mensajería basada en búsqueda en el Teams cuadro de redacción.":::

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede ayudar si tiene problemas para completar este tutorial.

**Bot no está conectado a Teams**

Si instalaste la aplicación pero no funciona, asegúrate de que el bot de la extensión de mensajería esté conectado al canal de Teams [ *bot de* Azure](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Es importante comprender que esto no es lo mismo que un canal en Teams. En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones compatible con Microsoft o [de terceros.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="see-also"></a>Consulte también

* [Teams comando o redacción](../messaging-extensions/what-are-messaging-extensions.md) 
* [Incluir una característica de desamuestra de vínculos](../messaging-extensions/how-to/link-unfurling.md)
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
