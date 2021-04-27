---
title: Empaquetar la aplicación
description: Obtén información sobre cómo empaquetar la aplicación de Microsoft Teams para probar, cargar y almacenar la publicación.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: c8341f3d83b5e6610e44276d6732affa1d1c1e91
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020143"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Crear un paquete de aplicación para la aplicación de Microsoft Teams

Las aplicaciones de Teams se definen mediante un archivo JSON de manifiesto de aplicación y se agrupan en un paquete de aplicación con sus iconos. Necesitarás un paquete de aplicación para cargar e instalar la aplicación en Teams y publicarla en el catálogo de aplicaciones de línea de negocio o en AppSource.

Un paquete de aplicación de Teams es un archivo .zip que contiene lo siguiente:

* Un archivo de manifiesto denominado , que especifica los atributos de la aplicación y apunta a los recursos necesarios para la experiencia, como la ubicación de su página de configuración de pestañas o el identificador de aplicación de Microsoft para `manifest.json` su bot.
* [Iconos de color y esquema de la aplicación](#app-icons).

## <a name="creating-a-manifest"></a>Creación de un manifiesto

**Teams App Studio puede** ayudar a configurar el manifiesto. También contiene una biblioteca de control React y ejemplos configurables para tarjetas. Para obtener más información, consulta [Introducción a App Studio](~/concepts/build-and-test/app-studio-overview.md).

El archivo de manifiesto debe llamarse "manifest.js" y estar en el nivel superior del paquete de carga. Tenga en cuenta que los manifiestos y paquetes creados anteriormente pueden admitir una versión anterior del esquema. Para las aplicaciones de Teams y, especialmente, el envío de AppSource (anteriormente Tienda Office), debe usar el esquema de [manifiesto actual.](~/resources/schema/manifest-schema.md)

> [!TIP]
> Especifique el esquema al principio del manifiesto para habilitar la IntelliSense o similar desde el editor de código:
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a>Iconos de la aplicación

El paquete de la aplicación debe incluir dos versiones PNG del icono de la aplicación: un icono de color y un icono de esquema. Para que la aplicación pase la revisión de AppSource, estos iconos deben cumplir los siguientes requisitos de tamaño.

> [!Note]
> Si la aplicación tiene un bot o una extensión de mensajería, los iconos también se incluirán en el registro del Servicio de bots de Microsoft Azure.

### <a name="color-icon"></a>Icono de color

La versión de color del icono se muestra en la mayoría de los escenarios de Teams y debe tener 192 x 192 píxeles. El símbolo del icono (96 x 96 píxeles) puede ser cualquier color o color, pero debe estar sobre un fondo cuadrado sólido o totalmente transparente.

Teams recorta automáticamente el icono para mostrar un cuadrado con esquinas redondeadas en varios escenarios y una forma hexagonal en escenarios de bot. Incluye 48 píxeles de relleno alrededor del símbolo para que estos recortes se puedan realizar sin perder ningún detalle.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Icono de color de Teams y instrucciones de diseño." border="false":::

### <a name="outline-icon"></a>Icono esquema

Un icono de esquema se muestra en dos escenarios:

* Cuando la aplicación está en uso y "izada" en la barra de aplicaciones a la izquierda de Teams.
* cuando un usuario ancla la extensión de mensajería de la aplicación.

El icono debe ser de 32 x 32 píxeles. Puede ser blanco con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores). El icono de esquema no debe tener ningún relleno adicional alrededor del símbolo.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Instrucciones de diseño de iconos de esquema de Teams." border="false":::

### <a name="best-practices"></a>Procedimientos recomendados

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Ilustración que muestra cómo diseñar los iconos de la aplicación." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Do: Follow the precise outline icon guidelines

Los valores RGB de blanco usados en el icono deben ser Rojo: 255, Verde: 255, Azul: 255. Todas las demás partes del icono de esquema deben ser totalmente transparentes, con el canal alfa establecido en 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Ilustración que muestra cómo no diseñar los iconos de la aplicación." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>No: Recortar en una forma cuadrada circular o redondeada

El icono de color enviado en el paquete de la aplicación debe ser cuadrado. No redondee las esquinas del icono. Teams ajusta automáticamente el radio de esquina.

   :::column-end:::
:::row-end:::

### <a name="examples"></a>Ejemplos

Este es el modo en que los iconos de la aplicación aparecen en diferentes contextos y capacidades de Teams.

#### <a name="personal-app"></a>Aplicación personal

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en una aplicación personal." border="false":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en un bot dentro del canal." border="false":::

#### <a name="messaging-extension"></a>Extensión de mensajería

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texto alternativo>" border="false":::
