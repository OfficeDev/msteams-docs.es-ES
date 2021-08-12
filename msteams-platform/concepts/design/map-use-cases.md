---
title: Asignar los casos de uso a Teams funcionalidades de la aplicación
author: surbhigupta
description: Identifica cómo pueden funcionar los casos de uso de la aplicación en la experiencia Teams aplicación.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 28f6b0af0854d19826d8f3542bb11ba0e025cbe1
ms.sourcegitcommit: 6a41c529a423c81a184c7a79125dbaaed0179788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2021
ms.locfileid: "53586036"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a>Asignar los casos de uso a Teams funcionalidades de la aplicación

Después de identificar *quién* es el usuario y *qué* problema  resolverá, es el momento de decidir cómo resolver el problema. *Quién,* *qué* y *cómo* completa el proceso de comprensión y asignación de los casos de uso a Teams funcionalidades de la aplicación. Debes definir el ámbito de la aplicación en función de las respuestas que has recibido del usuario a las consultas y, a continuación, decidir qué funcionalidad es la más adecuada para crear la aplicación.

> [!NOTE]
> Debes tener una buena comprensión de los puntos de entrada y los elementos de [interfaz de usuario](../../concepts/extensibility-points.md) disponibles para la aplicación. También debe asegurarse de que ha considerado cuidadosamente [los casos](../../concepts/design/understand-use-cases.md) de uso.

## <a name="choose-the-correct-scope-for-your-app"></a>Elegir el ámbito correcto para la aplicación

Al elegir el ámbito de la aplicación, tenga en cuenta lo siguiente:

* Una aplicación puede existir en todos los ámbitos.
* Las funcionalidades de la aplicación, como las extensiones de mensajería, siguen a los usuarios en todos los ámbitos.
* Los usuarios suelen dudar de agregar aplicaciones a Teams o canales.
* Los usuarios invitados pueden acceder al contenido expuesto en Teams o canales.

Puedes elegir entre el ámbito personal y el ámbito de equipo o canal de la aplicación en función de lo siguiente:

* Para el ámbito personal, haga las siguientes preguntas:
  * ¿Hay interacciones uno a uno con la aplicación necesarias por motivos de privacidad u otros motivos? Por ejemplo, comprobar el saldo de salida u otra información privada.
  * ¿Va a haber colaboración entre usuarios que podrían no tener una Teams? Por ejemplo, encontrar próximos eventos de toda la organización en una empresa.
  * ¿Hay notificaciones o mensajes personalizados que deban enviarse a un usuario a lo largo Teams experiencia de la aplicación? Por ejemplo, avisos de aprobaciones o registros.
* Para un ámbito compartido (equipo, canal o chat), haga las siguientes preguntas:
  * ¿La información presentada por la aplicación, ya sea en la pestaña o a través de un bot, es relevante y útil para la mayoría de los miembros de un equipo? Por ejemplo, aplicación Scrum.
  * ¿Podría cambiar el contexto de la aplicación en función del equipo al que se agrega? Por ejemplo, las tareas de Planner son diferentes en diferentes equipos. 
  * ¿Es posible que todos los miembros de una persona que necesiten colaborar sean parte de un solo equipo? Por ejemplo, agentes que trabajan en un vale.

Los siguientes escenarios te guiarán en la comprensión de la selección de puntos de entrada y elementos de interfaz de usuario que funcionan bien con las Teams de la aplicación:

> [!NOTE]
> No es una lista exhaustiva, pero le ayudará a pensar en algunas de las posibilidades disponibles.

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a>Crear, compartir y colaborar en elementos de un sistema externo

La aplicación Microsoft Teams es una excelente manera de interactuar con los datos y hay una variedad de puntos de integración entre los que elegir.

* **Extensiones de mensajería con comandos de búsqueda:** busque sistemas externos y comparta los resultados como una tarjeta interactiva.

* **Extensiones de mensajería con comandos de acción:** recopilar información para insertarla en un almacén de datos o realizar búsquedas avanzadas.

* **Pestañas:** cree experiencias web incrustadas para ver, trabajar con y compartir datos.

* **Conectores y webhooks:** una forma sencilla de insertar datos y enviar datos fuera del Teams cliente.

* **Módulos de** tareas: formularios modales interactivos desde donde los necesite para recopilar o mostrar información.

## <a name="initiate-workflows-and-processes"></a>Iniciar flujos de trabajo y procesos

A veces, solo necesita una forma rápida de iniciar un proceso o flujo de trabajo en un sistema externo.

* Comandos de acción extensiones **de mensajería:** desencadenador de mensajes, lo que permite a los usuarios enviar rápidamente el contenido de un mensaje a los servicios web.

* **Módulos de** tareas: ábralos desde una pestaña, un bot o una extensión de mensajería para recopilar información antes de iniciar un flujo de trabajo.

* **Bots conversacionales:** interactuar con los usuarios a través de texto y tarjetas enriquecciones.

* **Webhooks salientes:** una buena opción para una interacción simple de ida y vuelta cuando no es necesario crear un bot de conversación completo.

## <a name="send-notifications-and-alerts"></a>Enviar notificaciones y alertas

Enviar notificaciones asincrónicas y alertas a los usuarios en Teams. Use tarjetas interactivas para proporcionar acceso rápido a acciones y vínculos a información adicional que se usan con frecuencia.

* **Bots conversacionales:** enviar mensajes proactivos a grupos, canales o usuarios individuales.

* **Conectores y webhooks entrantes:** permitir que un canal se suscriba para recibir mensajes. Un conector permite a los usuarios adaptar la suscripción con una página de configuración.

## <a name="ask-questions-and-get-answers"></a>Hacer preguntas y obtener respuestas

La gente tiene preguntas y probablemente tiene muchas de las respuestas almacenadas en algún lugar. Desafortunadamente, a menudo es bastante difícil conectar los dos.

* **Bots conversacionales:** procesamiento de lenguaje natural, inteligencia artificial, aprendizaje automático y todas las palabras de voz. Usa un bot con tecnología de la nube inteligente para conectar a los usuarios con las respuestas que necesitan.

* **Pestañas:** inserte el portal web existente en Teams o cree una Teams específica para la funcionalidad agregada.

## <a name="get-social"></a>Obtener redes sociales

Una plataforma de colaboración es inherentemente una plataforma social. Deje que su lado creativo sea gratuito y agregue algo de diversión a su lugar de trabajo. Todos los usuarios deben ser capaces de enviar bromas, dar felicitaciones, obtener algunos memes, eliminar algunos emojis o cualquier otra cosa que le conste.

## <a name="think-in-terms-of-a-single-page-app"></a>Piense en términos de una aplicación de una sola página

Las pestañas son páginas web incrustadas. Prácticamente cualquier cosa que puedas hacer en un SPA, puedes hacer en una pestaña en Teams. Asegúrese de prestar atención al ámbito. Las pestañas de grupo y canal son para experiencias compartidas y las pestañas personales son para experiencias personales. La lista de cosas del equipo va en la pestaña canal y la lista de tus cosas va en la pestaña personal.

## <a name="start-small"></a>Iniciar pequeño

¿No está seguro de dónde empezar? ¿Se siente un poco abrumado por la increíble variedad de opciones disponibles para usted? Debes elegir una característica principal de la aplicación e iniciarla. Después de tener una idea del flujo de información a través de los distintos contextos de Teams, resulta mucho más sencillo imaginar una interacción más compleja.

## <a name="put-it-all-together"></a>Poner todo junto

Dicho esto, las mejores aplicaciones suelen combinar varias características, creando una aplicación que involucre a los usuarios en el contexto correcto con la funcionalidad adecuada en el momento adecuado. No debe forzar ninguna funcionalidad en un lugar al que no pertenezca. El hecho de que tenga un buen bot de conversación uno a uno no significa que lo agregue a ningún equipo. Los distintos puntos de extensibilidad son buenos para diferentes cosas y juegan a sus puntos fuertes para crear una aplicación correcta.

## <a name="see-also"></a>Vea también

[Crear la primera Microsoft Teams aplicación](../build-your-first-app/build-first-app-overview.md)
