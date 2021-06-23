---
title: Definir comandos de acción de extensión de mensajería
author: surbhigupta
description: Información general sobre los comandos de acción de extensión de mensajería
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b4420247d3a0c1116bd1aed09fa2edccf18ae902
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068927"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="1ae79-103">Definir comandos de acción de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="1ae79-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="1ae79-104">Los comandos de acción permiten presentar a los usuarios un elemento emergente modal denominado módulo de tareas en Teams.</span><span class="sxs-lookup"><span data-stu-id="1ae79-104">Action commands allow you to present your users with a modal popup called a task module in Teams.</span></span> <span data-ttu-id="1ae79-105">El módulo de tareas recopila o muestra información, procesa la interacción y envía la información de vuelta a Teams.</span><span class="sxs-lookup"><span data-stu-id="1ae79-105">The task module collects or displays information, processes the interaction and sends the information back to Teams.</span></span> <span data-ttu-id="1ae79-106">Este documento le guía sobre cómo seleccionar ubicaciones de invocación de comandos de acción, crear el módulo de tareas, enviar el mensaje final o la tarjeta, crear un comando de acción con app studio o crearlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="1ae79-106">This document guides you on how to select action command invoke locations, create your task module, send final message, or card, create action command using app studio, or create it manually.</span></span> 

<span data-ttu-id="1ae79-107">Antes de crear el comando de acción, debe decidir los siguientes factores:</span><span class="sxs-lookup"><span data-stu-id="1ae79-107">Before creating the action command you must decide the following factors:</span></span>

1. [<span data-ttu-id="1ae79-108">¿Desde dónde se puede desencadenar el comando de acción?</span><span class="sxs-lookup"><span data-stu-id="1ae79-108">Where can the action command be triggered from?</span></span>](#select-action-command-invoke-locations)
1. [<span data-ttu-id="1ae79-109">¿Cómo se creará el módulo de tareas?</span><span class="sxs-lookup"><span data-stu-id="1ae79-109">How will the task module be created?</span></span>](#select-how-to-create-your-task-module)
1. [<span data-ttu-id="1ae79-110">¿Se enviará el mensaje final o la tarjeta al canal desde un bot o se insertará el mensaje o la tarjeta en el área del mensaje de redacción para que el usuario envíe?</span><span class="sxs-lookup"><span data-stu-id="1ae79-110">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a><span data-ttu-id="1ae79-111">Seleccionar ubicaciones de invocación de comandos de acción</span><span class="sxs-lookup"><span data-stu-id="1ae79-111">Select action command invoke locations</span></span>

<span data-ttu-id="1ae79-112">En primer lugar, debe decidir la ubicación desde la que se debe invocar el comando de acción.</span><span class="sxs-lookup"><span data-stu-id="1ae79-112">First, you must decide the location from where your action command must be invoked.</span></span> <span data-ttu-id="1ae79-113">Al especificar el manifiesto de la aplicación, se puede invocar el comando `context` desde una o varias de las siguientes ubicaciones:</span><span class="sxs-lookup"><span data-stu-id="1ae79-113">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="1ae79-114">Área de redacción de mensajes: los botones situados en la parte inferior del área del mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="1ae79-114">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="1ae79-115">Cuadro de comando: @mentioning la aplicación en el cuadro de comandos.</span><span class="sxs-lookup"><span data-stu-id="1ae79-115">Command box: By @mentioning your app in the command box.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="1ae79-116">Si se invoca la extensión de mensajería desde el cuadro de comandos, no puede responder con un mensaje de bot insertado directamente en la conversación.</span><span class="sxs-lookup"><span data-stu-id="1ae79-116">If messaging extension is invoked from the command box, you cannot respond with a bot message inserted directly into the conversation.</span></span>

* <span data-ttu-id="1ae79-117">Mensaje: directamente desde un mensaje existente a través del `...` menú de desbordamiento de un mensaje.</span><span class="sxs-lookup"><span data-stu-id="1ae79-117">Message: Directly from an existing message through the `...` overflow menu on a message.</span></span> 
    > [!NOTE] 
    > <span data-ttu-id="1ae79-118">La invocación inicial al bot incluye un objeto JSON que contiene el mensaje desde el que se invocó.</span><span class="sxs-lookup"><span data-stu-id="1ae79-118">The initial invoke to your bot includes a JSON object containing the message from which it was invoked.</span></span> <span data-ttu-id="1ae79-119">Puede procesar el mensaje antes de presentarlo con un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="1ae79-119">You can process the message before presenting them with a task module.</span></span>

<span data-ttu-id="1ae79-120">La siguiente imagen muestra las ubicaciones desde las que se invoca el comando action:</span><span class="sxs-lookup"><span data-stu-id="1ae79-120">The following image displays the locations from where action command is invoked:</span></span>

![ubicaciones de invocación de comandos de acción](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a><span data-ttu-id="1ae79-122">Seleccionar cómo crear el módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="1ae79-122">Select how to create your task module</span></span>

<span data-ttu-id="1ae79-123">Además de seleccionar desde dónde se puede invocar el comando, también debe seleccionar cómo rellenar el formulario en el módulo de tareas para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1ae79-123">In addition to selecting where your command can be invoked from, you must also select how to populate the form in the task module for your users.</span></span> <span data-ttu-id="1ae79-124">Tiene las tres opciones siguientes para crear el formulario que se representa dentro del módulo de tareas:</span><span class="sxs-lookup"><span data-stu-id="1ae79-124">You have the following three options for creating the form that is rendered inside the task module:</span></span>   

* <span data-ttu-id="1ae79-125">**Lista estática de parámetros:** este es el método más sencillo.</span><span class="sxs-lookup"><span data-stu-id="1ae79-125">**Static list of parameters**: This is the simplest method.</span></span> <span data-ttu-id="1ae79-126">Puedes definir una lista de parámetros en el manifiesto de la aplicación que Teams cliente, pero no puedes controlar el formato en este caso.</span><span class="sxs-lookup"><span data-stu-id="1ae79-126">You can define a list of parameters in your app manifest the Teams client renders, but cannot control the formatting in this case.</span></span>
* <span data-ttu-id="1ae79-127">**Tarjeta adaptable:** puedes seleccionar usar una tarjeta adaptable, que proporciona un mayor control sobre la interfaz de usuario, pero aún te limita a los controles y opciones de formato disponibles.</span><span class="sxs-lookup"><span data-stu-id="1ae79-127">**Adaptive Card**:  You can select to use an Adaptive Card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="1ae79-128">**Vista web incrustada:** puede seleccionar insertar una vista web personalizada en el módulo de tareas para tener un control completo sobre la interfaz de usuario y los controles.</span><span class="sxs-lookup"><span data-stu-id="1ae79-128">**Embedded web view**: You can select to embed a custom web view in the task module to have a complete control over the UI and controls.</span></span> 

<span data-ttu-id="1ae79-129">Si selecciona crear el módulo de tareas con una lista estática de parámetros y cuando el usuario envía el módulo de tareas, se llama a la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1ae79-129">If you select to create the task module with a static list of parameters and when the user submits the task module, the messaging extension is called.</span></span> <span data-ttu-id="1ae79-130">Al usar una vista web incrustada o una tarjeta adaptable, la extensión de mensajería debe controlar un evento de invocación inicial del usuario, crear el módulo de tareas y devolverlo al cliente.</span><span class="sxs-lookup"><span data-stu-id="1ae79-130">When using an embedded web view or an Adaptive Card, your messaging extension must handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="select-how-the-final-message-is-sent"></a><span data-ttu-id="1ae79-131">Seleccionar cómo se envía el mensaje final</span><span class="sxs-lookup"><span data-stu-id="1ae79-131">Select how the final message is sent</span></span>

<span data-ttu-id="1ae79-132">En la mayoría de los casos, el comando action da como resultado una tarjeta insertada en el cuadro de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="1ae79-132">In most cases, the action command results in a card inserted into the compose message box.</span></span> <span data-ttu-id="1ae79-133">El usuario puede enviarlo al canal o chat.</span><span class="sxs-lookup"><span data-stu-id="1ae79-133">The user can send it into the channel or chat.</span></span> <span data-ttu-id="1ae79-134">En este caso, el mensaje proviene del usuario y el bot no puede editar ni actualizar aún más la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="1ae79-134">In this case, the message comes from the user, and the bot cannot edit or update the card further.</span></span>

<span data-ttu-id="1ae79-135">Si la extensión de mensajería se invoca desde el cuadro de redacción o directamente desde un mensaje, el servicio web puede insertar la respuesta final directamente en el canal o chat.</span><span class="sxs-lookup"><span data-stu-id="1ae79-135">If the messaging extension is invoked from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="1ae79-136">En este caso, la tarjeta adaptable proviene del bot, el bot la actualiza y responde al hilo de conversación si es necesario.</span><span class="sxs-lookup"><span data-stu-id="1ae79-136">In this case, the Adaptive Card comes from the bot, the bot updates it, and replies to the conversation thread if needed.</span></span> <span data-ttu-id="1ae79-137">Debes agregar el objeto al manifiesto de la aplicación `bot` con el mismo identificador y definir los ámbitos adecuados.</span><span class="sxs-lookup"><span data-stu-id="1ae79-137">You must add the `bot` object to the app manifest using  the same ID and defining the appropriate scopes.</span></span>

## <a name="add-the-action-command-to-your-app-manifest"></a><span data-ttu-id="1ae79-138">Agregar el comando action al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1ae79-138">Add the action command to your app manifest</span></span>

<span data-ttu-id="1ae79-139">Para agregar el comando action al manifiesto de la aplicación, debes agregar un nuevo objeto al `composeExtension` nivel superior del JSON del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ae79-139">To add the action command to the app manifest, you must add a new `composeExtension` object to the top level of the app manifest JSON.</span></span> <span data-ttu-id="1ae79-140">Puede usar una de las siguientes maneras de hacerlo:</span><span class="sxs-lookup"><span data-stu-id="1ae79-140">You can use one of the following ways to do so:</span></span>

* [<span data-ttu-id="1ae79-141">Crear un comando de acción con App Studio</span><span class="sxs-lookup"><span data-stu-id="1ae79-141">Create an action command using App Studio</span></span>](#create-an-action-command-using-app-studio)
* [<span data-ttu-id="1ae79-142">Crear un comando de acción manualmente</span><span class="sxs-lookup"><span data-stu-id="1ae79-142">Create an action command manually</span></span>](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a><span data-ttu-id="1ae79-143">Crear un comando de acción con App Studio</span><span class="sxs-lookup"><span data-stu-id="1ae79-143">Create an action command using App Studio</span></span>

> [!NOTE]
> <span data-ttu-id="1ae79-144">El requisito previo para crear un comando de acción es que ya ha creado una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1ae79-144">The prerequisite to create an action command is that you have already created a messaging extension.</span></span> <span data-ttu-id="1ae79-145">Para obtener información sobre cómo crear una extensión de mensajería, vea [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1ae79-145">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="1ae79-146">**Para crear un comando de acción**</span><span class="sxs-lookup"><span data-stu-id="1ae79-146">**To create an action command**</span></span>

1. <span data-ttu-id="1ae79-147">Abre **App Studio** desde el Microsoft Teams y selecciona la pestaña Editor de **manifiestos.**</span><span class="sxs-lookup"><span data-stu-id="1ae79-147">Open **App Studio** from the Microsoft Teams client and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="1ae79-148">Si ya creaste el paquete de la aplicación en **App Studio,** selecciónelo en la lista.</span><span class="sxs-lookup"><span data-stu-id="1ae79-148">If you already created your app package in **App Studio**, select it from the list.</span></span> <span data-ttu-id="1ae79-149">Si no has creado un paquete de aplicación, importa uno existente.</span><span class="sxs-lookup"><span data-stu-id="1ae79-149">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="1ae79-150">Después de importar un paquete de aplicación, selecciona **Extensiones de mensajería en** **Funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="1ae79-150">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="1ae79-151">Obtiene una ventana emergente para configurar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1ae79-151">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="1ae79-152">Selecciona **Configurar en la** ventana para incluir la extensión de mensajería en la experiencia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ae79-152">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="1ae79-153">En la siguiente imagen se muestra la ventana de configuración de la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="1ae79-153">The following image displays the messaging extension set up window:</span></span>

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>
    
1. <span data-ttu-id="1ae79-154">Para crear una extensión de mensajería, necesita un bot registrado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1ae79-154">To create a messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="1ae79-155">Puede usar un bot existente o crear un bot nuevo.</span><span class="sxs-lookup"><span data-stu-id="1ae79-155">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="1ae79-156">Seleccione **Crear nueva opción de bot,** asigne un nombre al nuevo bot y seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1ae79-156">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="1ae79-157">En la siguiente imagen se muestra la creación de bots para la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="1ae79-157">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="1ae79-158">Seleccione **Agregar** en la **sección Comando** de la página extensiones de mensajería para incluir los comandos que deciden el comportamiento de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1ae79-158">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="1ae79-159">La siguiente imagen muestra la adición de comandos para la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="1ae79-159">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. <span data-ttu-id="1ae79-160">Seleccione **Permitir que los usuarios desencadene acciones** en servicios externos mientras están dentro de Teams .</span><span class="sxs-lookup"><span data-stu-id="1ae79-160">Select **Allow users to trigger actions in external services while inside of Teams**.</span></span> <span data-ttu-id="1ae79-161">En la siguiente imagen se muestra la selección de comandos de acción:</span><span class="sxs-lookup"><span data-stu-id="1ae79-161">The following image displays the action command selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>
    
1. <span data-ttu-id="1ae79-162">Para usar un conjunto estático de parámetros para crear el módulo de tareas, seleccione Definir un conjunto de parámetros **estáticos para el comando**.</span><span class="sxs-lookup"><span data-stu-id="1ae79-162">To use a static set of parameters to create your task module, select **Define a set of static parameters for the command**.</span></span> 

    <span data-ttu-id="1ae79-163">En la imagen siguiente se muestra la selección del parámetro estático del comando de acción:</span><span class="sxs-lookup"><span data-stu-id="1ae79-163">The following image displays the action command static parameter selection:</span></span>

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/> 
   
    <span data-ttu-id="1ae79-164">La siguiente imagen muestra un ejemplo de configuración de parámetros estáticos:</span><span class="sxs-lookup"><span data-stu-id="1ae79-164">The following image displays an example static parameter set-up:</span></span> 

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    <span data-ttu-id="1ae79-165">En la siguiente imagen se muestra un ejemplo de pruebas de parámetros estáticos:</span><span class="sxs-lookup"><span data-stu-id="1ae79-165">The following image displays an example static parameter testing:</span></span>

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. <span data-ttu-id="1ae79-166">Para usar parámetros dinámicos, seleccione **Capturar un conjunto dinámico de parámetros del bot**.</span><span class="sxs-lookup"><span data-stu-id="1ae79-166">To use dynamic parameters, select to **Fetch a dynamic set of parameters from your bot**.</span></span> <span data-ttu-id="1ae79-167">En la siguiente imagen se muestra la selección del parámetro de comando de acción:</span><span class="sxs-lookup"><span data-stu-id="1ae79-167">The following image displays the action command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>
    
1. <span data-ttu-id="1ae79-168">Agregue un **identificador de comando** y un **título**.</span><span class="sxs-lookup"><span data-stu-id="1ae79-168">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="1ae79-169">Seleccione la ubicación desde la que desea invocar el comando de acción.</span><span class="sxs-lookup"><span data-stu-id="1ae79-169">Select the location from where you want to invoke the action command.</span></span> <span data-ttu-id="1ae79-170">La siguiente imagen muestra la ubicación de invocación del comando de acción:</span><span class="sxs-lookup"><span data-stu-id="1ae79-170">The following image displays the action command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. <span data-ttu-id="1ae79-171">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1ae79-171">Select **Save**.</span></span>
1. <span data-ttu-id="1ae79-172">Para agregar más parámetros, seleccione el **botón Agregar** en la **sección Parámetros.**</span><span class="sxs-lookup"><span data-stu-id="1ae79-172">To add more parameters, select the **Add** button in the **Parameters** section.</span></span>

### <a name="create-an-action-command-manually"></a><span data-ttu-id="1ae79-173">Crear un comando de acción manualmente</span><span class="sxs-lookup"><span data-stu-id="1ae79-173">Create an action command manually</span></span>

<span data-ttu-id="1ae79-174">Para agregar manualmente el comando de extensión de mensajería basada en acciones al manifiesto de la aplicación, debe agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos:</span><span class="sxs-lookup"><span data-stu-id="1ae79-174">To manually add your action-based messaging extension command to your app manifest, you must add the following parameters to the `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="1ae79-175">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="1ae79-175">Property name</span></span> | <span data-ttu-id="1ae79-176">Objetivo</span><span class="sxs-lookup"><span data-stu-id="1ae79-176">Purpose</span></span> | <span data-ttu-id="1ae79-177">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="1ae79-177">Required?</span></span> | <span data-ttu-id="1ae79-178">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="1ae79-178">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="1ae79-179">Esta propiedad es un identificador único que se asigna a este comando.</span><span class="sxs-lookup"><span data-stu-id="1ae79-179">This property is an unique ID that you assign to this command.</span></span> <span data-ttu-id="1ae79-180">La solicitud de usuario incluye este identificador.</span><span class="sxs-lookup"><span data-stu-id="1ae79-180">The user request includes this ID.</span></span> | <span data-ttu-id="1ae79-181">Sí</span><span class="sxs-lookup"><span data-stu-id="1ae79-181">Yes</span></span> | <span data-ttu-id="1ae79-182">1.0</span><span class="sxs-lookup"><span data-stu-id="1ae79-182">1.0</span></span> |
| `title` | <span data-ttu-id="1ae79-183">Esta propiedad es un nombre de comando.</span><span class="sxs-lookup"><span data-stu-id="1ae79-183">This property is a command name.</span></span> <span data-ttu-id="1ae79-184">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1ae79-184">This value appears in the UI.</span></span> | <span data-ttu-id="1ae79-185">Sí</span><span class="sxs-lookup"><span data-stu-id="1ae79-185">Yes</span></span> | <span data-ttu-id="1ae79-186">1.0</span><span class="sxs-lookup"><span data-stu-id="1ae79-186">1.0</span></span> |
| `type` | <span data-ttu-id="1ae79-187">Esta propiedad debe ser `action` un .</span><span class="sxs-lookup"><span data-stu-id="1ae79-187">This property must be an `action`.</span></span> | <span data-ttu-id="1ae79-188">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-188">No</span></span> | <span data-ttu-id="1ae79-189">1.4</span><span class="sxs-lookup"><span data-stu-id="1ae79-189">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="1ae79-190">Esta propiedad se establece en para una tarjeta adaptable o una vista web incrustada para el módulo de tareas, y para una lista estática de parámetros o al cargar la vista `true` `false` web mediante un `taskInfo` .</span><span class="sxs-lookup"><span data-stu-id="1ae79-190">This property is set to `true` for an adaptive card or embedded web view for your task module, and`false` for a static list of parameters or when loading the web view by a `taskInfo`.</span></span> | <span data-ttu-id="1ae79-191">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-191">No</span></span> | <span data-ttu-id="1ae79-192">1.4</span><span class="sxs-lookup"><span data-stu-id="1ae79-192">1.4</span></span> |
| `context` | <span data-ttu-id="1ae79-193">Esta propiedad es una matriz opcional de valores que define desde dónde se invoca la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1ae79-193">This property is an optional array of values that defines where the messaging extension is invoked from.</span></span> <span data-ttu-id="1ae79-194">Los valores posibles son`message`, `compose` o `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="1ae79-194">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="1ae79-195">El valor predeterminado es `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="1ae79-195">The default value is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="1ae79-196">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-196">No</span></span> | <span data-ttu-id="1ae79-197">1,5</span><span class="sxs-lookup"><span data-stu-id="1ae79-197">1.5</span></span> |

<span data-ttu-id="1ae79-198">Si usa una lista estática de parámetros, también debe agregar los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="1ae79-198">If you are using a static list of parameters, you must also add the following parameters:</span></span>

| <span data-ttu-id="1ae79-199">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="1ae79-199">Property name</span></span> | <span data-ttu-id="1ae79-200">Objetivo</span><span class="sxs-lookup"><span data-stu-id="1ae79-200">Purpose</span></span> | <span data-ttu-id="1ae79-201">¿Es necesario?</span><span class="sxs-lookup"><span data-stu-id="1ae79-201">Is required?</span></span> | <span data-ttu-id="1ae79-202">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="1ae79-202">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="1ae79-203">Esta propiedad describe la lista estática de parámetros para el comando.</span><span class="sxs-lookup"><span data-stu-id="1ae79-203">This property describes the static list of parameters for the command.</span></span> <span data-ttu-id="1ae79-204">Solo se usa cuando `fetchTask` es `false` .</span><span class="sxs-lookup"><span data-stu-id="1ae79-204">Only use when `fetchTask` is `false`.</span></span> | <span data-ttu-id="1ae79-205">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-205">No</span></span> | <span data-ttu-id="1ae79-206">1.0</span><span class="sxs-lookup"><span data-stu-id="1ae79-206">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="1ae79-207">Esta propiedad describe el nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="1ae79-207">This property describes the name of the parameter.</span></span> <span data-ttu-id="1ae79-208">Esto se envía al servicio en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="1ae79-208">This is sent to your service in the user request.</span></span> | <span data-ttu-id="1ae79-209">Sí</span><span class="sxs-lookup"><span data-stu-id="1ae79-209">Yes</span></span> | <span data-ttu-id="1ae79-210">1.0</span><span class="sxs-lookup"><span data-stu-id="1ae79-210">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="1ae79-211">Esta propiedad describe los propósitos del parámetro o el ejemplo del valor que se debe proporcionar.</span><span class="sxs-lookup"><span data-stu-id="1ae79-211">This property describes the parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="1ae79-212">Este valor aparece en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1ae79-212">This value appears in the UI.</span></span> | <span data-ttu-id="1ae79-213">Sí</span><span class="sxs-lookup"><span data-stu-id="1ae79-213">Yes</span></span> | <span data-ttu-id="1ae79-214">1.0</span><span class="sxs-lookup"><span data-stu-id="1ae79-214">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="1ae79-215">Esta propiedad es un título o etiqueta de parámetros fáciles de usar.</span><span class="sxs-lookup"><span data-stu-id="1ae79-215">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="1ae79-216">Sí</span><span class="sxs-lookup"><span data-stu-id="1ae79-216">Yes</span></span> | <span data-ttu-id="1ae79-217">1.0</span><span class="sxs-lookup"><span data-stu-id="1ae79-217">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="1ae79-218">Esta propiedad se establece en el tipo de entrada necesario.</span><span class="sxs-lookup"><span data-stu-id="1ae79-218">This property is set to the type of input required.</span></span> <span data-ttu-id="1ae79-219">Los valores posibles `text` incluyen , , , , , `textarea` `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="1ae79-219">The possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="1ae79-220">El valor predeterminado se establece en `text` .</span><span class="sxs-lookup"><span data-stu-id="1ae79-220">The default value is set to `text`.</span></span> | <span data-ttu-id="1ae79-221">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-221">No</span></span> | <span data-ttu-id="1ae79-222">1.4</span><span class="sxs-lookup"><span data-stu-id="1ae79-222">1.4</span></span> |

<span data-ttu-id="1ae79-223">Si usa una vista web incrustada, opcionalmente puede agregar el objeto para capturar la vista `taskInfo` web sin llamar directamente al bot.</span><span class="sxs-lookup"><span data-stu-id="1ae79-223">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="1ae79-224">Si selecciona esta opción, el comportamiento es similar al de usar una lista estática de parámetros.</span><span class="sxs-lookup"><span data-stu-id="1ae79-224">If you select this option, the behavior is similar to that of using a static list of parameters.</span></span> <span data-ttu-id="1ae79-225">En el caso de que la primera interacción con el bot [responde al módulo de tareas enviar acción](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span><span class="sxs-lookup"><span data-stu-id="1ae79-225">In that the first interaction with your bot is [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="1ae79-226">Si usa un `taskInfo` objeto, debe establecer el `fetchTask` parámetro en `false` .</span><span class="sxs-lookup"><span data-stu-id="1ae79-226">If you are using a `taskInfo` object, you must set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="1ae79-227">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="1ae79-227">Property name</span></span> | <span data-ttu-id="1ae79-228">Objetivo</span><span class="sxs-lookup"><span data-stu-id="1ae79-228">Purpose</span></span> | <span data-ttu-id="1ae79-229">¿Es necesario?</span><span class="sxs-lookup"><span data-stu-id="1ae79-229">Is required?</span></span> | <span data-ttu-id="1ae79-230">Versión mínima del manifiesto</span><span class="sxs-lookup"><span data-stu-id="1ae79-230">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="1ae79-231">Especifique el módulo de tareas que se debe precargar al usar un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1ae79-231">Specify the task module to preload when using a messaging extension command.</span></span> | <span data-ttu-id="1ae79-232">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-232">No</span></span> | <span data-ttu-id="1ae79-233">1.4</span><span class="sxs-lookup"><span data-stu-id="1ae79-233">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="1ae79-234">Título del módulo de tareas inicial.</span><span class="sxs-lookup"><span data-stu-id="1ae79-234">Initial task module title.</span></span> |<span data-ttu-id="1ae79-235">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-235">No</span></span> | <span data-ttu-id="1ae79-236">1.4</span><span class="sxs-lookup"><span data-stu-id="1ae79-236">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="1ae79-237">Ancho del módulo de tareas, ya sea un número en píxeles o un diseño predeterminado como `large` , `medium` o `small` .</span><span class="sxs-lookup"><span data-stu-id="1ae79-237">Task module width, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span> |<span data-ttu-id="1ae79-238">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-238">No</span></span> | <span data-ttu-id="1ae79-239">1.4</span><span class="sxs-lookup"><span data-stu-id="1ae79-239">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="1ae79-240">Alto del módulo de tareas, ya sea un número en píxeles o un diseño predeterminado como `large` , `medium` o `small` .</span><span class="sxs-lookup"><span data-stu-id="1ae79-240">Task module height, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span>|<span data-ttu-id="1ae79-241">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-241">No</span></span> | <span data-ttu-id="1ae79-242">1.4</span><span class="sxs-lookup"><span data-stu-id="1ae79-242">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="1ae79-243">Dirección URL de vista web inicial.</span><span class="sxs-lookup"><span data-stu-id="1ae79-243">Initial web view URL.</span></span>|<span data-ttu-id="1ae79-244">No</span><span class="sxs-lookup"><span data-stu-id="1ae79-244">No</span></span> | <span data-ttu-id="1ae79-245">1.4</span><span class="sxs-lookup"><span data-stu-id="1ae79-245">1.4</span></span> | 

#### <a name="app-manifest-example"></a><span data-ttu-id="1ae79-246">Ejemplo de manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1ae79-246">App manifest example</span></span>

<span data-ttu-id="1ae79-247">La siguiente sección es un ejemplo de un `composeExtensions` objeto que define dos comandos de acción.</span><span class="sxs-lookup"><span data-stu-id="1ae79-247">The following section is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="1ae79-248">No es un ejemplo del manifiesto completo.</span><span class="sxs-lookup"><span data-stu-id="1ae79-248">It is not an example of the complete manifest.</span></span> <span data-ttu-id="1ae79-249">Para ver el esquema de manifiesto de aplicación completo, consulta [Esquema de manifiesto de la aplicación:](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="1ae79-249">For the complete app manifest schema, see [app manifest schema](~/resources/schema/manifest-schema.md):</span></span>

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
        "fetchTask": true,
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

## <a name="code-sample"></a><span data-ttu-id="1ae79-250">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="1ae79-250">Code sample</span></span>

| <span data-ttu-id="1ae79-251">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1ae79-251">Sample Name</span></span>           | <span data-ttu-id="1ae79-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="1ae79-252">Description</span></span> | <span data-ttu-id="1ae79-253">.NET</span><span class="sxs-lookup"><span data-stu-id="1ae79-253">.NET</span></span>    | <span data-ttu-id="1ae79-254">Node.js</span><span class="sxs-lookup"><span data-stu-id="1ae79-254">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="1ae79-255">Teams extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="1ae79-255">Teams messaging extension action</span></span>| <span data-ttu-id="1ae79-256">Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="1ae79-256">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="1ae79-257">View</span><span class="sxs-lookup"><span data-stu-id="1ae79-257">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="1ae79-258">View</span><span class="sxs-lookup"><span data-stu-id="1ae79-258">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="1ae79-259">Teams de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="1ae79-259">Teams messaging extension search</span></span>   |  <span data-ttu-id="1ae79-260">Describe cómo definir comandos de búsqueda y responder a las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="1ae79-260">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="1ae79-261">View</span><span class="sxs-lookup"><span data-stu-id="1ae79-261">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="1ae79-262">View</span><span class="sxs-lookup"><span data-stu-id="1ae79-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="1ae79-263">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1ae79-263">Next step</span></span>

<span data-ttu-id="1ae79-264">Si usa una tarjeta adaptable o una vista web incrustada sin un objeto, el `taskInfo` siguiente paso es:</span><span class="sxs-lookup"><span data-stu-id="1ae79-264">If you are using either an Adaptive Card or an embedded web view without a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ae79-265">Crear y responder con un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="1ae79-265">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="1ae79-266">Si usa los parámetros o una vista web incrustada con un `taskInfo` objeto, el siguiente paso es:</span><span class="sxs-lookup"><span data-stu-id="1ae79-266">If you are using the parameters or an embedded web view with a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ae79-267">Responder al envío del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="1ae79-267">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

