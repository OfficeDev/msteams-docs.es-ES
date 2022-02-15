---
title: Creación de un bot
description: Describe cómo crear bots en Microsoft Teams
ms.topic: how-to
keywords: creación de bots de teams
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: 6c95055b6e053c4319810acb8923ea3f3178f3b9
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821412"
---
# <a name="create-a-bot"></a>Creación de un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Todos los bots creados con el Microsoft Bot Framework están configurados y listos para funcionar en Microsoft Teams.

Para obtener más información, consulte [Bot Framework Documentation](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) for general information on bots.

## <a name="create-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

**Teams App Studio es** una herramienta que puede ayudar a crear el bot y un paquete de aplicación que hace referencia al bot. También contiene una biblioteca de control React y ejemplos configurables para tarjetas. Para obtener más información, consulta [Introducción a Teams App Studio](~/concepts/build-and-test/app-studio-overview.md). Los pasos siguientes suponen que estás configurando manualmente el bot y no usando **Teams App Studio**:

1. Cree el bot con este vínculo: https://dev.botframework.com/bots/new. **Asegúrese de agregar Microsoft Teams como canal de la lista de canales destacados después de crear el bot.** Puede volver a usar cualquier identificador de aplicación de Microsoft que haya generado si ya ha creado el manifiesto o el paquete de la aplicación.

   ![Página de registro de Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si no desea crear el bot en Azure, debe usar este vínculo  para crear un nuevo bot: https://dev.botframework.com/bots/new. Si hace clic en crear **un bot** en el portal de Bot Framework en su lugar, creará [el bot en Microsoft Azure](#bots-and-microsoft-azure) en su lugar.

2. Cree el bot con el [paquete Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, el [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk) o la [API de Bot Connector](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Pruebe el bot con el [Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Implemente el bot en un servicio en la nube, como [Microsoft Azure](https://azure.microsoft.com/). Como alternativa, ejecute la aplicación localmente y use un servicio de túnel como [ngrok](https://ngrok.com) para exponer un punto de conexión https:// para el bot, como `https://45az0eb1.ngrok.io/api/messages`.

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Bots y Microsoft Azure
> A partir de diciembre de 2017, el portal de Bot Framework está optimizado para registrar bots en Microsoft Azure. Estos son algunos aspectos que debe tener en cuenta:
>
> * El canal de Microsoft Teams para bots registrados en Azure es gratuito. Los mensajes enviados a Teams canal no contarán para los mensajes consumidos para el bot.
> * Aunque es posible crear un nuevo [bot framework](https://dev.botframework.com/bots/new) sin usar Azure, debe usar esa dirección URL (https://dev.botframework.com/bots/new)que ya no se expone en el portal de Bot Framework).
> * Al editar las propiedades de un bot existente en la lista de [bots de Bot Framework](https://dev.botframework.com/bots), como su "punto de conexión de mensajería", que es común al desarrollar un bot por primera vez, especialmente si usa [ngrok](https://ngrok.com), verá la columna "Estado de migración" y un botón azul "Migrar" que le llevará al portal de Microsoft Azure. No hagas clic en el botón "Migrar" a menos que eso sea lo que quieras hacer; en su lugar, haga clic en el nombre del bot y puede editar sus propiedades:</br>
   ![Editar propiedades del bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si registra el bot mediante Microsoft Azure, el código del bot no necesita *hospedarse en* Microsoft Azure.
> * Si registra un bot con Azure Portal, debe tener una cuenta Microsoft Azure usuario. Puede [crear una de forma gratuita](https://azure.microsoft.com/free/). Para comprobar su identidad al crear una, debe proporcionar una tarjeta de crédito, pero no se le cobrará; siempre es gratuito crear y usar bots con Microsoft Teams.
> * Ahora puedes usar App Studio para registrar/actualizar la información de la aplicación y el bot directamente en Microsoft Teams. Solo tendrás que usar Azure Portal para agregar o configurar otros canales de Bot Framework, como Direct Line, Web Chat, Skype y Facebook Messenger.

## <a name="see-also"></a>Vea también

[Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).