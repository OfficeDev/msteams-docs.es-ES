---
title: Integrar capacidades multimedia
author: Rajeshwari-v
description: Cómo usar el SDK Teams cliente de JavaScript para habilitar funcionalidades multimedia
keywords: Medios de permisos de dispositivo nativos de las capacidades de micrófono de imagen de cámara
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 22d4a791e83cf36f18b75a3846865835b0ee024f
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211628"
---
# <a name="integrate-media-capabilities"></a>Integrar capacidades multimedia 

Puedes integrar las capacidades nativas del dispositivo, como la **cámara** y el **micrófono** con la Teams aplicación. Para la integración, puedes usar Microsoft Teams SDK de cliente de [JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona las herramientas necesarias para que la aplicación tenga acceso a los permisos [de dispositivo de un usuario.](native-device-permissions.md) Usa las API de funcionalidad multimedia adecuadas para  integrar  las capacidades del dispositivo, como la cámara y el micrófono con la plataforma Teams dentro de la aplicación móvil de Microsoft Teams y crear una experiencia más enriquecte. 

## <a name="advantage-of-integrating-media-capabilities"></a>Ventaja de integrar capacidades multimedia

La principal ventaja de integrar las capacidades de dispositivo en las aplicaciones Teams es que aprovecha los controles Teams nativos para proporcionar una experiencia enriqueciendo e inmersiva a los usuarios.
Para integrar las funcionalidades multimedia, debes actualizar el archivo de manifiesto de la aplicación y llamar a las API de funcionalidad multimedia. 

Para una integración eficaz, debe tener una buena comprensión de los fragmentos de código para llamar a las API [correspondientes,](#code-snippets) lo que le permite usar funcionalidades multimedia nativas.

Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la Teams aplicación.

> [!NOTE] 
> * Actualmente, Microsoft Teams compatibilidad con funcionalidades multimedia solo está disponible para clientes móviles.   
> * Actualmente, Teams no admite permisos de dispositivo para aplicaciones de varias ventanas, pestañas y el panel lateral de la reunión.    

## <a name="update-manifest"></a>Manifiesto de actualización

Actualice el Teams aplicaciónmanifest.js[el archivo](../../resources/schema/manifest-schema.md#devicepermissions) agregando la propiedad `devicePermissions` y especificando `media` . Permite a la aplicación solicitar los permisos necesarios a  los usuarios antes de empezar a usar la cámara para capturar  la imagen, abrir la galería para seleccionar una imagen para enviar como datos adjuntos o usar el micrófono para grabar la conversación. La actualización del manifiesto de la aplicación es la siguiente:

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> El **símbolo del sistema Solicitar permisos** se muestra automáticamente cuando se inicia una API de Teams relevante. Para obtener más información, consulta [Solicitar permisos de dispositivo](native-device-permissions.md).

## <a name="media-capability-apis"></a>API de funcionalidad multimedia

Las [API selectMedia,](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)y [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) permiten usar las funciones multimedia nativas de la siguiente manera:

* Usa el micrófono **nativo para** permitir a los usuarios grabar **audio** (grabar 10 minutos de conversación) desde el dispositivo.
* Usa el **control de cámara** nativa para permitir a los usuarios capturar y adjuntar **imágenes** sobre la marcha.
* Usa la compatibilidad **de galería nativa** para permitir a los usuarios seleccionar imágenes del dispositivo **como** datos adjuntos.
* Usa el **control visor de imágenes nativo** para obtener una vista previa de varias **imágenes** a la vez.
* Admite **la transferencia de imágenes grandes** (de 1 MB a 50 MB) a través del puente sdk.
* Admite **funciones avanzadas de imagen** que permiten a los usuarios obtener una vista previa y editar imágenes:
  * Digitalizar documentos, pizarras y tarjetas de presentación a través de la cámara.
  
> [!IMPORTANT]
> * Las API , y se pueden invocar desde varias superficies Teams, como módulos de `selectMedia` `getMedia` `viewImages` tareas, pestañas y aplicaciones personales. Para obtener más información, consulta [Puntos de entrada para Teams aplicaciones](../extensibility-points.md).
> * `selectMedia` La API se ha extendido para admitir propiedades de micrófono y audio.

Debes usar el siguiente conjunto de API para habilitar las capacidades multimedia del dispositivo:

| API      | Descripción   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**| Esta API permite a los usuarios **capturar o seleccionar medios de la cámara del** dispositivo y devolverlo a la aplicación web. Los usuarios pueden editar, recortar, girar, anotar o dibujar sobre imágenes antes del envío. En respuesta a , la aplicación web recibe los IDs multimedia de las imágenes seleccionadas `selectMedia` y una miniatura de los medios seleccionados. Esta API se puede configurar aún más a través de [la configuración ImageProps.](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)| Establece el [mediaType en](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) `4` en la API para obtener acceso a la funcionalidad de `selectMedia` micrófono. Esta API también permite a los usuarios grabar audio desde el micrófono del dispositivo y devolver clips grabados a la aplicación web. Los usuarios pueden pausar, volver a grabar y reproducir la vista previa de grabación antes del envío. En respuesta a **selectMedia,** la aplicación web recibe los IDs multimedia de la grabación de audio seleccionada. <br/> Use `maxDuration` , si necesita configurar una duración en minutos para grabar la conversación. La duración actual de la grabación es de 10 minutos, después de lo cual finaliza la grabación.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| Esta API recupera los medios capturados por `selectMedia` la API en fragmentos, independientemente del tamaño de los medios. Estos fragmentos se ensamblan y se envían a la aplicación web como un archivo o blob. Dividir los medios en fragmentos más pequeños facilita la transferencia de archivos de gran tamaño. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| Esta API permite al usuario ver imágenes en modo de pantalla completa como una lista desplazable.|

En la siguiente imagen se muestra la experiencia de la aplicación web `selectMedia` de api para la funcionalidad de imagen:

![cámara de dispositivo y experiencia de imagen en Teams](../../assets/images/tabs/image-capability.png)

En la siguiente imagen se muestra la experiencia de la aplicación web `selectMedia` de la API para la funcionalidad de micrófono:

![experiencia de aplicación web para la funcionalidad de micrófono](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Control de errores

Debes asegurarte de controlar estos errores correctamente en tu Teams aplicación. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores: 

|Código de error |  Nombre del error     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **404** | FILE_NOT_FOUND | El archivo especificado no se encuentra en la ubicación determinada.|
| **500** | INTERNAL_ERROR | Se produce un error interno al realizar la operación necesaria.|
| **1000** | PERMISSION_DENIED |El usuario deniega el permiso.|
| **3000** | NO_HW_SUPPORT | El hardware subyacente no admite la funcionalidad.|
| **4000**| INVALID_ARGUMENTS | Uno o más argumentos no son válidos.|
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

## <a name="see-also"></a>Consulte también

* [Integrar la funcionalidad de escáner de códigos QR o códigos de barras en Teams](qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
* [Integrar la funcionalidad selector de personas en Teams](people-picker-capability.md)

