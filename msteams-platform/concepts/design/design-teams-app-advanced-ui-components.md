---
title: Diseño de la aplicación con componentes avanzados de la interfaz de usuario
author: heath-hamilton
description: Obtenga información sobre los componentes de la interfaz de usuario de Teams, como rutas de navegación, barra de notificaciones, vista de fase junto con casos de uso pertinentes.
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: 055ee4440982add222b76454f1ff4382f129ff21
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558845"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>Diseño de la aplicación de Microsoft Teams con componentes avanzados de la interfaz de usuario

Los siguientes componentes son una combinación de [componentes básicos de la interfaz de usuario](~/concepts/design/design-teams-app-basic-ui-components.md) que puede usar para situaciones de diseño comunes de Teams, como la navegación.

## <a name="microsoft-teams-ui-kit"></a>Kit de interfaz de usuario de Microsoft Teams

En función de la <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">interfaz de usuario de Fluent</a>, el kit de interfaz de usuario de Microsoft Teams incluye componentes y patrones diseñados específicamente para compilar aplicaciones de Teams. En el kit de interfaz de usuario, puede capturar e insertar los componentes enumerados aquí directamente en el diseño y ver más ejemplos de cómo usar cada componente.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>Ruta de navegación

Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación. Ayudan a los usuarios a comprender cómo encaja la página que están viendo en la experiencia general y ofrecen acceso con un solo clic a niveles más altos de esa jerarquía.

### <a name="top-use-cases"></a>Casos de uso principales

* Comunicar jerarquía
* Navegación

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación en el móvil.":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación en el escritorio.":::

## <a name="left-nav"></a>Navegación izquierda

Use el panel de navegación izquierdo para examinar varias páginas dentro de la pestaña Teams. En el ejemplo siguiente, la navegación izquierda se encuentra entre la lista de canales y el contenido de la pestaña.

### <a name="top-use-cases"></a>Casos de uso principales

* Examine varias páginas dentro de una pestaña de Teams.
* Divida las aplicaciones complejas en varias páginas.

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda en el móvil.":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda en el escritorio.":::

## <a name="notification-bar"></a>Barra de notificaciones

Una barra de notificaciones es un área dedicada para mostrar mensajes breves e importantes que no requieren que el usuario realice una acción inmediata. Los iconos y colores de fondo específicos están asociados a tipos específicos de mensajes (consulte a continuación).

Puede implementar una barra de notificaciones mediante el componente [de alerta](https://fluentsite.z22.web.core.windows.net/0.59.0/components/alert/definition) de la interfaz de usuario de Fluent.

### <a name="top-use-cases"></a>Casos de uso principales

* Mensajes críticos, errores y advertencias
* Mensajes correctos
* Mensajes informativos o promocionales

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="En el ejemplo se muestra la plantilla de interfaz de usuario de la barra de notificaciones en dispositivos móviles.":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran las plantillas de interfaz de usuario de la barra de notificaciones en el escritorio.":::

## <a name="stage-view"></a>Vista de fase

La vista de fase permite a los usuarios ver contenido (como una imagen, un archivo o un sitio web) en una superficie grande en Teams sin cambiar de contexto. Este componente es principalmente para ver contenido. No lo use para interacciones complejas.

Vea cómo implementar la [vista de fase](~/tabs/tabs-link-unfurling.md).

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar contenido en una superficie grande dentro de Teams en lugar de otra aplicación o explorador
* Contenido multimedia destacado u otro contenido enriquecido

### <a name="mobile"></a>Móvil

La aplicación puede iniciar una fase desde una tarjeta adaptable, un vínculo compartido o componentes visuales (como un gráfico).

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="En el ejemplo se muestra una plantilla de fase en el móvil.":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de fase en el escritorio.":::

## <a name="toolbar"></a>Barra de herramientas

Una barra de herramientas es un contenedor para agrupar un conjunto de controles.

### <a name="top-use-cases"></a>Casos de uso principales

* Acciones contextuales en el contenido de la aplicación.
* Filtrar y buscar contextuales.
* Navegación y rutas de navegación.

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas en el móvil.":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas en el escritorio.":::
