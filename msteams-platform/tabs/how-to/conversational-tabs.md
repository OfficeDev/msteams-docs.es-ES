---
title: Crear pestañas de conversación
author: surbhigupta
description: Crear chat de sub entity conversacional para las pestañas del canal
keywords: Canal de pestañas de teams configurable
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: b563510b9ce232a98572430c76f1b8e59ddb4886
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179695"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="17e03-104">Crear pestañas de conversación</span><span class="sxs-lookup"><span data-stu-id="17e03-104">Create conversational tabs</span></span>

<span data-ttu-id="17e03-105">Las sub entidades conversacionales proporcionan una forma de permitir que los usuarios tengan conversaciones sobre las sub entidades en la pestaña, como tareas específicas, pacientes y oportunidades de ventas, en lugar de analizar toda la pestaña, también conocida como entidad.</span><span class="sxs-lookup"><span data-stu-id="17e03-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="17e03-106">Un canal tradicional o una pestaña configurable permite al usuario tener una conversación sobre una pestaña, pero el usuario requiere una conversación más centrada.</span><span class="sxs-lookup"><span data-stu-id="17e03-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user requires a more focused conversation.</span></span> <span data-ttu-id="17e03-107">El requisito de una conversación más centrada puede surgir si hay demasiado contenido para tener una discusión centralizada o porque el contenido cambió con el tiempo, lo que hace que la conversación sea irrelevante para el contenido que se muestra.</span><span class="sxs-lookup"><span data-stu-id="17e03-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or because the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="17e03-108">Las sub entidades de conversación proporcionan una experiencia de conversación mucho más centrada para las pestañas dinámicas.</span><span class="sxs-lookup"><span data-stu-id="17e03-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="17e03-109">Las sub entidades de conversación solo se admiten en canales.</span><span class="sxs-lookup"><span data-stu-id="17e03-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="17e03-110">Se pueden usar desde una pestaña personal o estática para crear o continuar conversaciones en pestañas que ya están ancladas a un canal.</span><span class="sxs-lookup"><span data-stu-id="17e03-110">They can be used from a personal or static tab to create or continue conversations in tabs that are already pinned to a channel.</span></span> <span data-ttu-id="17e03-111">La pestaña estática es útil si desea proporcionar una ubicación para que un usuario vea y acceda a las conversaciones que se están produciendo en varios canales.</span><span class="sxs-lookup"><span data-stu-id="17e03-111">The static tab is useful if you want to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17e03-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="17e03-112">Prerequisites</span></span>

<span data-ttu-id="17e03-113">Para admitir sub entidades de conversación, la aplicación web de pestañas debe tener la capacidad de almacenar una asignación entre sub entidades ↔ conversaciones en una base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="17e03-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="17e03-114">El se proporciona, pero debe almacenarlo y devolverlo a Teams para que los usuarios `conversationId` `conversationId` puedan continuar la conversación.</span><span class="sxs-lookup"><span data-stu-id="17e03-114">The `conversationId` is provided, but you must store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="17e03-115">Iniciar una nueva conversación</span><span class="sxs-lookup"><span data-stu-id="17e03-115">Start a new conversation</span></span>

<span data-ttu-id="17e03-116">Para iniciar una nueva conversación, use la `openConversation()` función.</span><span class="sxs-lookup"><span data-stu-id="17e03-116">To start a new conversation, use the `openConversation()` function.</span></span> <span data-ttu-id="17e03-117">Este método controla el inicio y la continuación de una conversación.</span><span class="sxs-lookup"><span data-stu-id="17e03-117">Starting and continuing a conversation are all handled by this method.</span></span> <span data-ttu-id="17e03-118">Las entradas de la función cambian en función de la acción que desee realizar.</span><span class="sxs-lookup"><span data-stu-id="17e03-118">The inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="17e03-119">Desde la perspectiva de los usuarios, se abre el panel de conversación a la derecha de la pantalla, ya sea para iniciar una conversación o continuar una conversación.</span><span class="sxs-lookup"><span data-stu-id="17e03-119">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="17e03-120">**openConversation** toma las siguientes entradas para iniciar una conversación en un canal:</span><span class="sxs-lookup"><span data-stu-id="17e03-120">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="17e03-121">**subEntityId:** este es el identificador de la subentidad específica.</span><span class="sxs-lookup"><span data-stu-id="17e03-121">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="17e03-122">Por ejemplo, task-123.</span><span class="sxs-lookup"><span data-stu-id="17e03-122">For example, task-123.</span></span>
* <span data-ttu-id="17e03-123">**entityId:** este es el identificador de la instancia de tabulación cuando se creó.</span><span class="sxs-lookup"><span data-stu-id="17e03-123">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="17e03-124">El identificador es importante para volver a hacer referencia a la misma instancia de pestaña.</span><span class="sxs-lookup"><span data-stu-id="17e03-124">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="17e03-125">**channelId:** este es el canal en el que reside la instancia de tabulación.</span><span class="sxs-lookup"><span data-stu-id="17e03-125">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="17e03-126">El **channelId** es opcional para las pestañas de canal.</span><span class="sxs-lookup"><span data-stu-id="17e03-126">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="17e03-127">Sin embargo, se recomienda mantener la implementación en todas las pestañas estáticas y de canal.</span><span class="sxs-lookup"><span data-stu-id="17e03-127">However, it is recommended if you want to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="17e03-128">**title:** este es el título que se muestra al usuario en el panel de chat.</span><span class="sxs-lookup"><span data-stu-id="17e03-128">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="17e03-129">La mayoría de estos valores también se pueden recuperar de la `getContext` API.</span><span class="sxs-lookup"><span data-stu-id="17e03-129">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="17e03-130">La siguiente imagen muestra el panel de conversación:</span><span class="sxs-lookup"><span data-stu-id="17e03-130">The following image shows the conversation panel:</span></span>

![Sub-entidades conversacionales: iniciar conversación](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="17e03-132">Si el usuario inicia una conversación, es importante escuchar la devolución de llamada de ese evento para recuperar y guardar **el conversationId**:</span><span class="sxs-lookup"><span data-stu-id="17e03-132">If the user starts a conversation, it is important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="17e03-133">El `conversationResponse` objeto contiene información relacionada con la conversación iniciada.</span><span class="sxs-lookup"><span data-stu-id="17e03-133">The `conversationResponse` object contains information related to the conversation that was started.</span></span> <span data-ttu-id="17e03-134">Se recomienda guardar todas las propiedades de este objeto de respuesta para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="17e03-134">It is recommended that you save all the properties of this response object for later use.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="17e03-135">Continuar una conversación</span><span class="sxs-lookup"><span data-stu-id="17e03-135">Continue a conversation</span></span>

<span data-ttu-id="17e03-136">Una vez que se inicia una conversación, las llamadas posteriores a requieren que también proporcione las mismas entradas que al iniciar una nueva conversación, pero también `openConversation()` incluya **el conversationId** [](#start-a-new-conversation).</span><span class="sxs-lookup"><span data-stu-id="17e03-136">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [start a new conversation](#start-a-new-conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="17e03-137">El panel de conversación se abre para el usuario con la conversación adecuada en vista.</span><span class="sxs-lookup"><span data-stu-id="17e03-137">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="17e03-138">Los usuarios pueden ver mensajes nuevos o entrantes en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="17e03-138">Users are able to see new or incoming messages in real-time.</span></span>

<span data-ttu-id="17e03-139">La siguiente imagen muestra el panel de conversación con la conversación adecuada:</span><span class="sxs-lookup"><span data-stu-id="17e03-139">The following image shows the conversation panel with the appropriate conversation:</span></span>

![Subeconversacionales: continuar la conversación](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="17e03-141">Mejorar una conversación</span><span class="sxs-lookup"><span data-stu-id="17e03-141">Enhance a conversation</span></span>

<span data-ttu-id="17e03-142">Es importante que la pestaña incluya [vínculos profundos a la sub entity](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="17e03-142">It is important that your tab includes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="17e03-143">Por ejemplo, el usuario que selecciona la pestaña chiclet deeplink de la conversación del canal.</span><span class="sxs-lookup"><span data-stu-id="17e03-143">For example, user selecting the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="17e03-144">El comportamiento esperado es recibir el vínculo profundo, abrir esa sub entity y, a continuación, abrir el panel de conversación para esa sub entity.</span><span class="sxs-lookup"><span data-stu-id="17e03-144">The expected behavior is to receive the deeplink, open that sub-entity, and then open the conversation panel for that sub-entity.</span></span>

<span data-ttu-id="17e03-145">Para admitir sub entidades conversacionales desde la pestaña personal o estática, no tiene que cambiar nada en la implementación.</span><span class="sxs-lookup"><span data-stu-id="17e03-145">To support conversational sub-entities from your personal or static tab, you do not have to change anything in your implementation.</span></span> <span data-ttu-id="17e03-146">Solo se admiten conversaciones iniciales o continuas desde pestañas de canal que ya están ancladas.</span><span class="sxs-lookup"><span data-stu-id="17e03-146">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="17e03-147">La compatibilidad con pestañas estáticas permite proporcionar una única ubicación para que los usuarios interactúen con todas las sub entidades.</span><span class="sxs-lookup"><span data-stu-id="17e03-147">Supporting static tabs allows you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="17e03-148">Es importante guardar el , y cuando la pestaña se crea originalmente en un canal para tener las propiedades correctas al abrir la vista de conversación `subEntityId` `entityId` en una pestaña `channelId` estática.</span><span class="sxs-lookup"><span data-stu-id="17e03-148">It is important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="17e03-149">Cerrar una conversación</span><span class="sxs-lookup"><span data-stu-id="17e03-149">Close a conversation</span></span>

<span data-ttu-id="17e03-150">Puede cerrar manualmente la vista de conversación llamando a la `closeConversation()` función.</span><span class="sxs-lookup"><span data-stu-id="17e03-150">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="17e03-151">También puede escuchar un evento cuando un usuario cierra la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="17e03-151">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="see-also"></a><span data-ttu-id="17e03-152">Vea también</span><span class="sxs-lookup"><span data-stu-id="17e03-152">See also</span></span>

* [<span data-ttu-id="17e03-153">Teams pestañas</span><span class="sxs-lookup"><span data-stu-id="17e03-153">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="17e03-154">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="17e03-154">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="17e03-155">Crear una pestaña de canal o grupo</span><span class="sxs-lookup"><span data-stu-id="17e03-155">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="17e03-156">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="17e03-156">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="17e03-157">Compilar pestañas con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="17e03-157">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="next-step"></a><span data-ttu-id="17e03-158">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="17e03-158">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="17e03-159">Cambios del margen de pestaña</span><span class="sxs-lookup"><span data-stu-id="17e03-159">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)