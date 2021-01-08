---
title: Solicitar permisos de dispositivo para la pestaña de Microsoft Teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que suelen requerir el consentimiento del usuario
keywords: desarrollo de pestañas de Microsoft Teams
ms.openlocfilehash: 6be183d2610616f3bd3bdf32554976322193c132
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731982"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Solicitar permisos de dispositivo para la pestaña de Microsoft Teams

Es posible que quiera enriquecer su pestaña con características que requieran acceso a la funcionalidad de dispositivos nativos como:

> [!div class="checklist"]
>
> * Digital
> * Micro
> * Ubicación
> * Notificaciones

[!Note] Para integrar las capacidades de cámara y de imagen en la aplicación móvil de Microsoft Teams, consulte [capacidades de cámara y de imagen en Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!IMPORTANT]
>
> * Actualmente, el cliente móvil de Microsoft Teams solo admite el acceso a `camera` , `gallery` , `mic` y `location` a través de las funciones de dispositivos nativos, y está disponible en todas las construcciones de aplicaciones, incluidas las pestañas. </br>
> * Compatibilidad con `camera` , `gallery` y `mic` se habilita a través de la [**API de selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Para la captura de imagen única, puede usar la [**API de captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).
> * La compatibilidad con `location` se habilita a través de la [**API de getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Se recomienda usar esta API ya que actualmente la [**API de geolocalización**](../../resources/schema/manifest-schema.md#devicepermissions) no es totalmente compatible con todos los clientes de escritorio.

## <a name="device-permissions"></a>Permisos de dispositivo

El acceso a los permisos de dispositivo de un usuario le permite crear experiencias mucho más enriquecidas, por ejemplo:

* Grabar y compartir vídeos breves
* Grabe memorandos de audio cortos y guárdelos para más tarde
* Usar la información de ubicación del usuario para mostrar información relevante

Aunque el acceso a estas características es estándar en la mayoría de los exploradores Web modernos, es necesario que los equipos sepan qué características le gustaría usar al actualizar el manifiesto de la aplicación. Esto le permitirá solicitar permisos, de la misma manera que lo haría en un explorador, mientras la aplicación se ejecuta en el cliente de escritorio de Microsoft Teams.

## <a name="manage-permissions"></a>Administrar permisos

# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abra Microsoft Teams.
1. En la esquina superior derecha de la ventana, seleccione el icono de su perfil.
1. Seleccione **Settings**  ->  **Permissions** en el menú desplegable.
1. Elija la configuración que desee.

![Pantalla Configuración del escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Microsoft Teams.
1. Vaya a **configuración**  ->  **permisos** de la aplicación.
1. Seleccione la aplicación para la que quiera elegir la configuración.
1. Elija la configuración que desee.

![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

---

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
> [!Note]
>
> Los medios también se usan para los permisos de cámara en dispositivos móviles.

Cada propiedad le permitirá solicitar al usuario que solicite su consentimiento:

| Propiedad      | Descripción   |
| --- | --- |
| medios         | permiso para usar la cámara, el micrófono, los altavoces y la galería de medios de Access |
| geolocalización   | permiso para devolver la ubicación del usuario      |
| notificaciones | permiso para enviar notificaciones de usuario      |
| MIDI          | permiso para enviar y recibir información MIDI de un instrumento musical digital   |
| openExternal  | permiso para abrir vínculos en aplicaciones externas  |

## <a name="checking-permissions-from-your-tab"></a>Comprobación de permisos en la pestaña

Una vez que haya agregado `devicePermissions` al manifiesto de la aplicación, puede comprobar los permisos mediante la API de "permisos" de HTML5 sin que se le pida confirmación.

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

Para mostrar una solicitud para obtener consentimiento para obtener acceso a los permisos del dispositivo, debe aprovechar la API de HTML5 o Teams adecuada. 

Por ejemplo, para solicitar al usuario que tenga acceso a su ubicación, debe llamar a `getCurrentPosition` :

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

Para usar la cámara en el escritorio o en la web, Microsoft Teams mostrará una solicitud de permiso cuando llame a `getUserMedia` :

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

Para capturar la imagen en dispositivos móviles, Teams Mobile le pedirá permiso cuando llame a `captureImage()` :

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

Las notificaciones le preguntarán al usuario cuando llame a `requestPermission` :

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

Para usar la cámara o la galería de fotografías de Access, Teams Mobile le pedirá permiso cuando llame a `selectMedia()` :

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Para usar MIC, Teams Mobile le pedirá permiso cuando llame a `selectMedia()` :

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Para solicitar al usuario que comparta la ubicación en la interfaz del mapa, Team Mobile le pedirá permiso cuando llame a `getLocation()` :

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[Escritorio](#tab/desktop)

![Mensaje de pestañas de permisos de dispositivo de escritorio](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

![Mensaje de pestañas de permisos de dispositivo móvil](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos en sesiones de inicio de sesión

Los permisos de dispositivos nativos se almacenan para cada sesión de inicio. Significa que si inicia sesión en otra instancia de Teams (por ejemplo: en otro equipo), los permisos de dispositivo de las sesiones anteriores no estarán disponibles. En su lugar, tendrá que volver a dar su consentimiento a los permisos de dispositivo para la nueva sesión de inicio de sesión. También significa que, si sale de la sesión de Microsoft Teams (o de los inquilinos de conmutador dentro de los equipos), los permisos de dispositivo se eliminarán para la sesión de inicio anterior. Tenga esto en cuenta cuando desarrolle permisos de dispositivos nativos: las funciones nativas con las que da su consentimiento están solo para su sesión de inicio _actual_ .
