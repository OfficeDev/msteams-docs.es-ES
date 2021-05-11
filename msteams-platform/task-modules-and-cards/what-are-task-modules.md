---
title: ¿Qué son los módulos de tareas?
author: clearab
description: Agregar experiencias emergentes modales para recopilar o mostrar información a los usuarios desde Microsoft Teams aplicaciones
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 7c047c02167e143cc8536c1dfcff3a335b18c46e
ms.sourcegitcommit: 20e623a82f9676dd036cf6a350dd480885e0ea2c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2021
ms.locfileid: "52300566"
---
# <a name="what-are-task-modules"></a>¿Qué son los módulos de tareas?

Los módulos de tareas le permiten crear experiencias emergentes modales en su aplicación de Teams. Dentro del elemento emergente puede ejecutar su propio código HTML/JavaScript personalizado, mostrar un widget basado en youtube o vídeo de Microsoft Stream o mostrar `<iframe>` una [tarjeta adaptable.](/adaptive-cards/) Son especialmente útiles para iniciar y completar tareas o para mostrar información enriquecid como vídeos o Power BI paneles. Una experiencia emergente suele ser más natural para los usuarios que inician y completan tareas en comparación con una pestaña o una experiencia de bot basada en conversación.

Los módulos de tareas se crean sobre la base Microsoft Teams pestañas; son esencialmente una pestaña dentro de una ventana emergente. Usan el mismo SDK, por lo que si has creado una pestaña ya estás en el 90 % de la forma de crear un módulo de tareas.

Los módulos de tarea pueden invocarse de tres maneras:

* **Pestañas de canal o personales.** Con el SDK Microsoft Teams Tabs puede invocar módulos de tareas desde botones, vínculos o menús de la pestaña. Esto [se trata detalladamente aquí.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Bots.** Botones en [las tarjetas](~/task-modules-and-cards/cards/cards-reference.md) enviadas desde el bot. Esto es especialmente útil cuando no necesita que todos los usuarios de un canal vean lo que está haciendo con un bot. Por ejemplo, cuando los usuarios responden a un sondeo de un canal, no resulta útil ver un registro de ese sondeo que se está creando. [Esto se trata detalladamente aquí.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **Fuera de Teams desde un vínculo profundo.** También puede crear direcciones URL para invocar un módulo de tareas desde cualquier lugar. [Esto se trata detalladamente aquí.](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>Cómo es un módulo de tareas

Este es el aspecto de un módulo de tareas cuando se invoca desde un bot (sin los rectángulos de colores y los círculos numerados, por supuesto):

![Ejemplo del módulo de tareas](~/assets/images/task-module/task-module-example.png)

Vamos a recorrerlo:

1. Icono de la [ `color` aplicación](~/resources/schema/manifest-schema.md#icons).
2. Nombre de la [ `short` aplicación](~/resources/schema/manifest-schema.md#name).
3. El título del módulo de tareas especificado en la `title` propiedad del [objeto TaskInfo](#the-taskinfo-object).
4. Botón cerrar/cancelar del módulo de tareas. Si el usuario presiona esto, la aplicación recibirá un `err` evento como se describe [aquí](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module). (**Nota:** Actualmente no es posible detectar este evento cuando se invoca un módulo de tareas desde un bot).
5. El rectángulo azul es el lugar donde aparece la página web si está cargando su propia página web mediante la propiedad `url` del [objeto TaskInfo](#the-taskinfo-object). Encontrará más detalles en la sección de tamaño [del módulo de](#task-module-sizing) tareas que se muestra a continuación.
6. Si va a mostrar una tarjeta adaptable a través de la propiedad del objeto TaskInfo, el relleno se agrega automáticamente, de lo contrario tendrá que `card` [controlarlo usted mismo.](#task-module-css-for-htmljavascript-task-modules) [](#the-taskinfo-object)
7. Aquí se representarán los botones de tarjeta adaptable. Si usa su propia página, debe crear sus propios botones.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Información general sobre invocar y descartar módulos de tareas

Los módulos de tareas se pueden invocar desde pestañas, bots o vínculos profundos y lo que aparece en uno puede ser HTML o una tarjeta adaptable, por lo que hay mucha flexibilidad en términos de cómo se invocan y cómo tratar el resultado de la interacción de un usuario. En la tabla siguiente se resume cómo funciona esto:

| **Invocado a través de...** | **El módulo de tareas es HTML/JavaScript** | **El módulo de tareas es tarjeta adaptable** |
| --- | --- | --- |
| **JavaScript en una pestaña** | 1. Use la función Teams SDK de cliente con una función de devolución de llamada `tasks.startTask()` `submitHandler(err, result)` opcional <br/><br/> 2. En el código del módulo de tareas, cuando el usuario haya terminado, llame a la función Teams SDK con `tasks.submitTask()` un `result` objeto como parámetro. Si se especificó una devolución de llamada `submitHandler` en , Teams la llama con como `tasks.startTask()` `result` parámetro.<br/><br/> 3. Si se produjo un error al invocar , se llama a la `tasks.startTask()` función con una cadena en su `submitHandler` `err` lugar. <br/><br/> 4. También puede especificar un al llamar; en `completionBotId` `teams.startTask()` ese caso, se envía al bot en `result` su lugar. | 1. Llame a la función Teams SDK de cliente con un objeto TaskInfo y que contenga el JSON para que la tarjeta adaptable se muestre en el elemento emergente `tasks.startTask()` del módulo de [](#the-taskinfo-object) `TaskInfo.card` tareas. <br/><br/> 2. Si se especificó una devolución de llamada en , Teams la llama con una cadena si se produjo un error al invocar o si el usuario cierra el elemento emergente del módulo de tareas con la X en la parte superior `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` derecha. <br/><br/> 3. Si el usuario presiona un botón Action.Submit, su `data` objeto se devuelve como el valor de `result` . |
| **Botón de tarjeta bot** | 1. Los botones de tarjeta bot, según el tipo de botón, pueden invocar módulos de tareas de dos maneras: una dirección URL de vínculo profundo o mediante el envío de un `task/fetch` mensaje. Vea a continuación cómo funcionan las direcciones URL de vínculo profundo. <br/><br/> 2. Si la acción del botón es ( tipo de botón para tarjetas adaptables), se envía un evento (un HTTP POST debajo de las portadas) al bot y el bot responde al POST con `type` `task/fetch` HTTP `Action.Submit` `task/fetch invoke` 200 [](#the-taskinfo-object)y al cuerpo de la respuesta que contiene un contenedor alrededor del objeto TaskInfo . Esto se explica detalladamente al [invocar un módulo de tareas mediante task/fetch](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch).<br/><br/> 3. Teams muestra el módulo de tareas; cuando el usuario haya terminado, llame a la Teams SDK `tasks.submitTask()` con un objeto como `result` parámetro. <br/><br/> 4. El bot recibe un `task/submit invoke` mensaje que contiene el `result` objeto. Tiene tres formas diferentes de responder al mensaje: no hacer nada (la tarea se completó correctamente), mostrar un mensaje al usuario en una ventana emergente o invocar otra ventana del módulo de tareas (es decir, crear una experiencia de `task/submit` asistente). Estas tres opciones se debaten más en [la discusión detallada sobre tarea/envío](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | 1. Al igual que los botones de las tarjetas de Bot Framework, los botones de las tarjetas adaptables admiten dos formas de invocar módulos de tareas: las direcciones URL de vínculo profundo con botones y el uso de `Action.openUrl` `task/fetch` `Action.Submit` botones. <br/><br/> 2. Los módulos de tareas con tarjetas adaptables funcionan de forma muy similar al caso HTML/JavaScript (vea la izquierda). La principal diferencia es que, dado que no hay JavaScript cuando se usan tarjetas adaptables, no hay forma de llamar a `tasks.submitTask()` . En su lugar, Teams toma el objeto y lo devuelve como la carga `data` `Action.Submit` del `task/submit` evento, como se describe [aquí](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). |
| **URL de vínculo profundo** <br/>[sintaxis URL](#task-module-deep-link-syntax) | 1. Teams invoca el módulo de tareas; la dirección URL que aparece dentro `<iframe>` del especificado en el parámetro del vínculo `url` profundo. No hay `submitHandler` devolución de llamada. <br/><br/> 2. Dentro del JavaScript de la página del módulo de tareas, llame para cerrarlo con un objeto como parámetro, lo mismo que al invocarlo desde una pestaña o un botón de tarjeta `tasks.submitTask()` `result` de bot. Sin embargo, la lógica de finalización es ligeramente diferente. Si la lógica de finalización reside en el cliente (es decir, si no hay bot) no hay devolución de llamada, por lo que cualquier lógica de finalización debe estar en el código anterior a la llamada `submitHandler` a `tasks.submitTask()` . Los errores de invocación solo se notifican a través de la consola. Si tiene un bot, puede especificar un parámetro en el vínculo profundo para `completionBotId` enviar el objeto a través de un `result` `task/submit` evento. | 1. Teams invoca el módulo de tareas; el cuerpo de la tarjeta JSON de la tarjeta adaptable se especifica como un valor codificado en URL del `card` parámetro del vínculo profundo. <br/><br/> 2. El usuario cierra el módulo de tareas haciendo clic en la X en la parte superior derecha del módulo de tareas o presionando un `Action.Submit` botón en la tarjeta. Dado que no hay que llamar, debe tener un bot al que enviar el valor de `submitHandler` los campos de tarjeta adaptable. Use el parámetro en el vínculo profundo para especificar el bot al que `completionBotId` se enviarán los datos a través de un `task/submit invoke` evento. |

## <a name="the-taskinfo-object"></a>El objeto TaskInfo

El `TaskInfo` objeto contiene los metadatos de un módulo de tareas. La definición de objeto está a continuación. Debe **definir** `url` (para un iFrame incrustado) o `card` (para una tarjeta adaptable).

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `title` | string | Aparece debajo del nombre de la aplicación y a la derecha del icono de la aplicación |
| `height` | número o cadena | Puede ser un número que representa el alto del módulo de tareas en píxeles, `small` o , `medium` o `large` . [Vea a continuación cómo se controlan el alto y el ancho](#task-module-sizing). |
| `width` | número o cadena | Puede ser un número que representa el ancho del módulo de tareas en píxeles, `small` o , `medium` o `large` . [Vea a continuación cómo se controlan el alto y el ancho](#task-module-sizing). |
| `url` | cadena | Dirección URL de la página cargada como dentro `<iframe>` del módulo de tareas. El dominio de la dirección URL debe estar en la matriz [validDomains](~/resources/schema/manifest-schema.md#validdomains) de la aplicación en el manifiesto de la aplicación. |
| `card` | Tarjeta adaptable o datos adjuntos de una tarjeta de bot de tarjeta adaptable | Json para que la tarjeta adaptable aparezca en el módulo de tareas. Si invocas desde un bot, tendrás que usar el JSON de tarjeta adaptable en un objeto Bot `attachment` Framework. Desde una pestaña, usarás solo una tarjeta adaptable. [Este es un ejemplo.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | cadena | Si un cliente no admite la característica del módulo de tareas, esta dirección URL se abre en una pestaña del explorador. |
| `completionBotId` | cadena | Especifica un identificador de aplicación de bot al que enviar el resultado de la interacción del usuario con el módulo de tareas. Si se especifica, el bot recibirá un `task/submit invoke` evento con un objeto JSON en la carga del evento. |

> [!NOTE]
> La característica del módulo de tareas requiere que los dominios de las direcciones URL que quiera cargar se incluyan en la matriz en el `validDomains` manifiesto de la aplicación.

## <a name="task-module-sizing"></a>Tamaño del módulo de tareas

El uso de números enteros `TaskInfo.width` para `TaskInfo.height` y establecerá el alto y el ancho en píxeles. Sin embargo, según el tamaño de la ventana y la resolución de pantalla del equipo, se reducirán proporcionalmente mientras se mantiene la relación de aspecto (ancho/alto).

Si y son , o el tamaño del rectángulo rojo de la imagen anterior es una proporción del espacio `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` disponible: 20%, 50%, 60% para `width` y 20%, 50%, 66% para `height` .

Los módulos de tareas invocados desde una pestaña se pueden cambiar dinámicamente. Después de llamar, puede llamar a donde las propiedades height y width del `tasks.startTask()` `tasks.updateTask(newSize)` objeto newSize se ajustan a la especificación TaskInfo (ex. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>CSS del módulo de tareas para módulos de tareas HTML/JavaScript

Los módulos de tareas basados en HTML/JavaScript tienen acceso a todo el área del módulo de tareas debajo del encabezado. Aunque esto ofrece una gran flexibilidad, si quieres que el relleno alrededor de los bordes se alinee con los elementos de encabezado y evite barras de desplazamiento innecesarias, tendrás que proporcionar el CSS correcto. Estos son algunos ejemplos para algunos casos de uso.

### <a name="example-1---youtube-video"></a>Ejemplo 1: vídeo de YouTube

YouTube ofrece la posibilidad de insertar vídeos en páginas web. Con una página web de código auxiliar simple es fácil mostrar esto en un módulo de tareas:

![Vídeo de YouTube](~/assets/images/task-module/youtube-example.png)

Este es el CÓDIGO HTML de esta página, sin css:

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

El CSS tiene este aspecto:

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

También puede usar el mismo enfoque para insertar una PowerApp. Como el alto/ancho de cualquier PowerApp individual es personalizable, es posible que deba ajustar el alto y el ancho para lograr la presentación deseada.

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Datos adjuntos de tarjeta adaptable o de bot de tarjeta adaptable

Como hemos indicado anteriormente, en función de cómo invojes a la tarjeta, tendrás que usar una tarjeta adaptable o un archivo adjunto de tarjeta de bot de tarjeta adaptable (que es solo una tarjeta adaptable envuelta en un objeto de datos `card` adjuntos).

Cuando invocas desde una pestaña, tendrás que usar una tarjeta adaptable. Este es un ejemplo muy sencillo:

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

Cuando invocas desde un bot, tendrás que usar un archivo adjunto de tarjeta de bot de tarjeta adaptable como en el ejemplo siguiente:

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

Tendrás que recordar si estás invocando un módulo de tareas que contiene una tarjeta adaptable desde un bot o una pestaña.

## <a name="task-module-deep-link-syntax"></a>Sintaxis de vínculo profundo del módulo de tareas

Un vínculo profundo del módulo de tareas es solo una serialización del [objeto TaskInfo](#the-taskinfo-object) con otras dos partes de información, y `APP_ID` opcionalmente: `BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Vea [Objeto TaskInfo para](#the-taskinfo-object) los tipos de datos y los valores permitidos para , , , y `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` .

> [!TIP]
> Asegúrese de codificar el vínculo profundo en dirección URL, especialmente al usar el `card` parámetro (por ejemplo, la función de [ `encodeURI()` JavaScript](https://www.w3schools.com/jsref/jsref_encodeURI.asp)).

Esta es la información sobre `APP_ID` y `BOT_APP_ID` :

| Valor | Tipo | ¿Necesario? | Descripción |
| --- | --- | --- | --- |
| `APP_ID` | string | Sí | El [identificador](~/resources/schema/manifest-schema.md#id) de la aplicación que invoca el módulo de tareas. La [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) del manifiesto `APP_ID` para debe contener el dominio para if está en la dirección `url` `url` URL. (El identificador de la aplicación ya se conoce cuando se invoca un módulo de tareas desde una pestaña o un bot, por lo que no se incluye en `TaskInfo` .) |
| `BOT_APP_ID` | string | No | Si se especifica un valor para, el objeto se envía a través de `completionBotId` un mensaje al bot `result` `task/submit invoke` especificado. `BOT_APP_ID` debe especificarse como bot en el manifiesto de la aplicación, es decir, no puede enviarlo a ningún bot. |

Ten en cuenta que es válido para y para ser el mismo, y en muchos casos será si una aplicación tiene un bot, ya que se recomienda usarlo como identificador de una aplicación si hay `APP_ID` `BOT_APP_ID` uno.

## <a name="keyboard-and-accessibility-guidelines"></a>Directrices de teclado y accesibilidad

Con los módulos de tareas basados en HTML/JavaScript, es tu responsabilidad garantizar que el módulo de tareas de la aplicación se pueda usar con un teclado. Los programas de lector de pantalla también dependen de la capacidad de navegar con el teclado. Como cuestión práctica, esto significa dos cosas:

1. Usar el [atributo tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) en las etiquetas HTML para controlar qué elementos se pueden centrar y si/dónde participa en la navegación secuencial del teclado (normalmente con las teclas <kbd>Tab</kbd> y <kbd>Mayús-Tab).</kbd>
2. Control de <kbd>la clave Esc</kbd> en JavaScript para el módulo de tareas. Este es un ejemplo de código que muestra cómo hacerlo:

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams garantizará que la navegación del teclado funcione correctamente desde el encabezado del módulo de tareas al HTML y viceversa.

## <a name="code-sample"></a>Ejemplo de código
|**Nombre de ejemplo** | **Descripción** | **.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Ejemplo de módulo de tareas (Bots-V4) | Ejemplos para crear módulos de tareas. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|Ejemplo de módulo de tareas (Tabs + Bots-V3) | Ejemplos para crear módulos de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|



> [!div class="nextstepaction"]
> [Más información: Solicitar permisos de dispositivo](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [Más información: Integrar funcionalidades multimedia](../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Más información: Integrar la funcionalidad del escáner de códigos de barras o QR en Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Más información: Integrar las capacidades de ubicación en Teams](../concepts/device-capabilities/location-capability.md)
