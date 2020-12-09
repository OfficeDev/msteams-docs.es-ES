---
title: Diseño de un bot
description: Obtenga información sobre cómo diseñar un bot de Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605496"
---
# <a name="designing-your-microsoft-teams-bot"></a>Diseño de un bot de Microsoft Teams

Los bots son aplicaciones de conversación que realizan un conjunto específico de tareas. Basado en <a href="https://dev.botframework.com/" target="_blank">Microsoft bot Framework</a>, los bots se comunican con los usuarios, responden a sus preguntas y les notifican de forma proactiva sobre los cambios y otros eventos. Son una buena forma de llegar.

Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar bots en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de IU de Microsoft Teams

Puede encontrar pautas de diseño de bot más completas, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a>Agregar un bot

Los bots están disponibles en chats, canales y aplicaciones personales. Puede Agregar un bot de una de las siguientes maneras:

* De la tienda Teams (AppSource).
* Mediante el control flotante de la aplicación seleccionando el icono **más** en el lado izquierdo de Teams.
* Con una @mention en el cuadro nuevo chat o redacción (en el ejemplo siguiente, se muestra cómo puede hacerlo en un chat en grupo).

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="En el ejemplo se muestra cómo agregar un bot en un chat de grupo mediante un @mention." border="false":::

## <a name="introduce-a-bot"></a>Presentar un bot

Es fundamental que el bot se presente a sí mismo y describa lo que puede hacer. Este intercambio inicial ayuda a los usuarios a comprender qué hacer con el bot, descubrir sus limitaciones y, lo que es más importante, familiarizarse con la interacción con él.

### <a name="welcome-message-in-a-one-on-one-chat"></a>Mensaje de bienvenida en un chat de uno a uno

En los contextos personales, los mensajes de bienvenida establecen el tono de la bot. El mensaje incluye un saludo, lo que el bot puede hacer y algunas sugerencias para interactuar (por ejemplo, "preguntarme sobre..."). Si es posible, estas sugerencias deben devolver respuestas almacenadas sin tener que iniciar sesión.

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="Ejemplo muestra una introducción a un bot en una aplicación personal." border="false":::

### <a name="introductions-in-group-chats-and-channels"></a>Introducciones en chats y canales de grupo

La introducción de la utilidad debe ser ligeramente diferente en los chats de grupo y en los canales, en comparación con un contexto personal (como una aplicación personal). En la vida real, si ha entrado en un salón lleno de personas; se introdujo en lugar de la bienvenida a todos los usuarios que ya están allí. Lleve a cabo este pensamiento en el diseño de bot.

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="Ejemplo muestra una introducción de bot en un contexto de colaboración." border="false":::

### <a name="bot-authentication-with-single-sign-on"></a>Autenticación de bot con inicio de sesión único

Cuando una persona mensaje un bot, puede que sea necesario iniciar sesión use todas sus características. Puede simplificar el proceso de autenticación con el inicio de sesión único (SSO).

No se olvide: en el menú de comandos de Bot (**¿Qué puedo hacer?**), también debe proporcionar un comando para cerrar la sesión.

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="Ejemplo muestra un bot con un botón de inicio de sesión." border="false":::

### <a name="tours"></a>Viajes

Puede incluir un paseo con mensajes de bienvenida y si el bot responde a algo como un comando "ayuda". Un paseo es la forma más eficaz de describir lo que puede hacer el bot. Si es aplicable, también son excelentes para describir otras características de la aplicación (por ejemplo, incluir capturas de pantallas de la extensión de mensajería).

> [!IMPORTANT]
> Los paseos deben ser accesibles sin tener que iniciar sesión.

#### <a name="one-on-one-chats"></a>Chats uno a uno

En una aplicación personal, un carrusel puede proporcionar una introducción eficaz a su bot y otras características de la aplicación. Incluir botones el procedimiento para que los usuarios prueben comandos de Bot (por ejemplo, **crear una tarea**).

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="Ejemplo muestra un paseo de bot en un chat de uno a uno." border="false":::

#### <a name="channels-and-group-chats"></a>Canales y chats de grupo

En los canales y los chats de grupos, un tour debe abrirse en un modal (también conocido como [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) , por lo que no interrumpe las conversaciones en curso). Esto también le ofrece la opción de implementar vistas basadas en roles para su tour.

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="Ejemplo muestra un paseo de bot en un canal." border="false":::

## <a name="chat-with-a-bot"></a>Chatear con un bot

Los bots se integran directamente en el marco de mensajería del equipo. Los usuarios pueden chatear con un bot para obtener respuestas a sus preguntas o escribir comandos para hacer que el bot realice un conjunto de tareas limitado o específico. Los bots pueden notificar de forma proactiva a los usuarios sobre cambios o actualizaciones de la aplicación mediante chat.

### <a name="chat-with-a-bot-in-different-contexts"></a>Chatear con un bot en diferentes contextos

Puede usar bots en los siguientes contextos:

* **Aplicaciones personales**: en una aplicación personal, un bot tiene una pestaña dedicada de chat.
* **Chat de uno en uno**: un usuario puede iniciar una conversación privada con un bot. Tiene la misma experiencia que el uso de un bot en una aplicación personal.
* **Chat en grupo**: los usuarios pueden interactuar con un bot en un chat grupal por @mentioning el bot.
* **Canal**: los usuarios pueden interactuar con un bot en un canal. @mentioning el nombre del bot en el cuadro de redacción. Recuerde que, en este contexto, el bot está disponible para todo el equipo, no solo para el canal.

### <a name="anatomy"></a>Anatomía

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="Ejemplo muestra una anatomía estructural de un bot." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Nombre y icono de la aplicación**|
|2 |**Pestaña chat**: abre el espacio para hablar con el bot (aplicable solo a las aplicaciones personales).|
|3 |**Pestañas personalizadas**: abre otro contenido relacionado con la aplicación.|
|4 |**Ficha acerca** de: muestra información básica sobre la aplicación.|
|5 |**Burbuja de chat**: conversaciones de robot use el marco de mensajería de Teams.|
|6 |**Tarjeta adaptable**: si las respuestas de su bot incluyen tarjetas adaptables, la tarjeta ocupa todo el ancho de la burbuja de chat.|
|7 |**Menú de comandos**: muestra los comandos estándar del bot (definidos por el usuario).

### <a name="command-menu"></a>Menú de comandos

El menú comando proporciona una lista de palabras o frases a las que desea que el bot responda siempre. El menú comando se muestra encima del cuadro de redacción cuando alguien está conversando con un bot. Cuando se selecciona un comando, se inserta en un mensaje.

La lista de comandos debe ser breve. El menú solo está destinado a resaltar las características principales del bot. Mantener también los comandos concisos. Por ejemplo, cree un comando llamado **ayuda** en lugar de, **por lo que puede ayudarme**?
El menú de comandos debe estar siempre disponible independientemente del estado de la conversación.

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="Ejemplo muestra el menú de comandos de un bot." border="false":::

## <a name="understand-what-people-are-saying"></a>Conocer lo que dicen los usuarios

Use un diccionario de sinónimos y obtenga personas de tantos fondos diferentes como sea posible para ayudarle a generar diferentes interpretaciones de consultas estándar.

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Ilustración que muestra cómo un bot puede interpretar ' Hello '." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;ayuda&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;gracias&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a>Extraer el propósito y los datos de los mensajes

Diseñar el bot para que reconozca la intención, que captura lo que alguien quiere desde un bot en respuesta a un mensaje o consulta. Intención clasifica un mensaje o una consulta como una sola acción con uno o varios objetos de datos que se ven afectados por la acción. 

En los ejemplos siguientes se describen la intención del usuario y los datos de los mensajes enviados a los bots.

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Ejemplo que muestra que en la oración ' reservar un vuelo para Seattle ', la intención del usuario es ' libro a vuelo ' y datos es ' Seattle '." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Ejemplo que muestra en la oración ' ¿Cuándo está abierto el almacén? ', el intento del usuario es ' When ' y los datos son ' Open '." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Ejemplo que muestra en la oración ' programar una reunión a las 13:00 con Bob en distribución ', la intención del usuario es &quot;programar una reunión&quot; y los datos son ' 13:00 ' y ' Bob en distribución '." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a>Analizar y mejorar

Obtenga información sobre lo que dicen los usuarios al chatear con el bot. Este será un proceso iterativo continuo a medida que crece la base de usuarios en distintas ubicaciones y organizaciones. Puede ajustar el reconocimiento de idioma y la asignación de intenciones de bot con la descripción de idioma de Microsoft (LUIS).

* [Descripción de Luis](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Descubra cómo Luis usa AI para proporcionar una comprensión de lenguaje natural (NLU) a los datos de la aplicación.
* [Integración con Luis](https://www.luis.ai/): Agregue capacidades de lenguaje natural a su bot sin el complejo proceso de crear modelos de aprendizaje automático.

## <a name="use-cases"></a>Casos de uso

### <a name="simple-queries"></a>Consultas sencillas

Los bots pueden proporcionar una coincidencia exacta a una consulta o grupo de coincidencias relacionadas para ayudar con la anulación de ambigüedades. Para obtener coincidencias relacionadas, agrupe el contenido con una tarjeta de lista.

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="Ejemplo muestra una interacción de consulta simple con un bot." border="false":::

### <a name="multi-turn-interactions"></a>Interacciones de múltiples torneados

Aunque el bot puede admitir solicitudes y preguntas completas, también debe ser capaz de controlar las interacciones de varios turnos. Anticiparse a los posibles pasos siguientes hace que sea mucho más fácil para los usuarios realizar un flujo de tareas completo (en lugar de esperar que se diseñe una solicitud completa).

En el siguiente ejemplo, el bot responde a cada mensaje con opciones para lo que es posible que quiera hacer a continuación.

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="Ejemplo muestra una interacción de varios turnos con un bot." border="false":::

### <a name="reach-out-to-users"></a>Ponerse en contacto con los usuarios

Con la mensajería proactiva, el bot puede actuar como un resumen que envía las notificaciones relevantes a un individuo, un chat en grupo o un canal a una frecuencia específica. Un bot puede enviar un mensaje cuando algo ha cambiado en un documento o se cierra un elemento de trabajo.

En el siguiente ejemplo, un usuario recibe una notificación del sistema que un bot ha puesto en un mensaje en otro canal.

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="Ejemplo muestra que una notificación de un bot es una mensajería proactiva de un usuario de otro canal." border="false":::

Ahora, en ese canal, el usuario puede leer su mensaje desde el bot.

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="Ejemplo muestra el usuario que mira el mensaje proactivo del bot." border="false":::

### <a name="use-tabs-with-bots"></a>Usar pestañas con bots

Una pestaña puede hacer que el bot sea más fácil de usar. Por ejemplo, si el bot puede crear elementos de trabajo, sería estupendo Mostrar todos esos elementos en una ubicación central dentro de una pestaña. Vea más información sobre el [diseño de pestañas](../../tabs/design/tabs.md).

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="Ejemplo muestra cómo una pestaña puede ayudar a organizar el contenido de los robots." border="false":::

## <a name="manage-a-bot"></a>Administrar un bot

Los usuarios deben poder cambiar la configuración de un bot. Puede proporcionar esta funcionalidad con comandos de bot, pero normalmente es más eficaz incluir toda la configuración en un [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (como se muestra en el ejemplo siguiente).

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="Ejemplo muestra un módulo de tareas para configurar las opciones de un bot." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="content"></a>Contenido

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-establish-a-clear-persona"></a>Do: establecer un rol claro

¿La luz y el tono de su bot, "solo los hechos" o la anomalía? ¿Cómo debe responder en escenarios diferentes? La planeación y documentación del rol de un bot facilita la escritura de respuestas que parecen naturales y coherentes.

Vea más información sobre cómo escribir para bots en el <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Kit de interfaz de usuario de Microsoft Teams (Figma).</a>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a>Do: transmitir claramente lo que puede hacer su bot

Los mensajes de bienvenida y los paseos ayudan a los usuarios a comprender lo que pueden hacer con el bot.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a>No: ocultar las características de la bot

Primera impresión importa. Es probable que los usuarios sean confusos o sospechosos cuando se les presente un mensaje de inicio de sesión de nondescript.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-recognize-non-questions"></a>Do: reconocer no preguntas

El bot debe ser capaz de responder a mensajes como "HI", "Help" y "Agradecimientos", además de tener en cuenta los errores y coloquialess comunes.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a>No: no se pierdan las oportunidades de alegría

Algunos usuarios esperan que las conversaciones fluyan naturalmente como lo harían con una persona real. Intente evitar las respuestas más difíciles a los mensajes sencillos.

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a>Solución de problemas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-provide-help"></a>Do: proporcionar ayuda

Si el bot no puede satisfacer una solicitud, proporcione medios para que un usuario se enseñe a interactuar con el bot.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-leave-users-stranded"></a>No: dejar a los usuarios en desuso

Los usuarios abandonarán rápidamente el bot si no pueden solucionar los problemas.

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a>Interacciones complejas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a>Do: usar módulos de tareas o pestañas

Si el bot proporciona una respuesta que requiere algunos pasos más, puede vincular a un módulo de tarea o a una pestaña para completar la tarea o el flujo.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a>No: hacer que las interacciones de varios turnos sean tediosas

Una conversación extensa para completar una tarea única es lenta y demasiado compleja. También se requiere que el desarrollador tenga en cuenta los cambios de estado (por ejemplo, el tiempo de espera de la conversación o el envío de un mensaje de "cancelación").

   :::column-end:::
:::row-end:::

### <a name="privacy"></a>Privacidad

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a>Do: mostrar solo información confidencial en un contexto personal

Si el bot está en un canal o en un chat de grupo, se recomienda dirigir a los usuarios a una ubicación privada (como un módulo de tareas, una ficha o un explorador) para ver la información confidencial.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a>No: algún contenido no está diseñado para ser visto por todos los usuarios

El bot no debe revelar información confidencial a un grupo de personas.

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a>Más información

Estas otras instrucciones pueden ayudarle con el diseño de su bot:

* [Diseño de la aplicación personal](../../concepts/design/personal-apps.md)
* [Diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md)
* [Diseño de módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a>Validar el diseño

Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.

> [!div class="nextstepaction"]
> [Comprobar las instrucciones de validación del diseño](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
