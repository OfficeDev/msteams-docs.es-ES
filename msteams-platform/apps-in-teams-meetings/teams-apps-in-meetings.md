---
title: Aplicaciones para Teams reuniones
author: laujan
description: información general sobre las aplicaciones en Teams reuniones basadas en el rol de participante y usuario
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: 69016f818a333cb4f7cecc252539e076838a0735
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949654"
---
# <a name="apps-for-teams-meetings"></a><span data-ttu-id="97753-104">Aplicaciones para Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="97753-104">Apps for Teams meetings</span></span>

<span data-ttu-id="97753-105">Las reuniones permiten la colaboración, la asociación, la comunicación informada y los comentarios compartidos en un foro inclusivo y activo.</span><span class="sxs-lookup"><span data-stu-id="97753-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="97753-106">La aplicación de reunión puede ofrecer una experiencia de usuario para cada fase del ciclo de vida de la reunión, incluida la experiencia de la aplicación previa, en la reunión y posterior a la reunión, según el estado del asistente.</span><span class="sxs-lookup"><span data-stu-id="97753-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting, and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="97753-107">Los usuarios pueden acceder a las aplicaciones durante las reuniones mediante la galería de pestañas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="97753-107">The users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="97753-108">Pre-stage a Kanban board.</span><span class="sxs-lookup"><span data-stu-id="97753-108">Pre-stage a Kanban board.</span></span>
* <span data-ttu-id="97753-109">Inicie un cuadro de diálogo que se puede ejecutar en la reunión.</span><span class="sxs-lookup"><span data-stu-id="97753-109">Launch an in-meeting actionable dialog.</span></span>
* <span data-ttu-id="97753-110">Crear una encuesta posterior a la reunión.</span><span class="sxs-lookup"><span data-stu-id="97753-110">Create a post-meeting survey.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/nKAy5rNDus4]

<span data-ttu-id="97753-111">En este artículo se proporciona información general sobre la extensibilidad de la aplicación de reunión, las referencias a la API, la habilitación y configuración de aplicaciones para reuniones y las escenas personalizadas del Modo conjunto en Teams.</span><span class="sxs-lookup"><span data-stu-id="97753-111">This article provides an overview of meeting app extensibility, API references, enable and configure apps for meetings, and custom Together Mode scenes in Teams.</span></span>

<span data-ttu-id="97753-112">Puedes mejorar tu experiencia de reunión mediante la característica de extensibilidad de reuniones, que te permite integrar tus aplicaciones dentro de las reuniones.</span><span class="sxs-lookup"><span data-stu-id="97753-112">You can enhance your meeting experience by using the meeting extensibility feature, which enables you to integrate your apps within meetings.</span></span> <span data-ttu-id="97753-113">También incluye diferentes etapas de un ciclo de vida de reunión, donde puede integrar pestañas, bots y extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="97753-113">It also includes different stages of a meeting lifecycle, where you can integrate tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="97753-114">Con las API de extensibilidad de reuniones, puede identificar diferentes roles de participante y tipos de usuario, obtener eventos de reunión, generar cuadros de diálogo en la reunión, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="97753-114">With meetings extensibility APIs, you can identify different participant roles and user types, get meeting events, generate in-meeting dialogs, and so on.</span></span>

<span data-ttu-id="97753-115">Para personalizar Teams con aplicaciones para reuniones, puedes habilitar las aplicaciones para reuniones Teams actualizando el manifiesto de la aplicación y también puedes configurar tus aplicaciones para escenarios de reunión.</span><span class="sxs-lookup"><span data-stu-id="97753-115">To customize Teams with apps for meetings, you can enable your apps for Teams meetings by updating your app manifest and you can also configure your apps for meeting scenarios.</span></span>

<span data-ttu-id="97753-116">La nueva característica personalizada de escenas del modo combinado permite a los usuarios colaborar en una reunión con su equipo en un solo lugar sin estar separados por cuadros.</span><span class="sxs-lookup"><span data-stu-id="97753-116">The new custom Together Mode scenes feature enables users to collaborate in a meeting with their team in one place without being separated by boxes.</span></span>

## <a name="see-also"></a><span data-ttu-id="97753-117">Vea también</span><span class="sxs-lookup"><span data-stu-id="97753-117">See also</span></span>

* [<span data-ttu-id="97753-118">Tab</span><span class="sxs-lookup"><span data-stu-id="97753-118">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="97753-119">Bot</span><span class="sxs-lookup"><span data-stu-id="97753-119">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="97753-120">Extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="97753-120">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="97753-121">Diseño de la aplicación</span><span class="sxs-lookup"><span data-stu-id="97753-121">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="97753-122">Requisitos previos y referencias de API para las aplicaciones en las reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="97753-122">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)
* [<span data-ttu-id="97753-123">Escenas del modo conjunto personalizado</span><span class="sxs-lookup"><span data-stu-id="97753-123">Custom Together Mode scenes</span></span>](~/apps-in-teams-meetings/teams-together-mode.md)

## <a name="next-step"></a><span data-ttu-id="97753-124">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="97753-124">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97753-125">Extensibilidad de la aplicación para reuniones</span><span class="sxs-lookup"><span data-stu-id="97753-125">Meeting app extensibility</span></span>](meeting-app-extensibility.md)
