---
title: Enviar solicitudes externas a Microsoft Teams con webhooks entrantes
author: laujan
description: ''
keywords: webhook saliente de pestañas de Teams *
ms.topic: conceptual
ms.author: laujan
ms.openlocfilehash: c2b3f5dd581441f89aff344c35fe7e110d4d2e68
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676144"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>Publicar solicitudes externas a los equipos con webhooks entrantes

## <a name="what-are-incoming-webhooks-in-teams"></a>¿Qué son los webhooks entrantes en Teams?

Los webhooks entrantes son un tipo especial de conector en Microsoft teams que proporcionan una forma sencilla para que una aplicación externa comparta contenido en los canales de equipo y que, a menudo, se usan como herramientas de seguimiento y notificación. Teams proporciona una dirección URL única a la que se envía una carga JSON con el mensaje que se desea publicar, normalmente en un formato de tarjeta. Las tarjetas son contenedores de interfaz de usuario (UI) que contienen contenido y acciones relacionadas con un solo tema y son una forma de presentar datos de mensajes de forma coherente. Teams usa las tarjetas en tres capacidades:

* Bots
* Extensiones de mensajería
* Conectores

## <a name="incoming-webhook-key-features"></a>Características de la clave de webhook entrante

| Característica | Descripción |
| ------- | ----------- |
|Configuración con ámbito|Los webhooks entrantes están en el ámbito y configurados en el nivel de canal (por ejemplo, los webhooks de salida tienen ámbito y se configuran en el nivel de equipo).|
|Proteger las definiciones de recursos|Los mensajes tienen el formato de cargas JSON. Esta estructura de mensajería declarativa evita la inyección de código malintencionado ya que no hay ejecución de código en el cliente.|
|Compatibilidad con la mensajería accionable|Si opta por enviar mensajes a través de tarjetas, debe usar el formato de **tarjeta de mensaje accionable** . Las tarjetas de mensajes que requieren acción se admiten en todos los grupos de Office 365, incluido Microsoft Teams. Estos son vínculos a la [referencia de tarjeta de mensaje heredada](/outlook/actionable-messages/message-card-reference) y la [animación de tarjeta de mensaje](https://messagecardplayground.azurewebsites.net).|
|Compatibilidad con mensajería HTTPS independiente| Las tarjetas son una buena forma de presentar la información de forma clara y coherente. Cualquier herramienta o marco que pueda enviar solicitudes HTTPS POST puede enviar mensajes a Microsoft Teams a través de un webhook entrante.|
|Compatibilidad con Markdown|Todos los campos de texto en tarjetas de mensajería accionables admiten el Markdown básico. **No use marcado HTML en las tarjetas**. El código HTML se pasa por alto y se trata como texto sin formato.|

> [!Note]  
> Los bots de Microsoft Teams, las extensiones de mensajería y el marco de bot admiten tarjetas adaptables, un marco de plataforma multitarjeta abierta. Los conectores de Microsoft Teams no admiten tarjetas adaptables en este momento. Sin embargo, es posible crear un [flujo](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) que envíe tarjetas adaptables a un canal de Teams.

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>Agregar un webhook entrante a un canal de Teams

> [!Important]  
> Si los**permisos** => de miembro de **configuración** => del equipo**permiten a los miembros crear, actualizar y quitar conectores** está seleccionado, cualquier miembro del equipo puede Agregar, modificar o eliminar un conector.

1. Navegue hasta el canal donde quiera agregar el webhook y seleccione *más opciones* (&#8226;&#8226;&#8226;) de la barra de navegación superior.
1. Elija **conectores** en el menú desplegable y busque el **webhook entrante**.
1. Seleccione el botón **configurar** , especifique un nombre y, opcionalmente, cargue un avatar de imagen para el webhook.
1. La ventana del cuadro de diálogo presentará una dirección URL única que se asignará al canal. Asegúrese de **copiar y guardar la dirección URL**, ya que tendrá que proporcionarla al servicio externo.
1. Seleccione el botón **listo** . El webhook estará disponible en el canal del equipo.

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Quitar un webhook entrante de un canal de Teams

1. Navegue hasta el canal en el que se ha agregado el webhook y seleccione (&#8226;&#8226;&#8226;) *más opciones* de la barra de navegación superior.
1. Elija **conectores** en el menú desplegable.
1. En la parte izquierda, en **administrar**, elija **configurada**.
1. Seleccione el *número configurado* para ver una lista de los conectores actuales.
1. Seleccione **administrar** junto al conector que desea eliminar.
1. Seleccione el botón **quitar** y aparecerá el cuadro de diálogo *quitar configuración* .
1. Opcionalmente, complete los campos del cuadro de diálogo y las casillas de verificación antes de seleccionar el botón **quitar** . El webhook se eliminará del canal del equipo.

## <a name="distribution"></a>Reparto

Tiene tres opciones para distribuir el webhook entrante:

* Configure un webhook entrante directamente para el equipo.
* Agregar una página de configuración y envolver el webhook de entrada en un [conector de O365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* Empaquetar y publicar el conector como parte del envío de [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) .

## <a name="learn-more"></a>Más información

* [Enviar mensajes a conectores y webhooks](~/webhooks-and-connectors/how-to/connectors-using.md)