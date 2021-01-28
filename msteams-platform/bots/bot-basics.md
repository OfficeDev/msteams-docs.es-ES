---
title: Conceptos básicos del bot
author: clearab
description: Comprenda los conceptos básicos de los bots en Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3c4e707fa4677c2441f348e8d09ecf4428ef1296
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014505"
---
# <a name="bot-basics"></a>Conceptos básicos del bot

En este documento se proporciona una introducción a los bots de Microsoft Teams que se basa en el artículo Cómo funcionan los [bots](https://aka.ms/how-bots-work) en la documentación básica de [Bot Framework.](https://aka.ms/azure-bot-service-docs) La principal diferencia entre los bots desarrollados para Microsoft Teams y el bot framework principal se encuentra en las características proporcionadas en Teams.

## <a name="teams-activity-handlers"></a>Controladores de actividad de Teams

El controlador de actividad de Teams se deriva del controlador de actividades de Microsoft Bot Framework. Enruta todas las actividades de Teams antes de permitir que se controle cualquier actividad que no sea específica de Teams.

Cuando un bot de Teams recibe una actividad, se dirige a los *controladores de actividad.* Todas las actividades se enrutar a través de un controlador base denominado *controlador de turno.* El *controlador de turno* llama al controlador de actividad necesario para administrar cualquier actividad recibida. El bot de Teams deriva de `TeamsActivityHandler` la clase, que se deriva de la clase de Bot `ActivityHandler` Framework.

# <a name="c"></a>[C#](#tab/csharp)

Los bots se crean con Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turno recibe una notificación de esa actividad entrante. A continuación, el controlador de turno envía la actividad entrante al `OnMessageActivityAsync` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turno recibe una notificación de esa actividad entrante y envía la actividad entrante a `OnConversationUpdateActivityAsync` . El controlador de actividades de Teams comprueba primero si hay eventos específicos de Teams. Si no se encuentra ningún evento, los pasa al controlador de actividades de Bot Framework.

En la clase de controlador de actividad de Teams, hay dos controladores de actividad de Teams principales y `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` . `OnConversationUpdateActivityAsync` enruta todas las actividades de actualización de conversaciones y `OnInvokeActivityAsync` enruta todas las actividades de invocación de Teams.

Para implementar la lógica para controladores de actividad específicos de Teams, debe invalidar los métodos del bot, como se muestra en la [sección lógica de bot.](#bot-logic) No hay ninguna implementación base para estos controladores, por lo tanto, debes agregar la lógica que quieras en la invalidación.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Los bots se crean con Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turno recibe una notificación de esa actividad entrante. A continuación, el controlador de turno envía la actividad entrante al `onMessage` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turno recibe una notificación de esa actividad entrante y envía la actividad entrante a `dispatchConversationUpdateActivity` . El controlador de actividades de Teams comprueba primero si hay eventos específicos de Teams. Si no se encuentra ningún evento, los pasa al controlador de actividades de Bot Framework.

En la clase de controlador de actividad de Teams, hay dos controladores de actividad de Teams principales `dispatchConversationUpdateActivity` y `onInvokeActivity` . `dispatchConversationUpdateActivity` enruta todas las actividades de actualización de conversaciones y `onInvokeActivity` enruta todas las actividades de invocación de Teams.

Para implementar la lógica para controladores de actividad específicos de Teams, debe invalidar los métodos del bot, como se muestra en la [sección lógica de bot.](#bot-logic) Defina la lógica del bot para estos controladores y, a continuación, asegúrese de **llamar `next()` al final.** Al llamar `next()` te aseguras de que se ejecuta el siguiente controlador.

# <a name="python"></a>[Python](#tab/python)

Los bots se crean con Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turno recibe una notificación de esa actividad entrante. A continuación, el controlador de turno envía la actividad entrante al `on_message_activity` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turno recibe una notificación de esa actividad entrante y envía la actividad entrante a `on_conversation_update_activity` . El controlador de actividades de Teams comprueba primero si hay eventos específicos de Teams. Si no se encuentra ningún evento, los pasa al controlador de actividades de Bot Framework.

En la clase de controlador de actividad de Teams, hay dos controladores de actividad de Teams principales y `on_conversation_update_activity` `on_invoke_activity` . `on_conversation_update_activity` enruta todas las actividades de actualización de conversaciones y `on_invoke_activity` enruta todas las actividades de invocación de Teams.

Para implementar la lógica para controladores de actividad específicos de Teams, debe invalidar los métodos del bot, como se muestra en la [sección lógica de bot.](#bot-logic) No hay ninguna implementación base para estos controladores, por lo tanto, debes agregar la lógica que quieras en tu invalidación.

---

## <a name="bot-logic"></a>Lógica de bot

La lógica del bot procesa las actividades entrantes de uno o más canales de bot y, en respuesta, genera actividades salientes. Esto sigue siendo así con los bots derivados de la clase del controlador de actividades de Teams, que primero comprueba las actividades de Teams. Después de comprobar las actividades de Teams, pasa todas las demás actividades al controlador de actividades de Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Controladores principales de Bot Framework

>[!NOTE]
> Excepto para las  *actividades de* los miembros agregados y eliminados, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no es de Teams.

Los controladores de actividad son diferentes en el contexto de un equipo, donde se agrega un nuevo miembro al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos incluye `ActivityHandler` lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibido | `OnTurnAsync` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensajes recibida | `OnMessageActivityAsync` | Este método se puede invalidar para controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `OnConversationUpdateActivityAsync` | Este método llama a un controlador si los miembros que no son el bot se unieron o dejaron la conversación, en una `ConversationUpdate` actividad. |
| Los miembros que no son bots se unieron a la conversación | `OnMembersAddedAsync` | Este método se puede invalidar para controlar a los miembros que se unen a una conversación. |
| Los miembros que no son bots dejaron la conversación | `OnMembersRemovedAsync` | Este método se puede invalidar para controlar a los miembros que salen de una conversación. |
| Actividad de evento recibida | `OnEventActivityAsync` | Este método llama a un controlador específico del tipo de evento, en una `Event` actividad. |
| Actividad de evento de respuesta de token recibida | `OnTokenResponseEventAsync` | Este método se puede invalidar para controlar eventos de respuesta de token. |
| Actividad de evento que no es de token-respuesta recibida | `OnEventAsync` | Este método se puede invalidar para controlar otros tipos de eventos. |
| Otro tipo de actividad recibida | `OnUnrecognizedActivityTypeAsync` | Este método se puede invalidar para controlar cualquier tipo de actividad que no se controle de otro modo. |

#### <a name="teams-specific-activity-handlers"></a>Controladores de actividad específicos de Teams

Amplía la lista de controladores de la sección controladores de `TeamsActivityHandler` Core Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Este método se puede invalidar para controlar un canal de Teams que se está creando. Para obtener más información, vea [El canal creado en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Este método se puede invalidar para controlar un canal de Teams que se va a eliminar. Para obtener más información, vea [El canal eliminado en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Este método se puede invalidar para controlar el cambio de nombre de un canal de Teams. Para obtener más información, vea Cambiar el nombre [del canal en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Este método se puede invalidar para controlar el cambio de nombre de un equipo de Teams. Para obtener más información, vea [El equipo cambió de nombre](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersAdded | `OnTeamsMembersAddedAsync` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar a los miembros que se unen a un equipo. Para obtener más información, vea [Los miembros del equipo agregados en](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar a los miembros que salen de un equipo. Para obtener más información, vea Miembros [del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en eventos [de actualización de conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Teams invocan actividades

La lista de controladores de actividad de Teams a los que se llama desde el controlador de actividad `OnInvokeActivityAsync` de Teams incluye lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Este método se invoca cuando se recibe una actividad de acción de tarjeta de conector O365 desde el conector. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Este método se invoca cuando se recibe una actividad de estado signIn verify desde el conector. |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tarea. |
| tarea/envío                     | `OnTeamsTaskModuleSubmitAsync`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación enumeradas en esta sección son para bots de conversación en Teams. El SDK de Bot Framework también admite invocar actividades específicas de extensiones de mensajería. Para obtener más información, vea [¿Qué son las extensiones de mensajería?](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Controladores principales de Bot Framework

>[!NOTE]
> Excepto para las  *actividades de* los miembros agregados y eliminados, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no es de Teams.

Los controladores de actividad son diferentes en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos incluye `ActivityHandler` lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibido | `onTurn` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensajes recibida | `onMessage` | Este método ayuda a controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `onConversationUpdate` | Este método llama a un controlador si los miembros que no son el bot se unieron o dejaron la conversación, en una `ConversationUpdate` actividad. |
| Los miembros que no son bots se unieron a la conversación | `onMembersAdded` | Este método ayuda a controlar los miembros que se unen a una conversación. |
| Los miembros que no son bots dejaron la conversación | `onMembersRemoved` | Este método ayuda a controlar los miembros que salen de una conversación. |
| Actividad de evento recibida | `onEvent` | Este método llama a un controlador específico del tipo de evento en una `Event` actividad. |
| Actividad de evento de respuesta de token recibida | `onTokenResponseEvent` | Este método ayuda a controlar eventos de respuesta de token. |
| Otro tipo de actividad recibida | `onUnrecognizedActivityType` | Este método ayuda a controlar cualquier tipo de actividad que no se controle de otro modo. |

#### <a name="teams-specific-activity-handlers"></a>Controladores de actividad específicos de Teams

Amplía la lista de controladores de la sección controladores de `TeamsActivityHandler` Core Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Este método se puede invalidar para controlar un canal de Teams que se está creando. Para obtener más información, vea [El canal creado en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Este método se puede invalidar para controlar un canal de Teams que se va a eliminar. Para obtener más información, vea [El canal eliminado en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Este método se puede invalidar para controlar el cambio de nombre de un canal de Teams. Para obtener más información, vea Cambiar el nombre [del canal en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Este método se puede invalidar para controlar el cambio de nombre de un equipo de Teams. Para obtener más información, vea [El equipo cambió de nombre](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersAdded | `OnTeamsMembersAddedAsync` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar a los miembros que se unen a un equipo. Para obtener más información, vea [Los miembros del equipo agregados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) en eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar a los miembros que salen de un equipo. Para obtener más información, vea Miembros [del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en eventos [de actualización de conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |

#### <a name="teams-invoke-activities"></a>Teams invocan actividades

La lista de controladores de actividad de Teams a los que se llama desde el controlador de actividad `onInvokeActivity` de Teams incluye lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Este método se invoca cuando se recibe una actividad de acción de tarjeta de conector O365 desde el conector. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Este método se invoca cuando se recibe una actividad de estado signIn verify desde el conector. |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tarea. |
| tarea/envío                     | `handleTeamsTaskModuleSubmit`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación que se enumeran en esta sección son para bots de conversación en Teams. El SDK de Bot Framework también admite invocar actividades específicas de extensiones de mensajería. Para obtener más información, vea [¿Qué son las extensiones de mensajería?](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Controladores principales de Bot Framework

>[!NOTE]
> Excepto para las  *actividades de* los miembros agregados y eliminados, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no es de Teams.

Los controladores de actividad son diferentes en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos incluye `ActivityHandler` lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibido | `on_turn` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensajes recibida | `on_message_activity` | Este método se puede invalidar para controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `on_conversation_update_activity` | Este método llama a un controlador si los miembros que no son el bot se unen a la conversación o la abandonan. |
| Los miembros que no son bots se unieron a la conversación | `on_members_added_activity` | Este método se puede invalidar para controlar a los miembros que se unen a una conversación. |
| Los miembros que no son bots dejaron la conversación | `on_members_removed_activity` | Este método se puede invalidar para controlar a los miembros que salen de una conversación. |
| Actividad de evento recibida | `on_event_activity` | Este método llama a un controlador específico del tipo de evento. |
| Actividad de evento de respuesta de token recibida | `on_token_response_event` | Este método se puede invalidar para controlar eventos de respuesta de token. |
| Actividad de evento que no es de token-respuesta recibida | `on_event` | Este método se puede invalidar para controlar otros tipos de eventos. |
| Otros tipos de actividad recibidos | `on_unrecognized_activity_type` | Este método se puede invalidar para controlar cualquier tipo de actividad que no se controle. |

#### <a name="teams-specific-activity-handlers"></a>Controladores de actividad específicos de Teams

Amplía la lista de controladores de la sección controladores de `TeamsActivityHandler` Core Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Este método se puede invalidar para controlar un canal de Teams que se está creando. Para obtener más información, vea [El canal creado en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `on_teams_channel_deleted` | Este método se puede invalidar para controlar un canal de Teams que se va a eliminar. Para obtener más información, vea [El canal eliminado en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `on_teams_channel_renamed` | Este método se puede invalidar para controlar el cambio de nombre de un canal de Teams. Para obtener más información, vea Cambiar el nombre [del canal en](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` Este método se puede invalidar para controlar el cambio de nombre de un equipo de Teams. Para obtener más información, vea [El equipo cambió de nombre](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersAdded | `on_teams_members_added` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar a los miembros que se unen a un equipo. Para obtener más información, vea [Los miembros del equipo agregados en](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) eventos de actualización de [conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `on_teams_members_removed` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler` . El método se puede invalidar para controlar a los miembros que salen de un equipo. Para obtener más información, vea Miembros [del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en eventos [de actualización de conversación.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Teams invocan actividades

La lista de controladores de actividad de Teams a los que se llama desde el controlador de actividad `on_invoke_activity` de Teams incluye lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `on_teams_file_consent`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Este método se invoca cuando se recibe una actividad de acción de tarjeta de conector O365 desde el conector. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Este método se invoca cuando se recibe una actividad de estado signIn verify desde el conector. |
| task/fetch                      | `on_teams_task_module_fetch`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tarea. |
| tarea/envío                     | `on_teams_task_module_submit`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación enumeradas en esta sección son para bots de conversación en Teams. El SDK de Bot Framework también admite invocar actividades específicas de extensiones de mensajería. Para obtener más información, vea [¿Qué son las extensiones de mensajería?](https://aka.ms/azure-bot-what-are-messaging-extensions)

---
