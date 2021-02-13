---
title: Plantillas de aplicación de Microsoft Teams
description: Vínculos y descripciones de plantillas de aplicación para la plataforma de Microsoft Teams
ms.topic: reference
keywords: Demostración de ejemplos de plantillas de Microsoft Teams
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 21721848ba7893380ac217b5f47ce6a6e669e869
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231641"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="05828-104">Plantillas de aplicación para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="05828-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="05828-105">Las plantillas de aplicación son ejemplos de aplicaciones completas para Microsoft Teams que son de código abierto y están disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="05828-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="05828-106">Cada plantilla de aplicación contiene instrucciones detalladas para implementar e instalar esa aplicación para la organización.</span><span class="sxs-lookup"><span data-stu-id="05828-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="05828-107">También proporciona una aplicación de ejemplo que puedes instalar y empezar a usar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="05828-107">It also provides a sample app that you can install and begin using immediately.</span></span> <span data-ttu-id="05828-108">El código fuente completo también está disponible, lo que le permite explorarlo en detalle o bifurcar el código y modificarlo para satisfacer sus requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="05828-108">The complete source code is available too, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="05828-109">Todas las plantillas de aplicación se proporcionan según los términos [de licencia de MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="05828-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>
>[!NOTE] 
><span data-ttu-id="05828-110">You, not Microsoft must license and support apps created from app templates for your users and organizations.</span><span class="sxs-lookup"><span data-stu-id="05828-110">You, not Microsoft must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="05828-111">**&#9734; indica las plantillas de aplicación recién publicadas.**</span><span class="sxs-lookup"><span data-stu-id="05828-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="05828-112">Ventajas clave</span><span class="sxs-lookup"><span data-stu-id="05828-112">Key benefits</span></span>

* <span data-ttu-id="05828-113">**Implemente directamente en la nube:** Todas las plantillas de aplicación incluyen scripts de implementación que le permiten hospedar todos los servicios necesarios en Microsoft Azure o power platform.</span><span class="sxs-lookup"><span data-stu-id="05828-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="05828-114">**Código de ejemplo recomendado:** Las plantillas de aplicación se ajustan a los procedimientos recomendados para la seguridad y la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="05828-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="05828-115">Todos los cambios enviados por la comunidad a las plantillas de aplicación se revisan para garantizar la conformidad.</span><span class="sxs-lookup"><span data-stu-id="05828-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="05828-116">**Personalizable y extensible:** Aunque todas las plantillas de aplicación se pueden implementar con una configuración mínima, proporcionamos la base de código completa y los scripts de implementación para que puedas personalizarlas o ampliarlas fácilmente para adaptarlas a tus necesidades únicas.</span><span class="sxs-lookup"><span data-stu-id="05828-116">**Customizable and extensible:** While all app templates can be deployed with minimal configuration, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="05828-117">**Documentación detallada:** Todas las plantillas de aplicación van acompañadas de documentación de un extremo a otro sobre la arquitectura de la solución, la implementación y los pasos de configuración.</span><span class="sxs-lookup"><span data-stu-id="05828-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot-9734"></a><span data-ttu-id="05828-118">Adopción de bot &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-118">Adoption Bot &#9734;</span></span>

<span data-ttu-id="05828-119">Bot de adopción es un bot de chat de atención al usuario creado con Power Virtual Agent para Teams (PVA).</span><span class="sxs-lookup"><span data-stu-id="05828-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams (PVA).</span></span> <span data-ttu-id="05828-120">Se puede considerar como la versión PVA de FAQPlus.</span><span class="sxs-lookup"><span data-stu-id="05828-120">It can be considered as the PVA version of FAQPlus.</span></span> <span data-ttu-id="05828-121">El bot de adopción responde a más de 100 preguntas comunes sobre Microsoft 365 y Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="05828-122">Puede editar los temas incluidos, agregar sus propios temas e ingerir preguntas frecuentes existentes.</span><span class="sxs-lookup"><span data-stu-id="05828-122">You can edit the included topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="05828-123">Si los usuarios necesitan ayuda adicional, el bot de adopción puede conectarlos a expertos o incluso extenderse para abrir vales de servicio con conectores de flujo premium.</span><span class="sxs-lookup"><span data-stu-id="05828-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span>

[<span data-ttu-id="05828-124">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-124">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="appointment-manager-9734"></a><span data-ttu-id="05828-125">Administrador de citas &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-125">Appointment Manager &#9734;</span></span>

<span data-ttu-id="05828-126">El Administrador de citas es una plantilla de aplicación de Teams para ayudar a las empresas a crear, administrar y llevar a cabo citas virtuales con los consumidores a través de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-126">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="05828-127">Las nuevas solicitudes de cita de los consumidores son visibles en los canales de Teams, donde se pueden asignar y reasignar rápidamente al personal de un equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-127">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="05828-128">Las solicitudes de cita se pueden ver en los niveles de equipo o personal a través de pestañas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="05828-128">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="05828-129">Cada cita está asociada a una reunión en línea de Teams, por lo que el personal y los consumidores pueden unirse fácilmente a la reunión en el momento programado.</span><span class="sxs-lookup"><span data-stu-id="05828-129">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="05828-130">La plantilla de aplicación se integra con Microsoft Bookings para facilitar la administración de citas.</span><span class="sxs-lookup"><span data-stu-id="05828-130">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="05828-131">Las citas programadas aparecen automáticamente en los calendarios de los miembros del personal asignados, y los consumidores reciben avisos y notificaciones por correo electrónico personalizables con vínculos de reunión incrustados.</span><span class="sxs-lookup"><span data-stu-id="05828-131">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="05828-132">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-132">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="05828-133">![Administrador de citas: Administrador de ](../assets/images/appointment-manager-overview.png)
 ![ citas de información general en Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="05828-133">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="05828-134">Preguntar</span><span class="sxs-lookup"><span data-stu-id="05828-134">Ask Away</span></span>

<span data-ttu-id="05828-135">Ask Away es un [bot de Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios llevar a cabo&A (preguntas y respuestas) dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-135">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="05828-136">Con el bot Ask Away, los miembros del equipo pueden enviar y votar preguntas compartidas por compañeros, lo que permite a los hosts de preguntas&A recopilar fácilmente preguntas de primer nivel dentro de un canal o chat.</span><span class="sxs-lookup"><span data-stu-id="05828-136">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="05828-137">El bot puede usarse para llevar a cabo una pregunta en tiempo real&una sesión en una reunión de Teams y permite a los asistentes enviar preguntas en directo a través del chat.</span><span class="sxs-lookup"><span data-stu-id="05828-137">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="05828-138">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-138">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Vista del cuadro de diálogo emergente de marcador para que los usuarios puedan votar preguntas](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="05828-140">Información de asociados</span><span class="sxs-lookup"><span data-stu-id="05828-140">Associate Insights</span></span>

<span data-ttu-id="05828-141">Associate Insights es una plantilla [de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que permite a los trabajadores de primera línea capturar y enviar directamente la opinión, la opinión y la percepción de los clientes.</span><span class="sxs-lookup"><span data-stu-id="05828-141">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="05828-142">Los trabajadores de primera línea suelen ser el primer representante de la compañía en interactuar con los clientes en un punto de contacto de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="05828-142">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="05828-143">Los equipos empresariales pueden compartir y usar los datos recopilados de forma colaborativa, por ejemplo, a través de una pestaña de Power BI Teams, para mejorar la experiencia del cliente y mejorar el producto.</span><span class="sxs-lookup"><span data-stu-id="05828-143">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="05828-144">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-144">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Vista de comentarios de información generada por la aplicación](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de Power BI de información generada por la aplicación](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="05828-147">Asistencia</span><span class="sxs-lookup"><span data-stu-id="05828-147">Attendance</span></span>

<span data-ttu-id="05828-148">La aplicación Asistencia es una [pestaña de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que se puede anclar en un equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-148">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="05828-149">Está diseñado para registrar la presencia, normalmente en configuraciones como entornos de aprendizaje y aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="05828-149">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="05828-150">Los usuarios pueden marcar o editar la asistencia hasta 30 días en el pasado y ver informes resumidos de asistencia para un grupo completo o asistentes individuales.</span><span class="sxs-lookup"><span data-stu-id="05828-150">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="05828-151">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-151">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Demostración de la aplicación de asistencia](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="05828-153">Libro a sala</span><span class="sxs-lookup"><span data-stu-id="05828-153">Book-a-room</span></span>

<span data-ttu-id="05828-154">Reservar una sala es un bot de [Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios buscar y reservar rápidamente una sala de reuniones durante 30 (valor predeterminado), 60 o 90 minutos a partir de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="05828-154">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="05828-155">El bot de libro a sala se incluye en las conversaciones personales o 1:1.</span><span class="sxs-lookup"><span data-stu-id="05828-155">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="05828-156">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-156">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Demostración de libro a salón](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="05828-158">Acceso de creación</span><span class="sxs-lookup"><span data-stu-id="05828-158">Building Access</span></span>

<span data-ttu-id="05828-159">Building Access es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que admite la administración de umbrales de ocupación y normas de distanciamiento social al permitir a los directores de instalaciones administrar, realizar un seguimiento y notificar la presencia en el sitio de los empleados.</span><span class="sxs-lookup"><span data-stu-id="05828-159">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="05828-160">La aplicación, creada con Microsoft [Power Apps](/powerapps/powerapps-overview)y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams y permite a las organizaciones determinar la preparación de la creación, establecer criterios de elegibilidad para el acceso en el sitio y recopilar información para la planeación futura.</span><span class="sxs-lookup"><span data-stu-id="05828-160">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="05828-161">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-161">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Crear una tarjeta de reserva de Access](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Creación de la vista de teclas de acceso](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="05828-164">Celebraciones</span><span class="sxs-lookup"><span data-stu-id="05828-164">Celebrations</span></span>

<span data-ttu-id="05828-165">Celebraciones es una aplicación de Teams que ayuda a los integrantes del equipo a celebrar su cumpleaños, aniversarios y otros eventos periódicos.</span><span class="sxs-lookup"><span data-stu-id="05828-165">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="05828-166">Recuerda ocasiones especiales de todos los miembros del equipo y envía un mensaje descriptivo en todos los equipos seleccionados en el momento de la creación del evento, para que los integrantes del equipo se sientan especiales en su día.</span><span class="sxs-lookup"><span data-stu-id="05828-166">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="05828-167">La aplicación proporciona una interfaz sencilla para que todos los miembros del equipo agreguen y visualmente sus eventos personalmente y también permite al usuario seleccionar los equipos en los que se comparten los eventos.</span><span class="sxs-lookup"><span data-stu-id="05828-167">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="05828-168">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-168">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="05828-169">Lista de comprobación</span><span class="sxs-lookup"><span data-stu-id="05828-169">Checklist</span></span>

<span data-ttu-id="05828-170">Lista de comprobación es una aplicación de extensión de mensajería [personalizada](../messaging-extensions/what-are-messaging-extensions.md) de Microsoft Teams que le permite colaborar con su equipo mediante la creación de una lista de comprobación compartida en un chat o canal.</span><span class="sxs-lookup"><span data-stu-id="05828-170">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="05828-171">La aplicación es compatible con todos los clientes de la plataforma teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="05828-171">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="05828-172">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-172">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Crear lista de comprobación en la vista Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a><span data-ttu-id="05828-174">Clase de &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-174">Classroom Drop-in &#9734;</span></span>

<span data-ttu-id="05828-175">Classroom Drop-in es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que permite a los líderes del sistema buscar equipos de clase (clases virtuales) y agregarse a sí mismos u otros a estos equipos de clase durante un período de entrega especificado, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05828-175">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="05828-176">La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate](/power-automate/getting-started)se integra profundamente con Microsoft Teams para garantizar que los centros educativos puedan optimizar sus operaciones en un entorno de aprendizaje híbrido proporcionando acceso a las partes interesadas relevantes para los equipos de clase por requisitos empresariales.</span><span class="sxs-lookup"><span data-stu-id="05828-176">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="05828-177">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-177">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Solicitud de acceso a clase](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="05828-179">Comunicador de la empresa</span><span class="sxs-lookup"><span data-stu-id="05828-179">Company Communicator</span></span>

<span data-ttu-id="05828-180">La aplicación Communicator empresa permite a los equipos corporativos crear y enviar mensajes destinados a varios equipos o a un gran número de empleados a través del chat, lo que permite que la organización llegue a los empleados justo donde colaboran.</span><span class="sxs-lookup"><span data-stu-id="05828-180">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="05828-181">Use esta plantilla para varios escenarios, como anuncios de nuevas iniciativas, incorporación de empleados, aprendizaje y desarrollo modernos o difusiones en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="05828-181">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="05828-182">La aplicación proporciona una interfaz sencilla para que los usuarios designados creen, obtengan una vista previa, colaboren y envíen mensajes.</span><span class="sxs-lookup"><span data-stu-id="05828-182">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="05828-183">Proporciona una base para crear capacidades de comunicación personalizadas dirigidas, como telemetría personalizada, sobre cuántos usuarios han reconocido o interactuado con un mensaje.</span><span class="sxs-lookup"><span data-stu-id="05828-183">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="05828-184">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-184">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![Vista de Communicator cuadro de redacción de jCompany](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="05828-186">Búsqueda de grupo de contactos</span><span class="sxs-lookup"><span data-stu-id="05828-186">Contact Group Lookup</span></span>

<span data-ttu-id="05828-187">La aplicación Búsqueda de grupos de contactos proporciona un enfoque práctico y útil para crear, obtener acceso y administrar los grupos de contactos de la organización (anteriormente conocidos como listas de distribución o grupos de comunicación).</span><span class="sxs-lookup"><span data-stu-id="05828-187">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="05828-188">Los usuarios pueden ver y chatear rápidamente con miembros del grupo, ver el estado de los miembros y crear un chat en grupo con miembros seleccionados en el grupo de contactos, todo ello dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-188">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="05828-189">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-189">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Vista favoritos anclados de búsqueda de grupo de contactos](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Demostración de chat de inicio de búsqueda de grupo de contactos](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation-9734"></a><span data-ttu-id="05828-192">Compañeros de trabajo &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-192">Co-worker Appreciation &#9734;</span></span>

<span data-ttu-id="05828-193">Con la plantilla de reconocimiento de compañeros de trabajo en Microsoft Teams, los usuarios pueden reconocer los logros de sus compañeros en el contexto de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-193">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="05828-194">Cuando los compañeros de trabajo seleccionan recompensar a un compañero, los destinatarios y otros miembros del equipo se etiquetan en una conversación de canal y reciben una notificación sobre los detalles de la distinción del canal.</span><span class="sxs-lookup"><span data-stu-id="05828-194">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="05828-195">Las distinciones se registran en la aplicación teams, que es segura, portátil y fácil de compartir.</span><span class="sxs-lookup"><span data-stu-id="05828-195">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="05828-196">Esto se puede considerar como la versión basada en PowerApps de la plantilla de aplicación Distintivos abiertos, con un marcador.</span><span class="sxs-lookup"><span data-stu-id="05828-196">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="05828-197">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-197">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![General](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="05828-199">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="05828-199">CrowdSourcer</span></span>

<span data-ttu-id="05828-200">CrowdSourcer es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona a los equipos información consultada procedente de forma colaborativa de los miembros del grupo.</span><span class="sxs-lookup"><span data-stu-id="05828-200">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="05828-201">Es una excelente manera de responder a las preguntas más frecuentes a la vez que permite a los participantes participar activamente y contribuir a un recurso de información divertido y útil.</span><span class="sxs-lookup"><span data-stu-id="05828-201">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="05828-202">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-202">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interacción entre usuarios finales de la fuente de concurrencia](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="05828-204">Adhesivos personalizados</span><span class="sxs-lookup"><span data-stu-id="05828-204">Custom Stickers</span></span>

<span data-ttu-id="05828-205">La autoexpresión es fundamental para una cultura de equipo en buen estado.</span><span class="sxs-lookup"><span data-stu-id="05828-205">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="05828-206">Esta plantilla de aplicación es una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) que permite a los usuarios usar adhesivos personalizados y GIF en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-206">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="05828-207">Esta plantilla proporciona una experiencia de configuración basada en web sencilla en la que cualquier usuario con acceso a la configuración puede cargar los GIF, adhesivos e imágenes que desean que tengan sus usuarios finales, lo que permite a todo el equipo usar cualquier conjunto de adhesivos que elija.</span><span class="sxs-lookup"><span data-stu-id="05828-207">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="05828-208">Esta aplicación también permite compartir fácilmente imágenes/GIF/adhesivos entre equipos sin necesidad de acceso a sitios de SharePoint o canales individuales como mecanismos de almacenamiento y uso compartido.</span><span class="sxs-lookup"><span data-stu-id="05828-208">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="05828-209">Por ejemplo, los equipos de productos pueden compartir fácilmente imágenes de producto y ARCHIVOS GIF en redes sociales, equipos de marketing y ventas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="05828-209">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="05828-210">También se puede ampliar esta aplicación desencadenando un flujo de notificación a equipos o individuos específicos cuando hay nuevas imágenes o GIF disponibles.</span><span class="sxs-lookup"><span data-stu-id="05828-210">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="05828-211">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-211">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Aplicación adhesivos](../assets/images/stickers.png)

## <a name="employee-ideas-9734"></a><span data-ttu-id="05828-213">Ideas para empleados &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-213">Employee Ideas &#9734;</span></span>

<span data-ttu-id="05828-214">La aplicación Ideas para empleados es la versión de PowerApps de la plantilla de aplicación Great Ideas basada en Azure.</span><span class="sxs-lookup"><span data-stu-id="05828-214">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="05828-215">La aplicación permite a los usuarios de Teams configurar y configurar una campaña de ideas.</span><span class="sxs-lookup"><span data-stu-id="05828-215">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="05828-216">Una campaña de ideas es una categoría para agrupar ideas en torno a temas comunes.</span><span class="sxs-lookup"><span data-stu-id="05828-216">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="05828-217">Los usuarios de Teams también pueden realizar las siguientes actividades:</span><span class="sxs-lookup"><span data-stu-id="05828-217">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="05828-218">Configura un formulario de envío estándar que los empleados necesitan enviar para cada idea.</span><span class="sxs-lookup"><span data-stu-id="05828-218">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="05828-219">Revisar y administrar las ideas y la lista de campañas.</span><span class="sxs-lookup"><span data-stu-id="05828-219">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="05828-220">Modificar y eliminar campañas.</span><span class="sxs-lookup"><span data-stu-id="05828-220">Modify and delete campaigns.</span></span>
* <span data-ttu-id="05828-221">Revisar los paneles de ideas principales.</span><span class="sxs-lookup"><span data-stu-id="05828-221">Review leader boards of ideas.</span></span>
* <span data-ttu-id="05828-222">Vota y comparte ideas priorizadas.</span><span class="sxs-lookup"><span data-stu-id="05828-222">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="05828-223">Enviar ideas para una campaña.</span><span class="sxs-lookup"><span data-stu-id="05828-223">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="05828-224">Ver la idea de otro miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-224">View other team member's idea.</span></span>
* <span data-ttu-id="05828-225">Vota sobre las ideas que más me gustaron.</span><span class="sxs-lookup"><span data-stu-id="05828-225">Vote on most liked ideas.</span></span>
* <span data-ttu-id="05828-226">Revisa el rendimiento de sus ideas en comparación con otras personas dentro de una campaña.</span><span class="sxs-lookup"><span data-stu-id="05828-226">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="05828-227">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-227">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Administrar la vista de campaña](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="05828-229">E-Prescriptions</span><span class="sxs-lookup"><span data-stu-id="05828-229">E-Prescriptions</span></span> 

<span data-ttu-id="05828-230">E-Prescriptions es una aplicación basada en [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)que mejora la salud virtual y la salud virtual mediante la automatización del proceso de emisión de e-prescriptions a los pacientes.</span><span class="sxs-lookup"><span data-stu-id="05828-230">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="05828-231">Los profesionales médicos pueden revisar rápidamente las citas, generar e-prescriptions y enviar correos electrónicos con datos adjuntos de la receta electrónica a los pacientes directamente dentro de la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-231">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="05828-232">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-232">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![Captura de pantalla de la aplicación E-Prescriptions.](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Captura de pantalla de la aplicación E-Prescriptions.](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a><span data-ttu-id="05828-237">Formación para empleados</span><span class="sxs-lookup"><span data-stu-id="05828-237">Employee Training</span></span> 

<span data-ttu-id="05828-238">La formación de los empleados es una aplicación de Microsoft Teams que permite a los organizadores publicar, realizar un seguimiento y promover fácilmente eventos de aprendizaje y aprendizaje para su organización.</span><span class="sxs-lookup"><span data-stu-id="05828-238">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="05828-239">Con la aplicación, los organizadores de eventos pueden enviar avisos y notificaciones a los registradores de eventos y los empleados pueden indicar interés en los próximos eventos, mantenerse actualizados sobre los eventos actuales y compartir detalles de eventos con compañeros a través de la extensión de mensajería de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-239">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="05828-240">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-240">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="05828-241">**Ver eventos de aprendizaje de empleados** ![ Imagen de la pestaña Formación para empleados](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="05828-241">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="05828-242">**Crear un evento de aprendizaje para empleados** ![ Formulario de creación de eventos de formación para empleados](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="05828-242">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="05828-243">Buscador de expertos</span><span class="sxs-lookup"><span data-stu-id="05828-243">Expert Finder</span></span>

<span data-ttu-id="05828-244">Expert Finder es un [bot de Microsoft Teams](../bots/what-are-bots.md) que identifica a miembros específicos de la organización en función de sus habilidades, intereses y atributos educativos.</span><span class="sxs-lookup"><span data-stu-id="05828-244">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="05828-245">Los miembros buscan expertos dentro de una organización que coinciden con una búsqueda de palabras clave de perfiles de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05828-245">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="05828-246">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-246">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Demostración de resultados de búsqueda del buscador de expertos](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="05828-248">Preguntas más frecuentes Plus</span><span class="sxs-lookup"><span data-stu-id="05828-248">FAQ Plus</span></span>

<span data-ttu-id="05828-249">Las preguntas conversacionales&Bots A son una forma sencilla de proporcionar respuestas a las preguntas más frecuentes de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="05828-249">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="05828-250">Sin embargo, la mayoría de los bots no interactúan con los usuarios de manera significativa porque no hay ninguna persona en el bucle cuando se produce un error en el bot.</span><span class="sxs-lookup"><span data-stu-id="05828-250">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="05828-251">Faq bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span><span class="sxs-lookup"><span data-stu-id="05828-251">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="05828-252">Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos.</span><span class="sxs-lookup"><span data-stu-id="05828-252">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="05828-253">Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde dentro del propio equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-253">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="05828-254">La versión más reciente de **FAQ Plus** admite las preguntas&A, ya que permite a un equipo de expertos completar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="05828-254">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="05828-255">&#x2714; agregar nuevas preguntas&como directamente a knowledge base mediante extensiones de mensaje.</span><span class="sxs-lookup"><span data-stu-id="05828-255">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="05828-256">&#x2714; editar y eliminar preguntas&pares A agregados por un bot.</span><span class="sxs-lookup"><span data-stu-id="05828-256">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="05828-257">&#x2714; seguimiento del historial de revisiones de las preguntas&as.</span><span class="sxs-lookup"><span data-stu-id="05828-257">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="05828-258">&#x2714; configurar una respuesta con detalles adicionales para mostrar como una [tarjeta adaptable.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="05828-258">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="05828-259">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-259">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Preguntas más frecuentes y gif](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app-9734"></a><span data-ttu-id="05828-261">Obtener la aplicación de soporte &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-261">Get Support App &#9734;</span></span>

<span data-ttu-id="05828-262">Las organizaciones que usan Microsoft Teams pueden usar la aplicación Obtener soporte técnico para permitir que cualquier conjunto de usuarios solicite asistencia a los supervisores.</span><span class="sxs-lookup"><span data-stu-id="05828-262">The Get Support app can be used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="05828-263">Esta aplicación incluye varias características, como:</span><span class="sxs-lookup"><span data-stu-id="05828-263">This app includes various features, such as:</span></span>
-   <span data-ttu-id="05828-264">Solicitar asistencia en distintas categorías desde una Power App</span><span class="sxs-lookup"><span data-stu-id="05828-264">Requesting assistance on different categories from a Power App</span></span>
-   <span data-ttu-id="05828-265">Notificaciones enviadas a los solicitantes en las que se les informa de quién se ha asignado</span><span class="sxs-lookup"><span data-stu-id="05828-265">Notifications sent to requestors informing them of who has been assigned</span></span> 
-   <span data-ttu-id="05828-266">Notificaciones enviadas a supervisores asignados en las que se les informa de quién necesita asistencia</span><span class="sxs-lookup"><span data-stu-id="05828-266">Notifications sent to assigned supervisors informing them of who needs assistance</span></span> 
-   <span data-ttu-id="05828-267">Análisis de escalaciones y patrones en SharePoint y PowerBI</span><span class="sxs-lookup"><span data-stu-id="05828-267">Analyzing escalations and patterns in SharePoint and PowerBI</span></span>

[<span data-ttu-id="05828-268">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-268">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Obtener gif de soporte técnico](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="05828-270">Rastreador de objetivos</span><span class="sxs-lookup"><span data-stu-id="05828-270">Goal Tracker</span></span>

<span data-ttu-id="05828-271">La aplicación Rastreador de objetivos es una solución completa para que su organización admita el establecimiento de objetivos, el progreso y el reconocimiento del éxito en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-271">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="05828-272">La aplicación permite a los usuarios establecer, realizar un seguimiento y actualizar los objetivos en un nivel profesional, personal y de equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-272">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="05828-273">Los miembros del equipo también reciben avisos y actualizaciones de estado a tiempo para mantenerse centrados y mantenerse al día.</span><span class="sxs-lookup"><span data-stu-id="05828-273">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="05828-274">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![Establecer objetivos](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Ver objetivos establecidos](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="05828-277">Ideas excelentes</span><span class="sxs-lookup"><span data-stu-id="05828-277">Great Ideas</span></span>

<span data-ttu-id="05828-278">La aplicación Great Ideas admite y fomenta la innovación y la creatividad dentro de la organización.</span><span class="sxs-lookup"><span data-stu-id="05828-278">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="05828-279">La aplicación permite a los empleados compartir ideas con compañeros y líderes, descubrir nuevos envíos, destacar contribuciones para la consideración del mismo nivel y emitir su voto a favor de las mejores propuestas dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-279">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="05828-280">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-280">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

:::row:::
  :::column span="2":::
    ![Ver ideas enviadas](../assets/images/great-ideas-all-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Ver ideas](../assets/images/great-ideas-digest-view.png)
:::column-end:::
:::row-end:::

## <a name="group-activities"></a><span data-ttu-id="05828-283">Actividades de grupo</span><span class="sxs-lookup"><span data-stu-id="05828-283">Group Activities</span></span>

<span data-ttu-id="05828-284">Actividades de grupo es una aplicación de Microsoft Teams que facilita a los propietarios del equipo la creación rápida de grupos de actividades y la administración de flujos de trabajo de colaboración en el contexto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-284">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="05828-285">Los autores de actividades están habilitados para crear actividades, distribuir aleatoriamente a los miembros del equipo en grupos y, opcionalmente, hacer que el bot envíe avisos hasta que se completen las actividades.</span><span class="sxs-lookup"><span data-stu-id="05828-285">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="05828-286">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-286">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Lista de actividades de grupo en Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Mensaje de notificación de actividad de grupo en un canal](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a><span data-ttu-id="05828-289">Hacer crecer tus habilidades</span><span class="sxs-lookup"><span data-stu-id="05828-289">Grow Your Skills</span></span>

<span data-ttu-id="05828-290">La aplicación Grow Your Skills admite el crecimiento y el desarrollo profesional al permitir que los empleados contribuyan a proyectos complementarios para tu organización mientras se aprende nuevas habilidades al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="05828-290">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="05828-291">Los empleados pueden usar la aplicación para buscar oportunidades que satisfagan sus intereses, disfrutar de una colaboración significativa con compañeros y adquirir nuevos niveles de experiencia y capacidades, todo ello dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-291">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="05828-292">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-292">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Vista de proyectos disponibles](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de aptitudes adquiridas del visor](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="05828-295">Soporte de Recursos Humanos</span><span class="sxs-lookup"><span data-stu-id="05828-295">HR Support</span></span>

<span data-ttu-id="05828-296">El bot de soporte técnico de RECURSOS humanos es una pregunta&un bot que pone en marcha a un profesional o experto de soporte técnico del equipo de recursos humanos cuando no puede ayudar.</span><span class="sxs-lookup"><span data-stu-id="05828-296">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="05828-297">Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos.</span><span class="sxs-lookup"><span data-stu-id="05828-297">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="05828-298">Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que son de ayuda para proporcionar soporte al actuar sobre las notificaciones desde dentro de su propio equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-298">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="05828-299">Además, el bot sugiere vínculos a preguntas y directivas de RECURSOS humanos recomendadas mediante la búsqueda de etiquetas preconfiguradas en la pregunta.</span><span class="sxs-lookup"><span data-stu-id="05828-299">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="05828-300">Estos iconos también se pueden encontrar en la pestaña asociada como referencia rápida.</span><span class="sxs-lookup"><span data-stu-id="05828-300">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="05828-301">El soporte técnico de RECURSOS humanos funciona bien para QnA ligero y para proporcionar soporte rápido al iniciar nuevos proyectos o iniciativas en la organización.</span><span class="sxs-lookup"><span data-stu-id="05828-301">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="05828-302">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-302">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Soporte de Recursos Humanos](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="05828-304">Rompehielo</span><span class="sxs-lookup"><span data-stu-id="05828-304">Icebreaker</span></span>

<span data-ttu-id="05828-305">Icebreaker es un bot de [Microsoft Teams](../bots/what-are-bots.md) que ayuda a su equipo a acercarse al emparejar a dos miembros aleatorios del equipo cada semana para reunirse.</span><span class="sxs-lookup"><span data-stu-id="05828-305">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="05828-306">El bot facilita la programación al sugerir automáticamente horas libres que funcionen para ambos miembros.</span><span class="sxs-lookup"><span data-stu-id="05828-306">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="05828-307">Refuerza las conexiones personales y crea una comunidad estrechamente apretada con esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="05828-307">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="05828-308">Además de fomentar las conexiones personales en todo el equipo, la aplicación Icebreaker puede ayudar a desarrollar comunidades basadas en intereses dentro de la organización.</span><span class="sxs-lookup"><span data-stu-id="05828-308">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="05828-309">Por ejemplo, puedes usar esta aplicación para un grupo de interés de DevOps para ayudar a que las ideas y los procedimientos recomendados se extienda de forma orgánica en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="05828-309">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="05828-310">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-310">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Aplicación Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="05828-312">Incentivos</span><span class="sxs-lookup"><span data-stu-id="05828-312">Incentives</span></span>

<span data-ttu-id="05828-313">Incentivos es una [plantilla de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que administra y realiza un seguimiento de la participación de los empleados incentivos en actividades designadas, como cursos e iniciativas de administración de cambios.</span><span class="sxs-lookup"><span data-stu-id="05828-313">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="05828-314">Los administradores usan la aplicación para establecer actividades designadas, asignar puntos para su finalización y especificar los niveles de puntos de elegibilidad necesarios para las recompensas.</span><span class="sxs-lookup"><span data-stu-id="05828-314">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="05828-315">Los empleados usan la aplicación para ver sus puntos acumulados y, al alcanzar la elegibilidad, solicitar y reclamar recompensas canjeables.</span><span class="sxs-lookup"><span data-stu-id="05828-315">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="05828-316">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-316">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Demostración de la aplicación de incentivos](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="05828-318">Incident Reporter</span><span class="sxs-lookup"><span data-stu-id="05828-318">Incident Reporter</span></span>

<span data-ttu-id="05828-319">Incident Reporter es un [bot de Microsoft Teams](../bots/what-are-bots.md)  que optimiza la administración de incidentes en su organización.</span><span class="sxs-lookup"><span data-stu-id="05828-319">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="05828-320">El bot facilita la recopilación automatizada de datos de incidentes, informes de incidentes personalizados, notificaciones relevantes para las partes interesadas y seguimiento de incidentes de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="05828-320">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="05828-321">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-321">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Vista de ámbito de grupo de informante de incidentes](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de ámbito personal del reportero de incidentes](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection-9734"></a><span data-ttu-id="05828-324">Inspección &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-324">Inspection &#9734;</span></span>

 <span data-ttu-id="05828-325">La inspección es una aplicación de Microsoft Teams que permite a los trabajadores de primera línea inspeccionar cualquier cosa, desde ubicaciones hasta activos y equipos.</span><span class="sxs-lookup"><span data-stu-id="05828-325">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="05828-326">Por ejemplo, una tienda comercial, una fábrica de fabricación o vehículos y máquinas.</span><span class="sxs-lookup"><span data-stu-id="05828-326">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="05828-327">Hay dos aplicaciones en esta solución, cada una destinada a distintos tipos de usuarios.</span><span class="sxs-lookup"><span data-stu-id="05828-327">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="05828-328">La aplicación permite a los trabajadores de primera línea inspeccionar un activo o área, administrar la calidad de productos y servicios o mantener la seguridad en el lugar de trabajo.</span><span class="sxs-lookup"><span data-stu-id="05828-328">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="05828-329">Facilita la comunicación entre los miembros del equipo para solucionar los problemas encontrados durante la inspección.</span><span class="sxs-lookup"><span data-stu-id="05828-329">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="05828-330">La aplicación proporciona informes sencillos a los administradores para acelerar la resolución de problemas y resaltar tendencias.</span><span class="sxs-lookup"><span data-stu-id="05828-330">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="05828-331">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-331">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Introducción a la inspección](../assets/images/inspection-app.png)  


## <a name="issue-reporting-9734"></a><span data-ttu-id="05828-333">Informes de problemas &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-333">Issue Reporting &#9734;</span></span>

<span data-ttu-id="05828-334">La aplicación De informes de problemas permite a los empleados y administradores generar y administrar problemas.</span><span class="sxs-lookup"><span data-stu-id="05828-334">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="05828-335">Consta de dos aplicaciones: aplicación de informes de problemas para informar de problemas y aplicación Administrar problemas para administrar problemas.</span><span class="sxs-lookup"><span data-stu-id="05828-335">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="05828-336">Los administradores del equipo usan la aplicación Administrar problemas para configurar la experiencia de la aplicación, incluido el canal en el que la aplicación crea los mensajes de Microsoft Teams y las tareas de Planner.</span><span class="sxs-lookup"><span data-stu-id="05828-336">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="05828-337">Los administradores también usan la aplicación para crear formularios de plantilla para recopilar detalles cuando un usuario informa de un problema.</span><span class="sxs-lookup"><span data-stu-id="05828-337">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="05828-338">Por ejemplo, revisar, editar o eliminar formularios de plantilla de problema.</span><span class="sxs-lookup"><span data-stu-id="05828-338">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="05828-339">La aplicación también se puede usar para revisar los problemas del equipo, informar sobre el historial de problemas y administrar de forma eficaz la resolución de problemas.</span><span class="sxs-lookup"><span data-stu-id="05828-339">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="05828-340">Los empleados usan la aplicación De informes de problemas para registrar problemas y detalles necesarios para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="05828-340">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="05828-341">La aplicación también se usa para modificar y resolver problemas existentes y obtener una vista de alto nivel de problemas individuales o de equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-341">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="05828-342">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-342">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Vista de equipo de informes de problemas](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="05828-344">Incorporación de nuevos empleados</span><span class="sxs-lookup"><span data-stu-id="05828-344">New Employee Onboarding</span></span> 

<span data-ttu-id="05828-345">La incorporación de nuevos empleados es una solución integrada de incorporación de nuevos empleados de Microsoft Teams y [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) que permite a su organización proporcionar una experiencia de incorporación coherente y de alta calidad para los empleados en su viaje de nuevos empleados.</span><span class="sxs-lookup"><span data-stu-id="05828-345">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="05828-346">Los equipos de recursos humanos y los administradores de contratación pueden usar la aplicación para proporcionar información relevante durante todo el proceso de orientación y orientación, así como para que los nuevos empleados compartan comentarios, proporcionen introducciones y completen las tareas de incorporación.</span><span class="sxs-lookup"><span data-stu-id="05828-346">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="05828-347">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-347">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="05828-348">**Tarjeta de bienvenida de nuevo empleado** ![ Imagen de la tarjeta de bienvenida del nuevo empleado](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="05828-348">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="05828-349">**Lista de comprobación de nuevos empleados** ![ Imagen de la lista de comprobación de nuevos empleados](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="05828-349">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="05828-350">Distintivos abiertos</span><span class="sxs-lookup"><span data-stu-id="05828-350">Open Badges</span></span>

<span data-ttu-id="05828-351">Open Badges es una aplicación de Microsoft Teams que permite a los usuarios obtener distintivos de credenciales de aprendizaje digital en el contexto de Teams y compartirlos en todas partes.</span><span class="sxs-lookup"><span data-stu-id="05828-351">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="05828-352">Con las funcionalidades de la autoridad emisora de distintivos digitales de terceros, [Badgr](https://badgr.org/), los distintivos concedidos se registran en el perfil Badgr de un destinatario y están disponibles para crear y compartir una imagen enriquecida de los recorridos de aprendizaje de toda la vida.</span><span class="sxs-lookup"><span data-stu-id="05828-352">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="05828-353">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![Imagen de distintivos disponibles](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de distintivos concedidos](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="05828-356">Sondeo</span><span class="sxs-lookup"><span data-stu-id="05828-356">Poll</span></span> 

<span data-ttu-id="05828-357">El sondeo es una aplicación de extensión de mensajería personalizada de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que le permite crear y enviar rápidamente sondeos en un chat o un canal para recopilar opiniones y preferencias del equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-357">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="05828-358">La aplicación es compatible con todos los clientes de la plataforma teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="05828-358">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="05828-359">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-359">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Crear sondeo en la vista Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="05828-361">Respuestas rápidas</span><span class="sxs-lookup"><span data-stu-id="05828-361">Quick Responses</span></span>

<span data-ttu-id="05828-362">Respuestas rápidas es una aplicación de Microsoft Teams que ofrece una solución sólida para responder eficazmente a las preguntas más frecuentes (PREGUNTAS FRECUENTES) de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="05828-362">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="05828-363">En lugar de responder a cada consulta de forma manual y continua, la aplicación compilará una biblioteca de respuestas para una experiencia de usuario interactiva a través de extensiones de [mensajería de](../messaging-extensions/what-are-messaging-extensions.md)Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-363">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="05828-364">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Vista de ejemplo de respuestas](../assets/images/quick-responses.png)

## <a name="rapid-assist-9734"></a><span data-ttu-id="05828-366">Asistencia rápida &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-366">Rapid Assist &#9734;</span></span>

<span data-ttu-id="05828-367">Asistencia rápida es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que permite a los asociados orientados al cliente conectarse rápidamente con los expertos para obtener respuestas rápidas, buscar información, hacer un seguimiento de las solicitudes abiertas y permitir que los expertos reciban notificaciones para recibir rápidamente una llamada para ayudar a responder preguntas.</span><span class="sxs-lookup"><span data-stu-id="05828-367">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="05828-368">La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate](/power-automate/getting-started)se integra profundamente con Microsoft Teams para permitir que las organizaciones conecten fácilmente a los trabajadores de primera línea con enlaces corporativos para resolver las consultas de los clientes y ofrecer una experiencia de cliente excelente.</span><span class="sxs-lookup"><span data-stu-id="05828-368">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="05828-369">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Interfaz de solicitud de usuario final](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Vista de solicitud de experto](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="05828-372">Reflejar</span><span class="sxs-lookup"><span data-stu-id="05828-372">Reflect</span></span> 

<span data-ttu-id="05828-373">Reflect es una aplicación de extensión de mensajería personalizada de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que proporciona un recurso seguro e inclusivo para que los miembros del equipo compartan el estado de su bienestar emocional con compañeros o líderes de grupo directamente dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-373">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="05828-374">La aplicación está disponible en chats de canal, grupo, reunión y 1:1, y la respuesta de la comprobación puede establecerse en pública, privada a remitente o totalmente anónima.</span><span class="sxs-lookup"><span data-stu-id="05828-374">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="05828-375">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="05828-376">**Sondeo de buen estado**</span><span class="sxs-lookup"><span data-stu-id="05828-376">**Well-being poll**</span></span>
    
    ![Reflejar el sondeo del usuario de la aplicación](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="05828-378">Soporte remoto</span><span class="sxs-lookup"><span data-stu-id="05828-378">Remote Support</span></span>

<span data-ttu-id="05828-379">El soporte remoto es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona una interfaz centrada entre los solicitantes de soporte técnico de toda la organización y el equipo de soporte interno.</span><span class="sxs-lookup"><span data-stu-id="05828-379">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="05828-380">Los usuarios finales pueden enviar, editar o retirar solicitudes de soporte técnico y el equipo de soporte técnico puede responder, administrar y actualizar solicitudes en la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-380">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="05828-381">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![Formulario de solicitud de soporte técnico](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Solicitar detalles de soporte técnico](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="05828-384">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="05828-384">Request-a-team</span></span>

<span data-ttu-id="05828-385">Request-a-team es una aplicación de Microsoft Teams que optimiza la creación de nuevos equipos para su organización empresarial.</span><span class="sxs-lookup"><span data-stu-id="05828-385">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="05828-386">La aplicación admite la normalización y los procedimientos recomendados al crear nuevas instancias de equipo mediante la integración de un formulario de solicitud guiado por el asistente, un proceso de aprobación incrustado, un panel de estado de solicitud y compilaciones automatizadas del equipo.</span><span class="sxs-lookup"><span data-stu-id="05828-386">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="05828-387">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-387">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Vista de página de inicio de solicitud a equipo](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de página del Asistente para solicitud de equipo](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="05828-390">Scrums para canales</span><span class="sxs-lookup"><span data-stu-id="05828-390">Scrums for Channels</span></span>

<span data-ttu-id="05828-391">Scrums para canales es una aplicación de asistente de scrum que permite a los usuarios programar y ejecutar scrums en canales de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-391">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="05828-392">La aplicación es ideal para equipos remotos y equipos formados por miembros de diversas ubicaciones geográficas y zonas horarias para compartir actualizaciones diarias y garantizar la participación en reuniones de soporte de scrum.</span><span class="sxs-lookup"><span data-stu-id="05828-392">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="05828-393">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="05828-394">Para llevar a cabo reuniones de scrum en un chat en grupo, consulte nuestra plantilla de [aplicación Scrums para chat](#scrums-for-group-chat) en grupo.</span><span class="sxs-lookup"><span data-stu-id="05828-394">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![Scrums para la vista de configuración de canales](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrums para la vista de estado del miembro del equipo de canales](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="05828-397">Scrums para chat en grupo</span><span class="sxs-lookup"><span data-stu-id="05828-397">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="05828-398">La plantilla de aplicación Estado de Scrums se ha actualizado y ahora es Scrums para chat en grupo.</span><span class="sxs-lookup"><span data-stu-id="05828-398">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="05828-399">Scrums para chat en grupo es un ayudante de scrum de apoyo que permite a los miembros del chat grupal ejecutar reuniones de pie asincrónicas y compartir fácilmente sus actualizaciones diarias.</span><span class="sxs-lookup"><span data-stu-id="05828-399">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="05828-400">Permite a todos los miembros del chat de grupo contribuir al scrum y ver las actualizaciones realizadas por otros usuarios en el scrum en ejecución.</span><span class="sxs-lookup"><span data-stu-id="05828-400">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="05828-401">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-401">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Demostración de Scrums para chat en grupo](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="05828-403">Compartir ahora</span><span class="sxs-lookup"><span data-stu-id="05828-403">Share Now</span></span> 

<span data-ttu-id="05828-404">La aplicación Compartir ahora promueve el intercambio positivo de información entre compañeros al permitir que los usuarios compartan fácilmente contenido dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-404">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="05828-405">Los usuarios interactúan con la aplicación para compartir elementos de interés con los miembros del equipo, descubrir nuevo contenido compartido, establecer preferencias y marcar favoritos para su posterior lectura.</span><span class="sxs-lookup"><span data-stu-id="05828-405">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="05828-406">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-406">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Seleccionar vista de contenido](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="05828-408">Búsqueda de lista de SharePoint</span><span class="sxs-lookup"><span data-stu-id="05828-408">SharePoint List Search</span></span>

<span data-ttu-id="05828-409">La colaboración en Microsoft Teams suele hacer referencia a la información contenida en los elementos de una lista de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="05828-409">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="05828-410">Simplemente pegar un vínculo al elemento en cuestión obliga a todos a cambiar el contexto de la conversación, buscar la información necesaria y, a continuación, volver a Teams para continuar la conversación.</span><span class="sxs-lookup"><span data-stu-id="05828-410">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="05828-411">A medida que continúa la conversación, normalmente los usuarios tendrán que volver al elemento de referencia varias veces para comprobar los nuevos comentarios y actualizar sus comentarios de la información contenida en el elemento.</span><span class="sxs-lookup"><span data-stu-id="05828-411">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="05828-412">Este cambio de contexto crea una barrera para una colaboración fluida y es una receta para las cosas que se atraviesan por las fisuras.</span><span class="sxs-lookup"><span data-stu-id="05828-412">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="05828-413">Para ayudar a mitigar este problema, estamos encantados de traerle la plantilla de aplicación Búsqueda de lista.</span><span class="sxs-lookup"><span data-stu-id="05828-413">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="05828-414">Millones de usuarios usan SharePoint para crear algunos de los flujos de trabajo principales de sus organizaciones.</span><span class="sxs-lookup"><span data-stu-id="05828-414">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="05828-415">Sin embargo, la colaboración en las listas puede ser especialmente tediosa.</span><span class="sxs-lookup"><span data-stu-id="05828-415">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="05828-416">Con la plantilla de aplicación Búsqueda de lista en Microsoft Teams, los usuarios pueden insertar información de elementos de lista de SharePoint directamente dentro de una conversación de chat para aliviar el cambio de contexto causado al insertar simplemente un vínculo en un chat.</span><span class="sxs-lookup"><span data-stu-id="05828-416">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="05828-417">La información se inserta como una tarjeta con formato automático fácil de leer, lo que ayuda a los usuarios a mantener la participación en la conversación.</span><span class="sxs-lookup"><span data-stu-id="05828-417">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="05828-418">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-418">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Aplicación de búsqueda de lista](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="05828-420">Check-ins del personal</span><span class="sxs-lookup"><span data-stu-id="05828-420">Staff Check-ins</span></span>

<span data-ttu-id="05828-421">Las protección del personal son una aplicación basada en [Power Apps](/powerapps/powerapps-overview)que permite la comunicación de supervisión entre su empresa y el personal de campo.</span><span class="sxs-lookup"><span data-stu-id="05828-421">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="05828-422">El personal puede proporcionar fácilmente información crítica y actualizaciones de estado de forma programada o ad-hoc directamente desde Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-422">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="05828-423">La aplicación admite la ubicación en tiempo real, fotos y notas, así como notificaciones de aviso y flujos de trabajo automatizados.</span><span class="sxs-lookup"><span data-stu-id="05828-423">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="05828-424">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-424">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Crear vista de comprobación](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="05828-426">Encuesta</span><span class="sxs-lookup"><span data-stu-id="05828-426">Survey</span></span>

<span data-ttu-id="05828-427">La encuesta es una aplicación personalizada de extensión de mensajería de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que le permite crear una encuesta en un chat o un canal para recopilar datos y obtener información que se puede realizar.</span><span class="sxs-lookup"><span data-stu-id="05828-427">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="05828-428">La aplicación es compatible con todos los clientes de la plataforma teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="05828-428">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="05828-429">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-429">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Crear una encuesta en la vista Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="virtual-rounding-9734"></a><span data-ttu-id="05828-431">Redondear virtual &#9734;</span><span class="sxs-lookup"><span data-stu-id="05828-431">Virtual Rounding &#9734;</span></span>

<span data-ttu-id="05828-432">Los proveedores de hospitales y de servicios de emergencia hacen decenas y, a menudo, cientos de "rondas" por día.</span><span class="sxs-lookup"><span data-stu-id="05828-432">Hospital and emergency room providers make dozens, and often hundreds of “rounds” per day.</span></span> <span data-ttu-id="05828-433">Estos rápidos check-ins en pacientes están pensados para proporcionar una comprobación del estado del paciente y garantizar que se aborde la preocupación del paciente.</span><span class="sxs-lookup"><span data-stu-id="05828-433">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="05828-434">Aunque el redondeo es una práctica esencial para garantizar que varios tipos de proveedores supervisan a los pacientes, representan una gran purga en PPE, ya que para cada visita, de cada proveedor, se debe usar una nueva máscara y un nuevo conjunto de ingredientes.</span><span class="sxs-lookup"><span data-stu-id="05828-434">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="05828-435">Con estas plantillas de aplicación, los trabajadores médicos pueden realizar fácilmente rondas virtualmente, a través de una reunión de Microsoft Teams entre el proveedor y el paciente.</span><span class="sxs-lookup"><span data-stu-id="05828-435">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="05828-436">También se hace referencia a la solución virtual de redondeo en la entrada del [blog](https://aka.ms/teamsvirtualrounding)Microsoft Health and LifeLogic .</span><span class="sxs-lookup"><span data-stu-id="05828-436">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="05828-437">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-437">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Redondeo virtual](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="05828-439">Administración de visitantes</span><span class="sxs-lookup"><span data-stu-id="05828-439">Visitor Management</span></span>

<span data-ttu-id="05828-440">La aplicación Administración de visitantes permite a su organización y a los empleados administrar de forma sencilla y eficaz el proceso de visitantes en el sitio, directamente desde Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="05828-440">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="05828-441">La aplicación permite a los empleados crear solicitudes de visitantes, realizar un seguimiento centralizado de un estado de solicitud a través del panel de visitantes y recibir notificaciones en tiempo real cuando llega un visitante.</span><span class="sxs-lookup"><span data-stu-id="05828-441">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="05828-442">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-442">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![Crear una vista de solicitud](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Notificación de llegada de visitantes](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards"></a><span data-ttu-id="05828-445">Workplace Awards</span><span class="sxs-lookup"><span data-stu-id="05828-445">Workplace Awards</span></span>

<span data-ttu-id="05828-446">Workplace Workplace Workplace es una plantilla de aplicación de Teams que proporciona un marco positivo para fomentar el reconocimiento y fomentar la cultura de compromiso de los empleados en el lugar de trabajo moderno.</span><span class="sxs-lookup"><span data-stu-id="05828-446">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="05828-447">La aplicación te permite configurar y administrar un programa de reconocimiento y recompensas para empleados (R&R) en el que los empleados pueden designar y apoyar fácilmente a los compañeros y el líder de R&R puede ver las nominaciones enviadas, conceder distinciones y anunciar destinatarios.</span><span class="sxs-lookup"><span data-stu-id="05828-447">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="05828-448">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="05828-448">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="05828-449">Tarjeta de nominación de reconocimientos en el lugar de trabajo</span><span class="sxs-lookup"><span data-stu-id="05828-449">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Pestaña lista de reconocimientos en el lugar de trabajo](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="05828-451">¿Tienes una idea de una plantilla de aplicación que te gustaría ver?</span><span class="sxs-lookup"><span data-stu-id="05828-451">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="05828-452">[Háganoslo saber.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)</span><span class="sxs-lookup"><span data-stu-id="05828-452">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
