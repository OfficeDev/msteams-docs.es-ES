---
title: Puntos de entrada para aplicaciones de Teams
author: heath-hamilton
description: Describe dónde pueden los usuarios descubrir y usar su aplicación en Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 72ce2620160f854bbe458821db01e91d2d9f62cd
ms.sourcegitcommit: 098d38dd947e87e69d289b99e807bea2d95c42f9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2020
ms.locfileid: "49713630"
---
# <a name="entry-points-for-teams-apps"></a>Puntos de entrada para aplicaciones de Teams

La plataforma de Teams ofrece un conjunto flexible de puntos de entrada en los que los usuarios pueden descubrir y usar su aplicación. Su aplicación puede ser tan simple como incrustar contenido web existente en una pestaña o una aplicación con varias facetas con la que los usuarios interactúen en varios contextos.

Las aplicaciones de mayor éxito son las que parecen nativas de Teams, por lo que es importante planificar cuidadosamente los puntos de entrada de su aplicación.

## <a name="teams-channels-and-chats"></a>Equipos, canales y chats

Los equipos, canales y chats son espacios de colaboración. Las aplicaciones en estos contextos están disponibles para cualquier usuario en dicho espacio y se suelen centrar en flujos de trabajo adicionales o en establecer nuevas interacciones sociales.

Aquí tiene una explicación sobre cómo se suelen usar las funciones de la aplicación de Teams en los contextos colaborativos:

* Las [**pestañas**](~/tabs/what-are-tabs.md) ofrecen una experiencia web insertada en pantalla completa configurada para el equipo, canal o chat de grupo. Todos los miembros interactúan con el mismo contenido basado en la web, por lo que es habitual una experiencia de aplicación de una sola página sin estado.

* Las [**extensiones de mensajería**](~/messaging-extensions/what-are-messaging-extensions.md) son accesos directos para insertar contenido externo en una conversación o para tomar acciones en mensajes sin salir de Teams. El despliegue de vínculos proporciona contenido enriquecido al compartir contenido desde una dirección URL común.

* Los [**bots**](~/bots/what-are-bots.md) interactúan con los miembros de la conversación a través del chat y responden a eventos (como agregar un nuevo miembro o cambiar el nombre de un canal). Las conversaciones con un bot en estos contextos son visibles para todos los miembros del equipo, canal o grupo, por lo que las conversaciones con bots deberían ser relevantes para todos.

* Los [**webhooks y conectores**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permiten a un servicio externo publicar mensajes en una conversación y a los usuarios enviar mensajes a un servicio.

* La [**API de REST de Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) obtiene datos sobre equipos, canales y chats de grupo para ayudar a automatizar y a administrar procesos de Teams.

## <a name="personal-apps"></a>Aplicaciones personales

Las [aplicaciones personales](~/concepts/design/personal-apps.md) se centran en las interacciones con un solo usuario. La experiencia en este contexto es única para cada usuario.

Aquí tiene una explicación sobre cómo se suelen usar las funciones de Teams en los contextos personales:

* Los [**bots**](~/bots/what-are-bots.md) mantienen conversaciones individuales con un usuario. Los bots que requieren conversaciones de varios turnos o que proporcionan notificaciones relevantes solo para un usuario específico son más adecuados en las aplicaciones personales.

* Las [**pestañas**](~/tabs/what-are-tabs.md) ofrecen una experiencia web insertada de pantalla completa que resulta significativa para el usuario que la ve.

## <a name="examples"></a>Ejemplos

Las directrices de diseño de aplicaciones de Teams proporcionan elementos visuales detallados que muestran dónde pueden los usuarios encontrar y usar aplicaciones de Teams.

> [!div class="nextstepaction"]
> [Ver las directrices de diseño de aplicaciones de Teams](../concepts/design/design-teams-app-overview.md)
