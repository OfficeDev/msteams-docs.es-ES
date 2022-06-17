---
title: 'Diseño de la aplicación: descripción de la estructura de la aplicación'
description: En este módulo, obtenga información sobre lo que puede y no puede personalizar en Microsoft Teams al diseñar la estructura de la aplicación.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: cbcf44572b0105f9c0af4c7dc8cd0b00b6f5f9b9
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144400"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Comprender la estructura de la aplicación de Microsoft Teams

Al compilar la aplicación, es importante saber lo que puede y lo que no puede personalizar en Microsoft Teams. Esta información puede ayudarle a comprender mejor qué partes de la experiencia de la aplicación controla.

Los siguientes contornos reticulares muestran:

* Las superficies que puede personalizar en cada funcionalidad de la aplicación de Teams (descritas en rosa).
* Ámbitos que admite cada funcionalidad.

> [!TIP]
> **¿Qué significa el ámbito?** Un área de Teams donde los usuarios pueden usar la aplicación. Las aplicaciones pueden tener uno o varios ámbitos, como personales, canales, chats y reuniones.

## <a name="personal-apps"></a>Aplicaciones personales

Las aplicaciones personales proporcionan un lienzo grande para hospedar el contenido de la aplicación para usuarios individuales.

***Ámbitos compatibles**: Personal*

### <a name="mobile"></a>Móvil

El lienzo es una vista web, por lo que puede personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para aplicaciones personales en mobile." border="false":::

### <a name="desktop"></a>Escritorio

El lienzo es un iframe para que pueda personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para aplicaciones personales en desktop." border="false":::

## <a name="tabs"></a>Pestañas

Las pestañas proporcionan un lienzo grande para hospedar el contenido de la aplicación para un grupo de usuarios. Puede incluir pestañas en espacios compartidos, como canales, chats e invitaciones a reuniones.

***Contenidos ámbitos**: canales, chats, reuniones*

### <a name="mobile"></a>Móvil

El lienzo es una vista web, por lo que puede personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para pestañas en el dispositivo móvil." border="false":::

### <a name="desktop"></a>Escritorio

El lienzo es un iframe para que pueda personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para pestañas en desktop." border="false":::

## <a name="bots"></a>Bots

Los bots son aplicaciones conversacionales que se integran con las características de mensajería nativa de Teams, por lo que el trabajo de la interfaz de usuario es controlado para usted. Desde el punto de vista del diseño, todavía hay oportunidades para agregar personalidad, funcionalidad personalizada e información completa y procesable con nuestra compatibilidad con el procesamiento de lenguaje natural (NLP) y la plataforma de Tarjetas adaptables.

***Ámbitos respaldados**: Personal, Canales, Chats, Reuniones*

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para bots en el dispositivo móvil." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para bots en el escritorio." border="false":::

## <a name="message-extensions"></a>Extensiones de mensajes

Las extensiones de mensajería son métodos accesos directos para insertar contenido de la aplicación o realizar una acción en un mensaje sin salir de la conversación. Las extensiones de mensajes basadas en acciones le proporcionan más control sobre la experiencia, mientras que Teams controla gran parte de lo que representa las extensiones de mensajes basadas en búsqueda.

***Ámbitos respaldados**: Personal, Canales, Chats, Reuniones*

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para extensiones de mensaje en el dispositivo móvil." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para las extensiones de mensaje en el escritorio." border="false":::

## <a name="meeting-extensions"></a>Extensiones de reunión

Las extensiones de reunión son aplicaciones para mejorar las reuniones en directo. Puede hospedar el contenido de la aplicación en varios escenarios, incluidos antes, durante y después de las reuniones.

***Contenidos ámbitos**: reuniones, chats*

### <a name="mobile"></a>Móvil

La superficie es una vista web, lo que le permite personalizar la experiencia, pero tenga en cuenta que durante las reuniones estas aplicaciones usan el tema oscuro.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para las extensiones de reunión en dispositivo móvil." border="false":::

### <a name="desktop"></a>Escritorio

La superficie es un iframe, lo que le permite personalizar la experiencia, pero tenga en cuenta que durante las reuniones estas aplicaciones usan el tema oscuro y son estrechas.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Imagen conceptual que muestra las áreas de front-end en Teams que los desarrolladores pueden personalizar para las extensiones de reunión en desktop." border="false":::
