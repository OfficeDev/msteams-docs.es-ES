---
title: Pestañas en dispositivos móviles
description: Describe las directrices para diseñar pestañas que funcionan en dispositivos móviles.
ms.topic: conceptual
localization_priority: Normal
keywords: directrices de diseño de equipos hacen referencia a las pestañas móviles de aplicaciones personales del marco
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566701"
---
# <a name="tabs-on-mobile"></a>Pestañas en dispositivos móviles

Puede incluir pestañas en Teams canales móviles, chats y aplicaciones personales.

## <a name="accessing-personal-tabs"></a>Acceso a pestañas personales

Puede acceder a pestañas personales en el cajón de la aplicación.

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Ilustración que muestra la Teams cajón de aplicaciones móviles." border="false":::

## <a name="accessing-channel-tabs"></a>Acceso a las pestañas de canal

Puedes acceder a las pestañas de canal y grupo seleccionando el botón **Más** en el canal o chat en el que se han agregado.

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Ilustración que muestra una pestaña móvil Teams." border="false":::

## <a name="design-considerations"></a>Consideraciones sobre diseño

Nuestra plataforma móvil permite que las aplicaciones sean una experiencia inmersiva con el contenido de la aplicación ocupando toda la pantalla, aparte de la navegación principal Teams. Para crear una experiencia inmersiva que se ajuste a Teams, siga estas directrices.

### <a name="responsive-design"></a>Diseño dinámico

Dado que la pestaña se puede abrir en dispositivos con una amplia gama de tamaños de pantalla, debe seguir los principios [de diseño responsivos.](https://www.w3schools.com/html/html_responsive.asp) Todas las construcciones clave deben ser accesibles en dispositivos móviles, y las vistas no deben distorsionarse. Asegúrese de que cuando la pestaña está cargada en un dispositivo móvil, todos los botones y enlaces son fácilmente accesibles mediante la navegación basada en dedos.

### <a name="layouts"></a>Diseños

Es importante elegir el diseño correcto para su pestaña. Debe tener en cuenta el tipo de información que está presentando y elegir un diseño que la organice para facilitar su consumo. Algunas opciones potenciales se describen a continuación.

#### <a name="single-canvas"></a>Lienzo único

Esta es una gran área donde se hace el trabajo. La aplicación Wiki Teams sigue este patrón. Si tiene una aplicación que no separa el contenido en componentes más pequeños, esto sería un buen ajuste.

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Ilustración que muestra una Teams pestaña de lienzo único móvil." border="false":::

#### <a name="list"></a>Lista

Las listas son excelentes para ordenar y filtrar grandes cantidades de datos y son excelentes para mantener las cosas más importantes en la parte superior. Es útil usar columnas clasificables. Las acciones se pueden agregar a cada elemento de lista en el menú de puntos suspensivos.

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Ilustración que muestra una pestaña de lista móvil Teams." border="false":::

#### <a name="grid"></a>rejilla

Las cuadrículas son útiles para mostrar elementos que son muy visuales. Ayuda a incluir un filtro o control de búsqueda en la parte superior.

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Ilustración que muestra una pestaña móvil Teams con un diseño de cuadrícula." border="false":::

### <a name="tabs-with-bots-on-mobile"></a>Pestañas con bots en el móvil

El ejemplo siguiente es una aplicación personal que tiene pestañas y un bot:

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Ilustración que muestra cómo la aplicación de Teams móvil que tiene pestañas y un bot." border="false":::

## <a name="ui-components"></a>Componentes de iu

### <a name="color-palettes"></a>Paletas de colores

El uso de nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a su aplicación a sentirse más como en casa en Teams. Dado que Teams móvil tiene dos temas de color (claro y oscuro), es una buena idea asegurarse de que su aplicación se ve muy bien en ambos.

#### <a name="light-color"></a>Color de luz

![paleta de colores claros](../../assets/images/light-color.png)

#### <a name="dark-color"></a>Color oscuro

![paleta de colores oscuros](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>Botones y controles

La forma en que se estilizan los botones ayuda a comunicar qué tipo de acción desencadenan. Mantenemos una amplia gama de botones con formato para mostrar diferentes niveles de énfasis. Los botones pueden tener texto, un icono o una combinación de texto y un icono. Para comunicar diferentes niveles en una jerarquía, diseñamos botones primarios y secundarios dentro de cada categoría.

#### <a name="buttons"></a>Botones

Botones primarios y secundarios.

![botones imagen](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>Controles de selección

Botones de opción, casillas de verificación y alternancias.

![controles de selección](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>Chiclets y pastillas

![chiclets y píldoras](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>Tipografía

La tipografía debe ser clara y deliberada. Haga hincapié en información importante y evite el uso de múltiples fuentes y tamaños para reducir la confusión. Recomendamos usar el caso de oración y evitar el uso de todos los límites para la localización y legibilidad.

![tipografía móvil](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>Campos y sobrevuelos

Los campos son áreas donde los usuarios pueden introducir texto. Los flyouts son más ligeros que los cuadros de diálogo y aparecen desde el panel superior.

#### <a name="list-controls"></a>Enumerar controles

![controles de listas móviles](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>Controles de campo

![controles de campo móviles](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>Consideraciones de los desarrolladores

Cuando estás creando una aplicación que incluye una pestaña, debes considerar (y probar) cómo funcionará tu pestaña en los clientes de Android e iOS Microsoft Teams. Las secciones siguientes describen algunos de los escenarios clave que debe tener en cuenta.

### <a name="authentication"></a>Autenticación

Para que la autenticación funcione en clientes móviles, debe actualizarlo Teams SDK de JavaScript a al menos la versión 1.4.1.

### <a name="low-bandwidth-and-intermittent-connections"></a>Bajo ancho de banda y conexiones intermitentes

Los clientes móviles necesitan regularmente funcionar con bajo ancho de banda y conexiones intermitentes. La aplicación debe controlar los tiempos de espera adecuadamente proporcionando un mensaje contextual al usuario. También debe tener indicadores de progreso del usuario para proporcionar comentarios a los usuarios para cualquier proceso de larga ejecución.

> [!NOTE]
> Las pestañas solo se habilitan en el móvil después de agregar la aplicación a una lista de permisos, en función de la entrada del equipo de aprobación. Para comprobar la capacidad de respuesta del móvil, póngase en contacto con teamsubm@microsoft.com.

### <a name="testing-on-mobile-clients"></a>Pruebas en clientes móviles

Debe validar que su pestaña funciona correctamente en dispositivos móviles de varios tamaños y calidades. Para dispositivos Android, puede usar [devTools para depurar](~/tabs/how-to/developer-tools.md) la pestaña mientras se está ejecutando. Le recomendamos que pruebe en dispositivos de alto y bajo rendimiento, incluida una tableta.

### <a name="distribution"></a>Distribución

Las aplicaciones que aparecen en la tienda Teams deben estar aprobadas para que el uso móvil funcione correctamente en el cliente móvil Teams. La disponibilidad y el comportamiento de las pestañas dependen de si la aplicación está aprobada.

#### <a name="apps-on-teams-store-approved-for-mobile"></a>Aplicaciones en Teams tienda aprobada para móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la tienda Teams y se aprueba para uso móvil:

|Funcionalidad   |¿Disponibilidad móvil?   |Comportamiento móvil|
|----------|-----------|------------|
|Canal <br /> y la pestaña de grupo|Sí|La pestaña se abre en el cliente móvil Teams mediante la configuración de la `contentUrl` aplicación.|
|Aplicación personal|Sí|Cada pestaña de la pestaña de la aplicación personal se abre en el cliente móvil Teams mediante su `contentUrl` configuración respectiva.|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Aplicaciones en Teams tienda no aprobadas para móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la tienda Teams pero no está aprobada para uso móvil:

| Funcionalidad | ¿Disponibilidad móvil? | Comportamiento móvil |
|----------|-----------|------------|
|Canal y pestaña de grupo|Sí|La pestaña se abre en el explorador predeterminado del dispositivo en lugar de la Teams cliente móvil mediante la configuración de la `websiteUrl` aplicación, que también debe incluirse en la función del código `setSettings()` [](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)fuente. Sin embargo, los usuarios todavía pueden ver la pestaña en el cliente móvil Teams seleccionando **Más** junto a la aplicación y eligiendo **Abrir**, lo que desencadena la configuración de la `contentUrl` aplicación.|
|Aplicación personal|No|No aplicable|

#### <a name="apps-not-on-teams-store"></a>Aplicaciones que no están en Teams tienda

Si estás descargando tu aplicación o publicando en el catálogo de aplicaciones de una organización, el comportamiento de las pestañas será el mismo que Teams aplicaciones de tienda aprobadas por Microsoft para dispositivos móviles.
