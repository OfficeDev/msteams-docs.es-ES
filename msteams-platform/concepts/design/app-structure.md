---
title: 'Diseñar la aplicación: comprender la estructura de la aplicación'
description: Comprende lo que puedes y no puedes personalizar en Microsoft Teams al diseñar la aplicación.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a574ebeb5416e614152bb24d52cc798f0032943c
ms.sourcegitcommit: 0fe60b3fd406a5768b18977df53d1f4c665e5300
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53133417"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="badfa-103">Comprender la estructura Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="badfa-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="badfa-104">Al compilar la aplicación, es importante saber lo que puedes y lo que no puedes personalizar en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="badfa-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="badfa-105">Esta información puede ayudarte a comprender mejor qué partes de la experiencia de la aplicación controlas.</span><span class="sxs-lookup"><span data-stu-id="badfa-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="badfa-106">Los siguientes fotogramas de cable muestran lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="badfa-106">The following wireframes show you:</span></span>

* <span data-ttu-id="badfa-107">Las superficies que puedes personalizar en cada Teams de la aplicación (esquemateada en rosa).</span><span class="sxs-lookup"><span data-stu-id="badfa-107">The surfaces you can customize in each Teams app capability (outlined in pink).</span></span>
* <span data-ttu-id="badfa-108">Los ámbitos que admite cada funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="badfa-108">The scopes each capability supports.</span></span>

> [!TIP]
> <span data-ttu-id="badfa-109">**¿Qué significa ámbito?**</span><span class="sxs-lookup"><span data-stu-id="badfa-109">**What does scope mean?**</span></span> <span data-ttu-id="badfa-110">Un ámbito es un área de Teams donde las personas pueden usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="badfa-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="badfa-111">Las aplicaciones pueden tener uno o varios ámbitos, incluidos personales, canales, chats y reuniones.</span><span class="sxs-lookup"><span data-stu-id="badfa-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="badfa-112">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="badfa-112">Personal apps</span></span>

<span data-ttu-id="badfa-113">Las aplicaciones personales proporcionan un lienzo grande para hospedar el contenido de la aplicación para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="badfa-113">Personal apps provide a large canvas to host your app content for individual users.</span></span>

<span data-ttu-id="badfa-114">\***Ámbitos admitidos**: Personal\*</span><span class="sxs-lookup"><span data-stu-id="badfa-114">\***Supported scopes**: Personal\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="badfa-115">Escritorio</span><span class="sxs-lookup"><span data-stu-id="badfa-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="badfa-116">El lienzo es un iframe para que puedas personalizar completamente la experiencia.</span><span class="sxs-lookup"><span data-stu-id="badfa-116">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para aplicaciones personales en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="badfa-118">Móvil</span><span class="sxs-lookup"><span data-stu-id="badfa-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="badfa-119">El lienzo es una vista web para que puedas personalizar completamente la experiencia.</span><span class="sxs-lookup"><span data-stu-id="badfa-119">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para aplicaciones personales en dispositivos móviles." border="false":::

---

## <a name="tabs"></a><span data-ttu-id="badfa-121">Pestañas</span><span class="sxs-lookup"><span data-stu-id="badfa-121">Tabs</span></span>

<span data-ttu-id="badfa-122">Las pestañas proporcionan un lienzo grande para hospedar el contenido de la aplicación para un grupo de usuarios.</span><span class="sxs-lookup"><span data-stu-id="badfa-122">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="badfa-123">Puede incluir pestañas en espacios compartidos como canales, chats e invitaciones a reuniones.</span><span class="sxs-lookup"><span data-stu-id="badfa-123">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span>

<span data-ttu-id="badfa-124">***Ámbitos admitidos:** canales, chats, reuniones*</span><span class="sxs-lookup"><span data-stu-id="badfa-124">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="badfa-125">Escritorio</span><span class="sxs-lookup"><span data-stu-id="badfa-125">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="badfa-126">El lienzo es un iframe para que puedas personalizar completamente la experiencia.</span><span class="sxs-lookup"><span data-stu-id="badfa-126">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las pestañas en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="badfa-128">Móvil</span><span class="sxs-lookup"><span data-stu-id="badfa-128">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="badfa-129">El lienzo es una vista web para que puedas personalizar completamente la experiencia.</span><span class="sxs-lookup"><span data-stu-id="badfa-129">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las pestañas en dispositivos móviles." border="false":::

---

## <a name="bots"></a><span data-ttu-id="badfa-131">Bots</span><span class="sxs-lookup"><span data-stu-id="badfa-131">Bots</span></span>

<span data-ttu-id="badfa-132">Los bots son aplicaciones de conversación que se integran con Teams de mensajería nativa, por lo que el trabajo de la interfaz de usuario se controla por ti.</span><span class="sxs-lookup"><span data-stu-id="badfa-132">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="badfa-133">Desde el punto de vista del diseño, aún hay oportunidades de agregar personalidad, funcionalidad personalizada e información rica y procesable con nuestra compatibilidad con procesamiento de lenguaje natural (NLP) y la plataforma de tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="badfa-133">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="badfa-134">***Ámbitos admitidos:** Personal, Canales, Chats, Reuniones*</span><span class="sxs-lookup"><span data-stu-id="badfa-134">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="badfa-135">Escritorio</span><span class="sxs-lookup"><span data-stu-id="badfa-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para bots en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="badfa-137">Móvil</span><span class="sxs-lookup"><span data-stu-id="badfa-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para bots en dispositivos móviles." border="false":::

---

## <a name="messaging-extensions"></a><span data-ttu-id="badfa-139">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="badfa-139">Messaging extensions</span></span>

<span data-ttu-id="badfa-140">Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o realizar una acción en un mensaje sin salir de la conversación.</span><span class="sxs-lookup"><span data-stu-id="badfa-140">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="badfa-141">Las extensiones de mensajería basadas en acciones te dan más control de la experiencia, mientras que Teams controla gran parte de lo que se representa para las extensiones de mensajería basadas en búsquedas.</span><span class="sxs-lookup"><span data-stu-id="badfa-141">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="badfa-142">***Ámbitos admitidos:** Personal, Canales, Chats, Reuniones*</span><span class="sxs-lookup"><span data-stu-id="badfa-142">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="badfa-143">Escritorio</span><span class="sxs-lookup"><span data-stu-id="badfa-143">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de mensajería en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="badfa-145">Móvil</span><span class="sxs-lookup"><span data-stu-id="badfa-145">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para extensiones de mensajería en dispositivos móviles." border="false":::

---

## <a name="meeting-extensions"></a><span data-ttu-id="badfa-147">Extensiones de reunión</span><span class="sxs-lookup"><span data-stu-id="badfa-147">Meeting extensions</span></span>

<span data-ttu-id="badfa-148">Las extensiones de reunión son aplicaciones para mejorar las reuniones en directo.</span><span class="sxs-lookup"><span data-stu-id="badfa-148">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="badfa-149">Puedes hospedar el contenido de la aplicación en varios escenarios, incluidos antes, durante y después de las reuniones.</span><span class="sxs-lookup"><span data-stu-id="badfa-149">You can host your app content in several scenarios, including before, during, and after meetings.</span></span>

<span data-ttu-id="badfa-150">***Ámbitos admitidos:** reuniones, chats*</span><span class="sxs-lookup"><span data-stu-id="badfa-150">\***Supported scopes**: Meetings, Chats\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="badfa-151">Escritorio</span><span class="sxs-lookup"><span data-stu-id="badfa-151">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="badfa-152">La superficie es un iframe, lo que te permite personalizar la experiencia, pero ten en cuenta que durante las reuniones estas aplicaciones usan un tema oscuro y son estrechas.</span><span class="sxs-lookup"><span data-stu-id="badfa-152">The surface is an iframe, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme and are narrow.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de reunión en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="badfa-154">Móvil</span><span class="sxs-lookup"><span data-stu-id="badfa-154">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="badfa-155">La superficie es una vista web, lo que te permite personalizar la experiencia, pero ten en cuenta que durante las reuniones estas aplicaciones usan un tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="badfa-155">The surface is a webview, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de reunión en dispositivos móviles." border="false":::

---
