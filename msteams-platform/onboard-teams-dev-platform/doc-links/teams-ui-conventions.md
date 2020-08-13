---
title: Determinación de los contextos de la aplicación Teams
author: heath-hamilton
description: En la planeación de la aplicación de Microsoft Teams, debe decidir si la aplicación se usará en espacios de colaboración, espacios personales o ambos.
ms.openlocfilehash: 05c92aa8b199cbdb58e477fb4a64467c150edbfd
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652197"
---
# <a name="getting-to-know-teams-ui-conventions"></a>Introducción a las convenciones de la interfaz de usuario de Microsoft Teams

Las aplicaciones normalmente presentan una o más convenciones de interfaz de usuario de Microsoft Teams estándar. La creación de las funciones de la aplicación mediante estas convenciones conduce a experiencias enriquecidas que se sienten nativas para los usuarios de Teams.

## <a name="cards"></a>Tarjetas

Las [tarjetas](~/task-modules-and-cards/what-are-cards.md) son contenedores de interfaz de usuario definidos por JSON esquematizado que pueden contener varias propiedades y datos adjuntos. Pueden contener texto con formato, medios, controles (como cuadros de lista desplegables y botones de radio) y botones que desencadenan acciones de tarjetas.

Las acciones de tarjeta pueden enviar cargas a la API de la aplicación, abrir un vínculo, iniciar flujos de autenticación o enviar mensajes a conversaciones. La plataforma de Microsoft Teams admite varios tipos de tarjetas, como tarjetas adaptables, tarjetas de héroe, tarjetas de miniaturas y mucho más. Puede combinar colecciones de tarjetas y mostrarlas en una lista o carrusel.

## <a name="task-modules"></a>Módulos de tareas

Los [módulos de tareas](~/task-modules-and-cards/what-are-task-modules.md) proporcionan experiencias de elemento emergente modal en Microsoft Teams. Son especialmente útiles para iniciar flujos de trabajo, recopilar datos del usuario o Mostrar información enriquecida como vídeos o paneles de Power BI. En los módulos de tareas, puede ejecutar código Front-end personalizado, mostrar un `<iframe>` Widget o mostrar una tarjeta adaptable.

A la hora de considerar cómo desea compilar la aplicación, recuerde que los modales son naturales para que los usuarios escriban información o completen tareas en comparación con una experiencia de ficha o de robot basada en conversaciones.

## <a name="deep-links"></a>Vínculos profundos

La aplicación puede crear [vínculos profundos de URL](~/concepts/build-and-test/deep-links.md) para ayudar a navegar al usuario a través de la aplicación y el cliente de Microsoft Teams. Puede crear un vínculo profundo para la mayoría de las entidades de Teams, y algunos (como una nueva convocatoria de reunión) le permiten rellenar previamente la información mediante el uso de cadenas de consulta en la dirección URL. 

Por ejemplo, el bot? a conversación podría enviar un mensaje a un canal con un vínculo profundo a un módulo de tareas que da como resultado una tarjeta que se envía como un mensaje uno a uno a un usuario, que a su vez contiene un vínculo profundo para crear una nueva reunión con un usuario específico en una determinada fecha y hora. Use vínculos profundos para conectarse a través de los distintos puntos de extensión disponibles para la aplicación y mantenga a su usuario en el contexto correcto en todo momento.

## <a name="web-based-content"></a>Contenido basado en Web

El [contenido basado en Web](~/tabs/how-to/create-tab-pages/content-page.md) es una página web que se hospeda y que se puede incrustar en un módulo de pestaña o de tareas. Para insertar la página web en el cliente de Teams, debe:

* Incluir `HTTPS` en la dirección URL.
* Estar incrustado en un `<iframe>` .
* Incluya el SDK cliente de JavaScript de Microsoft Teams e invoque el método del SDK `initialize()` al cargar la página.

## <a name="next-steps"></a>Pasos siguientes

* [Diseño de la aplicación](../../tabs/design/tabs.md)
