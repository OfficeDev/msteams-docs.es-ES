---
title: Aplicaciones en reuniones de Microsoft Teams
author: laujan
description: Información general sobre las aplicaciones de Microsoft Teams basadas en participantes y roles de usuario
ms.topic: overview
ms.author: lajanuar
keywords: API de las aplicaciones de Microsoft Teams rol de participante de usuario
ms.openlocfilehash: 13fc44e9831cf58f0ab847eab06cc5b99ed8cc70
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796228"
---
# <a name="apps-in-teams-meetings-developer-preview"></a>Aplicaciones en reuniones de Microsoft Teams (vista previa para desarrolladores)

>[!IMPORTANT]
> Las características incluidas en Microsoft Teams Developer Preview se proporcionan solo para fines de acceso anticipado, pruebas y comentarios. Pueden sufrir cambios antes de que estén disponibles en la versión pública y no deben usarse en las aplicaciones de producción.

Las reuniones son clave para la productividad en Microsoft Teams. Permiten la colaboración, la asociación, la comunicación informada y los comentarios compartidos en un foro activo y integrado. Como desarrollador, puede crear aplicaciones de [pestaña](../tabs/what-are-tabs.md#how-do-tabs-work), [Bot](../bots/what-are-bots.md)y extensión de [mensajes](../messaging-extensions/what-are-messaging-extensions.md) que se pueden configurar para mejorar y enriquecer una experiencia de reunión de Microsoft Teams. Los usuarios de la reunión pueden tener acceso a las aplicaciones a través de la galería de pestañas, para habilitar escenarios relevantes como preensayar un panel Kanban, iniciar un cuadro de diálogo que requiere acción en la reunión o crear un sondeo posterior a la reunión. La aplicación de la reunión puede proporcionar una experiencia de usuario para cada fase del ciclo de vida de la reunión en función del estado del asistente.

Los centros de la extensibilidad de la aplicación de reunión de los equipos en tres conceptos:

✔ **Ciclo de vida** de la reunión, antes, durante y después del intervalo de tiempo de la reunión.  
✔ **Rol de participante** : Organizador de la reunión, moderador o asistente.  
✔ **Tipo de usuario** : usuario de Microsoft Teams: en el inquilino, invitado, federado o anónimo.

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>Escenarios del ciclo de vida de reuniones

## <a name="tabs"></a>Pestañas

> [!IMPORTANT]
> Como con todas las aplicaciones de pestaña, la aplicación deberá seguir el [flujo de autenticación SSO](../tabs/how-to/authentication/auth-aad-sso.md) de Microsoft Teams para las pestañas.

> [!NOTE]
> Los clientes móviles solo admiten fichas en las superficies anteriores y posteriores a la reunión. Las experiencias en reunión (el panel y el cuadro de diálogo en reunión) en dispositivos móviles estarán disponibles próximamente

### <a name="pre-meeting-app-experience"></a>Experiencia de aplicación previa a la reunión

**Experiencia previa a la reunión:**

![experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

**Ficha anterior a la reunión:**

![vista de pestañas anteriores a la reunión](../assets/images/apps-in-meetings/PreMeetingTab.png)

Los usuarios con permisos de ✔ pueden agregar aplicaciones a una reunión a través de la galería de pestañas de dos maneras:

&emsp;&emsp;&#9679; a través de la ficha **detalles** en el formulario de programación de Teams.

&emsp;&emsp;&#9679; a través de la pestaña **chat** de reuniones en una reunión existente.</br> </br>

✔ Las aplicaciones de pestaña son accesibles en las páginas de **detalles** y **chats** de reuniones con un botón de icono de signo más (➕). |

### <a name="in-meeting-app-experience"></a>Experiencia de la aplicación de reunión

✔ Aplicaciones de reunión se hospedarán en la barra superior superior de la ventana de chat y como experiencia de la pestaña en la reunión mediante la pestaña en reunión. Cuando los usuarios agregan una pestaña a una reunión a través de la galería de pestañas, las aplicaciones que se ejecutan en las experiencias de **reunión** se exponen.

Los usuarios con permisos de ✔ pueden agregar aplicaciones durante la reunión.

✔ Cuando se carga en el contexto de una reunión, las aplicaciones podrán usar el SDK del cliente de Microsoft Teams para acceder al `meetingId` , `userMri` y `frameContext` para representar correctamente la experiencia.

✔ De una aplicación puede estar visible en dos áreas de la reunión de Microsoft Teams:

&emsp;&emsp;&#9679; **panel lateral** . </br>

> [!NOTE]
> Si el _manifiesto_ de la aplicación especifica que la pestaña está [optimizada para el panel lateral](create-apps-for-teams-meetings.md#in-meeting), es decir, donde se mostrará. También puede formar parte de una experiencia de bandeja de recursos compartidos, sujeta a pautas de diseño específicas.

&emsp;&emsp;&#9679; **cuadro de diálogo en la reunión** . Use el cuadro de diálogo de la reunión para mostrar contenido que requiere acción para los participantes en la reunión. *Consulte* [crear aplicaciones para reuniones de Microsoft Teams](create-apps-for-teams-meetings.md).

**Experiencia de reunión:**

![Experiencia de reunión](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Vista de cuadro de diálogo en reunión](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**Cuadro de diálogo que requiere acción en la reunión para los usuarios:**

![vista de cuadro de diálogo](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>Experiencia de aplicación posterior a la reunión

**Experiencia posterior a la reunión:**

![Vista posterior a la reunión](../assets/images/apps-in-meetings/PostMeeting.png)

El escenario de aplicación posterior a la reunión es similar a la experiencia de posreunión actual con la ventaja agregada de tener pestañas en la superficie. Los usuarios con permisos pueden agregar aplicaciones desde la galería de pestañas a una reunión a través de la pestaña **detalles** en el formulario de programación de Teams y la pestaña **chat** de reuniones en una reunión existente.

### <a name="bots"></a>Bots

Para la implementación de bot, vea nuestros [bots en la documentación de reuniones de Microsoft Teams](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) .

### <a name="messaging-extensions"></a>Extensiones de mensajería

Para la implementación de la extensión de mensajería, consulte nuestra documentación [de las reuniones de mensajería en Microsoft Teams](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) .

## <a name="participant-roles-and-user-types-in-a-meeting"></a>Roles de participantes y tipos de usuario en una reunión

![Participantes en una reunión](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>Roles de participantes

Puede diseñar la aplicación con autorización específica del participante. Por ejemplo, quizás solo un organizador o moderador puede crear un sondeo en las reuniones. Aunque la configuración de participante predeterminada la determina el administrador de TI de una organización, es posible que el organizador de la reunión desee cambiar la configuración de una reunión específica. Los organizadores pueden realizar estos cambios en la Página Web de opciones de reunión.

1. **Organizer** . El organizador programa una reunión, establece las opciones de la reunión, asigna roles de reunión e inicia la reunión. Solo los usuarios con una cuenta M365 (que posean una licencia de Teams) pueden ser organizadores y controlar los permisos de los asistentes.
1. **Moderador** . Los moderadores tienen casi las mismas capacidades que Organizer; sin embargo, un moderador no puede quitar un organizador de la sesión ni modificar las opciones de reunión para la sesión. De forma predeterminada, los participantes que se unen a una reunión tienen el rol de moderador.
1. **Asistente** . Un asistente es un usuario que ha sido invitado a asistir a una reunión pero que no tiene autorización para actuar como moderador. Los asistentes pueden interactuar con otros miembros de la reunión, pero no pueden administrar ninguna configuración de la reunión ni compartir contenido.

_Ver_ los [ **roles de una reunión de Microsoft Teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

Puede tener acceso a la página  **Opciones de reunión** de la siguiente manera:

&#11200; en Microsoft Teams, vaya al logotipo del calendario de **calendario** ![ ](../assets/images/apps-in-meetings/calendar-logo.png) , seleccione una reunión y, a continuación, **Opciones de reunión** .

&#11200; en una invitación a la reunión, seleccione **Opciones de reunión** .

&#11200; durante una reunión, seleccione **Mostrar participantes** ![ Mostrar icono ](../assets/images/apps-in-meetings/show-participants.png) de participantes en los controles de la reunión. A continuación, encima de la lista de participantes, elija **administrar permisos** .

### <a name="user-types"></a>Tipos de usuario

> [!NOTE]
> Los tipos de usuario pueden unirse a las reuniones y asumir una de las funciones de participante descritas anteriormente. El tipo de usuario no se expone como parte de la API de **getParticipantRole** .

1. **En el espacio empresarial** . Estos usuarios pertenecen a la organización y tienen credenciales en Azure Active Directory para el inquilino. Suelen ser empleados a tiempo completo, en el sitio o remotos.
1. **Invitado** . Un invitado es un participante de otra organización a la que se ha invitado a tener acceso a teams u otros recursos en el inquilino de su organización. Los invitados se agregan al Active Directory de la organización y pueden tener casi todas las mismas capacidades de teams que un miembro del equipo nativo con acceso total a los chats, las reuniones y los archivos del equipo. _Consulte_ [acceso de invitado en Microsoft Teams](/microsoftteams/guest-access)
1. **Federado/externo** . Un usuario federado es un usuario de Microsoft Teams externo de otra organización que ha sido invitado a unirse a una reunión. Como estos usuarios tienen credenciales válidas con socios federados, se tratan como autenticados por Teams, pero no tienen acceso a los equipos ni a otros recursos compartidos de su organización. Si desea que los usuarios externos tengan acceso a los equipos y canales, el acceso de invitado puede ser una opción mejor. _Consulte_ [administrar el acceso externo en Microsoft Teams](/microsoftteams/manage-external-access)
1. **Anónima** . Los usuarios anónimos no tienen una identidad de Active Directory y no están federados con un inquilino. El participante anónimo es como un usuario externo, pero su identidad no se proyecta en la reunión. Los usuarios anónimos no podrán acceder a las aplicaciones en una ventana de reunión.

## <a name="next-steps"></a>Siguientes pasos

> [!div class="nextstepaction"]
> [Crear aplicaciones para reuniones de Teams](create-apps-for-teams-meetings.md)
