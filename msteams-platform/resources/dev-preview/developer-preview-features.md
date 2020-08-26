---
title: Características de la versión preliminar para desarrolladores públicos
description: Detalla las características de la vista previa de Microsoft Teams para desarrolladores públicos
keywords: características para desarrolladores de Team Preview
ms.openlocfilehash: 773e0334bddf45b7b86d31329b99607f3b70c534
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874845"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="06394-104">Características de la versión preliminar para desarrolladores públicos para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="06394-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="06394-105">La vista previa para desarrolladores incluye las siguientes características nuevas:</span><span class="sxs-lookup"><span data-stu-id="06394-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="06394-106">Inicio de sesión único (SSO) de pestañas</span><span class="sxs-lookup"><span data-stu-id="06394-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="06394-107">Ahora puede usar el inicio [de sesión único (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en el escritorio y en el móvil mediante el SDK de Teams para JavaScript desde una página de contenido Web.</span><span class="sxs-lookup"><span data-stu-id="06394-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="06394-108">Una de las ventajas es que un usuario nunca tiene que iniciar sesión; una vez que hayan dado su consentimiento a la aplicación mediante su perfil: se iniciará sesión automáticamente en su pestaña (incluido el móvil).</span><span class="sxs-lookup"><span data-stu-id="06394-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="06394-109">Nuestra vista previa para desarrolladores está disponible en las versiones 1,5 y posteriores del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="06394-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="06394-110">Nuestra implementación actual solo puede obtener una cantidad limitada de API de Graph, pero proporcionamos una solución alternativa para obtener más API de Graph con nuestra API de autenticación existente.</span><span class="sxs-lookup"><span data-stu-id="06394-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="06394-111">Llamadas y bots de reuniones en línea</span><span class="sxs-lookup"><span data-stu-id="06394-111">Calls and online meeting bots</span></span>

<span data-ttu-id="06394-112">Con la adición de las [API de Microsoft Graph para las llamadas y las reuniones en línea](/graph/api/resources/communications-api-overview?view=graph-rest-beta), las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecidas mediante voz y vídeo.</span><span class="sxs-lookup"><span data-stu-id="06394-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="06394-113">Estas API le permiten agregar nuevas características de aplicación, como la respuesta interactiva de voz (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.</span><span class="sxs-lookup"><span data-stu-id="06394-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="06394-114">Hemos agregado una nueva sección sobre cómo crear y desarrollar llamadas y los bots de reuniones en línea, comenzando por la [información general](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06394-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="06394-115">Compatibilidad con Image ampliado</span><span class="sxs-lookup"><span data-stu-id="06394-115">Image enlarge support</span></span>

<span data-ttu-id="06394-116">Ahora es posible que los bots indiquen qué imágenes compartidas en las tarjetas adaptables de Teams se pueden ampliar.</span><span class="sxs-lookup"><span data-stu-id="06394-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="06394-117">Esto es útil para escenarios como compartir guías visuales paso a paso a través de bots que podrían resultar difíciles de leer para los usuarios en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="06394-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="06394-118">Para hacer que una imagen sea expansible, simplemente debe marcarla `allowExpand: true` como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="06394-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="06394-119">Esto provocará que el cliente web/de escritorio de Microsoft Teams represente un elemento al pasar sobre la imagen para permitir que el usuario expanda la imagen.</span><span class="sxs-lookup"><span data-stu-id="06394-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

