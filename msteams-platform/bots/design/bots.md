---
title: Cómo diseñar su bot
description: Obtenga información sobre cómo diseñar un bot para Teams y obtener el Kit de UI de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 98e36bf55e61ef59261959021409d9e60d8542f5
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630121"
---
# <a name="designing-your-microsoft-teams-bot"></a>Diseño de un bot para Microsoft Teams

Los bots son aplicaciones de conversación que realizan un conjunto específico de tareas. Basándose en <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, los bots se comunican con los usuarios, responden a sus preguntas y les notifican de forma proactiva sobre cambios y otros eventos. Son una herramienta excelente de comunicación.

A modo de guía en el diseño de su aplicación, a continuación se describe e ilustra cómo pueden los usuarios agregar, usar y administrar bots en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

En el Kit de UI de Microsoft Teams encontrará instrucciones de diseño de bot más completas, que incluyen elementos que puede usar y modificar como quiera.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a>Agregar un bot

Los bots están disponibles para chats, canales y aplicaciones personales.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

Los usuarios pueden agregar un bot de una de las siguientes maneras:

* Desde el Teams almacén.
* En el menú desplegable de la aplicación, seleccione el icono **Más** en el lado izquierdo de Teams.
* Con una @mención en el nuevo cuadro de chat o redacción (en el siguiente ejemplo se muestra cómo puede hacerlo en un chat de grupo).

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="En el ejemplo se muestra cómo agregar un bot en un chat de grupo con una @mención." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

Los usuarios pueden obtener acceso a los bots que se agregaron en el escritorio con un @mention.

:::image type="content" source="../../assets/images/bots/mobile-access-bot-chat-at-mention.png" alt-text="En el ejemplo se muestra cómo obtener acceso a un bot móvil en un chat de grupo mediante un @mention." border="false":::

---

## <a name="introduce-a-bot"></a>La presentación del bot

Es fundamental que el bot se presente y describa lo que puede hacer. Esta comunicación inicial ayuda a los usuarios a comprender qué pueden hacer con el bot, a conocer sus limitaciones y, lo que es más importante, a sentirse cómodos interactuando con él.

### <a name="welcome-message-in-a-one-on-one-chat"></a>Mensaje de bienvenida en un chat uno a uno

En contextos personales, los mensajes de bienvenida marcan el tono del bot. El mensaje incluye un saludo, lo que el bot puede hacer y algunas sugerencias sobre cómo interactuar. Por ejemplo, "Intente preguntarme sobre ...". Cuando sea posible, estas sugerencias deben devolver respuestas almacenadas sin necesidad de iniciar sesión.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="El ejemplo muestra una introducción a un bot en una aplicación personal." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-personal-welcome.png" alt-text="En el ejemplo se muestra una introducción de bot en una aplicación personal en el móvil." border="false":::

---

### <a name="welcome-message-in-channels-and-group-chats"></a>Mensaje de bienvenida en canales y chats de grupo

La introducción del bot debe ser ligeramente diferente en canales y chats de grupo en comparación con un espacio personal (como una aplicación personal). En la vida real, si entra en una sala llena de gente, no dará la bienvenida a las personas que ya están allí sino que será usted quien se presente. Lo mismo vale para el diseño de un bot.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="El ejemplo muestra una introducción a un bot en un contexto de colaboración." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-group-welcome.png" alt-text="En el ejemplo se muestra una introducción de bot en un contexto de colaboración en dispositivos móviles." border="false":::

---

### <a name="bot-authentication-with-single-sign-on"></a>Autenticación de bot con inicio de sesión único

Cuando alguien envía un mensaje a un bot, es posible que deba iniciar sesión para acceder a todas sus características. El inicio de sesión único (SSO) puede simplificar el proceso de autenticación.

No olvide que en el menú de comandos del bot (**¿Qué puedo hacer?**), también debe proporcionar un comando para cerrar sesión.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="En el ejemplo se muestra un bot con un botón de inicio de sesión." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-sso-example.png" alt-text="En el ejemplo se muestra un bot con un botón de inicio de sesión en el móvil." border="false":::

---

### <a name="tours"></a>Paseos

Puede incluir un paseo con mensajes de bienvenida y para cuando el bot responda a un comando de "ayuda" o algo parecido. Un paseo es la forma más eficaz de describir lo que puede hacer su bot. Si procede, también son excelentes para describir las otras características de la aplicación. Por ejemplo, incluya capturas de pantalla de la extensión de mensajería.

> [!IMPORTANT]
> Los viajes deben ser accesibles sin tener que iniciar sesión.

#### <a name="one-on-one-chats"></a>Chats uno a uno

En una aplicación personal, un carrusel puede ofrecer información general eficaz sobre el bot y otras características de la aplicación. Se recomienda incluir botones para permitir que los usuarios prueben comandos bot. Por ejemplo, **Crear una tarea**.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="El ejemplo muestra un paseo de bots en un chat uno a uno." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-personal.png" alt-text="En el ejemplo se muestra un recorrido por bots en un chat uno a uno en el móvil." border="false":::

---

#### <a name="channels-and-group-chats"></a>Canales y chats en grupo

En canales y chats de grupo, los paseos deben abrirse en un modal (también denominado [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) para no interrumpir las conversaciones en curso). Esto también le ofrece la opción de implementar vistas basadas en roles para su paseo.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="El ejemplo muestra un paseo de bots en un canal." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-channel.png" alt-text="En el ejemplo se muestra un recorrido por bots en un canal móvil." border="false":::

---

## <a name="chat-with-a-bot"></a>Chatear con un bot

Los bots se integran directamente en el marco de mensajería de Team. Los usuarios pueden chatear con un bot para obtener respuesta a sus preguntas o escribir comandos para que el bot realice un conjunto de tareas reducido o específico. Los bots pueden usar el chat para notificar a los usuarios frecuentemente de los cambios o actualizaciones que se realicen en la aplicación.

### <a name="chat-with-a-bot-in-different-contexts"></a>Chatear con un bot en diferentes contextos

Puede usar bots en los siguientes contextos:

* **Aplicaciones personal**: en una aplicación personal, un bot tiene una pestaña de chat dedicada.
* **Chat uno a uno**: un usuario puede iniciar una conversación privada con un bot. Es la misma experiencia que usar un bot en una aplicación personal.
* **Chat de grupo**: los usuarios pueden interactuar con un bot en un chat de grupo si @mencionan el bot.
* **Canal**: los usuarios pueden interactuar con un bot en un canal. Para ello, deben @mencionar el nombre del bot en el cuadro para redactar. Recuerde que, en este contexto, el bot está disponible para todo el equipo, no solo para el canal.

### <a name="anatomy"></a>Anatomía

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="El ejemplo muestra el sistema estructural de un bot." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Icono y nombre de la aplicación**|
|2|**Pestaña de chat**: abre el espacio para hablar con el bot (aplicable solo a las aplicaciones personales).|
|3|**Pestañas personalizadas**: abren otro contenido relacionado con la aplicación.|
|4 |**Pestañas Acerca de**: muestran información básica sobre la aplicación.|
|5 |**Burbujas de chat**: las conversaciones de bot usan el marco de mensajería de Teams.|
|6 |**Tarjeta adaptable:** si las respuestas del bot incluyen tarjetas adaptables, la tarjeta ocupa todo el ancho de la burbuja de chat.|
|7 |**Menú de comandos**: muestra los comandos estándar de su bot (definidos por usted).|

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un bot móvil." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Icono y nombre de la aplicación**|
|2|**Pestaña de chat**: abre el espacio para hablar con el bot (aplicable solo a las aplicaciones personales).|
|3|**Pestañas personalizadas**: abren otro contenido relacionado con la aplicación.|
|4 |**Burbujas de chat**: las conversaciones de bot usan el marco de mensajería de Teams.|
|5 |**Tarjeta adaptable:** si las respuestas del bot incluyen tarjetas adaptables, la tarjeta ocupa todo el ancho de la burbuja de chat.|

---

### <a name="command-menu"></a>Menú de comandos

En el menú de comandos se proporciona una lista de palabras o frases que quiere que el bot siempre responda. El menú de comandos se muestra encima del cuadro de redacción cuando alguien habla con un bot. Cuando se selecciona un comando, este se inserta en un mensaje.

La lista de comandos debería ser breve. El menú solo está pensado para resaltar las características principales del bot. Además, los comandos deben ser concisos. Por ejemplo, cree un comando llamado **Ayuda** en lugar de **¿Puede ayudarme, por favor?**
El menú de comandos siempre debe estar disponible independientemente del estado de la conversación.

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="En el ejemplo se muestra el menú de comandos de un bot." border="false":::

## <a name="understand-what-people-are-saying"></a>Entender qué dice la gente

Use un diccionario de sinónimos y la ayuda de personas tan diversas como le sea posible encontrar para ayudarle a generar distintas formulaciones de consultas estándar.

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;Hola&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;Ayuda&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;Gracias&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a>Extraer la intención y los datos de los mensajes

Diseñe el bot para reconocer la intención del usuario. La idea es capturar lo que alguien quiere de un bot como respuesta a un mensaje o una consulta. La intención clasifica un mensaje o consulta como una acción única con uno o varios objetos de datos afectados por la acción. 

En los ejemplos siguientes se describen la intención del usuario y los datos de los mensajes enviados a bots:

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Ejemplo que muestra la frase &quot;Reservar un vuelo a Seattle&quot;. La intención del usuario es &quot;reservar un vuelo&quot; y los datos son &quot;Seattle&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Ejemplo que muestra la frase &quot;Cuándo abre la tienda&quot;. La intención del usuario es &quot;cuándo&quot; y los datos son &quot;abrir&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Ejemplo con la frase &quot;Concertar una reunión a la 13:00 con Bob en el área de distribución&quot;. La intención del usuario es &quot;programar una reunión&quot; y los datos son &quot;13:00&quot; y &quot;Bob en el área de distribución&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a>Analizar y mejorar

Descubra qué dicen los usuarios al chatear con el bot. Este será un proceso iterativo que evoluciona continuamente a medida que su base de usuarios crece en distintas ubicaciones y organizaciones. Puede ajustar la asignación de intenciones y el reconocimiento de idiomas del bot con Microsoft Language Understanding (LUIS).

* [Descripción de LUIS](/azure/cognitive-services/luis/artificial-intelligence): descubra cómo LUIS usa la IA para aplicar métodos de comprensión del lenguaje natural (NLU) con los datos de su aplicación.
* [Integración con LUIS](https://www.luis.ai/): agregue capacidades de lenguaje natural al bot mientras evita el proceso complejo de crear modelos de aprendizaje automático.

## <a name="use-cases"></a>Casos de uso

### <a name="simple-queries"></a>Consultas sencillas

Cuando reciben una consulta, los bots pueden proporcionar una coincidencia exacta o un grupo de coincidencias relacionadas para ayudar con la desambiguación. En el caso de las coincidencias relacionadas, agrupe el contenido con una tarjeta de lista.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="El ejemplo muestra una interacción de consulta simple con un bot." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-simple-query.png" alt-text="En el ejemplo se muestra una interacción de consulta sencilla con un bot en el móvil." border="false":::

---

### <a name="multi-turn-interactions"></a>Interacciones de varios turnos

Su bot no solo debe poder admitir solicitudes y preguntas completas, sino también lidiar con interacciones de varios turnos. Anticipar los posibles pasos siguientes facilita mucho a los usuarios completar el flujo de tareas (les evita elaborar una solicitud exhaustiva).

En los ejemplos siguientes, el bot responde a cada mensaje con opciones para lo que podría querer hacer a continuación.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="El ejemplo muestra una interacción multiturno con un bot." border="false":::


# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-multi-turn.png" alt-text="En el ejemplo se muestra una interacción de varios turnos con un bot en el móvil." border="false":::


---

### <a name="reach-out-to-users"></a>Llegue a sus usuarios

Con la mensajería dinámica, el bot puede actuar como un boletín que envía notificaciones relevantes a un canal, chat de grupo o usuario con una frecuencia específica. Un bot puede enviar un mensaje cuando se ha hecho cambios en un documento o cuando se cierra un elemento de trabajo.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

En el ejemplo siguiente, el usuario recibe una notificación del sistema que indica que un bot les ha mensaje en otro canal.

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="En el ejemplo se muestra una notificación del sistema en la que un bot informa de forma dinámica a un usuario desde otro canal." border="false":::

Ahora, en ese canal, el usuario puede leer su mensaje del bot.

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="El ejemplo muestra a un usuario que observa el mensaje dinámico del bot." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

En el siguiente ejemplo, el usuario recibe una notificación de que un bot les envía un mensaje en otro canal.

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message-toast.png" alt-text="En el ejemplo se muestra una notificación del sistema de un bot que mensajería proactivamente a un usuario desde otro canal en el móvil." border="false":::

Ahora, en ese canal, el usuario puede leer su mensaje del bot.

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message.png" alt-text="En el ejemplo se muestra al usuario mirando el mensaje proactivo del bot en el móvil." border="false":::

---

### <a name="use-tabs-with-bots"></a>Usar pestañas con bots

En las aplicaciones personales, una pestaña puede complementar lo que el bot puede hacer. Por ejemplo, si el bot puede crear elementos de trabajo, sería útil mostrar todos esos elementos en una ubicación central dentro de una pestaña. Más información sobre las [pestañas de diseño](../../tabs/design/tabs.md).

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="El ejemplo muestra cómo una pestaña puede ayudar a organizar el contenido del bot." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-with-tab.png" alt-text="En un ejemplo se muestra cómo una pestaña puede ayudar a organizar el contenido del bot en el móvil." border="false":::

---

## <a name="manage-a-bot"></a>Administrar un bot

Los usuarios deberían poder cambiar la configuración de un bot. Puede proporcionar esta funcionalidad con comandos de bot, pero normalmente es más eficaz incluir toda la configuración en un [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (como se muestra en el siguiente ejemplo).

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="Un ejemplo muestra un módulo de tareas para configurar las opciones de un bot." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

Usa estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="content"></a>Contenido

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot para establecer una persona clara." border="false":::

#### <a name="do-establish-a-clear-persona"></a>Práctica recomendada: cree un rol coherente para el bot

¿Quiere que el tono del bot sea descriptivo y claro (que simplemente dé información) o que sea más simpático? ¿Cómo debe responder en distintos escenarios? Planear y documentar el rol del bot facilita la escritura de respuestas que parezcan naturales y cohesivas.

Encontrará más información sobre cómo escribir para los bots en el <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Kit de UI de Microsoft Teams (Figma).</a>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Ejemplo que muestra para transmitir claramente lo que el bot puede hacer." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a>Práctica recomendada: transmita claramente qué puede hacer el bot

Los mensajes de bienvenida y los paseos ayudan a los usuarios a comprender qué pueden hacer con el bot.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Ejemplo que muestra que no oscurece las características del bot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a>Práctica a evitar: ocultar las características del bot

Las primeras impresiones son importantes. Es probable que los usuarios se confundan o sientan sospechas cuando vean un mensaje de inicio de sesión indefinido.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="El ejemplo que muestra el bot debe reconocer que no hay preguntas." border="false":::

#### <a name="do-recognize-non-questions"></a>Práctica recomendada: que el bot reconozca mensajes que no son preguntas

El bot debería poder responder a mensajes como "Hola", "Ayuda" y "Gracias", así como sus variaciones coloquiales y las versiones con faltas de ortografía.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Ejemplo que muestra que debe evitar respuestas torpes a mensajes de bot simples." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a>Práctica a evitar: perder oportunidades para una charla agradable

Algunas personas esperan que las conversaciones fluyan de forma natural como lo harían con una persona. Intente evitar respuestas torpes a mensajes sencillos.

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a>Solución de problemas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Ejemplo que muestra bots debe ayudar a los usuarios a comprender cómo usar bots." border="false":::

#### <a name="do-provide-help"></a>Práctica recomendada: proporcione ayuda

Si el bot no puede satisfacer una solicitud, dé al usuario una manera de aprender por sí mismo a interactuar con el bot.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Ejemplo que muestra que el bot no debe varár a los usuarios." border="false":::

#### <a name="dont-leave-users-stranded"></a>Práctica a evitar: dejar a los usuarios sin ayuda

Los usuarios abandonarán rápidamente el bot si no pueden solucionar problemas con él.

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a>Interacciones complejas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Ejemplo que muestra que puede usar módulos de tareas o pestañas con el bot para interacciones complejas." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a>Práctica recomendada: use pestañas o módulos de tareas

Si su bot proporciona una respuesta que requiere pasos adicionales, puede vincular a un módulo de tareas o a una pestaña para completar la tarea o el flujo.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Ejemplo que muestra cómo el bot debe evitar interacciones en varios turnos." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a>Práctica a evitar: hacer interacciones multiuso tediosas

Una conversación extensa para completar una tarea simple ralentiza y complica el proceso. También obliga al desarrollador a tener en cuenta cambios de estado (por ejemplo, tiempos de espera para la conversación o el envío de un mensaje de cancelación).

   :::column-end:::
:::row-end:::

### <a name="privacy"></a>Privacidad

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Ejemplo que muestra cómo los bots solo deben mostrar información privada en un contexto personal." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a>Práctica recomendada: muestre información confidencial solo en un contexto personal

Si el bot está en un chat o canal de grupo, le recomendamos que dirija a los usuarios a una ubicación privada (por ejemplo, un módulo de tareas, una pestaña o un explorador) para ver la información confidencial.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Ejemplo que muestra cómo los bots no deben revelar información confidencial a un grupo o personas." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a>Práctica a evitar: presentar a todo el mundo contenido confidencial

El bot no debería revelar información confidencial a un grupo de personas.

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también

A continuación, tiene guías adicionales que le pueden ayudar con el diseño del bot:

* [Diseño de su aplicación personal](../../concepts/design/personal-apps.md)
* [Diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md)
* [Diseño de módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
