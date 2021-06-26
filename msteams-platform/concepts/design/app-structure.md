---
title: 'Diseñar la aplicación: comprender la estructura de la aplicación'
description: Comprende lo que puedes y no puedes personalizar en Microsoft Teams al diseñar la aplicación.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a574ebeb5416e614152bb24d52cc798f0032943c
ms.sourcegitcommit: 0fe60b3fd406a5768b18977df53d1f4c665e5300
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53133417"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Comprender la estructura Microsoft Teams aplicación

Al compilar la aplicación, es importante saber lo que puedes y lo que no puedes personalizar en Microsoft Teams. Esta información puede ayudarte a comprender mejor qué partes de la experiencia de la aplicación controlas.

Los siguientes fotogramas de cable muestran lo siguiente:

* Las superficies que puedes personalizar en cada Teams de la aplicación (esquemateada en rosa).
* Los ámbitos que admite cada funcionalidad.

> [!TIP]
> **¿Qué significa ámbito?** Un ámbito es un área de Teams donde las personas pueden usar la aplicación. Las aplicaciones pueden tener uno o varios ámbitos, incluidos personales, canales, chats y reuniones.

## <a name="personal-apps"></a>Aplicaciones personales

Las aplicaciones personales proporcionan un lienzo grande para hospedar el contenido de la aplicación para usuarios individuales.

***Ámbitos admitidos**: Personal*

# <a name="desktop"></a>[Escritorio](#tab/desktop)

El lienzo es un iframe para que puedas personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para aplicaciones personales en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

El lienzo es una vista web para que puedas personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para aplicaciones personales en dispositivos móviles." border="false":::

---

## <a name="tabs"></a>Pestañas

Las pestañas proporcionan un lienzo grande para hospedar el contenido de la aplicación para un grupo de usuarios. Puede incluir pestañas en espacios compartidos como canales, chats e invitaciones a reuniones.

***Ámbitos admitidos:** canales, chats, reuniones*

# <a name="desktop"></a>[Escritorio](#tab/desktop)

El lienzo es un iframe para que puedas personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las pestañas en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

El lienzo es una vista web para que puedas personalizar completamente la experiencia.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las pestañas en dispositivos móviles." border="false":::

---

## <a name="bots"></a>Bots

Los bots son aplicaciones de conversación que se integran con Teams de mensajería nativa, por lo que el trabajo de la interfaz de usuario se controla por ti. Desde el punto de vista del diseño, aún hay oportunidades de agregar personalidad, funcionalidad personalizada e información rica y procesable con nuestra compatibilidad con procesamiento de lenguaje natural (NLP) y la plataforma de tarjetas adaptables.

***Ámbitos admitidos:** Personal, Canales, Chats, Reuniones*

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para bots en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para bots en dispositivos móviles." border="false":::

---

## <a name="messaging-extensions"></a>Extensiones de mensajería

Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o realizar una acción en un mensaje sin salir de la conversación. Las extensiones de mensajería basadas en acciones te dan más control de la experiencia, mientras que Teams controla gran parte de lo que se representa para las extensiones de mensajería basadas en búsquedas.

***Ámbitos admitidos:** Personal, Canales, Chats, Reuniones*

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de mensajería en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para extensiones de mensajería en dispositivos móviles." border="false":::

---

## <a name="meeting-extensions"></a>Extensiones de reunión

Las extensiones de reunión son aplicaciones para mejorar las reuniones en directo. Puedes hospedar el contenido de la aplicación en varios escenarios, incluidos antes, durante y después de las reuniones.

***Ámbitos admitidos:** reuniones, chats*

# <a name="desktop"></a>[Escritorio](#tab/desktop)

La superficie es un iframe, lo que te permite personalizar la experiencia, pero ten en cuenta que durante las reuniones estas aplicaciones usan un tema oscuro y son estrechas.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de reunión en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

La superficie es una vista web, lo que te permite personalizar la experiencia, pero ten en cuenta que durante las reuniones estas aplicaciones usan un tema oscuro.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Imagen conceptual que muestra las áreas front-end de Teams que los desarrolladores pueden personalizar para las extensiones de reunión en dispositivos móviles." border="false":::

---
