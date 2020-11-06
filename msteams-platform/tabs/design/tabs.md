---
title: Directrices de diseño para pestañas
description: Describe las instrucciones para crear pestañas de contenido y colaboración
keywords: Directrices de diseño de Microsoft Teams referencia de marco de trabajo de configuración ficha estática ficha de canal de diseño de ficha sencillo
ms.openlocfilehash: 9ce72e97fa92e7d5db0fd51f29b2b905f378e788
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931802"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="df196-104">Contenido y conversaciones, todos a la vez mediante pestañas</span><span class="sxs-lookup"><span data-stu-id="df196-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="df196-105">**Pestañas en clientes móviles**</span><span class="sxs-lookup"><span data-stu-id="df196-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="df196-106">Siga las [instrucciones para las pestañas de dispositivos móviles](./tabs-mobile.md) al crear las pestañas.</span><span class="sxs-lookup"><span data-stu-id="df196-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="df196-107">Si su pestaña usa autenticación, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 o posterior, o se producirá un error de autenticación.</span><span class="sxs-lookup"><span data-stu-id="df196-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="df196-108">**Pestañas de canal o grupo (configurable) en dispositivos móviles:**</span><span class="sxs-lookup"><span data-stu-id="df196-108">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="df196-109">Los clientes móviles solo muestran pestañas configurables que tienen un valor para `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="df196-109">Mobile clients only show configurable tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="df196-110">Si desea que la pestaña aparezca en los clientes móviles de Teams, debe establecer el valor de `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="df196-110">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="df196-111">El comportamiento predeterminado de apertura en dispositivos móviles es abrir fuera del explorador con el `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="df196-111">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="df196-112">En el caso de las aplicaciones publicadas en la tienda de aplicaciones públicas, si desea que la ficha de canal se abra dentro de Teams de forma predeterminada, siga las [instrucciones para las pestañas de Mobile](~/tabs/design/tabs-mobile.md)y póngase en contacto con su representante de soporte técnico para que se le solicite que se le solicite que se le pida que</span><span class="sxs-lookup"><span data-stu-id="df196-112">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="df196-113">Las pestañas son lienzos que se pueden usar para compartir contenido, mantener conversaciones y hospedar servicios de terceros, todo ello dentro del flujo de trabajo ecológico de un equipo.</span><span class="sxs-lookup"><span data-stu-id="df196-113">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="df196-114">Cuando se crea una pestaña en Microsoft Teams, se coloca la aplicación web en su lugar y en el centro a la que se puede acceder fácilmente desde las conversaciones clave.</span><span class="sxs-lookup"><span data-stu-id="df196-114">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="df196-115">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="df196-115">Guidelines</span></span>

<span data-ttu-id="df196-116">Una buena pestaña debe mostrar las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="df196-116">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="df196-117">Funcionalidad centrada</span><span class="sxs-lookup"><span data-stu-id="df196-117">Focused functionality</span></span>

<span data-ttu-id="df196-118">Las pestañas funcionan mejor cuando se crean para satisfacer una necesidad específica.</span><span class="sxs-lookup"><span data-stu-id="df196-118">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="df196-119">Céntrese en un pequeño conjunto de tareas o en un subconjunto de datos que sea relevante para el canal en el que se encuentra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="df196-119">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="df196-120">Cromo reducido</span><span class="sxs-lookup"><span data-stu-id="df196-120">Reduced chrome</span></span>

<span data-ttu-id="df196-121">Evite crear varios paneles en una pestaña, agregar capas de navegación o requerir que los usuarios se desplacen tanto vertical como horizontalmente en una pestaña. Es decir, intente no tener pestañas en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="df196-121">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="df196-122">Integración</span><span class="sxs-lookup"><span data-stu-id="df196-122">Integration</span></span>

<span data-ttu-id="df196-123">Obtenga información sobre cómo notificar a los usuarios la actividad de pestañas mediante el registro de [tarjetas adaptables](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) en una conversación.</span><span class="sxs-lookup"><span data-stu-id="df196-123">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="df196-124">Conversación</span><span class="sxs-lookup"><span data-stu-id="df196-124">Conversational</span></span>

<span data-ttu-id="df196-125">Buscar una forma de facilitar la conversación alrededor de una pestaña. Esto garantiza que las conversaciones se centran en el contenido, los datos o el proceso a mano.</span><span class="sxs-lookup"><span data-stu-id="df196-125">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="df196-126">Acceso simplificado</span><span class="sxs-lookup"><span data-stu-id="df196-126">Streamlined access</span></span>

<span data-ttu-id="df196-127">Asegúrese de que está concediendo acceso a las personas adecuadas en el momento adecuado.</span><span class="sxs-lookup"><span data-stu-id="df196-127">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="df196-128">Mantener simple el proceso de inicio de sesión evitará la creación de obstáculos a la contribución y la colaboración.</span><span class="sxs-lookup"><span data-stu-id="df196-128">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="df196-129">Capacidad de respuesta al tamaño de la ventana</span><span class="sxs-lookup"><span data-stu-id="df196-129">Responsiveness to window sizing</span></span>

<span data-ttu-id="df196-130">Los equipos se pueden usar en tamaños de ventana tan pequeños como 720px, por lo que es importante asegurarse de que una pestaña se puede usar en una ventana pequeña tan importante como el uso de resoluciones muy altas.</span><span class="sxs-lookup"><span data-stu-id="df196-130">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="df196-131">Navegación plana</span><span class="sxs-lookup"><span data-stu-id="df196-131">Flat navigation</span></span>

<span data-ttu-id="df196-132">Le pedimos a los desarrolladores que no agreguen todo su portal a una pestaña. Mantener la navegación relativamente plana ayuda a mantener un modelo de conversación más sencillo.</span><span class="sxs-lookup"><span data-stu-id="df196-132">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="df196-133">En otras palabras, la conversación trata sobre una lista de cosas, como los elementos de trabajo clasificados o de un solo elemento, como una especificación.</span><span class="sxs-lookup"><span data-stu-id="df196-133">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="df196-134">Hay desafíos de navegación inherentes a la jerarquía de navegación profunda en conversaciones encadenadas.</span><span class="sxs-lookup"><span data-stu-id="df196-134">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="df196-135">Para obtener la mejor experiencia del usuario, la navegación de la pestaña debe mantenerse al mínimo y diseñarse de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="df196-135">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="df196-136">**Abre un módulo de tareas como una entidad o elemento de trabajo individual**.</span><span class="sxs-lookup"><span data-stu-id="df196-136">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="df196-137">Esto excluye completamente el chat y es la mejor opción para mantener el chat específicamente sobre la ficha y no sobre las subentidades o la experiencia de edición.</span><span class="sxs-lookup"><span data-stu-id="df196-137">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="df196-138">**Abre un pseudo cuadro de diálogo en un iframe**.</span><span class="sxs-lookup"><span data-stu-id="df196-138">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="df196-139">Si se usa con un fondo con pantalla, se recomienda usar el color más claro en lugar del oscuro.</span><span class="sxs-lookup"><span data-stu-id="df196-139">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="df196-140">La `app-gray-10 at 30%` transparencia funciona bien.</span><span class="sxs-lookup"><span data-stu-id="df196-140">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="df196-141">**Abre una página del explorador**.</span><span class="sxs-lookup"><span data-stu-id="df196-141">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="df196-142">Personalidad</span><span class="sxs-lookup"><span data-stu-id="df196-142">Personality</span></span>

<span data-ttu-id="df196-143">El lienzo de pestañas ofrece una gran oportunidad para personalizar su experiencia.</span><span class="sxs-lookup"><span data-stu-id="df196-143">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="df196-144">Su logotipo es una parte importante de su identidad y su conexión con los usuarios de, por lo que debe asegurarse de incluirlo:</span><span class="sxs-lookup"><span data-stu-id="df196-144">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="df196-145">Poner el logotipo en la esquina izquierda o derecha o a lo largo del borde inferior</span><span class="sxs-lookup"><span data-stu-id="df196-145">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="df196-146">Mantener el logotipo en pequeña y discreta</span><span class="sxs-lookup"><span data-stu-id="df196-146">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="df196-147">La incorporación de sus propios colores y diseños Twill también ayuda para comunicar la personalidad.</span><span class="sxs-lookup"><span data-stu-id="df196-147">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="df196-148">Trabaje con nuestro estilo visual para que su servicio se sienta como parte de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="df196-148">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="df196-149">*Consulte* , por ejemplo, [colores de Teams](../../concepts/design/components/color.md)</span><span class="sxs-lookup"><span data-stu-id="df196-149">*See* , for example [Teams Colors](../../concepts/design/components/color.md)</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="df196-150">Diseños de pestañas</span><span class="sxs-lookup"><span data-stu-id="df196-150">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="df196-151">Tipos de pestañas</span><span class="sxs-lookup"><span data-stu-id="df196-151">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="df196-152">Alto de página de configuración</span><span class="sxs-lookup"><span data-stu-id="df196-152">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="df196-153">En septiembre de 2018, se incrementó el alto de la [Página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md) de pestañas mientras el ancho permaneció sin cambios.</span><span class="sxs-lookup"><span data-stu-id="df196-153">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="df196-154">Si la aplicación está diseñada para el tamaño anterior, la página de configuración de pestañas tendrá una gran cantidad de espacio en blanco vertical.</span><span class="sxs-lookup"><span data-stu-id="df196-154">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="df196-155">Las aplicaciones de la tienda heredadas exentas de este cambio tendrán que ponerse en contacto con Microsoft después de la actualización para acomodar las nuevas dimensiones.</span><span class="sxs-lookup"><span data-stu-id="df196-155">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="df196-156">Las dimensiones de la página de configuración de pestañas:</span><span class="sxs-lookup"><span data-stu-id="df196-156">The dimensions of the tab configuration page:</span></span>


<img width="450px" title="Tamaños de las pestañas de configuración" src="~/assets/images/tabs/config-dialog-Contoso2.png" alt="sizes for config tabs" />


### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="df196-158">Instrucciones para el formato de página de configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="df196-158">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="df196-159">Base el alto mínimo del área de contenido de la página de configuración de pestañas en elementos gráficos de altura fija.</span><span class="sxs-lookup"><span data-stu-id="df196-159">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="df196-160">Calcula el espacio vertical disponible (el alto del área de contenido en la página de configuración) mediante `window.innerHeight` .</span><span class="sxs-lookup"><span data-stu-id="df196-160">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="df196-161">Esto devuelve el tamaño del `<iframe>` en el que reside la página de configuración, lo que puede cambiar en futuras versiones.</span><span class="sxs-lookup"><span data-stu-id="df196-161">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="df196-162">Al usar este valor, el contenido se ajustará automáticamente a los cambios futuros.</span><span class="sxs-lookup"><span data-stu-id="df196-162">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="df196-163">Asigna espacio vertical a los elementos variable-height menos lo que se necesita para los elementos de altura fija.</span><span class="sxs-lookup"><span data-stu-id="df196-163">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="df196-164">Para el estado de *Inicio de sesión* , centrar vertical y horizontalmente el contenido.</span><span class="sxs-lookup"><span data-stu-id="df196-164">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="df196-165">Si desea una imagen de fondo, necesitará una nueva imagen, ajustada para ajustarse al área (recomendado) o puede conservar la misma imagen y elegir entre:</span><span class="sxs-lookup"><span data-stu-id="df196-165">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="df196-166">alineación a la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="df196-166">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="df196-167">escalar la imagen para ajustarla.</span><span class="sxs-lookup"><span data-stu-id="df196-167">scaling the image to fit.</span></span>

<span data-ttu-id="df196-168">Cuando esté correctamente ajustado, la página de configuración de pestaña debe tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="df196-168">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Nueva pestaña Configuración" src="~/assets/images/tabs/config-dialog-Contoso.png" alt="new config tab"/>

## <a name="best-practices"></a><span data-ttu-id="df196-170">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="df196-170">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="df196-171">Incluir siempre un estado predeterminado</span><span class="sxs-lookup"><span data-stu-id="df196-171">Always include a default state</span></span>

<span data-ttu-id="df196-172">Incluya un estado predeterminado para que las pestañas se puedan configurar fácilmente incluso si la pestaña se puede configurar.</span><span class="sxs-lookup"><span data-stu-id="df196-172">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="df196-173">Vinculación profunda</span><span class="sxs-lookup"><span data-stu-id="df196-173">Deep linking</span></span>

<span data-ttu-id="df196-174">Siempre que sea posible, las tarjetas y los bots deben tener un vínculo profundo a datos enriquecidos en una pestaña hospedada. Por ejemplo, puede que una tarjeta muestre un resumen de los datos de los errores, pero al hacer clic en él se muestra el error completo en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="df196-174">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="df196-175">Poner</span><span class="sxs-lookup"><span data-stu-id="df196-175">Naming</span></span>

<span data-ttu-id="df196-176">En muchos casos, el nombre de la aplicación tomará un nombre de pestaña excelente.</span><span class="sxs-lookup"><span data-stu-id="df196-176">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="df196-177">Pero, también considere la posibilidad de asignar un nombre a las pestañas según la funcionalidad que proporcionan.</span><span class="sxs-lookup"><span data-stu-id="df196-177">But, also consider naming your tabs according to the functionality they provide.</span></span>

### <a name="multi-window"></a><span data-ttu-id="df196-178">Varias ventanas</span><span class="sxs-lookup"><span data-stu-id="df196-178">Multi-window</span></span>

<span data-ttu-id="df196-179">Las pestañas de canal que tienen capacidades de edición complejas deben abrir la vista del editor en varias ventanas en lugar de en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="df196-179">Channel tabs that have complex editing capabilities must open the editor view in multi-window rather than a tab.</span></span>

### <a name="no-horizontal-scrolling"></a><span data-ttu-id="df196-180">Sin desplazamiento horizontal</span><span class="sxs-lookup"><span data-stu-id="df196-180">No horizontal scrolling</span></span>

<span data-ttu-id="df196-181">La pestaña no debe tener desplazamiento horizontal.</span><span class="sxs-lookup"><span data-stu-id="df196-181">Tab should not have horizontal scrolling.</span></span>

### <a name="easy-navigation"></a><span data-ttu-id="df196-182">Navegación sencilla</span><span class="sxs-lookup"><span data-stu-id="df196-182">Easy navigation</span></span>

<span data-ttu-id="df196-183">La navegación dentro de una aplicación de pestaña debe ser fácil de seguir, es decir, las páginas tienen lo siguiente en caso necesario o aplicable:</span><span class="sxs-lookup"><span data-stu-id="df196-183">Navigation inside a tab app must be easy to follow i.e. pages have the following where necessary/applicable:</span></span>
* <span data-ttu-id="df196-184">Botones atrás</span><span class="sxs-lookup"><span data-stu-id="df196-184">Back buttons</span></span>
* <span data-ttu-id="df196-185">Encabezados de página</span><span class="sxs-lookup"><span data-stu-id="df196-185">Page headers</span></span>
* <span data-ttu-id="df196-186">Las rutas</span><span class="sxs-lookup"><span data-stu-id="df196-186">Breadcrumbs</span></span>
* <span data-ttu-id="df196-187">Menús de hamburguesa</span><span class="sxs-lookup"><span data-stu-id="df196-187">Hamburger menus</span></span>

### <a name="undo-last-action"></a><span data-ttu-id="df196-188">Deshacer la última acción</span><span class="sxs-lookup"><span data-stu-id="df196-188">Undo last action</span></span>

<span data-ttu-id="df196-189">El usuario debe poder deshacer la última acción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df196-189">User must be able to undo their last action in the app.</span></span>

### <a name="share-content"></a><span data-ttu-id="df196-190">Compartir contenido</span><span class="sxs-lookup"><span data-stu-id="df196-190">Share content</span></span>

<span data-ttu-id="df196-191">Las aplicaciones personales deben permitir a los usuarios compartir contenido de una experiencia de la aplicación personal con otros miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="df196-191">Personal apps should enable users to share content from a personal app experience with other team members.</span></span> <span data-ttu-id="df196-192">La ficha canal debe proporcionar navegación que complemente la navegación principal de los equipos, en lugar de entrar en conflicto con ella (por ejemplo, barras de navegación de carril izquierda).</span><span class="sxs-lookup"><span data-stu-id="df196-192">Channel tab must provide navigation that complements the main Teams navigation, rather than conflicting with it (such as left rail nav-bars).</span></span>

### <a name="single-view"></a><span data-ttu-id="df196-193">Vista única</span><span class="sxs-lookup"><span data-stu-id="df196-193">Single view</span></span>

<span data-ttu-id="df196-194">Las aplicaciones personales deben presentar contenido de instancias de ámbito de chat de equipo o grupo de esa aplicación en una sola vista, por ejemplo, un usuario de Trello debe poder ver todas las instancias de las placas de Trello en las que participan en el nivel de equipo en su aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="df196-194">Personal apps should present content from team or group chat scoped instances of that app in a single view, e.g., a Trello user should be able to see all instances of Trello boards they participate in at a team level in their personal app.</span></span>

### <a name="no-app-bar"></a><span data-ttu-id="df196-195">Sin barra de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="df196-195">No app bar</span></span>

<span data-ttu-id="df196-196">Las pestañas no deben proporcionar una barra de aplicaciones con iconos en el carril de la izquierda que entran en conflicto con la navegación principal de los equipos.</span><span class="sxs-lookup"><span data-stu-id="df196-196">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>

### <a name="navigation"></a><span data-ttu-id="df196-197">Navegación</span><span class="sxs-lookup"><span data-stu-id="df196-197">Navigation</span></span>

<span data-ttu-id="df196-198">Las pestañas no deben tener más de 3 niveles de navegación dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df196-198">Tabs should not have more than 3 levels of navigation within the app.</span></span>

### <a name="l2l3-view"></a><span data-ttu-id="df196-199">Vista L2/L3</span><span class="sxs-lookup"><span data-stu-id="df196-199">L2/L3 view</span></span>

<span data-ttu-id="df196-200">Las páginas secundarias y terciarias de una ficha deben abrirse en una vista L2/L3 en el área de la pestaña principal que se desplaza a través de la ruta de navegación.</span><span class="sxs-lookup"><span data-stu-id="df196-200">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>

### <a name="no-link-to-external-browser"></a><span data-ttu-id="df196-201">Sin vínculo al explorador externo</span><span class="sxs-lookup"><span data-stu-id="df196-201">No link to external browser</span></span>

<span data-ttu-id="df196-202">Los destinos de vínculo de las pestañas no deben vincularse a un explorador externo, sino que deben vincularse a los elementos div contenidos dentro de los equipos, por ejemplo, dentro de módulos de tareas, pestañas, etc.</span><span class="sxs-lookup"><span data-stu-id="df196-202">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams, e.g., inside task Modules, tabs, etc.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="df196-203">Notificaciones para pestañas</span><span class="sxs-lookup"><span data-stu-id="df196-203">Notifications for tabs</span></span>

<span data-ttu-id="df196-204">Hay dos modos de notificación para cambios de contenido de pestañas:</span><span class="sxs-lookup"><span data-stu-id="df196-204">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="df196-205">**Use la API de aplicaciones para notificar a los usuarios los cambios**.</span><span class="sxs-lookup"><span data-stu-id="df196-205">**Use the app API to notify users of changes**.</span></span> <span data-ttu-id="df196-206">Este mensaje se mostrará en la fuente de actividad del usuario y un vínculo profundo a la ficha. *consulte*  [Create deep links to Content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span><span class="sxs-lookup"><span data-stu-id="df196-206">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span></span>

> * <span data-ttu-id="df196-207">**Usar un bot**.</span><span class="sxs-lookup"><span data-stu-id="df196-207">**Use a bot**.</span></span> <span data-ttu-id="df196-208">Este método es preferible especialmente si el subproceso de la pestaña es de destino.</span><span class="sxs-lookup"><span data-stu-id="df196-208">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="df196-209">El resultado será que la conversación encadenada de la pestaña se desplazará a la vista como activa recientemente.</span><span class="sxs-lookup"><span data-stu-id="df196-209">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="df196-210">Este método también permite una sofisticación en el modo en que se envía la notificación.</span><span class="sxs-lookup"><span data-stu-id="df196-210">This method also allows for some sophistication in how the notification is sent.</span></span>

<span data-ttu-id="df196-211">El envío de un mensaje a un subproceso de tabulación aumenta la conciencia de la actividad a todos los usuarios sin notificar explícitamente a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="df196-211">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="df196-212">Se trata de un reconocimiento sin ruido.</span><span class="sxs-lookup"><span data-stu-id="df196-212">This is awareness without noise.</span></span> <span data-ttu-id="df196-213">Además, cuando `@mention`  hay usuarios específicos, la misma notificación se colocará en la fuente, lo que hará que se vinculen directamente al hilo de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="df196-213">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>

### <a name="tab-design-best-practices"></a><span data-ttu-id="df196-214">Procedimientos recomendados de diseño de pestañas</span><span class="sxs-lookup"><span data-stu-id="df196-214">Tab design best practices</span></span>

* <span data-ttu-id="df196-215">Las pestañas personales/estáticas deben permitir a los usuarios compartir contenido de una experiencia de la aplicación personal con otros miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="df196-215">Personal/Static tabs should enable users to share content from a personal app experience with another team members.</span></span>
* <span data-ttu-id="df196-216">Las pestañas personales/estáticas pueden presentar contenido de instancias de ámbito de chat de equipo o grupo de esa aplicación en una sola vista.</span><span class="sxs-lookup"><span data-stu-id="df196-216">Personal/Static tabs may present content from team or group chat scoped instances of that app in a single view.</span></span>
* <span data-ttu-id="df196-217">Los destinos de vínculo de las pestañas no deben vincularse a un explorador externo, sino que deben vincularse a los elementos div incluidos en Teams (ejemplo: en los módulos de tareas, pestañas, etc.).</span><span class="sxs-lookup"><span data-stu-id="df196-217">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams (example-inside, task modules, tabs, etc).</span></span>
* <span data-ttu-id="df196-218">Las pestañas deben responder a los temas del equipo.</span><span class="sxs-lookup"><span data-stu-id="df196-218">Tabs should be responsive to Team’s themes.</span></span> <span data-ttu-id="df196-219">Cuando se cambia el tema de Teams, el tema de la aplicación también debe cambiar para reflejar ese tema.</span><span class="sxs-lookup"><span data-stu-id="df196-219">When the Teams theme is changed, the theme within the app should also change to reflect that theme.</span></span>
* <span data-ttu-id="df196-220">Las pestañas deben usar componentes con estilo de equipo siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="df196-220">Tabs should use Teams-styled components where possible.</span></span> <span data-ttu-id="df196-221">Significa adoptar las fuentes de Microsoft Teams, las rampas de tipos, las paletas de colores, el sistema de cuadrícula, el movimiento, el tono de la voz, etc.</span><span class="sxs-lookup"><span data-stu-id="df196-221">It means adopting Teams fonts, type ramps, color palettes, grid system, motion, tone of voice, etc.</span></span>
* <span data-ttu-id="df196-222">Las pestañas deben usar los comportamientos de interacción de Microsoft Teams para la navegación en las páginas, la posición y el uso de cuadros de diálogo, jerarquías de información, etc.</span><span class="sxs-lookup"><span data-stu-id="df196-222">Tabs should use Teams interaction behaviors for in-page navigation, position, and use of dialogs, information hierarchies, etc.</span></span>
* <span data-ttu-id="df196-223">Las pestañas deben usar el menú hamburguesa de los equipos estándar o la ruta de navegación para la navegación en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df196-223">Tabs should use the standard Teams hamburger menu and/or breadcrumb for in-app navigation.</span></span> <span data-ttu-id="df196-224">Las pestañas no deben proporcionar una barra de aplicaciones con iconos en el carril de la izquierda que entran en conflicto con la navegación principal de los equipos.</span><span class="sxs-lookup"><span data-stu-id="df196-224">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>
* <span data-ttu-id="df196-225">Las pestañas no deben tener más de tres niveles de navegación dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df196-225">Tabs should not have more than three levels of navigation within the app.</span></span>
* <span data-ttu-id="df196-226">Las páginas secundarias y terciarias de una ficha deben abrirse en una vista L2/L3 en el área de la pestaña principal que se desplaza a través de la ruta de navegación.</span><span class="sxs-lookup"><span data-stu-id="df196-226">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>
* <span data-ttu-id="df196-227">Las pestañas que tienen capacidades de edición complejas en la aplicación deben abrir la vista del editor en varias ventanas en lugar de en una pestaña (para escritorio y Web).</span><span class="sxs-lookup"><span data-stu-id="df196-227">Tabs that have complex editing capabilities within the app should open the editor view in multi-window rather than a tab (for desktop and web).</span></span>
