---
title: Cambios del margen de pestaña
author: surbhigupta
description: Describe cómo la eliminación de márgenes de tabulación mejora la experiencia de creación de aplicaciones.
keywords: tab removing margins padding
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 7260c0baf6a33b69988d07cb6d0aef7f90b6c62f
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452840"
---
# <a name="tab-margin-changes"></a>Cambios del margen de pestaña

En este documento se describe cómo la eliminación de márgenes alrededor de todas las pestañas Microsoft Teams mejora la experiencia de creación de aplicaciones. Esta es una mejora introducida en Microsoft Teams 2021.
Puedes crear aplicaciones que parezcan más nativas Teams quitando los márgenes alrededor de todas las pestañas. Las pestañas con márgenes eliminados se alinean con Microsoft Teams del [kit de interfaz de usuario de Microsoft Teams.](~/tabs/design/tabs.md) La mayoría de las aplicaciones tienen un aspecto mejorado sin márgenes.

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Inteligencia de tabulación y sin márgenes" border="false":::

> [!NOTE]
> Esta característica no se aplica a los clientes móviles, ya que las pestañas vistas en los clientes móviles no tienen márgenes.

## <a name="guidelines"></a>Instrucciones

La eliminación de márgenes de tabulación afecta Teams aplicaciones que usan pestañas. En estos casos, puede agregar márgenes alrededor de los diseños de pestaña donde sea necesario. Los diseños de aplicaciones en producción tienen un efecto de relleno adicional, es decir, los márgenes proporcionados por Teams y los márgenes proporcionados por la pestaña. Sin embargo, el relleno adicional es solo temporal y desaparece en unas semanas, dejando solo el relleno proporcionado por la aplicación.

## <a name="faq"></a>Preguntas más frecuentes

**¿Está bien que chrome de la aplicación, como la barra de encabezado o la barra de tareas, toque los bordes de nuestros diseños?**

Sí, esto está bien y Teams este tipo de diseño. Ayuda a la aplicación a sentirse nativa.

**¿Está bien que el contenido de la aplicación, como texto, logotipos e imágenes, toque los bordes izquierdo y derecho de nuestros diseños?**

No, debes proporcionar tu propio relleno o márgenes a la izquierda y a la derecha de todo el contenido de la aplicación para asegurarte de que no toque los bordes de la interfaz de usuario. También puede agregar márgenes en la parte superior de la pestaña, si es necesario.

**¿Cuál es el tamaño de los márgenes de tabulación Teams aplicados anteriormente?**

* Izquierda y derecha: 20 píxeles
* Top: 16px
* Inferior: 0px

> [!IMPORTANT]
>
> * Todas las pestañas tienen sus márgenes quitados: pestañas personales, pestañas de chat (grupo), pestañas de reunión y pestañas de canal.
> * El cambio de eliminación del margen de tabulación se aplica a todas las pestañas. No hay forma de participar o no participar en el cambio.
> * El cambio de los márgenes de tabulación puede afectar a las pestañas que dependen de Microsoft Teams para proporcionar márgenes que rodean su interfaz de usuario.

## <a name="see-also"></a>Vea también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
