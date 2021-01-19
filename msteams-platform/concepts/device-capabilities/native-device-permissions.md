---
title: Solicitar permisos de dispositivo para la pestaña de Microsoft Teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
keywords: desarrollo de pestañas de teams
ms.openlocfilehash: b021ae4ae8b50ddd1f3603f696922c129eb25f10
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886747"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Solicitar permisos de dispositivo para la pestaña de Microsoft Teams

Es posible que quieras enriquecer la pestaña con características que requieren acceso a la funcionalidad de dispositivo nativo, como:

> [!div class="checklist"]
>
> * Cámara
> * Micrófono
> * Ubicación
> * Notificaciones

> [!NOTE]
> Para integrar las capacidades de cámara e imagen dentro de la aplicación móvil de Microsoft Teams, vea las funciones de cámara [e imagen en Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!IMPORTANT]
>
> * Actualmente, el cliente móvil de Teams solo admite el acceso a , y a través de las capacidades de dispositivo nativo y está disponible en todas las construcciones de `camera` `gallery` `mic` `location` aplicaciones, incluidas las pestañas. </br>
> * Compatibilidad con `camera` , y se habilita a través de la API `gallery` `mic` [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Para la captura de imagen única, puede usar [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).
> * La compatibilidad con `location` se habilita a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Se recomienda usar esta API, ya que la [**API de geolocalización**](../../resources/schema/manifest-schema.md#devicepermissions) no es totalmente compatible actualmente con todos los clientes de escritorio.

## <a name="device-permissions"></a>Permisos de dispositivo

El acceso a los permisos de dispositivo de un usuario le permite crear experiencias mucho más enriqueciendo, por ejemplo:

* Grabar y compartir vídeos cortos
* Grabar notas breves de audio y guardarlas para más adelante
* Usar la información de ubicación del usuario para mostrar información relevante

Aunque el acceso a estas características es estándar en la mayoría de los exploradores web modernos, necesita que Teams sepa qué características desea usar mediante la actualización del manifiesto de la aplicación. Esto le permitirá solicitar permisos, del mismo modo que lo haría en un explorador, mientras la aplicación se ejecuta en el cliente de escritorio de Teams.

## <a name="manage-permissions"></a>Administrar permisos

# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abra Teams.
1. En la esquina superior derecha de la ventana, seleccione el icono de perfil.
1. Seleccione **Permisos**  ->  **de configuración en** el menú desplegable.
1. Elige la configuración que quieras.

![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Teams.
1. Vaya a **Configuración de** permisos  ->  **de aplicación.**
1. Selecciona la aplicación para la que necesitas elegir la configuración.
1. Elige la configuración que quieras.

![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a>Propiedades

Actualiza las aplicaciones agregando y especificando cuál de las cinco propiedades `manifest.json` te gustaría usar en la `devicePermissions` aplicación:

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
> Los medios también se usan para permisos de cámara en dispositivos móviles.

Cada propiedad te permitirá pedir al usuario que solicite su consentimiento:

| Propiedad      | Description   |
| --- | --- |
| Elementos multimedia         | permiso para usar la cámara, el micrófono, los altavoces y la galería multimedia de acceso |
| geolocalización   | permiso para devolver la ubicación del usuario      |
| notifications | permiso para enviar notificaciones de usuario      |
| midi          | permiso para enviar y recibir información midi de un instrumento música digital   |
| openExternal  | permiso para abrir vínculos en aplicaciones externas  |

## <a name="checking-permissions-from-your-tab"></a>Comprobar los permisos de la pestaña

Una vez que haya agregado al manifiesto de la aplicación, puede comprobar los permisos mediante la API de "permisos" de HTML5 sin causar `devicePermissions` ningún mensaje.

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

Para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos de dispositivo, debe aprovechar la API de HTML5 o Teams adecuada. 

Por ejemplo, para solicitar al usuario que acceda a su ubicación, debe llamar `getCurrentPosition` a:

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

Para usar la cámara en el escritorio o en la web, Teams mostrará un mensaje de permiso cuando llame `getUserMedia` a:

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

Para capturar la imagen en dispositivos móviles, Teams mobile pedirá permiso al `captureImage()` llamar:

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

Las notificaciones preguntarán al usuario cuando `requestPermission` llame:

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

Para usar la cámara o acceder a la galería de fotos, Teams mobile pedirá permiso al `selectMedia()` llamar:

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Para usar micrófono, Teams Mobile pedirá permiso cuando `selectMedia()` llame:

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, teams móvil solicitará permiso cuando `getLocation()` llame:

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[Escritorio](#tab/desktop)

![Mensaje de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

![Mensaje de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos en sesiones de inicio de sesión

Los permisos de dispositivo nativo se almacenan para cada sesión de inicio de sesión. Esto significa que si inicia sesión en otra instancia de Teams (por ejemplo, en otro equipo), los permisos de dispositivo de las sesiones anteriores no estarán disponibles. En su lugar, tendrá que volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión de inicio de sesión. También significa que, si cierra sesión en Teams (o cambia de espacio empresarial dentro de Teams), los permisos del dispositivo se eliminarán para esa sesión de inicio de sesión anterior. Ten esto en cuenta al desarrollar permisos de dispositivo nativo: las funcionalidades nativas que consientes son solo para la sesión de inicio _de sesión_ actual.
