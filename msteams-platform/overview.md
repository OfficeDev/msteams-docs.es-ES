---
title: Creación de aplicaciones para la plataforma de Microsoft Teams
author: heath-hamilton
description: Información general sobre cómo los desarrolladores pueden ampliar y personalizar las características de Microsoft Teams con aplicaciones personalizadas.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6f5f3454885320669ef42383529d39fcfcfdfee8
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604790"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="35366-103">Desarrollar aplicaciones para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="35366-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="35366-104">Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza a los que los usuarios recopilan, aprenden y funcionan cada vez más.</span><span class="sxs-lookup"><span data-stu-id="35366-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="35366-105">Las aplicaciones son cómo extender Teams para ajustarse a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="35366-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="35366-106">Cree algo nuevo para Teams o integre una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="35366-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35366-107">Comenzar aquí</span><span class="sxs-lookup"><span data-stu-id="35366-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="35366-108">¿Qué son las aplicaciones de Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="35366-108">What are Teams apps?</span></span>

<span data-ttu-id="35366-109">Las aplicaciones de Microsoft Teams son una combinación de [capacidades](concepts/capabilities-overview.md) y [puntos de entrada](concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="35366-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="35366-110">Por ejemplo, los usuarios pueden chatear con el *Bot* de la aplicación (funcionalidad) en un *canal* (punto de entrada).</span><span class="sxs-lookup"><span data-stu-id="35366-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="35366-111">Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (administrar registros de pacientes).</span><span class="sxs-lookup"><span data-stu-id="35366-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="35366-112">Al planear la aplicación, recuerde que Teams es un centro de colaboración.</span><span class="sxs-lookup"><span data-stu-id="35366-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="35366-113">Las mejores aplicaciones de Team ayudan a los usuarios a expresarse y a trabajar mejor juntos.</span><span class="sxs-lookup"><span data-stu-id="35366-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="35366-114">Pestañas</span><span class="sxs-lookup"><span data-stu-id="35366-114">Tabs</span></span>

<span data-ttu-id="35366-115">**Obtenga información más fácilmente**: a veces solo necesita que las cosas sean más fáciles de encontrar.</span><span class="sxs-lookup"><span data-stu-id="35366-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="35366-116">Mostrar una página web importante en una [pestaña](tabs/what-are-tabs.md), que proporciona una experiencia web de pantalla completa para contenido estático y dinámico en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="35366-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Representación conceptual de las fichas que se ven en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="35366-118">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="35366-118">Messaging extensions</span></span>

<span data-ttu-id="35366-119">**Simplificar la tarea** en varias tareas: con [las extensiones de mensajería](messaging-extensions/what-are-messaging-extensions.md), puede compartir rápidamente información externa en una conversación.</span><span class="sxs-lookup"><span data-stu-id="35366-119">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="35366-120">También puede actuar en un mensaje, como la creación de un vale de ayuda basado en el contenido de una publicación de canal.</span><span class="sxs-lookup"><span data-stu-id="35366-120">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Representación conceptual de las extensiones de mensajería que tienen el mismo aspecto en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="35366-122">Bots</span><span class="sxs-lookup"><span data-stu-id="35366-122">Bots</span></span>

<span data-ttu-id="35366-123">**Convertir las palabras en acciones**: las conversaciones suelen tener como resultado la necesidad de hacer algo (generar un pedido, revisar el código, comprobar el estado de los tíquets, etc.).</span><span class="sxs-lookup"><span data-stu-id="35366-123">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="35366-124">Un [Bot](bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="35366-124">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Representación conceptual de qué bots se parecen en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="35366-126">Webhooks</span><span class="sxs-lookup"><span data-stu-id="35366-126">Webhooks</span></span>

<span data-ttu-id="35366-127">**Comunicarse con aplicaciones externas**: los [webhooks entrantes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar notificaciones de forma automática desde otra aplicación a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="35366-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="35366-128">Con los [webhooks salientes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), mensaje el servicio Web con un @mention.</span><span class="sxs-lookup"><span data-stu-id="35366-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Representación conceptual de los conectores que se asemejan en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="35366-130">Microsoft Graph para Teams</span><span class="sxs-lookup"><span data-stu-id="35366-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="35366-131">**Usar datos de Teams**: la [API de Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar características para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="35366-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="35366-133">Introducción</span><span class="sxs-lookup"><span data-stu-id="35366-133">Get started</span></span>

<span data-ttu-id="35366-134">Vaya directamente con nuestros tutoriales de primera aplicación o descubra cómo integrar e importar aplicaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="35366-134">Jump right in with our first app tutorials or find out how to integrate and import existing apps.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="35366-135">Empezar a crear</span><span class="sxs-lookup"><span data-stu-id="35366-135">Start building</span></span>

   <span data-ttu-id="35366-136">Familiarícese rápidamente con la creación de Teams creando una aplicación sencilla y agregando algunas funcionalidades que se usan con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="35366-136">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="35366-137">Compilar la primera aplicación ahora</span><span class="sxs-lookup"><span data-stu-id="35366-137">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="35366-138">Integración con Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="35366-138">Integrate with Teams</span></span>

   <span data-ttu-id="35366-139">Fusione las características que los usuarios adoran de una aplicación Web, servicio o sistema existente con las características de colaboración de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="35366-139">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="35366-140">Integrar una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="35366-140">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="35366-141">Un pequeño código va de un modo largo</span><span class="sxs-lookup"><span data-stu-id="35366-141">A little code goes a long way</span></span>

   <span data-ttu-id="35366-142">No es necesario ser un programador experto para crear una aplicación de Teams fantástica.</span><span class="sxs-lookup"><span data-stu-id="35366-142">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="35366-143">Pruebe con una de las soluciones de bajo código.</span><span class="sxs-lookup"><span data-stu-id="35366-143">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="35366-144">Crear una aplicación de código reducido</span><span class="sxs-lookup"><span data-stu-id="35366-144">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a><span data-ttu-id="35366-145">Recursos</span><span class="sxs-lookup"><span data-stu-id="35366-145">Resources</span></span>

* [<span data-ttu-id="35366-146">Agregar un recurso compartido a Microsoft Teams en el sitio web</span><span class="sxs-lookup"><span data-stu-id="35366-146">Add a Share to Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* <span data-ttu-id="35366-147"><a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Interfaz de usuario Fluent</a></span><span class="sxs-lookup"><span data-stu-id="35366-147"><a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a></span></span>
* [<span data-ttu-id="35366-148">SDK de cliente de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="35366-148">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="35366-149">[Bot Framework SDK para JavaScript](https://github.com/Microsoft/botbuilder-js) y [Bot Framework SDK para .net](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="35366-149">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="35366-150">Publicar la aplicación en una organización o AppSource</span><span class="sxs-lookup"><span data-stu-id="35366-150">Publish your app to an organization or AppSource</span></span>](concepts/deploy-and-publish/overview.md)
