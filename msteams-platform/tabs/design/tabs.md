---
title: Directrices de diseño para pestañas
description: Describe las instrucciones para crear pestañas de contenido y colaboración
keywords: Directrices de diseño de Microsoft Teams referencia de las fichas de marco de trabajo
ms.openlocfilehash: adf86678a42e2267af00734e1ef85efced882488
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675689"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="b6f01-104">Contenido y conversaciones, todos a la vez mediante pestañas</span><span class="sxs-lookup"><span data-stu-id="b6f01-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="b6f01-105">**Pestañas en clientes móviles**</span><span class="sxs-lookup"><span data-stu-id="b6f01-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="b6f01-106">Siga las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas.</span><span class="sxs-lookup"><span data-stu-id="b6f01-106">Follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="b6f01-107">Si su pestaña usa autenticación, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 o posterior, o se producirá un error de autenticación.</span><span class="sxs-lookup"><span data-stu-id="b6f01-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="b6f01-108">**Pestañas personales (estáticas) en dispositivos móviles:**</span><span class="sxs-lookup"><span data-stu-id="b6f01-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="b6f01-109">Las pestañas estáticas (aplicación personal) están disponibles en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b6f01-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="b6f01-110">Mientras crea las pestañas estáticas, asegúrese de seguir las [instrucciones para las pestañas de la móvil](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="b6f01-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="b6f01-111">**Pestañas de canal o grupo (configurable) en dispositivos móviles:**</span><span class="sxs-lookup"><span data-stu-id="b6f01-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="b6f01-112">Los clientes móviles solo muestran las pestañas que tienen `websiteUrl`un valor para.</span><span class="sxs-lookup"><span data-stu-id="b6f01-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="b6f01-113">Si desea que la pestaña aparezca en los clientes móviles de Teams, debe establecer el valor de `websiteUrl`.</span><span class="sxs-lookup"><span data-stu-id="b6f01-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="b6f01-114">El comportamiento predeterminado de apertura en dispositivos móviles es abrir fuera del explorador `websiteUrl`con el.</span><span class="sxs-lookup"><span data-stu-id="b6f01-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="b6f01-115">En el caso de las aplicaciones publicadas en la tienda de aplicaciones públicas, si desea que la ficha de canal se abra dentro de Teams de forma predeterminada, siga las [instrucciones para las pestañas de Mobile](~/tabs/design/tabs-mobile.md)y póngase en contacto con su representante de soporte técnico para que se le solicite que se le solicite que se le pida que</span><span class="sxs-lookup"><span data-stu-id="b6f01-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="b6f01-116">Las pestañas son lienzos que se pueden usar para compartir contenido, mantener conversaciones y hospedar servicios de terceros, todo ello dentro del flujo de trabajo ecológico de un equipo.</span><span class="sxs-lookup"><span data-stu-id="b6f01-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="b6f01-117">Cuando se crea una pestaña en Microsoft Teams, se coloca la aplicación web en su lugar y en el centro a la que se puede acceder fácilmente desde las conversaciones clave.</span><span class="sxs-lookup"><span data-stu-id="b6f01-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="b6f01-118">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="b6f01-118">Guidelines</span></span>

<span data-ttu-id="b6f01-119">Una buena pestaña debe mostrar las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="b6f01-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="b6f01-120">Funcionalidad centrada</span><span class="sxs-lookup"><span data-stu-id="b6f01-120">Focused functionality</span></span>

<span data-ttu-id="b6f01-121">Las pestañas funcionan mejor cuando se crean para satisfacer una necesidad específica.</span><span class="sxs-lookup"><span data-stu-id="b6f01-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="b6f01-122">Céntrese en un pequeño conjunto de tareas o en un subconjunto de datos que sea relevante para el canal en el que se encuentra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="b6f01-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="b6f01-123">Cromo reducido</span><span class="sxs-lookup"><span data-stu-id="b6f01-123">Reduced chrome</span></span>

<span data-ttu-id="b6f01-124">Evite crear varios paneles en una pestaña, agregar capas de navegación o requerir que los usuarios se desplacen tanto vertical como horizontalmente en una pestaña. Es decir, intente no tener pestañas en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="b6f01-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

> [!TIP]
> <span data-ttu-id="b6f01-125">Evite crear varios paneles en una pestaña, agregar capas de navegación o requerir que los usuarios se desplacen tanto vertical como horizontalmente en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="b6f01-125">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab.</span></span>

### <a name="integration"></a><span data-ttu-id="b6f01-126">Integración</span><span class="sxs-lookup"><span data-stu-id="b6f01-126">Integration</span></span>

<span data-ttu-id="b6f01-127">Obtenga información sobre cómo notificar a los usuarios la actividad de pestañas mediante el registro de tarjetas en una conversación, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b6f01-127">Find ways to notify users about tab activity by posting cards to a conversation, for example.</span></span>

### <a name="conversational"></a><span data-ttu-id="b6f01-128">Conversación</span><span class="sxs-lookup"><span data-stu-id="b6f01-128">Conversational</span></span>

<span data-ttu-id="b6f01-129">Buscar una forma de facilitar la conversación alrededor de una pestaña. Esto garantiza que las conversaciones se centran en el contenido, los datos o el proceso a mano.</span><span class="sxs-lookup"><span data-stu-id="b6f01-129">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="b6f01-130">Acceso simplificado</span><span class="sxs-lookup"><span data-stu-id="b6f01-130">Streamlined access</span></span>

<span data-ttu-id="b6f01-131">Asegúrese de que está concediendo acceso a las personas adecuadas en el momento adecuado.</span><span class="sxs-lookup"><span data-stu-id="b6f01-131">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="b6f01-132">Mantener simple el proceso de inicio de sesión evitará la creación de obstáculos a la contribución y la colaboración.</span><span class="sxs-lookup"><span data-stu-id="b6f01-132">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="personality"></a><span data-ttu-id="b6f01-133">Personalidad</span><span class="sxs-lookup"><span data-stu-id="b6f01-133">Personality</span></span>

<span data-ttu-id="b6f01-134">Tu lienzo de pestañas ofrece una buena oportunidad para personalizar tu experiencia.</span><span class="sxs-lookup"><span data-stu-id="b6f01-134">Your tab canvas presents a good opportunity to brand your experience.</span></span> <span data-ttu-id="b6f01-135">Incorpore sus propios logotipos, colores y diseños para comunicar la personalidad.</span><span class="sxs-lookup"><span data-stu-id="b6f01-135">Incorporate your own logos, colors, and layouts to communicate personality.</span></span>

<span data-ttu-id="b6f01-136">Su logotipo es una parte importante de su identidad y una conexión con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b6f01-136">Your logo is an important part of your identity and a connection with your users.</span></span> <span data-ttu-id="b6f01-137">Por lo tanto, asegúrese de incluirla.</span><span class="sxs-lookup"><span data-stu-id="b6f01-137">So be sure to include it.</span></span>

* <span data-ttu-id="b6f01-138">Poner el logotipo en la esquina izquierda o derecha o a lo largo del borde inferior</span><span class="sxs-lookup"><span data-stu-id="b6f01-138">Place your logo in the left or right corner or along the bottom edge</span></span>
* <span data-ttu-id="b6f01-139">Mantener el logotipo en pequeña y discreta</span><span class="sxs-lookup"><span data-stu-id="b6f01-139">Keep your logo small and unobtrusive</span></span>

> [!TIP]
> <span data-ttu-id="b6f01-140">Trabaje con nuestro estilo visual para que su servicio se sienta como parte de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b6f01-140">Please work with our visual style so your service feels like a part of Teams.</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="b6f01-141">Diseños de pestañas</span><span class="sxs-lookup"><span data-stu-id="b6f01-141">Tab layouts</span></span>

[!include[Tab layouts](~/includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="b6f01-142">Tipos de pestañas</span><span class="sxs-lookup"><span data-stu-id="b6f01-142">Types of tabs</span></span>

[!include[Tab types](~/includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="b6f01-143">Alto de página de configuración</span><span class="sxs-lookup"><span data-stu-id="b6f01-143">Configuration page height</span></span>

>[!NOTE]
><span data-ttu-id="b6f01-144">En septiembre de 2018, se incrementó el alto de la [Página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md) de pestañas mientras el ancho permaneció sin cambios.</span><span class="sxs-lookup"><span data-stu-id="b6f01-144">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="b6f01-145">Si la aplicación está diseñada para el tamaño anterior, la página de configuración de pestañas tendrá una gran cantidad de espacio en blanco vertical.</span><span class="sxs-lookup"><span data-stu-id="b6f01-145">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="b6f01-146">Las aplicaciones de la tienda heredadas exentas de este cambio tendrán que ponerse en contacto con Microsoft después de la actualización para acomodar las nuevas dimensiones.</span><span class="sxs-lookup"><span data-stu-id="b6f01-146">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="b6f01-147">Las dimensiones de la página de configuración de pestañas:</span><span class="sxs-lookup"><span data-stu-id="b6f01-147">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="Tamaños de las pestañas de configuración" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="b6f01-149">Instrucciones para el formato de página de configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="b6f01-149">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="b6f01-150">Base el alto mínimo del área de contenido de la página de configuración de pestañas en elementos gráficos de altura fija.</span><span class="sxs-lookup"><span data-stu-id="b6f01-150">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="b6f01-151">Calcula el espacio vertical disponible (el alto del área de contenido en la página de configuración `window.innerHeight`) mediante.</span><span class="sxs-lookup"><span data-stu-id="b6f01-151">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="b6f01-152">Esto devuelve el tamaño del en `<iframe>` el que reside la página de configuración, lo que puede cambiar en futuras versiones.</span><span class="sxs-lookup"><span data-stu-id="b6f01-152">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="b6f01-153">Al usar este valor, el contenido se ajustará automáticamente a los cambios futuros.</span><span class="sxs-lookup"><span data-stu-id="b6f01-153">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="b6f01-154">Asigna espacio vertical a los elementos variable-height menos lo que se necesita para los elementos de altura fija.</span><span class="sxs-lookup"><span data-stu-id="b6f01-154">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="b6f01-155">Para el estado de *Inicio de sesión* , centrar vertical y horizontalmente el contenido.</span><span class="sxs-lookup"><span data-stu-id="b6f01-155">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="b6f01-156">Si desea una imagen de fondo, necesitará una nueva imagen, ajustada para ajustarse al área (recomendado) o puede conservar la misma imagen y elegir entre:</span><span class="sxs-lookup"><span data-stu-id="b6f01-156">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="b6f01-157">alineación a la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="b6f01-157">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="b6f01-158">escalar la imagen para ajustarla.</span><span class="sxs-lookup"><span data-stu-id="b6f01-158">scaling the image to fit.</span></span>

<span data-ttu-id="b6f01-159">Cuando esté correctamente ajustado, la página de configuración de pestaña debe tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="b6f01-159">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Nueva pestaña Configuración" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="b6f01-161">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="b6f01-161">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="b6f01-162">Incluir siempre un estado predeterminado</span><span class="sxs-lookup"><span data-stu-id="b6f01-162">Always include a default state</span></span>

<span data-ttu-id="b6f01-163">Incluya un estado predeterminado para que las pestañas se puedan configurar fácilmente incluso si la pestaña se puede configurar.</span><span class="sxs-lookup"><span data-stu-id="b6f01-163">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="b6f01-164">Vinculación profunda</span><span class="sxs-lookup"><span data-stu-id="b6f01-164">Deep linking</span></span>

<span data-ttu-id="b6f01-165">Siempre que sea posible, las tarjetas y los bots deben tener un vínculo profundo a datos enriquecidos en una pestaña hospedada. Por ejemplo, puede que una tarjeta muestre un resumen de los datos de los errores, pero al hacer clic en él se muestra el error completo en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="b6f01-165">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="b6f01-166">Poner</span><span class="sxs-lookup"><span data-stu-id="b6f01-166">Naming</span></span>

<span data-ttu-id="b6f01-167">En muchos casos, el nombre de la aplicación puede crear un nombre de pestaña excelente.</span><span class="sxs-lookup"><span data-stu-id="b6f01-167">In many cases, the name of your app may make a great tab name.</span></span> <span data-ttu-id="b6f01-168">Pero considere la posibilidad de asignar un nombre a las pestañas según la funcionalidad que proporcionan.</span><span class="sxs-lookup"><span data-stu-id="b6f01-168">But consider naming your tabs according to the functionality they provide.</span></span>
