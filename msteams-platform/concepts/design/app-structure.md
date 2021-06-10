---
title: 'Diseñar la aplicación: comprender la estructura de la aplicación'
description: Comprende lo que puedes y no puedes personalizar en Microsoft Teams al diseñar la aplicación.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631391"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="3c122-103">Comprender la estructura Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="3c122-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="3c122-104">Al compilar la aplicación, es importante saber lo que puedes y lo que no puedes personalizar en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3c122-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="3c122-105">Esta información puede ayudarte a comprender mejor qué partes de la experiencia de la aplicación controlas.</span><span class="sxs-lookup"><span data-stu-id="3c122-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="3c122-106">Los siguientes fotogramas de cable muestran lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3c122-106">The following wireframes show you:</span></span>

* <span data-ttu-id="3c122-107">Las superficies que puedes personalizar en cada Teams de la aplicación (esquemateada en azul).</span><span class="sxs-lookup"><span data-stu-id="3c122-107">The surfaces you can customize in each Teams app capability (outlined in blue).</span></span>
* <span data-ttu-id="3c122-108">Los ámbitos que admite cada funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="3c122-108">The scopes each capability supports.</span></span>

> [!NOTE]
> <span data-ttu-id="3c122-109">**¿Qué significa ámbito?**</span><span class="sxs-lookup"><span data-stu-id="3c122-109">**What does scope mean?**</span></span> <span data-ttu-id="3c122-110">Un ámbito es un área de Teams donde las personas pueden usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c122-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="3c122-111">Las aplicaciones pueden tener uno o varios ámbitos, incluidos personales, canales, chats y reuniones.</span><span class="sxs-lookup"><span data-stu-id="3c122-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="3c122-112">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="3c122-112">Personal apps</span></span>

<span data-ttu-id="3c122-113">Las aplicaciones personales proporcionan un lienzo grande para hospedar el contenido de la aplicación para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="3c122-113">Personal apps provide a large canvas to host your app content for individual users.</span></span> <span data-ttu-id="3c122-114">El lienzo es un iframe para que puedas personalizar completamente la experiencia.</span><span class="sxs-lookup"><span data-stu-id="3c122-114">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="3c122-115">\***Ámbitos admitidos**: Personal\*</span><span class="sxs-lookup"><span data-stu-id="3c122-115">\***Supported scopes**: Personal\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para aplicaciones personales." border="false":::

## <a name="tabs"></a><span data-ttu-id="3c122-117">Pestañas</span><span class="sxs-lookup"><span data-stu-id="3c122-117">Tabs</span></span>

<span data-ttu-id="3c122-118">Las pestañas proporcionan un lienzo grande para hospedar el contenido de la aplicación para un grupo de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3c122-118">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="3c122-119">Puede incluir pestañas en espacios compartidos como canales, chats e invitaciones a reuniones.</span><span class="sxs-lookup"><span data-stu-id="3c122-119">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span> <span data-ttu-id="3c122-120">El lienzo es un iframe para que puedas personalizar completamente la experiencia.</span><span class="sxs-lookup"><span data-stu-id="3c122-120">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="3c122-121">***Ámbitos admitidos:** canales, chats, reuniones*</span><span class="sxs-lookup"><span data-stu-id="3c122-121">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las pestañas." border="false":::

## <a name="bots"></a><span data-ttu-id="3c122-123">Bots</span><span class="sxs-lookup"><span data-stu-id="3c122-123">Bots</span></span>

<span data-ttu-id="3c122-124">Los bots son aplicaciones de conversación que se integran con Teams de mensajería nativa, por lo que el trabajo de la interfaz de usuario se controla por ti.</span><span class="sxs-lookup"><span data-stu-id="3c122-124">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="3c122-125">Desde el punto de vista del diseño, aún hay oportunidades de agregar personalidad, funcionalidad personalizada e información rica y procesable con nuestra compatibilidad con procesamiento de lenguaje natural (NLP) y la plataforma de tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="3c122-125">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="3c122-126">***Ámbitos admitidos:** Personal, Canales, Chats, Reuniones*</span><span class="sxs-lookup"><span data-stu-id="3c122-126">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para bots." border="false":::

## <a name="messaging-extensions"></a><span data-ttu-id="3c122-128">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="3c122-128">Messaging extensions</span></span>

<span data-ttu-id="3c122-129">Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación.</span><span class="sxs-lookup"><span data-stu-id="3c122-129">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="3c122-130">Las extensiones de mensajería basadas en acciones te dan más control de la experiencia, mientras que Teams controla gran parte de lo que se representa para las extensiones de mensajería basadas en búsquedas.</span><span class="sxs-lookup"><span data-stu-id="3c122-130">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="3c122-131">***Ámbitos admitidos:** Personal, Canales, Chats, Reuniones*</span><span class="sxs-lookup"><span data-stu-id="3c122-131">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de mensajería." border="false":::

## <a name="meeting-extensions"></a><span data-ttu-id="3c122-133">Extensiones de reunión</span><span class="sxs-lookup"><span data-stu-id="3c122-133">Meeting extensions</span></span>

<span data-ttu-id="3c122-134">Las extensiones de reunión son aplicaciones para mejorar las reuniones en directo.</span><span class="sxs-lookup"><span data-stu-id="3c122-134">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="3c122-135">Puedes hospedar el contenido de la aplicación en varios escenarios, incluidos antes, durante y después de las reuniones.</span><span class="sxs-lookup"><span data-stu-id="3c122-135">You can host your app content in several scenarios, including before, during, and after meetings.</span></span> <span data-ttu-id="3c122-136">La superficie es un iframe, lo que te permite personalizar la experiencia, pero ten en cuenta que estas aplicaciones tienen un estilo oscuro y son estrechas durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="3c122-136">The surface is an iframe, allowing you to customize the experience, but keep in mind that these apps are dark themed and narrow during meetings.</span></span>

<span data-ttu-id="3c122-137">***Ámbitos admitidos:** reuniones, chats*</span><span class="sxs-lookup"><span data-stu-id="3c122-137">\***Supported scopes**: Meetings, Chats\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de reunión." border="false":::
