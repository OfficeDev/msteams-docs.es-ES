---
title: Habilitar la aplicación para personalizarla
author: heath-hamilton
description: Comprender cómo Teams los administradores pueden personalizar la aplicación para su organización.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: bf1b43629c87dd4123520c634772e5dea14e0bb5
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915086"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a><span data-ttu-id="ffc0a-103">Habilitar la aplicación Microsoft Teams personalizada</span><span class="sxs-lookup"><span data-stu-id="ffc0a-103">Enable your Microsoft Teams app to be customized</span></span>

<span data-ttu-id="ffc0a-104">Puedes permitir a los clientes personalizar algunos aspectos de la aplicación Microsoft Teams en el centro Teams administración.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-104">You can allow customers to customize some aspects of your Microsoft Teams app in the Teams admin center.</span></span> <span data-ttu-id="ffc0a-105">Esta característica solo es compatible con las aplicaciones publicadas en la Teams tienda.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-105">This feature is supported only for apps published to the Teams store.</span></span> <span data-ttu-id="ffc0a-106">Las aplicaciones y aplicaciones de instalación local publicadas para una organización no se pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-106">Sideloaded apps and apps published for an org can't be customized.</span></span>

<span data-ttu-id="ffc0a-107">Algunos ejemplos posibles de esta característica incluyen:</span><span class="sxs-lookup"><span data-stu-id="ffc0a-107">Some possible examples of this feature include:</span></span>

* <span data-ttu-id="ffc0a-108">Cambiar el color de acento de la aplicación para que coincida con la marca de una organización.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-108">Changing the app's accent color to match an org's brand.</span></span>
* <span data-ttu-id="ffc0a-109">Actualizar el nombre de la aplicación de *Contoso* al *agente contoso*, que es el nombre que verán los usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-109">Updating the app name from *Contoso* to *Contoso Agent*, which is the name users in the org will see.</span></span> <span data-ttu-id="ffc0a-110">(Nota: Los usuarios que agreguen un conector a un chat o un canal seguirán ven el nombre de la aplicación original, *Contoso*.)</span><span class="sxs-lookup"><span data-stu-id="ffc0a-110">(Note: Users adding a connector to a chat or a channel will still see the original app name, *Contoso*.)</span></span>

<span data-ttu-id="ffc0a-111">Puede habilitar esta característica en el Portal de [desarrolladores para Teams](https://dev.teams.microsoft.com/home).</span><span class="sxs-lookup"><span data-stu-id="ffc0a-111">You can enable this feature in the [Developer Portal for Teams](https://dev.teams.microsoft.com/home).</span></span> <span data-ttu-id="ffc0a-112">Esto configura , que no están disponibles en versiones anteriores a `configurableProperties` la 1.10 del manifiesto Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-112">This configures `configurableProperties`, which aren't available in versions prior to 1.10 of the Teams app manifest.</span></span>

## <a name="test-your-app"></a><span data-ttu-id="ffc0a-113">Probar la aplicación</span><span class="sxs-lookup"><span data-stu-id="ffc0a-113">Test your app</span></span>

<span data-ttu-id="ffc0a-114">No puede probar esta característica durante el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-114">You cannot test this feature during development.</span></span> <span data-ttu-id="ffc0a-115">La personalización de aplicaciones no se admite para la instalación local o la publicación en el catálogo de aplicaciones de una organización.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-115">App customization is not supported for sideloading or publishing to an organization's app catalog.</span></span>

## <a name="user-considerations"></a><span data-ttu-id="ffc0a-116">Consideraciones del usuario</span><span class="sxs-lookup"><span data-stu-id="ffc0a-116">User considerations</span></span>

<span data-ttu-id="ffc0a-117">Como editor de aplicaciones, proporcione la siguiente información a los clientes de Teams administradores:</span><span class="sxs-lookup"><span data-stu-id="ffc0a-117">As the app publisher, provide the following information to customers in Teams admins:</span></span>
* <span data-ttu-id="ffc0a-118">Incluya una nota que recomiende probar los cambios de personalización en Teams inquilino de prueba antes de realizar cambios en su entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-118">Include a note recommending to test customization changes in a Teams test tenant before making changes in their production environment.</span></span> 
* <span data-ttu-id="ffc0a-119">Proporciona procedimientos recomendados para personalizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ffc0a-119">Provide best practices for how to customize your app.</span></span>

## <a name="see-also"></a><span data-ttu-id="ffc0a-120">Ver también</span><span class="sxs-lookup"><span data-stu-id="ffc0a-120">See also</span></span>

* [<span data-ttu-id="ffc0a-121">Personalizar aplicaciones en el Centro Teams administración</span><span class="sxs-lookup"><span data-stu-id="ffc0a-121">Customize apps in the Teams admin center</span></span>](/MicrosoftTeams/customize-apps)
