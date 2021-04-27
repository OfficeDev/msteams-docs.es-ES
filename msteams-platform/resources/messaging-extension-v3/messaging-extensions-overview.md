---
title: Desarrollar extensiones de mensajería
description: Describe cómo empezar a usar extensiones de mensajería en Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: extensiones de mensajería de teams
ms.openlocfilehash: 2301a9af7574c193c7327bb45e38f91bedc73793
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020607"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="575d3-104">Desarrollar extensiones de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="575d3-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="575d3-105">Las extensiones de mensajería son una forma eficaz de que los usuarios puedan interactuar con la aplicación desde Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="575d3-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="575d3-106">Con esta funcionalidad, los usuarios pueden consultar o publicar información desde y hacia el servicio y publicar esa información, en forma de tarjetas, directamente en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="575d3-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="575d3-108">Las extensiones de mensajería aparecen en la parte inferior del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="575d3-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="575d3-109">Algunos están integrados, como Emoji, Giphy y Sticker.</span><span class="sxs-lookup"><span data-stu-id="575d3-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="575d3-110">Elige el **botón Más opciones** (**&#8943;**) para ver otras extensiones de mensajería, incluidas las que agregues desde la galería de aplicaciones o cargues tú mismo.</span><span class="sxs-lookup"><span data-stu-id="575d3-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="575d3-111">¿Cómo usaría las extensiones de mensajería?</span><span class="sxs-lookup"><span data-stu-id="575d3-111">How would you use messaging extensions?</span></span> <span data-ttu-id="575d3-112">Estas son algunas posibilidades:</span><span class="sxs-lookup"><span data-stu-id="575d3-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="575d3-113">Elementos de trabajo y errores</span><span class="sxs-lookup"><span data-stu-id="575d3-113">Work items and bugs</span></span>
* <span data-ttu-id="575d3-114">Vales de soporte al cliente</span><span class="sxs-lookup"><span data-stu-id="575d3-114">Customer support tickets</span></span>
* <span data-ttu-id="575d3-115">Gráficos e informes de uso</span><span class="sxs-lookup"><span data-stu-id="575d3-115">Usage charts and reports</span></span>
* <span data-ttu-id="575d3-116">Imágenes y contenido multimedia</span><span class="sxs-lookup"><span data-stu-id="575d3-116">Images and media content</span></span>
* <span data-ttu-id="575d3-117">Oportunidades de ventas y clientes potenciales</span><span class="sxs-lookup"><span data-stu-id="575d3-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="575d3-118">Tipos de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="575d3-118">Types of messaging extensions</span></span>

<span data-ttu-id="575d3-119">Hay principalmente dos tipos de extensiones de mensajería que puede crear para Teams hoy en día.</span><span class="sxs-lookup"><span data-stu-id="575d3-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="575d3-120">Los siguientes temas le guiarán a través del proceso de creación:</span><span class="sxs-lookup"><span data-stu-id="575d3-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="575d3-121">[Extensiones de mensajería basadas en búsquedas:](~/resources/messaging-extension-v3/search-extensions.md)consulte su servicio para obtener información e insertarla en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="575d3-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="575d3-122">Ejemplo: buscar un elemento de trabajo</span><span class="sxs-lookup"><span data-stu-id="575d3-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="575d3-123">[Extensiones de mensajería basadas en acciones:](~/resources/messaging-extension-v3/create-extensions.md)recopilar información del usuario y publicarla en un servicio de terceros.</span><span class="sxs-lookup"><span data-stu-id="575d3-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="575d3-124">Ejemplo: Crear un elemento de trabajo</span><span class="sxs-lookup"><span data-stu-id="575d3-124">Example: Create a work item</span></span>
