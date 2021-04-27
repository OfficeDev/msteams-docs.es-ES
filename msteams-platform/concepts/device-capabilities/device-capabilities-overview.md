---
title: 'Funcionalidades del dispositivo: información general'
author: Rajeshwari-v
description: Información general sobre las capacidades nativas del dispositivo.
ms.author: surbhigupta
keywords: Cámara image media microphone mic qr code qrcode bar code barcode scan scanner location capabilities native device permissions
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 7d214e5011abdc83d2f6b5b49c2261359259035e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020754"
---
# <a name="device-capabilities---overview"></a><span data-ttu-id="45f59-104">Funcionalidades del dispositivo: información general</span><span class="sxs-lookup"><span data-stu-id="45f59-104">Device capabilities - Overview</span></span>

<span data-ttu-id="45f59-105">La plataforma de Microsoft Teams mejora continuamente las capacidades de los desarrolladores y se alinea con experiencias integradas de primera persona.</span><span class="sxs-lookup"><span data-stu-id="45f59-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="45f59-106">La plataforma mejorada de Teams permite a los partners integrar las capacidades del dispositivo, como cámara, escáner qr o código de barras, galería de fotos, micrófono y ubicación con sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="45f59-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="45f59-107">Esta integración reduce la barrera para el desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="45f59-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="45f59-108">Funcionalidades de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="45f59-108">Native device capabilities</span></span>

<span data-ttu-id="45f59-109">Un dispositivo móvil o de escritorio tiene dispositivos integrados, como una cámara y un micrófono, denominados funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="45f59-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="45f59-110">Puedes acceder a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles en [microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span><span class="sxs-lookup"><span data-stu-id="45f59-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="45f59-111">Funcionalidades multimedia, como</span><span class="sxs-lookup"><span data-stu-id="45f59-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="45f59-112">Cámara</span><span class="sxs-lookup"><span data-stu-id="45f59-112">Camera</span></span>
    * <span data-ttu-id="45f59-113">Micrófono</span><span class="sxs-lookup"><span data-stu-id="45f59-113">Microphone</span></span>
    * <span data-ttu-id="45f59-114">Galería</span><span class="sxs-lookup"><span data-stu-id="45f59-114">Gallery</span></span>
    * <span data-ttu-id="45f59-115">Escáner qr o de código de barras</span><span class="sxs-lookup"><span data-stu-id="45f59-115">QR or barcode scanner</span></span>
* <span data-ttu-id="45f59-116">Ubicación</span><span class="sxs-lookup"><span data-stu-id="45f59-116">Location</span></span>

<span data-ttu-id="45f59-117">Después de obtener acceso a las capacidades del dispositivo, puedes integrarlas con la plataforma de Teams para mejorar la experiencia de colaboración.</span><span class="sxs-lookup"><span data-stu-id="45f59-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="45f59-118">Solicitar permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="45f59-118">Request device permissions</span></span>

<span data-ttu-id="45f59-119">Use las herramientas presentes en el SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams para solicitar los permisos necesarios para obtener acceso a las funcionalidades  [nativas](native-device-permissions.md) del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="45f59-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="45f59-120">Aunque el acceso a estas funcionalidades es estándar en exploradores web modernos, debes informar a Teams sobre las funcionalidades que usas actualizando el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="45f59-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="45f59-121">Esta actualización te permite solicitar permisos mientras la aplicación se ejecuta en clientes móviles o de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="45f59-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="45f59-122">Integrar funcionalidades de dispositivos</span><span class="sxs-lookup"><span data-stu-id="45f59-122">Integrate device capabilities</span></span>

<span data-ttu-id="45f59-123">Después de obtener acceso a las funcionalidades [](mobile-camera-image-permissions.md) del dispositivo, usa las API de capacidad multimedia de Teams para integrar las capacidades multimedia con la plataforma de Teams para mejorar la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="45f59-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="45f59-124">Estas funcionalidades integradas permiten a la aplicación:</span><span class="sxs-lookup"><span data-stu-id="45f59-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="45f59-125">Capturar y compartir imágenes</span><span class="sxs-lookup"><span data-stu-id="45f59-125">Capture and share images</span></span>
* <span data-ttu-id="45f59-126">Digitalizar QR o código de barras con [control de escáner](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="45f59-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md)</span></span>
* <span data-ttu-id="45f59-127">Grabar audio a través del micrófono</span><span class="sxs-lookup"><span data-stu-id="45f59-127">Record audio through microphone</span></span>
* <span data-ttu-id="45f59-128">Compartir ubicación mediante [el selector de ubicación](location-capability.md).</span><span class="sxs-lookup"><span data-stu-id="45f59-128">Share location using [location picker](location-capability.md).</span></span>
