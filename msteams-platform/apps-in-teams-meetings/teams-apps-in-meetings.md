---
title: Aplicaciones en reuniones Teams
author: laujan
description: visión general de las aplicaciones en Teams reuniones basadas en el papel del participante y el usuario
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: equipos aplicaciones reuniones usuario participante rol api
ms.openlocfilehash: c5419565d8defd03a3dcfcc5b05b9517cb4269e2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565930"
---
# <a name="apps-in-teams-meetings"></a>Aplicaciones en reuniones Teams

Las reuniones permiten la colaboración, la asociación, la comunicación informada y la retroalimentación compartida en un foro inclusivo y activo. La aplicación de reunión puede ofrecer una experiencia de usuario para cada etapa del ciclo de vida de la reunión, incluida la experiencia de la aplicación previa a la reunión, en la reunión y después de la reunión, en función del estado del asistente.

Teams usuarios finales pueden acceder a aplicaciones durante las reuniones mediante la galería de pestañas, por ejemplo:

* Pre-etapa de una tabla kanban
* Inicie un diálogo procesable en la reunión
* Crear una encuesta posterior a la reunión

La extensibilidad de la aplicación de reunión de Teams se basa en los siguientes conceptos:

✔ Ciclo de vida de reunión tiene etapas como antes, durante y después del período de tiempo de reunión.  
✔ Roles de participante en una reunión, como organizador de reuniones, presentador o asistente.  
✔ tipos de usuario en una reunión como el usuario de Teams en el inquilino, invitado, federado o anónimo.

En este artículo se describe información sobre el ciclo de vida de la reunión y cómo integrar pestañas, bots y extensiones de mensajería en la reunión. También le permite identificar roles de participante y también usar diferentes tipos de usuario para realizar tareas.

> [!NOTE]
> Para trabajar con las características de extensibilidad de la aplicación de reunión, debe tener los permisos adecuados.

### <a name="meeting-lifecycle"></a>Ciclo de vida de reunión

El ciclo de vida de la reunión consiste en experiencia previa a la reunión, en la reunión y en la aplicación posterior a la reunión. Puede integrar pestañas, bots y extensiones de mensajería en cada etapa del ciclo de vida de la reunión.

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a>Integre pestañas en el ciclo de vida de la reunión

Las pestañas permiten a los miembros del equipo acceder a servicios y contenido en un espacio específico dentro de un canal o chat. Esto permite al equipo trabajar directamente con pestañas y tener conversaciones sobre las herramientas y los datos disponibles dentro de las pestañas. En Teams reunión, los usuarios pueden agregar una pestaña seleccionando más <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>, y elegir la aplicación que quieren instalar como una pestaña.

> [!IMPORTANT]
> Si ha integrado una pestaña con la reunión, la aplicación debe seguir el [flujo de autenticación de inicio de sesión único (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) Teams para las pestañas.

> [!NOTE]
> * Los clientes móviles solo admiten pestañas en etapas previas y posteriores a la reunión. Las experiencias en la reunión que se encuentran en el cuadro de diálogo y el panel en la reunión actualmente no están disponibles en el móvil.
> * Las aplicaciones solo se admiten en reuniones programadas privadas.

### <a name="pre-meeting-app-experience"></a>Experiencia de la aplicación previa a la reunión

**Experiencia previa a la reunión:**

![experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

**Pestaña previa a la reunión:**

![vista de pestañas previa a la reunión](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔ Usuarios con permiso son usuarios que pueden agregar aplicaciones a una reunión durante diferentes etapas del ciclo de vida de la reunión. Estos usuarios pueden agregar aplicaciones a una reunión a través de la galería de pestañas de dos maneras:

   * Mediante la pestaña **Detalles** del formulario de programación Teams.

   * Uso de la pestaña **Chat** de la reunión en una reunión existente.

✔ aplicaciones de pestañas son accesibles en las reuniones **Detalles** y **chats** páginas mediante un botón más ➕.

✔ diseño de tabulación debe estar en un estado organizado si hay más de diez encuestas o encuestas.

### <a name="in-meeting-app-experience"></a>Experiencia de la aplicación en la reunión

✔ Aplicaciones de reunión se hospedan en la barra superior de la ventana de chat y como experiencia de pestaña en la reunión mediante la pestaña en la reunión. Cuando los usuarios agregan una pestaña a una reunión a través de la galería de pestañas, se muestran las aplicaciones que se encuentran durante las experiencias **de reunión.**

✔ usuarios con permiso pueden agregar aplicaciones durante la reunión.

✔ Cuando se cargan en el contexto de una reunión, las aplicaciones pueden aprovechar el SDK de cliente Teams para tener acceso `meetingId` a la versión y representar adecuadamente la `userMri` `frameContext` experiencia.

✔ Exportar un resultado de una encuesta o encuesta notifica a los usuarios que los resultados se descargaron correctamente.

✔ Una aplicación está visible en una reunión Teams en el panel lateral o en el cuadro de diálogo en la reunión. Utilice el cuadro de diálogo en la reunión para mostrar contenido procesable para los participantes de la reunión. Para obtener más información, consulte [Crear aplicaciones para reuniones de Teams.](create-apps-for-teams-meetings.md)

   > [!NOTE]
   > El manifiesto de la aplicación especifica que la pestaña está [optimizada para el panel lateral,](create-apps-for-teams-meetings.md#during-a-meeting)es donde se muestra. También puede ser parte de una experiencia de bandeja compartida, sujeto a las directrices de diseño especificadas.

Las siguientes imágenes muestran la aplicación como un cuadro de diálogo en la reunión y como un panel lateral independiente:

![Experiencia en el encuentro](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Vista de diálogo en la reunión](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a>Diálogo procesable en la reunión para los usuarios

![Vista de diálogo](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>Experiencia de la aplicación después de la reunión

![Vista posterior a la reunión](../assets/images/apps-in-meetings/PostMeeting.png)

✔ El escenario de la aplicación posterior a la reunión es similar a la experiencia actual posterior a la reunión con la ventaja añadida de tener pestañas que existen dentro de la superficie.

✔ Los usuarios con permiso pueden agregar aplicaciones desde la galería de pestañas a una reunión mediante la pestaña **Detalles** del formulario de programación Teams y la pestaña **Chat** de la reunión en una reunión existente.

✔ diseño de tabulación debe organizarse cuando hay más de diez encuestas o encuestas.

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>Integrar bots en el ciclo de vida de la reunión

Para la implementación de bots, comience con [crear un bot](../build-your-first-app/build-bot.md) y, a continuación, continúe con crear aplicaciones para reuniones [Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>Integrar extensiones de mensajería en el ciclo de vida de la reunión

Para la implementación de extensiones de mensajería, comience con [crear una extensión de mensajería](../messaging-extensions/how-to/create-messaging-extension.md) y, a continuación, continúe con crear aplicaciones para reuniones [Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)

## <a name="participant-roles-and-user-types-in-a-meeting"></a>Roles de participante y tipos de usuario en una reunión

![Participantes en una reunión](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>Funciones participantes

La configuración predeterminada de los participantes viene determinada por el administrador de TI de una organización. Los siguientes son los roles participantes en una reunión:

* **Organizador**: El organizador programa una reunión, establece las opciones de la reunión, asigna roles de reunión e inicia la reunión. Solo los usuarios con una cuenta M365 con una licencia de Teams pueden ser organizadores y controlar los permisos de asistente. Un organizador de reuniones puede cambiar la configuración de una reunión específica. Los organizadores pueden realizar estos cambios en la página web **de opciones de reunión.**
* **Presentador**: Los presentadores tienen las mismas capacidades que el organizador. Sin embargo, un presentador no puede quitar un organizador de la sesión ni modificar las opciones de reunión para la sesión. De forma predeterminada, los participantes que se unen a una reunión tienen el rol de presentador.
* **Asistente**: Un asistente es un usuario que ha sido invitado a asistir a una reunión pero que no está autorizado a actuar como presentador. Los asistentes pueden interactuar con otros miembros de la reunión, pero no pueden administrar ninguna de las configuraciones de la reunión ni compartir contenido.

Solo un organizador o presentador puede agregar, quitar o desinstalar aplicaciones. Solo el organizador o presentador puede crear encuestas en una reunión.

Para obtener más información, consulte [roles en una reunión Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

Puede acceder a la página  **Opciones de reunión** de la siguiente manera:

* En Teams, vaya al logotipo **calendario calendario,** seleccione una reunión y, a ![ ](../assets/images/apps-in-meetings/calendar-logo.png) continuación, **Opciones de reunión.**

* En una invitación a la reunión, seleccione **Opciones de reunión**.

* Durante una reunión, seleccione **Mostrar a los participantes** mostrar el icono de los participantes en los controles de la ![ ](../assets/images/apps-in-meetings/show-participants.png) reunión. A continuación, encima de la lista de participantes, elija **Administrar permisos**.

### <a name="user-types"></a>Tipos de usuario

> [!NOTE]
> Los usuarios con tipos de usuario específicos asignados pueden unirse a las reuniones y asumir uno de los roles de participante descritos en [los roles de participante.](#participant-roles) El tipo de usuario no se incluye en la API **getParticipantRole.**

Los siguientes tipos de usuario identifican lo que cada usuario puede hacer y a qué puede acceder:

* **En el inquilino:** los usuarios en el inquilino pertenecen a la organización y tienen credenciales en Azure Active Directory (AAD) para el inquilino. Por lo general, son empleados a tiempo completo, in situ o remotos. Un usuario en el inquilino puede ser un organizador, presentador o asistente.
* **Invitado**: Un invitado es un participante de otra organización invitado a acceder a Teams u otros recursos en el inquilino de la organización. Los invitados se agregan al AAD de su organización y tienen las mismas capacidades de Teams que un miembro nativo del equipo con acceso a chats de equipo, reuniones y archivos. Un usuario invitado puede ser un organizador, presentador o asistente. Para obtener más información, consulte [acceso de invitados en Teams](/microsoftteams/guest-access).
* **Federado o externo:** un usuario federado es un usuario externo Teams de otra organización que ha sido invitado a unirse a una reunión. Estos usuarios tienen credenciales válidas con socios federados y están autorizados por Teams. No tienen acceso a sus equipos u otros recursos compartidos de su organización. El acceso de invitados es una mejor opción para que los usuarios externos tengan acceso a equipos y canales. Para obtener más información, consulte [Administrar el acceso externo en Teams](/microsoftteams/manage-external-access).
* **Anónimo**: Los usuarios anónimos no tienen una identidad AAD y no están federados con un inquilino. El participante anónimo es como un usuario externo, pero su identidad no se proyecta en la reunión. Un usuario anónimo no puede ser un organizador, pero puede ser un presentador o un asistente.

> [!NOTE]
> Los usuarios anónimos heredan la directiva de permisos de aplicación de nivel de usuario predeterminada global. Para obtener más información, consulte [Administrar aplicaciones](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).

En la tabla siguiente se proporcionan los tipos de usuario y a qué características puede acceder cada usuario:

| Tipo de usuario | Pestañas | Bots | Extensiones de mensajería | Tarjetas adaptables | Módulos de tareas | Diálogo en la reunión |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Usuario anónimo | No disponible | No disponible | No disponible | Se permiten interacciones en el chat de la reunión. | Se permiten interacciones en el chat de la reunión desde una tarjeta adaptable. | No disponible |
| Invitado que forma parte del inquilino AAD | Se permite la interacción. No se permiten la creación, actualización y eliminación. | No disponible | No disponible | Se permiten interacciones en el chat de la reunión. | Se permiten interacciones en el chat de la reunión desde una tarjeta adaptable. | Disponible |
| federado | No disponible | No disponible | No disponible | No disponible | No disponible | No disponible |

## <a name="see-also"></a>Vea también

* [Tab](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [Bot](../bots/what-are-bots.md)
* [Extensión de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Diseño de la aplicación](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una aplicación](create-apps-for-teams-meetings.md)
