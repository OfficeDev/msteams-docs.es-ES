---
title: Solicitar permisos de dispositivo para la aplicación de Microsoft Teams
keywords: Funcionalidades de aplicaciones de teams permisos de dispositivo examen nativo qr imagen de vídeo de audio
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario, como las funcionalidades de escaneo qr, código de barras, imagen, audio y vídeo
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 5269aed130714bc9afbe97b170d955d79d79abc8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103309"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Solicitar permisos de dispositivo para la aplicación de Microsoft Teams

Puede enriquecer la aplicación de Teams con funcionalidades nativas de dispositivo, como cámara, micrófono y ubicación. Este documento le guía sobre cómo solicitar el consentimiento del usuario y acceder a los permisos de dispositivo nativo.

> [!NOTE]
>
> * Para integrar las funcionalidades multimedia dentro de la aplicación móvil de Microsoft Teams, consulte [Integración de funcionalidades multimedia](mobile-camera-image-permissions.md).
> * Para integrar la funcionalidad qr o escáner de códigos de barras dentro de su aplicación móvil Microsoft Teams, consulte [Integración de la funcionalidad qr o escáner de códigos de barras en Teams](qr-barcode-scanner-capability.md).
> * Para integrar las funcionalidades de ubicación dentro de la aplicación móvil Microsoft Teams, consulte [Integración de funcionalidades de ubicación](location-capability.md).

## <a name="native-device-permissions"></a>Permisos de dispositivos nativos

Debe solicitar los permisos del dispositivo para acceder a las funcionalidades nativas del dispositivo. Los permisos de dispositivo funcionan de forma similar para todas las construcciones de aplicación, como pestañas, módulos de tareas o extensiones de mensaje. El usuario debe ir a la página permisos de Teams configuración para administrar los permisos del dispositivo.
Al acceder a las funcionalidades del dispositivo, puede crear experiencias más enriquecidas en la plataforma Teams, como:

* Captura y visualización de imágenes.
* Escanear QR o código de barras.
* Grabar y compartir vídeos cortos.
* Grabe notas de audio y guárdelas para su uso posterior.
* Use la información de ubicación del usuario para mostrar la información pertinente.

> [!NOTE]
> * Actualmente, Teams no admite permisos de dispositivo para aplicaciones de varias ventanas, pestañas y el panel lateral de la reunión.
> * Los permisos de dispositivo son diferentes en el explorador. Para obtener más información, consulte [permisos de dispositivo del explorador](browser-device-permissions.md).

## <a name="access-device-permissions"></a>Permisos de acceso al dispositivo

El [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) proporciona las herramientas necesarias para que la aplicación móvil de Teams acceda a los [permisos de dispositivo](#manage-permissions) del usuario y cree una experiencia más enriquecida.

Aunque el acceso a estas características es estándar en los exploradores web modernos, debes informar a Teams sobre las características que usas actualizando el manifiesto de la aplicación. Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en el cliente de escritorio de Teams.

> [!NOTE]
> Actualmente, Microsoft Teams compatibilidad con las funcionalidades multimedia y la capacidad del escáner de códigos QR solo está disponible para clientes móviles.

## <a name="manage-permissions"></a>Administrar permisos

Un usuario puede administrar los permisos de dispositivo en Teams configuración seleccionando **Permitir** o **Denegar** permisos a aplicaciones específicas.

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Teams.
1. Vaya a **permisos de Configuración** >  **App**.
1. Seleccione la aplicación para la que necesita elegir la configuración.
1. Seleccione la configuración deseada.

    ![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abra la aplicación Teams.
1. Seleccione el icono de perfil en la esquina superior derecha de la ventana.
1. Seleccione **Configuración** >  **Permissions** en el menú desplegable.
1. Seleccione la configuración deseada.

   ![Pantalla de configuración de escritorio de permisos de dispositivo](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>Especificar permisos

Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades siguientes se usan en la aplicación:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Cada propiedad le permite solicitar al usuario su consentimiento:

| Propiedad      | Descripción   |
| --- | --- |
| Medio         | Permiso para usar la cámara, el micrófono, los altavoces y acceder a la galería multimedia. |
| Geolocalización   | Permiso para devolver la ubicación del usuario.      |
| Notificaciones | Permiso para enviar las notificaciones de usuario.      |
| Midi          | Permiso para enviar y recibir información de la Interfaz Digital de Instrumento Musical (MIDI) desde un instrumento musical digital.   |
| openExternal  | Permiso para abrir vínculos en aplicaciones externas.  |

## <a name="check-permissions-from-your-app"></a>Comprobación de permisos desde la aplicación

Después de agregar `devicePermissions` al manifiesto de la aplicación, compruebe los permisos mediante la **API de permisos HTML5** sin provocar un mensaje:

``` JavaScript
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

## <a name="use-teams-apis-to-get-device-permissions"></a>Uso de Teams API para obtener permisos de dispositivo

Aproveche la API html5 o Teams adecuada para mostrar un mensaje para obtener el consentimiento para acceder a los permisos del dispositivo.

> [!IMPORTANT]
>
> * La compatibilidad con `camera`, `gallery`y `microphone` se habilita a través de [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una única captura de imagen.
> * La compatibilidad con `location` está habilitada a través de [**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Debe usarlo `getLocation API` para la ubicación, ya que la API de geolocalización HTML5 no es totalmente compatible con Teams cliente de escritorio.

Por ejemplo:

* Para pedir al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()`:

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* Para pedir al usuario que acceda a su cámara en escritorio o web, debe llamar a `getUserMedia()`:

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* Para capturar la imagen en el móvil, Teams móvil solicita permiso al llamar a `captureImage()`:

    ```JavaScript
            function captureImage() {
            microsoftTeams.media.captureImage((error, files) => {
                // If there's any error, an alert shows the error message/code
                if (error) {
                    if (error.message) {
                        alert(" ErrorCode: " + error.errorCode + error.message);
                    } else {
                        alert(" ErrorCode: " + error.errorCode);
                    }
                } else if (files) {
                    image = files[0].content;
                    // Adding this image string in src attr of image tag will display the image on web page.
                    let imageString = "data:" + item.mimeType + ";base64," + image;
                }
            });
        } 
    ```

* Las notificaciones le pedirán al usuario cuando llame a `requestPermission()`:

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* Para usar la cámara o acceder a la galería de fotos, Teams móvil pide permiso al llamar a `selectMedia()`:

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia(mediaInput, (error, attachments) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         } else if (attachments) {
             // creating image array which contains image string for all attached images. 
             const imageArray = attachments.map((item, index) => {
                 return ("data:" + item.mimeType + ";base64," + item.preview)
             })
         }
     });
    } 
  ```

* Para usar el micrófono, Teams móvil solicita permiso al llamar a `selectMedia()`:

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         }

         if (attachments) {
             // taking the first attachment  
             let audioResult = attachments[0];

             // setting audio string which can be used in Video tag
             let audioData = "data:" + audioResult.mimeType + ";base64," + audioResult.preview
         }
     });
     }
    ```

* Para pedir al usuario que comparta la ubicación en la interfaz de mapa, Teams móvil pide permiso al llamar a `getLocation()`:

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[Móvil](#tab/mobile)

   ![Símbolo del sistema de permisos de dispositivos móviles con pestañas](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[Escritorio](#tab/desktop)

   ![Símbolo del sistema de permisos del dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos entre sesiones de inicio de sesión

Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión. Esto significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no están disponibles. Por lo tanto, debe volver a dar su consentimiento a los permisos de dispositivo para la nueva sesión. También significa que, si cierra la sesión de Teams o cambia de inquilino en Teams, los permisos del dispositivo se eliminan de la sesión de inicio de sesión anterior.  

> [!NOTE]
> Cuando da su consentimiento a los permisos de dispositivo nativo, solo es válido para la sesión de inicio de sesión _actual_ .

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de ejemplo** | **Descripción** | **Node.js** |
|---------------|--------------|--------|
|Permisos de dispositivo | Uso de Microsoft Teams aplicación de ejemplo de pestaña para mostrar los permisos del dispositivo |  [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>Consulte también

* [Permisos de dispositivo para el explorador](browser-device-permissions.md)
* [Integrar funcionalidades multimedia en Teams](mobile-camera-image-permissions.md)
* [Integración de la funcionalidad qr o escáner de códigos de barras en Teams](qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
