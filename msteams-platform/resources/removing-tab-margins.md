---
title: Quitar márgenes de tabulación en Microsoft Teams
author: laujan
description: Describe cómo la eliminación de márgenes de tabulación mejorará la experiencia del desarrollador.
keywords: tab removing margins padding
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 78d97dca73e7fce2bf4b911f5ea4588525667378
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019716"
---
# <a name="tab-margin-changes"></a>Cambios del margen de pestaña

En este documento se describe cómo la eliminación de márgenes alrededor de todas las pestañas de Microsoft Teams mejorará la experiencia del desarrollador al crear aplicaciones. Esta es una mejora introducida en Microsoft Teams en 2021.
La eliminación de los márgenes alrededor de todas las pestañas permitirá a los desarrolladores crear aplicaciones que parezcan más nativas de Teams. Esto también se alineará con nuestros diseños [de kit de interfaz de usuario.](~/tabs/design/tabs.md) La mayoría de las aplicaciones ya se ven mejor sin los márgenes que rodean sus experiencias. Sin embargo, algunas pestañas se ven afectadas visualmente por este cambio y los desarrolladores deben realizar los cambios necesarios.

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Inteligencia de tabulación y sin márgenes" border="false":::

> [!NOTE]
> Esta característica no se aplica a los clientes móviles, ya que las pestañas vistas en los clientes móviles no tienen márgenes. 

## <a name="timelines"></a>Escalas de tiempo

* 5 de marzo de 2021: Márgenes eliminados en [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).
* 15 de junio de 2021: los márgenes se quitarán en producción.

## <a name="guidelines"></a>Instrucciones

Las aplicaciones de Microsoft Teams que usan pestañas se verán afectadas por este cambio. Los desarrolladores deben cambiar a [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) para determinar cómo se ven afectadas sus pestañas y realizar los cambios necesarios.

Los desarrolladores de pestañas no deben depender de Teams para proporcionar márgenes alrededor de sus pestañas. Se recomienda a los desarrolladores que agreguen márgenes alrededor de sus diseños de pestañas cuando sea necesario. Los diseños de aplicaciones en producción pueden parecer que hay un relleno adicional, es decir, los márgenes proporcionados por Teams y los márgenes proporcionados por la pestaña. Sin embargo, el relleno adicional es solo temporal y desaparecerá en unas semanas, dejando solo el relleno proporcionado por la aplicación.

## <a name="faq"></a>Preguntas más frecuentes

**¿Está bien que chrome de la aplicación, como la barra de encabezado o la barra de tareas, toque los bordes de nuestros diseños?**

Sí, esto está bien y se recomienda. Esto ayuda a que la aplicación se sienta nativa.

**¿Está bien que el contenido de la aplicación, como texto, logotipos e imágenes, toque los bordes izquierdo y derecho de nuestros diseños?**

No, debes proporcionar tu propio relleno o márgenes a la izquierda y a la derecha de todo el contenido de la aplicación para asegurarte de que no toque los bordes de la interfaz de usuario. También puede agregar márgenes en la parte superior de la pestaña, si es necesario.

**¿Cuál es el tamaño de los márgenes aplicados anteriormente por Teams?**

* Izquierda y derecha: 20 píxeles
* Top: 16px
* Inferior: 0px

> [!IMPORTANT]
> * Todas las pestañas tienen sus márgenes quitados: pestañas personales, pestañas de chat (grupo), pestañas de reunión y pestañas de canal.
> * No hay forma de participar o no participar en este cambio. Se aplicará a todas las pestañas.
> * Este cambio puede afectar a las pestañas que dependen de Microsoft Teams para proporcionar márgenes que rodean su interfaz de usuario.
