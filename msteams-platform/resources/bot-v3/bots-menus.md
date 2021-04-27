---
title: Agregar un menú bot
description: Describe cómo crear menús para bots en Microsoft Teams
keywords: creación de menús de bots de teams
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: f4190d0b21abbe00994e082000202b7bc65b917c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019772"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="8e694-104">Agregar un menú bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8e694-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="8e694-105">Para ayudar a la detección y ayudar a educar a los usuarios sobre la funcionalidad del bot, ahora puedes agregar menús que superen cada vez que el usuario interactúe con el bot.</span><span class="sxs-lookup"><span data-stu-id="8e694-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="8e694-106">El menú mostrará el texto del comando y también proporcionará texto de ayuda, como un ejemplo de uso o una descripción del propósito del comando.</span><span class="sxs-lookup"><span data-stu-id="8e694-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![Captura de pantalla del menú bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="8e694-108">Cuando un usuario selecciona un elemento de menú, la cadena de comandos se inserta en el cuadro de texto para ayudar al usuario a completar el mensaje del bot.</span><span class="sxs-lookup"><span data-stu-id="8e694-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="8e694-109">Compatibilidad con menú bot en la aplicación móvil de Teams</span><span class="sxs-lookup"><span data-stu-id="8e694-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="8e694-110">Los menús del bot no se muestran en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="8e694-110">Bot menus are not displayed on mobile devices</span></span>

## <a name="app-manifest"></a><span data-ttu-id="8e694-111">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8e694-111">App manifest</span></span>

<span data-ttu-id="8e694-112">Para crear un menú bot, agrega un nuevo objeto al manifiesto [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) de la aplicación en la sección bot.</span><span class="sxs-lookup"><span data-stu-id="8e694-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="8e694-113">Puede declarar menús individuales con comandos independientes para cada ámbito que el bot admite ( , o ) Cada menú admite hasta `personal` `groupChat` `team` 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="8e694-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat` or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="8e694-114">Extracto de manifiesto: menú único para ambos ámbitos</span><span class="sxs-lookup"><span data-stu-id="8e694-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="8e694-115">Extracto de manifiesto: menú independiente por ámbito</span><span class="sxs-lookup"><span data-stu-id="8e694-115">Manifest excerpt - separate menu per scope</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="8e694-116">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="8e694-116">Best practices</span></span>

* <span data-ttu-id="8e694-117">Mantenlo sencillo: el menú del bot está diseñado para presentar las funciones clave del bot.</span><span class="sxs-lookup"><span data-stu-id="8e694-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="8e694-118">Tenga en cuenta que las opciones de menú no deben ser instrucciones de lenguaje natural extremadamente largas y complejas; deben ser comandos simples.</span><span class="sxs-lookup"><span data-stu-id="8e694-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="8e694-119">Siempre disponible: las acciones o comandos del menú Bot deben ser siempre invokables, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.</span><span class="sxs-lookup"><span data-stu-id="8e694-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
