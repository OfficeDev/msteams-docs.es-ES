---
title: Empaqueta tu aplicación
description: Obtén información sobre cómo empaquetar la aplicación Microsoft Teams para probar, cargar y almacenar publicaciones.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565217"
---
# <a name="create-a-microsoft-teams-app-package"></a>Crear un paquete de aplicación Microsoft Teams

Necesitas un paquete de aplicación, sin embargo, planeas distribuir tu aplicación Microsoft Teams. Un paquete válido es un archivo ZIP que contiene lo siguiente:

* **Manifiesto de aplicación:** describe cómo está configurada la aplicación, incluidas sus capacidades, recursos necesarios y otros atributos importantes.
* **Iconos de la aplicación:** cada paquete requiere un icono de color y contorno para la aplicación.

## <a name="app-manifest"></a>Manifiesto de la aplicación

El archivo de manifiesto de la aplicación debe estar en el nivel superior del paquete con el nombre `manifest.json` . 

Al publicar en el almacén de Teams, asegúrese de que el manifiesto hace referencia al [esquema](~/resources/schema/manifest-schema.md)más reciente.

## <a name="app-icons"></a>Iconos de la aplicación

El paquete de la aplicación debe incluir dos versiones PNG del icono de la aplicación: una versión de color y contorno.

> [!Note]
> Si la aplicación tiene un bot o una extensión de mensajería, los iconos también se incluirán en el registro Microsoft Azure Bot Service.

Para que la aplicación pase Teams revisión de la tienda, estos iconos deben cumplir los siguientes requisitos de tamaño.

### <a name="color-icon"></a>Icono de color

La versión en color del icono se muestra en la mayoría de los escenarios Teams y debe ser de 192x192 píxeles. Su símbolo de icono (96x96 píxeles) puede ser de cualquier color, pero debe sentarse sobre un fondo cuadrado sólido o totalmente transparente.

Teams recorta automáticamente el icono para mostrar un cuadrado con esquinas redondeadas en varios escenarios y una forma hexagonal en escenarios de bots. Para recortar el símbolo sin perder ningún detalle, incluye 48 píxeles de relleno alrededor de tu símbolo.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams icono de color y orientación de diseño." border="false":::

### <a name="outline-icon"></a>Icono de contorno

Un icono de contorno se muestra en dos escenarios:

* Cuando la aplicación está en uso y "izado" en la barra de aplicaciones en el lado izquierdo de Teams.
* Cuando un usuario ancle la extensión de mensajería de la aplicación.

El icono debe ser de 32x32 píxeles. Puede ser blanco con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores). El icono de contorno no debe tener ningún relleno adicional alrededor del símbolo.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams guía de diseño de iconos de contorno." border="false":::

### <a name="best-practices"></a>Procedimientos recomendados

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Ilustración que muestra cómo diseñar los iconos de la aplicación." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Hacer: Siga las directrices precisas del icono de contorno

Los valores RGB de blanco utilizados en el icono deben ser Rojo: 255, Verde: 255, Azul: 255. Todas las demás partes del icono de contorno deben ser totalmente transparentes, con el canal alfa establecido en 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Ilustración que muestra cómo no diseñar los iconos de la aplicación." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>No: Recortar en forma cuadrada circular o redondeada

El icono de color enviado en el paquete de la aplicación debe ser cuadrado. No redondees las esquinas de tu icono. Teams ajusta automáticamente el radio de esquina.

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>No: Copiar otras marcas

Sus iconos no deben imitar ningún producto protegido por derechos de autor que no posea. Por ejemplo, un diseño similar a un producto o marca de Microsoft.

### <a name="examples"></a>Ejemplos

Así es como aparecen los iconos de la aplicación en diferentes capacidades y contextos de Teams.

#### <a name="personal-app"></a>Aplicación personal

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en una aplicación personal." border="false":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en un bot dentro del canal." border="false":::

#### <a name="messaging-extension"></a>Extensión de mensajería

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<>de texto alternativo " border="false":::

## <a name="next-step"></a>Paso siguiente

Elige cómo planeas distribuir tu aplicación:

> [!div class="nextstepaction"]
> [Descarga tu aplicación en Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [Publica tu aplicación en tu organización](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [Publica tu aplicación en la tienda](~/concepts/deploy-and-publish/appsource/publish.md)
