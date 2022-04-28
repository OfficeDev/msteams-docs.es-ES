---
title: Introducción a las acciones universales para tarjetas adaptables
description: Información general rápida sobre acciones universales para tarjetas adaptables, como vistas específicas del usuario, compatibilidad secuencial con flujos de trabajo y mucho más para entornos de escritorio y móviles
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: dc3a61b323e462f90937d8b6c432d624c29e0125
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103414"
---
# <a name="universal-actions-for-adaptive-cards"></a>Acciones universales para tarjetas adaptables

Las acciones universales para tarjetas adaptables evolucionaron a partir de los comentarios de los desarrolladores que, aunque el diseño y la representación de tarjetas adaptables eran universales, el control de acciones no lo era. Incluso si un desarrollador quisiera enviar la misma tarjeta a diferentes lugares, tiene que controlar las acciones de forma diferente.

Acciones universales para tarjetas adaptables incorpora el bot como back-end común para controlar acciones e introduce un nuevo tipo de acción, `Action.Execute`, que funciona entre aplicaciones, como Teams y Outlook.

Este documento le ayuda a comprender cómo puede usar el modelo de Acciones universales para mejorar la experiencia del usuario al interactuar con tarjetas adaptables entre plataformas y aplicaciones.

> [!NOTE]
> La compatibilidad con acciones universales para tarjetas adaptables v1.4 solo está disponible para las tarjetas enviadas por el bot. La compatibilidad con las tarjetas enviadas a través del cuadro de redacción y el enlace de las tarjetas desplegadas estará disponible próximamente.

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a>Mejora de las experiencias del usuario con Acciones universales para tarjetas adaptables

Acciones universales para tarjetas adaptables mejora la experiencia del usuario al habilitar los siguientes escenarios:

* [Acciones universales](#universal-actions)
* [Vistas específicas de usuario](#user-specific-views)
* [Compatibilidad con flujos de trabajo secuenciales](#sequential-workflow-support)
* [Vistas actualizadas](#up-to-date-views)

### <a name="universal-actions"></a>Acciones universales

Antes de las acciones universales para tarjetas adaptables, diferentes hosts proporcionaba diferentes modelos de acción como se indica a continuación:

* Teams o bots usados`Action.Submit`, un enfoque que aplaza el modelo de comunicación real al canal subyacente.
* Outlook se usa `Action.Http` para comunicarse con el servicio back-end especificado explícitamente en la carga de la tarjeta adaptable.

En la imagen siguiente se muestra el modelo de acción incoherente actual:

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="Modelo de acción incoherente":::

Con acciones universales para tarjetas adaptables, puede usar para el `Action.Execute` control de acciones en distintas plataformas. `Action.Execute`funciona entre centros, incluidos Teams y Outlook. Además, se puede devolver una tarjeta adaptable como respuesta para una `Action.Execute` solicitud de invocación desencadenada.

En la imagen siguiente se muestra el nuevo modelo de acción universal:

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="Nuevas acciones universales para tarjetas adaptables":::

Ahora puede enviar la misma tarjeta a ambos, Teams y Outlook, y mantenerlos sincronizados entre sí mediante el bot subyacente. Cualquier acción realizada en cualquiera de las plataformas se refleja en la otra con esta *compilación una vez, implementar en cualquier lugar* (acciones universales para tarjetas adaptables).

En la imagen siguiente se muestran las acciones universales para tarjetas adaptables para Teams y Outlook:

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="~/assets/images/mobile-universal-bots-teams-outlook.png" alt-text="Tarjeta móvil para Teams y Outlook":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="Misma tarjeta para Teams y Outlook" lightbox="../../../assets/images/adaptive-cards/universal-bots-teams-outlook.png":::

* * *

### <a name="user-specific-views"></a>Vistas específicas de usuario

Hoy en día, todos los usuarios del Teams chat o canal ven exactamente las mismas acciones de vista y botón en la tarjeta adaptable. Sin embargo, en determinados escenarios hay un requisito para que determinados usuarios actúen de manera diferente y tengan acceso a información diferente dentro del mismo chat o canal.

Por ejemplo, si envía una tarjeta de informes de incidentes en un chat o canal, solo el usuario al que se asigna el incidente debe ver un botón **Resolver** . Por otro lado, el creador de incidentes debe ver un botón **Editar** y todos los demás usuarios solo deben poder ver los detalles del incidente. Esto es posible gracias a las vistas específicas del usuario habilitadas por la `refresh` propiedad .

En la imagen siguiente se muestra un ejemplo de una extensión de mensaje de vales (ME) en la que se muestran diferentes acciones de los usuarios del chat en función del requisito:

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Vistas específicas del usuario móvil" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Vistas específicas de usuario" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

* * *

Para obtener más información, vea [ejemplo de vistas específicas del usuario](User-Specific-Views.md).

### <a name="sequential-workflow-support"></a>Compatibilidad con flujos de trabajo secuenciales

Con la compatibilidad con el flujo de trabajo secuencial, los usuarios pueden avanzar a través de una serie de flujos de trabajo sin enviar tarjetas diferentes por separado. Esto es posible gracias a la capacidad de `Action.Execute` devolver una tarjeta adaptable en respuesta a una acción. Además, cualquier usuario del chat o canal puede progresar a través de su flujo de trabajo sin modificar la tarjeta de otros usuarios en el chat.

En la imagen siguiente se muestra un ejemplo de bot de pedidos de alimentos: <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

En la imagen siguiente se muestran los distintos estados de los distintos usuarios en el chat o canal:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Estados del bot de catering" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

Para obtener más información, vea [ejemplo de flujo de trabajo secuencial](Sequential-Workflows.md).

### <a name="up-to-date-views"></a>Vistas actualizadas

Puede crear tarjetas adaptables que se actualicen automáticamente. Por ejemplo, puede ser una solicitud de aprobación enviada por un usuario. Después de la aprobación, la tarjeta debe mostrar automáticamente los detalles sobre el tiempo de aprobación de la solicitud y quién aprobó la solicitud. El modelo de actualización le permite proporcionar dichas vistas actualizadas. En la imagen siguiente se muestra un flujo de aprobación de varios pasos y cómo se muestran las vistas de los distintos usuarios.

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="Vistas actualizadas específicas del usuario" lightbox="../../../assets/images/adaptive-cards/universal-bots-up-to-date-views.png":::

Para obtener más información, consulte [ejemplo de vistas actualizadas](Up-To-Date-Views.md).

Ahora, puede comprender cómo se pueden transformar las tarjetas adaptables con el nuevo modelo de Acciones universales para proporcionar una experiencia de usuario única y mejorada.

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a>Tarjetas adaptables y el nuevo modelo de acciones universales

Las tarjetas adaptables son una combinación de contenido, como texto y gráficos, y acciones que puede realizar un usuario. Para obtener más información, vea [Tarjetas adaptables](http://adaptivecards.io/). Las nuevas acciones universales para tarjetas adaptables permiten un control común de las acciones de tarjeta adaptable entre plataformas y aplicaciones. Para obtener más información, vea [Modelo de acción universal](/adaptive-cards/authoring-cards/universal-action-model).

Para empezar, actualice los escenarios mediante la guía de [inicio rápido](Work-with-universal-actions-for-adaptive-cards.md) y aproveche Las acciones universales.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Trabajar con Acciones universales para tarjetas adaptables](Work-with-universal-actions-for-adaptive-cards.md)

## <a name="see-also"></a>Vea también

* [¿Qué son los bots?](~/bots/what-are-bots.md)
* [Información general sobre tarjetas adaptables](~/task-modules-and-cards/what-are-cards.md)
* [Tarjetas adaptables @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)
* [Tarjetas adaptables @ Ignite 2020](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)
