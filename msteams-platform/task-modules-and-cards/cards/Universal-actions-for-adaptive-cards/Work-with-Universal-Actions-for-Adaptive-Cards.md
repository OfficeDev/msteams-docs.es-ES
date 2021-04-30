---
title: Trabajar con acciones universales para tarjetas adaptables
description: Trabajar con las acciones universales para tarjetas adaptables.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 8c260a4893d38ad365cbb3bdd5a7613a1b42654f
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088871"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="573e7-103">Trabajar con acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="573e7-103">Work with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="573e7-104">Las acciones universales para tarjetas adaptables proporcionan una forma de implementar escenarios basados en tarjetas adaptables para ambos, Teams y Outlook.</span><span class="sxs-lookup"><span data-stu-id="573e7-104">Universal Actions for Adaptive Cards provides a way to implement Adaptive Card based scenarios for both, Teams and Outlook.</span></span> <span data-ttu-id="573e7-105">Este documento trata lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="573e7-105">This document covers the following:</span></span>

* [<span data-ttu-id="573e7-106">Esquema usado para acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="573e7-106">Schema used for Universal Actions for Adaptive Cards</span></span>](#schema-for-universal-actions-for-adaptive-cards)
* [<span data-ttu-id="573e7-107">Actualizar modelo</span><span class="sxs-lookup"><span data-stu-id="573e7-107">Refresh model</span></span>](#refresh-model)
* [<span data-ttu-id="573e7-108">`adaptiveCard/action` actividad invoke</span><span class="sxs-lookup"><span data-stu-id="573e7-108">`adaptiveCard/action` invoke activity</span></span>](#adaptivecardaction-invoke-activity)
* [<span data-ttu-id="573e7-109">Compatibilidad con versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="573e7-109">Backward compatibility</span></span>](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a><span data-ttu-id="573e7-110">Guía de inicio rápido para aprovechar las acciones universales para tarjetas adaptables en Teams</span><span class="sxs-lookup"><span data-stu-id="573e7-110">Quick start guide to leverage Universal Actions for Adaptive Cards in Teams</span></span>

1. <span data-ttu-id="573e7-111">Reemplace todas las instancias de `Action.Submit` with para actualizar un escenario existente en `Action.Execute` Teams.</span><span class="sxs-lookup"><span data-stu-id="573e7-111">Replace all instances of `Action.Submit` with `Action.Execute` to update an existing scenario on Teams.</span></span>
2. <span data-ttu-id="573e7-112">Agregue una cláusula a la tarjeta adaptable, si desea aprovechar el modelo de actualización automática o si el escenario `refresh` requiere vistas específicas del usuario.</span><span class="sxs-lookup"><span data-stu-id="573e7-112">Add a `refresh` clause to your Adaptive Card, if you want to leverage the automatic refresh model or if your scenario requires User Specific Views.</span></span>

    >[!NOTE]
    > <span data-ttu-id="573e7-113">Especifique la `userIds` propiedad que se va a identificar, qué usuarios obtienen actualizaciones automáticas.</span><span class="sxs-lookup"><span data-stu-id="573e7-113">Specify the `userIds` property to identify, which users get automatic updates.</span></span>

3. <span data-ttu-id="573e7-114">Controla `adaptiveCard/action` las solicitudes de invocación en el bot.</span><span class="sxs-lookup"><span data-stu-id="573e7-114">Handle `adaptiveCard/action` invoke requests in your bot.</span></span>
4. <span data-ttu-id="573e7-115">Use el contexto de la solicitud de invocación para responder con tarjetas creadas específicamente para un usuario.</span><span class="sxs-lookup"><span data-stu-id="573e7-115">Use the invoke request's context to respond back with cards that are specifically created for a user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="573e7-116">Siempre que el bot devuelva una nueva tarjeta como resultado del procesamiento de una , la respuesta `Action.Execute` debe cumplir con el formato de respuesta.</span><span class="sxs-lookup"><span data-stu-id="573e7-116">Whenever your bot returns a new card as a result of processing an `Action.Execute`, the response must conform to the response format.</span></span>

## <a name="schema-for-universal-actions-for-adaptive-cards"></a><span data-ttu-id="573e7-117">Esquema de acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="573e7-117">Schema for Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="573e7-118">Las acciones universales para tarjetas adaptables se presentan en el esquema de tarjetas adaptables versión 1.4.</span><span class="sxs-lookup"><span data-stu-id="573e7-118">Universal Actions for Adaptive Cards is introduced in the Adaptive Cards schema version 1.4.</span></span> <span data-ttu-id="573e7-119">Para usar la tarjeta adaptable de forma eficaz, la propiedad de la tarjeta adaptable debe establecerse `version` en 1.4.</span><span class="sxs-lookup"><span data-stu-id="573e7-119">To use Adaptive Card effectively, the `version` property of your Adaptive Card must be set to 1.4.</span></span>

> [!NOTE]
> <span data-ttu-id="573e7-120">Establecer la propiedad en 1.4 hace que la tarjeta adaptable sea incompatible con clientes antiguos de las plataformas o aplicaciones, como Outlook y Teams, ya que no admiten las acciones universales para tarjetas `version` adaptables.</span><span class="sxs-lookup"><span data-stu-id="573e7-120">Setting the `version` property to 1.4 makes your Adaptive Card incompatible with older clients of the platforms or applications, such as Outlook and Teams, as they do not support the Universal Actions for Adaptive Cards.</span></span>

<span data-ttu-id="573e7-121">Si estableces la versión de la tarjeta en menor que 1.4 y usas una o ambas, la propiedad `refresh` y , sucede lo `Action.Execute` siguiente:</span><span class="sxs-lookup"><span data-stu-id="573e7-121">If you set the card version to less than 1.4 and use either or both, `refresh` property and `Action.Execute`, the following happens:</span></span>

| <span data-ttu-id="573e7-122">Client</span><span class="sxs-lookup"><span data-stu-id="573e7-122">Client</span></span> | <span data-ttu-id="573e7-123">Comportamiento</span><span class="sxs-lookup"><span data-stu-id="573e7-123">Behavior</span></span> |
| :-- | :-- |
| <span data-ttu-id="573e7-124">Teams</span><span class="sxs-lookup"><span data-stu-id="573e7-124">Teams</span></span> | <span data-ttu-id="573e7-125">La tarjeta deja de funcionar.</span><span class="sxs-lookup"><span data-stu-id="573e7-125">Your card stops working.</span></span> <span data-ttu-id="573e7-126">La tarjeta no se actualiza y no se representa en función de `Action.Execute` la versión del Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="573e7-126">Card is not refreshed and `Action.Execute` does not render depending on the version of the Teams client.</span></span> <span data-ttu-id="573e7-127">Para garantizar la máxima compatibilidad en Teams, defina `Action.Execute` con una en la propiedad de `Action.Submit` reserva.</span><span class="sxs-lookup"><span data-stu-id="573e7-127">To ensure maximum compatibility in Teams, define `Action.Execute` with an `Action.Submit` in the fallback property.</span></span> |

<span data-ttu-id="573e7-128">Para obtener más información sobre cómo admitir clientes más antiguos, vea [compatibilidad con versiones anteriores](#backward-compatibility).</span><span class="sxs-lookup"><span data-stu-id="573e7-128">For more information on how to support older clients, see [backward compatibility](#backward-compatibility).</span></span>

### <a name="actionexecute"></a><span data-ttu-id="573e7-129">Action.Exebonito</span><span class="sxs-lookup"><span data-stu-id="573e7-129">Action.Execute</span></span>

<span data-ttu-id="573e7-130">Al crear tarjetas adaptables, reemplace `Action.Submit` y `Action.Http` por `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="573e7-130">When authoring Adaptive Cards, replace `Action.Submit` and `Action.Http` with `Action.Execute`.</span></span> <span data-ttu-id="573e7-131">El esquema para `Action.Execute` es similar al de `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="573e7-131">The schema for `Action.Execute` is similar to that of `Action.Submit`.</span></span>

<span data-ttu-id="573e7-132">Para obtener más información, [ veaAction.Execute schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span><span class="sxs-lookup"><span data-stu-id="573e7-132">For more information, see [Action.Execute schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="573e7-133">Ahora, puedes usar el modelo de actualización para permitir que las tarjetas adaptables se actualicen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="573e7-133">Now, you can use the refresh model to allow Adaptive Cards to update automatically.</span></span>

## <a name="refresh-model"></a><span data-ttu-id="573e7-134">Actualizar modelo</span><span class="sxs-lookup"><span data-stu-id="573e7-134">Refresh model</span></span>

<span data-ttu-id="573e7-135">Para actualizar automáticamente la tarjeta adaptable, defina su propiedad, que `refresh` inserta una acción de tipo y una `Action.Execute` `userIds` matriz.</span><span class="sxs-lookup"><span data-stu-id="573e7-135">To automatically refresh your Adaptive Card, define its `refresh` property, which embeds an action of type `Action.Execute` and an `userIds` array.</span></span>

<span data-ttu-id="573e7-136">Para obtener más información, vea [refresh schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span><span class="sxs-lookup"><span data-stu-id="573e7-136">For more information, see [refresh schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span></span>

## <a name="user-ids-in-refresh"></a><span data-ttu-id="573e7-137">Id. de usuario en la actualización</span><span class="sxs-lookup"><span data-stu-id="573e7-137">User IDs in refresh</span></span>

<span data-ttu-id="573e7-138">Las siguientes son las características de UserIds en refresh:</span><span class="sxs-lookup"><span data-stu-id="573e7-138">The following are the features of UserIds in refresh:</span></span>

* <span data-ttu-id="573e7-139">UserIds es una matriz de MRI de usuario que forma parte de la `refresh` propiedad en tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="573e7-139">UserIds is an array of user MRI's which is part of the `refresh` property in Adaptive Cards.</span></span>

* <span data-ttu-id="573e7-140">Si la propiedad list se especifica como en la sección de actualización de la tarjeta, la tarjeta no se actualiza `userIds` `userIds: []` automáticamente.</span><span class="sxs-lookup"><span data-stu-id="573e7-140">If the `userIds` list property is specified as `userIds: []` in the refresh section of the card, the card is not automatically refreshed.</span></span> <span data-ttu-id="573e7-141">En su  lugar, se muestra una opción Actualizar tarjeta al usuario en el menú de triple punto en web o escritorio y en el menú contextual de pulsación larga en móvil, es decir, Android o iOS para actualizar manualmente la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="573e7-141">Instead, a **Refresh Card** option is displayed to the user in the triple dot menu in web or desktop and in the long press context menu in mobile, that is, Android or iOS to manually refresh the card.</span></span>

* <span data-ttu-id="573e7-142">La propiedad UserIds se agrega porque los canales Teams pueden incluir un gran número de miembros.</span><span class="sxs-lookup"><span data-stu-id="573e7-142">UserIds property is added because channels in Teams can include a large number of members.</span></span> <span data-ttu-id="573e7-143">Si todos los miembros están viendo el canal al mismo tiempo, una actualización automática incondicional da como resultado muchas llamadas simultáneas al bot.</span><span class="sxs-lookup"><span data-stu-id="573e7-143">If all members are viewing the channel at the same time, an unconditional automatic refresh results in many concurrent calls to the bot.</span></span> <span data-ttu-id="573e7-144">Para evitar esto, la propiedad siempre debe incluirse para identificar qué usuarios deben obtener una actualización automática con un máximo de `userIds` *60 (60) MRIs* de usuario .</span><span class="sxs-lookup"><span data-stu-id="573e7-144">To avoid this, the `userIds` property must always be included to identify which users must get an automatic refresh with a maximum of *60 (sixty) user MRIs*.</span></span>

* <span data-ttu-id="573e7-145">Para Teams obtener más información sobre cómo capturar los MRIs de usuario de un miembro de la conversación para agregarlos en la lista userIds en la sección actualizar de la tarjeta adaptable, vea [fetch roster or user profile](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span><span class="sxs-lookup"><span data-stu-id="573e7-145">For more information on how you can fetch Teams conversation member's user MRIs to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span></span>

* <span data-ttu-id="573e7-146">Ejemplo Teams MRI del usuario es`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span><span class="sxs-lookup"><span data-stu-id="573e7-146">Sample Teams user MRI is `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span></span>

> [!NOTE]
> <span data-ttu-id="573e7-147">La `userIds` propiedad se omite en Outlook y la propiedad siempre se activa `refresh` automáticamente.</span><span class="sxs-lookup"><span data-stu-id="573e7-147">The `userIds` property is ignored in Outlook, and the `refresh` property is always automatically activated.</span></span> <span data-ttu-id="573e7-148">No hay ningún problema de escala en Outlook porque los usuarios ven la tarjeta en diferentes momentos.</span><span class="sxs-lookup"><span data-stu-id="573e7-148">There is no scale issue in Outlook because users view the card at different times.</span></span>

<span data-ttu-id="573e7-149">El siguiente paso es usar la actividad `adaptiveCard/action` de invocación para comprender qué solicitud debe realizarse después `Action.Execute` de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="573e7-149">Next step is to use the `adaptiveCard/action` invoke activity to understand what request must be made after `Action.Execute` is executed.</span></span>

## <a name="adaptivecardaction-invoke-activity"></a><span data-ttu-id="573e7-150">`adaptiveCard/action` actividad invoke</span><span class="sxs-lookup"><span data-stu-id="573e7-150">`adaptiveCard/action` invoke activity</span></span>

<span data-ttu-id="573e7-151">Cuando se ejecuta en el cliente, se realiza un nuevo tipo de `Action.Execute` actividad Invoke en el `adaptiveCard/action` bot.</span><span class="sxs-lookup"><span data-stu-id="573e7-151">When `Action.Execute` is executed in the client, a new type of Invoke activity `adaptiveCard/action` is made to your bot.</span></span>

<span data-ttu-id="573e7-152">Para obtener más información, vea [request format and properties for a typical invoke `adaptiveCard/action` activity](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format).</span><span class="sxs-lookup"><span data-stu-id="573e7-152">For more information, see [request format and properties for a typical `adaptiveCard/action` invoke activity](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format).</span></span>

<span data-ttu-id="573e7-153">Para obtener más información, vea [response format and properties for a typical invoke activity with supported response `adaptiveCard/action` types](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format).</span><span class="sxs-lookup"><span data-stu-id="573e7-153">For more information, see [response format and properties for a typical `adaptiveCard/action` invoke activity with supported response types](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format).</span></span>

<span data-ttu-id="573e7-154">A continuación, puedes aplicar compatibilidad con versiones anteriores a clientes antiguos en diferentes plataformas y hacer que tu tarjeta adaptable sea compatible.</span><span class="sxs-lookup"><span data-stu-id="573e7-154">Next, you can apply backward compatibility to older clients across different platforms and make your Adaptive Card compatible.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="573e7-155">Compatibilidad con versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="573e7-155">Backward compatibility</span></span>

<span data-ttu-id="573e7-156">Las acciones universales para tarjetas adaptables permiten establecer propiedades que permiten la compatibilidad con versiones anteriores de Outlook y Teams.</span><span class="sxs-lookup"><span data-stu-id="573e7-156">Universal Actions for Adaptive Cards allows you to set properties that enable backward compatibility with older versions of Outlook and Teams.</span></span>

### <a name="teams"></a><span data-ttu-id="573e7-157">Teams</span><span class="sxs-lookup"><span data-stu-id="573e7-157">Teams</span></span>

<span data-ttu-id="573e7-158">Para garantizar la compatibilidad con versiones anteriores de las tarjetas adaptables con versiones anteriores de Teams, debe incluir la propiedad `fallback` y establecer su valor en `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="573e7-158">To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`.</span></span> <span data-ttu-id="573e7-159">Además, el código del bot debe procesar tanto `Action.Execute` como `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="573e7-159">Also, your bot code must process both `Action.Execute` and `Action.Submit`.</span></span>

<span data-ttu-id="573e7-160">Para obtener más información, vea [compatibilidad con versiones anteriores en Teams](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams).</span><span class="sxs-lookup"><span data-stu-id="573e7-160">For more information, see [backward compatibility on Teams](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams).</span></span>

## <a name="see-also"></a><span data-ttu-id="573e7-161">Vea también</span><span class="sxs-lookup"><span data-stu-id="573e7-161">See also</span></span>

* [<span data-ttu-id="573e7-162">Acciones de tarjeta adaptable en Teams</span><span class="sxs-lookup"><span data-stu-id="573e7-162">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="573e7-163">Cómo funcionan los bots</span><span class="sxs-lookup"><span data-stu-id="573e7-163">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
