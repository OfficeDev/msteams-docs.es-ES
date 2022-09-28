---
title: 'Funcionalidades del dispositivo: información general'
author: Rajeshwari-v
description: Obtenga información sobre cómo integrar funcionalidades nativas de dispositivos, como la ubicación y los medios (cámara, micrófono, galería, escáner qr o código de barras) con la aplicación Microsoft Teams.
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 04ae1a0b21c12ef7dda5d4bf8dfa799ac5726d15
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100570"
---
# <a name="device-capabilities"></a>Funciones del dispositivo

La plataforma de Microsoft Teams mejora continuamente las funconalidades de los desarrolladores en consonancia con las experiencias integradas de primera persona. La plataforma mejorada de Teams permite a los asociados integrar funcionalidades de dispositivos, como cámara, escáner de códigos de barras o QR, galería de fotos, micrófono y ubicación con sus aplicaciones web. Esta integración reduce la barrera del desarrollo de aplicaciones, acelera el ciclo de desarrollo y crea nuevos escenarios o casos de uso para la comunidad de desarrolladores.

Los permisos del dispositivo son diferentes en el explorador. Anteriormente, el explorador administraba cómo conceder permisos de acceso y ahora estos permisos se controlan en Teams. Para obtener más información, vea [Permisos del dispositivo en el navegador](browser-device-permissions.md).

## <a name="native-device-capabilities"></a>Funcionalidades de dispositivos nativos

Un móvil o un ordenador de sobremesa tienen dispositivos incorporados, como la cámara y el micrófono, llamados funcionalidades. Puede acceder a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles en el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):

* Funcionalidades multimedia, como
  * Cámara
  * Micrófono
  * Galería
  * Escáner de códigos de barras o código QR
* Ubicación

Después de obtener acceso a las funcionalidades del dispositivo, puede integrarlas con la plataforma Teams para mejorar la experiencia de colaboración.

## <a name="request-device-permissions"></a>Solicitar permisos de dispositivo

Use las herramientas presentes en [SDK de cliente JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) para solicitar los [permisos](native-device-permissions.md) necesarios para acceder a las funcionalidades nativas del dispositivo. Aunque el acceso a estas funcionalidades es estándar en los exploradores web modernos, debe informar a Teams sobre las funcionalidades que usa mediante la actualización del manifiesto de la aplicación. Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en clientes móviles o de escritorio de Teams.

## <a name="integrate-device-capabilities"></a>Integrar las funcionalidades del dispositivo

Después de obtener acceso a las funcionalidades del dispositivo, use las API de funcionalidad multimedia de Teams para [integrar funcionalidades multimedia](media-capabilities.md) con la plataforma de Teams para mejorar la experiencia del usuario. Estas funcionalidades integradas permiten a la aplicación:

* Capturar y compartir imágenes.
* Escanear código QR o código de barras usando el [control de escáner](qr-barcode-scanner-capability.md).
* Grabar audio a través del micrófono.
* Compartir ubicación mediante el [selector de ubicación](location-capability.md).

Además, puede integrar el [control de selector de personas](people-picker-capability.md) nativas de Teams, que permite a los usuarios buscar y seleccionar personas en la experiencia de la aplicación web.

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre           | Descripción | Node.js    |
|:---------------------|:--------------|:---------|
|Permisos de dispositivo | Describe cómo mostrar la aplicación de ejemplo de pestaña de Teams para los permisos de dispositivo. |[View](<https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs>)|
