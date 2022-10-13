---
title: Introducción al lienzo de Live Share
author: surbhigupta
description: En este módulo, obtenga más información sobre El lienzo de Live Share, una extensión que habilita la entrada manuscrita, punteros láser y cursores para las aplicaciones de reuniones.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 10/04/2022
ms.openlocfilehash: 9d1a776432f728c1e56caa357089be6e47c17e4c
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560613"
---
# <a name="live-share-canvas-overview"></a>Introducción al lienzo de Live Share

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-docs-feature-1.png" alt-text="Captura de pantalla que muestra un ejemplo de un lienzo sincronizado con otros participantes de una reunión de Teams.":::

En salas de conferencias y aulas de todo el mundo, las pizarras son una parte fundamental de la colaboración. Sin embargo, en los tiempos modernos, la pizarra ya no es suficiente. Con numerosas herramientas digitales como PowerPoint como punto focal de colaboración en la era moderna, es esencial habilitar el mismo potencial creativo.

Para permitir una colaboración más fluida, Microsoft creó PowerPoint Live, que se ha convertido en un elemento fundamental para el funcionamiento de las personas en Teams. Los presentadores pueden anotar sobre diapositivas para que todos puedan ver, usando plumas, resaltadores y punteros láser para llamar la atención sobre los conceptos clave. Con live share canvas, la aplicación puede aportar la eficacia de PowerPoint Live herramientas de entrada manuscrita con un esfuerzo mínimo.

## <a name="install"></a>Instalar

Para agregar la versión más reciente del SDK a la aplicación mediante npm:

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-canvas@next --save
```

O

Para agregar la versión más reciente del SDK a la aplicación mediante [Yarn](https://yarnpkg.com/):

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-canvas@next
```

## <a name="setting-up-the-package"></a>Configuración del paquete

El lienzo de Live Share tiene dos clases principales que permiten la colaboración llave en turno: `InkingManager` y `LiveCanvas`. `InkingManager` es responsable de adjuntar un elemento completo `<canvas>` a la aplicación, mientras que `LiveCanvas` administra la sincronización remota con otros participantes de la reunión. Si se usan juntos, la aplicación puede tener una funcionalidad completa similar a la pizarra en solo unas pocas líneas de código.

| Clases                                                                     | Descripción                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [InkingManager](/javascript/api/@microsoft/live-share-canvas/inkingmanager) | Clase que adjunta un `<canvas>` elemento a un determinado `<div>` para administrar automáticamente trazos de lápiz o resaltador, puntero láser, líneas y flechas, y borrados. Expone un conjunto de API (para controlar qué herramienta está activa) y valores de configuración básicos. |
| [LiveCanvas](/javascript/api/@microsoft/live-share-canvas/livecanvas)      | Clase `SharedObject` que sincroniza trazos y posiciones de cursor de `InkingManager` para todos los usuarios de una sesión de Live Share.                                                                                                                   |

Ejemplo:

```html
<body>
  <div id="canvas-host"></div>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const { liveCanvas } = container.initialObjects;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";
import { ContainerSchema } from "fluid-framework";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const liveCanvas = container.initialObjects.liveCanvas as LiveCanvas;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

---

## <a name="canvas-tools-and-cursors"></a>Herramientas y cursores de lienzo

Ahora que el lienzo de Live Share está configurado y sincronizado, puede configurar el lienzo para la interacción del usuario, como botones para seleccionar una herramienta de lápiz. En esta sección, analizaremos qué herramientas están disponibles y cómo usarlas.

### <a name="inking-tools"></a>Herramientas de entrada manuscrita

Cada herramienta de entrada manuscrita en el lienzo de Live Share representa trazos a medida que los usuarios dibujan. Si se usa una pantalla táctil o un lápiz óptico, las herramientas también admiten la dinámica de presión, lo que afecta al ancho del trazo. Los valores de configuración incluyen el color del pincel, el grosor, la forma y una flecha final opcional.

#### <a name="pen-tool"></a>Herramienta Lápiz

:::image type="content" source="../assets/images/teams-live-share/canvas-pen-tool.gif" alt-text="GIF muestra un ejemplo de trazos de dibujo en el lienzo mediante la herramienta de lápiz.":::

La herramienta pluma dibuja trazos sólidos que se almacenan en el lienzo. La forma de sugerencia predeterminada es un círculo.

```html
<div>
  <button id="pen">Enable Pen</button>
  <label for="pen-color">Select a color:</label>
  <input type="color" id="color" name="color" value="#000000" />
  <button id="pen-tip-size">Increase pen size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to pen
document.getElementById("pen").onclick = () => {
  inkingManager.tool = InkingTool.pen;
};
// Change the selected color for pen
document.getElementById("pen-color").onchange = () => {
  const colorPicker = document.getElementById("color");
  inkingManager.penBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for pen
document.getElementById("pen-tip-size").onclick = () => {
  inkingManager.penBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="highlighter-tool"></a>Herramienta Resaltador

:::image type="content" source="../assets/images/teams-live-share/canvas-highlighter-tool.gif" alt-text="GIF muestra un ejemplo de dibujo de trazos translúcidos en el lienzo mediante la herramienta de resaltado.":::

La herramienta de resaltado dibuja trazos translúcidos que se almacenan en el lienzo. La forma predeterminada de la punta es un cuadrado.

```html
<div>
  <button id="highlighter">Enable Highlighter</button><br />
  <label for="highlighter-color">Select a color:</label>
  <input type="color" id="highlighter-color" name="highlighter-color" value="#FFFC00" />
  <button id="highlighter-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to highlighter
document.getElementById("highlighter").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for highlighter
document.getElementById("highlighter-color").onchange = () => {
  const colorPicker = document.getElementById("highlighter-color");
  inkingManager.highlighterBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for highlighter
document.getElementById("highlighter-tip-size").onclick = () => {
  inkingManager.highlighterBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="eraser-tool"></a>Herramienta borrador

:::image type="content" source="../assets/images/teams-live-share/canvas-eraser-tool.gif" alt-text="GIF muestra un ejemplo de borrado de trazos en el lienzo mediante la herramienta de borrador.":::

La herramienta borrador borra trazos completos que cruzan su camino.

```html
<div>
  <button id="eraser">Enable Eraser</button><br />
  <button id="eraser-size">Increase eraser size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("eraser").onclick = () => {
  inkingManager.tool = InkingTool.eraser;
};
// Increase the tip size for eraser
document.getElementById("eraser-size").onclick = () => {
  inkingManager.eraserSize = inkingManager.eraserSize + 1;
};
```

#### <a name="point-eraser-tool"></a>Herramienta de borrador de punto

:::image type="content" source="../assets/images/teams-live-share/canvas-point-eraser-tool.gif" alt-text="GIF muestra un ejemplo de eliminación de puntos individuales dentro de trazos en el lienzo mediante la herramienta de borrador de puntos.":::

La herramienta borrador de puntos borra puntos individuales dentro de trazos que cruzan su ruta dividiendo los trazos existentes por la mitad. Esta herramienta es costosa computacionalmente y puede dar lugar a velocidades de fotogramas más lentas para los usuarios.

> [!NOTE]
> El borrador de punto comparte el mismo tamaño de punto de borrador que la herramienta de borrador normal.

```html
<div>
  <button id="point-eraser">Enable Point Eraser</button><br />
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("point-eraser").onclick = () => {
  inkingManager.tool = InkingTool.pointEraser;
};
```

#### <a name="laser-pointer"></a>Puntero láser

:::image type="content" source="../assets/images/teams-live-share/canvas-laser-tool.gif" alt-text="GIF muestra un ejemplo de trazos de dibujo en el lienzo mediante la herramienta de puntero láser.":::

El puntero láser es único, ya que la punta del láser tiene un efecto final a medida que mueve el mouse. Al dibujar trazos, el efecto final se representa durante un breve período antes de que se desvanezca por completo. Esta herramienta es perfecta para señalar información en la pantalla durante una reunión, ya que el moderador no tiene que cambiar entre herramientas para borrar trazos.

```html
<div>
  <button id="laser">Enable Laser Pointer</button><br />
  <label for="laser-color">Select a color:</label>
  <input type="color" id="laser-color" name="laser-color" value="#000000" />
  <button id="laser-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to laser pointer
document.getElementById("laser").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for laser pointer
document.getElementById("laser-color").onchange = () => {
  const colorPicker = document.getElementById("laser-color");
  inkingManager.laserPointerBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for laser pointer
document.getElementById("laser-tip-size").onclick = () => {
  inkingManager.laserPointerBrush.tipSize = inkingManager.laserPointerBrush.tipSize + 1;
};
```

#### <a name="line-and-arrow-tools"></a>Herramientas de línea y flecha

:::image type="content" source="../assets/images/teams-live-share/canvas-line-tool.gif" alt-text="GIF muestra un ejemplo de dibujo de líneas rectas en un lienzo mediante la herramienta de línea y flecha .":::

La herramienta de línea permite a los usuarios dibujar líneas rectas de un punto a otro, con una flecha opcional que se puede aplicar al final.

```html
<div>
  <button id="line">Enable Line</button><br />
  <button id="line-arrow">Enable Arrow</button><br />
  <input type="color" id="line-color" name="line-color" value="#000000" />
  <button id="line-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to line
document.getElementById("line").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "none";
};
// Change the selected tool to line
document.getElementById("line-arrow").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "open";
};
// Change the selected color for lineBrush
document.getElementById("line-color").onchange = () => {
  const colorPicker = document.getElementById("line-color");
  inkingManager.lineBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for lineBrush
document.getElementById("line-tip-size").onclick = () => {
  inkingManager.lineBrush.tipSize = inkingManager.lineBrush.tipSize + 1;
};
```

#### <a name="clear-all-strokes"></a>Borrar todos los trazos

Puede borrar todos los trazos del lienzo llamando a `inkingManager.clear()`. Esto elimina todos los trazos del lienzo.

### <a name="cursors"></a>Cursores

:::image type="content" source="../assets/images/teams-live-share/canvas-cursors.gif" alt-text="GIF muestra un ejemplo de usuarios que comparten un cursor en un lienzo.":::

Puede habilitar cursores en directo en la aplicación para que los usuarios realicen un seguimiento de las posiciones de los cursores entre sí en el lienzo. A diferencia de las herramientas de entrada manuscrita, los cursores funcionan completamente a través de la `LiveCanvas` clase . Opcionalmente, puede proporcionar un nombre y una imagen para identificar a cada usuario. Puede habilitar cursores por separado o con las herramientas de entrada manuscrita.

```javascript
// Optional. Set user display info
liveCanvas.onGetLocalUserInfo = () => {
  return {
    displayName: "YOUR USER NAME",
    pictureUri: "YOUR USER PICTURE URI",
  };
};
// Toggle Live Canvas cursor enabled state
liveCanvas.isCursorShared = !isCursorShared;
```

## <a name="optimizing-across-devices"></a>Optimización entre dispositivos

Para la mayoría de las aplicaciones en la web, el contenido se representa de forma diferente en función del tamaño de la pantalla o del estado variable de la aplicación. Si `InkingManager` no está optimizado correctamente para la aplicación, es posible que los trazos y cursores aparezcan de forma diferente para cada usuario. Live Share Canvas admite un conjunto sencillo de API, que permite ajustar las posiciones del `<canvas>` trazo para alinearse correctamente con el contenido.

De forma predeterminada, el lienzo de Live Share funciona mucho como una aplicación de pizarra, con el contenido alineado al centro de la ventanilla con un nivel de zoom de 1x. Solo se representa parte del contenido dentro de los límites visibles de `<canvas>`. Conceptualmente, es como grabar un vídeo desde la vista de pájaro. Mientras la ventanilla de la cámara está grabando una parte del mundo debajo de ella, el mundo real se extiende casi infinitamente en todas direcciones.

Este es un diagrama sencillo para ayudar a visualizar este concepto:

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-capabilities-docs-diagram-1.png" alt-text="Captura de pantalla que muestra el diseño del lienzo de pantalla completa para los usuarios de escritorio y móviles juntos.":::

Puede personalizar este comportamiento de las siguientes maneras:

- Cambiar el punto de referencia inicial a la esquina superior izquierda del lienzo.
- Modifique las posiciones x e y del desplazamiento de píxeles de la ventanilla.
- Cambie el nivel de escala de la ventanilla.

> [!NOTE]
> Los puntos de referencia, los desplazamientos y los niveles de escala son locales para el cliente y no se sincronizan entre los participantes de la reunión.

Ejemplo:

```html
<body>
  <button id="pan-left">Pan left</button>
  <button id="pan-up">Pan up</button>
  <button id="pan-right">Pan right</button>
  <button id="pan-down">Pan down</button>
  <button id="zoom-out">Zoom out</button>
  <button id="zoom-in">Zoom in</button>
  <button id="change-reference">Change reference</button>
</body>
```

```javascript
// ...

// Pan left
document.getElementById("pan-left").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x - 10,
    y: inkingManager.offset.y,
  };
};
// Pan up
document.getElementById("pan-up").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y - 10,
  };
};
// Pan right
document.getElementById("pan-right").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x + 10,
    y: inkingManager.offset.y,
  };
};
// Pan down
document.getElementById("pan-down").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y + 10,
  };
};
// Zoom out
document.getElementById("zoom-out").onclick = () => {
  if (inkingManager.scale > 0.1) {
    inkingManager.scale -= 0.1;
  }
};
// Zoom in
document.getElementById("zoom-in").onclick = () => {
  inkingManager.scale += 0.1;
};
// Change reference
document.getElementById("change-reference").onclick = () => {
  if (inkingManager.referencePoint === "center") {
    inkingManager.referencePoint = "topLeft";
  } else {
    inkingManager.referencePoint = "center";
  }
};
```

## <a name="ideal-scenarios"></a>Escenarios ideales

Con las páginas web que vienen en todas las formas y tamaños, no es posible crear un lienzo de Live Share para admitir todos los escenarios. El paquete es ideal para escenarios en los que todos los usuarios miran al mismo tiempo el mismo contenido. Aunque no todo el contenido debe estar visible en la pantalla, debe ser el contenido que se escala entre dispositivos linealmente.

Estos son un par de ejemplos de escenarios en los que el lienzo de Live Share es una excelente opción para la aplicación:

- Superponer imágenes y vídeos que se representan con la misma relación de aspecto en todos los clientes.
- Ver un mapa, un modelo 3D o una pizarra desde el mismo ángulo de rotación.

Ambos escenarios funcionan bien porque el contenido se puede ver igual en todos los dispositivos, incluso si los usuarios lo miran con diferentes niveles de zoom y desplazamientos. Si el diseño o el contenido de la aplicación cambian según el tamaño de la pantalla y no es posible generar una vista común para todos los participantes, es posible que el lienzo de Live Share no sea una buena opción para el escenario.

## <a name="code-samples"></a>Ejemplos de código

| Ejemplo de nombre          | Descripción                            | JavaScript                                                                                |
| -------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------- |
| Demostración de Live Canvas     | Aplicación de pizarra sencilla.         | [Ver](https://github.com/microsoft/live-share-sdk/tree/main/samples/03.live-canvas-demo) |
| Plantilla multimedia de React | Dibuje sobre un reproductor de vídeo sincronizado. | [View](https://aka.ms/liveshare-mediatemplate)                                            |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Tutorial de Agile Poker](../sbs-teams-live-share.yml)

## <a name="see-also"></a>Vea también

- [Preguntas más frecuentes sobre el SDK de Live Share](teams-live-share-faq.md)
- [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
- [Documentos de referencia del SDK de Live Share Canvas](/javascript/api/@microsoft/live-share-canvas/)
- [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
