---
title: ¿Qué son los módulos de tareas?
author: clearab
description: Agregar experiencias emergentes modales para recopilar o Mostrar información a los usuarios de las aplicaciones de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 22fdc7a9dab1ff6f27e2b0d144e54676b6cca50e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676146"
---
# <a name="what-are-task-modules"></a>¿Qué son los módulos de tareas?

Los módulos de tareas le permiten crear experiencias de elemento emergente modal en su aplicación de Teams. Dentro del elemento emergente, puede ejecutar su propio código HTML/JavaScript personalizado, Mostrar `<iframe>`un widget basado en un (por ejemplo, YouTube o Microsoft Stream video) o mostrar una [tarjeta adaptable](/adaptive-cards/). Son especialmente útiles para iniciar y completar tareas o para mostrar información enriquecida como vídeos o paneles de Power BI. A menudo, una experiencia emergente es más natural para los usuarios que inician y completan tareas en comparación con una experiencia de ficha o de robot basada en conversaciones.

Los módulos de tareas se basan en la base de las pestañas de Microsoft Teams; Básicamente, se trata de una pestaña dentro de una ventana emergente. Usan el mismo SDK, por lo que, si ha creado una pestaña, ya es 90% del camino para poder crear un módulo de tareas.

Los módulos de tareas se pueden invocar de tres maneras:

* **Fichas de canal o personal.** Mediante el SDK de pestañas de Microsoft Teams, puede invocar módulos de tareas desde botones, vínculos o menús en la ficha. [esto se describe en detalle aquí.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Transferido.** Botones en [tarjetas](~/task-modules-and-cards/cards/cards-reference.md) enviadas desde el bot. Esto es especialmente útil cuando no es necesario que todos los usuarios estén en un canal para ver lo que está haciendo con un bot. Por ejemplo, cuando los usuarios responden a un sondeo en un canal, no es muy útil ver un registro del sondeo que se está creando. [Esto se describe en detalle aquí.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **Fuera de los equipos desde un vínculo profundo.** También puede crear direcciones URL para invocar un módulo de tareas desde cualquier lugar. [Esto se describe en detalle aquí.](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>Aspecto de un módulo de tareas

Así es como se ve un módulo de tareas cuando se invoca desde un bot (sin los rectángulos coloreados y círculos numerados, por supuesto):

![Ejemplo de módulo de tarea](~/assets/images/task-module/task-module-example.png)

Vamos a examinarlo:

1. [ `color` Icono](~/resources/schema/manifest-schema.md#icons)de la aplicación.
2. El [ `short` nombre](~/resources/schema/manifest-schema.md#name)de la aplicación.
3. Título del módulo de tarea especificado en la `title` propiedad del [objeto TaskInfo](#the-taskinfo-object).
4. El botón Cerrar/cancelar del módulo de tareas. Si el usuario presiona esto, la aplicación recibirá un `err` evento tal y como se describe [aquí](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module). (**Nota:** actualmente no es posible detectar este evento cuando se invoca un módulo de tareas desde un bot).
5. El rectángulo azul es donde aparece la página web si está cargando su propia página web con la `url` propiedad del [objeto TaskInfo](#the-taskinfo-object). Encontrará más detalles en la sección [tamaño del módulo de tareas](#task-module-sizing) que aparece a continuación.
6. Si va a mostrar una tarjeta adaptable a `card` través de la propiedad del [objeto TaskInfo](#the-taskinfo-object) , el relleno se agrega de forma manual; de lo contrario, deberá [controlarlo por su cuenta](#task-module-css-for-htmljavascript-task-modules).
7. Los botones de tarjeta adaptable se representarán aquí. Si está usando su propia página, debe crear sus propios botones.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Información general sobre cómo invocar y desechar módulos de tareas

Los módulos de tareas se pueden invocar desde fichas, bots o vínculos profundos, y lo que aparece en uno puede ser HTML o una tarjeta adaptable, por lo que hay mucha flexibilidad en cuanto a cómo se invocan y cómo tratar con el resultado de la interacción del usuario. La siguiente tabla resume cómo funciona esto:

| **Invocado a través de...** | **El módulo de tareas es HTML/JavaScript** | **El módulo de tareas es una tarjeta adaptable** |
| --- | --- | --- |
| **JavaScript en una pestaña** | 1. usar la función `tasks.startTask()` cliente de Teams con una `submitHandler(err, result)` función de devolución de llamada opcional <br/><br/> 2. en el código del módulo de tareas, cuando el usuario haya finalizado, llame a `tasks.submitTask()` la función `result` de Team SDK con un objeto como parámetro. Si se `submitHandler` especificó una devolución `tasks.startTask()`de llamada en, teams la llama `result` como un parámetro.<br/><br/> 3. Si se produce un error al invocar `tasks.startTask()`, se `submitHandler` llama a la función con `err` una cadena en su lugar. <br/><br/> 4. también puede especificar un `completionBotId` cuando la llamada `teams.startTask()` , en cuyo caso `result` se envía al bot en su lugar. | 1. llamar a la función `tasks.startTask()` del SDK del cliente de Microsoft Teams con un [objeto TaskInfo](#the-taskinfo-object) y `TaskInfo.card` que contenga el JSON de la tarjeta adaptable para mostrar en el menú emergente del módulo de tareas. <br/><br/> 2. Si se `submitHandler` especificó una devolución `tasks.startTask()`de llamada en, Teams `err` la llama con una cadena si se produjo un `tasks.startTask()` error al invocar o si el usuario cierra el elemento emergente del módulo de tarea con la X en la esquina superior derecha. <br/><br/> 3. Si el usuario presiona un botón Action. Submit, su `data` objeto se devuelve como el valor de `result`. |
| **Botón ficha bot** | 1. los botones de la tarjeta de bot, según el tipo de botón, pueden invocar módulos de tareas de dos maneras: una dirección URL de `task/fetch` vínculo profundo o mediante el envío de un mensaje. Vea a continuación cómo funcionan las direcciones URL de vínculo en profundidad. <br/><br/> 2. Si `type` la acción del botón es `task/fetch` (`Action.Submit` tipo de botón para tarjetas adaptables) `task/fetch invoke` , se envía un evento (un post http en las cubiertas) al bot y el bot responde a la entrada con http 200 y al cuerpo de la respuesta que contiene un contenedor alrededor del [objeto TaskInfo](#the-taskinfo-object). Esto se explica en detalle en [invocación de un módulo de tareas a través de la tarea/obtención](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch).<br/><br/> 3. Teams muestra el módulo de tareas; Cuando el usuario haya finalizado, llame a la función `tasks.submitTask()` de Team `result` SDK con un objeto como parámetro. <br/><br/> 4. el bot recibe un `task/submit invoke` mensaje que contiene el `result` objeto. Tiene tres formas diferentes de responder al `task/submit` mensaje: no hacer nada (la tarea se completó correctamente), mostrar un mensaje al usuario en una ventana emergente o invocar otra ventana del módulo de tareas (es decir, la creación de una experiencia similar a un asistente). Estas tres opciones se describen más [en la descripción detallada sobre la tarea o el envío](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | 1. al igual que los botones de las tarjetas de la plataforma de bots, los botones de las tarjetas adaptables admiten dos `Action.openUrl` formas de invocar `task/fetch` módulos `Action.Submit` de tareas: direcciones URL de vínculo profundas con botones y mediante botones. <br/><br/> 2. los módulos de tareas con tarjetas adaptables funcionan de forma muy similar al caso de HTML/JavaScript (vea la izquierda). La principal diferencia es que, dado que no hay JavaScript cuando se usan tarjetas adaptables, no hay forma de llamar `tasks.submitTask()`. En su lugar, Teams `data` toma el `Action.Submit` objeto de y lo devuelve como la carga del `task/submit` evento, tal como se describe [aquí](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). |
| **Dirección URL de vínculo profundo** <br/>[sintaxis URL](#task-module-deep-link-syntax) | 1. Microsoft Teams invoca el módulo de tareas; Dirección URL que aparece dentro del `<iframe>` especificado en el `url` parámetro del vínculo en profundidad. No hay ninguna `submitHandler` devolución de llamada. <br/><br/> 2. en el JavaScript de la página en el módulo de tareas, `tasks.submitTask()` llame a para cerrarla `result` con un objeto como parámetro, igual que cuando se invoca desde un botón de ficha o de tarjeta de bot. Sin embargo, la lógica de finalización es ligeramente diferente. Si la lógica de finalización reside en el cliente (es decir, si no hay ningún bot), no `submitHandler` hay ninguna devolución de llamada, por lo que cualquier lógica de finalización debe `tasks.submitTask()`estar en el código anterior a la llamada a. Los errores de invocación solo se notifican a través de la consola. Si tiene un bot, puede especificar un `completionBotId` parámetro en el vínculo profundo para enviar el `result` objeto a través de un `task/submit` evento. | 1. Microsoft Teams invoca el módulo de tareas; el cuerpo de la tarjeta JSON de la tarjeta adaptable se especifica como un valor codificado como URL `card` del parámetro del vínculo profundo. <br/><br/> 2. el usuario cierra el módulo de tareas haciendo clic en la X en la esquina superior derecha del módulo de tareas o presionando un `Action.Submit` botón de la tarjeta. Como no hay llamada `submitHandler` a, debe tener un bot para enviar el valor de los campos de la tarjeta adaptable a. Use el `completionBotId` parámetro en el vínculo profundo para especificar el bot al que se van a enviar los datos `task/submit invoke` a través de un evento. |

> [!NOTE]
> La invocación de un módulo de tareas desde JavaScript no se admite en dispositivos móviles.

## <a name="the-taskinfo-object"></a>El objeto TaskInfo

El `TaskInfo` objeto contiene los metadatos de un módulo de tareas. A continuación se muestra la definición del objeto. **Debe** definir `url` (for en iframe incrustado) o `card` (para una tarjeta adaptable).

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `title` | string | Aparece debajo del nombre de la aplicación y a la derecha del icono de la aplicación |
| `height` | número o cadena | Puede ser un número que representa el alto del módulo de tareas en píxeles, `small`o `medium`, o `large`. [Vea a continuación cómo se administran el alto y el ancho](#task-module-sizing). |
| `width` | número o cadena | Puede ser un número que representa el ancho del módulo de tareas en píxeles, `small`o `medium`, o `large`. [Vea a continuación cómo se administran el alto y el ancho](#task-module-sizing). |
| `url` | string | La dirección URL de la página cargada como `<iframe>` dentro del módulo de tareas. El dominio de la dirección URL debe estar en la [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) de la aplicación en el manifiesto de la aplicación. |
| `card` | Datos adjuntos de tarjeta de robot adaptable o tarjeta de adaptación | El JSON para que la tarjeta adaptable aparezca en el módulo de tareas. Si va a invocar desde un bot, deberá usar el JSON de la tarjeta adaptable en un objeto de `attachment` bot Framework. En una pestaña, usará solo una tarjeta adaptable. [Este es un ejemplo.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | Si un cliente no admite la característica de módulo de tareas, esta dirección URL se abre en una pestaña del explorador. |
| `completionBotId` | string | Especifica un identificador de aplicación de bot para enviar el resultado de la interacción del usuario con el módulo de tareas a. Si se especifica, el bot recibirá `task/submit invoke` un evento con un objeto JSON en la carga del evento. |

> [!NOTE]
> La característica de módulo de tareas requiere que los dominios de las direcciones URL que desee cargar se incluyan en la `validDomains` matriz del manifiesto de la aplicación.

## <a name="task-module-sizing"></a>Tamaño del módulo de tareas

Si se usan enteros `TaskInfo.width` para `TaskInfo.height` y se establecerá el alto y el ancho en píxeles. Sin embargo, en función del tamaño de la ventana y la resolución de la pantalla del equipo, se reducirán proporcionalmente, a la vez que se mantiene la relación de aspecto (ancho/alto).

Si `TaskInfo.width` y `TaskInfo.height` son `"small"`, `"medium"` o `"large"` el tamaño del rectángulo rojo de la imagen anterior es una proporción del espacio disponible: 20%, 50%, 60% para `width` y 20%, 50%, 66% para. `height`

Los módulos de tareas invocados desde una ficha pueden cambiarse de tamaño dinámicamente. Después de `tasks.startTask()` llamar, puede `tasks.updateTask(newSize)` llamar a donde las propiedades Height y width del objeto NewSize se ajustan a la especificación TaskInfo (p. ej. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>CSS del módulo de tareas para módulos de tareas de HTML/JavaScript

Los módulos de tareas basados en HTML/JavaScript tienen acceso a todo el área del módulo de tareas debajo del encabezado. Aunque esto ofrece una gran flexibilidad, si desea que los bordes alrededor de los bordes se alineen con los elementos de encabezado y evite las barras de desplazamiento innecesarias, deberá proporcionar la CSS correcta. A continuación se muestran algunos ejemplos de algunos casos de uso.

### <a name="example-1---youtube-video"></a>Ejemplo 1: vídeo de YouTube

YouTube ofrece la capacidad de insertar vídeos en páginas Web. Con una página web de código auxiliar sencilla es fácil mostrar esto en un módulo de tareas:

![Vídeo de YouTube](~/assets/images/task-module/youtube-example.png)

Este es el HTML de esta página, sin CSS:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

La CSS tiene el siguiente aspecto:

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

### <a name="example-2---powerapp"></a>Ejemplo 2: PowerApp

Puede usar el mismo enfoque para insertar una PowerApp también. A medida que el alto o el ancho de una PowerApp individual es personalizable, es posible que deba ajustar la altura y el ancho para obtener la presentación deseada.

![PowerApp de administración de activos](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

Y el CSS es:

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Archivo adjunto de tarjeta adaptable o tarjeta de robot adaptable

Como se indicó anteriormente, en función de cómo invoque su `card` , tendrá que usar una tarjeta adaptable o un adjunto de tarjeta de bot? o de tarjeta adaptable (que es solo una tarjeta adaptable incluida en un objeto Attachment).

Cuando se realiza una llamada desde una pestaña, deberá usar una tarjeta adaptable. Este es un ejemplo muy sencillo:

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat:"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png",
            "size": "Medium"
        }
    ],
    "version": "1.0"
}
```

Al invocar desde un bot, deberá usar un adjunto de tarjeta de bot de tarjeta adaptable como en el ejemplo siguiente:

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
        "type": "AdaptiveCard",
        "body": [
            {
                "type": "TextBlock",
                "text": "Here is a ninja cat:"
            },
            {
                "type": "Image",
                "url": "http://adaptivecards.io/content/cats/1.png",
                "size": "Medium"
            }
        ],
        "version": "1.0"
    }
}
```

Deberá recordar si va a invocar un módulo de tareas que contiene una tarjeta adaptable desde un bot o una pestaña.

## <a name="task-module-deep-link-syntax"></a>Sintaxis de vínculo profundo del módulo de tareas

Un vínculo profundo del módulo de tareas es solo una serialización del [objeto TaskInfo](#the-taskinfo-object) con dos otras partes de la `APP_ID` información y, de `BOT_APP_ID`manera opcional, la:

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Vea [el objeto TaskInfo](#the-taskinfo-object) para los tipos de datos y los valores `<TaskInfo.url>`permitidos `<TaskInfo.height>`para `<TaskInfo.width>`, `<TaskInfo.card>`, `<TaskInfo.title>`, y.

> [!TIP]
> Asegúrese de codificar mediante URL el vínculo profundo, especialmente cuando use el `card` parámetro (por ejemplo, la [ `encodeURI()` función](https://www.w3schools.com/jsref/jsref_encodeURI.asp)de JavaScript).

Esta es la información sobre `APP_ID` y `BOT_APP_ID`:

| Valor | Tipo | ¿Necesario? | Descripción |
| --- | --- | --- | --- |
| `APP_ID` | string | Sí | El [identificador](~/resources/schema/manifest-schema.md#id) de la aplicación que invoca el módulo de tareas. La [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) del manifiesto `APP_ID` debe contener el dominio para `url` si `url` se encuentra en la dirección URL. (El identificador de la aplicación ya se conoce cuando se invoca un módulo de tareas desde una pestaña o un bot, que es el motivo por el `TaskInfo`que no se incluye en). |
| `BOT_APP_ID` | string | No | Si se especifica un `completionBotId` valor para, el `result` objeto se envía a través de `task/submit invoke` un mensaje al bot especificado. `BOT_APP_ID`debe especificarse como un bot en el manifiesto de la aplicación, es decir, no puede simplemente enviarlo a ningún bot. |

Tenga en cuenta que es válido `APP_ID` tanto `BOT_APP_ID` para como para ser el mismo y, en muchos casos, si una aplicación tiene un bot, ya que se recomienda usarlo como el identificador de una aplicación, en caso de existir.

## <a name="keyboard-and-accessibility-guidelines"></a>Directrices de teclado y accesibilidad

Con los módulos de tareas basados en HTML/JavaScript, es su responsabilidad asegurarse de que el módulo de tareas de la aplicación puede usarse con un teclado. Los programas de lector de pantalla también dependen de la capacidad de navegar con el teclado. Como un asunto práctico, significa dos cosas:

1. Usar el [atributo TabIndex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) en las etiquetas HTML para controlar qué elementos se pueden centrar y si está participando en la navegación secuencial de teclado (normalmente con las teclas <kbd>Tab</kbd> y <kbd>MAYÚS-TAB</kbd> ).
2. Control de la tecla <kbd>ESC</kbd> en JavaScript para el módulo de tareas. Este es un ejemplo de código que muestra cómo hacerlo:

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams garantizará que la navegación mediante teclado funciona correctamente desde el encabezado del módulo de tareas hasta el código HTML y viceversa.

## <a name="task-module-samples"></a>Ejemplos de módulos de tareas

* [Ejemplo de node. js/TypeScript](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [Ejemplo/.NET de C#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)
