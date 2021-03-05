---
title: Definir comandos de búsqueda de extensión de mensajería
author: clearab
description: Definir comandos de búsqueda de extensión de mensajería para aplicaciones de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449272"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="8c968-103">Definir comandos de búsqueda de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="8c968-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="8c968-104">Los comandos de búsqueda de extensión de mensajería permiten a los usuarios buscar en sistemas externos e insertar los resultados de esa búsqueda en un mensaje en forma de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="8c968-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

> [!NOTE]
> <span data-ttu-id="8c968-105">El límite de tamaño de la tarjeta de resultados es de 28 KB.</span><span class="sxs-lookup"><span data-stu-id="8c968-105">The result card size limit is 28 KB.</span></span> <span data-ttu-id="8c968-106">La tarjeta no se envía si su tamaño supera los 28 KB.</span><span class="sxs-lookup"><span data-stu-id="8c968-106">The card is not sent if its size exceeds 28 KB.</span></span> 

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="8c968-107">Elegir ubicaciones de invocación de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="8c968-107">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="8c968-108">Lo primero que debe decidir es desde dónde se puede desencadenar el comando de búsqueda (o, específicamente, *invocarlo).*</span><span class="sxs-lookup"><span data-stu-id="8c968-108">The first thing you need to decide is where your search command can be triggered (or specifically, *invoked*) from.</span></span> <span data-ttu-id="8c968-109">El comando de búsqueda se puede invocar desde una o ambas de las siguientes ubicaciones:</span><span class="sxs-lookup"><span data-stu-id="8c968-109">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="8c968-110">Los botones de la parte inferior del área del mensaje de redacción</span><span class="sxs-lookup"><span data-stu-id="8c968-110">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="8c968-111">Por @mentioning en el cuadro de comandos</span><span class="sxs-lookup"><span data-stu-id="8c968-111">By @mentioning in the command box</span></span>

<span data-ttu-id="8c968-112">Cuando se invoca desde el área del mensaje de redacción, el usuario tendrá la opción de enviar los resultados a la conversación.</span><span class="sxs-lookup"><span data-stu-id="8c968-112">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="8c968-113">Cuando se invoca desde el cuadro de comandos, el usuario puede interactuar con la tarjeta resultante o copiarla para usarla en otro lugar.</span><span class="sxs-lookup"><span data-stu-id="8c968-113">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="8c968-114">Agregar el comando al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8c968-114">Add the command to your app manifest</span></span>

<span data-ttu-id="8c968-115">Ahora que has decidido cómo interactuarán los usuarios con el comando de búsqueda, es el momento de agregarlo al manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c968-115">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="8c968-116">Para ello, agregarás un nuevo objeto al nivel superior del JSON del `composeExtension` manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c968-116">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="8c968-117">Puedes hacerlo con la ayuda de App Studio o manualmente.</span><span class="sxs-lookup"><span data-stu-id="8c968-117">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="8c968-118">Crear un comando con App Studio</span><span class="sxs-lookup"><span data-stu-id="8c968-118">Create a command using App Studio</span></span>

<span data-ttu-id="8c968-119">El requisito previo para crear un comando de búsqueda es que ya debe crear una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c968-119">The prerequisite to create a search command is that you must already create a messaging extension.</span></span> <span data-ttu-id="8c968-120">Para obtener información sobre cómo crear una extensión de mensajería, vea [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8c968-120">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="8c968-121">**Para crear un comando de búsqueda**</span><span class="sxs-lookup"><span data-stu-id="8c968-121">**To create a search command**</span></span>

1. <span data-ttu-id="8c968-122">En el cliente de Microsoft Teams, abra **App Studio** y seleccione la pestaña Editor **de manifiestos.**</span><span class="sxs-lookup"><span data-stu-id="8c968-122">From the Microsoft Teams client, open **App Studio**, and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="8c968-123">Si ya creaste un paquete de aplicación en **App Studio,** eligelo en la lista.</span><span class="sxs-lookup"><span data-stu-id="8c968-123">If you already created an app package in the **App Studio**, choose it from the list.</span></span> <span data-ttu-id="8c968-124">Si no has creado un paquete de aplicación, importa uno existente.</span><span class="sxs-lookup"><span data-stu-id="8c968-124">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="8c968-125">Después de importar un paquete de aplicación, selecciona **Extensiones de mensajería en** **Funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="8c968-125">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span>
1. <span data-ttu-id="8c968-126">Seleccione **Agregar** en la **sección Comando** de la página extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c968-126">Select **Add** in the **Command** section in the messaging extensions page.</span></span>
1. <span data-ttu-id="8c968-127">Elija **Permitir que los usuarios consulten su servicio para** obtener información e insertarla en un mensaje .</span><span class="sxs-lookup"><span data-stu-id="8c968-127">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
1. <span data-ttu-id="8c968-128">Agregue un **identificador de comando** y un **título**.</span><span class="sxs-lookup"><span data-stu-id="8c968-128">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="8c968-129">Seleccione la ubicación desde la que se debe desencadenar el comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="8c968-129">Select the location from where your search command must be triggered.</span></span> <span data-ttu-id="8c968-130">Seleccionar mensaje **no** modifica actualmente el comportamiento del comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="8c968-130">Selecting **message** does not currently alter the behavior of your search command.</span></span>
1. <span data-ttu-id="8c968-131">Agregue el parámetro de búsqueda y **seleccione Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8c968-131">Add your search parameter and select **Save**.</span></span>
 
### <a name="manually-create-a-command"></a><span data-ttu-id="8c968-132">Crear manualmente un comando</span><span class="sxs-lookup"><span data-stu-id="8c968-132">Manually create a command</span></span>

<span data-ttu-id="8c968-133">Para agregar manualmente el comando de búsqueda de extensión de mensajería al manifiesto de la aplicación, tendrás que agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="8c968-133">To manually add your messaging extension search command to your app manifest, you'll need to add the following parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="8c968-134">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="8c968-134">Property name</span></span> | <span data-ttu-id="8c968-135">Finalidad</span><span class="sxs-lookup"><span data-stu-id="8c968-135">Purpose</span></span> | <span data-ttu-id="8c968-136">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="8c968-136">Required?</span></span> | <span data-ttu-id="8c968-137">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="8c968-137">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="8c968-138">Identificador único que se asigna a este comando.</span><span class="sxs-lookup"><span data-stu-id="8c968-138">Unique ID that you assign to this command.</span></span> <span data-ttu-id="8c968-139">La solicitud de usuario incluirá este identificador.</span><span class="sxs-lookup"><span data-stu-id="8c968-139">The user request will include this ID.</span></span> | <span data-ttu-id="8c968-140">Sí</span><span class="sxs-lookup"><span data-stu-id="8c968-140">Yes</span></span> | <span data-ttu-id="8c968-141">1.0</span><span class="sxs-lookup"><span data-stu-id="8c968-141">1.0</span></span> |
| `title` | <span data-ttu-id="8c968-142">Nombre del comando.</span><span class="sxs-lookup"><span data-stu-id="8c968-142">Command name.</span></span> <span data-ttu-id="8c968-143">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="8c968-143">This value appears in the UI.</span></span> | <span data-ttu-id="8c968-144">Sí</span><span class="sxs-lookup"><span data-stu-id="8c968-144">Yes</span></span> | <span data-ttu-id="8c968-145">1.0</span><span class="sxs-lookup"><span data-stu-id="8c968-145">1.0</span></span> |
| `description` | <span data-ttu-id="8c968-146">Texto de ayuda que indica lo que hace este comando.</span><span class="sxs-lookup"><span data-stu-id="8c968-146">Help text indicating what this command does.</span></span> <span data-ttu-id="8c968-147">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="8c968-147">This value appears in the UI.</span></span> | <span data-ttu-id="8c968-148">Sí</span><span class="sxs-lookup"><span data-stu-id="8c968-148">Yes</span></span> | <span data-ttu-id="8c968-149">1.0</span><span class="sxs-lookup"><span data-stu-id="8c968-149">1.0</span></span> |
| `type` | <span data-ttu-id="8c968-150">Debe ser `query`</span><span class="sxs-lookup"><span data-stu-id="8c968-150">Must be `query`</span></span> | <span data-ttu-id="8c968-151">No</span><span class="sxs-lookup"><span data-stu-id="8c968-151">No</span></span> | <span data-ttu-id="8c968-152">1.4</span><span class="sxs-lookup"><span data-stu-id="8c968-152">1.4</span></span> |
|`initialRun` | <span data-ttu-id="8c968-153">Si se establece en **true,** indica que este comando debe ejecutarse tan pronto como el usuario elija este comando en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="8c968-153">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="8c968-154">No</span><span class="sxs-lookup"><span data-stu-id="8c968-154">No</span></span> | <span data-ttu-id="8c968-155">1.0</span><span class="sxs-lookup"><span data-stu-id="8c968-155">1.0</span></span> |
| `context` | <span data-ttu-id="8c968-156">Matriz opcional de valores que define el contexto en el que está disponible la acción de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="8c968-156">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="8c968-157">Los valores posibles `message` `compose` son , o `commandBox` .</span><span class="sxs-lookup"><span data-stu-id="8c968-157">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="8c968-158">El valor predeterminado es `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="8c968-158">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="8c968-159">No</span><span class="sxs-lookup"><span data-stu-id="8c968-159">No</span></span> | <span data-ttu-id="8c968-160">1,5</span><span class="sxs-lookup"><span data-stu-id="8c968-160">1.5</span></span> |

<span data-ttu-id="8c968-161">También tendrás que agregar los detalles del parámetro de búsqueda, que definirá el texto visible para el usuario en el cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="8c968-161">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="8c968-162">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="8c968-162">Property name</span></span> | <span data-ttu-id="8c968-163">Finalidad</span><span class="sxs-lookup"><span data-stu-id="8c968-163">Purpose</span></span> | <span data-ttu-id="8c968-164">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="8c968-164">Required?</span></span> | <span data-ttu-id="8c968-165">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="8c968-165">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="8c968-166">Lista estática de parámetros para el comando.</span><span class="sxs-lookup"><span data-stu-id="8c968-166">Static list of parameters for the command.</span></span> | <span data-ttu-id="8c968-167">No</span><span class="sxs-lookup"><span data-stu-id="8c968-167">No</span></span> | <span data-ttu-id="8c968-168">1.0</span><span class="sxs-lookup"><span data-stu-id="8c968-168">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="8c968-169">Nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="8c968-169">The name of the parameter.</span></span> <span data-ttu-id="8c968-170">Esto se envía al servicio en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="8c968-170">This is sent to your service in the user request.</span></span> | <span data-ttu-id="8c968-171">Sí</span><span class="sxs-lookup"><span data-stu-id="8c968-171">Yes</span></span> | <span data-ttu-id="8c968-172">1.0</span><span class="sxs-lookup"><span data-stu-id="8c968-172">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="8c968-173">Describe los propósitos de este parámetro o un ejemplo del valor que se debe proporcionar.</span><span class="sxs-lookup"><span data-stu-id="8c968-173">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="8c968-174">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="8c968-174">This value appears in the UI.</span></span> | <span data-ttu-id="8c968-175">Sí</span><span class="sxs-lookup"><span data-stu-id="8c968-175">Yes</span></span> | <span data-ttu-id="8c968-176">1.0</span><span class="sxs-lookup"><span data-stu-id="8c968-176">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="8c968-177">Título o etiqueta de parámetros fáciles de usar cortos.</span><span class="sxs-lookup"><span data-stu-id="8c968-177">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="8c968-178">Sí</span><span class="sxs-lookup"><span data-stu-id="8c968-178">Yes</span></span> | <span data-ttu-id="8c968-179">1.0</span><span class="sxs-lookup"><span data-stu-id="8c968-179">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="8c968-180">Se establece en el tipo de entrada necesario.</span><span class="sxs-lookup"><span data-stu-id="8c968-180">Set to the type of input required.</span></span> <span data-ttu-id="8c968-181">Los valores posibles `text` incluyen , , , , , `textarea` `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="8c968-181">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="8c968-182">El valor predeterminado está establecido en `text`</span><span class="sxs-lookup"><span data-stu-id="8c968-182">Default is set to `text`</span></span> | <span data-ttu-id="8c968-183">No</span><span class="sxs-lookup"><span data-stu-id="8c968-183">No</span></span> | <span data-ttu-id="8c968-184">1.4</span><span class="sxs-lookup"><span data-stu-id="8c968-184">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="8c968-185">Ejemplo de manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8c968-185">App manifest example</span></span>

<span data-ttu-id="8c968-186">A continuación se muestra un ejemplo `composeExtensions` de un objeto que define un comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="8c968-186">Below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="8c968-187">No es un ejemplo del manifiesto completo, para el esquema de manifiesto de aplicación completo vea: [Esquema de manifiesto de aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="8c968-187">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8c968-188">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="8c968-188">Next steps</span></span>

<span data-ttu-id="8c968-189">Ahora que ha agregado el comando de búsqueda, tendrá que controlar [la solicitud de búsqueda](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="8c968-189">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
