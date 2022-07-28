---
title: Aplicaciones para reuniones de Teams
author: surbhigupta
description: En este artículo, aprenderá cómo funcionan las aplicaciones en las reuniones de Microsoft Teams en función del rol de participante y usuario y la extensibilidad de la aplicación.
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 5dc0793ee899d5423b81af6e07083fd03c8e5621
ms.sourcegitcommit: dd70fedbe74f13725e0cb8dd4f56ff6395a1c8bc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2022
ms.locfileid: "67058252"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Aplicaciones para reuniones y llamadas de Teams

Las reuniones permiten la colaboración, la asociación, la comunicación informada y los comentarios compartidos. La aplicación de reunión puede ofrecer una experiencia de usuario para cada fase del ciclo de vida de la reunión. El ciclo de vida de la reunión incluye experiencias de la aplicación previas a la reunión, en la reunión y posteriores a la reunión, según el estado del asistente.

> [!Note]
>
> Actualmente, las aplicaciones para reuniones instantáneas, llamadas uno a uno y llamadas grupales solo están disponibles en [versión preliminar para desarrolladores públicos](~/resources/dev-preview/developer-preview-intro.md).

Teams admite el acceso a las aplicaciones durante la reunión para los siguientes tipos de reunión:

* [**Reuniones programadas**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): reuniones programadas a través del calendario de Teams.
* [**Llamadas uno a uno**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798): llamadas iniciadas en el chat uno a uno.
* [**Llamadas de grupo**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798): llamadas iniciadas en el chat de grupo.
* [**Reuniones instantáneas**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5): reuniones iniciadas mediante el botón **Reunirse ahora** en el calendario de Teams.

Los usuarios pueden agregar aplicaciones a la reunión mediante la opción de su **+** ventana de reunión de Teams.

:::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="Adición de una aplicación en la reunión" border="true":::

Visite la [tienda teams](https://go.microsoft.com/fwlink/p/?LinkID=2183121) y explore las aplicaciones diseñadas específicamente para reuniones.

> [!Note]
>
> * Actualmente, la adición de una aplicación no se admite en dispositivos móviles. Sin embargo, un usuario puede ver la aplicación y compartirla para realizar la fase desde el móvil.
>
> * Actualmente, cuando se agrega una tercera persona a una llamada uno a uno, la llamada se eleva a una llamada de grupo que significa que se inicia una nueva sesión. Las aplicaciones agregadas a la llamada uno a uno no están disponibles en la llamada de grupo. Sin embargo, se pueden agregar de nuevo.
>
> * Actualmente, las experiencias de aplicación no se admiten en las reuniones del canal de Teams (reuniones programadas y reuniones instantáneas).

En la siguiente ilustración se ofrece una idea de las características de extensibilidad de la aplicación de reunión:

![Extensibilidad de la aplicación para reuniones](../assets/images/apps-in-meetings/meetingappextensibility.png)

En este artículo se proporciona información general sobre la extensibilidad de aplicaciones de reunión, las referencias de API, la habilitación y configuración de aplicaciones para reuniones y las escenas personalizadas del Modo conferencia en Teams.

Mejore su experiencia de reunión mediante la característica de extensibilidad de la reunión. Esta característica permite integrar las aplicaciones en reuniones. También incluye diferentes fases del ciclo de vida de una reunión donde poder integrar pestañas, bots y extensiones de mensajes. Puede identificar varios roles de participante y tipos de usuario, obtener eventos de reunión y generar diálogos en la reunión.

Para personalizar Teams con aplicaciones para reuniones, habilite las aplicaciones para reuniones de Teams actualizando el manifiesto de la aplicación y configure las aplicaciones para escenarios de reuniones.

Personalice el permiso de aplicación para miembros externos en el canal compartido, si la aplicación comparte información importante. Los permisos de aplicación en [canales compartidos](../concepts/build-and-test/Shared-channels.md) siguen la lista de aplicaciones del equipo host y la directiva de aplicación del inquilino del host.

La nueva característica de escenas personalizadas en Modo conferencia permite a los usuarios colaborar en una reunión con el equipo desde un solo lugar.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Aplicaciones de reuniones unificadas](meeting-app-extensibility.md)

## <a name="see-also"></a>Consulte también

* [Diseñar la extensión de reunión de Microsoft Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Referencias de API de aplicaciones de reunión: Teams](~/apps-in-teams-meetings/api-references.md)
* [Escenas personalizadas del Modo conferencia](~/apps-in-teams-meetings/teams-together-mode.md)
* [Habilitar y configurar las aplicaciones para reuniones de Teams](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
* [Ciclo de vida de la reunión](meeting-app-extensibility.md#meeting-lifecycle)
* [Colaboración mejorada con el SDK de Live Share](teams-live-share-overview.md)
