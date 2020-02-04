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
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="f7cdf-104">Agregar un menú de bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f7cdf-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f7cdf-105">Para ayudarle en el descubrimiento y para ayudar a los usuarios a formar la funcionalidad del bot, ahora puede Agregar menús que se muestran cada vez que el usuario interactúa con el bot.</span><span class="sxs-lookup"><span data-stu-id="f7cdf-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="f7cdf-106">El menú mostrará el texto del comando y también proporcionará texto de ayuda, como un ejemplo de uso o una descripción de la finalidad del comando.</span><span class="sxs-lookup"><span data-stu-id="f7cdf-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![Captura de pantalla del menú de bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="f7cdf-108">Cuando un usuario selecciona un elemento de menú, la cadena de comandos se inserta en el cuadro de texto para ayudar a completar el mensaje del bot.</span><span class="sxs-lookup"><span data-stu-id="f7cdf-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="f7cdf-109">Compatibilidad con menús de bot en la aplicación móvil de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f7cdf-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="f7cdf-110">Los menús de bot no se muestran en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="f7cdf-110">Bot menus are not displayed on mobile devices</span></span>

## <a name="app-manifest"></a><span data-ttu-id="f7cdf-111">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f7cdf-111">App manifest</span></span>

<span data-ttu-id="f7cdf-112">Para crear un menú de bot, agregue un [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) nuevo objeto al manifiesto de la aplicación en la sección de bot.</span><span class="sxs-lookup"><span data-stu-id="f7cdf-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="f7cdf-113">Puede declarar menús individuales con comandos separados para cada ámbito que admita el bot (`personal` `groupChat` o bien `team`) cada menú admite hasta 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="f7cdf-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat` or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="f7cdf-114">Extracto de manifiesto-menú único para ambos ámbitos</span><span class="sxs-lookup"><span data-stu-id="f7cdf-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="f7cdf-115">Menú independiente de fragmentos de manifiestos por ámbito</span><span class="sxs-lookup"><span data-stu-id="f7cdf-115">Manifest excerpt - separate menu per scope</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="f7cdf-116">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="f7cdf-116">Best practices</span></span>

* <span data-ttu-id="f7cdf-117">Manténgase sencillo: el menú bot tiene como objetivo presentar las capacidades clave de su bot.</span><span class="sxs-lookup"><span data-stu-id="f7cdf-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="f7cdf-118">Sea breve: las opciones de menú no deben ser muy largas y complejas con instrucciones de lenguaje natural, ya que deben ser comandos simples.</span><span class="sxs-lookup"><span data-stu-id="f7cdf-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="f7cdf-119">Siempre disponible: las acciones o comandos del menú bot siempre deben invokablese, independientemente del estado de la conversación o el cuadro de diálogo en el que se encuentra el bot.</span><span class="sxs-lookup"><span data-stu-id="f7cdf-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
