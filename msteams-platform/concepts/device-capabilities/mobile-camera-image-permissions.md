---
title: Integrar capacidades multimedia
description: Cómo usar el SDK de cliente de JavaScript de Teams para habilitar las funcionalidades multimedia
keywords: medios de permisos de dispositivo nativo de capacidades de micrófono de imagen de cámara
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4126551858116343689e08c4b4f385eb0bbc7ed1
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231604"
---
# <a name="integrate-media-capabilities"></a>Integrar capacidades multimedia 

Este documento le guiará sobre cómo integrar funcionalidades multimedia. Esta integración combina las funcionalidades de dispositivo nativo, como la **cámara** y **el micrófono** con la plataforma de Teams.  

Puede usar el [SDK de cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)de Microsoft Teams, que proporciona las herramientas necesarias para que la aplicación tenga acceso a los permisos de dispositivo de un [usuario.](native-device-permissions.md) Use las **API de** funcionalidad multimedia adecuadas para integrar  las  funcionalidades de dispositivo nativo, como la cámara y el micrófono con la plataforma de Teams dentro de su aplicación móvil de Microsoft Teams, y cree una experiencia más completa. 

## <a name="advantage-of-integrating-media-capabilities"></a>Ventaja de la integración de funcionalidades multimedia

La principal ventaja de integrar las funcionalidades de los dispositivos en sus aplicaciones de Teams es que aprovecha los controles nativos de Teams para proporcionar una experiencia enriqueciendo y envolvente a los usuarios.
Para integrar las funcionalidades multimedia, debes actualizar el archivo de manifiesto de la aplicación y llamar a las API de funcionalidad multimedia. 

Para una integración eficaz, debe comprender bien los fragmentos de código para llamar a las API [correspondientes,](#code-snippets) lo que le permite usar funcionalidades de medios nativos.

Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores en su aplicación de Teams.

> [!NOTE] 
> Actualmente, la compatibilidad de Microsoft Teams con las funcionalidades multimedia solo está disponible para clientes móviles.

## <a name="update-manifest"></a>Actualizar manifiesto

Actualice la aplicación de Teams [manifest.jsarchivo](../../resources/schema/manifest-schema.md#devicepermissions) agregando la propiedad `devicePermissions` y especificando `media` . Permite que la aplicación solicite permisos de requisitos  a los usuarios antes de empezar a usar la cámara para  capturar la imagen, abrir la galería para seleccionar una imagen para enviar como datos adjuntos o usar el micrófono para grabar la conversación.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> El **mensaje Solicitar permisos se** muestra automáticamente cuando se inicia una API de Teams relevante. Para obtener más información, consulta [Solicitar permisos de dispositivo.](native-device-permissions.md)

## <a name="media-capability-apis"></a>API de funcionalidad multimedia

Las [API selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)y [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) te permiten usar funcionalidades de medios nativos de la siguiente manera:

* Usa el micrófono **nativo para** permitir a los usuarios grabar **audio** (grabar 10 minutos de conversación) desde el dispositivo.
* Usa el **control de cámara** nativo para permitir a los usuarios capturar y adjuntar **imágenes** sobre la marcha.
* Usa la compatibilidad **con la galería nativa** para permitir a los usuarios seleccionar imágenes de dispositivo **como** datos adjuntos.
* Usa el **control del visor de imágenes nativo** para obtener una vista previa de varias **imágenes** a la vez.
* Admite **la transferencia de imágenes de** gran tamaño (de 1 MB a 50 MB) a través del puente del SDK.
* Admite **capacidades avanzadas de imagen** que permiten a los usuarios obtener una vista previa y editar imágenes:
  * Digitalizar documentos, pizarras y tarjetas de presentación a través de la cámara.
  
> [!IMPORTANT]
>*   Las API y , se pueden invocar desde varias superficies de Teams, como módulos de `selectMedia` `getMedia` `viewImages` tareas, pestañas y aplicaciones personales. Para obtener más información, consulte [Puntos de entrada para aplicaciones de Teams.](../extensibility-points.md)
>* `selectMedia` La API se ha ampliado para admitir propiedades de micrófono y audio.

Debes usar el siguiente conjunto de API para habilitar las funcionalidades multimedia del dispositivo:

| API      | Descripción   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Cámara)**| Esta API permite a los usuarios **capturar o seleccionar contenido multimedia** de la cámara del dispositivo y devolverlo a la aplicación web. Los usuarios pueden editar, recortar, girar, anotar o dibujar sobre imágenes antes del envío. En respuesta a **selectMedia,** la aplicación web recibe los IDs multimedia de las imágenes seleccionadas y una miniatura de los medios seleccionados. Esta API se puede configurar aún más a través de la [configuración ImageProps.](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Micrófono**)| Establece el [mediaType en](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) `4` la API **selectMedia** para acceder a la funcionalidad de micrófono. Esta API también permite a los usuarios grabar audio desde el micrófono del dispositivo y devolver clips grabados a la aplicación web. Los usuarios pueden pausar, volver a grabar y reproducir la vista previa de grabación antes del envío. En respuesta a **selectMedia,** la aplicación web recibe los IDs multimedia de la grabación de audio seleccionada. <br/> Use `maxDuration` , si necesita configurar una duración en minutos para grabar la conversación. La duración actual de la grabación es de 10 minutos, después de lo cual finaliza la grabación.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| Esta API recupera los medios capturados por la API **selectMedia** en fragmentos, independientemente del tamaño del medio. Estos fragmentos se ensamblan y se envían de nuevo a la aplicación web como un archivo o blob. Dividir los medios en fragmentos más pequeños facilita la transferencia de archivos de gran tamaño. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| Esta API permite al usuario ver imágenes en modo de pantalla completa como una lista desplazable.|


**Experiencia de la aplicación web para la API selectMedia para la funcionalidad de imagen** 
 ![ experiencia de cámara e imagen del dispositivo en Teams](../../assets/images/tabs/image-capability.png)

**Experiencia de la aplicación web para la API selectMedia para la funcionalidad de micrófono** 
 ![ experiencia de la aplicación web para la funcionalidad de micrófono](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Control de errores

Debe asegurarse de controlar estos errores correctamente en su aplicación de Teams. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores: 


|Código de error |  Nombre del error     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **404** | FILE_NOT_FOUND | El archivo especificado no se encuentra en la ubicación especificada.|
| **500** | INTERNAL_ERROR | Se produce un error interno mientras se realiza la operación necesaria.|
| **1000** | PERMISSION_DENIED |El usuario deniega el permiso.|
| **2000** |NETWORK_ERROR | Problema de red.|
| **3000** | NO_HW_SUPPORT | El hardware subyacente no admite la funcionalidad.|
| **4000**| INVALID_ARGUMENTS | Uno o más argumentos no son válidos.|
| **5000** | UNAUTHORIZED_USER_OPERATION | El usuario no está autorizado a completar esta operación.|
| **6000** |INSUFFICIENT_RESOURCES | No se pudo completar la operación debido a la falta de recursos.|
|**7000** | THROTTLE | La plataforma limitó la solicitud a medida que la API se invocaba con frecuencia.|
|  **8000** | USER_ABORT |El usuario anula la operación.|
| **9000**| OLD_PLATFORM | El código de la plataforma está obsoleto y no implementa esta API.|
| **10000**| SIZE_EXCEEDED |  El valor devuelto es demasiado grande y ha superado los límites de tamaño de la plataforma.|

## <a name="code-snippets"></a>Fragmentos de código

**Llamadas `selectMedia` API** para capturar imágenes con cámara:

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

**Llamadas `getMedia` API** para recuperar medios grandes en fragmentos:

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

**Llamadas `viewImages` API por identificador devuelto por `selectMedia` API:**

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

**Llamadas `viewImages` API por dirección URL:**

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
