---
title: 'Diseño de la aplicación: descripción de la estructura de la aplicación'
description: Comprenda lo que puede y no puede personalizar en Microsoft Teams al diseñar la aplicación.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
keywords: wireframe channel chat meeting message extensions mobile desktop
ms.openlocfilehash: 8353fa74dce12642e5ca96c85c34dc06fc0da203
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103288"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Comprender la estructura de la aplicación de Microsoft Teams

Al compilar la aplicación, es importante saber lo que puede y no puede personalizar en Microsoft Teams. Esta información puede ayudarle a comprender mejor qué partes de la experiencia de la aplicación controla.

Las tramas de alambre siguientes muestran lo siguiente:

* Las superficies que se pueden personalizar en cada Teams funcionalidad de la aplicación (se describen en color rosa).
* Los ámbitos que admite cada funcionalidad.

> [!TIP]
> **¿Qué significa ámbito?** Un ámbito es un área de Teams donde los usuarios pueden usar la aplicación. Las aplicaciones pueden tener uno o varios ámbitos, como personales, canales, chats y reuniones.

## <a name="personal-apps"></a>Aplicaciones personales

Las aplicaciones personales proporcionan un lienzo grande para hospedar el contenido de la aplicación para usuarios individuales.

***Ámbitos admitidos**: Personal*

### <a name="mobile"></a>Móvil

El lienzo es una vista web para que pueda personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para aplicaciones personales en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

El lienzo es un iframe para que pueda personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end de Teams que los desarrolladores pueden personalizar para aplicaciones personales en el escritorio." border="false":::

## <a name="tabs"></a>Pestañas

Las pestañas proporcionan un lienzo grande para hospedar el contenido de la aplicación para un grupo de usuarios. Puede incluir pestañas en espacios compartidos, como canales, chats e invitaciones a reuniones.

***Ámbitos admitidos**: canales, chats, reuniones*

### <a name="mobile"></a>Móvil

El lienzo es una vista web para que pueda personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para pestañas en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

El lienzo es un iframe para que pueda personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para pestañas en el escritorio." border="false":::

## <a name="bots"></a>Bots

Los bots son aplicaciones conversacionales que se integran con Teams características de mensajería nativas, por lo que el trabajo de la interfaz de usuario se controla por ti. Desde el punto de vista del diseño, todavía hay oportunidades para agregar personalidad, funcionalidad personalizada e información enriquecida y procesable con nuestra plataforma de procesamiento de lenguaje natural (NLP) y tarjetas adaptables.

***Ámbitos admitidos**: Personal, Canales, Chats, Reuniones*

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para bots en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end de Teams que los desarrolladores pueden personalizar para bots en el escritorio." border="false":::

## <a name="message-extensions"></a>Extensiones de mensaje

Las extensiones de mensaje son accesos directos para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación. Las extensiones de mensajes basadas en acciones proporcionan más control de la experiencia, mientras que Teams controla gran parte de lo que se representa para las extensiones de mensajes basadas en búsqueda.

***Ámbitos admitidos**: Personal, Canales, Chats, Reuniones*

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para las extensiones de mensaje en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para las extensiones de mensaje en el escritorio." border="false":::

## <a name="meeting-extensions"></a>Extensiones de reunión

Las extensiones de reunión son aplicaciones para mejorar las reuniones en directo. Puede hospedar el contenido de la aplicación en varios escenarios, incluidos antes, durante y después de las reuniones.

***Ámbitos admitidos**: reuniones, chats*

### <a name="mobile"></a>Móvil

La superficie es una vista web, lo que te permite personalizar la experiencia, pero ten en cuenta que durante las reuniones estas aplicaciones usan un tema oscuro.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para las extensiones de reunión en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

La superficie es un iframe que te permite personalizar la experiencia, pero ten en cuenta que durante las reuniones estas aplicaciones usan un tema oscuro y son estrechas.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para las extensiones de reunión en el escritorio." border="false":::
