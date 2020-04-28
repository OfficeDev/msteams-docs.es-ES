---
title: Directrices de diseño para pestañas
description: Describe las instrucciones para crear pestañas de contenido y colaboración
keywords: Directrices de diseño de Microsoft Teams referencia de las fichas de marco de trabajo
ms.openlocfilehash: 342e01e348c74eb143391a7d238396a2d866766a
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914556"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="83a3e-104">Contenido y conversaciones, todos a la vez mediante pestañas</span><span class="sxs-lookup"><span data-stu-id="83a3e-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="83a3e-105">**Pestañas en clientes móviles**</span><span class="sxs-lookup"><span data-stu-id="83a3e-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="83a3e-106">Siga las [instrucciones para las pestañas de dispositivos móviles](./tabs-mobile.md) al crear las pestañas.</span><span class="sxs-lookup"><span data-stu-id="83a3e-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="83a3e-107">Si su pestaña usa autenticación, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 o posterior, o se producirá un error de autenticación.</span><span class="sxs-lookup"><span data-stu-id="83a3e-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="83a3e-108">**Pestañas personales (estáticas) en dispositivos móviles:**</span><span class="sxs-lookup"><span data-stu-id="83a3e-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="83a3e-109">Las pestañas estáticas (aplicación personal) están disponibles en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="83a3e-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="83a3e-110">Mientras crea las pestañas estáticas, asegúrese de seguir las [instrucciones para las pestañas de la móvil](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="83a3e-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="83a3e-111">**Pestañas de canal o grupo (configurable) en dispositivos móviles:**</span><span class="sxs-lookup"><span data-stu-id="83a3e-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="83a3e-112">Los clientes móviles solo muestran las pestañas que tienen `websiteUrl`un valor para.</span><span class="sxs-lookup"><span data-stu-id="83a3e-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="83a3e-113">Si desea que la pestaña aparezca en los clientes móviles de Teams, debe establecer el valor de `websiteUrl`.</span><span class="sxs-lookup"><span data-stu-id="83a3e-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="83a3e-114">El comportamiento predeterminado de apertura en dispositivos móviles es abrir fuera del explorador `websiteUrl`con el.</span><span class="sxs-lookup"><span data-stu-id="83a3e-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="83a3e-115">En el caso de las aplicaciones publicadas en la tienda de aplicaciones públicas, si desea que la ficha de canal se abra dentro de Teams de forma predeterminada, siga las [instrucciones para las pestañas de Mobile](~/tabs/design/tabs-mobile.md)y póngase en contacto con su representante de soporte técnico para que se le solicite que se le solicite que se le pida que</span><span class="sxs-lookup"><span data-stu-id="83a3e-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="83a3e-116">Las pestañas son lienzos que se pueden usar para compartir contenido, mantener conversaciones y hospedar servicios de terceros, todo ello dentro del flujo de trabajo ecológico de un equipo.</span><span class="sxs-lookup"><span data-stu-id="83a3e-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="83a3e-117">Cuando se crea una pestaña en Microsoft Teams, se coloca la aplicación web en su lugar y en el centro a la que se puede acceder fácilmente desde las conversaciones clave.</span><span class="sxs-lookup"><span data-stu-id="83a3e-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="83a3e-118">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="83a3e-118">Guidelines</span></span>

<span data-ttu-id="83a3e-119">Una buena pestaña debe mostrar las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="83a3e-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="83a3e-120">Funcionalidad centrada</span><span class="sxs-lookup"><span data-stu-id="83a3e-120">Focused functionality</span></span>

<span data-ttu-id="83a3e-121">Las pestañas funcionan mejor cuando se crean para satisfacer una necesidad específica.</span><span class="sxs-lookup"><span data-stu-id="83a3e-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="83a3e-122">Céntrese en un pequeño conjunto de tareas o en un subconjunto de datos que sea relevante para el canal en el que se encuentra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="83a3e-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="83a3e-123">Cromo reducido</span><span class="sxs-lookup"><span data-stu-id="83a3e-123">Reduced chrome</span></span>

<span data-ttu-id="83a3e-124">Evite crear varios paneles en una pestaña, agregar capas de navegación o requerir que los usuarios se desplacen tanto vertical como horizontalmente en una pestaña. Es decir, intente no tener pestañas en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="83a3e-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="83a3e-125">Integración</span><span class="sxs-lookup"><span data-stu-id="83a3e-125">Integration</span></span>

<span data-ttu-id="83a3e-126">Obtenga información sobre cómo notificar a los usuarios la actividad de pestañas mediante el registro de [tarjetas adaptables](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) en una conversación.</span><span class="sxs-lookup"><span data-stu-id="83a3e-126">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="83a3e-127">Conversación</span><span class="sxs-lookup"><span data-stu-id="83a3e-127">Conversational</span></span>

<span data-ttu-id="83a3e-128">Buscar una forma de facilitar la conversación alrededor de una pestaña. Esto garantiza que las conversaciones se centran en el contenido, los datos o el proceso a mano.</span><span class="sxs-lookup"><span data-stu-id="83a3e-128">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="83a3e-129">Acceso simplificado</span><span class="sxs-lookup"><span data-stu-id="83a3e-129">Streamlined access</span></span>

<span data-ttu-id="83a3e-130">Asegúrese de que está concediendo acceso a las personas adecuadas en el momento adecuado.</span><span class="sxs-lookup"><span data-stu-id="83a3e-130">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="83a3e-131">Mantener simple el proceso de inicio de sesión evitará la creación de obstáculos a la contribución y la colaboración.</span><span class="sxs-lookup"><span data-stu-id="83a3e-131">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="83a3e-132">Capacidad de respuesta al tamaño de la ventana</span><span class="sxs-lookup"><span data-stu-id="83a3e-132">Responsiveness to window sizing</span></span>

<span data-ttu-id="83a3e-133">Los equipos se pueden usar en tamaños de ventana tan pequeños como 720px, por lo que es importante asegurarse de que una pestaña se puede usar en una ventana pequeña tan importante como el uso de resoluciones muy altas.</span><span class="sxs-lookup"><span data-stu-id="83a3e-133">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="83a3e-134">Navegación plana</span><span class="sxs-lookup"><span data-stu-id="83a3e-134">Flat navigation</span></span>

<span data-ttu-id="83a3e-135">Se pide a los desarrolladores que no agreguen todo su portal a una pestaña. mantener la navegación relativamente plana ayuda a mantener un modelo de conversación más sencillo.</span><span class="sxs-lookup"><span data-stu-id="83a3e-135">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="83a3e-136">En otras palabras, la conversación trata sobre una lista de cosas, como los elementos de trabajo clasificados o de un solo elemento, como una especificación.</span><span class="sxs-lookup"><span data-stu-id="83a3e-136">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="83a3e-137">Hay desafíos de navegación inherentes a la jerarquía de navegación profunda en conversaciones encadenadas.</span><span class="sxs-lookup"><span data-stu-id="83a3e-137">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="83a3e-138">Para obtener la mejor experiencia del usuario, la navegación de la pestaña debe mantenerse al mínimo y diseñarse de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="83a3e-138">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="83a3e-139">**Abre un módulo de tareas como una entidad o elemento de trabajo individual**.</span><span class="sxs-lookup"><span data-stu-id="83a3e-139">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="83a3e-140">Esto excluye completamente el chat y es la mejor opción para mantener el chat específicamente sobre la ficha y no sobre las subentidades o la experiencia de edición.</span><span class="sxs-lookup"><span data-stu-id="83a3e-140">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="83a3e-141">**Abre un pseudo cuadro de diálogo en un iframe**.</span><span class="sxs-lookup"><span data-stu-id="83a3e-141">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="83a3e-142">Si se usa con un fondo con pantalla, se recomienda usar el color más claro en lugar del oscuro.</span><span class="sxs-lookup"><span data-stu-id="83a3e-142">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="83a3e-143">La `app-gray-10 at 30%` transparencia funciona bien.</span><span class="sxs-lookup"><span data-stu-id="83a3e-143">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="83a3e-144">**Abre una página del explorador**.</span><span class="sxs-lookup"><span data-stu-id="83a3e-144">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="83a3e-145">Personalidad</span><span class="sxs-lookup"><span data-stu-id="83a3e-145">Personality</span></span>

<span data-ttu-id="83a3e-146">El lienzo de pestañas ofrece una gran oportunidad para personalizar su experiencia.</span><span class="sxs-lookup"><span data-stu-id="83a3e-146">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="83a3e-147">Su logotipo es una parte importante de su identidad y su conexión con los usuarios de, por lo que debe asegurarse de incluirlo:</span><span class="sxs-lookup"><span data-stu-id="83a3e-147">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="83a3e-148">Poner el logotipo en la esquina izquierda o derecha o a lo largo del borde inferior</span><span class="sxs-lookup"><span data-stu-id="83a3e-148">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="83a3e-149">Mantener el logotipo en pequeña y discreta</span><span class="sxs-lookup"><span data-stu-id="83a3e-149">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="83a3e-150">La incorporación de sus propios colores y diseños Twill también ayuda para comunicar la personalidad.</span><span class="sxs-lookup"><span data-stu-id="83a3e-150">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="83a3e-151">Trabaje con nuestro estilo visual para que su servicio se sienta como parte de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="83a3e-151">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="83a3e-152">*Consulte*, por ejemplo, [colores de Microsoft Teams] (/Concepts/Design/Components/Typography.MD</span><span class="sxs-lookup"><span data-stu-id="83a3e-152">*See*, for example [Teams Colors](/concepts/design/components/typography.md</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="83a3e-153">Diseños de pestañas</span><span class="sxs-lookup"><span data-stu-id="83a3e-153">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="83a3e-154">Tipos de pestañas</span><span class="sxs-lookup"><span data-stu-id="83a3e-154">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="83a3e-155">Alto de página de configuración</span><span class="sxs-lookup"><span data-stu-id="83a3e-155">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="83a3e-156">En septiembre de 2018, se incrementó el alto de la [Página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md) de pestañas mientras el ancho permaneció sin cambios.</span><span class="sxs-lookup"><span data-stu-id="83a3e-156">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="83a3e-157">Si la aplicación está diseñada para el tamaño anterior, la página de configuración de pestañas tendrá una gran cantidad de espacio en blanco vertical.</span><span class="sxs-lookup"><span data-stu-id="83a3e-157">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="83a3e-158">Las aplicaciones de la tienda heredadas exentas de este cambio tendrán que ponerse en contacto con Microsoft después de la actualización para acomodar las nuevas dimensiones.</span><span class="sxs-lookup"><span data-stu-id="83a3e-158">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="83a3e-159">Las dimensiones de la página de configuración de pestañas:</span><span class="sxs-lookup"><span data-stu-id="83a3e-159">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="Tamaños de las pestañas de configuración" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="83a3e-161">Instrucciones para el formato de página de configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="83a3e-161">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="83a3e-162">Base el alto mínimo del área de contenido de la página de configuración de pestañas en elementos gráficos de altura fija.</span><span class="sxs-lookup"><span data-stu-id="83a3e-162">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="83a3e-163">Calcula el espacio vertical disponible (el alto del área de contenido en la página de configuración `window.innerHeight`) mediante.</span><span class="sxs-lookup"><span data-stu-id="83a3e-163">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="83a3e-164">Esto devuelve el tamaño del en `<iframe>` el que reside la página de configuración, lo que puede cambiar en futuras versiones.</span><span class="sxs-lookup"><span data-stu-id="83a3e-164">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="83a3e-165">Al usar este valor, el contenido se ajustará automáticamente a los cambios futuros.</span><span class="sxs-lookup"><span data-stu-id="83a3e-165">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="83a3e-166">Asigna espacio vertical a los elementos variable-height menos lo que se necesita para los elementos de altura fija.</span><span class="sxs-lookup"><span data-stu-id="83a3e-166">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="83a3e-167">Para el estado de *Inicio de sesión* , centrar vertical y horizontalmente el contenido.</span><span class="sxs-lookup"><span data-stu-id="83a3e-167">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="83a3e-168">Si desea una imagen de fondo, necesitará una nueva imagen, ajustada para ajustarse al área (recomendado) o puede conservar la misma imagen y elegir entre:</span><span class="sxs-lookup"><span data-stu-id="83a3e-168">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="83a3e-169">alineación a la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="83a3e-169">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="83a3e-170">escalar la imagen para ajustarla.</span><span class="sxs-lookup"><span data-stu-id="83a3e-170">scaling the image to fit.</span></span>

<span data-ttu-id="83a3e-171">Cuando esté correctamente ajustado, la página de configuración de pestaña debe tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="83a3e-171">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Nueva pestaña Configuración" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="83a3e-173">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="83a3e-173">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="83a3e-174">Incluir siempre un estado predeterminado</span><span class="sxs-lookup"><span data-stu-id="83a3e-174">Always include a default state</span></span>

<span data-ttu-id="83a3e-175">Incluya un estado predeterminado para que las pestañas se puedan configurar fácilmente incluso si la pestaña se puede configurar.</span><span class="sxs-lookup"><span data-stu-id="83a3e-175">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="83a3e-176">Vinculación profunda</span><span class="sxs-lookup"><span data-stu-id="83a3e-176">Deep linking</span></span>

<span data-ttu-id="83a3e-177">Siempre que sea posible, las tarjetas y los bots deben tener un vínculo profundo a datos enriquecidos en una pestaña hospedada. Por ejemplo, puede que una tarjeta muestre un resumen de los datos de los errores, pero al hacer clic en él se muestra el error completo en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="83a3e-177">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="83a3e-178">Poner</span><span class="sxs-lookup"><span data-stu-id="83a3e-178">Naming</span></span>

<span data-ttu-id="83a3e-179">En muchos casos, el nombre de la aplicación tomará un nombre de pestaña excelente.</span><span class="sxs-lookup"><span data-stu-id="83a3e-179">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="83a3e-180">Pero, también considere la posibilidad de asignar un nombre a las pestañas según la funcionalidad que proporcionan.</span><span class="sxs-lookup"><span data-stu-id="83a3e-180">But, also consider naming your tabs according to the functionality they provide.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="83a3e-181">Notificaciones para pestañas</span><span class="sxs-lookup"><span data-stu-id="83a3e-181">Notifications for tabs</span></span>

<span data-ttu-id="83a3e-182">Hay dos modos de notificación para cambios de contenido de pestañas:</span><span class="sxs-lookup"><span data-stu-id="83a3e-182">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="83a3e-183">**Use la API de aplicaciones para notificar a los usuarios los cambios**.</span><span class="sxs-lookup"><span data-stu-id="83a3e-183">**Use the app api to notify users of changes**.</span></span> <span data-ttu-id="83a3e-184">Este mensaje se mostrará en la fuente de actividad del usuario y un vínculo profundo a la ficha. *consulte*  [Create deep links to Content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest)</span><span class="sxs-lookup"><span data-stu-id="83a3e-184">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest)</span></span>
> * <span data-ttu-id="83a3e-185">**Usar un bot**.</span><span class="sxs-lookup"><span data-stu-id="83a3e-185">**Use a bot**.</span></span> <span data-ttu-id="83a3e-186">Este método es preferible especialmente si el subproceso de la pestaña es de destino.</span><span class="sxs-lookup"><span data-stu-id="83a3e-186">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="83a3e-187">El resultado será que la conversación encadenada de la pestaña se desplazará a la vista como activa recientemente.</span><span class="sxs-lookup"><span data-stu-id="83a3e-187">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="83a3e-188">Este método también permite una sofisticación en el modo en que se envía la notificación.</span><span class="sxs-lookup"><span data-stu-id="83a3e-188">This method also allows for some sophistication in how the notification is sent.</span></span>

  <span data-ttu-id="83a3e-189">El envío de un mensaje a un subproceso de tabulación aumenta la conciencia de la actividad a todos los usuarios sin notificar explícitamente a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="83a3e-189">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="83a3e-190">Se trata de un reconocimiento sin ruido.</span><span class="sxs-lookup"><span data-stu-id="83a3e-190">This is awareness without noise.</span></span> <span data-ttu-id="83a3e-191">Además, cuando hay usuarios `@mention` específicos, la misma notificación se colocará en la fuente, lo que hará que se vinculen directamente al hilo de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="83a3e-191">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>
