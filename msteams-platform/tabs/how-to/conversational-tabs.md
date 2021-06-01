---
title: Crear pestañas conversacionales
author: laujan
description: Crear chat de sub entity conversacional para las pestañas del canal
keywords: Canal de pestañas de teams configurable
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: 4171265a3ef4ad917661e258dd7305f82411c5ef
ms.sourcegitcommit: 118f7261d313feeac5b398fef56a44bd90104b2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2021
ms.locfileid: "52709655"
---
# <a name="create-conversational-tabs"></a>Crear pestañas conversacionales

Las sub entidades conversacionales proporcionan una forma de permitir que los usuarios tengan conversaciones sobre las sub entidades en la pestaña, como tareas específicas, pacientes y oportunidades de ventas, en lugar de analizar toda la pestaña, también conocida como entidad. Un canal tradicional o una pestaña configurable permite al usuario tener una conversación sobre una pestaña, pero es posible que el usuario quiera una conversación más centrada. Puede surgir el requisito de una conversación más centrada, si hay demasiado contenido para tener una discusión centralizada o si el contenido ha cambiado con el tiempo, lo que hace que la conversación sea irrelevante para el contenido que se muestra. Las sub entidades de conversación proporcionan una experiencia de conversación mucho más centrada para las pestañas dinámicas.

Las sub entidades de conversación solo se admiten en canales. Sin embargo, se pueden usar desde una pestaña personal o estática  para crear o continuar conversaciones en pestañas que ya están ancladas a un canal. La pestaña estática es útil si desea proporcionar una ubicación para que un usuario vea y acceda a las conversaciones que se están produciendo en varios canales.

## <a name="prerequisites"></a>Requisitos previos

Para admitir sub entidades de conversación, la aplicación web de pestañas debe tener la capacidad de almacenar una asignación entre sub entidades ↔ conversaciones en una base de datos back-end. Le proporcionaremos el , pero será su responsabilidad almacenarlo y devolverlo a Teams para que los usuarios `conversationId` `conversationId` puedan continuar la conversación.

## <a name="start-a-new-conversation"></a>Iniciar una nueva conversación

Para iniciar una nueva conversación, use la `openConversation()` función. Este método controla el inicio y la continuación de una conversación, pero las entradas a la función cambian en función de la acción que desee realizar. Desde la perspectiva de los usuarios, se abre el panel de conversación a la derecha de la pantalla, ya sea para iniciar una conversación o continuar una conversación.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** toma las siguientes entradas para iniciar una conversación en un canal:

* **subEntityId:** este es el identificador de la subentidad específica. Por ejemplo, task-123.
* **entityId:** este es el identificador de la instancia de tabulación cuando se creó. El identificador es importante para volver a hacer referencia a la misma instancia de pestaña.
* **channelId:** este es el canal en el que reside la instancia de tabulación.
   > [!NOTE]
   > El **channelId** es opcional para las pestañas de canal. Sin embargo, se recomienda mantener la implementación en todos los canales y pestañas estáticas igual.
* **title:** este es el título que se muestra al usuario en el panel de chat.

La mayoría de estos valores también se pueden recuperar de la `getContext` API.

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

Se abrirá el panel de conversación.

![Entidades de conversación sub- Iniciar conversación](~/assets/images/tabs/conversational-subentities/start-conversation.png)

Si el usuario inicia una conversación, es importante escuchar la devolución de llamada de ese evento para recuperar y guardar **el conversationId**:

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

El `conversationReponse` objeto contiene información relacionada con la conversación que se acaba de iniciar. Se recomienda guardar todas las propiedades de este objeto de respuesta para su reutilización más adelante.

## <a name="continue-a-conversation"></a>Continuar una conversación

Una vez que se inicia una conversación, las llamadas posteriores a requieren que también proporcione las mismas entradas que en Inicio de una nueva conversación de pestaña de canal, pero también `openConversation()` incluya **el conversationId** [](#Starting a new channel tab conversation). El panel de conversación se abre para el usuario con la conversación adecuada en vista. Los usuarios pueden ver mensajes nuevos o entrantes en tiempo real.

![Entidades de conversación sub- Continuar conversación](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>Mejorar una conversación

Por último, es importante que la pestaña consuma [vínculos profundos a la sub entity](~/concepts/build-and-test/deep-links.md). Por ejemplo, el usuario que hace clic en la pestaña chiclet deeplink de la conversación del canal. El comportamiento esperado es que reciba el vínculo profundo, abra esa sub entity y, a continuación, abra el panel de conversación para esa sub entity específica.

Para admitir sub entidades conversacionales desde la pestaña personal o estática, no tiene que cambiar nada acerca de la implementación. Solo se admiten conversaciones iniciales o continuas desde pestañas de canal que ya están ancladas. La compatibilidad con pestañas estáticas permite proporcionar una única ubicación para que los usuarios interactúen con todas las sub entidades. Sin embargo, es importante guardar la , y cuando la pestaña se crea originalmente en un canal para que tenga las propiedades correctas al abrir la vista de conversación en una pestaña `subEntityId` `entityId` `channelId` estática.

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
