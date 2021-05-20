---
title: Publicar solicitudes externas para Microsoft Teams con webhooks entrantes
author: laujan
description: cómo agregar webhook entrante a Teams aplicación
keywords: equipos pestañas webhook saliente
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bb2306cb57c069d3bed06702495da2775694643a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566820"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>Publicar solicitudes externas para Teams con webhooks entrantes

## <a name="what-are-incoming-webhooks-in-teams"></a>¿Qué son los webhooks entrantes en Teams?

Los webhooks entrantes son un tipo especial de conector en Teams que proporcionan una forma sencilla para que una aplicación externa comparta contenido en canales de equipo y que a menudo se usan como herramientas de seguimiento y notificación. Teams proporciona una dirección URL única a la que se envía una carga JSON con el mensaje que desea publicar, normalmente en formato de tarjeta. Las tarjetas son contenedores de interfaz de usuario (UI) que contienen contenido y acciones relacionadas con un único tema y son una forma de presentar los datos de mensajes de forma coherente. Teams utiliza tarjetas dentro de tres capacidades:

* Bots
* Extensiones de mensajería
* Conectores

## <a name="incoming-webhook-key-features"></a>Características clave de webhook entrantes

| Característica | Descripción |
| ------- | ----------- |
|Configuración con ámbito|Los webhooks entrantes están en el ámbito y configurados en el nivel de canal. Por ejemplo, los webhooks salientes se limitan y configuran en el nivel de equipo.|
|Definiciones seguras de recursos|Los mensajes tienen el formato de cargas JSON. Esta estructura de mensajería declarativa impide la inyección de código malintencionado, ya que no hay ninguna ejecución de código en el cliente.|
|Soporte de mensajería procesable|Si decide enviar mensajes a través de tarjetas, debe utilizar el formato **de tarjeta de mensaje procesable.** Las tarjetas de mensaje procesables se admiten en todos los grupos Office 365, incluidos los Teams. Aquí están los enlaces a la [referencia de la tarjeta de mensaje accionable heredada](/outlook/actionable-messages/message-card-reference) y al área de juegos de la tarjeta de [mensajes.](https://messagecardplayground.azurewebsites.net)|
|Soporte de mensajería HTTPS independiente| Las tarjetas son una gran manera de presentar información de una manera clara y consistente. Cualquier herramienta o marco de trabajo que pueda enviar solicitudes HTTPS POST puede enviar mensajes a Teams a través de un webhook entrante.|
|Soporte de reducción|Todos los campos de texto de las tarjetas de mensajería procesables admiten el markdown básico. **No uses marcado HTML en tus tarjetas.** puesto que se omite y se trata como texto sin formato.|

> [!Note]
> Teams bots, extensiones de mensajería, webhooks entrantes y Bot Framework admiten tarjetas adaptables, un marco de plataforma entre tarjetas abierto. [Teams conectores](../../webhooks-and-connectors/how-to/connectors-creating.md) no admiten actualmente tarjetas adaptables. Sin embargo, es posible crear un [flujo](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) que publique tarjetas adaptables en un canal Teams.

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>Agregue un webhook entrante a un canal de Teams

> [!Important]  
> Si los permisos **de miembro Configuración** de su equipo Permiten a los miembros  =>    =>  **crear, actualizar y quitar conectores** está seleccionado, cualquier miembro del equipo puede agregar, modificar o eliminar un conector.

**Para agregar un webhook entrante**

1. Vaya al canal donde desea agregar el webhook y seleccione (&#8226;&#8226;&#8226;) *Más opciones* en la barra de navegación superior.
1. Elija **Conectores** en el menú desplegable y busque **Webhook entrante**.
1. Seleccione el botón **Configurar,** proporcione un nombre y, opcionalmente, cargue un avatar de imagen para el webhook.
1. La ventana de diálogo presentará una dirección URL única que se asignará al canal. Asegúrese de **copiar y guardar la dirección URL:** deberá proporcionarla al servicio externo.
1. Seleccione el botón **Listo.** El webhook estará disponible en el canal del equipo.

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Eliminar un webhook entrante de un canal de Teams

**Para eliminar un webhook entrante**

1. Vaya al canal donde se agregó el webhook y seleccione (&#8226;&#8226;&#8226;) *Más opciones* en la barra de navegación superior.
1. Elija **Conectores** en el menú desplegable.
1. A la izquierda, en **Administrar**, elija **Configurado**.
1. Seleccione el *número Configurado* para ver una lista de los conectores actuales.
1. Seleccione **Administrar** junto al conector que desea eliminar.
1. Seleccione el botón **Quitar** y se le presentará un cuadro de diálogo *Quitar configuración.*
1. Opcionalmente, complete los campos y casillas de diálogo antes de seleccionar el botón **Quitar.** El webhook se eliminará del canal del equipo.

## <a name="distribution"></a>Distribución

Tiene tres opciones para distribuir su webhook entrante:

* Configure un webhook entrante directamente para su equipo.
* Agregue una página de configuración y envuelva el webhook entrante en un [conector O365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* Empaquete y publique el conector como parte del envío de [AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)

## <a name="see-also"></a>Vea también

[Envío de mensajes a conectores y webhooks](~/webhooks-and-connectors/how-to/connectors-using.md)
