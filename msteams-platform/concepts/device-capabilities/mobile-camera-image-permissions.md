---
title: Integrar capacidades multimedia
author: Rajeshwari-v
description: Cómo usar el SDK de cliente de JavaScript de Teams para habilitar funcionalidades multimedia
keywords: Medios de permisos de dispositivo nativos de las capacidades de micrófono de imagen de cámara
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 98b4cd80de20671d45f198e89e1c273e88b36a87
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058365"
---
# <a name="integrate-media-capabilities"></a>Integrar capacidades multimedia 

Este documento le guía sobre cómo integrar funcionalidades multimedia. Esta integración combina las capacidades nativas del dispositivo, como la **cámara** y **el micrófono** con la plataforma de Teams.  

Puedes usar el [SDK de cliente javaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)de Microsoft Teams, que proporciona las herramientas necesarias para que la aplicación tenga acceso a los permisos de dispositivo de un [usuario.](native-device-permissions.md) Usa las API de funcionalidad multimedia adecuadas para integrar  las  capacidades nativas del dispositivo, como la cámara y el micrófono con la plataforma teams dentro de la aplicación móvil de Microsoft Teams, y crea una experiencia más enriquecte. 

## <a name="advantage-of-integrating-media-capabilities"></a>Ventaja de integrar capacidades multimedia

La principal ventaja de integrar las capacidades de dispositivo en tus aplicaciones de Teams es que aprovecha los controles nativos de Teams para proporcionar una experiencia enriqueciendo e inmersiva a los usuarios.
Para integrar las funcionalidades multimedia, debes actualizar el archivo de manifiesto de la aplicación y llamar a las API de funcionalidad multimedia. 

Para una integración eficaz, debe tener una buena comprensión de los fragmentos de código para llamar a las API [correspondientes,](#code-snippets) lo que le permite usar funcionalidades multimedia nativas.

Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la aplicación de Teams.

> [!NOTE] 
> Actualmente, la compatibilidad de Microsoft Teams con las capacidades multimedia solo está disponible para clientes móviles.

## <a name="update-manifest"></a>Manifiesto de actualización

Actualice la aplicación de Teams [manifest.jsarchivo](../../resources/schema/manifest-schema.md#devicepermissions) agregando la propiedad `devicePermissions` y especificando `media` . Permite a la aplicación solicitar los permisos necesarios a  los usuarios antes de empezar a usar la cámara para capturar  la imagen, abrir la galería para seleccionar una imagen para enviar como datos adjuntos o usar el micrófono para grabar la conversación.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> El **símbolo del sistema Solicitar permisos** se muestra automáticamente cuando se inicia una API de Teams relevante. Para obtener más información, consulta [Solicitar permisos de dispositivo](native-device-permissions.md).

## <a name="media-capability-apis"></a>API de funcionalidad multimedia

Las [API selectMedia,](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)y [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) permiten usar las funciones multimedia nativas de la siguiente manera:

* Usa el micrófono **nativo para** permitir a los usuarios grabar **audio** (grabar 10 minutos de conversación) desde el dispositivo.
* Usa el **control de cámara** nativa para permitir a los usuarios capturar y adjuntar **imágenes** sobre la marcha.
* Usa la compatibilidad **de galería nativa** para permitir a los usuarios seleccionar imágenes del dispositivo **como** datos adjuntos.
* Usa el **control visor de imágenes nativo** para obtener una vista previa de varias **imágenes** a la vez.
* Admite **la transferencia de imágenes grandes** (de 1 MB a 50 MB) a través del puente sdk.
* Admite **funciones avanzadas de imagen** que permiten a los usuarios obtener una vista previa y editar imágenes:
  * Digitalizar documentos, pizarras y tarjetas de presentación a través de la cámara.
  
> [!IMPORTANT]
> * Las API , y se pueden invocar desde varias superficies de `selectMedia` `getMedia` `viewImages` Teams, como módulos de tareas, pestañas y aplicaciones personales. Para obtener más información, consulta [Puntos de entrada para aplicaciones de Teams.](../extensibility-points.md)
> * `selectMedia` La API se ha extendido para admitir propiedades de micrófono y audio.

Debes usar el siguiente conjunto de API para habilitar las capacidades multimedia del dispositivo:

| API      | Description   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**| Esta API permite a los usuarios **capturar o seleccionar medios de la cámara del** dispositivo y devolverlo a la aplicación web. Los usuarios pueden editar, recortar, girar, anotar o dibujar sobre imágenes antes del envío. En respuesta a , la aplicación web recibe los IDs multimedia de las imágenes seleccionadas `selectMedia` y una miniatura de los medios seleccionados. Esta API se puede configurar aún más a través de [la configuración ImageProps.](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)| Establece el [mediaType en](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) `4` en la API para obtener acceso a la funcionalidad de `selectMedia` micrófono. Esta API también permite a los usuarios grabar audio desde el micrófono del dispositivo y devolver clips grabados a la aplicación web. Los usuarios pueden pausar, volver a grabar y reproducir la vista previa de grabación antes del envío. En respuesta a **selectMedia,** la aplicación web recibe los IDs multimedia de la grabación de audio seleccionada. <br/> Use `maxDuration` , si necesita configurar una duración en minutos para grabar la conversación. La duración actual de la grabación es de 10 minutos, después de lo cual finaliza la grabación.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| Esta API recupera los medios capturados por `selectMedia` la API en fragmentos, independientemente del tamaño de los medios. Estos fragmentos se ensamblan y se envían a la aplicación web como un archivo o blob. Dividir los medios en fragmentos más pequeños facilita la transferencia de archivos de gran tamaño. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| Esta API permite al usuario ver imágenes en modo de pantalla completa como una lista desplazable.|


**Experiencia de aplicación web para la API de selectMedia para la funcionalidad de imagen** 
 ![ experiencia de cámara e imagen de dispositivo en Teams](../../assets/images/tabs/image-capability.png)

**Experiencia de aplicación web para la API de selectMedia para la funcionalidad de micrófono** 
 ![ experiencia de aplicación web para la funcionalidad de micrófono](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Control de errores

Debes asegurarte de controlar estos errores correctamente en la aplicación de Teams. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores: 


|Código de error |  Nombre del error     | Condición|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **404** | FILE_NOT_FOUND | El archivo especificado no se encuentra en la ubicación determinada.|
| **500** | INTERNAL_ERROR | Se produce un error interno al realizar la operación necesaria.|
| **1000** | PERMISSION_DENIED |El usuario deniega el permiso.|
| **2000** |NETWORK_ERROR | Problema de red.|
| **3000** | NO_HW_SUPPORT | El hardware subyacente no admite la funcionalidad.|
| **4000**| INVALID_ARGUMENTS | Uno o más argumentos no son válidos.|
| **5000** | UNAUTHORIZED_USER_OPERATION | El usuario no está autorizado a completar esta operación.|
| **6000** |INSUFFICIENT_RESOURCES | La operación no se pudo completar debido a la falta de recursos.|
|**7000** | THROTTLE | La plataforma limitó la solicitud a medida que la API se invocaba con frecuencia.|
|  **8000** | USER_ABORT |El usuario anula la operación.|
| **9000**| OLD_PLATFORM | El código de la plataforma está obsoleto y no implementa esta API.|
| **10000**| SIZE_EXCEEDED |  El valor devuelto es demasiado grande y ha superado los límites de tamaño de la plataforma.|

## <a name="code-snippets"></a>Fragmentos de código

**Llamada `selectMedia` API** para capturar imágenes con cámara:

```javascript
let imageProp: microsoftTeams.media.ImageProps = {
    sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
    startMode: microsoftTeams.media.CameraStartMode.Photo,
    ink: false,
    cameraSwitcher: false,
    textSticker: false,
    enableFilter: true,
};
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Image,
    maxMediaCount: 10,
    imageProps: imageProp
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    if (attachments) {
        let y = attachments[0];
        img.src = ("data:" + y.mimeType + ";base64," + y.preview);
    }
});
```

**Llamada `getMedia` API** para recuperar medios grandes en fragmentos:

```javascript
let media: microsoftTeams.media.Media = attachments[0]
media.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("image")) {
            img.src = (URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

**Llamada `viewImages` API por identificador devuelto por `selectMedia` API:**

```javascript
// View images by id:
// Assumption: attachmentArray = select Media API Output
let uriList = [];
if (attachmentArray && attachmentArray.length > 0) {
    for (let i = 0; i < attachmentArray.length; i++) {
        let file = attachmentArray[i];
        if (file.mimeType.includes("image")) {
            let imageUri = {
                value: file.content,
                type: 1,
            }
            uriList.push(imageUri);
        } else {
            alert("File type is not image");
        }
    }
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

**Llamada `viewImages` API por dirección URL:**

```javascript
// View Images by URL:
// Assumption 2 urls, url1 and url2
let uriList = [];
if (URL1 != null && URL1.length > 0) {
    let imageUri = {
        value: URL1,
        type: 2,
    }
    uriList.push(imageUri);
}
if (URL2 != null && URL2.length > 0) {
    let imageUri = {
        value: URL2,
        type: 2,
    }
    uriList.push(imageUri);
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

**Llamadas `selectMedia` y API para grabar audio a través del `getMedia` micrófono:**

```javascript
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Audio,
    maxMediaCount: 1,
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    // If you want to directly use the audio file (for smaller file sizes (~4MB))    if (attachments) {
    let audioResult = attachments[0];
    var videoElement = document.createElement("video");
    videoElement.setAttribute("src", ("data:" + y.mimeType + ";base64," + y.preview));
    //To use the audio file via get Media API for bigger audio file sizes greater than 4MB        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("video")) {
            videoElement.setAttribute("src", URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

## <a name="see-also"></a>Vea también

- [Integrar la funcionalidad del escáner de códigos DE BARRAS o QR en Teams](qr-barcode-scanner-capability.md)

- [Integrar capacidades de ubicación en Teams](location-capability.md)