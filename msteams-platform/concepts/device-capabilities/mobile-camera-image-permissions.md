---
title: Integrar capacidades multimedia
author: Rajeshwari-v
description: Obtenga información sobre cómo usar el SDK de cliente de JavaScript de Teams para habilitar funcionalidades multimedia mediante ejemplos de código
keywords: API multimedia de permisos de dispositivos nativos de las capacidades del micrófono de imagen de cámara
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: c9b31bf6fe97446bfbccdd1861612ec938733f88
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111265"
---
# <a name="integrate-media-capabilities"></a>Integrar capacidades multimedia

Capacidades nativas del dispositivo, como la **cámara** y el **micrófono**, que puede integrar con su aplicación de Teams. Para la integración, puede usar [ SDK de cliente JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), que proporciona las herramientas necesarias para que la aplicación tenga acceso a los [permisos de dispositivo](native-device-permissions.md). Use las API de funcionalidad multimedia adecuadas para integrar las funcionalidades del dispositivo, como **cámara** y **micrófono** con la plataforma teams dentro de la aplicación móvil de Microsoft Teams, y cree una experiencia más completa.

## <a name="advantage-of-integrating-media-capabilities"></a>Ventaja de la integración de funcionalidades multimedia

La principal ventaja de integrar las funcionalidades del dispositivo en las aplicaciones de Teams es que aprovecha los controles nativos de Teams para proporcionar una experiencia enriquecida y envolvente a los usuarios.
Para integrar las funcionalidades multimedia, debe actualizar el archivo de manifiesto de la aplicación y llamar a las API de funcionalidad multimedia.

Para una integración eficaz, debe tener un buen conocimiento de [code snippets](#code-snippets) para llamar a las API respectivas, lo que le permite usar funcionalidades multimedia nativas.

Es importante familiarizarse con los [errores de respuesta de la API](#error-handling) para controlar los errores de la aplicación de Teams.

> [!NOTE]
>
> * Actualmente, Microsoft Teams el uso de las funcionalidades de ubicación solo está disponible para clientes móviles.
> * Actualmente, Teams no admite permisos de dispositivo para aplicaciones de varias ventanas, pestañas y el panel lateral de las reuniones.
> * Los permisos del dispositivo son diferentes en el explorador. Para obtener más información, vea [Permisos del dispositivo en el navegador](browser-device-permissions.md).

## <a name="update-manifest"></a>Actualizar manifiesto

Actualice el archivo [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) de la aplicación Teams agregando la `devicePermissions` propiedad y especificando `media`. Permite que la aplicación solicite los permisos necesarios a los usuarios antes de empezar a usar el **cámara** para capturar la imagen, abrir la galería para seleccionar una imagen para enviar como datos adjuntos o usar el **micrófono** para grabar la conversación. La actualización del manifiesto de la aplicación es la siguiente:

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> El permiso de **solicitud de permisos** se muestra automáticamente cuando se inicia una API de Teams relevante. Para obtener más información, consulte [Solicitar permisos de dispositivo](native-device-permissions.md).

## <a name="media-capability-apis"></a>Funcionalidad multimedia

La [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true) y [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) API permiten usar funcionalidades multimedia nativas de la siguiente manera:

* Use el **micrófono** nativo para permitir que los usuarios **grabar audio** (grabar 10 minutos de conversación) desde el dispositivo.
* Usa el **control nativo cámara** para permitir que los usuarios **capturar y adjuntar imágenes** sobre la marcha.
* Utilice el **soporte nativo de la galería** para permitir que los usuarios **seleccionen las imágenes del dispositivo** como archivos adjuntos.
* Utilice el **control del visor de imágenes nativo** para obtener una **vista previa de varias imágenes** a la vez.
* Compatibilidad con **transferencia de imágenes grandes** (de 1 MB a 50 MB) a través del puente del SDK.
* Compatibilidad con **funcionalidades de imagen avanzada** permitir a los usuarios obtener una vista previa y editar imágenes:
  * Digitalice documentos, pizarras y tarjetas de presentación a través de la cámara.
  
> [!IMPORTANT]
>
> * Las API `selectMedia`, `getMedia` y `viewImages` se pueden invocar desde varias superficies de Teams, como módulos de tareas, pestañas y aplicaciones personales. Para obtener más información, vea [Entrada de puntos para aplicaciones de Teams](../extensibility-points.md).
> * `selectMedia` API se ha ampliado para admitir las propiedades de micrófono y audio.

Debe usar el siguiente conjunto de API para habilitar las funcionalidades de ubicación del dispositivo:

| API      | Descripción   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**cámara)**| Esta API permite a los usuarios **capture o seleccionar medios de la cámara del dispositivo** y devolverlos a la aplicación web. Los usuarios pueden editar, recortar, girar, anotar o dibujar imágenes antes del envío. En respuesta a `selectMedia`, la aplicación web recibe los identificadores multimedia de las imágenes seleccionadas y una miniatura del medio seleccionado. Esta API se puede configurar aún más a través de la configuración de [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true). |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**micrófono**)| Establezca el [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) en `4` en `selectMedia` API para acceder a la funcionalidad del micrófono. Esta API también permite a los usuarios grabar audio desde el micrófono del dispositivo y devolver clips grabados a la aplicación web. Los usuarios pueden pausar, volver a grabar y reproducir la vista previa de grabación antes del envío. En respuesta a **selectMedia**, la aplicación web recibe los identificadores multimedia de la grabación de audio seleccionada. <br/> Use `maxDuration` si necesita configurar una duración en minutos para grabar la conversación. La duración actual de la grabación es de 10 minutos, tras lo cual finaliza la grabación.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| Esta API recupera los medios capturados por `selectMedia` API en fragmentos, independientemente del tamaño del medio. Estos fragmentos se ensamblan y se devuelven a la aplicación web como un archivo o blob. Dividir los medios en fragmentos más pequeños facilita la transferencia de archivos grandes. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| Esta API permite al usuario ver imágenes en modo de pantalla completa como una lista desplazable.|

En la imagen siguiente se muestra la experiencia de la aplicación web de `selectMedia` API para la funcionalidad de imagen:

![experiencia de cámara e imagen del dispositivo en Teams](../../assets/images/tabs/image-capability.png)

En la imagen siguiente se muestra la experiencia de la aplicación web de `selectMedia` API para la funcionalidad del micrófono:

![experiencia de aplicación web para la funcionalidad de micrófono](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Control de errores

Debe asegurarse de controlar estos errores correctamente en la aplicación de Teams. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:

|Código de error |  Nombre de error     | Condición|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **404** | ARCHIVO NO ENCONTRADO. | El archivo especificado no se encuentra en la ubicación especificada.|
| **500** | INTERNAL_ERROR | Se produce un error interno al realizar la operación necesaria.|
| **1 000** | PERMISSION_DENIED |El usuario deniega el permiso.|
| **3000** | NO_HW_SUPPORT | El hardware subyacente no admite la funcionalidad.|
| **4000**| InvalidArguments | Uno o más argumentos no son válidos.|
|  **8000** | USER_ABORT |El usuario anula la operación.|
| **9000**| OLD_PLATFORM | El código de la plataforma no está actualizado y no implementa esta API.|
| **10000**| SIZE_EXCEEDED |  El valor devuelto es demasiado grande y ha superado los límites del tamaño de la plataforma.|

## <a name="code-snippets"></a>Fragmentos de código

**Calling `selectMedia` API** para capturar imágenes mediante la cámara:

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

**Calling `getMedia` API** para recuperar medios grandes en fragmentos:

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

**Calling `viewImages` API por identificador devuelto por `selectMedia` API**:

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

**Calling `viewImages` API por dirección URL**:

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

**Calling `selectMedia` y `getMedia` API para grabar audio a través del micrófono**:

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

* [Integrar la funcionalidad de escáner de código QR o código de barras en Teams](qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
* [Integración del selector de usuarios en Teams](people-picker-capability.md)
* [Requisiciones y consideraciones para bots multimedia hospedados en la aplicación](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
