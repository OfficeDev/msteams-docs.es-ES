---
title: Trabajar con Acciones universales para tarjetas adaptables
description: Trabajar con las acciones universales para tarjetas adaptables.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 4361f1c7774837b728c6382df4e62e00ea912e35
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649702"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Trabajar con Acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables proporcionan una forma de implementar escenarios basados en tarjetas adaptables para ambos, Teams y Outlook. Este documento trata lo siguiente:

* [Esquema usado para acciones universales para tarjetas adaptables](#schema-for-universal-actions-for-adaptive-cards)
* [Actualizar modelo](#refresh-model)
* [`adaptiveCard/action` actividad invoke](#adaptivecardaction-invoke-activity)
* [Compatibilidad con versiones anteriores](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a>Guía de inicio rápido para aprovechar las acciones universales para tarjetas adaptables en Teams

1. Reemplace todas las instancias de `Action.Submit` with para actualizar un escenario existente en `Action.Execute` Teams.
2. Agregue una cláusula a la tarjeta adaptable, si desea aprovechar el modelo de actualización automática o si el escenario `refresh` requiere vistas específicas del usuario.

    >[!NOTE]
    > Especifique la `userIds` propiedad que se va a identificar, qué usuarios obtienen actualizaciones automáticas.

3. Controla `adaptiveCard/action` las solicitudes de invocación en el bot.
4. Use el contexto de la solicitud de invocación para responder con tarjetas creadas específicamente para un usuario.

    > [!NOTE]
    > Siempre que el bot devuelva una nueva tarjeta como resultado del procesamiento de una , la respuesta `Action.Execute` debe cumplir con el formato de respuesta.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Esquema de acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables se presentan en el esquema de tarjetas adaptables versión 1.4. Para usar la tarjeta adaptable de forma eficaz, la propiedad de la tarjeta adaptable debe establecerse `version` en 1.4.

> [!NOTE]
> Establecer la propiedad en 1.4 hace que la tarjeta adaptable sea incompatible con clientes antiguos de las plataformas o aplicaciones, como Outlook y Teams, ya que no admiten las acciones universales para tarjetas `version` adaptables.

Si estableces la versión de la tarjeta en menor que 1.4 y usas una o ambas, la propiedad `refresh` y , sucede lo `Action.Execute` siguiente:

| Cliente | Comportamiento |
| :-- | :-- |
| Teams | La tarjeta deja de funcionar. La tarjeta no se actualiza y no se representa en función de `Action.Execute` la versión del Teams cliente. Para garantizar la máxima compatibilidad en Teams, defina `Action.Execute` con una en la propiedad de `Action.Submit` reserva. |

Para obtener más información sobre cómo admitir clientes más antiguos, vea [compatibilidad con versiones anteriores](#backward-compatibility).

### <a name="actionexecute"></a>Action.Exebonito

Al crear tarjetas adaptables, reemplace `Action.Submit` y `Action.Http` por `Action.Execute` . El esquema para `Action.Execute` es similar al de `Action.Submit` .

Para obtener más información, [ veaAction.Execute schema and properties](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Ahora, puedes usar el modelo de actualización para permitir que las tarjetas adaptables se actualicen automáticamente.

## <a name="refresh-model"></a>Actualizar modelo

Para actualizar automáticamente la tarjeta adaptable, defina su propiedad, que `refresh` inserta una acción de tipo y una `Action.Execute` `userIds` matriz.

Para obtener más información, vea [refresh schema and properties](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).

## <a name="user-ids-in-refresh"></a>Id. de usuario en la actualización

Las siguientes son las características de UserIds en refresh:

* UserIds es una matriz de MRI de usuario que forma parte de la `refresh` propiedad en tarjetas adaptables.

* Si la propiedad list se especifica como en la sección de actualización de la tarjeta, la tarjeta no se actualiza `userIds` `userIds: []` automáticamente. En su  lugar, se muestra una opción Actualizar tarjeta al usuario en el menú de triple punto en web o escritorio y en el menú contextual de pulsación larga en móvil, es decir, Android o iOS para actualizar manualmente la tarjeta.

* La propiedad UserIds se agrega porque los canales Teams pueden incluir un gran número de miembros. Si todos los miembros están viendo el canal al mismo tiempo, una actualización automática incondicional da como resultado muchas llamadas simultáneas al bot. Para evitar esto, la propiedad siempre debe incluirse para identificar qué usuarios deben obtener una actualización automática con un máximo de `userIds` *60 (60) MRIs* de usuario .

* Para Teams obtener más información sobre cómo capturar los MRIs de usuario de un miembro de la conversación para agregarlos en la lista userIds en la sección actualizar de la tarjeta adaptable, vea [fetch roster or user profile](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

* Ejemplo Teams MRI del usuario es`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> La `userIds` propiedad se omite en Outlook y la propiedad siempre se activa `refresh` automáticamente. No hay ningún problema de escala en Outlook porque los usuarios ven la tarjeta en diferentes momentos.

El siguiente paso es usar la actividad `adaptiveCard/action` de invocación para comprender qué solicitud debe realizarse después `Action.Execute` de ejecutarse.

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` actividad invoke

Cuando se ejecuta en el cliente, se realiza un nuevo tipo de `Action.Execute` actividad Invoke en el `adaptiveCard/action` bot.

Para obtener más información, vea [request format and properties for a typical invoke `adaptiveCard/action` activity](/adaptive-cards/authoring-cards/universal-action-model#request-format).

Para obtener más información, vea [response format and properties for a typical invoke activity with supported response `adaptiveCard/action` types](/adaptive-cards/authoring-cards/universal-action-model#response-format).

A continuación, puedes aplicar compatibilidad con versiones anteriores a clientes antiguos en diferentes plataformas y hacer que tu tarjeta adaptable sea compatible.

## <a name="backward-compatibility"></a>Compatibilidad con versiones anteriores

Las acciones universales para tarjetas adaptables permiten establecer propiedades que permiten la compatibilidad con versiones anteriores de Outlook y Teams.

### <a name="teams"></a>Teams

Para garantizar la compatibilidad con versiones anteriores de las tarjetas adaptables con versiones anteriores de Teams, debe incluir la propiedad `fallback` y establecer su valor en `Action.Submit` . Además, el código del bot debe procesar tanto `Action.Execute` como `Action.Submit` .

Para obtener más información, vea [compatibilidad con versiones anteriores en Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="code-sample"></a>Ejemplo de código

|Nombre de ejemplo | Descripción | . NETCore |
|----------------|-----------------|--------------|
| Teams bot de restauración | Crea un bot simple que acepte el pedido de alimentos con tarjetas adaptables. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a>Consulte también

* [Acciones de tarjeta adaptable en Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Cómo funcionan los bots](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
