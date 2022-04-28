---
title: Controladores de actividad de bots
author: surbhigupta
description: Comprenda los controladores de actividad del bot en Teams.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: evento de canal de consentimiento de la tarjeta de bot del marco de trabajo del controlador de actividad
ms.openlocfilehash: 34dd5e8042b71f4e7cc78df7e7c543c86a53f58e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104038"
---
# <a name="bot-activity-handlers"></a>Controladores de actividad de bots

Este documento se basa en el artículo sobre [cómo funcionan los bots](https://aka.ms/how-bots-work) en la documentación básica de [Bot Framework](https://aka.ms/azure-bot-service-docs). La principal diferencia entre los bots desarrollados para Microsoft Teams y el núcleo de Bot Framework se encuentra en las características proporcionadas en Teams.

Para organizar la lógica conversacional del bot, se usa un controlador de actividad. Las actividades se controlan de dos maneras mediante Teams controladores de actividad y lógica de bot. El controlador de actividad Teams agrega compatibilidad con eventos e interacciones específicos de Microsoft Teams. El objeto bot contiene el razonamiento conversacional o la lógica de un turno y expone un controlador de turnos, que es el método que puede aceptar actividades entrantes desde el adaptador del bot.

## <a name="teams-activity-handlers"></a>controladores de actividad de Teams

Teams controlador de actividad se deriva del controlador de actividad de Microsoft Bot Framework. Enruta todas las actividades Teams antes de permitir que se controlen las actividades específicas que no sean Teams.

Cuando un bot para Teams recibe una actividad, se enruta a los controladores de actividad. Todas las actividades se enrutan a través de un controlador base denominado controlador de turnos. El controlador de turnos llama al controlador de actividad necesario para administrar cualquier actividad recibida. El bot Teams se deriva de la `TeamsActivityHandler` clase , que se deriva de la clase de `ActivityHandler` Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

Los bots se crean mediante Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turnos recibe una notificación de esa actividad entrante. A continuación, el controlador de turnos envía la actividad entrante al controlador de `OnMessageActivityAsync` actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turnos recibe una notificación de esa actividad entrante y envía la actividad entrante a `OnConversationUpdateActivityAsync`. El controlador de actividad Teams comprueba primero si hay eventos Teams específicos. Si no se encuentra ningún evento, los pasa al controlador de actividad de Bot Framework.

En la clase de controlador de actividad Teams, hay dos controladores de actividad de Teams principales, `OnConversationUpdateActivityAsync` y `OnInvokeActivityAsync`. `OnConversationUpdateActivityAsync`enruta todas las actividades de actualización de conversación y `OnInvokeActivityAsync` enruta todas las Teams invocar actividades.

Para implementar la lógica para Teams controladores de actividad específicos, debe invalidar los métodos del bot, como se muestra en la sección [lógica del bot](#bot-logic). No hay ninguna implementación base para estos controladores, por lo que debe agregar la lógica que desee en la invalidación.

Fragmentos de código para controladores de actividad de Teams:

`OnTeamsChannelCreatedAsync`

```csharp

protected override Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelDeletedAsync`

```csharp

protected override Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelRenamedAsync`

```csharp

protected override Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsTeamRenamedAsync`

```csharp

protected override Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsMembersAddedAsync`

```csharp

protected override Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsMembersRemovedAsync`

```csharp

protected override Task OnTeamsMembersRemovedAsync(IList<TeamsChannelAccount> teamsMembersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken);
  {
   // Code logic here
  }
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Los bots se crean mediante Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turnos recibe una notificación de esa actividad entrante. A continuación, el controlador de turnos envía la actividad entrante al controlador de `onMessage` actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turnos recibe una notificación de esa actividad entrante y envía la actividad entrante a `dispatchConversationUpdateActivity`. El controlador de actividad Teams comprueba primero si hay eventos Teams específicos. Si no se encuentra ningún evento, los pasa al controlador de actividad de Bot Framework.

En la clase de controlador de actividad Teams, hay dos controladores de actividad de Teams principales, `dispatchConversationUpdateActivity` y `onInvokeActivity`. `dispatchConversationUpdateActivity`enruta todas las actividades de actualización de conversación y `onInvokeActivity` enruta todas las Teams invocar actividades.

Para implementar la lógica para Teams controladores de actividad específicos, debe invalidar los métodos del bot, como se muestra en la sección [lógica del bot](#bot-logic). Defina la lógica del bot para estos controladores y asegúrese de llamar `next()` al final. Al llamar a `next()` , asegúrese de que se ejecuta el siguiente controlador.

Fragmentos de código para controladores de actividad de Teams:

`OnTeamsChannelCreatedAsync`

```javascript

onTeamsChannelCreated(async (channelInfo, teamInfo, context, next) => {
       // code for handling
        await next()
    });
```

`OnTeamsChannelDeletedAsync`

```javascript

onTeamsChannelDeleted(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsChannelRenamedAsync`

```javascript

onTeamsChannelRenamed(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsTeamRenamedAsync`

```javascript

onTeamsTeamRenamedAsync(async (teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsMembersAddedAsync`

```javascript

onTeamsMembersAdded(async (membersAdded, teamInfo, context, next) => {
       // code for handling
    await next();
    });
```

`OnTeamsMembersRemovedAsync`

```javascript

onTeamsMembersRemoved(async (membersRemoved, teamInfo, context, next) => {
       // code for handling
    await next();
    });
```

# <a name="python"></a>[Python](#tab/python)

Los bots se crean mediante Bot Framework. Si los bots reciben una actividad de mensaje, el controlador de turnos recibe una notificación de esa actividad entrante. A continuación, el controlador de turnos envía la actividad entrante al controlador de `on_message_activity` actividad. En Teams, esta funcionalidad sigue siendo la misma. Si el bot recibe una actividad de actualización de conversación, el controlador de turnos recibe una notificación de esa actividad entrante y envía la actividad entrante a `on_conversation_update_activity`. El controlador de actividad Teams comprueba primero si hay eventos Teams específicos. Si no se encuentra ningún evento, los pasa al controlador de actividad de Bot Framework.

En la clase de controlador de actividad Teams, hay dos controladores de actividad de Teams principales, `on_conversation_update_activity` y `on_invoke_activity`. `on_conversation_update_activity`enruta todas las actividades de actualización de conversación y `on_invoke_activity` enruta todas las Teams invocar actividades.

Para implementar la lógica para Teams controladores de actividad específicos, debe invalidar los métodos del bot, como se muestra en la sección [lógica del bot](#bot-logic). No hay ninguna implementación base para estos controladores, por lo que debe agregar la lógica que desee en la invalidación.

---

## <a name="bot-logic"></a>Lógica del bot

La lógica del bot procesa las actividades entrantes desde uno o varios de los canales del bot y, en respuesta, genera actividades salientes. Esto sigue siendo cierto en el caso de los bots derivados de la clase de controlador de actividad Teams, que primero comprueba si hay actividades Teams. Después de comprobar Teams actividades, pasa todas las demás actividades al controlador de actividad de Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Controladores principales de Bot Framework

>[!NOTE]
>
>* Excepto para las actividades de los miembros **agregados** y **quitados**, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no es Teams.
>* `onInstallationUpdateActivityAsync()`se usa para obtener Teams configuración regional al agregar el bot a Teams.

Los controladores de actividad son diferentes en el contexto de un equipo, donde se agrega un nuevo miembro al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos en `ActivityHandler` incluye lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibida | `OnTurnAsync` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensaje recibida | `OnMessageActivityAsync` | Este método se puede invalidar para controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `OnConversationUpdateActivityAsync` | Este método llama a un controlador si miembros distintos del bot se unieron o abandonaron la conversación, en una `ConversationUpdate` actividad. |
| Miembros que no son bots se unieron a la conversación | `OnMembersAddedAsync` | Este método se puede invalidar para controlar los miembros que se unen a una conversación. |
| Los miembros que no son bots abandonaron la conversación | `OnMembersRemovedAsync` | Este método se puede invalidar para controlar los miembros que salen de una conversación. |
| Actividad de evento recibida | `OnEventActivityAsync` | Este método llama a un controlador específico del tipo de evento, en una `Event` actividad. |
| Actividad de evento de respuesta de token recibida | `OnTokenResponseEventAsync` | Este método se puede invalidar para controlar los eventos de respuesta de token. |
| Actividad de evento que no es de respuesta de token recibida | `OnEventAsync` | Este método se puede invalidar para controlar otros tipos de eventos. |
| Otro tipo de actividad recibido | `OnUnrecognizedActivityTypeAsync` | Este método se puede invalidar para controlar cualquier tipo de actividad de lo contrario no controlada. |

#### <a name="teams-specific-activity-handlers"></a>Teams controladores de actividad específicos

`TeamsActivityHandler` amplía la lista de controladores en la sección principales de controladores de Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Este método se puede invalidar para controlar un canal de Teams que se está creando. Para obtener más información, consulte [canal creado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Este método se puede invalidar para controlar un canal Teams que se va a eliminar. Para obtener más información, vea [Canal eliminado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) en [los eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Este método se puede invalidar para controlar un canal de Teams cuyo nombre se cambia. Para obtener más información, consulte [el nombre del canal](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Este método se puede invalidar para controlar un Teams equipo al que se va a cambiar el nombre. Para obtener más información, consulte [Cambio de nombre del equipo](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler`. El método se puede invalidar para controlar los miembros que se unen a un equipo. Para obtener más información, vea [Miembros del equipo agregados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler`. El método se puede invalidar para controlar los miembros que abandonan un equipo. Para obtener más información, vea [Miembros del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Teams invocar actividades

La lista de controladores de actividad Teams a los que se llama desde el `OnInvokeActivityAsync` controlador de actividad Teams incluye lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Este método se invoca cuando se recibe una actividad de acción de tarjeta del conector de Office 365 desde el conector. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Este método se invoca cuando se recibe una actividad de estado de comprobación de signIn desde el conector. |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tareas. |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación enumeradas en esta sección son para bots conversacionales en Teams. Bot Framework SDK también admite la invocación de actividades específicas de las extensiones de mensaje. Para obtener más información, consulte [¿Qué son las extensiones de mensaje](https://aka.ms/azure-bot-what-are-messaging-extensions)?

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Controladores principales de Bot Framework

>[!NOTE]
> Excepto para las actividades de los miembros **agregados** y **quitados**, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no es Teams.

Los controladores de actividad son diferentes en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos en `ActivityHandler` incluye lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibida | `onTurn` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensaje recibida | `onMessage` | Este método ayuda a controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `onConversationUpdate` | Este método llama a un controlador si miembros distintos del bot se unieron o abandonaron la conversación, en una `ConversationUpdate` actividad. |
| Miembros que no son bots se unieron a la conversación | `onMembersAdded` | Este método ayuda a controlar que los miembros se unan a una conversación. |
| Los miembros que no son bots abandonaron la conversación | `onMembersRemoved` | Este método ayuda a controlar que los miembros salgan de una conversación. |
| Actividad de evento recibida | `onEvent` | Este método llama a un controlador específico del tipo de evento, en una `Event` actividad. |
| Actividad de evento de respuesta de token recibida | `onTokenResponseEvent` | Este método ayuda a controlar los eventos de respuesta de token. |
| Otro tipo de actividad recibido | `onUnrecognizedActivityType` | Este método ayuda a controlar cualquier tipo de actividad de lo contrario no controlada. |

#### <a name="teams-specific-activity-handlers"></a>Teams controladores de actividad específicos

`TeamsActivityHandler` amplía la lista de controladores en la sección principales de controladores de Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Este método se puede invalidar para controlar un canal de Teams que se está creando. Para obtener más información, consulte [canal creado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Este método se puede invalidar para controlar un canal Teams que se va a eliminar. Para obtener más información, vea [Canal eliminado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) en [los eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Este método se puede invalidar para controlar un canal de Teams cuyo nombre se cambia. Para obtener más información, consulte [el nombre del canal](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Este método se puede invalidar para controlar un Teams equipo al que se va a cambiar el nombre. Para obtener más información, consulte [Cambio de nombre del equipo](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler`. El método se puede invalidar para controlar los miembros que se unen a un equipo. Para obtener más información, vea [Miembros del equipo agregados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler`. El método se puede invalidar para controlar los miembros que abandonan un equipo. Para obtener más información, vea [Miembros del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events). |

#### <a name="teams-invoke-activities"></a>Teams invocar actividades

La lista de controladores de actividad Teams a los que se llama desde el `onInvokeActivity` controlador de actividad Teams incluye lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Este método se invoca cuando se recibe una actividad de acción de tarjeta del conector de Office 365 desde el conector. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Este método se invoca cuando se recibe una actividad de estado de comprobación de signIn desde el conector. |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tareas. |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación enumeradas en esta sección son para bots conversacionales en Teams. Bot Framework SDK también admite la invocación de actividades específicas de las extensiones de mensaje. Para obtener más información, consulte [¿Qué son las extensiones de mensaje](https://aka.ms/azure-bot-what-are-messaging-extensions)?

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Controladores principales de Bot Framework

>[!NOTE]
> Excepto para las actividades de los miembros **agregados** y **quitados**, todos los controladores de actividad descritos en esta sección siguen funcionando como lo hacen con un bot que no es Teams.

Los controladores de actividad son diferentes en el contexto de un equipo, donde el nuevo miembro se agrega al equipo en lugar de un subproceso de mensaje.

La lista de controladores definidos en `ActivityHandler` incluye lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| Cualquier tipo de actividad recibida | `on_turn` | Este método llama a uno de los otros controladores, en función del tipo de actividad recibida. |
| Actividad de mensaje recibida | `on_message_activity` | Este método se puede invalidar para controlar una `Message` actividad. |
| Actividad de actualización de conversación recibida | `on_conversation_update_activity` | Este método llama a un controlador si miembros distintos del bot se unen o abandonan la conversación. |
| Miembros que no son bots se unieron a la conversación | `on_members_added_activity` | Este método se puede invalidar para controlar los miembros que se unen a una conversación. |
| Los miembros que no son bots abandonaron la conversación | `on_members_removed_activity` | Este método se puede invalidar para controlar los miembros que salen de una conversación. |
| Actividad de evento recibida | `on_event_activity` | Este método llama a un controlador específico del tipo de evento. |
| Actividad de evento de respuesta de token recibida | `on_token_response_event` | Este método se puede invalidar para controlar los eventos de respuesta de token. |
| Actividad de evento que no es de respuesta de token recibida | `on_event` | Este método se puede invalidar para controlar otros tipos de eventos. |
| Otros tipos de actividad recibidos | `on_unrecognized_activity_type` | Este método se puede invalidar para controlar cualquier tipo de actividad que no se controle. |

#### <a name="teams-specific-activity-handlers"></a>Teams controladores de actividad específicos

`TeamsActivityHandler` amplía la lista de controladores de la sección principal de controladores de Bot Framework para incluir lo siguiente:

| Evento | Controlador | Descripción |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Este método se puede invalidar para controlar un canal de Teams que se está creando. Para obtener más información, consulte [canal creado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `on_teams_channel_deleted` | Este método se puede invalidar para controlar un canal Teams que se va a eliminar. Para obtener más información, vea [Canal eliminado](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) en [los eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `on_teams_channel_renamed` | Este método se puede invalidar para controlar un canal de Teams cuyo nombre se cambia. Para obtener más información, consulte [el nombre del canal](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;`Este método se puede invalidar para controlar un Teams equipo al que se va a cambiar el nombre. Para obtener más información, consulte [Cambio de nombre del equipo](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en [eventos de actualización de conversación](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `on_teams_members_added` | Este método llama al `OnMembersAddedAsync` método en `ActivityHandler`. El método se puede invalidar para controlar los miembros que se unen a un equipo. Para obtener más información, vea [Miembros del equipo agregados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `on_teams_members_removed` | Este método llama al `OnMembersRemovedAsync` método en `ActivityHandler`. El método se puede invalidar para controlar los miembros que abandonan un equipo. Para obtener más información, vea [Miembros del equipo eliminados](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) en [eventos de actualización de conversaciones](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Teams invocar actividades

La lista de controladores de actividad Teams a los que se llama desde el `on_invoke_activity` controlador de actividad Teams incluye lo siguiente:

| Invocar tipos                    | Controlador                              | Descripción                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Este método se invoca cuando se recibe una actividad de invocación de acción de tarjeta desde el conector. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Este método se invoca cuando el usuario acepta una tarjeta de consentimiento de archivo. |
| fileConsent/invoke              | `on_teams_file_consent`            | Este método se invoca cuando se recibe una actividad de tarjeta de consentimiento de archivo desde el conector. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Este método se invoca cuando el usuario rechaza una tarjeta de consentimiento de archivo. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Este método se invoca cuando se recibe una actividad de acción de tarjeta del conector de Office 365 desde el conector. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Este método se invoca cuando se recibe una actividad de estado de comprobación de signIn desde el conector. |
| task/fetch                      | `on_teams_task_module_fetch`        | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se captura un módulo de tareas. |
| task/submit                     | `on_teams_task_module_submit`       | Este método se puede invalidar en una clase derivada para proporcionar lógica cuando se envía un módulo de tareas. |

Las actividades de invocación enumeradas en esta sección son para bots conversacionales en Teams. Bot Framework SDK también admite la invocación de actividades específicas de las extensiones de mensaje. Para obtener más información, consulte [¿Qué son las extensiones de mensaje](https://aka.ms/azure-bot-what-are-messaging-extensions)?

---

---

Ahora que se ha familiarizado con los controladores de actividad del bot, veamos cómo se comportan los bots de forma diferente en función de la conversación y de los mensajes que recibe o envía.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Conceptos básicos de la conversación](~/bots/how-to/conversations/conversation-basics.md)
