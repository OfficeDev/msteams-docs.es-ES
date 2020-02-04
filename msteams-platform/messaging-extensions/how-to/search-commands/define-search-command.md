---
title: Definir comandos de búsqueda de extensiones de mensajería
author: clearab
description: Definir comandos de búsqueda de extensiones de mensajería para las aplicaciones de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676020"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="296d6-103">Definir comandos de búsqueda de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="296d6-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="296d6-104">Los comandos de búsqueda de extensiones de mensajería permiten a los usuarios buscar en sistemas externos e insertar los resultados de la búsqueda en un mensaje en forma de una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="296d6-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="296d6-105">Elegir ubicaciones de invocación de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="296d6-105">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="296d6-106">Lo primero que debe decidir es donde se puede desencadenar el comando de búsqueda (o más concretamente, *invocado*) desde.</span><span class="sxs-lookup"><span data-stu-id="296d6-106">The first thing you need to decide is where your search command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="296d6-107">Se puede invocar el comando de búsqueda desde una o ambas de las siguientes ubicaciones:</span><span class="sxs-lookup"><span data-stu-id="296d6-107">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="296d6-108">Botones en la parte inferior del área de mensaje de redacción</span><span class="sxs-lookup"><span data-stu-id="296d6-108">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="296d6-109">Por @mentioning en el cuadro comando</span><span class="sxs-lookup"><span data-stu-id="296d6-109">By @mentioning in the command box</span></span>

<span data-ttu-id="296d6-110">Cuando se invoca desde el área de mensaje de redacción, el usuario tiene la opción de enviar los resultados a la conversación.</span><span class="sxs-lookup"><span data-stu-id="296d6-110">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="296d6-111">Cuando se invoca desde el cuadro comando, el usuario puede interactuar con la tarjeta resultante o copiarla para usarla en otro lugar.</span><span class="sxs-lookup"><span data-stu-id="296d6-111">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="296d6-112">Agregar el comando al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="296d6-112">Add the command to your app manifest</span></span>

<span data-ttu-id="296d6-113">Ahora que ha decidido cómo interactúan los usuarios con el comando de búsqueda, es el momento de agregarlo al manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="296d6-113">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="296d6-114">Para ello, agregará un nuevo `composeExtension` objeto al nivel superior del JSON del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="296d6-114">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="296d6-115">Puede hacerlo con la ayuda de App Studio, o bien manualmente.</span><span class="sxs-lookup"><span data-stu-id="296d6-115">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="296d6-116">Crear un comando con App Studio</span><span class="sxs-lookup"><span data-stu-id="296d6-116">Create a command using App Studio</span></span>

<span data-ttu-id="296d6-117">En los pasos siguientes se da por sentado que ya ha [creado una extensión de mensajería](~/messaging-extensions/how-to/create-messaging-extension.md).</span><span class="sxs-lookup"><span data-stu-id="296d6-117">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="296d6-118">En el cliente de Microsoft Teams, Abra **App Studio** y seleccione la pestaña **Editor de manifiestos** .</span><span class="sxs-lookup"><span data-stu-id="296d6-118">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="296d6-119">Si ya ha creado el paquete de la aplicación en App Studio, elija en la lista.</span><span class="sxs-lookup"><span data-stu-id="296d6-119">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="296d6-120">Si no es así, puedes importar un paquete de aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="296d6-120">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="296d6-121">Haga clic en el botón **Agregar** en la sección comando.</span><span class="sxs-lookup"><span data-stu-id="296d6-121">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="296d6-122">Elija **permitir que los usuarios consulten la información del servicio e insértela en un mensaje**.</span><span class="sxs-lookup"><span data-stu-id="296d6-122">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
5. <span data-ttu-id="296d6-123">Agregue un **identificador de comando** y un **título**.</span><span class="sxs-lookup"><span data-stu-id="296d6-123">Add a **Command Id** and a **Title**.</span></span>
6. <span data-ttu-id="296d6-124">Seleccione el lugar desde el que desea que se desencadene el comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="296d6-124">Select where you want your search command to be triggered from.</span></span> <span data-ttu-id="296d6-125">La selección de un **mensaje** no altera actualmente el comportamiento del comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="296d6-125">Selecting **message** does not currently alter the behavior of your search command.</span></span>
7. <span data-ttu-id="296d6-126">Agregue el parámetro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="296d6-126">Add your search parameter.</span></span>
8. <span data-ttu-id="296d6-127">Haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="296d6-127">Click Save.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="296d6-128">Crear manualmente un comando</span><span class="sxs-lookup"><span data-stu-id="296d6-128">Manually create a command</span></span>

<span data-ttu-id="296d6-129">Para agregar manualmente el comando de búsqueda de extensiones de mensajería al manifiesto de la aplicación, deberá agregar los siguientes parámetros a `composeExtension.commands` la matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="296d6-129">To manually add your messaging extension search command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="296d6-130">Nombre de la propiedad</span><span class="sxs-lookup"><span data-stu-id="296d6-130">Property name</span></span> | <span data-ttu-id="296d6-131">Objetivo</span><span class="sxs-lookup"><span data-stu-id="296d6-131">Purpose</span></span> | <span data-ttu-id="296d6-132">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="296d6-132">Required?</span></span> | <span data-ttu-id="296d6-133">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="296d6-133">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="296d6-134">IDENTIFICADOR único que asigna a este comando.</span><span class="sxs-lookup"><span data-stu-id="296d6-134">Unique ID that you assign to this command.</span></span> <span data-ttu-id="296d6-135">La solicitud del usuario incluirá este identificador.</span><span class="sxs-lookup"><span data-stu-id="296d6-135">The user request will include this ID.</span></span> | <span data-ttu-id="296d6-136">Sí</span><span class="sxs-lookup"><span data-stu-id="296d6-136">Yes</span></span> | <span data-ttu-id="296d6-137">1.0</span><span class="sxs-lookup"><span data-stu-id="296d6-137">1.0</span></span> |
| `title` | <span data-ttu-id="296d6-138">Nombre del comando.</span><span class="sxs-lookup"><span data-stu-id="296d6-138">Command name.</span></span> <span data-ttu-id="296d6-139">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="296d6-139">This value appears in the UI.</span></span> | <span data-ttu-id="296d6-140">Sí</span><span class="sxs-lookup"><span data-stu-id="296d6-140">Yes</span></span> | <span data-ttu-id="296d6-141">1.0</span><span class="sxs-lookup"><span data-stu-id="296d6-141">1.0</span></span> |
| `description` | <span data-ttu-id="296d6-142">Texto de ayuda que indica lo que hace este comando.</span><span class="sxs-lookup"><span data-stu-id="296d6-142">Help text indicating what this command does.</span></span> <span data-ttu-id="296d6-143">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="296d6-143">This value appears in the UI.</span></span> | <span data-ttu-id="296d6-144">Sí</span><span class="sxs-lookup"><span data-stu-id="296d6-144">Yes</span></span> | <span data-ttu-id="296d6-145">1.0</span><span class="sxs-lookup"><span data-stu-id="296d6-145">1.0</span></span> |
| `type` | <span data-ttu-id="296d6-146">Debe ser`query`</span><span class="sxs-lookup"><span data-stu-id="296d6-146">Must be `query`</span></span> | <span data-ttu-id="296d6-147">No</span><span class="sxs-lookup"><span data-stu-id="296d6-147">No</span></span> | <span data-ttu-id="296d6-148">1.4</span><span class="sxs-lookup"><span data-stu-id="296d6-148">1.4</span></span> |
|`initialRun` | <span data-ttu-id="296d6-149">Si se establece en **true**, indica que este comando debe ejecutarse en cuanto el usuario seleccione este comando en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="296d6-149">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="296d6-150">No</span><span class="sxs-lookup"><span data-stu-id="296d6-150">No</span></span> | <span data-ttu-id="296d6-151">1.0</span><span class="sxs-lookup"><span data-stu-id="296d6-151">1.0</span></span> |
| `context` | <span data-ttu-id="296d6-152">Matriz opcional de valores que define el contexto en el que está disponible la acción de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="296d6-152">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="296d6-153">Los valores posibles `message`son `compose`, o `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="296d6-153">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="296d6-154">El valor predeterminado es `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="296d6-154">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="296d6-155">No</span><span class="sxs-lookup"><span data-stu-id="296d6-155">No</span></span> | <span data-ttu-id="296d6-156">1,5</span><span class="sxs-lookup"><span data-stu-id="296d6-156">1.5</span></span> |

<span data-ttu-id="296d6-157">También necesitará agregar los detalles del parámetro de búsqueda, que definirán el texto visible para el usuario en el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="296d6-157">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="296d6-158">Nombre de la propiedad</span><span class="sxs-lookup"><span data-stu-id="296d6-158">Property name</span></span> | <span data-ttu-id="296d6-159">Objetivo</span><span class="sxs-lookup"><span data-stu-id="296d6-159">Purpose</span></span> | <span data-ttu-id="296d6-160">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="296d6-160">Required?</span></span> | <span data-ttu-id="296d6-161">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="296d6-161">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="296d6-162">Lista estática de parámetros para el comando.</span><span class="sxs-lookup"><span data-stu-id="296d6-162">Static list of parameters for the command.</span></span> | <span data-ttu-id="296d6-163">No</span><span class="sxs-lookup"><span data-stu-id="296d6-163">No</span></span> | <span data-ttu-id="296d6-164">1.0</span><span class="sxs-lookup"><span data-stu-id="296d6-164">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="296d6-165">Nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="296d6-165">The name of the parameter.</span></span> <span data-ttu-id="296d6-166">Se envía al servicio en la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="296d6-166">This is sent to your service in the user request.</span></span> | <span data-ttu-id="296d6-167">Sí</span><span class="sxs-lookup"><span data-stu-id="296d6-167">Yes</span></span> | <span data-ttu-id="296d6-168">1.0</span><span class="sxs-lookup"><span data-stu-id="296d6-168">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="296d6-169">Describe los propósitos de este parámetro o el ejemplo del valor que se debe proporcionar.</span><span class="sxs-lookup"><span data-stu-id="296d6-169">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="296d6-170">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="296d6-170">This value appears in the UI.</span></span> | <span data-ttu-id="296d6-171">Sí</span><span class="sxs-lookup"><span data-stu-id="296d6-171">Yes</span></span> | <span data-ttu-id="296d6-172">1.0</span><span class="sxs-lookup"><span data-stu-id="296d6-172">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="296d6-173">Nombre corto o etiqueta del parámetro sencillo para el usuario.</span><span class="sxs-lookup"><span data-stu-id="296d6-173">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="296d6-174">Sí</span><span class="sxs-lookup"><span data-stu-id="296d6-174">Yes</span></span> | <span data-ttu-id="296d6-175">1.0</span><span class="sxs-lookup"><span data-stu-id="296d6-175">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="296d6-176">Se establece en el tipo de entrada requerido.</span><span class="sxs-lookup"><span data-stu-id="296d6-176">Set to the type of input required.</span></span> <span data-ttu-id="296d6-177">Los valores posibles `text`son `textarea`: `number`, `date`, `time`, `toggle`,.</span><span class="sxs-lookup"><span data-stu-id="296d6-177">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="296d6-178">El valor predeterminado está establecido en`text`</span><span class="sxs-lookup"><span data-stu-id="296d6-178">Default is set to `text`</span></span> | <span data-ttu-id="296d6-179">No</span><span class="sxs-lookup"><span data-stu-id="296d6-179">No</span></span> | <span data-ttu-id="296d6-180">1.4</span><span class="sxs-lookup"><span data-stu-id="296d6-180">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="296d6-181">Ejemplo de manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="296d6-181">App manifest example</span></span>

<span data-ttu-id="296d6-182">A continuación, se muestra un ejemplo `composeExtensions` de un objeto que define un comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="296d6-182">The below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="296d6-183">No es un ejemplo del manifiesto completo, para el esquema completo del manifiesto de la aplicación, vea: [esquema del manifiesto](~/resources/schema/manifest-schema.md)de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="296d6-183">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="296d6-184">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="296d6-184">Next steps</span></span>

<span data-ttu-id="296d6-185">Ahora que ha agregado el comando de búsqueda, deberá [controlar la solicitud de búsqueda](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="296d6-185">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]