---
title: Integración de la funcionalidad selector de personas
author: Rajeshwari-v
description: Cómo usar Teams SDK de cliente de JavaScript para integrar la funcionalidad selector de personas
keywords: control de selector de personas
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 8399eeb1a088e4b60c466d51c223b9405ebf1711
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211644"
---
# <a name="integrate-people-picker-capability"></a><span data-ttu-id="2a92f-104">Integración de la funcionalidad selector de personas</span><span class="sxs-lookup"><span data-stu-id="2a92f-104">Integrate People Picker capability</span></span> 

<span data-ttu-id="2a92f-105">Selector de personas es un control para buscar y seleccionar personas.</span><span class="sxs-lookup"><span data-stu-id="2a92f-105">People Picker is a control to search and select people.</span></span> <span data-ttu-id="2a92f-106">Esta es una funcionalidad nativa disponible en Teams plataforma.</span><span class="sxs-lookup"><span data-stu-id="2a92f-106">This is a native capability available in Teams platform.</span></span> <span data-ttu-id="2a92f-107">Puedes integrar Teams de entrada del selector de personas nativo con tus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="2a92f-107">You can integrate Teams native People Picker input control with your web apps.</span></span> <span data-ttu-id="2a92f-108">Puede seleccionar entre una o varias selecciones y configuraciones, como limitar la búsqueda en un chat, canales o en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="2a92f-108">You can select between single or multi selection, and configurations, such as limiting search within a chat, channels, or across the entire organization.</span></span>

<span data-ttu-id="2a92f-109">Puedes usar Microsoft Teams [SDK de cliente de JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona API para integrar la funcionalidad selector de personas dentro de la aplicación `selectPeople` web.</span><span class="sxs-lookup"><span data-stu-id="2a92f-109">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides `selectPeople` API to integrate the People Picker capability within your web app.</span></span> 

## <a name="advantages-of-integrating-people-picker-capability"></a><span data-ttu-id="2a92f-110">Ventajas de integrar la funcionalidad selector de personas</span><span class="sxs-lookup"><span data-stu-id="2a92f-110">Advantages of integrating People Picker capability</span></span>

* <span data-ttu-id="2a92f-111">El control Selector de personas funciona en todas Teams superficies, como un módulo de tareas, un chat, un canal, una pestaña de reunión y una aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="2a92f-111">The People Picker control works in all of Teams surfaces, such as task module, a chat, channel, meeting tab, and personal app.</span></span>
* <span data-ttu-id="2a92f-112">Este control le permite buscar y seleccionar usuarios dentro de un chat, canal o toda la organización.</span><span class="sxs-lookup"><span data-stu-id="2a92f-112">This control allows you to search for and select users within a chat, channel, or the entire organization.</span></span>
*  <span data-ttu-id="2a92f-113">La funcionalidad Selector de personas ayuda con escenarios que implican la asignación de tareas, el etiquetado y la notificación a un usuario.</span><span class="sxs-lookup"><span data-stu-id="2a92f-113">The People Picker capability helps with scenarios involving task assignment, tagging, notifying a user.</span></span> 
* <span data-ttu-id="2a92f-114">Puedes usar este control fácilmente disponible en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2a92f-114">You can use this readily available control in your web app.</span></span> <span data-ttu-id="2a92f-115">Ahorra el esfuerzo y el tiempo de forma significativa para crear un control de este tipo por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="2a92f-115">It saves the effort and time significantly to build such a control on your own.</span></span>

<span data-ttu-id="2a92f-116">Debes llamar a la API para integrar el control selector de personas `selectPeople` en tu Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a92f-116">You must call the `selectPeople` API to integrate People Picker control in your Teams app.</span></span> <span data-ttu-id="2a92f-117">Para una integración eficaz, debe comprender el fragmento de [código](#code-snippet) para llamar a la API.</span><span class="sxs-lookup"><span data-stu-id="2a92f-117">For effective integration, you must have an understanding of [code snippet](#code-snippet) for calling the API.</span></span> <span data-ttu-id="2a92f-118">Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2a92f-118">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your web app.</span></span>

> [!NOTE] 
> <span data-ttu-id="2a92f-119">Actualmente, Microsoft Teams compatibilidad con la funcionalidad selector de personas solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="2a92f-119">Currently, Microsoft Teams support for People Picker capability is available for mobile clients only.</span></span>

## <a name="selectpeople-api"></a><span data-ttu-id="2a92f-120">`selectPeople` API</span><span class="sxs-lookup"><span data-stu-id="2a92f-120">`selectPeople` API</span></span> 

<span data-ttu-id="2a92f-121">`selectPeople`La API le permite agregar Teams nativa `People Picker input control` a las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="2a92f-121">`selectPeople` API enables you to add Teams native `People Picker input control` to your web apps.</span></span>  
<span data-ttu-id="2a92f-122">La descripción de la API es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a92f-122">The API description is as follows:</span></span>

| <span data-ttu-id="2a92f-123">API</span><span class="sxs-lookup"><span data-stu-id="2a92f-123">API</span></span>      | <span data-ttu-id="2a92f-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a92f-124">Description</span></span>  |
| --- | --- |
|<span data-ttu-id="2a92f-125">**selectPeople**</span><span class="sxs-lookup"><span data-stu-id="2a92f-125">**selectPeople**</span></span>|<span data-ttu-id="2a92f-126">Inicia un selector de personas y permite al usuario buscar y seleccionar una o más personas de la lista.</span><span class="sxs-lookup"><span data-stu-id="2a92f-126">Launches a People Picker and allows the user to search and select one or more people from the list.</span></span><br/><br/><span data-ttu-id="2a92f-127">Esta API devuelve el identificador, el nombre y la dirección de correo electrónico de los usuarios seleccionados a la aplicación web de llamada.</span><span class="sxs-lookup"><span data-stu-id="2a92f-127">This API returns the ID, name and email address of selected users to the calling web app.</span></span><br/><br/><span data-ttu-id="2a92f-128">En caso de una aplicación personal, el control busca en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="2a92f-128">In case of a personal app, the control searches across the organization.</span></span> <span data-ttu-id="2a92f-129">Si la aplicación se agrega a un chat o canal, el contexto de búsqueda se configura según el escenario.</span><span class="sxs-lookup"><span data-stu-id="2a92f-129">If the app is added to a chat or channel, then the search context is configured depending on the scenario.</span></span> <span data-ttu-id="2a92f-130">La búsqueda está restringida dentro de los miembros de ese chat, canal o disponible en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="2a92f-130">The search is restricted within the members of that chat, channel, or made available across the organization.</span></span>|

<span data-ttu-id="2a92f-131">La `selectPeople` API incluye las siguientes configuraciones de entrada:</span><span class="sxs-lookup"><span data-stu-id="2a92f-131">The `selectPeople` API comes along with following input configurations:</span></span>

|<span data-ttu-id="2a92f-132">Parámetro Configuration</span><span class="sxs-lookup"><span data-stu-id="2a92f-132">Configuration parameter</span></span>|<span data-ttu-id="2a92f-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="2a92f-133">Type</span></span>|<span data-ttu-id="2a92f-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a92f-134">Description</span></span>| <span data-ttu-id="2a92f-135">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2a92f-135">Default value</span></span>|
|-----|------|--------------|------|
|`title`| <span data-ttu-id="2a92f-136">Cadena</span><span class="sxs-lookup"><span data-stu-id="2a92f-136">String</span></span>| <span data-ttu-id="2a92f-137">Es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="2a92f-137">It is an optional parameter.</span></span> <span data-ttu-id="2a92f-138">Establece el título del control Selector de personas.</span><span class="sxs-lookup"><span data-stu-id="2a92f-138">It sets title for the People Picker control.</span></span> | <span data-ttu-id="2a92f-139">Seleccionar personas</span><span class="sxs-lookup"><span data-stu-id="2a92f-139">Select people</span></span>|
|`setSelected`|<span data-ttu-id="2a92f-140">Cadena</span><span class="sxs-lookup"><span data-stu-id="2a92f-140">String</span></span>| <span data-ttu-id="2a92f-141">Es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="2a92f-141">It is an optional parameter.</span></span> <span data-ttu-id="2a92f-142">Debe pasar los ID de AAD de las personas que se elegirán previamente.</span><span class="sxs-lookup"><span data-stu-id="2a92f-142">You must pass AAD IDs of the people to be preselected.</span></span> <span data-ttu-id="2a92f-143">Este parámetro preselecciona a los usuarios al iniciar el control Selector de personas.</span><span class="sxs-lookup"><span data-stu-id="2a92f-143">This parameter preselects people while launching the People Picker control.</span></span> <span data-ttu-id="2a92f-144">En caso de selección única, solo el primer usuario válido se prepopultó ignorando el resto.</span><span class="sxs-lookup"><span data-stu-id="2a92f-144">In case of single selection, only the first valid user is prepopulated ignoring the rest.</span></span> |<span data-ttu-id="2a92f-145">Null</span><span class="sxs-lookup"><span data-stu-id="2a92f-145">Null</span></span>| 
|`openOrgWideSearchInChatOrChannel`|<span data-ttu-id="2a92f-146">Booleano</span><span class="sxs-lookup"><span data-stu-id="2a92f-146">Boolean</span></span> | <span data-ttu-id="2a92f-147">Es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="2a92f-147">It is an optional parameter.</span></span> <span data-ttu-id="2a92f-148">Cuando se establece en true, inicia el Selector de personas en el ámbito de toda la organización incluso si la aplicación se agrega a un chat o canal.</span><span class="sxs-lookup"><span data-stu-id="2a92f-148">When it is set to true, it launches the People Picker in organization wide scope even if the app is added to a chat or channel.</span></span> |<span data-ttu-id="2a92f-149">Falso</span><span class="sxs-lookup"><span data-stu-id="2a92f-149">False</span></span>|
|`singleSelect`|<span data-ttu-id="2a92f-150">Booleano</span><span class="sxs-lookup"><span data-stu-id="2a92f-150">Boolean</span></span>|<span data-ttu-id="2a92f-151">Es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="2a92f-151">It is an optional parameter.</span></span> <span data-ttu-id="2a92f-152">Cuando se establece en true, inicia el Selector de personas que restringe la selección a un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="2a92f-152">When it is set to true, it launches the People Picker restricting the selection to one user only.</span></span> |<span data-ttu-id="2a92f-153">Falso</span><span class="sxs-lookup"><span data-stu-id="2a92f-153">False</span></span>|

<span data-ttu-id="2a92f-154">En la siguiente imagen se muestra la experiencia de la funcionalidad selector de personas en una aplicación web de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2a92f-154">The following image depicts the experience of People Picker capability in a sample web app:</span></span>

![Experiencia de la aplicación web de la funcionalidad selector de personas](../../assets/images/tabs/people-picker-control-capability.png)

### <a name="code-snippet"></a><span data-ttu-id="2a92f-156">Fragmento de código</span><span class="sxs-lookup"><span data-stu-id="2a92f-156">Code snippet</span></span>

<span data-ttu-id="2a92f-157">**Llamada `selectPeople` API** para seleccionar personas de una lista:</span><span class="sxs-lookup"><span data-stu-id="2a92f-157">**Calling `selectPeople` API** to select people from a list:</span></span>

```javascript
 microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  });
```

## <a name="error-handling"></a><span data-ttu-id="2a92f-158">Control de errores</span><span class="sxs-lookup"><span data-stu-id="2a92f-158">Error handling</span></span>

<span data-ttu-id="2a92f-159">Debes asegurarte de controlar los errores correctamente en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2a92f-159">You must ensure to handle the errors appropriately in your web app.</span></span> <span data-ttu-id="2a92f-160">En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:</span><span class="sxs-lookup"><span data-stu-id="2a92f-160">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="2a92f-161">Código de error</span><span class="sxs-lookup"><span data-stu-id="2a92f-161">Error code</span></span> |  <span data-ttu-id="2a92f-162">Nombre del error</span><span class="sxs-lookup"><span data-stu-id="2a92f-162">Error name</span></span>     | <span data-ttu-id="2a92f-163">Condition</span><span class="sxs-lookup"><span data-stu-id="2a92f-163">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="2a92f-164">**100**</span><span class="sxs-lookup"><span data-stu-id="2a92f-164">**100**</span></span> | <span data-ttu-id="2a92f-165">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="2a92f-165">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="2a92f-166">La API no se admite en la plataforma actual.</span><span class="sxs-lookup"><span data-stu-id="2a92f-166">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="2a92f-167">**500**</span><span class="sxs-lookup"><span data-stu-id="2a92f-167">**500**</span></span> | <span data-ttu-id="2a92f-168">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="2a92f-168">INTERNAL_ERROR</span></span> | <span data-ttu-id="2a92f-169">Se produce un error interno al iniciar el Selector de personas.</span><span class="sxs-lookup"><span data-stu-id="2a92f-169">Internal error is encountered while launching People Picker.</span></span>|
| <span data-ttu-id="2a92f-170">**4000**</span><span class="sxs-lookup"><span data-stu-id="2a92f-170">**4000**</span></span> | <span data-ttu-id="2a92f-171">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="2a92f-171">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="2a92f-172">La API se invoca con argumentos obligatorios incorrectos o insuficientes.</span><span class="sxs-lookup"><span data-stu-id="2a92f-172">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="2a92f-173">**8000**</span><span class="sxs-lookup"><span data-stu-id="2a92f-173">**8000**</span></span> | <span data-ttu-id="2a92f-174">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="2a92f-174">USER_ABORT</span></span> |<span data-ttu-id="2a92f-175">El usuario canceló la operación.</span><span class="sxs-lookup"><span data-stu-id="2a92f-175">User cancelled the operation.</span></span>|
| <span data-ttu-id="2a92f-176">**9000**</span><span class="sxs-lookup"><span data-stu-id="2a92f-176">**9000**</span></span> | <span data-ttu-id="2a92f-177">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="2a92f-177">OLD_PLATFORM</span></span> | <span data-ttu-id="2a92f-178">El usuario se encuentra en una compilación de plataforma antigua donde la implementación de la API no está presente.</span><span class="sxs-lookup"><span data-stu-id="2a92f-178">User is on old platform build where implementation of the API is not present.</span></span>  <span data-ttu-id="2a92f-179">La actualización de la compilación resuelve el problema.</span><span class="sxs-lookup"><span data-stu-id="2a92f-179">Upgrading the build resolves the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="2a92f-180">Consulte también</span><span class="sxs-lookup"><span data-stu-id="2a92f-180">See also</span></span>

* [<span data-ttu-id="2a92f-181">Integrar funcionalidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="2a92f-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="2a92f-182">Integrar la funcionalidad de escáner de código QR o código de barras en Teams</span><span class="sxs-lookup"><span data-stu-id="2a92f-182">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="2a92f-183">Integrar las capacidades de ubicación en Teams</span><span class="sxs-lookup"><span data-stu-id="2a92f-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
