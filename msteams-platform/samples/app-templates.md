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
# <a name="app-templates-for-microsoft-teams"></a>Plantillas de aplicaciones para Microsoft Teams

Las plantillas de aplicación son ejemplos de aplicaciones completas para Microsoft Teams que son de código abierto y están disponibles en GitHub. Cada plantilla de aplicación contiene instrucciones detalladas para implementar e instalar esa aplicación para la organización. También proporciona una aplicación de ejemplo que puedes instalar y empezar a usar inmediatamente. El código fuente completo también está disponible, lo que le permite explorarlo en detalle o bifurcar el código y modificarlo para satisfacer sus requisitos específicos.
Todas las plantillas de aplicación se proporcionan en los términos [de licencia mit.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)
>[!NOTE] 
>You, not Microsoft must license and support apps created from app templates for your users and organizations.

**&#9734; indica las plantillas de aplicación recién publicadas.**

### <a name="key-benefits"></a>Ventajas clave

* **Implemente directamente en la nube:** Todas las plantillas de aplicación incluyen scripts de implementación que le permiten hospedar todos los servicios necesarios en Microsoft Azure o power platform. 
* **Código de ejemplo recomendado:** Las plantillas de la aplicación se ajustan a los procedimientos recomendados en materia de seguridad e infraestructura. Se revisan todos los cambios enviados por la comunidad a las plantillas de la aplicación para garantizar la conformidad.
* **Personalizable y extensible:** Aunque todas las plantillas de aplicación se pueden implementar con una configuración mínima, proporcionamos toda la base de código y los scripts de implementación para que puedas personalizarlas o ampliarlas fácilmente para que se ajusten a tus necesidades únicas.
* **Documentación detallada:** Todas las plantillas de aplicación van acompañadas de documentación completa sobre los pasos de configuración, implementación y arquitectura de soluciones.  

## <a name="adoption-bot-9734"></a>Bot de adopción &#9734;

Bot de adopción es un bot de chat de atención al usuario creado con Power Virtual Agent para Teams (PVA). Puede considerarse como la versión PVA de FAQPlus. Bot de adopción responde a más de 100 preguntas comunes sobre Microsoft 365 y Teams. Puede editar los temas existentes, agregar sus propios temas e ingerir preguntas frecuentes existentes. Si los usuarios necesitan ayuda adicional, el Bot de adopción puede conectarlos a expertos o incluso extenderse para abrir vales de servicio con conectores de flujo premium. Este bot se puede instalar por su cuenta o estar integrado en una aplicación personalizada como el Centro [de adopción.](https://github.com/akporzondek/adoption_hub)

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="appointment-manager-9734"></a>Administrador de &#9734;

Appointment Manager es una plantilla de aplicación de Teams para ayudar a las empresas a crear, administrar y llevar a cabo citas virtuales con consumidores a través de Teams. Las nuevas solicitudes de cita de los consumidores son visibles en los canales de Teams, donde se pueden asignar y reasignar rápidamente al personal de un equipo. Las solicitudes de cita se pueden ver en los niveles de equipo o personal a través de pestañas personalizadas. Cada cita está asociada a una reunión en línea de Teams, por lo que el personal y los consumidores pueden unirse fácilmente a la reunión en el momento programado.

La plantilla de aplicación se integra con Microsoft Bookings para facilitar la administración de citas. Las citas programadas aparecen automáticamente en los calendarios de los miembros del personal asignados y los consumidores reciben notificaciones y avisos de correo electrónico personalizables con vínculos de reunión incrustados.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

![Administrador de citas Overview ](../assets/images/appointment-manager-overview.png)
 ![ Appointment Manager en Teams](../assets/images/appointment-manager-2.png)

## <a name="ask-away"></a>Preguntar fuera

Ask Away es un [bot de Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios llevar a cabo preguntas&A (preguntas y respuestas) en Teams. Con el bot Preguntar, los miembros del equipo pueden enviar y votar por arriba preguntas compartidas por compañeros, lo que permite que los hosts de preguntas&A recopile fácilmente las preguntas más importantes dentro de un canal o chat. El bot se puede usar para realizar una sesión de preguntas en tiempo real&Una sesión en una reunión de Teams y permite a los asistentes enviar preguntas en directo a través del chat.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Vista del cuadro de diálogo emergente de la tabla de clasificación para que los usuarios voten sobre las preguntas](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a>Información de asociados

Associate Insights es una plantilla [de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que permite a los trabajadores de primera línea capturar y enviar directamente la opinión, el sentimiento y la percepción del cliente. Los trabajadores de primera línea suelen ser el primer representante de la compañía en interactuar con los clientes en un punto a uno de contacto. Los equipos empresariales pueden compartir y usar los datos recopilados de forma colaborativa, por ejemplo, a través de una pestaña de Power BI Teams, para mejorar el producto y mejorar la experiencia del cliente.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

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

## <a name="attendance"></a>Asistencia

La aplicación Asistencia es una [pestaña Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que se puede anclar en un equipo. Está diseñado para registrar la presencia, normalmente en configuraciones como entornos de aprendizaje y aprendizaje. Los usuarios pueden marcar o editar la asistencia durante un máximo de 30 días en el pasado y ver informes de asistencia resumidos para un grupo completo o asistentes individuales.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Demostración de la aplicación de asistencia](../assets/images/attendance-app.png)

## <a name="book-a-room"></a>Libro a sala

Book-a-room es un bot de [Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30 (predeterminado), 60 o 90 minutos a partir de la hora actual. El bot Book-a-room tiene ámbitos para conversaciones personales o 1:1.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Demostración de libro a sala](../assets/images/book-a-room.png)

## <a name="building-access"></a>Acceso de creación

Building Access es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que admite la administración de umbrales de ocupación de edificios y normas de distanciamiento social al permitir que los directores de instalaciones administren, realicen un seguimiento e informen de la presencia de los empleados en el sitio. La aplicación, creada con Microsoft [Power Apps](/powerapps/powerapps-overview)y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams y permite a las organizaciones determinar la preparación de la creación, establecer criterios de elegibilidad para el acceso en el sitio y recopilar información para la planeación futura.

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

Celebraciones es una aplicación de Teams que ayuda a los miembros del equipo a celebrar los cumpleaños, aniversarios y otros eventos periódicos. Recuerda ocasiones especiales de todos los miembros del equipo y envía un mensaje descriptivo en todos los equipos seleccionados en el momento de la creación de eventos, para que los miembros del equipo se sientan especiales en su día.

La aplicación proporciona una interfaz sencilla para que todos los miembros del equipo agreguen y visualen personalmente sus eventos y también permite al usuario seleccionar los equipos en los que se comparten los eventos.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a>Lista de comprobación

Lista de comprobación es una aplicación de extensión [de](../messaging-extensions/what-are-messaging-extensions.md) mensajería personalizada de Microsoft Teams que te permite colaborar con tu equipo creando una lista de comprobación compartida en un chat o canal. La aplicación se admite en todos los clientes de plataforma de Teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.  

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Crear lista de comprobación en la vista Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a>Classroom Drop-in &#9734;

Classroom Drop-in es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)que permite a los líderes del sistema encontrar equipos de clase (aulas virtuales) y agregarse a sí mismos u otros a estos equipos de clase durante un período de entrega especificado, según sea necesario. La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate](/power-automate/getting-started)se integra profundamente con Microsoft Teams para garantizar que los institutos educativos puedan optimizar sus operaciones en un entorno de aprendizaje híbrido proporcionando acceso a partes interesadas relevantes para los equipos de clase por requisitos empresariales.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Solicitud de acceso a clases](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a>Comunicador de la empresa

La aplicación Communicator empresa permite a los equipos corporativos crear y enviar mensajes destinados a varios equipos o a un gran número de empleados a través del chat, lo que permite que la organización llegue a los empleados justo donde colaboran. Use esta plantilla para varios escenarios, como anuncios de nuevas iniciativas, incorporación de empleados, aprendizaje y desarrollo modernos o difusión en toda la organización.

La aplicación proporciona una interfaz sencilla para que los usuarios designados creen, obtengan una vista previa, colaboren y envíen mensajes.

Proporciona una base para crear capacidades de comunicación personalizadas dirigidas, como telemetría personalizada, sobre cuántos usuarios han reconocido o interactuado con un mensaje.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator de cuadro de redacción](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a>Búsqueda de grupos de contactos

La aplicación Búsqueda de grupos de contactos proporciona un enfoque práctico y útil para crear, acceder y administrar los grupos de contactos de la organización (anteriormente conocidos como listas de distribución o grupos de comunicación). Los usuarios pueden ver y chatear rápidamente con miembros del grupo, ver el estado de los miembros y crear un chat de grupo con miembros seleccionados en el grupo de contactos, todo dentro del entorno de Teams.

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

## <a name="co-worker-appreciation-9734"></a>Apreciación de compañeros de trabajo &#9734;

Con la plantilla de apreciación de compañeros de trabajo en Microsoft Teams, los usuarios pueden reconocer los logros de sus compañeros en el contexto de Teams. Cuando los compañeros de trabajo seleccionan recompensar a un compañero, los destinatarios y otros miembros del equipo se etiquetan en una conversación de canal y reciben una notificación sobre los detalles de la concesión del canal. Los galardones se registran en la aplicación teams, que es segura, portátil y fácilmente compartible. Esto se puede considerar como la versión basada en PowerApps de la plantilla de la aplicación Open Badges, con una tabla de clasificación.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![General](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a>CrowdSourcer

CrowdSourcer es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona a los equipos información consultada procedente de forma colaborativa de miembros del grupo. Es una excelente manera de responder a las preguntas más frecuentes al tiempo que permite a los participantes participar activamente y contribuir a un recurso de información divertido y útil.

[Obtenerlo en Github](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interacción entre usuarios finales de Crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a>Adhesivos personalizados

La autoexpresión es fundamental para una cultura de equipo en buen estado. Esta plantilla de aplicación es una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) que permite a los usuarios usar adhesivos y GIF personalizados dentro de Microsoft Teams. Esta plantilla proporciona una experiencia de configuración sencilla basada en web en la que cualquier persona con acceso a la configuración puede cargar los GIF/adhesivos/imágenes que desean que tengan sus usuarios finales, lo que permite a todo el equipo usar cualquier conjunto de adhesivos que elija.

Esta aplicación también permite compartir fácilmente imágenes/GIF/adhesivos entre equipos sin necesidad de tener acceso a sitios de SharePoint o canales individuales como mecanismos de almacenamiento y uso compartido. Por ejemplo, los equipos de productos pueden compartir fácilmente imágenes de producto y GIF a redes sociales, equipos de marketing y ventas mediante programación. También se puede extender esta aplicación desencadenando un flujo de notificación a equipos o individuos específicos cuando se hacen disponibles nuevas imágenes/GIF.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Aplicación Stickers](../assets/images/stickers.png)

## <a name="employee-ideas"></a>Ideas de los empleados

La aplicación Ideas para empleados es la versión de PowerApps de la plantilla de aplicación Great Ideas basada en Azure. La aplicación permite a los usuarios de Teams configurar y configurar una campaña de ideas. Una campaña de ideas es una categoría para agrupar ideas en torno a temas comunes.

Los usuarios de Teams también pueden realizar las siguientes actividades:
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

E-Prescriptions es una aplicación basada en [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)que mejora la telemedicina y el cuidado virtual automatizando el proceso de emisión de recetas electrónicas a los pacientes. Los profesionales médicos pueden revisar rápidamente las citas, generar recetas electrónicas y enviar correos electrónicos con datos adjuntos de la receta electrónica a los pacientes directamente en la plataforma teams.

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

La formación de los empleados es una aplicación de Microsoft Teams que permite a los organizadores publicar, realizar un seguimiento y promover fácilmente eventos de aprendizaje y aprendizaje para su organización.  Con la aplicación, los organizadores de eventos pueden enviar avisos y notificaciones a los registradores de eventos y los empleados pueden indicar interés en los próximos eventos, mantenerse actualizados en eventos actuales y compartir detalles de eventos con compañeros a través de la extensión de mensajería de Teams.

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

Expert Finder es un [bot de Microsoft Teams](../bots/what-are-bots.md) que identifica miembros específicos de la organización en función de sus aptitudes, intereses y atributos educativos. Los miembros encuentran expertos dentro de una organización que coinciden con una búsqueda de palabras clave de perfiles de usuario de Azure Active Directory.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Demostración de resultados de búsqueda del Buscador de expertos](../assets/images/expert-finder.png)

## <a name="faq-plus"></a>Preguntas más frecuentes Plus

Preguntas conversacionales&Bots son una forma sencilla de proporcionar respuestas a las preguntas más frecuentes de los usuarios. Sin embargo, la mayoría de los bots no interactúan con los usuarios de forma significativa porque no hay ningún humano en el bucle cuando se produce un error en el bot. Faq bot is a friendly Q&A bot that brings a human in the loop when it is unable to help. Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos. Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde el propio equipo.

> [!NOTE]
> La versión más reciente de **FAQ Plus** admite resoluciones de preguntas&A al permitir a un equipo de expertos completar lo siguiente:
>
> &#x2714; agregar nuevas preguntas&Como directamente a la base de conocimientos mediante extensiones de mensaje.
>
> &#x2714; Editar y eliminar preguntas&Pares agregados por un bot.
>
> &#x2714; seguimiento del historial de revisiones de Q&As.
>
> &#x2714; configurar una respuesta con detalles adicionales para mostrar como una [tarjeta adaptable.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)
>
[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif de preguntas más frecuentes](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app-9734"></a>Obtener la aplicación de soporte &#9734;

Las organizaciones que usan Microsoft Teams pueden usar la aplicación Obtener soporte técnico para permitir que cualquier conjunto de usuarios solicite asistencia a los supervisores. Esta aplicación incluye varias características, como:
-   Solicitar asistencia en distintas categorías desde una Power App
-   Notificaciones enviadas a los solicitantes para informarles de quién ha sido asignado 
-   Notificaciones enviadas a supervisores asignados para informarles de quién necesita asistencia 
-   Análisis de escalaciones y patrones en SharePoint y PowerBI

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Obtener gif de soporte técnico](../assets/images/get-support.gif)

## <a name="goal-tracker"></a>Rastreador de objetivos

La aplicación Rastreador de objetivos es una solución completa para que su organización admita el establecimiento de objetivos, la observación del progreso y el reconocimiento del éxito en Microsoft Teams. La aplicación permite a los usuarios establecer, realizar un seguimiento y actualizar objetivos en un nivel profesional, personal y de equipo. Los miembros del equipo también reciben avisos oportunos y actualizaciones de estado para mantenerse centrados y mantenerse al día.

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

Actividades de grupo es una aplicación de Microsoft Teams que facilita a los propietarios de equipos crear rápidamente grupos de actividades y administrar flujos de trabajo de colaboración en el contexto de Microsoft Teams. Los autores de actividades están habilitados para crear actividades, distribuir aleatoriamente miembros del equipo en grupos y, opcionalmente, hacer que el bot envíe avisos hasta que se completen las actividades.

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

## <a name="grow-your-skills"></a>Aumentar sus habilidades

La aplicación Crecer tus habilidades admite el crecimiento y el desarrollo profesionales, ya que permite a los empleados contribuir a proyectos complementarios para tu organización al mismo tiempo que aprenden nuevas habilidades. Los empleados pueden usar la aplicación para buscar oportunidades que satisfagan sus intereses, disfrutar de una colaboración significativa con compañeros y adquirir nuevos niveles de experiencia y capacidades, todo dentro del entorno de Teams.

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

Bot de soporte técnico de RECURSOS es una pregunta&Un bot que lleva a un profesional/experto de soporte técnico del equipo de recursos humanos en el bucle cuando no puede ayudar. Se puede hacer una pregunta al bot y el bot responde con una respuesta si está contenido en la base de conocimientos. Si no es así, el bot permite al usuario enviar una consulta que, a continuación, se publica en un equipo preconfigurado de expertos que ayudan a proporcionar soporte actuando sobre las notificaciones desde el propio equipo. Además, el bot sugiere vínculos a las preguntas y directivas de RECURSOS humanos recomendadas mediante la búsqueda de etiquetas preconfiguradas en la pregunta. Estos iconos también se pueden encontrar en la pestaña asociada como una referencia rápida. El soporte de recursos humanos funciona bien para QnA de peso ligero y para proporcionar soporte rápido al iniciar nuevos proyectos o iniciativas en la organización.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Soporte de Recursos Humanos](../assets/images/expert-user.png)

## <a name="icebreaker"></a>Rompehielo

Icebreaker es un [bot de Microsoft Teams](../bots/what-are-bots.md) que ayuda a tu equipo a acercarse emparejando dos miembros del equipo aleatorios cada semana para reunirse. El bot facilita la programación al sugerir automáticamente horas libres que funcionen para ambos miembros. Fortalezca las conexiones personales y cree una comunidad estrechamente unida con esta aplicación.

Además de fomentar las conexiones personales en todo el equipo, la aplicación Icebreaker puede ayudar a cultivar comunidades basadas en intereses dentro de la organización. Por ejemplo, puedes usar esta aplicación para un grupo de interés de DevOps para ayudar a que las ideas y los procedimientos recomendados se extienda orgánicamente en toda la organización.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Aplicación Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a>Incentivos

Incentives es una plantilla [de Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) que administra y realiza un seguimiento de la participación de los empleados en actividades designadas, como cursos e iniciativas de administración de cambios. Los administradores usan la aplicación para establecer actividades designadas, asignar puntos para su finalización y especificar los niveles de puntos de elegibilidad necesarios para las recompensas. Los empleados usan la aplicación para ver sus puntos acumulados y, al alcanzar la elegibilidad, solicitar y reclamar recompensas canjeables.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Demostración de aplicaciones de incentivos](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a>Reportero de incidentes

Incident Reporter es un [bot de Microsoft Teams](../bots/what-are-bots.md)  que optimiza la administración de incidentes en su organización. El bot facilita la recopilación automatizada de datos de incidentes, informes de incidentes personalizados, notificaciones relevantes para las partes interesadas y seguimiento de incidentes de un extremo a otro.

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

## <a name="inspection-9734"></a>Inspección &#9734;

 Inspección es una aplicación de Microsoft Teams que permite a los trabajadores de primera línea inspeccionar cualquier cosa, desde ubicaciones hasta activos y equipos. Por ejemplo, una tienda comercial, una planta de fabricación o vehículos y máquinas. Hay dos aplicaciones en esta solución, cada una destinada a diferentes tipos de usuarios.

La aplicación permite a los trabajadores de primera línea inspeccionar un activo o área, administrar la calidad de los productos y servicios o mantener la seguridad en el lugar de trabajo. Facilita la comunicación entre los miembros del equipo para solucionar los problemas encontrados durante la inspección. La aplicación proporciona informes sencillos para que los administradores agilicen la resolución de problemas y resalten las tendencias.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Introducción a la inspección](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a>Informes de problemas

La aplicación De informes de problemas permite a los empleados y administradores generar y administrar problemas. Consta de dos aplicaciones, Aplicación de informes de problemas para informar y Aplicación Administrar problemas para administrar problemas.

Los jefes de equipo usan la aplicación Administrar problemas para configurar la experiencia de la aplicación, incluido el canal en el que la aplicación crea los mensajes de Microsoft Teams y las tareas de Planner. Los administradores también usan la aplicación para crear formularios de plantilla para recopilar detalles cuando un usuario informa de un problema. Por ejemplo, revise, edite o elimine formularios de plantilla de problema. La aplicación también se puede usar para revisar los problemas del equipo, informar sobre el historial de problemas y administrar eficazmente la resolución de problemas.

Los empleados usan la aplicación De informes de problemas para registrar problemas y detalles necesarios para resolverlos. La aplicación también se usa para modificar y resolver problemas existentes y obtener una vista de alto nivel de problemas individuales o de equipo.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Vista de equipo de informes de problemas](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a>Incorporación de nuevos empleados 

La incorporación de nuevos empleados es una solución integrada de incorporación de nuevos empleados de Microsoft Teams y [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) que permite a su organización proporcionar una experiencia de incorporación coherente y de alta calidad para los empleados en su viaje de nueva contratación. Los equipos de recursos humanos y los administradores de contratación pueden usar la aplicación para proporcionar información relevante a lo largo del proceso de orientación e inducción, así como para que los nuevos empleados compartan comentarios, proporcionen introducciones y completen tareas de incorporación.

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

Open Badges es una aplicación de Microsoft Teams que permite a los usuarios obtener distintivos de credenciales de aprendizaje digital en el contexto de Teams y compartirlos en todas partes. Con las funcionalidades de la entidad emisora de distintivos digitales de terceros, [Badgr](https://badgr.org/), los distintivos concedidos se registran en el perfil badgr de un destinatario y están disponibles para crear y compartir una imagen enriquecida de los recorridos de aprendizaje de por vida.

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

Poll es una aplicación de extensión de mensajería personalizada de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que te permite crear y enviar rápidamente sondeos en un chat o un canal para recopilar opiniones y preferencias del equipo. La aplicación se admite en todos los clientes de plataforma de Teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Crear sondeo en la vista Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a>Respuestas rápidas

Respuestas rápidas es una aplicación de Microsoft Teams que ofrece una solución sólida para responder eficazmente a las preguntas más frecuentes (preguntas frecuentes) de los usuarios. En lugar de responder a cada consulta de forma manual y continua, la aplicación compilará una biblioteca de respuestas para una experiencia de usuario interactiva a través de extensiones de [mensajería de](../messaging-extensions/what-are-messaging-extensions.md)Teams .

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Vista de ejemplo de las respuestas](../assets/images/quick-responses.png)

## <a name="rapid-assist"></a>Asistencia rápida

Rapid Assist es una aplicación basada en Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) que permite a los asociados que se enfrentan al cliente conectarse rápidamente con los expertos para obtener respuestas rápidas, buscar información, realizar un seguimiento de las solicitudes abiertas y permitir que los expertos reciban notificaciones para obtener rápidamente una llamada para ayudar a responder preguntas. La aplicación creada con Microsoft [Power Apps](/powerapps/powerapps-overview) y [Power Automate,](/power-automate/getting-started)se integra profundamente con Microsoft Teams para permitir que las organizaciones conecten fácilmente a los trabajadores de primera línea con vínculos corporativos para resolver las consultas de los clientes y ofrecer una excelente experiencia de cliente. 

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

Reflect es una aplicación de extensión de mensajería personalizada de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) que proporciona un recurso seguro e inclusivo para que los miembros del equipo compartan el estado de su bienestar emocional con compañeros o jefes de grupo directamente en Teams. La aplicación está disponible en chats de canal, grupo, reunión y 1:1 y la respuesta de la entrada se puede establecer en pública, privada a remitente o totalmente anónima.

[Obtenerlo en GitHub](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    **Sondeo de bienestar**
    
    ![Reflejar sondeo de usuarios de aplicaciones](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a>Soporte remoto

El soporte remoto es un [bot de Microsoft Teams](../bots/what-are-bots.md) que proporciona una interfaz centrada entre los solicitantes de soporte técnico de toda la organización y el equipo de soporte técnico interno.  Los usuarios finales pueden enviar, editar o retirar solicitudes de soporte técnico y el equipo de soporte técnico puede responder, administrar y actualizar solicitudes en toda la plataforma de Teams.

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

Request-a-team es una aplicación de Microsoft Teams que optimiza la creación de nuevos equipos para su organización empresarial. La aplicación admite la estandarización y los procedimientos recomendados al crear nuevas instancias de equipo mediante la integración de un formulario de solicitud guiado por asistente, un proceso de aprobación incrustado, un panel de estado de solicitud y compilaciones automatizadas de equipo.

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

Scrums para canales es una aplicación auxiliar de scrum que permite a los usuarios programar y ejecutar scrums en canales de Microsoft Teams. La aplicación es ideal para equipos remotos y equipos formados por miembros de distintas ubicaciones geográficas y zonas horarias para compartir actualizaciones diarias y garantizar la participación en reuniones de soporte de scrum.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> Para realizar reuniones de scrum en un chat de grupo, consulta nuestra plantilla de aplicación [Scrums for Group Chat.](#scrums-for-group-chat)

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
> La plantilla de aplicación Estado de Scrums se ha actualizado y ahora es Scrums para chat en grupo.

Scrums for Group Chat es un asistente de scrum de apoyo que permite a los miembros del chat de grupo ejecutar reuniones de soporte asincrónicas y compartir fácilmente sus actualizaciones diarias. Permite a todos los miembros del chat de grupo contribuir al scrum y ver las actualizaciones realizadas por otros usuarios en el scrum en ejecución.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Demostración de Scrums para chat en grupo](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a>Compartir ahora 

La aplicación Compartir ahora promueve el intercambio positivo de información entre compañeros al permitir que los usuarios compartan fácilmente contenido en el entorno de Teams. Los usuarios interactúan con la aplicación para compartir elementos de interés con los miembros del equipo, descubrir nuevo contenido compartido, establecer preferencias y favoritos de marcadores para su lectura posterior.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Seleccionar vista de contenido](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a>Búsqueda de lista de SharePoint

La colaboración en Microsoft Teams suele hacer referencia a la información contenida en los elementos de una lista de SharePoint. Simplemente pegar un vínculo al elemento en cuestión obliga a todos a cambiar el contexto de la conversación, buscar la información necesaria y, a continuación, volver a Teams para continuar la conversación. A medida que la conversación continúa normalmente, las personas tendrán que volver al elemento de referencia varias veces para comprobar nuevos comentarios y actualizar sus memorias de la información contenida en el elemento. Este cambio de contexto crea una barrera para una colaboración fluida y es una receta para las cosas que pasan por las grietas.

Para ayudar a aliviar este dolor, estamos encantados de traerte la plantilla de aplicación Búsqueda de lista. Millones de usuarios usan SharePoint para crear algunos de los flujos de trabajo principales de sus organizaciones. Sin embargo, colaborar en las listas puede ser especialmente tedioso. Con la plantilla de aplicación Búsqueda de lista en Microsoft Teams, los usuarios pueden insertar información de elementos de lista de SharePoint directamente dentro de una conversación de chat para aliviar el cambio de contexto causado al insertar simplemente un vínculo en un chat. La información se inserta como una tarjeta de formato automático fácil de leer, lo que ayuda a los usuarios a mantener la conversación.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Aplicación de búsqueda de lista](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a>Check-ins del personal

Staff Check-ins es una aplicación basada en [Power Apps](/powerapps/powerapps-overview)que permite la comunicación de supervisión entre tu empresa y el personal de campo. El personal puede proporcionar fácilmente información crítica de tiempo y actualizaciones de estado de forma programada o ad hoc directamente desde Teams. La aplicación admite la ubicación en tiempo real, fotos y notas, así como notificaciones de aviso y flujos de trabajo automatizados.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Crear vista de check-in](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a>Encuesta

Survey es una aplicación de extensión de mensajería de Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) personalizada que te permite crear una encuesta en un chat o un canal para recopilar datos y obtener información útil.  La aplicación se admite en todos los clientes de plataforma de Teams (escritorio, explorador, iOS y Android) y está lista para su implementación como parte de su suscripción a Microsoft 365.  

[Obtenerlo en GitHub](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Crear encuesta en la vista Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally-9734"></a>Time Tally &#9734;

Un proyecto puede incluir varias tareas y varios proyectos se pueden asignar a los empleados. Los administradores deben comprender el progreso del proyecto durante el tiempo invertido por los empleados en estas tareas. Puede ser una actividad engorrosa, ya que los empleados deben rellenar los partes de horas. La aplicación Time Tally permite a los empleados rellenar sus partes de horas rápidamente, con el dispositivo móvil, y los administradores no tienen que realizar un seguimiento con los empleados en la entrada del parte de horas. Los administradores pueden ver el uso del proyecto en función de los recursos y pueden aprobar o rechazar las entradas. Las notificaciones de aviso se envían para garantizar el cumplimiento del parte de horas. Además, los datos históricos y los usos están disponibles para el análisis.

[Obtenerlo en GitHub](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Recuento de horas](../assets/images/11zon_gif.gif)


## <a name="virtual-rounding"></a>Redondeo virtual

Los proveedores de hospitales y de sala de emergencias hacen decenas y, a menudo, cientos de **rondas** al día. Estas rápidas check-ins en los pacientes están diseñadas para proporcionar una comprobación de estado sobre cómo está el paciente y asegurarse de que se aborde la preocupación del paciente. Aunque el redondeo es una práctica esencial para garantizar que los pacientes están siendo supervisados por varios tipos de proveedores, representan un enorme desagüe en el EPP, ya que para cada visita, de cada proveedor, se debe usar una máscara nueva y un nuevo conjunto de guantes. Con estas plantillas de aplicación, los trabajadores médicos pueden realizar fácilmente rondas virtualmente, a través de una reunión de Microsoft Teams entre el proveedor y el paciente.

También se hace referencia a la solución de redondeo virtual en la entrada de [blog](https://aka.ms/teamsvirtualrounding)Microsoft Health and Life Sciences .

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

## <a name="workplace-awards"></a>Workplace Awards

Workplace Awards es una plantilla de aplicación de Teams que proporciona un marco positivo para fomentar el reconocimiento y fomentar la cultura de la apreciación de los empleados en el lugar de trabajo moderno. La aplicación te permite configurar y administrar un programa de reconocimiento y recompensas de empleados (R&R) en el que los empleados pueden designar y aprobar fácilmente a los compañeros y el líder de R&R puede ver las nominaciones enviadas, conceder premios y anunciar destinatarios.

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

¿Tienes una idea de una plantilla de aplicación que quieras ver? [Por favor, háganos saber](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).
