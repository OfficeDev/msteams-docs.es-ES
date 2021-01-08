---
title: Presentación de tarjetas
description: Describe las tarjetas y cómo se usan en bots, conectores y extensiones de mensajería
keywords: mensajes de tarjetas de bots de conectores
ms.openlocfilehash: 00c649a1339f05b782e03a2c0db5cba2445f66bc
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777927"
---
# <a name="cards"></a>Tarjetas

Una *tarjeta* es un contenedor de interfaz de usuario (UI) para información breve o relacionada. Las tarjetas pueden tener varias propiedades y datos adjuntos. Las tarjetas pueden incluir botones que pueden desencadenar [acciones de tarjeta.](~/task-modules-and-cards/cards/cards-actions.md)

## <a name="adaptive-cards"></a>Tarjetas adaptables

[Las tarjetas](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) adaptables son una nueva especificación entre productos para tarjetas en productos de Microsoft, como Bots, Cortana, Outlook y Windows. Son el tipo de tarjeta recomendado para el nuevo desarrollo de Teams. Para obtener información general del equipo de tarjetas adaptables, consulta [Información general sobre tarjetas adaptables.](/adaptive-cards) Puede usar tarjetas adaptables en cualquier lugar donde pueda usar tarjetas hero existentes, tarjetas de Office365 y tarjetas en miniatura.

Además de las tarjetas adaptables, Teams admite otros dos tipos de tarjetas:

* Tarjetas de conector, que se usan como parte de los conectores de Office 365.
* Tarjetas sencillas del marco de bot, como las tarjetas en miniatura y de imagen principal.

Estos tipos de tarjetas se describen más completamente en la Referencia [de tarjeta de Teams.](~/task-modules-and-cards/cards/cards-reference.md)

Teams usa tarjetas en tres lugares diferentes:

* Conectores
* Bots
* Extensiones de mensajería

## <a name="adaptive-cards-and-incoming-webhooks"></a>Tarjetas adaptables y webhooks entrantes

> [!NOTE]
>
> ✔ Todos los elementos de esquema de tarjetas adaptables nativas, excepto `Action.Submit`, son completamente compatibles.
>
> ✔ Las acciones admitidas [**son Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)y [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

## <a name="cards-in-connectors"></a>Tarjetas en conectores

Las tarjetas se definieron por primera vez como parte de Outlook y Office 365 y se usan como parte de conectores de Office 365. Al igual que muchas aplicaciones de Office 365, Teams admite conectores. Puede obtener más información sobre conectores en Conectores de [Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)para Microsoft Teams y encontrar la especificación de tarjetas en conectores en referencia de tarjeta de mensaje que se [puede usar.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Tarjetas en bots

Microsoft Bot Framework amplió la especificación de tarjetas agregando un conjunto de tarjetas predefinidas que los bots podrían usar como parte de los mensajes de bot. Teams admite bots con Bot Framework, pero admite un conjunto ligeramente diferente de estas tarjetas. Puede encontrar información general sobre las tarjetas en Bot Framework en [Agregar datos adjuntos de tarjeta enriquecciones a los mensajes.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Estas tarjetas se *denominan tarjetas sencillas* en Teams.

Los bots de Teams pueden usar cualquier tipo de tarjeta: simple, conector o adaptable. Las tarjetas compatibles con bots en Teams se detallan en la referencia [de tarjetas de Teams.](~/task-modules-and-cards/cards/cards-reference.md)  

## <a name="cards-in-messaging-extensions"></a>Tarjetas en extensiones de mensajería

[Las extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) también pueden devolver una tarjeta. Las extensiones de mensajería pueden usar cualquier tipo de tarjeta: simple, conector o adaptable. Estas tarjetas se encuentran en la referencia [de tarjetas de Teams.](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="card-reference"></a>Referencia de tarjeta

Todas las tarjetas usadas por Teams se enumeran en la Referencia [de tarjetas de Teams.](~/task-modules-and-cards/cards/cards-reference.md) Esta referencia también describe las diferencias entre tarjetas y tarjetas de Bot Framework en Teams.
