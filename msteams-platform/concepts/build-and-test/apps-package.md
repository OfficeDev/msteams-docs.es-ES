---
title: Empaquetar la aplicación
description: Obtenga información sobre cómo empaquetar su aplicación de Microsoft Teams para probarlas, cargarlas y almacenar publicaciones.
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605291"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Crear un paquete de aplicación para la aplicación de Microsoft Teams

Las aplicaciones en Teams se definen mediante un archivo JSON del manifiesto de la aplicación y se incluyen en un paquete de la aplicación con sus iconos. Necesitará un paquete de aplicaciones para cargar e instalar la aplicación en Teams y publicar en el catálogo de aplicaciones de línea de negocio o en AppSource.

Un paquete de la aplicación Teams es un archivo. zip que contiene lo siguiente:

* Un archivo de manifiesto denominado `manifest.json` , que especifica los atributos de la aplicación y apunta a los recursos necesarios para su experiencia, como la ubicación de la página de configuración de la pestaña o el identificador de aplicación de Microsoft para su bot.
* [Iconos de colores y contornos de la aplicación](#app-icons).

## <a name="creating-a-manifest"></a>Creación de un manifiesto

*Teams App Studio* puede ayudarle a configurar el manifiesto. También contiene una biblioteca de control React y ejemplos configurables para tarjetas. Consulte [Introducción a App Studio](~/concepts/build-and-test/app-studio-overview.md).

El archivo de manifiesto debe tener el nombre "manifest.json" y estar en el nivel superior del paquete de carga. Tenga en cuenta que los manifiestos y paquetes creados anteriormente podrían admitir una versión anterior del esquema. Para las aplicaciones de Teams y el envío de AppSource (anteriormente tienda Office), debe usar el [esquema del manifiesto](~/resources/schema/manifest-schema.md)actual.

> [!TIP]
> Especifique el esquema al principio del manifiesto para habilitar IntelliSense o compatibilidad similar desde el editor de código:
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a>Iconos de la aplicación

El paquete de la aplicación debe incluir dos versiones de PNG del icono de la aplicación: un icono en color y un icono de esquema. Para que la aplicación pase la revisión de AppSource, estos iconos deben cumplir los siguientes requisitos de tamaño.

> [!Note]
> Si la aplicación tiene una extensión de bot ó n de mensajería, los iconos también se incluirán en el registro del servicio de bot de Microsoft Azure.

### <a name="color-icon"></a>Icono de color

La versión de color del icono se muestra en la mayoría de los escenarios de Teams y debe ser de 192x192 píxeles. El símbolo de icono (96x96 píxeles) puede tener cualquier color o colores, pero debe sentarse en un fondo cuadrado sólido o totalmente transparente.

Microsoft Teams recorta automáticamente el icono para mostrar un cuadrado con esquinas redondeadas en varios escenarios y una forma hexagonal en los escenarios de bot. Incluya 48 píxeles de relleno alrededor del símbolo para que estos cultivos puedan realizarse sin perder detalle.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Guía de diseño de iconos de color de Microsoft Teams." border="false":::

### <a name="outline-icon"></a>Icono de esquema

Un icono de esquema se muestra en dos escenarios:

* Cuando la aplicación esté en uso y "activada" en la barra de la aplicación a la izquierda de Teams.
* Cuando un usuario ancla la extensión de mensajería de la aplicación.

El icono debe ser de 32 x 32 píxeles. Puede ser blanca con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores). El icono de esquema no debe tener ningún relleno adicional alrededor del símbolo.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Guía de diseño de iconos de color de Microsoft Teams." border="false":::

### <a name="best-practices"></a>Procedimientos recomendados

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Ilustración que muestra cómo diseñar los iconos de la aplicación." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Do: siga las instrucciones del icono de esquema preciso

Los valores RGB de blanco usados en el icono deben tener el color rojo: 255, verde: 255, azul: 255. Todas las demás partes del icono de esquema deben ser completamente transparentes, con el canal alfa establecido en 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Ilustración que muestra cómo no diseñar los iconos de la aplicación." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>No: recortar en una forma cuadrada circular o redondeada

El icono de color enviado en el paquete de la aplicación debe ser cuadrado. No Redondee las esquinas del icono. Microsoft Teams ajusta automáticamente el radio de la esquina.

   :::column-end:::
:::row-end:::

### <a name="examples"></a>Ejemplos

Así es cómo aparecen los iconos de la aplicación en diferentes capacidades y contextos de Teams.

#### <a name="personal-app"></a>Aplicación personal

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en una aplicación personal." border="false":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Ejemplo que muestra cómo un icono de aplicación se busca en un bot dentro de un canal." border="false":::

#### <a name="messaging-extension"></a>Extensión de mensajería

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texto alternativo>" border="false":::
