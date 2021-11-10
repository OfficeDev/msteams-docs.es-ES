---
title: Puntos de entrada para aplicaciones de Teams
author: heath-hamilton
description: Describe los puntos de entrada de la aplicación, como el equipo, el canal y el chat en la experiencia personal y compartida de la aplicación
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 1bfaed5ec9c2ef1bec9dc3699dbb5914be213a44
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889086"
---
# <a name="entry-points-for-teams-apps"></a>Puntos de entrada para aplicaciones de Teams

La Teams proporciona un conjunto flexible de puntos de entrada, como equipo, canal y chat, donde los usuarios pueden descubrir y usar la aplicación. Su aplicación puede ser tan simple como incrustar contenido web existente en una pestaña o una aplicación con varias facetas con la que los usuarios interactúen en varios contextos.
Las aplicaciones más exitosas son nativas Teams, así que elige los puntos de entrada de la aplicación cuidadosamente.

## <a name="shared-app-experiences"></a>Experiencias de aplicaciones compartidas

El equipo, el canal y el chat son espacios de colaboración. Las aplicaciones en estos contextos están disponibles para todos los usuarios de ese espacio. Los espacios de colaboración suelen centrarse en flujos de trabajo adicionales o en desbloquear nuevas interacciones sociales.

En la siguiente lista se muestra cómo Teams funcionalidades de la aplicación se usan comúnmente en contextos de colaboración:

* Las [**pestañas**](~/tabs/what-are-tabs.md) ofrecen una experiencia web insertada en pantalla completa configurada para el equipo, canal o chat de grupo. Todos los miembros interactúan con el mismo contenido basado en web, por lo que es habitual una experiencia de aplicación sin estado de una sola página.

* Las [**extensiones de mensajería**](~/messaging-extensions/what-are-messaging-extensions.md) son accesos directos para insertar contenido externo en una conversación o para tomar acciones en mensajes sin salir de Teams. [La eliminación de vínculos](~/messaging-extensions/how-to/link-unfurling.md) proporciona contenido enriquecido al compartir contenido desde una dirección URL común.

* [**Los bots**](~/bots/what-are-bots.md) interactúan con los miembros de la conversación a través del chat y responden a eventos, como agregar un nuevo miembro o cambiar el nombre de un canal. 
   > [!NOTE]
   > Las conversaciones con un bot en estos contextos son visibles para todos los miembros del equipo, canal o grupo, por lo que las conversaciones de bot deben ser relevantes para todos.

* Los [**webhooks y conectores**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permiten a un servicio externo publicar mensajes en una conversación y a los usuarios enviar mensajes a un servicio.

* La [**API de REST de Microsoft Graph**](/graph/teams-concept-overview) obtiene datos sobre equipos, canales y chats de grupo para ayudar a automatizar y a administrar procesos de Teams.

## <a name="personal-app-experiences"></a>Experiencias de aplicaciones personales

Las [aplicaciones personales](../concepts/design/personal-apps.md) se centran en las interacciones con un solo usuario. La experiencia en este contexto es única para cada usuario.

En la siguiente lista se muestra cómo Teams funcionalidades se usan comúnmente en contextos personales:

* Los [**bots**](~/bots/what-are-bots.md) mantienen conversaciones individuales con un usuario. Los bots que requieren conversaciones de varios turnos o que proporcionan notificaciones relevantes solo para un usuario específico son más adecuados en las aplicaciones personales.

* [**Las pestañas**](~/tabs/what-are-tabs.md) proporcionan una experiencia web incrustada a pantalla completa que es significativa para el usuario que la está viendo.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Comprender casos de uso](../concepts/design/understand-use-cases.md)

## <a name="see-also"></a>Consulte también

[Teams de diseño de aplicaciones](../concepts/design/design-teams-app-overview.md) <br>
[Crear la primera Microsoft Teams aplicación](../build-your-first-app/build-first-app-overview.md)