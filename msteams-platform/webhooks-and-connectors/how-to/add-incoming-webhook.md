---
title: Crear un webhook entrante
author: laujan
description: En este módulo, aprenderá a agregar Webhook entrante a la aplicación de Teams y a publicar las solicitudes externas a Teams para usarlo
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ade5d5f30261cfd77140ab3cc9332bba15c76be8
ms.sourcegitcommit: 5c12af6a379c7cace409fda94677ea0334d7a3dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2022
ms.locfileid: "67337141"
---
# <a name="create-incoming-webhooks"></a>Crear webhooks entrantes

Un Webhook entrante permite a las aplicaciones externas compartir contenido en los canales de Microsoft Teams. Los webhooks se utilizan como herramientas de seguimiento y notificación. Los webhooks proporcionan una URL única, para enviar una carga útil JSON con un mensaje en formato de tarjeta. Las tarjetas son contenedores de interfaz de usuario que incluyen contenido y acciones relacionadas con un solo tema. Puede usar las tarjetas en las siguientes funciones:

* Bots
* Extensiones de mensajería
* Conectores

Vea el siguiente vídeo para obtener información sobre cómo crear un webhook entrante:
<br>
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4ODcY]

## <a name="key-features-of-an-incoming-webhook"></a>Características principales de un Webhook entrante

La siguiente tabla proporciona las características y la descripción de un Webhook entrante:

| Características | Descripción |
| -------- | ----------- |
|Tarjetas adaptables mediante un Webhook entrante | Las tarjetas adaptables se pueden enviar a través de webhooks entrantes. Para obtener más información, vea [Enviar tarjetas adaptables mediante webhooks entrantes.](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)|
|Compatibilidad con mensajería accionable|Las tarjetas de mensaje que pueden actuar se admiten en todos los grupos de Office 365, incluido Teams. Si envía mensajes a través de tarjetas, debe usar el formato de tarjeta de mensaje accionable. Para obtener más información, vea [ referencia de tarjeta de mensaje accionable heredada](/outlook/actionable-messages/message-card-reference) y [área de juegos de tarjetas de mensajes](https://messagecardplayground.azurewebsites.net).|
|Compatibilidad con mensajería HTTPS independiente|Las tarjetas proporcionan información de forma clara y coherente. Cualquier herramienta o marco que pueda enviar solicitudes HTTPS POST puede enviar mensajes a Teams a través de un Webhook entrante.|
|Compatibilidad con Markdown|Todos los campos de texto de las tarjetas de mensajería accionables admiten Markdown básico. No use el marcado HTML en las tarjetas. puesto que se omite y se trata como texto sin formato.|
|Configuración con ámbito|El webhook entrante tiene como ámbito y se configura en el nivel de canal.|
|Protección de definiciones de recursos|Los mensajes tienen formato de cargas JSON. Esta estructura de mensajería declarativa impide la inserción de código malintencionado.|

<!--- TBD: A note should be short and eye-catching. No need to put a list item inside a Note or any admonition for that matter. Re-write the below list item.
--->

> [!NOTE]
>
> * Los bots de Teams, las extensiones de mensajería, el Webhook entrante y el soporte de Bot Framework admiten Tarjetas adaptables. Las Tarjetas adaptables son un marco abierto de plataforma de tarjetas cruzadas que se utiliza en todas las plataformas como Windows, Android, iOS, etc. Actualmente, los [conectores de Teams](../../webhooks-and-connectors/how-to/connectors-creating.md) no admiten Tarjetas adaptables. Sin embargo, es posible crear un [flujo](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) que publique Tarjetas adaptables en un canal de Teams.
> * Para obtener más información sobre tarjetas y webhooks, vea [tarjetas adaptables y Webhooks entrantes](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks).

## <a name="create-an-incoming-webhook"></a>Crear un webhook entrante

Para agregar un Webhook entrante a un canal de Teams, siga estos pasos:

1. Abra el canal en el que desea agregar el webhook y seleccione &#8226;&#8226;&#8226; **Más opciones** en la barra de navegación superior.
1. Seleccione **Conectores** en el menú desplegable:

    ![Seleccionar conector](~/assets/images/connectors.png)

1. Busque **Webhook entrante** y seleccione **Agregar**.
1. Seleccione **Configurar**, proporcione un nombre y cargue una imagen para su webhook si es necesario:

    ![Botón Configurar](~/assets/images/configure.png)

1. Copie y guarde la URL única del webhook presente en la ventana de diálogo. La URL se asigna al canal y se puede utilizar para enviar información a los equipos. Seleccione **Listo**.

    ![Dirección URL única](~/assets/images/url.png)

El webhook está disponible en el canal de Teams.

Puede crear y enviar mensajes accionables a través del Webhook entrante o el Conector de Office 365. Para obtener más información, vea [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md).

> [!NOTE]
> En Teams, seleccione **Configuración** > **Permisos de miembro** > **Permitir a los miembros crear, actualizar y quitar conectores**, de modo que cualquier miembro del equipo pueda agregar, modificar o eliminar un conector.

## <a name="remove-an-incoming-webhook"></a>Eliminar un Webhook entrante

Para eliminar un Webhook entrante de un canal de Teams, siga estos pasos:

1. Abra el canal y seleccione &#8226;&#8226;&#8226; **Más opciones** en la barra de navegación superior.
1. Seleccione **Conectores** en el menú desplegable.
1. Seleccione **Configurado** en **Administrar**.
1. Seleccione el **<*1*> Configurado** para ver una lista de los conectores actuales:

    ![Webhook configurado](~/assets/images/configured.png)

1. Seleccione **Administrar** para el conector que desea eliminar:

    ![Administrar webhook](~/assets/images/manage.png)

1. Seleccione **Eliminar** para ver el cuadro de diálogo **Eliminar configuración**.

    ![Quitar Configuración](~/assets/images/removeconfiguration.png)

1. Complete los campos del cuadro de diálogo y las casillas de verificación y seleccione **Eliminar**.

    ![Quitar final](~/assets/images/finalremove.png)

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre           | Descripción | C#    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Webhook entrante|Este código de ejemplo muestra cómo enviar una tarjeta mediante el webhook entrante. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/incoming-webhook/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/incoming-webhook/nodejs) |

## <a name="see-also"></a>Consulte también

* [Crear un Webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Compartir en Teams desde aplicaciones web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Acceso y datos seguros en Azure Logic Apps](/azure/logic-apps/logic-apps-securing-a-logic-app)
* [Crear un bot de notificaciones con JavaScript](../../sbs-gs-notificationbot.yml)
* [Cree su primera aplicación de bot con JavaScript](../../sbs-gs-bot.yml)
