---
title: Aplicaciones de reuniones unificadas
author: surbhigupta
description: Obtenga información sobre el ciclo de vida de la reunión, la creación de la experiencia de reunión del usuario a lo largo del ciclo de vida de las reuniones en el entorno de escritorio y móvil, los roles de participante y los tipos de usuario. Además, obtenga información sobre la integración de bots y la extensión de mensajes en el ciclo de vida de la reunión.
ms.topic: conceptual
ms.localizationpriority: none
ms.author: surbhigupta
ms.date: 04/07/2022
ms.openlocfilehash: db90b3e3f026eced56c626a082f5ec6be04cb893
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560648"
---
# <a name="unified-meetings-apps"></a>Aplicaciones de reuniones unificadas

Las aplicaciones de reuniones unificadas de Teams se basan en los siguientes conceptos:

* El ciclo de vida de la reunión tiene diferentes fases: antes de la reunión, durante la reunión y después de la reunión.  
* Hay tres roles de participante distintos en una reunión: organizador, moderador y asistente. Para obtener más información, consulte [roles en una reunión de Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).  
* Hay varios [tipos de usuario](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) en una reunión: usuarios en el inquilino, [invitados](/microsoftteams/guest-access), [federados](/microsoftteams/manage-external-access) y anónimos.

En este artículo se describe la información sobre el ciclo de vida de las reuniones y cómo integrar pestañas, bots y extensiones de mensajes. Identifica diferentes roles de participante y tipos de usuario.

## <a name="meeting-lifecycle"></a>Ciclo de vida de la reunión

El ciclo de vida de una reunión consiste en la experiencia de la aplicación previa a la reunión, durante la reunión y posterior a la reunión. Se pueden integrar pestañas, bots y extensiones de mensajería en cada fase del ciclo de vida de la reunión.

> [!NOTE]
>
> * Las aplicaciones para reuniones programadas de canales públicos solo están disponibles actualmente en versión [preliminar para desarrolladores públicos](../resources/dev-preview/developer-preview-intro.md).
>
> * Las extensiones de reunión, como bots, tarjetas, extensiones de mensaje y acciones de mensaje, se admiten en el cliente web. Sin embargo, actualmente no se admiten por completo experiencias hospedadas como pestañas, burbujas de contenido y uso compartido en fase.

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a>Integrar pestañas en el ciclo de vida de la reunión

Las pestañas permiten a los miembros del equipo acceder a los servicios y el contenido en un espacio específico dentro de una reunión. El equipo trabaja directamente con pestañas y tiene conversaciones sobre las herramientas y los datos disponibles en las pestañas. En la reunión de Teams, puede agregar una pestaña seleccionando <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>y seleccione la aplicación que desea instalar.

> [!IMPORTANT]
> Se recomienda seguir el [flujo de autenticación de inicio de sesión único (SSO) de Teams para las pestañas](../tabs/how-to/authentication/tab-sso-overview.md), si ha integrado una aplicación de pestaña en la reunión.

> [!NOTE]
> La opción Agregar aplicación para la aplicación de pestaña extensión de reunión de Teams no se admite en el cliente web de Teams.

#### <a name="pre-meeting-app-experience"></a>Experiencia de la aplicación previa a la reunión

Con la experiencia de la aplicación previa a la reunión, se pueden buscar y agregar aplicaciones de reunión. También se pueden realizar tareas previas a la reunión, como desarrollar un sondeo para encuestar a los participantes de la reunión.

#### <a name="to-add-tabs-to-an-existing-meeting"></a>Para agregar pestañas a una reunión existente

1. En el calendario, seleccione una reunión a la que quiera agregar una pestaña.
1. Seleccione la pestaña **Detalles** y seleccione <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. Aparece la galería de pestañas.

    :::image type="content" source="~/assets/images/apps-in-meetings/PreMeeting.png" alt-text="Experiencia de la aplicación previa a la reunión.":::

1. En la galería de pestañas, seleccione la aplicación que desea agregar y siga los pasos necesarios. La aplicación se instala como una pestaña.

   > [!NOTE]
   > También puede agregar una pestaña a una reunión existente mediante la pestaña **Chat** de reunión.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="Pestañas durante una reunión.":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

Después de agregar las pestañas a una reunión existente en el móvil, puede ver las mismas aplicaciones en la experiencia previa a la reunión en la sección **Más** de los detalles de la reunión.

:::image type="content" source="~/assets/images/apps-in-meetings/mobilepremeeting.png" alt-text="Experiencia móvil previa a la reunión":::

---

#### <a name="in-meeting-app-experience"></a>Experiencia de la aplicación durante la reunión

Con la experiencia de la aplicación durante la reunión, puedes interactuar con los participantes durante la reunión mediante las aplicaciones y el cuadro de diálogo durante la reunión. Las aplicaciones de reunión se hospedan en la barra de herramientas de la ventana de reunión como una pestaña durante la reunión. Usa el cuadro de diálogo durante la reunión para mostrar el contenido que pueden usar los participantes de la reunión. Para obtener más información, consulte [Creación de aplicaciones para reuniones de Teams](create-apps-for-teams-meetings.md).

Para dispositivos móviles, las aplicaciones de reuniones están disponibles en **Aplicaciones** > puntos suspensivos &#x25CF;&#x25CF;&#x25CF; en la reunión. Seleccione **Aplicaciones** para ver todas las aplicaciones disponibles en la reunión.

En el caso del escritorio, puede agregar aplicaciones durante una reunión mediante la opción **Agregar una aplicación** :::image type="icon" source="../assets/icons/add-icon.png" border="false"::: desde la ventana de la reunión.

Para usar pestañas durante una reunión:

1. Vaya a Teams.
1. En el calendario, seleccione una reunión en la que quiera usar una pestaña.
1. Después de entrar en la reunión, en la barra de herramientas de la ventana de chat, seleccione la aplicación necesaria.
    Una aplicación es visible en una reunión de Teams en el panel lateral o en el cuadro de diálogo en la reunión.
1. En el cuadro de diálogo en la reunión, escriba la respuesta como comentarios.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/desktop-in-meeting-dialog-view.png" alt-text="Vista escritorio en reunión.":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

Después de entrar en la reunión y agregar la aplicación desde el escritorio o la web, la aplicación es visible en la reunión de Teams móvil en la sección **Aplicaciones** . Seleccione **Aplicaciones** para mostrar la lista de aplicaciones. El usuario puede iniciar cualquiera de las aplicaciones como un panel del lado de la reunión de la aplicación.

Se muestra el cuadro de diálogo en la reunión donde puede escribir la respuesta como comentarios.

:::image type="content" source="~/assets/images/apps-in-meetings/mobile-in-meeting-dialog-view.png" alt-text="Vista del cuadro de diálogo Móvil":::

> [!NOTE]
> No es necesario cambiar el manifiesto de aplicación para que las aplicaciones funcionen en dispositivos móviles.

---

> [!NOTE]
>
> * Las aplicaciones pueden aprovechar el SDK de cliente de Teams para acceder `meetingId`a , `userMri`y `frameContext` representar la experiencia adecuadamente.
> * Si el cuadro de diálogo en la reunión se representa correctamente, envía una notificación de que los resultados se descargan correctamente.
> * El manifiesto de aplicación especifica los lugares en los que quieres que aparezcan las aplicaciones. Para ello, especifique el campo de contexto en el manifiesto. También forma parte de una experiencia de la fase de reunión de uso compartido, según [las directrices de diseño](~\apps-in-teams-meetings\design\designing-apps-in-meetings.md) especificadas.

En la imagen siguiente se muestra el panel del lado de la reunión:

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/in-meeting-dialog1.png" alt-text="Panel del lado de la reunión":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="~/assets/images/apps-in-meetings/sidepanelmobile.png" alt-text="Mobilel del panel lateral en la reunión":::

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

:::image type="content" source="~/assets/images/apps-in-meetings/post.png" alt-text="Pestaña Contoso con resultados.":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="~/assets/images/apps-in-meetings/mobilepremeeting.png" alt-text="Experiencia de la aplicación posterior a la reunión.":::

---

#### <a name="apps-in-channel-meeting"></a>Aplicaciones en la reunión del canal

Una reunión de canal programada pública tiene la misma lista de aplicaciones que su equipo primario. La instalación de una aplicación en una reunión de canal también hace que esté disponible en el equipo primario y viceversa.

Sin embargo, las instancias de tabulación de una reunión de canal son independientes de las pestañas del propio canal. Por ejemplo, supongamos que un canal "Desarrollo" tiene una pestaña "Polly". Si crea una reunión "Standup" en ese canal, esa reunión no tendría una pestaña "Polly", hasta que agregue explícitamente [la pestaña a la reunión](#to-add-tabs-to-an-existing-meeting).

En las reuniones de canal programadas públicas, después de agregar una pestaña de reunión se puede acceder a ella desde la página de detalles de la reunión seleccionando en el objeto de reunión. Vea el ejemplo siguiente:

:::image type="content" source="~/assets/images/apps-in-meetings/after-a-meeting1.png" alt-text="Después de una reunión":::

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>Integración de bots en el ciclo de vida de la reunión

Los bots que están habilitados en `groupchat` el ámbito comienzan a funcionar en las reuniones. Para implementar bots, comience con [la compilación de un bot](../build-your-first-app/build-bot.md) y, a continuación, continúe con [la creación de aplicaciones para reuniones de Teams](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references).

### <a name="integrate-message-extensions-into-the-meeting-lifecycle"></a>Integración de extensiones de mensaje en el ciclo de vida de la reunión

Para implementar la extensión de mensaje, comience con [la compilación de una extensión de mensaje](../messaging-extensions/how-to/create-messaging-extension.md) y, a continuación, continúe con [la creación de aplicaciones para reuniones de Teams](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references).

Las aplicaciones de reuniones unificadas de Teams permiten diseñar la aplicación en función de los roles de participantes en una reunión.

## <a name="participant-roles-in-a-meeting"></a>Roles de participante en una reunión

:::image type="content" source="~/assets/images/apps-in-meetings/participant-roles.png" alt-text="Roles participantes en una reunión.":::

La configuración predeterminada de los participantes la determina el administrador de TI de una organización. A continuación se muestran los roles de participante en una reunión:

* **Organizador**: el organizador programa una reunión, establece las opciones de reunión, asigna roles de reunión e inicia la reunión. Solo los usuarios con la cuenta de Microsoft 365 y la licencia de Teams pueden ser organizadores y controlar los permisos de los asistentes. Un organizador de reuniones puede cambiar la configuración de una reunión específica. Los organizadores pueden realizar estos cambios en la página web **Opciones de reunión** .
* **Moderador**: los moderadores tienen las mismas capacidades de los organizadores con exclusiones. Un moderador no puede quitar un organizador de la sesión ni modificar las opciones de reunión de la sesión. De forma predeterminada, los participantes que se unen a una reunión tienen el rol de moderador.
* **Asistente**: se invita a un asistente a asistir a una reunión, pero no puede actuar como moderador. Los asistentes pueden interactuar con otros miembros de la reunión, pero no pueden administrar ninguna configuración de reunión ni compartir el contenido.

> [!NOTE]
> Solo un organizador o moderador puede agregar, quitar o desinstalar aplicaciones.

Para obtener más información, consulte [roles en una reunión de Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

Después de diseñar la aplicación en función de los roles de participante en una reunión, puede identificar cada tipo de usuario para las reuniones y seleccionar a qué puede acceder.

## <a name="user-types-in-a-meeting"></a>Tipos de usuario en una reunión

Los tipos de usuario, como en el inquilino, invitado, federado o usuario externo de una reunión, pueden realizar uno de los [roles participantes en una reunión](#participant-roles-in-a-meeting).

> [!NOTE]
> El tipo de usuario no se incluye en la API **getParticipantRole** .

Los tipos de usuario, como, organizador, moderador o asistente en una reunión, pueden ser [participantes en una reunión](#participant-roles-in-a-meeting).

En la lista siguiente se detallan los distintos tipos de usuario junto con su accesibilidad y rendimiento:

* **En el inquilino**: los usuarios del inquilino pertenecen a la organización y tienen credenciales en Azure Active Directory (AAD) para el inquilino. Son empleados a tiempo completo, in situ o remotos. Un usuario en el inquilino puede ser organizador, moderador o asistente.
* **Invitado**: un invitado es un participante de otra organización invitado a acceder a Teams u otros recursos del inquilino de la organización. Los invitados se agregan a Azure AD de la organización y tienen las mismas funcionalidades de Teams que un miembro nativo del equipo. Tienen acceso a chats de equipo, reuniones y archivos. Un invitado puede ser organizador, moderador o asistente. Para obtener más información, consulte [acceso de invitado en Teams](/microsoftteams/guest-access).
* **Federado o externo**: un usuario federado es un usuario externo de Teams de otra organización al que se ha invitado a unirse a una reunión. Los usuarios federados tienen credenciales válidas con asociados federados y Están autorizados por Teams. No tienen acceso a los equipos ni a otros recursos compartidos de su organización. El acceso de invitado es una mejor opción para que los usuarios externos tengan acceso a equipos y canales. Para obtener más información, consulte [Administración del acceso externo en Teams](/microsoftteams/manage-external-access).

    > [!NOTE]
    > Los usuarios de Teams pueden agregar aplicaciones cuando hospedan reuniones o chats con otras organizaciones. Los usuarios pueden usar aplicaciones compartidas por usuarios externos cuando los usuarios se unan a reuniones o chats hospedados por otras organizaciones. Las directivas de datos de la organización del usuario de hospedaje, así como las prácticas de uso compartido de datos de las aplicaciones de terceros compartidas por la organización de ese usuario, estarán en vigor.

    > [!IMPORTANT]
    > En este momento, las aplicaciones de terceros están disponibles en Government Community Cloud (GCC), pero no están disponibles para GCC-High y el Departamento de Defensa (DOD). Las aplicaciones de terceros están desactivadas de forma predeterminada para GCC. Para activar aplicaciones de terceros en GCC, consulte [administrar directivas de permisos de aplicaciones](/microsoftteams/teams-app-permission-policies) y [administrar aplicaciones](/microsoftteams/manage-apps).

* **Anónimo**: los usuarios anónimos no tienen una identidad de Azure AD y no están federados con un inquilino. Los participantes anónimos son como usuarios externos, pero su identidad no se muestra en la reunión. Los usuarios anónimos no pueden acceder a las aplicaciones de una ventana de reunión. Un usuario anónimo no puede ser organizador, pero puede ser moderador o asistente.

    > [!NOTE]
    > Los usuarios anónimos heredan la directiva de permisos de aplicación de nivel de usuario predeterminada global. Para obtener más información, vea [Administrar aplicaciones](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).

En la tabla siguiente se proporcionan los tipos de usuario y se enumeran las características a las que cada usuario puede acceder en las reuniones:

| Tipo de usuario | Pestañas | Bots | Extensiones de mensajería | Tarjetas adaptables | Módulos de tareas | Diálogo en la reunión | Fase de reunión |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Usuario anónimo | No disponible | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | No disponible | No disponible | No disponible |
| Invitado, parte del inquilino de Azure AD | Se permite la interacción. No se permiten crear, actualizar y eliminar. | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde la tarjeta adaptable. | Disponible | Puede iniciar, ver e interactuar con la aplicación en la fase de reunión solo en el cliente de escritorio de Teams y los dispositivos móviles de Teams. |
| Para obtener más información, consulte [Usuarios no estándar](/microsoftteams/non-standard-users). | La interacción se permite en las reuniones programadas. No se permiten crear, actualizar y eliminar. | Se permite la interacción. No se permiten adquirir, actualizar y eliminar. | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde la tarjeta adaptable. | No disponible | Puede iniciar, ver e interactuar con la aplicación en la fase de reunión solo en el cliente de escritorio de Teams y los dispositivos móviles de Teams. |

> [!NOTE]
>
> El comportamiento de los distintos tipos de usuario de las aplicaciones de las llamadas es idéntico a su comportamiento en las reuniones programadas, a excepción de lo siguiente:
>
> * Los usuarios federados no pueden interactuar con las aplicaciones de pestaña en las llamadas.
> * Si se agregan usuarios federados a una llamada existente con usuarios en el inquilino o invitados, todos los participantes perderán la capacidad de agregar, actualizar o quitar aplicaciones. Sin embargo, solo los usuarios locales o invitados existentes podrían interactuar con las aplicaciones que se agregaron antes de invitar a los usuarios federados a la llamada.
> * En el móvil, los usuarios anónimos no podrán acceder a las aplicaciones en las reuniones programadas del canal público.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Requisitos previos y referencias de API para las aplicaciones en las reuniones de Teams](create-apps-for-teams-meetings.md)

## <a name="see-also"></a>Vea también

* [Tab](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [Bot](../bots/what-are-bots.md)
* [Extensión de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Diseño de la aplicación](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Informe de asistencia a reuniones de Microsoft Teams](/microsoftteams/teams-analytics-and-reports/meeting-attendance-report)
* [Configurar la opción de grabación de la reunión en OneDrive para la Empresa y SharePoint](/MicrosoftTeams/tmr-meeting-recording-change#set-up-the-meeting-recording-option-for-onedrive-for-business-and-sharepoint)
