---
title: Solicitar permisos de dispositivo para la aplicación de Microsoft Teams
keywords: Permisos de capacidades de aplicaciones de teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
ms.topic: how-to
ms.openlocfilehash: 0343754eacbb6088a3e44fa5df8ec90e3b10b076
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231613"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Solicitar permisos de dispositivo para la aplicación de Microsoft Teams

Puede enriquecer su aplicación de Teams con funcionalidades de dispositivo nativo, como cámara, micrófono y ubicación. Este documento le guiará sobre cómo solicitar el consentimiento del usuario y obtener acceso a los permisos de dispositivo nativo.

> [!NOTE]
> Para integrar las capacidades multimedia dentro de la aplicación móvil de Microsoft Teams, vea [Integrar capacidades multimedia.](mobile-camera-image-permissions.md)

## <a name="native-device-permissions"></a>Permisos de dispositivo nativo

Debes solicitar los permisos del dispositivo para acceder a las funcionalidades de dispositivo nativo. Los permisos de dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería. El usuario debe ir a la página de permisos en la configuración de Teams para administrar los permisos de dispositivo.
Al acceder a las capacidades del dispositivo, puede crear experiencias más completas en la plataforma de Teams, como:
* Capturar y ver imágenes.
* Grabar y compartir vídeos cortos.
* Grabe los memos de audio y guárdelos para usarlos más adelante.
* Use la información de ubicación del usuario para mostrar información relevante.

## <a name="access-device-permissions"></a>Permisos de dispositivo de acceso

El SDK del cliente [de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams proporciona las herramientas necesarias para que la aplicación móvil de Teams tenga acceso a los permisos de dispositivo [del](#manage-permissions) usuario y cree una experiencia más completa.

Aunque el acceso a estas características es estándar en exploradores web modernos, debe informar a Teams sobre las características que usa actualizando el manifiesto de la aplicación. Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en el cliente de escritorio de Teams.

> [!NOTE] 
> Actualmente, la compatibilidad de Microsoft Teams con las funcionalidades multimedia solo está disponible para clientes móviles.

## <a name="manage-permissions"></a>Administrar permisos

Un usuario puede administrar los permisos de dispositivo en la configuración de Teams **seleccionando Permitir** o denegar **permisos** a aplicaciones específicas.
 
# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abra su aplicación de Teams.
1. Seleccione el icono de perfil en la esquina superior derecha de la ventana.
1. Seleccione **Permisos**  >  **de configuración** en el menú desplegable.
1. Selecciona la configuración que quieras.

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Teams.
1. Vaya a **Configuración de** permisos  >  **de aplicación.**
1. Selecciona la aplicación para la que necesitas elegir la configuración.
1. Selecciona la configuración que quieras.

    ![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Especificar permisos

Actualiza las aplicaciones `manifest.json` agregando y especificando cuál de las cinco propiedades que `devicePermissions` usas en la aplicación:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Cada propiedad le permite pedir al usuario que solicite su consentimiento:

| Propiedad      | Descripción   |
| --- | --- |
| medios         | Permiso para usar la cámara, el micrófono, los altavoces y el acceso a la galería multimedia. |
| geolocalización   | Permiso para devolver la ubicación del usuario.      |
| notifications | Permiso para enviar notificaciones de usuario.      |
| midi          | Permiso para enviar y recibir información de interfaz digital de instrumentos música (MIDI) de un instrumento música digital.   |
| openExternal  | Permiso para abrir vínculos en aplicaciones externas.  |

## <a name="check-permissions-from-your-app"></a>Comprobar los permisos de la aplicación

Después de agregar al manifiesto de la aplicación, compruebe los permisos mediante la API de permisos `devicePermissions` **de HTML5** sin causar un mensaje:

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

## <a name="use-teams-apis-to-get-device-permissions"></a>Usar las API de Teams para obtener permisos de dispositivo

Aproveche la API de HTML5 o Teams adecuada para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos de dispositivo.

> [!IMPORTANT]
> * Compatibilidad con `camera` , y se habilita a través de la API `gallery` `microphone` [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Usa [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una captura de imagen única.
> * La compatibilidad con `location` se habilita a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Debe usarlo para la ubicación, ya que la API de geolocalización de HTML5 actualmente no es totalmente compatible con el cliente `getLocation API` de escritorio de Teams.

Por ejemplo:
 * Para solicitar al usuario que acceda a su ubicación, debe llamar `getCurrentPosition()` a:

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Para solicitar al usuario que acceda a su cámara en el escritorio o en la web, debes llamar `getUserMedia()` a:

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Para capturar la imagen en dispositivos móviles, Teams Mobile pide permiso al `captureImage()` llamar:

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * Las notificaciones preguntarán al usuario cuando `requestPermission()` llame:

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Para usar la cámara o acceder a la galería de fotos, teams móvil pide permiso al `selectMedia()` llamar:

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Para usar el micrófono, el móvil de Teams pide permiso al `selectMedia()` llamar:

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, Teams Mobile pide permiso al `getLocation()` llamar:

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Escritorio](#tab/desktop)

   ![Mensaje de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

   ![Mensaje de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos en sesiones de inicio de sesión

Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión. Esto significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no estarán disponibles. Por lo tanto, debe volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión. También significa que, si sale de Teams o cambia de inquilino en Teams, los permisos de su dispositivo se eliminan de la sesión de inicio de sesión anterior.  

> [!NOTE]
> Cuando da su consentimiento a los permisos de dispositivo nativo, solo es válido para la sesión de inicio _de sesión_ actual.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Integrar capacidades multimedia en Teams](mobile-camera-image-permissions.md)
