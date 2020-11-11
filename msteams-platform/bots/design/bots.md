---
title: Directrices de diseño para bots
description: Describe las instrucciones para crear bots.
keywords: Directrices de diseño de Teams referencia de los bots del marco de trabajo hablando
ms.openlocfilehash: 0691c483d12e537772b74abc015d71e1704f88c8
ms.sourcegitcommit: fdb53284a20285f7e8a7daf25e85cb5d06c52b95
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/11/2020
ms.locfileid: "48992641"
---
# <a name="start-talking-with-bots"></a>Empezar a hablar con bots

Los bots son aplicaciones de conversación que realizan un conjunto de tareas estrecho o específico. Le ofrecen la oportunidad de comunicarse con los usuarios, responder a sus preguntas y notificarles de forma proactiva sobre los cambios. Son una buena forma de llegar.

---

## <a name="guidelines"></a>Instrucciones

### <a name="bot-design-guidelines"></a>Directrices de diseño de bot

* Los bots deben proporcionar las notificaciones relevantes cuando haya una actividad.
* Los bots no deben insertar datos confidenciales en un equipo, un chat grupal o una conversación de 1:1 a una audiencia que no debe ver los datos.
* Las notificaciones de bot deben incluir datos significativos para informar a los usuarios de la relevancia de la notificación.
* El tono del bot debe reflejar la voz de Teams, tal como se define en las instrucciones.
* Los bots deben proporcionar un mensaje de bienvenida de primera ejecución que resalte el valor del bot y cuáles son sus funciones principales, esto podría ser "realizar un paseo", un tutorial interactivo con tarjetas de carrusel o botones "probar".
* El texto de bot no debe tener errores ortográficos ni gramaticales.
* Los bots deben proporcionar un conjunto de comandos de bot predefinidos que se pueden accionar.
* Los mensajes de bot deben ser fáciles de comprender y accionable.
* Los bots deben proporcionar comandos de ayuda de retroceso cuando no se comprenda un mensaje.
* Los formularios, incrustados en tarjetas, enviados por un bot deben proporcionar entradas deterministas que no requieran actualizaciones secuenciales.
* Las notificaciones de bot deben estar en el ámbito de un equipo, un chat de grupo o una conversación de 1:1 con contenido relevante para la audiencia.

### <a name="avatars"></a>Avatares

Los avatares de bot están formados como hexágonos para que los usuarios puedan saber rápidamente que están hablando con un bot en lugar de con una persona. Enviará el Avatar como un cuadrado y lo recortaremos por usted. En lo que se refiere a los avatares, le recomendamos que el suyo pueda leerse a una distancia de 2 metros y con un contraste mayor.

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a>Botones

Admitimos hasta seis botones por tarjeta. Sea conciso al escribir texto de botón y tenga en cuenta que la mayoría de los botones solo deben dirigirse a la tarea a mano.

### <a name="graphics"></a>Gráficos

Los gráficos son una buena forma de decir un artículo, pero no todas las conversaciones de bot requieren gráficos, así que úselas para obtener el máximo impacto.

### <a name="onboarding-users"></a>Usuarios de la incorporación

Es fundamental que los bots se presenten y transmitan lo que pueden hacer para los usuarios. Este *valor de Exchange* ayuda a los usuarios a comprender qué se debe hacer con el bot, donde las limitaciones pueden estar y, lo que es más importante, ayuda a los usuarios a tolerar la interacción con un equipo que no será tan intuitivo como una persona real. Además, concede permiso a los datos de usuario en Exchange para el valor real que proporciona el servicio.

#### <a name="welcome-messages"></a>Mensajes de bienvenida

Los mensajes de bienvenida son la mejor forma de establecer el tono de la bot y deben usarse en escenarios personales y de equipo o grupo. El mensaje indica lo que hace el bot y algunas formas comunes de interactuar con él. Use ejemplos de funciones específicas como " *probar preguntando....* " en una lista con viñetas. Siempre que sea posible, estas sugerencias deben devolver respuestas almacenadas. Es fundamental que los ejemplos de funciones funcionen sin que los usuarios inicien sesión.
*Consulte* [los requisitos del mensaje de bienvenida](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-personal-bots-must-always-send-a-welcome-message-on-first-launch) para obtener más información.

#### <a name="tours"></a>Viajes

Incluya un atributo de *echar un paseo* con mensajes de bienvenida y respuestas a la entrada del usuario equivalente a " *ayuda* ". Esta es la forma más eficaz de informar a los usuarios sobre lo que puede hacer un bot. Los carruseles en la experiencia de uno a uno son una forma excelente de decir este caso e incluso *pruébelos, pruebe que* los botones que se vinculan a ejemplos de respuestas posibles son recomendables. Los paseos también son lugares estupendos para hablar de otras características de la aplicación. Por ejemplo, puede incluir capturas de pantallas de las extensiones de mensajería y las pestañas de Microsoft Teams.  Los usuarios no deben tener que iniciar sesión para tener acceso y usar un paseo.

Cuando se usan paseos en escenarios de equipo o grupo, deben abrirse en un módulo de tareas para que no se pueda agregar más ruido de tarjeta a las conversaciones en curso entre los usuarios.

### <a name="responding-to-users-and-failing-gracefully"></a>Responder a los usuarios y conmutar por error

El bot también debe ser capaz de responder a cosas como " *Hola* ", " *ayuda* " y " *gracias* " mientras se toman errores y coloquialess comunes en la cuenta. Por ejemplo:

#### <a name="x2713-hello"></a>&#x2713; Hello

`"Hi"`  `"How are you"`  `"Howdy"`

#### <a name="x2713-help"></a>Ayuda de &#x2713;

`"What do you do?"`  `"How does this work?"`  `"What the heck?"`

#### <a name="x2713-thanks"></a>&#x2713; gracias

`"Thank you"`  `"Thankyou"`  `"Thx"`

El bot debe ser capaz de administrar los siguientes tipos de consultas y entradas:

> [!div class="checklist"]
>
> * **Preguntas reconocidas**. Estas son las preguntas del "escenario de mejor caso" que esperaría de los usuarios.
> * **Personas sin preguntas reconocidas**. Consultas sobre la funcionalidad no admitida o las entradas aleatorias, no relacionadas o blasfemas.
> * **Preguntas no reconocidas** : entradas o entradas que son ininteligibles, sin significado o sin sentido.

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

En las conversaciones personales entre un bot y una sola persona, las pestañas pueden contener información y listas específicas del usuario. También es un buen punto de partida para mantener las respuestas de robot en las preguntas más frecuentes (p + f), de modo que los usuarios no necesitan seguir preguntando.

### <a name="x2713-a-place-to-finish-a-conversation"></a>&#x2713; un punto para finalizar una conversación

Puede crear un vínculo a una ficha desde una tarjeta. Si el bot proporciona una respuesta que requiere algunos pasos más, puede vincular a una pestaña para completar la tarea o el flujo. Por ejemplo, en respuesta a "¿cómo se da formato a mi iPhone?", una buena respuesta puede ser una tarjeta que resume los primeros pasos y un botón para *Mostrar más* que, a continuación, lleva al usuario a la pestaña de *ayuda* del bot y vínculos profundos a las instrucciones específicas.

### <a name="x2713-a-place-to-host-a-settings-page"></a>&#x2713; una ubicación para hospedar una página de configuración

Los bots deben tener algún control de usuario. Para muchos bots se permite a través de una interfaz de chat; sin embargo, es difícil recordar esa configuración. Una pestaña de configuración puede mostrar la configuración de los usuarios, permitir que los usuarios cambien todas a la vez y también puede ser un buen punto de desactivación para comportamientos personalizados de bot más complejos.

### <a name="x2713-a-place-to-provide-some-help"></a>&#x2713; un espacio para proporcionar ayuda

Agregue una pestaña que enseñe a los usuarios a comunicarse con su bot. Puede proporcionar algún contexto para lo que hace o las preguntas más frecuentes.

![Proporciona ayuda](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> La incorporación de partes del sitio en una pestaña ayudará a los usuarios a mantener el contexto de una conversación mientras usan el servicio. Elimina la necesidad de iniciar el servicio en un explorador y cambiar de una aplicación a otra.

---

## <a name="bots-in-channels"></a>Bots en los canales

La invocación de un bot en un canal se puede realizar mediante `@mention` . El cuadro de diálogo de bot debe ser único en los escenarios de uno a uno, y generalmente es una buena idea considerar enfoques separados. Esto es especialmente cierto en los casos siguientes:

### <a name="sensitive-data-sent-by-a-bot"></a>Datos confidenciales enviados por un bot

Mientras que los usuarios de un equipo pueden ser conocidos para el servicio, los roles de usuario reales no pueden. Esto significa que, por ejemplo, en un escenario educativo que implique acosos, la información de contacto de los padres y los estudiantes no se compartirá en una configuración de equipo. En su lugar, el mensaje del bot podría ser: "dos incidentes de acosos ocurrieron hoy" junto con un botón para mostrar detalles.

El inicio de detalles en una página web o un módulo de tareas puede solicitar credenciales de usuario o consultar con un índice de roles de usuario emparejados con cuentas de AAD. En ambas opciones, los datos están en un ámbito de vista privado y no habrá ninguna fuga de datos. Si se envían los mismos datos en una conversación de uno a uno entre un usuario y el bot, los datos solo están visibles para el usuario en ese contexto y, por lo tanto, son seguros para mostrarse completamente en el mensaje de bot. Sin embargo, se deben evitar los usuarios de un canal a un chat uno a uno, ya que la navegación forzada es muy disruptiva.

### <a name="sending-cards-as-a-response-to-interactions"></a>Envío de tarjetas como respuesta a interacciones

Al enviar una tarjeta de carrusel en respuesta a un *paseo* por una conversación de uno a uno es perfectamente aceptable, el mismo patrón podría producir decenas o centenares de *recorridos de paseo* en un canal activo con muchos usuarios. Para evitar esto, las tarjetas secundarias deben alojarse en un módulo de tareas. Este patrón mantiene a los usuarios en el contexto con el canal, mantiene el canal limpio de respuestas de robots excesivas y, opcionalmente, puede considerar diferentes roles de usuario cuando se muestra el *paseo* .

## <a name="useful-tips"></a>Sugerencias útiles

### <a name="x2713-remember-bots-arent-assistants"></a>&#x2713; Recuerde que los bots no son ayudantes

A diferencia de los agentes, por ejemplo, Cortana, los bots actúan como especialistas.

### <a name="x2713-discourage-chitchat"></a>&#x2713; desaconsejar chitchat

A menos que el bot se haya creado para la conversación, busque formas de redirigir chitchat a la finalización de tareas.

### <a name="x2713-introduce-some-personality"></a>&#x2713; introducen personalidad

Mantenga la personalidad de la personalidad del bot con la voz del producto. Piense en su robot como hablando de su empresa.

### <a name="x2713-maintain-tone"></a>&#x2713; mantener tono

Determine si desea que el tono sea agradable y claro, "solo los hechos" o súper extraña.

### <a name="x2713-encourage-easy-task-flow"></a>&#x2713; animar el flujo de tareas sencillo

Admite interacciones multiactivables, a la vez que permite preguntas completamente formadas. La planeación del siguiente paso ayudará a los usuarios a pasar por los flujos de tareas de forma mucho más fácil.

Si un usuario realiza varios pasos para completar una tarea, permita que el bot los lleve a cabo a través de cada paso, pero el fin es que sugiera una ruta de acceso más rápida. Por ejemplo, si un usuario ha tomado varias vueltas de conversación para establecer una reunión (especificando primero una reunión, indicando con quién, a continuación, la hora y, a continuación, el día), finalice la conversación con la siguiente sugerencia: la próxima vez, intente preguntar si puede ' programar una reunión con Bob al 1:00 mañana.
