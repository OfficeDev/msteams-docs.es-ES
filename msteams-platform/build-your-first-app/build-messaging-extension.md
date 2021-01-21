---
title: 'Introducción: crear una extensión de mensajería'
author: heath-hamilton
description: Cree rápidamente una extensión de mensajería de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 86d44740feaa2cd33aff0e1dde14d757420d90d6
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911922"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>Crear una extensión de mensajería para Microsoft Teams

Hay dos tipos de extensiones de mensajería *de aplicaciones de* Teams: comandos de búsqueda [y](../messaging-extensions/how-to/search-commands/define-search-command.md) comandos [de acción.](../messaging-extensions/how-to/action-commands/define-action-command.md)

En esta lección, creará un comando de búsqueda *(también* conocido como extensión de mensajería basada en *búsquedas),* que es un acceso directo para buscar contenido externo y compartirlo en Teams. Los usuarios pueden obtener acceso a los comandos de búsqueda desde el cuadro [de redacción o comando de Teams.](../messaging-extensions/what-are-messaging-extensions.md)

## <a name="your-assignment"></a>Su asignación

El servicio de ayuda de su organización se comunica con los usuarios a través de Teams, pero los vales residen en un sistema independiente. Esto significa que el personal de soporte técnico debe ir de una aplicación a otra constantemente. Investigará cómo puede reducir este cambio de contexto creando una extensión de mensajería sencilla basada en búsquedas para Teams.

## <a name="what-youll-learn"></a>Lo que aprenderás

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación y un bot de extensión de mensajería con Microsoft Teams Toolkit para Visual Studio código
> * Identificar las configuraciones de la aplicación y algunos de los scaffolding relevantes para las extensiones de mensajería
> * Hospedar una aplicación localmente
> * Configurar el bot para la extensión de mensajería
> * Instalación de prueba y instalación de prueba de una extensión de mensajería en Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese de comprender [e instalar los requisitos previos de](build-first-app-overview.md#get-prerequisites)desarrollo de Teams.

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

Microsoft Teams Toolkit le ayuda a configurar los siguientes componentes para la extensión de mensajería:

* **Configuraciones de aplicaciones y scaffolding relevantes** para extensiones de mensajería
* **Bot** para la extensión de mensajería que se registra automáticamente con el servicio de bots de Microsoft Azure

> [!TIP]
> Si no ha creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que le sea útil seguir estas instrucciones que explican los proyectos con más detalle.

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Crear una nueva aplicación :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: de **Teams.**
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.
1. En la pantalla **Agregar funcionalidades,** seleccione **Extensión de mensajería y,** a **continuación, Siguiente.**
1. Escriba un nombre para su aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).
1. En la **pantalla Configurar extensión de** mensajería, haga lo siguiente:
    1. Elija solo la **opción basada en** búsqueda para el tipo de extensión de mensajería.
    1. Seleccione **Crear un nuevo bot y,** a **continuación, crear registro de bot.** Si se realiza correctamente, el nuevo bot tendrá el **estado Registrado.**
    1. Por ahora, seleccione **No para** la opción de desenlazaje de vínculos.
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="2-identify-relevant-app-project-components"></a>2. Identificar componentes relevantes del proyecto de aplicación

Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

Para ver o actualizar las configuraciones de la extensión de mensajería, seleccione **App Studio** en el kit de herramientas y vaya a Extensiones **de mensajería.**

### <a name="app-scaffolding"></a>Scaffolding de aplicaciones

El scaffolding de la aplicación proporciona un archivo, ubicado en el directorio raíz del proyecto, para controlar cómo responde la extensión de mensajería (o técnicamente, el bot de la extensión de mensajería) a las consultas de búsqueda en `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurar un túnel seguro para la aplicación

Para realizar pruebas, vamos a hospedar la extensión de mensajería en un servidor web local (puerto 3978).

1. Si aún no lo ha hecho, instale [ngrok](https://ngrok.com/download).
1. En un terminal, ejecute `ngrok http -host-header=rewrite 3978` .
1. Copie la dirección URL HTTPS en el resultado (por ejemplo, `https://468b9ab725e9.ngrok.io` ), ya que Teams requiere conexiones HTTPS.

Con esta dirección URL, Teams (que requiere conexiones HTTPS) podrá túnel hasta donde hospeda la aplicación ( en el puerto `localhost` 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. Configurar el bot para la extensión de mensajería

Las extensiones de mensajería dependen de bots para enviar y procesar solicitudes de usuario de Teams a su servicio hospedado. El bot debe estar registrado con el Servicio de bots de Azure, que se ha realizado al configurar la aplicación con Teams Toolkit.

Debe especificar una dirección URL de extremo de bot para recibir y procesar consultas de búsqueda en la extensión de mensajería. Normalmente, la dirección URL tiene el aspecto `https://HOST_URL/api/messages` . Puedes configurarlo rápidamente en el kit de herramientas.

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Abrir Microsoft :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: Teams **Toolkit.**
1. Vaya a **Bots > registros de bots existentes** y seleccione el bot que creó durante la instalación.
1. En el **campo de dirección** del extremo del bot, escriba la dirección URL de ngrok (por ejemplo, ) donde hospeda el bot y `https://468b9ab725e9.ngrok.io` `/api/messages` anexe a él.

El bot podrá controlar las consultas en la extensión de mensajería.

## <a name="5-build-and-run-your-app"></a>5. Compilar y ejecutar la aplicación

Ha configurado una dirección URL para hospedar la extensión de mensajería y la ha configurado para controlar las búsquedas. Es el momento de que la aplicación esté en funcionamiento.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecute `npm start` .

Si se realiza correctamente, verá el siguiente mensaje que indica que el servicio de extensión de mensajería está escuchando la actividad en `localhost` su:

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Instalación local de la extensión de mensajería en Teams

Con la extensión de mensajería en ejecución, puede instalarla en Teams.

> [!TIP]
> Si no ha descargado localmente una aplicación de Teams antes y tiene problemas, siga estas [instrucciones.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.
1. En el cuadro de diálogo de instalación de la aplicación, **seleccione Agregar para mí.**

## <a name="7-test-your-messaging-extension"></a>7. Probar la extensión de mensajería

Obtenga información sobre cómo funcionan las extensiones de mensajería en un chat de Teams.

1. Inicie un nuevo chat. En el cuadro de redacción, seleccione **Más** y elija la aplicación de extensión de :::image type="icon" source="../assets/icons/teams-client-more.png"::: mensajería que acaba de instalar localmente.
1. Intente buscar algo (por ejemplo, **Vales).** Si la aplicación funciona, verá resultados de búsqueda de ejemplo (puede agregar los suyos más adelante).<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Captura de pantalla que muestra cómo se usa una extensión de mensajería basada en búsquedas en el cuadro de redacción de Teams.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una extensión de mensajería básica de Teams que está configurada para buscar contenido externo en el cuadro de redacción o comando.

## <a name="next-steps"></a>Pasos siguientes

Vea las páginas siguientes para continuar y crear una extensión de mensajería completa:

1. [Defina los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) que sean relevantes para su servicio.
1. Configure el servicio para [que responda a las búsquedas de los usuarios.](../messaging-extensions/how-to/search-commands/respond-to-search.md)

## <a name="troubleshooting"></a>Solución de problemas

La siguiente información puede resultar útil si tiene problemas para completar este tutorial.

### <a name="bot-isnt-connected-to-teams"></a>El bot no está conectado a Teams

Si ha instalado la aplicación pero no funciona, asegúrese de que el bot de la extensión de mensajería está conectado al canal de Teams del servicio de bot [de Azure. ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Es importante comprender que esto no es lo mismo que un canal en Teams. En este caso, un canal es cómo el servicio de bots de Azure conecta el bot a Teams u otra aplicación de comunicaciones de Microsoft o de [terceros compatible.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="learn-more"></a>Más información

* [Incluir una característica de desenlazaje de vínculos](../messaging-extensions/how-to/link-unfurling.md)
* Sigue nuestras [directrices de diseño](../messaging-extensions/design/messaging-extension-design.md) y compila con [plantillas de interfaz](../concepts/design/design-teams-app-ui-templates.md) de usuario listas para producción para crear una experiencia sin problemas.
* [Añadir autenticación](../messaging-extensions/how-to/add-authentication.md)
* [Crear una extensión de mensajería basada en acciones](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
