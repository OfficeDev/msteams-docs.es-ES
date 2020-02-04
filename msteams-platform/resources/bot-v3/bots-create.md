---
title: Crear un bot
description: Describe cómo crear bots en Microsoft Teams.
keywords: creación de bots de Teams
ms.date: 12/07/2018
ms.openlocfilehash: cb2d0974baf1d36a4acf077c219eb12449a5721a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675758"
---
# <a name="create-a-bot"></a>Crear un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Todos los bots creados con Microsoft bot Framework están configurados y preparados para trabajar en Microsoft Teams.

Consulte la [documentación de bot Framework](/azure/bot-service/?view=azure-bot-service-3.0) para obtener información general sobre bots.

## <a name="create-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

*Teams App Studio* es una herramienta que puede ayudarle a crear su bot y un paquete de aplicaciones que hace referencia a su bot. También contiene una biblioteca de control de reAct y ejemplos configurables para las tarjetas. Consulte [Introducción a teams App Studio](~/concepts/build-and-test/app-studio-overview.md). En los pasos siguientes se da por sentado que la mano está configurando su bot y no usando *Team App Studio*.

1. Cree el bot con este vínculo: https://dev.botframework.com/bots/new. **Asegúrese de agregar Microsoft Teams como canal desde la lista de canales destacados después de crear el bot.** No dude en volver a usar cualquier identificador de aplicación de Microsoft que haya generado si ya ha creado el manifiesto o el paquete de la aplicación.

   ![Página de registro de bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si no desea crear el bot en Azure, **debe** usar este vínculo para crear un nuevo bot: https://dev.botframework.com/bots/new. Si hace clic en el botón *crear un bot* en el portal del marco de trabajo de bot, en su lugar, [creará su bot en Microsoft Azure](#bots-and-microsoft-azure) .

2. Cree el bot mediante el paquete de NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) , el paquete NPM [de botbuilder-Teams](https://www.npmjs.com/package/botbuilder-teams) o la [API del conector de bot](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Pruebe el bot mediante el [emulador de bot Framework](https://docs.microsoft.com/bot-framework/debug-bots-emulator).

4. Implemente el bot en un servicio en la nube, como [Microsoft Azure](https://azure.microsoft.com/). Como alternativa, ejecute la aplicación de forma local y use un servicio de túnel (por ejemplo, [ngrok](https://ngrok.com) para exponer un extremo de https:// `https://45az0eb1.ngrok.io/api/messages`para su bot, por ejemplo,.

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Bots y Microsoft Azure
> A partir de diciembre de 2017, el portal de bot Framework está optimizado para registrar bots en Microsoft Azure. Estas son algunas de las cosas que debe saber:
>
> * El canal de Microsoft Teams para bots registrados en Azure es gratuito. Los mensajes enviados a través del canal de Microsoft Teams no se cuentan para los mensajes consumidos para el bot.
> * Aunque es posible [crear un nuevo bot Framework de bot](https://dev.botframework.com/bots/new) sin usar Azure, debe usar esa dirección URL (https://dev.botframework.com/bots/new), que ya no está expuesta en el portal de la estructura de bot.
> * Cuando se editan las propiedades de un bot existente en la [lista de los bots en el marco de bot](https://dev.botframework.com/bots) (por ejemplo, el "extremo de mensajería"), que es común al desarrollar por primera vez un bot, sobre todo si usa [ngrok](https://ngrok.com), verá la columna "estado de la migración" y un botón "migrar" de color azul que le llevará al portal de Microsoft Azure. No haga clic en el botón "migrar" a menos que sea lo que desea hacer; en su lugar, haga clic en el nombre del bot y podrá editar sus propiedades:</br>
   ![Editar propiedades de bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si registra el bot con Microsoft Azure, no es necesario que el código de bot se *hospede* en Microsoft Azure.
> * Si registra un bot con el portal de Microsoft Azure, debe tener una cuenta de Microsoft Azure. Puede [crear uno de forma gratuita](https://azure.microsoft.com/free/). Para comprobar su identidad al crear una, debe proporcionar una tarjeta de crédito, pero no se cargará. siempre es gratuito crear y usar bots con Microsoft Teams.
> * Ahora puede usar App Studio para registrar o actualizar la información de la aplicación y el bot directamente en Microsoft Teams. Solo tendrá que usar el portal de Microsoft Azure para agregar o configurar otros canales de bot Framework, como Direct line, web chat, Skype y Facebook Messenger.
