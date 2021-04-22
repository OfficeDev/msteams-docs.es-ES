---
title: Enviar identificador de inquilino e identificador de conversación a los encabezados de solicitud del bot
description: describe cómo enviar el identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: b3938b3011e09016f8594b2b17ba627d4922947b
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922536"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a><span data-ttu-id="01a98-103">Enviar identificador de inquilino e identificador de conversación a los encabezados de solicitud del bot</span><span class="sxs-lookup"><span data-stu-id="01a98-103">Send tenant ID and conversation ID to the request headers of the bot</span></span>

<span data-ttu-id="01a98-104">Las solicitudes salientes actuales al bot no contienen en el encabezado ni en la dirección URL ninguna información que ayude a los bots a enrutar el tráfico sin desempaquetar toda la carga.</span><span class="sxs-lookup"><span data-stu-id="01a98-104">The current outgoing requests to the bot do not contain in the header or URL any information that helps bots route the traffic without unpacking the entire payload.</span></span> <span data-ttu-id="01a98-105">Las actividades se envían al bot a través de una dirección URL similar a https://<your_domain>/api/messages.</span><span class="sxs-lookup"><span data-stu-id="01a98-105">The activities are sent to the bot through a URL similar to https://<your_domain>/api/messages.</span></span> <span data-ttu-id="01a98-106">Las solicitudes se reciben para mostrar el identificador de conversación y el identificador de inquilino en los encabezados.</span><span class="sxs-lookup"><span data-stu-id="01a98-106">Requests are received to show the conversation ID and tenant ID in the headers.</span></span>

## <a name="request-header-fields"></a><span data-ttu-id="01a98-107">Campos de encabezado de solicitud</span><span class="sxs-lookup"><span data-stu-id="01a98-107">Request header fields</span></span>

<span data-ttu-id="01a98-108">Se agregan dos campos de encabezado de solicitud no estándar a todas las solicitudes enviadas a bots, tanto para flujo asincrónico como para flujo sincrónico.</span><span class="sxs-lookup"><span data-stu-id="01a98-108">Two non-standard request header fields are added to all the requests sent to bots, for both asynchronous flow and synchronous flow.</span></span> <span data-ttu-id="01a98-109">En la tabla siguiente se proporcionan los campos de encabezado de solicitud y sus valores.</span><span class="sxs-lookup"><span data-stu-id="01a98-109">The following table provides the request header fields and their values.</span></span>

| <span data-ttu-id="01a98-110">Clave de campo</span><span class="sxs-lookup"><span data-stu-id="01a98-110">Field key</span></span> | <span data-ttu-id="01a98-111">Valor</span><span class="sxs-lookup"><span data-stu-id="01a98-111">Value</span></span> |
|----------------|-----------------|
| <span data-ttu-id="01a98-112">x-ms-conversation-id</span><span class="sxs-lookup"><span data-stu-id="01a98-112">x-ms-conversation-id</span></span> | <span data-ttu-id="01a98-113">El identificador de conversación correspondiente a la actividad de solicitud si corresponde y confirmado o comprobado.</span><span class="sxs-lookup"><span data-stu-id="01a98-113">The conversation ID corresponding to the request activity if applicable and confirmed or verified.</span></span> |
| <span data-ttu-id="01a98-114">x-ms-tenant-id</span><span class="sxs-lookup"><span data-stu-id="01a98-114">x-ms-tenant-id</span></span> | <span data-ttu-id="01a98-115">El identificador de inquilino correspondiente a la conversación en la actividad de solicitud.</span><span class="sxs-lookup"><span data-stu-id="01a98-115">The tenant ID corresponding to the conversation in the request activity.</span></span> |

<span data-ttu-id="01a98-116">Si el inquilino o el identificador de conversación no está presente en la actividad o no se validó en el lado del servicio, el valor está vacío.</span><span class="sxs-lookup"><span data-stu-id="01a98-116">If the tenant or conversation ID is not present in the activity or was not validated on the service side, the value is empty.</span></span>

![Campos de encabezado de solicitud](~/assets/images/bots/requestheaderfields.png)
