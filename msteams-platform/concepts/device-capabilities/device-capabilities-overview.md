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
# <a name="device-capabilities"></a>Funciones del dispositivo 

La plataforma de Microsoft Teams está mejorando continuamente las capacidades de los desarrolladores que se alinean con experiencias integradas propias. La plataforma mejorada de Teams permite a los partners integrar funcionalidades de dispositivos, como cámara, galería de fotos, micrófono y ubicación, con sus aplicaciones web. Esta integración reduce la barrera al desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.

## <a name="native-device-capabilities"></a>Funcionalidades de dispositivo nativo

Un dispositivo móvil o de escritorio tiene dispositivos integrados, como una cámara y un micrófono, llamados funcionalidades. Puede acceder a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de api dedicadas disponibles en el SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)de Microsoft Teams:
* Funcionalidades multimedia, como
    * Cámara
    * Micrófono
    * Galería
* Ubicación

Después de obtener acceso a las funcionalidades del dispositivo, puede integrarlas con la plataforma de Teams para mejorar la experiencia de colaboración. 

## <a name="request-device-permissions"></a>Solicitar permisos de dispositivo

Use las herramientas presentes en el SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams para solicitar los permisos  [necesarios para](native-device-permissions.md) obtener acceso a las funcionalidades de dispositivo nativo. Aunque el acceso a estas funcionalidades es estándar en exploradores web modernos, debe informar a Teams sobre las funcionalidades que está usando mediante la actualización del manifiesto de la aplicación. Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en clientes móviles o de escritorio de Teams.
 
 ## <a name="integrate-device-capabilities"></a>Integrar funcionalidades de dispositivos

Después de obtener acceso a las funcionalidades [](mobile-camera-image-permissions.md) del dispositivo, use las API de capacidad multimedia de **Teams** para integrar las capacidades con la plataforma de Teams para mejorar la experiencia del usuario. Estas funcionalidades integradas permiten que la aplicación:

* Capturar y compartir imágenes
* Grabar audio a través del micrófono
* Compartir la información de ubicación


