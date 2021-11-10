---
title: Controladores de actividad de bots
author: surbhigupta
description: Comprender los controladores de actividad del bot en Teams.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: Evento del canal de consentimiento de tarjeta de bot del controlador de actividades
ms.openlocfilehash: 6350d9f0e280f345780eeac277e334fef867a67f
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889135"
---
# <a name="bot-activity-handlers"></a>Controladores de actividad de bots

Este documento se basa en el artículo sobre cómo funcionan los [bots](https://aka.ms/how-bots-work) en la documentación básica [de Bot Framework](https://aka.ms/azure-bot-service-docs). La diferencia principal entre los bots desarrollados para Microsoft Teams y el bot framework principal se encuentra en las características que se proporcionan en Teams.

Para organizar la lógica de conversación del bot, se usa un controlador de actividades. Las actividades se controlan de dos maneras mediante Teams de actividad y lógica de bot. El controlador Teams de actividad agrega compatibilidad para Microsoft Teams eventos e interacciones específicos. El objeto bot contiene el razonamiento de conversación o la lógica de un turno y expone un controlador de turnos, que es el método que puede aceptar actividades entrantes del adaptador del bot.

## <a name="teams-activity-handlers"></a>Teams de actividad

Teams controlador de actividad se deriva del controlador de actividades de Microsoft Bot Framework. Enruta todas las Teams antes de permitir que se controle cualquier actividad que no Teams específicas.

Cuando un bot para Teams recibe una actividad, se enruta a los controladores de actividad. Todas las actividades se enrutan a través de un controlador base denominado controlador de turnos. El controlador de turnos llama al controlador de actividad necesario para administrar cualquier actividad recibida. El Teams bot se deriva de la clase, que se deriva de la clase `TeamsActivityHandler` de Bot `ActivityHandler` Framework.

# <a name="c"></a>[C#](#tab/csharp)

Los bots se crean con Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turnos recibe una notificación de esa actividad entrante. A continuación, el controlador de turnos envía la actividad entrante al `OnMessageActivityAsync` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turnos recibe una notificación de esa actividad entrante y envía la actividad entrante a `OnConversationUpdateActivityAsync` . El Teams de actividad comprueba primero si hay Teams eventos específicos. Si no se encuentra ningún evento, los pasa al controlador de actividad de Bot Framework.

En la Teams controlador de actividad, hay dos controladores de Teams principales y `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` . `OnConversationUpdateActivityAsync`enruta todas las actividades de actualización de conversación y `OnInvokeActivityAsync` enruta todas Teams invocar actividades.

Para implementar la lógica Teams controladores de actividad específicos, debe invalidar los métodos del bot como se muestra en la [sección lógica del](#bot-logic) bot. No hay ninguna implementación base para estos controladores, por lo tanto, debe agregar la lógica que desee en su invalidación.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Los bots se crean con Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turnos recibe una notificación de esa actividad entrante. A continuación, el controlador de turnos envía la actividad entrante al `onMessage` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turnos recibe una notificación de esa actividad entrante y envía la actividad entrante a `dispatchConversationUpdateActivity` . El Teams de actividad comprueba primero si hay Teams eventos específicos. Si no se encuentra ningún evento, los pasa al controlador de actividad de Bot Framework.

En la Teams controlador de actividad, hay dos controladores de Teams principales y `dispatchConversationUpdateActivity` `onInvokeActivity` . `dispatchConversationUpdateActivity`enruta todas las actividades de actualización de conversación y `onInvokeActivity` enruta todas Teams invocar actividades.

Para implementar la lógica Teams controladores de actividad específicos, debe invalidar los métodos del bot como se muestra en la [sección lógica del](#bot-logic) bot. Defina la lógica del bot para estos controladores y, a continuación, asegúrese de llamar `next()` al final. Al `next()` llamar, asegúrese de que se ejecute el siguiente controlador.

# <a name="python"></a>[Python](#tab/python)

Los bots se crean con Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turnos recibe una notificación de esa actividad entrante. A continuación, el controlador de turnos envía la actividad entrante al `on_message_activity` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turnos recibe una notificación de esa actividad entrante y envía la actividad entrante a `on_conversation_update_activity` . El Teams de actividad comprueba primero si hay Teams eventos específicos. Si no se encuentra ningún evento, los pasa al controlador de actividad de Bot Framework.

En la Teams controlador de actividad, hay dos controladores de Teams principales y `on_conversation_update_activity` `on_invoke_activity` . `on_conversation_update_activity`enruta todas las actividades de actualización de conversación y `on_invoke_activity` enruta todas Teams invocar actividades.

Para implementar la lógica Teams controladores de actividad específicos, debe invalidar los métodos del bot como se muestra en la [sección lógica del](#bot-logic) bot. No hay ninguna implementación base para estos controladores, por lo tanto, debe agregar la lógica que desee en su invalidación.

---

## <a name="bot-logic"></a>Lógica del bot

La lógica del bot procesa las actividades entrantes de uno o más canales de bot y, en respuesta, genera actividades salientes. Esto sigue siendo así con los bots derivados de la clase de controlador de Teams de actividad, que primero comprueba si hay Teams actividades. Después de comprobar si Teams actividades, pasa todas las demás actividades al controlador de actividades de Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Controladores de Core Bot Framework

>[!NOTE]
> Excepto para las  **actividades de** los miembros agregados y quitados, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no Teams usuario.

Los controladores de actividad son diferentes en el contexto de un equipo, donde se agrega un nuevo miembro al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos en `ActivityHandler` incluye lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibida | `OnTurnAsync` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensajes recibida | `OnMessageActivityAsync` | Este método se puede invalidar para controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `OnConversationUpdateActivityAsync` | Este método llama a un controlador si miembros distintos del bot se unieron o dejaron la conversación en una `ConversationUpdate` actividad. |
| Miembros que no son bots se unieron a la conversación | `OnMembersAddedAsync` | Este método se puede invalidar para controlar los miembros que se unen a una conversación. |
| Los miembros que no son bots dejaron la conversación | `OnMembersRemovedAsync` | Este método se puede invalidar para controlar los miembros que dejan una conversación. |
| Actividad de evento recibida | `OnEventActivityAsync` | Este método llama a un controlador específico del tipo de evento, en una `Event` actividad. |
| Actividad de evento de respuesta de token recibida | `OnTokenResponseEventAsync` | Este método se puede invalidar para controlar eventos de respuesta de token. |
| Actividad de evento que no es de token-response recibida | `OnEventAsync` | Este método se puede invalidar para controlar otros tipos de eventos. |
| Otro tipo de actividad recibida | `OnUnrecognizedActivityTypeAsync` | Este método se puede invalidar para controlar cualquier tipo de actividad que no se controle. |

#### <a name="teams-specific-activity-handlers"></a>Teams controladores de actividad específicos

Amplía la lista de controladores de la sección de controladores `TeamsActivityHandler` principales de Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Este método se puede invalidar para controlar un canal Teams que se está creando. Para obtener más información, vea [channel created](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) in conversation [update events](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Este método se puede invalidar para controlar un canal Teams que se va a eliminar. Para obtener más información, vea [channel deleted](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) in conversation [update events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Este método se puede invalidar para controlar un canal Teams que se va a cambiar el nombre. Para obtener más información, vea [channel renamed](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) in [conversation update events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Este método se puede invalidar para controlar un Teams equipo que se va a cambiar el nombre. Para obtener más información, vea [team renamed](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) in [conversation update events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar los miembros que se unen a un equipo. Para obtener más información, vea [miembros del equipo agregados en](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar los miembros que salen de un equipo. Para obtener más información, consulta [Miembros del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en eventos [de actualización de conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Teams invocar actividades

La lista de Teams controladores de actividad llamados desde `OnInvokeActivityAsync` el Teams de actividad incluyen lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Este método se invoca cuando se recibe una actividad de acción de tarjeta de conector O365 desde el conector. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Este método se invoca cuando se recibe una actividad de estado signIn verify desde el conector. |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tareas. |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación enumeradas en esta sección son para bots de conversación en Teams. El SDK de Bot Framework también admite invocar actividades específicas de extensiones de mensajería. Para obtener más información, [vea what are messaging extensions](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Controladores de Core Bot Framework

>[!NOTE]
> Excepto para las  **actividades de** los miembros agregados y quitados, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no Teams usuario.

Los controladores de actividad son diferentes en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos en `ActivityHandler` incluye lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibida | `onTurn` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensajes recibida | `onMessage` | Este método ayuda a controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `onConversationUpdate` | Este método llama a un controlador si miembros distintos del bot se unieron o dejaron la conversación en una `ConversationUpdate` actividad. |
| Miembros que no son bots se unieron a la conversación | `onMembersAdded` | Este método ayuda a controlar los miembros que se unen a una conversación. |
| Los miembros que no son bots dejaron la conversación | `onMembersRemoved` | Este método ayuda a controlar los miembros que dejan una conversación. |
| Actividad de evento recibida | `onEvent` | Este método llama a un controlador específico del tipo de evento, en una `Event` actividad. |
| Actividad de evento de respuesta de token recibida | `onTokenResponseEvent` | Este método ayuda a controlar eventos de respuesta de token. |
| Otro tipo de actividad recibida | `onUnrecognizedActivityType` | Este método ayuda a controlar cualquier tipo de actividad que no se controle. |

#### <a name="teams-specific-activity-handlers"></a>Teams controladores de actividad específicos

Amplía la lista de controladores de la sección de controladores `TeamsActivityHandler` principales de Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Este método se puede invalidar para controlar un canal Teams que se está creando. Para obtener más información, vea [channel created](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) in conversation [update events](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Este método se puede invalidar para controlar un canal Teams que se va a eliminar. Para obtener más información, vea [channel deleted](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) in conversation [update events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Este método se puede invalidar para controlar un canal Teams que se va a cambiar el nombre. Para obtener más información, vea [channel renamed](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) in [conversation update events](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Este método se puede invalidar para controlar un Teams equipo que se va a cambiar el nombre. Para obtener más información, vea [team renamed](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) in [conversation update events](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar los miembros que se unen a un equipo. Para obtener más información, vea [miembros del equipo agregados en](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar los miembros que salen de un equipo. Para obtener más información, consulta [Miembros del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en eventos [de actualización de conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |

#### <a name="teams-invoke-activities"></a>Teams invocar actividades

La lista de Teams controladores de actividad llamados desde `onInvokeActivity` el Teams de actividad incluyen lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Este método se invoca cuando se recibe una actividad de acción de tarjeta de conector O365 desde el conector. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Este método se invoca cuando se recibe una actividad de estado signIn verify desde el conector. |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tareas. |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación enumeradas en esta sección son para bots de conversación en Teams. El SDK de Bot Framework también admite invocar actividades específicas de extensiones de mensajería. Para obtener más información, [vea what are messaging extensions](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Controladores de Core Bot Framework

>[!NOTE]
> Excepto para las  **actividades de** los miembros agregados y quitados, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no Teams usuario.

Los controladores de actividad son diferentes en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos en `ActivityHandler` incluye lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibida | `on_turn` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensajes recibida | `on_message_activity` | Este método se puede invalidar para controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `on_conversation_update_activity` | Este método llama a un controlador si miembros distintos del bot se unen o salen de la conversación. |
| Miembros que no son bots se unieron a la conversación | `on_members_added_activity` | Este método se puede invalidar para controlar los miembros que se unen a una conversación. |
| Los miembros que no son bots dejaron la conversación | `on_members_removed_activity` | Este método se puede invalidar para controlar los miembros que dejan una conversación. |
| Actividad de evento recibida | `on_event_activity` | Este método llama a un controlador específico del tipo de evento. |
| Actividad de evento de respuesta de token recibida | `on_token_response_event` | Este método se puede invalidar para controlar eventos de respuesta de token. |
| Actividad de evento que no es de token-response recibida | `on_event` | Este método se puede invalidar para controlar otros tipos de eventos. |
| Otros tipos de actividad recibidos | `on_unrecognized_activity_type` | Este método se puede invalidar para controlar cualquier tipo de actividad que no se controle. |

#### <a name="teams-specific-activity-handlers"></a>Teams controladores de actividad específicos

Amplía la lista de controladores de la sección de controladores `TeamsActivityHandler` principales de Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Este método se puede invalidar para controlar un canal Teams que se está creando. Para obtener más información, vea [channel created](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) in conversation [update events](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `on_teams_channel_deleted` | Este método se puede invalidar para controlar un canal Teams que se va a eliminar. Para obtener más información, vea [channel deleted](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) in conversation [update events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `on_teams_channel_renamed` | Este método se puede invalidar para controlar un canal Teams que se va a cambiar el nombre. Para obtener más información, vea [channel renamed](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) in [conversation update events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;`Este método se puede invalidar para controlar un Teams equipo que se va a cambiar el nombre. Para obtener más información, vea [team renamed](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) in [conversation update events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `on_teams_members_added` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar los miembros que se unen a un equipo. Para obtener más información, vea [miembros del equipo agregados en](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `on_teams_members_removed` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar los miembros que salen de un equipo. Para obtener más información, consulta [Miembros del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en eventos [de actualización de conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Teams invocar actividades

La lista de Teams controladores de actividad llamados desde `on_invoke_activity` el Teams de actividad incluyen lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `on_teams_file_consent`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Este método se invoca cuando se recibe una actividad de acción de tarjeta de conector O365 desde el conector. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Este método se invoca cuando se recibe una actividad de estado signIn verify desde el conector. |
| task/fetch                      | `on_teams_task_module_fetch`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tareas. |
| task/submit                     | `on_teams_task_module_submit`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación enumeradas en esta sección son para bots de conversación en Teams. El SDK de Bot Framework también admite invocar actividades específicas de extensiones de mensajería. Para obtener más información, [vea what are messaging extensions](https://aka.ms/azure-bot-what-are-messaging-extensions).

---

* * *

Ahora que ya se ha familiarizado con los controladores de actividad del bot, veamos cómo los bots se comportan de forma diferente en función de la conversación y los mensajes que recibe o envía.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Conceptos básicos de la conversación](~/bots/how-to/conversations/conversation-basics.md)
