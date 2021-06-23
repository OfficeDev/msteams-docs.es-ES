---
title: Publicar solicitudes externas en Microsoft Teams webhooks entrantes
author: surbhigupta
description: cómo agregar webhook entrante a Teams aplicación
keywords: webhook saliente de pestañas de teams
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: acaf2c7ba8c9c6d34399b51f3c0ef9a1110c0fb4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068934"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>Publicar solicitudes externas en Teams webhooks entrantes

## <a name="what-are-incoming-webhooks-in-teams"></a>¿Qué son los webhooks entrantes en Teams?

Los webhooks entrantes son un tipo especial de Connector en Teams que proporcionan una forma sencilla de que una aplicación externa comparta contenido en canales de grupo y que a menudo se usan como herramientas de seguimiento y notificación. Teams proporciona una dirección URL única a la que envía una carga JSON con el mensaje que desea publicar, normalmente en formato de tarjeta. Las tarjetas son contenedores de interfaz de usuario (UI) que contienen contenido y acciones relacionadas con un solo tema y son una forma de presentar datos de mensajes de forma coherente. Teams tarjetas dentro de tres funciones:

* Bots
* Extensiones de mensajería
* Conectores

## <a name="incoming-webhook-key-features"></a>Características clave de webhook entrantes

| Característica | Descripción |
| ------- | ----------- |
|Configuración con ámbito|Los webhooks entrantes están en el ámbito y configurados en el nivel de canal. Por ejemplo, los webhooks salientes están en el ámbito y configurados en el nivel de equipo.|
|Definiciones de recursos seguros|Los mensajes tienen formato de carga JSON. Esta estructura de mensajería declarativa evita la inyección de código malintencionado, ya que no hay ninguna ejecución de código en el cliente.|
|Compatibilidad con mensajes que se pueden tomar medidas|Si decide enviar mensajes a través de tarjetas, debe usar el formato de tarjeta de mensaje que **se puede usar.** Las tarjetas de mensaje que pueden actuar se admiten en todos Office 365 grupos, incluidos Teams. Estos son los vínculos [a la referencia de](/outlook/actionable-messages/message-card-reference) tarjeta de mensaje de acción heredada y al área de juegos de [tarjetas de mensaje.](https://messagecardplayground.azurewebsites.net)|
|Compatibilidad con mensajería HTTPS independiente| Las tarjetas son una excelente manera de presentar información de una manera clara y coherente. Cualquier herramienta o marco que pueda enviar solicitudes HTTPS POST puede enviar mensajes a Teams a través de un webhook entrante.|
|Compatibilidad con Markdown|Todos los campos de texto de las tarjetas de mensajería que pueden actuar admiten Markdown básico. **No use el marcado HTML en las tarjetas**. puesto que se omite y se trata como texto sin formato.|

> [!Note]
> Teams bots, extensiones de mensajería, webhooks entrantes y Bot Framework admiten tarjetas adaptables, un marco de plataforma entre tarjetas abierto. [Teams conectores](../../webhooks-and-connectors/how-to/connectors-creating.md) no admiten actualmente tarjetas adaptables. Sin embargo, es posible crear un flujo [que](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) publica tarjetas adaptables en un Teams canal.

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>Agregar un webhook entrante a un canal Teams entrada

> [!Important]  
> Si los permisos de miembro Configuración del equipo Permitir a los miembros crear, actualizar y quitar conectores están  =>    =>  **seleccionados,** cualquier miembro del equipo puede agregar, modificar o eliminar un conector.

**Para agregar un webhook entrante**

1. Navegue hasta el canal donde desea agregar el webhook y seleccione (&#8226;&#8226;&#8226;) *Más opciones* en la barra de navegación superior.
1. Elija **Conectores** en el menú desplegable y busque **Webhook entrante**.
1. Selecciona el **botón Configurar,** proporciona un nombre y, opcionalmente, carga un avatar de imagen para el webhook.
1. La ventana de diálogo mostrará una dirección URL única que se asignará al canal. Asegúrese de copiar **y guardar la dirección URL;** tendrá que proporcionarla al servicio externo.
1. Seleccione el **botón Listo.** El webhook estará disponible en el canal de grupo.

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Quitar un webhook entrante de un canal Teams entrada

**Para quitar un webhook entrante**

1. Navegue hasta el canal donde se agregó el webhook y seleccione (&#8226;&#8226;&#8226;) *Más opciones* en la barra de navegación superior.
1. Elija **Conectores** en el menú desplegable.
1. A la izquierda, en **Administrar**, elija **Configurar**.
1. Seleccione el *número Configurado para* ver una lista de los conectores actuales.
1. Seleccione **Administrar** junto al conector que desea eliminar.
1. Seleccione el **botón** Quitar y aparecerá un cuadro *de diálogo* Quitar configuración.
1. Opcionalmente, complete los campos del cuadro de diálogo y las casillas antes de seleccionar el **botón** Quitar. El webhook se eliminará del canal de grupo.

## <a name="distribution"></a>Distribución

Tiene tres opciones para distribuir el webhook entrante:

* Configure un webhook entrante directamente para su equipo.
* Agregar una página de configuración y ajustar el webhook entrante en [un conector de O365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* Empaquetar y publicar el conector como parte del [envío de AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)

## <a name="see-also"></a>Consulte también

[Enviar mensajes a conectores y webhooks](~/webhooks-and-connectors/how-to/connectors-using.md)
