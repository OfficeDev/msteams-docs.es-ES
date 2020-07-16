---
title: Asistente virtual para Microsoft Teams
description: Procedimiento para crear habilidades y robots de asistente virtual para su uso en Microsoft Teams
keywords: bots de los asistentes virtuales de Microsoft Teams
ms.openlocfilehash: 0bb1ad832fd33675e607874fcc50f20ffbb96943
ms.sourcegitcommit: 26b7404142706290810064f8216abaa1c262d1e5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2020
ms.locfileid: "45146024"
---
# <a name="virtual-assistant-for-microsoft-teams"></a>Asistente virtual para Microsoft Teams

Asistente Virtual es una plantilla de código abierto de Microsoft que le permite crear una solución de conversación robusta y mantener un control total sobre la experiencia del usuario, la personalización de marca organizacional y los datos necesarios. La [plantilla de núcleo del asistente virtual](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) es el bloque de creación básico que reúne las tecnologías de Microsoft necesarias para crear un asistente virtual, incluido [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (Luis)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), así como capacidades esenciales, incluido el registro de habilidades, las cuentas vinculadas, la intención de conversación básica para ofrecer a los usuarios finales una variedad de interacciones y experiencias sin problemas. Además, las capacidades de plantilla incluyen ejemplos enriquecidos de [conocimientos](https://microsoft.github.io/botframework-solutions/overview/skills)de conversación reutilizables.  Se pueden integrar habilidades individuales en una solución de asistente virtual para habilitar varios escenarios. Mediante el uso del SDK de bot Framework, las habilidades se presentan en el código fuente, lo que le permite personalizar y ampliar según sea necesario. Vea [Qué es una habilidad del marco de bot](https://microsoft.github.io/botframework-solutions/overview/skills/).

![Diagrama de información general del asistente virtual](../assets/images/bots/virtual-assistant/overview.png)

Las actividades de mensajes de texto se redirigen a las aptitudes asociadas por el núcleo del asistente virtual mediante un modelo de [envío](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) . 

## <a name="implementation-considerations"></a>Consideraciones sobre la implementación

La decisión de agregar un asistente virtual puede incluir muchos determinantes y variar para cada organización. Estos son los factores que admiten la implementación de un asistente virtual para su organización:

- Un equipo central administra todas las experiencias de los empleados y tiene la capacidad de crear una experiencia de asistente virtual y administrar las actualizaciones de la experiencia principal, incluida la adición de nuevas habilidades.
- Existen varias aplicaciones en todas las funciones empresariales o el número se espera que crezca en el futuro.
- Las aplicaciones existentes son personalizables, son propiedad de la organización y se pueden convertir en habilidades para un asistente virtual.
- El equipo de las experiencias de los empleados centrales puede influir en las personalizaciones de las aplicaciones existentes y proporcionar las instrucciones necesarias para integrar las aplicaciones existentes como habilidades en la experiencia de asistente virtual

![El equipo central mantiene el asistente y la función de negocio Teams contribuyen a las habilidades](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Crear un asistente virtual centrado en Microsoft Teams

Microsoft ha publicado una [plantilla de Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) para crear asistentes y habilidades virtuales. Con la plantilla de Visual Studio, puede crear un asistente virtual, con una experiencia basada en texto y compatible con tarjetas complejas con acciones. Hemos mejorado la plantilla base de Visual Studio para incluir las capacidades de la plataforma de Microsoft Teams y las experiencias de la aplicación de Power excelentes Teams. Algunas de las capacidades incluyen compatibilidad con las tarjetas adaptables enriquecidas, los módulos de tareas, los chats de grupo y los equipos, y las extensiones de mensajería. *Consulte también*, [Tutorial: ampliar el asistente virtual a Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).

![Diagrama de alto nivel de una solución de asistente virtual](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Agregar tarjetas adaptables a su asistente virtual

Para enviar solicitudes correctamente, el asistente virtual debe identificar el modelo de LUIS correcto y la habilidad correspondiente asociada con ella. Sin embargo, el mecanismo de distribución no puede usarse para actividades de acción de tarjeta, ya que el modelo LUIS asociado con una habilidad puede no ser entrenado para los textos de acción de tarjeta, ya que son palabras clave predefinidas y fijas, y no utterances de un usuario.

Para solucionarlo, se incrusta la información sobre las habilidades en la carga de acciones de tarjeta. Cada habilidad debe incluirse `skillId` en el `value` campo de las acciones de la tarjeta. Esta es la mejor manera de asegurarse de que cada actividad de la acción de la tarjeta incluye la información de habilidad relevante y el asistente virtual puede usar esta información para el envío.

A continuación se muestra un ejemplo de datos de acción de tarjeta. Al proporcionarle `skillId` en el constructor, garantizamos que la información de habilidades siempre está presente en las acciones de la tarjeta.

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

A continuación, se presenta una `SkillCardActionData` clase en la plantilla de asistente virtual para extraer `skillId` de la carga de acciones de tarjeta.

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

A continuación se muestra un fragmento de código para extraer `skillId` de los datos de acción de tarjeta. La implementamos como un método de extensión en la clase [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .

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

### <a name="handle-interruptions-gracefully"></a>Controlar las interrupciones correctamente

El asistente virtual puede controlar las interrupciones en los casos en los que un usuario intenta invocar una habilidad mientras otra habilidad está activa en ese momento. hemos lanzado `TeamsSkillDialog` y `TeamsSwitchSkillDialog` , en función de [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de bot Framework, para permitir que los usuarios cambien la experiencia de las Aptitudes de las tarjetas. Para controlar esta solicitud, el asistente virtual solicita al usuario un mensaje de confirmación para cambiar de aptitudes.

![Mensaje de confirmación al cambiar a una nueva habilidad](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>Administración de solicitudes de módulos de tareas

Para agregar funciones de módulos de tareas a un asistente virtual, se incluyen dos métodos adicionales en el controlador de actividad del asistente virtual: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` . Estos métodos atienden actividades relacionadas con el módulo de tareas del asistente virtual, identifican la habilidad asociada a la solicitud y reenvían la solicitud a la habilidad identificada. 

El reenvío de solicitudes se realiza a través del método [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable) `PostActivityAsync` . Devuelve la respuesta como la `InvokeResponse` que se analiza y se convierte en `TaskModuleResponse` .

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

Se sigue un método similar para la distribución de la acción de tarjeta y las respuestas del módulo de tareas. Los datos de la acción buscar y enviar del módulo de tareas se actualizan para incluir `skillId` . `GetSkillId`El método de extensión de actividad extrae `skillId` de la carga que proporciona detalles sobre la habilidad que se debe invocar.

A continuación se muestra un fragmento de código para `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` los métodos y.

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

            return invokeResponse.GetTaskModuleRespose();
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

Además, todos los dominios de habilidad deben incluirse en la `validDomains` sección del archivo de manifiesto del asistente virtual para que los módulos de tareas invocados a través de una habilidad se procesen correctamente.

### <a name="handling-collaborative-app-scopes"></a>Administración de ámbitos de aplicaciones de colaboración

Las aplicaciones de Microsoft Teams pueden existir en varios ámbitos, entre los que se incluyen chat de 1:1, chat de grupo y canales. La plantilla principal de asistente virtual está diseñada para 1:1 chats. Como parte de la experiencia de incorporación, el asistente virtual solicita a los usuarios que tengan el nombre y mantenga el estado del usuario. Debido a que la experiencia de incorporación no es adecuada para los ámbitos de canal y de chat de grupo, se ha quitado.

Las habilidades deben administrar actividades en varios ámbitos (chat de 1:1, chat de grupo y conversación de canal). Si alguno de estos ámbitos no se admite, las habilidades deben responder con un mensaje apropiado.

Se han agregado las siguientes funciones de procesamiento al núcleo de asistente virtual:

- El asistente virtual se puede invocar sin mensajes de texto desde un canal o chat de grupo.
- Articulations se limpian (es decir, quitan los @mention necesarios del bot) antes de enviar el mensaje al módulo de distribución.

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

### <a name="handling-messaging-extensions"></a>Control de las extensiones de mensajería

Los comandos para una extensión de mensajería se declaran en el archivo de manifiesto de la aplicación. La interfaz de usuario de la extensión de mensajería funciona con estos comandos. Para que un asistente virtual pueda alimentar un comando de extensión de mensajería (como una habilidad adjunta), el propio manifiesto de un asistente virtual debe contener esos comandos. Los comandos de un manifiesto de una habilidad individual se deben agregar también al manifiesto del asistente virtual. El identificador de comando proporciona información sobre una habilidad asociada al anexar el identificador de aplicación de la habilidad a través de un separador ( `:` ).

A continuación se muestra un fragmento de código del archivo de manifiesto de una habilidad.

```json
 "composeExtensions": [
    {
        "botId": "<Skil_App_Id>",
        "commands": [
            {
                "id": "searchQuery",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

Y, a continuación, se muestra el fragmento de código de archivo de manifiesto de asistente virtual correspondiente.

```json
 "composeExtensions": [
    {
        "botId": "<VA_App_Id>",
        "commands": [
            {
                "id": "searchQuery:<skill_id>",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

Una vez que un usuario invoca los comandos, el asistente virtual puede identificar una habilidad asociada mediante el análisis del identificador de comando, la actualización de la actividad al quitar el sufijo adicional ( `:<skill_id>` ) del identificador de comando y reenviarlo a la habilidad correspondiente. No es necesario que el código de una habilidad controle el sufijo adicional, por lo que se evitan los conflictos entre los identificadores de comando en todas las aptitudes. Con este enfoque, todos los comandos de búsqueda y acción de una habilidad dentro de todos los contextos ("redacción", "commandBox" y "mensaje") se pueden alimentar por un asistente virtual.

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

Algunas actividades de extensión de mensajería no incluyen el identificador de comando. Por ejemplo, `composeExtension/selectItem` contiene solo el valor de la acción de pulsar invocar. Para identificar la habilidad asociada, `skillId` se adjunta a cada ficha de producto mientras forma una respuesta para `OnTeamsMessagingExtensionQueryAsync` . (Esto es similar al enfoque para [Agregar tarjetas adaptables a su asistente virtual](#add-adaptive-cards-to-your-virtual-assistant).

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>Ejemplo: convertir la plantilla de aplicación de libro a salón en una habilidad de asistente virtual

[Book-a-Room](app-templates.md#book-a-room) es un [robot de Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios buscar y reservar rápidamente una sala de reuniones para 30 (predeterminado), 60 o 90 minutos a partir de la hora actual. El bot? o de robot de libro a salón se limita a conversaciones personales o de 1:1.

![Asistente virtual con una habilidad para "reservar un salón"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

A continuación se indican los cambios Delta que se han incluido para convertirlos en una habilidad que se puede adjuntar a un asistente virtual. Se pueden seguir instrucciones similares para convertir cualquier bot existente de V4 en una habilidad.

### <a name="skill-manifest"></a>Manifiesto de habilidad

Un manifiesto de habilidad es un archivo JSON que expone el punto de conexión de mensajería de una habilidad, el identificador, el nombre y otros metadatos relevantes (este manifiesto es diferente del manifiesto usado para la transferencia local de una aplicación en Microsoft Teams) un asistente virtual requiere una ruta de acceso a este archivo como entrada para adjuntar una habilidad. Se ha agregado el siguiente manifiesto a la carpeta wwwroot del bot.

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

El modelo de envío del asistente virtual se basa en los modelos LUIS de habilidades adjuntas. El modelo de envío identifica la intención de cada actividad de texto y encuentra la habilidad asociada a ella.

El asistente virtual requiere el modelo LUIS (en `.lu` formato) de habilidad como entrada al adjuntar una habilidad. El JSON de LUIS se puede convertir al `.lu` formato mediante la herramienta botframework-CLI.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

El bot? a-Room de libros a salón tiene dos comandos principales para los usuarios:

- `Book room`
- `Manage Favorites`

Hemos creado un modelo LUIS que comprenda estos dos comandos. Los secretos correspondientes deben rellenarse `cognitivemodels.json` . El archivo JSON correspondiente de LUIS se puede encontrar [aquí](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) y así es como se `.lu` Ve el archivo correspondiente.

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

Con este enfoque, cualquier problema de comandos de un usuario a un asistente virtual relacionado con `book room` o `manage favorites` se puede identificar como un comando asociado con un bot de libro a salón y se reenvía a esta habilidad.
Por otra parte, el bot? n de salón de sala-a-Room tiene que usar el modelo LUIS para comprender estos comandos si no se escriben tal cual (por ejemplo: `I want to manage my favorite rooms` ).

### <a name="multi-language-support"></a>Compatibilidad con varios idiomas

Para este ejemplo, solo se ha creado un modelo LUIS con una referencia cultural inglés. Puede crear modelos LUIS correspondientes a otros idiomas y agregar entrada a `cognitivemodels.json` .

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

En paralelo, agregue el `.lu` archivo correspondiente en la ruta de acceso luisFolder. La estructura de carpetas debe ser de la siguiente manera:

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Actualice el comando botskills de la siguiente manera para modificar el `languages` parámetro:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

El asistente virtual usa `SetLocaleMiddleware` para identificar la configuración regional actual e invocar el modelo de envío correspondiente. (La actividad de la estructura de bot tiene un campo de configuración regional que usa este middleware). También le recomendamos que use lo mismo para su habilidad. El bot? n a-salón de guía no usa este middleware y, en su lugar, obtiene la configuración regional de la [entidad clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de la actividad de la actividad de bot Framework.

### <a name="claim-validation"></a>Validación de notificaciones

Hemos agregado [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) para restringir la habilidad a los autores de las llamadas. Para permitir que un asistente virtual llame a esta habilidad, llene `AllowedCallers` la matriz desde `appsettings` con ese identificador de aplicación del asistente virtual en particular.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

La matriz de llamadores permitidos puede restringir la habilidad que los consumidores pueden tener acceso a la habilidad. Agregar una entrada `*` a esta matriz, para aceptar llamadas de cualquier consumidor de aptitudes.

```
"AllowedCallers": [ "*" ],
```
[Aquí](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)encontrará documentación detallada para agregar validación de notificaciones a una habilidad.

### <a name="card-refresh-limitation"></a>Limitación de actualización de tarjeta

La actividad de actualización (actualización de tarjeta) no se admite todavía a través del asistente virtual ([problema de github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Por lo tanto, hemos reemplazado todas las llamadas `UpdateActivityAsync` de actualización de tarjeta () por el registro de nuevas llamadas de tarjeta ( `SendActivityAsync` ).

### <a name="card-actions-and-task-module-flows"></a>Acciones de tarjeta y flujos de módulo de tarea

Para reenviar actividades de la tarjeta o la acción del módulo de tareas a una habilidad asociada, la habilidad debe incrusrse `skillId` en ella.
Acción de tarjeta de bot? a-salón, las cargas de las acciones de búsqueda y envío del módulo de tareas se modifican para que contengan `skillId` un parámetro. 

Para obtener más información, consulte [esta](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) sección de esta documentación.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Controlar actividades desde el ámbito del canal o el chat de grupo

El bot? a-Room de libros a salón está diseñado solamente para chats privados (personal/1:1 ámbito). Como hemos personalizado el asistente virtual para admitir el chat de grupo y los ámbitos de canal, es posible que se invoque al asistente virtual desde estos ámbitos y, por lo tanto, el bot? a-Room del salón podría obtener actividades para el mismo. Por lo tanto, el bot? a-Room de libros a salón está personalizado para administrar esas actividades. La comprobación se ha implementado en `OnMessageActivityAsync` métodos del controlador de actividad de un bot de la sala.

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

También puede aprovechar las habilidades existentes del [repositorio de soluciones de bot Framework](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) o crear una nueva habilidad a partir de cero. Encontrará tutoriales para la versión más reciente [aquí](https://microsoft.github.io/botframework-solutions/overview/skills/). Consulte la [documentación](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0) para obtener información sobre el asistente virtual y la arquitectura de conocimientos.

## <a name="sample-code-to-get-started"></a>Código de ejemplo para empezar

- [Plantilla de Visual Studio actualizada](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [Código de cualificación de robot-a-salón](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a>Limitaciones conocidas del asistente virtual

- **EndOfConversation**. Una habilidad debe enviar una `endOfConversation` actividad cuando termine una conversación. base esta actividad, un asistente virtual finaliza el contexto con esa habilidad en particular y vuelve al contexto (raíz) del asistente virtual. Para el bot? a-Room de libros a salón, no hay un estado claro en el que se puede finalizar la conversación. Por lo tanto, no hemos enviado `endOfConversation` desde el bot? a-a-Room y cuando un usuario desea volver al contexto raíz, simplemente puede hacerlo por `start over` comando.
- **Actualización**de la tarjeta. Las actualizaciones de la tarjeta todavía no se admiten a través de asistente virtual.
- **Extensiones de mensajería**:
  - Actualmente, un asistente virtual puede admitir un máximo de diez comandos para las extensiones de mensajería.
  - La configuración de las extensiones de mensajería no se centra en comandos individuales, sino en toda la extensión. Esto limita la configuración para cada habilidad individual a través de asistente virtual.
  - Los identificadores de comando de las extensiones de mensajería tienen una longitud máxima de [64 caracteres](../resources/schema/manifest-schema.md#composeextensions) y se usarán 37 caracteres para incrustar información sobre las aptitudes. Por lo tanto, las restricciones actualizadas para el identificador de comando están limitadas a 27 caracteres.
>
>
