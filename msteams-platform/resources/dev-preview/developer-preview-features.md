---
title: Características de la versión preliminar de desarrolladores públicos
description: Detalles de las características de Microsoft Teams Public Developer Preview
ms.topic: reference
keywords: Características para desarrolladores de teams preview
ms.openlocfilehash: 05954383931444cd0fb53dc37d9f790257f7dd39
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634519"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="46a22-104">Características de public developer preview para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="46a22-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="46a22-105">La vista previa del desarrollador incluye las siguientes características nuevas:</span><span class="sxs-lookup"><span data-stu-id="46a22-105">The developer preview includes the following new features:</span></span>

## <a name="app-customization"></a><span data-ttu-id="46a22-106">Personalización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="46a22-106">App customization</span></span>

<span data-ttu-id="46a22-107">Ahora puede definir un conjunto selecto de propiedades, que un administrador de Teams puede personalizar o cambiar de marca en función de las necesidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="46a22-107">You can now define a select set of properties, which a Teams admin can customize or rebrand based on their organization's need.</span></span> <span data-ttu-id="46a22-108">Para obtener más información, consulta [característica de personalización de aplicaciones](~/concepts/design/design-teams-app-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46a22-108">For more information, see [app customization feature](~/concepts/design/design-teams-app-overview.md).</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="46a22-109">Inicio de sesión único (SSO) de pestañas</span><span class="sxs-lookup"><span data-stu-id="46a22-109">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="46a22-110">Ahora puede usar el inicio de sesión único [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar un usuario en escritorio y móvil mediante el SDK de JavaScript de Teams desde una página de contenido web.</span><span class="sxs-lookup"><span data-stu-id="46a22-110">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="46a22-111">Una de las ventajas es que un usuario nunca tiene que iniciar sesión; y una vez que han dado su consentimiento a la aplicación con su perfil: iniciarán sesión automáticamente en su pestaña (incluido el móvil).</span><span class="sxs-lookup"><span data-stu-id="46a22-111">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="46a22-112">Nuestra vista previa para desarrolladores está disponible en las versiones 1.5 y posteriores del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="46a22-112">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="46a22-113">Nuestra implementación actual solo puede obtener una cantidad limitada de API de Graph, pero proporcionamos una solución alternativa para obtener API de Graph adicionales mediante nuestra API de autenticación existente.</span><span class="sxs-lookup"><span data-stu-id="46a22-113">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="46a22-114">Llamadas y bots de reunión en línea</span><span class="sxs-lookup"><span data-stu-id="46a22-114">Calls and online meeting bots</span></span>

<span data-ttu-id="46a22-115">Con la adición de API de [Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)para llamadas y reuniones en línea, las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecciones mediante voz y vídeo.</span><span class="sxs-lookup"><span data-stu-id="46a22-115">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="46a22-116">Estas API te permiten agregar nuevas características de la aplicación, como la respuesta de voz interactiva (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.</span><span class="sxs-lookup"><span data-stu-id="46a22-116">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="46a22-117">Hemos agregado una nueva sección sobre cómo crear y desarrollar bots de llamadas y reuniones en línea, empezando por la [introducción](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46a22-117">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>


## <a name="image-enlarge-support"></a><span data-ttu-id="46a22-118">Compatibilidad con ampliación de imagen</span><span class="sxs-lookup"><span data-stu-id="46a22-118">Image enlarge support</span></span>

<span data-ttu-id="46a22-119">Ahora es posible que los bots indiquen qué imágenes compartidas en tarjetas adaptables en Teams se pueden ampliar.</span><span class="sxs-lookup"><span data-stu-id="46a22-119">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="46a22-120">Esto es útil para escenarios como compartir guías visuales detalladas paso a paso a través de bots que podrían ser difíciles de leer para los usuarios de lo contrario.</span><span class="sxs-lookup"><span data-stu-id="46a22-120">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="46a22-121">Para que una imagen se expanda, simplemente marcala `allowExpand: true` como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="46a22-121">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="46a22-122">Esto hará que el cliente web o de escritorio de Teams represente un elemento al pasar el puntero sobre la imagen para permitir que el usuario expanda la imagen.</span><span class="sxs-lookup"><span data-stu-id="46a22-122">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

