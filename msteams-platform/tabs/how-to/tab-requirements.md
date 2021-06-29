---
title: Requisitos previos
author: surbhigupta
description: Todas las pestañas Microsoft Teams deben cumplir estos requisitos.
keywords: Canal de grupo de pestañas de teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8566bb0457db76e4639593dcd67a0442749c0a31
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179940"
---
# <a name="prerequisites"></a><span data-ttu-id="e4cd3-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e4cd3-104">Prerequisites</span></span>

<span data-ttu-id="e4cd3-105">Teams pestañas deben cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="e4cd3-105">Teams tabs must adhere to the following prerequisites:</span></span>

* <span data-ttu-id="e4cd3-106">Debe permitir que las páginas de pestañas se muestran en un iFrame, con encabezados de respuesta HTTP X-Frame-Options y Content-Security-Policy.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-106">You must allow your tab pages to be shown in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="e4cd3-107">Establecer encabezado: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="e4cd3-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="e4cd3-108">Para la compatibilidad con Internet Explorer 11, establezca `X-Content-Security-Policy` .</span><span class="sxs-lookup"><span data-stu-id="e4cd3-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="e4cd3-109">Como alternativa, establezca el encabezado `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="e4cd3-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="e4cd3-110">Este encabezado está en desuso pero sigue siendo aceptado por la mayoría de los exploradores.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-110">This header is deprecated but still accepted by most browsers.</span></span>

* <span data-ttu-id="e4cd3-111">Normalmente, como medida de protección contra el robo de clics, las páginas de inicio de sesión no se representan en iFrames.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-111">Typically, as a safeguard against clickjacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="e4cd3-112">La lógica de autenticación debe usar un método que no sea el redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="e4cd3-113">Por ejemplo, use la autenticación basada en token o basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e4cd3-114">Chrome 80, programado para su lanzamiento a principios de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="e4cd3-115">Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="e4cd3-116">Para obtener más información, vea [SameSite cookie attribute](../../resources/samesite-cookie-update.md).</span><span class="sxs-lookup"><span data-stu-id="e4cd3-116">For more information, see [SameSite cookie attribute](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="e4cd3-117">Los exploradores cumplen una restricción de directiva del mismo origen.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-117">Browsers adhere to a same-origin policy restriction.</span></span> <span data-ttu-id="e4cd3-118">Impide que las páginas web soliciten dominios distintos de la página web servida.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-118">It prevents webpages from making requests to different domains than the served web page.</span></span> <span data-ttu-id="e4cd3-119">Sin embargo, puede redirigir la página de configuración o contenido a otro dominio o subdominio.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-119">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="e4cd3-120">La lógica de navegación entre dominios debe permitir que el cliente de Teams valide el origen con una lista estática en el manifiesto de la aplicación al cargar o comunicarse `validDomains` con la pestaña.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-120">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static `validDomains` list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="e4cd3-121">Debe dar estilo a las pestañas en función Teams el tema, el diseño y la intención del cliente.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-121">You must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="e4cd3-122">Normalmente, las pestañas funcionan mejor cuando se construyen para abordar una necesidad específica y centrarse en un pequeño conjunto de tareas o un subconjunto de datos que es relevante para la ubicación del canal de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-122">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="e4cd3-123">En la página de contenido, agregue una referencia a Microsoft Teams SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client) mediante etiquetas de script.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-123">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="e4cd3-124">Después de que se cargue la página, realice una llamada a , de lo `microsoftTeams.initialize()` contrario, no se mostrará la página.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-124">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="e4cd3-125">Para que la autenticación funcione en clientes móviles, debe actualizar Teams SDK de JavaScript a al menos la versión 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-125">For authentication to work on mobile clients, you must upgrade Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="e4cd3-126">Si decide que la pestaña canal o grupo aparezca en Teams móviles, la configuración debe tener un `setSettings()` valor para la `websiteUrl` propiedad.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="e4cd3-127">La pestaña Teams MS no admite la capacidad de cargar sitios web de intranet que usan certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="e4cd3-127">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="see-also"></a><span data-ttu-id="e4cd3-128">Vea también</span><span class="sxs-lookup"><span data-stu-id="e4cd3-128">See also</span></span>

* [<span data-ttu-id="e4cd3-129">Teams pestañas</span><span class="sxs-lookup"><span data-stu-id="e4cd3-129">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="e4cd3-130">Crear una pestaña de canal o grupo</span><span class="sxs-lookup"><span data-stu-id="e4cd3-130">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="e4cd3-131">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="e4cd3-131">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="e4cd3-132">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="e4cd3-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4cd3-133">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="e4cd3-133">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
