---
title: Asigne los casos de uso a Teams capacidades de la aplicación
author: clearab
description: Identifique cómo pueden funcionar los casos de uso de la aplicación dentro de la experiencia Teams.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 179d0a37d72577c36f2cc44a11a8217cb9f016b2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566113"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a>Asigne los casos de uso a Teams capacidades de la aplicación

Después de haber identificado *quién* es el usuario y *qué* problema va a resolver, es el momento de decidir *cómo* resolver el problema. El *quién,* *qué* y *cómo* completa el proceso de comprensión y asignación de los casos de uso a Teams capacidades de la aplicación. Debe definir el ámbito de la aplicación en función de las respuestas que haya recibido del usuario a las consultas y, a continuación, decidir qué capacidad es la más adecuada para compilar la aplicación.

> [!NOTE]
> Debe tener una buena comprensión de los [puntos](../../concepts/extensibility-points.md) de entrada y los elementos de interfaz de usuario disponibles para la aplicación. También debe asegurarse de considerar [cuidadosamente sus casos de uso.](../../concepts/design/understand-use-cases.md)

## <a name="choose-the-correct-scope-for-your-app"></a>Elige el ámbito correcto para tu aplicación

Al elegir el ámbito de la aplicación, tenga en cuenta lo siguiente:

* Una aplicación puede existir en todos los ámbitos.
* Las capacidades de la aplicación, como las extensiones de mensajería, siguen a los usuarios entre ámbitos.
* Los usuarios a menudo dudan en agregar aplicaciones a Teams o canales.
* Los usuarios invitados pueden acceder al contenido expuesto en Teams o canales.

Puede elegir entre el ámbito personal y el ámbito de equipo o canal de la aplicación en función de lo siguiente:

* Para el alcance personal, haga las siguientes preguntas:
  * ¿Hay interacciones uno a uno con la aplicación necesarias por motivos de privacidad u otras razones? Por ejemplo, comprobar el saldo de permisos u otra información privada.
  * ¿Va a haber colaboración entre los usuarios que podrían no tener ningún Teams común? Por ejemplo, encontrar próximos eventos de toda la organización en una empresa.
  * ¿Hay alguna notificación o mensaje personalizado que deba enviarse a un usuario a lo largo de la experiencia de la aplicación Teams? Por ejemplo, recordatorios para aprobaciones o registros.
* Para un ámbito compartido (equipo, canal o chat), haga las siguientes preguntas:
  * ¿Es la información presentada por la aplicación, ya sea en pestaña o a través de un bot, relevante y útil para la mayoría de los miembros de un equipo? Por ejemplo, la aplicación Scrum.
  * ¿Podría cambiar el contexto de la aplicación en función del equipo al que se agregue? Por ejemplo, las tareas del planificador son diferentes en diferentes equipos. 
  * ¿Es posible que todos los miembros de una persona que necesitan colaborar formen parte de un solo equipo? Por ejemplo, agentes trabajando en un ticket.

Los siguientes escenarios le guiarán en la comprensión de la selección de puntos de entrada y elementos de interfaz de usuario que funcionan bien con Teams capacidades de la aplicación:

> [!NOTE]
> No es una lista exhaustiva, pero te ayudará a pensar en algunas de las posibilidades disponibles para ti.

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a>Crear, compartir y colaborar en elementos de un sistema externo

App for Microsoft Teams es una gran manera de interactuar con sus datos y hay una variedad de puntos de integración para elegir.

* **Extensiones de mensajería con comandos de búsqueda:** busque sistemas externos y comparta los resultados como una tarjeta interactiva.

* **Extensiones de mensajería con comandos de acción:** recopile información para insertar en un almacén de datos o realizar búsquedas avanzadas.

* **Pestañas:** cree experiencias web incrustadas para ver, trabajar y compartir datos.

* **Conectores y webhooks**: Una forma sencilla de insertar datos y enviar datos fuera del cliente Teams.

* **Módulos de tareas**: Formularios modales interactivos desde cualquier lugar que los necesite para recopilar o mostrar información.

## <a name="initiate-workflows-and-processes"></a>Iniciar flujos de trabajo y procesos

A veces solo necesita una forma rápida de iniciar un proceso o flujo de trabajo en un sistema externo.

* **Comandos de acción extensiones** de mensajería: desencadena desde mensajes, lo que permite a los usuarios enviar rápidamente el contenido de un mensaje a los servicios web.

* **Módulos de tareas:** ábralos desde una pestaña, un bot o una extensión de mensajería para recopilar información antes de iniciar un flujo de trabajo.

* **Bots conversacionales:** Interactúa con tus usuarios a través de texto y tarjetas enriquecidas.

* **Webhooks salientes:** una buena opción para una interacción sencilla de ida y vuelta cuando no es necesario crear un bot conversacional completo.

## <a name="send-notifications-and-alerts"></a>Enviar notificaciones y alertas

Envíe notificaciones y alertas asincrónicas a los usuarios en Teams. Utilice tarjetas interactivas para proporcionar acceso rápido a acciones y enlaces de uso común a información adicional.

* **Bots conversacionales:** envía mensajes proactivos a grupos, canales o usuarios individuales.

* **Conectores y webhooks entrantes:** permite que un canal se suscriba para recibir mensajes. Un conector permite a los usuarios personalizar la suscripción con una página de configuración.

## <a name="ask-questions-and-get-answers"></a>Haz preguntas y obtén respuestas

La gente tiene preguntas y probablemente tienes muchas de las respuestas almacenadas en alguna parte. Desafortunadamente, a menudo es bastante difícil conectar los dos.

* **Bots conversacionales:** Procesamiento natural del lenguaje, IA, aprendizaje automático y todas las palabras de moda. Utilice un bot alimentado por la nube inteligente para conectar a los usuarios a las respuestas que necesitan.

* **Pestañas:** incrustar el portal web existente en Teams o crear una versión específica de Teams para una funcionalidad adicional.

## <a name="get-social"></a>Conseguir social

Una plataforma de colaboración es inherentemente una plataforma social. Deje que su lado creativo sea gratuito y agregue algo de diversión a su lugar de trabajo. Todos los usuarios deben ser capaces de enviar chistes, dar felicitaciones, obtener algunos memes, echar algunos emojis, o cualquier otra cosa que golpee su fantasía.

## <a name="think-in-terms-of-a-single-page-app"></a>Piense en términos de una aplicación de una sola página

Las pestañas son páginas web incrustadas. Prácticamente cualquier cosa que puedas hacer en un SPA, puedes hacer en una pestaña en Teams. Sólo asegúrese de prestar atención a la alcance. Las pestañas de grupo y canal son para experiencias compartidas y las pestañas personales son para experiencias personales. La lista de cosas del equipo va en la pestaña del canal y la lista de tus cosas va en la pestaña personal.

## <a name="start-small"></a>Empezar pequeño

¿No estás seguro de por dónde empezar? ¿Te sientes un poco abrumado con la increíble variedad de opciones disponibles para ti? Debe elegir una característica principal de la aplicación e iniciarla allí. Después de hacerse una idea del flujo de información a través de los diversos contextos en Teams, es mucho más simple imaginar una interacción más compleja.

## <a name="put-it-all-together"></a>Ponlo todo junto

Dicho esto, las mejores aplicaciones suelen combinar varias características, creando una aplicación que involucra a los usuarios en el contexto correcto con la funcionalidad correcta en el momento adecuado. No debe forzar ninguna funcionalidad en un lugar al que no pertenezca. El hecho de que tengas un buen bot conversacional uno a uno no significa que lo añadas a ningún equipo. Diferentes puntos de extensibilidad son buenos para diferentes cosas, jugar a sus fortalezas para crear una aplicación exitosa.

## <a name="see-also"></a>Vea también

[Desarrollar aplicaciones para Microsoft Teams](../../overview.md)
