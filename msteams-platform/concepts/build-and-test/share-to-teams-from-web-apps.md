---
title: Uso compartido en Teams desde aplicaciones web
description: Aprenda a agregar el botón Compartir a Teams incrustado en su sitio web, con una vista previa del sitio web, mediante ejemplos de código.
ms.topic: reference
ms.localizationpriority: medium
keywords: Compartir Teams Compartir en Teams
ms.openlocfilehash: ac08d3c697bc5f02eb8527d2239afe022cb421af
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685716"
---
# <a name="share-to-teams-from-web-apps"></a>Uso compartido en Teams desde aplicaciones web

Los sitios web de terceros pueden usar el script del iniciador para insertar Share para Teams botones en sus páginas web. Cuando se selecciona, se inicia la experiencia Compartir en Teams en una ventana emergente. Esto le permite compartir un vínculo directamente con cualquier persona o canal Microsoft Teams sin cambiar el contexto. Este documento le guía sobre cómo crear e insertar un botón Compartir para Teams para su sitio web, crear la versión preliminar del sitio web y ampliar Share a Teams para Educación.

> [!NOTE]
>
> * Solo se admiten las versiones de escritorio de MicrosoftEdge&nbsp; y Google Chrome.
> * No se admite el uso de Cuentas de invitado o Freemium.  

En la imagen siguiente se muestra la experiencia emergente Compartir en Teams:

:::image type="content" source="../../assets/images/share-to-teams-popup.png" alt-text="Compartir en Teams elemento emergente":::

## <a name="embed-a-share-to-teams-button"></a>Botón Insertar un recurso compartido en Teams

1. Agregue el `launcher.js` script en la página web.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Agregue un elemento HTML en la página web con el `teams-share-button` atributo de clase y el vínculo para compartir en el `data-href` atributo.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    Después de completar esto, el icono de Microsoft Teams se agrega a su sitio web. En la imagen siguiente se muestra el icono Compartir en Teams:

    ![Icono Compartir en Teams](~/assets/icons/share-to-teams-icon.png)

1. Como alternativa, si desea un tamaño de icono diferente para el botón Compartir para Teams, use el `data-icon-px-size` atributo .

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. Si el vínculo compartido requiere autenticación de usuario y la vista previa de la dirección URL del vínculo que se va a compartir no se representa bien en Teams, puede deshabilitar la vista previa de la dirección URL agregando el `data-preview` atributo establecido en `false`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Si la página representa contenido dinámicamente, puede usar el `shareToMicrosoftTeams.renderButtons()` método para forzar a **Share** a representarlo en el lugar adecuado de la canalización.

## <a name="craft-your-website-preview"></a>Creación de la versión preliminar del sitio web

Cuando el sitio web se comparte con Teams, la tarjeta que se inserta en el canal seleccionado contiene una vista previa de su sitio web. Para controlar el comportamiento de esta versión preliminar, asegúrese de que se agregan los metadatos adecuados al sitio web que se comparte, como la `data-href` dirección URL.  

Para mostrar la vista previa:

* Debe incluir una imagen en **miniatura** o un **título** y una **descripción**. Para obtener mejores resultados, incluya los tres.
* La dirección URL compartida no requiere autenticación. Si requiere autenticación, puede compartirla, pero no se crea la versión preliminar.

En la tabla siguiente se describen las etiquetas necesarias:

|Valor|Etiqueta meta| Abrir Graph|
|----|----|----|
|Título|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Descripción|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Imagen en miniatura| Ninguno. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Puede usar las versiones predeterminadas de HTML o la versión Open Graph.

## <a name="share-to-teams-for-education"></a>Compartir en Teams para Educación

Para los profesores que usan el botón Compartir para Teams, hay una opción adicional para `Create an Assignment`. Esto le permite crear rápidamente una asignación en el equipo elegido, en función del vínculo compartido. En la imagen siguiente se muestra Compartir en Teams para educación:

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="Compartir con Teams educación emergente":::

## <a name="full-launcherjs-definition"></a>Definición de launcher.js completa

| Propiedad | Atributo HTML | Tipo | Predeterminado | Descripción |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | No aplicable | Href del contenido que se va a compartir. |
| preview | `data-preview` | Boolean (como cadena) | `true` | Indica si se va a mostrar o no una vista previa del contenido que se va a compartir. |
| iconPxSize | `data-icon-px-size` | number (como una cadena) | `32` | Tamaño en píxeles del botón Compartir para Teams que se va a representar. |
| msgText | `data-msg-text` | string | No aplicable | Texto predeterminado que se va a insertar antes del vínculo en el cuadro de redacción del mensaje. El número máximo de caracteres es 200. |
| assignInstr | `data-assign-instr` | string | No aplicable | Texto predeterminado que se va a insertar en el campo "Instrucciones" de las asignaciones. El número máximo de caracteres es 200. |
| assignTitle | `data-assign-title` | string | No aplicable | Texto predeterminado que se va a insertar en el campo "Título" de las asignaciones. El número máximo de caracteres es 50. |

### <a name="methods"></a>Methods

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (opcional): `{ elements?: HTMLElement[] }`

Actualmente, todos los botones de recurso compartido se representan en la página. Si se proporciona un objeto opcional `options` con una lista de elementos, esos elementos se representan en botones de recurso compartido.

### <a name="set-default-form-values"></a>Establecimiento de valores de formulario predeterminados

Puede seleccionar establecer valores predeterminados para los campos siguientes en el formulario Compartir en Teams:

* Diga algo al respecto: `msgText`
* Instrucciones de asignación: `assignInstr`
* Título de asignación: `assignTitle`

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
* [Compartir en Teams desde una aplicación o pestaña personal](share-to-teams-from-personal-app-or-tab.md)
