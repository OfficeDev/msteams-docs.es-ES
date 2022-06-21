---
title: Creación de un bot
description: En este módulo, aprenderá a crear bots mediante el Microsoft Bot Framework y listos para trabajar en Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: a669b11baef8dc31a662ea2ad178ad3488f2d69e
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189525"
---
# <a name="create-a-bot"></a>Creación de un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Todos los bots creados con el Microsoft Bot Framework están configurados y listos para funcionar en Microsoft Teams.

Para obtener más información, consulte [La documentación de Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) para obtener información general sobre los bots.

## <a name="create-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

**Teams App Studio** es una herramienta que puede ayudar a crear el bot y un paquete de aplicación que hace referencia al bot. También contiene una biblioteca de control React y ejemplos configurables para tarjetas. Para obtener más información, consulte [Introducción a Teams App Studio](~/concepts/build-and-test/app-studio-overview.md). En los pasos siguientes se da por hecho que está configurando manualmente el bot y que no usa **Teams App Studio**:

1. Cree el bot mediante [Bot Framework](https://dev.botframework.com/bots/new). **Asegúrese de agregar Microsoft Teams como canal de la lista de canales destacados después de crear el bot.** Puede volver a usar cualquier identificador de aplicación de Microsoft que haya generado si ya ha creado el manifiesto o el paquete de la aplicación.

   ![Página de registro de Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si no desea crear el bot en Azure, **debe** usar este vínculo para crear un nuevo bot: [Bot Framework](https://dev.botframework.com/bots/new). Si en su lugar hace clic en **Crear un bot** en el portal de Bot Framework, creará [el bot en Microsoft Azure](#bots-and-microsoft-azure) en su lugar.

2. Compile el bot mediante el paquete [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, el [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk) o la [API de Bot Connector](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Pruebe el bot con el [Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Implemente el bot en un servicio en la nube, como [Microsoft Azure](https://azure.microsoft.com/). Como alternativa, ejecute la aplicación localmente y use un servicio de tunelización como [ngrok](https://ngrok.com) para exponer un punto de conexión de https:// para el bot, como `https://45az0eb1.ngrok.io/api/messages`.

> [!NOTE]
>
> ## <a name="bots-and-microsoft-azure"></a>Bots y Microsoft Azure
>
> A partir de diciembre de 2017, el portal de Bot Framework está optimizado para registrar bots en Microsoft Azure. Estos son algunos aspectos que debe tener en cuenta:
>
> * El canal de Microsoft Teams para bots registrados en Azure es gratuito. Los mensajes enviados a través del canal Teams no contarán para los mensajes consumidos para el bot.
> * Aunque es posible [crear un nuevo bot de Bot Framework](https://dev.botframework.com/bots/new) sin usar Azure, debe usar [crear un nuevo bot de Bot Framework](https://dev.botframework.com/bots/new), que ya no se expone en el portal de Bot Framework.
> * Al editar las propiedades de un bot existente en la [lista de bots de Bot Framework](https://dev.botframework.com/bots), como su "punto de conexión de mensajería", que es común al desarrollar por primera vez un bot, especialmente si usa [ngrok](https://ngrok.com), verá la columna "Estado de la migración" y un botón azul "Migrar" que le llevará al portal de Microsoft Azure. No haga clic en el botón "Migrar" a menos que eso sea lo que quiere hacer; en su lugar, haga clic en el nombre del bot y puede editar sus propiedades:</br>
   ![Editar propiedades del bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si registra el bot con Microsoft Azure, no es necesario *hospedar* el código del bot en Microsoft Azure.
> * Si registra un bot mediante Azure Portal, debe tener una cuenta de Microsoft Azure. Puede [crear una de forma gratuita](https://azure.microsoft.com/free/). Para comprobar su identidad al crear una, debe proporcionar una tarjeta de crédito, pero no se le cobrará; siempre es gratis crear y usar bots con Teams.
> * Ahora puede usar App Studio para registrar o actualizar la información de aplicaciones y bots directamente dentro de Teams. Solo tendrá que usar la Azure Portal para agregar o configurar otros canales de Bot Framework, como Direct Line, Chat en web, Skype y Facebook Messenger.

> [!WARNING]
>
>* Si ha estado usando App Studio, le recomendamos que pruebe el Portal para desarrolladores para configurar, distribuir y administrar las aplicaciones de Teams. App Studio quedará obsoleto a partir del 30 de junio de 2022

## <a name="see-also"></a>Consulte también

[Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
