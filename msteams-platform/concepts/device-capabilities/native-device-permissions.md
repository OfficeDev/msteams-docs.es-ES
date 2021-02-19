---
title: Solicitar permisos de dispositivo para la aplicación de Microsoft Teams
keywords: permisos de capacidades de aplicaciones de teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
ms.topic: how-to
ms.openlocfilehash: 60c28e1170e8bbdf664145bde7f7de585bd55a45
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294750"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Solicitar permisos de dispositivo para la aplicación de Microsoft Teams

Puedes enriquecer la aplicación de Teams con capacidades de dispositivo nativas, como cámara, micrófono y ubicación. Este documento le guía sobre cómo solicitar el consentimiento del usuario y obtener acceso a los permisos de dispositivo nativo.

> [!NOTE]
> * Para integrar las funcionalidades multimedia dentro de la aplicación móvil de Microsoft Teams, consulta [Integrar capacidades multimedia.](mobile-camera-image-permissions.md)
> * Para integrar la funcionalidad de escáner qr o de código de barras en la aplicación móvil de Microsoft Teams, consulta Integrar la funcionalidad [del escáner de códigos](qr-barcode-scanner-capability.md) de barras o QR en Teams

## <a name="native-device-permissions"></a>Permisos de dispositivo nativo

Debes solicitar los permisos del dispositivo para tener acceso a las funcionalidades nativas del dispositivo. Los permisos del dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería. El usuario debe ir a la página de permisos de la configuración de Teams para administrar los permisos de dispositivo.
Al acceder a las capacidades del dispositivo, puedes crear experiencias más completas en la plataforma de Teams, como:
* Capturar y ver imágenes.
* Digitalizar QR o código de barras.
* Grabar y compartir vídeos cortos.
* Grabe notas de audio y guárdelas para su uso posterior.
* Use la información de ubicación del usuario para mostrar información relevante.

## <a name="access-device-permissions"></a>Permisos de dispositivo de acceso

El [SDK de cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams proporciona las herramientas necesarias para que la aplicación móvil de Teams tenga acceso a los permisos de dispositivo [del](#manage-permissions) usuario y genere una experiencia más enriquecible.

Aunque el acceso a estas características es estándar en los exploradores web modernos, debes informar a Teams sobre las características que usas actualizando el manifiesto de la aplicación. Esta actualización te permite pedir permisos mientras la aplicación se ejecuta en el cliente de escritorio de Teams.

> [!NOTE] 
> Actualmente, la compatibilidad de Microsoft Teams con las capacidades multimedia y la funcionalidad del escáner de códigos de barras QR solo está disponible para clientes móviles.

## <a name="manage-permissions"></a>Administrar permisos

Un usuario puede administrar los permisos de dispositivo en la configuración de Teams seleccionando **Permitir** o **denegar** permisos a aplicaciones específicas.
 
# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abre la aplicación de Teams.
1. Seleccione el icono de perfil en la esquina superior derecha de la ventana.
1. Seleccione **Configuración**  >  **Permisos en** el menú desplegable.
1. Seleccione la configuración que desee.

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Teams.
1. Vaya a **Configuración**  >  **Permisos de aplicación**.
1. Selecciona la aplicación para la que necesitas elegir la configuración.
1. Seleccione la configuración que desee.

    ![Pantalla de configuración móvil de permisos de dispositivos](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Especificar permisos

Actualiza las aplicaciones agregando y especificando cuáles de las cinco propiedades `manifest.json` `devicePermissions` que usas en la aplicación:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Cada propiedad le permite pedir al usuario que pida su consentimiento:

| Propiedad      | Descripción   |
| --- | --- |
| Elementos multimedia         | Permiso para usar la cámara, el micrófono, los altavoces y la galería multimedia de acceso. |
| geolocalización   | Permiso para devolver la ubicación del usuario.      |
| notificaciones | Permiso para enviar las notificaciones de usuario.      |
| midi          | Permiso para enviar y recibir información de interfaz digital de instrumentos musicales (MIDI) desde un instrumento musical digital.   |
| openExternal  | Permiso para abrir vínculos en aplicaciones externas.  |

## <a name="check-permissions-from-your-app"></a>Comprobar los permisos de la aplicación

Después de agregar al manifiesto de la aplicación, comprueba los permisos mediante la API de permisos `devicePermissions` **HTML5** sin causar un mensaje:

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

Aproveche la API de HTML5 o Teams apropiada para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos del dispositivo.

> [!IMPORTANT]
> * Compatibilidad con `camera` , y está habilitada a través de `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Use [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una única captura de imagen.
> * La compatibilidad `location` con está habilitada a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Debe usarlo para la ubicación, ya que la API de `getLocation API` geolocalización de HTML5 actualmente no es totalmente compatible con el cliente de escritorio de Teams.

Por ejemplo:
 * Para solicitar al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()` :

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Para solicitar al usuario que acceda a su cámara en el escritorio o la web, debe llamar a `getUserMedia()` :

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Para capturar la imagen en el móvil, Teams mobile pide permiso al llamar `captureImage()` a :

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * Las notificaciones le pedirán al usuario que `requestPermission()` llame:

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Para usar la cámara o la galería de fotos de acceso, Teams mobile pide permiso al llamar a `selectMedia()` :

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Para usar el micrófono, Teams mobile pide permiso al llamar `selectMedia()` a :

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, Teams mobile pide permiso al llamar a `getLocation()` :

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Escritorio](#tab/desktop)

   ![Símbolo del sistema de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

   ![Símbolo del sistema de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos en sesiones de inicio de sesión

Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión. Significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no estarán disponibles. Por lo tanto, debe volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión. También significa que, si inicias sesión en Teams o cambias de inquilinos en Teams, los permisos del dispositivo se eliminan de la sesión de inicio de sesión anterior.  

> [!NOTE]
> Cuando da su consentimiento a los permisos de dispositivo nativo, solo es válido para la _sesión de_ inicio de sesión actual.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Integrar capacidades multimedia en Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Integrar la funcionalidad del escáner de códigos DE BARRAS o QR en Teams](qr-barcode-scanner-capability.md)
