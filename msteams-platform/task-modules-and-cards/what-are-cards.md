---
title: Tarjetas
description: Describe las tarjetas y cómo se usan en bots, conectores y extensiones de mensajería
ms.localizationpriority: medium
keywords: mensajes de tarjetas de bots de conectores
ms.topic: overview
ms.openlocfilehash: 50e8aa690d4de4dc5464a7e42dbc017e87afe35a
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475800"
---
# <a name="cards"></a>Tarjetas

Una tarjeta es un contenedor de interfaz de usuario (UI) para información breve o relacionada. Las tarjetas pueden tener varias propiedades y datos adjuntos y pueden incluir botones, que desencadenan [acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md). Con las tarjetas, puede organizar la información en grupos y dar a los usuarios la oportunidad de interactuar con partes específicas de la información.

Los bots para Teams admiten los siguientes tipos de tarjetas: tarjeta adaptable, tarjeta de héroe, tarjeta de lista, tarjeta de conector Office 365, tarjeta de recibo, tarjeta de inicio de sesión, tarjeta miniatura y colecciones de tarjetas. Puede agregar formato de texto enriquecido a las tarjetas mediante Markdown o HTML, según el tipo de tarjeta. Tarjetas usadas por bots y extensiones de mensajería en Microsoft Teams, agregar y responder a estas acciones de tarjeta, `openUrl` , , , y `messageBack` `imBack` `invoke` `signin` .

Teams usa tarjetas en tres lugares diferentes:

* Conectores
* Bots
* Extensiones de mensajería

## <a name="cards-in-connectors"></a>Tarjetas en conectores

Las tarjetas se definieron primero como parte de Outlook y Office 365 y ahora se usan como parte de Office 365 Connectors. Al igual que muchas Office 365, Teams admite conectores. Para obtener más información, [vea Office 365 Connectors for Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md). Puede encontrar la especificación de las tarjetas en conectores en [referencia de tarjeta de mensaje de acción.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Tarjetas en bots

El Microsoft Bot Framework amplía la especificación de tarjetas agregando un conjunto de tarjetas predefinidas que los bots pueden usar como parte de los mensajes de bot. Teams admite bots con Bot Framework, pero admite un conjunto diferente de estas tarjetas. La información general sobre las tarjetas en Bot Framework se puede encontrar en [agregar datos adjuntos de tarjetas enriquecciones a los mensajes.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Estas tarjetas se denominan tarjetas sencillas en Teams.

Los bots de Teams pueden usar tarjetas sencillas, tarjetas de conector o tarjetas adaptables. [Los tipos de tarjetas](~/task-modules-and-cards/cards/cards-reference.md) proporcionan información sobre tarjetas, admitidas por bots en Teams.

## <a name="cards-in-messaging-extensions"></a>Tarjetas en extensiones de mensajería

[Las extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) también pueden devolver una tarjeta. Las extensiones de mensajería pueden usar tarjetas sencillas, tarjetas de conector o tarjetas adaptables. Estas tarjetas se encuentran en [tipos de tarjetas](~/task-modules-and-cards/cards/cards-reference.md).

## <a name="types-of-cards"></a>Tipos de tarjetas

Todas las tarjetas usadas por Teams se enumeran en [tipos de tarjetas](~/task-modules-and-cards/cards/cards-reference.md). Esta referencia también describe las diferencias entre las tarjetas de Bot Framework y las tarjetas Teams.

## <a name="adaptive-cards"></a>Tarjetas adaptables

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

[Las tarjetas](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) adaptables son una nueva especificación entre productos para tarjetas en productos de Microsoft, incluidos bots, Cortana, Outlook y Windows. Son el tipo de tarjeta recomendado para el nuevo Teams desarrollo. Para obtener información general del equipo de tarjetas adaptables, vea [Adaptive Cards overview](/adaptive-cards). Puedes usar tarjetas adaptables en cualquier lugar que uses tarjetas de héroe existentes, tarjetas Office 365 y tarjetas en miniatura.

Además de las tarjetas adaptables, Teams admite otros dos tipos de tarjetas:

* Tarjetas de conector: se usan como parte de Office 365 conectores.
* Tarjetas sencillas: se usan desde Bot Framework, como la miniatura y las tarjetas de héroe.

### <a name="adaptive-cards-and-incoming-webhooks"></a>Tarjetas adaptables y webhooks entrantes

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * Todos los elementos nativos del esquema de tarjeta adaptable, excepto `Action.Submit` , son totalmente compatibles.
> * Las acciones admitidas [**son Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)y [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Las tarjetas adaptables con webhooks entrantes permiten usar las capacidades enriquecibles y flexibles de las tarjetas adaptables. Envía datos mediante webhooks entrantes en Teams desde su servicio web.

## <a name="support-for-aad-object-id-and-upn-in-user-mention"></a>Compatibilidad con el identificador de objeto de AAD y UPN en la mención del usuario 

Los bots con tarjetas adaptables admiten identificadores de mención de usuario, como id. de objeto de AAD y nombre de principio de usuario (UPN), además de los identificadores existentes. Los webhooks entrantes comienzan a admitir la mención de usuario en la tarjeta adaptable con el identificador de objeto de AAD y UPN.

## <a name="see-also"></a>Vea también

* [Dar formato a las tarjetas Teams](~/task-modules-and-cards/cards/cards-format.md)
* [Diseñar tarjetas adaptables](~/task-modules-and-cards/cards/design-effective-cards.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Tipos de tarjetas](~/task-modules-and-cards/cards/cards-reference.md)