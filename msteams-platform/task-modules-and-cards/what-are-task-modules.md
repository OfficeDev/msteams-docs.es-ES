---
title: Módulos de tareas
author: surbhigupta
description: Agregar experiencias emergentes modales para recopilar o mostrar información a los usuarios desde Microsoft Teams aplicaciones
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3b0e639acc8901a3637189e435fcfc159e992ae3a674a437733474087103193c
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57707685"
---
# <a name="task-modules"></a>Módulos de tareas

Los módulos de tareas permiten crear experiencias emergentes modales en la Teams aplicación. En la ventana emergente, puede:

* Ejecute su propio código HTML o JavaScript personalizado.
* Mostrar un `<iframe>` widget basado en, por ejemplo, un vídeo de YouTube o Microsoft Stream.
* Mostrar una [tarjeta adaptable](/adaptive-cards/).

Los módulos de tareas son útiles para iniciar y completar tareas o mostrar información enriquecida, como vídeos o paneles de Power Business Intelligence (BI). Una experiencia emergente suele ser más natural para los usuarios que inician y completan tareas en comparación con una pestaña o una experiencia de bot basada en conversación.

Los módulos de tareas se crean sobre la base de Microsoft Teams pestañas. Son esencialmente una pestaña dentro de una ventana emergente. Usan el mismo SDK, por lo que si ha creado una pestaña, ya está familiarizado con la creación de un módulo de tareas.

Los módulos de tarea pueden invocarse de tres maneras:

* Pestañas de canal o personales: con el SDK Microsoft Teams tabs, puede invocar módulos de tareas desde botones, vínculos o menús de la pestaña. Para obtener más información, vea [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).
* Bots: usar botones en [tarjetas](~/task-modules-and-cards/cards/cards-reference.md) enviadas desde el bot. Esto es útil cuando no se requiere que todos los usuarios de un canal vean lo que está haciendo con un bot. Por ejemplo, cuando los usuarios responden a un sondeo en un canal, no resulta útil ver un registro de esa encuesta que se está creando. Para obtener más información, vea [using task modules from Teams bots](~/task-modules-and-cards/task-modules/task-modules-bots.md).
* Fuera de Teams desde un vínculo profundo: también puede crear direcciones URL para invocar un módulo de tareas desde cualquier lugar. Para obtener más información, vea [sintaxis de vínculo profundo del módulo de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax).

## <a name="components-of-a-task-module"></a>Componentes de un módulo de tareas

Este es el aspecto de un módulo de tareas cuando se invoca desde un bot:

![Ejemplo del módulo de tareas](~/assets/images/task-module/task-module-example.png)

Un módulo de tareas incluye lo siguiente como se muestra en la imagen anterior:

1. Icono de la [ `color` aplicación](~/resources/schema/manifest-schema.md#icons).
2. Nombre de la [ `short` aplicación](~/resources/schema/manifest-schema.md#name).
3. El título del módulo de tareas especificado en la `title` propiedad del [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).
4. Botón cerrar o cancelar del módulo de tareas. Si el usuario selecciona este botón, la aplicación recibe un `err` evento. Para obtener más información, vea [el ejemplo para enviar el resultado de un módulo de tareas](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).

    > [!NOTE]
    > Actualmente no es posible detectar el evento cuando se invoca un módulo de `err` tareas desde un bot.

5. El rectángulo azul es donde aparece la página web si está cargando su propia página web mediante la propiedad `url` del [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object). Para obtener más información, vea [task module sizing](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing).
6. Si va a mostrar una tarjeta adaptable mediante la propiedad `card` del [objeto TaskInfo,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) el relleno se agregará automáticamente. Para obtener más información, vea [módulo de tareas CSS para módulos de tareas HTML o JavaScript](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules).
7. Los botones de tarjeta adaptable se representan después de **seleccionar Registrarse.** Cuando use su propia página, cree sus propios botones.

## <a name="see-also"></a>Vea también

[Tarjetas](~/task-modules-and-cards/what-are-cards.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Invocar y descartar módulos de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
