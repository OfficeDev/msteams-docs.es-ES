---
title: Pestañas en dispositivos móviles
description: Describe las instrucciones para diseñar pestañas que funcionan en dispositivos móviles.
keywords: guías de diseño de Microsoft Teams referencia del marco de trabajo de aplicaciones móviles
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279780"
---
# <a name="tabs-on-mobile"></a>Pestañas en dispositivos móviles

> [!NOTE]
> Si elige que la ficha canal/grupo aparezca en los clientes móviles de Teams, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad (vea a continuación).

Las pestañas personalizadas pueden formar parte de un canal, un chat en grupo o una aplicación personal (aplicaciones que contienen pestañas estáticas y/o un bot de uno a uno).

Las aplicaciones personales están disponibles en los clientes móviles en el cajón de la aplicación. La aplicación solo se puede instalar desde un cliente de escritorio o Web, y puede tardar hasta 24 horas en aparecer en los clientes móviles.

Las pestañas de canal también están disponibles en dispositivos móviles. El comportamiento predeterminado es usar actualmente el `websiteUrl` para iniciar la pestaña en una ventana del explorador. Sin embargo, se pueden cargar en un cliente móvil haciendo clic en el `...` menú de desbordamiento situado junto a la pestaña y seleccionando **abrir**, que usará el `contentUrl` para cargar la pestaña en el cliente móvil de Microsoft Teams.

## <a name="accessing-personal-tabs"></a>Obtener acceso a pestañas personales

La siguiente ilustración muestra cómo tener acceso a una pestaña personal en dispositivos móviles.

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Ilustración que muestra el alimentador de la aplicación móvil de Microsoft Teams." border="false":::

## <a name="accessing-channel-tabs"></a>Acceso a las pestañas de canal

La siguiente ilustración muestra cómo tener acceso a una ficha de canal en dispositivos móviles.

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Ilustración que muestra una pestaña de Microsoft Teams Mobile." border="false":::

## <a name="design-considerations"></a>Consideraciones sobre diseño

Nuestra plataforma móvil permite que las aplicaciones sean una experiencia envolvente con el contenido de la aplicación y que se ocupe de toda la pantalla, además de la navegación principal de Microsoft Teams. Para crear una experiencia envolvente que se ajuste a los equipos, siga estas instrucciones.

### <a name="responsive-design"></a>Diseño dinámico

Como la pestaña se puede abrir en dispositivos con una amplia variedad de tamaños de pantalla, debe seguir los principios de [diseño de capacidad de respuesta](https://www.w3schools.com/html/html_responsive.asp) . Todas las construcciones de clave deben ser accesibles en dispositivos móviles y las vistas no se deben distorsionar. Asegúrese de que, al cargar la pestaña en un dispositivo móvil, se puede acceder fácilmente a todos los botones y vínculos mediante la navegación basada en el dedo.

### <a name="layouts"></a>Diseños

Es importante elegir el diseño correcto para la ficha. Debe tener en cuenta el tipo de información que está presentando y elegir un diseño que la organice para un consumo sencillo. A continuación se describen algunas de las posibles opciones.

#### <a name="single-canvas"></a>Lienzo único

Este es un área de gran tamaño en la que se realiza el trabajo. La aplicación wiki de Teams sigue este patrón. Si tiene una aplicación que no separa el contenido en componentes más pequeños, sería una buena opción.

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Ilustración que muestra una pestaña de lienzo único de Teams Mobile." border="false":::

#### <a name="list"></a>Lista

Las listas son excelentes para ordenar y filtrar grandes cantidades de datos y son excelentes para conservar las cosas más importantes en la parte superior. Es útil usar columnas que se puedan ordenar. Se pueden agregar acciones a cada elemento de lista en el menú de puntos suspensivos.

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Ilustración que muestra una pestaña de la lista de Teams para móviles." border="false":::

#### <a name="grid"></a>Redes

Las cuadrículas son útiles para mostrar elementos que son muy visuales. Ayuda a incluir un filtro o control de búsqueda en la parte superior.

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Ilustración que muestra una pestaña de Microsoft Teams Mobile con un diseño de cuadrícula." border="false":::

### <a name="tabs-with-bots-on-mobile"></a>Pestañas con bots en dispositivos móviles

El siguiente ejemplo es una aplicación personal que tiene pestañas y un bot.

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Ilustración que muestra la aplicación de equipos móviles que tiene pestañas y un bot." border="false":::

## <a name="ui-components"></a>Componentes de la interfaz de usuario

### <a name="color-palettes"></a>Paletas de colores

El uso de nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a que la aplicación se sienta más en casa en Microsoft Teams. Como Teams Mobile tiene dos temas de color (claro y oscuro), es una buena idea asegurarse de que la aplicación tenga un aspecto excelente en ambos.

#### <a name="light-color"></a>Color claro

![paleta de colores claros](../../assets/images/light-color.png)

#### <a name="dark-color"></a>Color oscuro

![paleta de colores oscuro](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>Botones y controles

La forma en que los botones están estilo ayuda a comunicar el tipo de acción que desencadenan. Mantenemos una amplia gama de botones que tienen formato para mostrar distintos niveles de énfasis. Los botones pueden tener texto, un icono o una combinación de texto y un icono. Para comunicar distintos niveles de una jerarquía, se diseñaron botones principales y secundarios dentro de cada categoría.

#### <a name="buttons"></a>Botones

Botones principal y secundario.

![imagen de botones](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>Controles de selección

Botones de opción, casillas de verificación y alternancias.

![controles de selección](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>Chiclets y píldoras

![Chiclets y píldoras](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>Tipografía

La tipografía debe ser clara y intencionada. Resalte la información importante y evite usar varias fuentes y tamaños para reducir la confusión. Se recomienda usar el tipo de oración y evitar el uso de mayúsculas y minúsculas para la localización y la legibilidad.

![tipografía móvil](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>Campos y controles flotantes

Los campos son áreas en las que los usuarios pueden escribir texto. Los controles flotantes son más sencillos que los cuadros de diálogo y aparecen en el panel superior.

#### <a name="list-controls"></a>Enumerar controles

![controles de lista de dispositivos móviles](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>Controles de campo

![controles de campo de dispositivos móviles](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>Consideraciones para desarrolladores

Al crear una aplicación que incluya una pestaña, debe tener en cuenta (y probar) cómo funcionará la pestaña en los clientes de Android e iOS de Microsoft Teams. En las secciones siguientes se describen algunos de los escenarios clave que debe tener en cuenta.

### <a name="testing-on-mobile-clients"></a>Pruebas en clientes móviles

Debe validar que la pestaña funcione correctamente en dispositivos móviles de varios tamaños y cualidades. Para dispositivos Android, puede usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se ejecuta. Le recomendamos que realice pruebas tanto en los dispositivos de rendimiento alto como en los de baja performance, así como en tabletas.

### <a name="authentication"></a>Autenticación

Para que la autenticación funcione en los clientes móviles, debe actualizar el SDK de Teams de JavaScript a la versión 1.4.1 como mínimo.

### <a name="low-bandwidth-and-intermittent-connections"></a>Bajo ancho de banda y conexiones intermitentes

Los clientes móviles necesitan tener que funcionar con frecuencia con ancho de banda bajo y conexiones intermitentes. La aplicación debe controlar los tiempos de espera de forma adecuada al suministrar un mensaje contextual al usuario. También debe indicar los indicadores de progreso del usuario para proporcionar comentarios a los usuarios sobre los procesos de ejecución prolongada.
