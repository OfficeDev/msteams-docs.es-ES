---
title: Agregar un menú de bot
description: Describe cómo crear menús para bots en Microsoft Teams.
keywords: creación de menús bots de Microsoft Teams
ms.date: 05/20/2019
ms.openlocfilehash: 36a224dc21cccc5fcd1047e45e3d749e7ca19ea7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675748"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Agregar un menú de bot en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Para ayudarle en el descubrimiento y para ayudar a los usuarios a formar la funcionalidad del bot, ahora puede Agregar menús que se muestran cada vez que el usuario interactúa con el bot. El menú mostrará el texto del comando y también proporcionará texto de ayuda, como un ejemplo de uso o una descripción de la finalidad del comando.

![Captura de pantalla del menú de bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Cuando un usuario selecciona un elemento de menú, la cadena de comandos se inserta en el cuadro de texto para ayudar a completar el mensaje del bot.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Compatibilidad con menús de bot en la aplicación móvil de Microsoft Teams
> [!NOTE] 
> Los menús de bot no se muestran en dispositivos móviles

## <a name="app-manifest"></a>Manifiesto de la aplicación

Para crear un menú de bot, agregue un [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) nuevo objeto al manifiesto de la aplicación en la sección de bot. Puede declarar menús individuales con comandos separados para cada ámbito que admita el bot (`personal` `groupChat` o bien `team`) cada menú admite hasta 10 comandos.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Extracto de manifiesto-menú único para ambos ámbitos

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Menú independiente de fragmentos de manifiestos por ámbito

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

* Manténgase sencillo: el menú bot tiene como objetivo presentar las capacidades clave de su bot.
* Sea breve: las opciones de menú no deben ser muy largas y complejas con instrucciones de lenguaje natural, ya que deben ser comandos simples.
* Siempre disponible: las acciones o comandos del menú bot siempre deben invokablese, independientemente del estado de la conversación o el cuadro de diálogo en el que se encuentra el bot.
