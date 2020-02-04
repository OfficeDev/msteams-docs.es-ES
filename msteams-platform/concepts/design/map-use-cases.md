---
title: Asignar los casos de uso a funcionalidades de aplicación
author: clearab
description: Decidir cómo distribuir la aplicación
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5ebfa73df9b4f2c83533a33fbc6366c2c0ccffb4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676037"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a>Asignar los casos de uso a las funcionalidades de la aplicación Teams

Si aún no lo ha hecho, asegúrese de que ha considerado atentamente [los casos de uso](~/concepts/design/map-use-cases.md) . También debe comprender bien los [puntos de extensibilidad y los elementos](~/concepts/extensibility-points.md) de la interfaz de usuario disponibles para la aplicación. Una vez que haya averiguado *lo* que intenta resolver y para el *que* está resolviendo, es el momento de empezar a pensar en *Cómo*hacerlo.

A continuación encontrará algunos escenarios comunes y una selección de puntos de extensibilidad y elementos de la interfaz de usuario que funcionan bien con ellos. No está pensada como una lista exhaustiva, solo para ayudarle a pensar en algunas de las posibilidades disponibles para usted y la plataforma de Microsoft Teams.

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a>Crear, compartir y colaborar en elementos de un sistema externo

La aplicación para Microsoft Teams es una buena forma de interactuar con los datos y hay una variedad de puntos de integración entre los que elegir.

* Extensiones de mensajería con comandos de búsqueda: buscar sistemas externos y compartir los resultados como una tarjeta interactiva.

* Extensiones de mensajería con comandos de acción: recopila información para insertarla en un almacén de datos o realizar búsquedas avanzadas.

* Pestañas: cree experiencias Web integradas para ver, trabajar y compartir datos.

* Conectores y webhooks: una forma sencilla de insertar datos en el cliente de Microsoft Teams y enviar datos fuera del cliente de Microsoft Teams.

* Módulos de tareas: formularios interactivos modales desde cualquier lugar en el que los necesite para recopilar o Mostrar información.

## <a name="initiate-workflows-and-processes"></a>Iniciar flujos de trabajo y procesos

A veces, solo necesita una forma rápida de iniciar un proceso o un flujo de trabajo en un sistema externo.

* Comandos de acción de las extensiones de mensajería: desencadenador de mensajes, lo que permite a los usuarios enviar rápidamente el contenido de un mensaje a los servicios Web.

* Módulos de tareas: ábralos desde una pestaña, un bot o una extensión de mensajería para recopilar información antes de iniciar un flujo de trabajo.

* Bots de conversación: interactúe con los usuarios a través de texto y tarjetas enriquecidas.

* Webhooks salientes: una buena opción para una interacción hacia delante sencilla cuando no es necesario crear un bot conversado completo.

## <a name="send-notifications-and-alerts"></a>Enviar notificaciones y alertas

Envíe notificaciones asincrónicas y alertas a los usuarios de Microsoft Teams. Use tarjetas interactivas para proporcionar acceso rápido a acciones de uso frecuente y vínculos a información adicional.

* Bots de conversación: envíe mensajes proactivos a grupos, canales o usuarios individuales.

* Conectores & webhooks entrantes: permitir que un canal se suscriba para recibir mensajes. Con un conector permiten que los usuarios personalicen la suscripción con una página de configuración.

## <a name="ask-questions-and-get-answers"></a>Formular preguntas y obtener respuestas

Las personas tienen preguntas. Probablemente, tiene muchas respuestas almacenadas en algún lugar. Desafortunadamente, a menudo es bastante difícil conectar ambos.

* Bots de conversación: procesamiento de lenguaje natural, AI, aprendizaje de máquina, todo el buzzwords. Use un bot con tecnología de la nube inteligente para conectar a los usuarios a las respuestas que necesitan.

* Pestañas: Inserte el portal web existente en Microsoft Teams o cree una versión específica de Teams para una mayor funcionalidad.

## <a name="get-social"></a>Obtener social

Una plataforma de colaboración es intrínsecamente una plataforma social. Permita que el lado creativo sea gratis y agréguele diversión en su lugar de trabajo.

* Todos ellos: enviar chistes, dar a prestigio, obtener algunos memes, descartar algunos emojis o cualquier otra cosa que llegue a su sofisticado.

## <a name="anything-you-can-do-in-a-single-page-app-spa"></a>Todo lo que puede hacer en una aplicación de página única (SPA)

Las pestañas son páginas web incrustadas. Casi todo lo que puede hacer en un SPA, puede hacer en una pestaña en Microsoft Teams. No olvide prestar atención a la pestaña ámbito-grupo y canal para experiencias compartidas, las pestañas personales son para... experiencias personales. La lista de materiales del equipo se encuentra en la pestaña canal, la lista de sus cosas se incluye en la pestaña personal.

## <a name="start-small"></a>Iniciar pequeño

¿No está seguro de dónde empezar? ¿Se siente un poco abrumado con la gran variedad de opciones disponibles para usted? No fret, elija una característica principal de la aplicación e inicie allí. Una vez que se siente con el flujo de información a través de los distintos contextos de Teams, será mucho más sencillo crear una interacción más compleja.

## <a name="putting-it-all-together"></a>En conclusión

Como se dice, las mejores aplicaciones suelen combinar varias características y crear una aplicación que atraiga a los usuarios en el contexto adecuado con la funcionalidad correcta en el momento adecuado. No intente forzar la funcionalidad en un punto en el que no pertenezca, solo porque tiene un bot? a de conversación de uno a uno que no significa que simplemente deba agregarlo a un equipo. Los puntos de extensibilidad diferentes son buenos para cosas diferentes; Juegue a sus puntos fuertes y la aplicación se destacará.
