---
title: Plataforma de desarrolladores de Microsoft Teams
author: clearab
description: Información general sobre cómo los desarrolladores pueden ampliar y personalizar las características de Microsoft Teams con la plataforma de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 73cbd4f68d8878872147bd412972495de1b5de6e
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964574"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="d53a7-103">Creación para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d53a7-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="d53a7-104">Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza a los que los usuarios recopilan, aprenden y funcionan cada vez más.</span><span class="sxs-lookup"><span data-stu-id="d53a7-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="d53a7-105">Las aplicaciones son cómo extender Teams para ajustarse a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="d53a7-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="d53a7-106">Cree algo nuevo para Teams o integre una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="d53a7-106">Create something brand new for Teams or integrate an existing app.</span></span>

## <a name="what-are-teams-apps"></a><span data-ttu-id="d53a7-107">¿Qué son las aplicaciones de Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="d53a7-107">What are Teams apps?</span></span>

<span data-ttu-id="d53a7-108">Las personas descubren y usan las aplicaciones de Microsoft Teams a través de un conjunto de [capacidades](capabilities-overview.md)de plataforma.</span><span class="sxs-lookup"><span data-stu-id="d53a7-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="d53a7-109">Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (Ver registros de pacientes).</span><span class="sxs-lookup"><span data-stu-id="d53a7-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="d53a7-110">Al planear la aplicación, recuerde que Teams es un centro de colaboración.</span><span class="sxs-lookup"><span data-stu-id="d53a7-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="d53a7-111">Las mejores aplicaciones de Team ayudan a los usuarios a expresarse y a trabajar mejor juntos.</span><span class="sxs-lookup"><span data-stu-id="d53a7-111">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="d53a7-112">Pestañas</span><span class="sxs-lookup"><span data-stu-id="d53a7-112">Tabs</span></span>

<span data-ttu-id="d53a7-113">**Obtenga información más fácilmente**: a veces solo necesita que las cosas sean más fáciles de encontrar.</span><span class="sxs-lookup"><span data-stu-id="d53a7-113">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="d53a7-114">Mostrar una página web importante en una [pestaña](../tabs/what-are-tabs.md), que proporciona una experiencia web de pantalla completa para contenido estático y dinámico en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d53a7-114">Display an important webpage in a [tab](../tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="doc-links/images/overview-tabs.png" alt-text="Representación conceptual de las fichas que se ven en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="d53a7-116">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d53a7-116">Messaging extensions</span></span>

<span data-ttu-id="d53a7-117">**Simplificar la tarea**en varias tareas: con [las extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md), puede compartir rápidamente información externa en una conversación.</span><span class="sxs-lookup"><span data-stu-id="d53a7-117">**Make it easier to multitask**: With [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="d53a7-118">También puede actuar en un mensaje, como la creación de un vale de ayuda basado en el contenido de una publicación de canal.</span><span class="sxs-lookup"><span data-stu-id="d53a7-118">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="doc-links/images/overview-messaging.png" alt-text="Representación conceptual de las extensiones de mensajería que tienen el mismo aspecto en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="d53a7-120">Bots</span><span class="sxs-lookup"><span data-stu-id="d53a7-120">Bots</span></span>

<span data-ttu-id="d53a7-121">**Convertir las palabras en acciones**: las conversaciones suelen tener como resultado la necesidad de hacer algo (generar un pedido, revisar el código, comprobar el estado de los tíquets, etc.).</span><span class="sxs-lookup"><span data-stu-id="d53a7-121">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="d53a7-122">Un [Bot](../bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="d53a7-122">A [bot](../bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="doc-links/images/overview-bots.png" alt-text="Representación conceptual de qué bots se parecen en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="d53a7-124">Webhooks</span><span class="sxs-lookup"><span data-stu-id="d53a7-124">Webhooks</span></span>

<span data-ttu-id="d53a7-125">**Comunicarse con aplicaciones externas**: los [webhooks entrantes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar notificaciones de forma automática desde otra aplicación a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="d53a7-125">**Communicate with external apps**: [Incoming webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="d53a7-126">Con los [webhooks salientes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), mensaje el servicio Web con un @mention.</span><span class="sxs-lookup"><span data-stu-id="d53a7-126">With [outgoing webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="doc-links/images/overview-connectors.png" alt-text="Representación conceptual de los conectores que se asemejan en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="d53a7-128">Microsoft Graph para Teams</span><span class="sxs-lookup"><span data-stu-id="d53a7-128">Microsoft Graph for Teams</span></span>

<span data-ttu-id="d53a7-129">**Usar datos de Teams**: la [API de REST de Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar características para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d53a7-129">**Utilize Teams data**: The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="doc-links/images/overview-graph.png" alt-text="Representación conceptual de la API de REST de Microsoft Graph para Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="d53a7-131">Introducción</span><span class="sxs-lookup"><span data-stu-id="d53a7-131">Get started</span></span>

<span data-ttu-id="d53a7-132">Obtenga acceso directamente con nuestros primeros tutoriales de la aplicación, descubra cómo integrar e importar aplicaciones existentes o tómese su tiempo para obtener información sobre el ciclo de vida de desarrollo de aplicaciones de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d53a7-132">Jump right in with our first app tutorials, find out how to integrate and import existing apps, or take your time to learn about the Teams app development lifecycle.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="d53a7-133">Empezar a crear</span><span class="sxs-lookup"><span data-stu-id="d53a7-133">Start building</span></span>

   <span data-ttu-id="d53a7-134">Familiarícese rápidamente con la creación de Teams creando una aplicación sencilla y agregando algunas funcionalidades que se usan con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="d53a7-134">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="d53a7-135">Compilar la primera aplicación ahora</span><span class="sxs-lookup"><span data-stu-id="d53a7-135">Build your first app now</span></span>](build-your-first-app/building-real-world-app.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="d53a7-136">Integración con Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d53a7-136">Integrate with Teams</span></span>

   <span data-ttu-id="d53a7-137">Fusione las características que los usuarios adoran de una aplicación Web, servicio o sistema existente con las características de colaboración de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d53a7-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="d53a7-138">Integrar una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="d53a7-138">Integrate an existing app</span></span>](migrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="d53a7-139">Un pequeño código va de un modo largo</span><span class="sxs-lookup"><span data-stu-id="d53a7-139">A little code goes a long way</span></span>

   <span data-ttu-id="d53a7-140">No es necesario ser un programador experto para crear una aplicación de Teams fantástica.</span><span class="sxs-lookup"><span data-stu-id="d53a7-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="d53a7-141">Pruebe con una de las soluciones de bajo código.</span><span class="sxs-lookup"><span data-stu-id="d53a7-141">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="d53a7-142">Crear una aplicación de código reducido</span><span class="sxs-lookup"><span data-stu-id="d53a7-142">Create a low-code app</span></span>](low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="trust-the-process"></a><span data-ttu-id="d53a7-143">Confiar en el proceso</span><span class="sxs-lookup"><span data-stu-id="d53a7-143">Trust the process</span></span>

   <span data-ttu-id="d53a7-144">Obtenga información sobre todo el proceso de desarrollo de la plataforma de Microsoft Teams para planear, diseñar, crear y publicar una aplicación para su organización o para cualquier persona de manera eficaz.</span><span class="sxs-lookup"><span data-stu-id="d53a7-144">Learn the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="d53a7-145">Empezar a planear la aplicación</span><span class="sxs-lookup"><span data-stu-id="d53a7-145">Start planning your app</span></span>](../concepts/extensibility-points.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="d53a7-146">Recursos</span><span class="sxs-lookup"><span data-stu-id="d53a7-146">Resources</span></span>

* [<span data-ttu-id="d53a7-147">Agregar un recurso compartido a Microsoft Teams en el sitio web</span><span class="sxs-lookup"><span data-stu-id="d53a7-147">Add a Share to Teams button to your website</span></span>](../concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="d53a7-148">Sistema de diseño de Fluent</span><span class="sxs-lookup"><span data-stu-id="d53a7-148">Fluent Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="d53a7-149">SDK de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d53a7-149">Microsoft Teams JavaScript SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="d53a7-150">[Bot Framework SDK para JavaScript](https://github.com/Microsoft/botbuilder-js) y [Bot Framework SDK para .net](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="d53a7-150">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="d53a7-151">Publicar la aplicación en una organización o AppSource</span><span class="sxs-lookup"><span data-stu-id="d53a7-151">Publish your app to an organization or AppSource</span></span>](../concepts/deploy-and-publish/overview.md)
