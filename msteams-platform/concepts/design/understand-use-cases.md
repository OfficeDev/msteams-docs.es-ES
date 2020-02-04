---
title: Comprender los casos de uso
author: clearab
description: Decidir cómo distribuir la aplicación
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: ef1007c21e79cd69155b64f02d2980bcf6a708b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676035"
---
# <a name="understand-your-use-cases"></a>Comprender los casos de uso

La plataforma de Microsoft Teams ofrece una gran variedad de [puntos de extensibilidad y elementos](~/concepts/extensibility-points.md) de la interfaz de usuario que la aplicación puede aprovechar. Si aún no tiene una buena comprensión de lo que es posible en la plataforma de Microsoft Teams, primero debe leer ese artículo.

Cada método de interacción con los usuarios tiene sus propios puntos fuertes y débiles. La creación de una aplicación de Awesome Teams consiste en encontrar la combinación correcta para satisfacer las necesidades del usuario. Si va a cumplir esas necesidades, primero debe comprenderlos.

## <a name="what-problem-are-you-trying-to-solve"></a>¿Qué problema intenta resolver?

Cada buena aplicación tiene un problema principal (o necesita) que está tratando de resolver, antes de empezar a compilar necesita articular lo que ese problema es. En su corazón, Teams es una plataforma de colaboración, por lo que las aplicaciones que buscan resolver problemas de colaboración son muy apropiadas. También es una plataforma social, que se basa de forma nativa en varias plataformas, se basa en el corazón de Office 365 y ofrece un lienzo personal para crear aplicaciones en. Hay una amplia variedad de necesidades que se pueden resolver con una aplicación de Microsoft Teams, solo Asegúrese de que comprende qué está tratando de resolver.

## <a name="who-are-you-solving-it-for"></a>¿A quién le está resolviendo?

A veces esto puede ser obvio: "el sistema de supervisión de mi equipo necesita enviar alertas en algún lugar, tenemos que ser capaces de debatirlas realmente rápidamente y ninguno de nosotros queremos comprobar nuestro correo electrónico". A veces, la audiencia de destino puede crecer a lo largo del tiempo: "nuestro equipo hermana es realmente Jealous de nuestro sistema de alertas y ahora quieren en la acción". Conocer quiénes son los usuarios que le ayudarán a identificar el modelo de distribución adecuado, pero lo que es más importante, le ayudarán a identificar *Cómo usan Microsoft Teams*. ¿Son principalmente los trabajadores de primera línea en clientes móviles? ¿Espera que una gran cantidad de usuarios invitados necesiten tener acceso a su aplicación? ¿Usan equipos y canales, o principalmente chats en grupo? ¿Qué son los técnicamente sofisticados? ¿Necesitará una experiencia completa de incorporarse o le harán algunos punteros?

A veces, la respuesta es "queremos resolver este problema para todos los usuarios del equipo en todas partes". Si ese es el caso, querrá dedicar algún tiempo a comprender lo que [se necesita para publicar en AppSource](~/concepts/deploy-and-publish/appsource/prepare/overview.md).

## <a name="do-you-need-authentication"></a>¿Necesita autenticación?

Debe identificar antes si va a necesitar proteger los servicios que está exponiendo y en qué nivel. Recuerde que los servicios web que se van a exponer en la aplicación de Microsoft Teams están disponibles públicamente a través de Internet, por lo que, si necesita protegerlos, empiece a pensar cómo ahora.

## <a name="should-the-entire-app-be-in-teams"></a>¿Debe estar toda la aplicación en Teams?

Tanto si está creando algo completamente nuevo como si va a llevar una solución existente a Microsoft Teams, es importante que decida si toda la aplicación va a estar dentro del cliente de Microsoft Teams, o si tiene sentido realizar solo una parte de la experiencia. Con una combinación de pestañas, extensiones de mensajería, módulos de tareas, tarjetas interactivas y bots de conversación, puede crear aplicaciones complejas en su totalidad dentro de Microsoft Teams. Sin embargo, esto no tiene sentido siempre. Recuerde quiénes son sus usuarios y el problema que está tratando de resolver. ¿Ya tienen un sistema para solucionar la mayor parte del problema y solo tiene que ampliar un subconjunto de la funcionalidad a teams? Por lo general, si solo va a traer una parte de la solución, debe centrarse en el uso compartido, la colaboración y la inicialización y la supervisión de los flujos de trabajo.

## <a name="what-will-the-onboarding-experience-be-like"></a>¿Qué aspecto tendrá la experiencia de incorporación?

La experiencia de incorporación puede ser la diferencia entre el éxito o el error de la aplicación. Para cada funcionalidad de la aplicación y para cada contexto en el que se puede instalar la funcionalidad, debe tener un plan sobre cómo se va a presentar usted mismo. La forma en que se presenta el bot? a de conversación cuando se instala en un canal con mil personas probablemente será diferente de cuando se instala en un chat de uno a uno. ¿Qué sucede cuando un usuario configura la pestaña en un canal por primera vez? Si va a compartir tarjetas con una extensión de mensajería, ¿tiene sentido agregar un pequeño vínculo a una página "más información" para facilitar la introducción de los usuarios a otros elementos que pueden hacer la aplicación?

Conocer quiénes son sus usuarios le ayudarán a diseñar la experiencia correcta. ¿Espera que la mayoría de los usuarios ya tengan algún contexto de la aplicación para la que se encuentre o que ya haya usado sus servicios en otro contexto? ¿O está llegando a su aplicación sin conocimientos previos? Diseñe la experiencia de incorporación con los usuarios clave en mente.

Recuerde también que los usuarios pueden descubrir la aplicación de varias maneras, es posible que las instalen o que se les haya agregado a la aplicación cuando otro miembro del equipo la use para compartir contenido. Si quiere que la aplicación se extienda, debe buscar formas de presentarse a sí mismo a todos los usuarios.

Por encima de todo lo demás, recuerde que nadie le gusta correo no deseado. La repetición de mensajes personales y de canal es una buena forma de obtener una instalación rápida.

## <a name="next-steps"></a>Siguientes pasos

* [Asignar los casos de uso a la funcionalidad](~/concepts/design/map-use-cases.md)
* [Elegir cómo distribuir la aplicación](~/concepts/deploy-and-publish/apps-publish.md)

## <a name="learn-more"></a>Más información

* [Diseño de pestañas efectivas](~/tabs/design/tabs.md)
* [Crear bots increíbles](~/bots/design/bots.md)

