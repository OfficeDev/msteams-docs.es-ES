---
title: Creación de aplicaciones para la plataforma de Microsoft Teams
author: heath-hamilton
description: Información general sobre cómo los desarrolladores pueden ampliar y personalizar las características de Microsoft Teams con aplicaciones personalizadas.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: c430add71e7c23a44a552270c5e3c1bacbe650e4
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209816"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="833e0-103">Crear aplicaciones para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="833e0-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="833e0-104">Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza a los que los usuarios recopilan, aprenden y funcionan cada vez más.</span><span class="sxs-lookup"><span data-stu-id="833e0-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="833e0-105">Las aplicaciones son cómo extender Teams para ajustarse a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="833e0-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="833e0-106">Cree algo nuevo para Teams o integre una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="833e0-106">Create something brand new for Teams or integrate an existing app.</span></span>

## <a name="what-are-teams-apps"></a><span data-ttu-id="833e0-107">¿Qué son las aplicaciones de Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="833e0-107">What are Teams apps?</span></span>

<span data-ttu-id="833e0-108">Las aplicaciones de Microsoft Teams son una combinación de [capacidades](concepts/capabilities-overview.md) y [puntos de entrada](concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="833e0-108">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="833e0-109">Por ejemplo, los usuarios pueden chatear con el *Bot* de la aplicación (funcionalidad) en un *canal* (punto de entrada).</span><span class="sxs-lookup"><span data-stu-id="833e0-109">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="833e0-110">Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (administrar registros de pacientes).</span><span class="sxs-lookup"><span data-stu-id="833e0-110">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="833e0-111">Al planear la aplicación, recuerde que Teams es un centro de colaboración.</span><span class="sxs-lookup"><span data-stu-id="833e0-111">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="833e0-112">Las mejores aplicaciones de Team ayudan a los usuarios a expresarse y a trabajar mejor juntos.</span><span class="sxs-lookup"><span data-stu-id="833e0-112">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="833e0-113">Pestañas</span><span class="sxs-lookup"><span data-stu-id="833e0-113">Tabs</span></span>

<span data-ttu-id="833e0-114">**Obtenga información más fácilmente**: a veces solo necesita que las cosas sean más fáciles de encontrar.</span><span class="sxs-lookup"><span data-stu-id="833e0-114">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="833e0-115">Mostrar una página web importante en una [pestaña](tabs/what-are-tabs.md), que proporciona una experiencia web de pantalla completa para contenido estático y dinámico en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="833e0-115">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Representación conceptual de las fichas que se ven en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="833e0-117">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="833e0-117">Messaging extensions</span></span>

<span data-ttu-id="833e0-118">**Simplificar la tarea**en varias tareas: con [las extensiones de mensajería](messaging-extensions/what-are-messaging-extensions.md), puede compartir rápidamente información externa en una conversación.</span><span class="sxs-lookup"><span data-stu-id="833e0-118">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="833e0-119">También puede actuar en un mensaje, como la creación de un vale de ayuda basado en el contenido de una publicación de canal.</span><span class="sxs-lookup"><span data-stu-id="833e0-119">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Representación conceptual de las extensiones de mensajería que tienen el mismo aspecto en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="833e0-121">Bots</span><span class="sxs-lookup"><span data-stu-id="833e0-121">Bots</span></span>

<span data-ttu-id="833e0-122">**Convertir las palabras en acciones**: las conversaciones suelen tener como resultado la necesidad de hacer algo (generar un pedido, revisar el código, comprobar el estado de los tíquets, etc.).</span><span class="sxs-lookup"><span data-stu-id="833e0-122">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="833e0-123">Un [Bot](bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="833e0-123">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Representación conceptual de qué bots se parecen en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="833e0-125">Webhooks</span><span class="sxs-lookup"><span data-stu-id="833e0-125">Webhooks</span></span>

<span data-ttu-id="833e0-126">**Comunicarse con aplicaciones externas**: los [webhooks entrantes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar notificaciones de forma automática desde otra aplicación a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="833e0-126">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="833e0-127">Con los [webhooks salientes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), mensaje el servicio Web con un @mention.</span><span class="sxs-lookup"><span data-stu-id="833e0-127">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Representación conceptual de los conectores que se asemejan en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="833e0-129">Microsoft Graph para Teams</span><span class="sxs-lookup"><span data-stu-id="833e0-129">Microsoft Graph for Teams</span></span>

<span data-ttu-id="833e0-130">**Usar datos de Teams**: la [API de Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar características para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="833e0-130">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="833e0-132">Introducción</span><span class="sxs-lookup"><span data-stu-id="833e0-132">Get started</span></span>

<span data-ttu-id="833e0-133">Vaya directamente con nuestros tutoriales de primera aplicación o descubra cómo integrar e importar aplicaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="833e0-133">Jump right in with our first app tutorials or find out how to integrate and import existing apps.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="833e0-134">Empezar a crear</span><span class="sxs-lookup"><span data-stu-id="833e0-134">Start building</span></span>

   <span data-ttu-id="833e0-135">Familiarícese rápidamente con la creación de Teams creando una aplicación sencilla y agregando algunas funcionalidades que se usan con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="833e0-135">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="833e0-136">Compilar la primera aplicación ahora</span><span class="sxs-lookup"><span data-stu-id="833e0-136">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="833e0-137">Integración con Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="833e0-137">Integrate with Teams</span></span>

   <span data-ttu-id="833e0-138">Fusione las características que los usuarios adoran de una aplicación Web, servicio o sistema existente con las características de colaboración de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="833e0-138">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="833e0-139">Integrar una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="833e0-139">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="833e0-140">Un pequeño código va de un modo largo</span><span class="sxs-lookup"><span data-stu-id="833e0-140">A little code goes a long way</span></span>

   <span data-ttu-id="833e0-141">No es necesario ser un programador experto para crear una aplicación de Teams fantástica.</span><span class="sxs-lookup"><span data-stu-id="833e0-141">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="833e0-142">Pruebe con una de las soluciones de bajo código.</span><span class="sxs-lookup"><span data-stu-id="833e0-142">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="833e0-143">Crear una aplicación de código reducido</span><span class="sxs-lookup"><span data-stu-id="833e0-143">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a><span data-ttu-id="833e0-144">Recursos</span><span class="sxs-lookup"><span data-stu-id="833e0-144">Resources</span></span>

* [<span data-ttu-id="833e0-145">Agregar un recurso compartido a Microsoft Teams en el sitio web</span><span class="sxs-lookup"><span data-stu-id="833e0-145">Add a Share to Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="833e0-146">Sistema de diseño de Fluent</span><span class="sxs-lookup"><span data-stu-id="833e0-146">Fluent Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="833e0-147">SDK de cliente de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="833e0-147">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="833e0-148">[Bot Framework SDK para JavaScript](https://github.com/Microsoft/botbuilder-js) y [Bot Framework SDK para .net](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="833e0-148">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="833e0-149">Publicar la aplicación en una organización o AppSource</span><span class="sxs-lookup"><span data-stu-id="833e0-149">Publish your app to an organization or AppSource</span></span>](concepts/deploy-and-publish/overview.md)
