---
title: Información general sobre las acciones universales para tarjetas adaptables
description: Una introducción rápida a las acciones universales para tarjetas adaptables.
ms.topic: overview
localization_priority: Normal
ms.openlocfilehash: f8980743954c4dff2ced464bc599439c7519cefe
ms.sourcegitcommit: d1d1143e285cac5f23590ccba5389616d08f94b3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2021
ms.locfileid: "52781621"
---
# <a name="universal-actions-for-adaptive-cards"></a><span data-ttu-id="b9679-103">Acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="b9679-103">Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="b9679-104">Las acciones universales para tarjetas adaptables evolucionaron a partir de los comentarios de los desarrolladores que, aunque el diseño y la representación de las tarjetas adaptables era universal, el control de la acción no lo era.</span><span class="sxs-lookup"><span data-stu-id="b9679-104">Universal Actions for Adaptive Cards evolved from developer feedback that even though layout and rendering for Adaptive Cards was universal, action handling was not.</span></span> <span data-ttu-id="b9679-105">Incluso si un desarrollador quisiera enviar la misma tarjeta a distintos lugares, debe controlar las acciones de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="b9679-105">Even if a developer wanted to send the same card to different places, they have to handle actions differently.</span></span>

<span data-ttu-id="b9679-106">Las acciones universales para tarjetas adaptables traen el bot como el back-end común para controlar acciones e introduce un nuevo tipo de acción, , que funciona en todas las aplicaciones, como Teams y `Action.Execute` Outlook.</span><span class="sxs-lookup"><span data-stu-id="b9679-106">Universal Actions for Adaptive Cards brings the bot as the common backend for handling actions and introduces a new action type, `Action.Execute`, which works across apps, such as Teams and Outlook.</span></span>

<span data-ttu-id="b9679-107">Este documento le ayuda a comprender cómo puede usar el modelo de acciones universales para mejorar la experiencia del usuario de interactuar con tarjetas adaptables en plataformas y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b9679-107">This document helps you to understand how you can use Universal Actions model to enhance user experience of interacting with Adaptive Cards across platforms and applications.</span></span>

> [!NOTE]
> <span data-ttu-id="b9679-108">La compatibilidad con acciones universales para tarjetas adaptables solo está disponible para las tarjetas enviadas por el bot.</span><span class="sxs-lookup"><span data-stu-id="b9679-108">Support for Universal Actions for Adaptive Cards is only available for cards sent by bot.</span></span> <span data-ttu-id="b9679-109">La compatibilidad con las tarjetas enviadas a través del cuadro de redacción y las tarjetas de desamuestración de vínculos estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="b9679-109">Support for cards sent through compose box and link unfurling cards is coming soon.</span></span>

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="b9679-110">Mejorar las experiencias de usuario con acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="b9679-110">Enhance user experiences with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="b9679-111">Las acciones universales para tarjetas adaptables mejoran la experiencia del usuario al habilitar los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="b9679-111">Universal Actions for Adaptive Cards enhances user experience by enabling the following scenarios:</span></span>

* [<span data-ttu-id="b9679-112">Acciones universales</span><span class="sxs-lookup"><span data-stu-id="b9679-112">Universal Actions</span></span>](#universal-actions)
* [<span data-ttu-id="b9679-113">Vistas específicas de usuario</span><span class="sxs-lookup"><span data-stu-id="b9679-113">User Specific Views</span></span>](#user-specific-views)
* [<span data-ttu-id="b9679-114">Compatibilidad con flujos de trabajo secuenciales</span><span class="sxs-lookup"><span data-stu-id="b9679-114">Sequential Workflow support</span></span>](#sequential-workflow-support)
* [<span data-ttu-id="b9679-115">Vistas actualizadas</span><span class="sxs-lookup"><span data-stu-id="b9679-115">Up to date views</span></span>](#up-to-date-views)

### <a name="universal-actions"></a><span data-ttu-id="b9679-116">Acciones universales</span><span class="sxs-lookup"><span data-stu-id="b9679-116">Universal Actions</span></span>

<span data-ttu-id="b9679-117">Antes de las acciones universales para tarjetas adaptables, los distintos hosts proporcionaba diferentes modelos de acción de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="b9679-117">Before the Universal Actions for Adaptive Cards, different hosts provided different action models as follows:</span></span>

* <span data-ttu-id="b9679-118">Teams o bots usados , un enfoque que aplaza el modelo de comunicación `Action.Submit` real al canal subyacente.</span><span class="sxs-lookup"><span data-stu-id="b9679-118">Teams or bots used `Action.Submit`, an approach which defers the actual communication model to the underlying channel.</span></span>
* <span data-ttu-id="b9679-119">Outlook se `Action.Http` usa para comunicarse con el servicio back-end especificado explícitamente en la carga de la tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="b9679-119">Outlook used `Action.Http` to communicate with the backend service explicitly specified in the Adaptive Card payload.</span></span>

<span data-ttu-id="b9679-120">La siguiente imagen muestra el modelo de acción incoherente actual:</span><span class="sxs-lookup"><span data-stu-id="b9679-120">The following image shows the current inconsistent action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="Modelo de acción incoherente":::

<span data-ttu-id="b9679-122">Con las acciones universales para tarjetas adaptables, puedes usar para el control `Action.Execute` de acciones en diferentes plataformas.</span><span class="sxs-lookup"><span data-stu-id="b9679-122">With the Universal Actions for Adaptive Cards, you can use `Action.Execute` for action handling across different platforms.</span></span> <span data-ttu-id="b9679-123">`Action.Execute`funciona en todos los concentradores, incluidos Teams y Outlook.</span><span class="sxs-lookup"><span data-stu-id="b9679-123">`Action.Execute` works across hubs including Teams and Outlook.</span></span> <span data-ttu-id="b9679-124">Además, se puede devolver una tarjeta adaptable como respuesta para una `Action.Execute` solicitud de invocación desencadenada.</span><span class="sxs-lookup"><span data-stu-id="b9679-124">In addition, an Adaptive Card can be returned as response for an `Action.Execute` triggered invoke request.</span></span>

<span data-ttu-id="b9679-125">En la siguiente imagen se muestra el nuevo modelo de acción universal:</span><span class="sxs-lookup"><span data-stu-id="b9679-125">The following image shows the new Universal Action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="Nuevas acciones universales para tarjetas adaptables":::

<span data-ttu-id="b9679-127">Ahora puede enviar la misma tarjeta a ambos, Teams y Outlook, y mantenerlos sincronizados entre sí mediante el bot subyacente.</span><span class="sxs-lookup"><span data-stu-id="b9679-127">You can now send the same card to both, Teams and Outlook, and keep them in sync with each other using the underlying bot.</span></span> <span data-ttu-id="b9679-128">Cualquier acción realizada en cualquier plataforma se refleja en la otra con esta compilación una *vez,* implemente en cualquier lugar (acciones universales para tarjetas adaptables).</span><span class="sxs-lookup"><span data-stu-id="b9679-128">Any action taken on either platform is reflected to the other with this *build once, deploy anywhere* (Universal Actions for Adaptive Cards) model.</span></span>

<span data-ttu-id="b9679-129">En la siguiente imagen se muestran las acciones universales de las tarjetas adaptables para Teams y Outlook:</span><span class="sxs-lookup"><span data-stu-id="b9679-129">The following image depicts the Universal Actions for Adaptive Cards for both Teams and Outlook:</span></span>

# <a name="mobile"></a>[<span data-ttu-id="b9679-130">Móvil</span><span class="sxs-lookup"><span data-stu-id="b9679-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-teams-outlook.jpg" alt-text="La misma tarjeta móvil para Teams y Outlook":::

# <a name="desktop"></a>[<span data-ttu-id="b9679-132">Escritorio</span><span class="sxs-lookup"><span data-stu-id="b9679-132">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="La misma tarjeta que Teams y Outlook":::

* * *

### <a name="user-specific-views"></a><span data-ttu-id="b9679-134">Vistas específicas de usuario</span><span class="sxs-lookup"><span data-stu-id="b9679-134">User Specific Views</span></span>

<span data-ttu-id="b9679-135">Hoy en día, todos los usuarios Teams chat o canal ven exactamente las mismas acciones de vista y botón en la tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="b9679-135">Today every user in the Teams chat or channel sees the exact same view and button actions on the Adaptive Card.</span></span> <span data-ttu-id="b9679-136">Sin embargo, en determinados escenarios existe un requisito para que determinados usuarios actúen de forma diferente y tengan acceso a información diferente dentro del mismo chat o canal.</span><span class="sxs-lookup"><span data-stu-id="b9679-136">However, in certain scenarios there is a requirement for certain users to act differently and have access to different information within the same chat or channel.</span></span>

<span data-ttu-id="b9679-137">Por ejemplo, si envía una tarjeta de informes de incidentes en un chat o canal, solo el usuario al que se le asignó el incidente debe ver un **botón** Resolver.</span><span class="sxs-lookup"><span data-stu-id="b9679-137">For example, if you send an incident reporting card in a chat or channel, only the user who is assigned the incident must see a **Resolve** button.</span></span> <span data-ttu-id="b9679-138">Por otra parte, el creador de incidentes debe ver un botón **Editar** y todos los demás usuarios solo deben poder ver los detalles del incidente.</span><span class="sxs-lookup"><span data-stu-id="b9679-138">On the other hand, the incident creator must see an **Edit** button and all other users must only be able to view details of the incident.</span></span> <span data-ttu-id="b9679-139">Esto es posible mediante vistas específicas del usuario habilitadas por la `refresh` propiedad.</span><span class="sxs-lookup"><span data-stu-id="b9679-139">This is made possible by User Specific Views that is enabled by the `refresh` property.</span></span>

<span data-ttu-id="b9679-140">En la siguiente imagen se muestra un ejemplo de una extensión de mensajería de vales (ME) donde se muestran diferentes usuarios en el chat diferentes acciones según el requisito:</span><span class="sxs-lookup"><span data-stu-id="b9679-140">The following image shows an example of a ticketing messaging extension (ME) where different users in the chat are shown different actions based on the requirement:</span></span>

# <a name="mobile"></a>[<span data-ttu-id="b9679-141">Móvil</span><span class="sxs-lookup"><span data-stu-id="b9679-141">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Vistas específicas del usuario móvil":::

# <a name="desktop"></a>[<span data-ttu-id="b9679-143">Escritorio</span><span class="sxs-lookup"><span data-stu-id="b9679-143">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Vistas específicas de usuario":::

* * *

<span data-ttu-id="b9679-145">Para obtener más información, vea [el ejemplo de vistas específicas del usuario](User-Specific-Views.md).</span><span class="sxs-lookup"><span data-stu-id="b9679-145">For more information, see [sample for User Specific Views](User-Specific-Views.md).</span></span>

### <a name="sequential-workflow-support"></a><span data-ttu-id="b9679-146">Compatibilidad con flujos de trabajo secuenciales</span><span class="sxs-lookup"><span data-stu-id="b9679-146">Sequential Workflow support</span></span>

<span data-ttu-id="b9679-147">Con la compatibilidad con flujo de trabajo secuencial, los usuarios pueden avanzar a través de una serie de flujos de trabajo sin enviar tarjetas diferentes por separado.</span><span class="sxs-lookup"><span data-stu-id="b9679-147">With Sequential Workflow support, users can progress through a series of workflows without sending different cards separately.</span></span> <span data-ttu-id="b9679-148">Esto es posible gracias a la capacidad de `Action.Execute` devolver una tarjeta adaptable en respuesta a una acción.</span><span class="sxs-lookup"><span data-stu-id="b9679-148">This is made possible by the ability of `Action.Execute` to return an Adaptive Card in response to an action.</span></span> <span data-ttu-id="b9679-149">Además, cualquier usuario del chat o canal puede avanzar a través de su flujo de trabajo sin modificar la tarjeta para otros usuarios en el chat.</span><span class="sxs-lookup"><span data-stu-id="b9679-149">Also, any user in the chat or channel can progress through their workflow without modifying the card for other users in the chat.</span></span>

<span data-ttu-id="b9679-150">En la siguiente imagen se muestra un ejemplo de bot de ordenación de alimentos:</span><span class="sxs-lookup"><span data-stu-id="b9679-150">The following image illustrates a food ordering bot example:</span></span> <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="b9679-151">La siguiente imagen muestra los distintos estados para diferentes usuarios en el chat o canal:</span><span class="sxs-lookup"><span data-stu-id="b9679-151">The following image shows the various states for different users in the chat or channel:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Estados del bot de restauración":::

<span data-ttu-id="b9679-153">Para obtener más información, vea [el ejemplo de Flujo de trabajo secuencial](Sequential-Workflows.md).</span><span class="sxs-lookup"><span data-stu-id="b9679-153">For more information, see [sample for Sequential Workflow](Sequential-Workflows.md).</span></span>

### <a name="up-to-date-views"></a><span data-ttu-id="b9679-154">Vistas actualizadas</span><span class="sxs-lookup"><span data-stu-id="b9679-154">Up to date views</span></span>

<span data-ttu-id="b9679-155">Puedes crear tarjetas adaptables que se actualicen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b9679-155">You can create Adaptive Cards that update automatically.</span></span> <span data-ttu-id="b9679-156">Por ejemplo, puede ser una solicitud de aprobación enviada por un usuario.</span><span class="sxs-lookup"><span data-stu-id="b9679-156">For example, it can be an approval request sent by a user.</span></span> <span data-ttu-id="b9679-157">Después de la aprobación, la tarjeta debe mostrar automáticamente los detalles sobre el tiempo de aprobación de la solicitud y quién aprobó la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b9679-157">After approval, the card must automatically display details about the request approval time and who approved the request.</span></span> <span data-ttu-id="b9679-158">El modelo de actualización permite proporcionar dichas vistas actualizadas.</span><span class="sxs-lookup"><span data-stu-id="b9679-158">The refresh model enables you to provide such up to date views.</span></span> <span data-ttu-id="b9679-159">En la siguiente imagen se muestra un flujo de aprobación de varios pasos y cómo se muestran las vistas para diferentes usuarios.</span><span class="sxs-lookup"><span data-stu-id="b9679-159">The following image shows a multi-step approval flow and how the views for different users is shown.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="Vistas específicas del usuario actualizadas":::

<span data-ttu-id="b9679-161">Para obtener más información, vea [el ejemplo de vistas actualizadas](Up-To-Date-Views.md).</span><span class="sxs-lookup"><span data-stu-id="b9679-161">For more information, see [sample for up to date views](Up-To-Date-Views.md).</span></span>

<span data-ttu-id="b9679-162">Ahora, puede comprender cómo se pueden transformar las tarjetas adaptables con el nuevo modelo de acciones universales para proporcionar una experiencia de usuario única y mejorada.</span><span class="sxs-lookup"><span data-stu-id="b9679-162">Now, you can understand how Adaptive Cards can be transformed with the new Universal Actions model to provide a unique and enhanced user experience.</span></span>

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a><span data-ttu-id="b9679-163">Tarjetas adaptables y el nuevo modelo de acciones universales</span><span class="sxs-lookup"><span data-stu-id="b9679-163">Adaptive Cards and the new Universal Actions model</span></span>

<span data-ttu-id="b9679-164">Las tarjetas adaptables son una combinación de contenido, como texto y gráficos, y acciones que puede realizar un usuario.</span><span class="sxs-lookup"><span data-stu-id="b9679-164">Adaptive Cards are a combination of content, such as text and graphics, and actions that can be performed by a user.</span></span> <span data-ttu-id="b9679-165">Para obtener más información, vea [Adaptive Cards](http://adaptivecards.io/).</span><span class="sxs-lookup"><span data-stu-id="b9679-165">For more information, see [Adaptive Cards](http://adaptivecards.io/).</span></span> <span data-ttu-id="b9679-166">Las nuevas acciones universales para tarjetas adaptables permiten un control común de las acciones de tarjeta adaptable en plataformas y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b9679-166">The new Universal Actions for Adaptive Cards enables a common handling of the Adaptive Card actions across platforms and applications.</span></span> <span data-ttu-id="b9679-167">Para obtener más información, [vea Universal Action Model](/adaptive-cards/authoring-cards/universal-action-model).</span><span class="sxs-lookup"><span data-stu-id="b9679-167">For more information, see [Universal Action Model](/adaptive-cards/authoring-cards/universal-action-model).</span></span>

<span data-ttu-id="b9679-168">Puede empezar actualizando escenarios mediante la guía [de inicio rápido](Work-with-universal-actions-for-adaptive-cards.md) y aprovechar las acciones universales.</span><span class="sxs-lookup"><span data-stu-id="b9679-168">You can get started by updating scenarios using the [quick start guide](Work-with-universal-actions-for-adaptive-cards.md) and leverage Universal Actions.</span></span>

## <a name="see-also"></a><span data-ttu-id="b9679-169">Consulte también</span><span class="sxs-lookup"><span data-stu-id="b9679-169">See also</span></span>

* [<span data-ttu-id="b9679-170">Qué son los bots</span><span class="sxs-lookup"><span data-stu-id="b9679-170">What are bots</span></span>](~/bots/what-are-bots.md)
* [<span data-ttu-id="b9679-171">Introducción a las tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="b9679-171">Adaptive Cards overview</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="b9679-172">Tarjetas adaptables a Microsoft Build 2020</span><span class="sxs-lookup"><span data-stu-id="b9679-172">Adaptive Cards @ Microsoft Build 2020</span></span>](https://youtu.be/hEBhwB72Qn4?t=1393)
* [<span data-ttu-id="b9679-173">Tarjetas adaptables @ Ignite 2020</span><span class="sxs-lookup"><span data-stu-id="b9679-173">Adaptive Cards @ Ignite 2020</span></span>](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)

## <a name="next-step"></a><span data-ttu-id="b9679-174">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="b9679-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9679-175">Trabajar con Acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="b9679-175">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
