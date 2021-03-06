---
title: Microsoft Teams de aplicación
description: Vínculos y descripciones de plantillas de aplicación para la Microsoft Teams plataforma
ms.topic: reference
keywords: Microsoft Teams de ejemplos de plantillas
localization_priority: Normal
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 72bb5506e552dfa3d35426e99a7ee74088ef41f6
ms.sourcegitcommit: 0a775ae12419f3bc7484e557f4b4ae815bab64ec
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/08/2021
ms.locfileid: "53333697"
---
# <a name="app-templates-for-microsoft-teams"></a>Plantillas de aplicaciones para Microsoft Teams

Las plantillas de aplicación son ejemplos de aplicaciones completas para Microsoft Teams que son de código abierto y están disponibles en GitHub. Cada plantilla de aplicación contiene instrucciones detalladas para implementar e instalar esa aplicación para la organización. También proporciona una aplicación de ejemplo que puedes instalar y empezar a usar inmediatamente. El código fuente completo también está disponible, lo que le permite explorarlo en detalle o bifurcar el código y modificarlo para satisfacer sus requisitos específicos.
Todas las plantillas de aplicación se proporcionan en los términos [de licencia mit.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)

> [!NOTE] 
> Debes licenciar y admitir aplicaciones creadas a partir de plantillas de aplicación para tus usuarios y organizaciones.

**&#9734; indica las plantillas de aplicación recién publicadas.**

### <a name="key-benefits"></a>Ventajas clave

* **Implemente directamente en la nube:** Todas las plantillas de aplicación incluyen scripts de implementación que te permiten hospedar todos los servicios necesarios en Microsoft Azure o en power platform. 
* **Código de ejemplo recomendado:** Las plantillas de la aplicación se ajustan a los procedimientos recomendados en materia de seguridad e infraestructura. Se revisan todos los cambios enviados por la comunidad a las plantillas de la aplicación para garantizar la conformidad.
* **Personalizable y extensible:** Aunque todas las plantillas de aplicación se implementan con una configuración mínima, se proporcionan todos los scripts de implementación y base de código completos, para que puedas personalizarlas o ampliarlas fácilmente para que se ajusten a tus necesidades únicas.
* **Documentación detallada:** Todas las plantillas de aplicación van acompañadas de documentación completa sobre los pasos de configuración, implementación y arquitectura de soluciones.  

## <a name="adoption-bot"></a>Bot de adopción 

Bot de adopción es un bot de chat de atención al usuario creado con Power Virtual Agent para Teams PVA. Se considera como la versión PVA de FAQ Plus. Bot de adopción responde a más de 100 preguntas comunes sobre Microsoft 365 y Teams. Puede editar los temas existentes, agregar sus propios temas e ingerir preguntas frecuentes existentes. Si los usuarios necesitan ayuda adicional, el Bot de adopción puede conectarlos a expertos o incluso extenderse para abrir vales de servicio con conectores de flujo premium. Este bot se instala automáticamente o se basa en una aplicación personalizada, como el Centro [de adopción.](https://github.com/akporzondek/adoption_hub)

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a>Herramienta de adopción: plataforma de administración de campeones &#9734;

La plantilla de aplicación Champion Management Platform (CMP) te ayuda a administrar, escalar e inspirar a los campeones del trabajo en equipo para lograr más. Esta plantilla de aplicación se basa en el SharePoint Framework y se carga en una pestaña dentro de un equipo. Los grupos pueden aprovechar esta herramienta para ayudar a administrar la pertenencia al programa, proporcionar una tabla de clasificación y tipos de eventos para el registro y herramientas para superponer distintivos digitales a los participantes del programa.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a>Herramienta de adopción: Microsoft 365 Learning rutas de acceso (Introducción) &#9734;

La Introducción de aplicación te permite aportar la potencia de las Microsoft 365 de aprendizaje dentro de Microsoft Teams. Esta plantilla de aplicación te permite conceder un acceso fácil a páginas de aprendizaje específicas u otros activos de intranet y cargar el contenido directamente dentro de Teams. También puedes cambiar el nombre o el logotipo de la aplicación para que coincida con la personalción de marca de tu empresa.

[Obtenerlo en GitHub](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a>Administrador de citas 

Appointment Manager es una plantilla Teams aplicación para ayudar a las empresas a crear, administrar y llevar a cabo citas virtuales con los consumidores a través de Teams. Las nuevas solicitudes de cita de los consumidores están visibles en Teams canales, donde se asignan y reasignan rápidamente al personal de un equipo. Las solicitudes de cita se ven en niveles de equipo o personales a través de pestañas personalizadas. Cada cita está asociada a una Teams en línea, por lo que el personal y los consumidores pueden unirse fácilmente a la reunión en el momento programado.

La plantilla de aplicación se integra con Microsoft Bookings para facilitar la administración de citas. Las citas programadas aparecen automáticamente en los calendarios de los miembros del personal asignados y los consumidores reciben notificaciones y avisos de correo electrónico personalizables con vínculos de reunión incrustados.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

![Appointment Manager Overview ](../assets/images/appointment-manager-overview.png)
 ![ Appointment Manager in Teams](../assets/images/appointment-manager-2.png)

## <a name="ask-away"></a>Preguntar fuera

Ask Away es un [bot Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios realizar preguntas y respuestas, denominadaS&sesiones A dentro de Teams. Con el bot Preguntar, los miembros del equipo pueden enviar y votar por arriba preguntas compartidas por compañeros, lo que permite que los hosts de preguntas&A recopile fácilmente las preguntas más importantes dentro de un canal o chat. El bot se usa para realizar una sesión de preguntas en tiempo real&Una sesión en una reunión de Teams y permite a los asistentes enviar preguntas en directo a través del chat.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Vista del cuadro de diálogo emergente de la tabla de clasificación para que los usuarios voten sobre las preguntas](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a>Información de asociados

Associate Ideas es una [plantilla Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que permite a los trabajadores de primera línea capturar y enviar directamente la opinión, el sentimiento y la percepción del cliente. Los trabajadores de primera línea suelen ser el primer representante de la compañía en interactuar con los clientes en un punto a uno de contacto. Los equipos empresariales comparten y usan los datos recopilados de forma colaborativa, como a través de una pestaña Power BI Teams, para mejorar el producto y mejorar la experiencia del cliente.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Vista de comentarios de las perspectivas generadas por la aplicación](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Power BI vista de información generada por la aplicación](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a>Asistencia

La aplicación Asistencia es una [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que se ancla en un equipo. Está diseñado para registrar la presencia en configuraciones, como entornos de aprendizaje y aprendizaje. Los usuarios pueden marcar o editar la asistencia durante un máximo de 30 días en el pasado y ver informes de asistencia resumidos para un grupo completo o asistentes individuales. Para obtener más información sobre la asistencia de los equipos, vea [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).

La siguiente imagen muestra la demostración de la aplicación de asistencia:  

![Demostración de la aplicación de asistencia](../assets/images/attendance-app.png)

## <a name="book-a-room"></a>Libro a sala

Book-a-room es un bot de [Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30, 60 o 90 minutos a partir de la hora actual. El tiempo predeterminado es de 30 minutos. El bot Book-a-room tiene ámbitos para conversaciones personales o 1:1. Para obtener más información sobre la aplicación Book-a-room, consulta [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).  
En la siguiente imagen se muestra la demostración libro a sala:

![Demostración de libro a sala](../assets/images/book-a-room.png)

## <a name="building-access"></a>Acceso de creación

Building Access es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que admite la administración de umbrales de ocupación y normas de distanciamiento social al permitir a los directores de instalaciones administrar, realizar un seguimiento e informar de la presencia de los empleados en el sitio. La aplicación, creada con Microsoft [Power Apps](/powerapps/powerapps-overview)y [Power Automate](/power-automate/getting-started), se integra profundamente con Microsoft Teams y permite a las organizaciones determinar la preparación de la creación, establecer criterios de elegibilidad para el acceso en el sitio y recopilar información para la planeación futura.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Crear tarjeta de reserva de Access](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Creación de la vista clave de Access](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a>Celebraciones

Celebraciones es una Teams que ayuda a los miembros del equipo a celebrar los cumpleaños, aniversarios y otros eventos periódicos. Recuerda ocasiones especiales de todos los miembros del equipo y envía un mensaje descriptivo en todos los equipos seleccionados en el momento de la creación de eventos, para que los miembros del equipo se sientan especiales en su día.

La aplicación proporciona una interfaz sencilla para que todos los miembros del equipo agreguen y visualen personalmente sus eventos y también permite al usuario seleccionar los equipos en los que se comparten los eventos.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a>Lista de comprobación

Lista de comprobación es una aplicación Microsoft Teams extensión de [mensajería](../messaging-extensions/what-are-messaging-extensions.md) personalizada que te permite colaborar con tu equipo creando una lista de comprobación compartida en un chat o canal. La aplicación se admite en todos los Teams de la plataforma, como el explorador de escritorio, iOS y Android. La aplicación está lista para la implementación como parte de la Microsoft 365 suscripción.  

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![Crear lista de comprobación en Teams vista](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a>Classroom Drop-in 

Classroom Drop-in es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que permite a los líderes del sistema encontrar equipos de clase, significa aulas virtuales y agregarse a sí mismos u otros a estos equipos de clase durante un período de entrega especificado, según sea necesario. La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate](/power-automate/getting-started), se integra profundamente con Microsoft Teams para garantizar que los institutos educativos puedan optimizar sus operaciones en un entorno de aprendizaje híbrido proporcionando acceso a partes interesadas relevantes para los equipos de clase por requisitos empresariales.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Solicitud de acceso a clases](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a>Comunicador de la empresa

La aplicación Communicator empresa permite a los equipos corporativos crear y enviar mensajes destinados a varios equipos o a un gran número de empleados a través del chat, lo que permite a la organización llegar a los empleados justo donde colaboran. Use esta plantilla para varios escenarios, como anuncios de nuevas iniciativas, incorporación de empleados, aprendizaje moderno y desarrollo o difusión en toda la organización.

La aplicación proporciona una interfaz sencilla para que los usuarios designados creen, obtengan una vista previa, colaboren y envíen mensajes.

Proporciona una base para crear capacidades de comunicación personalizadas dirigidas, como telemetría personalizada, sobre cuántos usuarios han reconocido o interactuado con un mensaje.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator vista de cuadro de redacción](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a>Búsqueda de grupos de contactos

La aplicación Búsqueda de grupos de contactos proporciona un enfoque práctico y útil para crear, acceder y administrar los grupos de contactos de la organización, anteriormente conocidos como listas de distribución o grupos de comunicación. Los usuarios pueden ver y chatear rápidamente con miembros del grupo, ver el estado de los miembros y crear un chat de grupo con miembros seleccionados en el grupo de contactos, todo dentro del entorno Teams grupo.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

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

## <a name="co-worker-appreciation"></a>Apreciación del compañero de trabajo 

Con la plantilla de apreciación de compañeros de trabajo en Microsoft Teams, los usuarios pueden reconocer los logros de sus compañeros en el contexto Teams trabajo. Cuando los compañeros de trabajo seleccionan recompensar a un compañero, los destinatarios y otros miembros del equipo se etiquetan en una conversación de canal y reciben una notificación sobre los detalles de la concesión del canal. Los galardones se registran en la Teams, que es segura, portátil y fácilmente compartible. Esto se considera como la versión basada en PowerApps de la plantilla de aplicación Open Badges, con una tabla de clasificación.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![General](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a>CrowdSourcer

CrowdSourcer es un [bot Microsoft Teams que](../bots/what-are-bots.md) proporciona a los equipos información consultada procedente de forma colaborativa de miembros del grupo. Ayuda a responder a las preguntas más frecuentes a la vez que permite a los participantes participar activamente y contribuir a un recurso de información divertido y útil.

[Obtenerlo en Github](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interacción entre usuarios finales de Crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a>Adhesivos personalizados

La autoexpresión es fundamental para una cultura de equipo en buen estado. Esta plantilla de aplicación es una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) que permite a los usuarios usar adhesivos y GIF personalizados dentro de Microsoft Teams. Esta plantilla proporciona una experiencia de configuración sencilla basada en web en la que cualquier persona con acceso a la configuración puede cargar los GIF, adhesivos e imágenes que desean que tengan sus usuarios, lo que permite a todo el equipo usar cualquier conjunto de adhesivos que elija.

Esta aplicación también permite compartir fácilmente imágenes, GIF, adhesivos entre equipos sin necesidad de tener acceso SharePoint sitios o canales individuales como mecanismos de almacenamiento y uso compartido. Por ejemplo, los equipos de productos pueden compartir fácilmente imágenes de producto y GIF a redes sociales, marketing y equipos de ventas mediante programación. También se puede extender esta aplicación desencadenando un flujo de notificación a equipos o individuos específicos cuando se hacen disponibles imágenes nuevas y GIF.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Aplicación Stickers](../assets/images/stickers.png)

## <a name="employee-ideas"></a>Ideas de los empleados

La aplicación Ideas para empleados es la versión de PowerApps de la plantilla de aplicación Great Ideas basada en Azure. La aplicación permite a los Teams configurar y configurar una campaña de ideas. Una campaña de ideas es una categoría para agrupar ideas en torno a temas comunes.

Teams usuarios también pueden realizar las siguientes actividades:

* Configure un formulario de envío estándar que los empleados deben enviar para cada idea. 
* Revisa y administra las ideas y la lista de campañas.
* Modificar y eliminar campañas.
* Revisar las tablas de ideas de líderes.
* Vota y comparte ideas priorizadas.
* Enviar ideas para una campaña.
* Ver la idea de otro miembro del equipo.
* Vota sobre las ideas que más te gustan.
* Revisa el rendimiento de sus ideas en comparación con otras personas dentro de una campaña.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Administrar vista de campaña](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a>E-Prescriptions 

E-Prescriptions es una [aplicación](/powerapps/maker/canvas-apps/embed-teams-app) Power Apps que mejora la telemedicina y el cuidado virtual mediante la automatización del proceso de emisión de recetas electrónicas a los pacientes. Los profesionales médicos pueden revisar rápidamente las citas, generar recetas electrónicas y enviar correos electrónicos con datos adjuntos de la receta electrónica a los pacientes directamente dentro de Teams plataforma.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![Captura de pantalla de la aplicación E-Prescriptions. Muestra cómo un proveedor de atención médica puede seleccionar un botón generar para pedir una receta para un paciente.](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Captura de pantalla de la aplicación E-Prescriptions. Muestra cómo los administradores pueden administrar los proveedores de atención médica que usan la aplicación.](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a>Formación de empleados 

La formación de los empleados es una Microsoft Teams que permite a los organizadores publicar, realizar un seguimiento y promover fácilmente eventos de aprendizaje y aprendizaje para su organización.  Con la aplicación, los organizadores de eventos pueden enviar avisos y notificaciones a los registradores de eventos y los empleados pueden indicar interés en los próximos eventos, mantenerse actualizados sobre los eventos actuales y compartir detalles de eventos con compañeros a través de la extensión de mensajería Teams.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    **Ver eventos de formación de empleados** ![ Imagen de pestaña Formación de los empleados](../assets/images/employee-training-discover-tab.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    **Crear evento de formación de empleados** ![ Formulario de creación de eventos de formación para empleados](../assets/images/employee-training-create-event.jpg)
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a>Buscador de expertos

Buscador de expertos es [un bot Microsoft Teams](../bots/what-are-bots.md) que identifica miembros específicos de la organización en función de sus habilidades, intereses y atributos educativos. Los miembros encuentran expertos dentro de una organización que coinciden con una búsqueda de palabras clave Azure Active Directory perfiles de usuario.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Demostración de resultados de búsqueda del Buscador de expertos](../assets/images/expert-finder.png)

## <a name="faq-plus"></a>Preguntas más frecuentes Plus

Preguntas conversacionales&Bots son una forma sencilla de proporcionar respuestas a las preguntas más frecuentes de los usuarios. Sin embargo, la mayoría de los bots no pueden interactuar con los usuarios de forma significativa porque no hay ningún humano en el bucle cuando se produce un error en el bot. Faq bot is a friendly Q&A bot that brings a human in the loop when it is unable to help. Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos. Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde el propio equipo.

> [!NOTE]
> La versión más reciente de **FAQ Plus** admite resoluciones de preguntas&A al permitir a un equipo de expertos completar lo siguiente:
>
> &#x2714; agregar nuevas preguntas&Como directamente a la base de conocimientos mediante extensiones de mensaje.
>
> &#x2714; Editar y eliminar preguntas&Pares agregados por un bot.
>
> &#x2714; seguimiento del historial de revisiones de Q&As.
>
> &#x2714; configurar una respuesta con detalles adicionales para mostrar como [una tarjeta adaptable](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).
>
[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif de preguntas más frecuentes](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a>Obtener aplicación de soporte técnico

La aplicación Obtener soporte técnico la usan las organizaciones que usan Microsoft Teams, para permitir que cualquier conjunto de usuarios solicite asistencia a los supervisores. Esta aplicación incluye las siguientes características:
* Solicitar asistencia en distintas categorías desde una Power App.
* Notificaciones enviadas a los solicitantes para informarles de quién está asignado.
* Notificaciones enviadas a supervisores asignados que les informan de quién necesita asistencia. 
* Análisis de escalaciones y patrones en SharePoint y Power BI.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Obtener gif de soporte técnico](../assets/images/get-support.gif)

## <a name="goal-tracker"></a>Rastreador de objetivos

La aplicación Rastreador de objetivos es una solución completa para que la organización admita el establecimiento de objetivos, la observación del progreso y el reconocimiento del éxito en Microsoft Teams. La aplicación permite a los usuarios establecer, realizar un seguimiento y actualizar objetivos en un nivel profesional, personal y de equipo. Los miembros del equipo también reciben avisos oportunos y actualizaciones de estado para mantenerse centrados y mantenerse al día.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a>Grandes ideas

La aplicación Great Ideas admite y potencia la innovación y la creatividad dentro de la organización. La aplicación permite a los empleados compartir ideas con compañeros y líderes, descubrir nuevos envíos, contribuciones destacadas para la consideración del mismo nivel y emitir su voto para las mejores propuestas dentro de Microsoft Teams.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a>Actividades de grupo

Actividades de grupo es una Microsoft Teams que facilita a los propietarios de equipos crear rápidamente grupos de actividades y administrar flujos de trabajo de colaboración en el contexto de Microsoft Teams. Los autores de actividades están habilitados para crear actividades, distribuir aleatoriamente miembros del equipo en grupos y, opcionalmente, hacer que el bot envíe avisos hasta que se completen las actividades.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

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

## <a name="group-connect-9734"></a>Grupos Conectar &#9734;

Group Conectar es una aplicación Microsoft Teams que ayuda a los miembros de la organización a descubrir grupos de empleados y a encontrar información relevante para los grupos de empleados. La aplicación viene integrada con funciones enriquecciones para que los líderes de la organización se comuniquen con sus empleados en relación con grupos, eventos y recursos. La aplicación group Conectar también coincide con los miembros del grupo entre sí en la frecuencia deseada para fomentar la red y la cohesión dentro de un grupo. Para obtener más información sobre cómo puedes aprovechar la aplicación Group Conectar para ayudar a los grupos de empleados a fomentar dentro de tu organización, consulta la aplicación en GitHub.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-groupconnect)

![Descubrir grupos D&I](https://github.com/OfficeDev/microsoft-teams-apps-diversityandinclusion/wiki/Images/temp_group_connect_landing.png)

## <a name="grow-your-skills"></a>Aumentar sus habilidades

La aplicación Crecer tus habilidades admite el crecimiento y el desarrollo profesionales, ya que permite a los empleados contribuir a proyectos complementarios para tu organización al mismo tiempo que aprenden nuevas habilidades. Los empleados pueden usar la aplicación para buscar oportunidades que satisfagan sus intereses, disfrutar de una colaboración significativa con compañeros y adquirir nuevos niveles de experiencia y capacidades, todo dentro del entorno Teams.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

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

## <a name="hr-support"></a>Soporte de Recursos Humanos

Bot de soporte técnico de RECURSOS es una pregunta&Un bot que lleva a un profesional de soporte técnico o experto del equipo de recursos humanos en el bucle cuando no puede ayudar. Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos. Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde el propio equipo. Además, el bot sugiere vínculos a las directivas o preguntas de RECURSOS humanos recomendadas mediante la búsqueda de etiquetas preconfiguradas en la pregunta. Estos iconos se encuentran en la pestaña asociada como una referencia rápida. El soporte de recursos humanos funciona bien para preguntas&A y para proporcionar soporte rápido al iniciar nuevos proyectos o iniciativas en la organización.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Soporte de Recursos Humanos](../assets/images/expert-user.png)

## <a name="icebreaker"></a>Rompehielo

Icebreaker es un [bot Microsoft Teams](../bots/what-are-bots.md) que ayuda al equipo a acercarse emparejando dos miembros del equipo aleatorios cada semana para reunirse. El bot facilita la programación al sugerir automáticamente horas libres que funcionen para ambos miembros. Fortalezca las conexiones personales y cree una comunidad estrechamente unida con esta aplicación.

Además de fomentar las conexiones personales en todo el equipo, la aplicación Icebreaker puede ayudar a cultivar comunidades basadas en intereses dentro de la organización. Por ejemplo, puedes usar esta aplicación para un grupo de DevOps de interés para ayudar a que las ideas y los procedimientos recomendados se extienda orgánicamente en toda la organización.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker app](../assets/images/icebreaker.png)

## <a name="incentives"></a>Incentivos

Incentives es una [plantilla Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que administra y realiza un seguimiento de la participación de los empleados en actividades designadas, como cursos e iniciativas de administración de cambios. Los administradores usan la aplicación para establecer actividades designadas, asignar puntos para su finalización y especificar los niveles de puntos de elegibilidad necesarios para las recompensas. Los empleados usan la aplicación para ver sus puntos acumulados y, al alcanzar la elegibilidad, solicitar y reclamar recompensas canjeables.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Demostración de aplicaciones de incentivos](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a>Reportero de incidentes

Incident Reporter es un [bot Microsoft Teams que](../bots/what-are-bots.md) optimiza la administración de incidentes en la organización. El bot facilita la recopilación automatizada de datos de incidentes, informes de incidentes personalizados, notificaciones relevantes para las partes interesadas y seguimiento de incidentes de un extremo a otro.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

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

## <a name="inspection"></a>Inspección 

 Inspección es una aplicación Microsoft Teams que permite a los trabajadores de primera línea inspeccionar cualquier cosa desde ubicaciones hasta activos y equipos. Por ejemplo, una tienda comercial, una planta de fabricación o vehículos y máquinas. Hay dos aplicaciones en esta solución, cada una destinada a diferentes tipos de usuarios.

La aplicación permite a los trabajadores de primera línea inspeccionar un activo o área, administrar la calidad de los productos y servicios o mantener la seguridad en el lugar de trabajo. Facilita la comunicación entre los miembros del equipo para solucionar los problemas encontrados durante la inspección. La aplicación proporciona informes sencillos para que los administradores agilicen la resolución de problemas y resalten las tendencias.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Introducción a la inspección](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a>Informes de problemas

La aplicación De informes de problemas permite a los empleados y administradores generar y administrar problemas. Consta de dos aplicaciones, Aplicación de informes de problemas para informar y Aplicación Administrar problemas para administrar problemas.

Los jefes de equipo usan la aplicación Administrar problemas para configurar la experiencia de la aplicación, incluido el canal en el que la aplicación crea Microsoft Teams mensajes y tareas de Planner. Los administradores también usan la aplicación para crear formularios de plantilla para recopilar detalles cuando un usuario informa de un problema. Por ejemplo, revise, edite o elimine formularios de plantilla de problema. La aplicación también se usa para revisar los problemas del equipo, informar sobre el historial de problemas y administrar eficazmente la resolución de problemas.

Los empleados usan la aplicación De informes de problemas para registrar problemas y detalles necesarios para resolverlos. La aplicación también se usa para modificar y resolver problemas existentes y obtener una vista de alto nivel de problemas individuales o de equipo.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Vista de equipo de informes de problemas](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a>Incorporación de nuevos empleados 

La incorporación de nuevos empleados es una solución integrada de incorporación Microsoft Teams y SharePoint nuevos empleados que permite a su organización proporcionar una experiencia de incorporación coherente y de alta calidad [para](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) los empleados en su viaje de nueva contratación. Los equipos de recursos humanos y los administradores de contratación usan la aplicación para proporcionar información relevante durante todo el proceso de orientación e inducción, así como para que los nuevos empleados compartan comentarios, proporcionen introducciones y completen tareas de incorporación.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    **Nueva tarjeta de bienvenida para empleados** ![ Imagen de la nueva tarjeta de bienvenida del empleado](../assets/images/new-employee-welcome-card.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    **Lista de comprobación de nuevos empleados** ![ Imagen de la lista de comprobación de nuevos empleados](../assets/images/new-employee-checklist.png)  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a>Distintivos abiertos

Open Badges es una aplicación Microsoft Teams que permite a los usuarios obtener distintivos de credenciales de aprendizaje digital en el contexto Teams y compartirlos en todas partes. Con las funcionalidades de la entidad emisora de distintivos digitales de terceros, [Badgr](https://badgr.org/), los distintivos concedidos se registran en el perfil badgr de un destinatario y están disponibles para crear y compartir una imagen enriquecida de los recorridos de aprendizaje de por vida.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a>Sondeo 

Poll es una aplicación [](../messaging-extensions/what-are-messaging-extensions.md) Microsoft Teams de mensajería personalizada que te permite crear y enviar sondeos rápidamente en un chat o un canal para recopilar opiniones y preferencias del equipo. La aplicación se admite en todos los clientes de la plataforma Teams, como escritorio, explorador, iOS y Android, y está lista para su implementación como parte de la Microsoft 365 suscripción.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Crear sondeo en Teams vista](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a>Respuestas rápidas

Respuestas rápidas es una Microsoft Teams que ofrece una solución sólida para responder eficazmente a las preguntas frecuentes de los usuarios. En lugar de responder a cada consulta de forma manual y continua, la aplicación crea una biblioteca de respuestas para una experiencia de usuario interactiva a través de Teams [de mensajería](../messaging-extensions/what-are-messaging-extensions.md).

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Vista de ejemplo de las respuestas](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a>Cuestionario &#9734;

Quiz es una [aplicación](../messaging-extensions/what-are-messaging-extensions.md) Teams de mensajería personalizada que te permite crear un cuestionario dentro de un chat o un canal para comprobar el conocimiento y obtener resultados instantáneos. Puedes usar Quiz para exámenes en clase y sin conexión, comprobación de conocimientos dentro del equipo y para cuestionarios divertidos dentro de un equipo. La aplicación quiz se admite en varias plataformas, como Teams escritorio, explorador, iOS y clientes Android. Esta aplicación está lista para la implementación como parte de la suscripción Microsoft 365 existente.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Crear cuestionario en Teams vista](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a>Asistencia rápida

Rapid Assist es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que permite a los asociados que se enfrentan al cliente conectarse rápidamente con los expertos para obtener respuestas rápidas, buscar información, realizar un seguimiento de las solicitudes abiertas y permitir que los expertos reciban notificaciones para obtener rápidamente una llamada para ayudar a responder preguntas. La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams para permitir que las organizaciones conecten fácilmente a los trabajadores de primera línea con vínculos corporativos para resolver las consultas de los clientes y ofrecer una gran experiencia de cliente. 

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Interfaz de solicitud de usuario final](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Vista de solicitud de experto](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a>Reflejar 

Reflect es una [aplicación](../messaging-extensions/what-are-messaging-extensions.md) de extensión de mensajería Microsoft Teams personalizada que proporciona un recurso seguro e inclusivo para que los miembros del equipo compartan el estado de su bienestar emocional con compañeros o jefes de grupo directamente dentro de Teams. La aplicación está disponible en chats de canal, grupo, reunión y 1:1 y la respuesta de la comprobación se establece en pública, privada a remitente o totalmente anónima.

[Obtenerlo en GitHub](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    **Sondeo de bienestar**
    
    ![Reflejar sondeo de usuarios de aplicaciones](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a>Soporte remoto

El soporte remoto es [un bot Microsoft Teams](../bots/what-are-bots.md) que proporciona una interfaz centrada entre los solicitantes de soporte técnico de toda la organización y el equipo de soporte técnico interno.  Los usuarios finales pueden enviar, editar o retirar solicitudes de soporte técnico y el equipo de soporte técnico puede responder, administrar y actualizar solicitudes en toda la Teams plataforma.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a>Request-a-team

Request-a-team es una aplicación Microsoft Teams que optimiza la creación de nuevos equipos para la organización empresarial. La aplicación admite la estandarización y los procedimientos recomendados al crear nuevas instancias de equipo mediante la integración de un formulario de solicitud guiado por asistente, un proceso de aprobación incrustado, un panel de estado de solicitud y compilaciones automatizadas de equipo.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

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

## <a name="scrums-for-channels"></a>Scrums para canales

Scrums para canales es una aplicación auxiliar de scrum que permite a los usuarios programar y ejecutar scrums en canales dentro de Microsoft Teams. La aplicación es ideal para equipos remotos y equipos formados por miembros de distintas ubicaciones geográficas y zonas horarias para compartir actualizaciones diarias y garantizar la participación en reuniones de soporte de scrum.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> Para realizar reuniones de scrum en un chat de grupo, consulta [Scrums for Group Chat](#scrums-for-group-chat) app template.

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

## <a name="scrums-for-group-chat"></a>Scrums para chat en grupo

> [!NOTE]
> La plantilla de aplicación Estado de Scrums se actualiza y ahora es Scrums para chat en grupo.

Scrums for Group Chat es un asistente de scrum de apoyo que permite a los miembros del chat de grupo ejecutar reuniones de soporte asincrónicas y compartir fácilmente sus actualizaciones diarias. Permite a todos los miembros del chat de grupo contribuir al scrum y ver las actualizaciones realizadas por otros usuarios en el scrum en ejecución.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Demostración de Scrums para chat en grupo](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a>Compartir ahora 

La aplicación Compartir ahora promueve el intercambio positivo de información entre compañeros al permitir a los usuarios compartir fácilmente contenido dentro del entorno Teams usuario. Los usuarios interactúan con la aplicación para compartir elementos de interés con los miembros del equipo, descubrir nuevo contenido compartido, establecer preferencias y favoritos de marcadores para su lectura posterior.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Seleccionar vista de contenido](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a>Búsqueda de lista de SharePoint

La colaboración Microsoft Teams suele hacer referencia a la información contenida en los elementos de una SharePoint lista. Pegar un vínculo al elemento en cuestión obliga a todos a cambiar el contexto de la conversación, buscar la información necesaria y, a continuación, volver a Teams para continuar la conversación. A medida que continúa la conversación, los usuarios tienen que volver al elemento de referencia varias veces para comprobar nuevos comentarios y actualizar sus memorias de la información contenida en el elemento. Este cambio de contexto crea una barrera para una colaboración fluida.
Para resolver este problema, se usa la plantilla de aplicación Búsqueda de lista. Muchos usuarios usan SharePoint para crear algunos de los flujos de trabajo principales de sus organizaciones. Sin embargo, es difícil colaborar en las listas. Con la plantilla de aplicación Búsqueda de lista en Microsoft Teams SharePoint, los usuarios pueden insertar información de elementos de lista directamente dentro de una conversación de chat para aliviar el cambio de contexto causado al insertar simplemente un vínculo en un chat. La información se inserta como una tarjeta de formato automático fácil de leer, lo que ayuda a los usuarios a mantener la conversación.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Aplicación de búsqueda de lista](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a>Check-ins del personal

Staff Check-ins es una aplicación basada [Power Apps](/powerapps/powerapps-overview) que permite la comunicación de supervisión entre tu empresa y el personal de campo. El personal puede proporcionar fácilmente información crítica de tiempo y actualizaciones de estado de forma programada o ad hoc directamente desde Teams. La aplicación admite la ubicación en tiempo real, fotos, notas, notificaciones de aviso y flujos de trabajo automatizados.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Crear vista de check-in](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a>Encuesta

Survey es una aplicación [](../messaging-extensions/what-are-messaging-extensions.md) de extensión Microsoft Teams de mensajería personalizada que te permite crear una encuesta en un chat o un canal para recopilar datos y obtener información útil. La aplicación se admite en todos los clientes de la plataforma Teams, como escritorio, explorador, iOS y Android, y está lista para su implementación como parte de la Microsoft 365 suscripción.  

[Obtenerlo en GitHub](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Crear encuesta en Teams vista](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a>Recuento de horas 

Un proyecto puede incluir varias tareas y varios proyectos se pueden asignar a los empleados. Los administradores deben comprender el progreso del proyecto durante el tiempo invertido por los empleados en estas tareas. Puede ser una actividad engorrosa, ya que los empleados deben rellenar los partes de horas. La aplicación Time Tally permite a los empleados rellenar sus partes de horas rápidamente, con el dispositivo móvil, y los administradores no tienen que realizar un seguimiento con los empleados en la entrada del parte de horas. Los administradores pueden ver el uso del proyecto en función de los recursos y pueden aprobar o rechazar las entradas. Las notificaciones de aviso se envían para garantizar el cumplimiento del parte de horas. Además, los datos históricos y los usos están disponibles para el análisis.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Recuento de horas](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a>Aprendizaje &#9734;

El aprendizaje es una [aplicación](../messaging-extensions/what-are-messaging-extensions.md) Teams de mensajería personalizada que permite a los usuarios publicar un aprendizaje dentro de un chat o un canal para compartir y mejorar el conocimiento sin conexión. La aplicación se admite en varios clientes Teams plataforma, como escritorio, explorador, iOS y Android. Esta aplicación está lista para la implementación como parte de la Microsoft 365 suscripción.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Crear aprendizaje en Teams vista](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a>Redondeo virtual

Los proveedores de hospitales y de sala de **emergencias hacen muchas rondas** al día. Estas rápidas check-ins en los pacientes están diseñadas para proporcionar una comprobación de estado sobre cómo está el paciente y asegurarse de que se aborde la preocupación del paciente. Aunque el redondeo es una práctica esencial para garantizar que los pacientes están siendo supervisados por varios tipos de proveedores, representan un enorme desagüe en el EPP, ya que para cada visita, de cada proveedor, se usa una máscara nueva y un nuevo conjunto de guantes. Con estas plantillas de aplicación, los trabajadores médicos pueden realizar fácilmente rondas virtualmente, a través de una reunión Microsoft Teams entre el proveedor y el paciente.

También se hace referencia a la solución de redondeo virtual en la Microsoft Health de blog de Ciencias de la [vida.](https://aka.ms/teamsvirtualrounding)

[Obtenerlo en GitHub](https://github.com/SmartterHealth/Virtual-Rounding)

![Redondeo virtual](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a>Administración de visitantes

La aplicación Administración de visitantes permite a su organización y a los empleados administrar de forma fácil y eficaz el proceso de visitantes en el sitio, directamente desde Microsoft Teams. La aplicación permite a los empleados crear solicitudes de visitantes, realizar un seguimiento centralizado de un estado de solicitud a través del panel de visitantes y recibir notificaciones en tiempo real cuando llega un visitante.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="water-cooler-9734"></a>Enfriador de agua &#9734;

Water Cool es una aplicación Teams personalizada que permite a los equipos corporativos crear, invitar y unirse a conversaciones informales entre compañeros de equipo, como las que tienen lugar en el enfriador de agua o la sala de descanso. Use esta plantilla para varios escenarios, como nuevos anuncios no relacionados con proyectos, temas de interés, eventos actuales o conversaciones sobre aficiones. La aplicación proporciona una interfaz fácil para que cualquier persona encuentre una conversación existente o inicie una nueva. Es una base para crear capacidades de comunicación personalizadas dirigidas, lo que fomenta la interacción entre compañeros de trabajo que, de lo contrario, no pueden socializar durante los descansos.    

[Obtenerlo en GitHub](https://github.com/microsoft/csapps-msteams-watercooler)     

![Appscreens de Water Cool](../assets/images/appScreens.gif)    

### <a name="key-features"></a>Características principales

**Página principal del enfriador** de agua: puede examinar las salas existentes en las que los miembros del equipo interactúan en conversaciones existentes con determinadas personas o temas de interés. Las conversaciones activas en la **página principal** muestran un nombre de sala, una descripción breve, una duración de llamada y una imagen de sala. 

![Página principal del enfriador de agua](../assets/images/home-page.png)

**Sala de unirse:** use **la característica Unirse** a la sala para unirse a una conversación en curso inmediatamente. Seleccione **Unirse** a las conversaciones activas para unirse a la sala.

![Sala de unirse](../assets/images/joinRoom.gif)

**Creación de salas:** usa la **característica de creación de** sala para crear una Teams o chat para que todos los asistentes interactúen. Cree salas fácilmente especificando el nombre de la sala, la breve descripción, hasta cinco compañeros como grupo inicial y seleccionando del conjunto proporcionado de imágenes de la sala. 

![Creación de sala](../assets/images/createRoom.gif)

**Buscar sala:** use la característica **Buscar sala** para buscar palabras clave que coincidan con el tema o breves descripciones de conversaciones en curso.

![Buscar conversación](../assets/images/findConversation.gif)

**Invitación del asistente:** use la **característica de** invitación del asistente para invitar a usuarios adicionales después de la creación de la sala. Esto es similar a Teams llamada.

![Invitación de asistente](../assets/images/attendeeInvitation.gif)

**Distintivo de la** aplicación: el icono **del** enfriador de agua del menú izquierdo muestra un distintivo con el número de conversaciones activas visibles desde Teams mientras se usa cualquier aplicación. 

![Distintivo de aplicación](../assets/images/badge.gif)

## <a name="workplace-awards"></a>Workplace Awards

Workplace Awards es una plantilla Teams aplicación que proporciona un marco positivo para fomentar el reconocimiento y fomentar la cultura de la apreciación de los empleados en el lugar de trabajo moderno. La aplicación te permite configurar y administrar un reconocimiento y recompensas de empleados, denominado programa R&R donde los empleados pueden designar y respaldar fácilmente a compañeros y el líder de R&R puede ver las nominaciones enviadas, conceder premios y anunciar destinatarios.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![Tarjeta de nominación de los premios workplace ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Pestaña Lista de reconocimientos de lugares de trabajo](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

Para obtener más información sobre la plantilla de aplicación, consulta [Plantilla de aplicación](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).

## <a name="see-also"></a>Vea también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
