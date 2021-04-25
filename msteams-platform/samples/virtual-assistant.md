---
title: Asistente virtual para Microsoft Teams
description: Cómo crear bots y habilidades del Asistente virtual para su uso en Microsoft Teams
ms.topic: how-to
keywords: bots de asistente virtual de teams
ms.openlocfilehash: 52591435c5a7e1c65a8f86a7c41fe4a3a4fa5c83
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996026"
---
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="d3e07-104">Asistente virtual para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d3e07-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="d3e07-105">Virtual Assistant es una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida y mantener el control total de la experiencia del usuario, la personalidad de marca de la organización y los datos necesarios.</span><span class="sxs-lookup"><span data-stu-id="d3e07-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="d3e07-106">La [](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) plantilla principal del Asistente virtual es el bloque de creación básico que reúne las tecnologías de Microsoft necesarias para crear un Asistente virtual, incluidos [el SDK de Bot Framework,](https://github.com/microsoft/botframework-sdk)Language [Understanding (LUIS)](https://www.luis.ai/)y [QnA Maker,](https://www.qnamaker.ai/)así como las capacidades esenciales, como el registro de aptitudes, las cuentas vinculadas, la intención de conversación básica para ofrecer a los usuarios finales una variedad de interacciones y experiencias sin problemas.</span><span class="sxs-lookup"><span data-stu-id="d3e07-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="d3e07-107">Además, las capacidades de plantilla incluyen ejemplos enriquecidos de habilidades conversacionales [reutilizables.](https://microsoft.github.io/botframework-solutions/overview/skills)</span><span class="sxs-lookup"><span data-stu-id="d3e07-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="d3e07-108">Las habilidades individuales se pueden integrar en una solución de Asistente virtual para habilitar varios escenarios.</span><span class="sxs-lookup"><span data-stu-id="d3e07-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="d3e07-109">Con el SDK de Bot Framework, las habilidades se presentan en forma de código fuente, lo que permite personalizar y ampliar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d3e07-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="d3e07-110">Consulte [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="d3e07-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![Diagrama de información general del Asistente virtual](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="d3e07-112">Las actividades de mensajes de texto se enrutan a las aptitudes asociadas mediante el núcleo del Asistente virtual mediante un [modelo de](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) distribución.</span><span class="sxs-lookup"><span data-stu-id="d3e07-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="d3e07-113">Consideraciones de implementación</span><span class="sxs-lookup"><span data-stu-id="d3e07-113">Implementation considerations</span></span>

<span data-ttu-id="d3e07-114">La decisión de agregar un Asistente virtual puede incluir muchos determinantes y diferir para cada organización.</span><span class="sxs-lookup"><span data-stu-id="d3e07-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="d3e07-115">Estos son los factores que admiten la implementación de un Asistente virtual para su organización:</span><span class="sxs-lookup"><span data-stu-id="d3e07-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="d3e07-116">Un equipo central administra todas las experiencias de los empleados y tiene la capacidad de crear una experiencia de Asistente virtual y administrar las actualizaciones de la experiencia principal, incluida la adición de nuevas habilidades.</span><span class="sxs-lookup"><span data-stu-id="d3e07-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="d3e07-117">Existen varias aplicaciones en todas las funciones empresariales o se espera que el número crezca en el futuro.</span><span class="sxs-lookup"><span data-stu-id="d3e07-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="d3e07-118">Las aplicaciones existentes son personalizables, pertenecen a la organización y se pueden convertir en habilidades para un Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="d3e07-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="d3e07-119">El equipo central de experiencias de empleados puede influir en las personalizaciones de las aplicaciones existentes y proporcionar instrucciones necesarias para integrar las aplicaciones existentes como habilidades en la experiencia del Asistente virtual</span><span class="sxs-lookup"><span data-stu-id="d3e07-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![El equipo central mantiene el asistente y los equipos de funciones empresariales contribuyen con habilidades](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="d3e07-121">Crear un Asistente virtual centrado en Teams</span><span class="sxs-lookup"><span data-stu-id="d3e07-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="d3e07-122">Microsoft ha publicado una plantilla [Visual Studio para](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) crear asistentes virtuales y habilidades.</span><span class="sxs-lookup"><span data-stu-id="d3e07-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="d3e07-123">Con la Visual Studio, puedes crear un Asistente virtual con una experiencia basada en texto que admita tarjetas enriquecciones limitadas con acciones.</span><span class="sxs-lookup"><span data-stu-id="d3e07-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="d3e07-124">Hemos mejorado la plantilla Visual Studio base para incluir las capacidades de la plataforma de Microsoft Teams y mejorar las excelentes experiencias de la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="d3e07-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="d3e07-125">Algunas de las funcionalidades incluyen compatibilidad con tarjetas adaptables enriquecciones, módulos de tareas, chats de grupo o equipos y extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d3e07-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="d3e07-126">*Vea también*, [Tutorial: Extender el Asistente virtual a Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="d3e07-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![Diagrama de alto nivel de una solución de Asistente virtual](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="d3e07-128">Agregar tarjetas adaptables al Asistente virtual</span><span class="sxs-lookup"><span data-stu-id="d3e07-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="d3e07-129">Para enviar las solicitudes correctamente, el Asistente virtual debe identificar el modelo de LUIS correcto y la habilidad correspondiente asociada a él.</span><span class="sxs-lookup"><span data-stu-id="d3e07-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="d3e07-130">Sin embargo, el mecanismo de distribución no se puede usar para las actividades de acción de tarjeta, ya que es posible que el modelo de LUIS asociado a una habilidad no esté formado para los textos de acción de tarjeta, ya que se trata de palabras clave fijas predefinidas, no expresiones de un usuario.</span><span class="sxs-lookup"><span data-stu-id="d3e07-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="d3e07-131">Hemos resuelto esto insertando información de aptitudes en la carga de acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d3e07-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="d3e07-132">Cada habilidad debe `skillId` insertarse en el  `value` campo de acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d3e07-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="d3e07-133">Esta es la mejor manera de garantizar que cada actividad de acción de tarjeta lleve la información de habilidad relevante y el Asistente virtual pueda usar esta información para el envío.</span><span class="sxs-lookup"><span data-stu-id="d3e07-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="d3e07-134">A continuación se muestra un ejemplo de datos de acción de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d3e07-134">Below is a card action data sample.</span></span> <span data-ttu-id="d3e07-135">Al proporcionar `skillId` en el constructor, nos aseguramos de que la información de aptitudes esté siempre presente en las acciones de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d3e07-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="d3e07-136">A continuación, presentamos `SkillCardActionData` la clase en la plantilla Asistente virtual para extraer de la carga de la acción de `skillId` tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d3e07-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="d3e07-137">A continuación se muestra un fragmento de código para extraer  `skillId` de los datos de la acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d3e07-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="d3e07-138">Lo implementamos como un método de extensión en la [clase Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)</span><span class="sxs-lookup"><span data-stu-id="d3e07-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="d3e07-139">Controlar las interrupciones correctamente</span><span class="sxs-lookup"><span data-stu-id="d3e07-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="d3e07-140">El Asistente virtual puede controlar las interrupciones en casos en los que un usuario intenta invocar una habilidad mientras otra habilidad está activa actualmente.</span><span class="sxs-lookup"><span data-stu-id="d3e07-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="d3e07-141">hemos introducido y , basándonos en `TeamsSkillDialog` `TeamsSwitchSkillDialog` [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) y [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de Bot Framework, para permitir a los usuarios cambiar una experiencia de habilidad de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d3e07-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="d3e07-142">Para controlar esta solicitud, el Asistente virtual solicita al usuario un mensaje de confirmación para cambiar de habilidades.</span><span class="sxs-lookup"><span data-stu-id="d3e07-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![Mensaje de confirmación al cambiar a una nueva habilidad](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="d3e07-144">Controlar solicitudes de módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="d3e07-144">Handling task module requests</span></span>

<span data-ttu-id="d3e07-145">Para agregar capacidades de módulo de tareas a un Asistente virtual, se incluyen dos métodos adicionales en el controlador de actividades del Asistente virtual: `OnTeamsTaskModuleFetchAsync` y `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="d3e07-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="d3e07-146">Estos métodos escuchan las actividades relacionadas con el módulo de tareas del Asistente virtual, identifican la habilidad asociada con la solicitud y reenvía la solicitud a la habilidad identificada.</span><span class="sxs-lookup"><span data-stu-id="d3e07-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="d3e07-147">El reenvío de solicitudes se realiza mediante  [el método SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="d3e07-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="d3e07-148">Devuelve la respuesta según `InvokeResponse` la cual se analiza y se convierte en `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="d3e07-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="d3e07-149">Se sigue un enfoque similar para el envío de acciones de tarjeta y las respuestas del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="d3e07-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="d3e07-150">Los datos de acción de captura y envío del módulo de tareas se actualizan para incluir `skillId` .</span><span class="sxs-lookup"><span data-stu-id="d3e07-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="d3e07-151">El método De extensión `GetSkillId` de actividad extrae de la carga que proporciona detalles sobre la habilidad que debe `skillId` invocarse.</span><span class="sxs-lookup"><span data-stu-id="d3e07-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="d3e07-152">A continuación se muestra un fragmento de código `OnTeamsTaskModuleFetchAsync` para y `OnTeamsTaskModuleSubmitAsync` métodos.</span><span class="sxs-lookup"><span data-stu-id="d3e07-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="d3e07-153">Además, todos los dominios de habilidad deben incluirse en la sección del archivo de manifiesto del Asistente virtual para que los módulos de tareas invocados a través de una habilidad se `validDomains` represente correctamente.</span><span class="sxs-lookup"><span data-stu-id="d3e07-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="d3e07-154">Control de ámbitos de aplicaciones de colaboración</span><span class="sxs-lookup"><span data-stu-id="d3e07-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="d3e07-155">Las aplicaciones de Teams pueden existir en varios ámbitos, incluido el chat 1:1, el chat de grupo y los canales.</span><span class="sxs-lookup"><span data-stu-id="d3e07-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="d3e07-156">La plantilla principal del Asistente virtual está diseñada para chats 1:1.</span><span class="sxs-lookup"><span data-stu-id="d3e07-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="d3e07-157">Como parte de la experiencia de incorporación, el Asistente virtual solicita a los usuarios el nombre y mantiene el estado del usuario.</span><span class="sxs-lookup"><span data-stu-id="d3e07-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="d3e07-158">Dado que esa experiencia de incorporación no es adecuada para los ámbitos de chat o canal de grupo, se ha quitado.</span><span class="sxs-lookup"><span data-stu-id="d3e07-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="d3e07-159">Las habilidades deben controlar las actividades en varios ámbitos (chat 1:1, chat de grupo y conversación de canal).</span><span class="sxs-lookup"><span data-stu-id="d3e07-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="d3e07-160">Si alguno de estos ámbitos no es compatible, las aptitudes deben responder con un mensaje adecuado.</span><span class="sxs-lookup"><span data-stu-id="d3e07-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="d3e07-161">Se han agregado las siguientes funciones de procesamiento al núcleo del Asistente virtual:</span><span class="sxs-lookup"><span data-stu-id="d3e07-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="d3e07-162">El Asistente virtual se puede invocar sin ningún mensaje de texto desde un canal o chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="d3e07-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="d3e07-163">Las articulaciones se limpian (es decir, quitar la @mention del bot) antes de enviar el mensaje al módulo de envío.</span><span class="sxs-lookup"><span data-stu-id="d3e07-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="d3e07-164">Control de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d3e07-164">Handling messaging extensions</span></span>

<span data-ttu-id="d3e07-165">Los comandos de una extensión de mensajería se declaran en el archivo de manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d3e07-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="d3e07-166">La interfaz de usuario de extensión de mensajería está basada en esos comandos.</span><span class="sxs-lookup"><span data-stu-id="d3e07-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="d3e07-167">Para que un Asistente virtual encienda un comando de extensión de mensajería (como una habilidad adjunta), el propio manifiesto de un asistente virtual debe contener esos comandos.</span><span class="sxs-lookup"><span data-stu-id="d3e07-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="d3e07-168">Los comandos del manifiesto de una habilidad individual también deben agregarse al manifiesto del Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="d3e07-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="d3e07-169">El identificador de comando proporciona información sobre una habilidad asociada anexando el identificador de aplicación de la habilidad a través de un separador ( `:` ).</span><span class="sxs-lookup"><span data-stu-id="d3e07-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="d3e07-170">A continuación se muestra un fragmento de código del archivo de manifiesto de una habilidad.</span><span class="sxs-lookup"><span data-stu-id="d3e07-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="d3e07-171">Y, a continuación, se muestra el fragmento de código de código de manifiesto del Asistente virtual correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d3e07-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="d3e07-172">Una vez que un usuario invoca los comandos, el Asistente virtual puede identificar una habilidad asociada mediante el análisis del identificador de comando, actualizar la actividad quitando el sufijo adicional ( ) del identificador de comando y reenviarlo a la habilidad `:<skill_id>` correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d3e07-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="d3e07-173">El código de una habilidad no necesita controlar el sufijo adicional, por lo que se evitan conflictos entre identificadores de comandos en todas las habilidades.</span><span class="sxs-lookup"><span data-stu-id="d3e07-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="d3e07-174">Con este enfoque, todos los comandos de búsqueda y acción de una habilidad en todos los contextos ("redacción", "commandBox" y "mensaje") pueden ser alimentados por un Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="d3e07-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="d3e07-175">Algunas actividades de extensión de mensajería no incluyen el identificador de comando.</span><span class="sxs-lookup"><span data-stu-id="d3e07-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="d3e07-176">Por ejemplo, `composeExtension/selectItem` solo contiene el valor de la acción invocar pulsación.</span><span class="sxs-lookup"><span data-stu-id="d3e07-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="d3e07-177">Para identificar la habilidad asociada, `skillId`  se adjunta a cada tarjeta de elemento mientras se forma una respuesta para `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="d3e07-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="d3e07-178">(Esto es similar al enfoque para agregar [tarjetas adaptables al Asistente virtual](#add-adaptive-cards-to-your-virtual-assistant).</span><span class="sxs-lookup"><span data-stu-id="d3e07-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="d3e07-179">Ejemplo: Convertir la plantilla de aplicación Libro a sala en una habilidad de Asistente virtual</span><span class="sxs-lookup"><span data-stu-id="d3e07-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="d3e07-180">[Book-a-room](app-templates.md#book-a-room) es un bot de [Microsoft Teams](../bots/what-are-bots.md) que permite a los usuarios encontrar y reservar rápidamente una sala de reuniones durante 30 (predeterminado), 60 o 90 minutos a partir de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="d3e07-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="d3e07-181">El bot Book-a-room tiene ámbitos para conversaciones personales o 1:1.</span><span class="sxs-lookup"><span data-stu-id="d3e07-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![Asistente virtual con una habilidad de "reservar una sala"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="d3e07-183">Los siguientes son los cambios delta introducidos para convertirlo en una habilidad que se puede adjuntar a un Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="d3e07-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="d3e07-184">Se pueden seguir instrucciones similares para convertir cualquier bot v4 existente en una habilidad.</span><span class="sxs-lookup"><span data-stu-id="d3e07-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="d3e07-185">Manifiesto de habilidad</span><span class="sxs-lookup"><span data-stu-id="d3e07-185">Skill manifest</span></span>

<span data-ttu-id="d3e07-186">Un manifiesto de habilidad es un archivo JSON que expone el punto de conexión de mensajería, el identificador, el nombre y otros metadatos relevantes de una habilidad (este manifiesto es diferente del manifiesto usado para la instalación local de una aplicación en Microsoft Teams) Un Asistente virtual requiere una ruta de acceso a este archivo como entrada para adjuntar una habilidad.</span><span class="sxs-lookup"><span data-stu-id="d3e07-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="d3e07-187">Hemos agregado el siguiente manifiesto a la carpeta wwwroot del bot.</span><span class="sxs-lookup"><span data-stu-id="d3e07-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="d3e07-188">Integración de LUIS</span><span class="sxs-lookup"><span data-stu-id="d3e07-188">LUIS Integration</span></span>

<span data-ttu-id="d3e07-189">El modelo de distribución del Asistente virtual se basa en los modelos DE LUIS de las habilidades adjuntas.</span><span class="sxs-lookup"><span data-stu-id="d3e07-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="d3e07-190">El modelo de distribución identifica la intención de cada actividad de texto y descubre las aptitudes asociadas a ella.</span><span class="sxs-lookup"><span data-stu-id="d3e07-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="d3e07-191">El Asistente virtual requiere el modelo DE LUIS de la habilidad (en formato) como entrada al `.lu` adjuntar una habilidad.</span><span class="sxs-lookup"><span data-stu-id="d3e07-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="d3e07-192">LUIS json se puede convertir al `.lu` formato mediante la herramienta botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="d3e07-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="d3e07-193">El bot book-a-room tiene dos comandos principales para los usuarios:</span><span class="sxs-lookup"><span data-stu-id="d3e07-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="d3e07-194">Hemos creado un modelo de LUIS que entiende estos dos comandos.</span><span class="sxs-lookup"><span data-stu-id="d3e07-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="d3e07-195">Los secretos correspondientes deben rellenarse en `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="d3e07-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="d3e07-196">El archivo JSON de LUIS correspondiente se puede encontrar [aquí](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) y así es como se ve `.lu` el archivo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d3e07-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="d3e07-197">Con este enfoque, cualquier problema de comando por parte de un usuario al Asistente virtual relacionado con o puede identificarse como un comando asociado con el `book room` bot book-a-room y se reenvía `manage favorites` a esta habilidad.</span><span class="sxs-lookup"><span data-stu-id="d3e07-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="d3e07-198">Por otra parte, el bot de sala de libros debe usar el modelo DE LUIS para comprender estos comandos si no están escritos tal como está (por ejemplo: `I want to manage my favorite rooms` ).</span><span class="sxs-lookup"><span data-stu-id="d3e07-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="d3e07-199">Compatibilidad con varios idiomas</span><span class="sxs-lookup"><span data-stu-id="d3e07-199">Multi-Language support</span></span>

<span data-ttu-id="d3e07-200">Para este ejemplo, solo hemos creado un modelo de LUIS con cultura inglesa.</span><span class="sxs-lookup"><span data-stu-id="d3e07-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="d3e07-201">Puede crear modelos de LUIS correspondientes a otros idiomas y agregar una entrada a `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="d3e07-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="d3e07-202">En paralelo, agregue el archivo `.lu` correspondiente en la ruta de acceso de luisFolder.</span><span class="sxs-lookup"><span data-stu-id="d3e07-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="d3e07-203">La estructura de carpetas debe ser la siguiente:</span><span class="sxs-lookup"><span data-stu-id="d3e07-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="d3e07-204">Actualice el comando botskills de la siguiente manera para modificar el `languages` parámetro:</span><span class="sxs-lookup"><span data-stu-id="d3e07-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="d3e07-205">El Asistente virtual usa `SetLocaleMiddleware` para identificar la configuración regional actual e invocar el modelo de distribución correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d3e07-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="d3e07-206">(La actividad del marco de bot tiene un campo de configuración regional que usa este software intermedio). Te recomendamos que también uses lo mismo para tu habilidad.</span><span class="sxs-lookup"><span data-stu-id="d3e07-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="d3e07-207">El bot book-a-room no usa este middleware y, en su lugar, obtiene la configuración regional de la entidad clientInfo de la actividad del marco [de bot.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)</span><span class="sxs-lookup"><span data-stu-id="d3e07-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="d3e07-208">Validación de notificación</span><span class="sxs-lookup"><span data-stu-id="d3e07-208">Claim validation</span></span>

<span data-ttu-id="d3e07-209">Hemos agregado [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) para restringir a los autores de llamadas a la habilidad.</span><span class="sxs-lookup"><span data-stu-id="d3e07-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="d3e07-210">Para permitir que un Asistente virtual llame a esta habilidad, rellena la matriz desde con el identificador de aplicación de ese `AllowedCallers` `appsettings` asistente virtual en particular.</span><span class="sxs-lookup"><span data-stu-id="d3e07-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="d3e07-211">La matriz de autores de llamadas permitida puede restringir las aptitudes que los consumidores pueden tener acceso a la habilidad.</span><span class="sxs-lookup"><span data-stu-id="d3e07-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="d3e07-212">Agregue una sola `*` entrada a esta matriz para aceptar llamadas de cualquier consumidor de habilidades.</span><span class="sxs-lookup"><span data-stu-id="d3e07-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="d3e07-213">Puede encontrar documentación detallada para agregar la validación de notificaciones a una habilidad [aquí](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d3e07-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="d3e07-214">Limitación de actualización de tarjetas</span><span class="sxs-lookup"><span data-stu-id="d3e07-214">Card refresh limitation</span></span>

<span data-ttu-id="d3e07-215">La actualización de la actividad (actualización de tarjetas) aún no se admite a través del Asistente virtual ([problema de github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span><span class="sxs-lookup"><span data-stu-id="d3e07-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="d3e07-216">Por lo tanto, hemos reemplazado todas las llamadas de actualización de tarjetas ( `UpdateActivityAsync` ) con la publicación de nuevas llamadas de tarjeta( `SendActivityAsync` ).</span><span class="sxs-lookup"><span data-stu-id="d3e07-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="d3e07-217">Acciones de tarjeta y flujos de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="d3e07-217">Card actions and task module flows</span></span>

<span data-ttu-id="d3e07-218">Para reenviar la acción de la tarjeta o las actividades del módulo de tareas a una habilidad asociada, la habilidad debe `skillId` insertarse en ella.</span><span class="sxs-lookup"><span data-stu-id="d3e07-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="d3e07-219">La acción de la tarjeta de bot de libro a sala, la captura del módulo de tareas y las cargas de acción de envío se modifican para que `skillId` contengan como parámetro.</span><span class="sxs-lookup"><span data-stu-id="d3e07-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="d3e07-220">Para obtener más información, [consulte esta](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) sección de esta documentación.</span><span class="sxs-lookup"><span data-stu-id="d3e07-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="d3e07-221">Controlar actividades desde el ámbito de canal o chat de grupo</span><span class="sxs-lookup"><span data-stu-id="d3e07-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="d3e07-222">El bot book-a-room está diseñado solo para chats privados (ámbito personal/1:1).</span><span class="sxs-lookup"><span data-stu-id="d3e07-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="d3e07-223">Dado que hemos personalizado el Asistente virtual para admitir ámbitos de canal y chat en grupo, es posible que el Asistente virtual se invoque desde estos ámbitos y, por lo tanto, el bot de libro a sala pueda obtener actividades para el mismo.</span><span class="sxs-lookup"><span data-stu-id="d3e07-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="d3e07-224">Por lo tanto, el bot Book-a-room se personaliza para controlar esas actividades.</span><span class="sxs-lookup"><span data-stu-id="d3e07-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="d3e07-225">La comprobación se ha puesto en métodos del controlador de actividad del bot de `OnMessageActivityAsync` libro a sala.</span><span class="sxs-lookup"><span data-stu-id="d3e07-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="d3e07-226">También puede aprovechar las aptitudes existentes desde el repositorio [de Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) o crear una nueva habilidad desde cero.</span><span class="sxs-lookup"><span data-stu-id="d3e07-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="d3e07-227">Los tutoriales para las versiones posteriores se pueden [encontrar aquí](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="d3e07-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="d3e07-228">Consulte la documentación [sobre](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) el Asistente virtual y la arquitectura de habilidades.</span><span class="sxs-lookup"><span data-stu-id="d3e07-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="d3e07-229">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="d3e07-229">Code sample</span></span>

| <span data-ttu-id="d3e07-230">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="d3e07-230">**Sample name**</span></span> | <span data-ttu-id="d3e07-231">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="d3e07-231">**Description**</span></span> | <span data-ttu-id="d3e07-232">**C#**</span><span class="sxs-lookup"><span data-stu-id="d3e07-232">**C#**</span></span> | <span data-ttu-id="d3e07-233">**.NET**</span><span class="sxs-lookup"><span data-stu-id="d3e07-233">**.NET**</span></span> |
|----------|-----------------|----------|------------------|
| <span data-ttu-id="d3e07-234">Plantilla de Visual Studio actualizada</span><span class="sxs-lookup"><span data-stu-id="d3e07-234">Updated visual studio template</span></span> | <span data-ttu-id="d3e07-235">Plantilla personalizada para admitir las capacidades de teams.</span><span class="sxs-lookup"><span data-stu-id="d3e07-235">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="d3e07-236">View</span><span class="sxs-lookup"><span data-stu-id="d3e07-236">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| <span data-ttu-id="d3e07-237">Código de habilidad de bot de libro a sala</span><span class="sxs-lookup"><span data-stu-id="d3e07-237">Book-a-room bot skill code</span></span> | <span data-ttu-id="d3e07-238">Permite buscar y reservar rápidamente una sala de reuniones sobre la marcha.</span><span class="sxs-lookup"><span data-stu-id="d3e07-238">Lets you quickly find and book a meeting room on the go.</span></span> |  | [<span data-ttu-id="d3e07-239">View</span><span class="sxs-lookup"><span data-stu-id="d3e07-239">View</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |



## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="d3e07-240">Limitaciones conocidas del Asistente virtual</span><span class="sxs-lookup"><span data-stu-id="d3e07-240">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="d3e07-241">**EndOfConversation**.</span><span class="sxs-lookup"><span data-stu-id="d3e07-241">**EndOfConversation**.</span></span> <span data-ttu-id="d3e07-242">Una habilidad debe enviar una `endOfConversation` actividad cuando finalice una conversación.</span><span class="sxs-lookup"><span data-stu-id="d3e07-242">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="d3e07-243">base de esta actividad, un Asistente virtual termina el contexto con esa habilidad en particular y vuelve al contexto del Asistente virtual (raíz).</span><span class="sxs-lookup"><span data-stu-id="d3e07-243">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="d3e07-244">En el caso del bot Book-a-room, no hay un estado claro en el que se pueda finalizar la conversación.</span><span class="sxs-lookup"><span data-stu-id="d3e07-244">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="d3e07-245">Por lo tanto, no hemos enviado desde el bot Book-a-room y cuando el usuario quiere volver al contexto raíz, simplemente puede `endOfConversation` hacerlo por `start over` comando.</span><span class="sxs-lookup"><span data-stu-id="d3e07-245">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="d3e07-246">**Actualización de tarjeta**.</span><span class="sxs-lookup"><span data-stu-id="d3e07-246">**Card refresh**.</span></span> <span data-ttu-id="d3e07-247">Las actualizaciones de tarjetas aún no se admiten a través del Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="d3e07-247">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="d3e07-248">**Extensiones de mensajería**.:</span><span class="sxs-lookup"><span data-stu-id="d3e07-248">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="d3e07-249">Actualmente, un Asistente virtual puede admitir un máximo de diez comandos para extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d3e07-249">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="d3e07-250">La configuración de extensiones de mensajería no está en el ámbito de comandos individuales, sino de toda la extensión en sí.</span><span class="sxs-lookup"><span data-stu-id="d3e07-250">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="d3e07-251">Esto limita la configuración de cada habilidad individual a través del Asistente virtual.</span><span class="sxs-lookup"><span data-stu-id="d3e07-251">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="d3e07-252">Los IDs de comandos de extensiones de mensajería tienen una longitud máxima de [64](../resources/schema/manifest-schema.md#composeextensions) caracteres y se usarán 37 caracteres para insertar información de aptitudes.</span><span class="sxs-lookup"><span data-stu-id="d3e07-252">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="d3e07-253">Por lo tanto, las restricciones actualizadas para el identificador de comando están limitadas a 27 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d3e07-253">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
