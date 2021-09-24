---
title: Información general sobre las acciones universales para tarjetas adaptables
description: Una introducción rápida a las acciones universales para tarjetas adaptables.
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: ba957456e2926e11b021f6a2577706cef7fb5ad7
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475716"
---
# <a name="universal-actions-for-adaptive-cards"></a>Acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables evolucionaron a partir de los comentarios de los desarrolladores que, aunque el diseño y la representación de las tarjetas adaptables era universal, el control de la acción no lo era. Incluso si un desarrollador quisiera enviar la misma tarjeta a distintos lugares, debe controlar las acciones de forma diferente.

Las acciones universales para tarjetas adaptables traen el bot como el back-end común para controlar acciones e introduce un nuevo tipo de acción, , que funciona en todas las aplicaciones, como Teams y `Action.Execute` Outlook.

Este documento le ayuda a comprender cómo puede usar el modelo de acciones universales para mejorar la experiencia del usuario de interactuar con tarjetas adaptables en plataformas y aplicaciones.

> [!NOTE]
> La compatibilidad con acciones universales para tarjetas adaptables v1.4 solo está disponible para las tarjetas enviadas por el bot. La compatibilidad con las tarjetas enviadas a través del cuadro de redacción y las tarjetas de desamuestración de vínculos estará disponible próximamente.

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a>Mejorar las experiencias de usuario con acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables mejoran la experiencia del usuario al habilitar los siguientes escenarios:

* [Acciones universales](#universal-actions)
* [Vistas específicas de usuario](#user-specific-views)
* [Compatibilidad con flujos de trabajo secuenciales](#sequential-workflow-support)
* [Vistas actualizadas](#up-to-date-views)

### <a name="universal-actions"></a>Acciones universales

Antes de las acciones universales para tarjetas adaptables, los distintos hosts proporcionaba diferentes modelos de acción de la siguiente manera:

* Teams o bots usados , un enfoque que aplaza el modelo de comunicación `Action.Submit` real al canal subyacente.
* Outlook se `Action.Http` usa para comunicarse con el servicio back-end especificado explícitamente en la carga de la tarjeta adaptable.

La siguiente imagen muestra el modelo de acción incoherente actual:

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="Modelo de acción incoherente":::

Con las acciones universales para tarjetas adaptables, puedes usar para el control `Action.Execute` de acciones en diferentes plataformas. `Action.Execute`funciona en todos los concentradores, incluidos Teams y Outlook. Además, se puede devolver una tarjeta adaptable como respuesta para una `Action.Execute` solicitud de invocación desencadenada.

En la siguiente imagen se muestra el nuevo modelo de acción universal:

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="Nuevas acciones universales para tarjetas adaptables":::

Ahora puede enviar la misma tarjeta a ambos, Teams y Outlook, y mantenerlos sincronizados entre sí mediante el bot subyacente. Cualquier acción realizada en cualquier plataforma se refleja en la otra con esta compilación una *vez,* implemente en cualquier lugar (acciones universales para tarjetas adaptables).

En la siguiente imagen se muestran las acciones universales de las tarjetas adaptables para Teams y Outlook:

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-teams-outlook.jpg" alt-text="La misma tarjeta móvil para Teams y Outlook":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="La misma tarjeta que Teams y Outlook":::

* * *

### <a name="user-specific-views"></a>Vistas específicas de usuario

Hoy en día, todos los usuarios Teams chat o canal ven exactamente las mismas acciones de vista y botón en la tarjeta adaptable. Sin embargo, en determinados escenarios existe un requisito para que determinados usuarios actúen de forma diferente y tengan acceso a información diferente dentro del mismo chat o canal.

Por ejemplo, si envía una tarjeta de informes de incidentes en un chat o canal, solo el usuario al que se le asignó el incidente debe ver un **botón** Resolver. Por otra parte, el creador de incidentes debe ver un botón **Editar** y todos los demás usuarios solo deben poder ver los detalles del incidente. Esto es posible mediante vistas específicas del usuario habilitadas por la `refresh` propiedad.

En la siguiente imagen se muestra un ejemplo de una extensión de mensajería de vales (ME) donde se muestran diferentes usuarios en el chat diferentes acciones según el requisito:

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Vistas específicas del usuario móvil":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Vistas específicas de usuario":::

* * *

Para obtener más información, vea [el ejemplo de vistas específicas del usuario](User-Specific-Views.md).

### <a name="sequential-workflow-support"></a>Compatibilidad con flujos de trabajo secuenciales

Con la compatibilidad con flujo de trabajo secuencial, los usuarios pueden avanzar a través de una serie de flujos de trabajo sin enviar tarjetas diferentes por separado. Esto es posible gracias a la capacidad de `Action.Execute` devolver una tarjeta adaptable en respuesta a una acción. Además, cualquier usuario del chat o canal puede avanzar a través de su flujo de trabajo sin modificar la tarjeta para otros usuarios en el chat.

En la siguiente imagen se muestra un ejemplo de bot de ordenación de alimentos: <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

La siguiente imagen muestra los distintos estados para diferentes usuarios en el chat o canal:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Estados del bot de restauración":::

Para obtener más información, vea [el ejemplo de Flujo de trabajo secuencial](Sequential-Workflows.md).

### <a name="up-to-date-views"></a>Vistas actualizadas

Puedes crear tarjetas adaptables que se actualicen automáticamente. Por ejemplo, puede ser una solicitud de aprobación enviada por un usuario. Después de la aprobación, la tarjeta debe mostrar automáticamente los detalles sobre el tiempo de aprobación de la solicitud y quién aprobó la solicitud. El modelo de actualización permite proporcionar dichas vistas actualizadas. En la siguiente imagen se muestra un flujo de aprobación de varios pasos y cómo se muestran las vistas para diferentes usuarios.

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="Vistas específicas del usuario actualizadas":::

Para obtener más información, vea [el ejemplo de vistas actualizadas](Up-To-Date-Views.md).

Ahora, puede comprender cómo se pueden transformar las tarjetas adaptables con el nuevo modelo de acciones universales para proporcionar una experiencia de usuario única y mejorada.

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a>Tarjetas adaptables y el nuevo modelo de acciones universales

Las tarjetas adaptables son una combinación de contenido, como texto y gráficos, y acciones que puede realizar un usuario. Para obtener más información, vea [Adaptive Cards](http://adaptivecards.io/). Las nuevas acciones universales para tarjetas adaptables permiten un control común de las acciones de tarjeta adaptable en plataformas y aplicaciones. Para obtener más información, [vea Universal Action Model](/adaptive-cards/authoring-cards/universal-action-model).

Puede empezar actualizando escenarios mediante la guía [de inicio rápido](Work-with-universal-actions-for-adaptive-cards.md) y aprovechar las acciones universales.

## <a name="see-also"></a>Vea también

* [Qué son los bots](~/bots/what-are-bots.md)
* [Información general sobre tarjetas adaptables](~/task-modules-and-cards/what-are-cards.md)
* [Tarjetas adaptables a Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)
* [Tarjetas adaptables @ Ignite 2020](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Trabajar con Acciones universales para tarjetas adaptables](Work-with-universal-actions-for-adaptive-cards.md)
