---
title: Crear un webhook entrante
author: laujan
description: describe cómo agregar webhook entrante Teams aplicación y publicar solicitudes externas para Teams webhooks entrantes
keywords: webhook saliente de pestañas de teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c398776e2858283a8c4a8f7b5087e2efd365c7d3
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768143"
---
# <a name="create-incoming-webhook"></a>Crear webhook entrante

El webhook entrante permite que cualquier aplicación externa comparta contenido en Teams canales. Estos webhooks se usan como herramientas de seguimiento y notificación. Proporcionan una dirección URL única, a la que se envía una carga JSON con un mensaje en formato de tarjeta. Las tarjetas son contenedores de interfaz de usuario que incluyen contenido y acciones relacionadas con un solo tema. Teams tarjetas dentro de las siguientes funcionalidades:

* Bots
* Extensiones de mensajería
* Conectores

## <a name="key-features-of-incoming-webhook"></a>Características clave del webhook entrante

En la tabla siguiente se proporcionan las características y la descripción del webhook entrante:

| Características | Descripción |
| ------- | ----------- |
|Tarjetas adaptables con un webhook entrante|Las tarjetas adaptables se pueden enviar a través de webhooks entrantes. Para obtener más información, vea [Enviar tarjetas adaptables mediante webhooks entrantes.](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)|
|Compatibilidad con mensajes que se pueden tomar medidas|Las tarjetas de mensaje que pueden actuar se admiten en todos Office 365 grupos, incluidos Teams. Si envía mensajes a través de tarjetas, debe usar el formato de tarjeta de mensaje que se puede usar. Para obtener más información, vea [referencia de](/outlook/actionable-messages/message-card-reference) tarjeta de mensaje heredada y área de juegos de [tarjetas de mensaje.](https://messagecardplayground.azurewebsites.net)|
|Compatibilidad con mensajería HTTPS independiente|Las tarjetas proporcionan información de forma clara y coherente. Cualquier herramienta o marco que pueda enviar solicitudes HTTPS POST puede enviar mensajes a Teams a través de un webhook entrante.|
|Compatibilidad con Markdown|Todos los campos de texto de las tarjetas de mensajería que pueden actuar admiten Markdown básico. No use el marcado HTML en las tarjetas. puesto que se omite y se trata como texto sin formato.|
|Configuración con ámbito|El webhook entrante está en el ámbito y configurado en el nivel de canal.|
|Definiciones de recursos seguros|Los mensajes tienen formato de carga JSON. Esta estructura de mensajería declarativa impide la inserción de código malintencionado.|

> [!NOTE]
> * Teams bots, extensiones de mensajería, Webhook entrante y Bot Framework admiten tarjetas adaptables. Las tarjetas adaptables son un marco abierto entre plataformas que se puede usar en todas las plataformas, como Windows, Android, iOS, y así sucesivamente. Actualmente, [Teams conectores no](../../webhooks-and-connectors/how-to/connectors-creating.md) admiten tarjetas adaptables. Sin embargo, es posible crear un flujo [que](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) publica tarjetas adaptables en un Teams canal.
> * Para obtener más información sobre tarjetas y webhooks, vea [Adaptive cards and Incoming Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks).

## <a name="create-incoming-webhook"></a>Crear webhook entrante

**Para agregar un webhook entrante a un canal Teams entrada**

1. Vaya al canal donde desea agregar el webhook y seleccione &#8226;&#8226;&#8226; **Más opciones** de la barra de navegación superior.
1. Seleccione **Conectores en** el menú desplegable:

    ![Seleccionar conector](~/assets/images/connectors.png)

1. Busque **Webhook entrante y** seleccione **Agregar**.
1. Seleccione **Configurar**, proporcione un nombre y cargue una imagen para el webhook si es necesario:

    ![Botón Configurar](~/assets/images/configure.png)

1. La ventana de diálogo presenta una dirección URL única que se asigna al canal. Copie y guarde la dirección URL del webhook, para enviar información a Microsoft Teams y seleccione **Listo:**

    ![DIRECCIÓN URL única](~/assets/images/url.png)

El webhook está disponible en el canal Teams web.

Puede crear y enviar mensajes que pueden realizar acciones a través de Webhook entrante o Office 365 Connector. Para obtener más información, vea [Create and send messages](~/webhooks-and-connectors/how-to/connectors-using.md).

> [!NOTE]
> En Teams, seleccione **Configuración** Permisos de miembro Permitir a los miembros crear, actualizar y quitar conectores, de modo que cualquier miembro del equipo pueda agregar, modificar o eliminar  >    >  un conector.

## <a name="remove-incoming-webhook"></a>Quitar webhook entrante

**Para quitar un webhook entrante de un canal Teams entrada**

1. Vaya al canal.
1. Seleccione &#8226;&#8226;&#8226; **más opciones en** la barra de navegación superior.
1. Seleccione **Conectores en** el menú desplegable.
1. A la izquierda, en **Administrar**, seleccione **Configurado**.
1. Seleccione el **< *1*> configurado para** ver una lista de los conectores actuales:

    ![Webhook configurado](~/assets/images/configured.png)

1. Seleccione **Administrar** junto al conector que desea quitar:

    ![Administrar webhook](~/assets/images/manage.png)

1. Seleccione **Quitar**:

    ![Quitar webhook](~/assets/images/remove.png)

    Aparece **el cuadro de diálogo** Quitar configuración:

    ![Quitar configuración](~/assets/images/removeconfiguration.png)

1. Complete los campos y casillas del cuadro de diálogo y seleccione **Quitar**:

    ![Eliminación final](~/assets/images/finalremove.png)

    El webhook se quita del Teams canal.

## <a name="see-also"></a>Vea también

* [Crear un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Crear un botón Compartir en Teams](../../concepts/build-and-test/share-to-teams.md#create-share-to-teams-button)
* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
