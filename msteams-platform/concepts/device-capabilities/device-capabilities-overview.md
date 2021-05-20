---
title: Capacidades del dispositivo - Visión general
author: Rajeshwari-v
description: Descripción general de las capacidades de los dispositivos nativos.
ms.author: surbhigupta
keywords: micrófono de medios de imagen de la cámara qr código qrcode código de barras código de barras escanear la ubicación del escáner capacidades permisos de dispositivo nativo
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 8df8341e8996e4bf380575ac59e05325da16bd0d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566197"
---
# <a name="device-capabilities"></a><span data-ttu-id="34cb8-104">Funciones del dispositivo</span><span class="sxs-lookup"><span data-stu-id="34cb8-104">Device capabilities</span></span>

<span data-ttu-id="34cb8-105">Microsoft Teams plataforma está mejorando continuamente las capacidades de los desarrolladores que se alinean con las experiencias integradas de la primera parte.</span><span class="sxs-lookup"><span data-stu-id="34cb8-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="34cb8-106">La plataforma de Teams mejorada permite a los socios integrar capacidades de dispositivos, como cámara, QR o escáner de código de barras, galería de fotos, micrófono y ubicación con sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="34cb8-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="34cb8-107">Esta integración reduce la barrera para el desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="34cb8-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="34cb8-108">Capacidades de dispositivos nativos</span><span class="sxs-lookup"><span data-stu-id="34cb8-108">Native device capabilities</span></span>

<span data-ttu-id="34cb8-109">Un dispositivo móvil o de escritorio tiene dispositivos integrados, como una cámara y un micrófono, llamados capacidades.</span><span class="sxs-lookup"><span data-stu-id="34cb8-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="34cb8-110">Puede acceder a las siguientes capacidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles en [Microsoft Teams SDK de cliente javascript:](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="34cb8-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="34cb8-111">Capacidades de medios, como</span><span class="sxs-lookup"><span data-stu-id="34cb8-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="34cb8-112">cámara</span><span class="sxs-lookup"><span data-stu-id="34cb8-112">Camera</span></span>
    * <span data-ttu-id="34cb8-113">micrófono</span><span class="sxs-lookup"><span data-stu-id="34cb8-113">Microphone</span></span>
    * <span data-ttu-id="34cb8-114">Galería</span><span class="sxs-lookup"><span data-stu-id="34cb8-114">Gallery</span></span>
    * <span data-ttu-id="34cb8-115">Escáner QR o código de barras</span><span class="sxs-lookup"><span data-stu-id="34cb8-115">QR or barcode scanner</span></span>
* <span data-ttu-id="34cb8-116">Ubicación</span><span class="sxs-lookup"><span data-stu-id="34cb8-116">Location</span></span>

<span data-ttu-id="34cb8-117">Después de obtener acceso a las capacidades del dispositivo, puede integrarlas con Teams plataforma para mejorar la experiencia colaborativa.</span><span class="sxs-lookup"><span data-stu-id="34cb8-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="34cb8-118">Solicitar permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="34cb8-118">Request device permissions</span></span>

<span data-ttu-id="34cb8-119">Utilice las herramientas presentes en [Microsoft Teams SDK de cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) para solicitar los [permisos](native-device-permissions.md) necesarios para acceder a las capacidades del dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="34cb8-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="34cb8-120">Aunque el acceso a estas capacidades es estándar en los exploradores web modernos, debe informar a Teams sobre las capacidades que está utilizando actualizando el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34cb8-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="34cb8-121">Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en Teams clientes móviles o de escritorio.</span><span class="sxs-lookup"><span data-stu-id="34cb8-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="34cb8-122">Integrar capacidades de dispositivos</span><span class="sxs-lookup"><span data-stu-id="34cb8-122">Integrate device capabilities</span></span>

<span data-ttu-id="34cb8-123">Después de obtener acceso a las capacidades del dispositivo, use Teams API de capacidad de medios para [integrar capacidades multimedia](mobile-camera-image-permissions.md) con Teams plataforma para mejorar la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="34cb8-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="34cb8-124">Estas capacidades integradas permiten a la aplicación:</span><span class="sxs-lookup"><span data-stu-id="34cb8-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="34cb8-125">Captura y comparte imágenes.</span><span class="sxs-lookup"><span data-stu-id="34cb8-125">Capture and share images.</span></span>
* <span data-ttu-id="34cb8-126">Escanear QR o código de barras mediante [el control del escáner.](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="34cb8-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md).</span></span>
* <span data-ttu-id="34cb8-127">Grabe audio a través del micrófono.</span><span class="sxs-lookup"><span data-stu-id="34cb8-127">Record audio through microphone.</span></span>
* <span data-ttu-id="34cb8-128">Comparta la ubicación mediante [el selector de ubicación.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="34cb8-128">Share location using [location picker](location-capability.md).</span></span>
