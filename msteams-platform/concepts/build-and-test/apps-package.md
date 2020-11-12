---
title: Empaquetar la aplicación
description: Obtenga información sobre cómo empaquetar la aplicación para probarla, cargarla y publicarla en Microsoft Teams.
keywords: empaquetado de aplicaciones de Microsoft Teams
ms.topic: conceptual
ms.openlocfilehash: aec25d3346a93e15f704435f3c6aa3ddca9fd435
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/11/2020
ms.locfileid: "48997989"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Crear un paquete de aplicación para la aplicación de Microsoft Teams

Las aplicaciones en Teams se definen mediante un archivo JSON del manifiesto de la aplicación y se incluyen en un paquete de la aplicación con sus iconos. Necesitará un paquete de aplicaciones para cargar e instalar la aplicación en Teams, y para publicar en el catálogo de aplicaciones de línea de negocio o en AppSource.

Un paquete de la aplicación Teams es un archivo. zip que contiene lo siguiente:

* Un archivo de manifiesto denominado "manifest.json", que especifica los atributos de la aplicación y apunta a los recursos necesarios para su experiencia, como la ubicación de la página de configuración de la pestaña o el identificador de aplicación de Microsoft para su bot.
* Un icono de "esquema" transparente y un icono completo de "color". Vea los [iconos](#icons) más adelante en este tema para obtener más información.

## <a name="creating-a-manifest"></a>Creación de un manifiesto

*Teams App Studio* puede ayudarle a configurar el manifiesto. También contiene una biblioteca de control React y ejemplos configurables para tarjetas. Consulte [Introducción a App Studio](~/concepts/build-and-test/app-studio-overview.md).

El archivo de manifiesto debe tener el nombre "manifest.json" y estar en el nivel superior del paquete de carga. Tenga en cuenta que los manifiestos y paquetes creados anteriormente podrían admitir una versión anterior del esquema. Para las aplicaciones de Teams y el envío de AppSource (anteriormente tienda Office), debe usar el [esquema del manifiesto](~/resources/schema/manifest-schema.md)actual.

> [!TIP]
> Especifique el esquema al principio del manifiesto para habilitar IntelliSense o compatibilidad similar desde el editor de código:
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="icons"></a>Iconos

> [!Note]
> Si la aplicación contiene un bot o una extensión de mensajería, los iconos usados serán los iconos cargados en el registro de bot en el marco de robots.

Microsoft Teams requiere dos iconos para la experiencia de la aplicación, que se usarán en el producto. Los iconos deben incluirse en el paquete y se hace referencia a ellos mediante rutas relativas en el manifiesto. La longitud máxima de cada ruta de acceso es de 2048 bytes y el formato del icono es. png.

### <a name="color"></a>color

El `color` icono se usa en todo Microsoft Teams (en galerías de aplicaciones y pestañas, bots, controles flotantes, etc.). Este icono debe ser de 192x192 píxeles. El icono puede tener cualquier color (o colores), pero el fondo debe ser el color de énfasis de la marca. También debe tener una pequeña cantidad de espacio alrededor del icono para acomodar el recorte hexagonal para la versión del bot del icono.

### <a name="outline"></a>outline

El `outline` icono se usa en estos lugares: la barra de la aplicación y las extensiones de mensajería que el usuario ha marcado como "favorito". Este icono debe ser de 32 x 32 píxeles. El icono del esquema solo debe contener blanco y transparencia (sin otros colores). El icono puede ser blanco con fondo transparente o transparente con un fondo blanco. El icono de esquema no debe tener espaciado adicional alrededor del icono y debe estar tan bien recortado como sea posible y mantener al mismo tiempo las dimensiones 32x32. Estos son algunos ejemplos buenos:

> [!TIP]
>  * El color debe ser "blanco" en RGB, (rojo: 255, verde: 255, azul: 255).
>  * El icono de todos los demás elementos debe ser transparente.
>  * Para pasarlo, el icono pequeño debe ser completamente transparente, el canal alfa es 0 y cualquier otro valor es un error.

![Iconos de esquema de ejemplo](~/assets/images/icons/sample20x20s.png)

Por ejemplo, supongamos que su compañía es contoso. Debe enviar dos iconos:

![Escaparate de iconos](~/assets/images/framework/framework_submit_icon.png)

Esta es la forma en que los iconos aparecerán en la interfaz de usuario:

#### <a name="bot-and-chiclet-in-channel-view"></a>Bot y chiclet en la vista de canal

![Bot y chiclet UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a>Flotante

![Ejemplo de flotante de Contoso](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a>Barra de la aplicación y pantalla de inicio

![Ejemplo de barra de la aplicación de Contoso HomeScreen](~/assets/images/icons/appbarhomescreen.png)
