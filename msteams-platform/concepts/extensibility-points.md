---
title: Puntos extensibles en el cliente de Microsoft Teams
author: clearab
description: Comprenda los puntos de extensibilidad disponibles para la aplicación en el cliente de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f65a5111bf59b08347291caa15c557dc0a48e886
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675780"
---
# <a name="extensible-points-in-the-teams-client"></a>Puntos extensibles en el cliente de Microsoft Teams

Una aplicación integrada en la plataforma de Microsoft Teams amplía el cliente de Microsoft Teams (Web, móvil y escritorio) con los servicios web que hospeda. La plataforma de Microsoft Teams proporciona un conjunto completo y flexible de puntos de extensibilidad, construcciones de interfaz de usuario y API para que pueda aprovecharse de la creación de la aplicación. La aplicación puede ser tan sencilla como incrustar el sitio web existente en una pestaña para el equipo o una aplicación de varias facetas y con características atractivas para los usuarios en toda la amplitud del cliente de Microsoft Teams. Puede optar por integrar una aplicación existente, o bien crear una nueva experiencia creada completamente para Microsoft Teams.

Hay varios lugares en los que se puede ampliar el cliente de Microsoft Teams para permitir que los usuarios interactúen con la aplicación. Según el escenario, puede elegir centrarse en un punto único de extensión (como un bot de conversación personal) o combinar varios puntos de extensión.

## <a name="teams-channels-and-group-chats"></a>Equipos, canales y chats de grupo

Los equipos, canales y chats de Grupo permiten que varios usuarios colaboren. Las aplicaciones en este contexto se hacen disponibles para todos los miembros del grupo o la conversación, normalmente se centran en habilitar flujos de trabajo de colaboración adicionales o desbloquear nuevas interacciones sociales. La aplicación tendrá acceso a las API que le permitirán obtener información sobre los miembros de la conversación, los canales de un equipo y los metadatos sobre el equipo o la conversación.

Se pueden extender con:

* Los **[bots de conversación](~/bots/what-are-bots.md)** interactúan con los miembros de la conversación a través de la charla y responden a los eventos (como un nuevo miembro que se agrega o un canal al que se cambia el nombre). Todas las conversaciones que tienen un bot en este contexto son visibles para todos los miembros del canal o grupo, por lo que tendrá que asegurarse de que la conversación es relevante para todos los usuarios.

* **[Pestañas configurables](~/tabs/what-are-tabs.md)** que proporcionan una experiencia Web integrada de pantalla completa configurada para el chat de canal o de grupo en el que está instalado. Todos los miembros interactuarán en la misma aplicación web compartida, por lo que una experiencia de aplicación de una sola página sin estado es típica.

* **[Webhooks y conectores](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)** que habilitan servicios externos para publicar mensajes en la conversación y los usuarios para enviar mensajes a su servicio. Puede aprovechar las acciones de tarjetas y tarjetas para crear mensajes sofisticados y accionables.

### <a name="personal-apps"></a>Aplicaciones personales

Las [aplicaciones personales](~/concepts/design/personal-apps.md) son una parte de la aplicación de Microsoft teams que se centra en las interacciones con un solo usuario. La experiencia es única para cada usuario individual. Esta parte de la aplicación puede anclarse al RAÍL de navegación izquierdo, lo que permite el acceso con un solo clic a los usuarios.

Pueden contener:

* **[Bots de conversación](~/bots/what-are-bots.md)** con una conversación de uno a uno con el usuario. Como esta es una conversación privada, si la aplicación necesita tener una conversación de varios turnos o proporcionar una notificación relevante para un solo usuario, suele ser mejor tener esa interacción en una aplicación personal.

* **[Pestañas personales](~/tabs/what-are-tabs.md)** que proporcionan una experiencia Web integrada a pantalla completa.

## <a name="messages"></a>Mensajes

Los mensajes son el corazón de la colaboración en Microsoft Teams. Con un **[comando de acción de extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md)**, la aplicación puede permitir a los usuarios invocar la API de la aplicación desde un mensaje y enviar el contenido del mensaje a la aplicación para su procesamiento o acción. La aplicación puede responder presentando un formulario (un módulo de tareas) al usuario para recopilar más información, enviar una respuesta al mensaje original o enviar un mensaje directamente al usuario.

## <a name="writing-messages"></a>Escribir mensajes

La aplicación puede ayudar a los usuarios a crear mensajes más efectivos permitiéndoles realizar búsquedas o realizar acciones en un sistema externo e insertar los resultados en un formato enriquecido y estructurado completo con botones accionables.

Hay tres formas en que la aplicación puede ayudar a los usuarios a crear mensajes mejores:

* **[Extensiones de mensajería: comandos de búsqueda](~/messaging-extensions/what-are-messaging-extensions.md)** que permiten realizar búsquedas rápidas en un sistema externo, obtener una vista previa de los resultados de la búsqueda y, a continuación, insertar el resultado en el chat como una tarjeta enriquecida.

* **[Messaging Extension-Link unfurling](~/messaging-extensions/what-are-messaging-extensions.md)** permite que su aplicación supervise los dominios web que le interesan. Cuando se pega una dirección URL que contiene ese dominio en el cuadro de mensaje de redacción, se invocará la API de la aplicación, lo que le permitirá agregar una tarjeta enriquecida al mensaje con información adicional sobre el elemento al que se va a vincular.

* **[Extensión de mensajería: los comandos de acción](~/messaging-extensions/what-are-messaging-extensions.md)** presentan al usuario un formulario modal (un módulo de tareas), envían los resultados del formulario a la aplicación y, a continuación, insertan un mensaje en la conversación directamente o crean parte de un mensaje que el usuario puede editar antes de enviarlo a la conversación.

## <a name="user-interface-ui-elements"></a>Elementos de la interfaz de usuario (UI)

Además de los puntos de extensibilidad, la plataforma de Microsoft Teams proporciona elementos de interfaz de usuario flexibles para que las aplicaciones aprovechen. Estos elementos le permiten crear experiencias enriquecidas que se sienten nativas para el cliente de Microsoft Teams.

### <a name="cards--card-actions"></a>Acciones de tarjetas de & tarjeta

Las [tarjetas](~/task-modules-and-cards/what-are-cards.md) son contenedores de interfaz de usuario definidos por JSON esquematizado, que pueden contener varias propiedades y datos adjuntos. Pueden contener texto, elementos multimedia, controles (como cuadros de lista desplegables y botones de radio) con formato y botones que desencadenan acciones de tarjetas. Las acciones de tarjeta pueden enviar cargas a la API de la aplicación, abrir un vínculo, iniciar flujos de autenticación o enviar mensajes a conversaciones. La plataforma de Microsoft Teams admite varios tipos de tarjetas, entre las que se incluyen tarjetas adaptables, tarjetas de héroe, tarjetas de miniaturas y mucho más. Se pueden combinar en colecciones de tarjetas y mostrar en una lista o carrusel.

### <a name="task-modules"></a>Módulos de tareas

Los [módulos de tareas](~/task-modules-and-cards/what-are-task-modules.md) le permiten crear experiencias de elemento emergente modal en su aplicación de Teams. Dentro del elemento emergente puede ejecutar su propio código HTML/JavaScript personalizado, mostrar un `<iframe>` widget como YouTube o Microsoft Stream video, o mostrar una tarjeta adaptable. Son especialmente útiles para iniciar y completar tareas o para mostrar información enriquecida como vídeos o paneles de Power BI. A menudo, una experiencia emergente es más natural para los usuarios que inician y completan tareas en comparación con una experiencia de ficha o de robot basada en conversaciones.

### <a name="deep-links"></a>Vínculos profundos

La aplicación puede crear [vínculos profundos de URL](~/concepts/build-and-test/deep-links.md) para ayudar a navegar al usuario a través de la aplicación y el cliente de Microsoft Teams. Puede crear un vínculo profundo para la mayoría de las entidades de Teams, y algunos (como una nueva convocatoria de reunión) le permiten rellenar previamente la información mediante el uso de cadenas de consulta en la dirección URL. Por ejemplo, el bot? a conversación podría enviar un mensaje a un canal con un vínculo profundo a un módulo de tareas que da como resultado una tarjeta que se envía como un mensaje uno a uno a un usuario, que a su vez contiene un vínculo profundo para crear una nueva reunión con un usuario específico en una determinada fecha y hora. Use vínculos profundos para conectarse a través de los distintos puntos de extensión disponibles para la aplicación y mantenga a su usuario en el contexto correcto en todo momento.

### <a name="web-content-pages"></a>Páginas de contenido web

Una [Página de contenido web](~/tabs/how-to/create-tab-pages/content-page.md) es una página web que se hospeda y que se puede incrustar en una pestaña o módulo de tareas. Para habilitar la página web para que se pueda insertar en un cliente de Microsoft Teams, debe:

* Estar hospedado en HTTPS.
* Poder ser incrustado en un `<iframe>` por el cliente de Microsoft Teams.
* Incluya el SDK del cliente de JavaScript de Microsoft Teams e invoque el método del `initialize()` SDK al cargar la página.
