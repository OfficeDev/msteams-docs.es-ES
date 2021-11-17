---
title: 'Funcionalidades del dispositivo: información general'
author: Rajeshwari-v
description: Información general sobre las capacidades de dispositivo nativo, como cámara, imagen, medios, micrófono, micrófono, código qr y mucho más.
ms.author: surbhigupta
keywords: Cámara image media microphone mic qr code qrcode bar code barcode scan scanner location capabilities native device permissions
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: d51b9532822a6cb9df2f69975722d16da6ee2531
ms.sourcegitcommit: 1ac0bd55adfd49c42cd870dc71ceca3dcac70941
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/16/2021
ms.locfileid: "61041716"
---
# <a name="device-capabilities"></a>Funciones del dispositivo

Microsoft Teams plataforma está mejorando continuamente las capacidades de los desarrolladores que se alinean con las experiencias integradas de primera persona. La plataforma de Teams permite a los partners integrar las capacidades del dispositivo, como cámara, escáner qr o código de barras, galería de fotos, micrófono y ubicación con sus aplicaciones web. Esta integración reduce la barrera del desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.

Los permisos de dispositivo son diferentes en el explorador. Anteriormente, el explorador controló cómo conceder permisos de acceso y ahora estos permisos se controlan en Microsoft Teams. Para obtener más información, vea [permisos de dispositivo del explorador](browser-device-permissions.md).

## <a name="native-device-capabilities"></a>Funcionalidades de dispositivo nativo

Un dispositivo móvil o de escritorio tiene dispositivos integrados, como cámara y micrófono, denominados funcionalidades. Puedes obtener acceso a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles [en Microsoft Teams SDK de cliente de JavaScript:](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* Funcionalidades multimedia, como
    * Cámara
    * Micrófono
    * Galería
    * Escáner qr o de código de barras
* Ubicación

Después de obtener acceso a las funcionalidades del dispositivo, puedes integrarlas con la Teams para mejorar la experiencia de colaboración. 

## <a name="request-device-permissions"></a>Solicitar permisos de dispositivo

Use las herramientas presentes en Microsoft Teams SDK de cliente [de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) para solicitar los permisos [necesarios](native-device-permissions.md) para obtener acceso a las funcionalidades de dispositivo nativo. Aunque el acceso a estas funcionalidades es estándar en exploradores web modernos, debes informar a Teams sobre las funcionalidades que estás usando mediante la actualización del manifiesto de la aplicación. Esta actualización te permite solicitar permisos mientras la aplicación se ejecuta en Teams móviles o de escritorio.
 
 ## <a name="integrate-device-capabilities"></a>Integrar funcionalidades de dispositivos

Después de obtener acceso a las funcionalidades del [](mobile-camera-image-permissions.md) dispositivo, usa Teams API de funcionalidad multimedia para integrar las capacidades multimedia con la plataforma Teams para mejorar la experiencia del usuario. Estas funcionalidades integradas permiten a la aplicación:

* Capturar y compartir imágenes.
* Digitalizar QR o código de barras mediante [el control de escáner](qr-barcode-scanner-capability.md).
* Grabar audio a través del micrófono.
* Compartir ubicación mediante [el selector de ubicación](location-capability.md).

Además, puedes integrar el control Teams selector [de](people-picker-capability.md) personas nativas que permite a los usuarios buscar y seleccionar personas en la experiencia de la aplicación web.
