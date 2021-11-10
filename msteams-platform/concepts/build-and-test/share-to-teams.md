---
title: Crear un botón Compartir en Teams
description: Aprenda a agregar el botón Compartir Teams incrustado en su sitio web, con una vista previa del sitio web, con ejemplos de código
ms.topic: reference
ms.localizationpriority: medium
keywords: Compartir Teams compartir a Teams
ms.openlocfilehash: 0f9425ae28312aeb9700d260d9ac2cf208351d4c
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889289"
---
# <a name="create-share-to-teams-button"></a>Crear un botón Compartir en Teams

Los sitios web de terceros pueden usar el script del iniciador para insertar botones de share-to-Teams en sus páginas web. Cuando selecciona, inicia la experiencia compartir a Teams en una ventana emergente. Esto le permite compartir un vínculo directamente con cualquier persona o canal Microsoft Teams sin cambiar el contexto. Este documento le guía sobre cómo crear e insertar un botón Compartir a Teams para su sitio web, crear la vista previa del sitio web y ampliar Share-to-Teams para Educación.

> [!NOTE]
> * Solo se admiten las versiones de escritorio de Edge y Chrome.
> * No se admite el uso de freemium o cuentas de invitado.  

En la siguiente imagen se muestra la experiencia Teams emergente de Share-to-

![Elemento emergente de Teams compartir a Teams](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>Insertar un recurso compartido en Teams botón

1. Agregue el `launcher.js` script en la página web.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Agregue un elemento HTML en la página web con el atributo `teams-share-button` class y el vínculo para compartir en el `data-href` atributo.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    Después de completar esto, el Microsoft Teams se agrega al sitio web. La siguiente imagen muestra el icono Compartir a Teams:

    ![Compartir a Teams icono](~/assets/icons/share-to-teams-icon.png)

1. Como alternativa, si desea un tamaño de icono diferente para el botón Compartir a Teams, use el `data-icon-px-size` atributo.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. Si el vínculo compartido requiere autenticación de usuario y la vista previa de dirección URL del vínculo que se va a compartir no se representa correctamente en Teams, puede deshabilitar la vista previa de la dirección URL agregando el atributo establecido en `data-preview` `false` .

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Si la página representa contenido dinámicamente, puede usar el método para forzar a Share a representarse en el `shareToMicrosoftTeams.renderButtons()` lugar adecuado de la canalización. 

## <a name="craft-your-website-preview"></a>Crear una vista previa del sitio web

Cuando el sitio web se comparte Teams, la tarjeta que se inserta en el canal seleccionado contiene una vista previa del sitio web. Puedes controlar el comportamiento de esta vista previa asegurando que los metadatos adecuados se agregan al sitio web que se comparte, como la `data-href` dirección URL.  

**Para mostrar la vista previa**

* Debe incluir una imagen **en miniatura** o un **título** y una **descripción**. Para obtener los mejores resultados, incluya los tres.
* La dirección URL compartida no requiere autenticación. Si requiere autenticación, puede compartirla, pero no se crea la vista previa.

En la tabla siguiente se describen las etiquetas necesarias:

|Valor|Etiqueta meta| Abra Graph|
|----|----|----|
|Título|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Descripción|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Imagen en miniatura| ninguno. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Puede usar las versiones predeterminadas html o la versión Graph html.

## <a name="share-to-teams-for-education"></a>Compartir a Teams para Educación

Para los profesores que usan el botón Compartir Teams, hay una opción adicional para `Create an Assignment` . Esto le permite crear rápidamente una asignación en el equipo elegido, en función del vínculo compartido. En la siguiente imagen se muestra Share-to-Teams para educación: 

![Compartir con Teams educación emergente](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Definición launcher.js completa

| Propiedad | Atributo HTML | Tipo | Predeterminado | Descripción |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | cadenas | No aplicable | Href del contenido que se debe compartir. |
| preview | `data-preview` | boolean (como una cadena) | `true` | Mostrar o no una vista previa del contenido que se va a compartir. |
| iconPxSize | `data-icon-px-size` | número (como una cadena) | `32` | Tamaño en píxeles del botón Compartir a Teams que se representará. |
| msgText | `data-msg-text` | cadenas | No aplicable | Texto predeterminado que se va a insertar antes del vínculo en el cuadro de redacción del mensaje. El número máximo de caracteres es 200. |
| assignInstr | `data-assign-instr` | cadenas | No aplicable | Texto predeterminado que se va a insertar en el campo de asignaciones "Instrucciones". El número máximo de caracteres es 200. |
| assignTitle | `data-assign-title` | cadenas | No aplicable | Texto predeterminado que se va a insertar en el campo asignaciones "Título". El número máximo de caracteres es 50. |

### <a name="methods"></a>Métodos

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (opcional): `{ elements?: HTMLElement[] }`

Actualmente, todos los botones de recurso compartido se representan en la página. Si se proporciona `options` un objeto opcional con una lista de elementos, estos elementos se representan en botones de uso compartido.

### <a name="set-default-form-values"></a>Establecer valores de formulario predeterminados

Puede seleccionar para establecer los valores predeterminados de los siguientes campos en el formulario Compartir Teams formulario:

* Diga algo al respecto: `msgText`
* Instrucciones de asignación: `assignInstr`
* Título de asignación: `assignTitle`

#### <a name="example"></a>Ejemplo

 Los valores de formulario predeterminados se dan en el siguiente ejemplo:

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

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
