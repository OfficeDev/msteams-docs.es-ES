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
# <a name="create-virtual-assistant"></a><span data-ttu-id="6eedb-104">Crear un asistente virtual</span><span class="sxs-lookup"><span data-stu-id="6eedb-104">Create Virtual Assistant</span></span> 

<span data-ttu-id="6eedb-105">Virtual Assistant es una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida mientras mantiene el control total de la experiencia del usuario, la personalización de marca de la organización y los datos necesarios.</span><span class="sxs-lookup"><span data-stu-id="6eedb-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="6eedb-106">La [plantilla principal de Virtual Assistant](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) es el building block básico que reúne las tecnologías de Microsoft necesarias para crear un Asistente virtual, incluido el SDK de Bot [Framework,](https://github.com/microsoft/botframework-sdk) [Language Understanding (LUIS)](https://www.luis.ai/)y [QnA Maker.](https://www.qnamaker.ai/)</span><span class="sxs-lookup"><span data-stu-id="6eedb-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), and [QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="6eedb-107">También reúne las capacidades esenciales, incluyendo el registro de habilidades, cuentas vinculadas, intención conversacional básica para ofrecer una gama de interacciones y experiencias sin problemas a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="6eedb-107">It also brings together the essential capabilities including  skills registration, linked accounts, basic conversational intent to offer a range of seamless interactions and experiences to users.</span></span> <span data-ttu-id="6eedb-108">Además, las capacidades de la plantilla incluyen ejemplos enriquecidos de [habilidades](https://microsoft.github.io/botframework-solutions/overview/skills)conversacionales reutilizables.</span><span class="sxs-lookup"><span data-stu-id="6eedb-108">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="6eedb-109">Las habilidades individuales se integran en una solución de Virtual Assistant para habilitar múltiples escenarios.</span><span class="sxs-lookup"><span data-stu-id="6eedb-109">Individual skills are integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="6eedb-110">Con el SDK de Bot Framework, las habilidades se presentan en forma de código fuente, lo que le permite personalizar y ampliar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6eedb-110">Using the Bot Framework SDK, skills are presented in source code form, enabling you to customize and extend as required.</span></span> <span data-ttu-id="6eedb-111">Para obtener más información sobre las habilidades de Bot Framework, consulte [Qué es una habilidad de Bot Framework](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="6eedb-111">For more information on skills of Bot Framework, see [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="6eedb-112">Este documento le guía sobre las consideraciones de implementación del Asistente virtual para las organizaciones, cómo crear un Asistente virtual centrado Teams, ejemplo relacionado, ejemplo de código y limitaciones del Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="6eedb-112">This document guides you on Virtual Assistant implementation considerations for organizations, how to create a Teams focused Virtual Assistant, related example, code sample, and limitations of Virtual Assistant.</span></span>
<span data-ttu-id="6eedb-113">La siguiente imagen muestra la descripción general del asistente virtual:</span><span class="sxs-lookup"><span data-stu-id="6eedb-113">The following image displays the overview of virtual assistant:</span></span>

![Diagrama de visión general de Virtual Assistant](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="6eedb-115">Las actividades de mensajes de texto se enrutan a las habilidades asociadas por el núcleo del Asistente virtual mediante un modelo [de envío.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6eedb-115">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="6eedb-116">Consideraciones de implementación</span><span class="sxs-lookup"><span data-stu-id="6eedb-116">Implementation considerations</span></span>

<span data-ttu-id="6eedb-117">La decisión de agregar un Asistente Virtual incluye muchos determinantes y difiere para cada organización.</span><span class="sxs-lookup"><span data-stu-id="6eedb-117">The decision to add a Virtual Assistant includes many determinants and differs for each organization.</span></span> <span data-ttu-id="6eedb-118">Los factores auxiliares de una implementación de Virtual Assistant para su organización son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="6eedb-118">The supporting factors of a Virtual Assistant implementation for your organization are as follows:</span></span>

* <span data-ttu-id="6eedb-119">Un equipo central administra todas las experiencias de los empleados.</span><span class="sxs-lookup"><span data-stu-id="6eedb-119">A central team manages all employee experiences.</span></span> <span data-ttu-id="6eedb-120">Tiene la capacidad de crear una experiencia de Asistente Virtual y administrar actualizaciones de la experiencia principal, incluida la adición de nuevas habilidades.</span><span class="sxs-lookup"><span data-stu-id="6eedb-120">It has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
* <span data-ttu-id="6eedb-121">Existen varias aplicaciones entre las funciones empresariales y se espera que el número crezca en el futuro.</span><span class="sxs-lookup"><span data-stu-id="6eedb-121">Multiple applications exist across business functions and the number is expected to grow in the future.</span></span>
* <span data-ttu-id="6eedb-122">Las aplicaciones existentes son personalizables, propiedad de la organización, y se convierten en habilidades para un Asistente Virtual.</span><span class="sxs-lookup"><span data-stu-id="6eedb-122">Existing applications are customizable, owned by the organization, and are converted into skills for a Virtual Assistant.</span></span>
* <span data-ttu-id="6eedb-123">El equipo central de experiencias de empleados puede influir en las personalizaciones de las aplicaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="6eedb-123">The central employee experiences team is able to influence customizations to existing apps.</span></span> <span data-ttu-id="6eedb-124">También proporciona la orientación necesaria para integrar las aplicaciones existentes como habilidades en la experiencia de Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="6eedb-124">It also provides necessary guidance for integrating existing applications as skills in Virtual Assistant experience.</span></span>

<span data-ttu-id="6eedb-125">La siguiente imagen muestra las funciones empresariales de Virtual Assistant:</span><span class="sxs-lookup"><span data-stu-id="6eedb-125">The following image displays the business functions of Virtual Assistant:</span></span> 

![El equipo central mantiene al asistente y los equipos de funciones empresariales aportan habilidades](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="6eedb-127">Crear un asistente virtual centrado en la Teams</span><span class="sxs-lookup"><span data-stu-id="6eedb-127">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="6eedb-128">Microsoft ha publicado una [plantilla de Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) para crear asistentes virtuales y habilidades.</span><span class="sxs-lookup"><span data-stu-id="6eedb-128">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="6eedb-129">Con la plantilla Visual Studio, puede crear un Asistente Virtual, impulsado por una experiencia basada en texto con soporte para tarjetas enriquecidas limitadas con acciones.</span><span class="sxs-lookup"><span data-stu-id="6eedb-129">With the Visual Studio template, you can create a Virtual Assistant, powered by a text based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="6eedb-130">Hemos mejorado la plantilla base Visual Studio para incluir Microsoft Teams capacidades de plataforma y potenciar grandes experiencias de Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="6eedb-130">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="6eedb-131">Algunas de las capacidades incluyen compatibilidad con tarjetas adaptables enriquecidas, módulos de tareas, chats de equipos o grupos y extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="6eedb-131">A few of the capabilities include support for rich Adaptive Cards, task modules, teams or group chats, and messaging extensions.</span></span> <span data-ttu-id="6eedb-132">Para obtener más información sobre cómo ampliar Virtual Assistant a Microsoft Teams, consulte [Tutorial: Extender el asistente virtual a Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="6eedb-132">For more information on extending Virtual Assistant to Microsoft Teams, see [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>    
<span data-ttu-id="6eedb-133">La siguiente imagen muestra el diagrama de alto nivel de una solución de Virtual Assistant:</span><span class="sxs-lookup"><span data-stu-id="6eedb-133">The following image displays the high level diagram of a Virtual Assistant solution:</span></span>

![Diagrama de alto nivel de una solución de Virtual Assistant](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="6eedb-135">Añade tarjetas adaptables a tu Asistente Virtual</span><span class="sxs-lookup"><span data-stu-id="6eedb-135">Add Adaptive Cards to your Virtual Assistant</span></span>

<span data-ttu-id="6eedb-136">Para enviar solicitudes correctamente, el Asistente virtual debe identificar el modelo de LUIS correcto y la habilidad correspondiente asociada a él.</span><span class="sxs-lookup"><span data-stu-id="6eedb-136">To dispatch requests properly, your Virtual Assistant must identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="6eedb-137">Sin embargo, el mecanismo de envío no se puede usar para actividades de acción de tarjeta, ya que el modelo de LUIS asociado a una habilidad está entrenado para textos de acción de cartas.</span><span class="sxs-lookup"><span data-stu-id="6eedb-137">However, the dispatching mechanism cannot be used for card action activities as the LUIS model associated with a skill, is trained for card action texts.</span></span> <span data-ttu-id="6eedb-138">Los textos de acción de la tarjeta son palabras clave fijas, predefinidas y no se comentan desde un usuario.</span><span class="sxs-lookup"><span data-stu-id="6eedb-138">The card action texts are fixed, pre-defined keywords, and not commented from a user.</span></span>

<span data-ttu-id="6eedb-139">Este inconveniente se resuelve esto incorporando información de habilidad en la carga útil de la acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="6eedb-139">This drawback is resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="6eedb-140">Cada habilidad debe integrarse `skillId` en el campo de las acciones de  `value` cartas.</span><span class="sxs-lookup"><span data-stu-id="6eedb-140">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="6eedb-141">Debe asegurarse de que cada actividad de acción de la tarjeta lleva la información de habilidad relevante, y Virtual Assistant puede utilizar esta información para el envío.</span><span class="sxs-lookup"><span data-stu-id="6eedb-141">You must ensure that each card action activity carries the relevant skill information, and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="6eedb-142">Debe proporcionar `skillId` en el constructor para asegurarse de que la información de habilidad siempre está presente en las acciones de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="6eedb-142">You must provide `skillId` in the constructor to ensure that the skill information is always present in card actions.</span></span>
<span data-ttu-id="6eedb-143">En la siguiente sección se muestra un código de ejemplo de datos de acción de tarjeta:</span><span class="sxs-lookup"><span data-stu-id="6eedb-143">A card action data sample code is shown in the following section:</span></span>
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

<span data-ttu-id="6eedb-144">A continuación, `SkillCardActionData` la clase de la plantilla Asistente virtual se introduce para extraer de la carga útil de la acción `skillId` de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="6eedb-144">Next, `SkillCardActionData` class in the Virtual Assistant template is introduces to extract `skillId` from the card action payload.</span></span>
<span data-ttu-id="6eedb-145">En la siguiente sección se muestra un fragmento de código para extraer  `skillId` de la carga útil de la acción de la tarjeta:</span><span class="sxs-lookup"><span data-stu-id="6eedb-145">A code snippet to extract  `skillId` from card action payload is shown in the following section:</span></span>

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

<span data-ttu-id="6eedb-146">La implementación se realiza mediante un método de extensión en la [clase Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)</span><span class="sxs-lookup"><span data-stu-id="6eedb-146">The implementation is done by an extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>
<span data-ttu-id="6eedb-147">En la siguiente sección se muestra un fragmento de código para extraer  `skillId` de los datos de acción de la tarjeta:</span><span class="sxs-lookup"><span data-stu-id="6eedb-147">A code snippet to extract  `skillId` from card action data is shown in the following section:</span></span>

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

### <a name="handle-interruptions"></a><span data-ttu-id="6eedb-148">Interrupciones del mango</span><span class="sxs-lookup"><span data-stu-id="6eedb-148">Handle interruptions</span></span>

<span data-ttu-id="6eedb-149">Virtual Assistant puede controlar las interrupciones en los casos en que un usuario intenta invocar una habilidad mientras otra habilidad está activa actualmente.</span><span class="sxs-lookup"><span data-stu-id="6eedb-149">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="6eedb-150">`TeamsSkillDialog`, y `TeamsSwitchSkillDialog` se introducen en función del [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [el SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="6eedb-150">`TeamsSkillDialog`, and `TeamsSwitchSkillDialog`are introduced based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span></span> <span data-ttu-id="6eedb-151">Permiten a los usuarios cambiar una experiencia de habilidad de las acciones de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="6eedb-151">They enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="6eedb-152">Para controlar esta solicitud, el Asistente virtual solicita al usuario un mensaje de confirmación para cambiar las habilidades:</span><span class="sxs-lookup"><span data-stu-id="6eedb-152">To handle this request, the Virtual Assistant prompts the user with a confirmation message to switch skills:</span></span>

![Solicitud de confirmación al cambiar a una nueva habilidad](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a><span data-ttu-id="6eedb-154">Gestionar las solicitudes de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="6eedb-154">Handle task module requests</span></span>

<span data-ttu-id="6eedb-155">Para agregar capacidades de módulo de tareas a un Asistente virtual, se incluyen dos métodos adicionales en el controlador de actividad Asistente virtual: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="6eedb-155">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="6eedb-156">Estos métodos escuchan las actividades relacionadas con el módulo de tareas desde Virtual Assistant, identifican la habilidad asociada con la solicitud y reenvían la solicitud a la habilidad identificada.</span><span class="sxs-lookup"><span data-stu-id="6eedb-156">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="6eedb-157">El reenvío de solicitudes se realiza a través del método [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="6eedb-157">Request forwarding is done through the [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="6eedb-158">Devuelve la respuesta como `InvokeResponse` la que se analiza y se convierte en `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="6eedb-158">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>


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

<span data-ttu-id="6eedb-159">Se sigue un enfoque similar para el envío de acciones de tarjeta y las respuestas del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="6eedb-159">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="6eedb-160">Los datos de acción de captura y envío del módulo de tareas se actualizan para incluir `skillId` .</span><span class="sxs-lookup"><span data-stu-id="6eedb-160">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="6eedb-161">El método extensión de actividad `GetSkillId` extrae `skillId` de la carga útil que proporciona detalles sobre la habilidad que debe invocarse.</span><span class="sxs-lookup"><span data-stu-id="6eedb-161">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="6eedb-162">El fragmento de código `OnTeamsTaskModuleFetchAsync` para y métodos se dan en la siguiente `OnTeamsTaskModuleSubmitAsync` sección:</span><span class="sxs-lookup"><span data-stu-id="6eedb-162">The code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods are given in the following section:</span></span>

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

<span data-ttu-id="6eedb-163">Además, debe incluir todos los dominios de habilidad de la sección en el `validDomains` archivo de manifiesto de Virtual Assistant para que los módulos de tareas se invoquen a través de un renderizado de habilidades correctamente.</span><span class="sxs-lookup"><span data-stu-id="6eedb-163">Additionally, you must include all skill domains in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked through a skill render properly.</span></span>

### <a name="handle-collaborative-app-scopes"></a><span data-ttu-id="6eedb-164">Controlar los ámbitos de aplicación colaborativa</span><span class="sxs-lookup"><span data-stu-id="6eedb-164">Handle collaborative app scopes</span></span>

<span data-ttu-id="6eedb-165">Teams aplicaciones pueden existir en varios ámbitos, incluyendo chat 1:1, chat de grupo y canales.</span><span class="sxs-lookup"><span data-stu-id="6eedb-165">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="6eedb-166">La plantilla principal de Virtual Assistant está diseñada para chats 1:1.</span><span class="sxs-lookup"><span data-stu-id="6eedb-166">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="6eedb-167">Como parte de la experiencia de incorporación, Virtual Assistant solicita nombre a los usuarios y mantiene el estado del usuario.</span><span class="sxs-lookup"><span data-stu-id="6eedb-167">As part of the onboarding experience Virtual Assistant prompts users for name and maintains user state.</span></span> <span data-ttu-id="6eedb-168">Dado que esa experiencia de incorporación no es adecuada para el chat de grupo o los ámbitos de canal se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="6eedb-168">Since that onboarding experience is not suited for group chat or channel scopes it has been removed.</span></span>

<span data-ttu-id="6eedb-169">Las habilidades deben manejar actividades en múltiples ámbitos, como chat 1:1, chat en grupo y conversación de canal.</span><span class="sxs-lookup"><span data-stu-id="6eedb-169">Skills should handle activities in multiple scopes, such as 1:1 chat, group chat, and channel conversation.</span></span> <span data-ttu-id="6eedb-170">Si no se admite alguno de estos ámbitos, las habilidades deben responder con un mensaje adecuado.</span><span class="sxs-lookup"><span data-stu-id="6eedb-170">If any of these scopes are not supported, skills must respond with an appropriate message.</span></span>

<span data-ttu-id="6eedb-171">Las siguientes funciones de procesamiento se han agregado al núcleo de Virtual Assistant:</span><span class="sxs-lookup"><span data-stu-id="6eedb-171">The following  processing functions have been added to Virtual Assistant core:</span></span>

* <span data-ttu-id="6eedb-172">Virtual Assistant se puede invocar sin ningún mensaje de texto de un chat o canal de grupo.</span><span class="sxs-lookup"><span data-stu-id="6eedb-172">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
* <span data-ttu-id="6eedb-173">Las articulaciones se limpian antes de enviar el mensaje al módulo de envío.</span><span class="sxs-lookup"><span data-stu-id="6eedb-173">Articulations are cleaned before sending the message to the dispatch module.</span></span> <span data-ttu-id="6eedb-174">Por ejemplo, quite la @mention necesaria del bot.</span><span class="sxs-lookup"><span data-stu-id="6eedb-174">For example, remove the necessary @mention of the bot.</span></span>

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

### <a name="handle-messaging-extensions"></a><span data-ttu-id="6eedb-175">Manejar extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="6eedb-175">Handle messaging extensions</span></span>

<span data-ttu-id="6eedb-176">Los comandos de una extensión de mensajería se declaran en el archivo de manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6eedb-176">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="6eedb-177">La interfaz de usuario de la extensión de mensajería está alimentada por esos comandos.</span><span class="sxs-lookup"><span data-stu-id="6eedb-177">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="6eedb-178">Para que un Asistente virtual encienda un comando de extensión de mensajería como una habilidad adjunta, el propio manifiesto de un Asistente virtual debe contener esos comandos.</span><span class="sxs-lookup"><span data-stu-id="6eedb-178">For a Virtual Assistant to power a messaging extension command as an attached skill, a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="6eedb-179">Debe agregar los comandos del manifiesto de una habilidad individual al manifiesto del Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="6eedb-179">You must add the commands from an individual skill's manifest to the Virtual Assistant's manifest.</span></span> <span data-ttu-id="6eedb-180">El identificador de comando proporciona información sobre una habilidad asociada añadiendo el ID de aplicación de la habilidad a través de un `:` separador.</span><span class="sxs-lookup"><span data-stu-id="6eedb-180">The command ID provides information about an associated skill by appending the skill's app ID through a separator `:`.</span></span>

<span data-ttu-id="6eedb-181">El fragmento de código del archivo de manifiesto de una habilidad se muestra en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="6eedb-181">The snippet from a skill's manifest file is shown in the following section:</span></span>

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

<span data-ttu-id="6eedb-182">El fragmento de código de archivo de manifiesto del Asistente virtual correspondiente se muestra en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="6eedb-182">The corresponding Virtual Assistant manifest file code snippet is shown in the following section:</span></span>

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

<span data-ttu-id="6eedb-183">Una vez invocados los comandos por un usuario, el Asistente virtual puede identificar una habilidad asociada analizando el ID de comando, actualizar la actividad quitando el sufijo adicional `:<skill_id>` del ID de comando y reenviarlo a la habilidad correspondiente.</span><span class="sxs-lookup"><span data-stu-id="6eedb-183">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix `:<skill_id>` from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="6eedb-184">El código de una habilidad no necesita manejar el sufijo adicional.</span><span class="sxs-lookup"><span data-stu-id="6eedb-184">The code for a skill doesnot need to handle the extra suffix.</span></span> <span data-ttu-id="6eedb-185">Por lo tanto, se evitan los conflictos entre los dedo de mando a través de habilidades.</span><span class="sxs-lookup"><span data-stu-id="6eedb-185">Thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="6eedb-186">Con este enfoque, todos los comandos de búsqueda y acción de una habilidad dentro de todos los contextos, como **componer,** **commandBox** y **mensaje,** están alimentados por un Asistente Virtual.</span><span class="sxs-lookup"><span data-stu-id="6eedb-186">With this approach, all the search and action commands of a skill within all contexts, such as **compose**, **commandBox**, and **message** are powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="6eedb-187">Algunas actividades de extensión de mensajería no incluyen el identificador de comando.</span><span class="sxs-lookup"><span data-stu-id="6eedb-187">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="6eedb-188">Por ejemplo, `composeExtension/selectItem` contiene solo el valor de la acción de toque invoke.</span><span class="sxs-lookup"><span data-stu-id="6eedb-188">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="6eedb-189">Para identificar la habilidad asociada, `skillId`  se adjunta a cada carta de artículos mientras se forma una respuesta para `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="6eedb-189">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="6eedb-190">Esto es similar al enfoque para [agregar tarjetas adaptables a su Asistente Virtual.](#add-adaptive-cards-to-your-virtual-assistant)</span><span class="sxs-lookup"><span data-stu-id="6eedb-190">This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example"></a><span data-ttu-id="6eedb-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6eedb-191">Example</span></span>

<span data-ttu-id="6eedb-192">En el ejemplo siguiente se muestra cómo convertir la plantilla de aplicación Reservar una habitación en una habilidad asistente virtual: Reservar una habitación es un Microsoft Teams que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30, 60 o 90 minutos a partir de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="6eedb-192">The following example shows how to convert the Book-a-room app template to a Virtual Assistant skill: Book-a-room is a Microsoft Teams that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="6eedb-193">El tiempo predeterminado es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="6eedb-193">The default time is 30 minutes.</span></span> <span data-ttu-id="6eedb-194">El bot Book-a-room se limita a conversaciones personales o 1:1.</span><span class="sxs-lookup"><span data-stu-id="6eedb-194">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="6eedb-195">La siguiente imagen muestra un Asistente Virtual con un libro una habilidad **de habitación:**</span><span class="sxs-lookup"><span data-stu-id="6eedb-195">The following image displays a Virtual Assistant with a **book a room** skill:</span></span>

![Asistente virtual con una habilidad de "reservar una habitación"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="6eedb-197">Los siguientes son los cambios delta introducidos para convertirlo en una habilidad que se adjunta a un Asistente Virtual.</span><span class="sxs-lookup"><span data-stu-id="6eedb-197">Followings are the delta changes introduced to convert it to a skill which is attached to a Virtual Assistant.</span></span> <span data-ttu-id="6eedb-198">Se siguen directrices similares para convertir cualquier bot v4 existente en una habilidad.</span><span class="sxs-lookup"><span data-stu-id="6eedb-198">Similar guidelines are followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="6eedb-199">Manifiesto de habilidad</span><span class="sxs-lookup"><span data-stu-id="6eedb-199">Skill manifest</span></span>

<span data-ttu-id="6eedb-200">Un manifiesto de habilidad es un archivo JSON que expone el punto de conexión de mensajería, el IDENTIFICADOR, el nombre y otros metadatos relevantes de una habilidad.</span><span class="sxs-lookup"><span data-stu-id="6eedb-200">A skill manifest is a JSON file that exposes a skill's messaging endpoint, ID, name, and other relevant metadata.</span></span> <span data-ttu-id="6eedb-201">Este manifiesto es diferente del manifiesto utilizado para descargar una aplicación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6eedb-201">This manifest is different than the manifest used for sideloading an app in Microsoft Teams.</span></span> <span data-ttu-id="6eedb-202">Un Asistente virtual requiere una ruta de acceso a este archivo como entrada para asociar una habilidad.</span><span class="sxs-lookup"><span data-stu-id="6eedb-202">A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="6eedb-203">Hemos agregado el siguiente manifiesto a la carpeta wwwroot del bot.</span><span class="sxs-lookup"><span data-stu-id="6eedb-203">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="6eedb-204">Integración de LUIS</span><span class="sxs-lookup"><span data-stu-id="6eedb-204">LUIS Integration</span></span>

<span data-ttu-id="6eedb-205">El modelo de envío de Virtual Assistant se basa en los modelos de LUIS de habilidades adjuntas.</span><span class="sxs-lookup"><span data-stu-id="6eedb-205">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="6eedb-206">El modelo de envío identifica la intención de cada actividad de texto y descubre la habilidad asociada a ella.</span><span class="sxs-lookup"><span data-stu-id="6eedb-206">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="6eedb-207">Virtual Assistant requiere el modelo de LUIS de habilidad en `.lu` formato como entrada mientras se adjunta una habilidad.</span><span class="sxs-lookup"><span data-stu-id="6eedb-207">Virtual Assistant requires skill's LUIS model in `.lu` format as an input while attaching a skill.</span></span> <span data-ttu-id="6eedb-208">LUIS json se convierte en `.lu` formato mediante la herramienta botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="6eedb-208">LUIS json is converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="6eedb-209">Book-a-room bot tiene dos comandos principales para los usuarios:</span><span class="sxs-lookup"><span data-stu-id="6eedb-209">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="6eedb-210">Hemos creado un modelo de LUIS mediante la comprensión de estos dos comandos.</span><span class="sxs-lookup"><span data-stu-id="6eedb-210">We have built a LUIS model by understanding these two commands.</span></span> <span data-ttu-id="6eedb-211">Los secretos correspondientes deben rellenarse en `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="6eedb-211">Corresponding secrets must be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="6eedb-212">El archivo JSON de LUIS correspondiente se encuentra [aquí.](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)</span><span class="sxs-lookup"><span data-stu-id="6eedb-212">The corresponding LUIS JSON file is found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).</span></span>
<span data-ttu-id="6eedb-213">El archivo correspondiente `.lu` se muestra en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="6eedb-213">The corresponding `.lu` file is shown in the following section:</span></span>

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

<span data-ttu-id="6eedb-214">Con este enfoque, cualquier comando emitido por un usuario al Asistente virtual relacionado con `book room` o se identifica como un comando asociado con bot y se `manage favorites` `Book-a-room` reenvía a esta habilidad.</span><span class="sxs-lookup"><span data-stu-id="6eedb-214">With this approach, any command issued by a user to Virtual Assistant related to `book room` or `manage favorites` are identified as a command associated with `Book-a-room` bot and is forwarded to this skill.</span></span>
<span data-ttu-id="6eedb-215">Por otro lado, el bot debe usar el `Book-a-room room` modelo de LUIS para comprender estos comandos si no están escritos completos.</span><span class="sxs-lookup"><span data-stu-id="6eedb-215">On the other hand, `Book-a-room room` bot needs to use LUIS model to understand these commands if they are not typed full.</span></span> <span data-ttu-id="6eedb-216">Por ejemplo: `I want to manage my favorite rooms`.</span><span class="sxs-lookup"><span data-stu-id="6eedb-216">For example: `I want to manage my favorite rooms`.</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="6eedb-217">Soporte multilingüe</span><span class="sxs-lookup"><span data-stu-id="6eedb-217">Multi-Language support</span></span>

<span data-ttu-id="6eedb-218">Por ejemplo, se crea un modelo de LUIS con solo la referencia cultural en inglés.</span><span class="sxs-lookup"><span data-stu-id="6eedb-218">As an example, a LUIS model with only English culture is created.</span></span> <span data-ttu-id="6eedb-219">Puede crear modelos de LUIS correspondientes a otros idiomas y agregar entrada a `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="6eedb-219">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="6eedb-220">En paralelo, agregue el archivo correspondiente `.lu` en la ruta luisFolder.</span><span class="sxs-lookup"><span data-stu-id="6eedb-220">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="6eedb-221">La estructura de carpetas debe ser la siguiente:</span><span class="sxs-lookup"><span data-stu-id="6eedb-221">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="6eedb-222">Para modificar `languages` el parámetro, actualice el comando botskills de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="6eedb-222">To modify `languages` parameter, update botskills command as follows:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="6eedb-223">Virtual Assistant utiliza `SetLocaleMiddleware` para identificar la configuración regional actual e invocar el modelo de envío correspondiente.</span><span class="sxs-lookup"><span data-stu-id="6eedb-223">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="6eedb-224">La actividad del marco de bots tiene un campo de configuración regional que usa este middleware.</span><span class="sxs-lookup"><span data-stu-id="6eedb-224">Bot framework activity has locale field which is used by this middleware.</span></span> <span data-ttu-id="6eedb-225">También puedes usar lo mismo para tu habilidad.</span><span class="sxs-lookup"><span data-stu-id="6eedb-225">You can use the same for your skill as well.</span></span> <span data-ttu-id="6eedb-226">Book-a-room bot no usa este middleware y, en su lugar, obtiene la configuración regional de la [entidad clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de la actividad de marco de trabajo de Bot.</span><span class="sxs-lookup"><span data-stu-id="6eedb-226">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="6eedb-227">Validación de reclamaciones</span><span class="sxs-lookup"><span data-stu-id="6eedb-227">Claim validation</span></span>

<span data-ttu-id="6eedb-228">Hemos agregado [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) para restringir a los llamadores a la habilidad.</span><span class="sxs-lookup"><span data-stu-id="6eedb-228">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="6eedb-229">Para permitir que un Asistente virtual llame a esta habilidad, rellene `AllowedCallers` la matriz con el identificador de aplicación de ese Asistente virtual en `appsettings` particular.</span><span class="sxs-lookup"><span data-stu-id="6eedb-229">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="6eedb-230">La matriz de llamadas permitidas puede restringir qué habilidades pueden acceder los consumidores a la habilidad.</span><span class="sxs-lookup"><span data-stu-id="6eedb-230">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="6eedb-231">Agregue una sola entrada `*` a esta matriz, para aceptar llamadas de cualquier consumidor de habilidades.</span><span class="sxs-lookup"><span data-stu-id="6eedb-231">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```

<span data-ttu-id="6eedb-232">Para obtener más información sobre cómo agregar validación de notificaciones a una habilidad, consulte [Agregar validación de notificaciones a la habilidad](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="6eedb-232">For more information on adding claims validation to a skill, see [add claims validation to skill](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="limitation-of-card-refresh"></a><span data-ttu-id="6eedb-233">Limitación de la actualización de la tarjeta</span><span class="sxs-lookup"><span data-stu-id="6eedb-233">Limitation of card refresh</span></span> 

<span data-ttu-id="6eedb-234">La actividad de actualización, como la actualización de tarjetas, aún no se admite a través de Virtual Assistant[(problema de github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686)</span><span class="sxs-lookup"><span data-stu-id="6eedb-234">Updating activity, such as card refresh is not supported yet through Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="6eedb-235">Por lo tanto, hemos reemplazado todas las llamadas de actualización de tarjetas `UpdateActivityAsync` con la publicación de nuevas llamadas de `SendActivityAsync` tarjeta.</span><span class="sxs-lookup"><span data-stu-id="6eedb-235">Hence, we have replaced all card refresh calls `UpdateActivityAsync` with posting new card calls `SendActivityAsync`.</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="6eedb-236">Acciones de tarjetas y flujos de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="6eedb-236">Card actions and task module flows</span></span>

<span data-ttu-id="6eedb-237">Para reenviar las actividades de la acción de la carta o del módulo de tareas a una habilidad asociada, la habilidad debe `skillId` integrarse en ella.</span><span class="sxs-lookup"><span data-stu-id="6eedb-237">To forward card action or task module activities to an associated skill, the skill must embed `skillId` to it.</span></span>
<span data-ttu-id="6eedb-238">`Book-a-room` acción de la tarjeta bot, la obtención del módulo de tareas y el envío de cargas útiles de acción se modifican para que contengan `skillId` como parámetro.</span><span class="sxs-lookup"><span data-stu-id="6eedb-238">`Book-a-room` bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="6eedb-239">Para obtener más información, consulte [esta](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) sección de esta documentación.</span><span class="sxs-lookup"><span data-stu-id="6eedb-239">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="6eedb-240">Manejar actividades desde el chat grupal o el alcance del canal</span><span class="sxs-lookup"><span data-stu-id="6eedb-240">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="6eedb-241">`Book-a-room bot` está diseñado para chats privados, como personal o solo 1:1 alcance.</span><span class="sxs-lookup"><span data-stu-id="6eedb-241">`Book-a-room bot` is designed for private chats, such as personal or 1:1 scope only.</span></span> <span data-ttu-id="6eedb-242">Puesto que tenemos virtual assistant personalizado para admitir el chat de grupo y los ámbitos de canal, el Asistente virtual debe invocarse desde los ámbitos de canal y, por lo tanto, `Book-a-room` bot debe obtener actividades para el mismo ámbito.</span><span class="sxs-lookup"><span data-stu-id="6eedb-242">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant must be invoked from the channel scopes and thus, `Book-a-room` bot must get activities for the same scope.</span></span> <span data-ttu-id="6eedb-243">Por lo `Book-a-room` tanto, el bot está personalizado para manejar esas actividades.</span><span class="sxs-lookup"><span data-stu-id="6eedb-243">Hence `Book-a-room`bot is customized to handle those activities.</span></span> <span data-ttu-id="6eedb-244">Puede encontrar los métodos de protección del `OnMessageActivityAsync` controlador de actividad del `Book-a-room` bot.</span><span class="sxs-lookup"><span data-stu-id="6eedb-244">You can find the check in `OnMessageActivityAsync` methods of `Book-a-room` bot's activity handler.</span></span>

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

<span data-ttu-id="6eedb-245">También puede aprovechar las habilidades existentes desde el repositorio de [Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) o crear una nueva habilidad desde cero.</span><span class="sxs-lookup"><span data-stu-id="6eedb-245">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="6eedb-246">Para crear una nueva habilidad, consulte [tutoriales para crear una nueva habilidad.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="6eedb-246">For creating a new skill, see [tutorials to create a new skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="6eedb-247">Para obtener documentación de virtual asistente y arquitectura de habilidades, consulte[Asistente virtual y arquitectura de habilidades.](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6eedb-247">For Virtual Assistant and skills architecture documentation, see[Virtual Assistant and skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span></span>  

## <a name="limitations-of-virtual-assistant"></a><span data-ttu-id="6eedb-248">Limitaciones del Asistente Virtual</span><span class="sxs-lookup"><span data-stu-id="6eedb-248">Limitations of Virtual Assistant</span></span> 

* <span data-ttu-id="6eedb-249">**EndOfConversation**: Una habilidad debe enviar una `endOfConversation` actividad cuando finaliza una conversación.</span><span class="sxs-lookup"><span data-stu-id="6eedb-249">**EndOfConversation**: A skill must send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="6eedb-250">En función de la actividad, un Asistente virtual finaliza el contexto con esa habilidad en particular y vuelve al contexto raíz de Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="6eedb-250">Based on the activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's root context.</span></span> <span data-ttu-id="6eedb-251">Para book-a-room bot, no hay un estado claro donde se termine la conversación.</span><span class="sxs-lookup"><span data-stu-id="6eedb-251">For Book-a-room bot, there is no clear state where conversation is ended.</span></span> <span data-ttu-id="6eedb-252">Por lo tanto, no hemos enviado `endOfConversation` desde el bot y cuando el usuario quiere volver al contexto raíz simplemente pueden hacerlo por `Book-a-room` `start over` comando.</span><span class="sxs-lookup"><span data-stu-id="6eedb-252">Hence we have not sent `endOfConversation` from `Book-a-room` bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>  
* <span data-ttu-id="6eedb-253">**Actualización de tarjeta:** la actualización de la tarjeta aún no se admite a través del Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="6eedb-253">**Card refresh**: Card refresh is not yet supported through Virtual Assistant.</span></span>  
* <span data-ttu-id="6eedb-254">**Extensiones de mensajería**:</span><span class="sxs-lookup"><span data-stu-id="6eedb-254">**Messaging extensions**:</span></span>
  * <span data-ttu-id="6eedb-255">Actualmente, un Asistente virtual puede admitir un máximo de diez comandos para las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="6eedb-255">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  * <span data-ttu-id="6eedb-256">La configuración de extensiones de mensajería no está en el ámbito de comandos individuales, sino para toda la propia extensión.</span><span class="sxs-lookup"><span data-stu-id="6eedb-256">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="6eedb-257">Esto limita la configuración para cada habilidad individual a través de Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="6eedb-257">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  * <span data-ttu-id="6eedb-258">Los archivos de comandos de extensiones de mensajería tienen una longitud máxima de [64 caracteres](../resources/schema/manifest-schema.md#composeextensions) y se utilizan 37 caracteres para incrustar información de habilidades.</span><span class="sxs-lookup"><span data-stu-id="6eedb-258">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters are used for embedding skill information.</span></span> <span data-ttu-id="6eedb-259">Por lo tanto, las restricciones actualizadas para el ID de comando están limitadas a 27 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eedb-259">Thus, updated constraints for command ID are limited to 27 characters.</span></span>

<span data-ttu-id="6eedb-260">También puede aprovechar las habilidades existentes desde el repositorio de [Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) o crear una nueva habilidad desde cero.</span><span class="sxs-lookup"><span data-stu-id="6eedb-260">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="6eedb-261">Los tutoriales para el posterior se pueden encontrar [aquí.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="6eedb-261">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="6eedb-262">Consulte la [documentación](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) de Virtual Assistant y arquitectura de habilidades.</span><span class="sxs-lookup"><span data-stu-id="6eedb-262">Please refer to [documentation](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="6eedb-263">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="6eedb-263">Code sample</span></span>

| <span data-ttu-id="6eedb-264">**Nombre de la muestra**</span><span class="sxs-lookup"><span data-stu-id="6eedb-264">**Sample name**</span></span> | <span data-ttu-id="6eedb-265">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="6eedb-265">**Description**</span></span> | <span data-ttu-id="6eedb-266">**C#**</span><span class="sxs-lookup"><span data-stu-id="6eedb-266">**C#**</span></span> | <span data-ttu-id="6eedb-267">**.NET**</span><span class="sxs-lookup"><span data-stu-id="6eedb-267">**.NET**</span></span> |
|----------|-----------------|----------|------------------|
| <span data-ttu-id="6eedb-268">Plantilla de estudio visual actualizada</span><span class="sxs-lookup"><span data-stu-id="6eedb-268">Updated visual studio template</span></span> | <span data-ttu-id="6eedb-269">Plantilla personalizada para admitir las capacidades de los equipos.</span><span class="sxs-lookup"><span data-stu-id="6eedb-269">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="6eedb-270">View</span><span class="sxs-lookup"><span data-stu-id="6eedb-270">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| <span data-ttu-id="6eedb-271">Código de habilidad de bots de reserva en una habitación</span><span class="sxs-lookup"><span data-stu-id="6eedb-271">Book-a-room bot skill code</span></span> | <span data-ttu-id="6eedb-272">Le permite encontrar y reservar rápidamente una sala de reuniones sobre la marcha.</span><span class="sxs-lookup"><span data-stu-id="6eedb-272">Lets you quickly find and book a meeting room on the go.</span></span> |  | [<span data-ttu-id="6eedb-273">View</span><span class="sxs-lookup"><span data-stu-id="6eedb-273">View</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a><span data-ttu-id="6eedb-274">Vea también</span><span class="sxs-lookup"><span data-stu-id="6eedb-274">See also</span></span>

- [<span data-ttu-id="6eedb-275">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="6eedb-275">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

- [<span data-ttu-id="6eedb-276">Reservar una habitación</span><span class="sxs-lookup"><span data-stu-id="6eedb-276">Book-a-room</span></span>](app-templates.md#book-a-room)

- [<span data-ttu-id="6eedb-277">bot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6eedb-277">Microsoft Teams bot</span></span>](../bots/what-are-bots.md)