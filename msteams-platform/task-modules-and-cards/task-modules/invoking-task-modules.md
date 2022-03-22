---
title: Invocar y descartar módulos de tareas
description: Obtenga información sobre la invocación y el descarte de módulos de tareas, objeto de información de tarea, tamaño del módulo de tareas, sintaxis de vínculo profundo del módulo de tareas mediante ejemplos de código
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 84cca74d6e81dce9bbcd7637b5d0b6537524d831
ms.sourcegitcommit: a36760750ff4f510c374a4c956be57f7c1b4a0db
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2022
ms.locfileid: "63674729"
---
# <a name="invoke-and-dismiss-task-modules"></a>Invocar y descartar módulos de tareas

Los módulos de tareas se pueden invocar desde pestañas, bots o vínculos profundos. La respuesta puede estar en HTML, JavaScript o como una tarjeta adaptable. Hay mucha flexibilidad en términos de cómo se invocan los módulos de tareas y cómo tratar la respuesta de la interacción del usuario. En la tabla siguiente se resume cómo funciona esto:

| Invocado mediante | Módulo de tareas con HTML o JavaScript | Módulo de tareas con tarjeta adaptable |
| --- | --- | --- |
| JavaScript en una pestaña | 1. Use la función Teams SDK de cliente con `tasks.startTask()` una función de `submitHandler(err, result)` devolución de llamada opcional. <br/><br/> 2. En el código del módulo de tareas, cuando el usuario haya realizado las acciones, llame a `result` la función sdk `tasks.submitTask()` de Teams con un objeto como parámetro. Si se `submitHandler` especificó una devolución de llamada en `tasks.startTask()`, Teams la llama con como `result` parámetro. Si se produjo un error al invocar `tasks.startTask()`, se `submitHandler` llama a la función con una `err` cadena en su lugar. <br/><br/> 3. También puede especificar un al `completionBotId` llamar a `teams.startTask()`. A continuación `result` , se envía al bot en su lugar. | 1. Llame a la función Teams SDK `tasks.startTask()` de cliente con un objeto [TaskInfo](#the-taskinfo-object) `TaskInfo.card` y que contenga el JSON para que la tarjeta adaptable se muestre en la ventana emergente del módulo de tareas. <br/><br/> 2. `submitHandler` `tasks.startTask()`Si se especificó una devolución de llamada en , Teams `err` la llama con una cadena, si se produjo un error `tasks.startTask()` al invocar o si el usuario cierra la ventana emergente del módulo de tareas con la X en la parte superior derecha. <br/><br/> 3. Si el usuario presiona un botón `Action.Submit` , su `data` objeto se devuelve como el valor de `result`. |
| Botón de tarjeta bot | 1. Los botones de tarjeta bot, según el tipo de botón, pueden invocar módulos de tareas de dos maneras, una dirección URL de vínculo profundo o enviando un `task/fetch` mensaje. <br/><br/> 2. Si la acción `type` `task/fetch` `Action.Submit` del botón es el tipo de botón para tarjetas adaptables, `task/fetch invoke` se envía un evento que es un POST HTTP al bot. El bot responde al POST con HTTP 200 y al cuerpo de la respuesta que contiene un contenedor alrededor del [objeto TaskInfo](#the-taskinfo-object). Para obtener más información, [vea invocar un módulo de tareas mediante `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch). Teams muestra el módulo de tareas. <br/><br/> 3. Después de que el usuario haya realizado las acciones, llame a la función Teams SDK `tasks.submitTask()` con un `result` objeto como parámetro. El bot recibe un `task/submit invoke` mensaje que contiene el `result` objeto. <br/><br/> 4. `task/submit` Tiene tres formas diferentes de responder al mensaje, sin hacer nada que sea la tarea completada correctamente, mostrando un mensaje al usuario en una ventana emergente o invocando otra ventana del módulo de tareas. Para obtener más información, vea [discusión detallada sobre `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | <ul><li> Al igual que los botones de las tarjetas de Bot Framework, los botones de las tarjetas adaptables admiten dos formas de invocar módulos de tareas, las direcciones URL `Action.openUrl` `task/fetch` de vínculo profundo con botones y el uso de `Action.Submit` botones. </li></ul> <br/><br/> <ul><li> Los módulos de tareas con tarjetas adaptables funcionan de forma muy similar al caso html o JavaScript. La principal diferencia es que, dado que no hay JavaScript cuando se usan tarjetas adaptables, no hay forma de llamar a `tasks.submitTask()`. En su lugar, Teams toma el `data` objeto y `Action.Submit` lo devuelve como la carga del `task/submit` evento. Para obtener más información, [vea flexibilidad de `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). </li></ul> |
| URL de vínculo profundo <br/>[sintaxis URL](#task-module-deep-link-syntax) | 1. Teams invoca el módulo de tareas que es la dirección URL `<iframe>` que aparece dentro del especificado `url` en el parámetro del vínculo profundo. No hay devolución `submitHandler` de llamada. <br/><br/> 2. Dentro del JavaScript de la página del módulo de tareas, `tasks.submitTask()` `result` llame para cerrarlo con un objeto como parámetro, lo mismo que al invocarlo desde una pestaña o un botón de tarjeta de bot. Sin embargo, la lógica de finalización es ligeramente diferente. Si la lógica de finalización reside en el cliente que es si no hay bot, no `submitHandler` hay devolución de llamada, por lo que cualquier lógica de finalización debe estar en el código anterior a la llamada a `tasks.submitTask()`. Los errores de invocación solo se notifican a través de la consola. Si tiene un bot, puede especificar un `completionBotId` parámetro en el vínculo profundo para enviar el `result` objeto a través de un `task/submit` evento. | 1. Teams invoca el módulo de tareas que es el cuerpo de la tarjeta JSON de la tarjeta adaptable que se especifica como un valor codificado en URL `card` del parámetro del vínculo profundo. <br/><br/> 2. El usuario cierra el módulo de tareas seleccionando la X `Action.Submit` en la parte superior derecha del módulo de tareas o presionando un botón en la tarjeta. Dado que no hay que `submitHandler` llamar, el usuario debe tener un bot para enviar el valor de los campos de tarjeta adaptable. El usuario debe usar el `completionBotId` parámetro en el vínculo profundo para especificar el bot al que se enviarán los datos mediante un `task/submit invoke` evento. |

La siguiente sección especifica el objeto `TaskInfo` que define determinados atributos para un módulo de tareas.

## <a name="the-taskinfo-object"></a>El objeto TaskInfo

El `TaskInfo` objeto contiene los metadatos de un módulo de tareas. Defina el `url` para un iFrame incrustado o `card` para una tarjeta adaptable. En la tabla siguiente se proporciona la definición de objeto:

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `title` | string | Este atributo aparece debajo del nombre de la aplicación y a la derecha del icono de la aplicación. |
| `height` | número o cadena | Este atributo puede ser un número que representa el alto del módulo de tareas en píxeles, `small`o , `medium`o `large`. Para obtener más información, vea [tamaño del módulo de tareas](#task-module-sizing). |
| `width` | número o cadena | Este atributo puede ser un número que representa el ancho del módulo de tareas en píxeles, `small`o , `medium`o `large`. Para obtener más información, vea [tamaño del módulo de tareas](#task-module-sizing). |
| `url` | string | Este atributo es la dirección URL de la página cargada como dentro `<iframe>` del módulo de tareas. El dominio de la dirección URL debe estar en la matriz [validDomains](~/resources/schema/manifest-schema.md#validdomains) de la aplicación en el manifiesto de la aplicación. |
| `card` | Datos adjuntos de tarjeta adaptable o de bot de tarjeta adaptable | Este atributo es el JSON para que la tarjeta adaptable aparezca en el módulo de tareas. Si el usuario invoca desde un bot, use el JSON de tarjeta adaptable en un objeto Bot Framework `attachment` . Desde una pestaña, el usuario debe usar una tarjeta adaptable. Para obtener más información, consulte [Adaptive Card or Adaptive Card bot card attachment](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | Este atributo abre la dirección URL en una pestaña del explorador, si un cliente no admite la característica del módulo de tareas. |
| `completionBotId` | string | Este atributo especifica un identificador de aplicación bot para enviar el resultado de la interacción del usuario con el módulo de tareas. Si se especifica, el bot recibe un `task/submit invoke` evento con un objeto JSON en la carga del evento. |

> [!NOTE]
> La característica del módulo de tareas requiere que los dominios de las direcciones URL `validDomains` que quiera cargar se incluyan en la matriz en el manifiesto de la aplicación.

En la siguiente sección se especifica el tamaño del módulo de tareas que permite al usuario establecer el alto y el ancho del módulo de tareas.

## <a name="task-module-sizing"></a>Tamaño del módulo de tareas

El uso de enteros para `TaskInfo.width` y `TaskInfo.height`, establece el alto y el ancho del módulo de tareas en píxeles. Sin embargo, según el tamaño de la ventana y la resolución de pantalla del equipo, se reducen proporcionalmente mientras se mantiene la relación de aspecto que es de ancho o alto.

Si `TaskInfo.width` y `TaskInfo.height` son `"small"`, `"medium"`o `"large"`, el tamaño del rectángulo rojo de la siguiente imagen es una proporción del espacio disponible, 20%, 50% y 60% para `width` y 20%, 50% y 66% para `height`:

![Ejemplo del módulo de tareas](~/assets/images/task-module/task-module-example.png)

Los módulos de tareas invocados desde una pestaña se pueden cambiar dinámicamente. Después de llamar `tasks.startTask()` , puede llamar a donde `tasks.updateTask(newSize)` las propiedades height y width del objeto newSize se ajustan a la especificación TaskInfo, por ejemplo `{ height: 'medium', width: 'medium' }`.

En la siguiente sección se proporcionan ejemplos de la inserción de módulos de tareas en un vídeo de YouTube y una PowerApp.

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>CSS del módulo de tareas para módulos de tareas HTML o JavaScript

Los módulos de tareas basados en HTML o JavaScript tienen acceso a todo el área del módulo de tareas debajo del encabezado. Aunque eso ofrece una gran flexibilidad, si desea que el relleno alrededor de los bordes se alinee con los elementos de encabezado y evite barras de desplazamiento innecesarias, el usuario debe proporcionar el CSS correcto. Las secciones siguientes proporcionan algunos ejemplos para algunos casos de uso.

### <a name="example-1-youtube-video"></a>Ejemplo 1: Vídeo de YouTube

YouTube ofrece la posibilidad de insertar vídeos en páginas web. Es fácil insertar vídeos en páginas web en un módulo de tareas mediante una página web de código auxiliar simple.

![Vídeo de YouTube](~/assets/images/task-module/youtube-example.png)

El código siguiente proporciona un ejemplo de HTML para la página web sin css:

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

El código siguiente proporciona un ejemplo de CSS:

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

### <a name="example-2-powerapp"></a>Ejemplo 2: PowerApp

El usuario también puede usar el mismo enfoque para insertar una PowerApp. Como el alto o el ancho de cualquier PowerApp individual es personalizable, el usuario puede ajustar el alto y el ancho para lograr la presentación deseada.

![PowerApp de administración de activos](~/assets/images/task-module/powerapp-example.png)

El código siguiente proporciona un ejemplo de HTML para PowerApp:

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

El código siguiente proporciona un ejemplo de CSS:

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

En la siguiente sección se proporcionan detalles sobre cómo invocar la tarjeta mediante datos adjuntos de tarjeta adaptable o de bot de tarjeta adaptable.

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Datos adjuntos de tarjeta adaptable o de bot de tarjeta adaptable

Dependiendo de cómo invoje `card`su , debe usar una tarjeta adaptable o un archivo adjunto de tarjeta bot de tarjeta adaptable, que es una tarjeta adaptable envuelta en un objeto de datos adjuntos.

Cuando se invoca desde una pestaña, el usuario debe usar una tarjeta adaptable.

El código siguiente proporciona un ejemplo de una tarjeta adaptable:

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

El código siguiente proporciona un ejemplo de datos adjuntos de una tarjeta bot de tarjeta adaptable cuando se invoca desde un bot:

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

En la siguiente sección se proporcionan detalles sobre la sintaxis de vínculo profundo del módulo de tareas, incluidos `TaskInfo` el objeto y `APP_ID` `BOT_APP_ID`.

## <a name="task-module-deep-link-syntax"></a>Sintaxis de vínculo profundo del módulo de tareas

Un vínculo profundo del módulo de tareas es una serialización del objeto TaskInfo con los otros dos detalles siguientes, `APP_ID` y opcionalmente:`BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Para los tipos de datos y los valores permitidos para `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`y `<TaskInfo.title>`, vea [TaskInfo (objeto](#the-taskinfo-object)).

> [!TIP]
> La dirección URL codifica el vínculo profundo al usar el `card` parámetro, por ejemplo, la función de [`encodeURI()` JavaScript](https://www.w3schools.com/jsref/jsref_encodeURI.asp).

En la tabla siguiente se proporciona información sobre `APP_ID` y `BOT_APP_ID`:

| Valor | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `APP_ID` | string | Sí | El [identificador](~/resources/schema/manifest-schema.md#id) de la aplicación que invoca el módulo de tareas. La [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) del manifiesto para `APP_ID` debe contener el dominio para `url` if `url` está en la dirección URL. El identificador de la aplicación ya se conoce cuando se invoca un módulo de tareas desde una pestaña o un bot, por lo que no se incluye en `TaskInfo`. |
| `BOT_APP_ID` | string | No | Si se especifica un valor `completionBotId` para, el `result` objeto se envía mediante un `task/submit invoke` mensaje al bot especificado. `BOT_APP_ID` debe especificarse como bot en el manifiesto de la aplicación, es decir, no se puede enviar a ningún bot. |

> [!NOTE]
> `APP_ID` y `BOT_APP_ID` puede ser lo mismo en muchos casos, si una aplicación tiene un bot recomendado para usarlo como id. de una aplicación si la hay.

En la siguiente sección se proporcionan detalles sobre cómo usar un teclado con el módulo de tareas de la aplicación.

## <a name="keyboard-and-accessibility-guidelines"></a>Directrices de teclado y accesibilidad

Con módulos de tareas basados en HTML o JavaScript, debes asegurarte de que el módulo de tareas de la aplicación se pueda usar con un teclado. Los programas de lector de pantalla también dependen de la capacidad de navegar con el teclado. Esto incluye las dos cosas siguientes:

* Usar el [atributo tabindex en](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) las etiquetas HTML para controlar qué elementos se pueden centrar. Además, usa el atributo tabindex para identificar dónde participa en la navegación secuencial del teclado normalmente con las teclas <kbd>Tab</kbd> y <kbd>Mayús-Tab</kbd> .
* Control de <kbd>la clave Esc</kbd> en JavaScript para el módulo de tareas. El código siguiente proporciona un ejemplo de cómo controlar la <kbd>clave Esc</kbd> :

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams garantiza que la navegación por teclado funciona correctamente desde el encabezado del módulo de tareas al HTML y viceversa.

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Bots de ejemplo de módulo de tareas-V4 | Ejemplos para crear módulos de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[Ver](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|Fichas de ejemplo del módulo de tareas y bots-V3 | Ejemplos para crear módulos de tareas. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>Vea también

* [Solicitar permisos de dispositivo](~/concepts/device-capabilities/native-device-permissions.md)
* [Integrar capacidades multimedia](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Integrar la funcionalidad de escáner de códigos QR o códigos de barras en Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](~/concepts/device-capabilities/location-capability.md)
