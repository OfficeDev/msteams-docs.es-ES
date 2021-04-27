---
title: 'Introducción: crear una extensión de mensajería'
author: heath-hamilton
description: Cree rápidamente una extensión de mensajería de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: f3b5bc9c749d5e5276c0c7af7ff92f4ff5a00d0b
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020873"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>Crear una extensión de mensajería para Microsoft Teams

Hay dos tipos de extensiones de *mensajería de* Teams: comandos [de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) y comandos [de acción](../messaging-extensions/how-to/action-commands/define-action-command.md).

En esta lección, creará un comando de búsqueda *(también* conocido como una extensión de mensajería basada en *búsqueda),* que es un acceso directo para buscar contenido externo y compartirlo en Teams. Los usuarios pueden obtener acceso a los comandos de búsqueda desde el cuadro [de redacción o comando de Teams.](../messaging-extensions/what-are-messaging-extensions.md)

## <a name="your-assignment"></a>Su asignación

El servicio de ayuda de la organización se comunica con los usuarios a través de Teams, pero los vales residen en un sistema independiente. Esto significa que el personal de soporte técnico debe ir y venir constantemente entre aplicaciones. Investigará cómo puede reducir este cambio de contexto creando una extensión de mensajería sencilla basada en búsquedas para Teams.

## <a name="what-youll-learn"></a>Lo que aprenderás

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación y un bot de extensión de mensajería con Microsoft Teams Toolkit para Visual Studio código
> * Identificar las configuraciones de la aplicación y algunos de los scaffolding relevantes para las extensiones de mensajería
> * Hospedar una aplicación localmente
> * Configurar el bot para la extensión de mensajería
> * Instalación local y prueba de una extensión de mensajería en Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese de comprender e [instalar los requisitos previos](build-first-app-overview.md#get-prerequisites)de desarrollo de Teams .

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para la extensión de mensajería:

* **Configuraciones de aplicaciones y scaffolding relevantes** para extensiones de mensajería
* **Bot** para la extensión de mensajería que se registra automáticamente en el Servicio de bots de Microsoft Azure

> [!TIP]
> Si no has creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que te sea útil seguir estas instrucciones que explican los proyectos con más detalle.

1. En Visual Studio, selecciona **Microsoft Teams en** la barra de actividades izquierda y elige Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams**.
1. Cuando se le pida, inicie sesión con su cuenta de desarrollo de Microsoft 365.
1. En la **pantalla Agregar capacidades,** seleccione **Extensión de mensajería y,** a **continuación, Siguiente**.
1. Escribe un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).
1. En la **pantalla Configurar extensión de mensajería,** haga lo siguiente:
    1. Elija solo la **opción basada en búsqueda** para el tipo de extensión de mensajería.
    1. Seleccione **Crear un bot nuevo y, a** **continuación, Crear registro de bot**. Si se realiza correctamente, el nuevo bot tendrá un **estado Registrado.**
    1. Por ahora, seleccione **No** para la opción de desamuesar vínculos.
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="2-identify-relevant-app-project-components"></a>2. Identificar componentes relevantes del proyecto de aplicación

Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

Para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a Extensiones **de mensajería**.

### <a name="app-scaffolding"></a>Scaffolding de aplicaciones

El scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar cómo responde la extensión de mensajería (o técnicamente, el bot de la extensión de mensajería) a las consultas de búsqueda en `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurar un túnel seguro en la aplicación

Para realizar pruebas, vamos a hospedar la extensión de mensajería en un servidor web local (puerto 3978).

1. Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).
1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ) ya que Teams requiere conexiones HTTPS.

Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá realizar un túnel donde hospedas la aplicación ( en el `localhost` puerto 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. Configurar el bot para la extensión de mensajería

Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario de Teams al servicio hospedado. El bot debe estar registrado en el Servicio de bots de Azure, que se hizo al configurar la aplicación con Teams Toolkit.

Todavía debe especificar una dirección URL de extremo de bot para recibir y procesar consultas de búsqueda en la extensión de mensajería. Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` de . Puede configurarlo rápidamente en el kit de herramientas.

1. En Visual Studio, seleccione **Microsoft Teams en** la barra de actividades izquierda y elija Abrir Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Toolkit**.
1. Ve a **Bots > Registros de bots existentes** y selecciona el bot que creaste durante la instalación.
1. En el **campo Dirección del extremo bot,** escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.

El bot podrá controlar las consultas de la extensión de mensajería.

## <a name="5-build-and-run-your-app"></a>5. Crear y ejecutar la aplicación

Ha configurado una dirección URL para hospedar la extensión de mensajería y la ha configurado para controlar las búsquedas. Es hora de que la aplicación esté en funcionamiento.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecute `npm start` .

Si se realiza correctamente, verá el siguiente mensaje que indica que el servicio de extensión de mensajería está escuchando la actividad en su `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Instalación local de la extensión de mensajería en Teams

Con la extensión de mensajería en ejecución, puede instalarla en Teams.

> [!TIP]
> Si no has descargado previamente una aplicación de Teams y tienes problemas, sigue estas [instrucciones](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).

1. En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.
1. En el cuadro de diálogo de instalación de la aplicación, **selecciona Agregar para mí**.

## <a name="7-test-your-messaging-extension"></a>7. Probar la extensión de mensajería

Obtenga información sobre cómo funcionan las extensiones de mensajería en un chat de Teams.

1. Inicie un nuevo chat. En el cuadro redacción, selecciona **Más** y elige la aplicación de extensión :::image type="icon" source="../assets/icons/teams-client-more.png"::: de mensajería que acaba de instalar.
1. Intente buscar algo (por ejemplo, **Tickets**). Si la aplicación funciona, verás resultados de búsqueda de ejemplo (puedes agregar los tuyos más adelante).<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Captura de pantalla que muestra cómo se usa una extensión de mensajería basada en búsqueda en el cuadro de redacción de Teams.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una extensión de mensajería básica de Teams que está configurada para buscar contenido externo en el cuadro de redacción o comando.

## <a name="next-steps"></a>Siguientes pasos

Consulta las páginas siguientes para continuar y crear una extensión de mensajería con todas las características:

1. [Definir comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) que sean relevantes para el servicio.
1. Configure el servicio para [que responda a las búsquedas de los usuarios.](../messaging-extensions/how-to/search-commands/respond-to-search.md)

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede ayudar si tiene problemas para completar este tutorial.

### <a name="bot-isnt-connected-to-teams"></a>Bot no está conectado a Teams

Si has instalado la aplicación pero no funciona, asegúrate de que el bot de la extensión de mensajería esté conectado al canal de Teams del servicio de bot [de Azure. ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Es importante comprender que esto no es lo mismo que un canal en Teams. En este caso, un canal es cómo el Servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones compatible con Microsoft o [de terceros.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="learn-more"></a>Más información

* [Incluir una característica de desamuestra de vínculos](../messaging-extensions/how-to/link-unfurling.md)
* Siga nuestras [directrices de diseño](../messaging-extensions/design/messaging-extension-design.md) y cree con [plantillas de](../concepts/design/design-teams-app-ui-templates.md) interfaz de usuario preparadas para producción para crear una experiencia perfecta.
* [Añadir autenticación](../messaging-extensions/how-to/add-authentication.md)
* [Crear una extensión de mensajería basada en acciones](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)

