---
title: Añadir un bot de chat de Power Virtual Agents a Teams
author: surbhigupta
description: Aprenda a integrar un bot de chat de Power Virtual Agents en la plataforma de Teams para crear bots de chat conversacionales e integrarlo con Teams
ms.topic: how-to
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: 53a938ca4a195ba6f477de130a8290242709cb19
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111776"
---
# <a name="add-power-virtual-agents-chatbot"></a>Añadir un bot de chat de Power Virtual Agents

Power Virtual Agents es una solución de interfaz gráfica guiada sin código que permite a todos los miembros de su equipo crear bots de chat enriquecidos y conversacionales que se integren fácilmente con la plataforma de Teams. Todo el contenido creado en Power Virtual Agents se representa de forma natural en Teams. Los bots de Power Virtual Agents interactúan con los usuarios en el lienzo de chat nativo de Teams. Los administradores de TI, analistas de negocios, especialistas en dominios y desarrolladores de aplicaciones cualificados pueden diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo. Pueden crear un servicio web o registrarse directamente con Bot Framework.

Este documento le guía sobre cómo hacer que el bot de chat esté disponible en Teams a través del portal de Power Virtual Agents y agregue el bot a Teams mediante App Studio.

Power Virtual Agents le permite crear potentes bots de chat que pueden responder a las preguntas planteadas por sus clientes, otros empleados o visitantes a su sitio web o servicio.

Estos bots se pueden crear fácilmente sin necesidad de científicos de datos o desarrolladores.

> [!NOTE]
> * Al agregar el bot de chat a Microsoft Teams, algunos de los datos, como el contenido del bot y el contenido de chat de usuario, se comparten con Microsoft Teams. Esto significa que los datos fluyen fuera del [cumplimiento de la organización y de los límites geográficos o regionales](/power-virtual-agents/data-location). <br/>
> * No debe usar Microsoft Power Platform para crear aplicaciones que se van a publicar en la tienda de aplicaciones de Teams. Las aplicaciones de Microsoft Power Platform solo se pueden publicar en la tienda de aplicaciones de una organización.

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>Haga que su bot de chat esté disponible en Teams a través del portal de Power Virtual Agents

Para que el bot de chat esté disponible en Teams a través del portal de Power Virtual Agents, debe realizar los pasos de proceso siguientes:

Para que el bot de chat esté disponible en Teams:

1. **Publicación del contenido del bot más reciente**  
Después de crear un bot de chat en el portal de Power Virtual Agents, debe publicar el bot antes de que los usuarios de Teams puedan interactuar con él. Para obtener más información, consulte [Publicación del contenido del bot más reciente](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).

   ![publicar en el portal de power virtual agents](../../assets/images/pva-publish.png)

1. **Configuración del canal de Teams**  
Después de publicar el bot, agregue el canal de Teams para que el bot esté disponible para los usuarios de Teams.

   ![canales en el portal de power virtual agents](../../assets/images/pva-channels.png)

1. **Generación de un identificador de aplicación para el bot de chat**  
Después de agregar el canal de Teams al bot de chat, se genera un **identificador de aplicación** en el cuadro de diálogo. El identificador de aplicación es un identificador único generado por Microsoft para el bot. Guarde el identificador de aplicación para crear un paquete de aplicación para Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Agregar un bot a Teams mediante App Studio

Si [la carga de aplicaciones personalizadas está habilitada](/microsoftteams/admin-settings) en la instancia de Teams, puede usar Teams App Studio para cargar directamente el bot de chat y empezar a usarlo inmediatamente. Para compartir el bot de chat, puede solicitar al administrador que haga que el bot esté disponible en el catálogo de aplicaciones de inquilino o puede enviar el paquete de la aplicación a otros usuarios y pedirles que lo carguen de forma independiente.

1. **Instalar App Studio en Teams**  
App Studio es una aplicación de Teams. Instale App Studio desde la tienda de Teams que simplifica el proceso de creación y registro de bots en Teams:

   1. Seleccione el icono de la tienda de aplicaciones en la instancia de Teams y busque **App Studio**.

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>

   1. Seleccione el icono de **App Studio** y seleccione **Instalar** en el cuadro de diálogo emergente.

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **Creación del manifiesto de aplicación de Teams en App Studio**  
Los bots de Teams se definen mediante un archivo JSON de manifiesto de aplicación que proporciona la información básica sobre el bot y sus funcionalidades. En **App Studio**, seleccione **Editor de tarjetas** y seleccione **Crear una nueva aplicación**.

    ![crear una aplicación nueva](../../assets/images/get-started/create-new-app.png)

1. **Agregar los detalles del bot**  
Complete todos los campos necesarios. Para obtener una descripción completa de cada campo, consulte [definición de esquema de manifiesto](../../resources/schema/manifest-schema.md).

    ![agregar detalles de la aplicación](../../assets/images/get-started/add-app-details.png)

1. **Configuración del bot** Para configurar el bot, siga estos pasos:
     1. Abra la pestaña **Bots**.
     1. Seleccione **Configurar** > **Bot existente** y escriba el nombre del bot.

   ![Configuración del bot](../../assets/images/get-started/bot-set-up.png)

   En la imagen siguiente se muestra cómo configurar un bot existente:

   ![configuración del bot existente](../../assets/images/get-started/existing-bot-set-up.png)

1. **Agregar el identificador de aplicación**  
Para agregar el identificador de aplicación, realice los pasos siguientes:  
    1. Seleccione **Conectar a un identificador de bot diferente** y pegue el **identificador de aplicación** que copió anteriormente.
    1. Seleccione **Ámbito** > **Personal** > **Guardar**.

    ![agregar id. de aplicación](../../assets/images/get-started/add-app-id.png)

1. **Agregar dominios válidos para el bot**  
Este paso solo es necesario si el bot requiere que el usuario inicie sesión. Seleccione **Dominios y permisos** y, en el campo **Dominios válidos**, proporcione la siguiente entrada:

    ```bash
       token.botframework.com
    ```

1. **Prueba y distribución del bot**  
Abra la pestaña **Probar y distribuir** y seleccione **Instalar** para agregar el bot directamente a la instancia de Teams. Como alternativa, puede descargar el paquete de aplicación completado para compartirlo con usuarios de Teams o proporcionarlo al administrador para que el bot esté disponible en el catálogo de aplicaciones de inquilino.

1. **Iniciar un chat** Se ha completado el proceso de configuración para agregar el bot de chat de Power Virtual Agents a Teams. Ahora puede iniciar una conversación con el bot en un chat personal.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear un asistente virtual](~/samples/virtual-assistant.md)

## <a name="see-also"></a>Vea también

* [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* [Creación de un bot de chat para Teams con Microsoft Power Virtual Agents](../bot-features.md#bots-with-power-virtual-agents)
* [Portal de Power Virtual Agents](https://powervirtualagents.microsoft.com)
* [Publicación del bot de Power Virtual Agents](/power-virtual-agents/publication-fundamentals-publish-channels)
* [Seguridad y cumplimiento en Microsoft Teams](/MicrosoftTeams/security-compliance-overview)
