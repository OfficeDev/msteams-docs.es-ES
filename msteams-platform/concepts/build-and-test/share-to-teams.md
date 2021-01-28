---
title: Crear un botón de Compartir en Teams
description: Cómo agregar el botón Compartir a Teams insertado en su sitio web
ms.topic: reference
keywords: Compartir teams de forma share-to-teams
ms.openlocfilehash: 46091c957137cc871095ca6a57c0d61fa79d9458
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014337"
---
# <a name="create-a-share-to-teams-button-for-your-website"></a>Creación de un botón Compartir en Teams para el sitio web

>[!NOTE]
> * Solo se admiten las versiones de escritorio de Edge y Chrome.
> * No se admite el uso de cuentas de invitado o freemium.

Los sitios web de terceros pueden usar el script del iniciador para insertar botones Compartir en Teams en sus páginas web, lo que iniciará la experiencia Compartir en Teams en una ventana emergente cuando se haga clic en ellos. Esto le permitirá compartir un vínculo directamente con cualquier persona o canal de Microsoft Teams sin cambiar de contexto.

![Compartir en un elemento emergente de Teams](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>Cómo insertar un botón Compartir en Teams

En primer lugar, tendrá que agregar el `launcher.js` script en su página web.

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

A continuación, agregue un elemento HTML en la página web con el atributo `teams-share-button` de clase y el vínculo para compartir en el `data-href` atributo.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

Esto agregará el icono de Microsoft Teams a su sitio web.

![Icono Compartir en Teams](~/assets/icons/share-to-teams-icon.png)

Opcionalmente, si desea un tamaño de icono diferente para el botón Compartir en Teams, use el `data-icon-px-size` atributo.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

Si sabe que la vista previa de la dirección URL del vínculo que se va a compartir no se representará bien en Teams (por ejemplo, el vínculo requeriría autenticación de usuario), puede deshabilitar la vista previa de la dirección URL agregando el conjunto de atributos a `data-preview` `false` .

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

Si la página representa contenido dinámicamente, puede usar el método para forzar que el botón Compartir se represente en el `shareToMicrosoftTeams.renderButtons()` lugar adecuado de la canalización. 

## <a name="crafting-your-website-preview"></a>Creación de la vista previa del sitio web

Cuando su sitio web se comparte con Teams, la tarjeta que se inserta en el canal seleccionado contendrá una vista previa de su sitio web. Puede controlar el comportamiento de esta vista previa asegurándose de que los metadatos adecuados se agregan al sitio web que se comparte (la `data-href` dirección URL). En la tabla siguiente se describen las etiquetas necesarias. Puede usar las versiones predeterminadas html o la versión de Open Graph.

Para que se muestre la vista previa, debe:

* Incluya una imagen en miniatura o un título y una descripción (para obtener los mejores resultados, incluya los tres).
* La dirección URL que se comparte no puede requerir autenticación. Si lo hace, puede seguir compartiéndola, pero no se creará la vista previa.

|Valor|Etiqueta meta| Open Graph|
|----|----|----|
|El título|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Descripción|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Imagen en miniatura| none |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>Compartir con Teams para educación

Para los profesores que usan el botón Compartir en Teams, se le dará una opción adicional para `Create an Assignment` . Esto le permite crear rápidamente una asignación en el equipo elegido en función del vínculo compartido.

![Compartir en un elemento emergente de Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Definición launcher.js completa

| Propiedad | Atributo HTML | Tipo | Predeterminado | Descripción |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | cadena | No aplicable | El href del contenido que se desea compartir. |
| preview | `data-preview` | boolean (como una cadena) | `true` | Indica si se va a mostrar una vista previa del contenido que se va a compartir. |
| iconPxSize | `data-icon-px-size` | number (como una cadena) | `32` | El tamaño en píxeles del botón Compartir a Teams que se representará. |
| msgText | `data-msg-text` | cadena | No aplicable | Texto predeterminado que se insertará antes del vínculo en el cuadro de redacción del mensaje (límite de 200 caracteres) |
| assignInstr | `data-assign-instr` | cadena | No aplicable | Texto predeterminado que se va a insertar en el campo "Instrucciones" de asignaciones (límite de 200 caracteres) |
| assignTitle | `data-assign-title` | cadena | No aplicable | Texto predeterminado que se va a insertar en el campo "Título" de las asignaciones (límite de 50 caracteres) |

### <a name="methods"></a>Métodos

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (opcional): `{ elements?: HTMLElement[] }`

Representa todos los botones de recurso compartido que hay actualmente en la página. Si se proporciona un objeto opcional con una lista de elementos, esos elementos se representarán `options` en botones de uso compartido.

### <a name="setting-default-form-values"></a>Establecer valores de formulario predeterminados

Opcionalmente, puede elegir establecer valores predeterminados para los siguientes campos en el formulario Compartir en Teams:

* Diga algo al respecto ( `msgText` )
* Instrucciones de asignación ( `assignInstr` )
* Título de asignación ( `assignTitle` )

#### <a name="example-default-form-values"></a>Ejemplo: valores de formulario predeterminados

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
