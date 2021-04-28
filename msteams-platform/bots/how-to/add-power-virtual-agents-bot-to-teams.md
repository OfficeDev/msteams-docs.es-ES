---
title: Agregar el bot de chat de Power Virtual Agents a Teams
author: laujan
description: integración de un bot de chat de Power Virtual Agents en la plataforma teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: bd1528d06f9e9f4ca3a03f167ecb3c537977fb61
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058624"
---
# <a name="add-power-virtual-agents-chatbot"></a>Añadir un bot de chat de Power Virtual Agents 

Power Virtual Agents es una solución de interfaz gráfica guiada sin código que permite a todos los miembros del equipo crear bots de chat conversacionales enriquecidos que se integren fácilmente con la plataforma de Teams. Todo el contenido escrito en Power Virtual Agents se representa de forma natural en Teams. Los bots de Power Virtual Agents interactúan con los usuarios en el lienzo de chat nativo de Teams. Los administradores de TI, analistas empresariales, especialistas en dominios y desarrolladores de aplicaciones cualificados pueden diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo. Pueden crear un servicio web o registrarse directamente con Bot Framework. 

Este documento le guía sobre cómo hacer que el bot de chat esté disponible en Teams a través del portal de Power Virtual Agents y agregar el bot a Teams mediante App Studio. 

Power Virtual Agents te permite crear potentes bots de chat que pueden responder a preguntas de tus clientes, otros empleados o visitantes de tu sitio web o servicio.

Estos bots se pueden crear fácilmente sin necesidad de científicos de datos o desarrolladores.

> [!NOTE]
> Al agregar el bot de chat a Microsoft Teams, algunos de los datos, como el contenido del bot y el contenido de chat de usuario, se comparten con Microsoft Teams. Significa que los datos fluyen fuera del cumplimiento de la organización y de los límites [geográficos o regionales](/power-virtual-agents/data-location). <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>Hacer que el bot de chat esté disponible en Teams a través del portal de Power Virtual Agents

Para que el bot de chat esté disponible en Teams a través del portal de Power Virtual Agents, debe realizar los siguientes pasos de proceso:

**Para que el bot de chat esté disponible en Teams**

1. **Publicar el contenido del bot más reciente**  
Después de crear un bot de chat en el portal de Power Virtual Agents, debe publicar el bot antes de que los usuarios de Teams puedan interactuar con él. Para obtener más información, [vea Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).

   ![publicar en el portal de agentes virtuales de energía](../../assets/images/pva-publish.png)

1. **Configurar el canal de Teams**  
Después de publicar el bot, agrega el canal de Teams para que el bot esté disponible para los usuarios de Teams.

   ![canales en el portal de agentes virtuales de energía](../../assets/images/pva-channels.png)

1. **Generar un identificador de aplicación para el bot de chat**  
Después de agregar el canal de Teams al bot de chat, se genera un **identificador** de aplicación en el cuadro de diálogo. El identificador de la aplicación es un identificador único generado por Microsoft para el bot. Guarda el id. de aplicación para crear un paquete de aplicación para Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Agregar el bot a Teams con App Studio

Si [la carga de aplicaciones personalizadas está](/microsoftteams/admin-settings) habilitada en la instancia de Teams, puedes usar Teams App Studio para cargar directamente el bot de chat y empezar a usarlo inmediatamente. Para compartir el bot de chat, puedes solicitar al administrador que haga que el bot esté disponible en el catálogo de aplicaciones de inquilino o puedes enviar el paquete de la aplicación a otros usuarios y pedirles que lo carguen de forma independiente.

1. **Instalar App Studio en Teams**  
App Studio es una aplicación de Teams. Instalar App Studio desde la Tienda Teams que simplifica el proceso de creación y registro de bots en Teams: 

   1. Selecciona el icono de la tienda de aplicaciones en la instancia de Teams y busca **App Studio**.

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. Selecciona el **icono de App Studio** y selecciona **Instalar** en el cuadro de diálogo emergente.

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **Crear el manifiesto de la aplicación de Teams en App Studio**  
Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities. En **App Studio,** selecciona **Editor de manifiestos** y **selecciona Crear una nueva aplicación.**  
La siguiente imagen te guía para crear una nueva aplicación en App Studio:  

   ![crear una nueva aplicación](../../assets/images/get-started/create-new-app.png)

1. **Agregar los detalles del bot**  
Complete todos los campos necesarios. Para obtener una descripción completa de cada campo, vea [definición de esquema de manifiesto](../../resources/schema/manifest-schema.md).   
La siguiente imagen te guía para agregar los detalles de la aplicación:  

   ![agregar detalles de la aplicación](../../assets/images/get-started/add-app-details.png)

1. **Configurar el bot** Para configurar el bot, siga estos pasos: 
     1. Abra la **pestaña Bots.** 
     1. Seleccione **Configurar**  >  **bot existente** y escriba el nombre del bot.

   La siguiente imagen le guía para configurar un bot:    

   ![Configuración del bot](../../assets/images/get-started/bot-set-up.png) 

   La siguiente imagen le guía para configurar un bot existente:      

   ![configuración de bots existente](../../assets/images/get-started/existing-bot-set-up.png)    
1. **Agregar el id. de aplicación**  
Para agregar el identificador de aplicación, siga estos pasos:  
    1. Seleccione **Conectarse a un id. de bot** diferente y pegue el **Id. de** aplicación que copió anteriormente. 
    1. Seleccione **Guardar**  >  **personal**  >  **del ámbito**.      
La siguiente imagen le guía para configurar un bot existente:    

   ![agregar id. de aplicación](../../assets/images/get-started/add-app-id.png)

1. **Agregar dominios válidos para el bot**  
Este paso solo es necesario si el bot requiere que el usuario inicie sesión. Seleccione Dominios y permisos y, en el **campo Dominios** **válidos,** proporcione la siguiente entrada:

    ```bash
       token.botframework.com
    ```

7.  **Probar y distribuir el bot**  
Abra **la pestaña Probar y distribuir** y seleccione **Instalar** para agregar el bot directamente a la instancia de Teams. Como alternativa, puedes descargar el paquete de la aplicación completado para compartirlo con los usuarios de Teams o proporcionarlo al administrador para que el bot esté disponible en el catálogo de aplicaciones de inquilino.

8. **Iniciar un chat**   
Se ha completado el proceso de configuración para agregar el bot de chat de Power Virtual Agents a Teams. Ahora puedes iniciar una conversación con el bot en un chat personal.

## <a name="see-also"></a>Vea también

- [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- [Crear un bot de chat para Teams con Agentes virtuales de Microsoft Power](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).  

- [Portal de Power Virtual Agents](https://powervirtualagents.microsoft.com)

- [Publicar el bot de Power Virtual Agents](/power-virtual-agents/publication-fundamentals-publish-channels)

- [Seguridad y cumplimiento en Microsoft Teams](/MicrosoftTeams/security-compliance-overview).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear asistente virtual](~/samples/virtual-assistant.md)

