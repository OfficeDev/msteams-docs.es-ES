---
title: Reordenar pestañas de aplicaciones personales
description: Cómo cambiar el orden de las pestañas estáticas de la aplicación personal en su aplicación personal
keywords: desarrollo de pestañas de Microsoft Teams
ms.openlocfilehash: a8a7c3d23bac98ef1085a8f3443ca0fc92ae0a31
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "49554832"
---
# <a name="reorder-personal-app-tabs"></a><span data-ttu-id="d14d5-104">Reordenar pestañas de aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="d14d5-104">Reorder personal app tabs</span></span>

<span data-ttu-id="d14d5-105">A partir de la versión del manifiesto 1,7, los desarrolladores pueden reorganizar todas las pestañas en su aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="d14d5-105">Starting with manifest version 1.7 developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="d14d5-106">En concreto, un desarrollador puede mover la pestaña "chat de bot" (que siempre tiene el valor predeterminado a la primera posición) en cualquier lugar del encabezado de la pestaña de la aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="d14d5-106">In particular, a developer can move the “bot chat” tab (which has always defaulted to the first position) anywhere in the personal app tab header.</span></span> <span data-ttu-id="d14d5-107">Hemos declarado dos palabras clave de entityId de pestaña reservadas: "Conversations" y "About".</span><span class="sxs-lookup"><span data-stu-id="d14d5-107">We’ve declared two reserved tab entityId keywords: “conversations” and “about”.</span></span>

## <a name="moving-the-chatconversation-tab"></a><span data-ttu-id="d14d5-108">Mover la pestaña "chat/conversación"</span><span class="sxs-lookup"><span data-stu-id="d14d5-108">Moving the “Chat/Conversation” tab</span></span>

<span data-ttu-id="d14d5-109">Si crea un bot con un ámbito "personal", se mostrará siempre en la primera tabulación de una aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="d14d5-109">If you create a bot with a “personal” scope, it will always show up in the first tab position in a personal app.</span></span> <span data-ttu-id="d14d5-110">Si desea moverla a otro lugar, debe agregar un objeto de pestaña estático al manifiesto con la palabra clave reservada "conversaciones".</span><span class="sxs-lookup"><span data-stu-id="d14d5-110">If you wish to move it to another position, you need to add a static tab object to your manifest with the reserved keyword “conversations”.</span></span> <span data-ttu-id="d14d5-111">Siempre que agregue la pestaña "conversaciones" en la matriz "staticTabs", aquí es donde aparecerá la ficha conversación en el escritorio y en la Web.</span><span class="sxs-lookup"><span data-stu-id="d14d5-111">Wherever you add the “conversations” tab in the “staticTabs” array, that’s where the conversation tab will appear on web and desktop.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

> [!NOTE]
> <span data-ttu-id="d14d5-112">Tenga en cuenta que este comportamiento no se ve reflejado en dispositivos móviles, ya que el chat de bot personal ya tiene un lugar dedicado dentro de la aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="d14d5-112">Note that this behavior is not reflected on mobile since the personal bot chat already has a dedicated place within the personal app.</span></span>

## <a name="moving-the-about-tab"></a><span data-ttu-id="d14d5-113">Mover la pestaña "acerca de"</span><span class="sxs-lookup"><span data-stu-id="d14d5-113">Moving the “About” tab</span></span>

<span data-ttu-id="d14d5-114">La pestaña "acerca de" siempre es el final de la barra de encabezado de la pestaña de la aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="d14d5-114">The “About” tab always defaults to the end of the personal app tab header bar.</span></span> <span data-ttu-id="d14d5-115">Si desea moverla a otra posición, debe usar la "acerca de" entityId.</span><span class="sxs-lookup"><span data-stu-id="d14d5-115">If you wish to move it to another position, you need to use the “about” entityId.</span></span>

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
> [!NOTE]
> <span data-ttu-id="d14d5-116">Tenga en cuenta que la pestaña acerca de no se muestra en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="d14d5-116">Note that the about tab is not shown on mobile.</span></span>

## <a name="example-code"></a><span data-ttu-id="d14d5-117">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d14d5-117">Example code</span></span>

```json
{
   "staticTabs":[
      {
         "entityId":"homeTab",
         "name":"Home",
         "contentUrl":"https://www.contoso.com",
         "websiteUrl":" https://www.contoso.com ",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
