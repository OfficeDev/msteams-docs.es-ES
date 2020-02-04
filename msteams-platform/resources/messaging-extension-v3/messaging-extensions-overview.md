---
title: Desarrollar extensiones de mensajería
description: Describe cómo empezar a trabajar con extensiones de mensajería en Microsoft Teams
keywords: extensiones de mensajería de extensiones de mensajería de Microsoft Teams
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675737"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="d0a15-104">Desarrollar extensiones de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d0a15-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="d0a15-105">Las extensiones de mensajería son una manera eficaz de que los usuarios participen con la aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d0a15-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="d0a15-106">Con esta capacidad, los usuarios pueden consultar o publicar información desde y hacia el servicio y publicar la información, en forma de tarjetas, directamente en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="d0a15-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="d0a15-108">Las extensiones de mensajería aparecen a lo largo de la parte inferior del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="d0a15-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="d0a15-109">Algunos están integrados, como Emoji, Giphy y adhesivo.</span><span class="sxs-lookup"><span data-stu-id="d0a15-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="d0a15-110">Elija el botón **más opciones** (**&#8943;**) para ver otras extensiones de mensajería, incluidas las que se agregan desde la galería de aplicaciones o que se cargan.</span><span class="sxs-lookup"><span data-stu-id="d0a15-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="d0a15-111">¿Cómo usaría las extensiones de mensajería?</span><span class="sxs-lookup"><span data-stu-id="d0a15-111">How would you use messaging extensions?</span></span> <span data-ttu-id="d0a15-112">Estas son algunas de las posibilidades:</span><span class="sxs-lookup"><span data-stu-id="d0a15-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="d0a15-113">Elementos de trabajo y errores</span><span class="sxs-lookup"><span data-stu-id="d0a15-113">Work items and bugs</span></span>
* <span data-ttu-id="d0a15-114">Vales de soporte al cliente</span><span class="sxs-lookup"><span data-stu-id="d0a15-114">Customer support tickets</span></span>
* <span data-ttu-id="d0a15-115">Gráficos de uso e informes</span><span class="sxs-lookup"><span data-stu-id="d0a15-115">Usage charts and reports</span></span>
* <span data-ttu-id="d0a15-116">Imágenes y contenido multimedia</span><span class="sxs-lookup"><span data-stu-id="d0a15-116">Images and media content</span></span>
* <span data-ttu-id="d0a15-117">Oportunidades y clientes potenciales de ventas</span><span class="sxs-lookup"><span data-stu-id="d0a15-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="d0a15-118">Tipos de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d0a15-118">Types of messaging extensions</span></span>

<span data-ttu-id="d0a15-119">Hay principalmente dos tipos de extensiones de mensajería que puede crear para Microsoft Teams en la actualidad.</span><span class="sxs-lookup"><span data-stu-id="d0a15-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="d0a15-120">Los siguientes temas le guiarán por el proceso de creación:</span><span class="sxs-lookup"><span data-stu-id="d0a15-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="d0a15-121">[Search based Messaging Extensions](~/resources/messaging-extension-v3/search-extensions.md): consultar el servicio para obtener información e insertarlo en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="d0a15-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="d0a15-122">Ejemplo: buscar un elemento de trabajo</span><span class="sxs-lookup"><span data-stu-id="d0a15-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="d0a15-123">[Extensiones de mensajería basadas en acciones](~/resources/messaging-extension-v3/create-extensions.md): recopilan información del usuario y se publican en un servicio de terceros.</span><span class="sxs-lookup"><span data-stu-id="d0a15-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="d0a15-124">Ejemplo: crear un elemento de trabajo</span><span class="sxs-lookup"><span data-stu-id="d0a15-124">Example: Create a work item</span></span>
