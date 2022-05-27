---
title: Solicitar permisos de dispositivos para la aplicación de Microsoft Teams
description: Obtenga información sobre cómo actualizar el manifiesto de la aplicación y solicitar acceso a características nativas que implican el consentimiento del usuario, la ubicación, el código QR y el código de barras, la imagen, el audio y las funcionalidades de vídeo
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 624a079d7c72f77fac4109d11cde13974359884f
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757608"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Solicitar permisos de dispositivos para la aplicación de Microsoft Teams

Puede enriquecer la aplicación de Teams con funcionalidades nativas del dispositivo, como la cámara, el micrófono y la ubicación. Este documento le guiará sobre cómo solicitar el consentimiento del usuario y acceder a los permisos nativos del dispositivo.

> [!NOTE]
>
> * Para integrar las funcionalidades multimedia dentro de la aplicación móvil de Microsoft Teams, consulte [Integración de funcionalidades multimedia](mobile-camera-image-permissions.md).
> * Para integrar la funcionalidad de digitalización de código de barras o QR dentro de la aplicación móvil de Microsoft Teams, consulte [Integración de la funcionalidad de digitalización de código de barras o QR en Teams](qr-barcode-scanner-capability.md).
> * Para integrar las funcionalidades de ubicación dentro de la aplicación móvil de Microsoft Teams, consulte [Integración de las funcionalidades de ubicación](location-capability.md).

## <a name="native-device-permissions"></a>Permisos de dispositivos nativos

Deberá solicitar los permisos del dispositivo para acceder a las funcionalidades nativas del mismo. Los permisos del dispositivo funcionan de forma similar para todo lo que compone la aplicación, como pestañas, módulos de tareas o extensiones de mensajes. El usuario deberá ir a la página de permisos de la configuración de Teams para administrar los permisos del dispositivo.
Al acceder a las funcionalidades del dispositivo, podrá crear mejores experiencias en la plataforma de Teams, como:

* Capturar y ver imágenes.
* Escanear QR o códigos de barras.
* Grabar y compartir vídeos cortos.
* Grabar notas de audio y conservarlas para uso posterior.
* Usar la información de ubicación del usuario para mostrar información relevante.

> [!NOTE]
> * Actualmente, Teams no admite permisos de dispositivo para aplicaciones de varias ventanas, pestañas y el panel lateral de las reuniones.
> * Los permisos del dispositivo son diferentes en el explorador. Para obtener más información, vea [Permisos del dispositivo en el navegador](browser-device-permissions.md).

## <a name="access-device-permissions"></a>Acceso a los permisos del dispositivo

El [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) proporciona las herramientas necesarias para que la aplicación móvil de Teams acceda a los [permisos del dispositivo](#manage-permissions) del usuario y cree una experiencia más enriquecedora.

Aunque el acceso a estas características es estándar en los exploradores web modernos, deberá informar a Teams sobre las características que use actualizando el manifiesto de la aplicación. Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en el cliente de escritorio de Teams.

> [!NOTE]
> Actualmente, la compatibilidad de Microsoft Teams con las funcionalidades multimedia y del escáner de códigos QR solo está disponible para clientes móviles.

## <a name="manage-permissions"></a>Administrar permisos

Un usuario podrá administrar la configuración de los permisos del dispositivo en Teams seleccionando **Permitir** o **Denegar** permisos a aplicaciones específicas.

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Teams.
1. Vaya a **Configuración** > **Permisos de aplicaciones**.
1. Seleccione la aplicación para la que necesite elegir la configuración.
1. Seleccione la configuración deseada.

    ![Pantalla de configuración móvil de permisos del dispositivo](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abra la aplicación de Teams.
1. Seleccione el icono de perfil en la esquina superior derecha de la ventana.
1. Seleccione **Configuración** > **Permisos** en el menú desplegable.
1. Seleccione la configuración deseada.

   ![Pantalla de configuración de escritorio de permisos del dispositivo](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>Especificar los permisos

Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades siguientes usa en la aplicación:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Cada propiedad le permitirá solicitar al usuario su consentimiento:

| Propiedad      | Descripción   |
| --- | --- |
| medios         | Permiso para usar la cámara, el micrófono, los altavoces y acceder a la galería multimedia. |
| geolocalización   | Permiso para devolver la ubicación del usuario.      |
| notificaciones | Permiso para enviar las notificaciones del usuario.      |
| midi          | Permiso para enviar y recibir información de la interfaz digital de instrumentos musicales (MIDI) desde un instrumento musical digital.   |
| openExternal  | Permiso para abrir vínculos en aplicaciones externas.  |

## <a name="check-permissions-from-your-app"></a>Comprobación de permisos desde la aplicación

Después de agregar `devicePermissions` al manifiesto de la aplicación, compruebe los permisos mediante la **API de permisos HTML5** sin que se muestre un mensaje:

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

## <a name="use-teams-apis-to-get-device-permissions"></a>Use la API de Teams para obtener permisos de dispositivo

Aproveche HTML5 o la API de Teams para mostrar un mensaje y obtener el consentimiento para acceder a los permisos del dispositivo.

> [!IMPORTANT]
>
> * La compatibilidad con `camera`, `gallery` y `microphone` se habilita a través de la [**API selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Use la [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una única captura de imagen.
> * La compatibilidad con `location` se habilita a través de la [**API getLocation**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Debe usar `getLocation API` para la ubicación, ya que la API de geolocalización HTML5 no es totalmente compatible con el cliente de escritorio de Teams.

Por ejemplo:

* Para pedir al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()`:

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* Para pedir al usuario que acceda a su cámara en escritorio o web, debe llamar a `getUserMedia()`:

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* Para capturar la imagen en el móvil, Teams para móviles solicitará los permisos al llamar a `captureImage()`:

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

* Las notificaciones harán solicitudes al usuario cuando llame a `requestPermission()`:

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* Para usar la cámara o acceder a la galería de fotos, Teams para móviles pedirá permiso al llamar a `selectMedia()`:

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

* Para usar el micrófono, Teams para móviles solicitará permiso al llamar a `selectMedia()`:

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

* Para pedir al usuario que comparta la ubicación en la interfaz del mapa, Teams para móviles pedirá permiso al llamar a `getLocation()`:

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[Móvil](#tab/mobile)

   ![Pestañas de solicitudes de permisos de dispositivos móviles](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[Escritorio](#tab/desktop)

   ![Pestañas de solicitudes de permisos de dispositivos de escritorio](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos entre inicios de sesión

Los permisos del dispositivo se almacenan para cada inicio de sesión. Esto significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no están disponibles. Por lo tanto, deberá volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión. También significa que, si cierra la sesión de Teams o cambia de inquilino en Teams, los permisos del dispositivo se eliminarán del inicio de sesión anterior.  

> [!NOTE]
> Cuando de su consentimiento a los permisos del dispositivo nativo, solo será válido para el inicio de sesión _en curso_.

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de ejemplo** | **Descripción** | **Node.js** |
|---------------|--------------|--------|
|Permisos de dispositivo | Uso de la aplicación de ejemplo de pestañas de Microsoft Teams para mostrar los permisos del dispositivo |  [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>Consulte también

* [Permisos de dispositivo para el explorador](browser-device-permissions.md)
* [Integrar funcionalidades multimedia en Teams](mobile-camera-image-permissions.md)
* [Integrar la funcionalidad de escáner de código QR o código de barras en Teams](qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
