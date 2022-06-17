---
title: Agregar un menú de bot
description: En este módulo, aprenderá a agregar un menú de bot en Microsoft Teams y a crear menús para bots en Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: ed65699b930d3e5334dd7fbb03da18a1482d6e5d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143385"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Agregar un menú de bot en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Para ayudar a la detección y ayudar a educar a los usuarios sobre la funcionalidad del bot, ahora puede agregar menús que aparecen cada vez que el usuario interactúa con el bot. El menú mostrará el texto del comando y también proporcionará texto de ayuda, como un ejemplo de uso o una descripción del propósito del comando.

![Captura de pantalla del menú del bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Cuando un usuario selecciona un elemento de menú, la cadena de comando se inserta en el cuadro de texto para ayudar al usuario a completar el mensaje del bot.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Compatibilidad con menús de bot en Teams aplicación móvil

> [!NOTE]
> Los menús de bot no se muestran en dispositivos móviles.

## <a name="app-manifest"></a>Manifiesto de la aplicación

Para crear un menú de bot, agregue un nuevo [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) objeto al manifiesto de la aplicación en la sección bot. Puede declarar menús individuales con comandos independientes para cada ámbito que admita el bot (`personal`, `groupChat`o `team`) Cada menú admite hasta 10 comandos.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Extracto del manifiesto: menú único para ambos ámbitos

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "scopes": [
        "personal",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team",
            "personal"
          ],
          "commands":[
            {
              "title":"Help",
              "description":"Displays this help message"
            },
            {
              "title":"Search Flights",
              "description":"Search flights from Seattle to Phoenix May 2-5 departing after 3pm"
            },
            {
              "title":"Search Hotels",
              "description":"Search hotels in Portland tonight"
            },
            {
              "title":"Best Time to Fly",
              "description":"Best time to fly to London for a 5 day trip this summer"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Extracto del manifiesto: menú independiente por ámbito

```json
{
  ...
  "bots":[
    {
      "botId":"[Microsoft app ID for your bot]",
      "scopes": [
        "groupChat",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for channels"
            }
          ]
        },
        {
          "scopes":[
            "groupChat"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for group chat"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

## <a name="best-practices"></a>Procedimientos recomendados

* Mantenga la simplicidad: el menú del bot está diseñado para presentar las funcionalidades clave del bot.
* Manténgalo corto: las opciones de menú no deben ser instrucciones de lenguaje natural extremadamente largas y complejas, ya que deben ser comandos simples.
* Siempre disponible: las acciones o comandos del menú del bot deben ser siempre invocables, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.
