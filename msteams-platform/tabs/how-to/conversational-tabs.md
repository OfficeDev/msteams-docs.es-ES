---
title: Crear pestañas de conversación
author: surbhigupta
description: Aprenda a crear chat de subentidad conversacional para las pestañas de canal, para administrar conversaciones con ejemplos de código
keywords: Canal de pestañas de teams configurable
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: none
ms.openlocfilehash: ac58448ec390d0e954c0737d5b0700d0d91b04b1
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452602"
---
# <a name="create-conversational-tabs"></a>Crear pestañas de conversación

Las sub entidades conversacionales proporcionan una forma de permitir que los usuarios tengan conversaciones sobre sub entidades en la pestaña. Por ejemplo, una tarea específica, un paciente y una oportunidad de ventas, en lugar de analizar toda la pestaña, también conocida como entidad. Un canal tradicional o una pestaña configurable permite al usuario tener una conversación sobre una pestaña, pero el usuario requiere una conversación más centrada. Puede surgir el requisito de una conversación más centrada, si hay demasiado contenido para tener una discusión centralizada o porque el contenido cambió con el tiempo, lo que hace que la conversación sea irrelevante para el contenido mostrado. Las sub entidades de conversación proporcionan una experiencia de conversación mucho más centrada para las pestañas dinámicas.

Las sub entidades conversacionales solo se admiten en canales. Se pueden usar desde una pestaña personal o estática para crear o continuar conversaciones en pestañas que ya están ancladas a un canal. La pestaña estática es útil si desea proporcionar una ubicación para que un usuario vea y acceda a las conversaciones que se están produciendo en varios canales.

## <a name="prerequisites"></a>Requisitos previos

Para admitir sub entidades conversacionales, la aplicación web de pestañas debe tener la capacidad de almacenar una asignación entre conversaciones de sub ↔ entidades en una base de datos back-end. El `conversationId` se proporciona, pero debe almacenarlo `conversationId` y devolverlo a Teams para que los usuarios puedan continuar la conversación.

## <a name="start-a-new-conversation"></a>Iniciar una nueva conversación

Para iniciar una nueva conversación, use la `openConversation()` función. Este método controla el inicio y la continuación de una conversación. Las entradas de la función cambian en función de la acción que desee realizar, desde la perspectiva del usuario, se abre el panel de conversación a la derecha de la pantalla, ya sea para iniciar una conversación o continuar una conversación.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** toma las siguientes entradas para iniciar una conversación en un canal:

* **subEntityId**: el identificador de la subentidad específica. Por ejemplo, task-123.
* **entityId**: el identificador de la instancia de tabulación cuando se creó. El identificador es importante para volver a hacer referencia a la misma instancia de pestaña.
* **channelId**: canal en el que reside la instancia de tabulación.
   > [!NOTE]
   > El **channelId** es opcional para las pestañas de canal. Sin embargo, se recomienda mantener la implementación en todas las pestañas estáticas y de canal.
* **title**: el título que se muestra al usuario en el panel de chat.

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

Después de que se inicie una conversación, `openConversation()` las llamadas posteriores que se requieran, que también proporcione las mismas entradas que al iniciar una nueva [conversación, pero](#start-a-new-conversation) también incluya **el conversationId**. El panel de conversación se abre para los usuarios con la conversación adecuada en vista. Los usuarios pueden ver mensajes nuevos o entrantes en tiempo real.

La siguiente imagen muestra el panel de conversación con la conversación adecuada:

![Subeconversacionales: continuar la conversación](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>Mejorar una conversación

Es importante que la pestaña incluya [vínculos profundos a la subentidad](~/concepts/build-and-test/deep-links.md). Por ejemplo, el usuario que selecciona el vínculo profundo de tabulación de la conversación de canal. El comportamiento esperado es recibir el vínculo profundo, abrir esa subentidad y, a continuación, abrir el panel de conversación para esa subentidad.

Para admitir sub entidades conversacionales desde la pestaña personal o estática, no tiene que cambiar nada en la implementación. Solo se admiten conversaciones iniciales o continuas desde pestañas de canal que ya están ancladas. Admitir pestañas estáticas permite proporcionar una única ubicación para que los usuarios interactúen con todas las sub entidades. Es importante guardar el `subEntityId`, `entityId`y `channelId` cuando la pestaña se crea originalmente en un canal para tener las propiedades correctas al abrir la vista de conversación en una pestaña estática.

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

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Crear pestaña Conversación| Microsoft Teams muestra de pestaña para mostrar la pestaña crear conversación. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Cambios del margen de pestaña](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>Vea también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
