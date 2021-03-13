---
title: Aplicaciones en reuniones de Teams
author: laujan
description: información general sobre las aplicaciones en reuniones de Teams basadas en el rol de participante y usuario
ms.topic: overview
ms.author: lajanuar
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: 51fe2e0ebdaa56197bbebd1e5dbcf90698fb1f92
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753556"
---
# <a name="apps-in-teams-meetings"></a>Aplicaciones en reuniones de Teams

Las reuniones son clave para la productividad en Teams. Habilitan la colaboración, la asociación, la comunicación informada y los comentarios compartidos en un foro inclusivo y activo. Como desarrollador, puede crear aplicaciones configurables [](../messaging-extensions/what-are-messaging-extensions.md) de [pestaña,](../tabs/what-are-tabs.md#how-do-tabs-work) [bot](../bots/what-are-bots.md)y extensión de mensajes para mejorar y enriquecer una experiencia de reunión de Teams. Los usuarios de reuniones pueden acceder a las aplicaciones, a través de la galería de pestañas, para habilitar escenarios relevantes, como la preconfigurización de un panel de Kanban, el inicio de un cuadro de diálogo de acción en la reunión o la creación de un sondeo posterior a la reunión. La aplicación de reunión puede ofrecer una experiencia de usuario para cada fase del ciclo de vida de la reunión en función del estado de los asistentes.

La extensibilidad de la aplicación de reuniones de Teams se centra en tres conceptos:

✔ ciclo **de vida de la** reunión: antes, durante y después del período de tiempo de reunión.  
✔ de **participante:** organizador de la reunión, moderador o asistente.  
✔ **usuario:** usuario de Teams en el inquilino, invitado, federado o anónimo.

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>Escenarios de ciclo de vida de reuniones

## <a name="tabs"></a>Pestañas

> [!IMPORTANT]
> Al igual que con todas las aplicaciones de pestaña, la aplicación tendrá que seguir el flujo de autenticación [de SSO de](../tabs/how-to/authentication/auth-aad-sso.md) Teams para las pestañas.

> [!NOTE]
> * Los clientes móviles solo admiten pestañas en superficies previas a la reunión y posteriores a la reunión. Las experiencias en la reunión, como el cuadro de diálogo en la reunión y el panel en móvil, estarán disponibles próximamente.
> * Las aplicaciones solo se admiten en reuniones privadas programadas.

### <a name="pre-meeting-app-experience"></a>Experiencia de la aplicación previa a la reunión

**Experiencia previa a la reunión:**

![experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

**Pestaña Antes de la reunión:**

![vista de pestaña previa a la reunión](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔ usuarios con permiso pueden agregar aplicaciones a una reunión a través de la galería de pestañas de dos maneras:

&emsp;&emsp;&#9679; a través de la **pestaña Detalles** del formulario de programación de Teams.

&emsp;&emsp;&#9679; a través de la **pestaña Chat de** reunión en una reunión existente.</br> </br>

✔ de pestañas son **accesibles** en las páginas detalles y **chats** de reuniones con un icono más (➕) button.|

✔ diseño de tabulación debe estar en un estado organizado si hay más de diez sondeos o encuestas.

### <a name="in-meeting-app-experience"></a>Experiencia de la aplicación en la reunión

✔ las aplicaciones de reunión se hospedarán en la barra superior superior de la ventana de chat y como experiencia de pestaña en la reunión a través de la pestaña en la reunión. Cuando los usuarios agregan una pestaña a una  reunión a través de la galería de pestañas, se mostrarán las aplicaciones que se encuentran durante las experiencias de reunión.

✔ usuarios con permisos pueden agregar aplicaciones mientras están en la reunión.

✔ Cuando se carga en el contexto de una reunión, las aplicaciones podrán aprovechar el SDK de cliente de Teams para obtener acceso a , y representar adecuadamente `meetingId` `userMri` la `frameContext` experiencia.

✔ exportar un resultado de una encuesta o sondeos debe notificar a los usuarios que indiquen "los resultados se descargaron correctamente".

✔ para que una aplicación esté visible en una reunión de Teams en dos áreas:

&emsp;&emsp;&#9679; panel **lateral**. </br>

> [!NOTE]
> Si el _manifiesto de la_ aplicación especifica que la pestaña está optimizada para el panel [lateral,](create-apps-for-teams-meetings.md#during-a-meeting)es donde se mostrará. También puede formar parte de una experiencia de bandeja de uso compartido, sujeto a las directrices de diseño especificadas.

&emsp;&emsp;&#9679; diálogo **En la reunión**. Use el cuadro de diálogo en la reunión para mostrar el contenido que se puede usar para los participantes de la reunión. *Consulta* [Crear aplicaciones para reuniones de Teams](create-apps-for-teams-meetings.md).

**Experiencia en la reunión:**

![experiencia en la reunión](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Vista de cuadro de diálogo en la reunión](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**Cuadro de diálogo que puede actuar en la reunión para los usuarios:**

![vista de cuadro de diálogo](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>Experiencia de aplicación posterior a la reunión

**Experiencia posterior a la reunión:**

![vista posterior a la reunión](../assets/images/apps-in-meetings/PostMeeting.png)

✔ El escenario de la aplicación posterior a la reunión es similar a la experiencia actual posterior a la reunión con la ventaja añadida de tener pestañas que existen en la superficie. 

✔ usuarios con permisos pueden agregar aplicaciones desde la galería  de pestañas a una reunión mediante la pestaña Detalles del formulario de programación de Teams y la pestaña **Chat** de reunión en una reunión existente.

✔ diseño de tabulación debe estar en un estado organizado si hay más de diez sondeos o encuestas.

### <a name="bots"></a>Bots

Para la implementación del bot, comience [con la compilación de un bot](../build-your-first-app/build-bot.md) y, a continuación, continúe con crear aplicaciones para reuniones de [Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)

### <a name="messaging-extensions"></a>Extensiones de mensajería

Para la implementación de extensión de mensajería, comience [con la compilación](../messaging-extensions/how-to/create-messaging-extension.md) de una extensión de mensajería y, a continuación, continúe con [crear aplicaciones para reuniones de Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)

## <a name="participant-roles-and-user-types-in-a-meeting"></a>Roles de participante y tipos de usuario en una reunión

![Participantes en una reunión](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>Roles de participante

Puedes diseñar la aplicación con autorización específica del participante. Por ejemplo, quizás solo un organizador o moderador puede crear un sondeo en reuniones. Aunque la configuración predeterminada de los participantes la determina el administrador de TI de una organización, es posible que un organizador de la reunión quiera cambiar la configuración de una reunión específica. Los organizadores pueden realizar estos cambios en la página web Opciones de reunión.

1. **Organizador**. El organizador programa una reunión, establece las opciones de reunión, asigna roles de reunión e inicia la reunión. Solo los usuarios con una cuenta M365 (que posee una licencia de Teams) pueden ser organizadores y controlar los permisos de los asistentes.
1. **Moderador**. Los presentadores tienen casi las mismas capacidades que el organizador; sin embargo, un moderador no puede quitar un organizador de la sesión ni modificar las opciones de reunión para la sesión. De forma predeterminada, los participantes que se unen a una reunión tienen el rol de moderador.
1. **Attendee**. Un asistente es un usuario al que se ha invitado a asistir a una reunión pero que no está autorizado a actuar como moderador. Los asistentes pueden interactuar con otros miembros de la reunión, pero no pueden administrar la configuración de la reunión ni compartir contenido.

_Ver_ [ **Roles en una reunión de Teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

Puede acceder a la  **página Opciones de reunión** de la siguiente manera:

&#11200; En Teams, vaya  al logotipo del ![ calendario ](../assets/images/apps-in-meetings/calendar-logo.png) calendario, seleccione una reunión y, a continuación, **Opciones de reunión.**

&#11200; En una invitación a una reunión, seleccione **Opciones de reunión**.

&#11200; Durante una reunión, seleccione **Mostrar participantes** ![ mostrar el icono de participantes en los controles ](../assets/images/apps-in-meetings/show-participants.png) de la reunión. A continuación, encima de la lista de participantes, elija **Administrar permisos**.

### <a name="user-types"></a>Tipos de usuario

> [!NOTE]
> Los tipos de usuario pueden unirse a reuniones y asumir uno de los roles de participante descritos anteriormente. El tipo user no se expone como parte de la API **getParticipantRole.**

1. **In-tenant**. Estos usuarios pertenecen a la organización y tienen credenciales en Azure Active Directory para el inquilino. Normalmente son empleados a tiempo completo, in situ o remotos.
1. **Invitado**. Un invitado es un participante de otra organización que ha sido invitado a tener acceso a Teams u otros recursos en el inquilino de la organización. Los invitados se agregan a Active Directory de la organización y pueden tener casi todas las mismas capacidades de Teams que un miembro nativo del equipo con acceso total a chats de equipo, reuniones y archivos. _Consulta_ [Acceso de invitados en Microsoft Teams](/microsoftteams/guest-access)
1. **Federado/externo**. Un usuario federado es un usuario externo de Teams en otra organización al que se ha invitado a unirse a una reunión. Dado que estos usuarios tienen credenciales válidas con socios federados, Teams los trata como autenticados, pero no tienen acceso a los equipos u otros recursos compartidos de la organización. Si desea que los usuarios externos tengan acceso a equipos y canales, el acceso de invitado puede ser una mejor opción. _Consulta Administrar_ [el acceso externo en Microsoft Teams](/microsoftteams/manage-external-access)
1. **Anónimo**. Los usuarios anónimos no tienen una identidad de Active Directory y no están federados con un inquilino. El participante anónimo es como un usuario externo, pero su identidad no se proyecta en la reunión. Los usuarios anónimos no podrán acceder a las aplicaciones en una ventana de reunión.

## <a name="next-steps"></a>Siguientes pasos

> [!div class="nextstepaction"]
> [Diseño de la aplicación](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [Crear una aplicación](create-apps-for-teams-meetings.md)
