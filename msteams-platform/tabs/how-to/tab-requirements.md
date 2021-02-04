---
title: Descripción de los requisitos de la pestaña
author: laujan
description: Todas las pestañas de Microsoft Teams deben cumplir estos requisitos.
keywords: Canal de grupo de pestañas de teams configurable
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1f5a3eaa8ca16878944288d5dbbfa78cfe9fa3ce
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797945"
---
# <a name="tab-requirements"></a><span data-ttu-id="1793c-104">Requisitos de pestaña</span><span class="sxs-lookup"><span data-stu-id="1793c-104">Tab requirements</span></span>

<span data-ttu-id="1793c-105">Las pestañas de Teams deben cumplir los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="1793c-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="1793c-106">Debes permitir que las páginas de pestaña se atenúen en un iFrame, a través de encabezados de respuesta HTTP X-Frame-Options o Content-Security-Policy.</span><span class="sxs-lookup"><span data-stu-id="1793c-106">You must allow your tab pages to be served in an iFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="1793c-107">Establecer encabezado: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="1793c-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="1793c-108">Para la compatibilidad con Internet Explorer 11, establece `X-Content-Security-Policy` también.</span><span class="sxs-lookup"><span data-stu-id="1793c-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>
  * <span data-ttu-id="1793c-109">Como alternativa, establezca el encabezado `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="1793c-109">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="1793c-110">Este encabezado está en desuso pero sigue siendo respetado por la mayoría de los exploradores.</span><span class="sxs-lookup"><span data-stu-id="1793c-110">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="1793c-111">Por lo general, como medida de seguridad contra el inicio de sesión de clics, las páginas de inicio de sesión no se representan en iFrames.</span><span class="sxs-lookup"><span data-stu-id="1793c-111">Typically, as a safeguard against click-jacking, login pages don't render in iFrames.</span></span> <span data-ttu-id="1793c-112">Por lo tanto, la lógica de autenticación debe usar un método que no sea el redireccionamiento (por ejemplo, usar autenticación basada en token o basada en cookies).</span><span class="sxs-lookup"><span data-stu-id="1793c-112">Therefore, your authentication logic needs to use a method other than redirect (e.g., use token-based or cookie-based authentication).</span></span>

> [!NOTE]
> <span data-ttu-id="1793c-113">Chrome 80, programado para su lanzamiento a principios de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1793c-113">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="1793c-114">Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador.</span><span class="sxs-lookup"><span data-stu-id="1793c-114">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="1793c-115">*Vea* [el atributo de cookie SameSite (actualización de 2020).](../../resources/samesite-cookie-update.md)</span><span class="sxs-lookup"><span data-stu-id="1793c-115">*See* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="1793c-116">Los exploradores se adhieren a una restricción de directiva del mismo origen que impide que una página web haga solicitudes a un dominio diferente del que atendía una página web.</span><span class="sxs-lookup"><span data-stu-id="1793c-116">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="1793c-117">Sin embargo, es posible que deba redirigir la página de configuración o contenido a otro dominio o subdominio.</span><span class="sxs-lookup"><span data-stu-id="1793c-117">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="1793c-118">La lógica de navegación entre dominios debe permitir que el cliente de Teams valide el origen con una lista validDomains estática en el manifiesto de la aplicación al cargar o comunicarse con la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1793c-118">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="1793c-119">Para crear una experiencia sin problemas, debe dar estilo a las pestañas según el tema, el diseño y la intención del cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="1793c-119">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="1793c-120">Normalmente, las pestañas funcionan mejor cuando se han creado para abordar una necesidad específica y centrarse en un pequeño conjunto de tareas o en un subconjunto de datos que sea relevante para la ubicación del canal de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1793c-120">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="1793c-121">En la página de contenido, agregue una referencia al SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client) de Microsoft Teams con etiquetas de script.</span><span class="sxs-lookup"><span data-stu-id="1793c-121">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="1793c-122">Después de cargar la página, realice una llamada a `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="1793c-122">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="1793c-123">La página no se mostrará si no lo hace.</span><span class="sxs-lookup"><span data-stu-id="1793c-123">Your page will not be displayed if you do not.</span></span>