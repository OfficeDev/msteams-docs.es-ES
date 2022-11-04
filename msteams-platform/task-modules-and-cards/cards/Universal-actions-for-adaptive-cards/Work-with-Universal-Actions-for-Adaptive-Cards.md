---
title: Trabajar con acciones universales para tarjetas adaptables
description: Aprenda a trabajar con las acciones universales para tarjetas adaptables, incluido el esquema para UniversalActions para tarjetas adaptables, el modelo de actualización y la compatibilidad con versiones anteriores.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: d723b565cadfacc550cd4fd9c8648149e9d164e2
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833012"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Trabajar con Acciones universales para tarjetas adaptables

Universal Actions for Adaptive Cards provide a way to implement Adaptive Card based scenarios for both, Teams and Outlook. This document covers the following topics:

* [Esquema usado para acciones universales para tarjetas adaptables](#schema-for-universal-actions-for-adaptive-cards)
* [Actualizar modelo](#refresh-model)
* [`adaptiveCard/action` invocar actividad](#adaptivecardaction-invoke-activity)
* [Compatibilidad con versiones anteriores](#backward-compatibility)

## <a name="quick-start-guide-to-use-universal-actions-for-adaptive-cards-in-teams"></a>Guía de inicio rápido para usar las acciones universales para tarjetas adaptables en Teams

1. Reemplace todas las instancias de `Action.Submit` con `Action.Execute` para actualizar un escenario existente en Teams.
2. Agregue una cláusula `refresh` a su tarjeta adaptable si quiere usar el modelo de actualización automática o si su escenario requiere vistas específicas del usuario.

    >[!NOTE]
    > Especifique la `userIds` propiedad para identificar qué usuarios obtienen actualizaciones automáticas.

3. Controle `adaptiveCard/action` las solicitudes de invocación en su bot.
4. Use el contexto de la solicitud de invocación para responder con tarjetas creadas para un usuario.

    > [!NOTE]
    > Cada vez que el bot devuelve una nueva tarjeta como resultado del procesamiento de un `Action.Execute`, la respuesta debe ajustarse al formato de respuesta.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Esquema para acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables se presentan en la versión 1.4 del esquema de tarjetas adaptables. Para usar la tarjeta adaptable de forma eficaz, la propiedad `version` de su tarjeta adaptable debe establecerse en 1.4.

> [!NOTE]
> Al establecer la propiedad `version` en 1.4, la tarjeta adaptable no es compatible con clientes más antiguos de las plataformas o aplicaciones, como Outlook y Teams, ya que no admiten acciones universales para tarjetas adaptables.

Si establece la versión de la tarjeta en menos de 1.4 y usa una o ambas, `refresh` la propiedad y `Action.Execute`, ocurre lo siguiente:

| Cliente | Comportamiento |
| :-- | :-- |
| Teams | Su tarjeta deja de funcionar. La tarjeta no se actualiza y `Action.Execute` no se representa en función de la versión del cliente de Teams. Para garantizar la máxima compatibilidad en Teams, defina `Action.Execute` con una `Action.Submit` en la propiedad de reserva. |

Para obtener más información sobre cómo admitir clientes más antiguos, consulte [compatibilidad con versiones anteriores](#backward-compatibility).

### <a name="actionexecute"></a>Action.Execute

Al crear tarjetas adaptables, reemplace `Action.Submit` y `Action.Http` por `Action.Execute`. El esquema para`Action.Execute` es similar al de `Action.Submit`.

Para obtener más información, consulte[esquema Action.Execute y propiedades](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Ahora, puede usar el modelo de actualización para permitir que las tarjetas adaptables se actualicen automáticamente.

## <a name="refresh-model"></a>Actualizar modelo

Para actualizar automáticamente la tarjeta adaptable, defina su propiedad, `refresh`que inserta una acción del tipo `Action.Execute` y una matriz`userIds`.

Para obtener más información, consulte[actualizar esquema y propiedades](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).

## <a name="user-ids-in-refresh"></a>Identificadores de usuario en la actualización

Estas son las características de UserIds en la actualización:

* UserIds es una matriz de MRI de usuario, que forma parte de la propiedad `refresh` en Tarjetas adaptables.

* Si la `userIds` propiedad list se especifica como `userIds: []` en la sección de actualización de la tarjeta, la tarjeta no se actualiza automáticamente. En su lugar, se muestra una opción **Actualizar tarjeta** al usuario en el menú de puntos triples del cliente web o escritorio de Teams y en el menú contextual de prensa larga en teams mobile, es decir, Android o iOS para actualizar manualmente la tarjeta. Como alternativa, puede optar por omitir `userIds` la propiedad de actualización por completo en caso de que el escenario implique <=60 miembros en los canales o chats de grupo de Teams. El cliente de Teams invoca automáticamente llamadas de actualización para todos los usuarios si el grupo o canal tiene <=60 usuarios.

* Se ha agregado la propiedad UserIds porque los canales de Teams pueden incluir un gran número de miembros. Si todos los miembros ven el canal al mismo tiempo, una actualización automática incondicional da como resultado muchas llamadas simultáneas al bot. La propiedad `userIds` siempre debe incluirse para identificar qué usuarios deben obtener una actualización automática con un máximo de *60 (sesenta) MRI de usuario*.

* You can fetch Teams conversation member's user MRIs. For more information on how to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

 Puede obtener la MRI del usuario para el canal, el chat de grupo o el chat 1:1 mediante el ejemplo siguiente:

 1. Uso de TurnContext  

     `userMRI= turnContext.Activity.From.Id`

 1. Uso del método GetMemberAsync
  
     `var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);var userMRI = member.Id;`

* Un ejemplo de MRI de usuario de Teams es`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> La propiedad `userIds` se omite en Outlook y la propiedad `refresh` siempre se activa automáticamente. No hay ningún problema de escala en Outlook porque los usuarios ven la tarjeta en momentos diferentes.

El siguiente paso consiste en usar`adaptiveCard/action`la actividad de invocación para comprender qué solicitud se debe realizar luego de que `Action.Execute`es ejecutado.

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` invocar actividad

Cuando se ejecuta `Action.Execute` en el cliente, se realiza un nuevo tipo de actividad Invoke `adaptiveCard/action` en su bot.

Para obtener más información, consulte[el formato de solicitud y las propiedades de una típica `adaptiveCard/action`actividad de invocación ](/adaptive-cards/authoring-cards/universal-action-model#request-format).

Para obtener más información, consulte[el formato de respuesta y las propiedades de una típica `adaptiveCard/action`actividad de invocación con los tipos de respuesta admitidos](/adaptive-cards/authoring-cards/universal-action-model#response-format).

A continuación, puede aplicar compatibilidad con versiones anteriores a clientes más antiguos en distintas plataformas y hacer que la tarjeta adaptable sea compatible.

## <a name="backward-compatibility"></a>Compatibilidad con versiones anteriores

Las acciones universales para tarjetas adaptables le permiten establecer propiedades que permiten la compatibilidad con versiones anteriores de Outlook y Teams.

### <a name="teams"></a>Teams

To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`. Also, your bot code must process both `Action.Execute` and `Action.Submit`.

Para obtener más información, consulte [compatibilidad con versiones anteriores en Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="code-samples"></a>Ejemplos de código

|Ejemplo de nombre | Descripción | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Bot de servicio de alimentos de Teams | Cree un bot que acepte pedidos de alimentos mediante el uso de tarjetas adaptables. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| ND |
| Tarjetas adaptables de flujos de trabajo secuenciales | Demostrar cómo implementar flujos de trabajo secuenciales, vistas específicas del usuario y Tarjetas adaptables actualizadas en bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Consulte también

* [Acciones de tarjeta adaptable en Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Cómo funcionan los bots](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Flujos de trabajo secuenciales](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md)
* [Tarjetas actualizadas](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [Comentarios de finalización de formularios](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
