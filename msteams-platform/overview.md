---
title: Crear aplicaciones para la plataforma de Microsoft Teams
author: heath-hamilton
description: Obtenga información general sobre cómo los desarrolladores pueden ampliar las características de Microsoft Teams con aplicaciones personalizadas.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e40d2b0d8b0d12e6275b97f79d103310d22f9720
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475931"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="d32c8-103">Desarrollar aplicaciones para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d32c8-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="d32c8-104">Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza a los que cada vez más personas recopilan, aprenden y trabajan.</span><span class="sxs-lookup"><span data-stu-id="d32c8-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="d32c8-105">Las aplicaciones son la forma en que amplías Teams para que se ajusten a tus necesidades.</span><span class="sxs-lookup"><span data-stu-id="d32c8-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="d32c8-106">Crea algo nuevo para Teams o integra una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="d32c8-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d32c8-107">Comenzar aquí</span><span class="sxs-lookup"><span data-stu-id="d32c8-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="d32c8-108">¿Qué son las aplicaciones de Teams?</span><span class="sxs-lookup"><span data-stu-id="d32c8-108">What are Teams apps?</span></span>

<span data-ttu-id="d32c8-109">Las aplicaciones de Teams son una combinación de [funcionalidades](concepts/capabilities-overview.md) [y puntos de entrada.](concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="d32c8-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="d32c8-110">Por ejemplo, los usuarios pueden chatear con el *bot* (funcionalidad) de la aplicación en un *canal* (punto de entrada).</span><span class="sxs-lookup"><span data-stu-id="d32c8-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="d32c8-111">Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (administrar registros de pacientes).</span><span class="sxs-lookup"><span data-stu-id="d32c8-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="d32c8-112">Al planear la aplicación, recuerda que Teams es un centro de colaboración.</span><span class="sxs-lookup"><span data-stu-id="d32c8-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="d32c8-113">Las mejores aplicaciones de Teams ayudan a las personas a expresarse y a trabajar mejor juntos.</span><span class="sxs-lookup"><span data-stu-id="d32c8-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="d32c8-114">Pestañas</span><span class="sxs-lookup"><span data-stu-id="d32c8-114">Tabs</span></span>

<span data-ttu-id="d32c8-115">**Obtenga información más cómodamente:** a veces solo necesita facilitar la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="d32c8-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="d32c8-116">Muestra una página web importante en una [pestaña,](tabs/what-are-tabs.md)que proporciona una experiencia web a pantalla completa para contenido estático y dinámico en Teams.</span><span class="sxs-lookup"><span data-stu-id="d32c8-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Representación conceptual de cómo son las pestañas en el cliente de Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="d32c8-118">Bots</span><span class="sxs-lookup"><span data-stu-id="d32c8-118">Bots</span></span>

<span data-ttu-id="d32c8-119">**Convertir palabras en acciones:** las conversaciones a menudo resultan en la necesidad de hacer algo (generar un pedido, revisar mi código, comprobar el estado del vale, etc.).</span><span class="sxs-lookup"><span data-stu-id="d32c8-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="d32c8-120">Un [bot](bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="d32c8-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Representación conceptual de cómo son los bots en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="d32c8-122">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d32c8-122">Messaging extensions</span></span>

<span data-ttu-id="d32c8-123">**Facilita la multitarea:** con extensiones [de mensajería,](messaging-extensions/what-are-messaging-extensions.md)puedes compartir rápidamente información externa en una conversación.</span><span class="sxs-lookup"><span data-stu-id="d32c8-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="d32c8-124">También puede actuar en un mensaje, como crear un vale de ayuda basado en el contenido de una publicación de canal.</span><span class="sxs-lookup"><span data-stu-id="d32c8-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Representación conceptual de cómo son las extensiones de mensajería en el cliente de Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="d32c8-126">Webhooks</span><span class="sxs-lookup"><span data-stu-id="d32c8-126">Webhooks</span></span>

<span data-ttu-id="d32c8-127">**Comunicarse con aplicaciones externas:** [los webhooks entrantes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar automáticamente notificaciones desde otra aplicación a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="d32c8-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="d32c8-128">Con [webhooks salientes,](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envía un mensaje al servicio web con un @mention.</span><span class="sxs-lookup"><span data-stu-id="d32c8-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Representación conceptual de cómo son los conectores en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="d32c8-130">Microsoft Graph para Teams</span><span class="sxs-lookup"><span data-stu-id="d32c8-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="d32c8-131">**Usar datos de Teams:** la API de [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview) para Teams proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar las características de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d32c8-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a><span data-ttu-id="d32c8-133">Crear soluciones para aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d32c8-133">Build solutions for Microsoft Teams apps</span></span>
 
<span data-ttu-id="d32c8-134">Microsoft ofrece un libro de aspecto extensibilidad, una biblioteca de escenarios para aplicaciones de Teams organizadas por el sector.</span><span class="sxs-lookup"><span data-stu-id="d32c8-134">Microsoft offers an extensibility look book, a scenario library for Teams apps organized by industry.</span></span> <span data-ttu-id="d32c8-135">Este libro te ayuda a crear aplicaciones en la plataforma de Teams y a comprender diferentes escenarios posibles mediante diversas funcionalidades de plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="d32c8-135">This book helps you build apps on the Teams platform and understand different possible scenarios using various Teams platform capabilities.</span></span> <span data-ttu-id="d32c8-136">Los escenarios del libro de apariencias comienzan con un problema de negocio, las personas implicadas junto con sus desafíos y terminan con una solución de aplicación de Teams que aborda las necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="d32c8-136">The look book scenarios start with a business problem, the personas involved along with their challenges, and end with a Teams app solution addressing the business needs.</span></span>

<span data-ttu-id="d32c8-137">Cada escenario de esta biblioteca va acompañado de un conjunto de simulacros de concepto de diseño de alta fidelidad, que pueden servir de inspiración para diseñar tus aplicaciones y mejorar la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="d32c8-137">Each scenario in this library is accompanied by a set of high-fidelity design concept mocks, which can serve as an inspiration for designing your apps and enhancing user experience.</span></span> <span data-ttu-id="d32c8-138">Además, el libro de apariencias destaca los procedimientos recomendados de diseño y arquitectura seguidos en la creación de cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="d32c8-138">In addition, the look book highlights the design and architecture best practices followed in building each app.</span></span> <span data-ttu-id="d32c8-139">Para obtener más información, vea el libro de aspecto extensibilidad.</span><span class="sxs-lookup"><span data-stu-id="d32c8-139">For more information, see the extensibility look book.</span></span> <span data-ttu-id="d32c8-140">Para obtener más información, vea [extensibilidad look book](https://adoption.microsoft.com/extensibility-look-book/scenarios/).</span><span class="sxs-lookup"><span data-stu-id="d32c8-140">For more information, see [extensibility look book](https://adoption.microsoft.com/extensibility-look-book/scenarios/).</span></span> 

## <a name="start-building"></a><span data-ttu-id="d32c8-141">Iniciar la creación</span><span class="sxs-lookup"><span data-stu-id="d32c8-141">Start building</span></span>

<span data-ttu-id="d32c8-142">Familiarícese rápidamente con la creación de Teams mediante la creación de una aplicación sencilla y la adición de algunas funcionalidades de uso común.</span><span class="sxs-lookup"><span data-stu-id="d32c8-142">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d32c8-143">Crear la primera aplicación ahora</span><span class="sxs-lookup"><span data-stu-id="d32c8-143">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="d32c8-144">Integración con Teams</span><span class="sxs-lookup"><span data-stu-id="d32c8-144">Integrate with Teams</span></span>

<span data-ttu-id="d32c8-145">Combina las características que a los usuarios les gusta acerca de una aplicación web, un servicio o un sistema existentes con las características de colaboración de Teams.</span><span class="sxs-lookup"><span data-stu-id="d32c8-145">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d32c8-146">Integrar una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="d32c8-146">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="d32c8-147">Un poco de código va mucho más allá</span><span class="sxs-lookup"><span data-stu-id="d32c8-147">A little code goes a long way</span></span>

<span data-ttu-id="d32c8-148">No es necesario ser un programador experto para crear una gran aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="d32c8-148">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="d32c8-149">Pruebe una de varias soluciones de código bajo.</span><span class="sxs-lookup"><span data-stu-id="d32c8-149">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d32c8-150">Crear una aplicación de código bajo</span><span class="sxs-lookup"><span data-stu-id="d32c8-150">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="d32c8-151">Recursos</span><span class="sxs-lookup"><span data-stu-id="d32c8-151">Resources</span></span>

* [<span data-ttu-id="d32c8-152">Agregar un botón Compartir a Teams a su sitio web</span><span class="sxs-lookup"><span data-stu-id="d32c8-152">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="d32c8-153">Diseñar la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="d32c8-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="d32c8-154">SDK de cliente de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d32c8-154">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="d32c8-155">Sdk de Bot Framework para [JavaScript](https://github.com/Microsoft/botbuilder-js) y [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="d32c8-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="d32c8-156">Publicar la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="d32c8-156">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
