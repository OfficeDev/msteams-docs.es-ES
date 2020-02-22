---
title: Crear un bot
description: Describe cómo crear bots en Microsoft Teams.
keywords: creación de bots de Teams
ms.date: 12/07/2018
ms.openlocfilehash: 6d8441cb3bc89ae7a923cad72567eb52dd99dc4b
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228020"
---
# <a name="create-a-bot"></a>Crear un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Todos los bots creados con Microsoft bot Framework están configurados y preparados para trabajar en Microsoft Teams.

Consulte la [documentación de bot Framework](/azure/bot-service/?view=azure-bot-service-3.0) para obtener información general sobre bots.

## <a name="create-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

*Teams App Studio* es una herramienta que puede ayudarle a crear su bot y un paquete de aplicaciones que hace referencia a su bot. También contiene una biblioteca de control React y ejemplos configurables para tarjetas. Consulte [Introducción a Teams App Studio](~/concepts/build-and-test/app-studio-overview.md). En los pasos siguientes se da por sentado que la mano está configurando su bot y no usando *Team App Studio*.

1. Cree el bot con este vínculo: https://dev.botframework.com/bots/new. **Asegúrese de agregar Microsoft Teams como canal de la lista de canales destacados después de crear el bot.** Puede volver a usar cualquier identificador de aplicación de Microsoft que haya generado si ya ha creado el manifiesto o el paquete de la aplicación.

   ![Página de registro de Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si no desea crear el bot en Azure, **debe** usar este vínculo para crear un nuevo bot: https://dev.botframework.com/bots/new. Si hace clic en el botón *crear un bot* en el portal del marco de trabajo de bot, en su lugar, [creará su bot en Microsoft Azure](#bots-and-microsoft-azure) .

2. Cree el bot mediante el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) , el [SDK de bot](https://github.com/microsoft/botframework-sdk)o la [API del conector de bot](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference). *Vea también* [ejemplos del marco de bot](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

3. Pruebe el bot mediante el [emulador de bot Framework](https://docs.microsoft.com/bot-framework/debug-bots-emulator).

4. Implemente el bot en un servicio en la nube, como [Microsoft Azure](https://azure.microsoft.com/). Como alternativa, ejecute la aplicación de forma local y use un servicio de túnel (por ejemplo, [ngrok](https://ngrok.com) para exponer un extremo de https:// `https://45az0eb1.ngrok.io/api/messages`para su bot, por ejemplo,.

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Bots y Microsoft Azure
> A partir de diciembre de 2017, el portal de bot Framework está optimizado para registrar bots en Microsoft Azure. Estos son algunos aspectos que debe tener en cuenta:
>
> * El canal de Microsoft Teams para bots registrados en Azure es gratuito. Los mensajes enviados a través del canal de Microsoft Teams no se cuentan para los mensajes consumidos para el bot.
> * Aunque es posible [crear un nuevo bot Framework de bot](https://dev.botframework.com/bots/new) sin usar Azure, debe usar esa dirección URL (https://dev.botframework.com/bots/new), que ya no está expuesta en el portal de la estructura de bot.
> * Cuando se editan las propiedades de un bot existente en la [lista de los bots en el marco de bot](https://dev.botframework.com/bots) (por ejemplo, el "extremo de mensajería"), que es común al desarrollar por primera vez un bot, sobre todo si usa [ngrok](https://ngrok.com), verá la columna "estado de la migración" y un botón "migrar" de color azul que le llevará al portal de Microsoft Azure. No haga clic en el botón "migrar" a menos que sea lo que desea hacer; en su lugar, haga clic en el nombre del bot y podrá editar sus propiedades:</br>
   ![Editar propiedades del bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si registra el bot con Microsoft Azure, no es necesario que el código de bot se *hospede* en Microsoft Azure.
> * Si registra un bot con Microsoft Azure Portal, debe tener una cuenta de Microsoft Azure. Puede [crear una de forma gratuita](https://azure.microsoft.com/free/). Para comprobar su identidad al crear una, debe proporcionar una tarjeta de crédito, pero no se cargará. siempre es gratuito crear y usar bots con Microsoft Teams.
> * Ahora puede usar App Studio para registrar o actualizar la información de la aplicación y el bot directamente en Microsoft Teams. Solo tendrá que usar el portal de Microsoft Azure para agregar o configurar otros canales de bot Framework, como Direct line, web chat, Skype y Facebook Messenger.
