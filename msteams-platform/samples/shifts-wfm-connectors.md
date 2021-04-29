---
title: Conectores de turnos listos para producción
description: Conectores de turnos de administración de personal para Teams
ms.topic: reference
author: laujan
ms.date: 03/09/2020
localization_priority: Normal
keywords: Kronos de conectores de Microsoft Teams
ms.author: lajanuar
ms.openlocfilehash: 459797dd3f8425223c0dcbedc335955bf106ae37
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075741"
---
# <a name="production-ready-shifts-connectors"></a><span data-ttu-id="ba591-104">Conectores de turnos listos para producción</span><span class="sxs-lookup"><span data-stu-id="ba591-104">Production-ready Shifts Connectors</span></span>  

<span data-ttu-id="ba591-105">Los conectores de administración de fuerza de trabajo (WFM) de Teams Shifts son integraciones basadas en la comunidad, listas para producción y de código abierto, útiles para los trabajadores de primera línea.</span><span class="sxs-lookup"><span data-stu-id="ba591-105">Teams Shifts Workforce management (WFM) connectors are production-ready, open-source, and community-driven integrations, useful for firstline workers.</span></span> <span data-ttu-id="ba591-106">Ofrecen una experiencia perfecta y un proceso rápido para la transformación digital de los trabajadores de primera línea con Teams Shifts.</span><span class="sxs-lookup"><span data-stu-id="ba591-106">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="ba591-107">Cada conector proporciona instrucciones detalladas para la implementación e integración en la organización.</span><span class="sxs-lookup"><span data-stu-id="ba591-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="ba591-108">El código fuente completo está disponible en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="ba591-108">The complete source code is available in GitHub repository.</span></span> <span data-ttu-id="ba591-109">Puede explorar en detalle o bifurcar, y personalizar para satisfacer sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="ba591-109">You can explore in detail or fork, and customize to meet your specific needs.</span></span>   

<span data-ttu-id="ba591-110">En este documento se ofrece información general sobre las principales ventajas de los conectores WFM de Turnos de Teams, el conector de turnos de Kronos a Teams y el conector de turnos de JDA a Teams.</span><span class="sxs-lookup"><span data-stu-id="ba591-110">This document gives an overview of key benefits of Teams Shifts WFM connectors, Kronos-to-Teams Shifts connector, and JDA-to-Teams Shifts connector.</span></span>

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a><span data-ttu-id="ba591-111">Ventajas clave de los conectores WFM de Teams Shifts</span><span class="sxs-lookup"><span data-stu-id="ba591-111">Key benefits of Teams Shifts WFM connectors</span></span>

<span data-ttu-id="ba591-112">A continuación se desconocien las principales ventajas de los conectores WFM de Teams Shifts:</span><span class="sxs-lookup"><span data-stu-id="ba591-112">Following are the key benefits of Teams Shifts WFM connectors:</span></span>

* <span data-ttu-id="ba591-113">**Experiencia de plug and play:** Todos los conectores WFM de shifts incluyen ARM scripts de implementación de Azure que le permiten hospedar todos los servicios necesarios en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ba591-113">**Plug and play experience:** All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="ba591-114">No se requiere codificación para implementar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ba591-114">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="ba591-115">**Código listo para producción:** Todos los conectores Shifts se ajustan a los procedimientos recomendados de seguridad e infraestructura y se revisan todos los cambios enviados por la comunidad para garantizar la conformidad continua.</span><span class="sxs-lookup"><span data-stu-id="ba591-115">**Production-ready code:** All  Shifts connectors conform to the recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="ba591-116">**Personalizable y extensible:**   Mientras que todos los conectores DE WFM de turnos están listos para implementarse para su uso inmediato, con la base de código completa y los scripts de implementación disponibles.</span><span class="sxs-lookup"><span data-stu-id="ba591-116">**Customizable and extensible:**  While all Shifts WFM connectors are ready to deploy for immediate use, with the entire code base and deployment scripts readily available.</span></span> <span data-ttu-id="ba591-117">Puede personalizarlos o ampliarlos fácilmente para que se ajusten a sus necesidades únicas.</span><span class="sxs-lookup"><span data-stu-id="ba591-117">You can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="ba591-118">**Documentación detallada & soporte técnico:**   Todos los conectores DE WFM de turnos se acompañan de documentación completa para los pasos de configuración, implementación y arquitectura de soluciones.</span><span class="sxs-lookup"><span data-stu-id="ba591-118">**Detailed documentation & support:**  All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="ba591-119">Los repositorios del conector se supervisan, de modo que pueda informar de los problemas, desafíos o dificultades que encuentre a través del rastreador de problemas de GitHub del repositorio.</span><span class="sxs-lookup"><span data-stu-id="ba591-119">The connector repositories are monitored, so that you can report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="ba591-120">**Integración perfecta:** La integración entre las soluciones WFM y Teams Shifts permite a los trabajadores de primera línea usar la aplicación Teams Shifts para ver o administrar sus horarios y turnos de trabajo, y usar todas las demás características de colaboración enriquecciones proporcionadas en Teams directamente desde su dispositivo móvil o escritorio sin tener que cambiar el contexto a otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="ba591-120">**Seamless integration:** The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view or manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>  

<span data-ttu-id="ba591-121">**Vista Abrir turnos en Teams**</span><span class="sxs-lookup"><span data-stu-id="ba591-121">**Open shifts view in Teams**</span></span> 

<span data-ttu-id="ba591-122">La vista turnos de Teams se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="ba591-122">The shifts view in Teams is shown in the following image:</span></span> 

![Turnos abiertos en Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="ba591-124">Conector de cambios de Kronos a Teams</span><span class="sxs-lookup"><span data-stu-id="ba591-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="ba591-125">Con el código de código abierto, puedes integrar Kronos Workforce Central Versión 8.1 y versiones posteriores, con cambios de Teams como, aplicaciones de escritorio o móviles de Teams para los siguientes escenarios de administrador y trabajador de primera línea:</span><span class="sxs-lookup"><span data-stu-id="ba591-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="ba591-126">Ver programación.</span><span class="sxs-lookup"><span data-stu-id="ba591-126">View schedule.</span></span>

* <span data-ttu-id="ba591-127">Publicar y solicitar turnos abiertos.</span><span class="sxs-lookup"><span data-stu-id="ba591-127">Publish and request open shifts.</span></span>

* <span data-ttu-id="ba591-128">Turnos de intercambio.</span><span class="sxs-lookup"><span data-stu-id="ba591-128">Swap shifts.</span></span>

* <span data-ttu-id="ba591-129">Solicitar tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="ba591-129">Request time off.</span></span>

* <span data-ttu-id="ba591-130">Turnos de oferta.</span><span class="sxs-lookup"><span data-stu-id="ba591-130">Offer shifts.</span></span>

<span data-ttu-id="ba591-131">Para obtener más información sobre la implementación del conector de cambios de Kronos a Teams, consulte [Get it on GitHub](https://aka.ms/KronosShiftsConnector).</span><span class="sxs-lookup"><span data-stu-id="ba591-131">For more information on deployment of Kronos-to-Teams Shifts connector, see [Get it on GitHub](https://aka.ms/KronosShiftsConnector).</span></span>

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="ba591-132">Conector de turnos de JDA a Teams</span><span class="sxs-lookup"><span data-stu-id="ba591-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="ba591-133">Con el código de código abierto, puedes integrar JDA, como BlueYonder versión 17.2 y versiones posteriores, con cambios de Teams como, aplicaciones de teams móviles o de escritorio para los siguientes escenarios de administrador y trabajador de primera línea:</span><span class="sxs-lookup"><span data-stu-id="ba591-133">With open-source code, you can integrate JDA, such as BlueYonder Version 17.2 and above, with Teams Shifts  such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="ba591-134">Publicar turnos y programar grupos en JDA y verlos en Teams.</span><span class="sxs-lookup"><span data-stu-id="ba591-134">Publish shifts and schedule groups in JDA and view them in Teams.</span></span>

* <span data-ttu-id="ba591-135">Habilitar escenarios de programación enriquecidos, incluida la solicitud de intercambios de turnos y el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="ba591-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

* <span data-ttu-id="ba591-136">Establecer la disponibilidad del usuario mediante la [API de Microsoft Graph para turnos](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ba591-136">Set user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).</span></span>

<span data-ttu-id="ba591-137">Para obtener más información sobre la contribución y la sugerencia, vea [Get it on GitHub](https://aka.ms/JDAShiftsConnector).</span><span class="sxs-lookup"><span data-stu-id="ba591-137">For more information on contribution and suggestion, see [Get it on GitHub](https://aka.ms/JDAShiftsConnector).</span></span></br></br>

## <a name="see-also"></a><span data-ttu-id="ba591-138">Consulte también</span><span class="sxs-lookup"><span data-stu-id="ba591-138">See also</span></span>

[<span data-ttu-id="ba591-139">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ba591-139">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
