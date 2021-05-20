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
# <a name="device-capabilities"></a>Funciones del dispositivo

Microsoft Teams plataforma está mejorando continuamente las capacidades de los desarrolladores que se alinean con las experiencias integradas de la primera parte. La plataforma de Teams mejorada permite a los socios integrar capacidades de dispositivos, como cámara, QR o escáner de código de barras, galería de fotos, micrófono y ubicación con sus aplicaciones web. Esta integración reduce la barrera para el desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.

## <a name="native-device-capabilities"></a>Capacidades de dispositivos nativos

Un dispositivo móvil o de escritorio tiene dispositivos integrados, como una cámara y un micrófono, llamados capacidades. Puede acceder a las siguientes capacidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles en [Microsoft Teams SDK de cliente javascript:](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* Capacidades de medios, como
    * cámara
    * micrófono
    * Galería
    * Escáner QR o código de barras
* Ubicación

Después de obtener acceso a las capacidades del dispositivo, puede integrarlas con Teams plataforma para mejorar la experiencia colaborativa. 

## <a name="request-device-permissions"></a>Solicitar permisos de dispositivo

Utilice las herramientas presentes en [Microsoft Teams SDK de cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) para solicitar los [permisos](native-device-permissions.md) necesarios para acceder a las capacidades del dispositivo nativo. Aunque el acceso a estas capacidades es estándar en los exploradores web modernos, debe informar a Teams sobre las capacidades que está utilizando actualizando el manifiesto de la aplicación. Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en Teams clientes móviles o de escritorio.
 
 ## <a name="integrate-device-capabilities"></a>Integrar capacidades de dispositivos

Después de obtener acceso a las capacidades del dispositivo, use Teams API de capacidad de medios para [integrar capacidades multimedia](mobile-camera-image-permissions.md) con Teams plataforma para mejorar la experiencia del usuario. Estas capacidades integradas permiten a la aplicación:

* Captura y comparte imágenes.
* Escanear QR o código de barras mediante [el control del escáner.](qr-barcode-scanner-capability.md)
* Grabe audio a través del micrófono.
* Comparta la ubicación mediante [el selector de ubicación.](location-capability.md)
