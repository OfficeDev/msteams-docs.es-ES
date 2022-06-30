---
title: Solicitar permisos de dispositivos para la aplicación de Microsoft Teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que requieren el consentimiento del usuario, como las funcionalidades de escaneo qr, código de barras, imagen, audio y vídeo
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: e5ae6d2f5dda0d173e336b81d696de8847f591a2
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2022
ms.locfileid: "66557718"
---
# <a name="request-device-permissions-for-your-teams-app"></a>Solicitud de permisos de dispositivo para la aplicación de Teams

Puede enriquecer la aplicación de Teams con funcionalidades nativas del dispositivo, como la cámara, el micrófono y la ubicación. Este documento le guiará sobre cómo solicitar el consentimiento del usuario y acceder a los permisos nativos del dispositivo.

> [!NOTE]
>
> * Para integrar las funcionalidades multimedia en el cliente web, el escritorio y el móvil de Microsoft Teams, consulte [Integración de funcionalidades multimedia](media-capabilities.md).
> * Para integrar la funcionalidad de digitalización de código de barras o QR dentro de la aplicación móvil de Microsoft Teams, consulte [Integración de la funcionalidad de digitalización de código de barras o QR en Teams](qr-barcode-scanner-capability.md).
> * Para integrar las funcionalidades de ubicación en el cliente web, el escritorio y el móvil de Teams, consulte [Integración de funcionalidades de ubicación](location-capability.md).

## <a name="native-device-permissions"></a>Permisos de dispositivos nativos

Deberá solicitar los permisos del dispositivo para acceder a las funcionalidades nativas del mismo. Los permisos de dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería. El usuario deberá ir a la página de permisos de la configuración de Teams para administrar los permisos del dispositivo. Puede crear experiencias más enriquecidas en la plataforma Teams con la ayuda de funcionalidades de dispositivo, como: Debe solicitar los permisos del dispositivo para acceder a las funcionalidades nativas del dispositivo. Los permisos del dispositivo funcionan de forma similar para todo lo que compone la aplicación, como pestañas, módulos de tareas o extensiones de mensajes. El usuario deberá ir a la página de permisos de la configuración de Teams para administrar los permisos del dispositivo.
Al acceder a las funcionalidades del dispositivo, podrá crear mejores experiencias en la plataforma de Teams, como:

* Captura y visualización de imágenes
* Escanear QR o código de barras
* Grabación y uso compartido de vídeos cortos
* Grabar notas de audio y guardarlas para su uso posterior
* Usar la información de ubicación del usuario para mostrar la información pertinente

> [!NOTE]
>
> * Actualmente, Teams no admite permisos de dispositivo para aplicaciones de varias ventanas, pestañas y el panel lateral de las reuniones.
> * Los permisos del dispositivo son diferentes en el explorador. Para obtener más información, vea [Permisos de dispositivo en el navegador](browser-device-permissions.md).
> * Actualmente, Teams admite la funcionalidad de escáner de códigos de barras QR solo está disponible para clientes móviles.

## <a name="access-device-permissions"></a>Acceso a los permisos del dispositivo

El [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) proporciona las herramientas necesarias para que la aplicación de Teams acceda a los [permisos de dispositivo](#manage-permissions) del usuario y cree una experiencia más enriquecida.

Aunque el acceso a estas características es estándar en los exploradores web modernos, deberá informar a Teams sobre las características que use actualizando el manifiesto de la aplicación. Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en el escritorio de Teams.

## <a name="manage-permissions"></a>Administrar permisos

Un usuario podrá administrar la configuración de los permisos del dispositivo en Teams seleccionando **Permitir** o **Denegar** permisos a aplicaciones específicas.

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Teams.
1. Vaya a **Configuración** > **Permisos de aplicaciones**.
1. Seleccione la aplicación para la que necesite elegir la configuración.
1. Seleccione la configuración deseada.

    <!-- ![Device permissions mobile settings screen](../../assets/images/tabs/MobilePermissions.png) -->

    :::image type="content" source="~/assets/images/tabs/MobilePermissions.png" alt-text="Permisos móviles.":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abra la aplicación de Teams.
1. Seleccione el icono de perfil en la esquina superior derecha de la ventana.
1. Seleccione **Configuración** > **Permisos** en el menú desplegable.
1. Seleccione la configuración deseada.

   <!-- ![Device permissions desktop settings screen](~/assets/images/tabs/device-permissions.png) -->

   :::image type="content" source="~/assets/images/tabs/device-permissions.png" alt-text="Permiso de dispositivo.":::

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

Cada propiedad le permite pedir a los usuarios su consentimiento:

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

Aproveche la API de Teams o HTML5 adecuada para mostrar un mensaje para obtener el consentimiento para acceder a los permisos del dispositivo.

> [!IMPORTANT]
>
> * La compatibilidad con `camera`, `gallery` y `microphone` se habilita a través de la [**API selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Use la [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una única captura de imagen.
> * La compatibilidad con `location` se habilita a través de la [**API getLocation**](/javascript/api/@microsoft/teams-js/microsoftteams.location?.view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Debe usarlo `getLocation API` para la ubicación, ya que la API de geolocalización HTML5 no es totalmente compatible en el escritorio de Teams.

Por ejemplo:

* Para pedir al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()`:

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* Para pedir al usuario que acceda a su cámara en escritorio o web, debe llamar a `getUserMedia()`:

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* Para capturar las imágenes en dispositivos móviles, Teams Mobile solicita permiso al llamar a `captureImage()`:

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

* Las notificaciones solicitan al usuario que llame a `requestPermission()`:

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* Para usar la cámara o acceder a la galería de fotos, la aplicación Teams pide permiso al llamar a `selectMedia()`:

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

* Para pedir al usuario que comparta la ubicación en la interfaz de mapa, la aplicación Teams pide permiso al llamar a `getLocation()`:

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[Móvil](#tab/mobile)

   <!-- ![Tabs mobile device permissions prompt](../../assets/images/tabs/MobileLocationPermission.png) -->

   :::image type="content" source="~/assets/images/tabs/MobileLocationPermission.png" alt-text="Permiso de ubicación móvil.":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

   <!-- ![Tabs desktop device permissions prompt](~/assets/images/tabs/device-permissions-prompt.png) -->

   :::image type="content" source="~/assets/images/tabs/device-permissions-prompt.png" alt-text="Permiso de dispositivo en el escritorio.":::

---

## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos entre inicios de sesión

Los permisos del dispositivo se almacenan para cada inicio de sesión. Esto significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos del dispositivo de las sesiones anteriores no estarán disponibles. Por lo tanto, deberá volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión. También significa que, si cierra la sesión de Teams o cambia de inquilino en Teams, los permisos del dispositivo se eliminarán del inicio de sesión anterior.  

> [!NOTE]
> Cuando de su consentimiento a los permisos del dispositivo nativo, solo será válido para el inicio de sesión _en curso_.

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de ejemplo** | **Descripción** | **Node.js** |
|---------------|--------------|--------|
|Permisos de dispositivo | Uso de la aplicación de ejemplo de pestañas de Microsoft Teams para mostrar los permisos del dispositivo |  [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>Consulte también

* [Permisos de dispositivo para el explorador](browser-device-permissions.md)
* [Integrar capacidades multimedia](media-capabilities.md)
* [Integrar la funcionalidad de escáner de código QR o código de barras en Teams](qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
