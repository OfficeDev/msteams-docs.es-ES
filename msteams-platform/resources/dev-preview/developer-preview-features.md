---
title: Características de la versión preliminar de desarrolladores públicos
description: Detalles de las características de la versión Microsoft Teams public developer preview
ms.topic: reference
localization_priority: Normal
keywords: Características para desarrolladores de teams preview
ms.openlocfilehash: 84683420a5c61bb1eb493f8191bfbcbe97f6fb46
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230907"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="10f9e-104">Características en public developer preview for Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="10f9e-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="10f9e-105">Esta página estará en desuso en junio de 2021.</span><span class="sxs-lookup"><span data-stu-id="10f9e-105">This page will be deprecated in June 2021.</span></span> <span data-ttu-id="10f9e-106">Para obtener información sobre las características disponibles para la vista previa del desarrollador, consulta [¿Qué hay de nuevo?](~/whats-new.md)</span><span class="sxs-lookup"><span data-stu-id="10f9e-106">For information on features available for developer preview, see [What's new?](~/whats-new.md)</span></span>

<span data-ttu-id="10f9e-107">La vista previa del desarrollador incluye las siguientes características nuevas:</span><span class="sxs-lookup"><span data-stu-id="10f9e-107">The developer preview includes the following new features:</span></span>

## <a name="app-customization"></a><span data-ttu-id="10f9e-108">Personalización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="10f9e-108">App customization</span></span>

<span data-ttu-id="10f9e-109">Ahora puede definir un conjunto selecto de propiedades, que un administrador de Teams puede personalizar o cambiar la marca en función de las necesidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="10f9e-109">You can now define a select set of properties, which a Teams admin can customize or rebrand based on their organization's need.</span></span> <span data-ttu-id="10f9e-110">Para obtener más información, consulta [característica de personalización de aplicaciones](~/concepts/design/design-teams-app-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10f9e-110">For more information, see [app customization feature](~/concepts/design/design-teams-app-overview.md).</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="10f9e-111">Inicio de sesión único (SSO) de pestañas</span><span class="sxs-lookup"><span data-stu-id="10f9e-111">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="10f9e-112">Ahora puede usar el inicio de sesión único [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en escritorio y móvil mediante el SDK de JavaScript de Teams desde una página de contenido web.</span><span class="sxs-lookup"><span data-stu-id="10f9e-112">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="10f9e-113">Una de las ventajas es que un usuario nunca tiene que iniciar sesión; y una vez que han dado su consentimiento a la aplicación con su perfil: iniciarán sesión automáticamente en su pestaña (incluido el móvil).</span><span class="sxs-lookup"><span data-stu-id="10f9e-113">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="10f9e-114">Nuestra vista previa para desarrolladores está disponible en las versiones 1.5 y posteriores del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="10f9e-114">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="10f9e-115">Nuestra implementación actual solo puede obtener una cantidad limitada de API Graph, pero proporcionamos una solución alternativa para obtener api Graph con nuestra API de autenticación existente.</span><span class="sxs-lookup"><span data-stu-id="10f9e-115">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="10f9e-116">Llamadas y bots de reunión en línea</span><span class="sxs-lookup"><span data-stu-id="10f9e-116">Calls and online meeting bots</span></span>

<span data-ttu-id="10f9e-117">Con la adición de API [de Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)para llamadas y reuniones en línea, Microsoft Teams aplicaciones ahora pueden interactuar con los usuarios de formas enriquecciones mediante voz y vídeo.</span><span class="sxs-lookup"><span data-stu-id="10f9e-117">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="10f9e-118">Estas API te permiten agregar nuevas características de la aplicación, como la respuesta de voz interactiva (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.</span><span class="sxs-lookup"><span data-stu-id="10f9e-118">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="10f9e-119">Hemos agregado una nueva sección sobre cómo crear y desarrollar bots de llamadas y reuniones en línea, empezando por la [introducción](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10f9e-119">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>


## <a name="image-enlarge-support"></a><span data-ttu-id="10f9e-120">Compatibilidad con ampliación de imagen</span><span class="sxs-lookup"><span data-stu-id="10f9e-120">Image enlarge support</span></span>

<span data-ttu-id="10f9e-121">Ahora es posible que los bots indiquen qué imágenes compartidas en tarjetas adaptables en Teams pueden ampliarse.</span><span class="sxs-lookup"><span data-stu-id="10f9e-121">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="10f9e-122">Esto es útil para escenarios como compartir guías visuales detalladas paso a paso a través de bots que podrían ser difíciles de leer para los usuarios de lo contrario.</span><span class="sxs-lookup"><span data-stu-id="10f9e-122">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="10f9e-123">Para que una imagen se expanda, simplemente marcala `allowExpand: true` como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="10f9e-123">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="10f9e-124">Esto hará que Teams cliente web o de escritorio represente un elemento al pasar el mouse sobre la imagen para permitir que el usuario expanda la imagen.</span><span class="sxs-lookup"><span data-stu-id="10f9e-124">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>
