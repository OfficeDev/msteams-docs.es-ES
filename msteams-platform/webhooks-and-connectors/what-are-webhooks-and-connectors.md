---
title: Webhooks y conectores
author: clearab
description: Comprenda cómo los webhooks y conectores pueden conectar los servicios web al Teams cliente.
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2cb763a6637abd3faa500de871119f0b829871bf
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140057"
---
# <a name="webhooks-and-connectors"></a><span data-ttu-id="e9306-103">Webhooks y conectores</span><span class="sxs-lookup"><span data-stu-id="e9306-103">Webhooks and connectors</span></span>

<span data-ttu-id="e9306-104">Webhooks and connectors help to connect the web services to channels and teams in Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e9306-104">Webhooks and connectors help to connect the web services to channels and teams in Microsoft Teams.</span></span> <span data-ttu-id="e9306-105">Los webhooks son una devolución de llamada HTTP definida por el usuario que notifica a los usuarios sobre cualquier acción que haya tenido lugar en el Microsoft Teams web.</span><span class="sxs-lookup"><span data-stu-id="e9306-105">Webhooks are user defined HTTP callback that notifies users about any action that has taken place in the Microsoft Teams channel.</span></span> <span data-ttu-id="e9306-106">Es una forma de que una aplicación obtenga datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="e9306-106">It is a way for an app to get real time data.</span></span> <span data-ttu-id="e9306-107">Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web.</span><span class="sxs-lookup"><span data-stu-id="e9306-107">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="e9306-108">Exponen un extremo HTTPS para que el servicio publique mensajes en forma de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="e9306-108">They expose an HTTPS endpoint for your service to post messages in the form of cards.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="e9306-109">Webhooks salientes</span><span class="sxs-lookup"><span data-stu-id="e9306-109">Outgoing Webhooks</span></span>

<span data-ttu-id="e9306-110">Los webhooks ayudan Teams integrar con aplicaciones externas.</span><span class="sxs-lookup"><span data-stu-id="e9306-110">Webhooks help Teams to integrate with external apps.</span></span> <span data-ttu-id="e9306-111">Con webhooks salientes, puede enviar mensajes de texto desde un canal a los servicios web.</span><span class="sxs-lookup"><span data-stu-id="e9306-111">With Outgoing Webhooks, you can send text messages from a channel to the web services.</span></span> <span data-ttu-id="e9306-112">Después de configurar los webhooks salientes, los usuarios @mention webhook saliente y enviar un mensaje a los servicios web.</span><span class="sxs-lookup"><span data-stu-id="e9306-112">After configuring the Outgoing Webhooks, users can @mention Outgoing Webhook and send a message to web services.</span></span> <span data-ttu-id="e9306-113">El servicio responde en un plazo de diez segundos al mensaje con un texto o una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e9306-113">The service responds within ten seconds to the message with a text or a card.</span></span>

> [!NOTE]
> <span data-ttu-id="e9306-114">Los webhooks salientes se configuran por equipo y no se pueden incluir como parte de una aplicación Teams normal.</span><span class="sxs-lookup"><span data-stu-id="e9306-114">Outgoing Webhooks are configured on a per team basis and cannot be included as part of a normal Teams app.</span></span>

## <a name="connectors"></a><span data-ttu-id="e9306-115">Conectores</span><span class="sxs-lookup"><span data-stu-id="e9306-115">Connectors</span></span>

<span data-ttu-id="e9306-116">Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web.</span><span class="sxs-lookup"><span data-stu-id="e9306-116">Connectors allow users to subscribe to receive notifications and messages from the web services.</span></span> <span data-ttu-id="e9306-117">Exponen el punto de conexión HTTPS para que el servicio publique mensajes Teams canales, normalmente en forma de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="e9306-117">They expose the HTTPS endpoint for the service to post messages to Teams channels, typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="e9306-118">Webhooks entrantes</span><span class="sxs-lookup"><span data-stu-id="e9306-118">Incoming Webhooks</span></span>

<span data-ttu-id="e9306-119">Los webhooks entrantes ayudan a publicar mensajes desde aplicaciones a Teams.</span><span class="sxs-lookup"><span data-stu-id="e9306-119">Incoming Webhooks help in posting messages from apps to Teams.</span></span> <span data-ttu-id="e9306-120">Si los webhooks entrantes están habilitados para un equipo en cualquier canal, expone el extremo HTTPS, que acepta JSON con el formato correcto e inserta los mensajes en ese canal.</span><span class="sxs-lookup"><span data-stu-id="e9306-120">If Incoming Webhooks are enabled for a team in any channel, it exposes the HTTPS endpoint, which accepts correctly formatted JSON and inserts the messages into that channel.</span></span> <span data-ttu-id="e9306-121">Por ejemplo, puede crear un webhook entrante en el canal de DevOps, configurar la compilación e implementar y supervisar simultáneamente servicios para enviar alertas.</span><span class="sxs-lookup"><span data-stu-id="e9306-121">For example, you can create an Incoming Webhook in your DevOps channel, configure your build, and simultaneously deploy and monitor services to send alerts.</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="e9306-122">Conectores de Office 365</span><span class="sxs-lookup"><span data-stu-id="e9306-122">Office 365 Connectors</span></span>

<span data-ttu-id="e9306-123">Office 365 Los conectores te permiten crear una página de configuración personalizada para el webhook entrante y empaquetarlos como parte de una Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9306-123">Office 365 Connectors allow you to create a custom configuration page for your Incoming Webhook and package them as part of a Teams app.</span></span> <span data-ttu-id="e9306-124">Los mensajes se envían principalmente mediante Office 365 connector y tienen la capacidad de agregarles un conjunto limitado de acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e9306-124">You send messages primarily using Office 365 Connector cards and have the ability to add a limited set of card actions to them.</span></span> <span data-ttu-id="e9306-125">Por ejemplo, un conector meteorológico que permite a los usuarios seleccionar una ubicación y hora del día, para recibir actualizaciones sobre el tiempo del mañana.</span><span class="sxs-lookup"><span data-stu-id="e9306-125">For example, a weather connector that allows users to select a location and time of day, to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="e9306-126">Se configuran en un nivel de canal, pero se instalan en un nivel de equipo.</span><span class="sxs-lookup"><span data-stu-id="e9306-126">They are configured on a channel level but are installed at a team level.</span></span>

> [!NOTE]
> <span data-ttu-id="e9306-127">Puedes distribuir la aplicación Office 365 Connector Teams a nuestra AppStore.</span><span class="sxs-lookup"><span data-stu-id="e9306-127">You can distribute the Office 365 Connector Teams app to our AppStore.</span></span>

## <a name="create-and-send-messages"></a><span data-ttu-id="e9306-128">Crear y enviar mensajes</span><span class="sxs-lookup"><span data-stu-id="e9306-128">Create and send messages</span></span>

<span data-ttu-id="e9306-129">Los mensajes que se pueden usar permiten a los usuarios tomar medidas sin salir de su cliente de correo electrónico, lo que aumenta la participación de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e9306-129">Actionable messages allow users to take action without leaving their email client, increasing user engagement.</span></span> <span data-ttu-id="e9306-130">Con Office 365 webhooks entrantes y de entrada, puede enviar mensajes publicando una carga JSON en la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="e9306-130">With Office 365 and Incoming Webhooks, you can send messages by posting a JSON payload to the webhook URL.</span></span>

## <a name="see-also"></a><span data-ttu-id="e9306-131">Vea también</span><span class="sxs-lookup"><span data-stu-id="e9306-131">See also</span></span>

* [<span data-ttu-id="e9306-132">Crear un webhook entrante</span><span class="sxs-lookup"><span data-stu-id="e9306-132">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="e9306-133">Crear un Conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="e9306-133">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="e9306-134">Crear y enviar mensajes</span><span class="sxs-lookup"><span data-stu-id="e9306-134">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="next-step"></a><span data-ttu-id="e9306-135">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="e9306-135">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9306-136">Crear un webhook saliente</span><span class="sxs-lookup"><span data-stu-id="e9306-136">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
