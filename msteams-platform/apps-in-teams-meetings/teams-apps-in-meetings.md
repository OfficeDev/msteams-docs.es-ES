---
title: Aplicaciones en reuniones de Teams
author: laujan
description: información general sobre las aplicaciones en reuniones de Teams basadas en el rol de participante y usuario
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: 29a24b70921e51d63d804e7a3edd901f607d3148
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018386"
---
# <a name="apps-in-teams-meetings"></a>Aplicaciones en reuniones de Teams

Las reuniones permiten la colaboración, la asociación, la comunicación informada y los comentarios compartidos en un foro inclusivo y activo. La aplicación de reunión puede ofrecer una experiencia de usuario para cada fase del ciclo de vida de la reunión, incluida la experiencia de la aplicación previa, en la reunión y posterior a la reunión, según el estado del asistente.

Los usuarios finales de Teams pueden acceder a las aplicaciones durante las reuniones mediante la galería de pestañas, por ejemplo:

* Preescalo de un panel de Kanban
* Iniciar un cuadro de diálogo de acción en la reunión
* Crear un sondeo posterior a la reunión

La extensibilidad de la aplicación de reunión de Teams se basa en los siguientes conceptos:

✔ ciclo de vida de la reunión tiene fases como antes, durante y después del período de tiempo de la reunión.  
✔ roles de participante en una reunión, como organizador de la reunión, moderador o asistente.  
✔ usuarios en una reunión, como el usuario de Teams en el inquilino, invitado, federado o anónimo.

En este artículo se describe información sobre el ciclo de vida de la reunión y cómo integrar pestañas, bots y extensiones de mensajería en la reunión. También permite identificar roles de participantes y también usar diferentes tipos de usuario para realizar tareas.

> [!NOTE]
> Para trabajar con las características de extensibilidad de la aplicación de reunión, debe tener los permisos adecuados.

### <a name="meeting-lifecycle"></a>Ciclo de vida de la reunión

El ciclo de vida de la reunión consiste en la experiencia de la aplicación previa a la reunión, en la reunión y posterior a la reunión. Puede integrar pestañas, bots y extensiones de mensajería en cada fase del ciclo de vida de la reunión.

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a>Integrar pestañas en el ciclo de vida de la reunión

Las pestañas permiten a los miembros del equipo tener acceso a servicios y contenido en un espacio específico dentro de un canal o chat. Esto permite al equipo trabajar directamente con pestañas y tener conversaciones sobre las herramientas y los datos disponibles en las pestañas. En la reunión de Teams, los usuarios pueden agregar una pestaña seleccionando más <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>, y elegir la aplicación que quieren instalar como pestaña.

> [!IMPORTANT]
> Si has integrado una pestaña con la reunión, la aplicación debe seguir el flujo de autenticación de inicio de sesión único [(SSO)](../tabs/how-to/authentication/auth-aad-sso.md) de Teams para las pestañas.

> [!NOTE]
> * Los clientes móviles solo admiten pestañas en fases de reunión previas y posteriores. Las experiencias en la reunión que son el cuadro de diálogo y el panel en la reunión actualmente no están disponibles en dispositivos móviles.
> * Las aplicaciones solo se admiten en reuniones privadas programadas.

### <a name="pre-meeting-app-experience"></a>Experiencia de la aplicación previa a la reunión

**Experiencia previa a la reunión:**

![experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

**Pestaña Antes de la reunión:**

![vista de pestaña previa a la reunión](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔ usuarios con permisos son usuarios que pueden agregar aplicaciones a una reunión durante diferentes etapas del ciclo de vida de la reunión. Estos usuarios pueden agregar aplicaciones a una reunión a través de la galería de pestañas de dos maneras:

   * Mediante la **pestaña Detalles** del formulario de programación de Teams.

   * Uso de la **pestaña Chat de** reunión en una reunión existente.

✔ las aplicaciones tab son **accesibles** en las páginas detalles de reuniones y **chats** con un botón más ➕ sesión.

✔ diseño de tabulación debe estar en un estado organizado si hay más de diez sondeos o encuestas.

### <a name="in-meeting-app-experience"></a>Experiencia de la aplicación en la reunión

✔ las aplicaciones de reunión se hospedan en la barra superior superior de la ventana de chat y como experiencia de pestaña en la reunión mediante la pestaña en la reunión. Cuando los usuarios agregan una pestaña a una reunión a través de la galería de pestañas, se muestran las aplicaciones que se **encuentran durante las experiencias** de reunión.

✔ usuarios con permisos pueden agregar aplicaciones mientras están en la reunión.

✔ Cuando se carga en el contexto de una reunión, las aplicaciones pueden aprovechar el SDK de cliente de Teams para obtener acceso a , y representar `meetingId` `userMri` `frameContext` adecuadamente la experiencia.

✔ exportar un resultado de una encuesta o sondeo notifica a los usuarios que los resultados se descargaron correctamente.

✔ Una aplicación está visible en una reunión de Teams en el panel lateral o en el cuadro de diálogo en la reunión. Use el cuadro de diálogo en la reunión para mostrar el contenido que se puede usar para los participantes de la reunión. Para obtener más información, consulta [Crear aplicaciones para reuniones de Teams.](create-apps-for-teams-meetings.md)

   > [!NOTE]
   > El manifiesto de la aplicación especifica que la pestaña está optimizada para [el panel lateral,](create-apps-for-teams-meetings.md#during-a-meeting)que es donde se muestra. También puede formar parte de una experiencia de bandeja de uso compartido, sujeto a las directrices de diseño especificadas.

Las siguientes imágenes muestran la aplicación como un cuadro de diálogo en la reunión y como un panel lateral independiente:

![Experiencia en la reunión](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Vista de cuadro de diálogo en la reunión](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a>Cuadro de diálogo que puede actuar en la reunión para los usuarios

![Vista de cuadro de diálogo](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>Experiencia de aplicación posterior a la reunión

![Vista posterior a la reunión](../assets/images/apps-in-meetings/PostMeeting.png)

✔ El escenario de la aplicación posterior a la reunión es similar a la experiencia actual posterior a la reunión con la ventaja añadida de tener pestañas que existen en la superficie.

✔ usuarios con permiso pueden agregar aplicaciones desde la  galería de pestañas a una reunión mediante la pestaña Detalles del formulario de programación de Teams y la pestaña **Chat** de reunión en una reunión existente.

✔ diseño de tabulación debe organizarse cuando haya más de diez sondeos o encuestas.

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>Integrar bots en el ciclo de vida de la reunión

Para la implementación del bot, comience [con la compilación de un bot](../build-your-first-app/build-bot.md) y, a continuación, continúe con crear aplicaciones para reuniones de [Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>Integrar extensiones de mensajería en el ciclo de vida de la reunión

Para la implementación de extensión de mensajería, comience [con la compilación](../messaging-extensions/how-to/create-messaging-extension.md) de una extensión de mensajería y, a continuación, continúe con [crear aplicaciones para reuniones de Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)

## <a name="participant-roles-and-user-types-in-a-meeting"></a>Roles de participante y tipos de usuario en una reunión

![Participantes en una reunión](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>Roles de participante

La configuración predeterminada de los participantes la determina el administrador de TI de una organización. Los siguientes son los roles de participante en una reunión:

* **Organizador:** el organizador programa una reunión, establece las opciones de reunión, asigna roles de reunión e inicia la reunión. Solo los usuarios con una cuenta M365 con una licencia de Teams pueden ser organizadores y controlar los permisos de los asistentes. Un organizador de la reunión puede cambiar la configuración de una reunión específica. Los organizadores pueden realizar estos cambios en la página web **Opciones de** reunión.
* **Moderador:** los moderadores tienen las mismas capacidades que el organizador. Sin embargo, un moderador no puede quitar un organizador de la sesión ni modificar las opciones de reunión para la sesión. De forma predeterminada, los participantes que se unen a una reunión tienen el rol de moderador.
* **Asistente:** un asistente es un usuario al que se ha invitado a asistir a una reunión pero que no está autorizado a actuar como moderador. Los asistentes pueden interactuar con otros miembros de la reunión, pero no pueden administrar la configuración de la reunión ni compartir contenido.

Solo un organizador o moderador puede agregar, quitar o desinstalar aplicaciones. Solo el organizador o moderador puede crear sondeos en una reunión.

Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

Puede acceder a la  **página Opciones de reunión** de la siguiente manera:

* En Teams, vaya al **logotipo del** ![ calendario ](../assets/images/apps-in-meetings/calendar-logo.png) calendario, seleccione una reunión y, a continuación, **Opciones de reunión.**

* En una invitación a una reunión, seleccione **Opciones de reunión**.

* Durante una reunión, seleccione **Mostrar participantes** ![ mostrar el icono de participantes en los controles ](../assets/images/apps-in-meetings/show-participants.png) de la reunión. A continuación, encima de la lista de participantes, elija **Administrar permisos**.

### <a name="user-types"></a>Tipos de usuario

> [!NOTE]
> Los usuarios con tipos de usuario específicos asignados pueden unirse a reuniones y asumir uno de los roles de participante que se describen en [roles de participante.](#participant-roles) El tipo de usuario no se incluye en la API **getParticipantRole.**

Los siguientes tipos de usuario identifican lo que cada usuario puede hacer y a lo que puede acceder:

* **In-tenant:** los usuarios del espacio empresarial pertenecen a la organización y tienen credenciales en Azure Active Directory (AAD) para el inquilino. Normalmente son empleados a tiempo completo, in situ o remotos. Un usuario en el espacio empresarial puede ser organizador, moderador o asistente.
* **Invitado:** un invitado es un participante de otra organización invitado a tener acceso a Teams u otros recursos en el inquilino de la organización. Los invitados se agregan al AAD de la organización y tienen las mismas capacidades de Teams que un miembro nativo del equipo con acceso a chats de equipo, reuniones y archivos. Un usuario invitado puede ser organizador, moderador o asistente. Para obtener más información, vea [acceso de invitado en Teams](/microsoftteams/guest-access).
* **Federado o externo:** un usuario federado es un usuario externo de Teams en otra organización al que se ha invitado a unirse a una reunión. Estos usuarios tienen credenciales válidas con socios federados y están autorizados por Teams. No tienen acceso a los equipos ni a otros recursos compartidos de la organización. El acceso de invitado es una mejor opción para que los usuarios externos tengan acceso a equipos y canales. Para obtener más información, vea [manage external access in Teams](/microsoftteams/manage-external-access).
* **Anónimo:** los usuarios anónimos no tienen una identidad de AAD y no están federados con un inquilino. El participante anónimo es como un usuario externo, pero su identidad no se proyecta en la reunión. Un usuario anónimo no puede ser un organizador, pero puede ser un moderador o un asistente.

> [!NOTE]
> Los usuarios anónimos heredan la directiva de permisos de aplicación predeterminada global. Para obtener más información, consulta [Administrar aplicaciones](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).

En la tabla siguiente se proporcionan los tipos de usuario y las características a las que puede tener acceso cada usuario:

| Tipo de usuario | Pestañas | Bots | Extensiones de mensajería | Tarjetas adaptables | Módulos de tareas | Diálogo en la reunión |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Usuario anónimo | No disponible | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde una tarjeta adaptable. | No disponible |
| Invitado que forma parte del inquilino AAD | Se permite la interacción. No se permite crear, actualizar ni eliminar. | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde una tarjeta adaptable. | Disponible |
| Federado | No disponible | No disponible | No disponible | No disponible | No disponible | No disponible |

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Tab](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [Bot](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [Extensión de mensajería](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [Diseño de la aplicación](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a>Siguientes pasos

> [!div class="nextstepaction"]
> [Crear una aplicación](create-apps-for-teams-meetings.md)
