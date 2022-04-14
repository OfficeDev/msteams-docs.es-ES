---
title: Aplicaciones de reuniones unificadas
author: surbhigupta
description: Obtenga información sobre Teams ciclo de vida de las reuniones y la experiencia de reunión del usuario en el entorno de escritorio y móvil, los roles y los tipos de participantes y usuarios, integración de bots y extensión de mensajería en el ciclo de vida de la reunión.
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 4eb3b65213414b7e793795490613c343fc84ad3a
ms.sourcegitcommit: 77e92360bd8fb5afcda76195d90122ce8ef0389e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2022
ms.locfileid: "64838463"
---
# <a name="unified-meetings-apps"></a>Aplicaciones de reuniones unificadas

Teams aplicaciones unificadas de reuniones se basan en los siguientes conceptos:

* El ciclo de vida de la reunión tiene diferentes fases: antes de la reunión, durante la reunión y después de la reunión.  
* Hay tres roles de participante distintos en una reunión: organizador, moderador y asistente. Para obtener más información, vea [Roles en una reunión de Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).  
* Hay varios [tipos de usuario](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) en una reunión: usuarios en el inquilino, [invitados](/microsoftteams/guest-access), [federados](/microsoftteams/manage-external-access) y anónimos.

En este artículo se describe la información sobre el ciclo de vida de las reuniones y cómo integrar pestañas, bots y extensiones de mensajería. Identifica diferentes roles de participante y tipos de usuario.

## <a name="meeting-lifecycle"></a>Ciclo de vida de la reunión

El ciclo de vida de una reunión consiste en la experiencia de la aplicación previa a la reunión, durante la reunión y posterior a la reunión. Se pueden integrar pestañas, bots y extensiones de mensajería en cada fase del ciclo de vida de la reunión.

> [!NOTE]
> Las extensiones de reunión, como bots, tarjetas, extensiones de mensaje y acciones de mensaje, se admiten en el cliente web. Sin embargo, actualmente no se admiten por completo experiencias hospedadas como pestañas, burbujas de contenido y uso compartido en fase.

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a>Integrar pestañas en el ciclo de vida de la reunión

Las pestañas permiten a los miembros del equipo acceder a los servicios y el contenido en un espacio específico dentro de una reunión. El equipo trabaja directamente con pestañas y tiene conversaciones sobre las herramientas y los datos disponibles en las pestañas. En Teams reunión, puede agregar una pestaña seleccionando <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>y seleccione la aplicación que desea instalar.

> [!IMPORTANT]
> Si ha integrado una pestaña con la reunión, la aplicación debe seguir el [Teams flujo de autenticación de inicio de sesión único (SSO) para las pestañas](../tabs/how-to/authentication/auth-aad-sso.md).

> [!NOTE]
>
> * Las reuniones programadas privadas solo admiten aplicaciones.
> * La opción Agregar aplicación para Teams aplicación de pestaña de extensión de reunión no se admite en Teams cliente web.

#### <a name="pre-meeting-app-experience"></a>Experiencia de la aplicación previa a la reunión

Con la experiencia de la aplicación previa a la reunión, se pueden buscar y agregar aplicaciones de reunión. También se pueden realizar tareas previas a la reunión, como desarrollar un sondeo para encuestar a los participantes de la reunión.

Para agregar pestañas a una reunión existente:

1. En el calendario, seleccione una reunión a la que quiera agregar una pestaña.
1. Seleccione la pestaña **Detalles** y seleccione <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. Aparece la galería de pestañas.

    :::image type="content" source="~/assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="Experiencia de la aplicación previa a la reunión":::

1. En la galería de pestañas, seleccione la aplicación que desea agregar y siga los pasos necesarios. La aplicación se instala como una pestaña.

   > [!NOTE]
   >
   > * También puede agregar una pestaña a una reunión existente mediante la pestaña **Chat** de reunión.
   > * El diseño de tabulación debe estar en un estado organizado, si hay más de 10 sondeos o encuestas.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="Pestañas durante una reunión":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

Después de agregar las pestañas a una reunión existente en el móvil, puede ver las mismas aplicaciones en la experiencia previa a la reunión en la sección **Más** de los detalles de la reunión.

<img src="../assets/images/apps-in-meetings/mobilePostMeeting.png" alt="Mobile pre-meeting experience" width="200"/>  

---

#### <a name="in-meeting-app-experience"></a>Experiencia de la aplicación durante la reunión

Con la experiencia de la aplicación durante la reunión, puedes interactuar con los participantes durante la reunión mediante las aplicaciones y el cuadro de diálogo durante la reunión. Las aplicaciones de reunión se hospedan en la barra de herramientas de la ventana de reunión como una pestaña durante la reunión. Usa el cuadro de diálogo durante la reunión para mostrar el contenido que pueden usar los participantes de la reunión. Para obtener más información, consulte [Habilitación y configuración de aplicaciones para reuniones de Teams](enable-and-configure-your-app-for-teams-meetings.md).

Para dispositivos móviles, las aplicaciones de reuniones están disponibles en **Aplicaciones** > puntos suspensivos &#x25CF;&#x25CF;&#x25CF; en la reunión. Seleccione **Aplicaciones** para ver todas las aplicaciones disponibles en la reunión.

Para usar pestañas durante una reunión:

1. Ve a Teams.
1. En el calendario, seleccione una reunión en la que quiera usar una pestaña.
1. Después de entrar en la reunión, en la barra de herramientas de la ventana de chat, seleccione la aplicación necesaria.
    Una aplicación está visible en una Teams reunión en el panel lateral o en el cuadro de diálogo en la reunión.
1. En el cuadro de diálogo en la reunión, escriba la respuesta como comentarios.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/desktop-in-meeting-dialog-view.png" alt-text="Vista de escritorio":::


# <a name="mobile"></a>[Móvil](#tab/mobile)

Después de entrar en la reunión y agregar la aplicación desde el escritorio o la web, la aplicación está visible en la reunión de Teams móvil en la sección **Aplicaciones**. Seleccione **Aplicaciones** para mostrar la lista de aplicaciones. El usuario puede iniciar cualquiera de las aplicaciones como un panel del lado de la reunión de la aplicación.

Se muestra el cuadro de diálogo en la reunión donde puede escribir la respuesta como comentarios.

<img src="../assets/images/apps-in-meetings/mobile-in-meeting-dialog-view.png" alt="Mobile dialog box view" width="200"/>

> [!NOTE]
> No es necesario cambiar el manifiesto de aplicación para que las aplicaciones funcionen en dispositivos móviles.

---

> [!NOTE]
>
> * Las aplicaciones pueden aprovechar el SDK de cliente de Teams para acceder `meetingId`a , `userMri`y `frameContext` para representar la experiencia adecuadamente.
> * Si el cuadro de diálogo en la reunión se representa correctamente, envía una notificación de que los resultados se descargan correctamente.
> * El manifiesto de aplicación especifica los lugares en los que quieres que aparezcan las aplicaciones. Para ello, especifique el campo de contexto en el manifiesto. También forma parte de una experiencia de la fase de reunión de uso compartido, según [las directrices de diseño](~\apps-in-teams-meetings\design\designing-apps-in-meetings.md) especificadas.
> * La fase de reunión no es compatible con usuarios anónimos ni Teams cliente web.

En la imagen siguiente se muestra el panel del lado de la reunión:

# <a name="desktop"></a>[Escritorio](#tab/desktop)

![Panel del lado de la reunión](../assets/images/in-meeting-dialog.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

<img src="../assets/images/apps-in-meetings/sidepanelmobile.png" alt="In-meeting side panel mobile" width="300"/>

---

En la tabla siguiente se describe el comportamiento de la aplicación cuando se valida y no se valida:

|Funcionalidad de la aplicación | Se valida la aplicación | No se valida la aplicación |
|---|---|---|
| Extensibilidad de reuniones | La aplicación aparecerá en las reuniones. | La aplicación no aparecerá en las reuniones de los clientes móviles. |

Para obtener más información, consulte [directrices de validación de almacenamiento](../concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).

#### <a name="post-meeting-app-experience"></a>Experiencia de la aplicación posterior a la reunión

Con la experiencia de la aplicación posterior a la reunión, puede ver los resultados de la reunión, como los resultados de la encuesta de sondeo o los comentarios. Seleccionar <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/> para agregar una pestaña, obtener notas de la reunión y ver los resultados en los que los organizadores y asistentes deben tomar medidas.

En la imagen siguiente se muestra la pestaña **Contoso** con los resultados del sondeo y los comentarios recibidos de los asistentes a la reunión:

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/post.png" alt-text="Pestaña Contoso con resultados":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="~/assets/images/apps-in-meetings/mobilepremeeting.png" alt-text="Experiencia de la aplicación posterior a la reunión":::

---

> [!NOTE]
> El diseño de tabulación debe organizarse cuando haya más de 10 sondeos o encuestas.

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>Integración de bots en el ciclo de vida de la reunión

Los bots habilitados en el ámbito de chat en grupo comienzan a funcionar en las reuniones. Para implementar bots, comience con [la compilación de un bot](../build-your-first-app/build-bot.md) y, a continuación, continúe con [la creación de aplicaciones para Teams reuniones](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references).

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>Integración de extensiones de mensajería en el ciclo de vida de la reunión

Para implementar la extensión de mensajería, comience con [la compilación de una extensión de mensajería](../messaging-extensions/how-to/create-messaging-extension.md) y, a continuación, continúe con [la creación de aplicaciones para Teams reuniones](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references).

El Teams las aplicaciones de reuniones unificadas le permiten diseñar la aplicación en función de los roles de los participantes en una reunión.

## <a name="participant-roles-in-a-meeting"></a>Roles de participante en una reunión

:::image type="content" source="~/assets/images/apps-in-meetings/participant-roles.png" alt-text="Roles de participante en una reunión":::

La configuración predeterminada de los participantes la determina el administrador de TI de una organización. A continuación se muestran los roles de participante en una reunión:

* **Organizador**: el organizador programa una reunión, establece las opciones de reunión, asigna roles de reunión e inicia la reunión. Los usuarios con Microsoft 365 cuenta y licencia de Teams solo pueden ser los organizadores y controlar los permisos de los asistentes. Un organizador de reuniones puede cambiar la configuración de una reunión específica. Los organizadores pueden realizar estos cambios en la página web **Opciones de reunión** .

* **Moderador**: los moderadores tienen las mismas capacidades de los organizadores con exclusiones. Un moderador no puede quitar un organizador de la sesión ni modificar las opciones de reunión de la sesión. De forma predeterminada, los participantes que se unen a una reunión tienen el rol de moderador.

* **Asistente**: un asistente es un usuario que está invitado a asistir a la reunión. Los asistentes tienen funcionalidades limitadas durante la reunión, como:
  * Pueden interactuar con otros miembros de la reunión, pero no pueden administrar ninguna configuración de reunión ni compartir el contenido.  
  * Pueden ver o interactuar con la aplicación de pestaña en la fase de reunión en Teams cliente de escritorio sin instalar la aplicación o sin ningún derecho de aplicación. No pueden ver ni interactuar con la aplicación en la fase de reunión de un cliente web Teams.
  * No pueden ver ni interactuar con la aplicación en el panel lateral sin ningún derecho de aplicación.
  * No están autorizados para actuar como moderador.
  * Si el asistente se une como un usuario anónimo, no puede ver ni interactuar con la aplicación de pestaña en la fase de reunión en Teams clientes web y de escritorio.

> [!NOTE]
> Solo un organizador o moderador puede agregar, quitar o desinstalar aplicaciones.

Para obtener más información, vea [Roles en una reunión de Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

Después de diseñar la aplicación en función de los roles de participante en una reunión, puede identificar cada tipo de usuario para las reuniones y seleccionar a qué puede acceder.

## <a name="user-types-in-a-meeting"></a>Tipos de usuario en una reunión

Los tipos de usuario, como organizador, moderador o asistente en una reunión, pueden realizar uno de los [roles de participante en una reunión](#participant-roles-in-a-meeting).

> [!NOTE]
> El tipo de usuario no se incluye en la API **getParticipantRole** .

En la lista siguiente se detallan los distintos tipos de usuario junto con su accesibilidad y rendimiento:

* **En el inquilino**: los usuarios en el inquilino pertenecen a la organización y tienen credenciales en Microsoft Azure Active Directory (Azure AD) para el inquilino. Son empleados a tiempo completo, in situ o remotos. Un usuario en el inquilino puede ser organizador, moderador o asistente.
* **Invitado**: un invitado es un participante de otra organización invitado a acceder a Teams u otros recursos del inquilino de la organización. Los invitados se agregan a la Azure AD de la organización y tienen las mismas capacidades de Teams que un miembro nativo del equipo. Tienen acceso a chats de equipo, reuniones y archivos. Un invitado puede ser organizador, moderador o asistente. Para obtener más información, consulte [acceso de invitado en Teams](/microsoftteams/guest-access).
* **Federado o externo**: un usuario federado es un usuario Teams externo de otra organización al que se ha invitado a unirse a una reunión. Los usuarios federados tienen credenciales válidas con asociados federados y están autorizados por Teams. No tienen acceso a los equipos ni a otros recursos compartidos de su organización. El acceso de invitado es una mejor opción para que los usuarios externos tengan acceso a equipos y canales. Para obtener más información, consulte [Administración del acceso externo en Teams](/microsoftteams/manage-external-access).

    > [!NOTE]
    > Los usuarios Teams pueden agregar aplicaciones cuando hospedan reuniones o chats con otras organizaciones. Los usuarios pueden usar aplicaciones compartidas por usuarios externos cuando los usuarios se unan a reuniones o chats hospedados por otras organizaciones. Las directivas de datos de la organización del usuario de hospedaje, así como las prácticas de uso compartido de datos de las aplicaciones de terceros compartidas por la organización de ese usuario, estarán en vigor.

    > [!IMPORTANT]
    > Actualmente, las aplicaciones de terceros están disponibles en Government Community Cloud (GCC), pero no están disponibles para GCC-High y el Departamento de Defensa (DOD). Las aplicaciones de terceros están desactivadas de forma predeterminada para GCC. Para activar aplicaciones de terceros para GCC, consulte [Administración de directivas de permisos de aplicaciones](/microsoftteams/teams-app-permission-policies) y [administración de aplicaciones](/microsoftteams/manage-apps).

* **Anónimo**: los usuarios anónimos no tienen una identidad Azure AD y no están federados con un inquilino. Los participantes anónimos son como usuarios externos, pero su identidad no se muestra en la reunión. Los usuarios anónimos no pueden acceder a las aplicaciones en una ventana de reunión ni en una fase de reunión. Un usuario anónimo no puede ser organizador, pero puede ser moderador o asistente.

    > [!NOTE]
    > Los usuarios anónimos heredan la directiva de permisos de aplicación de nivel de usuario predeterminada global. Para obtener más información, vea [Administrar aplicaciones](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).

Un usuario anónimo o invitado no puede agregar, quitar ni desinstalar aplicaciones.

En la tabla siguiente se proporcionan los tipos de usuario y se enumeran las características a las que puede acceder cada usuario:

| Tipo de usuario | Pestañas | Bots | Extensiones de mensajería | Tarjetas adaptables | Módulos de tareas | Diálogo en la reunión | Fase de reunión |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Usuario anónimo | No disponible | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde la tarjeta adaptable. | No disponible | No disponible |
| Invitado, parte del inquilino Azure AD | Se permite la interacción. No se permiten crear, actualizar y eliminar. | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde la tarjeta adaptable. | Disponible | Puede iniciar, ver e interactuar con la aplicación en la fase de reunión solo en Teams cliente de escritorio |
| Para obtener más información, consulte [Usuarios no estándar](/microsoftteams/non-standard-users). | Se permite la interacción. No se permiten crear, actualizar y eliminar. | Se permite la interacción. No se permiten adquirir, actualizar y eliminar. | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde la tarjeta adaptable. | No disponible | Puede iniciar, ver e interactuar con la aplicación en la fase de reunión solo en Teams cliente de escritorio. |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Habilitación y configuración de las aplicaciones para reuniones de Teams](enable-and-configure-your-app-for-teams-meetings.md)

## <a name="see-also"></a>Consulte también

* [Tab](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [Bot](../bots/what-are-bots.md)
* [Extensión de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Diseño de la aplicación](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
