---
title: Crear un webhook entrante
author: laujan
description: describe cómo agregar webhook entrante Teams aplicación y publicar solicitudes externas para Teams webhooks entrantes
keywords: webhook saliente de pestañas de teams
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 53fe9725148579325386fa4677bebb61fdb72c56
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140143"
---
# <a name="create-incoming-webhook"></a><span data-ttu-id="697b9-104">Crear webhook entrante</span><span class="sxs-lookup"><span data-stu-id="697b9-104">Create Incoming Webhook</span></span>

<span data-ttu-id="697b9-105">El webhook entrante permite que cualquier aplicación externa comparta contenido en Teams canales.</span><span class="sxs-lookup"><span data-stu-id="697b9-105">Incoming Webhook allows any external apps to share content in Teams channels.</span></span> <span data-ttu-id="697b9-106">Estos webhooks se usan como herramientas de seguimiento y notificación.</span><span class="sxs-lookup"><span data-stu-id="697b9-106">These webhooks are used as tracking and notifying tools.</span></span> <span data-ttu-id="697b9-107">Proporcionan una dirección URL única, a la que se envía una carga JSON con un mensaje en formato de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="697b9-107">They provide a unique URL, to which you send a JSON payload with a message in card format.</span></span> <span data-ttu-id="697b9-108">Las tarjetas son contenedores de interfaz de usuario que incluyen contenido y acciones relacionadas con un solo tema.</span><span class="sxs-lookup"><span data-stu-id="697b9-108">Cards are user interface containers that include content and actions related to a single topic.</span></span> <span data-ttu-id="697b9-109">Teams tarjetas dentro de las siguientes funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="697b9-109">Teams use cards within the following capabilities:</span></span>

* <span data-ttu-id="697b9-110">Bots</span><span class="sxs-lookup"><span data-stu-id="697b9-110">Bots</span></span>
* <span data-ttu-id="697b9-111">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="697b9-111">Messaging extensions</span></span>
* <span data-ttu-id="697b9-112">Conectores</span><span class="sxs-lookup"><span data-stu-id="697b9-112">Connectors</span></span>

## <a name="key-features-of-incoming-webhook"></a><span data-ttu-id="697b9-113">Características clave del webhook entrante</span><span class="sxs-lookup"><span data-stu-id="697b9-113">Key features of Incoming Webhook</span></span>

<span data-ttu-id="697b9-114">En la tabla siguiente se proporcionan las características y la descripción del webhook entrante:</span><span class="sxs-lookup"><span data-stu-id="697b9-114">The following table provides the features and description of Incoming Webhook:</span></span>

| <span data-ttu-id="697b9-115">Características</span><span class="sxs-lookup"><span data-stu-id="697b9-115">Features</span></span> | <span data-ttu-id="697b9-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="697b9-116">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="697b9-117">Tarjetas adaptables con un webhook entrante</span><span class="sxs-lookup"><span data-stu-id="697b9-117">Adaptive Cards using an Incoming Webhook</span></span>|<span data-ttu-id="697b9-118">Las tarjetas adaptables se pueden enviar a través de webhooks entrantes.</span><span class="sxs-lookup"><span data-stu-id="697b9-118">Adaptive Cards can be sent through Incoming Webhooks.</span></span> <span data-ttu-id="697b9-119">Para obtener más información, vea [Enviar tarjetas adaptables mediante webhooks entrantes.](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)</span><span class="sxs-lookup"><span data-stu-id="697b9-119">For more information, see [Send Adaptive Cards using Incoming Webhooks](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook).</span></span>|
|<span data-ttu-id="697b9-120">Compatibilidad con mensajes que se pueden tomar medidas</span><span class="sxs-lookup"><span data-stu-id="697b9-120">Actionable messaging support</span></span>|<span data-ttu-id="697b9-121">Las tarjetas de mensaje que pueden actuar se admiten en todos Office 365 grupos, incluidos Teams.</span><span class="sxs-lookup"><span data-stu-id="697b9-121">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="697b9-122">Si envía mensajes a través de tarjetas, debe usar el formato de tarjeta de mensaje que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="697b9-122">If you send messages through cards, you must use the actionable message card format.</span></span> <span data-ttu-id="697b9-123">Para obtener más información, vea [referencia de](/outlook/actionable-messages/message-card-reference) tarjeta de mensaje heredada y área de juegos de [tarjetas de mensaje.](https://messagecardplayground.azurewebsites.net)</span><span class="sxs-lookup"><span data-stu-id="697b9-123">For more information, see [legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and [message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="697b9-124">Compatibilidad con mensajería HTTPS independiente</span><span class="sxs-lookup"><span data-stu-id="697b9-124">Independent HTTPS messaging support</span></span>|<span data-ttu-id="697b9-125">Las tarjetas proporcionan información de forma clara y coherente.</span><span class="sxs-lookup"><span data-stu-id="697b9-125">Cards provide information clearly and consistently.</span></span> <span data-ttu-id="697b9-126">Cualquier herramienta o marco que pueda enviar solicitudes HTTPS POST, puede enviar mensajes a Teams a través de un webhook entrante.</span><span class="sxs-lookup"><span data-stu-id="697b9-126">Any tool or framework that can send HTTPS POST requests, can send messages to Teams through an Incoming Webhook.</span></span>|
|<span data-ttu-id="697b9-127">Compatibilidad con Markdown</span><span class="sxs-lookup"><span data-stu-id="697b9-127">Markdown support</span></span>|<span data-ttu-id="697b9-128">Todos los campos de texto de las tarjetas de mensajería que pueden actuar admiten Markdown básico.</span><span class="sxs-lookup"><span data-stu-id="697b9-128">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="697b9-129">No use el marcado HTML en las tarjetas.</span><span class="sxs-lookup"><span data-stu-id="697b9-129">Do not use HTML markup in your cards.</span></span> <span data-ttu-id="697b9-130">puesto que se omite y se trata como texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="697b9-130">HTML is ignored and treated as plain text.</span></span>|
|<span data-ttu-id="697b9-131">Configuración con ámbito</span><span class="sxs-lookup"><span data-stu-id="697b9-131">Scoped configuration</span></span>|<span data-ttu-id="697b9-132">El webhook entrante está en el ámbito y configurado en el nivel de canal.</span><span class="sxs-lookup"><span data-stu-id="697b9-132">Incoming Webhook is scoped and configured at the channel level.</span></span>|
|<span data-ttu-id="697b9-133">Definiciones de recursos seguros</span><span class="sxs-lookup"><span data-stu-id="697b9-133">Secure resource definitions</span></span>|<span data-ttu-id="697b9-134">Los mensajes tienen formato de carga JSON.</span><span class="sxs-lookup"><span data-stu-id="697b9-134">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="697b9-135">Esta estructura de mensajería declarativa impide la inserción de código malintencionado.</span><span class="sxs-lookup"><span data-stu-id="697b9-135">This declarative messaging structure prevents the insertion of malicious code.</span></span>|

> [!NOTE]
> * <span data-ttu-id="697b9-136">Teams bots, extensiones de mensajería, Webhook entrante y Bot Framework admiten tarjetas adaptables, un marco abierto entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="697b9-136">Teams bots, messaging extensions, Incoming Webhook, and the Bot Framework support Adaptive Cards, an open cross card platform framework.</span></span> <span data-ttu-id="697b9-137">Actualmente, Teams no admiten [tarjetas](../../webhooks-and-connectors/how-to/connectors-creating.md) adaptables.</span><span class="sxs-lookup"><span data-stu-id="697b9-137">Currently, [Teams connectors](../../webhooks-and-connectors/how-to/connectors-creating.md) do not support Adaptive Cards.</span></span> <span data-ttu-id="697b9-138">Sin embargo, es posible crear un flujo [que](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) publica tarjetas adaptables en un Teams canal.</span><span class="sxs-lookup"><span data-stu-id="697b9-138">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts Adaptive Cards to a Teams channel.</span></span>
> * <span data-ttu-id="697b9-139">Para obtener más información sobre tarjetas y webhooks, vea [Adaptive cards and Incoming Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks).</span><span class="sxs-lookup"><span data-stu-id="697b9-139">For more information on cards and webhooks, see [Adaptive cards and Incoming Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks).</span></span>

## <a name="create-incoming-webhook"></a><span data-ttu-id="697b9-140">Crear webhook entrante</span><span class="sxs-lookup"><span data-stu-id="697b9-140">Create Incoming Webhook</span></span>

<span data-ttu-id="697b9-141">**Para agregar un webhook entrante a un canal Teams entrada**</span><span class="sxs-lookup"><span data-stu-id="697b9-141">**To add an Incoming Webhook to a Teams channel**</span></span>

1. <span data-ttu-id="697b9-142">Vaya al canal donde desea agregar el webhook y seleccione &#8226;&#8226;&#8226; **Más opciones** de la barra de navegación superior.</span><span class="sxs-lookup"><span data-stu-id="697b9-142">Go to the channel where you want to add the webhook and select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="697b9-143">Seleccione **Conectores en** el menú desplegable:</span><span class="sxs-lookup"><span data-stu-id="697b9-143">Select **Connectors** from the dropdown menu:</span></span>

    ![Seleccionar conector](~/assets/images/connectors.png)

1. <span data-ttu-id="697b9-145">Busque **Webhook entrante y** seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="697b9-145">Search for **Incoming Webhook** and select **Add**.</span></span>
1. <span data-ttu-id="697b9-146">Seleccione **Configurar**, proporcione un nombre y cargue una imagen para el webhook si es necesario:</span><span class="sxs-lookup"><span data-stu-id="697b9-146">Select **Configure**, provide a name, and upload an image for your webhook if required:</span></span>

    ![Botón Configurar](~/assets/images/configure.png)

1. <span data-ttu-id="697b9-148">La ventana de diálogo presenta una dirección URL única que se asigna al canal.</span><span class="sxs-lookup"><span data-stu-id="697b9-148">The dialog window presents a unique URL that maps to the channel.</span></span> <span data-ttu-id="697b9-149">Copie y guarde la dirección URL del webhook, para enviar información a Microsoft Teams y seleccione **Listo:**</span><span class="sxs-lookup"><span data-stu-id="697b9-149">Copy and save the webhook URL, to send information to Microsoft Teams and select **Done**:</span></span>

    ![DIRECCIÓN URL única](~/assets/images/url.png)

<span data-ttu-id="697b9-151">El webhook está disponible en el canal Teams web.</span><span class="sxs-lookup"><span data-stu-id="697b9-151">The webhook is available in the Teams channel.</span></span>

> [!NOTE]
> <span data-ttu-id="697b9-152">En Teams, seleccione **Configuración** Permisos de miembro Permitir a los miembros crear, actualizar y quitar conectores, de modo que cualquier miembro del equipo pueda agregar, modificar o eliminar  >    >  un conector.</span><span class="sxs-lookup"><span data-stu-id="697b9-152">In Teams, select **Settings** > **Member permissions** > **Allow members to create, update, and remove connectors**, so that any team member can add, modify, or delete a connector.</span></span>

## <a name="remove-incoming-webhook"></a><span data-ttu-id="697b9-153">Quitar webhook entrante</span><span class="sxs-lookup"><span data-stu-id="697b9-153">Remove Incoming Webhook</span></span>

<span data-ttu-id="697b9-154">**Para quitar un webhook entrante de un canal Teams entrada**</span><span class="sxs-lookup"><span data-stu-id="697b9-154">**To remove an Incoming Webhook from a Teams channel**</span></span>

1. <span data-ttu-id="697b9-155">Vaya al canal.</span><span class="sxs-lookup"><span data-stu-id="697b9-155">Go to the channel.</span></span>
1. <span data-ttu-id="697b9-156">Seleccione &#8226;&#8226;&#8226; **más opciones en** la barra de navegación superior.</span><span class="sxs-lookup"><span data-stu-id="697b9-156">Select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="697b9-157">Seleccione **Conectores en** el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="697b9-157">Select **Connectors** from the dropdown menu.</span></span>
1. <span data-ttu-id="697b9-158">A la izquierda, en **Administrar**, seleccione **Configurado**.</span><span class="sxs-lookup"><span data-stu-id="697b9-158">On the left, under **Manage**, select **Configured**.</span></span>
1. <span data-ttu-id="697b9-159">Seleccione el **< *1*> configurado para** ver una lista de los conectores actuales:</span><span class="sxs-lookup"><span data-stu-id="697b9-159">Select the **<*1*> Configured** to see a list of your current connectors:</span></span>

    ![Webhook configurado](~/assets/images/configured.png)

1. <span data-ttu-id="697b9-161">Seleccione **Administrar** junto al conector que desea quitar:</span><span class="sxs-lookup"><span data-stu-id="697b9-161">Select **Manage** next to the connector that you want to remove:</span></span>

    ![Administrar webhook](~/assets/images/manage.png)

1. <span data-ttu-id="697b9-163">Seleccione **Quitar**:</span><span class="sxs-lookup"><span data-stu-id="697b9-163">Select **Remove**:</span></span>

    ![Quitar webhook](~/assets/images/remove.png)

    <span data-ttu-id="697b9-165">Aparece **el cuadro de diálogo** Quitar configuración:</span><span class="sxs-lookup"><span data-stu-id="697b9-165">The **Remove Configuration** dialog box appears:</span></span>

    ![Quitar configuración](~/assets/images/removeconfiguration.png)

1. <span data-ttu-id="697b9-167">Complete los campos y casillas del cuadro de diálogo y seleccione **Quitar**:</span><span class="sxs-lookup"><span data-stu-id="697b9-167">Complete the dialog box fields and checkboxes and select **Remove**:</span></span>

    ![Eliminación final](~/assets/images/finalremove.png)

    <span data-ttu-id="697b9-169">El webhook se quita del Teams canal.</span><span class="sxs-lookup"><span data-stu-id="697b9-169">The webhook is removed from the Teams channel.</span></span>

## <a name="see-also"></a><span data-ttu-id="697b9-170">Vea también</span><span class="sxs-lookup"><span data-stu-id="697b9-170">See also</span></span>

* [<span data-ttu-id="697b9-171">Crear un webhook saliente</span><span class="sxs-lookup"><span data-stu-id="697b9-171">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [<span data-ttu-id="697b9-172">Crear un Conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="697b9-172">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="697b9-173">Crear y enviar mensajes</span><span class="sxs-lookup"><span data-stu-id="697b9-173">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
