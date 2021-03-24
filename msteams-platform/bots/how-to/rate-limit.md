---
title: Limitación de tasas
description: Limitación de tasas y procedimientos recomendados en Microsoft Teams
keywords: limitación de velocidad de bots de teams
ms.openlocfilehash: 840737178234bcd6e2da1925b0031083717e2b91
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034689"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="4da71-104">Optimizar el bot: limitación de velocidad y procedimientos recomendados en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4da71-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="4da71-105">Como principio general, la aplicación debe limitar el número de mensajes que publica a una conversación de canal o chat individual.</span><span class="sxs-lookup"><span data-stu-id="4da71-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="4da71-106">Esto garantiza una experiencia óptima que no se sienta "correo no deseado" para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="4da71-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="4da71-107">Para proteger Microsoft Teams y sus usuarios, las API de bot limitan la velocidad de las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="4da71-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="4da71-108">Las aplicaciones que superen este límite reciben un `HTTP 429 Too Many Requests` estado de error.</span><span class="sxs-lookup"><span data-stu-id="4da71-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="4da71-109">Todas las solicitudes están sujetas a la misma directiva de limitación de tasas, incluido el envío de mensajes, enumeraciones de canales y recuperaciones de listas.</span><span class="sxs-lookup"><span data-stu-id="4da71-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="4da71-110">Dado que los valores exactos de los límites de tasa están sujetos a cambios, se recomienda que la aplicación implemente el comportamiento de devolución adecuado cuando la API devuelva `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="4da71-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="4da71-111">Control de límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="4da71-111">Handling rate limits</span></span>

<span data-ttu-id="4da71-112">Al emitir una operación del SDK de Bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.</span><span class="sxs-lookup"><span data-stu-id="4da71-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

```csharp
try
{
    // Perform Bot Framework operation
    // for example, await connector.Conversations.UpdateActivityAsync(reply);
}
catch (HttpOperationException ex)
{
    if (ex.Response != null && (uint)ex.Response.StatusCode ==  429)
    {
        //Perform retry of the above operation/Action method
    }
}
```

## <a name="best-practices"></a><span data-ttu-id="4da71-113">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="4da71-113">Best practices</span></span>

<span data-ttu-id="4da71-114">En general, debe tomar precauciones simples para evitar recibir `HTTP 429` respuestas.</span><span class="sxs-lookup"><span data-stu-id="4da71-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="4da71-115">Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal.</span><span class="sxs-lookup"><span data-stu-id="4da71-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="4da71-116">En su lugar, considere la posibilidad de procesar por lotes las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="4da71-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="4da71-117">El uso de un retroceso exponencial con un vibración aleatoria es la forma recomendada de controlar 429s.</span><span class="sxs-lookup"><span data-stu-id="4da71-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="4da71-118">Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.</span><span class="sxs-lookup"><span data-stu-id="4da71-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="4da71-119">Ejemplo: detección de excepciones transitorias</span><span class="sxs-lookup"><span data-stu-id="4da71-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="4da71-120">Este es un ejemplo con retroceso exponencial a través del bloque de aplicaciones de control de errores transitorios.</span><span class="sxs-lookup"><span data-stu-id="4da71-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="4da71-121">Puede realizar backoff y reintentos mediante [el control de errores transitorios](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="4da71-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="4da71-122">Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span><span class="sxs-lookup"><span data-stu-id="4da71-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="4da71-123">*Vea también Control* [de errores transitorios](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="4da71-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
    {
        // List of error codes to retry on
        List<int> transientErrorStatusCodes = new List<int>() { 429 };

        public bool IsTransient(Exception ex)
        {
            if (ex.Message.Contains("429"))
                return true;

            var httpOperationException = ex as HttpOperationException;
            if (httpOperationException != null)
            {
                return httpOperationException.Response != null &&
                        transientErrorStatusCodes.Contains((int)httpOperationException.Response.StatusCode);
            }

            return false;
        }
    }
```

## <a name="example-backoff"></a><span data-ttu-id="4da71-124">Ejemplo: backoff</span><span class="sxs-lookup"><span data-stu-id="4da71-124">Example: backoff</span></span>

<span data-ttu-id="4da71-125">Además de detectar límites de velocidad, también puede realizar un retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="4da71-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

```csharp
/**
* The first parameter specifies the number of retries before failing the operation.
* The second parameter specifies the minimum and maximum backoff time respectively.
* The last parameter is used to add a randomized  +/- 20% delta to avoid numerous clients retrying simultaneously.
*/
var exponentialBackoffRetryStrategy = new ExponentialBackoff(3, TimeSpan.FromSeconds(2),
                        TimeSpan.FromSeconds(20), TimeSpan.FromSeconds(1));


// Define the Retry Policy
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), exponentialBackoffRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync( (Activity)reply) ).ConfigureAwait(false);
```

<span data-ttu-id="4da71-126">También puede realizar una ejecución `System.Action` de método con la directiva de reintentos descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4da71-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="4da71-127">La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de desuso lineal.</span><span class="sxs-lookup"><span data-stu-id="4da71-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="4da71-128">Se recomienda almacenar el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4da71-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="4da71-129">Para obtener más información, consulte esta guía práctica sobre varios patrones de reintentos: [Patrón de reintentos](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="4da71-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="4da71-130">Por bot por límite de subprocesos</span><span class="sxs-lookup"><span data-stu-id="4da71-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="4da71-131">La división de mensajes en el nivel de servicio dará como resultado solicitudes superiores a las esperadas por segundo (RPS).</span><span class="sxs-lookup"><span data-stu-id="4da71-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="4da71-132">Si le preocupa acercarse a los límites, debe implementar la estrategia de backoff descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4da71-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="4da71-133">Los valores proporcionados a continuación son solo para estimación.</span><span class="sxs-lookup"><span data-stu-id="4da71-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="4da71-134">Este límite controla el tráfico que un bot puede generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="4da71-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="4da71-135">Una conversación aquí es 1:1 entre bot y usuario, un chat en grupo o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="4da71-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="4da71-136">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="4da71-136">**Scenario**</span></span> | <span data-ttu-id="4da71-137">**Período de tiempo: (seg.)**</span><span class="sxs-lookup"><span data-stu-id="4da71-137">**Time-period (sec)**</span></span> | <span data-ttu-id="4da71-138">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="4da71-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4da71-139">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-139">Send to Conversation</span></span> | <span data-ttu-id="4da71-140">1</span><span class="sxs-lookup"><span data-stu-id="4da71-140">1</span></span> | <span data-ttu-id="4da71-141">7 </span><span class="sxs-lookup"><span data-stu-id="4da71-141">7</span></span> |
| <span data-ttu-id="4da71-142">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-142">Send to Conversation</span></span> | <span data-ttu-id="4da71-143">2</span><span class="sxs-lookup"><span data-stu-id="4da71-143">2</span></span> | <span data-ttu-id="4da71-144">8 </span><span class="sxs-lookup"><span data-stu-id="4da71-144">8</span></span> |
| <span data-ttu-id="4da71-145">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-145">Send to Conversation</span></span> | <span data-ttu-id="4da71-146">30</span><span class="sxs-lookup"><span data-stu-id="4da71-146">30</span></span> | <span data-ttu-id="4da71-147">60</span><span class="sxs-lookup"><span data-stu-id="4da71-147">60</span></span> |
| <span data-ttu-id="4da71-148">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-148">Send to Conversation</span></span> | <span data-ttu-id="4da71-149">3600</span><span class="sxs-lookup"><span data-stu-id="4da71-149">3600</span></span> | <span data-ttu-id="4da71-150">1800</span><span class="sxs-lookup"><span data-stu-id="4da71-150">1800</span></span> |
| <span data-ttu-id="4da71-151">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-151">Create Conversation</span></span> | <span data-ttu-id="4da71-152">1</span><span class="sxs-lookup"><span data-stu-id="4da71-152">1</span></span> | <span data-ttu-id="4da71-153">7 </span><span class="sxs-lookup"><span data-stu-id="4da71-153">7</span></span> |
| <span data-ttu-id="4da71-154">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-154">Create Conversation</span></span> | <span data-ttu-id="4da71-155">2</span><span class="sxs-lookup"><span data-stu-id="4da71-155">2</span></span> | <span data-ttu-id="4da71-156">8 </span><span class="sxs-lookup"><span data-stu-id="4da71-156">8</span></span> |
| <span data-ttu-id="4da71-157">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-157">Create Conversation</span></span> | <span data-ttu-id="4da71-158">30</span><span class="sxs-lookup"><span data-stu-id="4da71-158">30</span></span> | <span data-ttu-id="4da71-159">60</span><span class="sxs-lookup"><span data-stu-id="4da71-159">60</span></span> |
| <span data-ttu-id="4da71-160">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-160">Create Conversation</span></span> | <span data-ttu-id="4da71-161">3600</span><span class="sxs-lookup"><span data-stu-id="4da71-161">3600</span></span> | <span data-ttu-id="4da71-162">1800</span><span class="sxs-lookup"><span data-stu-id="4da71-162">1800</span></span> |
| <span data-ttu-id="4da71-163">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-163">Get Conversation Members</span></span>| <span data-ttu-id="4da71-164">1</span><span class="sxs-lookup"><span data-stu-id="4da71-164">1</span></span> | <span data-ttu-id="4da71-165">14 </span><span class="sxs-lookup"><span data-stu-id="4da71-165">14</span></span> |
| <span data-ttu-id="4da71-166">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-166">Get Conversation Members</span></span>| <span data-ttu-id="4da71-167">2</span><span class="sxs-lookup"><span data-stu-id="4da71-167">2</span></span> | <span data-ttu-id="4da71-168">16 </span><span class="sxs-lookup"><span data-stu-id="4da71-168">16</span></span> |
| <span data-ttu-id="4da71-169">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-169">Get Conversation Members</span></span>| <span data-ttu-id="4da71-170">30</span><span class="sxs-lookup"><span data-stu-id="4da71-170">30</span></span> | <span data-ttu-id="4da71-171">120</span><span class="sxs-lookup"><span data-stu-id="4da71-171">120</span></span> |
| <span data-ttu-id="4da71-172">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-172">Get Conversation Members</span></span>| <span data-ttu-id="4da71-173">3600</span><span class="sxs-lookup"><span data-stu-id="4da71-173">3600</span></span> | <span data-ttu-id="4da71-174">3600</span><span class="sxs-lookup"><span data-stu-id="4da71-174">3600</span></span> |
| <span data-ttu-id="4da71-175">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="4da71-175">Get Conversations</span></span> | <span data-ttu-id="4da71-176">1</span><span class="sxs-lookup"><span data-stu-id="4da71-176">1</span></span> | <span data-ttu-id="4da71-177">14 </span><span class="sxs-lookup"><span data-stu-id="4da71-177">14</span></span> |
| <span data-ttu-id="4da71-178">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="4da71-178">Get Conversations</span></span> | <span data-ttu-id="4da71-179">2</span><span class="sxs-lookup"><span data-stu-id="4da71-179">2</span></span> | <span data-ttu-id="4da71-180">16 </span><span class="sxs-lookup"><span data-stu-id="4da71-180">16</span></span> |
| <span data-ttu-id="4da71-181">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="4da71-181">Get Conversations</span></span> | <span data-ttu-id="4da71-182">30</span><span class="sxs-lookup"><span data-stu-id="4da71-182">30</span></span> | <span data-ttu-id="4da71-183">120</span><span class="sxs-lookup"><span data-stu-id="4da71-183">120</span></span> |
| <span data-ttu-id="4da71-184">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="4da71-184">Get Conversations</span></span> | <span data-ttu-id="4da71-185">3600</span><span class="sxs-lookup"><span data-stu-id="4da71-185">3600</span></span> | <span data-ttu-id="4da71-186">3600</span><span class="sxs-lookup"><span data-stu-id="4da71-186">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="4da71-187">Las versiones anteriores `TeamsInfo.getMembers` de y las API están en `TeamsInfo.GetMembersAsync` desuso.</span><span class="sxs-lookup"><span data-stu-id="4da71-187">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="4da71-188">Se limitarán a 5 solicitudes por minuto y devolverán un máximo de 10.000 miembros por equipo.</span><span class="sxs-lookup"><span data-stu-id="4da71-188">They will be throttled to 5 requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="4da71-189">Para actualizar el SDK de Bot Framework y el código para usar los extremos de API paginados más recientes, consulte [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span><span class="sxs-lookup"><span data-stu-id="4da71-189">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="4da71-190">Límite por subproceso para todos los bots</span><span class="sxs-lookup"><span data-stu-id="4da71-190">Per thread limit for all bots</span></span>

<span data-ttu-id="4da71-191">Este límite controla el tráfico que todos los bots pueden generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="4da71-191">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="4da71-192">Una conversación aquí es 1:1 entre bot y usuario, un chat en grupo o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="4da71-192">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="4da71-193">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="4da71-193">**Scenario**</span></span> | <span data-ttu-id="4da71-194">**Período de tiempo: (seg.)**</span><span class="sxs-lookup"><span data-stu-id="4da71-194">**Time-period (sec)**</span></span> | <span data-ttu-id="4da71-195">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="4da71-195">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4da71-196">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-196">Send to Conversation</span></span> | <span data-ttu-id="4da71-197">1</span><span class="sxs-lookup"><span data-stu-id="4da71-197">1</span></span> | <span data-ttu-id="4da71-198">14 </span><span class="sxs-lookup"><span data-stu-id="4da71-198">14</span></span> |
| <span data-ttu-id="4da71-199">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-199">Send to Conversation</span></span> | <span data-ttu-id="4da71-200">2</span><span class="sxs-lookup"><span data-stu-id="4da71-200">2</span></span> | <span data-ttu-id="4da71-201">16 </span><span class="sxs-lookup"><span data-stu-id="4da71-201">16</span></span> |
| <span data-ttu-id="4da71-202">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-202">Create Conversation</span></span> | <span data-ttu-id="4da71-203">1</span><span class="sxs-lookup"><span data-stu-id="4da71-203">1</span></span> | <span data-ttu-id="4da71-204">14 </span><span class="sxs-lookup"><span data-stu-id="4da71-204">14</span></span> |
| <span data-ttu-id="4da71-205">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-205">Create Conversation</span></span> | <span data-ttu-id="4da71-206">2</span><span class="sxs-lookup"><span data-stu-id="4da71-206">2</span></span> | <span data-ttu-id="4da71-207">16 </span><span class="sxs-lookup"><span data-stu-id="4da71-207">16</span></span> |
| <span data-ttu-id="4da71-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="4da71-208">CreateConversation</span></span>| <span data-ttu-id="4da71-209">1</span><span class="sxs-lookup"><span data-stu-id="4da71-209">1</span></span> | <span data-ttu-id="4da71-210">14 </span><span class="sxs-lookup"><span data-stu-id="4da71-210">14</span></span> |
| <span data-ttu-id="4da71-211">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="4da71-211">CreateConversation</span></span>| <span data-ttu-id="4da71-212">2</span><span class="sxs-lookup"><span data-stu-id="4da71-212">2</span></span> | <span data-ttu-id="4da71-213">16 </span><span class="sxs-lookup"><span data-stu-id="4da71-213">16</span></span> |
| <span data-ttu-id="4da71-214">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-214">Get Conversation Members</span></span>| <span data-ttu-id="4da71-215">1</span><span class="sxs-lookup"><span data-stu-id="4da71-215">1</span></span> | <span data-ttu-id="4da71-216">28</span><span class="sxs-lookup"><span data-stu-id="4da71-216">28</span></span> |
| <span data-ttu-id="4da71-217">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="4da71-217">Get Conversation Members</span></span>| <span data-ttu-id="4da71-218">2</span><span class="sxs-lookup"><span data-stu-id="4da71-218">2</span></span> | <span data-ttu-id="4da71-219">32</span><span class="sxs-lookup"><span data-stu-id="4da71-219">32</span></span> |
| <span data-ttu-id="4da71-220">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="4da71-220">Get Conversations</span></span> | <span data-ttu-id="4da71-221">1</span><span class="sxs-lookup"><span data-stu-id="4da71-221">1</span></span> | <span data-ttu-id="4da71-222">28</span><span class="sxs-lookup"><span data-stu-id="4da71-222">28</span></span> |
| <span data-ttu-id="4da71-223">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="4da71-223">Get Conversations</span></span> | <span data-ttu-id="4da71-224">2</span><span class="sxs-lookup"><span data-stu-id="4da71-224">2</span></span> | <span data-ttu-id="4da71-225">32</span><span class="sxs-lookup"><span data-stu-id="4da71-225">32</span></span> |
