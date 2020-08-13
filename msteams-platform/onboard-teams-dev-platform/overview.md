---
title: Plataforma para desarrolladores de Microsoft Teams
author: clearab
description: Información general sobre cómo los desarrolladores pueden ampliar y personalizar las características de Microsoft Teams con la plataforma de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d127acb33212f23dff9cf0dd83a1936044c10d5e
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652180"
---
# <a name="building-for-microsoft-teams"></a>Creación para Microsoft Teams

Las aplicaciones de Microsoft Teams aportan información clave, herramientas comunes y procesos de confianza a los que los usuarios recopilan, aprenden y funcionan cada vez más.

Las aplicaciones son cómo extender Teams para ajustarse a sus necesidades. Puede crear elementos nuevos para Microsoft Teams o simplemente integrar características en sus aplicaciones y servicios favoritos.

## <a name="what-can-teams-apps-do"></a>¿Qué pueden hacer las aplicaciones de Microsoft Teams?

Las personas descubren y usan las aplicaciones de Microsoft Teams a través de un conjunto de [capacidades](capabilities-overview.md)de plataforma.

Algunas aplicaciones son sencillas (enviar notificaciones), mientras que otras son complejas (Ver registros de pacientes). Al planear la aplicación, recuerde que Teams es un centro de colaboración. Las mejores aplicaciones de Team ayudan a los usuarios a expresarse y a trabajar mejor juntos.

### <a name="get-information-more-conveniently"></a>Obtener información más fácilmente

A veces solo necesita que las cosas sean más fáciles de encontrar. Mostrar una página web importante en una [pestaña](doc-links/what-are-tabs.md), que proporciona una experiencia web de pantalla completa para contenido estático y dinámico en Microsoft Teams.

![Representación conceptual de las fichas que se ven en el cliente de Microsoft Teams.](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a>Compartir vínculos sin conmutar contexto

Extraiga la información en una conversación y no deje nunca los equipos. Por ejemplo, con las [extensiones de mensajería](doc-links/what-are-messaging-extensions.md) puede compartir contenido enriquecido y fácilmente digestible desde un sistema externo mediante el cuadro de redacción del mensaje.

![Representación conceptual de las extensiones de mensajería que tienen el mismo aspecto en el cliente de Microsoft Teams](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a>Convertir palabras en acciones

Con frecuencia, las conversaciones tienen como resultado la necesidad de hacer algo (crear un pedido, revisar el código, etc.). Un [Bot](doc-links/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo dentro de Teams.

![Representación conceptual de los bots que tienen el mismo aspecto en el cliente de Microsoft Teams](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a>Comunicarse con los servicios y las aplicaciones externas

Los [webhooks entrantes](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) son una forma sencilla de enviar automáticamente alertas desde otra aplicación a un canal o chat de Microsoft Teams. Con los [webhooks salientes](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), puede enviar un mensaje al servicio Web con un @mention.

![Representación conceptual de los conectores que se asemejan en el cliente de Microsoft Teams.](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a>Uso de los datos de Teams

La [API de REST de Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar características para la aplicación.

!["Representación conceptual de la API de REST de Microsoft Graph para Teams](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a>Empezar a crear

   Familiarícese rápidamente con la creación de Teams creando una aplicación sencilla y agregando un par de capacidades de uso frecuente.

   > [!div class="nextstepaction"]
   > [Compilar la primera aplicación ahora](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a>Unir todo

   Simplificar los procesos y flujos de trabajo para los usuarios al combinar las aplicaciones Web, servicios y sistemas favoritos de su organización con las características de colaboración de Teams.

   > [!div class="nextstepaction"]
   > [Integrar una aplicación existente](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a>Confiar en el proceso

   Comprenda todo el proceso de desarrollo de la plataforma de Teams para planear, diseñar, crear y publicar una aplicación para su organización o cualquier persona de manera eficaz.

   > [!div class="nextstepaction"]
   > [Empezar a planear la aplicación](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a>Sin código, sin preocupaciones

   No es necesario ser programador para crear una aplicación fantástica. Cree una aplicación de Microsoft Teams con poco o ningún código usando la plataforma de energía de Microsoft.

   > [!div class="nextstepaction"]
   > [Importar una aplicación de Power Platform](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a>Recursos

* [Agregar un recurso compartido a Microsoft Teams en el sitio web](doc-links/share-to-teams.md)
* [Diseñar la aplicación con las instrucciones recomendadas](doc-links/designing-overview.md)
* [Sistema de diseño de interfaz de usuario Fluent](https://fluentsite.z22.web.core.windows.net/)
* [SDK de cliente de JavaScript de Microsoft Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* [Bot Framework SDK para JavaScript](https://github.com/Microsoft/botbuilder-js) y [Bot Framework SDK para .net](https://github.com/Microsoft/botbuilder-dotnet/)
