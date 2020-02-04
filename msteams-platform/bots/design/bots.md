---
title: Directrices de diseño para bots
description: Describe las instrucciones para crear bots.
keywords: Directrices de diseño de Teams referencia de los bots del marco de trabajo hablando
ms.openlocfilehash: f59a1e9c280f27567692b4d10341db79d05c3464
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676126"
---
# <a name="start-talking-with-bots"></a>Empezar a hablar con bots

Los bots son aplicaciones de conversación que realizan un conjunto de tareas estrecho o específico. Le ofrecen la oportunidad de comunicarse con los usuarios, responder a sus preguntas y notificarles de forma proactiva sobre los cambios. Son una buena forma de llegar.

---

## <a name="guidelines"></a>Instrucciones

### <a name="avatars"></a>Avatares

Los avatares de bot están formados como hexágonos para que los usuarios puedan saber rápidamente que están hablando con un bot en lugar de con una persona. Enviará el Avatar como un cuadrado y lo recortaremos por usted. En lo que se refiere a los avatares, le recomendamos que el suyo pueda leerse a una distancia de 2 metros y con un contraste mayor.

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a>Botones

Admitimos hasta seis botones por tarjeta. Sea conciso al escribir texto de botón y tenga en cuenta que la mayoría de los botones solo deben dirigirse a la tarea a mano.

### <a name="graphics"></a>Gráficos

Los gráficos son una buena forma de decir un artículo, pero no todas las conversaciones de bot requieren gráficos, así que úselas para obtener el máximo impacto.

### <a name="responding-to-users-and-failing-gracefully"></a>Responder a los usuarios y conmutar por error

El bot también debe ser capaz de responder a cosas como "HI", "Help" y "gracias" mientras se toman errores y coloquialess comunes en la cuenta. Por ejemplo:

#### <a name="x2713-hello"></a>&#x2713; Hello

`Hi` `how are you` `howdy`

#### <a name="x2713-help"></a>Ayuda de &#x2713;

`What do you do?` `How does this work?` `What the heck?`

#### <a name="x2713-thanks"></a>&#x2713; gracias

`Thank you` `thankyou` `thx`

El bot debe ser capaz de administrar los siguientes tipos de consultas y entradas:

* **Preguntas reconocidas**: estas son las preguntas de "escenario de mejor caso" que debería anticipar de los usuarios.
* Personas **sin preguntas reconocidas**: consultas sobre funcionalidad no admitida, fragmentos aleatorios de información o cuándo alguien desea Curse en su bot.
* **Preguntas no reconocidas**: entradas ininteligibles (es decir, galimatías).

Ejemplos de tipos de personalidad y respuesta de bot:

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> Al escribir la secuencia de comandos de bot, pregúntese a sí mismo: "¿la compañía estará avergonzada si la respuesta es capturada y compartida?"

### <a name="understanding-what-users-are-trying-to-say"></a>Descripción de lo que los usuarios intentan decir

#### <a name="use-a-thesaurus-for-synonyms"></a>Usar un diccionario de sinónimos para sinónimos

Al recopilar una lluvia de ideas, use un diccionario de sinónimos y obtenga personas de tantos fondos diferentes como sea posible para ayudarle a generar diferentes interpretaciones de cada consulta.

#### <a name="make-use-of-telemetry-and-interviews"></a>Hacer uso de telemetría y entrevistas

Averigüe qué opinan los usuarios y cuál fue su intención al consultar a su bot. Este será un proceso continuo a medida que se obtienen usuarios en distintas ubicaciones y tipos de compañías. Puede ajustar el reconocimiento de idioma y la asignación de intenciones con idiomas que comprenden el servicio inteligente ([Luis](/azure/cognitive-services/luis/what-is-luis)).

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a>¿Con qué frecuencia debería usar el bot para ponerse en contacto con un usuario?

#### <a name="x2713-when-a-state-has-changed"></a>&#x2713; cuando un Estado ha cambiado

Por ejemplo, si una asignación se marca como completada, cuando un error cambia, cuando hay nuevos medios sociales disponibles o cuando se ha completado un sondeo.

#### <a name="x2713-when-the-timing-is-right"></a>&#x2713; cuando el intervalo es el derecho

El bot puede actuar como un resumen diario y enviar una notificación al usuario o al canal en una frecuencia específica.

Deje el usuario en el control. Proporcionar la configuración de la notificación que incluya frecuencia y prioridad.

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a>Uso de pestañas

Las pestañas hacen que el bot sea mucho más funcional. Con las pestañas, puede crear lo siguiente:

### <a name="x2713-a-place-to-host-standing-queries"></a>&#x2713; un punto de hospedar consultas permanentes

En las conversaciones personales entre un bot y una sola persona, las pestañas pueden hospedar información y listas específicas del usuario. También es un buen punto de partida para mantener las respuestas de robot en las preguntas más frecuentes (p + f), de modo que los usuarios no necesitan seguir preguntando.

### <a name="x2713-a-place-to-finish-a-conversation"></a>&#x2713; un punto para finalizar una conversación

Puede crear un vínculo a una ficha desde una tarjeta. Si el bot proporciona una respuesta que requiere algunos pasos más, puede vincular a una pestaña para completar la tarea o el flujo.

### <a name="x2713-a-place-to-provide-some-help"></a>&#x2713; un espacio para proporcionar ayuda

Agregue una pestaña que enseñe a los usuarios a comunicarse con su bot. Puede proporcionar algún contexto para lo que hace o las preguntas más frecuentes.

![Proporciona ayuda](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> La incorporación de partes de su sitio en una pestaña ayudará a alguien a mantener el contexto de una conversación mientras usa el servicio. Elimina la necesidad de iniciar el servicio en un explorador y cambiar de una aplicación a otra.

---

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="x2713-bots-arent-assistants"></a>Los bots de &#x2713; no son auxiliares

A diferencia de los agentes, por ejemplo, Cortana, los bots actúan como especialistas.

### <a name="x2713-discourage-chitchat"></a>&#x2713; desaconsejar chitchat

A menos que el bot se haya creado para la conversación, busque formas de redirigir chitchat a la finalización de tareas.

### <a name="x2713-introduce-some-personality"></a>&#x2713; introducen personalidad

Mantenga la personalidad de la personalidad del bot con la voz del producto. Piense en su robot como hablando de su empresa.

### <a name="x2713-maintain-tone"></a>&#x2713; mantener tono

Determine si desea que el tono sea agradable y claro, "solo los hechos" o súper extraña.

### <a name="x2713-encourage-easy-task-flow"></a>&#x2713; animar el flujo de tareas sencillo

Admite interacciones multiactivables, a la vez que permite preguntas completamente formadas. La planeación del siguiente paso ayudará a los usuarios a pasar por los flujos de tareas de forma mucho más fácil.

Si un usuario realiza varios pasos para completar una tarea, permita que el bot los lleve a cabo a través de cada paso, pero el fin es que sugiera una ruta de acceso más rápida. Por ejemplo, si un usuario ha tomado varias vueltas de conversación para establecer una reunión (especificando primero una reunión, e identifica con quién, a continuación, indicando la hora y, a continuación, indicando el día), finalice la conversación con la siguiente sugerencia: la próxima vez, intente preguntar si puede ' programar una reunión con Bob al 1:00 mañana '.