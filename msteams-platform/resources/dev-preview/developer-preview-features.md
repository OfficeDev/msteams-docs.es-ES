---
title: Características de la versión preliminar pública para desarrolladores
description: Detalles de las características de la versión preliminar para desarrolladores públicos de Microsoft Teams
ms.topic: reference
keywords: Características para desarrolladores de vista previa de teams
ms.openlocfilehash: 3275ef7ac0d4ba052f417f6e852f48e2fdf267f5
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014358"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="8e81f-104">Características de la versión preliminar para desarrolladores públicos de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8e81f-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="8e81f-105">La vista previa del desarrollador incluye las siguientes características nuevas:</span><span class="sxs-lookup"><span data-stu-id="8e81f-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="8e81f-106">Inicio de sesión único (SSO) de pestañas</span><span class="sxs-lookup"><span data-stu-id="8e81f-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="8e81f-107">Ahora puede usar el inicio de sesión único [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en dispositivos móviles y de escritorio con el SDK de JavaScript de Teams desde una página de contenido web.</span><span class="sxs-lookup"><span data-stu-id="8e81f-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="8e81f-108">Una de las ventajas es que un usuario nunca tiene que iniciar sesión; y una vez que haya dado su consentimiento a la aplicación con su perfil: iniciará sesión automáticamente en su pestaña (incluido el móvil).</span><span class="sxs-lookup"><span data-stu-id="8e81f-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="8e81f-109">Nuestra versión preliminar para desarrolladores está disponible en las versiones de manifiesto 1.5 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="8e81f-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="8e81f-110">Nuestra implementación actual solo puede obtener una cantidad limitada de API de Graph, pero proporcionamos una solución alternativa para obtener API de Graph adicionales mediante nuestra API de autenticación existente.</span><span class="sxs-lookup"><span data-stu-id="8e81f-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="8e81f-111">Bots de llamadas y reuniones en línea</span><span class="sxs-lookup"><span data-stu-id="8e81f-111">Calls and online meeting bots</span></span>

<span data-ttu-id="8e81f-112">Con la adición de las API de [Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta)para llamadas y reuniones en línea, las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecciones mediante voz y vídeo.</span><span class="sxs-lookup"><span data-stu-id="8e81f-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="8e81f-113">Estas API le permiten agregar nuevas características de la aplicación, como la respuesta interactiva de voz (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.</span><span class="sxs-lookup"><span data-stu-id="8e81f-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="8e81f-114">Hemos agregado una nueva sección sobre cómo crear y desarrollar bots de llamadas y reuniones en línea, empezando por la [introducción.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8e81f-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="8e81f-115">Compatibilidad con ampliación de imagen</span><span class="sxs-lookup"><span data-stu-id="8e81f-115">Image enlarge support</span></span>

<span data-ttu-id="8e81f-116">Ahora es posible que los bots indiquen qué imágenes compartidas en tarjetas adaptables en Teams se pueden ampliar.</span><span class="sxs-lookup"><span data-stu-id="8e81f-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="8e81f-117">Esto es útil para escenarios como compartir guías visuales detalladas paso a paso a través de bots que podrían resultar difíciles de leer para los usuarios de lo contrario.</span><span class="sxs-lookup"><span data-stu-id="8e81f-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="8e81f-118">Para que una imagen se expanda, solo tienes que `allowExpand: true` marcarla como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="8e81f-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="8e81f-119">Esto hará que el cliente web o de escritorio de Teams represente un elemento al pasar sobre la imagen para permitir al usuario expandir la imagen.</span><span class="sxs-lookup"><span data-stu-id="8e81f-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

