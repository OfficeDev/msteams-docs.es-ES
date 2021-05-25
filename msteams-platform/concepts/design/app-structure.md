---
title: 'Diseñar la aplicación: comprender la estructura de la aplicación'
description: Comprende lo que puedes y no puedes personalizar en Microsoft Teams al diseñar la aplicación.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631391"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Comprender la estructura Microsoft Teams aplicación

Al compilar la aplicación, es importante saber lo que puedes y lo que no puedes personalizar en Microsoft Teams. Esta información puede ayudarte a comprender mejor qué partes de la experiencia de la aplicación controlas.

Los siguientes fotogramas de cable muestran lo siguiente:

* Las superficies que puedes personalizar en cada Teams de la aplicación (esquemateada en azul).
* Los ámbitos que admite cada funcionalidad.

> [!NOTE]
> **¿Qué significa ámbito?** Un ámbito es un área de Teams donde las personas pueden usar la aplicación. Las aplicaciones pueden tener uno o varios ámbitos, incluidos personales, canales, chats y reuniones.

## <a name="personal-apps"></a>Aplicaciones personales

Las aplicaciones personales proporcionan un lienzo grande para hospedar el contenido de la aplicación para usuarios individuales. El lienzo es un iframe para que puedas personalizar completamente la experiencia.

***Ámbitos admitidos**: Personal*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para aplicaciones personales." border="false":::

## <a name="tabs"></a>Pestañas

Las pestañas proporcionan un lienzo grande para hospedar el contenido de la aplicación para un grupo de usuarios. Puede incluir pestañas en espacios compartidos como canales, chats e invitaciones a reuniones. El lienzo es un iframe para que puedas personalizar completamente la experiencia.

***Ámbitos admitidos:** canales, chats, reuniones*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las pestañas." border="false":::

## <a name="bots"></a>Bots

Los bots son aplicaciones de conversación que se integran con Teams de mensajería nativa, por lo que el trabajo de la interfaz de usuario se controla por ti. Desde el punto de vista del diseño, aún hay oportunidades de agregar personalidad, funcionalidad personalizada e información rica y procesable con nuestra compatibilidad con procesamiento de lenguaje natural (NLP) y la plataforma de tarjetas adaptables.

***Ámbitos admitidos:** Personal, Canales, Chats, Reuniones*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para bots." border="false":::

## <a name="messaging-extensions"></a>Extensiones de mensajería

Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación. Las extensiones de mensajería basadas en acciones te dan más control de la experiencia, mientras que Teams controla gran parte de lo que se representa para las extensiones de mensajería basadas en búsquedas.

***Ámbitos admitidos:** Personal, Canales, Chats, Reuniones*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de mensajería." border="false":::

## <a name="meeting-extensions"></a>Extensiones de reunión

Las extensiones de reunión son aplicaciones para mejorar las reuniones en directo. Puedes hospedar el contenido de la aplicación en varios escenarios, incluidos antes, durante y después de las reuniones. La superficie es un iframe, lo que te permite personalizar la experiencia, pero ten en cuenta que estas aplicaciones tienen un estilo oscuro y son estrechas durante las reuniones.

***Ámbitos admitidos:** reuniones, chats*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de reunión." border="false":::
