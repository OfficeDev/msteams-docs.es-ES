---
title: Crear pestañas de conversación
author: surbhigupta
description: En este módulo, aprenderá a crear un chat de subentidad conversacional para las pestañas del canal, para administrar conversaciones mediante ejemplos de código.
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: medium
ms.openlocfilehash: 4ba0545d78f892941836994d054a3fafcee183a4
ms.sourcegitcommit: 06fdb41c124f82ea1b66181485339cb200ea7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2022
ms.locfileid: "66962422"
---
# <a name="create-conversational-tabs"></a>Crear pestañas de conversación

Las subentidades conversacionales proporcionan una manera de permitir que los usuarios tengan conversaciones sobre subentidades en la pestaña. Por ejemplo, una tarea específica, un paciente y una oportunidad de ventas, en lugar de analizar toda la pestaña, también conocida como entidad. Un canal tradicional o una pestaña configurable permite al usuario tener una conversación sobre una pestaña, pero el usuario requiere una conversación más centrada. El requisito de una conversación más centrada puede surgir, ya sea si hay demasiado contenido para tener una discusión centralizada o porque el contenido ha cambiado con el tiempo, lo que hace que la conversación sea irrelevante para el contenido mostrado. Las subentidades conversacionales proporcionan una experiencia de conversación mucho más centrada para las pestañas dinámicas.

Las subentidades conversacionales solo se admiten en canales. Se pueden usar desde una pestaña personal o estática para crear o continuar conversaciones en pestañas que ya están ancladas a un canal. La pestaña estática es útil si desea proporcionar una ubicación para que un usuario vea y acceda a las conversaciones que se producen en varios canales.

## <a name="prerequisites"></a>Requisitos previos

Para admitir subentidades conversacionales, la aplicación web de pestaña debe tener la capacidad de almacenar una asignación entre conversaciones de subentidades ↔ en una base de datos back-end. Se `conversationId` proporciona , pero debe almacenarlo y devolverlo a Teams para que `conversationId` los usuarios continúen la conversación.

## <a name="start-a-new-conversation"></a>Iniciar una nueva conversación

Para iniciar una nueva conversación, use la `openConversation()` función . Este método controla el inicio y la continuación de una conversación. Las entradas de la función cambian en función de la acción que quiera realizar, desde la perspectiva del usuario, lo que abre el panel de conversación a la derecha de la pantalla, ya sea para iniciar una conversación o continuar una conversación.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** toma las siguientes entradas para iniciar una conversación en un canal:

* **subEntityId**: el identificador de su subentidad específica. Por ejemplo, task-123.
* **entityId**: el identificador de la instancia de pestaña cuando se creó. El identificador es importante para volver a la misma instancia de pestaña.
* **channelId**: el canal en el que reside la instancia de pestaña.
   > [!NOTE]
   > **ChannelId** es opcional para las pestañas de canal. Sin embargo, se recomienda mantener la implementación en todas las pestañas estáticas y de canal.
* **title**: el título que se muestra al usuario en el panel de chat.

La mayoría de estos valores también se pueden recuperar de la [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) API (`microsoftTeams.getContext()` en TeamsJS v1). Para obtener más información, vea [PageInfo interface](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

En la imagen siguiente se muestra el panel de conversación:

:::image type="content" source="../../assets/images/tabs/conversational-subentities/start-conversation.png" alt-text="iniciar conversaciones":::

Si el usuario inicia una conversación, es importante escuchar la devolución de llamada de ese evento para recuperar y guardar el **conversationId**:

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onStartConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

El `conversationResponse` objeto contiene información relacionada con la conversación que se inició. Se recomienda guardar todas las propiedades de este objeto de respuesta para su uso posterior.

## <a name="continue-a-conversation"></a>Continuar una conversación

Una vez iniciada una conversación, las llamadas posteriores a `openConversation()` requerir también proporcionan las mismas entradas que al [iniciar una nueva conversación](#start-a-new-conversation), pero también incluyen **conversationId**. El panel de conversación se abre para los usuarios con la conversación adecuada a la vista. Los usuarios pueden ver mensajes nuevos o entrantes en tiempo real.

En la imagen siguiente se muestra el panel de conversación con la conversación adecuada:

:::image type="content" source="../../assets/images/tabs/conversational-subentities/continue-conversation.png" alt-text="continuar las conversaciones":::

## <a name="enhance-a-conversation"></a>Mejora de una conversación

Es importante que la pestaña incluya [vínculos profundos a su subentidad](~/concepts/build-and-test/deep-links.md). Por ejemplo, el usuario que selecciona el vínculo profundo de la pestaña chiclet de la conversación del canal. El comportamiento esperado es recibir el vínculo profundo, abrir esa subentidad y, a continuación, abrir el panel de conversación para esa subentidad.

Para admitir subentidades conversacionales desde la pestaña personal o estática, no es necesario cambiar nada en la implementación. Solo se admiten conversaciones iniciales o continuas desde pestañas de canal que ya están ancladas. Admitir pestañas estáticas le permite proporcionar una única ubicación para que los usuarios interactúen con todas sus subentidades. Es importante guardar `subEntityId`, `entityId`y `channelId` cuando la pestaña se crea originalmente en un canal para tener las propiedades adecuadas al abrir la vista de conversación en una pestaña estática.

## <a name="close-a-conversation"></a>Cerrar una conversación

Puede cerrar manualmente la vista de conversación llamando a la `closeConversation()` función .

```javascript
microsoftTeams.conversations.closeConversation();
```

También puede escuchar un evento cuando los usuarios **seleccionan Cerrar (X)** en la vista de conversación.

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onCloseConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Pestaña Crear conversación| Aplicación de ejemplo de pestaña de Microsoft Teams para mostrar la pestaña Crear conversación. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Cambios del margen de pestaña](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>Vea también

* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o de canal](~/tabs/how-to/create-channel-group-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
