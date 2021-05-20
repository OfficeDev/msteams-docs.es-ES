---
title: ¿Qué son los módulos de tareas?
author: clearab
description: Añade experiencias emergentes modales para recopilar o mostrar información a tus usuarios desde tus aplicaciones de Microsoft Teams
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23157e30ce25c2dfa1c21e7f5c4ddd4f735b660f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566847"
---
# <a name="task-modules"></a>Módulos de tareas

Los módulos de tareas le permiten crear experiencias emergentes modales en su aplicación de Teams. Dentro de la ventana emergente puede ejecutar su propio código HTML /JavaScript personalizado, mostrar un `<iframe>` widget basado en un YouTube o Microsoft Stream o mostrar una tarjeta [adaptable.](/adaptive-cards/) Son especialmente útiles para iniciar y completar tareas o mostrar información enriquecida como vídeos o paneles de Power BI. Una experiencia emergente suele ser más natural para los usuarios que inician y completan tareas en comparación con una pestaña o una experiencia de bot basada en conversaciones.

Los módulos de tareas se basan en la base de Microsoft Teams pestañas; son esencialmente una pestaña dentro de una ventana emergente. Usan el mismo SDK, por lo que si ha creado una pestaña, ya está al 90% de la forma de poder crear un módulo de tareas.

Los módulos de tarea pueden invocarse de tres maneras:

* **Canal o pestañas personales:** con el SDK de Microsoft Teams Tabs puede invocar módulos de tareas desde botones, vínculos o menús de la [pestaña.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Bots**: Botones en [las tarjetas](~/task-modules-and-cards/cards/cards-reference.md) enviadas desde el bot. Esto es particularmente útil cuando no necesitas a todos en un canal para ver lo que estás haciendo con un bot. Por ejemplo, cuando los usuarios responden a un sondeo de un canal, no resulta útil ver un registro de ese sondeo que se está creando. [Esto está cubierto en detalle aquí.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **Fuera de Teams desde un vínculo profundo:** también puede crear direcciones URL para invocar un módulo de tareas desde cualquier lugar. [Esto está cubierto en detalle aquí.](#task-module-deep-link-syntax)

## <a name="task-module-looks-like"></a>El módulo de tareas parece

Así es como se ve un módulo de tareas cuando se invoca desde un bot (sin los rectángulos de color y los círculos numerados, por supuesto):

![Ejemplo del módulo de tareas](~/assets/images/task-module/task-module-example.png)

Vamos a caminar a través de él:

1. Icono de [ `color` ](~/resources/schema/manifest-schema.md#icons)la aplicación.
1. El [ `short` nombre](~/resources/schema/manifest-schema.md#name)de la aplicación.
1. Título del módulo de tareas especificado en la `title` propiedad del [objeto TaskInfo](#the-taskinfo-object).
1. El botón de cierre/cancelación del módulo de tareas. Si el usuario presiona esto, la aplicación recibirá un `err` evento como se describe [aquí.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)
    > [!Note]
    > Actualmente no es posible detectar este evento cuando se invoca un módulo de tareas desde un bot.
1. El rectángulo azul es el lugar donde aparece la página web si está cargando su propia página web mediante la `url` propiedad del [objeto TaskInfo](#the-taskinfo-object). Más detalles está en la sección [de tamaño del módulo de tareas](#task-module-sizing) a continuación.
1. Si está mostrando una tarjeta adaptable a través de la `card` propiedad del [objeto TaskInfo,](#the-taskinfo-object) el relleno se agrega para usted, de lo contrario tendrá que [manejar esto usted mismo.](#task-module-css-for-htmljavascript-task-modules)
1. Los botones de tarjeta adaptables se representarán aquí. Si usas tu propia página, debes crear tus propios botones.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Visión general de la invocación y desestimación de módulos de tareas

Los módulos de tareas se pueden invocar desde pestañas, bots o vínculos profundos y lo que aparece en uno puede ser HTML o una tarjeta adaptable, por lo que hay mucha flexibilidad en términos de cómo se invocan y cómo lidiar con el resultado de la interacción de un usuario. La siguiente tabla resume cómo funciona esto:

| **Invocado a través de...** | **El módulo de tareas es HTML/JavaScript** | **Módulo de tareas es tarjeta adaptable** |
| --- | --- | --- |
| **JavaScript en una pestaña** | 1. Utilice la función SDK de cliente Teams `tasks.startTask()` con una función de devolución de llamada `submitHandler(err, result)` opcional. <br/><br/> 2. En el código del módulo de tareas, cuando el usuario haya terminado, llame a la función SDK de Teams `tasks.submitTask()` con un objeto como `result` parámetro. Si `submitHandler` se especificó una devolución de llamada en , Teams la llama como `tasks.startTask()` `result` parámetro.<br/><br/> 3. Si hubo un error al `tasks.startTask()` invocar, se llama a la función con una cadena en `submitHandler` su `err` lugar. <br/><br/> 4. También puede especificar un `completionBotId` al llamar - en ese caso se envía al bot en su `teams.startTask()` `result` lugar. | 1. Llame a la función SDK de cliente Teams `tasks.startTask()` con un [objeto TaskInfo](#the-taskinfo-object) y `TaskInfo.card` que contenga el JSON para que la tarjeta adaptable se muestre en la ventana emergente del módulo de tareas. <br/><br/> 2. Si se especificó una `submitHandler` devolución de llamada en , Teams la llama con una cadena si hubo un error al invocar `tasks.startTask()` o si el usuario cierra la ventana emergente del módulo de tareas usando la `err` X en la parte superior `tasks.startTask()` derecha. <br/><br/> 3. Si el usuario presiona un action.submit botón entonces su `data` objeto se devuelve como el valor de `result` . |
| **Botón de la tarjeta bot** | 1. Los botones de la tarjeta bot, dependiendo del tipo de botón, pueden invocar módulos de tareas de dos maneras: una URL de vínculo profundo o mediante el envío de un `task/fetch` mensaje. Consulte a continuación cómo funcionan las DIRECCIONES URL de vínculo profundo. <br/><br/> 2. Si la acción del botón es ( tipo de `type` `task/fetch` botón para tarjetas `Action.Submit` `task/fetch invoke` adaptables), se envía un evento (un HTTP POST bajo las cubiertas) al bot, y el bot responde al POST con HTTP 200 y el cuerpo de respuesta que contiene un contenedor alrededor del [objeto TaskInfo](#the-taskinfo-object). Esto se explica en detalle al [invocar un módulo de tareas a través de tareas/captura.](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch)<br/><br/> 3. Teams muestra el módulo de tareas; cuando el usuario haya terminado, llame a la función SDK de Teams `tasks.submitTask()` con un objeto como `result` parámetro. <br/><br/> 4. El bot recibe un `task/submit invoke` mensaje que contiene el `result` objeto. Tiene tres maneras diferentes de responder al `task/submit` mensaje: no hacer nada (la tarea completada correctamente), mostrando un mensaje al usuario en una ventana emergente o invocando otra ventana del módulo de tareas (es decir, creando una experiencia similar a una asistente). Estas tres opciones se discuten más [en el debate detallado sobre la tarea/envío.](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) | 1. Al igual que los botones de las tarjetas Bot Framework, los botones de las tarjetas adaptables admiten dos formas de invocar módulos de tareas: URL de enlace profundo con `Action.openUrl` botones y a través del uso de `task/fetch` `Action.Submit` botones. <br/><br/> 2. Los módulos de tareas con tarjetas adaptables funcionan de forma muy similar al caso HTML/JavaScript (véase la izquierda). La principal diferencia es que como no hay JavaScript cuando usas tarjetas adaptables, no hay forma de `tasks.submitTask()` llamar. En su lugar, Teams toma el `data` objeto y lo devuelve como la carga útil del `Action.Submit` `task/submit` evento, como se describe [aquí.](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) |
| **URL de enlace profundo** <br/>[sintaxis URL](#task-module-deep-link-syntax) | 1. Teams invoca el módulo de tareas; la dirección URL que aparece dentro de lo `<iframe>` especificado en el parámetro del vínculo `url` profundo. No hay `submitHandler` devolución de llamada. <br/><br/> 2. Dentro del JavaScript de la página en el módulo de tareas, llame `tasks.submitTask()` para cerrarlo con un `result` objeto como parámetro, lo mismo que al invocarlo desde una pestaña o un botón de tarjeta bot. Sin embargo, la lógica de finalización es ligeramente diferente. Si la lógica de finalización reside en el cliente (es decir, si no hay ningún bot) no hay `submitHandler` devolución de llamada, por lo que cualquier lógica de finalización debe estar en el código anterior a la llamada a `tasks.submitTask()` . Los errores de invocación solo se notifican a través de la consola. Si tiene un bot, puede especificar un `completionBotId` parámetro en el vínculo profundo para enviar el objeto a través de un `result` `task/submit` evento. | 1. Teams invoca el módulo de tareas; el cuerpo de la tarjeta JSON de la tarjeta adaptable se especifica como un valor codificado por URL del `card` parámetro del vínculo profundo. <br/><br/> 2. El usuario cierra el módulo de tareas haciendo clic en la X en la parte superior derecha del módulo de tareas o presionando un `Action.Submit` botón en la tarjeta. Puesto que no hay `submitHandler` que llamar, debe tener un bot al que enviar el valor de los campos de la tarjeta adaptable. Utilice el `completionBotId` parámetro del vínculo profundo para especificar el bot al que desea enviar los datos a través de un `task/submit invoke` evento. |

## <a name="the-taskinfo-object"></a>El objeto TaskInfo

El `TaskInfo` objeto contiene los metadatos de un módulo de tareas. La definición de objeto está a continuación. **Debe** definir para `url` un iFrame incrustado o `card` para una tarjeta adaptable.

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `title` | string | Aparece debajo del nombre de la aplicación y a la derecha del icono de la aplicación. |
| `height` | número o cadena | Puede ser un número que represente la altura del módulo de tareas en píxeles, o `small` `medium` , o `large` . [Consulte a continuación cómo se manejan la altura y el ancho.](#task-module-sizing) |
| `width` | número o cadena | Puede ser un número que represente el ancho del módulo de tareas en píxeles, o `small` `medium` , o `large` . [Consulte a continuación cómo se manejan la altura y el ancho.](#task-module-sizing) |
| `url` | cadena | La dirección URL de la página cargada como un `<iframe>` dentro del módulo de tareas. El dominio de la dirección URL debe estar en la [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) de la aplicación en el manifiesto de la aplicación. |
| `card` | Tarjeta adaptable o un accesorio de tarjeta de bot de tarjeta adaptable | Json para que la tarjeta adaptable aparezca en el módulo de tareas. Si va a invocar desde un bot, deberá usar el JSON de la tarjeta adaptable en un objeto de Bot `attachment` Framework. Desde una pestaña usarás solo una tarjeta adaptable. [Aquí hay un ejemplo.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | cadena | Si un cliente no admite la característica del módulo de tareas, esta dirección URL se abre en una pestaña del explorador. |
| `completionBotId` | cadena | Especifica un identificador de aplicación de bot para enviar el resultado de la interacción del usuario con el módulo de tareas. Si se especifica, el bot recibirá un `task/submit invoke` evento con un objeto JSON en la carga del evento. |

> [!NOTE]
> La característica del módulo de tareas requiere que los dominios de las direcciones URL que desea cargar se incluyan en la matriz en el `validDomains` manifiesto de la aplicación.

## <a name="task-module-sizing"></a>Tamaño del módulo de tareas

El uso de enteros para `TaskInfo.width` y `TaskInfo.height` establecerá la altura y el ancho en píxeles. Sin embargo, dependiendo del tamaño de la ventana y la resolución de la pantalla del equipo se reducirán proporcionalmente manteniendo la relación de aspecto (anchura/altura).

Si `TaskInfo.width` `TaskInfo.height` y son , o el `"small"` tamaño del rectángulo rojo en la imagen de arriba es una proporción del espacio `"medium"` `"large"` disponible: 20%, 50%, 60% para `width` y 20%, 50%, 66% para `height` .

Los módulos de tareas invocados desde una pestaña se pueden redimensionar dinámicamente. Después de llamar `tasks.startTask()` puede llamar a donde las propiedades height y width del objeto `tasks.updateTask(newSize)` newSize se ajustan a la especificación TaskInfo (por ejemplo. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>Módulo de tareas CSS para módulos de tareas HTML/JavaScript

Los módulos de tareas basados en HTML/JavaScript tienen acceso a toda el área del módulo de tareas debajo del encabezado. Aunque eso ofrece una gran flexibilidad, si desea que el relleno alrededor de los bordes se alinee con los elementos de encabezado y evite las barras de desplazamiento innecesarias, deberá proporcionar el CSS adecuado. Estos son algunos ejemplos para algunos casos de uso.

### <a name="example-1---youtube-video"></a>Ejemplo 1 - Vídeo de YouTube

YouTube ofrece la posibilidad de incrustar vídeos en páginas web. Usando una simple página web de código auxiliar es fácil mostrar esto en un módulo de tareas:

![Vídeo de YouTube](~/assets/images/task-module/youtube-example.png)

Aquí está el HTML para esta página, sin el CSS:

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

### <a name="example-2---powerapp"></a>Ejemplo 2 - PowerApp

También puede usar el mismo enfoque para incrustar un PowerApp. Como la altura/anchura de cualquier PowerApp individual es personalizable, es posible que deba ajustar la altura y el ancho para lograr la presentación deseada.

![PowerApp de gestión de activos](~/assets/images/task-module/powerapp-example.png)

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Tarjeta adaptable o accesorio de tarjeta de bot de tarjeta adaptable

Como hemos señalado anteriormente, dependiendo de cómo esté invocando su `card` necesitará usar una tarjeta adaptable o un archivo adjunto de tarjeta de bot de tarjeta adaptable (que es solo una tarjeta adaptable envuelta en un objeto de archivo adjunto).

Cuando estés invocando desde una pestaña, deberás usar una tarjeta adaptable. Este es un ejemplo muy simple:

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

Cuando estés invocando desde un bot, deberás usar un archivo adjunto de tarjeta bot de tarjeta adaptable como en el ejemplo siguiente:

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

Deberá recordar si está invocando un módulo de tareas que contiene una tarjeta adaptable de un bot o una pestaña.

## <a name="task-module-deep-link-syntax"></a>Sintaxis de vínculo profundo del módulo de tareas

Un vínculo profundo del módulo de tareas es solo una serialización del [objeto TaskInfo](#the-taskinfo-object) con otras dos piezas de información `APP_ID` y, opcionalmente, `BOT_APP_ID` :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Consulte [objeto TaskInfo](#the-taskinfo-object) para los tipos de datos y los valores permitidos para `<TaskInfo.url>` , , , y `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` .

> [!TIP]
> Asegúrese de codificar la URL en el vínculo profundo, especialmente cuando se utiliza el `card` parámetro (por ejemplo, [ `encodeURI()` la función](https://www.w3schools.com/jsref/jsref_encodeURI.asp)de JavaScript).

Aquí está la información sobre `APP_ID` `BOT_APP_ID` y:

| Valor | Tipo | ¿Necesario? | Descripción |
| --- | --- | --- | --- |
| `APP_ID` | string | Sí | Identificador [](~/resources/schema/manifest-schema.md#id) de la aplicación que invoca el módulo de tareas. La [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) en el manifiesto `APP_ID` para debe contener el dominio para si está en la dirección `url` `url` URL. (El identificador de aplicación ya se conoce cuando se invoca un módulo de tareas desde una pestaña o un bot, por lo que no se incluye en `TaskInfo` .) |
| `BOT_APP_ID` | string | No | Si se especifica un valor `completionBotId` para, el `result` objeto se envía a través de un mensaje al bot `task/submit invoke` especificado. `BOT_APP_ID` debe especificarse como un bot en el manifiesto de la aplicación, es decir, no se puede simplemente enviarlo a cualquier bot. |

Tenga en cuenta que es válido para `APP_ID` y para ser el `BOT_APP_ID` mismo, y en muchos casos será si una aplicación tiene un bot ya que se recomienda usarlo como identificador de una aplicación si hay uno.

## <a name="keyboard-and-accessibility-guidelines"></a>Directrices de teclado y accesibilidad

Con los módulos de tareas basados en HTML/JavaScript, es su responsabilidad asegurarse de que el módulo de tareas de la aplicación se puede utilizar con un teclado. Los programas de lector de pantalla también dependen de la capacidad de navegar utilizando el teclado. Como cuestión práctica, esto significa dos cosas:

1. Uso del [atributo tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) en las etiquetas HTML para controlar qué elementos se pueden enfocar y si/dónde participa en la navegación secuencial del teclado (normalmente con las teclas <kbd>Tab</kbd> y <kbd>Mayús-Tab).</kbd>
2. Control de la clave <kbd>Esc</kbd> en JavaScript para el módulo de tareas. Aquí hay un ejemplo de código que muestra cómo hacer esto:

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams garantizará que la navegación del teclado funcione correctamente desde el encabezado del módulo de tareas en su HTML y viceversa.

## <a name="code-sample"></a>Ejemplo de código
|**Nombre de la muestra** | **Descripción** | **.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Ejemplo del módulo de tareas (Bots-V4) | Ejemplos para crear módulos de tareas. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|Ejemplo del módulo de tareas (pestañas + Bots-V3) | Ejemplos para crear módulos de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>Vea también

* [Solicitar permisos de dispositivo](../concepts/device-capabilities/native-device-permissions.md)
* [Integrar capacidades multimedia](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Integrar la capacidad del escáner QR o de código de barras en Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Integrar capacidades de ubicación en Teams](../concepts/device-capabilities/location-capability.md)
