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
# <a name="device-capabilities---overview"></a>Funcionalidades del dispositivo: información general

La plataforma de Microsoft Teams mejora continuamente las capacidades de los desarrolladores y se alinea con experiencias integradas de primera persona. La plataforma mejorada de Teams permite a los partners integrar las capacidades del dispositivo, como cámara, escáner qr o código de barras, galería de fotos, micrófono y ubicación con sus aplicaciones web. Esta integración reduce la barrera para el desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.

## <a name="native-device-capabilities"></a>Funcionalidades de dispositivo nativo

Un dispositivo móvil o de escritorio tiene dispositivos integrados, como una cámara y un micrófono, denominados funcionalidades. Puedes acceder a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles en [microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):
* Funcionalidades multimedia, como
    * Cámara
    * Micrófono
    * Galería
    * Escáner qr o de código de barras
* Ubicación

Después de obtener acceso a las capacidades del dispositivo, puedes integrarlas con la plataforma de Teams para mejorar la experiencia de colaboración. 

## <a name="request-device-permissions"></a>Solicitar permisos de dispositivo

Use las herramientas presentes en el SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams para solicitar los permisos necesarios para obtener acceso a las funcionalidades  [nativas](native-device-permissions.md) del dispositivo. Aunque el acceso a estas funcionalidades es estándar en exploradores web modernos, debes informar a Teams sobre las funcionalidades que usas actualizando el manifiesto de la aplicación. Esta actualización te permite solicitar permisos mientras la aplicación se ejecuta en clientes móviles o de escritorio de Teams.
 
 ## <a name="integrate-device-capabilities"></a>Integrar funcionalidades de dispositivos

Después de obtener acceso a las funcionalidades [](mobile-camera-image-permissions.md) del dispositivo, usa las API de capacidad multimedia de Teams para integrar las capacidades multimedia con la plataforma de Teams para mejorar la experiencia del usuario. Estas funcionalidades integradas permiten a la aplicación:

* Capturar y compartir imágenes
* Digitalizar QR o código de barras con [control de escáner](qr-barcode-scanner-capability.md)
* Grabar audio a través del micrófono
* Compartir ubicación mediante [el selector de ubicación](location-capability.md).
