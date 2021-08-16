---
title: 'Funcionalidades del dispositivo: información general'
author: Rajeshwari-v
description: Información general sobre las capacidades nativas del dispositivo.
ms.author: surbhigupta
keywords: Cámara image media microphone mic qr code qrcode bar code barcode scan scanner location capabilities native device permissions
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 4b09d4d81301aa8fc125da98a3633dc79e05d3d1
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345728"
---
# <a name="device-capabilities"></a>Funciones del dispositivo

Microsoft Teams plataforma está mejorando continuamente las capacidades de los desarrolladores que se alinean con las experiencias integradas de primera persona. La plataforma de Teams permite a los partners integrar las capacidades del dispositivo, como cámara, escáner qr o código de barras, galería de fotos, micrófono y ubicación con sus aplicaciones web. Esta integración reduce la barrera para el desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.

## <a name="native-device-capabilities"></a>Funcionalidades de dispositivo nativo

Un dispositivo móvil o de escritorio tiene dispositivos integrados, como una cámara y un micrófono, denominados funcionalidades. Puedes obtener acceso a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles [en Microsoft Teams SDK de cliente de JavaScript:](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* Funcionalidades multimedia, como
    * Cámara
    * Micrófono
    * Galería
    * Escáner qr o de código de barras
* Ubicación

Después de obtener acceso a las capacidades del dispositivo, puedes integrarlas Teams plataforma para mejorar la experiencia de colaboración. 

## <a name="request-device-permissions"></a>Solicitar permisos de dispositivo

Use las herramientas presentes en Microsoft Teams SDK de cliente [de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) para solicitar los permisos [necesarios](native-device-permissions.md) para obtener acceso a las funcionalidades de dispositivo nativo. Aunque el acceso a estas funcionalidades es estándar en exploradores web modernos, debes informar a Teams sobre las funcionalidades que estás usando mediante la actualización del manifiesto de la aplicación. Esta actualización te permite solicitar permisos mientras la aplicación se ejecuta en Teams móviles o de escritorio.
 
 ## <a name="integrate-device-capabilities"></a>Integrar funcionalidades de dispositivos

Después de obtener acceso a las funcionalidades del dispositivo, usa Teams API de funcionalidad multimedia para integrar las capacidades multimedia con Teams plataforma para mejorar la experiencia del usuario. [](mobile-camera-image-permissions.md) Estas funcionalidades integradas permiten a la aplicación:

* Capturar y compartir imágenes.
* Digitalizar QR o código de barras mediante [el control de escáner](qr-barcode-scanner-capability.md).
* Grabar audio a través del micrófono.
* Compartir ubicación mediante [el selector de ubicación](location-capability.md).

Además, puedes integrar el control Teams selector [de](people-picker-capability.md) personas nativas que permite a los usuarios buscar y seleccionar personas en la experiencia de la aplicación web.


