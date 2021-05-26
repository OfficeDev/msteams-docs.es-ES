---
title: Crear aplicaciones para la Microsoft Teams plataforma
author: heath-hamilton
description: Obtenga información general sobre cómo los desarrolladores pueden ampliar Microsoft Teams características con aplicaciones personalizadas.
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 796353a4c556794a518a451e8a45989351729eb9
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646540"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="49286-103">Desarrollar aplicaciones para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="49286-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="49286-104">Microsoft Teams aplicaciones aportan información clave, herramientas comunes y procesos de confianza a los que las personas se reúnen, aprenden y trabajan cada vez más.</span><span class="sxs-lookup"><span data-stu-id="49286-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="49286-105">Las aplicaciones son la forma en que Teams para adaptarse a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="49286-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="49286-106">Crea algo nuevo para Teams o integra una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="49286-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49286-107">Comenzar aquí</span><span class="sxs-lookup"><span data-stu-id="49286-107">Start here</span></span>](get-started/prerequisites.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="49286-108">¿Qué Teams aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="49286-108">What are Teams apps?</span></span>

<span data-ttu-id="49286-109">Teams aplicaciones son una combinación de [funcionalidades.](concepts/capabilities-overview.md)</span><span class="sxs-lookup"><span data-stu-id="49286-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md).</span></span> <span data-ttu-id="49286-110">Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (administrar registros de pacientes).</span><span class="sxs-lookup"><span data-stu-id="49286-110">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="49286-111">Al planear la aplicación, recuerda que Teams es un centro de colaboración.</span><span class="sxs-lookup"><span data-stu-id="49286-111">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="49286-112">Las mejores Teams ayudan a las personas a expresarse y a trabajar mejor juntos.</span><span class="sxs-lookup"><span data-stu-id="49286-112">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="personal-apps"></a><span data-ttu-id="49286-113">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="49286-113">Personal apps</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="49286-114">**Ayudar a los usuarios** a centrarse: una [aplicación personal](concepts/design/personal-apps.md) es un espacio o bot dedicado para ayudar a los usuarios a centrarse en sus propias tareas o ver actividades importantes para ellos.</span><span class="sxs-lookup"><span data-stu-id="49286-114">**Help people focus**: A [personal app](concepts/design/personal-apps.md) is a dedicated space or bot to help users focus on their own tasks or view activities important to them.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="Representación conceptual de cómo son las aplicaciones personales en el Teams cliente." border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a><span data-ttu-id="49286-116">Pestañas</span><span class="sxs-lookup"><span data-stu-id="49286-116">Tabs</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="49286-117">**Colaborar más cómodamente:** muestre el contenido basado en web en una [pestaña](tabs/what-are-tabs.md) donde los usuarios puedan analizarlo y trabajar en él juntos.</span><span class="sxs-lookup"><span data-stu-id="49286-117">**Collaborate more conveniently**: Display your web-based content in a [tab](tabs/what-are-tabs.md) where people can discuss and work on it together.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="Representación conceptual de cómo son las pestañas en el Teams cliente." border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a><span data-ttu-id="49286-119">Bots</span><span class="sxs-lookup"><span data-stu-id="49286-119">Bots</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="49286-120">**Convertir palabras en acciones:** las conversaciones a menudo resultan en la necesidad de hacer algo (generar un pedido, revisar mi código, comprobar el estado del vale, y así sucesivamente).</span><span class="sxs-lookup"><span data-stu-id="49286-120">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="49286-121">Un [bot](bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo directamente dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="49286-121">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="Representación conceptual de cómo son los bots en el Teams cliente." border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a><span data-ttu-id="49286-123">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="49286-123">Messaging extensions</span></span>

:::row:::

   :::column span="1":::

<span data-ttu-id="49286-124">**Facilita la multitarea:** con extensiones [de mensajería,](messaging-extensions/what-are-messaging-extensions.md)puedes compartir rápidamente información externa en una conversación.</span><span class="sxs-lookup"><span data-stu-id="49286-124">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="49286-125">También puede actuar en un mensaje, como crear un vale de ayuda basado en el contenido de una publicación de canal.</span><span class="sxs-lookup"><span data-stu-id="49286-125">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="Representación conceptual de cómo son las extensiones de mensajería en el Teams cliente." border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a><span data-ttu-id="49286-127">Extensiones de reunión</span><span class="sxs-lookup"><span data-stu-id="49286-127">Meeting extensions</span></span>

:::row:::

   :::column span="1":::

<span data-ttu-id="49286-128">**Crear aplicaciones para reuniones:** hay algunas opciones para incorporar la aplicación a la [experiencia de Teams de llamadas.](apps-in-teams-meetings/design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="49286-128">**Create apps for meetings**: There are a few options for [incorporating your app into the Teams calling experience](apps-in-teams-meetings/design/designing-apps-in-meetings.md).</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="Representación conceptual de cómo son las extensiones de reunión en el Teams cliente." border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a><span data-ttu-id="49286-130">Webhooks y conectores</span><span class="sxs-lookup"><span data-stu-id="49286-130">Webhooks and connectors</span></span>

:::row:::

   :::column span="":::

<span data-ttu-id="49286-131">**Comunicarse con aplicaciones externas:** [los webhooks entrantes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar automáticamente notificaciones desde otra aplicación a un canal Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="49286-131">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="49286-132">Con [webhooks salientes,](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envía un mensaje al servicio web con un @mention.</span><span class="sxs-lookup"><span data-stu-id="49286-132">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Representación conceptual de cómo son los conectores en el Teams cliente." border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="49286-134">Microsoft Graph para Teams</span><span class="sxs-lookup"><span data-stu-id="49286-134">Microsoft Graph for Teams</span></span>

:::row:::

   :::column span="":::

<span data-ttu-id="49286-135">**Usar Teams:** la API de [Microsoft Graph](/graph/teams-concept-overview) para Teams proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar las características de la aplicación (como notificaciones enriquecciones).</span><span class="sxs-lookup"><span data-stu-id="49286-135">**Utilize Teams data**: The [Microsoft Graph API for Teams](/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app (such as rich notifications).</span></span>

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="49286-137">Iniciar la creación</span><span class="sxs-lookup"><span data-stu-id="49286-137">Start building</span></span>

<span data-ttu-id="49286-138">Familiarícese rápidamente con la creación de Teams mediante la configuración del entorno y la creación de una aplicación sencilla.</span><span class="sxs-lookup"><span data-stu-id="49286-138">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49286-139">Compilar una aplicación por primera vez</span><span class="sxs-lookup"><span data-stu-id="49286-139">Build your first app</span></span>](get-started/prerequisites.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="49286-140">Integración con Teams</span><span class="sxs-lookup"><span data-stu-id="49286-140">Integrate with Teams</span></span>

<span data-ttu-id="49286-141">Combina las características que a los usuarios les gusta acerca de una aplicación web, un servicio o un sistema existentes con las características de colaboración de Teams.</span><span class="sxs-lookup"><span data-stu-id="49286-141">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49286-142">Integrar una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="49286-142">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="49286-143">Un poco de código va mucho más allá</span><span class="sxs-lookup"><span data-stu-id="49286-143">A little code goes a long way</span></span>

<span data-ttu-id="49286-144">No es necesario ser un programador experto para crear una aplicación Teams web.</span><span class="sxs-lookup"><span data-stu-id="49286-144">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="49286-145">Pruebe una de varias soluciones de código bajo.</span><span class="sxs-lookup"><span data-stu-id="49286-145">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49286-146">Crear una aplicación de código bajo</span><span class="sxs-lookup"><span data-stu-id="49286-146">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="49286-147">Obtener ideas para tu aplicación</span><span class="sxs-lookup"><span data-stu-id="49286-147">Get ideas for your app</span></span>

<span data-ttu-id="49286-148">¿Está buscando inspiración para el desarrollo de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="49286-148">Looking for app development inspiration?</span></span> <span data-ttu-id="49286-149">Explore nuestra lista de escenarios reales y soluciones del sector con simulacros de concepto de alta fidelidad para comprender las distintas formas en que Teams aplicaciones pueden ayudar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="49286-149">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49286-150">Ver escenarios de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="49286-150">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="49286-151">Vea también</span><span class="sxs-lookup"><span data-stu-id="49286-151">See also</span></span>

* [<span data-ttu-id="49286-152">Agregar un botón Compartir a Teams a su sitio web</span><span class="sxs-lookup"><span data-stu-id="49286-152">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="49286-153">Diseñar la aplicación Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="49286-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="49286-154">Microsoft Teams SDK de cliente de JavaScript</span><span class="sxs-lookup"><span data-stu-id="49286-154">Microsoft Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="49286-155">Sdk de Bot Framework para [JavaScript](https://github.com/Microsoft/botbuilder-js) y [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="49286-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="49286-156">Distribuir la aplicación Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="49286-156">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
