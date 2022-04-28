---
title: Crear un asistente virtual
description: Aprenda a crear Virtual Assistant bot para Microsoft Teams mediante ejemplos de código y fragmentos de código con características como tarjetas adaptables; control de interrupciones, solicitudes de módulos de tareas, ámbitos de aplicación de colaboración y extensiones de mensajes; uso del manifiesto de aptitud; Compatibilidad con varios lenguajes, validación de notificaciones, integración de LUIS y modo.
ms.localizationpriority: medium
ms.topic: how-to
keywords: bots del asistente virtual de teams
ms.openlocfilehash: e473fd8166be6285ec90d78401b1df028d81b5b0
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104108"
---
# <a name="create-virtual-assistant"></a>Crear un asistente virtual

Virtual Assistant es una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida y mantener el control total de la experiencia del usuario, la personalización de marca de la organización y los datos necesarios. La [plantilla principal Virtual Assistant](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) es el bloque de creación básico que reúne las tecnologías de Microsoft necesarias para crear un Virtual Assistant, incluidos bot [framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/) y [QnA Maker](https://www.qnamaker.ai/). También reúne las funcionalidades esenciales, como el registro de aptitudes, las cuentas vinculadas, la intención conversacional básica para ofrecer una gama de interacciones y experiencias sin problemas a los usuarios. Además, las funcionalidades de plantilla incluyen ejemplos completos de [aptitudes conversacionales](https://microsoft.github.io/botframework-solutions/overview/skills) reutilizables.  Las aptitudes individuales se integran en una solución Virtual Assistant para habilitar varios escenarios. Con el SDK de Bot Framework, las aptitudes se presentan en forma de código fuente, lo que le permite personalizar y ampliar según sea necesario. Para obtener más información sobre las aptitudes de Bot Framework, consulte [¿Qué es una aptitud de Bot Framework](https://microsoft.github.io/botframework-solutions/overview/skills/)? Este documento le guía sobre Virtual Assistant consideraciones de implementación para las organizaciones, cómo crear un Teams centrado en Virtual Assistant, ejemplo relacionado, ejemplo de código y limitaciones de Virtual Assistant.
En la imagen siguiente se muestra la información general del asistente virtual:

![diagrama de información general de Virtual Assistant](../assets/images/bots/virtual-assistant/overview.png)

Las actividades de mensajes de texto se enrutan a aptitudes asociadas por el núcleo de Virtual Assistant mediante un modelo [de distribución](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true).

## <a name="implementation-considerations"></a>Consideraciones de implementación

La decisión de agregar un Virtual Assistant incluye muchos determinantes y diferencias para cada organización. Los factores auxiliares de una implementación de Virtual Assistant para su organización son los siguientes:

* Un equipo central administra todas las experiencias de los empleados. Tiene la capacidad de crear una experiencia Virtual Assistant y administrar las actualizaciones de la experiencia principal, incluida la incorporación de nuevas aptitudes.
* Existen varias aplicaciones entre las funciones empresariales y se espera que el número crezca en el futuro.
* Las aplicaciones existentes son personalizables, son propiedad de la organización y se convierten en aptitudes para un Virtual Assistant.
* El equipo central de experiencias de empleados puede influir en las personalizaciones de las aplicaciones existentes. También proporciona las instrucciones necesarias para integrar las aplicaciones existentes como aptitudes en Virtual Assistant experiencia.

En la imagen siguiente se muestran las funciones empresariales de Virtual Assistant:

![El equipo central mantiene el asistente y los equipos de funciones empresariales aportan aptitudes](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Creación de un Virtual Assistant centrado en Teams

Microsoft ha publicado una [plantilla de Microsoft Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) para crear asistentes virtuales y aptitudes. Con la plantilla de Visual Studio, puede crear un Virtual Assistant, con tecnología de una experiencia basada en texto con compatibilidad con tarjetas enriquecidas limitadas con acciones. Hemos mejorado la plantilla base de Visual Studio para incluir funcionalidades de plataforma de Microsoft Teams y mejorar las experiencias de la aplicación Teams. Algunas de las funcionalidades incluyen compatibilidad con tarjetas adaptables enriquecidas, módulos de tareas, equipos o chats de grupo y extensiones de mensajes. Para obtener más información sobre cómo ampliar Virtual Assistant a Microsoft Teams, vea [Tutorial: Extender el Virtual Assistant a Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).
En la imagen siguiente se muestra el diagrama de alto nivel de una solución de Virtual Assistant:

![Diagrama de alto nivel de una solución de Virtual Assistant](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Agregar tarjetas adaptables a la Virtual Assistant

Para enviar solicitudes correctamente, el Virtual Assistant debe identificar el modelo de LUIS correcto y la aptitud correspondiente asociada a él. Sin embargo, el mecanismo de distribución no se puede usar para las actividades de acción de tarjeta, ya que el modelo de LUIS asociado a una aptitud se entrena para textos de acción de tarjeta. Los textos de acción de tarjeta son palabras clave fijas, predefinidas y no comentadas por un usuario.

Este inconveniente se resuelve insertando información de aptitudes en la carga de la acción de la tarjeta. Cada aptitud debe insertarse `skillId` en el  `value` campo de acciones de tarjeta. Debe asegurarse de que cada actividad de acción de tarjeta lleva la información de aptitud pertinente y Virtual Assistant puede usar esta información para el envío.

Debe proporcionar `skillId` en el constructor para asegurarse de que la información de aptitud siempre está presente en las acciones de tarjeta.
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

A continuación, `SkillCardActionData` se introduce la clase de la plantilla Virtual Assistant para extraer `skillId` de la carga de la acción de la tarjeta.
En la sección siguiente se muestra un fragmento de código para extraer  `skillId` de la carga de la acción de tarjeta:

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

La implementación se realiza mediante un método de extensión en la clase [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .
En la sección siguiente se muestra un fragmento de código que se va a extraer  `skillId` de los datos de acción de tarjeta:

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

### <a name="handle-interruptions"></a>Controlar interrupciones

Virtual Assistant puede controlar interrupciones en los casos en los que un usuario intenta invocar una aptitud mientras otra aptitud está activa actualmente. `TeamsSkillDialog`, y `TeamsSwitchSkillDialog`se introducen en función de [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs) de Bot Framework. Permiten a los usuarios cambiar una experiencia de aptitud de las acciones de tarjeta. Para controlar esta solicitud, el Virtual Assistant solicita al usuario un mensaje de confirmación para cambiar de aptitudes:

![Mensaje de confirmación al cambiar a una nueva aptitud](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Control de solicitudes de módulo de tareas

Para agregar funcionalidades de módulo de tareas a un Virtual Assistant, se incluyen dos métodos adicionales en el controlador de actividad Virtual Assistant: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync`. Estos métodos escuchan actividades relacionadas con módulos de tareas desde Virtual Assistant, identifican la aptitud asociada a la solicitud y reenvía la solicitud a la aptitud identificada.

El reenvío de solicitudes se realiza a través del método [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)`PostActivityAsync`. Devuelve la respuesta como `InvokeResponse` que se analiza y se convierte en `TaskModuleResponse` .

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

Se sigue un enfoque similar para el envío de acciones de tarjeta y las respuestas del módulo de tareas. Los datos de la acción de captura y envío del módulo de tareas se actualizan para incluir `skillId`.
El método `GetSkillId` De extensión de actividad extrae `skillId` de la carga, que proporciona detalles sobre la aptitud que se debe invocar.

El fragmento de código para `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` los métodos se proporcionan en la sección siguiente:

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

Además, debe incluir todos los dominios de aptitud en la `validDomains` sección del archivo de manifiesto de Virtual Assistant para que los módulos de tareas invocados a través de una aptitud se representen correctamente.

### <a name="handle-collaborative-app-scopes"></a>Control de ámbitos de aplicaciones colaborativas

Teams aplicaciones pueden existir en varios ámbitos, incluido el chat 1:1, el chat en grupo y los canales. La plantilla de Virtual Assistant principal está diseñada para chats 1:1. Como parte de la experiencia de incorporación Virtual Assistant solicita a los usuarios el nombre y mantiene el estado del usuario. Dado que la experiencia de incorporación no es adecuada para el chat en grupo o los ámbitos de canal, se ha quitado.

Las aptitudes deben controlar las actividades en varios ámbitos, como el chat 1:1, el chat en grupo y la conversación de canal. Si no se admite alguno de estos ámbitos, las aptitudes deben responder con un mensaje adecuado.

Se han agregado las siguientes funciones de procesamiento a Virtual Assistant núcleo:

* Virtual Assistant se puede invocar sin ningún mensaje de texto de un chat o canal de grupo.
* Las articulaciones se limpian antes de enviar el mensaje al módulo de distribución. Por ejemplo, quite la @mention necesaria del bot.

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

### <a name="handle-message-extensions"></a>Control de extensiones de mensaje

Los comandos de una extensión de mensaje se declaran en el archivo de manifiesto de la aplicación. La interfaz de usuario de la extensión de mensaje funciona con esos comandos. Para que un Virtual Assistant active un comando de extensión de mensaje como una aptitud adjunta, el propio manifiesto de un Virtual Assistant debe contener esos comandos. Debe agregar los comandos del manifiesto de una aptitud individual al manifiesto del Virtual Assistant. El identificador de comando proporciona información sobre una aptitud asociada anexando el identificador de aplicación de la aptitud a través de un separador `:`.

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
    ....   
```

El fragmento de código de archivo de manifiesto correspondiente Virtual Assistant se muestra en la sección siguiente:

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

Una vez que un usuario invoca los comandos, el Virtual Assistant puede identificar una aptitud asociada analizando el identificador de comando, actualizando la actividad quitando el sufijo `:<skill_id>` adicional del identificador de comando y reenviéndolo a la aptitud correspondiente. El código de una aptitud no necesita controlar el sufijo adicional. Por lo tanto, se evitan los conflictos entre los identificadores de comando entre las aptitudes. Con este enfoque, todos los comandos de búsqueda y acción de una aptitud dentro de todos los contextos, como **compose**, **commandBox** y **message**, tienen la tecnología de un Virtual Assistant.

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

Algunas actividades de extensión de mensaje no incluyen el identificador de comando. Por ejemplo, `composeExtension/selectItem` contiene solo el valor de la acción de invocación de pulsación. Para identificar la aptitud asociada, `skillId`  se adjunta a cada tarjeta de elemento al formar una respuesta para `OnTeamsMessagingExtensionQueryAsync`. Esto es similar al enfoque para [agregar tarjetas adaptables a la Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).

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

En el ejemplo siguiente se muestra cómo convertir la plantilla de aplicación Book-a-room en una aptitud Virtual Assistant: Book-a-room es un Microsoft Teams que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30, 60 o 90 minutos a partir de la hora actual. El tiempo predeterminado es de 30 minutos. El bot book-a-room se limita a las conversaciones personales o 1:1.
En la imagen siguiente se muestra un Virtual Assistant con una aptitud **reservar una sala**:

![Virtual Assistant con una aptitud de "reservar una habitación"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

A continuación se muestran los cambios diferenciales introducidos para convertirlo en una aptitud que se adjunta a un Virtual Assistant. Se siguen directrices similares para convertir cualquier bot v4 existente en una aptitud.

### <a name="skill-manifest"></a>Manifiesto de aptitud

Un manifiesto de aptitud es un archivo JSON que expone el punto de conexión de mensajería, el identificador, el nombre y otros metadatos pertinentes de una aptitud. Este manifiesto es diferente del manifiesto usado para transferir localmente una aplicación en Microsoft Teams. Un Virtual Assistant requiere una ruta de acceso a este archivo como entrada para adjuntar una aptitud. Hemos agregado el siguiente manifiesto a la carpeta wwwroot del bot.

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

el modelo de distribución de Virtual Assistant se basa en los modelos de LUIS de las aptitudes adjuntas. El modelo de distribución identifica la intención de cada actividad de texto y detecta la aptitud asociada a ella.

Virtual Assistant requiere el modelo de LUIS de la aptitud en `.lu` formato de entrada al adjuntar una aptitud. LUIS json se convierte al `.lu` formato mediante la herramienta botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

El bot book-a-room tiene dos comandos principales para los usuarios:

* `Book room`
* `Manage Favorites`

Hemos creado un modelo de LUIS mediante la comprensión de estos dos comandos. Los secretos correspondientes deben rellenarse en `cognitivemodels.json`. El archivo JSON de LUIS correspondiente se encuentra [aquí](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).
El archivo correspondiente `.lu` se muestra en la sección siguiente:

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

Con este enfoque, cualquier comando emitido por un usuario para Virtual Assistant relacionado con `book room` o `manage favorites` se identifica como un comando asociado al `Book-a-room` bot y se reenvía a esta aptitud.
Por otro lado, `Book-a-room room` el bot debe usar el modelo de LUIS para comprender estos comandos si no están escritos completos. Por ejemplo: `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Compatibilidad con varios idiomas

Por ejemplo, se crea un modelo de LUIS con solo referencia cultural en inglés. Puede crear modelos de LUIS correspondientes a otros idiomas y agregar entrada a `cognitivemodels.json`.

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

Para modificar el `languages` parámetro, actualice el comando botskills de la siguiente manera:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Virtual Assistant usa `SetLocaleMiddleware` para identificar la configuración regional actual e invocar el modelo de distribución correspondiente. La actividad de Bot Framework tiene un campo de configuración regional que usa este middleware. También puede usar lo mismo para su habilidad. El bot book-a-room no usa este middleware y, en su lugar, obtiene la configuración regional de la [entidad clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo) de la actividad de Bot Framework.

### <a name="claim-validation"></a>Validación de notificaciones

Hemos agregado [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) para restringir a los autores de llamadas a la aptitud. Para permitir que un Virtual Assistant llame a esta aptitud, rellene `AllowedCallers` la matriz de `appsettings` con el identificador de aplicación de ese Virtual Assistant determinado.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

La matriz de llamadores permitidos puede restringir qué consumidores de aptitudes pueden acceder a la aptitud. Agregue una entrada `*` única a esta matriz para aceptar llamadas de cualquier consumidor de aptitudes.

```
"AllowedCallers": [ "*" ],
```

Para obtener más información sobre cómo agregar la validación de notificaciones a una aptitud, vea [Agregar validación de notificaciones a la aptitud](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).

### <a name="limitation-of-card-refresh"></a>Limitación de la actualización de tarjetas

La actividad de actualización, como la actualización de tarjetas, no se admite aún a través de Virtual Assistant ([problema de GitHub](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Por lo tanto, hemos reemplazado todas las llamadas de actualización de tarjetas `UpdateActivityAsync` por publicar nuevas llamadas de `SendActivityAsync`tarjeta .

### <a name="card-actions-and-task-module-flows"></a>Acciones de tarjeta y flujos de módulo de tareas

Para reenviar las actividades de la acción de tarjeta o del módulo de tareas a una aptitud asociada, la aptitud debe insertarse `skillId` en ella.
`Book-a-room` La acción de la tarjeta bot, la captura del módulo de tareas y las cargas de acción de envío se modifican para que contengan `skillId` como parámetro.

Para obtener más información, consulte [esta](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) sección de esta documentación.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Control de actividades desde el ámbito de canal o chat de grupo

`Book-a-room bot` está diseñado para chats privados, como solo para ámbitos personales o 1:1. Dado que hemos personalizado Virtual Assistant para admitir ámbitos de canal y chat de grupo, el Virtual Assistant debe invocarse desde los ámbitos del canal y, por tanto, `Book-a-room` el bot debe obtener actividades para el mismo ámbito. Por lo tanto, `Book-a-room`el bot se personaliza para controlar esas actividades. Puede encontrar los métodos de protección `OnMessageActivityAsync` del controlador de `Book-a-room` actividad del bot.

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

También puede aprovechar las aptitudes existentes desde el [repositorio de Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) o crear una nueva aptitud desde cero. Para crear una nueva aptitud, consulte [tutoriales para crear una nueva aptitud](https://microsoft.github.io/botframework-solutions/overview/skills/). Para obtener Virtual Assistant y documentación sobre la arquitectura de aptitudes, consulte [Virtual Assistant y arquitectura de aptitudes](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).  

## <a name="limitations-of-virtual-assistant"></a>Limitaciones de Virtual Assistant

* **EndOfConversation**: una aptitud debe enviar una `endOfConversation` actividad cuando finaliza una conversación. En función de la actividad, un Virtual Assistant finaliza el contexto con esa aptitud determinada y vuelve al contexto raíz de Virtual Assistant. En el caso del bot book-a-room, no hay un estado claro en el que se termine la conversación. Por lo tanto, no hemos enviado `endOfConversation` desde el `Book-a-room` bot y cuando el usuario quiere volver al contexto raíz, simplemente puede hacerlo por `start over` comando.  
* **Actualización de tarjetas**: la actualización de tarjetas aún no se admite a través de Virtual Assistant.  
* **Extensiones de mensaje**:
  * Actualmente, un Virtual Assistant puede admitir un máximo de diez comandos para las extensiones de mensaje.
  * La configuración de las extensiones de mensaje no se limita a comandos individuales, sino a toda la extensión. Esto limita la configuración de cada aptitud individual a través de Virtual Assistant.
  * Los identificadores de comando de extensiones de mensaje tienen una longitud máxima de [64 caracteres](../resources/schema/manifest-schema.md#composeextensions) y se usan 37 caracteres para insertar información de aptitudes. Por lo tanto, las restricciones actualizadas para el identificador de comando están limitadas a 27 caracteres.

También puede aprovechar las aptitudes existentes desde el [repositorio de Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) o crear una nueva aptitud desde cero. Puede encontrar tutoriales para más adelante [aquí](https://microsoft.github.io/botframework-solutions/overview/skills/). Consulte la [documentación](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) para obtener Virtual Assistant y la arquitectura de aptitudes.

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| Plantilla de Visual Studio actualizada | Plantilla personalizada para admitir las funcionalidades de los equipos. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| Código de aptitud del bot book-a-room | Le permite encontrar y reservar rápidamente una sala de reuniones sobre la marcha. | [Ver](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |

## <a name="see-also"></a>Consulte también

* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Libro a habitación](app-templates.md#app-template-code-samples)
* [bot de Microsoft Teams](../bots/what-are-bots.md)
