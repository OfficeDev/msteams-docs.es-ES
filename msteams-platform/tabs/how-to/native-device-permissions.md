---
title: Solicitar permisos de dispositivo para la pestaña de Microsoft Teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que suelen requerir el consentimiento del usuario
keywords: desarrollo de pestañas de Microsoft Teams
ms.openlocfilehash: 454466ff17ecf275f6ae6c7413df8e117335f3c8
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675712"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Solicitar permisos de dispositivo para la pestaña de Microsoft Teams

Es posible que quiera enriquecer su pestaña con características que requieran la funcionalidad de dispositivo nativo de Access como:

* Digital
* Micro
* Ubicación
* Notificaciones

![Pantalla de configuración de permisos de dispositivo](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> Actualmente, la funcionalidad de dispositivos nativos no es compatible con las pestañas de clientes móviles, pero pronto estará disponible la compatibilidad completa. Para prepararse para este cambio, debe seguir las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas. Las aplicaciones personales (pestañas estáticas) están disponibles actualmente en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).
>
> Cuando se publica la compatibilidad completa de pestañas:
>
> * Todas las pestañas estarán siempre disponibles en dispositivos móviles
> * El `contentUrl` **se cargará en el cliente móvil de Microsoft Teams**.
> * En las pestañas canal/grupo, los usuarios pueden abrir la pestaña en un explorador independiente `websiteUrl`a través de `contentUrl` la, pero se cargará primero.  

## <a name="device-permissions"></a>Permisos de dispositivo

El acceso a los permisos de dispositivo de un usuario le permite crear experiencias mucho más enriquecidas, por ejemplo:

* Grabar y compartir vídeos breves
* Grabe memorandos de audio cortos y guárdelos para más tarde
* Usar la información de ubicación del usuario para mostrar información relevante

Aunque el acceso a estas características es estándar en la mayoría de los exploradores Web modernos, es necesario que los equipos sepan qué características desea usar al actualizar el manifiesto de la aplicación. Esto le permitirá solicitar permisos, de la misma manera que lo haría en un explorador, mientras la aplicación se ejecuta en el cliente de escritorio de Microsoft Teams.

## <a name="properties"></a>Propiedades

Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades desea usar en la aplicación:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Cada propiedad le permitirá pedir al usuario que pida su consentimiento

| Propiedad      | Descripción   |
| --- | --- |
| medios         | permiso para usar la cámara, el micrófono y los altavoces |
| geolocalización   | permiso para devolver la ubicación del usuario      |
| notificaciones | permiso para enviar notificaciones de usuario      |
| MIDI          | permiso para enviar y recibir información MIDI de un instrumento musical digital   |
| openExternal  | permiso para abrir vínculos en aplicaciones externas  |

## <a name="checking-permissions-from-your-tab"></a>Comprobación de permisos en la pestaña

Una vez que haya `devicePermissions` agregado al manifiesto de la aplicación, puede comprobar los permisos mediante la API de "permisos" de HTML5 sin que se le pida confirmación.

``` Javascript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="prompting-the-user"></a>Preguntar al usuario

Para mostrar una solicitud para obtener consentimiento para obtener acceso a los permisos del dispositivo, necesita aprovechar la API de HTML5 adecuada. Por ejemplo, para pedir al usuario que tenga acceso a su cámara, debe llamar a`getUserMedia`

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

La ubicación geográfica mostrará una solicitud de permiso cuando llame a`getCurrentPosition`

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

Las notificaciones le preguntarán al usuario cuando llame a`requestPermission`

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Pestañas del mensaje de permisos de dispositivo](~/assets/images/tabs/device-permissions-prompt.png)