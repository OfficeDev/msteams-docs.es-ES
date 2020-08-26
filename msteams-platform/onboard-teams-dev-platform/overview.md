---
title: Plataforma para desarrolladores de Microsoft Teams
author: clearab
description: Información general sobre cómo los desarrolladores pueden ampliar y personalizar las características de Microsoft Teams con la plataforma de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 4af4d34ffa4581be6e69f6233d3eb356aa6a2a08
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874887"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="1faff-103">Creación para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1faff-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="1faff-104">Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza a los que los usuarios recopilan, aprenden y funcionan cada vez más.</span><span class="sxs-lookup"><span data-stu-id="1faff-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="1faff-105">Las aplicaciones son cómo extender Teams para ajustarse a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="1faff-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="1faff-106">Puede crear elementos nuevos para Microsoft Teams o simplemente integrar características en sus aplicaciones y servicios favoritos.</span><span class="sxs-lookup"><span data-stu-id="1faff-106">You can create something brand new for Teams or simply integrate features in your favorite apps and services.</span></span>

## <a name="what-can-teams-apps-do"></a><span data-ttu-id="1faff-107">¿Qué pueden hacer las aplicaciones de Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="1faff-107">What can Teams apps do?</span></span>

<span data-ttu-id="1faff-108">Las personas descubren y usan las aplicaciones de Microsoft Teams a través de un conjunto de [capacidades](capabilities-overview.md)de plataforma.</span><span class="sxs-lookup"><span data-stu-id="1faff-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="1faff-109">Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (Ver registros de pacientes).</span><span class="sxs-lookup"><span data-stu-id="1faff-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="1faff-110">Al planear la aplicación, recuerde que Teams es un centro de colaboración.</span><span class="sxs-lookup"><span data-stu-id="1faff-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="1faff-111">Las mejores aplicaciones de Team ayudan a los usuarios a expresarse y a trabajar mejor juntos.</span><span class="sxs-lookup"><span data-stu-id="1faff-111">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="get-information-more-conveniently"></a><span data-ttu-id="1faff-112">Obtener información más fácilmente</span><span class="sxs-lookup"><span data-stu-id="1faff-112">Get information more conveniently</span></span>

<span data-ttu-id="1faff-113">A veces solo necesita que las cosas sean más fáciles de encontrar.</span><span class="sxs-lookup"><span data-stu-id="1faff-113">Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="1faff-114">Mostrar una página web importante en una [pestaña](doc-links/what-are-tabs.md), que proporciona una experiencia web de pantalla completa para contenido estático y dinámico en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1faff-114">Display an important webpage in a [tab](doc-links/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

![Representación conceptual de las fichas que se ven en el cliente de Microsoft Teams.](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a><span data-ttu-id="1faff-116">Compartir vínculos sin conmutar contexto</span><span class="sxs-lookup"><span data-stu-id="1faff-116">Share links without switching context</span></span>

<span data-ttu-id="1faff-117">Extraiga la información en una conversación y no deje nunca los equipos.</span><span class="sxs-lookup"><span data-stu-id="1faff-117">Pull information into a conversation and never leave Teams.</span></span> <span data-ttu-id="1faff-118">Por ejemplo, con las [extensiones de mensajería](doc-links/what-are-messaging-extensions.md) puede compartir contenido enriquecido y fácilmente digestible desde un sistema externo mediante el cuadro de redacción del mensaje.</span><span class="sxs-lookup"><span data-stu-id="1faff-118">For example, with [messaging extensions](doc-links/what-are-messaging-extensions.md) you can share rich, easily digestible content from an external system using the message compose box.</span></span>

![Representación conceptual de las extensiones de mensajería que tienen el mismo aspecto en el cliente de Microsoft Teams](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a><span data-ttu-id="1faff-120">Convertir palabras en acciones</span><span class="sxs-lookup"><span data-stu-id="1faff-120">Turn words into actions</span></span>

<span data-ttu-id="1faff-121">Con frecuencia, las conversaciones tienen como resultado la necesidad de hacer algo (crear un pedido, revisar el código, etc.).</span><span class="sxs-lookup"><span data-stu-id="1faff-121">Conversations often result in the need to do something (create an order, review my code, etc.).</span></span> <span data-ttu-id="1faff-122">Un [Bot](doc-links/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="1faff-122">A [bot](doc-links/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

![Representación conceptual de los bots que tienen el mismo aspecto en el cliente de Microsoft Teams](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a><span data-ttu-id="1faff-124">Comunicarse con los servicios y las aplicaciones externas</span><span class="sxs-lookup"><span data-stu-id="1faff-124">Communicate with external apps and services</span></span>

<span data-ttu-id="1faff-125">Los [webhooks entrantes](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar automáticamente alertas desde otra aplicación a un canal o chat de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1faff-125">[Incoming webhooks](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send alerts from another app to a Teams channel or chat.</span></span> <span data-ttu-id="1faff-126">Con los [webhooks salientes](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), puede enviar un mensaje al servicio Web con un @mention.</span><span class="sxs-lookup"><span data-stu-id="1faff-126">With [outgoing webhooks](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), you can send a message to your web service with an @mention.</span></span>

![Representación conceptual de los conectores que se asemejan en el cliente de Microsoft Teams.](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a><span data-ttu-id="1faff-128">Uso de los datos de Teams</span><span class="sxs-lookup"><span data-stu-id="1faff-128">Utilize Teams data</span></span>

<span data-ttu-id="1faff-129">La [API de REST de Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar características para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1faff-129">The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

!["Representación conceptual de la API de REST de Microsoft Graph para Teams](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a><span data-ttu-id="1faff-131">Empezar a crear</span><span class="sxs-lookup"><span data-stu-id="1faff-131">Start building</span></span>

   <span data-ttu-id="1faff-132">Familiarícese rápidamente con la creación de Teams creando una aplicación sencilla y agregando un par de capacidades de uso frecuente.</span><span class="sxs-lookup"><span data-stu-id="1faff-132">Quickly familiarize yourself with building for Teams by creating a simple app and adding a couple commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="1faff-133">Compilar la primera aplicación ahora</span><span class="sxs-lookup"><span data-stu-id="1faff-133">Build your first app now</span></span>](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a><span data-ttu-id="1faff-134">Unir todo</span><span class="sxs-lookup"><span data-stu-id="1faff-134">Bring it all together</span></span>

   <span data-ttu-id="1faff-135">Simplificar los procesos y flujos de trabajo para los usuarios al combinar las aplicaciones Web, servicios y sistemas favoritos de su organización con las características de colaboración de Teams.</span><span class="sxs-lookup"><span data-stu-id="1faff-135">Simplify processes and workflows for users by blending your organization's favorite web apps, services, and systems with Teams collaborative features.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="1faff-136">Integrar una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="1faff-136">Integrate an existing app</span></span>](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a><span data-ttu-id="1faff-137">Confiar en el proceso</span><span class="sxs-lookup"><span data-stu-id="1faff-137">Trust the process</span></span>

   <span data-ttu-id="1faff-138">Comprenda todo el proceso de desarrollo de la plataforma de Teams para planear, diseñar, crear y publicar una aplicación para su organización o cualquier persona de manera eficaz.</span><span class="sxs-lookup"><span data-stu-id="1faff-138">Understand the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="1faff-139">Empezar a planear la aplicación</span><span class="sxs-lookup"><span data-stu-id="1faff-139">Start planning your app</span></span>](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a><span data-ttu-id="1faff-140">Sin código, sin preocupaciones</span><span class="sxs-lookup"><span data-stu-id="1faff-140">No code, no worries</span></span>

   <span data-ttu-id="1faff-141">No es necesario ser programador para crear una aplicación fantástica.</span><span class="sxs-lookup"><span data-stu-id="1faff-141">You don't need to be a programmer to build a great app.</span></span> <span data-ttu-id="1faff-142">Cree una aplicación de Microsoft Teams con poco o ningún código usando la plataforma de energía de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1faff-142">Create a Teams app with little to no code using the Microsoft Power Platform.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="1faff-143">Importar una aplicación de Power Platform</span><span class="sxs-lookup"><span data-stu-id="1faff-143">Import a Power Platform app</span></span>](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a><span data-ttu-id="1faff-144">Recursos</span><span class="sxs-lookup"><span data-stu-id="1faff-144">Resources</span></span>

* [<span data-ttu-id="1faff-145">Agregar un recurso compartido a Microsoft Teams en el sitio web</span><span class="sxs-lookup"><span data-stu-id="1faff-145">Add a Share to Teams button to your website</span></span>](doc-links/share-to-teams.md)
* [<span data-ttu-id="1faff-146">Sistema de diseño de interfaz de usuario Fluent</span><span class="sxs-lookup"><span data-stu-id="1faff-146">Fluent UI Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="1faff-147">SDK de cliente de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1faff-147">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* <span data-ttu-id="1faff-148">[Bot Framework SDK para JavaScript](https://github.com/Microsoft/botbuilder-js) y [Bot Framework SDK para .net](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="1faff-148">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
