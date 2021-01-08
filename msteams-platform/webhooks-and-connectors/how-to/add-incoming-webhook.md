---
title: Publicar solicitudes externas en Microsoft Teams con webhooks entrantes
author: laujan
description: cómo agregar webhook entrante a la aplicación de Teams
keywords: webhook saliente de pestañas de teams*
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a05f9ec448a722f3d662a8323a40ebe6b2de1e27
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777920"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>Publicar solicitudes externas en Teams con webhooks entrantes

## <a name="what-are-incoming-webhooks-in-teams"></a>¿Qué son los webhooks entrantes en Teams?

Los webhooks entrantes son un tipo especial de conector en Teams que proporcionan una forma sencilla para que una aplicación externa comparta contenido en canales de equipo y se usan a menudo como herramientas de seguimiento y notificación. Teams proporciona una dirección URL única a la que envía una carga JSON con el mensaje que desea publicar, normalmente en formato de tarjeta. Las tarjetas son contenedores de interfaz de usuario (UI) que contienen contenido y acciones relacionadas con un solo tema y son una forma de presentar los datos del mensaje de forma coherente. Teams usa tarjetas dentro de tres capacidades:

* Bots
* Extensiones de mensajería
* Conectores

## <a name="incoming-webhook-key-features"></a>Características clave del webhook entrante

| Característica | Descripción |
| ------- | ----------- |
|Configuración con ámbito|Los webhooks entrantes tienen ámbito y se configuran en el nivel de canal (por ejemplo, los webhooks salientes tienen ámbito y se configuran en el nivel de equipo).|
|Definiciones de recursos seguros|Los mensajes tienen formato de cargas JSON. Esta estructura de mensajería declarativa impide la inserción de código malintencionado, ya que no hay ninguna ejecución de código en el cliente.|
|Compatibilidad con mensajería que puede ser de acción|Si decide enviar mensajes a través de tarjetas, debe usar el formato de tarjeta **de mensaje que necesita** acción. Las tarjetas de mensaje que pueden actuar se admiten en todos los grupos de Office 365, incluido Teams. A continuación se incluyen vínculos [a la referencia de la](/outlook/actionable-messages/message-card-reference) tarjeta de mensaje que necesita acción heredada y al área de juegos de [tarjetas de mensaje.](https://messagecardplayground.azurewebsites.net)|
|Compatibilidad de mensajería HTTPS independiente| Las tarjetas son una excelente manera de presentar información de una manera clara y coherente. Cualquier herramienta o marco que pueda enviar solicitudes HTTPS POST puede enviar mensajes a Teams a través de un webhook entrante.|
|Soporte técnico de Markdown|Todos los campos de texto de las tarjetas de mensajería que pueden actuar admiten Markdown básico. **No use marcado HTML en sus tarjetas.** HTML se omite y se trata como texto sin formato.|

> [!Note]
> Los bots de Teams, las extensiones de mensajería, los webhooks entrantes y bot Framework admiten las tarjetas adaptables, un marco de plataforma abierta para tarjetas cruzadas. [Actualmente, los conectores](../../webhooks-and-connectors/how-to/connectors-creating.md) de Teams no admiten tarjetas adaptables. Sin embargo, es posible crear un flujo [que](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) publica tarjetas adaptables en un canal de Teams.

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>Agregar un webhook entrante a un canal de Teams

> [!Important]  
> Si los permisos de miembros de configuración de su equipo Permiten a los miembros crear, actualizar y quitar conectores está seleccionado, cualquier miembro del equipo puede agregar, modificar o  =>    =>   eliminar un conector.

1. Navegue hasta el canal donde desea agregar el webhook y seleccione (&#8226;&#8226;&#8226;) Más *opciones* en la barra de navegación superior.
1. Choose **Connectors** from the drop-down menu and search for **Incoming Webhook**.
1. Selecciona el **botón** Configurar, proporciona un nombre y, opcionalmente, carga un avatar de imagen para el webhook.
1. La ventana de diálogo mostrará una dirección URL única que se asignará al canal. Asegúrese de copiar **y guardar la dirección URL;** tendrá que proporcionarla al servicio externo.
1. Seleccione el **botón Listo.** El webhook estará disponible en el canal de grupo.

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Quitar un webhook entrante de un canal de Teams

1. Navegue hasta el canal donde se agregó el webhook y seleccione (&#8226;&#8226;&#8226;) *Más opciones* en la barra de navegación superior.
1. Elija **Conectores** en el menú desplegable.
1. A la izquierda, en **Administrar**, elija **Configurado.**
1. Seleccione el *número Configurado* para ver una lista de los conectores actuales.
1. Seleccione **Administrar** junto al conector que desea eliminar.
1. Seleccione el **botón** Quitar y aparecerá  un cuadro de diálogo Quitar configuración.
1. Opcionalmente, completa los campos y casillas del cuadro de diálogo antes de seleccionar el **botón** Quitar. El webhook se eliminará del canal de equipo.

## <a name="distribution"></a>Distribución

Tiene tres opciones para distribuir el webhook entrante:

* Configure un webhook entrante directamente para su equipo.
* Agregar una página de configuración y encapsular el webhook entrante en un [conector de O365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* Empaquetar y publicar el conector como parte del envío [de AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)

## <a name="learn-more"></a>Obtén más información

* [Enviar mensajes a conectores y webhooks](~/webhooks-and-connectors/how-to/connectors-using.md)
