---
title: Agregar un menú bot
description: Describe cómo crear menús para bots en Microsoft Teams
keywords: creación de menús de bots de teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 14100c9032f0adf964975abbe436c84194475a99
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157686"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Agregar un menú bot en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Para ayudar a la detección y ayudar a educar a los usuarios sobre la funcionalidad del bot, ahora puedes agregar menús que superen cada vez que el usuario interactúe con el bot. El menú mostrará el texto del comando y también proporcionará texto de ayuda, como un ejemplo de uso o una descripción del propósito del comando.

![Captura de pantalla del menú bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Cuando un usuario selecciona un elemento de menú, la cadena de comandos se inserta en el cuadro de texto para ayudar al usuario a completar el mensaje del bot.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Compatibilidad con menú bot en Teams móvil
> [!NOTE] 
> Los menús bot no se muestran en dispositivos móviles.

## <a name="app-manifest"></a>Manifiesto de la aplicación

Para crear un menú bot, agrega un nuevo objeto al manifiesto [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) de la aplicación en la sección bot. Puede declarar menús individuales con comandos independientes para cada ámbito que el bot admite ( , o ) Cada menú admite hasta `personal` `groupChat` `team` 10 comandos.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Extracto de manifiesto: menú único para ambos ámbitos

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Extracto de manifiesto: menú independiente por ámbito

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

* Mantenlo sencillo: el menú del bot está diseñado para presentar las funciones clave del bot.
* Tenga en cuenta que las opciones de menú no deben ser instrucciones de lenguaje natural extremadamente largas y complejas; deben ser comandos simples.
* Siempre disponible: las acciones o comandos del menú Bot deben ser siempre invokables, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.
