---
title: Creación de una aplicación para Microsoft Teams
author: clearab
description: Comprenda el proceso típico para compilar una aplicación para Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7ec67c52f9321579da34c490175f6becc3a8fdfd
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120258"
---
# <a name="building-an-app-for-microsoft-teams"></a>Creación de una aplicación para Microsoft Teams

La creación y distribución de una aplicación integrada en la plataforma de Microsoft Teams implica decidir qué se va a crear, crear los servicios Web, crear un paquete de aplicaciones y distribuir ese paquete a los usuarios finales de destino. Corresponderá a los administradores de una organización decidir quién puede tener acceso e instalar la aplicación, y los usuarios tendrán que instalar la aplicación en cualquier contexto en particular.

## <a name="design-a-great-app"></a>Diseñar una aplicación fantástica

El paso más importante en la creación de una aplicación correcta para Microsoft Teams es elegir los puntos de extensibilidad y los elementos de la interfaz de usuario de combinación correctos para aprovecharlos. A veces, se trata de una decisión bastante fácil, pero para aplicaciones más complejas debe dedicar mucho tiempo a comprender el problema que está tratando de resolver con la aplicación y asignar la solución en las distintas formas en que los usuarios pueden interactuar con la aplicación en el cliente de Microsoft Teams. No subestimar la importancia del contexto y el ámbito. Un bot de conversación que funciona muy bien en una conversación de uno a uno no funciona en absoluto como parte de una conversación en grupo o una conversación de canal.

1. En primer lugar, [comprenda los puntos de extensibilidad del cliente de Microsoft Teams y los elementos](~/concepts/extensibility-points.md) de la interfaz de usuario disponibles para la aplicación.

2. A continuación, asegúrese [de que comprende los casos de uso](~/concepts/design/understand-use-cases.md).

3. Por último, [asigne los casos de uso a las características de la plataforma de Teams](~/concepts/design/map-use-cases.md).

Una vez que haya decidido qué puntos y características de extensibilidad debe aprovechar la aplicación, le conviene que piense en cada una de esas interacciones. Según el diseño de la aplicación, es posible que quiera consultar:

* [Diseño de grandes pestañas](~/tabs/design/tabs.md)
* [Diseño de bots de conversación útiles](~/bots/design/bots.md)

## <a name="prepare-your-environment"></a>Preparar el entorno

Debe asegurarse de que tiene un entorno en el que puede cargar y probar la aplicación de Microsoft Teams. Si aún no tiene una suscripción de O365 con Microsoft Teams habilitada y la capacidad de cargar aplicaciones en ella, puede [registrarse en el programa para desarrolladores de o365](https://developer.microsoft.com/microsoft-365/dev-program) que le proporcionará acceso a una suscripción gratuita de Office 365 con fines de desarrollo.

Vea [preparar el entorno de O365](~/concepts/build-and-test/prepare-your-o365-tenant.md) para obtener más información.

## <a name="build-and-test-your-app"></a>Compilar y probar la aplicación

La creación y prueba de la aplicación para Microsoft Teams no es muy diferente a la creación de cualquier otra aplicación Web. La principal diferencia es la necesidad de usar el manifiesto de la aplicación en el paquete de la aplicación para conectar el cliente de Teams a los servicios Web. Siempre que realice un cambio en el manifiesto de la aplicación, tendrá que volver a cargar el paquete de la aplicación y actualizar la aplicación en Teams volviendo a instalarlo. Cambios en el servicio Web sin embargo, no es necesario que vuelva a instalar la aplicación en el cliente de Microsoft Teams.

Cuando se crea inicialmente la aplicación, se actualizan los servicios web y el paquete de la aplicación con regularidad, lo que suele volver a cargar e instalar la aplicación en el cliente de Microsoft Teams varias veces (especialmente durante la configuración inicial de la aplicación). Sin embargo, como lo que se está creando estabiliza la necesidad de modificar el manifiesto de la aplicación se reducirá y se realizarán principalmente cambios en el servicio Web.

### <a name="build-your-web-services"></a>Compilar los servicios Web

Una vez que haya decidido cómo los usuarios van a interactuar con la aplicación, su tiempo para crear los servicios web para potenciarla. En función de lo que esté creando, Teams ofrece varios SDK, plantillas, ejemplos de código y generadores para ayudarle a empezar, incluidos:

* Bot Framework SDK para [las extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) y los [bots de conversación](~/bots/what-are-bots.md)
* SDK del cliente de Microsoft Teams para [pestañas](~/tabs/what-are-tabs.md) y otras páginas de contenido
* Un [generador de Yeoman](~/tutorials/get-started-yeoman.md) para la creación de aplicaciones en node. js
* **Vista previa** Un conjunto de controles de código abierto para las páginas de contenido web: [interfaz de usuario de Fluent](https://microsoft.github.io/fluent-ui-react/)
* [Plantillas de aplicación](~/samples/app-templates.md) de producción lista para usar
* Varios [ejemplos](~/samples/code-samples.md) que le ayudarán a empezar

Recuerde que tendrá que hospedar los servicios Web de manera que puedan ser accesibles públicamente a través de Internet (normalmente en un proveedor de servicios en la nube como Azure) y servir el contenido a través de HTTPS.

### <a name="create-your-app-package"></a>Crear el paquete de la aplicación

También tendrá que crear un paquete de aplicación que se puede distribuir e instalar en Microsoft Teams. El paquete de la aplicación contiene dos iconos y un archivo de manifiesto JSON que describe los metadatos de la aplicación, los puntos de extensión que usa la aplicación y punteros a los servicios que encienden los puntos de extensión.

Al crear el paquete de la aplicación, puede elegir crearlo manualmente o usar App Studio, que es una aplicación dentro de Microsoft teams que le ayuda a realizar las aplicaciones de Microsoft Teams (conocemos, muy meta). App Studio le guiará en la creación del manifiesto de la aplicación y puede ayudarle a registrar el bot con el marco de trabajo de bot. También contiene un diseñador de tarjetas que le ayuda a crear tarjetas y acciones de tarjeta visualmente y a enviarle ejemplos en Microsoft Teams.

## <a name="distributing-your-app"></a>Distribución de la aplicación

Tiene tres opciones para la [distribución de la aplicación de Microsoft Teams](~/concepts/deploy-and-publish/apps-publish.md), en función de la audiencia de destino.

* **Comparte directamente el paquete de la aplicación.** Puede elegir compartir el paquete de la aplicación directamente con los usuarios. Esto es especialmente útil si la aplicación está dirigida a un público limitado (solo un par de equipos o individuos) y durante el desarrollo y prueba de la aplicación.
  
* **Publique la aplicación en el catálogo de aplicaciones de la organización.** Si la aplicación es aplicable a una organización específica (o si ha personalizado la aplicación para satisfacer las necesidades específicas de la organización), un administrador de inquilinos puede cargar la aplicación en el catálogo de aplicaciones de la organización. Esto hace que la aplicación esté disponible para que cualquier usuario de la organización la instale (pero no la instala automáticamente).
  
* **Publique la aplicación en la tienda de aplicaciones pública.** Si la aplicación está pensada para todos los usuarios de Microsoft Teams en todas partes, puede enviar la aplicación para su publicación en el almacén de aplicaciones públicas. Tendrá que pasar por un proceso de revisión riguroso, por lo que debe asegurarse de que ha punteado en la i y la Cruz de su t.

Al distribuir la aplicación, debe tener en cuenta no solo el público que desea, pero las directivas de TI en su lugar en la organización con la que desea compartir la aplicación. Cada organización tiene un control total sobre la determinación de las aplicaciones que se cargarán en el catálogo de aplicaciones de la organización y las aplicaciones que estarán disponibles para su instalación desde la tienda de aplicaciones.

### <a name="the-app-you-create-versus-the-app-your-users-install"></a>La aplicación que cree frente a la aplicación que instalen los usuarios

La aplicación puede aprovechar varios puntos de extensibilidad en el cliente de Microsoft Teams y trabajar en una variedad de ámbitos. El paquete de la aplicación que distribuya a los usuarios definirá todos estos como una única entidad. Sin embargo, dado que todas las instalaciones de aplicaciones en Microsoft Teams son *específicas del contexto*, es posible que la aplicación no siempre se instale para todos los usuarios.

Por ejemplo, Imagine que la aplicación contiene un bot Conversation que funciona tanto en conversaciones personales como en el equipo, así como en una pestaña personal y una ficha canal. Cuando la aplicación está instalada, se instalará en un contexto específico; si un usuario instala la aplicación en un equipo, no tiene que instalar necesariamente la parte personal de la aplicación. Esto puede ser un poco confuso en primer lugar, solo debe recordar que todas las partes de la aplicación se instalarán y se configurarán en cualquier contexto determinado.

## <a name="get-started-quickly"></a>Introducción rápida

¿Desea empezar rápidamente? Consulte uno de nuestros tutoriales de introducción o un tutorial para una característica de la plataforma determinada (que se encuentra en cada sección de características de la documentación).

Tutoriales de introducción:

* [Crear un bot y una aplicación de pestañas en C #](~/tutorials/get-started-dotnet-app-studio.md)
* [Compilar una aplicación de Bot y Tab en JavaScript/node. js](~/tutorials/get-started-nodejs-app-studio.md)
* [Crear una aplicación con el generador de Yeoman](~/tutorials/get-started-yeoman.md)
