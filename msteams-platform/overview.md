---
title: Plataforma para desarrolladores de Microsoft Teams
author: clearab
description: Página de información general que describe la plataforma para desarrolladores de Microsoft Teams y cómo empezar a compilar aplicaciones para Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: cb9d91f2de29bac00f4cdcd9672adf9d7d4ee734
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676206"
---
# <a name="what-are-microsoft-teams-apps"></a>¿Qué son las aplicaciones de Microsoft Teams?

Microsoft Teams es un espacio de trabajo de colaboración en Office 365 que se integra con las aplicaciones y los servicios que los usuarios usan para realizar el trabajo de forma conjunta. La plataforma de desarrolladores de Microsoft Teams facilita a los desarrolladores la integración de sus propias aplicaciones y servicios para mejorar la productividad, tomar decisiones con mayor rapidez, proporcionar el enfoque (reduciendo el cambio de contexto) y crear colaboración sobre el contenido existente y flujos. Las aplicaciones integradas en la plataforma Microsoft Teams son puentes entre el cliente de Microsoft Teams y los servicios y flujos de trabajo; la introducción directa en el contexto de la plataforma de colaboración.

## <a name="what-can-teams-apps-do"></a>¿Qué pueden hacer las aplicaciones de Microsoft Teams?

Las aplicaciones integradas en la plataforma de Microsoft Teams se centran principalmente en el aumento de la colaboración y la mejora de la productividad. La aplicación puede ser algo sencilla, como enviar notificaciones desde otros sistemas o aplicaciones multifacetas complejas. Solo tenga en cuenta que Teams es una plataforma de colaboración social; las mejores aplicaciones se centran en ayudar a los usuarios a expresarse y a trabajar mejor juntos.

* **Colaborar en elementos de sistemas externos.** Uno de los escenarios principales de una aplicación de Microsoft Teams es llevar la información o los elementos a Microsoft Teams desde otro lugar y tener una conversación a su alrededor. Puede insertar información en Microsoft Teams, habilitar a los usuarios para que busquen y los recuperen a petición, o para que estén disponibles en una vista Web incrustada.

* **Desencadenar flujos de trabajo desde conversaciones.** Con frecuencia, las conversaciones dan como resultado la necesidad de iniciar algún flujo de trabajo o realizar alguna acción; Tome una nota sobre eso, revise mi solicitud de incorporación de impuestos, conviértala en un responsable de ventas, etc. La aplicación de Microsoft Teams puede poner el acceso a ese flujo de trabajo dentro de Teams.

* **Notifique a su equipo sobre eventos importantes.** ¿Hay notificaciones de correo electrónico enfermas? Envíe notificaciones a teams en su lugar. Envíe notificaciones directamente a los usuarios, a un canal, a la fuente de actividades o a cualquier persona que se suscriba a ellos.

* **Incruste funcionalidad de otros sitios y servicios.** A veces solo necesita facilitar la detección de la aplicación. Inserte la aplicación de una sola página existente o cree algo desde el principio para Microsoft Teams.

## <a name="how-do-teams-apps-work"></a>¿Cómo funcionan las aplicaciones de Teams?

Lo primero que debe saber sobre las aplicaciones personalizadas para Microsoft Teams (aparte de lo sorprendente que pueden ser) es que Teams no es un servicio de hospedaje. El paquete de la aplicación contiene metadatos sobre la aplicación (nombre, iconos, etc.) y punteros a los servicios web que hospeda que encienden la aplicación. Microsoft Teams proporciona el mecanismo de distribución, construcciones de interfaz de usuario/experiencia del usuario para aprovechar las ventajas de y las API que puede usar para ampliar la información y las acciones disponibles para la aplicación.

Una aplicación de Microsoft Teams consta de tres partes principales:

* **El cliente de Microsoft Teams (Web, escritorio o móvil)** donde los usuarios interactuarán con la aplicación.
* **Paquete de la aplicación Teams** que crea la aplicación instalada por los usuarios y que contiene los metadatos y los punteros de la aplicación a sus servicios.
* **El servicio, el flujo de trabajo o el sitio web** que realizan la lógica, el almacenamiento de datos y las llamadas API necesarios para potenciar la aplicación.

Es importante tener en cuenta que cualquier funcionalidad que exponga en una aplicación de Microsoft Teams estará disponible públicamente a través de Internet, a menos que realice pasos adicionales para protegerla. Si proporciona acceso a información confidencial o protegida, le conviene que asegúrese de que los servicios se encuentran en un mínimo que autentiquen el punto de conexión que se conecta a la aplicación o que [autentiquen a los usuarios](~/concepts/authentication/authentication.md).

## <a name="how-can-you-share-your-teams-app"></a>¿Cómo puede compartir la aplicación de Teams?

Cuando esté listo para compartir las aplicaciones de Microsoft Teams, tiene tres opciones en función de quién es la audiencia de destino.

* **[Cargar la aplicación directamente](~/concepts/deploy-and-publish/apps-upload.md)** Si solo es necesario compartir la aplicación en su equipo o en algunas personas de la organización, puede compartir el paquete de la aplicación y cargarlo directamente.
* **[Publicar en el catálogo de aplicaciones de la organización](~/concepts/deploy-and-publish/apps-publish.md)** Puede compartir su aplicación con toda la organización a través del catálogo de aplicaciones.
* **[Publicar en la tienda de aplicaciones pública](~/concepts/deploy-and-publish/apps-publish.md)** Si la aplicación es para todos los usuarios, puede publicarla en nuestra tienda de aplicaciones pública. En función de sus objetivos, puede ser elegible para la asistencia de marketing y ventas.

## <a name="get-started"></a>Introducción

* [Crear un bot y una aplicación de pestañas en C #](~/tutorials/get-started-dotnet-app-studio.md)
* [Compilar una aplicación de Bot y Tab en JavaScript/node. js](~/tutorials/get-started-nodejs-app-studio.md)

## <a name="learn-more"></a>Más información

* [Puntos de extensibilidad en el cliente de Microsoft Teams](~/concepts/extensibility-points.md)
* [Creación de aplicaciones para Teams](~/concepts/building-an-app.md)
