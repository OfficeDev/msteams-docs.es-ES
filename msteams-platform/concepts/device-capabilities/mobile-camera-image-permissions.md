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
# <a name="integrate-media-capabilities"></a><span data-ttu-id="7f0b9-104">Integrar capacidades multimedia</span><span class="sxs-lookup"><span data-stu-id="7f0b9-104">Integrate media capabilities</span></span> 

<span data-ttu-id="7f0b9-105">Puedes integrar las capacidades nativas del dispositivo, como la **cámara** y el **micrófono** con la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-105">You can integrate native device capabilities, such as the **camera** and **microphone** with your Teams app.</span></span> <span data-ttu-id="7f0b9-106">Para la integración, puedes usar Microsoft Teams SDK de cliente de [JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona las herramientas necesarias para que la aplicación tenga acceso a los permisos [de dispositivo de un usuario.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="7f0b9-106">For integration, you can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="7f0b9-107">Usa las API de funcionalidad multimedia adecuadas para  integrar  las capacidades del dispositivo, como la cámara y el micrófono con la plataforma Teams dentro de la aplicación móvil de Microsoft Teams y crear una experiencia más enriquecte.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-107">Use suitable media capability APIs to integrate the device capabilities, such as **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="7f0b9-108">Ventaja de integrar capacidades multimedia</span><span class="sxs-lookup"><span data-stu-id="7f0b9-108">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="7f0b9-109">La principal ventaja de integrar las capacidades de dispositivo en las aplicaciones Teams es que aprovecha los controles Teams nativos para proporcionar una experiencia enriqueciendo e inmersiva a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-109">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="7f0b9-110">Para integrar las funcionalidades multimedia, debes actualizar el archivo de manifiesto de la aplicación y llamar a las API de funcionalidad multimedia.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-110">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="7f0b9-111">Para una integración eficaz, debe tener una buena comprensión de los fragmentos de código para llamar a las API [correspondientes,](#code-snippets) lo que le permite usar funcionalidades multimedia nativas.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-111">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="7f0b9-112">Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-112">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> * <span data-ttu-id="7f0b9-113">Actualmente, Microsoft Teams compatibilidad con funcionalidades multimedia solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-113">Currently, Microsoft Teams support for media capabilities is available for mobile clients only.</span></span>   
> * <span data-ttu-id="7f0b9-114">Actualmente, Teams no admite permisos de dispositivo para aplicaciones de varias ventanas, pestañas y el panel lateral de la reunión.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-114">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span>    

## <a name="update-manifest"></a><span data-ttu-id="7f0b9-115">Manifiesto de actualización</span><span class="sxs-lookup"><span data-stu-id="7f0b9-115">Update manifest</span></span>

<span data-ttu-id="7f0b9-116">Actualice el Teams aplicaciónmanifest.js[el archivo](../../resources/schema/manifest-schema.md#devicepermissions) agregando la propiedad `devicePermissions` y especificando `media` .</span><span class="sxs-lookup"><span data-stu-id="7f0b9-116">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="7f0b9-117">Permite a la aplicación solicitar los permisos necesarios a  los usuarios antes de empezar a usar la cámara para capturar  la imagen, abrir la galería para seleccionar una imagen para enviar como datos adjuntos o usar el micrófono para grabar la conversación.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-117">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span> <span data-ttu-id="7f0b9-118">La actualización del manifiesto de la aplicación es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-118">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="7f0b9-119">El **símbolo del sistema Solicitar permisos** se muestra automáticamente cuando se inicia una API de Teams relevante.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-119">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="7f0b9-120">Para obtener más información, consulta [Solicitar permisos de dispositivo](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="7f0b9-120">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="7f0b9-121">API de funcionalidad multimedia</span><span class="sxs-lookup"><span data-stu-id="7f0b9-121">Media capability APIs</span></span>

<span data-ttu-id="7f0b9-122">Las [API selectMedia,](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)y [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) permiten usar las funciones multimedia nativas de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-122">The [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="7f0b9-123">Usa el micrófono **nativo para** permitir a los usuarios grabar **audio** (grabar 10 minutos de conversación) desde el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-123">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="7f0b9-124">Usa el **control de cámara** nativa para permitir a los usuarios capturar y adjuntar **imágenes** sobre la marcha.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-124">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="7f0b9-125">Usa la compatibilidad **de galería nativa** para permitir a los usuarios seleccionar imágenes del dispositivo **como** datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-125">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="7f0b9-126">Usa el **control visor de imágenes nativo** para obtener una vista previa de varias **imágenes** a la vez.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-126">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="7f0b9-127">Admite **la transferencia de imágenes grandes** (de 1 MB a 50 MB) a través del puente sdk.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-127">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="7f0b9-128">Admite **funciones avanzadas de imagen** que permiten a los usuarios obtener una vista previa y editar imágenes:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-128">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="7f0b9-129">Digitalizar documentos, pizarras y tarjetas de presentación a través de la cámara.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-129">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
> * <span data-ttu-id="7f0b9-130">Las API , y se pueden invocar desde varias superficies Teams, como módulos de `selectMedia` `getMedia` `viewImages` tareas, pestañas y aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-130">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces, such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="7f0b9-131">Para obtener más información, consulta [Puntos de entrada para Teams aplicaciones](../extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="7f0b9-131">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
> * <span data-ttu-id="7f0b9-132">`selectMedia` La API se ha extendido para admitir propiedades de micrófono y audio.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-132">`selectMedia` API has been extended to support microphone and audio properties.</span></span>

<span data-ttu-id="7f0b9-133">Debes usar el siguiente conjunto de API para habilitar las capacidades multimedia del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-133">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="7f0b9-134">API</span><span class="sxs-lookup"><span data-stu-id="7f0b9-134">API</span></span>      | <span data-ttu-id="7f0b9-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="7f0b9-135">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="7f0b9-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="7f0b9-137">Esta API permite a los usuarios **capturar o seleccionar medios de la cámara del** dispositivo y devolverlo a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-137">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="7f0b9-138">Los usuarios pueden editar, recortar, girar, anotar o dibujar sobre imágenes antes del envío.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-138">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="7f0b9-139">En respuesta a , la aplicación web recibe los IDs multimedia de las imágenes seleccionadas `selectMedia` y una miniatura de los medios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-139">In response to `selectMedia`, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="7f0b9-140">Esta API se puede configurar aún más a través de [la configuración ImageProps.](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="7f0b9-140">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="7f0b9-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span><span class="sxs-lookup"><span data-stu-id="7f0b9-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="7f0b9-142">Establece el [mediaType en](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) `4` en la API para obtener acceso a la funcionalidad de `selectMedia` micrófono.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-142">Set the [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in `selectMedia` API for accessing microphone  capability.</span></span> <span data-ttu-id="7f0b9-143">Esta API también permite a los usuarios grabar audio desde el micrófono del dispositivo y devolver clips grabados a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-143">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="7f0b9-144">Los usuarios pueden pausar, volver a grabar y reproducir la vista previa de grabación antes del envío.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-144">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="7f0b9-145">En respuesta a **selectMedia,** la aplicación web recibe los IDs multimedia de la grabación de audio seleccionada.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-145">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="7f0b9-146">Use `maxDuration` , si necesita configurar una duración en minutos para grabar la conversación.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-146">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="7f0b9-147">La duración actual de la grabación es de 10 minutos, después de lo cual finaliza la grabación.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-147">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="7f0b9-148">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-148">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="7f0b9-149">Esta API recupera los medios capturados por `selectMedia` la API en fragmentos, independientemente del tamaño de los medios.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-149">This API retrieves the media captured by `selectMedia` API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="7f0b9-150">Estos fragmentos se ensamblan y se envían a la aplicación web como un archivo o blob.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-150">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="7f0b9-151">Dividir los medios en fragmentos más pequeños facilita la transferencia de archivos de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-151">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="7f0b9-152">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-152">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="7f0b9-153">Esta API permite al usuario ver imágenes en modo de pantalla completa como una lista desplazable.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-153">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|

<span data-ttu-id="7f0b9-154">En la siguiente imagen se muestra la experiencia de la aplicación web `selectMedia` de api para la funcionalidad de imagen:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-154">The following image depicts web app experience of `selectMedia` API for image capability:</span></span>

![cámara de dispositivo y experiencia de imagen en Teams](../../assets/images/tabs/image-capability.png)

<span data-ttu-id="7f0b9-156">En la siguiente imagen se muestra la experiencia de la aplicación web `selectMedia` de la API para la funcionalidad de micrófono:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-156">The following image depicts web app experience of `selectMedia` API for microphone capability:</span></span>

![experiencia de aplicación web para la funcionalidad de micrófono](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a><span data-ttu-id="7f0b9-158">Control de errores</span><span class="sxs-lookup"><span data-stu-id="7f0b9-158">Error handling</span></span>

<span data-ttu-id="7f0b9-159">Debes asegurarte de controlar estos errores correctamente en tu Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-159">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="7f0b9-160">En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-160">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="7f0b9-161">Código de error</span><span class="sxs-lookup"><span data-stu-id="7f0b9-161">Error code</span></span> |  <span data-ttu-id="7f0b9-162">Nombre del error</span><span class="sxs-lookup"><span data-stu-id="7f0b9-162">Error name</span></span>     | <span data-ttu-id="7f0b9-163">Condition</span><span class="sxs-lookup"><span data-stu-id="7f0b9-163">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="7f0b9-164">**100**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-164">**100**</span></span> | <span data-ttu-id="7f0b9-165">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="7f0b9-165">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="7f0b9-166">La API no se admite en la plataforma actual.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-166">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="7f0b9-167">**404**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-167">**404**</span></span> | <span data-ttu-id="7f0b9-168">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="7f0b9-168">FILE_NOT_FOUND</span></span> | <span data-ttu-id="7f0b9-169">El archivo especificado no se encuentra en la ubicación determinada.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-169">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="7f0b9-170">**500**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-170">**500**</span></span> | <span data-ttu-id="7f0b9-171">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="7f0b9-171">INTERNAL_ERROR</span></span> | <span data-ttu-id="7f0b9-172">Se produce un error interno al realizar la operación necesaria.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-172">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="7f0b9-173">**1000**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-173">**1000**</span></span> | <span data-ttu-id="7f0b9-174">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="7f0b9-174">PERMISSION_DENIED</span></span> |<span data-ttu-id="7f0b9-175">El usuario deniega el permiso.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-175">Permission is denied by the user.</span></span>|
| <span data-ttu-id="7f0b9-176">**3000**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-176">**3000**</span></span> | <span data-ttu-id="7f0b9-177">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="7f0b9-177">NO_HW_SUPPORT</span></span> | <span data-ttu-id="7f0b9-178">El hardware subyacente no admite la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-178">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="7f0b9-179">**4000**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-179">**4000**</span></span>| <span data-ttu-id="7f0b9-180">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="7f0b9-180">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="7f0b9-181">Uno o más argumentos no son válidos.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-181">One or more arguments are invalid.</span></span>|
|  <span data-ttu-id="7f0b9-182">**8000**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-182">**8000**</span></span> | <span data-ttu-id="7f0b9-183">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="7f0b9-183">USER_ABORT</span></span> |<span data-ttu-id="7f0b9-184">El usuario anula la operación.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-184">User aborts the operation.</span></span>|
| <span data-ttu-id="7f0b9-185">**9000**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-185">**9000**</span></span>| <span data-ttu-id="7f0b9-186">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="7f0b9-186">OLD_PLATFORM</span></span> | <span data-ttu-id="7f0b9-187">El código de la plataforma está obsoleto y no implementa esta API.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-187">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="7f0b9-188">**10000**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-188">**10000**</span></span>| <span data-ttu-id="7f0b9-189">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="7f0b9-189">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="7f0b9-190">El valor devuelto es demasiado grande y ha superado los límites de tamaño de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="7f0b9-190">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="7f0b9-191">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="7f0b9-191">Code snippets</span></span>

<span data-ttu-id="7f0b9-192">**Llamada `selectMedia` API** para capturar imágenes con cámara:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-192">**Calling `selectMedia` API** for capturing images using camera:</span></span>

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

<span data-ttu-id="7f0b9-193">**Llamada `getMedia` API** para recuperar medios grandes en fragmentos:</span><span class="sxs-lookup"><span data-stu-id="7f0b9-193">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

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

<span data-ttu-id="7f0b9-194">**Llamada `viewImages` API por identificador devuelto por `selectMedia` API:**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-194">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

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

<span data-ttu-id="7f0b9-195">**Llamada `viewImages` API por dirección URL:**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-195">**Calling `viewImages` API by URL**:</span></span>

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

<span data-ttu-id="7f0b9-196">**Llamadas `selectMedia` y API para grabar audio a través del `getMedia` micrófono:**</span><span class="sxs-lookup"><span data-stu-id="7f0b9-196">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="7f0b9-197">Consulte también</span><span class="sxs-lookup"><span data-stu-id="7f0b9-197">See also</span></span>

* [<span data-ttu-id="7f0b9-198">Integrar la funcionalidad de escáner de códigos QR o códigos de barras en Teams</span><span class="sxs-lookup"><span data-stu-id="7f0b9-198">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="7f0b9-199">Integrar las capacidades de ubicación en Teams</span><span class="sxs-lookup"><span data-stu-id="7f0b9-199">Integrate location capabilities in Teams</span></span>](location-capability.md)
* [<span data-ttu-id="7f0b9-200">Integrar la funcionalidad selector de personas en Teams</span><span class="sxs-lookup"><span data-stu-id="7f0b9-200">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)

