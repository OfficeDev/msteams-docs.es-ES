---
title: Pestañas en dispositivos móviles
description: Describe las directrices para diseñar pestañas que funcionan en dispositivos móviles.
ms.topic: conceptual
localization_priority: Normal
keywords: Las directrices de diseño de teams hacen referencia a las pestañas móviles de aplicaciones personales del marco de trabajo de teams
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566701"
---
# <a name="tabs-on-mobile"></a>Pestañas en dispositivos móviles

Puedes incluir pestañas en Teams móviles, chats y aplicaciones personales.

## <a name="accessing-personal-tabs"></a>Acceso a pestañas personales

Puedes acceder a pestañas personales en el cajón de la aplicación.

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Ilustración que muestra el Teams de aplicaciones móviles." border="false":::

## <a name="accessing-channel-tabs"></a>Acceso a pestañas de canal

Puedes acceder a las pestañas canal  y grupo seleccionando el botón Más en el canal o chat en el que se han agregado.

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Ilustración que muestra una Teams móvil." border="false":::

## <a name="design-considerations"></a>Consideraciones sobre diseño

Nuestra plataforma móvil permite que las aplicaciones sean una experiencia envolvente con el contenido de la aplicación que toma toda la pantalla aparte de la navegación Teams navegación. Para crear una experiencia envolvente que se adapte a Teams, siga estas directrices.

### <a name="responsive-design"></a>Diseño dinámico

Dado que la pestaña se puede abrir en dispositivos con una amplia variedad de tamaños de pantalla, debe seguir los principios [de diseño](https://www.w3schools.com/html/html_responsive.asp) dinámico. Todas las construcciones clave deben ser accesibles en dispositivos móviles y las vistas no deben distorsionarse. Asegúrese de que cuando la pestaña se carga en un dispositivo móvil, todos los botones y vínculos son fácilmente accesibles mediante la navegación basada en los dedos.

### <a name="layouts"></a>Diseños

Es importante elegir el diseño correcto para la pestaña. Debe tener en cuenta el tipo de información que está presentando y elegir un diseño que la organice para un consumo fácil. A continuación se describen algunas opciones potenciales.

#### <a name="single-canvas"></a>Lienzo único

Este es un área grande donde se realiza el trabajo. La Teams wiki sigue este patrón. Si tienes una aplicación que no separa el contenido en componentes más pequeños, sería un buen ajuste.

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Ilustración que muestra una Teams de lienzo único móvil." border="false":::

#### <a name="list"></a>Lista

Las listas son excelentes para ordenar y filtrar grandes cantidades de datos y son excelentes para mantener las cosas más importantes en la parte superior. Es útil usar columnas que se pueden ordenar. Las acciones se pueden agregar a cada elemento de lista en el menú de puntos suspensivos.

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Ilustración que muestra una Teams de lista móvil." border="false":::

#### <a name="grid"></a>Cuadrícula

Las cuadrículas son útiles para mostrar elementos que son altamente visuales. Ayuda a incluir un filtro o un control de búsqueda en la parte superior.

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Ilustración que muestra una Teams móvil con un diseño de cuadrícula." border="false":::

### <a name="tabs-with-bots-on-mobile"></a>Pestañas con bots en dispositivos móviles

El siguiente ejemplo es una aplicación personal que tiene pestañas y un bot:

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Ilustración que muestra cómo se Teams móvil que tiene pestañas y un bot." border="false":::

## <a name="ui-components"></a>Componentes de la interfaz de usuario

### <a name="color-palettes"></a>Paletas de colores

El uso de nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a tu aplicación a sentirse más como en casa en Teams. Dado Teams móvil tiene dos temas de color (claro y oscuro), es una buena idea asegurarse de que la aplicación tenga un aspecto excelente en ambos.

#### <a name="light-color"></a>Color claro

![paleta de colores claros](../../assets/images/light-color.png)

#### <a name="dark-color"></a>Color oscuro

![paleta de colores oscuros](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>Botones y controles

El estilo de los botones ayuda a comunicar el tipo de acción que desencadenan. Mantenemos una amplia variedad de botones con formato para mostrar diferentes niveles de énfasis. Los botones pueden tener texto, un icono o una combinación de texto y un icono. Para comunicar diferentes niveles en una jerarquía, diseñamos botones principales y secundarios dentro de cada categoría.

#### <a name="buttons"></a>Botones

Botones principales y secundarios.

![imagen de botones](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>Controles de selección

Botones de radio, casillas y alternancias.

![controles de selección](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>Chiclets y pastillas

![chiclets y pastillas](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>Tipografía

La tipografía debe ser clara y con propósito. Haga hincapié en la información importante y evite usar varias fuentes y tamaños para reducir la confusión. Se recomienda usar el caso de oración y evitar el uso de todos los límites para la localización y legibilidad.

![tipografía móvil](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>Campos y desplegables

Los campos son áreas donde los usuarios pueden introducir texto. Los paneles desplegables son más ligeros que los cuadros de diálogo y aparecen en el panel superior.

#### <a name="list-controls"></a>Enumerar controles

![controles de lista móvil](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>Controles de campo

![controles de campo móvil](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>Consideraciones de desarrollador

Cuando crees una aplicación que incluya una pestaña, debes considerar (y probar) cómo funcionará la pestaña en los clientes de Android e iOS Microsoft Teams usuario. En las secciones siguientes se describen algunos de los escenarios clave que debe tener en cuenta.

### <a name="authentication"></a>Autenticación

Para que la autenticación funcione en clientes móviles, debe actualizar Teams SDK de JavaScript a al menos la versión 1.4.1.

### <a name="low-bandwidth-and-intermittent-connections"></a>Ancho de banda bajo y conexiones intermitentes

Los clientes móviles necesitan funcionar regularmente con un ancho de banda bajo y conexiones intermitentes. La aplicación debe controlar los tiempos de espera correctamente proporcionando un mensaje contextual al usuario. También debe usar indicadores de progreso del usuario para proporcionar comentarios a los usuarios sobre los procesos de larga ejecución.

> [!NOTE]
> Las pestañas solo se habilitan en dispositivos móviles después de agregar la aplicación a una lista de permitidos, en función de la entrada del equipo de aprobación. Para comprobar la capacidad de respuesta de los dispositivos móviles, llegue a teamsubm@microsoft.com.

### <a name="testing-on-mobile-clients"></a>Pruebas en clientes móviles

Debes validar que la pestaña funciona correctamente en dispositivos móviles de distintos tamaños y calidades. Para dispositivos Android, puedes usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se ejecuta. Se recomienda probar en dispositivos de alto y bajo rendimiento, incluida una tableta.

### <a name="distribution"></a>Distribución

Las aplicaciones que aparecen en la Teams deben aprobarse para que el uso móvil funcione correctamente en el Teams móvil. La disponibilidad y el comportamiento de las pestañas depende de si la aplicación está aprobada.

#### <a name="apps-on-teams-store-approved-for-mobile"></a>Aplicaciones en la Teams aprobadas para dispositivos móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la Teams y se aprueba para uso móvil:

|Funcionalidad   |¿Disponibilidad móvil?   |Comportamiento móvil|
|----------|-----------|------------|
|Canal <br /> y ficha grupo|Sí|La pestaña se abre en el Teams móvil mediante la configuración de la `contentUrl` aplicación.|
|Aplicación personal|Sí|Cada pestaña de la pestaña aplicación personal se abre en el Teams móvil mediante su configuración `contentUrl` respectiva.|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Aplicaciones en Teams no aprobadas para móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la Teams pero no se aprueba para el uso móvil:

| Funcionalidad | ¿Disponibilidad móvil? | Comportamiento móvil |
|----------|-----------|------------|
|Pestaña Canal y grupo|Sí|La pestaña se abre en el explorador predeterminado del dispositivo en lugar del cliente móvil de Teams mediante la configuración de la aplicación, que también debe incluirse en la función del código `websiteUrl` `setSettings()` [fuente](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true). Sin embargo, los usuarios aún pueden ver la pestaña  en el cliente móvil de Teams seleccionando Más junto a la aplicación y **seleccionando Abrir**, que desencadena la configuración de la `contentUrl` aplicación.|
|Aplicación personal|No|No aplicable|

#### <a name="apps-not-on-teams-store"></a>Aplicaciones que no están Teams tienda

Si estás descargando localmente la aplicación o publicando en el catálogo de aplicaciones de una organización, el comportamiento de las pestañas será el mismo que las aplicaciones de la tienda Teams aprobadas por Microsoft para dispositivos móviles.
