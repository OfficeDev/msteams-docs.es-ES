---
title: Entender los casos de uso
author: clearab
description: Entender los casos de uso
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 270771ecc47bbfc03a33d1603f680bc3424989ad
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231620"
---
# <a name="understand-your-use-cases"></a>Entender los casos de uso

La plataforma de Microsoft Teams ofrece una gran variedad de puntos de [extensibilidad](~/concepts/extensibility-points.md) y elementos de interfaz de usuario de los que su aplicación puede aprovechar. Si aún no tiene una buena comprensión de lo que es posible en la plataforma teams, primero debe leer ese artículo.

Cada método de interacción con los usuarios tiene sus propios puntos fuertes y débiles. La creación de una aplicación de Teams increíble se trata de encontrar la combinación adecuada para satisfacer las necesidades del usuario. Si va a satisfacer esas necesidades, primero debe comprenderlas.

## <a name="what-problem-are-you-trying-to-solve"></a>¿Qué problema está intentando resolver?

Cada aplicación buena tiene un problema principal (o necesidad) que está intentando resolver; antes de empezar a crear, debes articular cuál es ese problema. En su corazón, Teams es una plataforma de colaboración, por lo que las aplicaciones que buscan resolver problemas de colaboración son una excelente opción. También es una plataforma social, es nativamente multiplataforma, se encuentra en el centro de Office 365 y ofrece un lienzo personal en el que puede crear aplicaciones. Hay una gran variedad de necesidades que se pueden resolver con una aplicación de Teams, solo tiene que asegurarse de que comprende cuál está intentando resolver.

## <a name="who-are-you-solving-it-for"></a>¿Para quién lo estás resolviendo?

A veces esto puede ser obvio: "El sistema de supervisión de mi equipo necesita enviar alertas en algún lugar, necesitamos poder analizarlas realmente rápidamente y ninguno de nosotros desea comprobar nuestro correo electrónico". A veces, el público objetivo puede crecer a lo largo del tiempo: "Nuestro equipo de trabajo es realmente relatorio de nuestro sistema de alertas y ahora quieren actuar". Comprender quiénes son los usuarios le ayudará a identificar el modelo de distribución correcto, pero lo que es más importante le ayudará a identificar *cómo usan Teams.* ¿Son principalmente trabajadores de primera línea en clientes móviles? ¿Esperas que muchos usuarios invitados necesiten acceso a tu aplicación? ¿Usan equipos y canales, o principalmente chats grupales? ¿Qué tan sofisticadas técnicamente son? ¿Necesitará una experiencia de incorporación exhaustiva o lo harán algunos punteros?

A veces, la respuesta es "Queremos resolver este problema para todos los usuarios del equipo en todas partes". Si ese es el caso para ti, querrás dedicar algo de tiempo a comprender lo que se necesita para [publicarse en AppSource.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)

## <a name="do-you-need-authentication"></a>¿Necesita autenticación?

Debes identificar desde el principio si vas a necesitar proteger los servicios que expones y en qué nivel. Recuerde que los servicios web que mostrará en su aplicación de Teams están disponibles públicamente a través de Internet, por lo que si necesita protegerlos, empiece a pensar en cómo hacerlo ahora.

## <a name="should-the-entire-app-be-in-teams"></a>¿Toda la aplicación debe estar en Teams?

Tanto si está creando algo totalmente nuevo como si va a introducir una solución existente en Teams, es importante decidir si toda la aplicación va a estar dentro del cliente de Teams o si tiene sentido traer solo una parte de la experiencia. Con una combinación de pestañas, extensiones de mensajería, módulos de tareas, tarjetas interactivas y bots de conversación, puede crear aplicaciones complejas completamente dentro de Teams. Sin embargo, eso no siempre tiene sentido. Recuerde quiénes son los usuarios y el problema que está intentando resolver. ¿Ya tienen un sistema para resolver la mayor parte del problema y solo necesita ampliar un subgrupo de funcionalidades en Teams? Por lo general, si solo va a incluir una parte de la solución, debe centrarse en el uso compartido, la colaboración y la iniciación y supervisión de flujos de trabajo.

## <a name="what-will-the-onboarding-experience-be-like"></a>¿Cómo será la experiencia de incorporación?

La experiencia de incorporación puede ser la diferencia entre el éxito o el error de la aplicación. Para cada funcionalidad de la aplicación y para cada contexto en el que se puede instalar esa funcionalidad, debes tener un plan sobre cómo te vas a presentar. La forma en que se presenta el bot de conversación cuando se instala en un canal con miles de personas probablemente será diferente de cuando se instala en un chat de uno a uno. ¿Qué sucede cuando un usuario configura la pestaña por primera vez en un canal? Si estás compartiendo tarjetas con una extensión de mensajería, ¿tiene sentido agregar un pequeño vínculo a una página de "más información" para ayudar a presentar a los usuarios qué más puede hacer tu aplicación?

Saber quiénes son los usuarios le ayudará a crear la experiencia correcta. ¿Esperas que la mayoría de las personas ya tengan algún contexto de para qué está tu aplicación o que ya han usado los servicios en otro contexto? ¿O van a llegar a la aplicación sin conocimientos previos? Diseña tu experiencia de incorporación pensando en los usuarios clave.

Recuerda también que los usuarios pueden descubrir la aplicación de varias maneras: pueden ser los que la instalan o pueden introducirse en la aplicación cuando otro miembro del equipo la usa para compartir contenido. Si quieres que tu aplicación se extienda, debes buscar formas de presentarte a todos los usuarios.

Por encima de todo, recuerde que a nadie le gusta el correo no deseado. Una buena forma de deshacerse de los mensajes personales y de canal es una buena forma de no instalarse rápidamente.

## <a name="next-steps"></a>Pasos siguientes

* [Asignar los casos de uso a la funcionalidad](~/concepts/design/map-use-cases.md)
* [Elegir cómo distribuir la aplicación](../deploy-and-publish/overview.md)

## <a name="learn-more"></a>Más información

* [Diseñar pestañas eficaces](~/tabs/design/tabs.md)
* [Crear bots sorprendentes](~/bots/design/bots.md)

