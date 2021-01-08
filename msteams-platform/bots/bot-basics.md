---
title: Conceptos básicos de bot
author: clearab
description: Comprenda los conceptos básicos de los bots en Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 43dd351b30fdba3435d39aca43aae0f2de00ed24
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731961"
---
# <a name="bot-basics"></a>Conceptos básicos de bot

Se trata de una introducción que se basa en el artículo sobre [Cómo funcionan los bots](https://aka.ms/how-bots-work) en la documentación principal del [marco de bot](https://aka.ms/azure-bot-service-docs). Puede que le resulte útil el artículo y los otros artículos de la sección *conceptos* .

La diferencia principal en los bots desarrollados para Microsoft Teams es la forma en que se administran las actividades. El controlador de actividades de Microsoft Teams se deriva del controlador de actividad del marco de robots para enrutar todas las actividades de Teams antes de permitir que se controlen actividades específicas que no pertenecen a teams.

## <a name="teams-activity-handlers"></a>Controladores de actividades de Microsoft Teams

Cuando un bot para Microsoft Teams recibe una actividad, lo pasa a sus *controladores de actividad*. En las cubiertas, hay un controlador base denominado el *controlador de torneado*, al que se redirigen todas las actividades. El *controlador de torneado* llama al controlador de actividades necesario para controlar cualquier tipo de actividad que se haya recibido. La diferencia entre un bot diseñado para Microsoft Teams es que se deriva de `TeamsActivityHandler` la clase derivada de la clase del marco de robots `ActivityHandler` .

# <a name="c"></a>[C#](#tab/csharp)

Como con cualquier bot creado mediante Microsoft bot Framework, si el bot recibe una actividad de mensaje, el controlador de torneado ve esa actividad entrante y la envía al `OnMessageActivityAsync` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de torneado ve esa actividad entrante y la envía al `OnConversationUpdateActivityAsync` . Controlador de actividad de Microsoft *Teams* primero, comprobará los eventos específicos de Microsoft Teams y los pasará al controlador de actividad del marco de bot si no se encuentra ninguno.

En la clase del controlador de actividad de Microsoft Teams, hay dos controladores de actividad principales de Teams `OnConversationUpdateActivityAsync` que enrutan todas las actividades de actualización de la conversación y `OnInvokeActivityAsync` que enrutan todas las actividades de invocación de Teams.

Para implementar la lógica de los controladores de actividades específicos de Teams, invalide estos métodos en el bot, tal como se muestra en la sección [lógica de bot](#bot-logic) a continuación. Para cada uno de estos controladores, no hay ninguna implementación base, así que solo agregue la lógica que desee en su reemplazo.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Como con cualquier bot creado mediante Microsoft bot Framework, si el bot recibe una actividad de mensaje, el controlador de torneado ve esa actividad entrante y la envía al `onMessage` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de torneado ve esa actividad entrante y la envía al `dispatchConversationUpdateActivity` . Controlador de actividad de Microsoft *Teams* que primero comprobará los eventos específicos de Microsoft Teams y lo pasarán al controlador de actividad de bot frameworks si no se encuentra ninguno.

En la clase del controlador de actividad de Microsoft Teams, hay dos controladores de actividad principales de Teams `dispatchConversationUpdateActivity` que enrutan todas las actividades de actualización de la conversación y `onInvokeActivity` que enrutan todas las actividades de invocación de Teams.

Para implementar la lógica de los controladores de actividades específicos de Teams, invalide estos métodos en el bot tal como se muestra en la sección de la [lógica de bot](#bot-logic) . Para cada uno de estos controladores, defina la lógica del bot y, a continuación, **Asegúrese de llamar `next()` al final**. Al llamar `next()` , asegúrese de que se ejecuta el siguiente controlador.

# <a name="python"></a>[Python](#tab/python)

Los bots se crean mediante Microsoft bot Framework, si el bot recibe una actividad de mensaje, el controlador de giro recibe una notificación de la actividad entrante. A continuación, el controlador de Turn envía la actividad de entrada al `on_message_activity` controlador de actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de torneado recibe una notificación de esa actividad entrante y envía la actividad entrante a `on_conversation_update_activity` . El controlador de actividad de Microsoft Teams buscará primero los eventos específicos de Teams. Si no se encuentra ningún evento, se pasarán al controlador de actividad del marco de robots.

En la clase del controlador de actividad de Microsoft Teams, hay dos controladores de actividad principales de Teams `on_conversation_update_activity` y `on_invoke_activity` . `on_conversation_update_activity` enruta todas las actividades de actualización de conversaciones y `on_invoke_activity` enruta todas las actividades de invocación de Teams.

Para implementar la lógica de los controladores de actividades específicos de Teams, debe invalidar estos métodos en el bot, tal como se muestra en la sección [lógica de bot](#bot-logic) . No hay ninguna implementación base para estos controladores; por lo tanto, debe agregar la lógica que desee en su reemplazo.

---

## <a name="bot-logic"></a>Lógica de bot

La lógica de bot procesa las actividades entrantes de uno o varios de los canales de robot y genera actividades de salida en respuesta.  Esto sigue siendo el caso de los bots derivados de la clase del controlador de actividad de Microsoft Teams, que primero comprueba las actividades de Microsoft Teams y, a continuación, pasa todas las demás actividades al controlador de actividad de los marcos de bot.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Controladores de Framework bot principales

Todos los controladores de actividades que se describen a continuación seguirán funcionando como lo hacen con un bot que no es de Microsoft Teams, con la excepción de controlar los miembros *agregados* y las actividades *eliminadas* por los miembros, éstos serán distintos en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de a un hilo de mensaje.

Los controladores definidos en `ActivityHandler` se describen a continuación:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibido | `OnTurnAsync` | Llama a uno de los otros controladores, en función del tipo de actividad que se ha recibido. |
| Actividad de mensaje recibida | `OnMessageActivityAsync` | Invalide esto para controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `OnConversationUpdateActivityAsync` | En una `ConversationUpdate` actividad, llama a un controlador si los miembros que no son el bot se unen a la conversación o la dejan. |
| Los miembros que no son de bot se unieron a la conversación | `OnMembersAddedAsync` | Invalide esto para controlar los miembros que se unen a una conversación. |
| Los miembros que no son de bot dejan la conversación | `OnMembersRemovedAsync` | Invalide esto para controlar a los miembros que abandonen una conversación. |
| Actividad de evento recibida | `OnEventActivityAsync` | En una `Event` actividad, llama a un controlador específico para el tipo de evento. |
| Actividad de evento de respuesta de token-respuesta recibida | `OnTokenResponseEventAsync` | Invalide esto para controlar los eventos de respuesta de token. |
| Actividad de evento que no es de respuesta de tokens recibida | `OnEventAsync` | Invalide esto para controlar otros tipos de eventos. |
| Se recibió otro tipo de actividad | `OnUnrecognizedActivityTypeAsync` | Invalide esto para controlar cualquier tipo de actividad no controlado de otro modo. |

#### <a name="teams-specific-handlers"></a>Controladores específicos de Teams

El `TeamsActivityHandler` extiende la lista de controladores anteriores para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Invalide esto para controlar el canal de teams que se está creando. Para obtener más información, consulte [Channel created](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) in [Conversation Update Events](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Invalide esto para controlar el canal de Microsoft teams que se va a eliminar. Para obtener más información, consulte [canal eliminado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Invalide esto para controlar el canal de un canal de Microsoft Teams. Para obtener más información, consulte [canal con nombre cambiado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) en [Conversation Update Events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Invalide esto para administrar el cambio de nombre de un equipo de Teams. Para obtener más información, vea cambio de [nombre de equipo](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en eventos de [actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Llama al `OnMembersAddedAsync` método en `ActivityHandler` . Invalide esto para controlar a los miembros que se unen a un equipo. Para obtener más información, vea [miembros del equipo agregados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Llama al `OnMembersRemovedAsync` método en `ActivityHandler` . Invalide esto para controlar a los miembros que salen de un equipo. Para obtener más información, vea [miembros del equipo quitados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Actividades de invocación de Microsoft Teams

A continuación, se muestra una lista de todos los controladores de actividad de Teams a los que se llama desde el controlador de actividad de Microsoft `OnInvokeActivityAsync` _Teams_ :

| Tipos de invocación                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction. Invoke               | `OnTeamsCardActionInvokeAsync`       | Invocar acción de tarjeta de equipo. |
| fileConsent/Invoke              | `OnTeamsFileConsentAcceptAsync`      | Aceptación del consentimiento del archivo de Microsoft Teams. |
| fileConsent/Invoke              | `OnTeamsFileConsentAsync`            | Consentimiento del archivo de Teams. |
| fileConsent/Invoke              | `OnTeamsFileConsentDeclineAsync`     | Consentimiento del archivo de Teams. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Acción de la tarjeta del conector de O365 de Teams. |
| Inicio de sesión/verifyState              | `OnTeamsSigninVerifyStateAsync`      | El estado de comprobación de inicio de sesión de Microsoft Teams. |
| tarea/recopilación                      | `OnTeamsTaskModuleFetchAsync`        | Búsqueda de módulos de tareas de Microsoft Teams. |
| tarea o envío                     | `OnTeamsTaskModuleSubmitAsync`       | Envío del módulo de tareas de Microsoft Teams. |

Las actividades de invocación enumeradas anteriormente son para bots de conversación en Microsoft Teams. El SDK de bot Framework también admite invocaciones específicas de las extensiones de mensajería. Para obtener más información, consulte [What is Messaging Extensions](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Todos los controladores de actividades descritos a continuación seguirán funcionando como lo hacen con un bot que no es de Microsoft Teams, con la excepción de controlar las actividades de los miembros *agregados* y de los miembros *quitados* , éstos serán distintos en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de un hilo de mensaje.

#### <a name="core-bot-framework-handlers"></a>Controladores de Framework bot principales

Los controladores definidos en `ActivityHandler` se describen a continuación.

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibido | `onTurn` | Llama a uno de los otros controladores, en función del tipo de actividad que se ha recibido. |
| Actividad de mensaje recibida | `onMessage` | Proporcionar una función para que esto controle una `Message` actividad. |
| Actividad de actualización de conversación recibida | `onConversationUpdate` | En una `ConversationUpdate` actividad, llama a un controlador si los miembros que no son el bot se unen a la conversación o la dejan. |
| Los miembros que no son de bot se unieron a la conversación | `onMembersAdded` | Proporcionar una función para que esto controle los miembros que se unen a una conversación. |
| Los miembros que no son de bot dejan la conversación | `onMembersRemoved` | Proporcione una función para que esto gestione a los miembros que abandonen una conversación. |
| Actividad de evento recibida | `onEvent` | En una `Event` actividad, llama a un controlador específico para el tipo de evento. |
| Actividad de evento de respuesta de token-respuesta recibida | `onTokenResponseEvent` | Proporcionar una función para que esto controle los eventos de respuesta de token. |
| Se recibió otro tipo de actividad | `onUnrecognizedActivityType` | Proporcione una función para que esto controle cualquier tipo de actividad no controlada de otro modo. |
| Controladores de actividades completados | `onDialog` | Proporcione una función para que pueda controlar cualquier procesamiento que deba realizarse al final de un turno una vez que haya finalizado el resto de los controladores de actividades. |

#### <a name="teams-specific-handlers"></a>Controladores específicos de Teams

La `TeamsActivityHandler` amplía la lista de controladores de la sección Controladores de Framework de bot principales para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Invalide esto para controlar el canal de teams que se está creando. Para obtener más información, consulte [Channel created](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) in [Conversation Update Events](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Invalide esto para controlar el canal de Microsoft teams que se va a eliminar. Para obtener más información, consulte [canal eliminado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Invalide esto para controlar el canal de un canal de Microsoft Teams. Para obtener más información, consulte [canal con nombre cambiado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) en [Conversation Update Events](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Invalide esto para administrar el cambio de nombre de un equipo de Teams. Para obtener más información, vea cambio de [nombre de equipo](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en eventos de [actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Llama al `OnMembersAddedAsync` método en `ActivityHandler` . Invalide esto para controlar a los miembros que se unen a un equipo. Para obtener más información, vea [miembros del equipo agregados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Llama al `OnMembersRemovedAsync` método en `ActivityHandler` . Invalide esto para controlar a los miembros que salen de un equipo. Para obtener más información, vea [miembros del equipo quitados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events). |

#### <a name="teams-invoke-activities"></a>Actividades de invocación de Microsoft Teams

A continuación, se muestra una lista de todos los controladores de actividad de Teams a los que se llama desde el controlador de actividad de Microsoft `onInvokeActivity` Teams:

| Tipos de invocación                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction. Invoke               | `handleTeamsCardActionInvoke`       | Invocar acción de tarjeta de equipo. |
| fileConsent/Invoke              | `handleTeamsFileConsentAccept`      | Aceptación del consentimiento del archivo de Microsoft Teams. |
| fileConsent/Invoke              | `handleTeamsFileConsent`            | Consentimiento del archivo de Teams. |
| fileConsent/Invoke              | `handleTeamsFileConsentDecline`     | Consentimiento del archivo de Teams. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Acción de la tarjeta del conector de O365 de Teams. |
| Inicio de sesión/verifyState              | `handleTeamsSigninVerifyState`      | El estado de comprobación de inicio de sesión de Microsoft Teams. |
| tarea/recopilación                      | `handleTeamsTaskModuleFetch`        | Búsqueda de módulos de tareas de Microsoft Teams. |
| tarea o envío                     | `handleTeamsTaskModuleSubmit`       | Envío del módulo de tareas de Microsoft Teams. |

Las actividades de invocación que se enumeran en la sección actividades de invocación de Microsoft Teams son para bots de conversación en Microsoft Teams. El SDK de bot Framework también admite actividades de invocación específicas de las extensiones de mensajería. Para obtener más información, consulte [What is Messaging Extensions](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Controladores de Framework bot principales

>[!NOTE]
> Excepto para las actividades de los miembros agregados y quitados, todos los controladores de actividades descritos en esta sección siguen funcionando como lo hacen con un bot que no es de Microsoft Teams.

Los controladores de actividades son diferentes en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de a un hilo de mensaje.

La lista de controladores definidos en `ActivityHandler` incluye lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibido | `on_turn` | Llama a uno de los otros controladores, en función del tipo de actividad que se ha recibido. |
| Actividad de mensaje recibida | `on_message_activity` | Invalida esto para controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `on_conversation_update_activity` | Llama a un controlador si los miembros que no son el bot se unen o abandonan la conversación. |
| Los miembros que no son de bot se unieron a la conversación | `on_members_added_activity` | Invalida esto para controlar los miembros que se unen a una conversación. |
| Los miembros que no son de bot dejan la conversación | `on_members_removed_activity` | Invalida esto para controlar a los miembros que abandonen una conversación. |
| Actividad de evento recibida | `on_event_activity` | Llama a un controlador específico para el tipo de evento. |
| Actividad de evento de respuesta de token-respuesta recibida | `on_token_response_event` | Invalida esto para controlar los eventos de respuesta de token. |
| Actividad de evento que no es de respuesta de tokens recibida | `on_event` | Invalida esto para controlar otros tipos de eventos. |
| Otros tipos de actividades recibidas | `on_unrecognized_activity_type` | Invalida esto para controlar cualquier tipo de actividad que no se controla. |

#### <a name="teams-specific-handlers"></a>Controladores específicos de Teams

La `TeamsActivityHandler` amplía la lista de controladores de la sección Controladores de Framework de bot principales para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Invalida esto para controlar el canal de teams que se está creando. Para obtener más información, consulte [canal creado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) en la [actualización de conversaciones eventos](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `on_teams_channel_deleted` | Invalida esto para controlar el canal de Microsoft teams que se va a eliminar. Para obtener más información, vea [canal eliminado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) en [conversación actualizar eventos](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `on_teams_channel_renamed` | Suplanta esto para controlar el cambio del nombre de un canal de Teams. Para obtener más información, consulte [canal cambiado el nombre](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) de [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` Invalida esto para administrar el cambio de nombre de un equipo de Teams. Para obtener más información, vea cambio de [nombre de equipo](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en eventos de [actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `on_teams_members_added` | Llama al `OnMembersAddedAsync` método en `ActivityHandler` . Invalida esto para controlar los miembros que se unen a un equipo. Para obtener más información, vea [miembros del equipo agregados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `on_teams_members_removed` | Llama al `OnMembersRemovedAsync` método en `ActivityHandler` . Invalida esto para controlar a los miembros que salen de un equipo. Para obtener más información, vea [miembros del equipo quitados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Actividades de invocación de Microsoft Teams

La lista de controladores de actividad de equipos a los que se llama desde el controlador de actividad de Microsoft `on_invoke_activity` Teams incluye lo siguiente:

| Tipos de invocación                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction. Invoke               | `on_teams_card_action_invoke`       | Invocar acción de tarjeta de equipo. |
| fileConsent/Invoke              | `on_teams_file_consent_accept`      | Aceptación del consentimiento del archivo de Microsoft Teams. |
| fileConsent/Invoke              | `on_teams_file_consent`            | Consentimiento del archivo de Teams. |
| fileConsent/Invoke              | `on_teams_file_consent_decline`     | Rechazo del consentimiento del archivo de Microsoft Teams. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Acción de la tarjeta del conector de O365 de Teams. |
| Inicio de sesión/verifyState              | `on_teams_signin_verify_state`      | El estado de comprobación de inicio de sesión de Microsoft Teams. |
| tarea/recopilación                      | `on_teams_task_module_fetch`        | Búsqueda de módulos de tareas de Microsoft Teams. |
| tarea o envío                     | `on_teams_task_module_submit`       | Envío del módulo de tareas de Microsoft Teams. |

Las actividades de invocación que se enumeran en la sección actividades de invocación de Microsoft Teams son para bots de conversación en Microsoft Teams. El SDK de bot Framework también admite actividades de invocación específicas de las extensiones de mensajería. Para obtener más información, consulte [What is Messaging Extensions](https://aka.ms/azure-bot-what-are-messaging-extensions).

---
