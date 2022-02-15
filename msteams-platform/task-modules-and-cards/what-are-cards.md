---
title: Tarjetas
description: Describe las tarjetas y cómo se usan en bots, conectores y extensiones de mensajería
ms.localizationpriority: high
keywords: conectores bots tarjetas mensajería
ms.topic: overview
ms.openlocfilehash: 7ab05607e7c5abf897c790bb777e5c697edc9e08
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821587"
---
# <a name="cards"></a>Tarjetas

Una tarjeta es un contenedor de interfaz de usuario (UI) para información breve o relacionada. Las tarjetas pueden tener diversas propiedades y datos adjuntos y pueden incluir botones para activar las [acciones de las tarjetas](~/task-modules-and-cards/cards/cards-actions.md). Con las tarjetas, puede organizar la información en grupos y dar a los usuarios la oportunidad de interactuar con partes específicas de la información.

Los bots para Teams admiten los siguientes tipos de tarjetas:
 
- Tarjeta adaptable
- Tarjeta de héroe
- Tarjeta de lista
- Tarjeta conector de Office 365
- Tarjeta de recibo
- Tarjeta de inicio de sesión
- Tarjeta miniatura
- Colecciones de tarjetas

Puede agregar formato de texto enriquecido a las tarjetas mediante Markdown o HTML, según el tipo de tarjeta. Tarjetas usadas por bots y extensiones de mensajería en Microsoft Teams, agregar y responder a estas acciones de tarjeta, `openUrl`, `messageBack`, `imBack`, `invoke` y `signin`.

Teams usa tarjetas en tres lugares diferentes:

* Conectores
* Bots
* Extensiones de mensajería

## <a name="cards-in-connectors"></a>Tarjetas en conectores

Las tarjetas se definieron primero como parte de Outlook y Office 365 y ahora se usan como parte de Conectores de Office 365. Al igual que muchas aplicaciones de Office 365, Teams admite conectores. Para obtener más información, vea [Conectores de Office 365 para Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md). Puede encontrar la especificación de las tarjetas en conectores en [referencia de tarjeta de mensaje de acción](/outlook/actionable-messages/card-reference).

## <a name="cards-in-bots"></a>Tarjetas en bots

El Microsoft Bot Framework amplía la especificación de tarjetas agregando un conjunto de tarjetas predefinidas que los bots pueden usar como parte de los mensajes de bot. Teams admite bots que usan el Bot Framework, pero admite un conjunto diferente de estas tarjetas. La información general sobre las tarjetas de Bot Framework se puede encontrar en [agregar datos adjuntos de tarjetas enriquecidas a mensajes](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards). Estas tarjetas se denominan tarjetas sencillas en Teams.

Los bots de Teams pueden usar tarjetas sencillas, tarjetas de conector o tarjetas adaptables. [Tipos de tarjetas](~/task-modules-and-cards/cards/cards-reference.md) proporciona información sobre las tarjetas compatibles con bots en Teams.

## <a name="cards-in-messaging-extensions"></a>Tarjetas en extensiones de mensajería

Las [extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) también pueden devolver una tarjeta. Las extensiones de mensajería pueden usar tarjetas sencillas, tarjetas de conector o tarjetas adaptables. Estas tarjetas se encuentran en [tipos de tarjetas](~/task-modules-and-cards/cards/cards-reference.md).

## <a name="types-of-cards"></a>Tipos de tarjetas

Todas las tarjetas usadas por Teams se enumeran en [tipos de tarjetas](~/task-modules-and-cards/cards/cards-reference.md). Esta referencia también describe las diferencias entre las tarjetas de Bot Framework y las tarjetas en Teams.

## <a name="adaptive-cards"></a>Tarjetas adaptables

Las [tarjetas adaptables](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) son una nueva especificación entre productos para tarjetas en productos de Microsoft, incluidos bots, Cortana, Outlook y Windows. Son el tipo de tarjeta recomendado para el nuevo desarrollo de Teams. Para obtener información general del equipo de tarjetas adaptables, consulte [Información general sobre tarjetas adaptables adaptable](/adaptive-cards). Puedes usar tarjetas adaptables en cualquier lugar que use tarjetas de héroe existentes, tarjetas de Office 365 y tarjetas en miniatura.

Además de las tarjetas adaptables, Teams admite otros dos tipos de tarjetas:

* Tarjetas de conector: se usan como parte de los conectores de Office 365.
* Tarjetas sencillas: se usan desde el Bot Framework, como las tarjetas de miniatura y las tarjetas de héroe.

### <a name="people-picker-in-adaptive-cards"></a>Selector de usuarios en Tarjetas adaptables

El [selector de usuarios](cards/people-picker.md#people-picker-in-adaptive-cards) agregado como control de entrada en Tarjetas adaptables habilita la búsqueda y la selección de usuarios. Puede usarlo en chats, canales, módulos de tareas y pestañas. Los clientes móviles y de escritorio admiten el selector de usuarios, lo que proporciona una experiencia de escritura en línea. 

### <a name="type-ahead-search-in-adaptive-cards"></a>Búsqueda de escritura anticipada en Tarjetas adaptables  

La búsqueda de escritura anticipada agregada como control de entrada en tarjetas adaptables habilita la experiencia de [búsqueda dinámica](~/task-modules-and-cards/cards/dynamic-search.md) desde un conjunto de datos cargado dinámicamente. También permite a los usuarios realizar una búsqueda estática de escritura anticipada dentro de una lista con un número limitado de opciones. Los clientes móviles y de escritorio admiten la experiencia de búsqueda dinámica de escritura anticipada. 

### <a name="adaptive-cards-and-incoming-webhooks"></a>Tarjetas adaptables y webhooks entrantes

> [!NOTE]
> * Todos los elementos de esquema de tarjetas adaptables nativas, excepto `Action.Submit`, son completamente compatibles.
> * Las acciones compatibles son [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) y [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Las tarjetas adaptables con webhooks entrantes permiten usar las funcionalidades enriquecidas y flexibles de las tarjetas adaptables. Envía datos mediante webhooks entrantes en Teams desde su servicio web.

## <a name="support-for-azure-ad-object-id-and-upn-in-user-mention"></a>Compatibilidad con el identificador de objeto de Azure AD y el UPN en la mención de usuario 

Los bots con Tarjetas adaptables admiten identificadores de mención de usuario, como el identificador de objeto de Microsoft Azure Active Directory (Azure AD) y el nombre principal de usuario (UPN), además de los identificadores existentes. Los webhooks entrantes comienzan a admitir la mención de usuario en Tarjetas adaptables con el identificador de objeto de Azure AD y el UPN.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Tipos de tarjetas](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="see-also"></a>Vea también

* [Dar formato a las tarjetas en Teams](~/task-modules-and-cards/cards/cards-format.md)
* [Diseñar tarjetas adaptables](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Tarjetas adaptables en bots](../bots/how-to/conversations/conversation-messages.md#adaptive-cards)