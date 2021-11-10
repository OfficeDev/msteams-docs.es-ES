---
title: Descripción de los casos de uso de la aplicación
author: heath-hamilton
description: Planear la aplicación, comprender el usuario y sus necesidades, comprender los problemas de usuario que resolvería la aplicación, planear la autenticación de usuario y su experiencia de incorporación
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 835e40e2c93387ee7db9fab7eb1f8c56951019c9
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888422"
---
# <a name="understand-your-use-cases"></a>Entender los casos de uso

La Microsoft Teams ofrece una gran variedad de puntos de entrada y elementos de [interfaz](../../concepts/extensibility-points.md) de usuario que la aplicación puede aprovechar.
> [!NOTE]
> Antes de empezar a crear los casos de uso, debe tener una buena comprensión de las Teams y de lo que es posible en la plataforma Teams usarlas.

Cada método de interacción con los usuarios tiene sus puntos fuertes y débiles. Crear una aplicación Teams es encontrar la combinación adecuada para satisfacer las necesidades del usuario. If you're going to meet those needs, you first need to understand them.

## <a name="understand-the-problem"></a>Comprender el problema

Cada aplicación tiene un problema principal o una necesidad de resolver. Antes de empezar a crear una aplicación, debes expresar cuál es ese problema. En su corazón, Teams es una plataforma de colaboración, por lo que las aplicaciones que puentean las diferencias para lograr una colaboración eficaz son un gran ajuste. También es una plataforma social, es nativamente multiplataforma, se encuentra en el centro de Office 365 y ofrece un lienzo personal para crear aplicaciones. En esta plataforma social, hay una amplia variedad de necesidades que se pueden resolver con una Teams aplicación. Puede resolver una amplia variedad de problemas, siempre que comprenda cuál está intentando resolver. Antes de empezar a crear una aplicación, haga preguntas relevantes, como:

* ¿Cuáles son las ventajas y desventajas del sistema de estado actual que usan los usuarios?
* ¿Cuáles son los problemas a los que se enfrentan los usuarios que desea abordar?
* ¿Qué características o capacidades les gustan y les gusta a los usuarios en su forma actual de realizar el proceso?

## <a name="understand-your-user"></a>Comprender al usuario

Comprenda quién es su usuario y puede identificar el modelo de distribución adecuado. Le ayuda a identificar cómo usan los usuarios Teams. Haga preguntas relevantes, como:

* ¿Los usuarios son principalmente trabajadores de primera línea en clientes móviles?
* ¿Esperas que muchos usuarios invitados necesiten acceso a la aplicación?
* ¿Usan equipos y canales o principalmente chats de grupo?
* ¿Qué tan sofisticados técnicamente son los usuarios principales?
* ¿Necesita una experiencia de incorporación exhaustiva o algunos punteros pueden hacer?

A veces, la respuesta es que queremos resolver este problema para todos los *Teams en todas partes.* Si ese es el caso, dedóstese un poco de tiempo en comprender lo que se necesita para [publicarse en AppSource](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).

## <a name="understand-the-limitations-of-the-app"></a>Comprender las limitaciones de la aplicación

Conocer las limitaciones de las aplicaciones para la accesibilidad de datos y el requisito de residencia de datos te ayudará a diseñar mejores aplicaciones. Esto es importante, ya que tener información sobre quién es el propietario de los datos y la disponibilidad de las API afecta a la arquitectura de la solución. De nuevo, haga preguntas relevantes, como:

* ¿Cuáles son los desafíos con la integración back-end de la aplicación actual?
* Quién es propietario de los datos back-end? In-house or third-party.
* ¿Hay firewalls que afectan al funcionamiento de la aplicación?
* ¿Hay API para tener acceso a los datos que necesitas para el funcionamiento de la aplicación? 

## <a name="provide-authentication"></a>Proporcionar autenticación

Debe identificar desde el principio si necesita proteger los servicios que está exponiendo y en qué nivel. Recuerde que los servicios web expuestos en la aplicación Teams están disponibles públicamente a través de Internet. Por lo tanto, si necesita protegerlos, empiece a pensar en ello ahora. Si necesita una solución que requiera proporcionar acceso de invitado a los usuarios externos al inquilino, se deben colocar restricciones y permisos de acceso para proteger la información confidencial. Deberás diseñar aplicaciones teniendo en cuenta las limitaciones que vienen con el acceso de usuario invitado. Por lo tanto, haga preguntas, como: 

* ¿Tendrán los usuarios acceso a diferentes vistas de datos en función de sus roles?
* ¿Hay PII implicado?
* ¿Las interacciones también se basarán en los roles de usuario?
* ¿Los usuarios externos tendrán acceso a la aplicación?

## <a name="decide-what-goes-in-teams"></a>Decida qué va en Teams

Tanto si estás creando algo nuevo o llevando una solución existente a Teams, es importante decidir si toda la aplicación va a estar dentro del Teams cliente. Compruebe si tiene sentido traer solo una parte de la experiencia. Con una combinación de pestañas, extensiones de mensajería, módulos de tareas, tarjetas adaptables y bots conversacionales, puedes crear aplicaciones complejas completamente en Teams.
Recuerde quiénes son los usuarios y el problema que está intentando resolver. ¿Ya tienen un sistema para resolver la mayor parte del problema o solo necesita extender un subgrupo de la funcionalidad a Teams? Normalmente, si va a incluir una parte de la solución, debe centrarse en compartir, colaborar, iniciar y supervisar flujos de trabajo.

## <a name="plan-the-onboarding-experience"></a>Planificar la experiencia de incorporación

La experiencia de incorporación puede ser la diferencia entre el éxito o el error de la aplicación. Para cada funcionalidad de la aplicación y cada contexto en el que se pueda instalar la funcionalidad, debes tener un plan de cómo te vas a presentar. La forma en que se presenta el bot de conversación cuando se instala en un canal con mil personas es diferente cuando se instala en un chat uno a uno. ¿Qué sucede cuando un usuario configura la pestaña por primera vez en un canal? Si estás compartiendo tarjetas con una extensión de mensajería, ¿tiene sentido agregar un pequeño vínculo **a** una página más para ayudar a introducir a los usuarios a lo que puede hacer la aplicación?

Saber quiénes son los usuarios, le ayuda a crear la experiencia correcta. ¿Esperas que la mayoría de las personas ya tengan algún contexto de para qué está la aplicación o que ya han usado los servicios en otro contexto? ¿Vienen a la aplicación sin conocimientos previos? Crea tu experiencia de incorporación pensando en los usuarios clave.

Recuerde que los usuarios pueden descubrir la aplicación de varias maneras. Pueden ser los que la instalan o pueden introducirse en la aplicación cuando otro usuario la usa para compartir contenido. Si quieres que más usuarios usen la aplicación, debes buscar formas de presentarte a todos.

Sobre todo, recuerda que a nadie le gusta el correo no deseado. La limpieza de mensajes personales y de canal es una buena forma de deshacer la instalación rápidamente.

## <a name="plan-for-the-future"></a>Planear el futuro

Identifique qué nuevas características prefiere tener el usuario en la solución actual. Si tienes una guía básica para nuevas características que agregar a la aplicación, el diseño y la arquitectura se verán afectados.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Asignar los casos de uso](../../concepts/design/map-use-cases.md)

## <a name="see-also"></a>Consulte también

[Funciones del dispositivo](~/concepts/device-capabilities/device-capabilities-overview.md)
