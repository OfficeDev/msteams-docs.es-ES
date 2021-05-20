---
title: Crear un asistente virtual
description: Cómo crear bot virtual asistente y habilidades para su uso en Microsoft Teams
localization_priority: Normal
ms.topic: how-to
keywords: equipos de robots asistentes virtuales
ms.openlocfilehash: 072d9cb5742cd39101587cad32e3048bd36cc1d8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566876"
---
# <a name="create-virtual-assistant"></a>Crear un asistente virtual 

Virtual Assistant es una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida mientras mantiene el control total de la experiencia del usuario, la personalización de marca de la organización y los datos necesarios. La [plantilla principal de Virtual Assistant](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) es el building block básico que reúne las tecnologías de Microsoft necesarias para crear un Asistente virtual, incluido el SDK de Bot [Framework,](https://github.com/microsoft/botframework-sdk) [Language Understanding (LUIS)](https://www.luis.ai/)y [QnA Maker.](https://www.qnamaker.ai/) También reúne las capacidades esenciales, incluyendo el registro de habilidades, cuentas vinculadas, intención conversacional básica para ofrecer una gama de interacciones y experiencias sin problemas a los usuarios. Además, las capacidades de la plantilla incluyen ejemplos enriquecidos de [habilidades](https://microsoft.github.io/botframework-solutions/overview/skills)conversacionales reutilizables.  Las habilidades individuales se integran en una solución de Virtual Assistant para habilitar múltiples escenarios. Con el SDK de Bot Framework, las habilidades se presentan en forma de código fuente, lo que le permite personalizar y ampliar según sea necesario. Para obtener más información sobre las habilidades de Bot Framework, consulte [Qué es una habilidad de Bot Framework](https://microsoft.github.io/botframework-solutions/overview/skills/). Este documento le guía sobre las consideraciones de implementación del Asistente virtual para las organizaciones, cómo crear un Asistente virtual centrado Teams, ejemplo relacionado, ejemplo de código y limitaciones del Asistente virtual.
La siguiente imagen muestra la descripción general del asistente virtual:

![Diagrama de visión general de Virtual Assistant](../assets/images/bots/virtual-assistant/overview.png)

Las actividades de mensajes de texto se enrutan a las habilidades asociadas por el núcleo del Asistente virtual mediante un modelo [de envío.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) 

## <a name="implementation-considerations"></a>Consideraciones de implementación

La decisión de agregar un Asistente Virtual incluye muchos determinantes y difiere para cada organización. Los factores auxiliares de una implementación de Virtual Assistant para su organización son los siguientes:

* Un equipo central administra todas las experiencias de los empleados. Tiene la capacidad de crear una experiencia de Asistente Virtual y administrar actualizaciones de la experiencia principal, incluida la adición de nuevas habilidades.
* Existen varias aplicaciones entre las funciones empresariales y se espera que el número crezca en el futuro.
* Las aplicaciones existentes son personalizables, propiedad de la organización, y se convierten en habilidades para un Asistente Virtual.
* El equipo central de experiencias de empleados puede influir en las personalizaciones de las aplicaciones existentes. También proporciona la orientación necesaria para integrar las aplicaciones existentes como habilidades en la experiencia de Virtual Assistant.

La siguiente imagen muestra las funciones empresariales de Virtual Assistant: 

![El equipo central mantiene al asistente y los equipos de funciones empresariales aportan habilidades](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Crear un asistente virtual centrado en la Teams

Microsoft ha publicado una [plantilla de Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) para crear asistentes virtuales y habilidades. Con la plantilla Visual Studio, puede crear un Asistente Virtual, impulsado por una experiencia basada en texto con soporte para tarjetas enriquecidas limitadas con acciones. Hemos mejorado la plantilla base Visual Studio para incluir Microsoft Teams capacidades de plataforma y potenciar grandes experiencias de Teams aplicación. Algunas de las capacidades incluyen compatibilidad con tarjetas adaptables enriquecidas, módulos de tareas, chats de equipos o grupos y extensiones de mensajería. Para obtener más información sobre cómo ampliar Virtual Assistant a Microsoft Teams, consulte [Tutorial: Extender el asistente virtual a Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).    
La siguiente imagen muestra el diagrama de alto nivel de una solución de Virtual Assistant:

![Diagrama de alto nivel de una solución de Virtual Assistant](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Añade tarjetas adaptables a tu Asistente Virtual

Para enviar solicitudes correctamente, el Asistente virtual debe identificar el modelo de LUIS correcto y la habilidad correspondiente asociada a él. Sin embargo, el mecanismo de envío no se puede usar para actividades de acción de tarjeta, ya que el modelo de LUIS asociado a una habilidad está entrenado para textos de acción de cartas. Los textos de acción de la tarjeta son palabras clave fijas, predefinidas y no se comentan desde un usuario.

Este inconveniente se resuelve esto incorporando información de habilidad en la carga útil de la acción de la tarjeta. Cada habilidad debe integrarse `skillId` en el campo de las acciones de  `value` cartas. Debe asegurarse de que cada actividad de acción de la tarjeta lleva la información de habilidad relevante, y Virtual Assistant puede utilizar esta información para el envío.

Debe proporcionar `skillId` en el constructor para asegurarse de que la información de habilidad siempre está presente en las acciones de la tarjeta.
En la siguiente sección se muestra un código de ejemplo de datos de acción de tarjeta:
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

A continuación, `SkillCardActionData` la clase de la plantilla Asistente virtual se introduce para extraer de la carga útil de la acción `skillId` de la tarjeta.
En la siguiente sección se muestra un fragmento de código para extraer  `skillId` de la carga útil de la acción de la tarjeta:

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

La implementación se realiza mediante un método de extensión en la [clase Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)
En la siguiente sección se muestra un fragmento de código para extraer  `skillId` de los datos de acción de la tarjeta:

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

### <a name="handle-interruptions"></a>Interrupciones del mango

Virtual Assistant puede controlar las interrupciones en los casos en que un usuario intenta invocar una habilidad mientras otra habilidad está activa actualmente. `TeamsSkillDialog`, y `TeamsSwitchSkillDialog` se introducen en función del [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [el SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de Bot Framework. Permiten a los usuarios cambiar una experiencia de habilidad de las acciones de la tarjeta. Para controlar esta solicitud, el Asistente virtual solicita al usuario un mensaje de confirmación para cambiar las habilidades:

![Solicitud de confirmación al cambiar a una nueva habilidad](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Gestionar las solicitudes de módulos de tareas

Para agregar capacidades de módulo de tareas a un Asistente virtual, se incluyen dos métodos adicionales en el controlador de actividad Asistente virtual: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` . Estos métodos escuchan las actividades relacionadas con el módulo de tareas desde Virtual Assistant, identifican la habilidad asociada con la solicitud y reenvían la solicitud a la habilidad identificada. 

El reenvío de solicitudes se realiza a través del método [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync` . Devuelve la respuesta como `InvokeResponse` la que se analiza y se convierte en `TaskModuleResponse` .


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

Se sigue un enfoque similar para el envío de acciones de tarjeta y las respuestas del módulo de tareas. Los datos de acción de captura y envío del módulo de tareas se actualizan para incluir `skillId` . El método extensión de actividad `GetSkillId` extrae `skillId` de la carga útil que proporciona detalles sobre la habilidad que debe invocarse.

El fragmento de código `OnTeamsTaskModuleFetchAsync` para y métodos se dan en la siguiente `OnTeamsTaskModuleSubmitAsync` sección:

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

Además, debe incluir todos los dominios de habilidad de la sección en el `validDomains` archivo de manifiesto de Virtual Assistant para que los módulos de tareas se invoquen a través de un renderizado de habilidades correctamente.

### <a name="handle-collaborative-app-scopes"></a>Controlar los ámbitos de aplicación colaborativa

Teams aplicaciones pueden existir en varios ámbitos, incluyendo chat 1:1, chat de grupo y canales. La plantilla principal de Virtual Assistant está diseñada para chats 1:1. Como parte de la experiencia de incorporación, Virtual Assistant solicita nombre a los usuarios y mantiene el estado del usuario. Dado que esa experiencia de incorporación no es adecuada para el chat de grupo o los ámbitos de canal se ha eliminado.

Las habilidades deben manejar actividades en múltiples ámbitos, como chat 1:1, chat en grupo y conversación de canal. Si no se admite alguno de estos ámbitos, las habilidades deben responder con un mensaje adecuado.

Las siguientes funciones de procesamiento se han agregado al núcleo de Virtual Assistant:

* Virtual Assistant se puede invocar sin ningún mensaje de texto de un chat o canal de grupo.
* Las articulaciones se limpian antes de enviar el mensaje al módulo de envío. Por ejemplo, quite la @mention necesaria del bot.

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

### <a name="handle-messaging-extensions"></a>Manejar extensiones de mensajería

Los comandos de una extensión de mensajería se declaran en el archivo de manifiesto de la aplicación. La interfaz de usuario de la extensión de mensajería está alimentada por esos comandos. Para que un Asistente virtual encienda un comando de extensión de mensajería como una habilidad adjunta, el propio manifiesto de un Asistente virtual debe contener esos comandos. Debe agregar los comandos del manifiesto de una habilidad individual al manifiesto del Asistente virtual. El identificador de comando proporciona información sobre una habilidad asociada añadiendo el ID de aplicación de la habilidad a través de un `:` separador.

El fragmento de código del archivo de manifiesto de una habilidad se muestra en la siguiente sección:

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

El fragmento de código de archivo de manifiesto del Asistente virtual correspondiente se muestra en la siguiente sección:

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

Una vez invocados los comandos por un usuario, el Asistente virtual puede identificar una habilidad asociada analizando el ID de comando, actualizar la actividad quitando el sufijo adicional `:<skill_id>` del ID de comando y reenviarlo a la habilidad correspondiente. El código de una habilidad no necesita manejar el sufijo adicional. Por lo tanto, se evitan los conflictos entre los dedo de mando a través de habilidades. Con este enfoque, todos los comandos de búsqueda y acción de una habilidad dentro de todos los contextos, como **componer,** **commandBox** y **mensaje,** están alimentados por un Asistente Virtual.

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

Algunas actividades de extensión de mensajería no incluyen el identificador de comando. Por ejemplo, `composeExtension/selectItem` contiene solo el valor de la acción de toque invoke. Para identificar la habilidad asociada, `skillId`  se adjunta a cada carta de artículos mientras se forma una respuesta para `OnTeamsMessagingExtensionQueryAsync` . Esto es similar al enfoque para [agregar tarjetas adaptables a su Asistente Virtual.](#add-adaptive-cards-to-your-virtual-assistant)

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

En el ejemplo siguiente se muestra cómo convertir la plantilla de aplicación Reservar una habitación en una habilidad asistente virtual: Reservar una habitación es un Microsoft Teams que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30, 60 o 90 minutos a partir de la hora actual. El tiempo predeterminado es de 30 minutos. El bot Book-a-room se limita a conversaciones personales o 1:1. La siguiente imagen muestra un Asistente Virtual con un libro una habilidad **de habitación:**

![Asistente virtual con una habilidad de "reservar una habitación"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Los siguientes son los cambios delta introducidos para convertirlo en una habilidad que se adjunta a un Asistente Virtual. Se siguen directrices similares para convertir cualquier bot v4 existente en una habilidad.

### <a name="skill-manifest"></a>Manifiesto de habilidad

Un manifiesto de habilidad es un archivo JSON que expone el punto de conexión de mensajería, el IDENTIFICADOR, el nombre y otros metadatos relevantes de una habilidad. Este manifiesto es diferente del manifiesto utilizado para descargar una aplicación en Microsoft Teams. Un Asistente virtual requiere una ruta de acceso a este archivo como entrada para asociar una habilidad. Hemos agregado el siguiente manifiesto a la carpeta wwwroot del bot.

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

El modelo de envío de Virtual Assistant se basa en los modelos de LUIS de habilidades adjuntas. El modelo de envío identifica la intención de cada actividad de texto y descubre la habilidad asociada a ella.

Virtual Assistant requiere el modelo de LUIS de habilidad en `.lu` formato como entrada mientras se adjunta una habilidad. LUIS json se convierte en `.lu` formato mediante la herramienta botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Book-a-room bot tiene dos comandos principales para los usuarios:

- `Book room`
- `Manage Favorites`

Hemos creado un modelo de LUIS mediante la comprensión de estos dos comandos. Los secretos correspondientes deben rellenarse en `cognitivemodels.json` . El archivo JSON de LUIS correspondiente se encuentra [aquí.](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)
El archivo correspondiente `.lu` se muestra en la siguiente sección:

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

Con este enfoque, cualquier comando emitido por un usuario al Asistente virtual relacionado con `book room` o se identifica como un comando asociado con bot y se `manage favorites` `Book-a-room` reenvía a esta habilidad.
Por otro lado, el bot debe usar el `Book-a-room room` modelo de LUIS para comprender estos comandos si no están escritos completos. Por ejemplo: `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Soporte multilingüe

Por ejemplo, se crea un modelo de LUIS con solo la referencia cultural en inglés. Puede crear modelos de LUIS correspondientes a otros idiomas y agregar entrada a `cognitivemodels.json` .

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

En paralelo, agregue el archivo correspondiente `.lu` en la ruta luisFolder. La estructura de carpetas debe ser la siguiente:

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Para modificar `languages` el parámetro, actualice el comando botskills de la siguiente manera:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Virtual Assistant utiliza `SetLocaleMiddleware` para identificar la configuración regional actual e invocar el modelo de envío correspondiente. La actividad del marco de bots tiene un campo de configuración regional que usa este middleware. También puedes usar lo mismo para tu habilidad. Book-a-room bot no usa este middleware y, en su lugar, obtiene la configuración regional de la [entidad clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de la actividad de marco de trabajo de Bot.

### <a name="claim-validation"></a>Validación de reclamaciones

Hemos agregado [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) para restringir a los llamadores a la habilidad. Para permitir que un Asistente virtual llame a esta habilidad, rellene `AllowedCallers` la matriz con el identificador de aplicación de ese Asistente virtual en `appsettings` particular.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

La matriz de llamadas permitidas puede restringir qué habilidades pueden acceder los consumidores a la habilidad. Agregue una sola entrada `*` a esta matriz, para aceptar llamadas de cualquier consumidor de habilidades.

```
"AllowedCallers": [ "*" ],
```

Para obtener más información sobre cómo agregar validación de notificaciones a una habilidad, consulte [Agregar validación de notificaciones a la habilidad](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).

### <a name="limitation-of-card-refresh"></a>Limitación de la actualización de la tarjeta 

La actividad de actualización, como la actualización de tarjetas, aún no se admite a través de Virtual Assistant[(problema de github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686) Por lo tanto, hemos reemplazado todas las llamadas de actualización de tarjetas `UpdateActivityAsync` con la publicación de nuevas llamadas de `SendActivityAsync` tarjeta.

### <a name="card-actions-and-task-module-flows"></a>Acciones de tarjetas y flujos de módulos de tareas

Para reenviar las actividades de la acción de la carta o del módulo de tareas a una habilidad asociada, la habilidad debe `skillId` integrarse en ella.
`Book-a-room` acción de la tarjeta bot, la obtención del módulo de tareas y el envío de cargas útiles de acción se modifican para que contengan `skillId` como parámetro. 

Para obtener más información, consulte [esta](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) sección de esta documentación.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Manejar actividades desde el chat grupal o el alcance del canal

`Book-a-room bot` está diseñado para chats privados, como personal o solo 1:1 alcance. Puesto que tenemos virtual assistant personalizado para admitir el chat de grupo y los ámbitos de canal, el Asistente virtual debe invocarse desde los ámbitos de canal y, por lo tanto, `Book-a-room` bot debe obtener actividades para el mismo ámbito. Por lo `Book-a-room` tanto, el bot está personalizado para manejar esas actividades. Puede encontrar los métodos de protección del `OnMessageActivityAsync` controlador de actividad del `Book-a-room` bot.

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

También puede aprovechar las habilidades existentes desde el repositorio de [Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) o crear una nueva habilidad desde cero. Para crear una nueva habilidad, consulte [tutoriales para crear una nueva habilidad.](https://microsoft.github.io/botframework-solutions/overview/skills/) Para obtener documentación de virtual asistente y arquitectura de habilidades, consulte[Asistente virtual y arquitectura de habilidades.](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)  

## <a name="limitations-of-virtual-assistant"></a>Limitaciones del Asistente Virtual 

* **EndOfConversation**: Una habilidad debe enviar una `endOfConversation` actividad cuando finaliza una conversación. En función de la actividad, un Asistente virtual finaliza el contexto con esa habilidad en particular y vuelve al contexto raíz de Virtual Assistant. Para book-a-room bot, no hay un estado claro donde se termine la conversación. Por lo tanto, no hemos enviado `endOfConversation` desde el bot y cuando el usuario quiere volver al contexto raíz simplemente pueden hacerlo por `Book-a-room` `start over` comando.  
* **Actualización de tarjeta:** la actualización de la tarjeta aún no se admite a través del Asistente virtual.  
* **Extensiones de mensajería**:
  * Actualmente, un Asistente virtual puede admitir un máximo de diez comandos para las extensiones de mensajería.
  * La configuración de extensiones de mensajería no está en el ámbito de comandos individuales, sino para toda la propia extensión. Esto limita la configuración para cada habilidad individual a través de Virtual Assistant.
  * Los archivos de comandos de extensiones de mensajería tienen una longitud máxima de [64 caracteres](../resources/schema/manifest-schema.md#composeextensions) y se utilizan 37 caracteres para incrustar información de habilidades. Por lo tanto, las restricciones actualizadas para el ID de comando están limitadas a 27 caracteres.

También puede aprovechar las habilidades existentes desde el repositorio de [Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) o crear una nueva habilidad desde cero. Los tutoriales para el posterior se pueden encontrar [aquí.](https://microsoft.github.io/botframework-solutions/overview/skills/) Consulte la [documentación](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) de Virtual Assistant y arquitectura de habilidades.

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de la muestra** | **Descripción** | **C#** | **.NET** |
|----------|-----------------|----------|------------------|
| Plantilla de estudio visual actualizada | Plantilla personalizada para admitir las capacidades de los equipos. | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| Código de habilidad de bots de reserva en una habitación | Le permite encontrar y reservar rápidamente una sala de reuniones sobre la marcha. |  | [View](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a>Vea también

- [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)

- [Reservar una habitación](app-templates.md#book-a-room)

- [bot Microsoft Teams](../bots/what-are-bots.md)