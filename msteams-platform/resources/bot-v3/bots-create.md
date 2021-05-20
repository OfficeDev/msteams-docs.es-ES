---
title: Creación de un bot
description: Describe cómo crear bots en Microsoft Teams
ms.topic: how-to
keywords: creación de bots de equipos
localization_priority: Normal
ms.date: 12/07/2018
ms.openlocfilehash: 67aa3e2cfd1950dced84785a9f6f35cfd4d5ff85
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566778"
---
# <a name="create-a-bot"></a>Creación de un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Todos los bots creados con el Microsoft Bot Framework están configurados y listos para funcionar en Microsoft Teams.

Para obtener más información, consulte [Documentación de Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) para obtener información general sobre bots.

## <a name="create-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

**Teams App Studio** es una herramienta que puede ayudar a crear el bot y un paquete de aplicación que hace referencia al bot. También contiene una biblioteca de control React y ejemplos configurables para tarjetas. Para obtener más información, consulte [Introducción a Teams App Studio](~/concepts/build-and-test/app-studio-overview.md). Los pasos siguientes suponen que está configurando a mano el bot y no utilizando **Teams App Studio:**

1. Cree el bot mediante este vínculo: https://dev.botframework.com/bots/new . **Asegúrese de agregar Microsoft Teams como canal de la lista de canales destacados después de crear el bot.** Puede volver a usar cualquier identificador de aplicación de Microsoft que haya generado si ya ha creado el manifiesto o el paquete de la aplicación.

   ![Página de registro de Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si no desea crear el bot en Azure, **debe** usar este vínculo para crear un nuevo bot: https://dev.botframework.com/bots/new . Si hace clic en crear **un bot** en el portal de Bot Framework en su lugar, creará el bot en [Microsoft Azure en](#bots-and-microsoft-azure) su lugar.

2. Cree el bot mediante el paquete [microsoft.bot.connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, el [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk)o la API de Bot [Connector](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Pruebe el bot con la [Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Implemente el bot en un servicio en la nube, como [Microsoft Azure](https://azure.microsoft.com/). Como alternativa, ejecute la aplicación localmente y use un servicio de tunelización como [ngrok](https://ngrok.com) para exponer un punto de conexión https:// para el bot, como `https://45az0eb1.ngrok.io/api/messages` .

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Bots y Microsoft Azure
> A partir de diciembre de 2017, el portal de Bot Framework está optimizado para registrar bots en Microsoft Azure. Estos son algunos aspectos que debe tener en cuenta:
>
> * El canal de Microsoft Teams para bots registrados en Azure es gratuito. Los mensajes enviados a través del canal de Teams no contarán para los mensajes consumidos para el bot.
> * Aunque es posible [crear un nuevo bot de Bot Framework](https://dev.botframework.com/bots/new) sin usar Azure, debe usar esa dirección URL ( , que ya no se expone en bot framework https://dev.botframework.com/bots/new) portal.
> * Al editar las propiedades de un bot existente en la [lista de bots en Bot Framework,](https://dev.botframework.com/bots) como su "punto de conexión de mensajería", que es común al desarrollar por primera vez un bot, especialmente si usa [ngrok,](https://ngrok.com)verá la columna "Estado de migración" y un botón azul "Migrar" que le llevará al portal de Microsoft Azure. No haga clic en el botón "Migrar" a menos que eso sea lo que desea hacer; en su lugar, haga clic en el nombre del bot y puede editar sus propiedades:</br>
   ![Editar propiedades del bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si registra el bot con Microsoft Azure, el código del bot no es necesario *hospedarse* en Microsoft Azure.
> * Si registra un bot con Microsoft Azure Portal, debe tener una cuenta de Microsoft Azure. Puede [crear una de forma gratuita](https://azure.microsoft.com/free/). Para verificar su identidad al crear una, debe proporcionar una tarjeta de crédito, pero no se cargará; siempre es gratis crear y usar bots con Microsoft Teams.
> * Ahora puede usar App Studio para registrar/actualizar la información de aplicaciones y bots directamente en Microsoft Teams. Solo tendrás que usar el portal de Microsoft Azure para agregar o configurar otros canales de Bot Framework como Línea directa, Chat web, Skype y Facebook Messenger.

## <a name="see-also"></a>Vea también

[Muestras de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).