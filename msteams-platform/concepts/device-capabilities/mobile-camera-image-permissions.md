---
title: Capacidades de cámara e imagen en Microsoft Teams
description: Cómo usar Teams cliente de JavaScript de Microsoft para habilitar capacidades nativas de cámara e imagen
keywords: capacidades de imagen de cámara permisos nativos de dispositivo
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d0ca4dc9c289ec525aa99ea0e156a9f91f5b5d4a
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576897"
---
# <a name="camera-and-image-capabilities-in-teams"></a>Capacidades de cámara e imagen en Microsoft Teams

>[!IMPORTANT]
>
> * Actualmente, la compatibilidad de Microsoft Teams con las capacidades de cámara y de imagen solo está disponible para los clientes móviles.
>* Las `selectMedia` `getMedia` API, y `viewImages` se pueden invocar desde varias superficies de Microsoft Teams, como módulos de tareas, pestañas y aplicaciones personales. Para obtener más información, _consulte_ [puntos de entrada para las aplicaciones de Microsoft Teams](../extensibility-points.md)

Puede usar el  [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)para integrar fácilmente las capacidades de cámara y de imagen en su aplicación móvil de Microsoft Teams. El SDK proporciona las herramientas necesarias para que su aplicación tenga acceso a [los permisos de dispositivo](native-device-permissions.md?tabs=desktop#device-permissions) de un usuario y cree una experiencia más enriquecida.

Las API de [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)y [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) permiten usar capacidades nativas de cámara/imagen de la siguiente manera:

* Use el **control de cámara** nativo para permitir a los usuarios **capturar y adjuntar imágenes** en cualquier modo.
* Use la **compatibilidad con Galería** nativa para permitir que los usuarios **seleccionen imágenes de dispositivo** como datos adjuntos.
* Use Native **Image Viewer control** para **obtener una vista previa de varias imágenes** a la vez.
* Admitir la **transferencia de imágenes de gran tamaño** (hasta 50 MB) a través del puente de SDK
* Admitir **capacidades avanzadas de imagen** que permiten a los usuarios obtener una vista previa de las imágenes y editarlas:
  * Digitalice el documento, la pizarra, las tarjetas de presentación, etc., a través de la cámara.
  * Recorte y gire las imágenes.
  * Agregar texto, tinta o anotación a mano alzada a la imagen.

## <a name="get-started"></a>Introducción

Actualice la aplicación de Microsoft Teams [manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) el archivo; para ello, agregue la `devicePermissions`  propiedad y especifique `media` . Esto permite a su aplicación solicitar los permisos necesarios a los usuarios finales antes de usar la cámara para capturar la imagen o abrir la galería para seleccionar una imagen para enviar como datos adjuntos.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> El mensaje de _solicitud de permisos_ se muestra automáticamente cuando se inicia una API de Teams pertinente. Para obtener más información, *consulte* [solicitar permisos de dispositivo](native-device-permissions.md).

## <a name="using-camera-and-image-capability-apis"></a>Usar las API de funcionalidad de cámara e imagen

Puede usar el siguiente conjunto de API para habilitar las funciones de cámara y de dispositivo de imagen:

| API      | Descripción   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| Esta API permite a los usuarios **capturar o seleccionar elementos multimedia de un dispositivo nativo** y volver a la aplicación Web. Los usuarios pueden elegir entre editar, recortar, girar, anotar o dibujar sobre imágenes antes de enviarla. En respuesta a **selectMedia**, la aplicación web recibirá identificadores de medios de las imágenes seleccionadas y puede recibir una miniatura de los medios seleccionados. |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| Esta API recupera los medios en fragmentos, independientemente de su tamaño. Estos fragmentos se ensamblan y se envían de nuevo a la aplicación web como archivo/BLOB. Con esta API, la imagen se divide en fragmentos más pequeños para facilitar la transferencia de imágenes de gran tamaño. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| Esta API permite al usuario ver imágenes en modo de pantalla completa como una lista desplazable.|

**Experiencia de la aplicación web para SELECTMEDIA API** 
 ![ Experiencia de imagen y cámara de dispositivo en Microsoft Teams](../../assets/images/tabs/image-capability-screenshot.jpg)

## <a name="error-handling"></a>Control de errores

Debe comprender los códigos de error de respuesta de la API y controlarlos correctamente. A continuación se muestra una lista de códigos de error que puede devolver la plataforma:

|Código de error |  Nombre del error     | Condition|
| --- | --- | --- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no es compatible con la plataforma actual.|
| **404** | FILE_NOT_FOUND | No se encontró el archivo especificado en la ubicación indicada.|
| **500** | INTERNAL_ERROR | Error interno detectado al realizar la operación necesaria.|
| **1000** | PERMISSION_DENIED |Permisos denegados por el usuario.|
| **2000** |NETWORK_ERROR | Problema de red.|
| **3000** | NO_HW_SUPPORT | El hardware subyacente no admite la funcionalidad.|
| **4000**| INVALID_ARGUMENTS | Uno o más argumentos no son válidos.|
| **5000** | UNAUTHORIZED_USER_OPERATION | El usuario no está autorizado para completar esta operación.|
| **6000** |INSUFFICIENT_RESOURCES | La operación no se pudo completar debido a recursos insuficientes.|
|**7000** | THROTTLE | La plataforma ha limitado la solicitud porque la API se ha invocado con demasiada frecuencia.|
|  **8000** | USER_ABORT |El usuario ha anulado la operación.|
| **9000**| OLD_PLATFORM | El código de plataforma está obsoleto y no implementa esta API.|
| **10000**| SIZE_EXCEEDED |  El valor devuelto es demasiado grande y ha superado los límites de tamaño de la plataforma.|

## <a name="sample-code-snippets"></a>Ejemplos de fragmentos de código

**API de llamada `selectMedia`**

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

**API de llamada `getMedia`**

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

**Llamar a la `viewImages`  API por ID.**

```javascript
view images by id:
    assumption: attachmentArray = select Media API Outputlet uriList = [];
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

**Llamar a la API viewImages por dirección URL**

```javascript
View Images by URL:
    // Assumption 2 urls, url1 and url2let uriList = [];
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
}
```
