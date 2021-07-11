---
title: Trabajar con acciones universales para tarjetas adaptables
description: Trabajar con las acciones universales para tarjetas adaptables.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 4361f1c7774837b728c6382df4e62e00ea912e35
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649702"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Trabajar con acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables proporcionan una manera de implementar tarjetas adaptables basadas en escenarios tanto para Teams como para Outlook. En este documento se trata lo siguiente:

* [Esquema usado para acciones universales para tarjetas adaptables](#schema-for-universal-actions-for-adaptive-cards)
* [Actualizar modelo](#refresh-model)
* [`adaptiveCard/action` invocar actividad](#adaptivecardaction-invoke-activity)
* [Compatibilidad con versiones anteriores](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a>Guía de inicio rápido para aprovechar las acciones universales para tarjetas adaptables en Teams

1. Reemplace todas las instancias de `Action.Submit` con `Action.Execute` para actualizar un escenario existente en Teams.
2. Agregue una cláusula `refresh` a su tarjeta adaptable si desea aprovechar el modelo de actualización automática o si su escenario requiere vistas específicas del usuario.

    >[!NOTE]
    > Especifique la propiedad `userIds` que se va a identificar, qué usuarios obtienen actualizaciones automáticas.

3. Controle `adaptiveCard/action` las solicitudes de invocación en su bot.
4. Use el contexto de la solicitud de invocación para responder con tarjetas creadas específicamente para un usuario.

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

* UserIds es una matriz de usuario de MRI que forma parte de la propiedad `refresh` en tarjetas adaptables.

* Si la lista de propiedad`userIds` se especifica como `userIds: []` en la sección de actualización de la tarjeta, la tarjeta no se actualiza automáticamente. En su lugar, se muestra al usuario una opción **Actualizar tarjeta** en el menú de puntos triples en la web o el escritorio, y en el menú contextual de larga duración en dispositivos móviles, es decir, Android o iOS para actualizar manualmente la tarjeta.

* Se ha agregado la propiedad UserIds porque los canales de Teams pueden incluir un gran número de miembros. Si todos los miembros ven el canal al mismo tiempo, una actualización automática incondicional da como resultado muchas llamadas simultáneas al bot. Para evitar esto, la propiedad `userIds` siempre debe incluirse para identificar qué usuarios deben obtener una actualización automática con un máximo de *60 (sesenta) MRIs de usuario*.

* Para obtener más información sobre cómo puede capturar los MRI de usuario de los miembros de la conversación de Teams para agregarlos a la lista userIds en la sección de actualización de la tarjeta adaptable, consulte[capturar la lista o el perfil de usuario](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

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

Para garantizar la compatibilidad de versiones anteriores de sus tarjetas adaptables con versiones anteriores de Teams, debe incluir la propiedad `fallback` y establecer su valor en `Action.Submit`. Además, el código de su bot debe procesar tanto`Action.Execute` como `Action.Submit`.

Para obtener más información, consulte [compatibilidad con versiones anteriores en Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NETCore |
|----------------|-----------------|--------------|
| Bot de servicio de alimentos de Teams | Cree un bot sencillo que acepte pedidos de alimentos mediante el uso de tarjetas adaptables. |[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a>Consulte también

* [Acciones de tarjeta adaptable en Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Cómo funcionan los bots](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
