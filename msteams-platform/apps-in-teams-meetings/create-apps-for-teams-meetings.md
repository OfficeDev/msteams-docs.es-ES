---
title: Requisitos previos para las aplicaciones en las reuniones de Teams
author: surbhigupta
description: Identificar requisitos previos con aplicaciones para Teams reuniones
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: 9ac6e87a8f85d0e8d73c6bf58dd705a55f887f43
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720235"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Requisitos previos para las aplicaciones en las reuniones de Teams

Con aplicaciones para Teams reuniones, puedes expandir las capacidades de tus aplicaciones en todo el ciclo de vida de la reunión. Antes de trabajar con aplicaciones para Teams reuniones, debes cumplir los siguientes requisitos previos:

* Saber cómo desarrollar aplicaciones Teams aplicaciones. Para obtener más información sobre cómo desarrollar Teams aplicación, consulta [Teams desarrollo de aplicaciones.](../overview.md)

* Actualiza el Teams de la aplicación para indicar que la aplicación está disponible para reuniones. Para obtener más información, consulta [manifiesto de la aplicación](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).

* Usa la aplicación que admite pestañas configurables en el ámbito groupchat. Para obtener más información, vea [ámbito de chat de grupo](../resources/schema/manifest-schema.md#configurabletabs) y cree una pestaña de [grupo.](../build-your-first-app/build-channel-tab.md)

* Siga las directrices generales Teams diseño de pestañas para escenarios previos y posteriores a la reunión. Para obtener experiencias durante las reuniones, consulte las directrices de diseño de la pestaña en la reunión y del cuadro de diálogo en la reunión. Para obtener más información, [vea Teams de](../tabs/design/tabs.md)diseño de pestañas, directrices de diseño de pestañas en la reunión y directrices de diseño de cuadros de diálogo en la [reunión.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)

* Admite el `groupchat` ámbito para habilitar la aplicación en chats previos y posteriores a la reunión. Con la experiencia de la aplicación antes de la reunión, puedes encontrar y agregar aplicaciones de reunión y realizar las tareas previas a la reunión. Con la experiencia de la aplicación posterior a la reunión, puedes ver los resultados de la reunión, como los resultados de encuestas o la tarifa
* Los parámetros de dirección URL de la API de reunión deben `meetingId` `userId` tener , y `tenantId` . Los parámetros están disponibles como parte de la actividad Teams SDK de cliente y bot. Además, puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la [autenticación de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)

* La `GetParticipant` API debe tener un registro de bot y un identificador para generar tokens de autenticación. Para obtener más información, vea [bot registration and ID](../build-your-first-app/build-bot.md).

* Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión. Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión. Para el cuadro de diálogo en la reunión, vea el parámetro de `bot Id` finalización en `NotificationSignal` la API.

* La `Meeting Details` API debe tener un registro de bot e id. de bot. Requiere bot SDK para obtener `TurnContext` .

* Para eventos de reunión en tiempo real, debe estar familiarizado con el objeto disponible a través `TurnContext` del SDK de bot. El `Activity` objeto en contiene la carga con la hora de inicio y finalización `TurnContext` real. Los eventos de reunión en tiempo real requieren un identificador de bot registrado de Teams plataforma.

* Tener parámetros `meetingId` , y en la dirección URL de la API de `userId` `tenantId` reunión. Los parámetros están disponibles como parte de la actividad Teams SDK de cliente y bot. Además, puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la [autenticación de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)

* Tener un registro de bot y un identificador en la `GetParticipant` API para generar tokens de autenticación. Para obtener más información, vea [bot registration and ID](../build-your-first-app/build-bot.md).

* Mantenga la aplicación actualizada en función de las actividades de eventos de la reunión. Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión. Para el cuadro de diálogo en la reunión, compruebe el parámetro de `bot Id` finalización en `NotificationSignal` la API.

* Tener un registro de bot e id. de bot en la `MeetingDetails` API. Requiere bot SDK para obtener `TurnContext` .

* Familiarícese con el `TurnContext` objeto disponible a través del SDK de bot. El `Activity` objeto en contiene la carga con la hora de inicio y finalización `TurnContext` real. Los eventos de reunión en tiempo real requieren un identificador de bot registrado de Teams plataforma.

Una vez que hayas pasado por los requisitos previos, puedes usar las referencias de api de aplicaciones de reunión , , y que te permiten tener acceso a la información mediante atributos y mostrar `GetUserContext` `GetParticipant` contenido `NotificationSignal` `Meeting Details` relevante.

> [!NOTE]
> Teams SDK de JavaScript (_versión_: 1.10 y versiones posteriores) para que SSO funcione en el panel lateral de la reunión.

## <a name="see-also"></a>Vea también

* [Directrices de diseño de cuadros de diálogo en la reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
* [Aplicaciones para Teams reuniones](teams-apps-in-meetings.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Referencias API de aplicaciones de reuniones](API-references.md)
