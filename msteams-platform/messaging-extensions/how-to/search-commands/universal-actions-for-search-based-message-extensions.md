---
title: Acciones universales para extensiones de mensajes basadas en búsqueda
author: v-ypalikila
description: En este artículo, obtenga información sobre Acciones universales y actualización automática de tarjetas adaptables en extensiones de mensaje basadas en búsquedas.
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: 18f5b783797d69144aac82e5ebd95fc30dad57a2
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819971"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>Acciones universales para extensiones de mensajes basadas en búsqueda

Las tarjetas adaptables de las extensiones de mensaje basadas en búsqueda ahora admiten Acciones universales. Para habilitar Acciones universales para extensiones de mensaje basadas en búsqueda, la aplicación debe cumplir el [esquema de Acciones universales para tarjetas adaptables](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) junto con los siguientes requisitos:

1. La aplicación debe tener un bot de conversación definido en el manifiesto de la aplicación.
1. Si ya tiene un bot conversacional, debe usar el mismo bot que se usa en la extensión de mensaje.
1. Si la tarjeta se envía en un grupo, la aplicación debe especificar `team` o `groupchat` el ámbito de su bot en el manifiesto.

Ejemplo de un esquema JSON con `team` valores y `groupchat` :

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "scopes": [
                    "team",
                    "personal",
                    "groupchat"
                ]
        }
    ],
    "composeExtensions": [
        {
            "canUpdateConfiguration": true,
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%", // Use the same bot as what is specified in the bots section above
        }
    ]
}
```

## <a name="automatic-refresh-for-adaptive-cards-in-search-based-message-extensions"></a>Actualización automática de tarjetas adaptables en extensiones de mensaje basadas en búsqueda

Habilite la actualización automática para tarjetas adaptables en extensiones de mensaje basadas en búsquedas para asegurarse de que los usuarios siempre ven la información más reciente. Para habilitarlo, defina `userIds` la matriz en o `8:orgid:<AAD ID>` en `29:<ID>` formato en la `refresh` propiedad . Para obtener más información, vea [Trabajar con acciones universales para tarjetas adaptables](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh).

Ejemplo de `userIds` matriz en la `refresh` propiedad :

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "userIds": [
                "8:orgid:<AADID>",
                "29:<id>"
            ],
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

> [!NOTE]
> La actualización automática está habilitada para todos los usuarios del chat de grupo o canal con *menos o igual que* 60 usuarios. En el caso de las conversaciones (chat en grupo o canal) con más de 60 usuarios, los usuarios pueden usar el botón Actualizar en el menú de opciones de mensaje para obtener el resultado más reciente.

Ejemplo de `Action.Execute` en la `refresh` propiedad :

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

## <a name="just-in-time-install"></a>Instalación Just-In-Time

Just-In-Time (JIT) le permite instalar una extensión de tarjeta o mensaje para varios usuarios en un chat de grupo o canal. Para admitir acciones universales en extensiones de mensaje basadas en búsquedas, el bot se agrega a la conversación donde el usuario envía la tarjeta (con `Action.Execute`).

Cuando un usuario selecciona una tarjeta y la envía en un chat de grupo o canal, aparece un mensaje de instalación **JIT** . Una vez que el usuario selecciona la opción **de envío** , la aplicación se agrega a todos los usuarios en el chat o canal en segundo plano.

> [!NOTE]
> En el caso de las aplicaciones que no tienen `Action.Execute` y `refresh` el esquema definido, el símbolo del sistema de instalación no se muestra a los usuarios.

Ejemplo de un flujo de usuario de instalación dinámica de ME y JIT:

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF muestra el flujo de usuario para una extensión de mensaje dinámica e instalación JIT.":::

## <a name="see-also"></a>Vea también

* [Extensiones de mensajes](../../what-are-messaging-extensions.md)
* [Tarjetas adaptables](../../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Acciones universales para tarjetas adaptables](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
