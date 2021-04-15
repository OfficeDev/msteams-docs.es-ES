---
title: Agregar el bot de chat de Power Virtual Agents a Teams
author: laujan
description: integración de un bot de chat de Power Virtual Agents en la plataforma teams
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 6103e3b58d7283eab6e9a9932f6dc7778d6fc697
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697098"
---
# <a name="integrate-a-power-virtual-agents-chatbot-with-microsoft-teams"></a>Integrar un bot de chat de Power Virtual Agents con Microsoft Teams

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) es una solución de interfaz gráfica guiada sin código que permite a todos los miembros del equipo crear bots de chat conversacionales enriquecidos que se integren fácilmente con la plataforma de Teams. Todo el contenido escrito en Power Virtual Agents se representa de forma natural en los bots de Teams y Power Virtual Agents que interactúan con los usuarios en el lienzo de chat nativo de Teams. Los administradores de TI, analistas empresariales, especialistas en dominios y desarrolladores de aplicaciones cualificados pueden diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo, crear un servicio web o registrarse directamente con Bot Framework.  *Consulte* [Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).

> [!NOTE]
> Al agregar el bot de chat a Microsoft Teams, algunos datos, como el contenido del bot y el contenido de chat del usuario final, se compartirán con Microsoft Teams (lo que significa que los datos fluirán fuera del cumplimiento de la organización y los límites geográficos o [regionales).](/power-virtual-agents/data-location) <br/>
> Para obtener más información, vea [security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).

## <a name="make-your-chatbot-available-in-teams-via-the-power-virtual-agents-portal"></a>Hacer que el bot de chat esté disponible en Teams a través del portal de Power Virtual Agents

1. **Publicar el contenido del bot más reciente.**  Después de crear un bot de chat en el portal de [Power Virtual Agents,](https://powervirtualagents.microsoft.com)debes publicar el bot al menos una vez antes de que los usuarios de Teams puedan interactuar con él. Consulte [Publicar el contenido del bot más reciente.](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)

![publicar en el portal de agentes virtuales de energía](../../assets/images/pva-publish.png)

2. **Configurar el canal de Teams**. Después de publicar el bot, puedes agregar el canal de Teams para que el bot esté disponible para los usuarios de Teams.

![canales en el portal de agentes virtuales de energía](../../assets/images/pva-channels.png)

3. **Generar un identificador de aplicación para el bot de chat.**  Cuando el canal de Teams se haya agregado  correctamente al bot de chat, se generará un identificador de aplicación en el cuadro de diálogo. El identificador de aplicación es un identificador único generado por Microsoft para el bot.  Copia y guarda el id. de aplicación: lo necesitarás más adelante para crear un paquete de aplicación para Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Agregar el bot a Teams con App Studio

Si [la carga de aplicaciones personalizadas está](/microsoftteams/admin-settings) habilitada en la instancia de Teams, puedes usar Teams App Studio para cargar directamente el bot de chat y empezar a usarlo inmediatamente. Si quieres compartir el bot de chat, puedes solicitar que el administrador haga que el bot esté disponible en el catálogo de aplicaciones de inquilino o puedes enviar a otros usuarios el paquete de la aplicación y pedirles que lo carguen de forma independiente.

1. **Instalar App Studio en Teams**. App Studio es una aplicación de Teams que puedes instalar desde la Tienda Teams que simplifica la creación y el registro del bot en Teams: 

  * Selecciona el icono de la tienda de aplicaciones en la parte inferior de la barra de navegación izquierda de la instancia de Teams y busca **App Studio**.
>

&emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="/msteams-docs/msteams-platform/assets/images/get-started/app-studio-store.png"/>   

  * Selecciona el **icono de App Studio** y elige **Instalar** en el cuadro de diálogo emergente.
>
&emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. **Crea el manifiesto de la aplicación de Teams en App Studio**.  Bots in Teams are defined by an app manifest (JSON) file that provides basic information about your bot and its capabilities. En **App Studio,** selecciona **Editor de manifiesto** Crear una nueva   =>  **aplicación.**
3. **Agregue los detalles del bot**. Para obtener una descripción completa de cada campo, vea [definición de esquema de manifiesto](../../resources/schema/manifest-schema.md). Asegúrese de completar todos los campos necesarios.
4. **Configurar el bot**. Vaya a la **pestaña Bots,** seleccione el **botón Configurar,** elija **Bot existente** y escriba el nombre del bot.
5. **Agregue el identificador de aplicación**. Navegue hasta **Conectarse a un identificador de bot diferente** y pegue el **id.** de aplicación que copió anteriormente. En el ámbito, **seleccione Personal** y, a continuación, **seleccione Guardar**.
6. **Agregue dominios válidos para el bot**.  Este paso solo es necesario si el bot requiere que el usuario inicie sesión. Vaya a Dominios y permisos y, en el **campo Dominios** **válidos,** introduzca lo siguiente:

```bash
token.botframework.com
```

7.  **Probar y distribuir el bot**. Elija la **pestaña Probar y distribuir** y elija **Instalar** para agregar el bot directamente a la instancia de Teams. Opcionalmente, puedes descargar el paquete de la aplicación completado para compartirlo con los usuarios de Teams o proporcionarlo al administrador para que el bot esté disponible en el catálogo de aplicaciones de inquilino.
8. **Iniciar un chat**. El proceso de configuración para agregar el bot de chat de Power Virtual Agents a Teams ha finalizado. Ahora puedes iniciar una conversación con el bot en un chat personal.

> [!div class="nextstepaction"]
> [Más información: Publicar el bot de Power Virtual Agents](/power-virtual-agents/publication-fundamentals-publish-channels)
