---
title: Empaquetar la aplicación
description: Obtenga información sobre cómo empaquetar la aplicación de Microsoft Teams para probar, cargar y publicar en la tienda.
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 002da681a464770a31fa6963e96fdff54701b35f
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059682"
---
# <a name="create-a-microsoft-teams-app-package"></a>Crear un paquete de aplicación de Microsoft Teams

Necesita un paquete de aplicación, pero planea distribuir la aplicación de Microsoft Teams. Un paquete válido es un archivo ZIP que contiene lo siguiente:

* **Manifiesto de aplicación**: describe cómo se configura la aplicación, incluidas sus funcionalidades, los recursos necesarios y otros atributos importantes.
* **Iconos de la aplicación**: cada paquete requiere un icono de color y contorno para la aplicación.

## <a name="app-manifest"></a>Manifiesto de la aplicación

El archivo de manifiesto de la aplicación debe estar en el nivel superior del paquete con el nombre `manifest.json`. 

Al publicar en la tienda de Teams, asegúrese de que el manifiesto hace referencia al [esquema](~/resources/schema/manifest-schema.md) más reciente.

## <a name="app-icons"></a>Iconos de la aplicación

El paquete de la aplicación debe incluir dos versiones PNG del icono de la aplicación: una versión de color y contorno.

> [!Note]
> Si la aplicación tiene un bot o una extensión de mensajería, los iconos también se incluirán en el registro de Microsoft Azure Bot Service.

Para que la aplicación pase la revisión de la tienda de Teams, estos iconos deben cumplir los siguientes requisitos de tamaño.

### <a name="color-icon"></a>Icono de color

La versión en color de su icono se muestra en la mayoría de los escenarios de Teams y debe tener 192x192 píxeles. El símbolo de icono (96 x 96 píxeles) puede ser cualquier color, pero debe situarse sobre un fondo cuadrado sólido o totalmente transparente.

Teams recorta automáticamente el icono para mostrar un cuadrado con esquinas redondeadas en varios escenarios y una forma hexagonal en escenarios de bot. Para recortar el símbolo sin perder ningún detalle, incluya 48 píxeles de relleno alrededor del símbolo.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Icono de color de Teams y la guía de diseño." border="false":::

### <a name="outline-icon"></a>Icono de esquema

Un icono de esquema se muestra en dos escenarios:

* Cuando la aplicación está en uso y “hospedada” en la barra de aplicaciones del lado izquierdo de Teams.
* Cuando un usuario ancla la extensión de mensajería de la aplicación.

El icono debe ser de 32 x 32 píxeles. Puede ser blanco con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores). El icono de esquema no debe tener relleno adicional alrededor del símbolo.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Guía de diseño de iconos de esquema de Teams." border="false":::

### <a name="best-practices"></a>Procedimientos recomendados

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Ilustración que muestra cómo diseñar los iconos de la aplicación." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Hacer: seguir las directrices precisas del icono de esquema

Los valores RGB de blanco usados en el icono deben ser Rojo: 255, Verde: 255, Azul: 255. Todas las demás partes del icono de esquema deben ser totalmente transparentes, con el canal alfa establecido en 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Ilustración que muestra cómo no diseñar los iconos de la aplicación." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>No: recortar con una forma cuadrada circular o redondeada

El icono de color enviado en el paquete de la aplicación debe ser cuadrado. No redondee las esquinas del icono. Teams ajusta automáticamente el radio de la esquina.

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>No: copiar otras marcas

Los iconos no deben imitar ningún producto protegido por derechos de autor que no posea. Por ejemplo, un diseño similar a un producto o marca de Microsoft.

### <a name="examples"></a>Ejemplos

Así es como aparecen los iconos de aplicación en diferentes contextos y funcionalidades de Teams.

#### <a name="personal-app"></a>Aplicación personal

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Ejemplo que muestra el aspecto de un icono de aplicación en una aplicación personal." border="false":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Ejemplo que muestra el aspecto de un icono de aplicación en un bot dentro del canal." border="false":::

#### <a name="messaging-extension"></a>Extensión de mensajería

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texto alternativo>" border="false":::

## <a name="next-step"></a>Paso siguiente

Elija cómo planea distribuir la aplicación:

> [!div class="nextstepaction"]
> [Transferir localmente la aplicación en Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [Publicar la aplicación en su organización](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [Publicar la aplicación en la tienda](~/concepts/deploy-and-publish/appsource/publish.md)

## <a name="see-also"></a>Vea también

[Administre sus aplicaciones con el Portal para desarrolladores de Microsoft Teams](~/concepts/build-and-test/teams-developer-portal.md)