---
title: Introducción a las tarjetas
description: Describe las tarjetas y cómo se usan en bots, conectores y extensiones de mensajería.
keywords: mensajes de conectores de tarjetas de bots
ms.openlocfilehash: a260313c6e9442ce7bd76524e41e6465617bafb5
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675910"
---
# <a name="cards"></a>Tarjetas

Una *tarjeta* es un contenedor de interfaz de usuario (UI) para datos cortos o relacionados. Las tarjetas pueden tener varias propiedades y datos adjuntos. Las tarjetas pueden incluir botones que pueden desencadenar [acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).

## <a name="adaptive-cards"></a>Tarjetas adaptables

Las [tarjetas adaptables](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) son una nueva especificación cruzada de producto para las tarjetas de los productos de Microsoft, incluidos los bots, Cortana, Outlook y Windows. Son el tipo de tarjeta recomendado para el desarrollo de nuevos equipos. Para obtener información general del equipo de tarjetas adaptables, vea información [General sobre las tarjetas adaptables](/adaptive-cards). Puede usar tarjetas adaptables en cualquier lugar en el que pueda usar tarjetas de héroe, tarjetas de Office365 y tarjetas de miniaturas existentes.

Además de las tarjetas adaptables, Teams admite otros dos tipos de tarjetas:

* Tarjetas de conector, usadas como parte de los conectores de Office 365.
* Tarjetas sencillas desde el marco de bot, como las tarjetas de miniaturas y Heroes.

Estos tipos de tarjeta se describen más detalladamente en la referencia de la [tarjeta Teams](~/task-modules-and-cards/cards/cards-reference.md).

Microsoft Teams usa tarjetas en tres lugares diferentes:

* Conectores
* Bots
* Extensiones de mensajería

## <a name="cards-in-connectors"></a>Tarjetas en conectores

Las tarjetas se definieron por primera vez como parte de Outlook y Office 365, y se usan como parte de conectores de Office 365. Como muchas aplicaciones de Office 365, Teams admite conectores. Puede obtener más información sobre conectores en [conectores de Office 365 para Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)y buscar la especificación de tarjetas en conectores en la referencia de la [tarjeta de mensaje accionable](/outlook/actionable-messages/card-reference).

## <a name="cards-in-bots"></a>Tarjetas en bots

Microsoft bot Framework amplió la especificación de las tarjetas agregando un conjunto de tarjetas predefinidas que los bots podrían usar como parte de los mensajes de bot. Microsoft Teams admite bots mediante el marco de bot, pero admite un conjunto de estas tarjetas ligeramente distinto. La información general sobre las tarjetas en el marco de trabajo de bot puede encontrarse en [Agregar datos adjuntos de tarjeta enriquecida a los mensajes](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards). Estas tarjetas se denominan *tarjetas sencillas* en Microsoft Teams.

Los bots de Teams pueden usar cualquier tipo de tarjeta: simple, conector o adaptable. Las tarjetas que son compatibles con bots en Teams se detallan en [Team Cards Reference](~/task-modules-and-cards/cards/cards-reference.md).  

## <a name="cards-in-messaging-extensions"></a>Tarjetas en extensiones de mensajería

[Las extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) también pueden devolver una tarjeta. Las extensiones de mensajería pueden usar cualquier tipo de tarjeta: simple, conector o adaptable. Estas tarjetas se encuentran en la [referencia de la tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md).

## <a name="card-reference"></a>Referencia de tarjeta

Todas las tarjetas que usan los equipos se muestran en la referencia de la [tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md). Esta referencia también describe las diferencias entre las tarjetas y las tarjetas de .NET Framework en Microsoft Teams.
