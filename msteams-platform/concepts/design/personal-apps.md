---
title: Referencia de directrices de diseño
description: Describe las instrucciones para diseñar una aplicación personal
keywords: guías de diseño de Microsoft Teams referencia de aplicaciones personales
ms.openlocfilehash: f66691234149afa56a6753dd51379c9f2355318e
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455502"
---
# <a name="personal-apps"></a><span data-ttu-id="77df3-104">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="77df3-104">Personal apps</span></span>

> [!NOTE]
> <span data-ttu-id="77df3-105">Teams admite completamente la compatibilidad con las pestañas de los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="77df3-105">Full support for tabs on mobile clients is supported in Teams.</span></span> <span data-ttu-id="77df3-106">Debe seguir las [instrucciones para las pestañas de dispositivos móviles](../../tabs/design/tabs-mobile.md) al crear pestañas para plataformas móviles.</span><span class="sxs-lookup"><span data-stu-id="77df3-106">You should follow the [guidance for tabs on mobile](../../tabs/design/tabs-mobile.md) when creating tabs for mobile platforms.</span></span>

<span data-ttu-id="77df3-107">Una aplicación personal es una aplicación de Microsoft Teams con un ámbito personal.</span><span class="sxs-lookup"><span data-stu-id="77df3-107">A personal app is a Teams application with a personal scope.</span></span>  <span data-ttu-id="77df3-108">Como desarrollador de aplicaciones, tiene la opción de proporcionar una versión de la aplicación que se Centre en las interacciones con un único usuario.</span><span class="sxs-lookup"><span data-stu-id="77df3-108">As an app developer, you have the option to provide a version of your app that focuses on interactions with a single user.</span></span> <span data-ttu-id="77df3-109">Puede ser un [Bot de conversación](../../bots/what-are-bots.md) para participar en conversaciones de uno a uno con un usuario o con una [pestaña personal](../../tabs/what-are-tabs.md) que proporciona una experiencia Web integrada.</span><span class="sxs-lookup"><span data-stu-id="77df3-109">It can be a [conversational bot](../../bots/what-are-bots.md) to engage in one-to-one conversations with a user or a [personal tab](../../tabs/what-are-tabs.md) providing an embedded web experience.</span></span> <span data-ttu-id="77df3-110">Las aplicaciones personales permiten a los usuarios ver su contenido seleccionado en un solo punto.</span><span class="sxs-lookup"><span data-stu-id="77df3-110">Personal apps enable users to view their select content in one place.</span></span> <span data-ttu-id="77df3-111">En la siguiente captura de pantalla, contoso es una aplicación personal en el flotante de la aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="77df3-111">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![imagen del menú de desbordamiento de la aplicación](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="77df3-113">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="77df3-113">Guidelines</span></span>

<span data-ttu-id="77df3-114">Una aplicación personal suele contener las siguientes pestañas:</span><span class="sxs-lookup"><span data-stu-id="77df3-114">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="77df3-115">La pestaña</span><span class="sxs-lookup"><span data-stu-id="77df3-115">Your tab</span></span>

<span data-ttu-id="77df3-116">Aquí es donde los usuarios verán todo su contenido.</span><span class="sxs-lookup"><span data-stu-id="77df3-116">This is where your users will see all their stuff.</span></span> <span data-ttu-id="77df3-117">Su espacio personal.</span><span class="sxs-lookup"><span data-stu-id="77df3-117">It's their personal space.</span></span> <span data-ttu-id="77df3-118">La pestaña se puede organizar como una lista, una cuadrícula, columnas o un solo lienzo... lo que mejor se adapte a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="77df3-118">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="77df3-119">Para obtener más información sobre el diseño de pestañas efectivas, vea: [diseño de pestañas](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="77df3-119">For additional information on designing effective tabs see: [Tabs design](../../tabs/design/tabs.md).</span></span>

<span data-ttu-id="77df3-120">Como esta pestaña puede mostrar elementos de varios canales, cada elemento debería mostrar su propio equipo, canal y pestaña para que el usuario pueda ver fácilmente dónde se originó.</span><span class="sxs-lookup"><span data-stu-id="77df3-120">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

![Ficha tareas personales](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="77df3-122">Posterior</span><span class="sxs-lookup"><span data-stu-id="77df3-122">Recent</span></span>

<span data-ttu-id="77df3-123">La pestaña **reciente** permite a un usuario examinar todo lo que haya visto recientemente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77df3-123">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="77df3-124">Aparece en orden cronológico (de mayor a menos reciente).</span><span class="sxs-lookup"><span data-stu-id="77df3-124">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="77df3-125">Al hacer clic en un elemento de esta lista, se desplazará al usuario hasta el canal y la ficha del elemento.</span><span class="sxs-lookup"><span data-stu-id="77df3-125">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![Pestaña reciente](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="77df3-127">Todo</span><span class="sxs-lookup"><span data-stu-id="77df3-127">All</span></span>

<span data-ttu-id="77df3-128">Esta es una lista de todas las pestañas de la organización de la persona (a las que tienen acceso, en cualquier caso).</span><span class="sxs-lookup"><span data-stu-id="77df3-128">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="77df3-129">Es decir, los muestra en todas partes donde se usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77df3-129">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="77df3-130">Como en la ficha **reciente** , al seleccionar un elemento de la lista, el usuario pasa directamente al canal y a la ficha correspondientes.</span><span class="sxs-lookup"><span data-stu-id="77df3-130">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="77df3-131">Bot</span><span class="sxs-lookup"><span data-stu-id="77df3-131">Bot</span></span>

<span data-ttu-id="77df3-132">Un bot no es necesario, pero es una buena forma de comunicarse directa y privadamente con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="77df3-132">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="77df3-133">La notificación es una de las funciones más importantes de una aplicación personal y la mejor forma de notificarla que con la comunicación directa.</span><span class="sxs-lookup"><span data-stu-id="77df3-133">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="77df3-134">Los bots entregan mensajes en forma de tarjetas, que pueden proporcionar información específica (por ejemplo, una alerta de que el contenido nuevo está disponible) o actualizaciones amplias (como una lista de tareas pendientes diaria).</span><span class="sxs-lookup"><span data-stu-id="77df3-134">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="77df3-135">Para obtener más información sobre el diseño de bots efectivos, vea: [diseño de bot](../../bots/design/bots.md).</span><span class="sxs-lookup"><span data-stu-id="77df3-135">For additional information on designing effective bots see: [Bot design](../../bots/design/bots.md).</span></span>

![Saludo de bot](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="77df3-137">Ayuda y configuración</span><span class="sxs-lookup"><span data-stu-id="77df3-137">Help and Settings</span></span>

<span data-ttu-id="77df3-138">El contenido de la ayuda permite a los usuarios descubrir los matices de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77df3-138">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="77df3-139">Agregue una pestaña de **configuración** para darles la capacidad de personalizarla.</span><span class="sxs-lookup"><span data-stu-id="77df3-139">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="77df3-140">Acerca de</span><span class="sxs-lookup"><span data-stu-id="77df3-140">About</span></span>

<span data-ttu-id="77df3-141">Incluya una ficha **acerca** de para proporcionar información como el número de versión, las capacidades, la privacidad y los vínculos de permisos.</span><span class="sxs-lookup"><span data-stu-id="77df3-141">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="77df3-142">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="77df3-142">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="77df3-143">Comunicarse directamente con los usuarios</span><span class="sxs-lookup"><span data-stu-id="77df3-143">Communicate directly with your users</span></span>

<span data-ttu-id="77df3-144">Usar un bot para notificar a los usuarios los cambios y las nuevas características.</span><span class="sxs-lookup"><span data-stu-id="77df3-144">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="77df3-145">Personalice sus pestañas...</span><span class="sxs-lookup"><span data-stu-id="77df3-145">Customize your tabs...</span></span>

<span data-ttu-id="77df3-146">No dude en agregar otras pestañas que ayuden a los usuarios a realizar tareas específicas.</span><span class="sxs-lookup"><span data-stu-id="77df3-146">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="77df3-147">... y hacer que sean relevantes para todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="77df3-147">...and make them relevant to every user</span></span>

<span data-ttu-id="77df3-148">Cada pestaña que declare en el manifiesto de la aplicación será visible para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="77df3-148">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="77df3-149">Por ejemplo, si la aplicación personal es una herramienta de informes de gastos que usan tanto los administradores como los empleados, una ficha de **aprobación** debe proporcionar contenido que sea significativo para ambas funciones.</span><span class="sxs-lookup"><span data-stu-id="77df3-149">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
