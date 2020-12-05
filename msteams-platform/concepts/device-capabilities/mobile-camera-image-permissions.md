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
# <a name="camera-and-image-capabilities-in-teams"></a><span data-ttu-id="c5cbc-104">Capacidades de cámara e imagen en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c5cbc-104">Camera and image capabilities in Teams</span></span>

>[!IMPORTANT]
>
> * <span data-ttu-id="c5cbc-105">Actualmente, la compatibilidad de Microsoft Teams con las capacidades de cámara y de imagen solo está disponible para los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-105">At present, Teams support for camera and image capabilities is only available for mobile clients.</span></span>
>* <span data-ttu-id="c5cbc-106">Las `selectMedia` `getMedia` API, y `viewImages` se pueden invocar desde varias superficies de Microsoft Teams, como módulos de tareas, pestañas y aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-106">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="c5cbc-107">Para obtener más información, _consulte_ [puntos de entrada para las aplicaciones de Microsoft Teams](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="c5cbc-107">For more details, _see_ [Entry points for Teams apps](../extensibility-points.md)</span></span>

<span data-ttu-id="c5cbc-108">Puede usar el  [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)para integrar fácilmente las capacidades de cámara y de imagen en su aplicación móvil de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-108">You can use the  [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), to easily integrate camera and image capabilities within your Microsoft Teams mobile app.</span></span> <span data-ttu-id="c5cbc-109">El SDK proporciona las herramientas necesarias para que su aplicación tenga acceso a [los permisos de dispositivo](native-device-permissions.md?tabs=desktop#device-permissions) de un usuario y cree una experiencia más enriquecida.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-109">The SDK provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md?tabs=desktop#device-permissions) and build a richer experience.</span></span>

<span data-ttu-id="c5cbc-110">Las API de [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)y [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) permiten usar capacidades nativas de cámara/imagen de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c5cbc-110">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native camera/image capabilities as follows:</span></span>

* <span data-ttu-id="c5cbc-111">Use el **control de cámara** nativo para permitir a los usuarios **capturar y adjuntar imágenes** en cualquier modo.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-111">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="c5cbc-112">Use la **compatibilidad con Galería** nativa para permitir que los usuarios **seleccionen imágenes de dispositivo** como datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-112">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="c5cbc-113">Use Native **Image Viewer control** para **obtener una vista previa de varias imágenes** a la vez.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-113">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="c5cbc-114">Admitir la **transferencia de imágenes de gran tamaño** (hasta 50 MB) a través del puente de SDK</span><span class="sxs-lookup"><span data-stu-id="c5cbc-114">Support **large image transfer** (up to 50 MB) via the SDK bridge</span></span>
* <span data-ttu-id="c5cbc-115">Admitir **capacidades avanzadas de imagen** que permiten a los usuarios obtener una vista previa de las imágenes y editarlas:</span><span class="sxs-lookup"><span data-stu-id="c5cbc-115">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="c5cbc-116">Digitalice el documento, la pizarra, las tarjetas de presentación, etc., a través de la cámara.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-116">Scan document, whiteboard, business cards, etc., through the camera.</span></span>
  * <span data-ttu-id="c5cbc-117">Recorte y gire las imágenes.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-117">Crop and rotate the images.</span></span>
  * <span data-ttu-id="c5cbc-118">Agregar texto, tinta o anotación a mano alzada a la imagen.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-118">Add text, ink, or freehand annotation to the image.</span></span>

## <a name="get-started"></a><span data-ttu-id="c5cbc-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="c5cbc-119">Get started</span></span>

<span data-ttu-id="c5cbc-120">Actualice la aplicación de Microsoft Teams [manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) el archivo; para ello, agregue la `devicePermissions`  propiedad y especifique `media` .</span><span class="sxs-lookup"><span data-stu-id="c5cbc-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions`  property and specifying `media`.</span></span> <span data-ttu-id="c5cbc-121">Esto permite a su aplicación solicitar los permisos necesarios a los usuarios finales antes de usar la cámara para capturar la imagen o abrir la galería para seleccionar una imagen para enviar como datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-121">This allows your app to ask for requisite permissions from end-users before they use the camera to capture the image or open the gallery to select an image to submit as an attachment.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="c5cbc-122">El mensaje de _solicitud de permisos_ se muestra automáticamente cuando se inicia una API de Teams pertinente.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-122">The _Request Permissions_ prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="c5cbc-123">Para obtener más información, *consulte* [solicitar permisos de dispositivo](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="c5cbc-123">For more details, *see* [Request device permissions](native-device-permissions.md).</span></span>

## <a name="using-camera-and-image-capability-apis"></a><span data-ttu-id="c5cbc-124">Usar las API de funcionalidad de cámara e imagen</span><span class="sxs-lookup"><span data-stu-id="c5cbc-124">Using camera and image capability APIs</span></span>

<span data-ttu-id="c5cbc-125">Puede usar el siguiente conjunto de API para habilitar las funciones de cámara y de dispositivo de imagen:</span><span class="sxs-lookup"><span data-stu-id="c5cbc-125">You can use the following set of APIs to enable camera and image device capabilities:</span></span>

| <span data-ttu-id="c5cbc-126">API</span><span class="sxs-lookup"><span data-stu-id="c5cbc-126">API</span></span>      | <span data-ttu-id="c5cbc-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="c5cbc-127">Description</span></span>   |
| --- | --- |
| [<span data-ttu-id="c5cbc-128">**selectMedia**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-128">**selectMedia**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| <span data-ttu-id="c5cbc-129">Esta API permite a los usuarios **capturar o seleccionar elementos multimedia de un dispositivo nativo** y volver a la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-129">This API allows users to **capture or select media from a native device** and return to the web-app.</span></span> <span data-ttu-id="c5cbc-130">Los usuarios pueden elegir entre editar, recortar, girar, anotar o dibujar sobre imágenes antes de enviarla.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-130">Users may choose to edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="c5cbc-131">En respuesta a **selectMedia**, la aplicación web recibirá identificadores de medios de las imágenes seleccionadas y puede recibir una miniatura de los medios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-131">In response to **selectMedia**, the web-app will receive media ids of selected images and may receive a thumbnail of the selected media.</span></span> |
| [<span data-ttu-id="c5cbc-132">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-132">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="c5cbc-133">Esta API recupera los medios en fragmentos, independientemente de su tamaño.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-133">This API retrieves the media in chunks irrespective of size.</span></span> <span data-ttu-id="c5cbc-134">Estos fragmentos se ensamblan y se envían de nuevo a la aplicación web como archivo/BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-134">These chunks are assembled and sent back to the web app as a file/blob.</span></span> <span data-ttu-id="c5cbc-135">Con esta API, la imagen se divide en fragmentos más pequeños para facilitar la transferencia de imágenes de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-135">With this API an image is broken into smaller chunks to facilitate large image transfer.</span></span> |
| [<span data-ttu-id="c5cbc-136">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-136">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="c5cbc-137">Esta API permite al usuario ver imágenes en modo de pantalla completa como una lista desplazable.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-137">This API enables the user to view images full-screen mode as a scrollable list.</span></span>|

<span data-ttu-id="c5cbc-138">**Experiencia de la aplicación web para SELECTMEDIA API** 
 ![ Experiencia de imagen y cámara de dispositivo en Microsoft Teams](../../assets/images/tabs/image-capability-screenshot.jpg)</span><span class="sxs-lookup"><span data-stu-id="c5cbc-138">**Web app experience for selectMedia API**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability-screenshot.jpg)</span></span>

## <a name="error-handling"></a><span data-ttu-id="c5cbc-139">Control de errores</span><span class="sxs-lookup"><span data-stu-id="c5cbc-139">Error handling</span></span>

<span data-ttu-id="c5cbc-140">Debe comprender los códigos de error de respuesta de la API y controlarlos correctamente.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-140">You should understand the API response error codes and handle them appropriately.</span></span> <span data-ttu-id="c5cbc-141">A continuación se muestra una lista de códigos de error que puede devolver la plataforma:</span><span class="sxs-lookup"><span data-stu-id="c5cbc-141">Below is a list of error codes that may be returned by the platform:</span></span>

|<span data-ttu-id="c5cbc-142">Código de error</span><span class="sxs-lookup"><span data-stu-id="c5cbc-142">Error code</span></span> |  <span data-ttu-id="c5cbc-143">Nombre del error</span><span class="sxs-lookup"><span data-stu-id="c5cbc-143">Error Name</span></span>     | <span data-ttu-id="c5cbc-144">Condition</span><span class="sxs-lookup"><span data-stu-id="c5cbc-144">Condition</span></span>|
| --- | --- | --- |
| <span data-ttu-id="c5cbc-145">**100**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-145">**100**</span></span> | <span data-ttu-id="c5cbc-146">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="c5cbc-146">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="c5cbc-147">La API no es compatible con la plataforma actual.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-147">API not supported in the current platform.</span></span>|
| <span data-ttu-id="c5cbc-148">**404**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-148">**404**</span></span> | <span data-ttu-id="c5cbc-149">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="c5cbc-149">FILE_NOT_FOUND</span></span> | <span data-ttu-id="c5cbc-150">No se encontró el archivo especificado en la ubicación indicada.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-150">The file specified was not found on the given location.</span></span>|
| <span data-ttu-id="c5cbc-151">**500**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-151">**500**</span></span> | <span data-ttu-id="c5cbc-152">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="c5cbc-152">INTERNAL_ERROR</span></span> | <span data-ttu-id="c5cbc-153">Error interno detectado al realizar la operación necesaria.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-153">Internal error encountered while performing the required operation.</span></span>|
| <span data-ttu-id="c5cbc-154">**1000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-154">**1000**</span></span> | <span data-ttu-id="c5cbc-155">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="c5cbc-155">PERMISSION_DENIED</span></span> |<span data-ttu-id="c5cbc-156">Permisos denegados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-156">Permissions denied by the user.</span></span>|
| <span data-ttu-id="c5cbc-157">**2000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-157">**2000**</span></span> |<span data-ttu-id="c5cbc-158">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="c5cbc-158">NETWORK_ERROR</span></span> | <span data-ttu-id="c5cbc-159">Problema de red.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-159">Network issue.</span></span>|
| <span data-ttu-id="c5cbc-160">**3000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-160">**3000**</span></span> | <span data-ttu-id="c5cbc-161">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="c5cbc-161">NO_HW_SUPPORT</span></span> | <span data-ttu-id="c5cbc-162">El hardware subyacente no admite la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-162">Underlying hardware doesn't support the capability.</span></span>|
| <span data-ttu-id="c5cbc-163">**4000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-163">**4000**</span></span>| <span data-ttu-id="c5cbc-164">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="c5cbc-164">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="c5cbc-165">Uno o más argumentos no son válidos.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-165">One or more arguments is invalid.</span></span>|
| <span data-ttu-id="c5cbc-166">**5000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-166">**5000**</span></span> | <span data-ttu-id="c5cbc-167">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="c5cbc-167">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="c5cbc-168">El usuario no está autorizado para completar esta operación.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-168">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="c5cbc-169">**6000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-169">**6000**</span></span> |<span data-ttu-id="c5cbc-170">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="c5cbc-170">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="c5cbc-171">La operación no se pudo completar debido a recursos insuficientes.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-171">The operation couldn't be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="c5cbc-172">**7000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-172">**7000**</span></span> | <span data-ttu-id="c5cbc-173">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="c5cbc-173">THROTTLE</span></span> | <span data-ttu-id="c5cbc-174">La plataforma ha limitado la solicitud porque la API se ha invocado con demasiada frecuencia.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-174">The platform throttled the request because the API was invoked too frequently.</span></span>|
|  <span data-ttu-id="c5cbc-175">**8000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-175">**8000**</span></span> | <span data-ttu-id="c5cbc-176">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="c5cbc-176">USER_ABORT</span></span> |<span data-ttu-id="c5cbc-177">El usuario ha anulado la operación.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-177">User aborted the operation.</span></span>|
| <span data-ttu-id="c5cbc-178">**9000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-178">**9000**</span></span>| <span data-ttu-id="c5cbc-179">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="c5cbc-179">OLD_PLATFORM</span></span> | <span data-ttu-id="c5cbc-180">El código de plataforma está obsoleto y no implementa esta API.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-180">The platform code is outdated and doesn't implement this API.</span></span>|
| <span data-ttu-id="c5cbc-181">**10000**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-181">**10000**</span></span>| <span data-ttu-id="c5cbc-182">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="c5cbc-182">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="c5cbc-183">El valor devuelto es demasiado grande y ha superado los límites de tamaño de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="c5cbc-183">The return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="sample-code-snippets"></a><span data-ttu-id="c5cbc-184">Ejemplos de fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="c5cbc-184">Sample code snippets</span></span>

<span data-ttu-id="c5cbc-185">**API de llamada `selectMedia`**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-185">**Calling `selectMedia` API**</span></span>

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

<span data-ttu-id="c5cbc-186">**API de llamada `getMedia`**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-186">**Calling `getMedia` API**</span></span>

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

<span data-ttu-id="c5cbc-187">**Llamar a la `viewImages`  API por ID.**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-187">**Calling `viewImages`  API by ID**</span></span>

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

<span data-ttu-id="c5cbc-188">**Llamar a la API viewImages por dirección URL**</span><span class="sxs-lookup"><span data-stu-id="c5cbc-188">**Calling viewImages API by URL**</span></span>

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
