---
title: Crear aplicaciones para la plataforma de Microsoft Teams
author: heath-hamilton
description: Obtenga información general sobre cómo los desarrolladores pueden ampliar las características de Microsoft Teams con aplicaciones personalizadas.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: b4f5d5fa3014d2acc5e4178a89c84ddb5a250132
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596213"
---
# <a name="build-apps-for-microsoft-teams"></a>Desarrollar aplicaciones para Microsoft Teams

Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza a los que cada vez más personas recopilan, aprenden y trabajan.

Las aplicaciones son la forma en que amplías Teams para que se ajusten a tus necesidades. Crea algo nuevo para Teams o integra una aplicación existente.

> [!div class="nextstepaction"]
> [Comenzar aquí](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>¿Qué son las aplicaciones de Teams?

Las aplicaciones de Teams son una combinación de [funcionalidades](concepts/capabilities-overview.md) [y puntos de entrada.](concepts/extensibility-points.md) Por ejemplo, los usuarios pueden chatear con el *bot* (funcionalidad) de la aplicación en un *canal* (punto de entrada).

Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (administrar registros de pacientes). Al planear la aplicación, recuerda que Teams es un centro de colaboración. Las mejores aplicaciones de Teams ayudan a las personas a expresarse y a trabajar mejor juntos.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Pestañas

**Obtenga información más cómodamente:** a veces solo necesita facilitar la búsqueda. Muestra una página web importante en una [pestaña,](tabs/what-are-tabs.md)que proporciona una experiencia web a pantalla completa para contenido estático y dinámico en Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Representación conceptual de cómo son las pestañas en el cliente de Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>Bots

**Convertir palabras en acciones:** las conversaciones a menudo resultan en la necesidad de hacer algo (generar un pedido, revisar mi código, comprobar el estado del vale, etc.). Un [bot](bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo dentro de Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Representación conceptual de cómo son los bots en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Extensiones de mensajería

**Facilita la multitarea:** con extensiones [de mensajería,](messaging-extensions/what-are-messaging-extensions.md)puedes compartir rápidamente información externa en una conversación. También puede actuar en un mensaje, como crear un vale de ayuda basado en el contenido de una publicación de canal.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Representación conceptual de cómo son las extensiones de mensajería en el cliente de Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhooks

**Comunicarse con aplicaciones externas:** [los webhooks entrantes](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar automáticamente notificaciones desde otra aplicación a un canal de Teams. Con [webhooks salientes,](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envía un mensaje al servicio web con un @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Representación conceptual de cómo son los conectores en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph para Teams

**Usar datos de Teams:** la API de [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview) para Teams proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar las características de la aplicación.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>Iniciar la creación

Familiarícese rápidamente con la creación de Teams configurando su entorno y creando una aplicación sencilla.

> [!div class="nextstepaction"]
> [Compilar una aplicación por primera vez](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Integración con Teams

Combina las características que a los usuarios les gusta acerca de una aplicación web, un servicio o un sistema existentes con las características de colaboración de Teams.

> [!div class="nextstepaction"]
> [Integrar una aplicación existente](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Un poco de código va mucho más allá

No es necesario ser un programador experto para crear una gran aplicación de Teams. Pruebe una de varias soluciones de código bajo.

> [!div class="nextstepaction"]
> [Crear una aplicación de código bajo](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>Obtener ideas para tu aplicación

¿Está buscando inspiración para el desarrollo de aplicaciones? Explore nuestra lista de escenarios reales y soluciones del sector con simulacros de concepto de alta fidelidad para comprender las distintas formas en que las aplicaciones de Teams pueden ayudar a los usuarios.

> [!div class="nextstepaction"]
> [Ver escenarios de aplicaciones](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>Ver también

* [Agregar un botón Compartir a Teams a su sitio web](concepts/build-and-test/share-to-teams.md)
* [Diseñar la aplicación de Teams](concepts/design/design-teams-app-overview.md)
* [SDK de cliente de JavaScript de Microsoft Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* Sdk de Bot Framework para [JavaScript](https://github.com/Microsoft/botbuilder-js) y [.NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Publicar la aplicación de Teams](concepts/deploy-and-publish/overview.md)
