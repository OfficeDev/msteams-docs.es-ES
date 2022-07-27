---
title: Módulos de tareas
author: surbhigupta
description: En este módulo, aprenderá a agregar experiencias emergentes modales para recopilar o mostrar información a los usuarios desde las aplicaciones de Microsoft Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23d6a0f1645fefe66544c755ddb617eba9ea8f3e
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035299"
---
# <a name="task-modules"></a>Módulos de tareas

Los módulos de tareas le permiten crear experiencias emergentes modales en la aplicación de Teams. En el elemento emergente, puede hacer lo siguiente:

* Ejecute su propio código HTML o JavaScript personalizado.
* Muestra un `<iframe>`widget basado en YouTube o Microsoft Stream vídeo.
* Mostrar una [tarjeta adaptable](/adaptive-cards/).

Los módulos de tareas son útiles para iniciar y completar tareas o mostrar información enriquecida, como vídeos o paneles de Power Business Intelligence (BI). Una experiencia emergente suele ser más natural para los usuarios que inician y completan tareas en comparación con una pestaña o una experiencia de bot basada en conversación.

Los módulos de tareas se basan en las pestañas de Microsoft Teams. Básicamente son una pestaña dentro de una ventana emergente. Usan el mismo SDK, por lo que si ha creado una pestaña, ya está familiarizado con la creación de un módulo de tareas.

Los módulos de tarea pueden invocarse de tres maneras:

* Pestañas personales o de canal: con el SDK de pestañas de Microsoft Teams, puede invocar módulos de tareas desde botones, vínculos o menús de la pestaña. Para obtener más información, consulte [Uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md).
* Bots: usar botones en [las tarjetas enviadas](~/task-modules-and-cards/cards/cards-reference.md) desde el bot. Esto resulta útil cuando no se requiere que todos los usuarios de un canal vean lo que está haciendo con un bot. Por ejemplo, al hacer que los usuarios respondan a un sondeo en un canal, no resulta útil ver un registro de ese sondeo que se va a crear. Para obtener más información, consulte [Uso de módulos de tareas de bots de Teams](~/task-modules-and-cards/task-modules/task-modules-bots.md).
* Fuera de Teams desde un vínculo profundo: también puede crear direcciones URL para invocar un módulo de tareas desde cualquier lugar. Para obtener más información, vea [Sintaxis de vínculo profundo del módulo de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax).

## <a name="components-of-a-task-module"></a>Componentes de un módulo de tareas

Este es el aspecto de un módulo de tareas cuando se invoca desde un bot:

:::image type="content" source="../assets/images/task-module/task-module-example.png" alt-text="ejemplo de módulo de tarea":::

Un módulo de tareas incluye lo siguiente, como se muestra en la imagen anterior:

1. Icono de la [`color`](~/resources/schema/manifest-schema.md#icons)aplicación.
2. Nombre de la [`short`](~/resources/schema/manifest-schema.md#name)aplicación.
3. Título del módulo de tareas especificado en la `title` propiedad del [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).
4. Botón de cierre o cancelación del módulo de tareas. Si el usuario selecciona este botón, la aplicación recibe un `err` evento. Para obtener más información, vea [ejemplo para enviar el resultado de un módulo de tareas](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).

    > [!NOTE]
    > Actualmente no es posible detectar el `err` evento cuando se invoca un módulo de tareas desde un bot.

5. El rectángulo azul es donde aparece la página web si carga su propia página web mediante la `url` propiedad del [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object). Para obtener más información, consulte el [ajuste de tamaño del módulo de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing).
6. Si va a mostrar una tarjeta adaptable mediante la `card` propiedad del [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) , el relleno se agrega automáticamente. Para obtener más información, consulte [módulo de tareas CSS para módulos de tareas HTML o JavaScript](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules).
7. Los botones de tarjeta adaptable se representan después de seleccionar **Registrarse**. Al usar su propia página, cree sus propios botones.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Invocar y descartar módulos de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="see-also"></a>Vea también

[Tarjetas](~/task-modules-and-cards/what-are-cards.md)
