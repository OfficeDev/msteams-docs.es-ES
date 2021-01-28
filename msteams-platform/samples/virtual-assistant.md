---
title: Asistente virtual para Microsoft Teams
description: Cómo crear bots y aptitudes del Asistente virtual para su uso en Microsoft Teams
ms.topic: how-to
keywords: Bots de asistente virtual de teams
ms.openlocfilehash: d72b1afbf975707d694d4aaef31263a3ce467629
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014617"
---
# <a name="virtual-assistant-for-microsoft-teams"></a>Asistente virtual para Microsoft Teams

El Asistente virtual es una plantilla de código abierto de Microsoft que le permite crear una solución de conversación sólida mientras mantiene el control total de la experiencia del usuario, la personalidad de marca de la organización y los datos necesarios. La plantilla principal del Asistente [virtual](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) es el bloque de creación básico que reúne las tecnologías de Microsoft necesarias para crear un Asistente virtual, incluido [el SDK](https://github.com/microsoft/botframework-sdk)de Bot Framework , Language Understanding [(CION)](https://www.luis.ai/)y [QnA Maker,](https://www.qnamaker.ai/)así como las capacidades esenciales, como el registro de aptitudes, las cuentas vinculadas y la intención de conversación básica para ofrecer a los usuarios finales una variedad de interacciones y experiencias sin problemas. Además, las capacidades de plantilla incluyen ejemplos enriquecidos de aptitudes conversacionales [reutilizables.](https://microsoft.github.io/botframework-solutions/overview/skills)  Las habilidades individuales se pueden integrar en una solución de asistente virtual para habilitar varios escenarios. Con el SDK de Bot Framework, las aptitudes se presentan en forma de código fuente, lo que permite personalizar y ampliar según sea necesario. Vea [¿Qué es una habilidad de Bot Framework?](https://microsoft.github.io/botframework-solutions/overview/skills/)

![Diagrama de información general del Asistente virtual](../assets/images/bots/virtual-assistant/overview.png)

Las actividades de mensajes de texto se enrutar a las habilidades asociadas mediante el núcleo del Asistente virtual mediante un modelo [de](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) envío. 

## <a name="implementation-considerations"></a>Consideraciones de implementación

La decisión de agregar un asistente virtual puede incluir muchos determinantes y diferir para cada organización. Estos son los factores que admiten la implementación de un Asistente virtual para su organización:

- Un equipo central administra todas las experiencias de los empleados y tiene la capacidad de crear una experiencia de Asistente virtual y administrar las actualizaciones de la experiencia principal, incluida la adición de nuevas habilidades.
- Existen varias aplicaciones en todas las funciones empresariales o se espera que el número aumente en el futuro.
- Las aplicaciones existentes son personalizables, son propiedad de la organización y se pueden convertir en aptitudes para un Asistente virtual.
- El equipo central de experiencias de empleados puede influir en las personalizaciones de las aplicaciones existentes y proporcionar las instrucciones necesarias para integrar las aplicaciones existentes como aptitudes en la experiencia del Asistente virtual.

![El equipo central mantiene el asistente y los equipos de funciones empresariales aportan aptitudes](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Crear un Asistente virtual centrado en Teams

Microsoft ha publicado una plantilla [Visual Studio para](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) crear asistentes virtuales y habilidades. Con la Visual Studio, puedes crear un Asistente virtual, con tecnología de una experiencia basada en texto con compatibilidad con tarjetas enriquecciones limitadas con acciones. Hemos mejorado la plantilla Visual Studio base para incluir las capacidades de la plataforma de Microsoft Teams y mejorar las excelentes experiencias de aplicación de Teams. Algunas de las funcionalidades incluyen compatibilidad con tarjetas adaptables enriquecciones, módulos de tareas, chats de grupo o equipos y extensiones de mensajería. *Vea también*, [Tutorial: Ampliar el asistente virtual a Microsoft Teams.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)

![Diagrama de alto nivel de una solución de asistente virtual](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Agregar tarjetas adaptables al Asistente virtual

Para enviar las solicitudes correctamente, el Asistente virtual debe identificar el modelo DESA correcto y las habilidades correspondientes asociadas a él. Sin embargo, el mecanismo de envío no se puede usar para las actividades de acción de tarjeta, ya que es posible que el modelo DESA asociado con una habilidad no esté formado para los textos de acción de la tarjeta, ya que son palabras clave fijas predefinidas, no expresiones de un usuario.

Hemos resuelto esto insertando información de aptitudes en la carga de acción de la tarjeta. Todas las habilidades deben `skillId` insertarse en  `value` el campo de acciones de tarjeta. Esta es la mejor manera de asegurarse de que cada actividad de acción de tarjeta lleva la información de aptitudes relevante y el Asistente virtual puede usar esta información para el envío.

A continuación se muestra un ejemplo de datos de acción de tarjeta. Al proporcionar en el constructor nos aseguramos de que la información `skillId` de aptitudes esté siempre presente en las acciones de la tarjeta.

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

A continuación, presentamos `SkillCardActionData` la clase en la plantilla asistente virtual para extraer de la carga de acción de la `skillId` tarjeta.

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

A continuación se muestra un fragmento de código para extraer  `skillId` de los datos de la acción de la tarjeta. Lo implementamos como un método de extensión en la [clase Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)

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

El Asistente virtual puede controlar las interrupciones en los casos en los que un usuario intenta invocar una habilidad mientras otra habilidad está activa actualmente. hemos introducido y , en función de `TeamsSkillDialog` `TeamsSwitchSkillDialog` [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de Bot Framework, para permitir a los usuarios cambiar una experiencia de habilidades de acciones de tarjeta. Para controlar esta solicitud, el Asistente virtual solicita al usuario un mensaje de confirmación para cambiar de habilidades.

![Aviso de confirmación al cambiar a una nueva habilidad](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>Control de solicitudes de módulos de tareas

Para agregar capacidades de módulo de tareas a un Asistente virtual, se incluyen dos métodos adicionales en el controlador de actividad del Asistente virtual: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` . Estos métodos escuchan las actividades relacionadas con los módulos de tareas desde el Asistente virtual, identifican las aptitudes asociadas con la solicitud y reenvía la solicitud a la habilidad identificada. 

El reenvío de solicitudes se realiza mediante el  [método SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable) `PostActivityAsync` . Devuelve la respuesta según `InvokeResponse` la cual se analiza y se convierte en `TaskModuleResponse` .

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

Se sigue un enfoque similar para el envío de acciones de tarjeta y las respuestas del módulo de tareas. Los datos de acción de envío y captura del módulo de tareas se actualizan para incluir `skillId` . El método de extensión `GetSkillId` de actividad extrae de la carga que proporciona detalles sobre las `skillId` aptitudes que se deben invocar.

A continuación se muestra un fragmento de código para `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` métodos.

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

Además, todos los dominios de aptitudes deben incluirse en la sección del archivo de manifiesto del Asistente virtual para que los módulos de tareas invocados a través de una habilidad se `validDomains` represente correctamente.

### <a name="handling-collaborative-app-scopes"></a>Control de ámbitos de aplicaciones de colaboración

Las aplicaciones de Teams pueden existir en varios ámbitos, incluido el chat 1:1, el chat en grupo y los canales. La plantilla principal del Asistente virtual está diseñada para chats de 1:1. Como parte de la experiencia de incorporación, el Asistente virtual solicita a los usuarios el nombre y mantiene el estado del usuario. Dado que la experiencia de incorporación no es adecuada para los ámbitos de canal o chat en grupo, se ha quitado.

Las habilidades deben controlar las actividades en varios ámbitos (chat 1:1, chat en grupo y conversación de canal). Si alguno de estos ámbitos no es compatible, las aptitudes deben responder con un mensaje adecuado.

Se han agregado las siguientes funciones de procesamiento al núcleo del Asistente virtual:

- El Asistente virtual se puede invocar sin ningún mensaje de texto desde un canal o chat de grupo.
- Las provocaciones se limpian (es decir, quitan el @mention del bot) antes de enviar el mensaje al módulo de envío.

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

### <a name="handling-messaging-extensions"></a>Control de extensiones de mensajería

Los comandos de una extensión de mensajería se declaran en el archivo de manifiesto de la aplicación. La interfaz de usuario de extensión de mensajería funciona con esos comandos. Para que un Asistente virtual encienda un comando de extensión de mensajería (como una habilidad adjunta), el propio manifiesto de un asistente virtual debe contener esos comandos. Los comandos de un manifiesto de aptitudes individuales también deben agregarse al manifiesto del Asistente virtual. El identificador de comando proporciona información sobre una habilidad asociada anexando el identificador de aplicación de la habilidad a través de un separador ( `:` ).

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

Y, a continuación, se muestra el fragmento de código de archivo de manifiesto del Asistente virtual correspondiente.

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

Una vez que un usuario invoca los comandos, el Asistente virtual puede identificar una habilidad asociada analizando el identificador de comando, actualizando la actividad quitando el sufijo adicional ( ) del identificador de comando y reenvía a la habilidad `:<skill_id>` correspondiente. El código para una habilidad no necesita controlar el sufijo adicional, por lo tanto, se evitan conflictos entre identificadores de comandos entre aptitudes. Con este enfoque, todos los comandos de búsqueda y acción de una habilidad en todos los contextos ("redacción", "cuadro de comandos" y "mensaje") pueden ser desarrollados por un asistente virtual.

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

Algunas actividades de extensión de mensajería no incluyen el identificador de comando. Por ejemplo, contiene solo el valor de la acción de invocar `composeExtension/selectItem` pulsación. Para identificar las aptitudes asociadas, `skillId`  se adjunta a cada tarjeta de elemento mientras se forma una respuesta para `OnTeamsMessagingExtensionQueryAsync` . (Esto es similar al enfoque para [agregar tarjetas adaptables al Asistente virtual.](#add-adaptive-cards-to-your-virtual-assistant)

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>Ejemplo: convertir la plantilla de aplicación Libro a salón en una habilidad del Asistente virtual

[Reservar una](app-templates.md#book-a-room) sala es un bot de [Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios buscar y reservar rápidamente una sala de reuniones durante 30 (predeterminado), 60 o 90 minutos a partir de la hora actual. El bot de libro a sala se incluye en las conversaciones personales o 1:1.

![Asistente virtual con habilidad para "reservar una sala"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

A continuación se presentan los cambios delta introducidos para convertirlo en una habilidad que se puede adjuntar a un Asistente virtual. Se pueden seguir instrucciones similares para convertir cualquier bot v4 existente en una habilidad.

### <a name="skill-manifest"></a>Manifiesto de aptitudes

Un manifiesto de aptitudes es un archivo JSON que expone el punto de conexión de mensajería, el identificador, el nombre y otros metadatos relevantes de una habilidad (este manifiesto es diferente del manifiesto usado para la instalación de prueba de una aplicación en Microsoft Teams) Un asistente virtual requiere una ruta de acceso a este archivo como entrada para adjuntar una habilidad. Hemos agregado el siguiente manifiesto a la carpeta wwwroot del bot.

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

El modelo de envío del Asistente virtual se basa en los modelos DESA de habilidades adjuntas. El modelo de envío identifica la intención de cada actividad de texto y descubre las aptitudes asociadas a ella.

El Asistente virtual requiere el modelo DESA de habilidades (en formato) como entrada `.lu` mientras se adjunta una habilidad. El json de LUIS se puede convertir al `.lu` formato mediante la herramienta botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

El bot de libro a sala tiene dos comandos principales para los usuarios:

- `Book room`
- `Manage Favorites`

Hemos creado un modelo DEI para comprender estos dos comandos. Los secretos correspondientes deben rellenarse en `cognitivemodels.json` . Aquí se puede encontrar el archivo JSON [de](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) SUS correspondiente y este es el aspecto del `.lu` archivo correspondiente.

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

Con este enfoque, cualquier problema de comando de un usuario al Asistente virtual relacionado con o puede identificarse como un comando asociado con el bot de libro a sala y se reenvía `book room` `manage favorites` a esta habilidad.
Por otro lado, el bot de sala de libros debe usar el modelo DESA para comprender estos comandos si no están escritos tal como están (por ejemplo: `I want to manage my favorite rooms` ).

### <a name="multi-language-support"></a>Compatibilidad con varios idiomas

Para este ejemplo, solo hemos creado un modelo DEI CON la cultura inglesa. Puede crear modelos DESI correspondientes a otros idiomas y agregar entradas a `cognitivemodels.json` .

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

En paralelo, agregue el archivo `.lu` correspondiente en la ruta de acceso de luisFolder. La estructura de carpetas debe ser la siguiente:

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

El Asistente virtual `SetLocaleMiddleware` usa para identificar la configuración regional actual e invocar el modelo de distribución correspondiente. (La actividad de bot framework tiene un campo de configuración regional que usa este software intermedio). Te recomendamos que también uses lo mismo para tus habilidades. El bot book-a-room no usa este software intermedio y, en su lugar, obtiene la configuración regional de la entidad [clientInfo de](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)la actividad de Bot Framework.

### <a name="claim-validation"></a>Validación de notificación

Hemos agregado [claimsValidator para](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) restringir a los autores de llamadas a la habilidad. Para permitir que un asistente virtual llame a esta habilidad, rellena la matriz con el id. de aplicación de ese asistente `AllowedCallers` `appsettings` virtual en particular.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

La matriz de autores de llamadas permitida puede restringir qué aptitudes pueden tener acceso los consumidores. Agregue una sola `*` entrada a esta matriz para aceptar llamadas de cualquier consumidor de aptitudes.

```
"AllowedCallers": [ "*" ],
```
Puede encontrar documentación detallada para agregar la validación de notificaciones a una habilidad [aquí.](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)

### <a name="card-refresh-limitation"></a>Limitación de actualización de tarjetas

La actualización de actividad (actualización de tarjeta) aún no se admite a través del Asistente virtual[(problema de GitHub).](https://github.com/microsoft/botbuilder-dotnet/issues/3686) Por lo tanto, hemos reemplazado todas las llamadas de actualización de tarjeta ( `UpdateActivityAsync` ) con la publicación de nuevas llamadas de tarjeta( `SendActivityAsync` ).

### <a name="card-actions-and-task-module-flows"></a>Acciones de tarjeta y flujos de módulos de tareas

Para reenviar actividades de la acción de la tarjeta o del módulo de tareas a una habilidad asociada, esta debe `skillId` insertarse en ella.
La acción de la tarjeta de bot de libro a sala, la captura del módulo de tareas y las cargas de acción de envío se modifican para que `skillId` contengan como parámetro. 

Para obtener más información, [consulte esta](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) sección de esta documentación.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Controlar actividades desde el ámbito de canal o chat en grupo

El bot de libro a salón está diseñado solo para chats privados (ámbito personal/1:1). Dado que hemos personalizado el Asistente virtual para admitir ámbitos de canal y chat en grupo, es posible que se invoque al Asistente virtual desde estos ámbitos y, por lo tanto, el bot de libro a salón puede obtener actividades para la misma. Por lo tanto, el bot Book-a-room se personaliza para controlar esas actividades. La comprobación se ha puesto en métodos del controlador de actividad del bot de Libro `OnMessageActivityAsync` a sala.

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

También puede aprovechar las aptitudes existentes del repositorio de soluciones de [Bot Framework o](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) crear una nueva habilidad desde cero. Puede encontrar tutoriales para las versiones posteriores [aquí.](https://microsoft.github.io/botframework-solutions/overview/skills/) Consulte la documentación [del](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   Asistente virtual y la arquitectura de habilidades.

## <a name="sample-code-to-get-started"></a>Código de ejemplo para empezar

- [Plantilla de Visual Studio actualizada](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [Código de habilidades de bot de libro a sala](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a>Limitaciones conocidas del Asistente virtual

- **EndOfConversation**. Una habilidad debe enviar una `endOfConversation` actividad cuando termina una conversación. base de esta actividad, un Asistente virtual termina el contexto con esa habilidad en particular y vuelve al contexto (raíz) del Asistente virtual. Para el bot de libro a sala, no hay ningún estado claro en el que se pueda finalizar la conversación. Por lo tanto, no hemos enviado desde el bot libro a sala y cuando el usuario desea volver al contexto raíz, simplemente puede `endOfConversation` hacerlo por `start over` comando.
- **Actualización de la tarjeta.** Las actualizaciones de tarjetas aún no se admiten a través del Asistente virtual.
- **Extensiones de mensajería.:**
  - Actualmente, un Asistente virtual puede admitir un máximo de diez comandos para extensiones de mensajería.
  - La configuración de extensiones de mensajería no está en el ámbito de comandos individuales, sino de toda la extensión en sí. Esto limita la configuración de cada habilidad individual a través del Asistente virtual.
  - Los IDs de comandos de extensiones de mensajería tienen una longitud máxima de [64](../resources/schema/manifest-schema.md#composeextensions) caracteres y se usarán 37 caracteres para insertar información de aptitudes. Por lo tanto, las restricciones actualizadas para el identificador de comando están limitadas a 27 caracteres.
>
>
