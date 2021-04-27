---
title: Plantillas de aplicación de Microsoft Teams
description: Vínculos y descripciones de plantillas de aplicación para la plataforma de Microsoft Teams
ms.topic: reference
keywords: Demostración de ejemplos de plantillas de Microsoft Teams
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 58cda9f400081a47bb9bebf20ba509ee3623dc0b
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020524"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="7feb5-104">Plantillas de aplicaciones para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7feb5-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="7feb5-105">Las plantillas de aplicación son ejemplos de aplicaciones completas para Microsoft Teams que son de código abierto y están disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="7feb5-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="7feb5-106">Cada plantilla de aplicación contiene instrucciones detalladas para implementar e instalar esa aplicación para la organización.</span><span class="sxs-lookup"><span data-stu-id="7feb5-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="7feb5-107">También proporciona una aplicación de ejemplo que puedes instalar y empezar a usar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="7feb5-107">It also provides a sample app that you can install and start using immediately.</span></span> <span data-ttu-id="7feb5-108">El código fuente completo también está disponible, lo que le permite explorarlo en detalle o bifurcar el código y modificarlo para satisfacer sus requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-108">The complete source code is also available, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="7feb5-109">Todas las plantillas de aplicación se proporcionan en los términos [de licencia mit.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="7feb5-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>

> [!NOTE] 
> <span data-ttu-id="7feb5-110">Debes licenciar y admitir aplicaciones creadas a partir de plantillas de aplicación para tus usuarios y organizaciones.</span><span class="sxs-lookup"><span data-stu-id="7feb5-110">You must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="7feb5-111">**&#9734; indica las plantillas de aplicación recién publicadas.**</span><span class="sxs-lookup"><span data-stu-id="7feb5-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="7feb5-112">Ventajas clave</span><span class="sxs-lookup"><span data-stu-id="7feb5-112">Key benefits</span></span>

* <span data-ttu-id="7feb5-113">**Implemente directamente en la nube:** Todas las plantillas de aplicación incluyen scripts de implementación que le permiten hospedar todos los servicios necesarios en Microsoft Azure o power platform.</span><span class="sxs-lookup"><span data-stu-id="7feb5-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="7feb5-114">**Código de ejemplo recomendado:** Las plantillas de la aplicación se ajustan a los procedimientos recomendados en materia de seguridad e infraestructura.</span><span class="sxs-lookup"><span data-stu-id="7feb5-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="7feb5-115">Se revisan todos los cambios enviados por la comunidad a las plantillas de la aplicación para garantizar la conformidad.</span><span class="sxs-lookup"><span data-stu-id="7feb5-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="7feb5-116">**Personalizable y extensible:** Aunque todas las plantillas de aplicación se implementan con una configuración mínima, se proporcionan todos los scripts de implementación y base de código completos, para que puedas personalizarlas o ampliarlas fácilmente para que se ajusten a tus necesidades únicas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-116">**Customizable and extensible:** While all app templates are deployed with minimal configuration, the entire code base and deployment scripts are provided, so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="7feb5-117">**Documentación detallada:** Todas las plantillas de aplicación van acompañadas de documentación completa sobre los pasos de configuración, implementación y arquitectura de soluciones.</span><span class="sxs-lookup"><span data-stu-id="7feb5-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="7feb5-118">Bot de adopción</span><span class="sxs-lookup"><span data-stu-id="7feb5-118">Adoption Bot</span></span> 

<span data-ttu-id="7feb5-119">Bot de adopción es un bot de chat de atención al usuario creado con Power Virtual Agent para PVA de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams PVA.</span></span> <span data-ttu-id="7feb5-120">Se considera como la versión PVA de FAQ Plus.</span><span class="sxs-lookup"><span data-stu-id="7feb5-120">It is considered as the PVA version of FAQ Plus.</span></span> <span data-ttu-id="7feb5-121">Bot de adopción responde a más de 100 preguntas comunes sobre Microsoft 365 y Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="7feb5-122">Puede editar los temas existentes, agregar sus propios temas e ingerir preguntas frecuentes existentes.</span><span class="sxs-lookup"><span data-stu-id="7feb5-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="7feb5-123">Si los usuarios necesitan ayuda adicional, el Bot de adopción puede conectarlos a expertos o incluso extenderse para abrir vales de servicio con conectores de flujo premium.</span><span class="sxs-lookup"><span data-stu-id="7feb5-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span> <span data-ttu-id="7feb5-124">Este bot se instala automáticamente o se basa en una aplicación personalizada, como el Centro [de adopción.](https://github.com/akporzondek/adoption_hub)</span><span class="sxs-lookup"><span data-stu-id="7feb5-124">This bot is self-installed or built into a custom app, such as the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="7feb5-125">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a><span data-ttu-id="7feb5-126">Herramienta de adopción: plataforma de administración de campeones &#9734;</span><span class="sxs-lookup"><span data-stu-id="7feb5-126">Adoption Tool- Champion Management Platform &#9734;</span></span>

<span data-ttu-id="7feb5-127">La plantilla de aplicación Champion Management Platform (CMP) te ayuda a administrar, escalar e inspirar a los campeones del trabajo en equipo para lograr más.</span><span class="sxs-lookup"><span data-stu-id="7feb5-127">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="7feb5-128">Esta plantilla de aplicación se basa en SharePoint Framework y se carga en una pestaña dentro de un equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-128">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="7feb5-129">Los grupos pueden aprovechar esta herramienta para ayudar a administrar la pertenencia al programa, proporcionar una tabla de clasificación y tipos de eventos para el registro y herramientas para superponer distintivos digitales a los participantes del programa.</span><span class="sxs-lookup"><span data-stu-id="7feb5-129">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="7feb5-130">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-130">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a><span data-ttu-id="7feb5-131">Herramienta de adopción: rutas de aprendizaje de Microsoft 365 (introducción) &#9734;</span><span class="sxs-lookup"><span data-stu-id="7feb5-131">Adoption Tool- Microsoft 365 Learning Pathways (Get Started) &#9734;</span></span>

<span data-ttu-id="7feb5-132">La plantilla de aplicación Introducción te permite aportar la potencia de las rutas de aprendizaje de Microsoft 365 dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-132">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="7feb5-133">Esta plantilla de aplicación te permite conceder un fácil acceso a páginas de aprendizaje específicas u otros activos de intranet y cargar el contenido directamente en Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-133">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="7feb5-134">También puedes cambiar el nombre o el logotipo de la aplicación para que coincida con la personalción de marca de tu empresa.</span><span class="sxs-lookup"><span data-stu-id="7feb5-134">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="7feb5-135">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-135">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="7feb5-136">Administrador de citas</span><span class="sxs-lookup"><span data-stu-id="7feb5-136">Appointment Manager</span></span> 

<span data-ttu-id="7feb5-137">Appointment Manager es una plantilla de aplicación de Teams para ayudar a las empresas a crear, administrar y llevar a cabo citas virtuales con consumidores a través de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-137">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="7feb5-138">Las nuevas solicitudes de cita de los consumidores son visibles en los canales de Teams, donde se asignan y reasignan rápidamente al personal de un equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-138">New appointment requests from consumers are visible in Teams channels, where they are quickly assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="7feb5-139">Las solicitudes de cita se ven en niveles de equipo o personales a través de pestañas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-139">Appointment requests are viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="7feb5-140">Cada cita está asociada a una reunión en línea de Teams, por lo que el personal y los consumidores pueden unirse fácilmente a la reunión en el momento programado.</span><span class="sxs-lookup"><span data-stu-id="7feb5-140">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="7feb5-141">La plantilla de aplicación se integra con Microsoft Bookings para facilitar la administración de citas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-141">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="7feb5-142">Las citas programadas aparecen automáticamente en los calendarios de los miembros del personal asignados y los consumidores reciben notificaciones y avisos de correo electrónico personalizables con vínculos de reunión incrustados.</span><span class="sxs-lookup"><span data-stu-id="7feb5-142">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="7feb5-143">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="7feb5-144">![Administrador de citas Overview ](../assets/images/appointment-manager-overview.png)
 ![ Appointment Manager en Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="7feb5-144">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="7feb5-145">Preguntar fuera</span><span class="sxs-lookup"><span data-stu-id="7feb5-145">Ask Away</span></span>

<span data-ttu-id="7feb5-146">Ask Away es un [bot de Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios realizar preguntas y respuestas, denominadaS&sesiones A dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-146">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Question and Answer, called Q&A sessions within Teams.</span></span> <span data-ttu-id="7feb5-147">Con el bot Preguntar, los miembros del equipo pueden enviar y votar por arriba preguntas compartidas por compañeros, lo que permite que los hosts de preguntas&A recopile fácilmente las preguntas más importantes dentro de un canal o chat.</span><span class="sxs-lookup"><span data-stu-id="7feb5-147">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="7feb5-148">El bot se usa para realizar una Q en tiempo real&Una sesión en una reunión de Teams y permite a los asistentes enviar preguntas en directo a través del chat.</span><span class="sxs-lookup"><span data-stu-id="7feb5-148">The bot is used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live through chat.</span></span>

[<span data-ttu-id="7feb5-149">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-149">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Vista del cuadro de diálogo emergente de la tabla de clasificación para que los usuarios voten sobre las preguntas](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="7feb5-151">Información de asociados</span><span class="sxs-lookup"><span data-stu-id="7feb5-151">Associate Insights</span></span>

<span data-ttu-id="7feb5-152">Associate Insights es una plantilla [de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que permite a los trabajadores de primera línea capturar y enviar directamente la opinión, el sentimiento y la percepción del cliente.</span><span class="sxs-lookup"><span data-stu-id="7feb5-152">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="7feb5-153">Los trabajadores de primera línea suelen ser el primer representante de la compañía en interactuar con los clientes en un punto a uno de contacto.</span><span class="sxs-lookup"><span data-stu-id="7feb5-153">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="7feb5-154">Los equipos empresariales comparten y usan los datos recopilados de forma colaborativa, como a través de una pestaña de Power BI Teams, para mejorar la experiencia del cliente y mejorar la experiencia del producto.</span><span class="sxs-lookup"><span data-stu-id="7feb5-154">The collected data are shared and used collaboratively by business teams, such as through a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="7feb5-155">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-155">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

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

## <a name="attendance"></a><span data-ttu-id="7feb5-158">Asistencia</span><span class="sxs-lookup"><span data-stu-id="7feb5-158">Attendance</span></span>

<span data-ttu-id="7feb5-159">La aplicación Asistencia es una [pestaña Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) anclada en un equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-159">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that are pinned in a team.</span></span> <span data-ttu-id="7feb5-160">Está diseñado para registrar la presencia en configuraciones, como entornos de aprendizaje y aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="7feb5-160">It is designed to record presence in settings, such as learning and training environments.</span></span> <span data-ttu-id="7feb5-161">Los usuarios pueden marcar o editar la asistencia durante un máximo de 30 días en el pasado y ver informes de asistencia resumidos para un grupo completo o asistentes individuales.</span><span class="sxs-lookup"><span data-stu-id="7feb5-161">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span> <span data-ttu-id="7feb5-162">Para obtener más información sobre la asistencia de equipos, consulte [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span><span class="sxs-lookup"><span data-stu-id="7feb5-162">For more information on teams attendance, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span></span>

<span data-ttu-id="7feb5-163">La siguiente imagen muestra la demostración de la aplicación de asistencia:</span><span class="sxs-lookup"><span data-stu-id="7feb5-163">The following image displays the attendance app demo:</span></span>  

![Demostración de la aplicación de asistencia](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="7feb5-165">Libro a sala</span><span class="sxs-lookup"><span data-stu-id="7feb5-165">Book-a-room</span></span>

<span data-ttu-id="7feb5-166">Book-a-room es un bot de [Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30, 60 o 90 minutos a partir de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="7feb5-166">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="7feb5-167">El tiempo predeterminado es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-167">The default time is 30 minutes.</span></span> <span data-ttu-id="7feb5-168">El bot Book-a-room tiene ámbitos para conversaciones personales o 1:1.</span><span class="sxs-lookup"><span data-stu-id="7feb5-168">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="7feb5-169">Para obtener más información sobre la aplicación Book-a-room, consulte [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span><span class="sxs-lookup"><span data-stu-id="7feb5-169">For more information on Book-a-room app, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span></span>  
<span data-ttu-id="7feb5-170">En la siguiente imagen se muestra la demostración libro a sala:</span><span class="sxs-lookup"><span data-stu-id="7feb5-170">The following image displays the Book-a-room demo:</span></span>

![Demostración de libro a sala](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="7feb5-172">Acceso de creación</span><span class="sxs-lookup"><span data-stu-id="7feb5-172">Building Access</span></span>

<span data-ttu-id="7feb5-173">Building Access es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que admite la administración de umbrales de ocupación y normas de distanciamiento social al permitir a los directores de instalaciones administrar, realizar un seguimiento e informar de la presencia de los empleados en el sitio.</span><span class="sxs-lookup"><span data-stu-id="7feb5-173">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="7feb5-174">La aplicación, creada con Microsoft [Power Apps](/powerapps/powerapps-overview)y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams y permite a las organizaciones determinar la preparación de la creación, establecer criterios de elegibilidad para el acceso en el sitio y recopilar información para la planeación futura.</span><span class="sxs-lookup"><span data-stu-id="7feb5-174">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="7feb5-175">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-175">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Crear tarjeta de reserva de Access](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Creación de la vista clave de Access](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="7feb5-178">Celebraciones</span><span class="sxs-lookup"><span data-stu-id="7feb5-178">Celebrations</span></span>

<span data-ttu-id="7feb5-179">Celebraciones es una aplicación de Teams que ayuda a los miembros del equipo a celebrar los cumpleaños, aniversarios y otros eventos periódicos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-179">Celebrations is a Teams app that helps team members to celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="7feb5-180">Recuerda ocasiones especiales de todos los miembros del equipo y envía un mensaje descriptivo en todos los equipos seleccionados en el momento de la creación de eventos, para que los miembros del equipo se sientan especiales en su día.</span><span class="sxs-lookup"><span data-stu-id="7feb5-180">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="7feb5-181">La aplicación proporciona una interfaz sencilla para que todos los miembros del equipo agreguen y visualen personalmente sus eventos y también permite al usuario seleccionar los equipos en los que se comparten los eventos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-181">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="7feb5-182">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-182">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="7feb5-183">Lista de comprobación</span><span class="sxs-lookup"><span data-stu-id="7feb5-183">Checklist</span></span>

<span data-ttu-id="7feb5-184">Lista de comprobación es una aplicación de extensión [de](../messaging-extensions/what-are-messaging-extensions.md) mensajería personalizada de Microsoft Teams que te permite colaborar con tu equipo creando una lista de comprobación compartida en un chat o canal.</span><span class="sxs-lookup"><span data-stu-id="7feb5-184">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="7feb5-185">La aplicación se admite en todos los clientes de plataforma de Teams, como el explorador de escritorio, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="7feb5-185">The app is supported across all Teams platform clients, such as desktop browser, iOS, and Android.</span></span> <span data-ttu-id="7feb5-186">La aplicación está lista para la implementación como parte de la suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="7feb5-186">The app is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="7feb5-187">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-187">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![Crear lista de comprobación en la vista Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="7feb5-189">Classroom Drop-in</span><span class="sxs-lookup"><span data-stu-id="7feb5-189">Classroom Drop-in</span></span> 

<span data-ttu-id="7feb5-190">Classroom Drop-in es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que permite a los líderes del sistema encontrar equipos de clase, significa aulas virtuales y agregarse a sí mismos u otros a estos equipos de clase durante un período de entrega especificado, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7feb5-190">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams, means virtual classrooms and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="7feb5-191">La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate](/power-automate/getting-started)se integra profundamente con Microsoft Teams para garantizar que los institutos educativos puedan optimizar sus operaciones en un entorno de aprendizaje híbrido proporcionando acceso a partes interesadas relevantes para los equipos de clase por requisitos empresariales.</span><span class="sxs-lookup"><span data-stu-id="7feb5-191">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="7feb5-192">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-192">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Solicitud de acceso a clases](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="7feb5-194">Comunicador de la empresa</span><span class="sxs-lookup"><span data-stu-id="7feb5-194">Company Communicator</span></span>

<span data-ttu-id="7feb5-195">La aplicación Communicator empresa permite a los equipos corporativos crear y enviar mensajes destinados a varios equipos o a un gran número de empleados a través del chat, lo que permite que la organización llegue a los empleados justo donde colaboran.</span><span class="sxs-lookup"><span data-stu-id="7feb5-195">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="7feb5-196">Use esta plantilla para varios escenarios, como anuncios de nuevas iniciativas, incorporación de empleados, aprendizaje y desarrollo modernos o difusión en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="7feb5-196">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="7feb5-197">La aplicación proporciona una interfaz sencilla para que los usuarios designados creen, obtengan una vista previa, colaboren y envíen mensajes.</span><span class="sxs-lookup"><span data-stu-id="7feb5-197">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="7feb5-198">Proporciona una base para crear capacidades de comunicación personalizadas dirigidas, como telemetría personalizada, sobre cuántos usuarios han reconocido o interactuado con un mensaje.</span><span class="sxs-lookup"><span data-stu-id="7feb5-198">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="7feb5-199">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-199">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator de cuadro de redacción](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="7feb5-201">Búsqueda de grupos de contactos</span><span class="sxs-lookup"><span data-stu-id="7feb5-201">Contact Group Lookup</span></span>

<span data-ttu-id="7feb5-202">La aplicación Búsqueda de grupos de contactos proporciona un enfoque práctico y útil para crear, acceder y administrar los grupos de contactos de la organización, anteriormente conocidos como listas de distribución o grupos de comunicación.</span><span class="sxs-lookup"><span data-stu-id="7feb5-202">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups, formerly known as distribution lists or communication groups.</span></span> <span data-ttu-id="7feb5-203">Los usuarios pueden ver y chatear rápidamente con miembros del grupo, ver el estado de los miembros y crear un chat de grupo con miembros seleccionados en el grupo de contactos, todo dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-203">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="7feb5-204">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-204">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

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

## <a name="co-worker-appreciation"></a><span data-ttu-id="7feb5-207">Apreciación del compañero de trabajo</span><span class="sxs-lookup"><span data-stu-id="7feb5-207">Co-worker Appreciation</span></span> 

<span data-ttu-id="7feb5-208">Con la plantilla de apreciación de compañeros de trabajo en Microsoft Teams, los usuarios pueden reconocer los logros de sus compañeros en el contexto de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-208">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="7feb5-209">Cuando los compañeros de trabajo seleccionan recompensar a un compañero, los destinatarios y otros miembros del equipo se etiquetan en una conversación de canal y reciben una notificación sobre los detalles de la concesión del canal.</span><span class="sxs-lookup"><span data-stu-id="7feb5-209">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="7feb5-210">Los galardones se registran en la aplicación teams, que es segura, portátil y fácilmente compartible.</span><span class="sxs-lookup"><span data-stu-id="7feb5-210">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="7feb5-211">Esto se considera como la versión basada en PowerApps de la plantilla de aplicación Open Badges, con una tabla de clasificación.</span><span class="sxs-lookup"><span data-stu-id="7feb5-211">This is considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="7feb5-212">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-212">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![General](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="7feb5-214">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="7feb5-214">CrowdSourcer</span></span>

<span data-ttu-id="7feb5-215">CrowdSourcer es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona a los equipos información consultada procedente de forma colaborativa de miembros del grupo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-215">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="7feb5-216">Ayuda a responder a las preguntas más frecuentes a la vez que permite a los participantes participar activamente y contribuir a un recurso de información divertido y útil.</span><span class="sxs-lookup"><span data-stu-id="7feb5-216">It helps to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="7feb5-217">Obtenerlo en Github</span><span class="sxs-lookup"><span data-stu-id="7feb5-217">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interacción entre usuarios finales de Crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="7feb5-219">Adhesivos personalizados</span><span class="sxs-lookup"><span data-stu-id="7feb5-219">Custom Stickers</span></span>

<span data-ttu-id="7feb5-220">La autoexpresión es fundamental para una cultura de equipo en buen estado.</span><span class="sxs-lookup"><span data-stu-id="7feb5-220">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="7feb5-221">Esta plantilla de aplicación es una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) que permite a los usuarios usar adhesivos y GIF personalizados dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-221">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="7feb5-222">Esta plantilla proporciona una experiencia de configuración sencilla basada en web en la que cualquier persona con acceso a la configuración puede cargar los GIF, adhesivos e imágenes que desean que tengan sus usuarios, lo que permite a todo el equipo usar cualquier conjunto de adhesivos que elija.</span><span class="sxs-lookup"><span data-stu-id="7feb5-222">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs, stickers, and images they want their users to have, allowing your entire team to use any set of stickers you choose.</span></span>

<span data-ttu-id="7feb5-223">Esta aplicación también permite compartir fácilmente imágenes, GIF, adhesivos entre equipos sin necesidad de tener acceso a sitios de SharePoint o canales individuales como mecanismos de almacenamiento y uso compartido.</span><span class="sxs-lookup"><span data-stu-id="7feb5-223">This app also enables easy sharing of images, GIFs, stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="7feb5-224">Por ejemplo, los equipos de productos pueden compartir fácilmente imágenes de producto y GIF a redes sociales, equipos de marketing y ventas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="7feb5-224">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="7feb5-225">También se puede extender esta aplicación desencadenando un flujo de notificación a equipos o individuos específicos cuando se hacen disponibles imágenes nuevas y GIF.</span><span class="sxs-lookup"><span data-stu-id="7feb5-225">One can also extend this app by triggering a notification flow to specific teams or individuals when new images, and GIFs are made available.</span></span>

[<span data-ttu-id="7feb5-226">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-226">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Aplicación Stickers](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="7feb5-228">Ideas de los empleados</span><span class="sxs-lookup"><span data-stu-id="7feb5-228">Employee Ideas</span></span>

<span data-ttu-id="7feb5-229">La aplicación Ideas para empleados es la versión de PowerApps de la plantilla de aplicación Great Ideas basada en Azure.</span><span class="sxs-lookup"><span data-stu-id="7feb5-229">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="7feb5-230">La aplicación permite a los usuarios de Teams configurar y configurar una campaña de ideas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-230">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="7feb5-231">Una campaña de ideas es una categoría para agrupar ideas en torno a temas comunes.</span><span class="sxs-lookup"><span data-stu-id="7feb5-231">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="7feb5-232">Los usuarios de Teams también pueden realizar las siguientes actividades:</span><span class="sxs-lookup"><span data-stu-id="7feb5-232">Teams users can also perform the following activities:</span></span>

* <span data-ttu-id="7feb5-233">Configure un formulario de envío estándar que los empleados deben enviar para cada idea.</span><span class="sxs-lookup"><span data-stu-id="7feb5-233">Configure a standard submission form that employees must submit for each idea.</span></span> 
* <span data-ttu-id="7feb5-234">Revisa y administra las ideas y la lista de campañas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-234">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="7feb5-235">Modificar y eliminar campañas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-235">Modify and delete campaigns.</span></span>
* <span data-ttu-id="7feb5-236">Revisar las tablas de ideas de líderes.</span><span class="sxs-lookup"><span data-stu-id="7feb5-236">Review leader boards of ideas.</span></span>
* <span data-ttu-id="7feb5-237">Vota y comparte ideas priorizadas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-237">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="7feb5-238">Enviar ideas para una campaña.</span><span class="sxs-lookup"><span data-stu-id="7feb5-238">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="7feb5-239">Ver la idea de otro miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-239">View other team member's idea.</span></span>
* <span data-ttu-id="7feb5-240">Vota sobre las ideas que más te gustan.</span><span class="sxs-lookup"><span data-stu-id="7feb5-240">Vote on most liked ideas.</span></span>
* <span data-ttu-id="7feb5-241">Revisa el rendimiento de sus ideas en comparación con otras personas dentro de una campaña.</span><span class="sxs-lookup"><span data-stu-id="7feb5-241">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="7feb5-242">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-242">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Administrar vista de campaña](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="7feb5-244">E-Prescriptions</span><span class="sxs-lookup"><span data-stu-id="7feb5-244">E-Prescriptions</span></span> 

<span data-ttu-id="7feb5-245">E-Prescriptions es una aplicación basada en [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que mejora la telemedicina y el cuidado virtual automatizando el proceso de emisión de recetas electrónicas a los pacientes.</span><span class="sxs-lookup"><span data-stu-id="7feb5-245">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="7feb5-246">Los profesionales médicos pueden revisar rápidamente las citas, generar recetas electrónicas y enviar correos electrónicos con datos adjuntos de la receta electrónica a los pacientes directamente en la plataforma teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-246">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="7feb5-247">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-247">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

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

## <a name="employee-training"></a><span data-ttu-id="7feb5-252">Formación de empleados</span><span class="sxs-lookup"><span data-stu-id="7feb5-252">Employee Training</span></span> 

<span data-ttu-id="7feb5-253">La formación de los empleados es una aplicación de Microsoft Teams que permite a los organizadores publicar, realizar un seguimiento y promover fácilmente eventos de aprendizaje y aprendizaje para su organización.</span><span class="sxs-lookup"><span data-stu-id="7feb5-253">Employee training is a Microsoft Teams app that enables organizers to easily publish, track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="7feb5-254">Con la aplicación, los organizadores de eventos pueden enviar avisos y notificaciones a los registradores de eventos y los empleados pueden indicar interés en los próximos eventos, mantenerse actualizados sobre los eventos actuales y compartir detalles de eventos con compañeros a través de la extensión de mensajería de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-254">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues through the Teams messaging extension.</span></span>

[<span data-ttu-id="7feb5-255">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="7feb5-256">**Ver eventos de formación de empleados** ![ Imagen de pestaña Formación de los empleados](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="7feb5-256">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="7feb5-257">**Crear evento de formación de empleados** ![ Formulario de creación de eventos de formación para empleados](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="7feb5-257">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="7feb5-258">Buscador de expertos</span><span class="sxs-lookup"><span data-stu-id="7feb5-258">Expert Finder</span></span>

<span data-ttu-id="7feb5-259">Expert Finder es un [bot de Microsoft Teams](../bots/what-are-bots.md) que identifica miembros específicos de la organización en función de sus aptitudes, intereses y atributos educativos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-259">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="7feb5-260">Los miembros encuentran expertos dentro de una organización que coinciden con una búsqueda de palabras clave de perfiles de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7feb5-260">Members find experts within an organization that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="7feb5-261">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Demostración de resultados de búsqueda del Buscador de expertos](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="7feb5-263">Preguntas más frecuentes Plus</span><span class="sxs-lookup"><span data-stu-id="7feb5-263">FAQ Plus</span></span>

<span data-ttu-id="7feb5-264">Preguntas conversacionales&Bots son una forma sencilla de proporcionar respuestas a las preguntas más frecuentes de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7feb5-264">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="7feb5-265">Sin embargo, la mayoría de los bots no pueden interactuar con los usuarios de forma significativa porque no hay ningún humano en el bucle cuando se produce un error en el bot.</span><span class="sxs-lookup"><span data-stu-id="7feb5-265">But, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="7feb5-266">Faq bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span><span class="sxs-lookup"><span data-stu-id="7feb5-266">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="7feb5-267">Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-267">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="7feb5-268">Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde el propio equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-268">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="7feb5-269">La versión más reciente de **FAQ Plus** admite resoluciones de preguntas&A al permitir a un equipo de expertos completar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7feb5-269">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="7feb5-270">&#x2714; agregar nuevas preguntas&Como directamente a la base de conocimientos mediante extensiones de mensaje.</span><span class="sxs-lookup"><span data-stu-id="7feb5-270">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="7feb5-271">&#x2714; Editar y eliminar preguntas&Pares agregados por un bot.</span><span class="sxs-lookup"><span data-stu-id="7feb5-271">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="7feb5-272">&#x2714; seguimiento del historial de revisiones de Q&As.</span><span class="sxs-lookup"><span data-stu-id="7feb5-272">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="7feb5-273">&#x2714; configurar una respuesta con detalles adicionales para mostrar como [una tarjeta adaptable](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span><span class="sxs-lookup"><span data-stu-id="7feb5-273">&#x2714; Configure an answer with additional details to display as an [Adaptive Card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="7feb5-274">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif de preguntas más frecuentes](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="7feb5-276">Obtener aplicación de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="7feb5-276">Get Support App</span></span>

<span data-ttu-id="7feb5-277">Las organizaciones que usan Microsoft Teams usan la aplicación Obtener soporte técnico para permitir que cualquier conjunto de usuarios solicite asistencia a los supervisores.</span><span class="sxs-lookup"><span data-stu-id="7feb5-277">The Get Support app is used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="7feb5-278">Esta aplicación incluye las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="7feb5-278">This app includes the following features:</span></span>
* <span data-ttu-id="7feb5-279">Solicitar asistencia en distintas categorías desde una Power App.</span><span class="sxs-lookup"><span data-stu-id="7feb5-279">Requesting assistance on different categories from a Power App.</span></span>
* <span data-ttu-id="7feb5-280">Notificaciones enviadas a los solicitantes que les informan de quién tiene asignada la liebre.</span><span class="sxs-lookup"><span data-stu-id="7feb5-280">Notifications sent to requestors informing them of who hare assigned.</span></span>
* <span data-ttu-id="7feb5-281">Notificaciones enviadas a supervisores asignados que les informan de quién necesita asistencia.</span><span class="sxs-lookup"><span data-stu-id="7feb5-281">Notifications sent to assigned supervisors informing them of who needs assistance.</span></span> 
* <span data-ttu-id="7feb5-282">Análisis de escalaciones y patrones en SharePoint y PowerBI.S</span><span class="sxs-lookup"><span data-stu-id="7feb5-282">Analyzing escalations and patterns in SharePoint and PowerBI.S</span></span>

[<span data-ttu-id="7feb5-283">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-283">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Obtener gif de soporte técnico](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="7feb5-285">Rastreador de objetivos</span><span class="sxs-lookup"><span data-stu-id="7feb5-285">Goal Tracker</span></span>

<span data-ttu-id="7feb5-286">La aplicación Rastreador de objetivos es una solución completa para que su organización admita el establecimiento de objetivos, la observación del progreso y el reconocimiento del éxito en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-286">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="7feb5-287">La aplicación permite a los usuarios establecer, realizar un seguimiento y actualizar objetivos en un nivel profesional, personal y de equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-287">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="7feb5-288">Los miembros del equipo también reciben avisos oportunos y actualizaciones de estado para mantenerse centrados y mantenerse al día.</span><span class="sxs-lookup"><span data-stu-id="7feb5-288">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="7feb5-289">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-289">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a><span data-ttu-id="7feb5-292">Grandes ideas</span><span class="sxs-lookup"><span data-stu-id="7feb5-292">Great Ideas</span></span>

<span data-ttu-id="7feb5-293">La aplicación Great Ideas admite y potencia la innovación y la creatividad dentro de la organización.</span><span class="sxs-lookup"><span data-stu-id="7feb5-293">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="7feb5-294">La aplicación permite a los empleados compartir ideas con compañeros y líderes, descubrir nuevos envíos, contribuciones destacadas para la consideración del mismo nivel y emitir su voto para las mejores propuestas dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-294">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="7feb5-295">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-295">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="7feb5-298">Actividades de grupo</span><span class="sxs-lookup"><span data-stu-id="7feb5-298">Group Activities</span></span>

<span data-ttu-id="7feb5-299">Actividades de grupo es una aplicación de Microsoft Teams que facilita a los propietarios de equipos crear rápidamente grupos de actividades y administrar flujos de trabajo de colaboración en el contexto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-299">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="7feb5-300">Los autores de actividades están habilitados para crear actividades, distribuir aleatoriamente miembros del equipo en grupos y, opcionalmente, hacer que el bot envíe avisos hasta que se completen las actividades.</span><span class="sxs-lookup"><span data-stu-id="7feb5-300">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="7feb5-301">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-301">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

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

## <a name="grow-your-skills"></a><span data-ttu-id="7feb5-304">Aumentar sus habilidades</span><span class="sxs-lookup"><span data-stu-id="7feb5-304">Grow Your Skills</span></span>

<span data-ttu-id="7feb5-305">La aplicación Crecer tus habilidades admite el crecimiento y el desarrollo profesionales, ya que permite a los empleados contribuir a proyectos complementarios para tu organización al mismo tiempo que aprenden nuevas habilidades.</span><span class="sxs-lookup"><span data-stu-id="7feb5-305">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="7feb5-306">Los empleados pueden usar la aplicación para buscar oportunidades que satisfagan sus intereses, disfrutar de una colaboración significativa con compañeros y adquirir nuevos niveles de experiencia y capacidades, todo dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-306">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="7feb5-307">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-307">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

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

## <a name="hr-support"></a><span data-ttu-id="7feb5-310">Soporte de Recursos Humanos</span><span class="sxs-lookup"><span data-stu-id="7feb5-310">HR Support</span></span>

<span data-ttu-id="7feb5-311">Bot de soporte técnico de RECURSOS es una pregunta&Un bot que lleva a un profesional de soporte técnico o experto del equipo de recursos humanos en el bucle cuando no puede ayudar.</span><span class="sxs-lookup"><span data-stu-id="7feb5-311">HR Support bot is a friendly Q&A bot that brings a support professional or expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="7feb5-312">Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-312">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="7feb5-313">Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde el propio equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-313">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="7feb5-314">Además, el bot sugiere vínculos a las directivas o preguntas de RECURSOS humanos recomendadas mediante la búsqueda de etiquetas preconfiguradas en la pregunta.</span><span class="sxs-lookup"><span data-stu-id="7feb5-314">Additionally, the bot suggests links to recommended HR policies or questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="7feb5-315">Estos iconos se encuentran en la pestaña asociada como una referencia rápida.</span><span class="sxs-lookup"><span data-stu-id="7feb5-315">These tiles are found in the associated tab as a quick reference.</span></span> <span data-ttu-id="7feb5-316">El soporte de recursos humanos funciona bien para preguntas&A y para proporcionar soporte rápido al iniciar nuevos proyectos o iniciativas en la organización.</span><span class="sxs-lookup"><span data-stu-id="7feb5-316">HR Support works well for light weight Q&A and to provide quick support when launching new projects or initiatives in the organization.</span></span>

[<span data-ttu-id="7feb5-317">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-317">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Soporte de Recursos Humanos](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="7feb5-319">Rompehielo</span><span class="sxs-lookup"><span data-stu-id="7feb5-319">Icebreaker</span></span>

<span data-ttu-id="7feb5-320">Icebreaker es un [bot de Microsoft Teams](../bots/what-are-bots.md) que ayuda a tu equipo a acercarse emparejando dos miembros del equipo aleatorios cada semana para reunirse.</span><span class="sxs-lookup"><span data-stu-id="7feb5-320">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="7feb5-321">El bot facilita la programación al sugerir automáticamente horas libres que funcionen para ambos miembros.</span><span class="sxs-lookup"><span data-stu-id="7feb5-321">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="7feb5-322">Fortalezca las conexiones personales y cree una comunidad estrechamente unida con esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="7feb5-322">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="7feb5-323">Además de fomentar las conexiones personales en todo el equipo, la aplicación Icebreaker puede ayudar a cultivar comunidades basadas en intereses dentro de la organización.</span><span class="sxs-lookup"><span data-stu-id="7feb5-323">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="7feb5-324">Por ejemplo, puedes usar esta aplicación para un grupo de interés de DevOps para ayudar a que las ideas y los procedimientos recomendados se extienda orgánicamente en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="7feb5-324">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="7feb5-325">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-325">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Aplicación Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="7feb5-327">Incentivos</span><span class="sxs-lookup"><span data-stu-id="7feb5-327">Incentives</span></span>

<span data-ttu-id="7feb5-328">Incentives es una plantilla [de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que administra y realiza un seguimiento de la participación de los empleados en actividades designadas, como cursos e iniciativas de administración de cambios.</span><span class="sxs-lookup"><span data-stu-id="7feb5-328">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities, such as trainings and change management initiatives.</span></span> <span data-ttu-id="7feb5-329">Los administradores usan la aplicación para establecer actividades designadas, asignar puntos para su finalización y especificar los niveles de puntos de elegibilidad necesarios para las recompensas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-329">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="7feb5-330">Los empleados usan la aplicación para ver sus puntos acumulados y, al alcanzar la elegibilidad, solicitar y reclamar recompensas canjeables.</span><span class="sxs-lookup"><span data-stu-id="7feb5-330">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="7feb5-331">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-331">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Demostración de aplicaciones de incentivos](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="7feb5-333">Reportero de incidentes</span><span class="sxs-lookup"><span data-stu-id="7feb5-333">Incident Reporter</span></span>

<span data-ttu-id="7feb5-334">Incident Reporter es un [bot de Microsoft Teams](../bots/what-are-bots.md)  que optimiza la administración de incidentes en su organización.</span><span class="sxs-lookup"><span data-stu-id="7feb5-334">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="7feb5-335">El bot facilita la recopilación automatizada de datos de incidentes, informes de incidentes personalizados, notificaciones relevantes para las partes interesadas y seguimiento de incidentes de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="7feb5-335">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="7feb5-336">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-336">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

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

## <a name="inspection"></a><span data-ttu-id="7feb5-339">Inspección</span><span class="sxs-lookup"><span data-stu-id="7feb5-339">Inspection</span></span> 

 <span data-ttu-id="7feb5-340">Inspección es una aplicación de Microsoft Teams que permite a los trabajadores de primera línea inspeccionar cualquier cosa, desde ubicaciones hasta activos y equipos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-340">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="7feb5-341">Por ejemplo, una tienda comercial, una planta de fabricación o vehículos y máquinas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-341">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="7feb5-342">Hay dos aplicaciones en esta solución, cada una destinada a diferentes tipos de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7feb5-342">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="7feb5-343">La aplicación permite a los trabajadores de primera línea inspeccionar un activo o área, administrar la calidad de los productos y servicios o mantener la seguridad en el lugar de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-343">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="7feb5-344">Facilita la comunicación entre los miembros del equipo para solucionar los problemas encontrados durante la inspección.</span><span class="sxs-lookup"><span data-stu-id="7feb5-344">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="7feb5-345">La aplicación proporciona informes sencillos para que los administradores agilicen la resolución de problemas y resalten las tendencias.</span><span class="sxs-lookup"><span data-stu-id="7feb5-345">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="7feb5-346">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-346">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Introducción a la inspección](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="7feb5-348">Informes de problemas</span><span class="sxs-lookup"><span data-stu-id="7feb5-348">Issue Reporting</span></span>

<span data-ttu-id="7feb5-349">La aplicación De informes de problemas permite a los empleados y administradores generar y administrar problemas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-349">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="7feb5-350">Consta de dos aplicaciones, Aplicación de informes de problemas para informar y Aplicación Administrar problemas para administrar problemas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-350">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="7feb5-351">Los jefes de equipo usan la aplicación Administrar problemas para configurar la experiencia de la aplicación, incluido el canal en el que la aplicación crea los mensajes de Microsoft Teams y las tareas de Planner.</span><span class="sxs-lookup"><span data-stu-id="7feb5-351">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="7feb5-352">Los administradores también usan la aplicación para crear formularios de plantilla para recopilar detalles cuando un usuario informa de un problema.</span><span class="sxs-lookup"><span data-stu-id="7feb5-352">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="7feb5-353">Por ejemplo, revise, edite o elimine formularios de plantilla de problema.</span><span class="sxs-lookup"><span data-stu-id="7feb5-353">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="7feb5-354">La aplicación también se usa para revisar los problemas del equipo, informar sobre el historial de problemas y administrar eficazmente la resolución de problemas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-354">The app is also used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="7feb5-355">Los empleados usan la aplicación De informes de problemas para registrar problemas y detalles necesarios para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-355">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="7feb5-356">La aplicación también se usa para modificar y resolver problemas existentes y obtener una vista de alto nivel de problemas individuales o de equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-356">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="7feb5-357">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-357">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Vista de equipo de informes de problemas](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="7feb5-359">Incorporación de nuevos empleados</span><span class="sxs-lookup"><span data-stu-id="7feb5-359">New Employee Onboarding</span></span> 

<span data-ttu-id="7feb5-360">La incorporación de nuevos empleados es una solución integrada de incorporación de nuevos empleados de Microsoft Teams y [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) que permite a su organización proporcionar una experiencia de incorporación coherente y de alta calidad para los empleados en su viaje de nueva contratación.</span><span class="sxs-lookup"><span data-stu-id="7feb5-360">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="7feb5-361">Los equipos de recursos humanos y los administradores de contratación usan la aplicación para proporcionar información relevante durante todo el proceso de orientación e inducción, así como para que los nuevos empleados compartan comentarios, proporcionen introducciones y completen tareas de incorporación.</span><span class="sxs-lookup"><span data-stu-id="7feb5-361">The app is used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="7feb5-362">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-362">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="7feb5-363">**Nueva tarjeta de bienvenida para empleados** ![ Imagen de la nueva tarjeta de bienvenida del empleado](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="7feb5-363">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="7feb5-364">**Lista de comprobación de nuevos empleados** ![ Imagen de la lista de comprobación de nuevos empleados](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="7feb5-364">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="7feb5-365">Distintivos abiertos</span><span class="sxs-lookup"><span data-stu-id="7feb5-365">Open Badges</span></span>

<span data-ttu-id="7feb5-366">Open Badges es una aplicación de Microsoft Teams que permite a los usuarios obtener distintivos de credenciales de aprendizaje digital en el contexto de Teams y compartirlos en todas partes.</span><span class="sxs-lookup"><span data-stu-id="7feb5-366">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="7feb5-367">Con las funcionalidades de la entidad emisora de distintivos digitales de terceros, [Badgr](https://badgr.org/), los distintivos concedidos se registran en el perfil badgr de un destinatario y están disponibles para crear y compartir una imagen enriquecida de los recorridos de aprendizaje de por vida.</span><span class="sxs-lookup"><span data-stu-id="7feb5-367">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="7feb5-368">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-368">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a><span data-ttu-id="7feb5-371">Sondeo</span><span class="sxs-lookup"><span data-stu-id="7feb5-371">Poll</span></span> 

<span data-ttu-id="7feb5-372">Poll es una aplicación de extensión de mensajería personalizada de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que te permite crear y enviar rápidamente sondeos en un chat o un canal para recopilar opiniones y preferencias del equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-372">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="7feb5-373">La aplicación se admite en todos los clientes de plataforma de Teams, como escritorio, explorador, iOS y Android y está lista para su implementación como parte de su suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="7feb5-373">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="7feb5-374">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-374">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Crear sondeo en la vista Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="7feb5-376">Respuestas rápidas</span><span class="sxs-lookup"><span data-stu-id="7feb5-376">Quick Responses</span></span>

<span data-ttu-id="7feb5-377">Respuestas rápidas es una aplicación de Microsoft Teams que ofrece una solución sólida para responder eficazmente a las preguntas frecuentes de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7feb5-377">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions FAQs.</span></span> <span data-ttu-id="7feb5-378">En lugar de responder a cada consulta manualmente y repetir continuamente información, la aplicación crea una biblioteca de respuestas para una experiencia de usuario interactiva a través de extensiones de mensajería [de](../messaging-extensions/what-are-messaging-extensions.md)Teams .</span><span class="sxs-lookup"><span data-stu-id="7feb5-378">Instead of answering each query manually and continuously repeating information, the app builds a library of responses for an interactive user experience through Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="7feb5-379">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-379">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Vista de ejemplo de las respuestas](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a><span data-ttu-id="7feb5-381">Cuestionario &#9734;</span><span class="sxs-lookup"><span data-stu-id="7feb5-381">Quiz  &#9734;</span></span>

<span data-ttu-id="7feb5-382">Quiz es una aplicación de extensión de mensajería personalizada de [Teams](../messaging-extensions/what-are-messaging-extensions.md) que te permite crear un cuestionario dentro de un chat o un canal para comprobar el conocimiento y obtener resultados instantáneos.</span><span class="sxs-lookup"><span data-stu-id="7feb5-382">Quiz is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a quiz within a chat or a channel for knowledge check and instantaneous results.</span></span> <span data-ttu-id="7feb5-383">Puedes usar Quiz para exámenes en clase y sin conexión, comprobación de conocimientos dentro del equipo y para cuestionarios divertidos dentro de un equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-383">You can use Quiz for, In-class and offline exams, Knowledge check within team, and for fun quizzes within a team.</span></span> <span data-ttu-id="7feb5-384">La aplicación de cuestionario se admite en varias plataformas, como clientes de escritorio, explorador, iOS y Android de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-384">Quiz app is supported across multiple platforms, such as Teams desktop, browser, iOS, and Android clients.</span></span> <span data-ttu-id="7feb5-385">Esta aplicación está lista para su implementación como parte de la suscripción a Microsoft 365 existente.</span><span class="sxs-lookup"><span data-stu-id="7feb5-385">This app is ready for deployment as part of your existing Microsoft 365 subscription.</span></span>

[<span data-ttu-id="7feb5-386">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-386">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Crear cuestionario en la vista Teams](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a><span data-ttu-id="7feb5-388">Asistencia rápida</span><span class="sxs-lookup"><span data-stu-id="7feb5-388">Rapid Assist</span></span>

<span data-ttu-id="7feb5-389">Rapid Assist es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que permite a los asociados que se enfrentan al cliente conectarse rápidamente con los expertos para obtener respuestas rápidas, buscar información, realizar un seguimiento de las solicitudes abiertas y permitir que los expertos reciban notificaciones para obtener rápidamente una llamada para ayudar a responder preguntas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-389">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="7feb5-390">La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams para permitir que las organizaciones conecten fácilmente a los trabajadores de primera línea con vínculos corporativos para resolver las consultas de los clientes y ofrecer una excelente experiencia de cliente.</span><span class="sxs-lookup"><span data-stu-id="7feb5-390">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="7feb5-391">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-391">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Interfaz de solicitud de usuario final](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Vista de solicitud de experto](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="7feb5-394">Reflejar</span><span class="sxs-lookup"><span data-stu-id="7feb5-394">Reflect</span></span> 

<span data-ttu-id="7feb5-395">Reflect es una aplicación de extensión de mensajería personalizada de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que proporciona un recurso seguro e inclusivo para que los miembros del equipo compartan el estado de su bienestar emocional con compañeros o jefes de grupo directamente dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-395">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues or group leaders directly within Teams.</span></span> <span data-ttu-id="7feb5-396">La aplicación está disponible en chats de canal, grupo, reunión y 1:1 y la respuesta de la comprobación se establece en pública, privada a remitente o totalmente anónima.</span><span class="sxs-lookup"><span data-stu-id="7feb5-396">The app is available in channel, group, meeting, and 1:1 chats and the check-in response is set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="7feb5-397">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-397">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="7feb5-398">**Sondeo de bienestar**</span><span class="sxs-lookup"><span data-stu-id="7feb5-398">**Well-being poll**</span></span>
    
    ![Reflejar sondeo de usuarios de aplicaciones](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="7feb5-400">Soporte remoto</span><span class="sxs-lookup"><span data-stu-id="7feb5-400">Remote Support</span></span>

<span data-ttu-id="7feb5-401">El soporte remoto es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona una interfaz centrada entre los solicitantes de soporte técnico de toda la organización y el equipo de soporte técnico interno.</span><span class="sxs-lookup"><span data-stu-id="7feb5-401">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="7feb5-402">Los usuarios finales pueden enviar, editar o retirar solicitudes de soporte técnico y el equipo de soporte técnico puede responder, administrar y actualizar solicitudes en toda la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-402">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="7feb5-403">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-403">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a><span data-ttu-id="7feb5-406">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="7feb5-406">Request-a-team</span></span>

<span data-ttu-id="7feb5-407">Request-a-team es una aplicación de Microsoft Teams que optimiza la creación de nuevos equipos para su organización empresarial.</span><span class="sxs-lookup"><span data-stu-id="7feb5-407">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="7feb5-408">La aplicación admite la estandarización y los procedimientos recomendados al crear nuevas instancias de equipo mediante la integración de un formulario de solicitud guiado por asistente, un proceso de aprobación incrustado, un panel de estado de solicitud y compilaciones automatizadas de equipo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-408">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="7feb5-409">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-409">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

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

## <a name="scrums-for-channels"></a><span data-ttu-id="7feb5-412">Scrums para canales</span><span class="sxs-lookup"><span data-stu-id="7feb5-412">Scrums for Channels</span></span>

<span data-ttu-id="7feb5-413">Scrums para canales es una aplicación auxiliar de scrum que permite a los usuarios programar y ejecutar scrums en canales de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-413">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="7feb5-414">La aplicación es ideal para equipos remotos y equipos formados por miembros de distintas ubicaciones geográficas y zonas horarias para compartir actualizaciones diarias y garantizar la participación en reuniones de soporte de scrum.</span><span class="sxs-lookup"><span data-stu-id="7feb5-414">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="7feb5-415">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-415">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="7feb5-416">Para realizar reuniones de scrum en un chat de grupo, consulta [Scrums for Group Chat](#scrums-for-group-chat) app template.</span><span class="sxs-lookup"><span data-stu-id="7feb5-416">To conduct scrum meetings in a group chat, see [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

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

## <a name="scrums-for-group-chat"></a><span data-ttu-id="7feb5-419">Scrums para chat en grupo</span><span class="sxs-lookup"><span data-stu-id="7feb5-419">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="7feb5-420">La plantilla de aplicación Estado de Scrums se actualiza y ahora es Scrums para chat en grupo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-420">The Scrums Status app template is updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="7feb5-421">Scrums for Group Chat es un asistente de scrum de apoyo que permite a los miembros del chat de grupo ejecutar reuniones de soporte asincrónicas y compartir fácilmente sus actualizaciones diarias.</span><span class="sxs-lookup"><span data-stu-id="7feb5-421">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="7feb5-422">Permite a todos los miembros del chat de grupo contribuir al scrum y ver las actualizaciones realizadas por otros usuarios en el scrum en ejecución.</span><span class="sxs-lookup"><span data-stu-id="7feb5-422">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="7feb5-423">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-423">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Demostración de Scrums para chat en grupo](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="7feb5-425">Compartir ahora</span><span class="sxs-lookup"><span data-stu-id="7feb5-425">Share Now</span></span> 

<span data-ttu-id="7feb5-426">La aplicación Compartir ahora promueve el intercambio positivo de información entre compañeros al permitir que los usuarios compartan fácilmente contenido en el entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-426">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="7feb5-427">Los usuarios interactúan con la aplicación para compartir elementos de interés con los miembros del equipo, descubrir nuevo contenido compartido, establecer preferencias y favoritos de marcadores para su lectura posterior.</span><span class="sxs-lookup"><span data-stu-id="7feb5-427">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="7feb5-428">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-428">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Seleccionar vista de contenido](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="7feb5-430">Búsqueda de lista de SharePoint</span><span class="sxs-lookup"><span data-stu-id="7feb5-430">SharePoint List Search</span></span>

<span data-ttu-id="7feb5-431">La colaboración en Microsoft Teams suele hacer referencia a la información contenida en los elementos de una lista de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7feb5-431">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="7feb5-432">Pegar un vínculo al elemento en cuestión obliga a todos a cambiar el contexto de la conversación, buscar la información necesaria y, a continuación, volver a Teams para continuar la conversación.</span><span class="sxs-lookup"><span data-stu-id="7feb5-432">Paste a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="7feb5-433">A medida que continúa la conversación, los usuarios tienen que volver al elemento de referencia varias veces para comprobar nuevos comentarios y actualizar sus memorias de la información contenida en el elemento.</span><span class="sxs-lookup"><span data-stu-id="7feb5-433">As the conversation continues  people have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="7feb5-434">Este cambio de contexto crea una barrera para una colaboración fluida.</span><span class="sxs-lookup"><span data-stu-id="7feb5-434">This context switching creates a barrier to smooth collaboration.</span></span>
<span data-ttu-id="7feb5-435">Para resolver este problema, se usa la plantilla de aplicación Búsqueda de lista.</span><span class="sxs-lookup"><span data-stu-id="7feb5-435">To resolve this problem, the List Search app template is used.</span></span> <span data-ttu-id="7feb5-436">Muchos usuarios usan SharePoint para crear algunos de los flujos de trabajo principales de sus organizaciones.</span><span class="sxs-lookup"><span data-stu-id="7feb5-436">Many users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="7feb5-437">Sin embargo, es difícil colaborar en las listas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-437">However, collaborating around lists is difficult.</span></span> <span data-ttu-id="7feb5-438">Con la plantilla de aplicación Búsqueda de lista en Microsoft Teams, los usuarios pueden insertar información de elementos de lista de SharePoint directamente dentro de una conversación de chat para aliviar el cambio de contexto causado al insertar simplemente un vínculo en un chat.</span><span class="sxs-lookup"><span data-stu-id="7feb5-438">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="7feb5-439">La información se inserta como una tarjeta de formato automático fácil de leer, lo que ayuda a los usuarios a mantener la conversación.</span><span class="sxs-lookup"><span data-stu-id="7feb5-439">The information is inserted as an easy-to-read auto-formatted card, helping the users stay engaged in the conversation.</span></span>

[<span data-ttu-id="7feb5-440">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-440">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Aplicación de búsqueda de lista](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="7feb5-442">Check-ins del personal</span><span class="sxs-lookup"><span data-stu-id="7feb5-442">Staff Check-ins</span></span>

<span data-ttu-id="7feb5-443">Staff Check-ins es una aplicación basada en [Power Apps](/powerapps/powerapps-overview) que permite la comunicación de supervisión entre tu empresa y el personal de campo.</span><span class="sxs-lookup"><span data-stu-id="7feb5-443">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview) based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="7feb5-444">El personal puede proporcionar fácilmente información crítica de tiempo y actualizaciones de estado de forma programada o ad hoc directamente desde Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-444">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="7feb5-445">La aplicación admite la ubicación en tiempo real, fotos, notas, notificaciones de aviso y flujos de trabajo automatizados.</span><span class="sxs-lookup"><span data-stu-id="7feb5-445">The app supports real-time location, photos, notes, reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="7feb5-446">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-446">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Crear vista de check-in](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="7feb5-448">Encuesta</span><span class="sxs-lookup"><span data-stu-id="7feb5-448">Survey</span></span>

<span data-ttu-id="7feb5-449">Survey es una aplicación de extensión de mensajería de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) personalizada que te permite crear una encuesta en un chat o un canal para recopilar datos y obtener información útil.</span><span class="sxs-lookup"><span data-stu-id="7feb5-449">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span> <span data-ttu-id="7feb5-450">La aplicación se admite en todos los clientes de plataforma de Teams, como escritorio, explorador, iOS y Android y está lista para su implementación como parte de su suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="7feb5-450">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="7feb5-451">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-451">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Crear encuesta en la vista Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="7feb5-453">Recuento de horas</span><span class="sxs-lookup"><span data-stu-id="7feb5-453">Time Tally</span></span> 

<span data-ttu-id="7feb5-454">Un proyecto puede incluir varias tareas y varios proyectos se pueden asignar a los empleados.</span><span class="sxs-lookup"><span data-stu-id="7feb5-454">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="7feb5-455">Los administradores deben comprender el progreso del proyecto durante el tiempo invertido por los empleados en estas tareas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-455">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="7feb5-456">Puede ser una actividad engorrosa, ya que los empleados deben rellenar los partes de horas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-456">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="7feb5-457">La aplicación Time Tally permite a los empleados rellenar sus partes de horas rápidamente, con el dispositivo móvil, y los administradores no tienen que realizar un seguimiento con los empleados en la entrada del parte de horas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-457">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="7feb5-458">Los administradores pueden ver el uso del proyecto en función de los recursos y pueden aprobar o rechazar las entradas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-458">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="7feb5-459">Las notificaciones de aviso se envían para garantizar el cumplimiento del parte de horas.</span><span class="sxs-lookup"><span data-stu-id="7feb5-459">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="7feb5-460">Además, los datos históricos y los usos están disponibles para el análisis.</span><span class="sxs-lookup"><span data-stu-id="7feb5-460">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="7feb5-461">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-461">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Recuento de horas](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a><span data-ttu-id="7feb5-463">Aprendizaje &#9734;</span><span class="sxs-lookup"><span data-stu-id="7feb5-463">Training  &#9734;</span></span>

<span data-ttu-id="7feb5-464">El aprendizaje es una aplicación de extensión de mensajería personalizada de [Teams](../messaging-extensions/what-are-messaging-extensions.md) que permite a los usuarios publicar un aprendizaje dentro de un chat o un canal para compartir y mejorar el conocimiento sin conexión.</span><span class="sxs-lookup"><span data-stu-id="7feb5-464">Training is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables users to publish a training within a chat or a channel for offline knowledge sharing and upskilling.</span></span> <span data-ttu-id="7feb5-465">La aplicación se admite en varios clientes de plataforma de Teams, como escritorio, explorador, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="7feb5-465">The app is supported across multiple Teams platform clients, such as desktop, browser, iOS, and Android.</span></span> <span data-ttu-id="7feb5-466">Esta aplicación está lista para su implementación como parte de la suscripción a Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="7feb5-466">This app is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="7feb5-467">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-467">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Crear aprendizaje en la vista Teams](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a><span data-ttu-id="7feb5-469">Redondeo virtual</span><span class="sxs-lookup"><span data-stu-id="7feb5-469">Virtual Rounding</span></span>

<span data-ttu-id="7feb5-470">Los proveedores de hospitales y de sala de **emergencias hacen muchas rondas** al día.</span><span class="sxs-lookup"><span data-stu-id="7feb5-470">Hospital and emergency room providers make many **rounds** per day.</span></span> <span data-ttu-id="7feb5-471">Estas rápidas check-ins en los pacientes están diseñadas para proporcionar una comprobación de estado sobre cómo está el paciente y asegurarse de que se aborde la preocupación del paciente.</span><span class="sxs-lookup"><span data-stu-id="7feb5-471">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="7feb5-472">Aunque el redondeo es una práctica esencial para garantizar que los pacientes están siendo supervisados por varios tipos de proveedores, representan un enorme desagüe en el EPP, ya que para cada visita, de cada proveedor, se usa una máscara nueva y un nuevo conjunto de guantes.</span><span class="sxs-lookup"><span data-stu-id="7feb5-472">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves are used.</span></span> <span data-ttu-id="7feb5-473">Con estas plantillas de aplicación, los trabajadores médicos pueden realizar fácilmente rondas virtualmente, a través de una reunión de Microsoft Teams entre el proveedor y el paciente.</span><span class="sxs-lookup"><span data-stu-id="7feb5-473">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="7feb5-474">También se hace referencia a la solución de redondeo virtual en la entrada de [blog](https://aka.ms/teamsvirtualrounding)Microsoft Health and Life Sciences .</span><span class="sxs-lookup"><span data-stu-id="7feb5-474">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="7feb5-475">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-475">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Redondeo virtual](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="7feb5-477">Administración de visitantes</span><span class="sxs-lookup"><span data-stu-id="7feb5-477">Visitor Management</span></span>

<span data-ttu-id="7feb5-478">La aplicación Administración de visitantes permite a su organización y a los empleados administrar de forma fácil y eficaz el proceso de visitantes en el sitio, directamente desde Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7feb5-478">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="7feb5-479">La aplicación permite a los empleados crear solicitudes de visitantes, realizar un seguimiento centralizado de un estado de solicitud a través del panel de visitantes y recibir notificaciones en tiempo real cuando llega un visitante.</span><span class="sxs-lookup"><span data-stu-id="7feb5-479">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="7feb5-480">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-480">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="7feb5-483">Workplace Awards</span><span class="sxs-lookup"><span data-stu-id="7feb5-483">Workplace Awards</span></span>

<span data-ttu-id="7feb5-484">Workplace Awards es una plantilla de aplicación de Teams que proporciona un marco positivo para fomentar el reconocimiento y fomentar la cultura de la apreciación de los empleados en el lugar de trabajo moderno.</span><span class="sxs-lookup"><span data-stu-id="7feb5-484">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="7feb5-485">La aplicación te permite configurar y administrar un reconocimiento y recompensas de empleados, denominado programa R&R donde los empleados pueden designar y respaldar fácilmente a compañeros y el líder de R&R puede ver las nominaciones enviadas, conceder premios y anunciar destinatarios.</span><span class="sxs-lookup"><span data-stu-id="7feb5-485">The app enables you to setup and manage an employee rewards and recognition, called R&R program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="7feb5-486">Obtenerlo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7feb5-486">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="7feb5-487">Tarjeta de nominación de los premios workplace</span><span class="sxs-lookup"><span data-stu-id="7feb5-487">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Pestaña Lista de reconocimientos de lugares de trabajo](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="7feb5-489">Para obtener más información sobre la plantilla de aplicación, consulta [Plantilla de aplicación](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span><span class="sxs-lookup"><span data-stu-id="7feb5-489">For more information on app template, see [App template](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>

## <a name="see-also"></a><span data-ttu-id="7feb5-490">Consulte también</span><span class="sxs-lookup"><span data-stu-id="7feb5-490">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7feb5-491">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="7feb5-491">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
