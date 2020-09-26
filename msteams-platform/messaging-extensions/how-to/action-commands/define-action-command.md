---
title: Definir comandos de acción de la extensión de mensajería
author: clearab
description: Información general sobre las extensiones de mensajería en la plataforma de Microsoft Teams
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 89cf92260418701ef4809f5a13750b991b9f7acb
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279679"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="45cd1-103">Definir comandos de acción de la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="45cd1-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="45cd1-104">Los comandos de acción permiten presentar a los usuarios un elemento emergente modal (denominado módulo de tareas en Microsoft Teams) para recopilar o Mostrar información, luego procesar su interacción y enviar información de vuelta a teams.</span><span class="sxs-lookup"><span data-stu-id="45cd1-104">Action commands allow you present your users with a modal popup (called a task module in Teams) to collect or display information, then process their interaction and send information back to Teams.</span></span> <span data-ttu-id="45cd1-105">Antes de crear el comando tendrá que decidir:</span><span class="sxs-lookup"><span data-stu-id="45cd1-105">Before creating your command you'll need to decide:</span></span>

1. <span data-ttu-id="45cd1-106">¿Desde dónde se puede activar el comando de acción?</span><span class="sxs-lookup"><span data-stu-id="45cd1-106">Where can the action command be triggered from?</span></span>
1. <span data-ttu-id="45cd1-107">¿Cómo se creará el módulo de tareas?</span><span class="sxs-lookup"><span data-stu-id="45cd1-107">How will the task module be created?</span></span>
1. <span data-ttu-id="45cd1-108">¿Se enviará el mensaje final o la tarjeta al canal desde un bot, o bien se insertará el mensaje o la tarjeta en el área de mensaje de redacción para que el usuario lo envíe?</span><span class="sxs-lookup"><span data-stu-id="45cd1-108">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>

## <a name="choose-action-command-invoke-locations"></a><span data-ttu-id="45cd1-109">Comando elegir acción invocar ubicaciones</span><span class="sxs-lookup"><span data-stu-id="45cd1-109">Choose action command invoke locations</span></span>

<span data-ttu-id="45cd1-110">Lo primero que debe decidir es donde se puede desencadenar el comando de acción (o más concretamente, *invocado*) desde.</span><span class="sxs-lookup"><span data-stu-id="45cd1-110">The first thing you need to decide is where your action command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="45cd1-111">Al especificar el `context` en el manifiesto de la aplicación, se puede invocar al comando desde una o varias de las siguientes ubicaciones:</span><span class="sxs-lookup"><span data-stu-id="45cd1-111">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="45cd1-112">Botones de la parte inferior del área de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="45cd1-112">The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="45cd1-113">@Mentioning la aplicación en el cuadro comando.</span><span class="sxs-lookup"><span data-stu-id="45cd1-113">By @mentioning your app in the command box.</span></span> <span data-ttu-id="45cd1-114">Nota: no puede responder con un mensaje de bot insertado directamente en la conversación si la extensión de mensajería se invoca desde el cuadro de comandos.</span><span class="sxs-lookup"><span data-stu-id="45cd1-114">Note: You cannot respond with a bot message inserted directly into the conversation if your messaging extension is invoked from the command box.</span></span>
* <span data-ttu-id="45cd1-115">Directamente desde un mensaje existente a través del... menú de desbordamiento en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="45cd1-115">Directly from an existing message via the ... overflow menu on a message.</span></span> <span data-ttu-id="45cd1-116">Nota: la invocación inicial a su bot incluirá un objeto JSON que contiene el mensaje desde el que se invocó, que puede procesar antes de presentarlo con un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="45cd1-116">Note: The initial invoke to your bot will include a JSON object containing the message from which it was invoked, which you can process before presenting them with a task module.</span></span>

## <a name="choose-how-to-build-your-task-module"></a><span data-ttu-id="45cd1-117">Elegir cómo crear el módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="45cd1-117">Choose how to build your task module</span></span>

<span data-ttu-id="45cd1-118">Además de elegir desde dónde se puede invocar el comando, también debe elegir cómo rellenar el formulario en el módulo de tareas para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="45cd1-118">In addition to choosing where your command can be invoked from, you must also chose how to populate the form in the task module for your users.</span></span> <span data-ttu-id="45cd1-119">Tiene tres opciones para crear el formulario que se representa en el módulo de tareas:</span><span class="sxs-lookup"><span data-stu-id="45cd1-119">You have three options for creating the form that is rendered inside the task module:</span></span>

* <span data-ttu-id="45cd1-120">**Lista estática de parámetros** : es la opción más sencilla.</span><span class="sxs-lookup"><span data-stu-id="45cd1-120">**Static list of parameters** - This is the simplest option.</span></span> <span data-ttu-id="45cd1-121">Puede definir una lista de parámetros (campos de entrada) en el manifiesto de la aplicación que se representará en el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="45cd1-121">You can define a list of parameters (input fields) in your app manifest the Teams client will render.</span></span> <span data-ttu-id="45cd1-122">No se puede controlar el formato con esta opción.</span><span class="sxs-lookup"><span data-stu-id="45cd1-122">You cannot control the formatting with this option.</span></span>
* <span data-ttu-id="45cd1-123">**Tarjeta adaptable** : puede elegir usar una tarjeta adaptable, que proporciona un mayor control sobre la interfaz de usuario, pero sigue limitando los controles y las opciones de formato disponibles.</span><span class="sxs-lookup"><span data-stu-id="45cd1-123">**Adaptive card** - You can choose to use an adaptive card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="45cd1-124">**Vista Web incrustada** : Si necesita controlar completamente la interfaz de usuario y los controles, puede optar por incrustar una vista web personalizada en el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="45cd1-124">**Embedded web view** - If you need complete control over the UI and controls, you can choose to embed a custom web view in the task module.</span></span>

<span data-ttu-id="45cd1-125">Si elige crear el módulo de tareas con una lista estática de parámetros, la primera llamada a la extensión de mensajería será cuando un usuario envíe el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="45cd1-125">If you choose to create your task module with a static list of parameters, the first call to your messaging extension will be when a user submits the task module.</span></span> <span data-ttu-id="45cd1-126">Cuando se usa una vista Web incrustada o una tarjeta adaptable, la extensión de mensajería debe controlar un evento de invocación inicial del usuario, crear el módulo de tarea y devolverlo al cliente.</span><span class="sxs-lookup"><span data-stu-id="45cd1-126">When using an embedded web view or an adaptive card, your messaging extension will need to handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="choose-how-the-final-message-will-be-sent"></a><span data-ttu-id="45cd1-127">Elegir cómo se enviará el mensaje final</span><span class="sxs-lookup"><span data-stu-id="45cd1-127">Choose how the final message will be sent</span></span>

<span data-ttu-id="45cd1-128">En la mayoría de los casos, el comando de acción dará como resultado una tarjeta insertada en el cuadro de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="45cd1-128">In most cases, your action command will result in a card inserted into the compose message box.</span></span> <span data-ttu-id="45cd1-129">A continuación, el usuario puede decidir enviarlo al canal o al chat.</span><span class="sxs-lookup"><span data-stu-id="45cd1-129">Your user can then decide to send it into the channel or chat.</span></span> <span data-ttu-id="45cd1-130">El mensaje en este caso procede del usuario y el bot no podrá editar ni actualizar la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="45cd1-130">The message in this case comes from the user, and your bot will not be able to edit or update the card further.</span></span>

<span data-ttu-id="45cd1-131">Si la extensión de mensajería se desencadena desde el cuadro de redacción o directamente desde un mensaje, el servicio web puede insertar la respuesta final directamente en el canal o el chat.</span><span class="sxs-lookup"><span data-stu-id="45cd1-131">If your messaging extension is triggered from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="45cd1-132">En este caso, la tarjeta adaptable procede del bot, el bot podrá actualizarlo, y el bot también puede responder al hilo de conversación si es necesario.</span><span class="sxs-lookup"><span data-stu-id="45cd1-132">In this case, the adaptive card comes from the bot, the bot will be able to update it, and the bot can also reply to the conversation thread if needed.</span></span> <span data-ttu-id="45cd1-133">Tendrá que agregar el `bot` objeto al manifiesto de la aplicación con el mismo identificador y definir los ámbitos apropiados.</span><span class="sxs-lookup"><span data-stu-id="45cd1-133">You will need to add the `bot` object to your app manifest using the same Id and defining the appropriate scopes.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="45cd1-134">Agregar el comando al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="45cd1-134">Add the command to your app manifest</span></span>

<span data-ttu-id="45cd1-135">Ahora que ha decidido cómo interactúan los usuarios con el comando de acción, es el momento de agregarlo al manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="45cd1-135">Now that you've decided how users will interact with your action command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="45cd1-136">Para ello, agregará un nuevo `composeExtension` objeto al nivel superior del JSON del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="45cd1-136">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="45cd1-137">Puede hacerlo con la ayuda de App Studio, o bien manualmente.</span><span class="sxs-lookup"><span data-stu-id="45cd1-137">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="45cd1-138">Crear un comando con App Studio</span><span class="sxs-lookup"><span data-stu-id="45cd1-138">Create a command using App Studio</span></span>

<span data-ttu-id="45cd1-139">En los pasos siguientes se da por sentado que ya ha [creado una extensión de mensajería](~/messaging-extensions/how-to/create-messaging-extension.md).</span><span class="sxs-lookup"><span data-stu-id="45cd1-139">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="45cd1-140">En el cliente de Microsoft Teams, Abra **App Studio** y seleccione la pestaña **Editor de manifiestos** .</span><span class="sxs-lookup"><span data-stu-id="45cd1-140">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="45cd1-141">Si ya ha creado el paquete de la aplicación en App Studio, elija en la lista.</span><span class="sxs-lookup"><span data-stu-id="45cd1-141">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="45cd1-142">Si no es así, puedes importar un paquete de aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="45cd1-142">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="45cd1-143">Haga clic en el botón **Agregar** en la sección comando.</span><span class="sxs-lookup"><span data-stu-id="45cd1-143">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="45cd1-144">Elija **permitir que los usuarios desencadenen acciones en servicios externos mientras se encuentra dentro de Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="45cd1-144">Choose **Allow users to trigger actions in external services while inside of Teams**.</span></span>
5. <span data-ttu-id="45cd1-145">Si desea usar un conjunto estático de parámetros para crear el módulo de tareas, seleccione esa opción.</span><span class="sxs-lookup"><span data-stu-id="45cd1-145">If you want to use a static set of parameters to create your task module, select that option.</span></span> <span data-ttu-id="45cd1-146">De lo contrario, elija **recuperar un conjunto dinámico de parámetros de su bot**.</span><span class="sxs-lookup"><span data-stu-id="45cd1-146">Otherwise, choose to **Fetch a dynamic set of parameters from your bot**.</span></span>
6. <span data-ttu-id="45cd1-147">Agregue un **identificador de comando** y un **título**.</span><span class="sxs-lookup"><span data-stu-id="45cd1-147">Add a **Command Id** and a **Title**.</span></span>
7. <span data-ttu-id="45cd1-148">Seleccione el lugar desde el que desea que se desencadene el comando de acción.</span><span class="sxs-lookup"><span data-stu-id="45cd1-148">Select where you want your action command to be triggered from.</span></span>
8. <span data-ttu-id="45cd1-149">Si está usando parámetros para el módulo de tareas, agregue el primero.</span><span class="sxs-lookup"><span data-stu-id="45cd1-149">If you're using parameters for your task module, add the first one.</span></span>
9. <span data-ttu-id="45cd1-150">Click Save</span><span class="sxs-lookup"><span data-stu-id="45cd1-150">Click Save</span></span>
10. <span data-ttu-id="45cd1-151">Si necesita agregar más parámetros, haga clic en el botón **Agregar** de la sección **parámetros** para agregarlos.</span><span class="sxs-lookup"><span data-stu-id="45cd1-151">If you need to add more parameters, click the **Add** button in the **Parameters** section to add them.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="45cd1-152">Crear manualmente un comando</span><span class="sxs-lookup"><span data-stu-id="45cd1-152">Manually create a command</span></span>

<span data-ttu-id="45cd1-153">Para agregar manualmente el comando de extensión de mensajería basada en acciones al manifiesto de la aplicación, deberá agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="45cd1-153">To manually add your action-based messaging extension command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="45cd1-154">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="45cd1-154">Property name</span></span> | <span data-ttu-id="45cd1-155">Finalidad</span><span class="sxs-lookup"><span data-stu-id="45cd1-155">Purpose</span></span> | <span data-ttu-id="45cd1-156">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="45cd1-156">Required?</span></span> | <span data-ttu-id="45cd1-157">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="45cd1-157">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="45cd1-158">IDENTIFICADOR único que asigna a este comando.</span><span class="sxs-lookup"><span data-stu-id="45cd1-158">Unique ID that you assign to this command.</span></span> <span data-ttu-id="45cd1-159">La solicitud del usuario incluirá este identificador.</span><span class="sxs-lookup"><span data-stu-id="45cd1-159">The user request will include this ID.</span></span> | <span data-ttu-id="45cd1-160">Sí</span><span class="sxs-lookup"><span data-stu-id="45cd1-160">Yes</span></span> | <span data-ttu-id="45cd1-161">1.0</span><span class="sxs-lookup"><span data-stu-id="45cd1-161">1.0</span></span> |
| `title` | <span data-ttu-id="45cd1-162">Nombre del comando.</span><span class="sxs-lookup"><span data-stu-id="45cd1-162">Command name.</span></span> <span data-ttu-id="45cd1-163">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="45cd1-163">This value appears in the UI.</span></span> | <span data-ttu-id="45cd1-164">Sí</span><span class="sxs-lookup"><span data-stu-id="45cd1-164">Yes</span></span> | <span data-ttu-id="45cd1-165">1.0</span><span class="sxs-lookup"><span data-stu-id="45cd1-165">1.0</span></span> |
| `type` | <span data-ttu-id="45cd1-166">Debe ser `action`</span><span class="sxs-lookup"><span data-stu-id="45cd1-166">Must be `action`</span></span> | <span data-ttu-id="45cd1-167">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-167">No</span></span> | <span data-ttu-id="45cd1-168">1.4</span><span class="sxs-lookup"><span data-stu-id="45cd1-168">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="45cd1-169">`true` para una tarjeta adaptable o una vista Web incrustada para el módulo de tareas, `false` para una lista estática de parámetros o cuando se carga la vista Web mediante un `taskInfo`</span><span class="sxs-lookup"><span data-stu-id="45cd1-169">`true` for an adaptive card or embedded web view for your task module, `false` for a static list of parameters or when loading the web view by a `taskInfo`</span></span> | <span data-ttu-id="45cd1-170">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-170">No</span></span> | <span data-ttu-id="45cd1-171">1.4</span><span class="sxs-lookup"><span data-stu-id="45cd1-171">1.4</span></span> |
| `context` | <span data-ttu-id="45cd1-172">Matriz opcional de valores que define dónde se puede invocar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="45cd1-172">Optional array of values that defines where the messaging extension can be invoked from.</span></span> <span data-ttu-id="45cd1-173">Los valores posibles son `message` , `compose` o `commandBox` .</span><span class="sxs-lookup"><span data-stu-id="45cd1-173">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="45cd1-174">El valor predeterminado es `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="45cd1-174">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="45cd1-175">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-175">No</span></span> | <span data-ttu-id="45cd1-176">1,5</span><span class="sxs-lookup"><span data-stu-id="45cd1-176">1.5</span></span> |

<span data-ttu-id="45cd1-177">Si usa una lista de parámetros estática, también los agregará.</span><span class="sxs-lookup"><span data-stu-id="45cd1-177">If you are using a static list of parameters, you'll add them as well.</span></span>

| <span data-ttu-id="45cd1-178">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="45cd1-178">Property name</span></span> | <span data-ttu-id="45cd1-179">Finalidad</span><span class="sxs-lookup"><span data-stu-id="45cd1-179">Purpose</span></span> | <span data-ttu-id="45cd1-180">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="45cd1-180">Required?</span></span> | <span data-ttu-id="45cd1-181">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="45cd1-181">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="45cd1-182">Lista estática de parámetros para el comando.</span><span class="sxs-lookup"><span data-stu-id="45cd1-182">Static list of parameters for the command.</span></span> <span data-ttu-id="45cd1-183">Usar solo cuando `fetchTask` es `false`</span><span class="sxs-lookup"><span data-stu-id="45cd1-183">Only use when `fetchTask` is `false`</span></span> | <span data-ttu-id="45cd1-184">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-184">No</span></span> | <span data-ttu-id="45cd1-185">1.0</span><span class="sxs-lookup"><span data-stu-id="45cd1-185">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="45cd1-186">Nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="45cd1-186">The name of the parameter.</span></span> <span data-ttu-id="45cd1-187">Se envía al servicio en la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="45cd1-187">This is sent to your service in the user request.</span></span> | <span data-ttu-id="45cd1-188">Sí</span><span class="sxs-lookup"><span data-stu-id="45cd1-188">Yes</span></span> | <span data-ttu-id="45cd1-189">1.0</span><span class="sxs-lookup"><span data-stu-id="45cd1-189">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="45cd1-190">Describe los propósitos de este parámetro o el ejemplo del valor que se debe proporcionar.</span><span class="sxs-lookup"><span data-stu-id="45cd1-190">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="45cd1-191">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="45cd1-191">This value appears in the UI.</span></span> | <span data-ttu-id="45cd1-192">Sí</span><span class="sxs-lookup"><span data-stu-id="45cd1-192">Yes</span></span> | <span data-ttu-id="45cd1-193">1.0</span><span class="sxs-lookup"><span data-stu-id="45cd1-193">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="45cd1-194">Nombre corto o etiqueta del parámetro sencillo para el usuario.</span><span class="sxs-lookup"><span data-stu-id="45cd1-194">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="45cd1-195">Sí</span><span class="sxs-lookup"><span data-stu-id="45cd1-195">Yes</span></span> | <span data-ttu-id="45cd1-196">1.0</span><span class="sxs-lookup"><span data-stu-id="45cd1-196">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="45cd1-197">Se establece en el tipo de entrada requerido.</span><span class="sxs-lookup"><span data-stu-id="45cd1-197">Set to the type of input required.</span></span> <span data-ttu-id="45cd1-198">Los valores posibles son `text` : `textarea` , `number` , `date` , `time` , `toggle` .</span><span class="sxs-lookup"><span data-stu-id="45cd1-198">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="45cd1-199">El valor predeterminado está establecido en `text`</span><span class="sxs-lookup"><span data-stu-id="45cd1-199">Default is set to `text`</span></span> | <span data-ttu-id="45cd1-200">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-200">No</span></span> | <span data-ttu-id="45cd1-201">1.4</span><span class="sxs-lookup"><span data-stu-id="45cd1-201">1.4</span></span> |

<span data-ttu-id="45cd1-202">Si usa una vista Web incrustada, puede agregar opcionalmente el `taskInfo` objeto para recuperar la vista Web sin llamar a su bot directamente.</span><span class="sxs-lookup"><span data-stu-id="45cd1-202">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="45cd1-203">Si decide usar esta opción, el comportamiento es similar al uso de una lista estática de parámetros en que la primera interacción con el bot [responderá a la acción de envío del módulo de tarea](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span><span class="sxs-lookup"><span data-stu-id="45cd1-203">If you choose to use this option, the behavior is similar to using a static list of parameters in that the first interaction with your bot will be [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="45cd1-204">Si usa un `taskInfo` objeto, asegúrese de establecer también el `fetchTask` parámetro en `false` .</span><span class="sxs-lookup"><span data-stu-id="45cd1-204">If you are using a `taskInfo` object, be sure to also set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="45cd1-205">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="45cd1-205">Property name</span></span> | <span data-ttu-id="45cd1-206">Finalidad</span><span class="sxs-lookup"><span data-stu-id="45cd1-206">Purpose</span></span> | <span data-ttu-id="45cd1-207">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="45cd1-207">Required?</span></span> | <span data-ttu-id="45cd1-208">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="45cd1-208">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="45cd1-209">Especificar el módulo de tarea para cargar previamente cuando se usa un comando de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="45cd1-209">Specify the task module to preload when using a messaging extension command</span></span>| <span data-ttu-id="45cd1-210">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-210">No</span></span> | <span data-ttu-id="45cd1-211">1.4</span><span class="sxs-lookup"><span data-stu-id="45cd1-211">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="45cd1-212">Título del módulo de tarea inicial</span><span class="sxs-lookup"><span data-stu-id="45cd1-212">Initial task module title</span></span>|<span data-ttu-id="45cd1-213">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-213">No</span></span> | <span data-ttu-id="45cd1-214">1.4</span><span class="sxs-lookup"><span data-stu-id="45cd1-214">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="45cd1-215">Ancho del módulo de tareas, ya sea un número en píxeles o un diseño predeterminado, como "Large", "Medium" o "Small"</span><span class="sxs-lookup"><span data-stu-id="45cd1-215">Task module width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="45cd1-216">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-216">No</span></span> | <span data-ttu-id="45cd1-217">1.4</span><span class="sxs-lookup"><span data-stu-id="45cd1-217">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="45cd1-218">Alto del módulo de tareas: número en píxeles o diseño predeterminado, como "Large", "Medium" o "Small"</span><span class="sxs-lookup"><span data-stu-id="45cd1-218">Task module height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="45cd1-219">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-219">No</span></span> | <span data-ttu-id="45cd1-220">1.4</span><span class="sxs-lookup"><span data-stu-id="45cd1-220">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="45cd1-221">Dirección URL de vista Web inicial</span><span class="sxs-lookup"><span data-stu-id="45cd1-221">Initial web view URL</span></span>|<span data-ttu-id="45cd1-222">No</span><span class="sxs-lookup"><span data-stu-id="45cd1-222">No</span></span> | <span data-ttu-id="45cd1-223">1.4</span><span class="sxs-lookup"><span data-stu-id="45cd1-223">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="45cd1-224">Ejemplo de manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="45cd1-224">App manifest example</span></span>

<span data-ttu-id="45cd1-225">A continuación, se muestra un ejemplo de un `composeExtensions` objeto que define dos comandos de acción.</span><span class="sxs-lookup"><span data-stu-id="45cd1-225">The below is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="45cd1-226">No es un ejemplo del manifiesto completo, para el esquema completo del manifiesto de la aplicación, vea: [esquema del manifiesto](~/resources/schema/manifest-schema.md)de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="45cd1-226">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": false,
        "parameters": [
          {
            "name": "Name",
            "description": "To Do Title",
            "title": "Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "description": "Description of the task",
            "title": "Description",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "description": "Due date for the task",
            "title": "Date",
            "inputType": "date"
          }
        ]
      },
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Reassign a todo item",
        "type": "action",
        "fetchTask": true,
      }
    ]
  }
]
...
```

## <a name="next-steps"></a><span data-ttu-id="45cd1-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45cd1-227">Next steps</span></span>

<span data-ttu-id="45cd1-228">Si usa una tarjeta adaptable o una vista Web incrustada sin un `taskInfo` objeto, querrá:</span><span class="sxs-lookup"><span data-stu-id="45cd1-228">If you are using either an adaptive card or an embedded web view without a `taskInfo` object, you'll want to:</span></span>

* [<span data-ttu-id="45cd1-229">Crear y responder con un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="45cd1-229">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="45cd1-230">Si usa parámetros o una vista Web incrustada con un `taskInfo` objeto, el siguiente paso es:</span><span class="sxs-lookup"><span data-stu-id="45cd1-230">If you are using parameters or an embedded web view with a `taskInfo` object, the next step for you is to:</span></span>

* [<span data-ttu-id="45cd1-231">Responder al envío del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="45cd1-231">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
