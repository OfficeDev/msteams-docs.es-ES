---
title: Información general sobre las funcionalidades del dispositivo
description: Información general sobre las funcionalidades de dispositivo nativo.
keywords: Permisos de dispositivo nativo de capacidades de micrófono multimedia de imagen de cámara
ms.topic: overview
ms.openlocfilehash: 8b2f92cb4586d646bde02742883122bb009847ea
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50232852"
---
# <a name="device-capabilities"></a><span data-ttu-id="3c4fb-104">Funciones del dispositivo</span><span class="sxs-lookup"><span data-stu-id="3c4fb-104">Device capabilities</span></span> 

<span data-ttu-id="3c4fb-105">La plataforma de Microsoft Teams está mejorando continuamente las capacidades de los desarrolladores que se alinean con experiencias integradas propias.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="3c4fb-106">La plataforma mejorada de Teams permite a los partners integrar funcionalidades de dispositivos, como cámara, galería de fotos, micrófono y ubicación, con sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, photo gallery, microphone, and location, with their web apps.</span></span> <span data-ttu-id="3c4fb-107">Esta integración reduce la barrera al desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="3c4fb-108">Funcionalidades de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="3c4fb-108">Native device capabilities</span></span>

<span data-ttu-id="3c4fb-109">Un dispositivo móvil o de escritorio tiene dispositivos integrados, como una cámara y un micrófono, llamados funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="3c4fb-110">Puede acceder a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de api dedicadas disponibles en el SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)de Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="3c4fb-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="3c4fb-111">Funcionalidades multimedia, como</span><span class="sxs-lookup"><span data-stu-id="3c4fb-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="3c4fb-112">Cámara</span><span class="sxs-lookup"><span data-stu-id="3c4fb-112">Camera</span></span>
    * <span data-ttu-id="3c4fb-113">Micrófono</span><span class="sxs-lookup"><span data-stu-id="3c4fb-113">Microphone</span></span>
    * <span data-ttu-id="3c4fb-114">Galería</span><span class="sxs-lookup"><span data-stu-id="3c4fb-114">Gallery</span></span>
* <span data-ttu-id="3c4fb-115">Ubicación</span><span class="sxs-lookup"><span data-stu-id="3c4fb-115">Location</span></span>

<span data-ttu-id="3c4fb-116">Después de obtener acceso a las funcionalidades del dispositivo, puede integrarlas con la plataforma de Teams para mejorar la experiencia de colaboración.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-116">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="3c4fb-117">Solicitar permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="3c4fb-117">Request device permissions</span></span>

<span data-ttu-id="3c4fb-118">Use las herramientas presentes en el SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams para solicitar los permisos  [necesarios para](native-device-permissions.md) obtener acceso a las funcionalidades de dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-118">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to  request the required  [permissions](native-device-permissions.md) for  accessing the native device capabilities.</span></span> <span data-ttu-id="3c4fb-119">Aunque el acceso a estas funcionalidades es estándar en exploradores web modernos, debe informar a Teams sobre las funcionalidades que está usando mediante la actualización del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-119">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="3c4fb-120">Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en clientes móviles o de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-120">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="3c4fb-121">Integrar funcionalidades de dispositivos</span><span class="sxs-lookup"><span data-stu-id="3c4fb-121">Integrate device capabilities</span></span>

<span data-ttu-id="3c4fb-122">Después de obtener acceso a las funcionalidades [](mobile-camera-image-permissions.md) del dispositivo, use las API de capacidad multimedia de **Teams** para integrar las capacidades con la plataforma de Teams para mejorar la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="3c4fb-122">After getting access to device capabilities,use **Teams media capability APIs** to [integrate the capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="3c4fb-123">Estas funcionalidades integradas permiten que la aplicación:</span><span class="sxs-lookup"><span data-stu-id="3c4fb-123">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="3c4fb-124">Capturar y compartir imágenes</span><span class="sxs-lookup"><span data-stu-id="3c4fb-124">Capture and share images</span></span>
* <span data-ttu-id="3c4fb-125">Grabar audio a través del micrófono</span><span class="sxs-lookup"><span data-stu-id="3c4fb-125">Record audio through microphone</span></span>
* <span data-ttu-id="3c4fb-126">Compartir la información de ubicación</span><span class="sxs-lookup"><span data-stu-id="3c4fb-126">Share the location information</span></span>


