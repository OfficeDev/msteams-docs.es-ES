---
title: Integrar capacidades multimedia
author: Rajeshwari-v
description: Obtenga información sobre cómo usar el SDK de cliente de JavaScript de Teams para habilitar las funcionalidades multimedia mediante ejemplos de código y también obtenga información sobre la ventaja de integrar las funcionalidades multimedia.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: bfa63b42383e507f004b0225c64f381e47e547f0
ms.sourcegitcommit: 1ea035bc20303070268db38472839584ad4280b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68653374"
---
# <a name="integrate-media-capabilities"></a>Integrar capacidades multimedia

Puede integrar funcionalidades de dispositivos nativos, como cámara y micrófono con la aplicación de Teams. Para la integración, puede usar el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) que proporciona las herramientas necesarias para que la aplicación acceda a [los permisos de dispositivo](native-device-permissions.md) de un usuario. Use las API de funcionalidad multimedia adecuadas para integrar las funcionalidades del dispositivo, como la cámara y el micrófono con la plataforma de Teams dentro de la aplicación de Microsoft Teams, y crear una experiencia más enriquecida. La funcionalidad multimedia está disponible para el cliente web, el escritorio y el móvil de Teams. Para integrar las funcionalidades multimedia, debe actualizar el archivo de manifiesto de la aplicación y llamar a las API de funcionalidad multimedia.

Para una integración eficaz, debe tener una buena comprensión de [los fragmentos de código](#code-snippets) para llamar a las API correspondientes, lo que le permite usar funcionalidades de medios nativos. Es importante familiarizarse con los [errores de respuesta de la API](#error-handling) para controlar los errores en la aplicación de Teams.

## <a name="advantages"></a>Ventajas

La ventaja de integrar las funcionalidades de dispositivo en las aplicaciones de Teams es que usa controles nativos de Teams para proporcionar una experiencia enriquecida e inmersiva para los usuarios. En los escenarios siguientes se muestran las ventajas de las funcionalidades multimedia:

* Permitir al usuario capturar las simulaciones aproximadas dibujadas en una pizarra física a través de su teléfono móvil y usar las imágenes capturadas como opciones de sondeo en el chat de grupo de Teams.

* Permitir al usuario grabar el mensaje de audio y adjuntarlo a un vale de incidente.

* Permitir al usuario escanear los documentos físicos desde el teléfono inteligente para presentar una reclamación de seguro de automóvil.

* Permitir al usuario grabar un vídeo en un sitio de trabajo y cargarlo para su asistencia.

> [!NOTE]
>
> * Actualmente, Teams no admite permisos de dispositivo en la ventana de chat emergente, las pestañas y el panel lateral de la reunión.</br>
> * Los permisos del dispositivo son diferentes en el explorador. Para obtener más información, vea [Permisos de dispositivo en el navegador](browser-device-permissions.md).
> * El símbolo del sistema de permisos de solicitud se muestra automáticamente en el móvil cuando se inicia una API de Teams pertinente. Para obtener más información, consulte [solicitar permisos de dispositivo](native-device-permissions.md).

## <a name="update-manifest"></a>Actualizar manifiesto

Actualice el archivo [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) de la aplicación Teams agregando la `devicePermissions` propiedad y especificando `media`. Permite que la aplicación solicite los permisos necesarios a los usuarios antes de empezar a usar el cámara para capturar la imagen, abrir la galería para seleccionar una imagen para enviar como datos adjuntos o usar el micrófono para grabar la conversación. La actualización del manifiesto de la aplicación es la siguiente:

``` json
"devicePermissions": [
    "media",
],
```

## <a name="media-capability-apis"></a>Funcionalidad multimedia

La [selectMedia](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia), [getMedia](/javascript/api/@microsoft/teams-js/media.media#@microsoft-teams-js-media-media-getmedia) y [viewImages](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-viewimages) API permiten usar funcionalidades multimedia nativas de la siguiente manera:

* Use el **micrófono** nativo para permitir que los usuarios **grabar audio** (grabar 10 minutos de conversación) desde el dispositivo.
* Use **el control de cámara** nativo para permitir a los usuarios **capturar y adjuntar imágenes** y **capturar vídeos** (grabar hasta cinco minutos de vídeo) sobre la marcha.
* Utilice el **soporte nativo de la galería** para permitir que los usuarios **seleccionen las imágenes del dispositivo** como archivos adjuntos.
* Utilice el **control del visor de imágenes nativo** para obtener una **vista previa de varias imágenes** a la vez.
* Compatibilidad con **transferencia de imágenes grandes** (de 1 MB a 50 MB) a través del puente del SDK.
* Admite **funcionalidades avanzadas de imágenes** al permitir a los usuarios obtener una vista previa y editar imágenes.
* Escanee documentos, pizarra y tarjetas de presentación a través de la cámara.
  
> [!IMPORTANT]
>
> * Las API `selectMedia`, `getMedia` y `viewImages` se pueden invocar desde varias superficies de Teams, como módulos de tareas, pestañas y aplicaciones personales. Para obtener más información, consulte [Puntos de entrada para aplicaciones de Teams](../extensibility-points.md).</br>
> * La `selectMedia` API admite funcionalidades de cámara y micrófono a través de diferentes configuraciones de entrada.
> * La `selectMedia` API para acceder a la funcionalidad de micrófono solo admite clientes móviles.
> * El recuento máximo de imágenes cargadas viene determinado por [`maxMediaCount`](/javascript/api/@microsoft/teams-js/media.mediainputs#@microsoft-teams-js-media-mediainputs-maxmediacount) y también por el tamaño total de la matriz devuelta por la `selectMedia` API. Asegúrese de que el tamaño de la matriz no supere los 4 MB; si el tamaño de la matriz supera los 4 MB, la API genera un código de error 10000 que es SIZE_EXCEEDED error.

En la tabla siguiente se muestra un conjunto de API para habilitar las funcionalidades multimedia del dispositivo:

| API      | Descripción   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia) (**cámara)**| Esta API permite a los usuarios **capture o seleccionar medios de la cámara del dispositivo** y devolverlos a la aplicación web. Los usuarios pueden editar, recortar, girar, anotar o dibujar imágenes antes del envío. En respuesta a `selectMedia`, la aplicación web recibe los identificadores multimedia de las imágenes seleccionadas y una miniatura del medio seleccionado. Esta API se puede configurar aún más a través de la configuración de [ImageProps](/javascript/api/@microsoft/teams-js/media.imageprops). |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia) (**micrófono**)| Establezca [mediaType](/javascript/api/@microsoft/teams-js/media.mediatype) `4` en (Audio) en `selectMedia` la API para acceder a la funcionalidad de micrófono. Esta API también permite a los usuarios grabar audio desde el micrófono del dispositivo y devolver clips grabados a la aplicación web. Los usuarios pueden pausar, volver a grabar y reproducir la vista previa de grabación antes del envío. En respuesta a **selectMedia**, la aplicación web recibe los identificadores multimedia de las grabaciones de audio seleccionadas. <br/> Use `maxDuration`, si necesita configurar una duración en minutos para grabar la conversación. La duración actual de la grabación es de 10 minutos, tras lo cual finaliza la grabación.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/media.media#@microsoft-teams-js-media-media-getmedia)| Esta API recupera los medios capturados por `selectMedia` API en fragmentos, independientemente del tamaño del medio. Estos fragmentos se ensamblan y se devuelven a la aplicación web como un archivo o blob. Dividir los medios en fragmentos más pequeños facilita la transferencia de archivos grandes. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-viewimages)| Esta API permite al usuario ver imágenes en modo de pantalla completa como una lista desplazable.|

# <a name="mobile"></a>[Móvil](#tab/mobile)

En la imagen siguiente se muestra la experiencia de la aplicación web de `selectMedia` API para la funcionalidad de imagen:

:::image type="content" source="~/assets/images/tabs/media-capability-mobile2.png" alt-text="Ilustración que muestra la funcionalidad de imagen para dispositivos móviles.":::

> [!NOTE]
> En dispositivos con la versión de Android inferior a 7, la `selectMedia` API inicia la experiencia nativa de la cámara Android en lugar de la experiencia nativa de la cámara de Teams.

En la imagen siguiente se muestra la experiencia de la aplicación web de `selectMedia` la API para la funcionalidad de micrófono:

:::image type="content" source="~/assets/images/tabs/microphone-capability.png" alt-text="Ilustración que muestra la funcionalidad del micrófono para dispositivos móviles.":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

En la imagen siguiente se muestra la experiencia de la aplicación web de `selectMedia` API para la funcionalidad de imagen:

:::image type="content" source="~/assets/images/tabs/media-capability-desktop1.png" alt-text="Ilustración que muestra la funcionalidad multimedia para el escritorio.":::

---

## <a name="error-handling"></a>Control de errores

Asegúrese de controlar estos errores correctamente en la aplicación de Teams. En la tabla siguiente se enumeran los códigos de error y las descripciones con las que se generan los errores:

|Código de error |  Nombre de error     | Descripción|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **404** | ARCHIVO NO ENCONTRADO. | El archivo especificado no se encuentra en la ubicación especificada.|
| **500** | INTERNAL_ERROR | Se produce un error interno al realizar la operación necesaria.|
| **1 000** | PERMISSION_DENIED |El usuario deniega el permiso.|
| **3000** | NO_HW_SUPPORT | El hardware no admite la funcionalidad.|
| **4000**| InvalidArguments | Uno o más argumentos no son válidos.|
|  **8000** | USER_ABORT |El usuario anula la operación.|
| **9000**| OLD_PLATFORM | El código de la plataforma no está actualizado y no implementa esta API.|
| **10000**| SIZE_EXCEEDED |  El valor devuelto es demasiado grande y ha superado los límites de tamaño de la plataforma.|

## <a name="code-snippets"></a>Fragmentos de código

* Llame a `selectMedia` LA API para capturar imágenes mediante la cámara:

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

* Llame a `selectMedia` LA API para capturar vídeos mediante la cámara:

  * Captura de vídeos con `fullscreen: true`:

       `fullscreen: true` abre la cámara en modo de grabación de vídeo. Proporciona una opción para usar la cámara delantera y trasera y también proporciona otros atributos, como se mencionó en el ejemplo siguiente:

       ```javascript
        
         const defaultLensVideoProps: microsoftTeams.media.VideoProps = {
             sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
             startMode: microsoftTeams.media.CameraStartMode.Video,
             cameraSwitcher: true,
             maxDuration: 30
        }
         const defaultLensVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 6,
             videoProps: defaultLensVideoProps
        }
       ```

  * Captura de vídeos con `fullscreen: false`:

       `fullscreen: false` abre la cámara en modo de grabación de vídeo y usa solo la cámara frontal. Normalmente `fullscreen: false` se usa cuando el usuario quiere grabar vídeo mientras lee contenido en la pantalla del dispositivo.

       Este modo también admite `isStopButtonVisible: true` que agrega un botón de detención en la pantalla que permite al usuario detener la grabación. Si `isStopButtonVisible: false`es , la grabación se puede detener llamando a mediaController API o cuando la duración de la grabación ha alcanzado `maxDuration` el tiempo especificado.

       A continuación se muestra un ejemplo para detener la grabación con `maxDuration` el tiempo especificado:

       ```javascript
          const defaultNativeVideoProps: microsoftTeams.media.VideoProps = {
             maxDuration: 30,
             isFullScreenMode: false,
             isStopButtonVisible: false,
             videoController: new microsoftTeams.media.VideoController(videoControllerCallback)
         }
          const defaultNativeVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 1,
             videoProps: defaultNativeVideoProps
         }
       ```

       A continuación se muestra un ejemplo para detener la grabación llamando a mediaController API:

       ```javascript
          const defaultNativeVideoProps: microsoftTeams.media.VideoProps = {
             videoController.stop(),
             isFullScreenMode: false,
             isStopButtonVisible: false,
             videoController: new microsoftTeams.media.VideoController(videoControllerCallback)
         }
          const defaultNativeVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 1,
             videoProps: defaultNativeVideoProps
         }
       ```

* Llame a `selectMedia` LA API para capturar imágenes y vídeo mediante la cámara:

  Esto permite a los usuarios seleccionar entre capturar una imagen o un vídeo.

    ```javascript
    
      const defaultVideoAndImageProps: microsoftTeams.media.VideoAndImageProps = {
        sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
        startMode: microsoftTeams.media.CameraStartMode.Photo,
        ink: true,
        cameraSwitcher: true,
        textSticker: true,
        enableFilter: true,
        maxDuration: 30
      }
    
      const defaultVideoAndImageMediaInput: microsoftTeams.media.MediaInputs = {
        mediaType: microsoftTeams.media.MediaType.VideoAndImage,
        maxMediaCount: 6,
        videoAndImageProps: defaultVideoAndImageProps
      }
    
      let videoControllerCallback: microsoftTeams.media.VideoControllerCallback = {
        onRecordingStarted() {
          console.log('onRecordingStarted Callback Invoked');
        },
      };
    
      microsoftTeams.media.selectMedia(defaultVideoAndImageMediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
        if (error) {
            if (error.message) {
                alert(" ErrorCode: " + error.errorCode + error.message);
            } else {
                alert(" ErrorCode: " + error.errorCode);
            }
        }
        
        var videoElement = document.createElement("video");
        attachments[0].getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
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
        });
        
    ```

* Llame a `getMedia` la API para recuperar medios grandes en fragmentos:

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

* Llame a `viewImages` LA API por identificador, que devuelve `selectMedia` la API:

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

* Llame a `viewImages` LA API por dirección URL:

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

* Llamadas `selectMedia` y `getMedia` API para grabar audio a través de micrófono:

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
        videoElement.setAttribute("src", ("data:" + audioResult.mimeType + ";base64," + audioResult.preview));
        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
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
    });
    ```

## <a name="file-download-on-teams-mobile"></a>Descarga de archivos en el móvil de Teams

Puede configurar una aplicación para permitir que los usuarios descarguen archivos de la vista web en su dispositivo móvil.

>[!NOTE]
> La descarga de archivos solo se admite en el cliente móvil de Android Teams y solo se pueden descargar archivos no autenticados.

Para habilitarlo, siga estos pasos:

1. Actualice el archivo [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) de la aplicación de Teams agregando la `devicePermissions` propiedad y especificando `media` como se muestra en el [manifiesto de actualización](#update-manifest).

2. Use el siguiente formato y agregue el atributo de descarga HMTL a la página web:

    ```html
    <a href="path_to_file" download="download">Download</a>
    ```

## <a name="see-also"></a>Consulte también

* [Integrar la funcionalidad de escáner de código QR o código de barras en Teams](qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
* [Integrar Selector de personas](people-picker-capability.md)
* [Requisiciones y consideraciones para bots multimedia hospedados en la aplicación](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
