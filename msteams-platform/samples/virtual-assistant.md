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
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="b78ac-104">Asistente virtual para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b78ac-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="b78ac-105">Asistente Virtual es una plantilla de código abierto de Microsoft que le permite crear una solución de conversación robusta y mantener un control total sobre la experiencia del usuario, la personalización de marca organizacional y los datos necesarios.</span><span class="sxs-lookup"><span data-stu-id="b78ac-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="b78ac-106">La [plantilla de núcleo del asistente virtual](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) es el bloque de creación básico que reúne las tecnologías de Microsoft necesarias para crear un asistente virtual, incluido [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (Luis)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), así como capacidades esenciales, incluido el registro de habilidades, las cuentas vinculadas, la intención de conversación básica para ofrecer a los usuarios finales una variedad de interacciones y experiencias sin problemas.</span><span class="sxs-lookup"><span data-stu-id="b78ac-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="b78ac-107">Además, las capacidades de plantilla incluyen ejemplos enriquecidos de [conocimientos](https://microsoft.github.io/botframework-solutions/overview/skills)de conversación reutilizables.</span><span class="sxs-lookup"><span data-stu-id="b78ac-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="b78ac-108">Se pueden integrar habilidades individuales en una solución de asistente virtual para habilitar varios escenarios.</span><span class="sxs-lookup"><span data-stu-id="b78ac-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="b78ac-109">Mediante el uso del SDK de bot Framework, las habilidades se presentan en el código fuente, lo que le permite personalizar y ampliar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b78ac-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="b78ac-110">Vea [Qué es una habilidad del marco de bot](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="b78ac-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![Diagrama de información general del asistente virtual](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="b78ac-112">Las actividades de mensajes de texto se redirigen a las aptitudes asociadas por el núcleo del asistente virtual mediante un modelo de [envío](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) .</span><span class="sxs-lookup"><span data-stu-id="b78ac-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="b78ac-113">Consideraciones sobre la implementación</span><span class="sxs-lookup"><span data-stu-id="b78ac-113">Implementation considerations</span></span>

<span data-ttu-id="b78ac-114">La decisión de agregar un asistente virtual puede incluir muchos determinantes y variar para cada organización.</span><span class="sxs-lookup"><span data-stu-id="b78ac-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="b78ac-115">Estos son los factores que admiten la implementación de un asistente virtual para su organización:</span><span class="sxs-lookup"><span data-stu-id="b78ac-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="b78ac-116">Un equipo central administra todas las experiencias de los empleados y tiene la capacidad de crear una experiencia de asistente virtual y administrar las actualizaciones de la experiencia principal, incluida la adición de nuevas habilidades.</span><span class="sxs-lookup"><span data-stu-id="b78ac-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="b78ac-117">Existen varias aplicaciones en todas las funciones empresariales o el número se espera que crezca en el futuro.</span><span class="sxs-lookup"><span data-stu-id="b78ac-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="b78ac-118">Las aplicaciones existentes son personalizables, son propiedad de la organización y se pueden convertir en habilidades para un asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="b78ac-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="b78ac-119">El equipo de las experiencias de los empleados centrales puede influir en las personalizaciones de las aplicaciones existentes y proporcionar las instrucciones necesarias para integrar las aplicaciones existentes como habilidades en la experiencia de asistente virtual</span><span class="sxs-lookup"><span data-stu-id="b78ac-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![El equipo central mantiene el asistente y la función de negocio Teams contribuyen a las habilidades](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="b78ac-121">Crear un asistente virtual centrado en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b78ac-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="b78ac-122">Microsoft ha publicado una [plantilla de Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) para crear asistentes y habilidades virtuales.</span><span class="sxs-lookup"><span data-stu-id="b78ac-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="b78ac-123">Con la plantilla de Visual Studio, puede crear un asistente virtual, con una experiencia basada en texto y compatible con tarjetas complejas con acciones.</span><span class="sxs-lookup"><span data-stu-id="b78ac-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="b78ac-124">Hemos mejorado la plantilla base de Visual Studio para incluir las capacidades de la plataforma de Microsoft Teams y las experiencias de la aplicación de Power excelentes Teams.</span><span class="sxs-lookup"><span data-stu-id="b78ac-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="b78ac-125">Algunas de las capacidades incluyen compatibilidad con las tarjetas adaptables enriquecidas, los módulos de tareas, los chats de grupo y los equipos, y las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b78ac-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="b78ac-126">*Consulte también*, [Tutorial: ampliar el asistente virtual a Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="b78ac-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![Diagrama de alto nivel de una solución de asistente virtual](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="b78ac-128">Agregar tarjetas adaptables a su asistente virtual</span><span class="sxs-lookup"><span data-stu-id="b78ac-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="b78ac-129">Para enviar solicitudes correctamente, el asistente virtual debe identificar el modelo de LUIS correcto y la habilidad correspondiente asociada con ella.</span><span class="sxs-lookup"><span data-stu-id="b78ac-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="b78ac-130">Sin embargo, el mecanismo de distribución no puede usarse para actividades de acción de tarjeta, ya que el modelo LUIS asociado con una habilidad puede no ser entrenado para los textos de acción de tarjeta, ya que son palabras clave predefinidas y fijas, y no utterances de un usuario.</span><span class="sxs-lookup"><span data-stu-id="b78ac-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="b78ac-131">Para solucionarlo, se incrusta la información sobre las habilidades en la carga de acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b78ac-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="b78ac-132">Cada habilidad debe incluirse `skillId` en el `value` campo de las acciones de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b78ac-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="b78ac-133">Esta es la mejor manera de asegurarse de que cada actividad de la acción de la tarjeta incluye la información de habilidad relevante y el asistente virtual puede usar esta información para el envío.</span><span class="sxs-lookup"><span data-stu-id="b78ac-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="b78ac-134">A continuación se muestra un ejemplo de datos de acción de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b78ac-134">Below is a card action data sample.</span></span> <span data-ttu-id="b78ac-135">Al proporcionarle `skillId` en el constructor, garantizamos que la información de habilidades siempre está presente en las acciones de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b78ac-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="b78ac-136">A continuación, se presenta una `SkillCardActionData` clase en la plantilla de asistente virtual para extraer `skillId` de la carga de acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b78ac-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="b78ac-137">A continuación se muestra un fragmento de código para extraer `skillId` de los datos de acción de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b78ac-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="b78ac-138">La implementamos como un método de extensión en la clase [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .</span><span class="sxs-lookup"><span data-stu-id="b78ac-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="b78ac-139">Controlar las interrupciones correctamente</span><span class="sxs-lookup"><span data-stu-id="b78ac-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="b78ac-140">El asistente virtual puede controlar las interrupciones en los casos en los que un usuario intenta invocar una habilidad mientras otra habilidad está activa en ese momento.</span><span class="sxs-lookup"><span data-stu-id="b78ac-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="b78ac-141">hemos lanzado `TeamsSkillDialog` y `TeamsSwitchSkillDialog` , en función de [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de bot Framework, para permitir que los usuarios cambien la experiencia de las Aptitudes de las tarjetas.</span><span class="sxs-lookup"><span data-stu-id="b78ac-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="b78ac-142">Para controlar esta solicitud, el asistente virtual solicita al usuario un mensaje de confirmación para cambiar de aptitudes.</span><span class="sxs-lookup"><span data-stu-id="b78ac-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![Mensaje de confirmación al cambiar a una nueva habilidad](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="b78ac-144">Administración de solicitudes de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="b78ac-144">Handling task module requests</span></span>

<span data-ttu-id="b78ac-145">Para agregar funciones de módulos de tareas a un asistente virtual, se incluyen dos métodos adicionales en el controlador de actividad del asistente virtual: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="b78ac-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="b78ac-146">Estos métodos atienden actividades relacionadas con el módulo de tareas del asistente virtual, identifican la habilidad asociada a la solicitud y reenvían la solicitud a la habilidad identificada.</span><span class="sxs-lookup"><span data-stu-id="b78ac-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="b78ac-147">El reenvío de solicitudes se realiza a través del método [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable) `PostActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="b78ac-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable), `PostActivityAsync` method.</span></span> <span data-ttu-id="b78ac-148">Devuelve la respuesta como la `InvokeResponse` que se analiza y se convierte en `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="b78ac-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="b78ac-149">Se sigue un método similar para la distribución de la acción de tarjeta y las respuestas del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="b78ac-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="b78ac-150">Los datos de la acción buscar y enviar del módulo de tareas se actualizan para incluir `skillId` .</span><span class="sxs-lookup"><span data-stu-id="b78ac-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="b78ac-151">`GetSkillId`El método de extensión de actividad extrae `skillId` de la carga que proporciona detalles sobre la habilidad que se debe invocar.</span><span class="sxs-lookup"><span data-stu-id="b78ac-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="b78ac-152">A continuación se muestra un fragmento de código para `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` los métodos y.</span><span class="sxs-lookup"><span data-stu-id="b78ac-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="b78ac-153">Además, todos los dominios de habilidad deben incluirse en la `validDomains` sección del archivo de manifiesto del asistente virtual para que los módulos de tareas invocados a través de una habilidad se procesen correctamente.</span><span class="sxs-lookup"><span data-stu-id="b78ac-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="b78ac-154">Administración de ámbitos de aplicaciones de colaboración</span><span class="sxs-lookup"><span data-stu-id="b78ac-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="b78ac-155">Las aplicaciones de Microsoft Teams pueden existir en varios ámbitos, entre los que se incluyen chat de 1:1, chat de grupo y canales.</span><span class="sxs-lookup"><span data-stu-id="b78ac-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="b78ac-156">La plantilla principal de asistente virtual está diseñada para 1:1 chats.</span><span class="sxs-lookup"><span data-stu-id="b78ac-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="b78ac-157">Como parte de la experiencia de incorporación, el asistente virtual solicita a los usuarios que tengan el nombre y mantenga el estado del usuario.</span><span class="sxs-lookup"><span data-stu-id="b78ac-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="b78ac-158">Debido a que la experiencia de incorporación no es adecuada para los ámbitos de canal y de chat de grupo, se ha quitado.</span><span class="sxs-lookup"><span data-stu-id="b78ac-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="b78ac-159">Las habilidades deben administrar actividades en varios ámbitos (chat de 1:1, chat de grupo y conversación de canal).</span><span class="sxs-lookup"><span data-stu-id="b78ac-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="b78ac-160">Si alguno de estos ámbitos no se admite, las habilidades deben responder con un mensaje apropiado.</span><span class="sxs-lookup"><span data-stu-id="b78ac-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="b78ac-161">Se han agregado las siguientes funciones de procesamiento al núcleo de asistente virtual:</span><span class="sxs-lookup"><span data-stu-id="b78ac-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="b78ac-162">El asistente virtual se puede invocar sin mensajes de texto desde un canal o chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="b78ac-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="b78ac-163">Articulations se limpian (es decir, quitan los @mention necesarios del bot) antes de enviar el mensaje al módulo de distribución.</span><span class="sxs-lookup"><span data-stu-id="b78ac-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="b78ac-164">Control de las extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="b78ac-164">Handling messaging extensions</span></span>

<span data-ttu-id="b78ac-165">Los comandos para una extensión de mensajería se declaran en el archivo de manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b78ac-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="b78ac-166">La interfaz de usuario de la extensión de mensajería funciona con estos comandos.</span><span class="sxs-lookup"><span data-stu-id="b78ac-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="b78ac-167">Para que un asistente virtual pueda alimentar un comando de extensión de mensajería (como una habilidad adjunta), el propio manifiesto de un asistente virtual debe contener esos comandos.</span><span class="sxs-lookup"><span data-stu-id="b78ac-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="b78ac-168">Los comandos de un manifiesto de una habilidad individual se deben agregar también al manifiesto del asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="b78ac-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="b78ac-169">El identificador de comando proporciona información sobre una habilidad asociada al anexar el identificador de aplicación de la habilidad a través de un separador ( `:` ).</span><span class="sxs-lookup"><span data-stu-id="b78ac-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="b78ac-170">A continuación se muestra un fragmento de código del archivo de manifiesto de una habilidad.</span><span class="sxs-lookup"><span data-stu-id="b78ac-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="b78ac-171">Y, a continuación, se muestra el fragmento de código de archivo de manifiesto de asistente virtual correspondiente.</span><span class="sxs-lookup"><span data-stu-id="b78ac-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="b78ac-172">Una vez que un usuario invoca los comandos, el asistente virtual puede identificar una habilidad asociada mediante el análisis del identificador de comando, la actualización de la actividad al quitar el sufijo adicional ( `:<skill_id>` ) del identificador de comando y reenviarlo a la habilidad correspondiente.</span><span class="sxs-lookup"><span data-stu-id="b78ac-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="b78ac-173">No es necesario que el código de una habilidad controle el sufijo adicional, por lo que se evitan los conflictos entre los identificadores de comando en todas las aptitudes.</span><span class="sxs-lookup"><span data-stu-id="b78ac-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="b78ac-174">Con este enfoque, todos los comandos de búsqueda y acción de una habilidad dentro de todos los contextos ("redacción", "commandBox" y "mensaje") se pueden alimentar por un asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="b78ac-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="b78ac-175">Algunas actividades de extensión de mensajería no incluyen el identificador de comando.</span><span class="sxs-lookup"><span data-stu-id="b78ac-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="b78ac-176">Por ejemplo, `composeExtension/selectItem` contiene solo el valor de la acción de pulsar invocar.</span><span class="sxs-lookup"><span data-stu-id="b78ac-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="b78ac-177">Para identificar la habilidad asociada, `skillId` se adjunta a cada ficha de producto mientras forma una respuesta para `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="b78ac-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="b78ac-178">(Esto es similar al enfoque para [Agregar tarjetas adaptables a su asistente virtual](#add-adaptive-cards-to-your-virtual-assistant).</span><span class="sxs-lookup"><span data-stu-id="b78ac-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="b78ac-179">Ejemplo: convertir la plantilla de aplicación de libro a salón en una habilidad de asistente virtual</span><span class="sxs-lookup"><span data-stu-id="b78ac-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="b78ac-180">[Book-a-Room](app-templates.md#book-a-room) es un [robot de Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios buscar y reservar rápidamente una sala de reuniones para 30 (predeterminado), 60 o 90 minutos a partir de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="b78ac-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="b78ac-181">El bot? o de robot de libro a salón se limita a conversaciones personales o de 1:1.</span><span class="sxs-lookup"><span data-stu-id="b78ac-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![Asistente virtual con una habilidad para "reservar un salón"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="b78ac-183">A continuación se indican los cambios Delta que se han incluido para convertirlos en una habilidad que se puede adjuntar a un asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="b78ac-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="b78ac-184">Se pueden seguir instrucciones similares para convertir cualquier bot existente de V4 en una habilidad.</span><span class="sxs-lookup"><span data-stu-id="b78ac-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="b78ac-185">Manifiesto de habilidad</span><span class="sxs-lookup"><span data-stu-id="b78ac-185">Skill manifest</span></span>

<span data-ttu-id="b78ac-186">Un manifiesto de habilidad es un archivo JSON que expone el punto de conexión de mensajería de una habilidad, el identificador, el nombre y otros metadatos relevantes (este manifiesto es diferente del manifiesto usado para la transferencia local de una aplicación en Microsoft Teams) un asistente virtual requiere una ruta de acceso a este archivo como entrada para adjuntar una habilidad.</span><span class="sxs-lookup"><span data-stu-id="b78ac-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="b78ac-187">Se ha agregado el siguiente manifiesto a la carpeta wwwroot del bot.</span><span class="sxs-lookup"><span data-stu-id="b78ac-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="b78ac-188">Integración de LUIS</span><span class="sxs-lookup"><span data-stu-id="b78ac-188">LUIS Integration</span></span>

<span data-ttu-id="b78ac-189">El modelo de envío del asistente virtual se basa en los modelos LUIS de habilidades adjuntas.</span><span class="sxs-lookup"><span data-stu-id="b78ac-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="b78ac-190">El modelo de envío identifica la intención de cada actividad de texto y encuentra la habilidad asociada a ella.</span><span class="sxs-lookup"><span data-stu-id="b78ac-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="b78ac-191">El asistente virtual requiere el modelo LUIS (en `.lu` formato) de habilidad como entrada al adjuntar una habilidad.</span><span class="sxs-lookup"><span data-stu-id="b78ac-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="b78ac-192">El JSON de LUIS se puede convertir al `.lu` formato mediante la herramienta botframework-CLI.</span><span class="sxs-lookup"><span data-stu-id="b78ac-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="b78ac-193">El bot? a-Room de libros a salón tiene dos comandos principales para los usuarios:</span><span class="sxs-lookup"><span data-stu-id="b78ac-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="b78ac-194">Hemos creado un modelo LUIS que comprenda estos dos comandos.</span><span class="sxs-lookup"><span data-stu-id="b78ac-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="b78ac-195">Los secretos correspondientes deben rellenarse `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="b78ac-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="b78ac-196">El archivo JSON correspondiente de LUIS se puede encontrar [aquí](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) y así es como se `.lu` Ve el archivo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="b78ac-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="b78ac-197">Con este enfoque, cualquier problema de comandos de un usuario a un asistente virtual relacionado con `book room` o `manage favorites` se puede identificar como un comando asociado con un bot de libro a salón y se reenvía a esta habilidad.</span><span class="sxs-lookup"><span data-stu-id="b78ac-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="b78ac-198">Por otra parte, el bot? n de salón de sala-a-Room tiene que usar el modelo LUIS para comprender estos comandos si no se escriben tal cual (por ejemplo: `I want to manage my favorite rooms` ).</span><span class="sxs-lookup"><span data-stu-id="b78ac-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="b78ac-199">Compatibilidad con varios idiomas</span><span class="sxs-lookup"><span data-stu-id="b78ac-199">Multi-Language support</span></span>

<span data-ttu-id="b78ac-200">Para este ejemplo, solo se ha creado un modelo LUIS con una referencia cultural inglés.</span><span class="sxs-lookup"><span data-stu-id="b78ac-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="b78ac-201">Puede crear modelos LUIS correspondientes a otros idiomas y agregar entrada a `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="b78ac-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="b78ac-202">En paralelo, agregue el `.lu` archivo correspondiente en la ruta de acceso luisFolder.</span><span class="sxs-lookup"><span data-stu-id="b78ac-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="b78ac-203">La estructura de carpetas debe ser de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="b78ac-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="b78ac-204">Actualice el comando botskills de la siguiente manera para modificar el `languages` parámetro:</span><span class="sxs-lookup"><span data-stu-id="b78ac-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="b78ac-205">El asistente virtual usa `SetLocaleMiddleware` para identificar la configuración regional actual e invocar el modelo de envío correspondiente.</span><span class="sxs-lookup"><span data-stu-id="b78ac-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="b78ac-206">(La actividad de la estructura de bot tiene un campo de configuración regional que usa este middleware). También le recomendamos que use lo mismo para su habilidad.</span><span class="sxs-lookup"><span data-stu-id="b78ac-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="b78ac-207">El bot? n a-salón de guía no usa este middleware y, en su lugar, obtiene la configuración regional de la [entidad clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de la actividad de la actividad de bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b78ac-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="b78ac-208">Validación de notificaciones</span><span class="sxs-lookup"><span data-stu-id="b78ac-208">Claim validation</span></span>

<span data-ttu-id="b78ac-209">Hemos agregado [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) para restringir la habilidad a los autores de las llamadas.</span><span class="sxs-lookup"><span data-stu-id="b78ac-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="b78ac-210">Para permitir que un asistente virtual llame a esta habilidad, llene `AllowedCallers` la matriz desde `appsettings` con ese identificador de aplicación del asistente virtual en particular.</span><span class="sxs-lookup"><span data-stu-id="b78ac-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="b78ac-211">La matriz de llamadores permitidos puede restringir la habilidad que los consumidores pueden tener acceso a la habilidad.</span><span class="sxs-lookup"><span data-stu-id="b78ac-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="b78ac-212">Agregar una entrada `*` a esta matriz, para aceptar llamadas de cualquier consumidor de aptitudes.</span><span class="sxs-lookup"><span data-stu-id="b78ac-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="b78ac-213">[Aquí](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)encontrará documentación detallada para agregar validación de notificaciones a una habilidad.</span><span class="sxs-lookup"><span data-stu-id="b78ac-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="b78ac-214">Limitación de actualización de tarjeta</span><span class="sxs-lookup"><span data-stu-id="b78ac-214">Card refresh limitation</span></span>

<span data-ttu-id="b78ac-215">La actividad de actualización (actualización de tarjeta) no se admite todavía a través del asistente virtual ([problema de github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span><span class="sxs-lookup"><span data-stu-id="b78ac-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="b78ac-216">Por lo tanto, hemos reemplazado todas las llamadas `UpdateActivityAsync` de actualización de tarjeta () por el registro de nuevas llamadas de tarjeta ( `SendActivityAsync` ).</span><span class="sxs-lookup"><span data-stu-id="b78ac-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="b78ac-217">Acciones de tarjeta y flujos de módulo de tarea</span><span class="sxs-lookup"><span data-stu-id="b78ac-217">Card actions and task module flows</span></span>

<span data-ttu-id="b78ac-218">Para reenviar actividades de la tarjeta o la acción del módulo de tareas a una habilidad asociada, la habilidad debe incrusrse `skillId` en ella.</span><span class="sxs-lookup"><span data-stu-id="b78ac-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="b78ac-219">Acción de tarjeta de bot? a-salón, las cargas de las acciones de búsqueda y envío del módulo de tareas se modifican para que contengan `skillId` un parámetro.</span><span class="sxs-lookup"><span data-stu-id="b78ac-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="b78ac-220">Para obtener más información, consulte [esta](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) sección de esta documentación.</span><span class="sxs-lookup"><span data-stu-id="b78ac-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="b78ac-221">Controlar actividades desde el ámbito del canal o el chat de grupo</span><span class="sxs-lookup"><span data-stu-id="b78ac-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="b78ac-222">El bot? a-Room de libros a salón está diseñado solamente para chats privados (personal/1:1 ámbito).</span><span class="sxs-lookup"><span data-stu-id="b78ac-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="b78ac-223">Como hemos personalizado el asistente virtual para admitir el chat de grupo y los ámbitos de canal, es posible que se invoque al asistente virtual desde estos ámbitos y, por lo tanto, el bot? a-Room del salón podría obtener actividades para el mismo.</span><span class="sxs-lookup"><span data-stu-id="b78ac-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="b78ac-224">Por lo tanto, el bot? a-Room de libros a salón está personalizado para administrar esas actividades.</span><span class="sxs-lookup"><span data-stu-id="b78ac-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="b78ac-225">La comprobación se ha implementado en `OnMessageActivityAsync` métodos del controlador de actividad de un bot de la sala.</span><span class="sxs-lookup"><span data-stu-id="b78ac-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="b78ac-226">También puede aprovechar las habilidades existentes del [repositorio de soluciones de bot Framework](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) o crear una nueva habilidad a partir de cero.</span><span class="sxs-lookup"><span data-stu-id="b78ac-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="b78ac-227">Encontrará tutoriales para la versión más reciente [aquí](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="b78ac-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="b78ac-228">Consulte la [documentación](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0) para obtener información sobre el asistente virtual y la arquitectura de conocimientos.</span><span class="sxs-lookup"><span data-stu-id="b78ac-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   for Virtual Assistant and skills architecture.</span></span>

## <a name="sample-code-to-get-started"></a><span data-ttu-id="b78ac-229">Código de ejemplo para empezar</span><span class="sxs-lookup"><span data-stu-id="b78ac-229">Sample code to get started</span></span>

- [<span data-ttu-id="b78ac-230">Plantilla de Visual Studio actualizada</span><span class="sxs-lookup"><span data-stu-id="b78ac-230">Updated visual studio template</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [<span data-ttu-id="b78ac-231">Código de cualificación de robot-a-salón</span><span class="sxs-lookup"><span data-stu-id="b78ac-231">Book-a-room bot skill code</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="b78ac-232">Limitaciones conocidas del asistente virtual</span><span class="sxs-lookup"><span data-stu-id="b78ac-232">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="b78ac-233">**EndOfConversation**.</span><span class="sxs-lookup"><span data-stu-id="b78ac-233">**EndOfConversation**.</span></span> <span data-ttu-id="b78ac-234">Una habilidad debe enviar una `endOfConversation` actividad cuando termine una conversación.</span><span class="sxs-lookup"><span data-stu-id="b78ac-234">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="b78ac-235">base esta actividad, un asistente virtual finaliza el contexto con esa habilidad en particular y vuelve al contexto (raíz) del asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="b78ac-235">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="b78ac-236">Para el bot? a-Room de libros a salón, no hay un estado claro en el que se puede finalizar la conversación.</span><span class="sxs-lookup"><span data-stu-id="b78ac-236">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="b78ac-237">Por lo tanto, no hemos enviado `endOfConversation` desde el bot? a-a-Room y cuando un usuario desea volver al contexto raíz, simplemente puede hacerlo por `start over` comando.</span><span class="sxs-lookup"><span data-stu-id="b78ac-237">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="b78ac-238">**Actualización**de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b78ac-238">**Card refresh**.</span></span> <span data-ttu-id="b78ac-239">Las actualizaciones de la tarjeta todavía no se admiten a través de asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="b78ac-239">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="b78ac-240">**Extensiones de mensajería**:</span><span class="sxs-lookup"><span data-stu-id="b78ac-240">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="b78ac-241">Actualmente, un asistente virtual puede admitir un máximo de diez comandos para las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b78ac-241">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="b78ac-242">La configuración de las extensiones de mensajería no se centra en comandos individuales, sino en toda la extensión.</span><span class="sxs-lookup"><span data-stu-id="b78ac-242">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="b78ac-243">Esto limita la configuración para cada habilidad individual a través de asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="b78ac-243">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="b78ac-244">Los identificadores de comando de las extensiones de mensajería tienen una longitud máxima de [64 caracteres](../resources/schema/manifest-schema.md#composeextensions) y se usarán 37 caracteres para incrustar información sobre las aptitudes.</span><span class="sxs-lookup"><span data-stu-id="b78ac-244">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="b78ac-245">Por lo tanto, las restricciones actualizadas para el identificador de comando están limitadas a 27 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b78ac-245">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
