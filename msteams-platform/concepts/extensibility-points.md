---
title: Puntos de entrada para las aplicaciones de Microsoft Teams
author: heath-hamilton
description: Describe cómo y dónde usan la aplicación las personas en Microsoft Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 1c68467177fc440993f059133f049f18785374b7
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209784"
---
# <a name="entry-points-for-teams-apps"></a>Puntos de entrada para las aplicaciones de Microsoft Teams

La plataforma de Microsoft Teams proporciona un conjunto flexible de puntos de entrada en los que los usuarios pueden descubrir y usar la aplicación. La aplicación puede ser tan sencilla como insertar un sitio web existente en una pestaña personal o una aplicación multifaceta con la que los usuarios interactúan en varios puntos de entrada.

Las aplicaciones más correctas se sienten de forma nativa en Teams, por lo que es importante planear cuidadosamente los puntos de entrada de la aplicación.

## <a name="teams-channels-and-group-chats"></a>Equipos, canales y chats en grupo

Los equipos, canales y chats de grupo son espacios de colaboración. Las aplicaciones que usan estos puntos de entrada están disponibles para todos los miembros y normalmente se centran en flujos de trabajo adicionales o desbloqueando nuevas interacciones sociales.

Esta es la manera en que las funcionalidades de la aplicación Teams se usan comúnmente en contextos de colaboración:

* Las [**pestañas**](~/tabs/what-are-tabs.md) proporcionan una experiencia web incrustada a pantalla completa configurada para el equipo, el canal o el chat de grupo. Todos los miembros interactúan con el mismo contenido basado en Web, por lo que una experiencia de aplicación de una sola página sin estado es típica.

* [**Las extensiones de mensajería**](~/messaging-extensions/what-are-messaging-extensions.md) son accesos directos para insertar contenido externo en una conversación o realizar acciones en mensajes sin salir de Microsoft Teams. Vínculo unfurling proporciona contenido enriquecido al compartir contenido desde una dirección URL común.

* Los [**bots**](~/bots/what-are-bots.md) interactúan con los miembros de la conversación a través de chat y responden a los eventos (como agregar un nuevo miembro o cambiar el nombre de un canal). Las conversaciones con un bot en estos contextos son visibles para todos los miembros del equipo, canal o grupo, por lo que las conversaciones del robot deben ser relevantes para todos los usuarios.

* Los [**webhooks y los conectores**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permiten que un servicio externo publique mensajes en una conversación y los usuarios envíen mensajes a un servicio.

* [**API de REST de Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) para obtener datos sobre equipos, canales y chats de grupo para ayudar a automatizar y administrar los procesos de Teams.

## <a name="personal-apps"></a>Aplicaciones personales

Las [aplicaciones personales](~/concepts/design/personal-apps.md) se centran en las interacciones con un único usuario. La experiencia en este contexto es única para cada usuario. Los usuarios pueden anclar aplicaciones personales en el riel de navegación izquierdo para un acceso rápido.

Esta es la forma en que las funcionalidades de Microsoft Teams se usan con frecuencia en contextos personales:

* Los [**bots**](~/bots/what-are-bots.md) tienen conversaciones de uno en uno con un usuario. Los bots que requieren conversaciones de varios turnos o proporcionan notificaciones relevantes solo para un usuario específico son los más adecuados en contextos personales.

* Las [**pestañas**](~/tabs/what-are-tabs.md) proporcionan una experiencia Web integrada a pantalla completa que tiene sentido para los usuarios individuales.

## <a name="ui-components"></a>Componentes de la interfaz de usuario

Las aplicaciones suelen mostrar uno o varios componentes estándar de la interfaz de usuario de Microsoft Teams. La creación de la aplicación con estos componentes conduce a experiencias enriquecidas que se sienten nativas para los usuarios de Teams.

### <a name="cards"></a>Tarjetas

Las [tarjetas](~/task-modules-and-cards/what-are-cards.md) son contenedores de interfaz de usuario definidos por JSON que pueden contener texto con formato, medios, controles (como menús desplegables y botones de radio) y botones que activan una acción.

Las acciones de tarjeta pueden enviar cargas a la API de la aplicación, abrir un vínculo, iniciar flujos de autenticación o enviar mensajes a conversaciones. La plataforma de Microsoft Teams admite varias tarjetas, incluidas tarjetas adaptables, tarjetas de héroe, tarjetas de miniaturas y mucho más. Puede combinar colecciones de tarjetas y visualizarlas en una lista o carrusel.

### <a name="task-modules"></a>Módulos de tareas

Los [módulos de tareas](~/task-modules-and-cards/what-are-task-modules.md) proporcionan experiencias modales en Microsoft Teams. Son especialmente útiles para iniciar flujos de trabajo, recopilar datos del usuario o Mostrar información enriquecida como vídeos o paneles de Power BI. En los módulos de tareas, puede ejecutar código Front-end personalizado, mostrar un `<iframe>` Widget o mostrar una tarjeta adaptable.

A la hora de considerar cómo desea compilar la aplicación, recuerde que los modales son naturales para que los usuarios escriban información o completen tareas en comparación con una experiencia de ficha o de robot basada en conversaciones.

### <a name="deep-links"></a>Vínculos profundos

La aplicación puede crear [vínculos profundos de URL](~/concepts/build-and-test/deep-links.md) para ayudar a navegar al usuario a través de la aplicación y el cliente de Microsoft Teams. Puede crear un vínculo profundo para la mayoría de las entidades de Microsoft Teams, y algunos (como una nueva convocatoria de reunión) le permiten rellenar previamente la información mediante el uso de cadenas de consulta en la dirección URL.

Por ejemplo, el bot conversante podría enviar un mensaje a un canal con un vínculo profundo a un módulo de tareas que da como resultado que una tarjeta se envíe como un mensaje uno a uno a un usuario, que a su vez contiene un vínculo profundo para crear una nueva reunión con un usuario específico en una fecha y hora determinada. Use vínculos profundos para conectarse a través de los distintos puntos de extensión disponibles para la aplicación y mantenga a su usuario en el contexto correcto en todo momento.

### <a name="web-based-content"></a>Contenido basado en Web

El [contenido basado en Web](~/tabs/how-to/create-tab-pages/content-page.md) es una página web que se hospeda y que se puede incrustar en un módulo de pestaña o de tareas.
