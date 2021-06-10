---
title: Definir comandos de búsqueda de extensión de mensajería
author: clearab
description: Definir comandos de búsqueda de extensión de mensajería para Microsoft Teams aplicaciones.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 19f1fdf7bd4efdbb0de11d1abad341ec24bc27bd
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696808"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="2e2cb-103">Definir comandos de búsqueda de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="2e2cb-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="2e2cb-104">Los comandos de búsqueda de extensión de mensajería permiten a los usuarios buscar sistemas externos e insertar los resultados de esa búsqueda en un mensaje en forma de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-104">Messaging extension search commands allow users to search external systems and insert the results of that search into a message in the form of a card.</span></span> <span data-ttu-id="2e2cb-105">Este documento le guía sobre cómo seleccionar ubicaciones de invocar comandos de búsqueda y agregar el comando de búsqueda al manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-105">This document guides you on how to select  search command invoke locations, and add the search command to your app manifest.</span></span>

> [!NOTE]
> <span data-ttu-id="2e2cb-106">El límite de tamaño de la tarjeta de resultados es de 28 KB.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-106">The result card size limit is 28 KB.</span></span> <span data-ttu-id="2e2cb-107">La tarjeta no se envía si su tamaño supera los 28 KB.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-107">The card is not sent if its size exceeds 28 KB.</span></span>

## <a name="select-search-command-invoke-locations"></a><span data-ttu-id="2e2cb-108">Seleccionar ubicaciones de invocación de comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="2e2cb-108">Select search command invoke locations</span></span>

<span data-ttu-id="2e2cb-109">El comando de búsqueda se invoca desde una o ambas de las siguientes ubicaciones:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-109">The search command is invoked from any one or both of the following locations:</span></span>

* <span data-ttu-id="2e2cb-110">Área de redacción de mensajes: los botones situados en la parte inferior del área del mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-110">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="2e2cb-111">Cuadro de comando: @mentioning en el cuadro de comandos.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-111">Command box: By @mentioning in the command box.</span></span>

<span data-ttu-id="2e2cb-112">Cuando se invoca el comando de búsqueda desde el área del mensaje de redacción, el usuario envía los resultados a la conversación.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-112">When search command is invoked from the compose message area, the user sends the results to the conversation.</span></span> <span data-ttu-id="2e2cb-113">Cuando se invoca desde el cuadro de comandos, el usuario interactúa con la tarjeta resultante o la copia para su uso en otro lugar.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-113">When it is invoked from the command box, the user interacts with the resulting card, or copies it for use elsewhere.</span></span>

<span data-ttu-id="2e2cb-114">En la siguiente imagen se muestran las ubicaciones de invocación del comando de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-114">The following image displays the invoke locations of the search command:</span></span>

![Ubicaciones de invocar comandos de búsqueda](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a><span data-ttu-id="2e2cb-116">Agregar el comando de búsqueda al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2e2cb-116">Add the search command to your app manifest</span></span>

<span data-ttu-id="2e2cb-117">Para agregar el comando de búsqueda al manifiesto de la aplicación, debes agregar un nuevo objeto al nivel superior del JSON del `composeExtension` manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-117">To add the search command to your app manifest, you must add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="2e2cb-118">Puedes agregar el comando de búsqueda con la ayuda de App Studio o manualmente.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-118">You can add the search command either with the help of App Studio, or manually.</span></span>

### <a name="create-a-search-command-using-app-studio"></a><span data-ttu-id="2e2cb-119">Crear un comando de búsqueda con App Studio</span><span class="sxs-lookup"><span data-stu-id="2e2cb-119">Create a search command using App Studio</span></span>

<span data-ttu-id="2e2cb-120">El requisito previo para crear un comando de búsqueda es que ya debe haber creado una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-120">The prerequisite to create a search command is that you must already have created a messaging extension.</span></span> <span data-ttu-id="2e2cb-121">Para obtener información sobre cómo crear una extensión de mensajería, vea [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2e2cb-121">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="2e2cb-122">**Para crear un comando de búsqueda**</span><span class="sxs-lookup"><span data-stu-id="2e2cb-122">**To create a search command**</span></span>

1. <span data-ttu-id="2e2cb-123">Abre **App Studio** desde el Microsoft Teams y selecciona la pestaña Editor **de** manifiestos.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-123">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1.  <span data-ttu-id="2e2cb-124">Si ya creaste el paquete de la aplicación **en App Studio,** selecciona de la lista.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-124">If you already created your app package in **App Studio**, select from the list.</span></span> <span data-ttu-id="2e2cb-125">Si no has creado un paquete de aplicación, importa uno existente.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-125">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="2e2cb-126">Después de importar el paquete de la aplicación, selecciona **Extensiones de mensajería en** **Funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-126">After importing app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="2e2cb-127">Obtiene una ventana emergente para configurar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-127">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="2e2cb-128">Selecciona **Configurar en la** ventana para incluir la extensión de mensajería en la experiencia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-128">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="2e2cb-129">En la siguiente imagen se muestra la página de configuración de extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-129">The following image displays the messaging extension set up page:</span></span> 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. <span data-ttu-id="2e2cb-130">Para crear la extensión de mensajería, necesita un bot registrado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-130">To create the messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="2e2cb-131">Puede usar un bot existente o crear un bot nuevo.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-131">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="2e2cb-132">Seleccione **Crear nueva opción de bot,** asigne un nombre al nuevo bot y seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-132">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="2e2cb-133">En la siguiente imagen se muestra la creación de bots para la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-133">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="2e2cb-134">Seleccione **Agregar** en la **sección Comando** de la página extensiones de mensajería para incluir los comandos que deciden el comportamiento de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-134">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="2e2cb-135">La siguiente imagen muestra la adición de comandos para la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-135">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. <span data-ttu-id="2e2cb-136">Seleccione **Permitir que los usuarios consulten su servicio para obtener información e insertarla en un mensaje**.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-136">Select **Allow users to query your service for information and insert that into a message**.</span></span> <span data-ttu-id="2e2cb-137">La siguiente imagen muestra la selección del parámetro de comando de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-137">The following image displays the search command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. <span data-ttu-id="2e2cb-138">Agregue un **identificador de comando** y un **título**.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-138">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="2e2cb-139">Seleccione la ubicación desde la que se debe invocar el comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-139">Select the location from where your search command must be invoked.</span></span> <span data-ttu-id="2e2cb-140">Seleccionar mensaje **no** modifica actualmente el comportamiento del comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-140">Selecting **message** does not currently alter the behavior of your search command.</span></span> <span data-ttu-id="2e2cb-141">La siguiente imagen muestra la ubicación de invocación del comando de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-141">The following image displays the search command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. <span data-ttu-id="2e2cb-142">Agregue el parámetro de búsqueda y **seleccione Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-142">Add your search parameter and select **Save**.</span></span>

### <a name="create-a-search-command-manually"></a><span data-ttu-id="2e2cb-143">Crear un comando de búsqueda manualmente</span><span class="sxs-lookup"><span data-stu-id="2e2cb-143">Create a search command manually</span></span> 

<span data-ttu-id="2e2cb-144">Para agregar manualmente el comando de búsqueda de extensión de mensajería al manifiesto de la aplicación, debes agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-144">To manually add your messaging extension search command to your app manifest, you must add the following parameters to your `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="2e2cb-145">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="2e2cb-145">Property name</span></span> | <span data-ttu-id="2e2cb-146">Objetivo</span><span class="sxs-lookup"><span data-stu-id="2e2cb-146">Purpose</span></span> | <span data-ttu-id="2e2cb-147">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="2e2cb-147">Required?</span></span> | <span data-ttu-id="2e2cb-148">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="2e2cb-148">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="2e2cb-149">Esta propiedad es un identificador único que se asigna al comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-149">This property is an unique ID that you assign to search command.</span></span> <span data-ttu-id="2e2cb-150">La solicitud de usuario incluye este identificador.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-150">The user request includes this ID.</span></span> | <span data-ttu-id="2e2cb-151">Sí</span><span class="sxs-lookup"><span data-stu-id="2e2cb-151">Yes</span></span> | <span data-ttu-id="2e2cb-152">1.0</span><span class="sxs-lookup"><span data-stu-id="2e2cb-152">1.0</span></span> |
| `title` | <span data-ttu-id="2e2cb-153">Esta propiedad es un nombre de comando.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-153">This property is a command name.</span></span> <span data-ttu-id="2e2cb-154">Este valor aparece en la interfaz de usuario (UI).</span><span class="sxs-lookup"><span data-stu-id="2e2cb-154">This value appears in the user interface (UI).</span></span> | <span data-ttu-id="2e2cb-155">Sí</span><span class="sxs-lookup"><span data-stu-id="2e2cb-155">Yes</span></span> | <span data-ttu-id="2e2cb-156">1.0</span><span class="sxs-lookup"><span data-stu-id="2e2cb-156">1.0</span></span> |
| `description` | <span data-ttu-id="2e2cb-157">Esta propiedad es un texto de ayuda que indica lo que hace este comando.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-157">This property is a help text indicating what this command does.</span></span> <span data-ttu-id="2e2cb-158">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-158">This value appears in the UI.</span></span> | <span data-ttu-id="2e2cb-159">Sí</span><span class="sxs-lookup"><span data-stu-id="2e2cb-159">Yes</span></span> | <span data-ttu-id="2e2cb-160">1.0</span><span class="sxs-lookup"><span data-stu-id="2e2cb-160">1.0</span></span> |
| `type` | <span data-ttu-id="2e2cb-161">Esta propiedad debe ser `query` un .</span><span class="sxs-lookup"><span data-stu-id="2e2cb-161">This property must be a `query`.</span></span> | <span data-ttu-id="2e2cb-162">No</span><span class="sxs-lookup"><span data-stu-id="2e2cb-162">No</span></span> | <span data-ttu-id="2e2cb-163">1.4</span><span class="sxs-lookup"><span data-stu-id="2e2cb-163">1.4</span></span> |
|`initialRun` | <span data-ttu-id="2e2cb-164">Si esta propiedad se establece en **true,** indica que este comando debe ejecutarse tan pronto como el usuario seleccione este comando en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-164">If this property is set to **true**, it indicates this command should be executed as soon as the user selects this command in the UI.</span></span> | <span data-ttu-id="2e2cb-165">No</span><span class="sxs-lookup"><span data-stu-id="2e2cb-165">No</span></span> | <span data-ttu-id="2e2cb-166">1.0</span><span class="sxs-lookup"><span data-stu-id="2e2cb-166">1.0</span></span> |
| `context` | <span data-ttu-id="2e2cb-167">Esta propiedad es una matriz opcional de valores que define el contexto en el que está disponible la acción de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-167">This property is an optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="2e2cb-168">Los valores posibles son`message`, `compose` o `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-168">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="2e2cb-169">El valor predeterminado es `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-169">The default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="2e2cb-170">No</span><span class="sxs-lookup"><span data-stu-id="2e2cb-170">No</span></span> | <span data-ttu-id="2e2cb-171">1,5</span><span class="sxs-lookup"><span data-stu-id="2e2cb-171">1.5</span></span> |

<span data-ttu-id="2e2cb-172">Debe agregar los detalles del parámetro de búsqueda, que define el texto visible para el usuario en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-172">You must add the details of the search parameter, that defines the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="2e2cb-173">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="2e2cb-173">Property name</span></span> | <span data-ttu-id="2e2cb-174">Objetivo</span><span class="sxs-lookup"><span data-stu-id="2e2cb-174">Purpose</span></span> | <span data-ttu-id="2e2cb-175">¿Es necesario?</span><span class="sxs-lookup"><span data-stu-id="2e2cb-175">Is required?</span></span> | <span data-ttu-id="2e2cb-176">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="2e2cb-176">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="2e2cb-177">Esta propiedad define una lista estática de parámetros para el comando.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-177">This property defines a static list of parameters for the command.</span></span> | <span data-ttu-id="2e2cb-178">No</span><span class="sxs-lookup"><span data-stu-id="2e2cb-178">No</span></span> | <span data-ttu-id="2e2cb-179">1.0</span><span class="sxs-lookup"><span data-stu-id="2e2cb-179">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="2e2cb-180">Esta propiedad describe el nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-180">This property describes the name of the parameter.</span></span> <span data-ttu-id="2e2cb-181">Esto se envía al servicio en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-181">This is sent to your service in the user request.</span></span> | <span data-ttu-id="2e2cb-182">Sí</span><span class="sxs-lookup"><span data-stu-id="2e2cb-182">Yes</span></span> | <span data-ttu-id="2e2cb-183">1.0</span><span class="sxs-lookup"><span data-stu-id="2e2cb-183">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="2e2cb-184">Esta propiedad describe los propósitos del parámetro o el ejemplo del valor que se debe proporcionar.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-184">This property describes the parameter’s purposes or example of the value that must be provided.</span></span> <span data-ttu-id="2e2cb-185">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-185">This value appears in the UI.</span></span> | <span data-ttu-id="2e2cb-186">Sí</span><span class="sxs-lookup"><span data-stu-id="2e2cb-186">Yes</span></span> | <span data-ttu-id="2e2cb-187">1.0</span><span class="sxs-lookup"><span data-stu-id="2e2cb-187">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="2e2cb-188">Esta propiedad es un título o etiqueta de parámetros fáciles de usar.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-188">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="2e2cb-189">Sí</span><span class="sxs-lookup"><span data-stu-id="2e2cb-189">Yes</span></span> | <span data-ttu-id="2e2cb-190">1.0</span><span class="sxs-lookup"><span data-stu-id="2e2cb-190">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="2e2cb-191">Esta propiedad se establece en el tipo de entrada necesaria.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-191">This property is set to the type of the input required.</span></span> <span data-ttu-id="2e2cb-192">Los valores posibles `text` incluyen , , , , , `textarea` `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="2e2cb-192">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="2e2cb-193">El valor predeterminado se establece en `text` .</span><span class="sxs-lookup"><span data-stu-id="2e2cb-193">Default is set to `text`.</span></span> | <span data-ttu-id="2e2cb-194">No</span><span class="sxs-lookup"><span data-stu-id="2e2cb-194">No</span></span> | <span data-ttu-id="2e2cb-195">1.4</span><span class="sxs-lookup"><span data-stu-id="2e2cb-195">1.4</span></span> |

#### <a name="example"></a><span data-ttu-id="2e2cb-196">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2e2cb-196">Example</span></span>

<span data-ttu-id="2e2cb-197">En la siguiente sección se muestra un ejemplo del manifiesto de aplicación simple del `composeExtensions` objeto que define un comando de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="2e2cb-197">Following section is an example of the simple app manifest of the `composeExtensions` object defining a search command:</span></span> 

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```
<span data-ttu-id="2e2cb-198">Para ver el manifiesto completo de la aplicación, consulta [Esquema de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2e2cb-198">For the complete app manifest, see [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="2e2cb-199">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="2e2cb-199">Code sample</span></span>

| <span data-ttu-id="2e2cb-200">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2e2cb-200">Sample Name</span></span>           | <span data-ttu-id="2e2cb-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="2e2cb-201">Description</span></span> | <span data-ttu-id="2e2cb-202">.NET</span><span class="sxs-lookup"><span data-stu-id="2e2cb-202">.NET</span></span>    | <span data-ttu-id="2e2cb-203">Node.js</span><span class="sxs-lookup"><span data-stu-id="2e2cb-203">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="2e2cb-204">Teams extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="2e2cb-204">Teams messaging extension action</span></span>| <span data-ttu-id="2e2cb-205">Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-205">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="2e2cb-206">View</span><span class="sxs-lookup"><span data-stu-id="2e2cb-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="2e2cb-207">View</span><span class="sxs-lookup"><span data-stu-id="2e2cb-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="2e2cb-208">Teams de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="2e2cb-208">Teams messaging extension search</span></span>   |  <span data-ttu-id="2e2cb-209">Describe cómo definir comandos de búsqueda y responder a las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="2e2cb-209">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="2e2cb-210">View</span><span class="sxs-lookup"><span data-stu-id="2e2cb-210">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="2e2cb-211">View</span><span class="sxs-lookup"><span data-stu-id="2e2cb-211">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="2e2cb-212">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="2e2cb-212">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="2e2cb-213">[Responder a los comandos de búsqueda](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="2e2cb-213">[Respond to the search commands](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

