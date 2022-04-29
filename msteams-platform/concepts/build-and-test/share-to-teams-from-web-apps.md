---
title: Compartir en Teams desde aplicaciones web
description: Obtenga información sobre cómo agregar el botón Compartir a Teams insertado en su sitio web, con una vista previa del sitio web, mediante ejemplos de código
ms.topic: reference
ms.localizationpriority: high
keywords: Compartir Teams con Teams
ms.openlocfilehash: 1f6a32c150fce323df19f452895184a4233c57fc
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111734"
---
# <a name="share-to-teams-from-web-apps"></a>Compartir en Teams desde aplicaciones web

Los sitios web de terceros pueden usar el script del iniciador para insertar Compartir a Teams en los botones de sus páginas web. Al seleccionar el botón, se inicia la experiencia Compartir a Teams en una ventana emergente. Esto le permite compartir un vínculo directamente con cualquier persona o canal de Microsoft Teams sin cambiar de contexto. Este documento le guía sobre cómo crear e insertar un botón Compartir en Teams para su sitio web, crear la vista previa del sitio web y ampliar Compartir a Teams para el ámbito educativo.

> [!NOTE]
>
> * Solo se admiten las versiones de escritorio de Microsoft&nbsp;Edge y Google Chrome.
> * No se admite el uso de cuentas de Freemium o de invitado.  

En la imagen siguiente se muestra la experiencia emergente Compartir en Teams:

:::image type="content" source="../../assets/images/share-to-teams-popup.png" alt-text="Compatir a la ventana emergente de Teams":::

## <a name="embed-a-share-to-teams-button"></a>Crear un botón Compartir en Teams

1. Agregue el script `launcher.js` en la página web.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Agregue un elemento HTML a la página web con el atributo de clase `teams-share-button` y el vínculo que se va a compartir en el atributo `data-href`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    Después de completarlo, el icono de Microsoft Teams se agrega a su sitio web. En la imagen siguiente se muestra el icono Compartir en Teams:

    ![Icono de Compartir en Teams](~/assets/icons/share-to-teams-icon.png)

1. Como alternativa, si desea un tamaño de icono diferente para el botón Compartir en Teams, use el atributo `data-icon-px-size`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. Si el vínculo compartido requiere autenticación de usuario y la vista previa de la dirección URL del vínculo que se va a compartir no se representa correctamente en Teams, puede deshabilitar la vista previa de la dirección URL agregando el atributo `data-preview` establecido en `false`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Si la página representa dinámicamente el contenido, puede usar el método `shareToMicrosoftTeams.renderButtons()` para forzar que **Share** se represente en el lugar adecuado de la canalización.

## <a name="craft-your-website-preview"></a>Crear la vista previa del sitio web

Cuando el sitio web se comparte con Teams, la tarjeta que se inserta en el canal seleccionado contiene una vista previa de su sitio web. Puede controlar el comportamiento de esta versión preliminar asegurándose de que se agregan los metadatos adecuados al sitio web que se comparte, como la dirección URL `data-href`.  

Para mostrar la vista previa:

* Debe incluir una imagen **Miniatura**, o un **Título** y **Descripción**. Para obtener mejores resultados, incluya los tres.
* La dirección URL compartida no requiere autenticación. Si requiere autenticación, puede compartirla, pero no se crea la versión preliminar.

En la tabla siguiente se describen las etiquetas necesarias:

|Valor|Etiqueta meta| Abrir Graph|
|----|----|----|
|Título|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Descripción|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Imagen en miniatura| Ninguno |`<meta property="og:image" content="http://example.com/image.jpg">`|

Puede usar las versiones predeterminadas de HTML o la versión de Open Graph.

## <a name="share-to-teams-for-education"></a>Compartir con Teams para el ámbito educativo

Para los profesores que usan el botón Compartir en Teams, hay una opción adicional para `Create an Assignment`. Esto le permite crear rápidamente una tarea en el equipo elegido, basándose en el vínculo compartido. En la imagen siguiente se muestra Compartir en Teams para el ámbito educativo:

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="Compartir en la ventana emergente de educación de Teams":::

## <a name="full-launcherjs-definition"></a>Definición completa de launcher.js

| Propiedad | Atributo HTML | Tipo | Predeterminado | Descripción |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | No aplicable | HREF del contenido que se va a compartir. |
| preview | `data-preview` | Booleano (como una cadena) | `true` | Indica si se va a mostrar o no una vista previa del contenido que se va a compartir. |
| iconPxSize | `data-icon-px-size` | number (como una cadena) | `32` | Tamaño en píxeles del botón Compartir en Teams que se va a representar. |
| msgText | `data-msg-text` | cadena | No aplicable | Texto predeterminado que se va a insertar antes del vínculo en el cuadro de redacción del mensaje. El número máximo de caracteres es 200. |
| assignInstr | `data-assign-instr` | string | No aplicable | Texto predeterminado que se va a insertar en las asignaciones de campo "Instrucciones". El número máximo de caracteres es 200. |
| assignTitle | `data-assign-title` | string | No aplicable | Texto predeterminado que se va a insertar en las asignaciones de campo "Título". El número máximo de caracteres es 50. |

### <a name="methods"></a>Methods

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (opcional): `{ elements?: HTMLElement[] }`

Actualmente, todos los botones de uso compartido se representan en la página. Si se proporciona un objeto `options` opcional con una lista de elementos, esos elementos se representan en botones de uso compartido.

### <a name="set-default-form-values"></a>Establecer valores de formulario predeterminados

Puede seleccionar establecer los valores predeterminados para los siguientes campos en el formulario Compartir en Teams:

* Di algo sobre esto: `msgText`
* Instrucciones de la tarea: `assignInstr`
* El título de la tarea: `assignTitle`

#### <a name="example"></a>Ejemplo

 Los valores de formulario predeterminados se proporcionan en el ejemplo siguiente:

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a>Consulte también

* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Compartir en Teams desde una aplicación personal o una pestaña](share-to-teams-from-personal-app-or-tab.md)
