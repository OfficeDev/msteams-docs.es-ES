---
title: Crear un asistente virtual
description: Cómo crear un Virtual Assistant bot y habilidades para su uso en Microsoft Teams
localization_priority: Normal
ms.topic: how-to
keywords: bots de asistente virtual de teams
ms.openlocfilehash: 976dacbd8b0bef7a3158d5ff35c5c38d97707c63
ms.sourcegitcommit: e327c9766dfa05abb468cdc71319e3cba7c6c79f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/14/2021
ms.locfileid: "53428726"
---
# <a name="create-virtual-assistant"></a><span data-ttu-id="d2e5d-104">Crear un asistente virtual</span><span class="sxs-lookup"><span data-stu-id="d2e5d-104">Create Virtual Assistant</span></span> 

<span data-ttu-id="d2e5d-105">Virtual Assistant es una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida y mantener el control total de la experiencia del usuario, la personalidad de marca de la organización y los datos necesarios.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="d2e5d-106">La [plantilla](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) principal de Virtual Assistant es el bloque de creación básico que reúne las tecnologías de Microsoft necesarias para crear un Virtual Assistant, incluido el SDK de [Bot Framework,](https://github.com/microsoft/botframework-sdk) [Language Understanding (LUIS)](https://www.luis.ai/)y [QnA Maker](https://www.qnamaker.ai/).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), and [QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="d2e5d-107">También reúne las capacidades esenciales, como el registro de aptitudes, las cuentas vinculadas, la intención conversacional básica de ofrecer a los usuarios una amplia variedad de interacciones y experiencias sin problemas.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-107">It also brings together the essential capabilities including  skills registration, linked accounts, basic conversational intent to offer a range of seamless interactions and experiences to users.</span></span> <span data-ttu-id="d2e5d-108">Además, las capacidades de plantilla incluyen ejemplos enriquecidos de habilidades conversacionales [reutilizables.](https://microsoft.github.io/botframework-solutions/overview/skills)</span><span class="sxs-lookup"><span data-stu-id="d2e5d-108">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="d2e5d-109">Las habilidades individuales se integran en Virtual Assistant solución para habilitar varios escenarios.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-109">Individual skills are integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="d2e5d-110">Con el SDK de Bot Framework, las habilidades se presentan en forma de código fuente, lo que permite personalizar y ampliar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-110">Using the Bot Framework SDK, skills are presented in source code form, enabling you to customize and extend as required.</span></span> <span data-ttu-id="d2e5d-111">Para obtener más información sobre las habilidades de Bot Framework, vea [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-111">For more information on skills of Bot Framework, see [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="d2e5d-112">Este documento le guía sobre Virtual Assistant de implementación para las organizaciones, cómo crear un Virtual Assistant centrado en Teams, ejemplo relacionado, ejemplo de código y limitaciones de Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-112">This document guides you on Virtual Assistant implementation considerations for organizations, how to create a Teams focused Virtual Assistant, related example, code sample, and limitations of Virtual Assistant.</span></span>
<span data-ttu-id="d2e5d-113">En la siguiente imagen se muestra la introducción al asistente virtual:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-113">The following image displays the overview of virtual assistant:</span></span>

![Virtual Assistant de información general](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="d2e5d-115">Las actividades de mensajes de texto se enrutan a las aptitudes asociadas mediante el Virtual Assistant principal mediante un modelo [de](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) distribución.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-115">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="d2e5d-116">Consideraciones de implementación</span><span class="sxs-lookup"><span data-stu-id="d2e5d-116">Implementation considerations</span></span>

<span data-ttu-id="d2e5d-117">La decisión de agregar un Virtual Assistant incluye muchos determinantes y difiere para cada organización.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-117">The decision to add a Virtual Assistant includes many determinants and differs for each organization.</span></span> <span data-ttu-id="d2e5d-118">Los factores de soporte de una Virtual Assistant implementación de la organización son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-118">The supporting factors of a Virtual Assistant implementation for your organization are as follows:</span></span>

* <span data-ttu-id="d2e5d-119">Un equipo central administra todas las experiencias de los empleados.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-119">A central team manages all employee experiences.</span></span> <span data-ttu-id="d2e5d-120">Tiene la capacidad de crear una experiencia Virtual Assistant y administrar actualizaciones de la experiencia principal, incluida la adición de nuevas habilidades.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-120">It has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
* <span data-ttu-id="d2e5d-121">Existen varias aplicaciones en todas las funciones empresariales y se espera que el número aumente en el futuro.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-121">Multiple applications exist across business functions and the number is expected to grow in the future.</span></span>
* <span data-ttu-id="d2e5d-122">Las aplicaciones existentes son personalizables, pertenecen a la organización y se convierten en aptitudes para un Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-122">Existing applications are customizable, owned by the organization, and are converted into skills for a Virtual Assistant.</span></span>
* <span data-ttu-id="d2e5d-123">El equipo de experiencias de los empleados centrales puede influir en las personalizaciones de las aplicaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-123">The central employee experiences team is able to influence customizations to existing apps.</span></span> <span data-ttu-id="d2e5d-124">También proporciona instrucciones necesarias para integrar aplicaciones existentes como habilidades en Virtual Assistant experiencia.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-124">It also provides necessary guidance for integrating existing applications as skills in Virtual Assistant experience.</span></span>

<span data-ttu-id="d2e5d-125">En la siguiente imagen se muestran las funciones empresariales de Virtual Assistant:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-125">The following image displays the business functions of Virtual Assistant:</span></span> 

![El equipo central mantiene el asistente y los equipos de funciones empresariales contribuyen con habilidades](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="d2e5d-127">Crear un Teams centrado en Virtual Assistant</span><span class="sxs-lookup"><span data-stu-id="d2e5d-127">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="d2e5d-128">Microsoft ha publicado una plantilla [Visual Studio para](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) crear asistentes virtuales y habilidades.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-128">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="d2e5d-129">Con la Visual Studio, puedes crear una Virtual Assistant, con una experiencia basada en texto con compatibilidad con tarjetas enriquecciones limitadas con acciones.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-129">With the Visual Studio template, you can create a Virtual Assistant, powered by a text based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="d2e5d-130">Hemos mejorado la plantilla Visual Studio base para incluir Microsoft Teams de plataforma y mejorar las Teams aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-130">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="d2e5d-131">Algunas de las funcionalidades incluyen compatibilidad con tarjetas adaptables enriquecciones, módulos de tareas, chats de grupo o equipos y extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-131">A few of the capabilities include support for rich Adaptive Cards, task modules, teams or group chats, and messaging extensions.</span></span> <span data-ttu-id="d2e5d-132">Para obtener más información sobre cómo Virtual Assistant a Microsoft Teams, vea [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-132">For more information on extending Virtual Assistant to Microsoft Teams, see [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>    
<span data-ttu-id="d2e5d-133">La siguiente imagen muestra el diagrama de alto nivel de una Virtual Assistant solución:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-133">The following image displays the high level diagram of a Virtual Assistant solution:</span></span>

![Diagrama de alto nivel de una Virtual Assistant solución](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="d2e5d-135">Agregar tarjetas adaptables a su Virtual Assistant</span><span class="sxs-lookup"><span data-stu-id="d2e5d-135">Add Adaptive Cards to your Virtual Assistant</span></span>

<span data-ttu-id="d2e5d-136">Para enviar solicitudes correctamente, el Virtual Assistant debe identificar el modelo de LUIS correcto y la habilidad correspondiente asociada a él.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-136">To dispatch requests properly, your Virtual Assistant must identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="d2e5d-137">Sin embargo, el mecanismo de distribución no se puede usar para las actividades de acción de tarjeta, ya que el modelo de LUIS asociado con una habilidad está formado para los textos de acción de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-137">However, the dispatching mechanism cannot be used for card action activities as the LUIS model associated with a skill, is trained for card action texts.</span></span> <span data-ttu-id="d2e5d-138">Los textos de acción de la tarjeta son palabras clave fijas, predefinidas y no comentadas por un usuario.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-138">The card action texts are fixed, pre-defined keywords, and not commented from a user.</span></span>

<span data-ttu-id="d2e5d-139">Este inconveniente se resuelve insertando información de aptitudes en la carga de acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-139">This drawback is resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="d2e5d-140">Cada habilidad debe `skillId` insertarse en el  `value` campo de acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-140">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="d2e5d-141">Debe asegurarse de que cada actividad de acción de tarjeta lleva la información de habilidad pertinente y Virtual Assistant puede usar esta información para el envío.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-141">You must ensure that each card action activity carries the relevant skill information, and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="d2e5d-142">Debe proporcionar en el constructor para asegurarse de que la información de `skillId` aptitudes siempre está presente en las acciones de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-142">You must provide `skillId` in the constructor to ensure that the skill information is always present in card actions.</span></span>
<span data-ttu-id="d2e5d-143">En la siguiente sección se muestra un código de ejemplo de datos de acción de tarjeta:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-143">A card action data sample code is shown in the following section:</span></span>
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

<span data-ttu-id="d2e5d-144">A `SkillCardActionData` continuación, la clase de la Virtual Assistant se presenta para extraer `skillId` de la carga de la acción de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-144">Next, `SkillCardActionData` class in the Virtual Assistant template is introduces to extract `skillId` from the card action payload.</span></span>
<span data-ttu-id="d2e5d-145">En la siguiente sección se muestra un fragmento de código para extraer de la carga de acción de la  `skillId` tarjeta:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-145">A code snippet to extract  `skillId` from card action payload is shown in the following section:</span></span>

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

<span data-ttu-id="d2e5d-146">La implementación se realiza mediante un método de extensión en la [clase Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)</span><span class="sxs-lookup"><span data-stu-id="d2e5d-146">The implementation is done by an extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>
<span data-ttu-id="d2e5d-147">En la siguiente sección se muestra un fragmento de código para extraer de datos de acción de  `skillId` tarjeta:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-147">A code snippet to extract  `skillId` from card action data is shown in the following section:</span></span>

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

### <a name="handle-interruptions"></a><span data-ttu-id="d2e5d-148">Controlar interrupciones</span><span class="sxs-lookup"><span data-stu-id="d2e5d-148">Handle interruptions</span></span>

<span data-ttu-id="d2e5d-149">Virtual Assistant controlar las interrupciones en casos en los que un usuario intenta invocar una habilidad mientras otra habilidad está activa actualmente.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-149">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="d2e5d-150">`TeamsSkillDialog`, y `TeamsSwitchSkillDialog` se presentan en función de [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-150">`TeamsSkillDialog`, and `TeamsSwitchSkillDialog`are introduced based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span></span> <span data-ttu-id="d2e5d-151">Permiten a los usuarios cambiar una experiencia de habilidad de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-151">They enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="d2e5d-152">Para controlar esta solicitud, el Virtual Assistant solicita al usuario un mensaje de confirmación para cambiar de aptitudes:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-152">To handle this request, the Virtual Assistant prompts the user with a confirmation message to switch skills:</span></span>

![Mensaje de confirmación al cambiar a una nueva habilidad](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a><span data-ttu-id="d2e5d-154">Controlar solicitudes de módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="d2e5d-154">Handle task module requests</span></span>

<span data-ttu-id="d2e5d-155">Para agregar capacidades de módulo de tareas a un Virtual Assistant, se incluyen dos métodos adicionales en el controlador Virtual Assistant actividad: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-155">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="d2e5d-156">Estos métodos escuchan las actividades relacionadas con el módulo de tareas de Virtual Assistant, identifican la habilidad asociada con la solicitud y reenvía la solicitud a la habilidad identificada.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-156">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="d2e5d-157">El reenvío de solicitudes se realiza a través [del método SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-157">Request forwarding is done through the [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="d2e5d-158">Devuelve la respuesta según `InvokeResponse` la cual se analiza y se convierte en `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-158">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>


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

<span data-ttu-id="d2e5d-159">Se sigue un enfoque similar para el envío de acciones de tarjeta y las respuestas del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-159">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="d2e5d-160">Los datos de acción de captura y envío del módulo de tareas se actualizan para incluir `skillId` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-160">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="d2e5d-161">El método De extensión `GetSkillId` de actividad extrae de la carga que proporciona detalles sobre la habilidad que debe `skillId` invocarse.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-161">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="d2e5d-162">El fragmento de código `OnTeamsTaskModuleFetchAsync` para y `OnTeamsTaskModuleSubmitAsync` los métodos se proporciona en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-162">The code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods are given in the following section:</span></span>

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

<span data-ttu-id="d2e5d-163">Además, debe incluir todos los dominios de habilidad en la sección del archivo de manifiesto de Virtual Assistant para que los módulos de tareas invocados a través de una habilidad se represente `validDomains` correctamente.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-163">Additionally, you must include all skill domains in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked through a skill render properly.</span></span>

### <a name="handle-collaborative-app-scopes"></a><span data-ttu-id="d2e5d-164">Controlar ámbitos de aplicaciones de colaboración</span><span class="sxs-lookup"><span data-stu-id="d2e5d-164">Handle collaborative app scopes</span></span>

<span data-ttu-id="d2e5d-165">Teams aplicaciones pueden existir en varios ámbitos, incluido el chat 1:1, el chat de grupo y los canales.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-165">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="d2e5d-166">La plantilla Virtual Assistant principal está diseñada para chats 1:1.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-166">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="d2e5d-167">Como parte de la experiencia de incorporación, Virtual Assistant solicita a los usuarios el nombre y mantiene el estado del usuario.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-167">As part of the onboarding experience Virtual Assistant prompts users for name and maintains user state.</span></span> <span data-ttu-id="d2e5d-168">Dado que esa experiencia de incorporación no es adecuada para el chat de grupo o los ámbitos de canal, se ha quitado.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-168">Since that onboarding experience is not suited for group chat or channel scopes it has been removed.</span></span>

<span data-ttu-id="d2e5d-169">Las habilidades deben controlar actividades en varios ámbitos, como chat 1:1, chat de grupo y conversación de canal.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-169">Skills should handle activities in multiple scopes, such as 1:1 chat, group chat, and channel conversation.</span></span> <span data-ttu-id="d2e5d-170">Si alguno de estos ámbitos no es compatible, las aptitudes deben responder con un mensaje adecuado.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-170">If any of these scopes are not supported, skills must respond with an appropriate message.</span></span>

<span data-ttu-id="d2e5d-171">Las siguientes funciones de procesamiento se han agregado al Virtual Assistant principal:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-171">The following  processing functions have been added to Virtual Assistant core:</span></span>

* <span data-ttu-id="d2e5d-172">Virtual Assistant se puede invocar sin ningún mensaje de texto desde un canal o chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-172">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
* <span data-ttu-id="d2e5d-173">Las articulaciones se limpian antes de enviar el mensaje al módulo de envío.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-173">Articulations are cleaned before sending the message to the dispatch module.</span></span> <span data-ttu-id="d2e5d-174">Por ejemplo, quite el @mention necesario del bot.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-174">For example, remove the necessary @mention of the bot.</span></span>

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

### <a name="handle-messaging-extensions"></a><span data-ttu-id="d2e5d-175">Controlar extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d2e5d-175">Handle messaging extensions</span></span>

<span data-ttu-id="d2e5d-176">Los comandos de una extensión de mensajería se declaran en el archivo de manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-176">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="d2e5d-177">La interfaz de usuario de extensión de mensajería está basada en esos comandos.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-177">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="d2e5d-178">Para que Virtual Assistant un comando de extensión de mensajería como una habilidad adjunta, el propio manifiesto de un Virtual Assistant debe contener esos comandos.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-178">For a Virtual Assistant to power a messaging extension command as an attached skill, a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="d2e5d-179">Debes agregar los comandos del manifiesto de una habilidad individual al Virtual Assistant del usuario.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-179">You must add the commands from an individual skill's manifest to the Virtual Assistant's manifest.</span></span> <span data-ttu-id="d2e5d-180">El identificador de comando proporciona información sobre una habilidad asociada anexando el identificador de aplicación de la habilidad a través de un separador `:` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-180">The command ID provides information about an associated skill by appending the skill's app ID through a separator `:`.</span></span>

<span data-ttu-id="d2e5d-181">El fragmento de código del archivo de manifiesto de una habilidad se muestra en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-181">The snippet from a skill's manifest file is shown in the following section:</span></span>

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

<span data-ttu-id="d2e5d-182">El fragmento Virtual Assistant código de archivo de manifiesto correspondiente se muestra en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-182">The corresponding Virtual Assistant manifest file code snippet is shown in the following section:</span></span>

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

<span data-ttu-id="d2e5d-183">Una vez que un usuario invoca los comandos, el Virtual Assistant puede identificar una habilidad asociada mediante el análisis del identificador de comando, actualizar la actividad quitando el sufijo adicional del identificador de comando y reenviarlo a la habilidad `:<skill_id>` correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-183">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix `:<skill_id>` from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="d2e5d-184">El código de una habilidad no necesita controlar el sufijo adicional.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-184">The code for a skill doesnot need to handle the extra suffix.</span></span> <span data-ttu-id="d2e5d-185">Por lo tanto, se evitan conflictos entre los IDs de comandos entre las habilidades.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-185">Thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="d2e5d-186">Con este enfoque, todos los comandos de búsqueda y acción de una habilidad en todos los contextos, como **redacción,** **commandBox** y **mensaje,** están alimentados por un Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-186">With this approach, all the search and action commands of a skill within all contexts, such as **compose**, **commandBox**, and **message** are powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="d2e5d-187">Algunas actividades de extensión de mensajería no incluyen el identificador de comando.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-187">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="d2e5d-188">Por ejemplo, `composeExtension/selectItem` solo contiene el valor de la acción invocar pulsación.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-188">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="d2e5d-189">Para identificar la habilidad asociada, `skillId`  se adjunta a cada tarjeta de elemento mientras se forma una respuesta para `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-189">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="d2e5d-190">Esto es similar al enfoque para agregar [tarjetas adaptables a su Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-190">This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example"></a><span data-ttu-id="d2e5d-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d2e5d-191">Example</span></span>

<span data-ttu-id="d2e5d-192">En el ejemplo siguiente se muestra cómo convertir la plantilla de aplicación Libro a sala en una habilidad de Virtual Assistant: Book-a-room es un Microsoft Teams que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30, 60 o 90 minutos a partir de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-192">The following example shows how to convert the Book-a-room app template to a Virtual Assistant skill: Book-a-room is a Microsoft Teams that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="d2e5d-193">El tiempo predeterminado es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-193">The default time is 30 minutes.</span></span> <span data-ttu-id="d2e5d-194">El bot Book-a-room tiene ámbitos para conversaciones personales o 1:1.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-194">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="d2e5d-195">En la siguiente imagen se muestra Virtual Assistant con un **libro una habilidad de** sala:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-195">The following image displays a Virtual Assistant with a **book a room** skill:</span></span>

![Virtual Assistant con una habilidad de "reservar una sala"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="d2e5d-197">Los siguientes son los cambios delta introducidos para convertirlo en una habilidad que se adjunta a un Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-197">Followings are the delta changes introduced to convert it to a skill which is attached to a Virtual Assistant.</span></span> <span data-ttu-id="d2e5d-198">Se siguen directrices similares para convertir cualquier bot de v4 existente en una habilidad.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-198">Similar guidelines are followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="d2e5d-199">Manifiesto de habilidad</span><span class="sxs-lookup"><span data-stu-id="d2e5d-199">Skill manifest</span></span>

<span data-ttu-id="d2e5d-200">Un manifiesto de habilidad es un archivo JSON que expone el punto de conexión de mensajería, el identificador, el nombre y otros metadatos relevantes de una habilidad.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-200">A skill manifest is a JSON file that exposes a skill's messaging endpoint, ID, name, and other relevant metadata.</span></span> <span data-ttu-id="d2e5d-201">Este manifiesto es diferente del manifiesto usado para la instalación local de una aplicación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-201">This manifest is different than the manifest used for sideloading an app in Microsoft Teams.</span></span> <span data-ttu-id="d2e5d-202">Un Virtual Assistant requiere una ruta de acceso a este archivo como entrada para adjuntar una habilidad.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-202">A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="d2e5d-203">Hemos agregado el siguiente manifiesto a la carpeta wwwroot del bot.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-203">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="d2e5d-204">Integración de LUIS</span><span class="sxs-lookup"><span data-stu-id="d2e5d-204">LUIS Integration</span></span>

<span data-ttu-id="d2e5d-205">Virtual Assistant el modelo de distribución de Virtual Assistant se basa en los modelos DE LUIS de las habilidades adjuntas.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-205">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="d2e5d-206">El modelo de distribución identifica la intención de cada actividad de texto y descubre las aptitudes asociadas a ella.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-206">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="d2e5d-207">Virtual Assistant requiere el modelo DE LUIS de la habilidad en formato como entrada al `.lu` adjuntar una habilidad.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-207">Virtual Assistant requires skill's LUIS model in `.lu` format as an input while attaching a skill.</span></span> <span data-ttu-id="d2e5d-208">LUIS json se convierte al `.lu` formato mediante la herramienta botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-208">LUIS json is converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="d2e5d-209">El bot book-a-room tiene dos comandos principales para los usuarios:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-209">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="d2e5d-210">Hemos creado un modelo de LUIS al comprender estos dos comandos.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-210">We have built a LUIS model by understanding these two commands.</span></span> <span data-ttu-id="d2e5d-211">Los secretos correspondientes deben rellenarse en `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-211">Corresponding secrets must be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="d2e5d-212">El archivo JSON de LUIS correspondiente se [encuentra aquí](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-212">The corresponding LUIS JSON file is found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).</span></span>
<span data-ttu-id="d2e5d-213">El archivo `.lu` correspondiente se muestra en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-213">The corresponding `.lu` file is shown in the following section:</span></span>

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

<span data-ttu-id="d2e5d-214">Con este enfoque, cualquier comando emitido por un usuario para Virtual Assistant relacionado con o se identifica como un comando asociado con el bot y se reenvía `book room` `manage favorites` a esta `Book-a-room` habilidad.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-214">With this approach, any command issued by a user to Virtual Assistant related to `book room` or `manage favorites` are identified as a command associated with `Book-a-room` bot and is forwarded to this skill.</span></span>
<span data-ttu-id="d2e5d-215">Por otra parte, el bot necesita usar el modelo DESI para comprender estos comandos si `Book-a-room room` no están llenos.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-215">On the other hand, `Book-a-room room` bot needs to use LUIS model to understand these commands if they are not typed full.</span></span> <span data-ttu-id="d2e5d-216">Por ejemplo: `I want to manage my favorite rooms`.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-216">For example: `I want to manage my favorite rooms`.</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="d2e5d-217">Compatibilidad con varios idiomas</span><span class="sxs-lookup"><span data-stu-id="d2e5d-217">Multi-Language support</span></span>

<span data-ttu-id="d2e5d-218">Por ejemplo, se crea un modelo de LUIS con solo cultura inglesa.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-218">As an example, a LUIS model with only English culture is created.</span></span> <span data-ttu-id="d2e5d-219">Puede crear modelos de LUIS correspondientes a otros idiomas y agregar una entrada a `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-219">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="d2e5d-220">En paralelo, agregue el archivo `.lu` correspondiente en la ruta de acceso de luisFolder.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-220">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="d2e5d-221">La estructura de carpetas debe ser la siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-221">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="d2e5d-222">Para modificar `languages` el parámetro, actualice el comando botskills de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-222">To modify `languages` parameter, update botskills command as follows:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="d2e5d-223">Virtual Assistant para `SetLocaleMiddleware` identificar la configuración regional actual e invocar el modelo de distribución correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-223">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="d2e5d-224">La actividad del marco de bot tiene un campo de configuración regional que usa este software intermedio.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-224">Bot framework activity has locale field which is used by this middleware.</span></span> <span data-ttu-id="d2e5d-225">También puedes usar lo mismo para tu habilidad.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-225">You can use the same for your skill as well.</span></span> <span data-ttu-id="d2e5d-226">El bot book-a-room no usa este middleware y, en su lugar, obtiene la configuración regional de la entidad clientInfo de la actividad del marco [de bot.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)</span><span class="sxs-lookup"><span data-stu-id="d2e5d-226">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="d2e5d-227">Validación de notificación</span><span class="sxs-lookup"><span data-stu-id="d2e5d-227">Claim validation</span></span>

<span data-ttu-id="d2e5d-228">Hemos agregado [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) para restringir a los autores de llamadas a la habilidad.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-228">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="d2e5d-229">Para permitir que un Virtual Assistant llame a esta habilidad, rellene la matriz desde con el identificador de aplicación de `AllowedCallers` `appsettings` Virtual Assistant específico.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-229">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="d2e5d-230">La matriz de autores de llamadas permitida puede restringir las aptitudes que los consumidores pueden tener acceso a la habilidad.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-230">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="d2e5d-231">Agregue una sola `*` entrada a esta matriz para aceptar llamadas de cualquier consumidor de habilidades.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-231">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```

<span data-ttu-id="d2e5d-232">Para obtener más información sobre cómo agregar validación de notificaciones a una habilidad, vea [Agregar validación de notificaciones a la habilidad](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-232">For more information on adding claims validation to a skill, see [add claims validation to skill](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="limitation-of-card-refresh"></a><span data-ttu-id="d2e5d-233">Limitación de actualización de tarjetas</span><span class="sxs-lookup"><span data-stu-id="d2e5d-233">Limitation of card refresh</span></span> 

<span data-ttu-id="d2e5d-234">La actualización de actividad, como la actualización de tarjetas, aún no se admite Virtual Assistant ([problema de github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-234">Updating activity, such as card refresh is not supported yet through Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="d2e5d-235">Por lo tanto, hemos reemplazado todas las llamadas de actualización de `UpdateActivityAsync` tarjetas con la publicación de nuevas llamadas de tarjeta `SendActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="d2e5d-235">Hence, we have replaced all card refresh calls `UpdateActivityAsync` with posting new card calls `SendActivityAsync`.</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="d2e5d-236">Acciones de tarjeta y flujos de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="d2e5d-236">Card actions and task module flows</span></span>

<span data-ttu-id="d2e5d-237">Para reenviar la acción de la tarjeta o las actividades del módulo de tareas a una habilidad asociada, la habilidad debe `skillId` insertarse en ella.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-237">To forward card action or task module activities to an associated skill, the skill must embed `skillId` to it.</span></span>
<span data-ttu-id="d2e5d-238">`Book-a-room` La acción de la tarjeta bot, la captura del módulo de tareas y las cargas de acción de envío se modifican para que `skillId` contengan como parámetro.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-238">`Book-a-room` bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="d2e5d-239">Para obtener más información, [consulte esta](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) sección de esta documentación.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-239">For more information refer [this](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="d2e5d-240">Controlar actividades desde el ámbito de canal o chat de grupo</span><span class="sxs-lookup"><span data-stu-id="d2e5d-240">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="d2e5d-241">`Book-a-room bot` está diseñado para chats privados, como ámbito personal o 1:1 solo.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-241">`Book-a-room bot` is designed for private chats, such as personal or 1:1 scope only.</span></span> <span data-ttu-id="d2e5d-242">Dado que hemos personalizado Virtual Assistant para admitir ámbitos de canal y chat de grupo, el Virtual Assistant debe invocarse desde los ámbitos de canal y, por lo tanto, el bot debe obtener actividades para el mismo `Book-a-room` ámbito.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-242">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant must be invoked from the channel scopes and thus, `Book-a-room` bot must get activities for the same scope.</span></span> <span data-ttu-id="d2e5d-243">Por `Book-a-room` lo tanto, el bot se personaliza para controlar esas actividades.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-243">Hence `Book-a-room`bot is customized to handle those activities.</span></span> <span data-ttu-id="d2e5d-244">Puede encontrar los métodos de protección `OnMessageActivityAsync` del controlador de actividad del `Book-a-room` bot.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-244">You can find the check in `OnMessageActivityAsync` methods of `Book-a-room` bot's activity handler.</span></span>

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

<span data-ttu-id="d2e5d-245">También puede aprovechar las aptitudes existentes desde el repositorio [de Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) o crear una nueva habilidad desde cero.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-245">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="d2e5d-246">Para crear una nueva habilidad, consulta [tutoriales para crear una nueva habilidad.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="d2e5d-246">For creating a new skill, see [tutorials to create a new skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="d2e5d-247">Para obtener Virtual Assistant arquitectura de habilidades y conocimientos,[vea Virtual Assistant y arquitectura de habilidades](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-247">For Virtual Assistant and skills architecture documentation, see[Virtual Assistant and skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span></span>  

## <a name="limitations-of-virtual-assistant"></a><span data-ttu-id="d2e5d-248">Limitaciones de Virtual Assistant</span><span class="sxs-lookup"><span data-stu-id="d2e5d-248">Limitations of Virtual Assistant</span></span> 

* <span data-ttu-id="d2e5d-249">**EndOfConversation:** una habilidad debe enviar una `endOfConversation` actividad cuando finalice una conversación.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-249">**EndOfConversation**: A skill must send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="d2e5d-250">En función de la actividad, un Virtual Assistant termina el contexto con esa habilidad en particular y vuelve al contexto raíz de Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-250">Based on the activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's root context.</span></span> <span data-ttu-id="d2e5d-251">En el caso del bot Book-a-room, no hay un estado claro en el que se termine la conversación.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-251">For Book-a-room bot, there is no clear state where conversation is ended.</span></span> <span data-ttu-id="d2e5d-252">Por lo tanto, no hemos enviado desde el bot y cuando el usuario quiere volver al contexto raíz, simplemente `endOfConversation` puede hacerlo por `Book-a-room` `start over` comando.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-252">Hence we have not sent `endOfConversation` from `Book-a-room` bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>  
* <span data-ttu-id="d2e5d-253">**Actualización de tarjetas:** la actualización de tarjetas aún no se admite Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-253">**Card refresh**: Card refresh is not yet supported through Virtual Assistant.</span></span>  
* <span data-ttu-id="d2e5d-254">**Extensiones de mensajería**:</span><span class="sxs-lookup"><span data-stu-id="d2e5d-254">**Messaging extensions**:</span></span>
  * <span data-ttu-id="d2e5d-255">Actualmente, un Virtual Assistant puede admitir un máximo de diez comandos para extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-255">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  * <span data-ttu-id="d2e5d-256">La configuración de extensiones de mensajería no está en el ámbito de comandos individuales, sino de toda la extensión en sí.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-256">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="d2e5d-257">Esto limita la configuración de cada habilidad individual mediante Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-257">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  * <span data-ttu-id="d2e5d-258">Los IDs de comandos de extensiones de mensajería tienen una longitud máxima de [64](../resources/schema/manifest-schema.md#composeextensions) caracteres y se usan 37 caracteres para insertar información de aptitudes.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-258">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters are used for embedding skill information.</span></span> <span data-ttu-id="d2e5d-259">Por lo tanto, las restricciones actualizadas para el identificador de comando están limitadas a 27 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-259">Thus, updated constraints for command ID are limited to 27 characters.</span></span>

<span data-ttu-id="d2e5d-260">También puede aprovechar las aptitudes existentes desde el repositorio [de Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) o crear una nueva habilidad desde cero.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-260">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="d2e5d-261">Los tutoriales para las versiones posteriores se pueden [encontrar aquí](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="d2e5d-261">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="d2e5d-262">Consulte la documentación [sobre la](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) arquitectura Virtual Assistant y habilidades.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-262">Please refer to [documentation](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="d2e5d-263">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="d2e5d-263">Code sample</span></span>

| <span data-ttu-id="d2e5d-264">**Ejemplo de nombre**</span><span class="sxs-lookup"><span data-stu-id="d2e5d-264">**Sample name**</span></span> | <span data-ttu-id="d2e5d-265">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="d2e5d-265">**Description**</span></span> | <span data-ttu-id="d2e5d-266">**C#**  **.NET**</span><span class="sxs-lookup"><span data-stu-id="d2e5d-266">**C#**  **.NET**</span></span> |
|----------|-----------------|---------------------------|
| <span data-ttu-id="d2e5d-267">Plantilla de Visual Studio actualizada</span><span class="sxs-lookup"><span data-stu-id="d2e5d-267">Updated visual studio template</span></span> | <span data-ttu-id="d2e5d-268">Plantilla personalizada para admitir las capacidades de teams.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-268">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="d2e5d-269">Ver</span><span class="sxs-lookup"><span data-stu-id="d2e5d-269">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| <span data-ttu-id="d2e5d-270">Código de habilidad de bot de libro a sala</span><span class="sxs-lookup"><span data-stu-id="d2e5d-270">Book-a-room bot skill code</span></span> | <span data-ttu-id="d2e5d-271">Permite buscar y reservar rápidamente una sala de reuniones sobre la marcha.</span><span class="sxs-lookup"><span data-stu-id="d2e5d-271">Lets you quickly find and book a meeting room on the go.</span></span> | [<span data-ttu-id="d2e5d-272">Ver</span><span class="sxs-lookup"><span data-stu-id="d2e5d-272">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |


## <a name="see-also"></a><span data-ttu-id="d2e5d-273">Consulte también</span><span class="sxs-lookup"><span data-stu-id="d2e5d-273">See also</span></span>

* [<span data-ttu-id="d2e5d-274">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="d2e5d-274">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
* [<span data-ttu-id="d2e5d-275">Libro a sala</span><span class="sxs-lookup"><span data-stu-id="d2e5d-275">Book-a-room</span></span>](app-templates.md#book-a-room)
* [<span data-ttu-id="d2e5d-276">Microsoft Teams bot</span><span class="sxs-lookup"><span data-stu-id="d2e5d-276">Microsoft Teams bot</span></span>](../bots/what-are-bots.md)
