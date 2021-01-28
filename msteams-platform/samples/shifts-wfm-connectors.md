---
title: Conectores de turnos de Teams
description: Conectores de turnos de administración de recursos para Teams
ms.topic: reference
author: laujan
ms.date: 03/09/2020
keywords: Conectores de Microsoft Teams
ms.author: lajanuar
ms.openlocfilehash: 9d32c9e1aa3baba660440492df55bb00f677baa4
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014596"
---
# <a name="microsoft-teams-shifts-wfm-connectors"></a><span data-ttu-id="fbf9a-104">Microsoft Teams cambia los conectores WFM</span><span class="sxs-lookup"><span data-stu-id="fbf9a-104">Microsoft Teams Shifts WFM connectors</span></span>  

## <a name="workforce-management-connectors-wfm-for-firstline-workers"></a><span data-ttu-id="fbf9a-105">Conectores de administración de recursos (WFM) para trabajadores de primera línea</span><span class="sxs-lookup"><span data-stu-id="fbf9a-105">Workforce management connectors (WFM) for firstline workers</span></span> 

<span data-ttu-id="fbf9a-106">Los conectores WFM de turnos de Teams son integraciones preparadas para producción, de código abierto y controladas por la comunidad que ofrecen una experiencia sin problemas y un proceso rápido para la transformación digital de los trabajadores de primera línea con Teams Shifts.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-106">Teams Shifts WFM connectors are production-ready, open-source, and community-driven integrations that offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="fbf9a-107">Cada conector proporciona instrucciones detalladas para la implementación e integración en su organización.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="fbf9a-108">El código fuente completo está disponible en nuestro repositorio de GitHub, donde se puede explorar en detalle y/o bifurcarse y adaptarse para satisfacer sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-108">The complete source code is available in our GitHub repo where it can be explored in detail and/or forked and tailored to meet your specific needs.</span></span>

## <a name="key-benefits-teams-shifts-wfm-connectors"></a><span data-ttu-id="fbf9a-109">Ventajas clave: Teams cambia los conectores WFM</span><span class="sxs-lookup"><span data-stu-id="fbf9a-109">Key benefits: Teams Shifts WFM connectors</span></span>

* <span data-ttu-id="fbf9a-110">**Experiencia plug and play.**</span><span class="sxs-lookup"><span data-stu-id="fbf9a-110">**Plug and play experience.**</span></span> <span data-ttu-id="fbf9a-111">Todos los conectores de WFM de turnos ARM scripts de implementación de Azure que le permiten hospedar todos los servicios necesarios en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-111">All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="fbf9a-112">No se requiere codificación para implementar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-112">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="fbf9a-113">**Código listo para producción.**</span><span class="sxs-lookup"><span data-stu-id="fbf9a-113">**Production-ready code.**</span></span> <span data-ttu-id="fbf9a-114">Todos los conectores Shifts se ajustan a los procedimientos recomendados de seguridad e infraestructura y se revisan todos los cambios enviados por la comunidad para garantizar una conformidad continua.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-114">All  Shifts connectors conform to recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="fbf9a-115">**Personalizable y extensible.**</span><span class="sxs-lookup"><span data-stu-id="fbf9a-115">**Customizable and extensible.**</span></span> <span data-ttu-id="fbf9a-116"> Aunque todos los conectores de WFM de turnos están listos para implementarse para su uso inmediato, proporcionamos la base de código completa y los scripts de implementación para que pueda personalizarlos o ampliarlos fácilmente para adaptarlos a sus necesidades únicas.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-116"> While all Shifts WFM connectors are ready to deploy for immediate use, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="fbf9a-117">**Documentación detallada & soporte técnico.**</span><span class="sxs-lookup"><span data-stu-id="fbf9a-117">**Detailed documentation & support.**</span></span> <span data-ttu-id="fbf9a-118"> Todos los conectores de WFM de turnos van acompañados de documentación de un extremo a otro para los pasos de arquitectura, implementación y configuración de la solución.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-118"> All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="fbf9a-119">Los repositorios del conector se supervisan, así que informe de cualquier problema, desafío o dificultad que encuentre a través del rastreador de problemas de GitHub del repositorio.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-119">The connector repositories are monitored, so please report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="fbf9a-120">**Integración perfecta.**</span><span class="sxs-lookup"><span data-stu-id="fbf9a-120">**Seamless integration.**</span></span> <span data-ttu-id="fbf9a-121">La integración entre las soluciones WFM y Turnos de Teams permite a los trabajadores de primera línea usar la aplicación Turnos de Teams para ver/administrar sus horarios y horas de turnos, y usar todas las demás características de colaboración enriquez proporcionadas en Teams directamente desde su dispositivo móvil o escritorio sin tener que cambiar de contexto a otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-121">The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view/manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>

<span data-ttu-id="fbf9a-122">**Abrir la vista turnos en Teams**</span><span class="sxs-lookup"><span data-stu-id="fbf9a-122">**Open shifts view in Teams**</span></span>  
<span data-ttu-id="fbf9a-123">![Turnos abiertos en Teams](../assets/images/teams-open-shifts-view.png)</span><span class="sxs-lookup"><span data-stu-id="fbf9a-123">![Open shifts in Teams](../assets/images/teams-open-shifts-view.png)</span></span>

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="fbf9a-124">Conector de turnos de Kronos a Teams</span><span class="sxs-lookup"><span data-stu-id="fbf9a-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="fbf9a-125">Con el código de código abierto, puede integrar Kronos Workforce Central Versión 8.1 y posteriores, con Teams Shifts (aplicación de Teams de escritorio/móvil) para los siguientes escenarios de administrador y trabajo de primera línea:</span><span class="sxs-lookup"><span data-stu-id="fbf9a-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts (desktop/mobile Teams app) for the following firstline worker and manager scenarios:</span></span>

1. <span data-ttu-id="fbf9a-126">Ver programación.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-126">View schedule.</span></span>

1. <span data-ttu-id="fbf9a-127">Publicar y solicitar turnos abiertos.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-127">Publish and request open shifts.</span></span>

1. <span data-ttu-id="fbf9a-128">Turnos de intercambio.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-128">Swap shifts.</span></span>

1. <span data-ttu-id="fbf9a-129">Solicitar tiempo libre.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-129">Request time off.</span></span>

1. <span data-ttu-id="fbf9a-130">Ofrecer turnos.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-130">Offer shifts.</span></span>

[<span data-ttu-id="fbf9a-131">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="fbf9a-131">Get it on GitHub</span></span>]( https://aka.ms/KronosShiftsConnector)

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="fbf9a-132">Conector de turnos de JDA a Teams</span><span class="sxs-lookup"><span data-stu-id="fbf9a-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="fbf9a-133">Con el código de código abierto, puede integrar JDA (BlueYonder) versión 17.2 y versiones posteriores, con Teams Shifts (aplicación teams de escritorio/móvil) para los siguientes escenarios de administrador y trabajador de primera línea:</span><span class="sxs-lookup"><span data-stu-id="fbf9a-133">With open-source code, you can integrate JDA (BlueYonder) Version 17.2 and above, with Teams Shifts (desktop/mobile Teams app) for the following firstline worker and manager scenarios:</span></span>

1. <span data-ttu-id="fbf9a-134">Publicar turnos y programar grupos en JDA y ver en Teams.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-134">Publish shifts and schedule groups in JDA and view in Teams.</span></span>

1. <span data-ttu-id="fbf9a-135">Habilita escenarios de programación enriquecidos, incluida la solicitud de intercambios de turnos y el tiempo libre.</span><span class="sxs-lookup"><span data-stu-id="fbf9a-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

1. <span data-ttu-id="fbf9a-136">Establecer la disponibilidad del usuario mediante la [API de Microsoft Graph para turnos](/graph/api/resources/shift?view=graph-rest-beta) .</span><span class="sxs-lookup"><span data-stu-id="fbf9a-136">Set  user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta) .</span></span>

[<span data-ttu-id="fbf9a-137">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="fbf9a-137">Get it on GitHub</span></span>](https://aka.ms/JDAShiftsConnector)</br></br>
