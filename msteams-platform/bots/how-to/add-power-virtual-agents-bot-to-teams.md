---
title: Agregar Chatbot de agentes de Power virtual a teams
author: laujan
description: integración de un Chatbot de agentes de Power virtual en la plataforma de Microsoft Teams
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 3f877505cb2ef20bbd74d236dc17816df04bbef1
ms.sourcegitcommit: 43e1be9d9e3651ce73a8d2139e44d75550a0ca60
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2020
ms.locfileid: "49366871"
---
# <a name="integrate-a-power-virtual-agents-chatbot-with-microsoft-teams"></a>Integración de agentes de Power virtual Chatbot con Microsoft Teams

[Power virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) es una solución de interfaz gráfica sin código guiada que permite a todos los miembros de su equipo crear chatbotss de conversación que se integran fácilmente con la plataforma de Microsoft Teams. Todo el contenido creado por los agentes de Power virtual se representa de forma natural en Teams y los bots de los agentes virtuales de energía, se relaciona con los usuarios del lienzo de chat nativo de Teams. Los administradores de ti, analistas de negocios, especialistas en dominios y programadores de aplicaciones cualificados pueden diseñar, desarrollar y publicar agentes virtuales inteligentes para Microsoft Teams sin tener que configurar un entorno de desarrollo, crear un servicio web o registrarse directamente con bot Framework.  *Consulte* [Create a Chatbot for Teams with Microsoft Power virtual Agents](../what-are-bots.md#create-a-chatbot-for-teams-with-microsoft-power-virtual-agents).

> [!NOTE]
> Al agregar su Chatbot a Microsoft Teams, algunos de los datos, como el contenido de Bot y el contenido de chat de usuario final, se compartirán con Microsoft Teams (lo que significa que los datos fluyen fuera de los [límites de cumplimiento y de la zona o regional](/power-virtual-agents/data-location)de la organización). <br/>
> Para obtener más información, consulte [seguridad y cumplimiento en Microsoft Teams](/MicrosoftTeams/security-compliance-overview).

## <a name="make-your-chatbot-available-in-teams-via-the-power-virtual-agents-portal"></a>Hacer que su Chatbot esté disponible en Microsoft Teams a través del portal de Power virtual Agents

1. **Publique el contenido de bot más reciente**.  Una vez que haya creado un Chatbot en el [portal de agentes de Power virtual](https://powervirtualagents.microsoft.com), debe publicar el bot al menos una vez antes de que los usuarios de Microsoft Teams puedan interactuar con él. Consulte [publicar el último contenido de bot](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).

![Portal de publicación de agentes de Power virtual](../../assets/images/pva-publish.png)

2. **Configure el canal de Teams**. Después de publicar el bot, puede Agregar el canal de Teams para que el bot esté disponible para los usuarios de Microsoft Teams.

![canales en el portal de agentes de Power virtual](../../assets/images/pva-channels.png)

3. **Genere un identificador de aplicación para su Chatbot**.  Cuando el canal de Teams se haya agregado correctamente a su Chatbot, se generará un **identificador de aplicación** en el cuadro de diálogo. El identificador de la aplicación es un identificador único de Microsoft generado por el bot.  Copie y guarde el identificador de aplicación: lo necesitará más tarde para crear un paquete de aplicación para Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Agregar un bot a teams con App Studio

Si la [carga de aplicaciones personalizadas está habilitada](/microsoftteams/admin-settings) en la instancia de Teams, puede usar Team App Studio para cargar directamente sus Chatbot y empezar a usarlo inmediatamente. Si quiere compartir sus Chatbot, puede solicitar que su administrador haga que su bot esté disponible en el catálogo de aplicaciones del espacio empresarial, o bien puede enviar a otros usuarios el paquete de la aplicación y pedirles que lo carguen de forma independiente.

1. **Instale App Studio en Teams**. App Studio es una aplicación de Microsoft teams que puede instalar desde la tienda Teams y que simplifica la creación y el registro de su bot en Teams: 

  * Seleccione el icono de la tienda de aplicaciones en la parte inferior de la barra de navegación izquierda de la instancia de Teams y busque **App Studio**.
>

&emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="/msteams-docs/msteams-platform/assets/images/get-started/app-studio-store.png"/>   

  * Seleccione el icono de **App Studio** y elija **instalar** en el cuadro de diálogo emergente.
>
&emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. **Cree el manifiesto de la aplicación Teams en App Studio**.  Los bots en Teams se definen mediante un archivo de manifiesto de la aplicación (JSON) que proporciona información básica sobre el bot y sus funciones. En el editor de **manifiestos** de **App Studio** , haga clic en   =>  **crear una nueva aplicación**.
3. **Agregue los detalles del bot**. Para obtener una descripción completa de cada campo, consulte [definición del esquema del manifiesto](../../resources/schema/manifest-schema.md). Asegúrese de completar todos los campos obligatorios.
4. **Configure el bot**. Desplácese a la ficha **bots** , seleccione el botón **configurar** , elija **Bot existente** y escriba el nombre del bot.
5. **Agregue el identificador de la aplicación**. Navegue a **conectar con un identificador de bot diferente** y pegue el **identificador** de la aplicación que ha copiado anteriormente. En ámbito, seleccione **personal** y, a continuación, seleccione **Guardar**.
6. **Agregue dominios válidos para el bot**.  Este paso solo es necesario si el bot requiere que el usuario inicie sesión. Vaya a **dominios y permisos** y, en el campo **dominios válidos** , escriba lo siguiente:

```bash
token.botframework.com
```

7.  **Pruebe y distribuya el bot**. Seleccione la pestaña **probar y distribuir** y elija **instalar** para agregar el bot directamente a la instancia de Teams. Opcionalmente, puede descargar el paquete de la aplicación que se ha completado para compartirlo con los usuarios de Microsoft Teams o proporcionarlo a su administrador para que el bot esté disponible en el catálogo de aplicaciones del espacio empresarial.
8. **Inicie un chat**. Se ha completado el proceso de instalación para agregar el robot de chat de los agentes virtuales de Power a teams. Ahora puede iniciar una conversación con el bot en un chat personal.

> [!div class="nextstepaction"]
> [Más información: publicar el bot de Power virtual Agents](/power-virtual-agents/publication-fundamentals-publish-channels)
