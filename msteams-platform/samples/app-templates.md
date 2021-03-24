---
title: Plantillas de aplicación de Microsoft Teams
description: Vínculos y descripciones de plantillas de aplicación para la plataforma de Microsoft Teams
ms.topic: reference
keywords: Demostración de ejemplos de plantillas de Microsoft Teams
ms.author: lajanuar
author: laujan
ms.openlocfilehash: fffacb567f4b74f282020d61aea07e142256c84a
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034742"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="a8aad-104">Plantillas de aplicaciones para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a8aad-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="a8aad-105">Las plantillas de aplicación son ejemplos de aplicaciones completas para Microsoft Teams que son de código abierto y están disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8aad-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="a8aad-106">Cada plantilla de aplicación contiene instrucciones detalladas para implementar e instalar esa aplicación para la organización.</span><span class="sxs-lookup"><span data-stu-id="a8aad-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="a8aad-107">También proporciona una aplicación de ejemplo que puedes instalar y empezar a usar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="a8aad-107">It also provides a sample app that you can install and begin using immediately.</span></span> <span data-ttu-id="a8aad-108">El código fuente completo también está disponible, lo que le permite explorarlo en detalle o bifurcar el código y modificarlo para satisfacer sus requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="a8aad-108">The complete source code is available too, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="a8aad-109">Todas las plantillas de aplicación se proporcionan en los términos [de licencia mit.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="a8aad-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>
>[!NOTE] 
><span data-ttu-id="a8aad-110">You, not Microsoft must license and support apps created from app templates for your users and organizations.</span><span class="sxs-lookup"><span data-stu-id="a8aad-110">You, not Microsoft must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="a8aad-111">**&#9734; indica las plantillas de aplicación recién publicadas.**</span><span class="sxs-lookup"><span data-stu-id="a8aad-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="a8aad-112">Ventajas clave</span><span class="sxs-lookup"><span data-stu-id="a8aad-112">Key benefits</span></span>

* <span data-ttu-id="a8aad-113">**Implemente directamente en la nube:** Todas las plantillas de aplicación incluyen scripts de implementación que le permiten hospedar todos los servicios necesarios en Microsoft Azure o power platform.</span><span class="sxs-lookup"><span data-stu-id="a8aad-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="a8aad-114">**Código de ejemplo recomendado:** Las plantillas de la aplicación se ajustan a los procedimientos recomendados en materia de seguridad e infraestructura.</span><span class="sxs-lookup"><span data-stu-id="a8aad-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="a8aad-115">Se revisan todos los cambios enviados por la comunidad a las plantillas de la aplicación para garantizar la conformidad.</span><span class="sxs-lookup"><span data-stu-id="a8aad-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="a8aad-116">**Personalizable y extensible:** Aunque todas las plantillas de aplicación se pueden implementar con una configuración mínima, proporcionamos toda la base de código y los scripts de implementación para que puedas personalizarlas o ampliarlas fácilmente para que se ajusten a tus necesidades únicas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-116">**Customizable and extensible:** While all app templates can be deployed with minimal configuration, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="a8aad-117">**Documentación detallada:** Todas las plantillas de aplicación van acompañadas de documentación completa sobre los pasos de configuración, implementación y arquitectura de soluciones.</span><span class="sxs-lookup"><span data-stu-id="a8aad-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot-9734"></a><span data-ttu-id="a8aad-118">Bot de adopción &#9734;</span><span class="sxs-lookup"><span data-stu-id="a8aad-118">Adoption Bot &#9734;</span></span>

<span data-ttu-id="a8aad-119">Bot de adopción es un bot de chat de atención al usuario creado con Power Virtual Agent para Teams (PVA).</span><span class="sxs-lookup"><span data-stu-id="a8aad-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams (PVA).</span></span> <span data-ttu-id="a8aad-120">Puede considerarse como la versión PVA de FAQPlus.</span><span class="sxs-lookup"><span data-stu-id="a8aad-120">It can be considered as the PVA version of FAQPlus.</span></span> <span data-ttu-id="a8aad-121">Bot de adopción responde a más de 100 preguntas comunes sobre Microsoft 365 y Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="a8aad-122">Puede editar los temas existentes, agregar sus propios temas e ingerir preguntas frecuentes existentes.</span><span class="sxs-lookup"><span data-stu-id="a8aad-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="a8aad-123">Si los usuarios necesitan ayuda adicional, el Bot de adopción puede conectarlos a expertos o incluso extenderse para abrir vales de servicio con conectores de flujo premium. Este bot se puede instalar por su cuenta o estar integrado en una aplicación personalizada como el Centro [de adopción.](https://github.com/akporzondek/adoption_hub)</span><span class="sxs-lookup"><span data-stu-id="a8aad-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.This bot can be installed on it's own or built into a custom app like the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="a8aad-124">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-124">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="appointment-manager-9734"></a><span data-ttu-id="a8aad-125">Administrador de &#9734;</span><span class="sxs-lookup"><span data-stu-id="a8aad-125">Appointment Manager &#9734;</span></span>

<span data-ttu-id="a8aad-126">Appointment Manager es una plantilla de aplicación de Teams para ayudar a las empresas a crear, administrar y llevar a cabo citas virtuales con consumidores a través de Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-126">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="a8aad-127">Las nuevas solicitudes de cita de los consumidores son visibles en los canales de Teams, donde se pueden asignar y reasignar rápidamente al personal de un equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-127">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="a8aad-128">Las solicitudes de cita se pueden ver en los niveles de equipo o personal a través de pestañas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-128">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="a8aad-129">Cada cita está asociada a una reunión en línea de Teams, por lo que el personal y los consumidores pueden unirse fácilmente a la reunión en el momento programado.</span><span class="sxs-lookup"><span data-stu-id="a8aad-129">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="a8aad-130">La plantilla de aplicación se integra con Microsoft Bookings para facilitar la administración de citas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-130">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="a8aad-131">Las citas programadas aparecen automáticamente en los calendarios de los miembros del personal asignados y los consumidores reciben notificaciones y avisos de correo electrónico personalizables con vínculos de reunión incrustados.</span><span class="sxs-lookup"><span data-stu-id="a8aad-131">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="a8aad-132">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-132">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="a8aad-133">![Administrador de citas Overview ](../assets/images/appointment-manager-overview.png)
 ![ Appointment Manager en Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="a8aad-133">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="a8aad-134">Preguntar fuera</span><span class="sxs-lookup"><span data-stu-id="a8aad-134">Ask Away</span></span>

<span data-ttu-id="a8aad-135">Ask Away es un [bot de Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios llevar a cabo preguntas&A (preguntas y respuestas) en Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-135">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="a8aad-136">Con el bot Preguntar, los miembros del equipo pueden enviar y votar por arriba preguntas compartidas por compañeros, lo que permite que los hosts de preguntas&A recopile fácilmente las preguntas más importantes dentro de un canal o chat.</span><span class="sxs-lookup"><span data-stu-id="a8aad-136">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="a8aad-137">El bot se puede usar para realizar una sesión de preguntas en tiempo real&Una sesión en una reunión de Teams y permite a los asistentes enviar preguntas en directo a través del chat.</span><span class="sxs-lookup"><span data-stu-id="a8aad-137">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="a8aad-138">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-138">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Vista del cuadro de diálogo emergente de la tabla de clasificación para que los usuarios voten sobre las preguntas](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="a8aad-140">Información de asociados</span><span class="sxs-lookup"><span data-stu-id="a8aad-140">Associate Insights</span></span>

<span data-ttu-id="a8aad-141">Associate Insights es una plantilla [de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que permite a los trabajadores de primera línea capturar y enviar directamente la opinión, el sentimiento y la percepción del cliente.</span><span class="sxs-lookup"><span data-stu-id="a8aad-141">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="a8aad-142">Los trabajadores de primera línea suelen ser el primer representante de la compañía en interactuar con los clientes en un punto a uno de contacto.</span><span class="sxs-lookup"><span data-stu-id="a8aad-142">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="a8aad-143">Los equipos empresariales pueden compartir y usar los datos recopilados de forma colaborativa, por ejemplo, a través de una pestaña de Power BI Teams, para mejorar el producto y mejorar la experiencia del cliente.</span><span class="sxs-lookup"><span data-stu-id="a8aad-143">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="a8aad-144">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-144">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Vista de comentarios de las perspectivas generadas por la aplicación](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de Power BI de las perspectivas generadas por la aplicación](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="a8aad-147">Asistencia</span><span class="sxs-lookup"><span data-stu-id="a8aad-147">Attendance</span></span>

<span data-ttu-id="a8aad-148">La aplicación Asistencia es una [pestaña Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que se puede anclar en un equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-148">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="a8aad-149">Está diseñado para registrar la presencia, normalmente en configuraciones como entornos de aprendizaje y aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="a8aad-149">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="a8aad-150">Los usuarios pueden marcar o editar la asistencia durante un máximo de 30 días en el pasado y ver informes de asistencia resumidos para un grupo completo o asistentes individuales.</span><span class="sxs-lookup"><span data-stu-id="a8aad-150">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="a8aad-151">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-151">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Demostración de la aplicación de asistencia](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="a8aad-153">Libro a sala</span><span class="sxs-lookup"><span data-stu-id="a8aad-153">Book-a-room</span></span>

<span data-ttu-id="a8aad-154">Book-a-room es un bot de [Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30 (predeterminado), 60 o 90 minutos a partir de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="a8aad-154">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="a8aad-155">El bot Book-a-room tiene ámbitos para conversaciones personales o 1:1.</span><span class="sxs-lookup"><span data-stu-id="a8aad-155">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="a8aad-156">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-156">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Demostración de libro a sala](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="a8aad-158">Acceso de creación</span><span class="sxs-lookup"><span data-stu-id="a8aad-158">Building Access</span></span>

<span data-ttu-id="a8aad-159">Building Access es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que admite la administración de umbrales de ocupación de edificios y normas de distanciamiento social al permitir que los directores de instalaciones administren, realicen un seguimiento e informen de la presencia de los empleados en el sitio.</span><span class="sxs-lookup"><span data-stu-id="a8aad-159">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="a8aad-160">La aplicación, creada con Microsoft [Power Apps](/powerapps/powerapps-overview)y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams y permite a las organizaciones determinar la preparación de la creación, establecer criterios de elegibilidad para el acceso en el sitio y recopilar información para la planeación futura.</span><span class="sxs-lookup"><span data-stu-id="a8aad-160">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="a8aad-161">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-161">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Crear tarjeta de reserva de Access](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Creación de la vista clave de Access](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="a8aad-164">Celebraciones</span><span class="sxs-lookup"><span data-stu-id="a8aad-164">Celebrations</span></span>

<span data-ttu-id="a8aad-165">Celebraciones es una aplicación de Teams que ayuda a los miembros del equipo a celebrar los cumpleaños, aniversarios y otros eventos periódicos.</span><span class="sxs-lookup"><span data-stu-id="a8aad-165">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="a8aad-166">Recuerda ocasiones especiales de todos los miembros del equipo y envía un mensaje descriptivo en todos los equipos seleccionados en el momento de la creación de eventos, para que los miembros del equipo se sientan especiales en su día.</span><span class="sxs-lookup"><span data-stu-id="a8aad-166">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="a8aad-167">La aplicación proporciona una interfaz sencilla para que todos los miembros del equipo agreguen y visualen personalmente sus eventos y también permite al usuario seleccionar los equipos en los que se comparten los eventos.</span><span class="sxs-lookup"><span data-stu-id="a8aad-167">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="a8aad-168">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-168">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="a8aad-169">Lista de comprobación</span><span class="sxs-lookup"><span data-stu-id="a8aad-169">Checklist</span></span>

<span data-ttu-id="a8aad-170">Lista de comprobación es una aplicación de extensión [de](../messaging-extensions/what-are-messaging-extensions.md) mensajería personalizada de Microsoft Teams que te permite colaborar con tu equipo creando una lista de comprobación compartida en un chat o canal.</span><span class="sxs-lookup"><span data-stu-id="a8aad-170">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="a8aad-171">La aplicación se admite en todos los clientes de plataforma de Teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="a8aad-171">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="a8aad-172">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-172">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Crear lista de comprobación en la vista Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a><span data-ttu-id="a8aad-174">Classroom Drop-in &#9734;</span><span class="sxs-lookup"><span data-stu-id="a8aad-174">Classroom Drop-in &#9734;</span></span>

<span data-ttu-id="a8aad-175">Classroom Drop-in es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que permite a los líderes del sistema encontrar equipos de clase (aulas virtuales) y agregarse a sí mismos u otros a estos equipos de clase durante un período de entrega especificado, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a8aad-175">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="a8aad-176">La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate](/power-automate/getting-started)se integra profundamente con Microsoft Teams para garantizar que los institutos educativos puedan optimizar sus operaciones en un entorno de aprendizaje híbrido proporcionando acceso a partes interesadas relevantes para los equipos de clase por requisitos empresariales.</span><span class="sxs-lookup"><span data-stu-id="a8aad-176">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="a8aad-177">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-177">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Solicitud de acceso a clases](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="a8aad-179">Comunicador de la empresa</span><span class="sxs-lookup"><span data-stu-id="a8aad-179">Company Communicator</span></span>

<span data-ttu-id="a8aad-180">La aplicación Communicator empresa permite a los equipos corporativos crear y enviar mensajes destinados a varios equipos o a un gran número de empleados a través del chat, lo que permite que la organización llegue a los empleados justo donde colaboran.</span><span class="sxs-lookup"><span data-stu-id="a8aad-180">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="a8aad-181">Use esta plantilla para varios escenarios, como anuncios de nuevas iniciativas, incorporación de empleados, aprendizaje y desarrollo modernos o difusión en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="a8aad-181">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="a8aad-182">La aplicación proporciona una interfaz sencilla para que los usuarios designados creen, obtengan una vista previa, colaboren y envíen mensajes.</span><span class="sxs-lookup"><span data-stu-id="a8aad-182">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="a8aad-183">Proporciona una base para crear capacidades de comunicación personalizadas dirigidas, como telemetría personalizada, sobre cuántos usuarios han reconocido o interactuado con un mensaje.</span><span class="sxs-lookup"><span data-stu-id="a8aad-183">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="a8aad-184">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-184">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator de cuadro de redacción](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="a8aad-186">Búsqueda de grupos de contactos</span><span class="sxs-lookup"><span data-stu-id="a8aad-186">Contact Group Lookup</span></span>

<span data-ttu-id="a8aad-187">La aplicación Búsqueda de grupos de contactos proporciona un enfoque práctico y útil para crear, acceder y administrar los grupos de contactos de la organización (anteriormente conocidos como listas de distribución o grupos de comunicación).</span><span class="sxs-lookup"><span data-stu-id="a8aad-187">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="a8aad-188">Los usuarios pueden ver y chatear rápidamente con miembros del grupo, ver el estado de los miembros y crear un chat de grupo con miembros seleccionados en el grupo de contactos, todo dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-188">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="a8aad-189">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-189">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Vista Favoritos anclados búsqueda de grupo de contactos](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Demostración de chat inicio de búsqueda de grupo de contactos](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation-9734"></a><span data-ttu-id="a8aad-192">Apreciación de compañeros de trabajo &#9734;</span><span class="sxs-lookup"><span data-stu-id="a8aad-192">Co-worker Appreciation &#9734;</span></span>

<span data-ttu-id="a8aad-193">Con la plantilla de apreciación de compañeros de trabajo en Microsoft Teams, los usuarios pueden reconocer los logros de sus compañeros en el contexto de Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-193">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="a8aad-194">Cuando los compañeros de trabajo seleccionan recompensar a un compañero, los destinatarios y otros miembros del equipo se etiquetan en una conversación de canal y reciben una notificación sobre los detalles de la concesión del canal.</span><span class="sxs-lookup"><span data-stu-id="a8aad-194">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="a8aad-195">Los galardones se registran en la aplicación teams, que es segura, portátil y fácilmente compartible.</span><span class="sxs-lookup"><span data-stu-id="a8aad-195">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="a8aad-196">Esto se puede considerar como la versión basada en PowerApps de la plantilla de la aplicación Open Badges, con una tabla de clasificación.</span><span class="sxs-lookup"><span data-stu-id="a8aad-196">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="a8aad-197">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-197">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![General](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="a8aad-199">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="a8aad-199">CrowdSourcer</span></span>

<span data-ttu-id="a8aad-200">CrowdSourcer es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona a los equipos información consultada procedente de forma colaborativa de miembros del grupo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-200">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="a8aad-201">Es una excelente manera de responder a las preguntas más frecuentes al tiempo que permite a los participantes participar activamente y contribuir a un recurso de información divertido y útil.</span><span class="sxs-lookup"><span data-stu-id="a8aad-201">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="a8aad-202">Obtenerlo en Github</span><span class="sxs-lookup"><span data-stu-id="a8aad-202">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interacción entre usuarios finales de Crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="a8aad-204">Adhesivos personalizados</span><span class="sxs-lookup"><span data-stu-id="a8aad-204">Custom Stickers</span></span>

<span data-ttu-id="a8aad-205">La autoexpresión es fundamental para una cultura de equipo en buen estado.</span><span class="sxs-lookup"><span data-stu-id="a8aad-205">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="a8aad-206">Esta plantilla de aplicación es una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) que permite a los usuarios usar adhesivos y GIF personalizados dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-206">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="a8aad-207">Esta plantilla proporciona una experiencia de configuración sencilla basada en web en la que cualquier persona con acceso a la configuración puede cargar los GIF/adhesivos/imágenes que desean que tengan sus usuarios finales, lo que permite a todo el equipo usar cualquier conjunto de adhesivos que elija.</span><span class="sxs-lookup"><span data-stu-id="a8aad-207">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="a8aad-208">Esta aplicación también permite compartir fácilmente imágenes/GIF/adhesivos entre equipos sin necesidad de tener acceso a sitios de SharePoint o canales individuales como mecanismos de almacenamiento y uso compartido.</span><span class="sxs-lookup"><span data-stu-id="a8aad-208">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="a8aad-209">Por ejemplo, los equipos de productos pueden compartir fácilmente imágenes de producto y GIF a redes sociales, equipos de marketing y ventas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="a8aad-209">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="a8aad-210">También se puede extender esta aplicación desencadenando un flujo de notificación a equipos o individuos específicos cuando se hacen disponibles nuevas imágenes/GIF.</span><span class="sxs-lookup"><span data-stu-id="a8aad-210">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="a8aad-211">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-211">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Aplicación Stickers](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="a8aad-213">Ideas de los empleados</span><span class="sxs-lookup"><span data-stu-id="a8aad-213">Employee Ideas</span></span>

<span data-ttu-id="a8aad-214">La aplicación Ideas para empleados es la versión de PowerApps de la plantilla de aplicación Great Ideas basada en Azure.</span><span class="sxs-lookup"><span data-stu-id="a8aad-214">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="a8aad-215">La aplicación permite a los usuarios de Teams configurar y configurar una campaña de ideas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-215">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="a8aad-216">Una campaña de ideas es una categoría para agrupar ideas en torno a temas comunes.</span><span class="sxs-lookup"><span data-stu-id="a8aad-216">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="a8aad-217">Los usuarios de Teams también pueden realizar las siguientes actividades:</span><span class="sxs-lookup"><span data-stu-id="a8aad-217">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="a8aad-218">Configure un formulario de envío estándar que los empleados deben enviar para cada idea.</span><span class="sxs-lookup"><span data-stu-id="a8aad-218">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="a8aad-219">Revisa y administra las ideas y la lista de campañas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-219">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="a8aad-220">Modificar y eliminar campañas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-220">Modify and delete campaigns.</span></span>
* <span data-ttu-id="a8aad-221">Revisar las tablas de ideas de líderes.</span><span class="sxs-lookup"><span data-stu-id="a8aad-221">Review leader boards of ideas.</span></span>
* <span data-ttu-id="a8aad-222">Vota y comparte ideas priorizadas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-222">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="a8aad-223">Enviar ideas para una campaña.</span><span class="sxs-lookup"><span data-stu-id="a8aad-223">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="a8aad-224">Ver la idea de otro miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-224">View other team member's idea.</span></span>
* <span data-ttu-id="a8aad-225">Vota sobre las ideas que más te gustan.</span><span class="sxs-lookup"><span data-stu-id="a8aad-225">Vote on most liked ideas.</span></span>
* <span data-ttu-id="a8aad-226">Revisa el rendimiento de sus ideas en comparación con otras personas dentro de una campaña.</span><span class="sxs-lookup"><span data-stu-id="a8aad-226">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="a8aad-227">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-227">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Administrar vista de campaña](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="a8aad-229">E-Prescriptions</span><span class="sxs-lookup"><span data-stu-id="a8aad-229">E-Prescriptions</span></span> 

<span data-ttu-id="a8aad-230">E-Prescriptions es una aplicación basada en [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)que mejora la telemedicina y el cuidado virtual automatizando el proceso de emisión de recetas electrónicas a los pacientes.</span><span class="sxs-lookup"><span data-stu-id="a8aad-230">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="a8aad-231">Los profesionales médicos pueden revisar rápidamente las citas, generar recetas electrónicas y enviar correos electrónicos con datos adjuntos de la receta electrónica a los pacientes directamente en la plataforma teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-231">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="a8aad-232">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-232">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

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

## <a name="employee-training"></a><span data-ttu-id="a8aad-237">Formación de empleados</span><span class="sxs-lookup"><span data-stu-id="a8aad-237">Employee Training</span></span> 

<span data-ttu-id="a8aad-238">La formación de los empleados es una aplicación de Microsoft Teams que permite a los organizadores publicar, realizar un seguimiento y promover fácilmente eventos de aprendizaje y aprendizaje para su organización.</span><span class="sxs-lookup"><span data-stu-id="a8aad-238">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="a8aad-239">Con la aplicación, los organizadores de eventos pueden enviar avisos y notificaciones a los registradores de eventos y los empleados pueden indicar interés en los próximos eventos, mantenerse actualizados en eventos actuales y compartir detalles de eventos con compañeros a través de la extensión de mensajería de Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-239">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="a8aad-240">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-240">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="a8aad-241">**Ver eventos de formación de empleados** ![ Imagen de pestaña Formación de los empleados](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="a8aad-241">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="a8aad-242">**Crear evento de formación de empleados** ![ Formulario de creación de eventos de formación para empleados](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="a8aad-242">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="a8aad-243">Buscador de expertos</span><span class="sxs-lookup"><span data-stu-id="a8aad-243">Expert Finder</span></span>

<span data-ttu-id="a8aad-244">Expert Finder es un [bot de Microsoft Teams](../bots/what-are-bots.md) que identifica miembros específicos de la organización en función de sus aptitudes, intereses y atributos educativos.</span><span class="sxs-lookup"><span data-stu-id="a8aad-244">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="a8aad-245">Los miembros encuentran expertos dentro de una organización que coinciden con una búsqueda de palabras clave de perfiles de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8aad-245">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="a8aad-246">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-246">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Demostración de resultados de búsqueda del Buscador de expertos](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="a8aad-248">Preguntas más frecuentes Plus</span><span class="sxs-lookup"><span data-stu-id="a8aad-248">FAQ Plus</span></span>

<span data-ttu-id="a8aad-249">Preguntas conversacionales&Bots son una forma sencilla de proporcionar respuestas a las preguntas más frecuentes de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a8aad-249">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="a8aad-250">Sin embargo, la mayoría de los bots no interactúan con los usuarios de forma significativa porque no hay ningún humano en el bucle cuando se produce un error en el bot.</span><span class="sxs-lookup"><span data-stu-id="a8aad-250">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="a8aad-251">Faq bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span><span class="sxs-lookup"><span data-stu-id="a8aad-251">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="a8aad-252">Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos.</span><span class="sxs-lookup"><span data-stu-id="a8aad-252">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="a8aad-253">Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde el propio equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-253">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="a8aad-254">La versión más reciente de **FAQ Plus** admite resoluciones de preguntas&A al permitir a un equipo de expertos completar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a8aad-254">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="a8aad-255">&#x2714; agregar nuevas preguntas&Como directamente a la base de conocimientos mediante extensiones de mensaje.</span><span class="sxs-lookup"><span data-stu-id="a8aad-255">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="a8aad-256">&#x2714; Editar y eliminar preguntas&Pares agregados por un bot.</span><span class="sxs-lookup"><span data-stu-id="a8aad-256">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="a8aad-257">&#x2714; seguimiento del historial de revisiones de Q&As.</span><span class="sxs-lookup"><span data-stu-id="a8aad-257">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="a8aad-258">&#x2714; configurar una respuesta con detalles adicionales para mostrar como una [tarjeta adaptable.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="a8aad-258">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="a8aad-259">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-259">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif de preguntas más frecuentes](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app-9734"></a><span data-ttu-id="a8aad-261">Obtener la aplicación de soporte &#9734;</span><span class="sxs-lookup"><span data-stu-id="a8aad-261">Get Support App &#9734;</span></span>

<span data-ttu-id="a8aad-262">Las organizaciones que usan Microsoft Teams pueden usar la aplicación Obtener soporte técnico para permitir que cualquier conjunto de usuarios solicite asistencia a los supervisores.</span><span class="sxs-lookup"><span data-stu-id="a8aad-262">The Get Support app can be used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="a8aad-263">Esta aplicación incluye varias características, como:</span><span class="sxs-lookup"><span data-stu-id="a8aad-263">This app includes various features, such as:</span></span>
-   <span data-ttu-id="a8aad-264">Solicitar asistencia en distintas categorías desde una Power App</span><span class="sxs-lookup"><span data-stu-id="a8aad-264">Requesting assistance on different categories from a Power App</span></span>
-   <span data-ttu-id="a8aad-265">Notificaciones enviadas a los solicitantes para informarles de quién ha sido asignado</span><span class="sxs-lookup"><span data-stu-id="a8aad-265">Notifications sent to requestors informing them of who has been assigned</span></span> 
-   <span data-ttu-id="a8aad-266">Notificaciones enviadas a supervisores asignados para informarles de quién necesita asistencia</span><span class="sxs-lookup"><span data-stu-id="a8aad-266">Notifications sent to assigned supervisors informing them of who needs assistance</span></span> 
-   <span data-ttu-id="a8aad-267">Análisis de escalaciones y patrones en SharePoint y PowerBI</span><span class="sxs-lookup"><span data-stu-id="a8aad-267">Analyzing escalations and patterns in SharePoint and PowerBI</span></span>

[<span data-ttu-id="a8aad-268">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-268">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Obtener gif de soporte técnico](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="a8aad-270">Rastreador de objetivos</span><span class="sxs-lookup"><span data-stu-id="a8aad-270">Goal Tracker</span></span>

<span data-ttu-id="a8aad-271">La aplicación Rastreador de objetivos es una solución completa para que su organización admita el establecimiento de objetivos, la observación del progreso y el reconocimiento del éxito en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-271">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="a8aad-272">La aplicación permite a los usuarios establecer, realizar un seguimiento y actualizar objetivos en un nivel profesional, personal y de equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-272">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="a8aad-273">Los miembros del equipo también reciben avisos oportunos y actualizaciones de estado para mantenerse centrados y mantenerse al día.</span><span class="sxs-lookup"><span data-stu-id="a8aad-273">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="a8aad-274">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a><span data-ttu-id="a8aad-277">Grandes ideas</span><span class="sxs-lookup"><span data-stu-id="a8aad-277">Great Ideas</span></span>

<span data-ttu-id="a8aad-278">La aplicación Great Ideas admite y potencia la innovación y la creatividad dentro de la organización.</span><span class="sxs-lookup"><span data-stu-id="a8aad-278">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="a8aad-279">La aplicación permite a los empleados compartir ideas con compañeros y líderes, descubrir nuevos envíos, contribuciones destacadas para la consideración del mismo nivel y emitir su voto para las mejores propuestas dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-279">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="a8aad-280">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-280">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="a8aad-283">Actividades de grupo</span><span class="sxs-lookup"><span data-stu-id="a8aad-283">Group Activities</span></span>

<span data-ttu-id="a8aad-284">Actividades de grupo es una aplicación de Microsoft Teams que facilita a los propietarios de equipos crear rápidamente grupos de actividades y administrar flujos de trabajo de colaboración en el contexto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-284">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="a8aad-285">Los autores de actividades están habilitados para crear actividades, distribuir aleatoriamente miembros del equipo en grupos y, opcionalmente, hacer que el bot envíe avisos hasta que se completen las actividades.</span><span class="sxs-lookup"><span data-stu-id="a8aad-285">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="a8aad-286">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-286">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

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

## <a name="grow-your-skills"></a><span data-ttu-id="a8aad-289">Aumentar sus habilidades</span><span class="sxs-lookup"><span data-stu-id="a8aad-289">Grow Your Skills</span></span>

<span data-ttu-id="a8aad-290">La aplicación Crecer tus habilidades admite el crecimiento y el desarrollo profesionales, ya que permite a los empleados contribuir a proyectos complementarios para tu organización al mismo tiempo que aprenden nuevas habilidades.</span><span class="sxs-lookup"><span data-stu-id="a8aad-290">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="a8aad-291">Los empleados pueden usar la aplicación para buscar oportunidades que satisfagan sus intereses, disfrutar de una colaboración significativa con compañeros y adquirir nuevos niveles de experiencia y capacidades, todo dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-291">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="a8aad-292">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-292">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Vista Proyectos disponibles](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de habilidades adquiridas del visor](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="a8aad-295">Soporte de Recursos Humanos</span><span class="sxs-lookup"><span data-stu-id="a8aad-295">HR Support</span></span>

<span data-ttu-id="a8aad-296">Bot de soporte técnico de RECURSOS es una pregunta&Un bot que lleva a un profesional/experto de soporte técnico del equipo de recursos humanos en el bucle cuando no puede ayudar.</span><span class="sxs-lookup"><span data-stu-id="a8aad-296">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="a8aad-297">Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos.</span><span class="sxs-lookup"><span data-stu-id="a8aad-297">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="a8aad-298">Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde el propio equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-298">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="a8aad-299">Además, el bot sugiere vínculos a las preguntas y directivas de RECURSOS humanos recomendadas mediante la búsqueda de etiquetas preconfiguradas en la pregunta.</span><span class="sxs-lookup"><span data-stu-id="a8aad-299">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="a8aad-300">Estos iconos también se pueden encontrar en la pestaña asociada como una referencia rápida.</span><span class="sxs-lookup"><span data-stu-id="a8aad-300">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="a8aad-301">El soporte de recursos humanos funciona bien para QnA de peso ligero y para proporcionar soporte rápido al iniciar nuevos proyectos o iniciativas en la organización.</span><span class="sxs-lookup"><span data-stu-id="a8aad-301">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="a8aad-302">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-302">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Soporte de Recursos Humanos](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="a8aad-304">Rompehielo</span><span class="sxs-lookup"><span data-stu-id="a8aad-304">Icebreaker</span></span>

<span data-ttu-id="a8aad-305">Icebreaker es un [bot de Microsoft Teams](../bots/what-are-bots.md) que ayuda a tu equipo a acercarse emparejando dos miembros del equipo aleatorios cada semana para reunirse.</span><span class="sxs-lookup"><span data-stu-id="a8aad-305">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="a8aad-306">El bot facilita la programación al sugerir automáticamente horas libres que funcionen para ambos miembros.</span><span class="sxs-lookup"><span data-stu-id="a8aad-306">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="a8aad-307">Fortalezca las conexiones personales y cree una comunidad estrechamente unida con esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="a8aad-307">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="a8aad-308">Además de fomentar las conexiones personales en todo el equipo, la aplicación Icebreaker puede ayudar a cultivar comunidades basadas en intereses dentro de la organización.</span><span class="sxs-lookup"><span data-stu-id="a8aad-308">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="a8aad-309">Por ejemplo, puedes usar esta aplicación para un grupo de interés de DevOps para ayudar a que las ideas y los procedimientos recomendados se extienda orgánicamente en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="a8aad-309">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="a8aad-310">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-310">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Aplicación Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="a8aad-312">Incentivos</span><span class="sxs-lookup"><span data-stu-id="a8aad-312">Incentives</span></span>

<span data-ttu-id="a8aad-313">Incentives es una plantilla [de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que administra y realiza un seguimiento de la participación de los empleados en actividades designadas, como cursos e iniciativas de administración de cambios.</span><span class="sxs-lookup"><span data-stu-id="a8aad-313">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="a8aad-314">Los administradores usan la aplicación para establecer actividades designadas, asignar puntos para su finalización y especificar los niveles de puntos de elegibilidad necesarios para las recompensas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-314">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="a8aad-315">Los empleados usan la aplicación para ver sus puntos acumulados y, al alcanzar la elegibilidad, solicitar y reclamar recompensas canjeables.</span><span class="sxs-lookup"><span data-stu-id="a8aad-315">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="a8aad-316">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-316">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Demostración de aplicaciones de incentivos](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="a8aad-318">Reportero de incidentes</span><span class="sxs-lookup"><span data-stu-id="a8aad-318">Incident Reporter</span></span>

<span data-ttu-id="a8aad-319">Incident Reporter es un [bot de Microsoft Teams](../bots/what-are-bots.md)  que optimiza la administración de incidentes en su organización.</span><span class="sxs-lookup"><span data-stu-id="a8aad-319">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="a8aad-320">El bot facilita la recopilación automatizada de datos de incidentes, informes de incidentes personalizados, notificaciones relevantes para las partes interesadas y seguimiento de incidentes de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="a8aad-320">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="a8aad-321">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-321">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Vista de ámbito de grupo del reportero de incidentes](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de ámbito personal del reportero de incidentes](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection-9734"></a><span data-ttu-id="a8aad-324">Inspección &#9734;</span><span class="sxs-lookup"><span data-stu-id="a8aad-324">Inspection &#9734;</span></span>

 <span data-ttu-id="a8aad-325">Inspección es una aplicación de Microsoft Teams que permite a los trabajadores de primera línea inspeccionar cualquier cosa, desde ubicaciones hasta activos y equipos.</span><span class="sxs-lookup"><span data-stu-id="a8aad-325">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="a8aad-326">Por ejemplo, una tienda comercial, una planta de fabricación o vehículos y máquinas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-326">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="a8aad-327">Hay dos aplicaciones en esta solución, cada una destinada a diferentes tipos de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a8aad-327">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="a8aad-328">La aplicación permite a los trabajadores de primera línea inspeccionar un activo o área, administrar la calidad de los productos y servicios o mantener la seguridad en el lugar de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-328">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="a8aad-329">Facilita la comunicación entre los miembros del equipo para solucionar los problemas encontrados durante la inspección.</span><span class="sxs-lookup"><span data-stu-id="a8aad-329">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="a8aad-330">La aplicación proporciona informes sencillos para que los administradores agilicen la resolución de problemas y resalten las tendencias.</span><span class="sxs-lookup"><span data-stu-id="a8aad-330">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="a8aad-331">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-331">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Introducción a la inspección](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="a8aad-333">Informes de problemas</span><span class="sxs-lookup"><span data-stu-id="a8aad-333">Issue Reporting</span></span>

<span data-ttu-id="a8aad-334">La aplicación De informes de problemas permite a los empleados y administradores generar y administrar problemas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-334">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="a8aad-335">Consta de dos aplicaciones, Aplicación de informes de problemas para informar y Aplicación Administrar problemas para administrar problemas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-335">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="a8aad-336">Los jefes de equipo usan la aplicación Administrar problemas para configurar la experiencia de la aplicación, incluido el canal en el que la aplicación crea los mensajes de Microsoft Teams y las tareas de Planner.</span><span class="sxs-lookup"><span data-stu-id="a8aad-336">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="a8aad-337">Los administradores también usan la aplicación para crear formularios de plantilla para recopilar detalles cuando un usuario informa de un problema.</span><span class="sxs-lookup"><span data-stu-id="a8aad-337">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="a8aad-338">Por ejemplo, revise, edite o elimine formularios de plantilla de problema.</span><span class="sxs-lookup"><span data-stu-id="a8aad-338">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="a8aad-339">La aplicación también se puede usar para revisar los problemas del equipo, informar sobre el historial de problemas y administrar eficazmente la resolución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-339">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="a8aad-340">Los empleados usan la aplicación De informes de problemas para registrar problemas y detalles necesarios para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="a8aad-340">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="a8aad-341">La aplicación también se usa para modificar y resolver problemas existentes y obtener una vista de alto nivel de problemas individuales o de equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-341">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="a8aad-342">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-342">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Vista de equipo de informes de problemas](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="a8aad-344">Incorporación de nuevos empleados</span><span class="sxs-lookup"><span data-stu-id="a8aad-344">New Employee Onboarding</span></span> 

<span data-ttu-id="a8aad-345">La incorporación de nuevos empleados es una solución integrada de incorporación de nuevos empleados de Microsoft Teams y [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) que permite a su organización proporcionar una experiencia de incorporación coherente y de alta calidad para los empleados en su viaje de nueva contratación.</span><span class="sxs-lookup"><span data-stu-id="a8aad-345">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="a8aad-346">Los equipos de recursos humanos y los administradores de contratación pueden usar la aplicación para proporcionar información relevante a lo largo del proceso de orientación e inducción, así como para que los nuevos empleados compartan comentarios, proporcionen introducciones y completen tareas de incorporación.</span><span class="sxs-lookup"><span data-stu-id="a8aad-346">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="a8aad-347">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-347">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="a8aad-348">**Nueva tarjeta de bienvenida para empleados** ![ Imagen de la nueva tarjeta de bienvenida del empleado](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="a8aad-348">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="a8aad-349">**Lista de comprobación de nuevos empleados** ![ Imagen de la lista de comprobación de nuevos empleados](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="a8aad-349">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="a8aad-350">Distintivos abiertos</span><span class="sxs-lookup"><span data-stu-id="a8aad-350">Open Badges</span></span>

<span data-ttu-id="a8aad-351">Open Badges es una aplicación de Microsoft Teams que permite a los usuarios obtener distintivos de credenciales de aprendizaje digital en el contexto de Teams y compartirlos en todas partes.</span><span class="sxs-lookup"><span data-stu-id="a8aad-351">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="a8aad-352">Con las funcionalidades de la entidad emisora de distintivos digitales de terceros, [Badgr](https://badgr.org/), los distintivos concedidos se registran en el perfil badgr de un destinatario y están disponibles para crear y compartir una imagen enriquecida de los recorridos de aprendizaje de por vida.</span><span class="sxs-lookup"><span data-stu-id="a8aad-352">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="a8aad-353">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![Imagen de distintivos disponibles](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista Distintivos otorgados](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="a8aad-356">Sondeo</span><span class="sxs-lookup"><span data-stu-id="a8aad-356">Poll</span></span> 

<span data-ttu-id="a8aad-357">Poll es una aplicación de extensión de mensajería personalizada de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que te permite crear y enviar rápidamente sondeos en un chat o un canal para recopilar opiniones y preferencias del equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-357">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="a8aad-358">La aplicación se admite en todos los clientes de plataforma de Teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="a8aad-358">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="a8aad-359">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-359">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Crear sondeo en la vista Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="a8aad-361">Respuestas rápidas</span><span class="sxs-lookup"><span data-stu-id="a8aad-361">Quick Responses</span></span>

<span data-ttu-id="a8aad-362">Respuestas rápidas es una aplicación de Microsoft Teams que ofrece una solución sólida para responder eficazmente a las preguntas más frecuentes (preguntas frecuentes) de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a8aad-362">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="a8aad-363">En lugar de responder a cada consulta de forma manual y continua, la aplicación compilará una biblioteca de respuestas para una experiencia de usuario interactiva a través de extensiones de [mensajería de](../messaging-extensions/what-are-messaging-extensions.md)Teams .</span><span class="sxs-lookup"><span data-stu-id="a8aad-363">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="a8aad-364">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Vista de ejemplo de las respuestas](../assets/images/quick-responses.png)

## <a name="rapid-assist"></a><span data-ttu-id="a8aad-366">Asistencia rápida</span><span class="sxs-lookup"><span data-stu-id="a8aad-366">Rapid Assist</span></span>

<span data-ttu-id="a8aad-367">Rapid Assist es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que permite a los asociados que se enfrentan al cliente conectarse rápidamente con los expertos para obtener respuestas rápidas, buscar información, realizar un seguimiento de las solicitudes abiertas y permitir que los expertos reciban notificaciones para obtener rápidamente una llamada para ayudar a responder preguntas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-367">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="a8aad-368">La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams para permitir que las organizaciones conecten fácilmente a los trabajadores de primera línea con vínculos corporativos para resolver las consultas de los clientes y ofrecer una excelente experiencia de cliente.</span><span class="sxs-lookup"><span data-stu-id="a8aad-368">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="a8aad-369">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Interfaz de solicitud de usuario final](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Vista de solicitud de experto](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="a8aad-372">Reflejar</span><span class="sxs-lookup"><span data-stu-id="a8aad-372">Reflect</span></span> 

<span data-ttu-id="a8aad-373">Reflect es una aplicación de extensión de mensajería personalizada de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que proporciona un recurso seguro e inclusivo para que los miembros del equipo compartan el estado de su bienestar emocional con compañeros o jefes de grupo directamente en Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-373">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="a8aad-374">La aplicación está disponible en chats de canal, grupo, reunión y 1:1 y la respuesta de la entrada se puede establecer en pública, privada a remitente o totalmente anónima.</span><span class="sxs-lookup"><span data-stu-id="a8aad-374">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="a8aad-375">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="a8aad-376">**Sondeo de bienestar**</span><span class="sxs-lookup"><span data-stu-id="a8aad-376">**Well-being poll**</span></span>
    
    ![Reflejar sondeo de usuarios de aplicaciones](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="a8aad-378">Soporte remoto</span><span class="sxs-lookup"><span data-stu-id="a8aad-378">Remote Support</span></span>

<span data-ttu-id="a8aad-379">El soporte remoto es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona una interfaz centrada entre los solicitantes de soporte técnico de toda la organización y el equipo de soporte técnico interno.</span><span class="sxs-lookup"><span data-stu-id="a8aad-379">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="a8aad-380">Los usuarios finales pueden enviar, editar o retirar solicitudes de soporte técnico y el equipo de soporte técnico puede responder, administrar y actualizar solicitudes en toda la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-380">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="a8aad-381">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![Formulario de soporte técnico de solicitud](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Detalles de la solicitud de soporte técnico](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="a8aad-384">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="a8aad-384">Request-a-team</span></span>

<span data-ttu-id="a8aad-385">Request-a-team es una aplicación de Microsoft Teams que optimiza la creación de nuevos equipos para su organización empresarial.</span><span class="sxs-lookup"><span data-stu-id="a8aad-385">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="a8aad-386">La aplicación admite la estandarización y los procedimientos recomendados al crear nuevas instancias de equipo mediante la integración de un formulario de solicitud guiado por asistente, un proceso de aprobación incrustado, un panel de estado de solicitud y compilaciones automatizadas de equipo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-386">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="a8aad-387">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-387">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Vista de página de inicio de request-a-team](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de página del Asistente para solicitud de un equipo](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="a8aad-390">Scrums para canales</span><span class="sxs-lookup"><span data-stu-id="a8aad-390">Scrums for Channels</span></span>

<span data-ttu-id="a8aad-391">Scrums para canales es una aplicación auxiliar de scrum que permite a los usuarios programar y ejecutar scrums en canales de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-391">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="a8aad-392">La aplicación es ideal para equipos remotos y equipos formados por miembros de distintas ubicaciones geográficas y zonas horarias para compartir actualizaciones diarias y garantizar la participación en reuniones de soporte de scrum.</span><span class="sxs-lookup"><span data-stu-id="a8aad-392">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="a8aad-393">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="a8aad-394">Para realizar reuniones de scrum en un chat de grupo, consulta nuestra plantilla de aplicación [Scrums for Group Chat.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="a8aad-394">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

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

## <a name="scrums-for-group-chat"></a><span data-ttu-id="a8aad-397">Scrums para chat en grupo</span><span class="sxs-lookup"><span data-stu-id="a8aad-397">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="a8aad-398">La plantilla de aplicación Estado de Scrums se ha actualizado y ahora es Scrums para chat en grupo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-398">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="a8aad-399">Scrums for Group Chat es un asistente de scrum de apoyo que permite a los miembros del chat de grupo ejecutar reuniones de soporte asincrónicas y compartir fácilmente sus actualizaciones diarias.</span><span class="sxs-lookup"><span data-stu-id="a8aad-399">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="a8aad-400">Permite a todos los miembros del chat de grupo contribuir al scrum y ver las actualizaciones realizadas por otros usuarios en el scrum en ejecución.</span><span class="sxs-lookup"><span data-stu-id="a8aad-400">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="a8aad-401">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-401">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Demostración de Scrums para chat en grupo](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="a8aad-403">Compartir ahora</span><span class="sxs-lookup"><span data-stu-id="a8aad-403">Share Now</span></span> 

<span data-ttu-id="a8aad-404">La aplicación Compartir ahora promueve el intercambio positivo de información entre compañeros al permitir que los usuarios compartan fácilmente contenido en el entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-404">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="a8aad-405">Los usuarios interactúan con la aplicación para compartir elementos de interés con los miembros del equipo, descubrir nuevo contenido compartido, establecer preferencias y favoritos de marcadores para su lectura posterior.</span><span class="sxs-lookup"><span data-stu-id="a8aad-405">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="a8aad-406">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-406">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Seleccionar vista de contenido](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="a8aad-408">Búsqueda de lista de SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8aad-408">SharePoint List Search</span></span>

<span data-ttu-id="a8aad-409">La colaboración en Microsoft Teams suele hacer referencia a la información contenida en los elementos de una lista de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a8aad-409">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="a8aad-410">Simplemente pegar un vínculo al elemento en cuestión obliga a todos a cambiar el contexto de la conversación, buscar la información necesaria y, a continuación, volver a Teams para continuar la conversación.</span><span class="sxs-lookup"><span data-stu-id="a8aad-410">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="a8aad-411">A medida que la conversación continúa normalmente, las personas tendrán que volver al elemento de referencia varias veces para comprobar nuevos comentarios y actualizar sus memorias de la información contenida en el elemento.</span><span class="sxs-lookup"><span data-stu-id="a8aad-411">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="a8aad-412">Este cambio de contexto crea una barrera para una colaboración fluida y es una receta para las cosas que pasan por las grietas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-412">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="a8aad-413">Para ayudar a aliviar este dolor, estamos encantados de traerte la plantilla de aplicación Búsqueda de lista.</span><span class="sxs-lookup"><span data-stu-id="a8aad-413">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="a8aad-414">Millones de usuarios usan SharePoint para crear algunos de los flujos de trabajo principales de sus organizaciones.</span><span class="sxs-lookup"><span data-stu-id="a8aad-414">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="a8aad-415">Sin embargo, colaborar en las listas puede ser especialmente tedioso.</span><span class="sxs-lookup"><span data-stu-id="a8aad-415">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="a8aad-416">Con la plantilla de aplicación Búsqueda de lista en Microsoft Teams, los usuarios pueden insertar información de elementos de lista de SharePoint directamente dentro de una conversación de chat para aliviar el cambio de contexto causado al insertar simplemente un vínculo en un chat.</span><span class="sxs-lookup"><span data-stu-id="a8aad-416">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="a8aad-417">La información se inserta como una tarjeta de formato automático fácil de leer, lo que ayuda a los usuarios a mantener la conversación.</span><span class="sxs-lookup"><span data-stu-id="a8aad-417">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="a8aad-418">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-418">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Aplicación de búsqueda de lista](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="a8aad-420">Check-ins del personal</span><span class="sxs-lookup"><span data-stu-id="a8aad-420">Staff Check-ins</span></span>

<span data-ttu-id="a8aad-421">Staff Check-ins es una aplicación basada en [Power Apps](/powerapps/powerapps-overview)que permite la comunicación de supervisión entre tu empresa y el personal de campo.</span><span class="sxs-lookup"><span data-stu-id="a8aad-421">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="a8aad-422">El personal puede proporcionar fácilmente información crítica de tiempo y actualizaciones de estado de forma programada o ad hoc directamente desde Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-422">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="a8aad-423">La aplicación admite la ubicación en tiempo real, fotos y notas, así como notificaciones de aviso y flujos de trabajo automatizados.</span><span class="sxs-lookup"><span data-stu-id="a8aad-423">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="a8aad-424">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-424">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Crear vista de check-in](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="a8aad-426">Encuesta</span><span class="sxs-lookup"><span data-stu-id="a8aad-426">Survey</span></span>

<span data-ttu-id="a8aad-427">Survey es una aplicación de extensión de mensajería de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) personalizada que te permite crear una encuesta en un chat o un canal para recopilar datos y obtener información útil.</span><span class="sxs-lookup"><span data-stu-id="a8aad-427">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="a8aad-428">La aplicación se admite en todos los clientes de plataforma de Teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="a8aad-428">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="a8aad-429">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-429">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Crear encuesta en la vista Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally-9734"></a><span data-ttu-id="a8aad-431">Time Tally &#9734;</span><span class="sxs-lookup"><span data-stu-id="a8aad-431">Time Tally &#9734;</span></span>

<span data-ttu-id="a8aad-432">Un proyecto puede incluir varias tareas y varios proyectos se pueden asignar a los empleados.</span><span class="sxs-lookup"><span data-stu-id="a8aad-432">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="a8aad-433">Los administradores deben comprender el progreso del proyecto durante el tiempo invertido por los empleados en estas tareas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-433">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="a8aad-434">Puede ser una actividad engorrosa, ya que los empleados deben rellenar los partes de horas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-434">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="a8aad-435">La aplicación Time Tally permite a los empleados rellenar sus partes de horas rápidamente, con el dispositivo móvil, y los administradores no tienen que realizar un seguimiento con los empleados en la entrada del parte de horas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-435">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="a8aad-436">Los administradores pueden ver el uso del proyecto en función de los recursos y pueden aprobar o rechazar las entradas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-436">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="a8aad-437">Las notificaciones de aviso se envían para garantizar el cumplimiento del parte de horas.</span><span class="sxs-lookup"><span data-stu-id="a8aad-437">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="a8aad-438">Además, los datos históricos y los usos están disponibles para el análisis.</span><span class="sxs-lookup"><span data-stu-id="a8aad-438">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="a8aad-439">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-439">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Recuento de horas](../assets/images/11zon_gif.gif)


## <a name="virtual-rounding"></a><span data-ttu-id="a8aad-441">Redondeo virtual</span><span class="sxs-lookup"><span data-stu-id="a8aad-441">Virtual Rounding</span></span>

<span data-ttu-id="a8aad-442">Los proveedores de hospitales y de sala de emergencias hacen decenas y, a menudo, cientos de **rondas** al día.</span><span class="sxs-lookup"><span data-stu-id="a8aad-442">Hospital and emergency room providers make dozens, and often hundreds of **rounds** per day.</span></span> <span data-ttu-id="a8aad-443">Estas rápidas check-ins en los pacientes están diseñadas para proporcionar una comprobación de estado sobre cómo está el paciente y asegurarse de que se aborde la preocupación del paciente.</span><span class="sxs-lookup"><span data-stu-id="a8aad-443">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="a8aad-444">Aunque el redondeo es una práctica esencial para garantizar que los pacientes están siendo supervisados por varios tipos de proveedores, representan un enorme desagüe en el EPP, ya que para cada visita, de cada proveedor, se debe usar una máscara nueva y un nuevo conjunto de guantes.</span><span class="sxs-lookup"><span data-stu-id="a8aad-444">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="a8aad-445">Con estas plantillas de aplicación, los trabajadores médicos pueden realizar fácilmente rondas virtualmente, a través de una reunión de Microsoft Teams entre el proveedor y el paciente.</span><span class="sxs-lookup"><span data-stu-id="a8aad-445">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="a8aad-446">También se hace referencia a la solución de redondeo virtual en la entrada de [blog](https://aka.ms/teamsvirtualrounding)Microsoft Health and Life Sciences .</span><span class="sxs-lookup"><span data-stu-id="a8aad-446">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="a8aad-447">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-447">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Redondeo virtual](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="a8aad-449">Administración de visitantes</span><span class="sxs-lookup"><span data-stu-id="a8aad-449">Visitor Management</span></span>

<span data-ttu-id="a8aad-450">La aplicación Administración de visitantes permite a su organización y a los empleados administrar de forma fácil y eficaz el proceso de visitantes en el sitio, directamente desde Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aad-450">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="a8aad-451">La aplicación permite a los empleados crear solicitudes de visitantes, realizar un seguimiento centralizado de un estado de solicitud a través del panel de visitantes y recibir notificaciones en tiempo real cuando llega un visitante.</span><span class="sxs-lookup"><span data-stu-id="a8aad-451">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="a8aad-452">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-452">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="a8aad-455">Workplace Awards</span><span class="sxs-lookup"><span data-stu-id="a8aad-455">Workplace Awards</span></span>

<span data-ttu-id="a8aad-456">Workplace Awards es una plantilla de aplicación de Teams que proporciona un marco positivo para fomentar el reconocimiento y fomentar la cultura de la apreciación de los empleados en el lugar de trabajo moderno.</span><span class="sxs-lookup"><span data-stu-id="a8aad-456">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="a8aad-457">La aplicación te permite configurar y administrar un programa de reconocimiento y recompensas de empleados (R&R) en el que los empleados pueden designar y aprobar fácilmente a los compañeros y el líder de R&R puede ver las nominaciones enviadas, conceder premios y anunciar destinatarios.</span><span class="sxs-lookup"><span data-stu-id="a8aad-457">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="a8aad-458">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="a8aad-458">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="a8aad-459">Tarjeta de nominación de los premios workplace</span><span class="sxs-lookup"><span data-stu-id="a8aad-459">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Pestaña Lista de reconocimientos de lugares de trabajo](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="a8aad-461">¿Tienes una idea de una plantilla de aplicación que quieras ver?</span><span class="sxs-lookup"><span data-stu-id="a8aad-461">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="a8aad-462">[Por favor, háganos saber](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span><span class="sxs-lookup"><span data-stu-id="a8aad-462">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
