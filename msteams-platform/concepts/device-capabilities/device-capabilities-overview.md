---
title: 'Funcionalidades del dispositivo: información general'
author: Rajeshwari-v
description: Información general sobre las capacidades nativas del dispositivo.
ms.author: surbhigupta
keywords: Cámara image media microphone mic qr code qrcode bar code barcode scan scanner location capabilities native device permissions
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 069bd27057784076b3b701d013ead209ec6fa3a9
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211586"
---
# <a name="device-capabilities"></a><span data-ttu-id="12876-104">Funciones del dispositivo</span><span class="sxs-lookup"><span data-stu-id="12876-104">Device capabilities</span></span>

<span data-ttu-id="12876-105">Microsoft Teams plataforma está mejorando continuamente las capacidades de los desarrolladores que se alinean con las experiencias integradas de primera persona.</span><span class="sxs-lookup"><span data-stu-id="12876-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="12876-106">La plataforma de Teams permite a los partners integrar las capacidades del dispositivo, como cámara, escáner qr o código de barras, galería de fotos, micrófono y ubicación con sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="12876-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="12876-107">Esta integración reduce la barrera para el desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="12876-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="12876-108">Funcionalidades de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="12876-108">Native device capabilities</span></span>

<span data-ttu-id="12876-109">Un dispositivo móvil o de escritorio tiene dispositivos integrados, como una cámara y un micrófono, denominados funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="12876-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="12876-110">Puedes obtener acceso a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles [en Microsoft Teams SDK de cliente de JavaScript:](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="12876-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="12876-111">Funcionalidades multimedia, como</span><span class="sxs-lookup"><span data-stu-id="12876-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="12876-112">Cámara</span><span class="sxs-lookup"><span data-stu-id="12876-112">Camera</span></span>
    * <span data-ttu-id="12876-113">Micrófono</span><span class="sxs-lookup"><span data-stu-id="12876-113">Microphone</span></span>
    * <span data-ttu-id="12876-114">Galería</span><span class="sxs-lookup"><span data-stu-id="12876-114">Gallery</span></span>
    * <span data-ttu-id="12876-115">Escáner qr o de código de barras</span><span class="sxs-lookup"><span data-stu-id="12876-115">QR or barcode scanner</span></span>
* <span data-ttu-id="12876-116">Ubicación</span><span class="sxs-lookup"><span data-stu-id="12876-116">Location</span></span>

<span data-ttu-id="12876-117">Después de obtener acceso a las capacidades del dispositivo, puedes integrarlas Teams plataforma para mejorar la experiencia de colaboración.</span><span class="sxs-lookup"><span data-stu-id="12876-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="12876-118">Solicitar permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="12876-118">Request device permissions</span></span>

<span data-ttu-id="12876-119">Use las herramientas presentes en Microsoft Teams SDK de cliente [de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) para solicitar los permisos [necesarios](native-device-permissions.md) para obtener acceso a las funcionalidades de dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="12876-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="12876-120">Aunque el acceso a estas funcionalidades es estándar en exploradores web modernos, debes informar a Teams sobre las funcionalidades que estás usando mediante la actualización del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12876-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="12876-121">Esta actualización te permite solicitar permisos mientras la aplicación se ejecuta en Teams móviles o de escritorio.</span><span class="sxs-lookup"><span data-stu-id="12876-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="12876-122">Integrar funcionalidades de dispositivos</span><span class="sxs-lookup"><span data-stu-id="12876-122">Integrate device capabilities</span></span>

<span data-ttu-id="12876-123">Después de obtener acceso a las funcionalidades del dispositivo, usa Teams API de funcionalidad multimedia para integrar las capacidades multimedia con Teams plataforma para mejorar la experiencia del usuario. [](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="12876-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="12876-124">Estas funcionalidades integradas permiten a la aplicación:</span><span class="sxs-lookup"><span data-stu-id="12876-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="12876-125">Capturar y compartir imágenes.</span><span class="sxs-lookup"><span data-stu-id="12876-125">Capture and share images.</span></span>
* <span data-ttu-id="12876-126">Digitalizar QR o código de barras mediante [el control de escáner](qr-barcode-scanner-capability.md).</span><span class="sxs-lookup"><span data-stu-id="12876-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md).</span></span>
* <span data-ttu-id="12876-127">Grabar audio a través del micrófono.</span><span class="sxs-lookup"><span data-stu-id="12876-127">Record audio through microphone.</span></span>
* <span data-ttu-id="12876-128">Compartir ubicación mediante [el selector de ubicación](location-capability.md).</span><span class="sxs-lookup"><span data-stu-id="12876-128">Share location using [location picker](location-capability.md).</span></span>

<span data-ttu-id="12876-129">Además, puedes integrar el control Teams selector [de](people-picker-capability.md) personas nativas que permite a los usuarios buscar y seleccionar personas en la experiencia de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="12876-129">Also, you can integrate the Teams native [people picker control](people-picker-capability.md) that allows users to search and select people in the web app experience.</span></span>
