---
title: Presentación de tarjetas
description: Describe las tarjetas y cómo se usan en bots, conectores y extensiones de mensajería
localization_priority: Normal
ms.topic: conceptual
keywords: mensajes de tarjetas de bots de conectores
ms.openlocfilehash: acf5dc95b742a433c092be9e293d589b5919bb4d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020271"
---
# <a name="cards"></a>Tarjetas

Una *tarjeta* es un contenedor de interfaz de usuario (UI) para información breve o relacionada. Las tarjetas pueden tener varias propiedades y datos adjuntos. Las tarjetas pueden incluir botones que pueden desencadenar [acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).

## <a name="adaptive-cards"></a>Tarjetas adaptables

[Las tarjetas](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) adaptables son una nueva especificación entre productos para tarjetas en productos de Microsoft, incluidos Bots, Cortana, Outlook y Windows. Son el tipo de tarjeta recomendado para el nuevo desarrollo de Teams. Para obtener información general del equipo de tarjetas adaptables, [vea Adaptive Cards Overview](/adaptive-cards). Puede usar tarjetas adaptables en cualquier lugar donde pueda usar tarjetas hero existentes, tarjetas de Office365 y tarjetas en miniatura.

Además de las tarjetas adaptables, Teams admite otros dos tipos de tarjetas:

* Tarjetas de conector, que se usan como parte de conectores de Office 365.
* Tarjetas sencillas del marco del bot, como la miniatura y las tarjetas de héroe.

Estos tipos de tarjetas se describen más completamente en la [referencia de tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md).

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

Las tarjetas se definieron por primera vez como parte de Outlook y Office 365 y se usan como parte de Office 365 Connectors. Al igual que muchas aplicaciones de Office 365, Teams admite conectores. Puede obtener más información sobre conectores en [Office 365 Connectors para Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)y encontrar la especificación de tarjetas en conectores en Referencia de tarjeta de mensaje de [acción.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Tarjetas en bots

Microsoft Bot Framework extendió la especificación de tarjetas agregando un conjunto de tarjetas predefinidas que los bots podrían usar como parte de los mensajes de bot. Teams admite bots con Bot Framework, pero admite un conjunto ligeramente diferente de estas tarjetas. Puede encontrar información general sobre las tarjetas en Bot Framework en [Agregar datos adjuntos de tarjetas enriquecciones a los mensajes.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Estas tarjetas se *denominan tarjetas sencillas* en Teams.

Los bots de Teams pueden usar cualquier tipo de tarjeta: simple, conector o adaptable. Las tarjetas compatibles con bots en Teams se detallan en [Referencia de tarjeta de Teams.](~/task-modules-and-cards/cards/cards-reference.md)  

## <a name="cards-in-messaging-extensions"></a>Tarjetas en extensiones de mensajería

[Las extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) también pueden devolver una tarjeta. Las extensiones de mensajería pueden usar cualquier tipo de tarjeta: simple, conector o adaptable. Estas tarjetas se encuentran en la [referencia de tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md).

## <a name="card-reference"></a>Referencia de tarjeta

Todas las tarjetas usadas por Teams se enumeran en la [referencia de tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md). Esta referencia también describe las diferencias entre las tarjetas de Bot Framework y las tarjetas de Teams.
