---
title: Crear aplicaciones para la plataforma de Microsoft Teams
author: heath-hamilton
description: Obtenga información general sobre cómo los desarrolladores pueden ampliar las características de Microsoft Teams con aplicaciones personalizadas.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 45be2dd7d0e421ac331cfc02703f0b81eab3dfe5
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797774"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="bd708-103">Desarrollar aplicaciones para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bd708-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="bd708-104">Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza para que los usuarios recopile, aprendan y trabajen cada vez más.</span><span class="sxs-lookup"><span data-stu-id="bd708-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="bd708-105">Las aplicaciones son la forma en que amplía Teams para adaptarse a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="bd708-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="bd708-106">Cree algo nuevo para Teams o integre una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="bd708-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bd708-107">Comenzar aquí</span><span class="sxs-lookup"><span data-stu-id="bd708-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="bd708-108">¿Qué son las aplicaciones de Teams?</span><span class="sxs-lookup"><span data-stu-id="bd708-108">What are Teams apps?</span></span>

<span data-ttu-id="bd708-109">Las aplicaciones de Teams son una combinación de [funcionalidades](concepts/capabilities-overview.md) y [puntos de entrada.](concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="bd708-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="bd708-110">Por ejemplo, los usuarios pueden chatear con el bot (funcionalidad) de la *aplicación* en un *canal* (punto de entrada).</span><span class="sxs-lookup"><span data-stu-id="bd708-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="bd708-111">Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (administrar registros de pacientes).</span><span class="sxs-lookup"><span data-stu-id="bd708-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="bd708-112">Al planear la aplicación, recuerde que Teams es un centro de colaboración.</span><span class="sxs-lookup"><span data-stu-id="bd708-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="bd708-113">Las mejores aplicaciones de Teams ayudan a los usuarios a expresarse y a trabajar mejor juntos.</span><span class="sxs-lookup"><span data-stu-id="bd708-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="bd708-114">Pestañas</span><span class="sxs-lookup"><span data-stu-id="bd708-114">Tabs</span></span>

<span data-ttu-id="bd708-115">**Obtenga información de forma más cómoda:** a veces solo necesita facilitar la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="bd708-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="bd708-116">Mostrar una página web importante en una [pestaña,](tabs/what-are-tabs.md)que proporciona una experiencia web de pantalla completa para contenido estático y dinámico en Teams.</span><span class="sxs-lookup"><span data-stu-id="bd708-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Representación conceptual del aspecto de las pestañas en el cliente de Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="bd708-118">Bots</span><span class="sxs-lookup"><span data-stu-id="bd708-118">Bots</span></span>

<span data-ttu-id="bd708-119">**Convertir palabras en acciones:** las conversaciones a menudo resultan en la necesidad de hacer algo (generar un pedido, revisar mi código, comprobar el estado del vale, etc.).</span><span class="sxs-lookup"><span data-stu-id="bd708-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="bd708-120">Un [bot](bots/what-are-bots.md) puede iniciar este tipo de flujos de trabajo dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="bd708-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Representación conceptual del aspecto de los bots en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="bd708-122">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="bd708-122">Messaging extensions</span></span>

<span data-ttu-id="bd708-123">**Haga que sea más fácil realizar varias** tareas: con las extensiones de [mensajería,](messaging-extensions/what-are-messaging-extensions.md)puede compartir rápidamente información externa en una conversación.</span><span class="sxs-lookup"><span data-stu-id="bd708-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="bd708-124">También puede actuar en un mensaje, como crear un vale de ayuda basado en el contenido de una publicación de canal.</span><span class="sxs-lookup"><span data-stu-id="bd708-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Representación conceptual del aspecto de las extensiones de mensajería en el cliente de Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="bd708-126">Webhooks</span><span class="sxs-lookup"><span data-stu-id="bd708-126">Webhooks</span></span>

<span data-ttu-id="bd708-127">**Comunicarse con aplicaciones externas:** [los webhooks entrantes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar automáticamente notificaciones desde otra aplicación a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="bd708-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="bd708-128">Con [los webhooks salientes,](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envía un mensaje al servicio web con un @mention.</span><span class="sxs-lookup"><span data-stu-id="bd708-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Representación conceptual del aspecto de los conectores en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="bd708-130">Microsoft Graph para Teams</span><span class="sxs-lookup"><span data-stu-id="bd708-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="bd708-131">**Usar datos de Teams:** la API de [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview) para Teams proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar las características de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd708-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="bd708-133">Empezar a compilar</span><span class="sxs-lookup"><span data-stu-id="bd708-133">Start building</span></span>

   <span data-ttu-id="bd708-134">Familiarícese rápidamente con la creación de Teams mediante la creación de una aplicación sencilla y la adición de algunas funcionalidades que se usan habitualmente.</span><span class="sxs-lookup"><span data-stu-id="bd708-134">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="bd708-135">Crear la primera aplicación ahora</span><span class="sxs-lookup"><span data-stu-id="bd708-135">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="bd708-136">Integrar con Teams</span><span class="sxs-lookup"><span data-stu-id="bd708-136">Integrate with Teams</span></span>

   <span data-ttu-id="bd708-137">Combine las características que les gustan a los usuarios sobre una aplicación web, un servicio o un sistema existentes con las características de colaboración de Teams.</span><span class="sxs-lookup"><span data-stu-id="bd708-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="bd708-138">Integrar una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="bd708-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="bd708-139">Un poco de código va mucho más allá</span><span class="sxs-lookup"><span data-stu-id="bd708-139">A little code goes a long way</span></span>

   <span data-ttu-id="bd708-140">No es necesario ser un programador experto para crear una excelente aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="bd708-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="bd708-141">Pruebe una de varias soluciones de código bajo.</span><span class="sxs-lookup"><span data-stu-id="bd708-141">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="bd708-142">Crear una aplicación de código bajo</span><span class="sxs-lookup"><span data-stu-id="bd708-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="bd708-143">Recursos</span><span class="sxs-lookup"><span data-stu-id="bd708-143">Resources</span></span>

* [<span data-ttu-id="bd708-144">Agregar un botón Compartir a Teams a su sitio web</span><span class="sxs-lookup"><span data-stu-id="bd708-144">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* <span data-ttu-id="bd708-145"><a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Interfaz de usuario Fluent</a></span><span class="sxs-lookup"><span data-stu-id="bd708-145"><a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a></span></span>
* [<span data-ttu-id="bd708-146">SDK de cliente de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bd708-146">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="bd708-147">[SDK de Bot Framework para JavaScript](https://github.com/Microsoft/botbuilder-js) y [SDK de Bot Framework para .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="bd708-147">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="bd708-148">Publicar la aplicación en una organización o AppSource</span><span class="sxs-lookup"><span data-stu-id="bd708-148">Publish your app to an organization or AppSource</span></span>](concepts/deploy-and-publish/overview.md)
