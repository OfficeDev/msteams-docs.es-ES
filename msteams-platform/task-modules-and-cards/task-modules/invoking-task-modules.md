---
title: Invocar y descartar módulos de tareas
description: Obtenga información sobre cómo invocar y descartar módulos de tareas, objetos de información de tareas, dimensionamiento del módulo de tareas, sintaxis de vínculo profundo del módulo de tareas mediante ejemplos de código
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5685e789dd6f4ad7cc39173e11af15dd9f7360fe
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073698"
---
# <a name="invoke-and-dismiss-task-modules"></a>Invocar y descartar módulos de tareas

Los módulos de tareas se pueden invocar desde pestañas, bots o vínculos profundos. La respuesta puede estar en HTML, JavaScript o como tarjeta adaptable. Hay mucha flexibilidad en términos de cómo se invocan los módulos de tareas y cómo tratar la respuesta de la interacción del usuario. En la tabla siguiente se resume cómo funciona esto:

| Se invoca mediante | Módulo de tareas con HTML o JavaScript | Módulo de tareas con tarjeta adaptable |
| --- | --- | --- |
| JavaScript en una pestaña | 1. Use la función `tasks.startTask()` Teams SDK de cliente con una función de devolución de llamada opcional`submitHandler(err, result)`. <br/><br/> 2. En el código del módulo de tareas, cuando el usuario haya realizado las acciones, llame a la función `tasks.submitTask()` Teams SDK con un `result` objeto como parámetro. Si se especificó una `submitHandler` devolución de llamada en `tasks.startTask()`, Teams la llama con `result` como parámetro. Si se produjo un error al invocar `tasks.startTask()`, se llama a la `submitHandler` función con una `err` cadena en su lugar. <br/><br/> 3. También puede especificar al `completionBotId` llamar a `teams.startTask()`. `result` A continuación, se envía al bot en su lugar. | 1. Llame a la función `tasks.startTask()` Teams SDK de cliente con un [objeto TaskInfo](#the-taskinfo-object) y `TaskInfo.card` que contenga el JSON de la tarjeta adaptable que se mostrará en el módulo de tareas emergente. <br/><br/> 2. Si se especificó una `submitHandler` devolución de llamada en `tasks.startTask()`, Teams la llama con una `err` cadena, si se produjo un error al invocar `tasks.startTask()` o si el usuario cierra la ventana emergente del módulo de tareas con la X en la esquina superior derecha. <br/><br/> 3. Si el usuario presiona un `Action.Submit` botón, su `data` objeto se devuelve como el valor de `result`. |
| Botón de tarjeta de bot | 1. Los botones de tarjeta de bot, dependiendo del tipo de botón, pueden invocar módulos de tareas de dos maneras, una dirección URL de vínculo profundo o enviando un `task/fetch` mensaje. <br/><br/> 2. Si la acción `type` del botón es que es `task/fetch` `Action.Submit` el tipo de botón para tarjetas adaptables, se envía al bot un `task/fetch invoke` evento que es un HTTP POST. El bot responde al POST con HTTP 200 y el cuerpo de la respuesta que contiene un contenedor alrededor del [objeto TaskInfo](#the-taskinfo-object). Para obtener más información, vea [invocación de un módulo de tareas mediante `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch). Teams muestra el módulo de tareas. <br/><br/> 3. Una vez que el usuario haya realizado las acciones, llame a la función `tasks.submitTask()` Teams SDK con un `result` objeto como parámetro. El bot recibe un `task/submit invoke` mensaje que contiene el `result` objeto . <br/><br/> 4. Tiene tres maneras diferentes de responder al `task/submit` mensaje, haciendo nada que sea la tarea completada correctamente, mostrando un mensaje al usuario en una ventana emergente o invocando otra ventana del módulo de tareas. Para obtener más información, consulte [la explicación detallada sobre `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | <ul><li> Al igual que los botones de las tarjetas de Bot Framework, los botones de tarjetas adaptables admiten dos formas de invocar módulos de tareas, direcciones URL de vínculo profundo con `Action.openUrl` botones y `task/fetch` usar `Action.Submit` botones. </li></ul> <br/><br/> <ul><li> Los módulos de tareas con tarjetas adaptables funcionan de forma muy similar al caso HTML o JavaScript. La principal diferencia es que, dado que no hay JavaScript cuando se usan tarjetas adaptables, no hay ninguna manera de llamar `tasks.submitTask()`a . En su lugar, Teams toma el `data` objeto de `Action.Submit` y lo devuelve como la carga del `task/submit` evento. Para obtener más información, vea [flexibilidad de `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). </li></ul> |
| Dirección URL de vínculo profundo <br/>[sintaxis URL](#task-module-deep-link-syntax) | 1. Teams invoca el módulo de tareas que es la dirección URL que aparece dentro del `<iframe>` especificado en el `url` parámetro del vínculo profundo. No hay devolución de `submitHandler` llamada. <br/><br/> 2. Dentro del JavaScript de la página en el módulo de tareas, llame `tasks.submitTask()` a para cerrarlo con un `result` objeto como parámetro, lo mismo que al invocarlo desde una pestaña o un botón de tarjeta de bot. Sin embargo, la lógica de finalización es ligeramente diferente. Si la lógica de finalización reside en el cliente que es si no hay ningún bot, no hay ninguna `submitHandler` devolución de llamada, por lo que cualquier lógica de finalización debe estar en el código anterior a la llamada a `tasks.submitTask()`. Los errores de invocación solo se notifican a través de la consola. Si tiene un bot, puede especificar un `completionBotId` parámetro en el vínculo profundo para enviar el `result` objeto a través de un `task/submit` evento. | 1. Teams invoca el módulo de tareas que es el cuerpo de la tarjeta JSON de la tarjeta adaptable que se especifica como un valor codificado en URL del `card` parámetro del vínculo profundo. <br/><br/> 2. El usuario cierra el módulo de tareas seleccionando la X en la esquina superior derecha del módulo de tareas o presionando un `Action.Submit` botón en la tarjeta. Dado que no hay ninguna `submitHandler` llamada, el usuario debe tener un bot para enviar el valor de los campos de tarjeta adaptable. El usuario debe usar el `completionBotId` parámetro en el vínculo profundo para especificar el bot al que enviar los datos mediante un `task/submit invoke` evento. |

En la sección siguiente se especifica el `TaskInfo` objeto que define determinados atributos para un módulo de tareas.

## <a name="the-taskinfo-object"></a>El objeto TaskInfo

El `TaskInfo` objeto contiene los metadatos de un módulo de tareas. Defina para `url` un iFrame incrustado o `card` para una tarjeta adaptable. En la tabla siguiente se proporciona la definición de objeto:

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `title` | string | Este atributo aparece debajo del nombre de la aplicación y a la derecha del icono de la aplicación. |
| `height` | número o cadena | Este atributo puede ser un número que representa el alto del módulo de tareas en píxeles, o `small`, `medium`o `large`. Para obtener más información, vea [Dimensionamiento del módulo de tareas](#task-module-sizing). |
| `width` | número o cadena | Este atributo puede ser un número que representa el ancho del módulo de tareas en píxeles, o `small`, `medium`o `large`. Para obtener más información, vea [Dimensionamiento del módulo de tareas](#task-module-sizing). |
| `url` | string | Este atributo es la dirección URL de la página cargada como dentro `<iframe>` del módulo de tareas. El dominio de la dirección URL debe estar en la [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) de la aplicación en el manifiesto de la aplicación. |
| `card` | Tarjeta adaptable o datos adjuntos de tarjetas de bot de tarjeta adaptable | Este atributo es el JSON para que la tarjeta adaptable aparezca en el módulo de tareas. Si el usuario invoca desde un bot, use json de tarjeta adaptable en un objeto bot framework `attachment` . Desde una pestaña, el usuario debe usar una tarjeta adaptable. Para obtener más información, consulte [Datos adjuntos de tarjeta adaptable o tarjeta de bot de tarjeta adaptable](#adaptive-card-or-adaptive-card-bot-card-attachment). |
| `fallbackUrl` | string | Este atributo abre la dirección URL en una pestaña del explorador, si un cliente no admite la característica del módulo de tareas. |
| `completionBotId` | string | Este atributo especifica un identificador de aplicación de bot para enviar el resultado de la interacción del usuario con el módulo de tareas. Si se especifica, el bot recibe un `task/submit invoke` evento con un objeto JSON en la carga del evento. |

> [!NOTE]
> La característica del módulo de tareas requiere que los dominios de las direcciones URL que quiera cargar se incluyan en la matriz en el `validDomains` manifiesto de la aplicación.

En la sección siguiente se especifica el tamaño del módulo de tareas que permite al usuario establecer el alto y el ancho del módulo de tareas.

## <a name="task-module-sizing"></a>Tamaño del módulo de tareas

El uso de enteros para `TaskInfo.width` y `TaskInfo.height`, establece el alto y el ancho del módulo de tareas en píxeles. Sin embargo, dependiendo del tamaño de la ventana del equipo y la resolución de pantalla, se reducen proporcionalmente al tiempo que se mantiene la relación de aspecto que es ancho o alto.

Si `TaskInfo.width` y `TaskInfo.height` son `"small"`, `"medium"`o `"large"`, el tamaño del rectángulo rojo de la imagen siguiente es una proporción del espacio disponible, 20 %, 50 % y 60 % para `width` y 20 %, 50 % y 66 % para `height`:

:::image type="content" source="../../assets/images/task-module/task-module-example.png" alt-text="ejemplo de módulo de tarea":::

Los módulos de tareas invocados desde una pestaña se pueden cambiar de tamaño dinámicamente. Después de llamar a `tasks.startTask()` , puede llamar a `tasks.updateTask(newSize)` donde las propiedades height y width del objeto newSize se ajustan a la especificación TaskInfo, por ejemplo `{ height: 'medium', width: 'medium' }`.

En la sección siguiente se proporcionan ejemplos de inserción de módulos de tareas en un vídeo de YouTube y una aplicación PowerApp.

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>CSS del módulo de tareas para módulos de tareas HTML o JavaScript

Los módulos de tareas basados en HTML o JavaScript tienen acceso a todo el área del módulo de tareas debajo del encabezado. Aunque esto ofrece una gran flexibilidad, si desea que el relleno alrededor de los bordes se alinee con los elementos de encabezado y evite barras de desplazamiento innecesarias, el usuario debe proporcionar el CSS adecuado. En las secciones siguientes se proporcionan algunos ejemplos de algunos casos de uso.

### <a name="example-1-youtube-video"></a>Ejemplo 1: Vídeo de YouTube

YouTube ofrece la posibilidad de insertar vídeos en páginas web. Es fácil insertar vídeos en páginas web en un módulo de tareas mediante una página web de código auxiliar simple.

:::image type="content" source="../../assets/images/task-module/youtube-example.png" alt-text="Ejemplo de Youtube":::

El código siguiente proporciona un ejemplo del CÓDIGO HTML de la página web sin CSS:

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

El usuario también puede usar el mismo enfoque para insertar una PowerApp. Dado que el alto o ancho de cualquier PowerApp individual es personalizable, el usuario puede ajustar el alto y el ancho para lograr la presentación deseada.

:::image type="content" source="../../assets/images/task-module/powerapp-example.png" alt-text="Powerapp":::

El código siguiente proporciona un ejemplo del código HTML para PowerApp:

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

En la sección siguiente se proporcionan detalles sobre cómo invocar la tarjeta mediante datos adjuntos de tarjeta adaptable o tarjeta de bot de tarjeta adaptable.

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Tarjeta adaptable o datos adjuntos de tarjetas de bot de tarjeta adaptable

En función de cómo invoque `card`, debe usar una tarjeta adaptable o un archivo adjunto de tarjeta de bot de tarjeta adaptable, que es una tarjeta adaptable encapsulada en un objeto de datos adjuntos.

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

El código siguiente proporciona un ejemplo de datos adjuntos de tarjetas de bot de tarjeta adaptable cuando se invoca desde un bot:

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

En la sección siguiente se proporcionan detalles sobre la sintaxis de vínculo profundo del módulo de tareas, incluidos el `TaskInfo` objeto y `APP_ID` `BOT_APP_ID`.

## <a name="task-module-deep-link-syntax"></a>Sintaxis de vínculo profundo del módulo de tareas

Un vínculo profundo del módulo de tareas es una serialización del objeto TaskInfo con los dos detalles siguientes y, opcionalmente, `APP_ID` :`BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Para conocer los tipos de datos y los valores permitidos para `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`y `<TaskInfo.title>`, vea [Objeto TaskInfo](#the-taskinfo-object).

> [!TIP]
> La dirección URL codifica el vínculo profundo cuando se usa el `card` parámetro , por ejemplo, la función de [`encodeURI()`](https://www.w3schools.com/jsref/jsref_encodeURI.asp)JavaScript.

En la tabla siguiente se proporciona información sobre `APP_ID` y `BOT_APP_ID`:

| Valor | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `APP_ID` | string | Sí | [Identificador de](~/resources/schema/manifest-schema.md#id) la aplicación que invoca el módulo de tareas. La [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) del manifiesto de `APP_ID` debe contener el dominio para `url` si `url` está en la dirección URL. El identificador de la aplicación ya se conoce cuando se invoca un módulo de tareas desde una pestaña o un bot, por lo que no se incluye en `TaskInfo`. |
| `BOT_APP_ID` | string | No | Si se especifica un valor para `completionBotId` , el `result` objeto se envía mediante un `task/submit invoke` mensaje al bot especificado. `BOT_APP_ID` debe especificarse como bot en el manifiesto de la aplicación, es decir, no se puede enviar a ningún bot. |

> [!NOTE]
> `APP_ID` y `BOT_APP_ID` puede ser el mismo en muchos casos, si una aplicación tiene un bot recomendado para usarlo como identificador de aplicación si hay uno.

En la sección siguiente se proporcionan detalles sobre el uso de un teclado con el módulo de tareas de la aplicación.

## <a name="keyboard-and-accessibility-guidelines"></a>Instrucciones de teclado y accesibilidad

Con los módulos de tareas basados en HTML o JavaScript, debe asegurarse de que el módulo de tareas de la aplicación se puede usar con un teclado. Los programas de lector de pantalla también dependen de la capacidad de navegar con el teclado. Esto incluye las dos cosas siguientes:

* Usar el [atributo tabindex](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) en las etiquetas HTML para controlar qué elementos se pueden centrar. Además, use el atributo tabindex para identificar dónde participa en la navegación secuencial del teclado normalmente con las teclas <kbd>Tab</kbd> y <kbd>Mayús-Tab</kbd> .
* Control de la clave <kbd>Esc</kbd> en JavaScript para el módulo de tareas. El código siguiente proporciona un ejemplo de cómo controlar la clave <kbd>Esc</kbd> :

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams garantiza que la navegación por teclado funciona correctamente desde el encabezado del módulo de tareas hasta el HTML y viceversa.

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Bots de ejemplo del módulo de tareas-V4 | Ejemplos para crear módulos de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|Pestañas y bots de ejemplo del módulo de tareas-V3 | Ejemplos para crear módulos de tareas. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>Vea también

* [Solicitar permisos de dispositivo](~/concepts/device-capabilities/native-device-permissions.md)
* [Integrar capacidades multimedia](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Integración de la funcionalidad qr o escáner de códigos de barras en Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](~/concepts/device-capabilities/location-capability.md)
