---
title: Crear aplicaciones para la plataforma Microsoft Teams
author: heath-hamilton
description: Obtenga información general sobre cómo pueden ampliar los desarrolladores las características de Microsoft Teams con aplicaciones personalizadas.
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 1a7957c8ea6d889ffe5ab7e40c8a5bb1377b6ca5
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059626"
---
# <a name="build-apps-for-microsoft-teams"></a>Desarrollar aplicaciones para Microsoft Teams

Las aplicaciones de Microsoft Teams aportan información importante, herramientas comunes y procesos de confianza con los que las personas se reúnen, aprenden y trabajan cada vez más.

Las aplicaciones son una forma de expandir Teams para adaptarlo a sus necesidades. Cree algo totalmente nuevo para Teams o integre una aplicación existente.

> [!div class="nextstepaction"]
> [Comenzar aquí](get-started/get-started-overview.md)

## <a name="what-are-teams-apps"></a>¿Qué son las aplicaciones de Teams?

Las aplicaciones de Teams son una combinación de [funcionalidades](concepts/capabilities-overview.md). Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (administrar registros de pacientes). Al planear la aplicación, recuerde que Teams es un centro de colaboración. Las mejores aplicaciones de Teams ayudan a los usuarios a expresarse y a trabajar mejor juntos.

### <a name="personal-apps"></a>Aplicaciones personales

:::row:::
   :::column span="1":::

**Ayudar a los usuarios a concentrarse**: una [aplicación personal](concepts/design/personal-apps.md) es un espacio o bot dedicado a ayudar a los usuarios a concentrarse en sus propias tareas o ver actividades importantes para ellos.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="Representación conceptual de cómo son las aplicaciones personales en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a>Pestañas

:::row:::
   :::column span="1":::

**Colaborar de forma más cómoda**: muestre el contenido basado en web en una [pestaña](tabs/what-are-tabs.md) donde los usuarios puedan analizarlo y trabajar en él juntos.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="Representación conceptual de cómo son las pestañas en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a>Bots

:::row:::
   :::column span="1":::

**Convertir palabras en acciones**: las conversaciones suelen dar lugar a la necesidad de hacer algo (generar un pedido, revisar mi código, comprobar el estado de la incidencia, etc). Un [bot](bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo directamente dentro de Teams.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="Representación conceptual de cómo son los bots en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a>Extensiones de mensajería

:::row:::

   :::column span="1":::

**Facilita la multitarea**: con las [extensiones de mensajería](messaging-extensions/what-are-messaging-extensions.md), puede compartir rápidamente información externa en una conversación. También puede actuar sobre un mensaje, como crear una incidencia de ayuda basada en el contenido de una publicación del canal.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="Representación conceptual de cómo son las extensiones de mensajería en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a>Extensiones de reunión

:::row:::

   :::column span="1":::

**Crear aplicaciones para reuniones**: hay algunas opciones para [incorporar la aplicación a la experiencia de llamada de Teams](apps-in-teams-meetings/design/designing-apps-in-meetings.md).

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="Representación conceptual de cómo son las extensiones de reunión en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a>Webhooks y conectores

:::row:::

   :::column span="":::

**Comunicarse con aplicaciones externas**: los [webhooks entrantes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una manera sencilla de enviar automáticamente notificaciones desde otra aplicación a un canal de Teams. Con los [webhooks salientes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), envíe un mensaje al servicio web con un @mention.

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Representación conceptual de cómo son los conectores en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph para Teams

:::row:::

   :::column span="":::

**Usar datos de Teams**: la [API de Microsoft Graph para Teams](/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar las características de la aplicación (como notificaciones enriquecdas).

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>Empezar a compilar

Familiarícese rápidamente con la compilación de Teams mediante la configuración del entorno y la creación de una aplicación sencilla.

> [!div class="nextstepaction"]
> [Compilar una aplicación por primera vez](get-started/get-started-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Integración con Teams

Combine las características que a los usuarios les gustan de una aplicación web, un servicio o un sistema existentes con las características de colaboración de Teams.

> [!div class="nextstepaction"]
> [Integrar una aplicación existente](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Con un poco de código se va muy lejos

No es necesario ser un programador experto para crear una aplicación excelente de Teams. Pruebe una de varias soluciones con poco código.

> [!div class="nextstepaction"]
> [Crear una aplicación con poco código](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>Obtener ideas para su aplicación

¿Busca inspiración para el desarrollo de aplicaciones? Explore nuestra lista de escenarios reales y soluciones del sector con conceptos ficticios de alta fidelidad para comprender las distintas formas en que las aplicaciones de Teams pueden ayudar a los usuarios.

> [!div class="nextstepaction"]
> [Ver escenarios de aplicaciones](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="test-your-app-running-across-microsoft-365"></a>Prueba de ejecución de la aplicación en Microsoft 365

Puede obtener una vista previa de las aplicaciones de Teams que se ejecutan en otras experiencias de Microsoft 365 de uso elevado con la versión preliminar del SDK de cliente de JavaScript v2 de Microsoft Teams.

> [!div class="nextstepaction"]
> [Ampliar la aplicación](m365-apps/overview.md)

## <a name="see-also"></a>Vea también

* [Conceptos básicos de aplicación](~/concepts/app-fundamentals-overview.md)
* [Diseñar la aplicación de Teams](~/concepts/design/design-teams-app-process.md)
* [Asignar los casos de uso a las funcionalidades de la aplicación de Teams](~/concepts/design/map-use-cases.md)
