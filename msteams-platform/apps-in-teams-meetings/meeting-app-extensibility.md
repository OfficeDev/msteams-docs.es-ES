---
title: Extensibilidad de aplicaciones de reunión
author: laujan
description: Comprender la extensibilidad de la aplicación de reunión
ms.topic: conceptual
ms.openlocfilehash: 96770a6a06d7a4478d8a00a7928c74b38d7b4b2c
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649844"
---
# <a name="meeting-app-extensibility"></a>Extensibilidad de aplicaciones de reunión

Teams extensibilidad de la aplicación de reunión se basa en los siguientes conceptos:

* El ciclo de vida de la reunión tiene diferentes fases, como antes de la reunión, en la reunión y después de la reunión.  
* Hay tres roles de participante distintos en una reunión: organizador, moderador y asistente. Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).  
* Hay varios tipos [de usuario](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) en una reunión: usuarios anónimos, [](/microsoftteams/guest-access)invitados, invitados y federados. [](/microsoftteams/manage-external-access)

En este artículo se describe información sobre el ciclo de vida de la reunión y cómo integrar pestañas, bots y extensiones de mensajería en la reunión. Proporciona información para identificar diferentes roles de participante y diferentes tipos de usuario para realizar tareas.

## <a name="meeting-lifecycle"></a>Ciclo de vida de la reunión

El ciclo de vida de la reunión consiste en la experiencia de la aplicación previa a la reunión, en la reunión y posterior a la reunión. Puede integrar pestañas, bots y extensiones de mensajería en cada fase del ciclo de vida de la reunión.

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a>Integrar pestañas en el ciclo de vida de la reunión

Las pestañas permiten a los miembros del equipo tener acceso a servicios y contenido en un espacio específico dentro de una reunión. El equipo trabaja directamente con pestañas y tiene conversaciones sobre las herramientas y los datos disponibles en las pestañas. En Teams reunión, los usuarios pueden agregar una pestaña seleccionando <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>, y elegir la aplicación que quieren instalar.

> [!IMPORTANT]
> Si has integrado una pestaña con la reunión Teams, la aplicación debe seguir el flujo de autenticación de inicio de sesión único (SSO) para las [pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)

> [!NOTE]
> * Los clientes móviles solo admiten pestañas en fases de reunión previas y posteriores. Las experiencias en la reunión que son el cuadro de diálogo y el panel en la reunión actualmente no están disponibles en dispositivos móviles.
> * Las aplicaciones solo se admiten en reuniones privadas programadas.

#### <a name="pre-meeting-app-experience"></a>Experiencia de la aplicación previa a la reunión

Con la experiencia de la aplicación previa a la reunión, puedes buscar y agregar aplicaciones de reunión y realizar tareas previas a la reunión, como desarrollar un sondeo para encuestar a los participantes de la reunión.

**Para agregar pestañas a una reunión existente**

1. En el calendario, seleccione una reunión a la que desee agregar una pestaña.
1. Seleccione la **pestaña Detalles** y seleccione <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. Aparece la galería de pestañas.

    ![Experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

1. En la galería de pestañas, selecciona la aplicación que quieras agregar y sigue los pasos según sea necesario. La aplicación se instala como una pestaña.

    ![Vista de tabulación previa a la reunión](../assets/images/apps-in-meetings/PreMeetingTab.png)

    > [!NOTE]
    > * También puede agregar una pestaña mediante la **pestaña Chat de** reunión en una reunión existente.
    > * El diseño de tabulación debe estar en un estado organizado, si hay más de diez sondeos o encuestas.

#### <a name="in-meeting-app-experience"></a>Experiencia de la aplicación en la reunión

Con la experiencia de la aplicación en la reunión, puedes interactuar con los participantes durante la reunión mediante aplicaciones y el cuadro de diálogo en la reunión. Las aplicaciones de reunión se hospedan en la barra superior superior de la ventana de reunión como pestaña en la reunión. Use el cuadro de diálogo en la reunión para mostrar el contenido que se puede usar para los participantes de la reunión. Para obtener más información, consulta [Crear aplicaciones para Teams reuniones.](create-apps-for-teams-meetings.md)

**Para usar pestañas durante una reunión**

1. Después de entrar en la reunión, en la barra superior de la ventana de chat, selecciona la aplicación que quieras usar. Una aplicación está visible en una reunión Teams en el panel lateral o en el cuadro de diálogo en la reunión.
1. En el cuadro de diálogo en la reunión, escriba la respuesta como comentarios.

    ![Vista cuadro de diálogo](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

    > [!NOTE]
    > * Las aplicaciones pueden aprovechar Teams SDK de cliente para obtener acceso a , y representar `meetingId` `userMri` la experiencia `frameContext` correctamente.
    > * Si el cuadro de diálogo en la reunión se representa correctamente, se le notificará que los resultados se descargaron correctamente.
    > * El manifiesto de la aplicación especifica los lugares donde quieres que aparezcan. El campo de contexto se usa para este propósito. También puede formar parte de una experiencia de bandeja de uso compartido, sujeto a las directrices de diseño especificadas.

    En la siguiente imagen se muestra el panel lateral de la reunión:

    ![Panel lateral en la reunión](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="post-meeting-app-experience"></a>Experiencia de aplicación posterior a la reunión

Con la experiencia de la aplicación posterior a la reunión, puedes ver los resultados de la reunión, como los resultados de la encuesta o los comentarios. Select <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/> para agregar una pestaña y obtener notas y resultados de la reunión en los que los organizadores y asistentes deben tomar medidas.

En la siguiente imagen se muestra la **pestaña Contoso** con los resultados del sondeo y los comentarios recibidos de los asistentes a la reunión:

![Vista posterior a la reunión](../assets/images/apps-in-meetings/PostMeeting.png)

> [!NOTE]
> El diseño de tabulación debe organizarse cuando haya más de diez sondeos o encuestas.

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>Integrar bots en el ciclo de vida de la reunión

Los bots habilitados en el ámbito groupchat empiezan a funcionar en reuniones. Para implementar bots, comience con [la compilación de un bot](../build-your-first-app/build-bot.md) y, a continuación, continúe con crear aplicaciones para Teams [reuniones](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references).

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>Integrar extensiones de mensajería en el ciclo de vida de la reunión

Para implementar extensiones de mensajería, comience con la compilación de una extensión [de mensajería](../messaging-extensions/how-to/create-messaging-extension.md) y, a continuación, continúe con crear aplicaciones para Teams [reuniones](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references).

La extensibilidad Teams aplicación de reunión te permite diseñar la aplicación en función de los roles de los participantes en una reunión.

## <a name="participant-roles-in-a-meeting"></a>Roles de participante en una reunión

![Participantes en una reunión](../assets/images/apps-in-meetings/participant-roles.png)

La configuración predeterminada de los participantes la determina el administrador de TI de una organización. Los siguientes son los roles de participante en una reunión:

* **Organizador:** el organizador programa una reunión, establece las opciones de reunión, asigna roles de reunión e inicia la reunión. Solo los usuarios con cuenta M365 y Teams licencia pueden ser organizadores y controlar los permisos de los asistentes. Un organizador de la reunión puede cambiar la configuración de una reunión específica. Los organizadores pueden realizar estos cambios en la página web **Opciones de** reunión.
* **Moderador:** los moderadores tienen las mismas capacidades de organizadores con exclusiones. Un moderador no puede quitar un organizador de la sesión ni modificar las opciones de reunión para la sesión. De forma predeterminada, los participantes que se unen a una reunión tienen el rol de moderador.
* **Asistente:** un asistente es un usuario al que se ha invitado a asistir a una reunión pero no está autorizado a actuar como moderador. Los asistentes pueden interactuar con otros miembros de la reunión, pero no pueden administrar la configuración de la reunión ni compartir contenido.

> [!NOTE]
> Solo un organizador o moderador puede agregar, quitar o desinstalar aplicaciones.

Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

Después de diseñar la aplicación en función de los roles de los participantes en una reunión, puedes identificar cada tipo de usuario para las reuniones y seleccionar a qué pueden tener acceso.

## <a name="user-types-in-a-meeting"></a>Tipos de usuario en una reunión

> [!NOTE]
> El tipo de usuario no se incluye en la API **getParticipantRole.**

Los tipos de usuario, como, organizador, moderador o asistente en una reunión pueden realizar uno de los roles de participante [en una reunión](#participant-roles-in-a-meeting).

En la siguiente lista se detallan los distintos tipos de usuario junto con su accesibilidad y rendimiento:

* **In-tenant:** los usuarios del espacio empresarial pertenecen a la organización y tienen credenciales en Azure Active Directory (AAD) para el inquilino. Normalmente son empleados a tiempo completo, in situ o remotos. Un usuario en el espacio empresarial puede ser organizador, moderador o asistente.
* **Invitado:** un invitado es un participante de otra organización invitado a acceder a Teams u otros recursos en el espacio empresarial de la organización. Los invitados se agregan al AAD de la organización y tienen las mismas Teams que un miembro nativo del equipo con acceso a chats de equipo, reuniones y archivos. Un usuario invitado puede ser organizador, moderador o asistente. Para obtener más información, vea [acceso de invitado en Teams](/microsoftteams/guest-access).
* **Federado o externo:** un usuario federado es un usuario Teams externo de otra organización al que se ha invitado a unirse a una reunión. Los usuarios federados tienen credenciales válidas con socios federados y están autorizados por Teams. No tienen acceso a los equipos ni a otros recursos compartidos de la organización. El acceso de invitado es una mejor opción para que los usuarios externos tengan acceso a equipos y canales. Para obtener más información, vea [manage external access in Teams](/microsoftteams/manage-external-access).

    > [!NOTE]
    > Los Teams pueden agregar aplicaciones cuando hospedan reuniones o chats con otras organizaciones. Los usuarios pueden usar aplicaciones compartidas por usuarios externos cuando los usuarios se unen a reuniones o chats hospedados por otras organizaciones. Las directivas de datos de la organización del usuario de hospedaje, así como las prácticas de uso compartido de datos de las aplicaciones de terceros compartidas por la organización de ese usuario, estarán en vigor.

* **Anónimo:** los usuarios anónimos no tienen una identidad de AAD y no están federados con un inquilino. Los participantes anónimos son como usuarios externos, pero su identidad no se proyecta en la reunión. Los usuarios anónimos no pueden acceder a aplicaciones en una ventana de reunión. Un usuario anónimo no puede ser un organizador, pero puede ser moderador o asistente.

    > [!NOTE]
    > Los usuarios anónimos heredan la directiva de permisos de aplicación predeterminada global. Para obtener más información, consulta [administrar aplicaciones](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).

Un usuario invitado o anónimo no puede agregar, quitar ni desinstalar aplicaciones.

En la tabla siguiente se proporcionan los tipos de usuario y las características a las que puede tener acceso cada usuario:

| Tipo de usuario | Pestañas | Bots | Extensiones de mensajería | Tarjetas adaptables | Módulos de tareas | Diálogo en la reunión |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Usuario anónimo | No disponible | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde una tarjeta adaptable. | No disponible |
| Invitado que forma parte del inquilino AAD | Se permite la interacción. No se permite crear, actualizar ni eliminar. | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde una tarjeta adaptable. | Disponible |
| Federado | No disponible | No disponible | No disponible | No disponible | No disponible | No disponible |

## <a name="see-also"></a>Vea también

* [Tab](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [Bot](../bots/what-are-bots.md)
* [Extensión de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Diseño de la aplicación](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Requisitos previos y referencias de API para aplicaciones en Teams reuniones](create-apps-for-teams-meetings.md)