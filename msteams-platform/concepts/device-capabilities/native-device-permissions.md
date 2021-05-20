---
title: Solicitar permisos de dispositivo para la aplicación Microsoft Teams
keywords: permisos de capacidades de aplicaciones de equipos
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 34f84285dc883cc474cf1720c42b1699f76c6653
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566183"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Solicitar permisos de dispositivo para la aplicación Microsoft Teams

Puede enriquecer la aplicación Teams con capacidades de dispositivo nativas, como cámara, micrófono y ubicación. Este documento le guía sobre cómo solicitar el consentimiento del usuario y acceder a los permisos del dispositivo nativo.

> [!NOTE]
> * Para integrar las capacidades de medios dentro de la aplicación móvil Microsoft Teams, consulte [Integrar capacidades de medios.](mobile-camera-image-permissions.md)
> * Para integrar la capacidad del escáner QR o de código de barras dentro de su aplicación móvil Microsoft Teams, consulte [Integrar la capacidad del escáner QR o de código de barras en Teams.](qr-barcode-scanner-capability.md)
> * Para integrar capacidades de ubicación dentro de la aplicación móvil Microsoft Teams, consulte [Integrar capacidades de ubicación.](location-capability.md)

## <a name="native-device-permissions"></a>Permisos de dispositivo nativo

Debe solicitar los permisos del dispositivo para acceder a las capacidades de dispositivos nativos. Los permisos de dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería. El usuario debe ir a la página de permisos en Teams configuración para administrar los permisos del dispositivo.
Al acceder a las capacidades del dispositivo, puede crear experiencias más enriquecidas en la plataforma Teams, como:
* Capturar y ver imágenes.
* Escanea QR o código de barras.
* Graba y comparte vídeos cortos.
* Graba notas de audio y guárdalas para su uso posterior.
* Utilice la información de ubicación del usuario para mostrar la información relevante.

## <a name="access-device-permissions"></a>Permisos de dispositivo de acceso

El [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) proporciona las herramientas necesarias para que la aplicación móvil Teams acceda a los permisos de [dispositivo](#manage-permissions) del usuario y cree una experiencia más enriquecida.

Aunque el acceso a estas características es estándar en los navegadores web modernos, debe informar a Teams sobre las características que usa actualizando el manifiesto de la aplicación. Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en el cliente de escritorio Teams.

> [!NOTE] 
> Actualmente, Microsoft Teams soporte para capacidades de medios y la capacidad del escáner de código de barras QR solo está disponible para clientes móviles.

## <a name="manage-permissions"></a>Administrar permisos

Un usuario puede administrar permisos de dispositivo en Teams configuración seleccionando **Permitir** o **Denegar** permisos a aplicaciones específicas.
 
# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abre la aplicación Teams.
1. Seleccione el icono de perfil en la esquina superior derecha de la ventana.
1. Seleccione **Configuración**  >  **Permisos** en el menú desplegable.
1. Seleccione la configuración deseada.

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Teams.
1. Vaya a **Configuración**  >  **Permisos de aplicación**.
1. Seleccione la aplicación para la que debe elegir la configuración.
1. Seleccione la configuración deseada.

    ![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Especificar permisos

Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades que usa en la aplicación:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Cada propiedad le permite solicitar al usuario que pida su consentimiento:

| Propiedad      | Descripción   |
| --- | --- |
| Elementos multimedia         | Permiso para usar la cámara, el micrófono, los altavoces y la galería de medios de acceso. |
| geolocalización   | Permiso para devolver la ubicación del usuario.      |
| notificaciones | Permiso para enviar las notificaciones de usuario.      |
| midi          | Permiso para enviar y recibir información de la Interfaz Digital de Instrumento Musical (MIDI) de un instrumento musical digital.   |
| openExternal  | Permiso para abrir vínculos en aplicaciones externas.  |

## <a name="check-permissions-from-your-app"></a>Compruebe los permisos de la aplicación

Después de agregar `devicePermissions` al manifiesto de la aplicación, compruebe los permisos mediante la API de permisos **HTML5** sin provocar un mensaje:

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

## <a name="use-teams-apis-to-get-device-permissions"></a>Use Teams API para obtener permisos de dispositivo

Aproveche html5 o Teams API adecuados para mostrar un mensaje para obtener consentimiento para acceder a los permisos del dispositivo.

> [!IMPORTANT]
> * Compatibilidad con `camera` , y está habilitado a través de `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Utilice [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una sola captura de imagen.
> * La compatibilidad `location` con la compatibilidad con [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)está habilitada. Debe usar esto `getLocation API` para la ubicación, ya que la API de geolocalización HTML5 no es totalmente compatible con Teams cliente de escritorio.

Por ejemplo:
 * Para solicitar al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()` :

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Para pedir al usuario que acceda a su cámara en el escritorio o la web debe llamar `getUserMedia()` a:

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Para capturar la imagen en el móvil, Teams móvil pide permiso cuando se llama `captureImage()` a:

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * Las notificaciones le preguntarán al usuario cuando `requestPermission()` llame:

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Para utilizar la cámara o acceder a la galería de fotos, Teams móvil pide permiso cuando se `selectMedia()` llama:

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Para utilizar el micrófono, Teams móvil pide permiso cuando se `selectMedia()` llama:

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Para pedir al usuario que comparta la ubicación en la interfaz del mapa, Teams móvil pide permiso al `getLocation()` llamar:

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Escritorio](#tab/desktop)

   ![Solicitud de permisos de dispositivo de escritorio en pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

   ![Solicitud de permisos de dispositivos móviles en pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos en las sesiones de inicio de sesión

Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión. Esto significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no están disponibles. Por lo tanto, debe volver a dar su consentimiento a los permisos de dispositivo para la nueva sesión. También significa que, si cierra sesión en Teams o cambia de inquilino en Teams, los permisos de dispositivo se eliminan de la sesión de inicio de sesión anterior.  

> [!NOTE]
> Cuando acepta los permisos de dispositivo nativo, solo es válido para la sesión de inicio de sesión _actual._

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Integrar capacidades de medios en Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Integrar la capacidad del escáner QR o de código de barras en Teams](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Integrar capacidades de ubicación en Teams](location-capability.md)
