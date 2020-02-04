---
title: Botón compartir a equipos insertados
description: Cómo agregar el botón compartir a Microsoft Teams insertado en el sitio web
keywords: Compartir recursos compartidos entre equipos
ms.openlocfilehash: 219724e6ef3448db8a5b1fc70a519803255ffee6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676058"
---
# <a name="creating-a-share-to-teams-embedded-button"></a>Creación de un botón de compartir a un equipo integrado en Teams

>[!NOTE]
> * Solo se admiten las versiones de escritorio de Edge y Chrome.
> * No se admite el uso de cuentas de Freemium o invitado.

Los sitios web de terceros pueden usar el script del iniciador para incrustar recursos compartidos en los equipos de sus páginas web, lo que iniciará la experiencia compartir a Microsoft Teams en una ventana emergente al hacer clic en ella. Esto le permitirá compartir un vínculo directamente a cualquier persona o canal de Microsoft Teams sin cambiar el contexto.

![Menú emergente compartir a Microsoft Teams](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>Cómo incrustar un recurso compartido en el botón de Microsoft Teams

En primer lugar, tendrá que agregar el `launcher.js` script en su página web.

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

A continuación, agregue un elemento HTML en la Página Web `teams-share-button` con el atributo class y el vínculo para compartir `data-href` en el atributo.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

Se agregará el icono de Microsoft Teams a su sitio Web.

![Icono compartir a teams](~/assets/icons/share-to-teams-icon.png)

De manera opcional, si desea un tamaño de icono diferente para el botón compartir a Teams, `data-icon-px-size` use el atributo.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

Si sabe que la vista previa de la dirección URL del vínculo que se va a compartir no se representará correctamente en Teams (por ejemplo, el vínculo requerirá la autenticación del `data-preview` usuario), `false`puede deshabilitar la vista previa de la dirección URL agregando el atributo set a.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

Si la página representa el contenido de forma dinámica, puede usar el `shareToMicrosoftTeams.renderButtons()` método para forzar que el botón **compartir** se represente en el punto adecuado de la canalización.

## <a name="crafting-your-website-preview"></a>Diseñar la vista previa del sitio web

Cuando se comparta su sitio web con Microsoft Teams, la tarjeta que se inserte en el canal seleccionado contendrá una vista previa de su sitio Web. Puede controlar el comportamiento de esta vista previa garantizando que se agreguen los metadatos adecuados al sitio web que se va `data-href` a compartir (la dirección URL). En la tabla siguiente se describen las etiquetas necesarias. Puede usar las versiones predeterminadas de HTML o la versión de Open Graph.

Para que se muestre la vista previa, debe:

* Incluya una imagen en miniatura, o bien un título y una descripción (para obtener mejores resultados, incluir los tres).
* La dirección URL que se comparte no puede requerir autenticación. Si es así, puede compartirla, pero no se creará la vista previa.

|Valor|Etiqueta meta| Abrir gráfico|
|----|----|----|
|Título|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Descripción|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Imagen en miniatura| none |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>Compartir con Teams para el ámbito educativo

Para los profesores que usen el botón compartir a Microsoft Teams, se le ofrecerá una opción adicional `Create an Assignment`. Esto le permite crear rápidamente una tarea en el equipo seleccionado en función del vínculo compartido.

![Menú emergente compartir a Microsoft Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Definición de Launcher. js completa

| Propiedad | Atributo HTML | Tipo | Valor predeterminado | Descripción |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | N/D | Href del contenido que se va a compartir. |
| preview | `data-preview` | booleano (como una cadena) | `true` | Indica si se va a mostrar una vista previa del contenido que se va a compartir. |
| iconPxSize | `data-icon-px-size` | número (como una cadena) | `32` | Tamaño en píxeles del botón Share-to-teams que se va a representar. |
| msgText | `data-msg-text` | string | N/D | Texto predeterminado que se inserta delante del vínculo en el cuadro de redacción del mensaje (límite de 200 caracteres) |
| assignInstr | `data-assign-instr` | string | N/D | Texto predeterminado que se insertará en el campo "instrucciones" de las asignaciones (límite de 200 caracteres) |
| assignTitle | `data-assign-title` | string | N/D | Texto predeterminado que se va a insertar en el campo "título" de las asignaciones (límite de 50 caracteres) |

### <a name="methods"></a>Métodos

**`shareToMicrosoftTeams.renderButtons(options)`**

`options`(opcional):`{ elements?: HTMLElement[] }`

Representa todos los botones compartir que hay actualmente en la página. Si se proporciona `options` un objeto opcional con una lista de elementos, esos elementos se representarán en botones para compartir.

### <a name="setting-default-form-values"></a>Establecer valores de formulario predeterminado

De manera opcional, puede elegir establecer los valores predeterminados para los siguientes campos en el formulario compartir a Microsoft Teams:

* Indique algo sobre esto (`msgText`).
* Instrucciones de asignación`assignInstr`()
* Título de la`assignTitle`asignación ()

#### <a name="example-default-form-values"></a>Ejemplo: valores predeterminados del formulario

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
