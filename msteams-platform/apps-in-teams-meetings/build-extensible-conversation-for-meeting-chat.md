---
title: Creación de una conversación extensible para el chat de reuniones
author: v-sdhakshina
description: En este artículo, aprenderá a crear conversaciones extensibles para el chat de reuniones de Microsoft Teams con bots, tarjetas y extensiones de mensajes.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: 65fc91d51cd4c740f28d5f33a2ad578f214c20a8
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615496"
---
# <a name="build-extensible-conversation-for-meeting-chat"></a>Creación de una conversación extensible para el chat de reuniones

Puede hacer que las conversaciones sean extensibles en las reuniones de Microsoft Teams. Los bots, las extensiones de mensajes, las tarjetas y los módulos de tareas se pueden combinar para ofrecer una experiencia intuitiva.

## <a name="bots"></a>Bots

Un bot también se conoce como bot de chat o bot de conversación. Se trata de una aplicación que ejecuta tareas sencillas y repetitivas por parte de usuarios como el servicio de atención al cliente o el personal de soporte técnico. Los bots se usan a diario para, por ejemplo, proporcionar información sobre el tiempo, reservar cenas o facilitar información sobre viajes. Las interacciones con bots pueden ser preguntas y respuestas rápidas o conversaciones complejas. Es necesario habilitar un bot en el `team` ámbito de una reunión de canal y el `groupchat` ámbito de todos los demás tipos de reunión. Para implementar bots, comience con [Compilación de un bot](/microsoftteams/platform//sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode).

### <a name="bot-apis"></a>Las API del bot

El [Bot Framework](https://dev.botframework.com/) es un SDK enriquecido que se usa para crear bots mediante C#, Java, Python y JavaScript. Si tiene un bot basado en el Bot Framework, puede modificarlo para que funcione en Teams. Microsoft le recomienda usar C# o Node.js para aprovechar nuestros [SDK](/microsoftteams/platform/).

### <a name="code-samples---bots"></a>Ejemplos de código: bots

|Ejemplo de nombre | Descripción | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|
| Bot de conversación de Teams | Control de eventos de mensajería y conversación | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |
|Ejemplos de bot | Conjunto de ejemplos de bots  | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python) |

## <a name="message-extensions"></a>Extensiones de mensajería

Las extensiones de mensaje permiten a los usuarios interactuar con el servicio web a través de botones y formularios en el cliente de Teams. Los usuarios pueden buscar o iniciar acciones en un sistema externo desde el área del mensaje de redacción, el cuadro de comandos o directamente desde un mensaje. Puede devolver los resultados de esa interacción al cliente de Teams en forma de una tarjeta con formato enriquecido. La implementación de extensiones de mensaje para chats de reunión no es diferente de los chats normales. Para implementar la extensión de mensaje, comience con [Extensiones de mensaje](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions?tabs=dotnet).

## <a name="cards-and-task-modules"></a>Tarjetas y módulos de tareas

Las tarjetas proporcionan a los usuarios varios mensajes visuales, de audio y seleccionables y además ayudan con el flujo a de la conversación. Con los módulos de tareas, puede crear experiencias emergentes modales en Teams. Son especialmente útiles para iniciar y completar tareas o mostrar información completa, como vídeos o paneles de Power BI (inteligencia empresarial). Para obtener más información, consulte [Creación de tarjetas y módulos de tareas](/microsoftteams/platform/task-modules-and-cards/cards-and-task-modules).

## <a name="feature-compatibility-by-user-types"></a>Compatibilidad de características por tipos de usuario

En la tabla siguiente se proporcionan los tipos de usuario y se enumeran las características a las que cada usuario puede acceder en las reuniones:

| Tipo de usuario | Bots | Extensiones de mensajería | Tarjetas adaptables | Módulos de tareas |
| :-- | :-- | :-- | :-- | :-- |
| Usuario en el inquilino | Disponible | Disponible | Disponible | Disponible |
| Invitado, parte del inquilino de Azure AD | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde la tarjeta adaptable. |
| Para obtener más información, consulte [Usuarios no estándar](/microsoftteams/non-standard-users). | Se permite la interacción. No se permiten adquirir, actualizar y eliminar. | No disponible | Se permiten interacciones en el chat de reunión. | Se permiten interacciones en el chat de reunión desde la tarjeta adaptable. |
| Usuario anónimo | No disponible | No disponible | Se permiten interacciones en el chat de reunión. | No disponible |

## <a name="see-also"></a>Vea también

* [Diseñe su extensión de mensajería de Microsoft Teams](../messaging-extensions/design/messaging-extension-design.md)
* [Diseño de módulos de tareas para la aplicación de Microsoft Teams](../task-modules-and-cards/task-modules/design-teams-task-modules.md)
