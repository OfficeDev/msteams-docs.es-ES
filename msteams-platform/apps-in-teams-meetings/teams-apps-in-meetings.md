---
title: Aplicaciones para reuniones de Teams
author: surbhigupta
description: En este artículo, aprenderá cómo funcionan las aplicaciones en las reuniones de Microsoft Teams en función del rol de participante y usuario y la extensibilidad de la aplicación.
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: f253a4ca3d09e48f99df36fdcb77bdd740fab5ff
ms.sourcegitcommit: bb15ce26cd65bec90991b703069424ab4b4e1a61
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/28/2022
ms.locfileid: "68772275"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Aplicaciones para reuniones y llamadas de Teams

Las reuniones permiten la colaboración, la asociación, la comunicación informada y los comentarios compartidos. El espacio de reuniones puede ofrecer una experiencia de usuario para cada fase del ciclo de vida de la reunión. En la siguiente ilustración se ofrece una idea de las características de extensibilidad de la aplicación de reunión:

:::image type="content" source="../assets/images/apps-in-meetings/meetingappextensibility.png" alt-text="En la captura de pantalla se muestra cómo funciona la extensibilidad de la aplicación de reunión.":::

Debe estar familiarizado con los siguientes conceptos de producto para crear experiencias de reunión personalizadas con aplicaciones en Microsoft Teams.

## <a name="supported-meeting-types-in-teams"></a>Tipos de reunión admitidos en Teams

Teams admite el acceso a las aplicaciones durante la reunión para los siguientes tipos de reunión:

* [**Reuniones programadas**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): reuniones programadas a través del calendario de Teams.
* [**Reuniones de canales programadas**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): reuniones programadas a través de canales públicos de Teams.
* [**Llamadas uno a uno**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798): llamadas iniciadas en el chat uno a uno.
* [**Llamadas de grupo**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798): llamadas iniciadas en el chat de grupo.
* [**Reuniones instantáneas**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5): reuniones iniciadas mediante el botón **Reunirse ahora** en el calendario de Teams.
* [**Seminario web**](https://support.microsoft.com/office/get-started-with-teams-webinars-42f3f874-22dc-4289-b53f-bbc1a69013e3): botón Seminario web iniciado a través del **seminario web** en la lista desplegable **Nueva reunión** .

Obtenga más información sobre [las reuniones, la expiración y las directivas](/MicrosoftTeams/meeting-expiration) y [las reuniones de Teams, seminarios web y eventos en directo](/microsoftteams/quick-start-meetings-live-events).
> [!NOTE]
>
> * Las aplicaciones para reuniones programadas de canales públicos solo están disponibles actualmente en versión [preliminar para desarrolladores públicos](../resources/dev-preview/developer-preview-intro.md).
> * Las aplicaciones no se admiten en lo siguiente:
>   * [Llamadas de Teams de red telefónica conmutada (RTC)](/microsoftteams/cloud-voice-landing-page#public-switched-telephone-network-connectivity-options)
>   * [Llamadas de Teams cifradas de un extremo a otro](https://support.microsoft.com/office/use-end-to-end-encryption-for-teams-calls-1274b4d2-b5c5-4b24-a376-606fa6728a90)
>   * [Reuniones de canales instantáneos](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)
>   * Reuniones en [un canal compartido](https://support.microsoft.com/office/what-is-a-shared-channel-in-teams-e70a8c22-fee4-4d6e-986f-9e0781d7d11d)

## <a name="meeting-lifecycle"></a>Ciclo de vida de la reunión

El ciclo de vida de una reunión incluye experiencia de aplicación previa a la reunión, en reunión y posterior a la reunión, según el tipo de usuario y el rol del usuario en una reunión de Teams.

## <a name="user-types-in-teams"></a>Tipos de usuario en Teams

Teams admite tipos de usuario, como en inquilino, invitado, usuario federado o externo en una reunión de Teams. Cada tipo de usuario puede tener uno de los [roles de usuario en la reunión de Teams](#user-roles-in-teams-meeting).

> [!NOTE]
>
> Actualmente, cuando se agrega una tercera persona a una llamada uno a uno, la llamada se eleva a una llamada de grupo que significa que se inicia una nueva sesión. Las aplicaciones agregadas a la llamada uno a uno no están disponibles en la llamada de grupo. Sin embargo, se pueden agregar de nuevo.

En la lista siguiente se detallan los distintos tipos de usuario junto con su accesibilidad:

* **En el inquilino**: los usuarios del inquilino pertenecen a la organización y tienen credenciales en Azure Active Directory (AAD) para el inquilino. Son empleados a tiempo completo, in situ o remotos. Un usuario en el inquilino puede ser organizador, moderador o asistente.
* **Invitado**: un invitado es un participante de otra organización invitado a acceder a Teams u otros recursos del inquilino de la organización. Los invitados se agregan a Azure AD de la organización y tienen las mismas funcionalidades de Teams que un miembro nativo del equipo. Tienen acceso a chats de equipo, reuniones y archivos. Un invitado puede ser organizador, moderador o asistente. Para obtener más información, consulte [acceso de invitado en Teams](/microsoftteams/guest-access).
* **Federado o externo**: un usuario federado o externo es un usuario de Teams de otra organización al que se ha invitado a unirse a una reunión. Los usuarios federados tienen credenciales válidas con asociados federados y Están autorizados por Teams. No tienen acceso a Teams ni a otros recursos compartidos de su organización. El acceso de invitado es una mejor opción para que los usuarios externos tengan acceso a Teams y canales. Para obtener más información, consulte [Administración del acceso externo en Teams](/microsoftteams/manage-external-access).

    > [!NOTE]
    > Los usuarios de Teams pueden agregar aplicaciones cuando hospedan reuniones o chats con otras organizaciones. Cuando un usuario externo comparte aplicaciones con la reunión, todo el usuario puede acceder a la aplicación. Las directivas de datos y las prácticas de uso compartido de datos de la organización host de las aplicaciones de terceros compartidas por la organización de ese usuario estarán en vigor.

* **Anónimo**: los usuarios anónimos no tienen una identidad de Azure AD y no están federados con un inquilino. Los participantes anónimos son como usuarios externos, pero su identidad no se muestra en la reunión. Los usuarios anónimos no pueden acceder a las aplicaciones de una ventana de reunión. Un usuario anónimo no puede ver el logotipo del bot en el chat de reunión. Un usuario anónimo puede ser moderador o asistente, pero no puede ser organizador.

    > [!NOTE]
    > Los usuarios anónimos heredan la directiva de permisos de aplicación de nivel de usuario predeterminada global. Para obtener más información, vea [Administrar aplicaciones](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).

## <a name="user-roles-in-teams-meeting"></a>Roles de usuario en la reunión de Teams

A continuación se muestran los roles de usuario en una reunión de Teams:

* **Organizador**: el organizador programa una reunión, establece las opciones de reunión, asigna roles de reunión, controla los permisos de los asistentes e inicia la reunión. Solo los usuarios con una cuenta de Microsoft 365 y una licencia de Teams pueden ser el organizador. Un organizador de reuniones puede cambiar la configuración de una reunión específica desde la [página **Opciones**](https://support.microsoft.com/en-us/office/change-participant-settings-for-a-teams-meeting-53261366-dbd5-45f9-aae9-a70e6354f88e) de la reunión.

* **Moderador**: los moderadores de una reunión tienen funcionalidades similares a las del organizador, con la excepción de quitar un organizador de la sesión y modificar las opciones de reunión para la sesión.

* **Asistente**: un asistente es un usuario que está invitado a asistir a la reunión. Los asistentes tienen funcionalidades limitadas durante la reunión.

> [!NOTE]
> Solo un organizador o moderador puede agregar, quitar o desinstalar aplicaciones.

Para obtener más información, consulte [roles en una reunión de Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

> [!TIP]
>
> * La [configuración predeterminada de los participantes](/microsoftteams/meeting-policies-participants-and-guests) la determina el administrador de TI de una organización.Según la configuración predeterminada, los participantes que se unan a una reunión tienen el rol de moderador.
> * El rol de moderador no está disponible en las llamadas uno a uno.
> * Un usuario que inicia la llamada de grupo desde un chat se considera organizador.

> [!IMPORTANT]
>
> * Actualmente, las aplicaciones de terceros están disponibles en Government Community Cloud (GCC), pero no están disponibles para los inquilinos de GCC-High y del Departamento de Defensa (DOD).
> * Las aplicaciones de terceros están desactivadas de forma predeterminada para GCC. Para activar aplicaciones de terceros en GCC, consulte [administrar directivas de permisos de aplicaciones](/microsoftteams/teams-app-permission-policies) y [administrar aplicaciones](/microsoftteams/manage-apps).

## <a name="see-also"></a>Consulte también

* [Diseñar la extensión de reunión de Microsoft Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Pestañas de compilación para la reunión](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Compilación de aplicaciones para la fase de reunión de Teams](build-apps-for-teams-meeting-stage.md)
* [Creación de una conversación extensible para el chat de reuniones](build-extensible-conversation-for-meeting-chat.md)
* [Compilación de aplicaciones para usuarios anónimos](build-apps-for-anonymous-user.md)
* [API de aplicaciones de reunión](meeting-apps-apis.md)
* [Colaboración mejorada con el SDK de Live Share](teams-live-share-overview.md)
* [Escenas personalizadas del Modo conferencia](~/apps-in-teams-meetings/teams-together-mode.md)
