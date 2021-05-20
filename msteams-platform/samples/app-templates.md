---
title: plantillas de aplicación Microsoft Teams
description: Enlaces y descripciones de plantillas de aplicaciones para la plataforma Microsoft Teams
ms.topic: reference
keywords: plantillas de Microsoft Teams muestra demostración
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 8cfb066ee3c202fb8611a61bbde3058207a62a35
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566345"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="c6421-104">Plantillas de aplicaciones para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c6421-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="c6421-105">Las plantillas de aplicación son ejemplos de aplicaciones completas para Microsoft Teams que son de código abierto y están disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c6421-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="c6421-106">Cada plantilla de aplicación contiene instrucciones detalladas para implementar e instalar esa aplicación para su organización.</span><span class="sxs-lookup"><span data-stu-id="c6421-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="c6421-107">También proporciona una aplicación de ejemplo que puede instalar y empezar a usar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="c6421-107">It also provides a sample app that you can install and start using immediately.</span></span> <span data-ttu-id="c6421-108">El código fuente completo también está disponible, lo que le permite explorarlo en detalle o tenedor el código y modificarlo para cumplir con sus requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="c6421-108">The complete source code is also available, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="c6421-109">Todas las plantillas de aplicaciones se proporcionan bajo los términos [de la Licencia MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="c6421-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>

> [!NOTE] 
> <span data-ttu-id="c6421-110">Debe licenciar y admitir aplicaciones creadas a partir de plantillas de aplicación para los usuarios y organizaciones.</span><span class="sxs-lookup"><span data-stu-id="c6421-110">You must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="c6421-111">**&#9734; Indica las plantillas de aplicación recién publicadas.**</span><span class="sxs-lookup"><span data-stu-id="c6421-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="c6421-112">Beneficios clave</span><span class="sxs-lookup"><span data-stu-id="c6421-112">Key benefits</span></span>

* <span data-ttu-id="c6421-113">**Implemente directamente en la nube:** Todas las plantillas de aplicación incluyen scripts de implementación que le permiten hospedar todos los servicios necesarios en Microsoft Azure o Power Platform.</span><span class="sxs-lookup"><span data-stu-id="c6421-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="c6421-114">**Código de ejemplo recomendado:** Las plantillas de aplicación se ajustan a las prácticas recomendadas en torno a seguridad e infraestructura.</span><span class="sxs-lookup"><span data-stu-id="c6421-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="c6421-115">Todos los cambios enviados por la comunidad a las plantillas de la aplicación se revisan para garantizar la conformidad.</span><span class="sxs-lookup"><span data-stu-id="c6421-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="c6421-116">**Personalizable y extensible:** Aunque todas las plantillas de aplicación se implementan con una configuración mínima, se proporcionan todos los scripts de base de código e implementación, para que pueda personalizarlas o ampliarlas fácilmente para que se adapten a sus necesidades únicas.</span><span class="sxs-lookup"><span data-stu-id="c6421-116">**Customizable and extensible:** While all app templates are deployed with minimal configuration, the entire code base and deployment scripts are provided, so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="c6421-117">**Documentación detallada:** Todas las plantillas de aplicación van acompañadas de documentación integral sobre la arquitectura de la solución, la implementación y los pasos de configuración.</span><span class="sxs-lookup"><span data-stu-id="c6421-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="c6421-118">Bot de adopción</span><span class="sxs-lookup"><span data-stu-id="c6421-118">Adoption Bot</span></span> 

<span data-ttu-id="c6421-119">Adoption Bot es un bot de chat de atención al usuario creado con Power Virtual Agent para Teams PVA.</span><span class="sxs-lookup"><span data-stu-id="c6421-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams PVA.</span></span> <span data-ttu-id="c6421-120">Se considera como la versión PVA de FAQ Plus.</span><span class="sxs-lookup"><span data-stu-id="c6421-120">It is considered as the PVA version of FAQ Plus.</span></span> <span data-ttu-id="c6421-121">Adoption Bot responde a más de 100 preguntas comunes sobre Microsoft 365 y Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="c6421-122">Puede editar los temas existentes, agregar sus propios temas e ingerir preguntas frecuentes existentes.</span><span class="sxs-lookup"><span data-stu-id="c6421-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="c6421-123">Si los usuarios necesitan ayuda adicional, Adoption Bot puede conectarlos a expertos o incluso ampliarlos a tickets de servicio abiertos con conectores de flujo premium.</span><span class="sxs-lookup"><span data-stu-id="c6421-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span> <span data-ttu-id="c6421-124">Este bot se autoinstala o está integrado en una aplicación personalizada, como [Adoption Hub.](https://github.com/akporzondek/adoption_hub)</span><span class="sxs-lookup"><span data-stu-id="c6421-124">This bot is self-installed or built into a custom app, such as the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="c6421-125">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a><span data-ttu-id="c6421-126">Herramienta de adopción- Plataforma de gestión Champion &#9734;</span><span class="sxs-lookup"><span data-stu-id="c6421-126">Adoption Tool- Champion Management Platform &#9734;</span></span>

<span data-ttu-id="c6421-127">La plantilla de aplicación Champion Management Platform (CMP) te ayuda a administrar, escalar e inspirar a tus campeones de trabajo en equipo a lograr más.</span><span class="sxs-lookup"><span data-stu-id="c6421-127">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="c6421-128">Esta plantilla de aplicación se basa en el SharePoint Framework y se carga en una pestaña dentro de un equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-128">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="c6421-129">Los grupos pueden aprovechar esta herramienta para ayudar a administrar la pertenencia al programa, proporcionar una tabla de clasificación y tipos de eventos para el registro y herramientas para superponer insignias digitales a los participantes del programa.</span><span class="sxs-lookup"><span data-stu-id="c6421-129">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="c6421-130">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-130">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a><span data-ttu-id="c6421-131">Herramienta de adopción- Microsoft 365 vías de aprendizaje (Introducción) &#9734;</span><span class="sxs-lookup"><span data-stu-id="c6421-131">Adoption Tool- Microsoft 365 Learning Pathways (Get Started) &#9734;</span></span>

<span data-ttu-id="c6421-132">La plantilla de aplicación Introducción le permite traer el poder de Microsoft 365 vías de aprendizaje dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-132">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="c6421-133">Esta plantilla de aplicación le permite conceder un fácil acceso a páginas de formación específicas u otros activos de intranet y cargar el contenido directamente dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-133">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="c6421-134">También puede cambiar el nombre o el logotipo de la aplicación para que coincida con la marca de su empresa.</span><span class="sxs-lookup"><span data-stu-id="c6421-134">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="c6421-135">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-135">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="c6421-136">Gerente de Citas</span><span class="sxs-lookup"><span data-stu-id="c6421-136">Appointment Manager</span></span> 

<span data-ttu-id="c6421-137">Appointment Manager es una plantilla de aplicación Teams para ayudar a las empresas a crear, administrar y llevar a cabo citas virtuales con los consumidores a través de Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-137">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="c6421-138">Las nuevas solicitudes de citas de los consumidores son visibles en Teams canales, donde se asignan rápidamente y se reasignan al personal de un equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-138">New appointment requests from consumers are visible in Teams channels, where they are quickly assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="c6421-139">Las solicitudes de cita se ven a nivel de equipo o personal a través de pestañas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="c6421-139">Appointment requests are viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="c6421-140">Cada cita está asociada a una reunión Teams en línea, de ahí que el personal y los consumidores puedan unirse fácilmente a la reunión a la hora programada.</span><span class="sxs-lookup"><span data-stu-id="c6421-140">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="c6421-141">La plantilla de aplicación se integra con Microsoft Bookings para facilitar la gestión de citas.</span><span class="sxs-lookup"><span data-stu-id="c6421-141">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="c6421-142">Las citas programadas aparecen automáticamente en los calendarios de los miembros del personal asignados, y los consumidores reciben notificaciones y recordatorios de correo electrónico personalizables con enlaces de reunión incrustados.</span><span class="sxs-lookup"><span data-stu-id="c6421-142">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="c6421-143">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="c6421-144">![Gerente de Citas General ](../assets/images/appointment-manager-overview.png)
 ![ Gerente de Citas en Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="c6421-144">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="c6421-145">Pregunte lejos</span><span class="sxs-lookup"><span data-stu-id="c6421-145">Ask Away</span></span>

<span data-ttu-id="c6421-146">Ask Away es un [bot Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios realizar sesiones de preguntas y respuestas, llamadas Q&A dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-146">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Question and Answer, called Q&A sessions within Teams.</span></span> <span data-ttu-id="c6421-147">Con el bot Ask Away, los miembros del equipo pueden enviar y votar preguntas compartidas por colegas que permiten a los anfitriones de Q&A recopilar fácilmente preguntas de primer nivel dentro de un canal o chat.</span><span class="sxs-lookup"><span data-stu-id="c6421-147">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="c6421-148">El bot se utiliza para llevar a cabo una sesión Q&A en tiempo real en una reunión de Teams y permite a los asistentes enviar preguntas en vivo a través del chat.</span><span class="sxs-lookup"><span data-stu-id="c6421-148">The bot is used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live through chat.</span></span>

[<span data-ttu-id="c6421-149">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-149">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Vista del cuadro de diálogo emergente de la tabla de clasificación para que los usuarios voten sobre las preguntas](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="c6421-151">Información de asociados</span><span class="sxs-lookup"><span data-stu-id="c6421-151">Associate Insights</span></span>

<span data-ttu-id="c6421-152">Associate Insights es una plantilla [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que permite a los trabajadores de primera línea capturar y enviar directamente la opinión, el sentimiento y la percepción del cliente.</span><span class="sxs-lookup"><span data-stu-id="c6421-152">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="c6421-153">Los trabajadores de primera línea suelen ser el primer representante de la empresa en interactuar con los clientes en un punto de contacto uno a uno.</span><span class="sxs-lookup"><span data-stu-id="c6421-153">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="c6421-154">Los datos recopilados son compartidos y utilizados en colaboración por equipos empresariales, por ejemplo a través de una pestaña de Power BI Teams, para mejorar el producto y mejorar la experiencia del cliente.</span><span class="sxs-lookup"><span data-stu-id="c6421-154">The collected data are shared and used collaboratively by business teams, such as through a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="c6421-155">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-155">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Vista de comentarios de las perspectivas generadas por la aplicación](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Power BI vista de los conocimientos generados por la aplicación](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="c6421-158">Asistencia</span><span class="sxs-lookup"><span data-stu-id="c6421-158">Attendance</span></span>

<span data-ttu-id="c6421-159">La aplicación Asistencia es una pestaña [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que se anclan en un equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-159">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that are pinned in a team.</span></span> <span data-ttu-id="c6421-160">Está diseñado para registrar la presencia en entornos, como entornos de aprendizaje y formación.</span><span class="sxs-lookup"><span data-stu-id="c6421-160">It is designed to record presence in settings, such as learning and training environments.</span></span> <span data-ttu-id="c6421-161">Los usuarios pueden marcar o editar la asistencia durante un tiempo de hasta 30 días en el pasado y ver informes de asistencia resumidos para todo un grupo o asistentes individuales.</span><span class="sxs-lookup"><span data-stu-id="c6421-161">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span> <span data-ttu-id="c6421-162">Para obtener más información sobre la asistencia de equipos, consulte [Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span><span class="sxs-lookup"><span data-stu-id="c6421-162">For more information on teams attendance, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span></span>

<span data-ttu-id="c6421-163">La siguiente imagen muestra la demostración de la aplicación de asistencia:</span><span class="sxs-lookup"><span data-stu-id="c6421-163">The following image displays the attendance app demo:</span></span>  

![Demostración de la aplicación de asistencia](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="c6421-165">Reservar una habitación</span><span class="sxs-lookup"><span data-stu-id="c6421-165">Book-a-room</span></span>

<span data-ttu-id="c6421-166">Book-a-room es un [bot Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30, 60 o 90 minutos a partir de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="c6421-166">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="c6421-167">El tiempo predeterminado es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="c6421-167">The default time is 30 minutes.</span></span> <span data-ttu-id="c6421-168">El bot Book-a-room se limita a conversaciones personales o 1:1.</span><span class="sxs-lookup"><span data-stu-id="c6421-168">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="c6421-169">Para obtener más información sobre la aplicación Reservar una habitación, consulte [Obtenerla en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span><span class="sxs-lookup"><span data-stu-id="c6421-169">For more information on Book-a-room app, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span></span>  
<span data-ttu-id="c6421-170">La siguiente imagen muestra la demostración Libro a habitación:</span><span class="sxs-lookup"><span data-stu-id="c6421-170">The following image displays the Book-a-room demo:</span></span>

![Demostración de reservar una habitación](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="c6421-172">Acceso al edificio</span><span class="sxs-lookup"><span data-stu-id="c6421-172">Building Access</span></span>

<span data-ttu-id="c6421-173">Building Access es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que admite la administración de umbrales de ocupación de edificios y normas de distanciamiento social al permitir a los directores de instalaciones administrar, realizar un seguimiento e informar de la presencia de los empleados en el lugar.</span><span class="sxs-lookup"><span data-stu-id="c6421-173">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="c6421-174">La aplicación, creada con Microsoft [Power Apps](/powerapps/powerapps-overview)y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams y permite a las organizaciones determinar la preparación de la creación, establecer criterios de elegibilidad para el acceso in situ y recopilar información para la planificación futura.</span><span class="sxs-lookup"><span data-stu-id="c6421-174">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="c6421-175">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-175">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Tarjeta de reserva de acceso al edificio](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Vista clave de acceso al edificio](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="c6421-178">Celebraciones</span><span class="sxs-lookup"><span data-stu-id="c6421-178">Celebrations</span></span>

<span data-ttu-id="c6421-179">Celebrations es una aplicación Teams que ayuda a los miembros del equipo a celebrar los cumpleaños, aniversarios y otros eventos recurrentes de los demás.</span><span class="sxs-lookup"><span data-stu-id="c6421-179">Celebrations is a Teams app that helps team members to celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="c6421-180">Recuerda ocasiones especiales de todos los miembros del equipo y envía un mensaje amistoso en todos los equipos seleccionados en el momento de la creación del evento, para que los miembros del equipo se sientan especiales en su día.</span><span class="sxs-lookup"><span data-stu-id="c6421-180">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="c6421-181">La aplicación proporciona una interfaz fácil para que todos los miembros del equipo agreguen y vean personalmente sus eventos y también permite al usuario seleccionar los equipos en los que se comparten los eventos.</span><span class="sxs-lookup"><span data-stu-id="c6421-181">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="c6421-182">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-182">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="c6421-183">Lista de comprobación</span><span class="sxs-lookup"><span data-stu-id="c6421-183">Checklist</span></span>

<span data-ttu-id="c6421-184">Lista de comprobación es una aplicación de extensión de [mensajería](../messaging-extensions/what-are-messaging-extensions.md) Microsoft Teams personalizada que le permite colaborar con su equipo mediante la creación de una lista de comprobación compartida en un chat o canal.</span><span class="sxs-lookup"><span data-stu-id="c6421-184">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="c6421-185">La aplicación es compatible con todos los clientes de Teams plataforma, como navegador de escritorio, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="c6421-185">The app is supported across all Teams platform clients, such as desktop browser, iOS, and Android.</span></span> <span data-ttu-id="c6421-186">La aplicación está lista para su implementación como parte de la suscripción Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="c6421-186">The app is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="c6421-187">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-187">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![Crear lista de comprobación en Teams vista](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="c6421-189">Entrega en el aula</span><span class="sxs-lookup"><span data-stu-id="c6421-189">Classroom Drop-in</span></span> 

<span data-ttu-id="c6421-190">Classroom Drop-in es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que permite a los líderes del sistema encontrar equipos de clase, significa aulas virtuales y agregarse a estos equipos de clase para un período de entrega especificado, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c6421-190">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams, means virtual classrooms and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="c6421-191">La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams para garantizar que los institutos educativos puedan optimizar sus operaciones en un entorno de aprendizaje híbrido proporcionando acceso a las partes interesadas relevantes para los equipos de clase por requerimientos empresariales.</span><span class="sxs-lookup"><span data-stu-id="c6421-191">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="c6421-192">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-192">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Solicitud de entrega en el aula](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="c6421-194">Comunicador de la empresa</span><span class="sxs-lookup"><span data-stu-id="c6421-194">Company Communicator</span></span>

<span data-ttu-id="c6421-195">La aplicación Communicator de la empresa permite a los equipos corporativos crear y enviar mensajes destinados a varios equipos o un gran número de empleados a través del chat, lo que permite a la organización llegar a los empleados justo donde colaboran.</span><span class="sxs-lookup"><span data-stu-id="c6421-195">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="c6421-196">Utilice esta plantilla para múltiples escenarios, como nuevos anuncios de iniciativa, incorporación de empleados, aprendizaje moderno y desarrollo o transmisiones en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="c6421-196">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning, and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="c6421-197">La aplicación proporciona una interfaz fácil para que los usuarios designados creen, obtengan una vista previa, colaboren y envíen mensajes.</span><span class="sxs-lookup"><span data-stu-id="c6421-197">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="c6421-198">Proporciona una base para crear capacidades de comunicación dirigidas personalizadas, como telemetría personalizada en cuántos usuarios reconocieron o interactuaron con un mensaje.</span><span class="sxs-lookup"><span data-stu-id="c6421-198">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="c6421-199">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-199">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator vista de cuadro de composición](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="c6421-201">Búsqueda de grupo de contacto</span><span class="sxs-lookup"><span data-stu-id="c6421-201">Contact Group Lookup</span></span>

<span data-ttu-id="c6421-202">La aplicación Búsqueda de grupos de contactos proporciona un enfoque conveniente y útil para crear, acceder y administrar los grupos de contactos de su organización, anteriormente conocidos como listas de distribución o grupos de comunicación.</span><span class="sxs-lookup"><span data-stu-id="c6421-202">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups, formerly known as distribution lists or communication groups.</span></span> <span data-ttu-id="c6421-203">Los usuarios pueden ver y chatear rápidamente con los miembros del grupo, ver el estado de los miembros y crear un chat de grupo con miembros seleccionados en el grupo de contactos, todo dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-203">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="c6421-204">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-204">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Vista de favoritos anclados búsqueda de grupos de contacto](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Búsqueda de grupo de contacto inicia demostración de chat](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation"></a><span data-ttu-id="c6421-207">Apreciación de los compañeros de trabajo</span><span class="sxs-lookup"><span data-stu-id="c6421-207">Co-worker Appreciation</span></span> 

<span data-ttu-id="c6421-208">Utilizando la plantilla de apreciación de compañeros de trabajo en Microsoft Teams, los usuarios pueden reconocer los logros de sus colegas en el contexto de la Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-208">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="c6421-209">Cuando los compañeros de trabajo seleccionan recompensar a un colega, los destinatarios y otros miembros del equipo se etiquetan en una conversación de canal y reciben una notificación sobre los detalles del premio del canal.</span><span class="sxs-lookup"><span data-stu-id="c6421-209">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="c6421-210">Los premios se registran en la aplicación Teams, que es segura, portátil y fácilmente compartible.</span><span class="sxs-lookup"><span data-stu-id="c6421-210">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="c6421-211">Esto se considera como la versión basada en PowerApps de la plantilla de aplicación Abrir insignias, con una tabla de clasificación.</span><span class="sxs-lookup"><span data-stu-id="c6421-211">This is considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="c6421-212">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-212">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![en general](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="c6421-214">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="c6421-214">CrowdSourcer</span></span>

<span data-ttu-id="c6421-215">CrowdSourcer es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona a los equipos información consultada procedente en colaboración de los miembros del grupo.</span><span class="sxs-lookup"><span data-stu-id="c6421-215">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="c6421-216">Ayuda a responder preguntas frecuentes al tiempo que permite a los participantes participar activamente y contribuir a un recurso de información divertido y útil.</span><span class="sxs-lookup"><span data-stu-id="c6421-216">It helps to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="c6421-217">Consiga en Github</span><span class="sxs-lookup"><span data-stu-id="c6421-217">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interacción entre el usuario final de Crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="c6421-219">Adhesivos personalizados</span><span class="sxs-lookup"><span data-stu-id="c6421-219">Custom Stickers</span></span>

<span data-ttu-id="c6421-220">La autoexpresión es fundamental para una cultura de equipo saludable.</span><span class="sxs-lookup"><span data-stu-id="c6421-220">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="c6421-221">Esta plantilla de aplicación es una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) que permite a los usuarios utilizar pegatinas personalizadas y GIF dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-221">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="c6421-222">Esta plantilla proporciona una experiencia de configuración fácil basada en la web donde cualquier persona con acceso a la configuración puede cargar los GIF, pegatinas e imágenes que desea que tengan sus usuarios, lo que permite a todo su equipo utilizar cualquier conjunto de pegatinas que elija.</span><span class="sxs-lookup"><span data-stu-id="c6421-222">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs, stickers, and images they want their users to have, allowing your entire team to use any set of stickers you choose.</span></span>

<span data-ttu-id="c6421-223">Esta aplicación también permite compartir fácilmente imágenes, GIF, pegatinas entre equipos sin necesidad de acceso a sitios SharePoint o canales individuales como mecanismos de almacenamiento y uso compartido.</span><span class="sxs-lookup"><span data-stu-id="c6421-223">This app also enables easy sharing of images, GIFs, stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="c6421-224">Por ejemplo, los equipos de productos pueden compartir fácilmente imágenes de productos y GIF a las redes sociales, marketing y equipos de ventas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="c6421-224">For example, product teams can easily share product images and GIFs to social media, marketing, and sales teams programmatically.</span></span> <span data-ttu-id="c6421-225">También se puede ampliar esta aplicación activando un flujo de notificación a equipos o individuos específicos cuando se pongan nuevas imágenes y GIF.</span><span class="sxs-lookup"><span data-stu-id="c6421-225">One can also extend this app by triggering a notification flow to specific teams or individuals when new images, and GIFs are made available.</span></span>

[<span data-ttu-id="c6421-226">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-226">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Aplicación stickers](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="c6421-228">Ideas de los empleados</span><span class="sxs-lookup"><span data-stu-id="c6421-228">Employee Ideas</span></span>

<span data-ttu-id="c6421-229">La aplicación Ideas de empleados es la versión de PowerApps de la plantilla de aplicación Great Ideas basada en Azure.</span><span class="sxs-lookup"><span data-stu-id="c6421-229">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="c6421-230">La aplicación permite a los usuarios de Teams configurar y configurar una campaña de ideas.</span><span class="sxs-lookup"><span data-stu-id="c6421-230">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="c6421-231">Una campaña de ideas es una categoría para agrupar ideas en torno a temas comunes.</span><span class="sxs-lookup"><span data-stu-id="c6421-231">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="c6421-232">Teams usuarios también pueden realizar las siguientes actividades:</span><span class="sxs-lookup"><span data-stu-id="c6421-232">Teams users can also perform the following activities:</span></span>

* <span data-ttu-id="c6421-233">Configure un formulario de envío estándar que los empleados deben enviar para cada idea.</span><span class="sxs-lookup"><span data-stu-id="c6421-233">Configure a standard submission form that employees must submit for each idea.</span></span> 
* <span data-ttu-id="c6421-234">Revise y gestione las ideas y la lista de campañas.</span><span class="sxs-lookup"><span data-stu-id="c6421-234">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="c6421-235">Modificar y eliminar campañas.</span><span class="sxs-lookup"><span data-stu-id="c6421-235">Modify and delete campaigns.</span></span>
* <span data-ttu-id="c6421-236">Revise las tablas de ideas de los líderes.</span><span class="sxs-lookup"><span data-stu-id="c6421-236">Review leader boards of ideas.</span></span>
* <span data-ttu-id="c6421-237">Voten y compartan ideas priorizadas.</span><span class="sxs-lookup"><span data-stu-id="c6421-237">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="c6421-238">Envía ideas para una campaña.</span><span class="sxs-lookup"><span data-stu-id="c6421-238">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="c6421-239">Vea la idea de otro miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-239">View other team member's idea.</span></span>
* <span data-ttu-id="c6421-240">Vota sobre las ideas más queridas.</span><span class="sxs-lookup"><span data-stu-id="c6421-240">Vote on most liked ideas.</span></span>
* <span data-ttu-id="c6421-241">Revise el desempeño de sus ideas en comparación con otras dentro de una campaña.</span><span class="sxs-lookup"><span data-stu-id="c6421-241">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="c6421-242">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-242">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Administrar la vista de campaña](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="c6421-244">Recetas electrónicas</span><span class="sxs-lookup"><span data-stu-id="c6421-244">E-Prescriptions</span></span> 

<span data-ttu-id="c6421-245">E-Prescriptions es una aplicación basada en [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que mejora la telemedicina y la atención virtual mediante la automatización del proceso de emisión de recetas electrónicas a los pacientes.</span><span class="sxs-lookup"><span data-stu-id="c6421-245">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="c6421-246">Los profesionales médicos pueden revisar rápidamente las citas, generar recetas electrónicas y enviar correos electrónicos con archivos adjuntos de receta electrónica a los pacientes directamente dentro de la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-246">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="c6421-247">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-247">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

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

## <a name="employee-training"></a><span data-ttu-id="c6421-252">Formación de empleados</span><span class="sxs-lookup"><span data-stu-id="c6421-252">Employee Training</span></span> 

<span data-ttu-id="c6421-253">La capacitación de los empleados es una aplicación Microsoft Teams que permite a los organizadores publicar, realizar un seguimiento y promover fácilmente eventos de aprendizaje y capacitación para su organización.</span><span class="sxs-lookup"><span data-stu-id="c6421-253">Employee training is a Microsoft Teams app that enables organizers to easily publish, track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="c6421-254">Con la aplicación, los planificadores de eventos pueden enviar recordatorios y notificaciones a los solicitantes de registro de eventos y los empleados pueden indicar interés en los próximos eventos, mantenerse actualizados sobre los eventos actuales y compartir los detalles del evento con los colegas a través de la extensión de mensajería Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-254">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues through the Teams messaging extension.</span></span>

[<span data-ttu-id="c6421-255">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="c6421-256">**Ver eventos de capacitación de empleados** ![ Imagen de la pestaña de capacitación de los empleados](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="c6421-256">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="c6421-257">**Crear evento de capacitación de empleados** ![ Capacitación de empleados crea formulario de evento](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="c6421-257">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="c6421-258">Buscador experto</span><span class="sxs-lookup"><span data-stu-id="c6421-258">Expert Finder</span></span>

<span data-ttu-id="c6421-259">Expert Finder es un [bot Microsoft Teams](../bots/what-are-bots.md) que identifica a miembros específicos de la organización en función de sus habilidades, intereses y atributos educativos.</span><span class="sxs-lookup"><span data-stu-id="c6421-259">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="c6421-260">Los miembros encuentran expertos dentro de una organización que coinciden con una búsqueda de palabras clave de perfiles de usuario Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6421-260">Members find experts within an organization that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="c6421-261">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Demostración de resultados de búsqueda del Buscador de Expertos](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="c6421-263">Preguntas más frecuentes Plus</span><span class="sxs-lookup"><span data-stu-id="c6421-263">FAQ Plus</span></span>

<span data-ttu-id="c6421-264">Los bots conversacionales Q&A son una manera fácil de proporcionar respuestas a las preguntas más frecuentes por parte de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c6421-264">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="c6421-265">Pero, la mayoría de los bots no interactúan con los usuarios de manera significativa porque no hay ningún humano en el bucle cuando el bot falla.</span><span class="sxs-lookup"><span data-stu-id="c6421-265">But, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="c6421-266">Faq bot es un bot Q&A amigable que trae a un humano en el bucle cuando no puede ayudar.</span><span class="sxs-lookup"><span data-stu-id="c6421-266">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="c6421-267">Uno puede hacerle una pregunta al bot y el bot responde con una respuesta si está contenida en la base de conocimiento.</span><span class="sxs-lookup"><span data-stu-id="c6421-267">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="c6421-268">Si no es así, el bot permite al usuario enviar una consulta que luego se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde dentro del propio equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-268">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="c6421-269">La última versión de **FAQ Plus** admite resoluciones Q&A mejoradas al permitir a un equipo de expertos completar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6421-269">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="c6421-270">&#x2714; Agregue nuevas&Q directamente a la base de conocimiento mediante extensiones de mensaje.</span><span class="sxs-lookup"><span data-stu-id="c6421-270">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="c6421-271">&#x2714; Editar y eliminar pares Q&A agregados por un bot.</span><span class="sxs-lookup"><span data-stu-id="c6421-271">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="c6421-272">&#x2714; Realizar un seguimiento del historial de revisiones de Q&As.</span><span class="sxs-lookup"><span data-stu-id="c6421-272">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="c6421-273">&#x2714; Configurar una respuesta con detalles adicionales para mostrarla como tarjeta [adaptable.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="c6421-273">&#x2714; Configure an answer with additional details to display as an [Adaptive Card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="c6421-274">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ Más gif](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="c6421-276">Obtener aplicación de soporte</span><span class="sxs-lookup"><span data-stu-id="c6421-276">Get Support App</span></span>

<span data-ttu-id="c6421-277">La aplicación Obtener soporte técnico es utilizada por organizaciones que usan Microsoft Teams, para permitir que cualquier conjunto de usuarios solicite ayuda a los supervisores.</span><span class="sxs-lookup"><span data-stu-id="c6421-277">The Get Support app is used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="c6421-278">Esta aplicación incluye las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="c6421-278">This app includes the following features:</span></span>
* <span data-ttu-id="c6421-279">Solicitar ayuda en diferentes categorías desde una aplicación de energía.</span><span class="sxs-lookup"><span data-stu-id="c6421-279">Requesting assistance on different categories from a Power App.</span></span>
* <span data-ttu-id="c6421-280">Notificaciones enviadas a los solicitantes informándoles de quién ha sido asignado.</span><span class="sxs-lookup"><span data-stu-id="c6421-280">Notifications sent to requestors informing them of who hare assigned.</span></span>
* <span data-ttu-id="c6421-281">Notificaciones enviadas a los supervisores asignados informándoles de quién necesita ayuda.</span><span class="sxs-lookup"><span data-stu-id="c6421-281">Notifications sent to assigned supervisors informing them of who needs assistance.</span></span> 
* <span data-ttu-id="c6421-282">Análisis de escalamientos y patrones en SharePoint y PowerBI.S.</span><span class="sxs-lookup"><span data-stu-id="c6421-282">Analyzing escalations and patterns in SharePoint and PowerBI.S.</span></span>

[<span data-ttu-id="c6421-283">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-283">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Obtener soporte Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="c6421-285">Rastreador de objetivos</span><span class="sxs-lookup"><span data-stu-id="c6421-285">Goal Tracker</span></span>

<span data-ttu-id="c6421-286">La aplicación Goal Tracker es una solución integral para que su organización admita el establecimiento de objetivos, la observación del progreso y el reconocimiento del éxito dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-286">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="c6421-287">La aplicación permite a los usuarios establecer, realizar un seguimiento y actualizar los objetivos a nivel profesional, personal y de equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-287">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="c6421-288">Los miembros del equipo también reciben recordatorios oportunos y actualizaciones de estado para mantenerse enfocados y mantenerse en el buen camino.</span><span class="sxs-lookup"><span data-stu-id="c6421-288">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="c6421-289">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-289">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![Establecer metas](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Ver objetivos establecidos](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="c6421-292">Grandes ideas</span><span class="sxs-lookup"><span data-stu-id="c6421-292">Great Ideas</span></span>

<span data-ttu-id="c6421-293">La aplicación Great Ideas apoya y potencia la innovación y la creatividad dentro de su organización.</span><span class="sxs-lookup"><span data-stu-id="c6421-293">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="c6421-294">La aplicación permite a sus empleados compartir ideas con colegas y liderazgo, descubrir nuevos envíos, destacar las contribuciones para la consideración por pares y emitir su voto por las mejores propuestas dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-294">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="c6421-295">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-295">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="c6421-298">Actividades grupales</span><span class="sxs-lookup"><span data-stu-id="c6421-298">Group Activities</span></span>

<span data-ttu-id="c6421-299">Actividades de grupo es una aplicación Microsoft Teams que facilita a los propietarios de equipos crear rápidamente grupos de actividades y administrar flujos de trabajo de colaboración en el contexto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-299">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="c6421-300">Los autores de actividades están habilitados para crear actividades, distribuir aleatoriamente a los miembros del equipo en grupos y, opcionalmente, hacer que el bot envíe recordatorios hasta que se completen las actividades.</span><span class="sxs-lookup"><span data-stu-id="c6421-300">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="c6421-301">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-301">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Lista de actividades grupales en Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Mensaje de notificación de actividad de grupo en un canal](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="group-connect-9734"></a><span data-ttu-id="c6421-304">Grupo Conectar &#9734;</span><span class="sxs-lookup"><span data-stu-id="c6421-304">Group Connect &#9734;</span></span>

<span data-ttu-id="c6421-305">Group Conectar es una aplicación Microsoft Teams que ayuda a los miembros de la organización a detectar grupos de empleados y encontrar información relevante para los grupos de empleados.</span><span class="sxs-lookup"><span data-stu-id="c6421-305">Group Connect is a Microsoft Teams app that helps organization members discover employee groups and find information relevant to employee groups.</span></span> <span data-ttu-id="c6421-306">La aplicación viene integrada con capacidades enriquecidas para que los líderes de la organización se comuniquen con sus empleados con respecto a grupos, eventos y recursos.</span><span class="sxs-lookup"><span data-stu-id="c6421-306">The app comes built-in with rich capabilities for organization leaders to communicate with their employees regarding groups, events, and resources.</span></span> <span data-ttu-id="c6421-307">La aplicación Group Conectar también hace coincidir a los miembros del grupo entre sí en la frecuencia deseada para fomentar la creación de redes y la cohesión dentro de un grupo.</span><span class="sxs-lookup"><span data-stu-id="c6421-307">The Group Connect app also matches group members with each other at their desired frequency to encourage networking and cohesion within a group.</span></span> <span data-ttu-id="c6421-308">Para obtener más información sobre cómo puede aprovechar la aplicación de Conectar de grupo para ayudar a los grupos de empleados a fomentar dentro de su organización, consulte la aplicación en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c6421-308">For more information on how you can leverage the Group Connect app to help employee groups foster within your organization, see the app on GitHub.</span></span>

[<span data-ttu-id="c6421-309">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-309">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupconnect)

![Descubre D&grupos I](https://github.com/OfficeDev/microsoft-teams-apps-diversityandinclusion/wiki/Images/temp_group_connect_landing.png)

## <a name="grow-your-skills"></a><span data-ttu-id="c6421-311">Haz crecer tus habilidades</span><span class="sxs-lookup"><span data-stu-id="c6421-311">Grow Your Skills</span></span>

<span data-ttu-id="c6421-312">La aplicación Grow Your Skills apoya el crecimiento y el desarrollo profesionales al permitir que los empleados contribuyan a proyectos suplementarios para su organización mientras aprenden simultáneamente nuevas habilidades.</span><span class="sxs-lookup"><span data-stu-id="c6421-312">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="c6421-313">Los empleados pueden usar la aplicación para localizar oportunidades que satisfagan sus intereses, disfrutar de una colaboración significativa con sus compañeros y adquirir nuevos niveles de experiencia y capacidades, todo dentro del entorno Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-313">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="c6421-314">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-314">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Vista de proyectos disponibles](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de habilidades adquiridas del espectador](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="c6421-317">Soporte de Recursos Humanos</span><span class="sxs-lookup"><span data-stu-id="c6421-317">HR Support</span></span>

<span data-ttu-id="c6421-318">El bot de soporte de HR es un bot Q&A amigable que trae un profesional de soporte o experto del equipo de recursos humanos en el bucle cuando no puede ayudar.</span><span class="sxs-lookup"><span data-stu-id="c6421-318">HR Support bot is a friendly Q&A bot that brings a support professional or expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="c6421-319">Uno puede hacerle una pregunta al bot y el bot responde con una respuesta si está contenida en la base de conocimiento.</span><span class="sxs-lookup"><span data-stu-id="c6421-319">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="c6421-320">Si no es así, el bot permite al usuario enviar una consulta que luego se publica en un equipo preconfigurado de expertos que son ayuda para proporcionar soporte actuando sobre las notificaciones desde dentro de su propio equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-320">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="c6421-321">Además, el bot sugiere vínculos a directivas o preguntas de recursos humanos recomendadas mediante la búsqueda de etiquetas preconfiguradas en la pregunta.</span><span class="sxs-lookup"><span data-stu-id="c6421-321">Additionally, the bot suggests links to recommended HR policies or questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="c6421-322">Estos iconos se encuentran en la pestaña asociada como una referencia rápida.</span><span class="sxs-lookup"><span data-stu-id="c6421-322">These tiles are found in the associated tab as a quick reference.</span></span> <span data-ttu-id="c6421-323">El soporte de recursos humanos funciona bien para Q&A de peso ligero y para proporcionar un apoyo rápido al lanzar nuevos proyectos o iniciativas en la organización.</span><span class="sxs-lookup"><span data-stu-id="c6421-323">HR Support works well for light weight Q&A and to provide quick support when launching new projects or initiatives in the organization.</span></span>

[<span data-ttu-id="c6421-324">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-324">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Soporte de Recursos Humanos](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="c6421-326">Rompehielo</span><span class="sxs-lookup"><span data-stu-id="c6421-326">Icebreaker</span></span>

<span data-ttu-id="c6421-327">Icebreaker es un [bot Microsoft Teams](../bots/what-are-bots.md) que ayuda a tu equipo a acercarse emparejando a dos miembros aleatorios del equipo cada semana para reunirse.</span><span class="sxs-lookup"><span data-stu-id="c6421-327">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="c6421-328">El bot facilita la programación sugiriendo automáticamente tiempos libres que funcionen para ambos miembros.</span><span class="sxs-lookup"><span data-stu-id="c6421-328">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="c6421-329">Fortalecer las conexiones personales y construir una comunidad estrechamente unida con esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6421-329">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="c6421-330">Además de fomentar las conexiones personales en todo el equipo, la aplicación Icebreaker puede ayudar a cultivar comunidades basadas en intereses dentro de su organización.</span><span class="sxs-lookup"><span data-stu-id="c6421-330">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="c6421-331">Por ejemplo, puede usar esta aplicación para un grupo de DevOps interés para ayudar a las ideas y prácticas recomendadas distribuidas orgánicamente por toda la organización.</span><span class="sxs-lookup"><span data-stu-id="c6421-331">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="c6421-332">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-332">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Aplicación rompehielos](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="c6421-334">incentivos</span><span class="sxs-lookup"><span data-stu-id="c6421-334">Incentives</span></span>

<span data-ttu-id="c6421-335">Incentivos es una plantilla [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que gestiona y realiza un seguimiento de la participación incentivada de los empleados en actividades designadas, como capacitaciones e iniciativas de gestión del cambio.</span><span class="sxs-lookup"><span data-stu-id="c6421-335">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities, such as trainings and change management initiatives.</span></span> <span data-ttu-id="c6421-336">Los administradores usan la aplicación para establecer actividades designadas, asignar puntos para completar y especificar los niveles de puntos de elegibilidad necesarios para las recompensas.</span><span class="sxs-lookup"><span data-stu-id="c6421-336">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="c6421-337">Los empleados utilizan la aplicación para ver sus puntos acumulados y, al llegar a la elegibilidad, solicitar y reclamar recompensas canjeables.</span><span class="sxs-lookup"><span data-stu-id="c6421-337">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="c6421-338">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-338">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Incentivos de la demostración de la aplicación](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="c6421-340">Reportero de incidentes</span><span class="sxs-lookup"><span data-stu-id="c6421-340">Incident Reporter</span></span>

<span data-ttu-id="c6421-341">Incident Reporter es un [bot de Microsoft Teams](../bots/what-are-bots.md) que optimiza la administración de incidentes en su organización.</span><span class="sxs-lookup"><span data-stu-id="c6421-341">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="c6421-342">El bot facilita la recopilación automatizada de datos de incidentes, informes de incidentes personalizados, notificaciones relevantes de partes interesadas y seguimiento de incidentes de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="c6421-342">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="c6421-343">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-343">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Vista de alcance del grupo de reporteros de incidentes](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de alcance personal del reportero de incidentes](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection"></a><span data-ttu-id="c6421-346">inspección</span><span class="sxs-lookup"><span data-stu-id="c6421-346">Inspection</span></span> 

 <span data-ttu-id="c6421-347">La inspección es una aplicación Microsoft Teams que permite a los trabajadores de primera línea inspeccionar cualquier cosa, desde ubicaciones hasta activos y equipos.</span><span class="sxs-lookup"><span data-stu-id="c6421-347">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="c6421-348">Por ejemplo, una tienda minorista, una planta de fabricación o vehículos y máquinas.</span><span class="sxs-lookup"><span data-stu-id="c6421-348">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="c6421-349">Hay dos aplicaciones en esta solución, cada una destinada a diferentes tipos de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c6421-349">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="c6421-350">La aplicación permite a los trabajadores de primera línea inspeccionar un activo o área, administrar la calidad de los productos y servicios, o mantener la seguridad en el lugar de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c6421-350">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="c6421-351">Facilita la comunicación entre los miembros del equipo para abordar los problemas encontrados durante la inspección.</span><span class="sxs-lookup"><span data-stu-id="c6421-351">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="c6421-352">La aplicación proporciona informes sencillos para que los administradores aceleren la resolución de problemas y resalten las tendencias.</span><span class="sxs-lookup"><span data-stu-id="c6421-352">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="c6421-353">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Visión general de la inspección](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="c6421-355">Informes de emisión</span><span class="sxs-lookup"><span data-stu-id="c6421-355">Issue Reporting</span></span>

<span data-ttu-id="c6421-356">La aplicación Informes de problemas permite a los empleados y gerentes plantear y administrar problemas.</span><span class="sxs-lookup"><span data-stu-id="c6421-356">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="c6421-357">Consta de dos aplicaciones, aplicación de informes de problemas para informar de problemas y administrar problemas de aplicación para administrar problemas.</span><span class="sxs-lookup"><span data-stu-id="c6421-357">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="c6421-358">Los administradores de equipos usan la aplicación Administrar problemas para configurar la experiencia de la aplicación, incluido el canal en el que la aplicación crea Microsoft Teams mensajes y las tareas de Planificador.</span><span class="sxs-lookup"><span data-stu-id="c6421-358">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="c6421-359">Los administradores también usan la aplicación para crear formularios de plantilla para recopilar detalles cuando un usuario notifica un problema.</span><span class="sxs-lookup"><span data-stu-id="c6421-359">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="c6421-360">Por ejemplo, revise, edite o elimine formularios de plantilla de problema.</span><span class="sxs-lookup"><span data-stu-id="c6421-360">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="c6421-361">La aplicación también se usa para revisar los problemas del equipo, informar sobre el historial de problemas y administrar eficazmente la resolución de problemas.</span><span class="sxs-lookup"><span data-stu-id="c6421-361">The app is also used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="c6421-362">Los empleados usan la aplicación de informes de problemas para registrar los problemas y los detalles necesarios para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="c6421-362">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="c6421-363">La aplicación también se utiliza para modificar y resolver problemas existentes y obtener una vista de alto nivel de problemas individuales o de equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-363">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="c6421-364">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Vista del equipo de informes de problemas](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="c6421-366">Incorporación de nuevos empleados</span><span class="sxs-lookup"><span data-stu-id="c6421-366">New Employee Onboarding</span></span> 

<span data-ttu-id="c6421-367">La incorporación de nuevos empleados es una solución integrada de incorporación de Microsoft Teams y [SharePoint nuevo empleado](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) que permite a su organización proporcionar una experiencia de incorporación consistente y de alta calidad para los empleados en su viaje de nueva contratación.</span><span class="sxs-lookup"><span data-stu-id="c6421-367">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="c6421-368">La aplicación es utilizada por equipos de recursos humanos y gerentes de contratación para proporcionar información relevante a lo largo del proceso de orientación e inducción y por nuevas contrataciones para compartir comentarios, proporcionar presentaciones y completar tareas de incorporación.</span><span class="sxs-lookup"><span data-stu-id="c6421-368">The app is used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="c6421-369">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="c6421-370">**Nueva tarjeta de bienvenida para empleados** ![ Imagen de la nueva tarjeta de bienvenida para empleados](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="c6421-370">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="c6421-371">**Nueva lista de verificación de empleados** ![ Imagen de la nueva lista de verificación de empleados](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="c6421-371">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="c6421-372">Insignias abiertas</span><span class="sxs-lookup"><span data-stu-id="c6421-372">Open Badges</span></span>

<span data-ttu-id="c6421-373">Open Badges es una aplicación Microsoft Teams que permite a las personas obtener insignias de credenciales de aprendizaje digital dentro del contexto Teams y compartirlas en todas partes.</span><span class="sxs-lookup"><span data-stu-id="c6421-373">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="c6421-374">Utilizando las capacidades de la autoridad emisora de insignias digitales de terceros, [Badgr](https://badgr.org/), las insignias otorgadas se registran en el perfil badgr de un destinatario y están disponibles para construir y compartir una imagen rica de los viajes de aprendizaje de por vida.</span><span class="sxs-lookup"><span data-stu-id="c6421-374">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="c6421-375">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![Imagen de las insignias disponibles](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de insignias otorgadas](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="c6421-378">encuesta</span><span class="sxs-lookup"><span data-stu-id="c6421-378">Poll</span></span> 

<span data-ttu-id="c6421-379">Poll es una aplicación de extensión de [mensajería](../messaging-extensions/what-are-messaging-extensions.md) Microsoft Teams personalizada que le permite crear y enviar rápidamente encuestas en un chat o un canal para recopilar opiniones y preferencias del equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-379">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="c6421-380">La aplicación es compatible con todos los clientes de Teams plataforma, como escritorio, navegador, iOS y Android y está lista para su implementación como parte de su suscripción Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="c6421-380">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="c6421-381">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Crear sondeo en Teams vista](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="c6421-383">Respuestas rápidas</span><span class="sxs-lookup"><span data-stu-id="c6421-383">Quick Responses</span></span>

<span data-ttu-id="c6421-384">Quick Responses es una aplicación Microsoft Teams que ofrece una solución sólida para responder eficazmente a las preguntas frecuentes de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c6421-384">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions FAQs.</span></span> <span data-ttu-id="c6421-385">En lugar de responder a cada consulta de forma manual y continua repitiendo información, la aplicación crea una biblioteca de respuestas para una experiencia de usuario interactiva a través de extensiones de [mensajería](../messaging-extensions/what-are-messaging-extensions.md)Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-385">Instead of answering each query manually and continuously repeating information, the app builds a library of responses for an interactive user experience through Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="c6421-386">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-386">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Vista de muestra de las respuestas](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a><span data-ttu-id="c6421-388">&#9734; de preguntas</span><span class="sxs-lookup"><span data-stu-id="c6421-388">Quiz  &#9734;</span></span>

<span data-ttu-id="c6421-389">Quiz es una aplicación de [extensión de mensajería Teams](../messaging-extensions/what-are-messaging-extensions.md) personalizada que le permite crear un cuestionario dentro de un chat o un canal para la comprobación de conocimiento y resultados instantáneos.</span><span class="sxs-lookup"><span data-stu-id="c6421-389">Quiz is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a quiz within a chat or a channel for knowledge check and instantaneous results.</span></span> <span data-ttu-id="c6421-390">Puedes usar quiz para exámenes en clase y sin conexión, verificación de conocimientos dentro del equipo y para cuestionarios divertidos dentro de un equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-390">You can use Quiz for, In-class and offline exams, Knowledge check within team, and for fun quizzes within a team.</span></span> <span data-ttu-id="c6421-391">La aplicación de prueba es compatible con varias plataformas, como Teams clientes de escritorio, navegador, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="c6421-391">Quiz app is supported across multiple platforms, such as Teams desktop, browser, iOS, and Android clients.</span></span> <span data-ttu-id="c6421-392">Esta aplicación está lista para su implementación como parte de la suscripción de Microsoft 365 existente.</span><span class="sxs-lookup"><span data-stu-id="c6421-392">This app is ready for deployment as part of your existing Microsoft 365 subscription.</span></span>

[<span data-ttu-id="c6421-393">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Crear cuestionario en Teams vista](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a><span data-ttu-id="c6421-395">Asistencia rápida</span><span class="sxs-lookup"><span data-stu-id="c6421-395">Rapid Assist</span></span>

<span data-ttu-id="c6421-396">Rapid Assist es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que permite a los asociados orientados al cliente conectarse rápidamente con los expertos para obtener respuestas rápidas, buscar información, realizar un seguimiento de las solicitudes abiertas y permitir que los expertos reciban notificaciones para recibir rápidamente una llamada para ayudar a responder preguntas.</span><span class="sxs-lookup"><span data-stu-id="c6421-396">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="c6421-397">La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams para permitir a las organizaciones conectar fácilmente a los trabajadores de primera línea con enlaces corporativos para resolver las consultas de los clientes y ofrecer una gran experiencia al cliente.</span><span class="sxs-lookup"><span data-stu-id="c6421-397">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="c6421-398">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-398">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Interfaz de solicitud de usuario final](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Vista de solicitud de expertos](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="c6421-401">reflejar</span><span class="sxs-lookup"><span data-stu-id="c6421-401">Reflect</span></span> 

<span data-ttu-id="c6421-402">Reflect es una aplicación de extensión de [mensajería](../messaging-extensions/what-are-messaging-extensions.md) Microsoft Teams personalizada que proporciona un recurso seguro e inclusivo para que los miembros de su equipo compartan el estado de su bienestar emocional con colegas o líderes de grupo directamente dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-402">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues or group leaders directly within Teams.</span></span> <span data-ttu-id="c6421-403">La aplicación está disponible en los chats de canal, grupo, reunión y 1:1 y la respuesta de check-in se establece en público, privado a remitente o totalmente anónimo.</span><span class="sxs-lookup"><span data-stu-id="c6421-403">The app is available in channel, group, meeting, and 1:1 chats and the check-in response is set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="c6421-404">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-404">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="c6421-405">**Encuesta de bienestar**</span><span class="sxs-lookup"><span data-stu-id="c6421-405">**Well-being poll**</span></span>
    
    ![Reflejar encuesta de usuarios de aplicaciones](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="c6421-407">Soporte remoto</span><span class="sxs-lookup"><span data-stu-id="c6421-407">Remote Support</span></span>

<span data-ttu-id="c6421-408">El soporte remoto es un [bot Microsoft Teams](../bots/what-are-bots.md) que proporciona una interfaz enfocada entre los solicitantes de soporte técnico en toda la organización y el equipo de soporte interno.</span><span class="sxs-lookup"><span data-stu-id="c6421-408">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="c6421-409">Los usuarios finales pueden enviar, editar o retirar solicitudes de soporte técnico y el equipo de soporte técnico puede responder, administrar y actualizar las solicitudes desde la plataforma Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-409">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="c6421-410">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-410">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![Solicitar formulario de apoyo](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Solicitar detalles de soporte](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="c6421-413">Solicitud-a-equipo</span><span class="sxs-lookup"><span data-stu-id="c6421-413">Request-a-team</span></span>

<span data-ttu-id="c6421-414">Request-a-team es una aplicación Microsoft Teams que optimiza la creación de nuevos equipos para su organización empresarial.</span><span class="sxs-lookup"><span data-stu-id="c6421-414">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="c6421-415">La aplicación admite la estandarización y las prácticas recomendadas al crear nuevas instancias de equipo mediante la integración de un formulario de solicitud guiado por asistente, un proceso de aprobación incrustado, un panel de estado de solicitud y compilaciones automatizadas del equipo.</span><span class="sxs-lookup"><span data-stu-id="c6421-415">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="c6421-416">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-416">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Vista de página de inicio de solicitud a equipo](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vista de página del asistente de solicitud a equipo](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="c6421-419">Scrums para canales</span><span class="sxs-lookup"><span data-stu-id="c6421-419">Scrums for Channels</span></span>

<span data-ttu-id="c6421-420">Scrums for Channels es una aplicación asistente scrum que permite a los usuarios programar y ejecutar scrums en canales dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-420">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="c6421-421">La aplicación es ideal para equipos remotos y equipos compuestos por miembros de diferentes ubicaciones geográficas y zonas horarias para compartir actualizaciones diarias y garantizar la participación en reuniones de stand-up scrum.</span><span class="sxs-lookup"><span data-stu-id="c6421-421">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="c6421-422">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-422">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="c6421-423">Para realizar reuniones scrum en un chat de grupo, consulte la plantilla de aplicación [Scrums for Group Chat.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="c6421-423">To conduct scrum meetings in a group chat, see [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

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

## <a name="scrums-for-group-chat"></a><span data-ttu-id="c6421-426">Scrums para chat de grupo</span><span class="sxs-lookup"><span data-stu-id="c6421-426">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="c6421-427">La plantilla de aplicación Scrums Status se actualiza y ahora es Scrums para el chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="c6421-427">The Scrums Status app template is updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="c6421-428">Scrums for Group Chat es un asistente de scrum de apoyo que permite a los miembros del chat de grupo ejecutar reuniones asincrónicas de stand-up y compartir fácilmente sus actualizaciones diarias.</span><span class="sxs-lookup"><span data-stu-id="c6421-428">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="c6421-429">Permite a todos los miembros del chat de grupo contribuir al scrum y ver las actualizaciones hechas por otros en el scrum en ejecución.</span><span class="sxs-lookup"><span data-stu-id="c6421-429">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="c6421-430">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-430">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums para la demostración de Chat de Grupo](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="c6421-432">Compartir ahora</span><span class="sxs-lookup"><span data-stu-id="c6421-432">Share Now</span></span> 

<span data-ttu-id="c6421-433">La aplicación Compartir ahora promueve el intercambio positivo de información entre colegas al permitir que los usuarios compartan fácilmente contenido dentro del entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-433">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="c6421-434">Los usuarios interactúan con la aplicación para compartir elementos de interés con los miembros del equipo, descubrir nuevo contenido compartido, establecer preferencias y marcar favoritos para su posterior lectura.</span><span class="sxs-lookup"><span data-stu-id="c6421-434">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="c6421-435">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-435">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Seleccionar vista de contenido](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="c6421-437">Búsqueda de lista de SharePoint</span><span class="sxs-lookup"><span data-stu-id="c6421-437">SharePoint List Search</span></span>

<span data-ttu-id="c6421-438">La colaboración en Microsoft Teams con bastante frecuencia hace referencia a la información contenida en los elementos de una lista de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c6421-438">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="c6421-439">Pegar un enlace al elemento en cuestión obliga a todos a cambiar de contexto lejos de la conversación, encontrar la información necesaria y, a continuación, volver a Teams para continuar la conversación.</span><span class="sxs-lookup"><span data-stu-id="c6421-439">Paste a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="c6421-440">A medida que la conversación continúa, las personas tienen que volver al elemento de referencia varias veces para verificar nuevos comentarios y actualizar sus memorias de la información contenida en el elemento.</span><span class="sxs-lookup"><span data-stu-id="c6421-440">As the conversation continues  people have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="c6421-441">Este cambio de contexto crea una barrera para suavizar la colaboración.</span><span class="sxs-lookup"><span data-stu-id="c6421-441">This context switching creates a barrier to smooth collaboration.</span></span>
<span data-ttu-id="c6421-442">Para resolver este problema, se usa la plantilla de aplicación Lista de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c6421-442">To resolve this problem, the List Search app template is used.</span></span> <span data-ttu-id="c6421-443">Muchos usuarios usan SharePoint para alimentar algunos de los flujos de trabajo principales de sus organizaciones.</span><span class="sxs-lookup"><span data-stu-id="c6421-443">Many users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="c6421-444">Sin embargo, colaborar en torno a las listas es difícil.</span><span class="sxs-lookup"><span data-stu-id="c6421-444">However, collaborating around lists is difficult.</span></span> <span data-ttu-id="c6421-445">Con la plantilla de aplicación Búsqueda de lista en Microsoft Teams, los usuarios pueden insertar información de elementos de SharePoint lista directamente dentro de una conversación de chat para aliviar el cambio de contexto causado al simplemente insertar un vínculo en un chat.</span><span class="sxs-lookup"><span data-stu-id="c6421-445">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="c6421-446">La información se inserta como una tarjeta con formato automático fácil de leer, lo que ayuda a los usuarios a mantenerse involucrados en la conversación.</span><span class="sxs-lookup"><span data-stu-id="c6421-446">The information is inserted as an easy-to-read auto-formatted card, helping the users stay engaged in the conversation.</span></span>

[<span data-ttu-id="c6421-447">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-447">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Lista de aplicaciones de búsqueda](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="c6421-449">Check-ins del personal</span><span class="sxs-lookup"><span data-stu-id="c6421-449">Staff Check-ins</span></span>

<span data-ttu-id="c6421-450">Los check-ins de personal son una aplicación basada en [Power Apps](/powerapps/powerapps-overview) que permite la comunicación de supervisión entre su empresa y el personal de campo.</span><span class="sxs-lookup"><span data-stu-id="c6421-450">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview) based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="c6421-451">El personal puede proporcionar fácilmente información de tiempo crítico y actualizaciones de estado de forma programada o ad hoc directamente desde Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-451">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="c6421-452">La aplicación admite la ubicación en tiempo real, fotos, notas, notificaciones de recordatorio y flujos de trabajo automatizados.</span><span class="sxs-lookup"><span data-stu-id="c6421-452">The app supports real-time location, photos, notes, reminder notifications, and automated workflows.</span></span>

[<span data-ttu-id="c6421-453">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-453">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Crear vista de check-in](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="c6421-455">Encuesta</span><span class="sxs-lookup"><span data-stu-id="c6421-455">Survey</span></span>

<span data-ttu-id="c6421-456">Survey es una aplicación de extensión de [mensajería](../messaging-extensions/what-are-messaging-extensions.md) Microsoft Teams personalizada que te permite crear una encuesta en un chat o un canal para recopilar datos y obtener información procesable.</span><span class="sxs-lookup"><span data-stu-id="c6421-456">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span> <span data-ttu-id="c6421-457">La aplicación es compatible con todos los clientes de Teams plataforma, como escritorio, navegador, iOS y Android y está lista para su implementación como parte de su suscripción Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="c6421-457">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="c6421-458">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-458">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Crear encuesta en Teams vista](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="c6421-460">Recuento de tiempos</span><span class="sxs-lookup"><span data-stu-id="c6421-460">Time Tally</span></span> 

<span data-ttu-id="c6421-461">Un proyecto puede incluir varias tareas y se pueden asignar varios proyectos a los empleados.</span><span class="sxs-lookup"><span data-stu-id="c6421-461">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="c6421-462">Los gerentes están obligados a comprender el progreso del proyecto a través del tiempo empleado en estas tareas.</span><span class="sxs-lookup"><span data-stu-id="c6421-462">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="c6421-463">Esto puede ser una actividad engorrosa, ya que los empleados necesitan rellenar las hojas de horas.</span><span class="sxs-lookup"><span data-stu-id="c6421-463">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="c6421-464">La aplicación Time Tally permite a los empleados llenar sus hojas de horas rápidamente, utilizando el dispositivo móvil, y los gerentes no tienen que hacer un seguimiento con los empleados en la entrada del intervalo de horas.</span><span class="sxs-lookup"><span data-stu-id="c6421-464">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="c6421-465">Los administradores pueden ver la utilización del proyecto en función de los recursos y pueden aprobar o rechazar las entradas.</span><span class="sxs-lookup"><span data-stu-id="c6421-465">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="c6421-466">Se envían notificaciones de recordatorio para garantizar el cumplimiento del horario.</span><span class="sxs-lookup"><span data-stu-id="c6421-466">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="c6421-467">Además, los datos históricos y las utilizaciónes están disponibles para análisis.</span><span class="sxs-lookup"><span data-stu-id="c6421-467">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="c6421-468">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-468">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Recuento de tiempos](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a><span data-ttu-id="c6421-470">Formación &#9734;</span><span class="sxs-lookup"><span data-stu-id="c6421-470">Training  &#9734;</span></span>

<span data-ttu-id="c6421-471">La formación es una aplicación de [extensión de mensajería Teams](../messaging-extensions/what-are-messaging-extensions.md) personalizada que permite a los usuarios publicar una formación dentro de un chat o un canal para compartir y aumentar los conocimientos sin conexión.</span><span class="sxs-lookup"><span data-stu-id="c6421-471">Training is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables users to publish a training within a chat or a channel for offline knowledge sharing and upskilling.</span></span> <span data-ttu-id="c6421-472">La aplicación es compatible con varios clientes de Teams plataforma, como escritorio, navegador, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="c6421-472">The app is supported across multiple Teams platform clients, such as desktop, browser, iOS, and Android.</span></span> <span data-ttu-id="c6421-473">Esta aplicación está lista para su implementación como parte de la suscripción Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="c6421-473">This app is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="c6421-474">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-474">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Crear formación en Teams vista](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a><span data-ttu-id="c6421-476">Redondeo virtual</span><span class="sxs-lookup"><span data-stu-id="c6421-476">Virtual Rounding</span></span>

<span data-ttu-id="c6421-477">Los proveedores de hospitales y salas de emergencias hacen muchas **rondas** por día.</span><span class="sxs-lookup"><span data-stu-id="c6421-477">Hospital and emergency room providers make many **rounds** per day.</span></span> <span data-ttu-id="c6421-478">Estos registros rápidos en los pacientes están destinados a proporcionar una comprobación de estado sobre cómo está el paciente y asegurarse de que se abordan las preocupaciones del paciente.</span><span class="sxs-lookup"><span data-stu-id="c6421-478">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="c6421-479">Si bien el redondeo es una práctica esencial para garantizar que los pacientes estén siendo monitoreados por múltiples tipos de proveedores, representan un enorme drenaje en el EBP, ya que para cada visita, de cada proveedor, se utiliza una nueva máscara y un nuevo conjunto de guantes.</span><span class="sxs-lookup"><span data-stu-id="c6421-479">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves are used.</span></span> <span data-ttu-id="c6421-480">Con estas plantillas de aplicaciones, los trabajadores médicos pueden realizar rondas fácilmente virtualmente, a través de una reunión Microsoft Teams entre el proveedor y el paciente.</span><span class="sxs-lookup"><span data-stu-id="c6421-480">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="c6421-481">También se hace referencia a la solución de redondeo virtual en la entrada de [blog](https://aka.ms/teamsvirtualrounding)Microsoft Health y Ciencias de la Vida.</span><span class="sxs-lookup"><span data-stu-id="c6421-481">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="c6421-482">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-482">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Redondeo virtual](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="c6421-484">Gestión de visitantes</span><span class="sxs-lookup"><span data-stu-id="c6421-484">Visitor Management</span></span>

<span data-ttu-id="c6421-485">La aplicación Gestión de visitantes permite a su organización y empleados administrar de forma fácil y eficiente el proceso de visitantes in situ, directamente desde Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c6421-485">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="c6421-486">La aplicación permite a los empleados crear solicitudes de visitantes, realizar un seguimiento central del estado de una solicitud a través del panel de visitantes y recibir notificaciones en tiempo real cuando llega un visitante.</span><span class="sxs-lookup"><span data-stu-id="c6421-486">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="c6421-487">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-487">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="c6421-490">Premios en el lugar de trabajo</span><span class="sxs-lookup"><span data-stu-id="c6421-490">Workplace Awards</span></span>

<span data-ttu-id="c6421-491">Workplace Awards es una plantilla de aplicación Teams que proporciona un marco positivo para fomentar el reconocimiento y fomentar la cultura de la apreciación de los empleados en el lugar de trabajo moderno.</span><span class="sxs-lookup"><span data-stu-id="c6421-491">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="c6421-492">La aplicación le permite configurar y administrar una recompensa y reconocimiento de empleados, llamado programa R&R donde los empleados pueden nominar y respaldar fácilmente a sus colegas y su líder R&R puede ver las nominaciones presentadas, conceder premios y anunciar destinatarios.</span><span class="sxs-lookup"><span data-stu-id="c6421-492">The app enables you to setup and manage an employee rewards and recognition, called R&R program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="c6421-493">Sómelo en GitHub</span><span class="sxs-lookup"><span data-stu-id="c6421-493">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="c6421-494">Tarjeta de nominación de premios en el lugar de trabajo</span><span class="sxs-lookup"><span data-stu-id="c6421-494">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Pestaña de lista de premios en el lugar de trabajo](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="c6421-496">Para obtener más información sobre la plantilla de aplicación, consulte [Plantilla de aplicación](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span><span class="sxs-lookup"><span data-stu-id="c6421-496">For more information on app template, see [App template](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>

## <a name="see-also"></a><span data-ttu-id="c6421-497">Vea también</span><span class="sxs-lookup"><span data-stu-id="c6421-497">See also</span></span>

[<span data-ttu-id="c6421-498">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="c6421-498">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
