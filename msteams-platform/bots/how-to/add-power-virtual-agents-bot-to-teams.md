---
title: Añadir Power Virtual Agents chatbot a Teams
author: laujan
description: integración de un chatbot Power Virtual Agents en la plataforma Teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 2a8f9c23eaa1acf2555b91cc4caf8d0f3298c114
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566120"
---
# <a name="add-power-virtual-agents-chatbot"></a>Añadir un bot de chat de Power Virtual Agents 

Power Virtual Agents es una solución de interfaz gráfica guiada sin código que permite a cada miembro de su equipo crear chatbots ricos y conversacionales que se integran fácilmente con la plataforma Teams. Todo el contenido creado en Power Virtual Agents se representa naturalmente en Teams. Power Virtual Agents bots interactúan con los usuarios en el lienzo de chat nativo de Teams. Los administradores de TI, analistas de negocios, especialistas en dominios y desarrolladores de aplicaciones calificados pueden diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo. Pueden crear un servicio web o registrarse directamente en Bot Framework. 

Este documento le guía sobre cómo hacer que su chatbot esté disponible en Teams a través del portal de Power Virtual Agents y agregar su bot a Teams usando App Studio. 

Power Virtual Agents le permite crear potentes chatbots que pueden responder a las preguntas planteadas por sus clientes, otros empleados o visitantes a su sitio web o servicio.

Estos robots se pueden crear fácilmente sin necesidad de científicos de datos o desarrolladores.

> [!NOTE]
> Al agregar el chatbot a Microsoft Teams, algunos de los datos, como el contenido del bot y el contenido de chat del usuario, se comparten con Microsoft Teams. Esto significa que los datos fluyen fuera del cumplimiento de su [organización y de los límites geográficos o regionales.](/power-virtual-agents/data-location) <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>Haga que su chatbot esté disponible en Teams a través del portal de Power Virtual Agents

Para que el chatbot esté disponible en Teams a través del portal de Power Virtual Agents, debe realizar los siguientes pasos de proceso:

**Para que el chatbot esté disponible en Teams**

1. **Publicar el contenido del bot más reciente**  
Después de crear un chatbot en el portal de Power Virtual Agents, debe publicar el bot antes de Teams los usuarios puedan interactuar con él. Para obtener más información, consulte [Publicar el contenido del bot más reciente.](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)

   ![publicar en el portal de agentes virtuales de energía](../../assets/images/pva-publish.png)

1. **Configure el canal de Teams**  
Después de publicar el bot, agregue el canal de Teams para que el bot esté disponible para Teams usuarios.

   ![canales en el portal de agentes virtuales de energía](../../assets/images/pva-channels.png)

1. **Genera un ID de aplicación para tu chatbot**  
Después de agregar el canal Teams al chatbot, se genera un **ID de aplicación** en el cuadro de diálogo. El identificador de aplicación es un identificador único generado por Microsoft para el bot. Guarde el identificador de aplicación para crear un paquete de aplicación para Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Agrega tu bot a Teams usando App Studio

Si [la carga de aplicaciones personalizadas está habilitada](/microsoftteams/admin-settings) en la instancia de Teams, puede usar Teams App Studio para cargar directamente el chatbot y empezar a usarlo inmediatamente. Para compartir el chatbot, puedes solicitar al administrador que haga que tu bot esté disponible en el catálogo de aplicaciones de inquilinos o puedes enviar el paquete de la aplicación a otros usuarios y pedirles que lo carguen de forma independiente.

1. **Instalar App Studio en Teams**  
App Studio es una aplicación Teams. Instale App Studio desde la tienda Teams que simplifica el proceso de creación y registro de bots en Teams: 

   1. Seleccione el icono de la tienda de aplicaciones en Teams instancia y busque **App Studio**.

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. Seleccione el icono **de App Studio** y seleccione **Instalar** en el cuadro de diálogo emergente.

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **Crear el manifiesto de la aplicación Teams en App Studio**  
Los bots de Teams se definen mediante un archivo JSON de manifiesto de aplicación que proporciona la información básica sobre el bot y sus capacidades. En **App Studio**, seleccione Editor de **manifiestos** y seleccione Crear una nueva **aplicación**.

    ![crear una nueva aplicación](../../assets/images/get-started/create-new-app.png)

1. **Agregue los detalles del bot**  
Complete todos los campos obligatorios. Para obtener una descripción completa de cada campo, vea [definición de esquema de manifiesto.](../../resources/schema/manifest-schema.md)

    ![añadir detalles de la aplicación](../../assets/images/get-started/add-app-details.png)

1. **Configura tu bot** Para configurar el bot, realice los pasos siguientes: 
     1. Abra la pestaña **Bots.** 
     1. Seleccione **Configurar**  >  **bot existente** e introduzca el nombre del bot.

   ![Configuración de bots](../../assets/images/get-started/bot-set-up.png) 

   La siguiente imagen muestra cómo configurar un bot existente:      

   ![configuración de bots existente](../../assets/images/get-started/existing-bot-set-up.png)
       
1. **Añade tu ID de aplicación**  
Para agregar el IDENTIFICADOR de la aplicación, siga estos pasos:  
    1. Seleccione **Conectar en un id de bot diferente** y pegue el Identificador de **aplicación** que copió anteriormente. 
    1. Seleccione Guardar personal **de ámbito**  >    >  .

    ![añadir id de aplicación](../../assets/images/get-started/add-app-id.png)

1. **Agregue dominios válidos para el bot**  
Este paso solo es necesario si el bot requiere que el usuario inicie sesión. Seleccione **Dominios y permisos** y, en el campo **Dominios válidos,** proporcione la siguiente entrada:

    ```bash
       token.botframework.com
    ```

1. **Prueba y distribuye tu bot**  
Abra la pestaña **Probar y distribuir** y seleccione **Instalar** para agregar el bot directamente a la instancia de Teams. Como alternativa, puede descargar el paquete de aplicación completado para compartirlo con usuarios Teams o proporcionarlo al administrador para que el bot esté disponible en el catálogo de aplicaciones de inquilinos.

1. **Iniciar un chat**   
El proceso de configuración para agregar el bot de chat Power Virtual Agents a Teams está completo. Ahora puede iniciar una conversación con su bot en un chat personal.

## <a name="see-also"></a>Vea también

- [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- [Cree un chatbot para Teams con Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).  

- [Portal de Power Virtual Agents](https://powervirtualagents.microsoft.com)

- [Publique su bot de Power Virtual Agents](/power-virtual-agents/publication-fundamentals-publish-channels)

- [Seguridad y cumplimiento en Microsoft Teams.](/MicrosoftTeams/security-compliance-overview)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear asistente virtual](~/samples/virtual-assistant.md)

