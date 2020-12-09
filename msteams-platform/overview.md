---
title: Creación de aplicaciones para la plataforma de Microsoft Teams
author: heath-hamilton
description: Información general sobre cómo los desarrolladores pueden ampliar y personalizar las características de Microsoft Teams con aplicaciones personalizadas.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6f5f3454885320669ef42383529d39fcfcfdfee8
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604790"
---
# <a name="build-apps-for-microsoft-teams"></a>Desarrollar aplicaciones para Microsoft Teams

Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza a los que los usuarios recopilan, aprenden y funcionan cada vez más.

Las aplicaciones son cómo extender Teams para ajustarse a sus necesidades. Cree algo nuevo para Teams o integre una aplicación existente.

> [!div class="nextstepaction"]
> [Comenzar aquí](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>¿Qué son las aplicaciones de Microsoft Teams?

Las aplicaciones de Microsoft Teams son una combinación de [capacidades](concepts/capabilities-overview.md) y [puntos de entrada](concepts/extensibility-points.md). Por ejemplo, los usuarios pueden chatear con el *Bot* de la aplicación (funcionalidad) en un *canal* (punto de entrada).

Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (administrar registros de pacientes). Al planear la aplicación, recuerde que Teams es un centro de colaboración. Las mejores aplicaciones de Team ayudan a los usuarios a expresarse y a trabajar mejor juntos.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Pestañas

**Obtenga información más fácilmente**: a veces solo necesita que las cosas sean más fáciles de encontrar. Mostrar una página web importante en una [pestaña](tabs/what-are-tabs.md), que proporciona una experiencia web de pantalla completa para contenido estático y dinámico en Microsoft Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Representación conceptual de las fichas que se ven en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a>Extensiones de mensajería

**Simplificar la tarea** en varias tareas: con [las extensiones de mensajería](messaging-extensions/what-are-messaging-extensions.md), puede compartir rápidamente información externa en una conversación. También puede actuar en un mensaje, como la creación de un vale de ayuda basado en el contenido de una publicación de canal.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Representación conceptual de las extensiones de mensajería que tienen el mismo aspecto en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>Bots

**Convertir las palabras en acciones**: las conversaciones suelen tener como resultado la necesidad de hacer algo (generar un pedido, revisar el código, comprobar el estado de los tíquets, etc.). Un [Bot](bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo dentro de Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Representación conceptual de qué bots se parecen en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a>Webhooks

**Comunicarse con aplicaciones externas**: los [webhooks entrantes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar notificaciones de forma automática desde otra aplicación a un canal de Teams. Con los [webhooks salientes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), mensaje el servicio Web con un @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Representación conceptual de los conectores que se asemejan en el cliente de Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph para Teams

**Usar datos de Teams**: la [API de Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar características para la aplicación.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a>Introducción

Vaya directamente con nuestros tutoriales de primera aplicación o descubra cómo integrar e importar aplicaciones existentes.

:::row:::
   :::column span="2":::

### <a name="start-building"></a>Empezar a crear

   Familiarícese rápidamente con la creación de Teams creando una aplicación sencilla y agregando algunas funcionalidades que se usan con más frecuencia.

   > [!div class="nextstepaction"]
   > [Compilar la primera aplicación ahora](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a>Integración con Microsoft Teams

   Fusione las características que los usuarios adoran de una aplicación Web, servicio o sistema existente con las características de colaboración de Microsoft Teams.

   > [!div class="nextstepaction"]
   > [Integrar una aplicación existente](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a>Un pequeño código va de un modo largo

   No es necesario ser un programador experto para crear una aplicación de Teams fantástica. Pruebe con una de las soluciones de bajo código.

   > [!div class="nextstepaction"]
   > [Crear una aplicación de código reducido](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a>Recursos

* [Agregar un recurso compartido a Microsoft Teams en el sitio web](concepts/build-and-test/share-to-teams.md)
* <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Interfaz de usuario Fluent</a>
* [SDK de cliente de JavaScript de Microsoft Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Bot Framework SDK para JavaScript](https://github.com/Microsoft/botbuilder-js) y [Bot Framework SDK para .net](https://github.com/Microsoft/botbuilder-dotnet/)
* [Publicar la aplicación en una organización o AppSource](concepts/deploy-and-publish/overview.md)
