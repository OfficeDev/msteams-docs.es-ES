---
title: Crear un asistente virtual
description: Obtenga información sobre cómo crear un bot de Virtual Assistant para Teams mediante ejemplos de código y fragmentos de código con características como tarjetas adaptables, control de interrupciones y mucho más.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 4f35edee79dba5b6a8faa9720906915bec27d6d5
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499282"
---
# <a name="create-virtual-assistant"></a>Crear un asistente virtual

Asistente virtual es una plantilla de código abierto de Microsoft que permite crear una solución conversacional sólida a la vez que mantiene el control total de la experiencia del usuario, la marca de la organización y los datos necesarios. La [plantilla de base del asistente virtual](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) es el bloque de creación básico que reúne las tecnologías de Microsoft necesarias para crear un asistente virtual, incluidos el [SDK Bot Framework](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/)y [QnA Maker](https://www.qnamaker.ai/). También reúne las funcionalidades esenciales, como el registro de aptitudes, las cuentas vinculadas y la intención conversacional básica para ofrecer a los usuarios una variedad de interacciones y experiencias fluidas. Además, las funcionalidades de plantilla incluyen ejemplos enriquecidos de [aptitudes conversacionales](https://microsoft.github.io/botframework-solutions/overview/skills) reutilizables.  Las aptitudes individuales se integran en una solución del asistente virtual para habilitar varios escenarios. Con el SDK Bot Framework, las aptitudes se presentan en formato de código fuente, lo que le permite personalizar y ampliar según sea necesario. Para obtener más información sobre las aptitudes de Bot Framework, consulte [¿Qué es una aptitud Bot Framework?](https://microsoft.github.io/botframework-solutions/overview/skills/). Este documento le guía en las consideraciones relativas a la implementación para las organizaciones del asistente virtual, la creación de un asistente virtual centrado en Teams, el ejemplo relacionado, el ejemplo de código y las limitaciones del asistente virtual.
En la imagen siguiente se muestra la información general del asistente virtual:

![Diagrama de información general del asistente virtual](../assets/images/bots/virtual-assistant/overview.png)

El núcleo del asistente virtual enruta las actividades de mensajes de texto a las aptitudes asociadas mediante un modelo de [distribución](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true).

## <a name="implementation-considerations"></a>Consideraciones acerca de la implementación

La decisión de agregar un asistente virtual incluye muchos determinantes y diferencias para cada organización. Los factores de apoyo de una implementación de un asistente virtual para su organización son los siguientes:

* Un equipo central administra todas las experiencias de los empleados. Tiene la capacidad de crear una experiencia de un asistente virtual y administrar las actualizaciones de la experiencia principal, incluida la adición de nuevas aptitudes.
* Existen varias aplicaciones entre las funciones empresariales y se espera que el número crezca en el futuro.
* Las aplicaciones existentes son personalizables, son propiedad de la organización y se convierten en aptitudes para un asistente virtual.
* El equipo central de experiencias de los empleados puede influir en las personalizaciones de las aplicaciones existentes. También proporciona las instrucciones necesarias para integrar las aplicaciones existentes como aptitudes en la experiencia del asistente virtual.

En la imagen siguiente se muestran las funciones empresariales del asistente virtual:

![El equipo central gestiona el asistente y los equipos de funciones empresariales aportan aptitudes](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Crear un asistente virtual centrado en Teams

Microsoft ha publicado una [plantilla de Microsoft Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) para crear asistentes virtuales y aptitudes. Con la plantilla de Visual Studio, puede crear un asistente virtual, optimizado por una experiencia basada en texto con compatibilidad con tarjetas enriquecidas limitadas con acciones. Hemos mejorado la plantilla base de Visual Studio para incluir funcionalidades de plataforma de Microsoft Teams y mejorar las experiencias de aplicaciones de Teams. Algunas de las funcionalidades incluyen la compatibilidad con las tarjetas adaptables enriquecidos, los módulos de tareas, los equipos o chats de grupo y las extensiones de mensajes. Para obtener más información sobre la extensión del asistente virtual a Microsoft Teams, vea [Tutorial: Ampliar su asistente virtual a Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).
En la imagen siguiente se muestra el diagrama de alto nivel de una solución de asistente virtual:

![Diagrama de alto nivel de una solución de asistente virtual.](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Agregar las tarjetas adaptables a su asistente virtual

Para enviar las solicitudes correctamente, el asistente virtual debe identificar el modelo LUIS correcto y la aptitud correspondiente asociada a él. Sin embargo, el mecanismo de distribución no se puede usar para las actividades de acción de tarjeta, ya que el modelo de LUIS asociado a una aptitud se entrena para los textos de acción de tarjeta. Los textos de acción de tarjeta son las palabras clave fijas predefinidas y no comentadas por un usuario.

Este inconveniente se resuelve mediante la inserción de información de aptitud en la carga de acción de la tarjeta. Cada aptitud debe insertar `skillId` en el campo `value` de acciones de tarjeta. Debe asegurarse de que cada actividad de acción de tarjeta lleva la información de aptitud pertinente y el asistente virtual puede utilizar esta información para el envío.

Debe proporcionar `skillId` en el constructor para asegurarse de que la información de aptitudes siempre está presente en las acciones de tarjeta.
En la sección siguiente se muestra un código de ejemplo de datos de acción de tarjeta:

```csharp
    public class CardActionData
    {
        public CardActionData(string skillId)
        {
            this.SkillId = skillId;
        }

        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }

    ...
    var button = new CardAction
    {
        Type = ActionTypes.MessageBack,
        Title = "Card action button",
        Text = "card action button text",
        Value = new CardActionData(<SkillId>),
    };
```

A continuación, la clase `SkillCardActionData` de la plantilla del asistente virtual se introduce para extraer `skillId` de la carga de la acción de tarjeta.
En la sección siguiente se muestra un fragmento de código para extraer `skillId` de la carga de la acción de tarjeta:

```csharp
    // Skill Card action data should contain skillId parameter
    // This class is used to deserialize it and get skillId 
    public class SkillCardActionData
    {
        /// <summary>
        /// Gets the ID of the skil that should handle this card
        /// </summary>
        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }
```

La implementación se realiza mediante un método de extensión en la clase [Actividad](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md).
En la sección siguiente se muestra un fragmento de código para extraer `skillId` de la acción de tarjeta:

```csharp
    public static class ActivityExtensions
    {
        // Fetches skillId from CardAction data if present
        public static string GetSkillId(this Activity activity)
        {
            string skillId = string.Empty;

            try
            {
                if (activity.Type.Equals(ActivityTypes.Message) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(activity.Value.ToString());
                    skillId = data.SkillId;
                }
                else if (activity.Type.Equals(ActivityTypes.Invoke) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(JObject.Parse(activity.Value.ToString()).SelectToken("data").ToString());
                    skillId = data.SkillId;
                }
            }
            catch
            {
                // If not able to retrive skillId, empty skillId should be returned
            }

            return skillId;
        }
    }
```

### <a name="handle-interruptions"></a>Controlar las interrupciones

El asistente virtual puede controlar las interrupciones en los casos en los que un usuario intenta invocar una aptitud mientras otra aptitud está activa en ese momento. `TeamsSkillDialog` y `TeamsSwitchSkillDialog` se presentan en función de [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs) de Bot Framework. Permiten a los usuarios cambiar una experiencia de aptitud de las acciones de tarjeta. Para controlar esta solicitud, el asistente virtual solicita al usuario cambiar las aptitudes con un mensaje de confirmación:

![Mensaje de confirmación al cambiar a una nueva aptitud](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Controlar solicitudes de módulo de tareas

Para agregar funcionalidades del módulo de tareas a un asistente virtual, se incluyen dos métodos adicionales en el controlador de actividad del asistente virtual: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync`. Estos métodos escuchan las actividades relacionadas con el módulo de tareas desde el asistente virtual, identifican la aptitud asociada a la solicitud y reenvían la solicitud a la aptitud identificada.

El reenvío de solicitudes se realiza a través del método [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync`. Devuelve la respuesta como `InvokeResponse` que se analiza y convierte en `TaskModuleResponse`.

```csharp
    public static TaskModuleResponse GetTaskModuleRespose(this InvokeResponse invokeResponse)
    {
        if (invokeResponse.Body != null)
        {
            return new TaskModuleResponse()
            {
                Task = GetTask(invokeResponse.Body),
            };
        }

        return null;
    }

    private static TaskModuleResponseBase GetTask(object invokeResponseBody)
        {
            JObject resposeBody = (JObject)JToken.FromObject(invokeResponseBody);
            var task = resposeBody.GetValue("task");
            var taskType = task.SelectToken("type").ToString();

            return taskType switch
            {
                "continue" => new TaskModuleContinueResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToObject<TaskModuleTaskInfo>(),
                },
                "message" => new TaskModuleMessageResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToString(),
                },
                _ => null,
            };
        }
```

Se sigue un enfoque similar para la distribución de acciones de tarjeta y las respuestas del módulo de tareas. Los datos de acción de captura y envío del módulo de tareas se actualizan para incluir `skillId`.
El método de extensión de actividad `GetSkillId` extrae `skillId` de la carga que proporciona detalles sobre la aptitud que se debe invocar.

El fragmento de código para los métodos `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` se proporciona en la sección siguiente:

```csharp
    // Invoked when a "task/fetch" event is received to invoke task module.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken);

            return invokeResponse.GetTaskModuleResponse();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }

    // Invoked when a 'task/submit' invoke activity is received for task module submit actions.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

            return invokeResponse.GetTaskModuleRespose();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }
```

Además, debe incluir todos los dominios de aptitud en la sección `validDomains` del archivo de manifiesto del asistente virtual para que los módulos de tareas invocados a través de una aptitud se representen correctamente.

### <a name="handle-collaborative-app-scopes"></a>Controlar los ámbitos de aplicaciones colaborativas

Las aplicaciones Teams pueden existir en varios ámbitos, como chats individuales, chats grupales y canales. La plantilla del asistente virtual principal está diseñada para chats individuales. Como parte de la experiencia de incorporación, el asistente virtual solicita a los usuarios un nombre y mantiene el estado del usuario. Dado que la experiencia de incorporación no es adecuada para el chat en grupo o los ámbitos de canal, se ha quitado.

Las aptitudes deben controlar las actividades en varios ámbitos, como el chat individual, el chat grupal y la conversación de canal. Si no se admite alguno de estos ámbitos, las aptitudes deben responder con un mensaje adecuado.

Se han agregado las siguientes funciones de procesamiento al núcleo del asistente virtual:

* El asistente virtual se puede invocar sin ningún mensaje de texto de un canal o chat de grupo.
* Las articulaciones se limpian antes de enviar el mensaje al módulo de distribución. Por ejemplo, quite la @mención necesaria del bot.

```csharp
    if (innerDc.Context.Activity.Conversation?.IsGroup == true)
    {
        // Remove bot atmentions for teams/groupchat scope
        innerDc.Context.Activity.RemoveRecipientMention();

        // If bot is invoked without any text, reply with FirstPromptMessage
        if (string.IsNullOrWhiteSpace(innerDc.Context.Activity.Text))
        {
            await innerDc.Context.SendActivityAsync(_templateEngine.GenerateActivityForLocale("FirstPromptMessage"));
            return EndOfTurn;
        }
    }
```

### <a name="handle-message-extensions"></a>Controlar extensiones de mensaje

Los comandos de una extensión de mensaje se declaran en el archivo de manifiesto de la aplicación. La interfaz de usuario de la extensión de mensaje funciona con esos comandos. Para que un asistente virtual alimente un comando de extensión de mensaje como una aptitud adjunta, el propio manifiesto de un asistente virtual debe contener esos comandos. Debe agregar los comandos del manifiesto de una aptitud individual al manifiesto del asistente virtual. El identificador de comando proporciona información sobre una aptitud asociada anexando un identificador de aplicación de la aptitud a través de un separador `:`.

El fragmento de código del archivo de manifiesto de una aptitud se muestra en la sección siguiente:

```json
 "composeExtensions": [
    {
        "botId": "<Skil_App_Id>",
        "commands": [
            {
                "id": "searchQuery",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
                 ....}
         ]
     }
 ]
                 
```

El fragmento de código del archivo de manifiesto del asistente virtual correspondiente se muestra en la sección siguiente:

```json
 "composeExtensions": [
    {
        "botId": "<VA_App_Id>",
        "commands": [
            {
                "id": "searchQuery:<skill_id>",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
                 ....}
         ]
     }
 ]
 
```

Una vez que un usuario invoca los comandos, el asistente virtual puede identificar una aptitud asociada analizando el identificador de comando, actualiza la actividad quitando el sufijo adicional `:<skill_id>` del identificador de comando y reenvíándolo a la aptitud correspondiente. No es necesario que el código de una aptitud controle el sufijo adicional. Por lo tanto, se evitan los conflictos entre los identificadores de comando entre las aptitudes. Con este enfoque, todos los comandos de búsqueda y acción de una aptitud dentro de todos los contextos, como **la composición**, **commandBox** y **mensajes** se basan en un asistente virtual.

```csharp
    const string MessagingExtensionCommandIdSeparator = ":";

    // Invoked when a 'composeExtension/submitAction' invoke activity is received for a messaging extension action command
    protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        return await ForwardMessagingExtensionActionCommandActivityToSkill(turnContext, action, cancellationToken);
    }

    // Forwards invoke activity to right skill for messaging extension action commands.
    private async Task<MessagingExtensionActionResponse> ForwardMessagingExtensionActionCommandActivityToSkill(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        var skillId = ExtractSkillIdFromMessagingExtensionActionCommand(turnContext, action);
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionActionResponse();
    }

    // Extracts skill Id from messaging extension command and updates activity value
    private string ExtractSkillIdFromMessagingExtensionActionCommand(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action)
    {
        var commandArray = action.CommandId.Split(MessagingExtensionCommandIdSeparator);
        var skillId = commandArray.Last();

        // Update activity value by removing skill id before forwarding to the skill.
        var activityValue = JsonConvert.DeserializeObject<MessagingExtensionAction>(turnContext.Activity.Value.ToString());
        activityValue.CommandId = string.Join(MessagingExtensionCommandIdSeparator, commandArray, 0 commandArray.Length - 1);
        turnContext.Activity.Value = activityValue;

        return skillId;
    }
```

Algunas actividades de extensión de mensaje no incluyen el identificador de comando. Por ejemplo, `composeExtension/selectItem` contiene solo el valor de la acción de toque de invocación. Para identificar la aptitud asociada, `skillId` se adjunta a cada tarjeta de elemento al formar una respuesta para `OnTeamsMessagingExtensionQueryAsync`. Esto es similar al enfoque para [agregar tarjetas adaptables al asistente virtual](#add-adaptive-cards-to-your-virtual-assistant).

```csharp
    // Invoked when a 'composeExtension/selectItem' invoke activity is received for compose extension query command.
    protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
    {
        var data = JsonConvert.DeserializeObject<SkillCardActionData>(query.ToString());
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == data.SkillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionResponse();
    }
```

---

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo convertir la plantilla de aplicación Book-a-room en una aptitud de Virtual Assistant: Reservar una sala es un equipo de Teams que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30, 60 o 90 minutos a partir de la hora actual. El valor predeterminado es 30 minutos. El bot de reserva de reuniones se limita a las conversaciones personales o individuales.
En la imagen siguiente se muestra un asistente virtual con una aptitud **reservar una sala**:

![Asistente virtual con una aptitud "reservar una sala"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

A continuación se muestran los cambios diferenciales introducidos para convertirlo en una aptitud, que se adjunta a un asistente virtual. Se siguen instrucciones similares para convertir cualquier bot v4 existente en una aptitud.

### <a name="skill-manifest"></a>Manifiesto de aptitud

Un manifiesto de aptitud es un archivo JSON que expone el punto de conexión de mensajería, el identificador, el nombre y otros metadatos pertinentes de una aptitud. Este manifiesto es diferente del manifiesto usado para transferir localmente una aplicación en Teams. Un asistente virtual requiere una ruta de acceso a este archivo como entrada para adjuntar una aptitud. Hemos agregado el siguiente manifiesto a la carpeta wwwroot del bot.

```bash
botskills connect --remoteManifest "<url to skill's manifest>" ..
```

```json
{
  "$schema": "https://schemas.botframework.com/schemas/skills/skill-manifest-2.1.preview-0.json",
  "$id": "microsoft_teams_apps_bookaroom",
  "name": "microsoft-teams-apps-bookaroom",
  "description": "microsoft-teams-apps-bookaroom description",
  "publisherName": "Your Company",
  "version": "1.1",
  "iconUrl": "<icon url>",
  "copyright": "Copyright (c) Microsoft Corporation. All rights reserved.",
  "license": "",
  "privacyUrl": "<privacy url>",
  "endpoints": [
    {
      "name": "production",
      "protocol": "BotFrameworkV3",
      "description": "Production endpoint for the skill",
      "endpointUrl": "<endpoint url>",
      "msAppId": "skill app id"
    }
  ],
  "dispatchModels": {
    "languages": {
      "en-us": [
        {
          "id": "microsoft-teams-apps-bookaroom-en",
          "name": "microsoft-teams-apps-bookaroom LU (English)",
          "contentType": "application/lu",
          "url": "file://book-a-meeting.lu",
          "description": "English language model for the skill"
        }
      ]
    }
  },
  "activities": {
    "message": {
      "type": "message",
      "description": "Receives the users utterance and attempts to resolve it using the skill's LU models"
    }
  }
}
```

### <a name="luis-integration"></a>Integración de LUIS

El modelo de distribución del asistente virtual se basa en los modelos LUIS de las aptitudes adjuntas. El modelo de distribución identifica la intención de cada actividad de texto y detecta la aptitud asociada a ella.

El asistente virtual requiere el modelo LUIS de la aptitud en `.lu` formato como entrada al adjuntar una aptitud. El json de LUIS se convierte al formato `.lu` mediante la herramienta botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

El bot de reserva de reuniones tiene dos comandos principales para los usuarios:

* `Book room`
* `Manage Favorites`

Hemos creado un modelo LUIS mediante la comprensión de estos dos comandos. Los secretos correspondientes deben rellenarse en `cognitivemodels.json`. El archivo JSON de LUIS correspondiente se encuentra [aquí](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).
El archivo `.lu` correspondiente se muestra en la sección siguiente:

```
> ! Automatically generated by [LUDown CLI](https://github.com/Microsoft/botbuilder-tools/tree/master/Ludown), Tue Mar 31 2020 17:30:32 GMT+0530 (India Standard Time)

> ! Source LUIS JSON file: book-a-meeting.json

> ! Source QnA TSV file: Not Specified

> ! Source QnA Alterations file: Not Specified


> # Intent definitions

## BOOK ROOM
- book a room
- book room
- please book a room
- reserve a room
- i want to book a room
- i want to book a room please
- get me a room please
- get me a room


## MANAGE FAVORITES
- manage favorites
- manage favorite
- please manage my favorite rooms
- manage my favorite rooms please
- manage my favorite rooms
- i want to manage my favorite rooms

## None


> # Entity definitions


> # PREBUILT Entity definitions


> # Phrase list definitions


> # List entities

> # RegEx entities
```

Con este enfoque, cualquier comando emitido por un usuario al asistente virtual relacionado con `book room` o `manage favorites` se identifican como un comando asociado al `Book-a-room` bot y se reenvía a esta aptitud.
Por otro lado, `Book-a-room room` el bot debe usar el modelo de LUIS para comprender estos comandos si no están escritos completos. Por ejemplo: `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Compatibilidad con varios idiomas

Por ejemplo, se crea un modelo LUIS con únicamente la cultura inglesa. Puede crear modelos LUIS correspondientes a otros idiomas y agregar una entrada a `cognitivemodels.json`.

```json
{
  "defaultLocale": "en-us",
  "languageModels": {
    "en-us": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    },
    "<your_language_culture>": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    }
  }
}
```

En paralelo, agregue el archivo correspondiente `.lu` en la ruta de acceso luisFolder. La estructura de carpetas debe ser la siguiente:

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Para modificar el `languages` parámetro, actualice el comando de aptitudes del bot como se indica a continuación:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

El asistente virtual usa `SetLocaleMiddleware` para identificar la configuración regional actual e invocar el modelo de envío correspondiente. La actividad de Bot Framework tiene un campo de configuración regional que usa este middleware. También puede usar lo mismo para su aptitud. El bot book-a-room no usa este middleware y, en su lugar, obtiene la configuración regional de la [entidad clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo) de la actividad de Bot Framework.

### <a name="claim-validation"></a>Validación de notificaciones

Hemos agregado [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) para restringir a los autores de llamadas a la aptitud. Para permitir que un asistente virtual llame a esta aptitud, rellene `AllowedCallers` la matriz a partir del identificador de aplicación `appsettings` de ese asistente virtual en particular.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

La matriz de llamadores permitidos puede restringir los consumidores de aptitudes que pueden acceder a la aptitud. Agregue una entrada `*` única a esta matriz para aceptar las llamadas de cualquier consumidor de aptitudes.

```
"AllowedCallers": [ "*" ],
```

Para obtener más información sobre cómo agregar la validación de notificaciones a una aptitud, consulte [agregar validación de notificaciones a la aptitud](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).

### <a name="limitation-of-card-refresh"></a>Limitación de la actualización de tarjetas

La actividad de actualización, como la actualización de tarjetas, aún no se admite a través de Virtual Assistant ([problema de GitHub](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Por lo tanto, hemos reemplazado todas las llamadas de actualización de tarjetas `UpdateActivityAsync` por publicar nuevas llamadas de `SendActivityAsync`tarjeta .

### <a name="card-actions-and-task-module-flows"></a>Acciones de tarjeta y flujos de módulos de tareas

Para reenviar las actividades de acción de tarjeta o de módulo de tareas a una aptitud asociada, la aptitud debe insertar `skillId` en ella.
`Book-a-room` la acción de tarjeta de bot, las cargas de acción de captura y envío del módulo de tareas se modifican para que contengan `skillId` como parámetro.

Para obtener más información, consulte [esta](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) sección de esta documentación.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Controlar las actividades desde el chat de grupo o el ámbito del canal

`Book-a-room bot` está diseñado solo para los chats privados, como el ámbito personal o individual. Dado que hemos personalizado el asistente virtual para admitir los ámbitos de canal y chat de grupo, el asistente virtual debe invocarse desde los ámbitos de canal y, por tanto, `Book-a-room` el bot debe obtener actividades para el mismo ámbito. Por lo tanto, `Book-a-room`el bot se personaliza para controlar esas actividades. Puede encontrar la comprobación de métodos `OnMessageActivityAsync` del controlador de actividad del bot `Book-a-room`.

```csharp
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        // Check if activities are from groupchat/ teams scope. This might happen when the bot is consumed by Virtual Assistant.
        if (turnContext.Activity.Conversation.IsGroup == true)
        {
            await ShowNotSupportedInGroupChatCardAsync(turnContext).ConfigureAwait(false);
        }
        else
        {
            ...
        }
    }
```

También puede aprovechar las aptitudes existentes del repositorio de [repositorio de Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) o crear una nueva aptitud completamente desde cero. Para crear una nueva aptitud, consulte [tutoriales para crear una nueva aptitud](https://microsoft.github.io/botframework-solutions/overview/skills/). Para obtener documentación sobre virtual assistant y arquitectura de aptitudes, consulte [Virtual Assistant and skills architecture(Asistente virtual y arquitectura de aptitudes](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)).  

## <a name="limitations-of-virtual-assistant"></a>Limitaciones del asistente virtual

* **EndOfConversation**: una aptitud debe enviar una actividad `endOfConversation` cuando finaliza una conversación. En función de la actividad, un asistente virtual finaliza el contexto con esa aptitud determinada y vuelve al contexto raíz del asistente virtual. En el caso del bot book-a-room, no hay un estado claro en el que se termine la conversación. Por lo tanto, no hemos enviado `endOfConversation` desde el `Book-a-room` bot y, cuando el usuario quiere volver al contexto raíz, simplemente puede hacerlo por `start over` comando.  
* **Actualización de tarjetas**: la actualización de tarjetas aún no se admite a través de Virtual Assistant.  
* **Extensiones de mensaje**:
  * Actualmente, un asistente virtual puede admitir un máximo de diez comandos para las extensiones de mensaje.
  * La configuración de las extensiones de mensaje no se limita a comandos individuales, sino a toda la propia extensión. Esto limita la configuración de cada aptitud individual a través del asistente virtual.
  * Los identificadores de comandos de extensiones de mensaje tienen una longitud máxima de [64 caracteres](../resources/schema/manifest-schema.md#composeextensions) y se usan 37 caracteres para insertar información de aptitudes. Por lo tanto, las restricciones actualizadas para el identificador de comando están limitadas a 27 caracteres.

También puede aprovechar las aptitudes existentes del repositorio de [repositorio de Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) o crear una nueva aptitud completamente desde cero. Los tutoriales para más adelante se pueden encontrar [aquí](https://microsoft.github.io/botframework-solutions/overview/skills/). Consulte la [documentación](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) relativa al asistente virtual y la arquitectura de las aptitudes.

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| Plantilla de Visual Studio actualizada | Plantilla personalizada para admitir las capacidades de los equipos. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| Código de aptitud de bot de reserva de reuniones | Le permite encontrar y reservar rápidamente una sala de reuniones sobre la marcha. | [Ver](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |

## <a name="see-also"></a>Consulte también

* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Bot de reserva de reuniones](app-templates.md#app-template-code-samples)
* [Bot de Microsoft Teams](../bots/what-are-bots.md)
