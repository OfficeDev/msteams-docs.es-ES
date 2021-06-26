---
title: Crear pestañas de conversación
author: surbhigupta
description: Crear chat de sub entity conversacional para las pestañas del canal
keywords: Canal de pestañas de teams configurable
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: fbc5e90842c892cfb7e14f845563d7d2ffb397bb
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140267"
---
# <a name="create-conversational-tabs"></a>Crear pestañas de conversación

Las sub entidades conversacionales proporcionan una forma de permitir que los usuarios tengan conversaciones sobre las sub entidades en la pestaña, como tareas específicas, pacientes y oportunidades de ventas, en lugar de analizar toda la pestaña, también conocida como entidad. Un canal tradicional o una pestaña configurable permite al usuario tener una conversación sobre una pestaña, pero el usuario requiere una conversación más centrada. El requisito de una conversación más centrada puede surgir si hay demasiado contenido para tener una discusión centralizada o porque el contenido cambió con el tiempo, lo que hace que la conversación sea irrelevante para el contenido que se muestra. Las sub entidades de conversación proporcionan una experiencia de conversación mucho más centrada para las pestañas dinámicas.

Las sub entidades de conversación solo se admiten en canales. Se pueden usar desde una pestaña personal o estática para crear o continuar conversaciones en pestañas que ya están ancladas a un canal. La pestaña estática es útil si desea proporcionar una ubicación para que un usuario vea y acceda a las conversaciones que se están produciendo en varios canales.

## <a name="prerequisites"></a>Requisitos previos

Para admitir sub entidades de conversación, la aplicación web de pestañas debe tener la capacidad de almacenar una asignación entre sub entidades ↔ conversaciones en una base de datos back-end. El se proporciona, pero debe almacenarlo y devolverlo a Teams para que los usuarios `conversationId` `conversationId` puedan continuar la conversación.

## <a name="start-a-new-conversation"></a>Iniciar una nueva conversación

Para iniciar una nueva conversación, use la `openConversation()` función. Este método controla el inicio y la continuación de una conversación. Las entradas de la función cambian en función de la acción que desee realizar. Desde la perspectiva de los usuarios, se abre el panel de conversación a la derecha de la pantalla, ya sea para iniciar una conversación o continuar una conversación.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** toma las siguientes entradas para iniciar una conversación en un canal:

* **subEntityId:** este es el identificador de la subentidad específica. Por ejemplo, task-123.
* **entityId:** este es el identificador de la instancia de tabulación cuando se creó. El identificador es importante para volver a hacer referencia a la misma instancia de pestaña.
* **channelId:** este es el canal en el que reside la instancia de tabulación.
   > [!NOTE]
   > El **channelId** es opcional para las pestañas de canal. Sin embargo, se recomienda mantener la implementación en todas las pestañas estáticas y de canal.
* **title:** este es el título que se muestra al usuario en el panel de chat.

La mayoría de estos valores también se pueden recuperar de la `getContext` API.

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

La siguiente imagen muestra el panel de conversación:

![Sub-entidades conversacionales: iniciar conversación](~/assets/images/tabs/conversational-subentities/start-conversation.png)

Si el usuario inicia una conversación, es importante escuchar la devolución de llamada de ese evento para recuperar y guardar **el conversationId**:

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

El `conversationResponse` objeto contiene información relacionada con la conversación iniciada. Se recomienda guardar todas las propiedades de este objeto de respuesta para su uso posterior.

## <a name="continue-a-conversation"></a>Continuar una conversación

Una vez que se inicia una conversación, las llamadas posteriores a requieren que también proporcione las mismas entradas que al iniciar una nueva conversación, pero también `openConversation()` incluya **el conversationId** [](#start-a-new-conversation). El panel de conversación se abre para el usuario con la conversación adecuada en vista. Los usuarios pueden ver mensajes nuevos o entrantes en tiempo real.

La siguiente imagen muestra el panel de conversación con la conversación adecuada:

![Subeconversacionales: continuar la conversación](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>Mejorar una conversación

Es importante que la pestaña incluya [vínculos profundos a la sub entity](~/concepts/build-and-test/deep-links.md). Por ejemplo, el usuario que selecciona la pestaña chiclet deeplink de la conversación del canal. El comportamiento esperado es recibir el vínculo profundo, abrir esa sub entity y, a continuación, abrir el panel de conversación para esa sub entity.

Para admitir sub entidades conversacionales desde la pestaña personal o estática, no tiene que cambiar nada en la implementación. Solo se admiten conversaciones iniciales o continuas desde pestañas de canal que ya están ancladas. La compatibilidad con pestañas estáticas permite proporcionar una única ubicación para que los usuarios interactúen con todas las sub entidades. Es importante guardar el , y cuando la pestaña se crea originalmente en un canal para tener las propiedades correctas al abrir la vista de conversación `subEntityId` `entityId` en una pestaña `channelId` estática.

## <a name="close-a-conversation"></a>Cerrar una conversación

Puede cerrar manualmente la vista de conversación llamando a la `closeConversation()` función.

```javascript
microsoftTeams.conversations.closeConversation();
```

También puede escuchar un evento cuando un usuario cierra la vista de conversación.

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="see-also"></a>Vea también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Requisitos previos](~/tabs/how-to/tab-requirements.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Creación de una página de contenido](~/tabs/how-to/create-tab-pages/content-page.md)
* [Creación de una página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [Crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Obtención del contexto de Teams para la pestaña](~/tabs/how-to/access-teams-context.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Expansión del vínculo de la pestaña y vista de fases](~/tabs/tabs-link-unfurling.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Cambios del margen de pestaña](~/resources/removing-tab-margins.md)