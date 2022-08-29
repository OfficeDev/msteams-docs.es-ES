---
title: Cambios del margen de pestaña
author: surbhigupta
description: Obtenga información sobre cómo quitar márgenes alrededor de pestañas en Microsoft Teams con el kit de interfaz de usuario. Conozca el efecto de relleno adicional, el tamaño del margen para la izquierda, la derecha, la parte superior y la parte inferior.
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 715c6b735323e442490de8634384054be565e7a8
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450446"
---
# <a name="tab-margin-changes"></a>Cambios del margen de pestaña

En este documento se describe cómo la eliminación de márgenes alrededor de todas las pestañas de Microsoft Teams mejora la experiencia de creación de aplicaciones. Esta es una mejora introducida en Teams en 2021.
Puede crear aplicaciones que parezcan más nativas de Teams quitando los márgenes alrededor de todas las pestañas. Las pestañas con márgenes quitados se alinean con los [diseños de kit de interfaz de usuario](~/tabs/design/tabs.md) de Microsoft Teams. La mayoría de las aplicaciones experimentan un aspecto mejorado sin márgenes.

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Ingenio de tabulación y sin márgenes":::

> [!NOTE]
> Esta característica no es aplicable a los clientes móviles, ya que las pestañas que se ven en los clientes móviles no tienen márgenes.

## <a name="guidelines"></a>Instrucciones

La eliminación de márgenes de tabulación afecta a las aplicaciones de Teams que usan pestañas. En tales casos, puede agregar márgenes alrededor de los diseños de pestaña donde sea necesario. Los diseños de aplicación en producción tienen un efecto de relleno adicional, es decir, márgenes proporcionados por Teams y márgenes proporcionados por la pestaña. Sin embargo, el relleno adicional solo es temporal y desaparece en unas semanas, dejando solo el relleno proporcionado por la aplicación.

## <a name="faq"></a>Preguntas más frecuentes

**¿Está bien que el cromo de la aplicación, como la barra de encabezado o la barra de tareas, toque los bordes de nuestros diseños?**

Sí, esto está bien y Teams fomenta este diseño. Ayuda a la aplicación a sentirse nativa.

**¿Está bien que el contenido de la aplicación, como texto, logotipos e imágenes, toque los bordes izquierdo y derecho de nuestros diseños?**

No, debes proporcionar tu propio relleno o márgenes a la izquierda y a la derecha de todo el contenido de la aplicación para garantizar que no toque los bordes de la interfaz de usuario. También puede agregar márgenes en la parte superior de la pestaña, si es necesario.

**¿Cuál es el tamaño de los márgenes de tabulación que Teams aplicó anteriormente?**

* Izquierda y derecha: 20 píxeles
* Superior: 16 píxeles
* Inferior: 0 píxeles

> [!IMPORTANT]
>
> * Todas las pestañas tienen sus márgenes quitados: pestañas personales, pestañas de chat (grupo), pestañas de reunión y pestañas de canal.
> * El cambio de eliminación del margen de tabulación se aplica a todas las pestañas. No hay ninguna manera de participar o no participar en el cambio.
> * El cambio de los márgenes de tabulación puede afectar a las pestañas que dependen de Microsoft Teams para proporcionar márgenes alrededor de su interfaz de usuario.

## <a name="see-also"></a>Vea también

* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o de canal](~/tabs/how-to/create-channel-group-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
