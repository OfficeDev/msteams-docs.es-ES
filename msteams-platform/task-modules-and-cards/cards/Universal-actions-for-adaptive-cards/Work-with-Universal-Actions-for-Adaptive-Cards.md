---
title: Trabajar con acciones universales para tarjetas adaptables
description: Aprenda a trabajar con las acciones universales para tarjetas adaptables, incluido el esquema de UniversalActions para tarjetas adaptables, el modelo Refresh y la compatibilidad con versiones anteriores con ejemplos de código.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 488385d560f3f372be8149631eb1a04a3642f65f
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888366"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Trabajar con Acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables proporcionan una forma de implementar escenarios basados en tarjetas adaptables para ambos, Teams y Outlook. En este documento se tratan los temas siguientes:

* [Esquema usado para acciones universales para tarjetas adaptables](#schema-for-universal-actions-for-adaptive-cards)
* [Actualizar modelo](#refresh-model)
* [`adaptiveCard/action` invocar actividad](#adaptivecardaction-invoke-activity)
* [Compatibilidad con versiones anteriores](#backward-compatibility)

## <a name="quick-start-guide-to-use-universal-actions-for-adaptive-cards-in-teams"></a>Guía de inicio rápido para usar acciones universales para tarjetas adaptables en Teams

1. Reemplace todas las instancias de `Action.Submit` con `Action.Execute` para actualizar un escenario existente en Teams.
2. Agregue una cláusula a la tarjeta adaptable, si desea usar el modelo de actualización automática o si su escenario `refresh` requiere vistas específicas del usuario.

    >[!NOTE]
    > Especifique la propiedad `userIds` que se va a identificar, qué usuarios obtienen actualizaciones automáticas.

3. Controle `adaptiveCard/action` las solicitudes de invocación en su bot.
4. Use el contexto de la solicitud de invocación para responder de nuevo con tarjetas creadas para un usuario.

    > [!NOTE]
    > Cada vez que el bot devuelve una nueva tarjeta como resultado del procesamiento de un `Action.Execute`, la respuesta debe ajustarse al formato de respuesta.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Esquema para acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables se presentan en el esquema de tarjetas adaptables versión 1.4. Para usar la tarjeta adaptable de forma eficaz, la propiedad `version` de su tarjeta adaptable debe establecerse en 1.4.

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

* UserIds es una matriz de MRIs de usuario, que forma parte de la `refresh` propiedad en Tarjetas adaptables.

* Si la lista de propiedad`userIds` se especifica como `userIds: []` en la sección de actualización de la tarjeta, la tarjeta no se actualiza automáticamente. En su lugar, se muestra al usuario una opción **Actualizar tarjeta** en el menú de puntos triples en la web o el escritorio, y en el menú contextual de larga duración en dispositivos móviles, es decir, Android o iOS para actualizar manualmente la tarjeta.

* Se ha agregado la propiedad UserIds porque los canales de Teams pueden incluir un gran número de miembros. Si todos los miembros ven el canal al mismo tiempo, una actualización automática incondicional da como resultado muchas llamadas simultáneas al bot. La propiedad siempre debe incluirse para identificar qué usuarios deben obtener una actualización automática con un máximo de `userIds` *60 (60) MRIs de usuario.*

* Puede capturar los TEAMS de usuario del miembro de la conversación. Para obtener más información sobre cómo agregar en la lista userIds en la sección de actualización de la tarjeta adaptable, vea [fetch roster or user profile](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

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

Las acciones universales para tarjetas adaptables permiten establecer propiedades que permiten la compatibilidad con versiones anteriores de Outlook y Teams.

### <a name="teams"></a>Teams

Para garantizar la compatibilidad de versiones anteriores de sus tarjetas adaptables con versiones anteriores de Teams, debe incluir la propiedad `fallback` y establecer su valor en `Action.Submit`. Además, el código de su bot debe procesar tanto`Action.Execute` como `Action.Submit`.

Para obtener más información, consulte [compatibilidad con versiones anteriores en Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="code-samples"></a>Ejemplos de código

|Ejemplo de nombre | Descripción | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Bot de servicio de alimentos de Teams | Crea un bot que acepte el pedido de alimentos con tarjetas adaptables. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| Aún no disponible |
| Tarjetas adaptables de flujos de trabajo secuenciales | Muestra cómo implementar flujos de trabajo secuenciales, vistas específicas del usuario y tarjetas adaptables actualizadas en bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Consulte también

* [Acciones de tarjeta adaptable en Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Cómo funcionan los bots](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Flujos de trabajo secuenciales](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md)
* [Tarjetas actualizadas](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
