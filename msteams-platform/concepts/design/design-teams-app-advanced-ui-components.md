---
title: Diseñar la aplicación con componentes de interfaz de usuario avanzados
author: heath-hamilton
description: Obtenga información sobre los componentes de la interfaz de usuario usados Teams .
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 6f2bd9cd237751adb15db45bbd6e3cdfea35ce09
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328082"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>Diseñar la aplicación Microsoft Teams con componentes de interfaz de usuario avanzados

Los siguientes componentes son una combinación de componentes básicos de [la](~/concepts/design/design-teams-app-basic-ui-components.md) interfaz de usuario que puedes usar para situaciones comunes Teams de diseño, como la navegación.

## <a name="microsoft-teams-ui-kit"></a>Kit de interfaz de usuario de Microsoft Teams

En función <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">de Fluent interfaz de</a>usuario, el kit Microsoft Teams de interfaz de usuario incluye componentes y patrones diseñados específicamente para crear Teams aplicaciones. En el kit de interfaz de usuario, puedes agarrar e insertar los componentes enumerados aquí directamente en el diseño y ver más ejemplos de cómo usar cada componente.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>Ruta de navegación

Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación. Ayudan a los usuarios a comprender cómo la página que están viendo se ajusta a la experiencia general y ofrecen acceso con un solo clic a niveles más altos de esa jerarquía.

### <a name="top-use-cases"></a>Casos de uso principales

* Jerarquía de comunicación
* Navegación

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación en el móvil." border="false":::

---

## <a name="left-nav"></a>Navegación izquierda

Use la navegación izquierda para examinar varias páginas dentro de la Teams pestaña. En el siguiente ejemplo, la navegación izquierda se encuentra entre la lista de canales y el contenido de la pestaña.

### <a name="top-use-cases"></a>Casos de uso principales

* Examinar varias páginas dentro de una Teams pestaña.
* Dividir aplicaciones complejas en varias páginas.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda en el móvil." border="false":::

---

## <a name="notification-bar"></a>Barra de notificaciones

Una barra de notificaciones es un área dedicada para mostrar mensajes breves e importantes que no requieren que el usuario tome medidas inmediatas. Los iconos y los colores de fondo específicos están asociados con tipos específicos de mensajes (vea a continuación).

### <a name="top-use-cases"></a>Casos de uso principales

* Mensajes críticos, errores y advertencias
* Mensajes de éxito
* Mensajes informativos o promocionales

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran las plantillas de interfaz de usuario de la barra de notificaciones en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="En el ejemplo se muestra la plantilla de interfaz de usuario de la barra de notificaciones en el móvil." border="false":::

---

## <a name="stage"></a>Etapa

Stage permite a los usuarios ver contenido (como una imagen, un archivo o un sitio web) en una superficie grande Teams sin cambiar de contexto. La fase es principalmente para ver contenido. No use fases para interacciones complejas.

Obtenga información sobre cómo implementar [la fase](~/tabs/tabs-link-unfurling.md).

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar contenido en una superficie grande dentro de Teams en lugar de otra aplicación o explorador
* Contenido multimedia destacado u otro contenido enriquecido

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de fase en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

La aplicación puede iniciar una fase desde una tarjeta adaptable, un vínculo compartido o componentes visuales (como un gráfico).

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="En el ejemplo se muestra una plantilla de fase en el móvil." border="false":::

---

## <a name="toolbar"></a>Barra de herramientas

Una barra de herramientas es un contenedor para agrupar un conjunto de controles.

### <a name="top-use-cases"></a>Casos de uso principales

* Acciones contextuales en el contenido de la aplicación
* Filtro contextual y búsqueda
* Navegación y rutas de navegación

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas en el móvil." border="false":::

---
