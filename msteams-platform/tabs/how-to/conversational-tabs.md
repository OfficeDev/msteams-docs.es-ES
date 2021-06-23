---
title: Crear pestañas de conversación
author: surbhigupta
description: Crear chat de sub entity conversacional para las pestañas del canal
keywords: Canal de pestañas de teams configurable
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: 343cbe26ded2792489640ae3d86ec94c7c6db72b
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069226"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="e3917-104">Crear pestañas de conversación</span><span class="sxs-lookup"><span data-stu-id="e3917-104">Create conversational tabs</span></span>

<span data-ttu-id="e3917-105">Las sub entidades conversacionales proporcionan una forma de permitir que los usuarios tengan conversaciones sobre las sub entidades en la pestaña, como tareas específicas, pacientes y oportunidades de ventas, en lugar de analizar toda la pestaña, también conocida como entidad.</span><span class="sxs-lookup"><span data-stu-id="e3917-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="e3917-106">Un canal tradicional o una pestaña configurable permite al usuario tener una conversación sobre una pestaña, pero es posible que el usuario quiera una conversación más centrada.</span><span class="sxs-lookup"><span data-stu-id="e3917-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user may want a more focused conversation.</span></span> <span data-ttu-id="e3917-107">Puede surgir el requisito de una conversación más centrada, si hay demasiado contenido para tener una discusión centralizada o si el contenido ha cambiado con el tiempo, lo que hace que la conversación sea irrelevante para el contenido que se muestra.</span><span class="sxs-lookup"><span data-stu-id="e3917-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="e3917-108">Las sub entidades de conversación proporcionan una experiencia de conversación mucho más centrada para las pestañas dinámicas.</span><span class="sxs-lookup"><span data-stu-id="e3917-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="e3917-109">Las sub entidades de conversación solo se admiten en canales.</span><span class="sxs-lookup"><span data-stu-id="e3917-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="e3917-110">Sin embargo, se pueden usar desde una pestaña personal o estática  para crear o continuar conversaciones en pestañas que ya están ancladas a un canal.</span><span class="sxs-lookup"><span data-stu-id="e3917-110">However, they can be used from a personal or static tab to create or continue conversations in tabs that are *already* pinned to a channel.</span></span> <span data-ttu-id="e3917-111">La pestaña estática es útil si desea proporcionar una ubicación para que un usuario vea y acceda a las conversaciones que se están produciendo en varios canales.</span><span class="sxs-lookup"><span data-stu-id="e3917-111">The static tab is useful if you wish to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3917-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e3917-112">Prerequisites</span></span>

<span data-ttu-id="e3917-113">Para admitir sub entidades de conversación, la aplicación web de pestañas debe tener la capacidad de almacenar una asignación entre sub entidades ↔ conversaciones en una base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="e3917-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="e3917-114">Le proporcionaremos el , pero será su responsabilidad almacenarlo y devolverlo a Teams para que los usuarios `conversationId` `conversationId` puedan continuar la conversación.</span><span class="sxs-lookup"><span data-stu-id="e3917-114">We will provide you with the `conversationId`, but it will be your responsibility to store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="e3917-115">Iniciar una nueva conversación</span><span class="sxs-lookup"><span data-stu-id="e3917-115">Start a new conversation</span></span>

<span data-ttu-id="e3917-116">Para iniciar una nueva conversación, use la `openConversation()` función.</span><span class="sxs-lookup"><span data-stu-id="e3917-116">To start a new conversation, you use the `openConversation()` function.</span></span> <span data-ttu-id="e3917-117">Este método controla el inicio y la continuación de una conversación, pero las entradas a la función cambian en función de la acción que desee realizar.</span><span class="sxs-lookup"><span data-stu-id="e3917-117">Starting and continuing a conversation are all handled by this method, however, the inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="e3917-118">Desde la perspectiva de los usuarios, se abre el panel de conversación a la derecha de la pantalla, ya sea para iniciar una conversación o continuar una conversación.</span><span class="sxs-lookup"><span data-stu-id="e3917-118">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="e3917-119">**openConversation** toma las siguientes entradas para iniciar una conversación en un canal:</span><span class="sxs-lookup"><span data-stu-id="e3917-119">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="e3917-120">**subEntityId:** este es el identificador de la subentidad específica.</span><span class="sxs-lookup"><span data-stu-id="e3917-120">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="e3917-121">Por ejemplo, task-123.</span><span class="sxs-lookup"><span data-stu-id="e3917-121">For example, task-123.</span></span>
* <span data-ttu-id="e3917-122">**entityId:** este es el identificador de la instancia de tabulación cuando se creó.</span><span class="sxs-lookup"><span data-stu-id="e3917-122">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="e3917-123">El identificador es importante para volver a hacer referencia a la misma instancia de pestaña.</span><span class="sxs-lookup"><span data-stu-id="e3917-123">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="e3917-124">**channelId:** este es el canal en el que reside la instancia de tabulación.</span><span class="sxs-lookup"><span data-stu-id="e3917-124">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="e3917-125">El **channelId** es opcional para las pestañas de canal.</span><span class="sxs-lookup"><span data-stu-id="e3917-125">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="e3917-126">Sin embargo, se recomienda mantener la implementación en todos los canales y pestañas estáticas igual.</span><span class="sxs-lookup"><span data-stu-id="e3917-126">However, it is recommended if you wish to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="e3917-127">**title:** este es el título que se muestra al usuario en el panel de chat.</span><span class="sxs-lookup"><span data-stu-id="e3917-127">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="e3917-128">La mayoría de estos valores también se pueden recuperar de la `getContext` API.</span><span class="sxs-lookup"><span data-stu-id="e3917-128">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="e3917-129">Se abrirá el panel de conversación.</span><span class="sxs-lookup"><span data-stu-id="e3917-129">This will open the conversation panel.</span></span>

![Entidades de conversación sub- Iniciar conversación](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="e3917-131">Si el usuario inicia una conversación, es importante escuchar la devolución de llamada de ese evento para recuperar y guardar **el conversationId**:</span><span class="sxs-lookup"><span data-stu-id="e3917-131">If the user starts a conversation, it’s important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="e3917-132">El `conversationReponse` objeto contiene información relacionada con la conversación que se acaba de iniciar.</span><span class="sxs-lookup"><span data-stu-id="e3917-132">The `conversationReponse` object contains information related to the conversation that was just started.</span></span> <span data-ttu-id="e3917-133">Se recomienda guardar todas las propiedades de este objeto de respuesta para su reutilización más adelante.</span><span class="sxs-lookup"><span data-stu-id="e3917-133">We recommend you save all the properties of this response object for reuse later.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="e3917-134">Continuar una conversación</span><span class="sxs-lookup"><span data-stu-id="e3917-134">Continue a conversation</span></span>

<span data-ttu-id="e3917-135">Una vez que se inicia una conversación, las llamadas posteriores a requieren que también proporcione las mismas entradas que en Inicio de una nueva conversación de pestaña de canal, pero también `openConversation()` incluya **el conversationId** [](#Starting a new channel tab conversation).</span><span class="sxs-lookup"><span data-stu-id="e3917-135">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [Starting a new channel tab conversation](#Starting a new channel tab conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="e3917-136">El panel de conversación se abre para el usuario con la conversación adecuada en vista.</span><span class="sxs-lookup"><span data-stu-id="e3917-136">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="e3917-137">Los usuarios pueden ver mensajes nuevos o entrantes en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="e3917-137">Users are able to see new or incoming messages in real-time.</span></span>

![Entidades de conversación sub- Continuar conversación](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="e3917-139">Mejorar una conversación</span><span class="sxs-lookup"><span data-stu-id="e3917-139">Enhance a conversation</span></span>

<span data-ttu-id="e3917-140">Por último, es importante que la pestaña consuma [vínculos profundos a la sub entity](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="e3917-140">Finally, it’s important that your tab consumes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="e3917-141">Por ejemplo, el usuario que hace clic en la pestaña chiclet deeplink de la conversación del canal.</span><span class="sxs-lookup"><span data-stu-id="e3917-141">For example, user clicking the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="e3917-142">El comportamiento esperado es que reciba el vínculo profundo, abra esa sub entity y, a continuación, abra el panel de conversación para esa sub entity específica.</span><span class="sxs-lookup"><span data-stu-id="e3917-142">The expected behavior is for you to receive the deeplink, open that sub-entity, and then open the conversation panel for that specific sub-entity.</span></span>

<span data-ttu-id="e3917-143">Para admitir sub entidades conversacionales desde la pestaña personal o estática, no tiene que cambiar nada acerca de la implementación.</span><span class="sxs-lookup"><span data-stu-id="e3917-143">To support conversational sub-entities from your personal or static tab, you do not have to change anything about your implementation.</span></span> <span data-ttu-id="e3917-144">Solo se admiten conversaciones iniciales o continuas desde pestañas de canal que ya están ancladas.</span><span class="sxs-lookup"><span data-stu-id="e3917-144">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="e3917-145">La compatibilidad con pestañas estáticas permite proporcionar una única ubicación para que los usuarios interactúen con todas las sub entidades.</span><span class="sxs-lookup"><span data-stu-id="e3917-145">Supporting static tabs allow you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="e3917-146">Sin embargo, es importante guardar la , y cuando la pestaña se crea originalmente en un canal para que tenga las propiedades correctas al abrir la vista de conversación en una pestaña `subEntityId` `entityId` `channelId` estática.</span><span class="sxs-lookup"><span data-stu-id="e3917-146">It is, however, important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel in order for you to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="e3917-147">Cerrar una conversación</span><span class="sxs-lookup"><span data-stu-id="e3917-147">Close a conversation</span></span>

<span data-ttu-id="e3917-148">Puede cerrar manualmente la vista de conversación llamando a la `closeConversation()` función.</span><span class="sxs-lookup"><span data-stu-id="e3917-148">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="e3917-149">También puede escuchar un evento cuando un usuario cierra la vista de conversación.</span><span class="sxs-lookup"><span data-stu-id="e3917-149">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```
