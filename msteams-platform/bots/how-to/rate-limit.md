---
title: Optimizar el bot con limitación de velocidad en Teams
description: Limitación de tasas y procedimientos recomendados en Microsoft Teams
ms.topic: conceptual
keywords: limitación de velocidad de bots de teams
ms.openlocfilehash: 245c51fc736e5f888299535c3e50ec6232183623
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697000"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="e25c2-104">Optimizar el bot con limitación de velocidad en Teams</span><span class="sxs-lookup"><span data-stu-id="e25c2-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="e25c2-105">La limitación de velocidad es un método para limitar los mensajes a una frecuencia máxima determinada.</span><span class="sxs-lookup"><span data-stu-id="e25c2-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="e25c2-106">Como principio general, la aplicación debe limitar el número de mensajes que publica a una conversación de canal o chat individual.</span><span class="sxs-lookup"><span data-stu-id="e25c2-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="e25c2-107">Esto garantiza una experiencia óptima y los mensajes no aparecen como correo no deseado para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e25c2-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="e25c2-108">Para proteger Microsoft Teams y sus usuarios, las API de bot proporcionan un límite de velocidad para las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="e25c2-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="e25c2-109">Las aplicaciones que superen este límite reciben un `HTTP 429 Too Many Requests` estado de error.</span><span class="sxs-lookup"><span data-stu-id="e25c2-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="e25c2-110">Todas las solicitudes están sujetas a la misma directiva de limitación de tasas, incluido el envío de mensajes, enumeraciones de canales y recuperaciones de listas.</span><span class="sxs-lookup"><span data-stu-id="e25c2-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="e25c2-111">Como los valores exactos de los límites de tasa están sujetos a cambios, la aplicación debe implementar el comportamiento de devolución adecuado cuando la API devuelva `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="e25c2-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="e25c2-112">Controlar límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="e25c2-112">Handle rate limits</span></span>

<span data-ttu-id="e25c2-113">Al emitir una operación del SDK de Bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.</span><span class="sxs-lookup"><span data-stu-id="e25c2-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="e25c2-114">El siguiente código muestra un ejemplo de control de límites de velocidad:</span><span class="sxs-lookup"><span data-stu-id="e25c2-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="e25c2-115">Después de controlar los límites de velocidad de los bots, puedes controlar `HTTP 429` las respuestas con un retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="e25c2-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="e25c2-116">Controlar `HTTP 429` respuestas</span><span class="sxs-lookup"><span data-stu-id="e25c2-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="e25c2-117">En general, debe tomar precauciones simples para evitar recibir `HTTP 429` respuestas.</span><span class="sxs-lookup"><span data-stu-id="e25c2-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="e25c2-118">Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal.</span><span class="sxs-lookup"><span data-stu-id="e25c2-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="e25c2-119">En su lugar, cree un lote de las solicitudes api.</span><span class="sxs-lookup"><span data-stu-id="e25c2-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="e25c2-120">El uso de un retroceso exponencial con un vibración aleatoria es la forma recomendada de controlar 429s.</span><span class="sxs-lookup"><span data-stu-id="e25c2-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="e25c2-121">Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.</span><span class="sxs-lookup"><span data-stu-id="e25c2-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="e25c2-122">Después de controlar `HTTP 429` las respuestas, puede seguir el ejemplo para detectar excepciones transitorias.</span><span class="sxs-lookup"><span data-stu-id="e25c2-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="e25c2-123">Ejemplo de detección de excepciones transitorias</span><span class="sxs-lookup"><span data-stu-id="e25c2-123">Detect transient exceptions example</span></span>

<span data-ttu-id="e25c2-124">El siguiente código muestra un ejemplo de uso de retroceso exponencial mediante el bloque de aplicación de control de errores transitorios:</span><span class="sxs-lookup"><span data-stu-id="e25c2-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="e25c2-125">Puede realizar backoff y reintentos mediante [el control de errores transitorios](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="e25c2-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="e25c2-126">Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea agregar el bloque de aplicación de control de [errores transitorios a la solución](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="e25c2-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="e25c2-127">Vea también [control de errores transitorios](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="e25c2-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="e25c2-128">Después de pasar por el ejemplo para detectar excepciones transitorias, vaya a través del ejemplo de retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="e25c2-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="e25c2-129">Puede usar retroceso exponencial en lugar de reintentar errores.</span><span class="sxs-lookup"><span data-stu-id="e25c2-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="e25c2-130">Ejemplo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="e25c2-130">Backoff example</span></span>

<span data-ttu-id="e25c2-131">Además de detectar límites de velocidad, también puede realizar un retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="e25c2-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="e25c2-132">El código siguiente muestra un ejemplo de retroceso exponencial:</span><span class="sxs-lookup"><span data-stu-id="e25c2-132">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="e25c2-133">También puede realizar una ejecución `System.Action` de método con la directiva de reintentos descrita en esta sección.</span><span class="sxs-lookup"><span data-stu-id="e25c2-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="e25c2-134">La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de desuso lineal.</span><span class="sxs-lookup"><span data-stu-id="e25c2-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="e25c2-135">Almacena el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e25c2-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="e25c2-136">Para obtener más información, vea [retry patterns](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="e25c2-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="e25c2-137">También puedes controlar el límite de velocidad usando el límite por bot por subproceso.</span><span class="sxs-lookup"><span data-stu-id="e25c2-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="e25c2-138">Por bot por límite de subprocesos</span><span class="sxs-lookup"><span data-stu-id="e25c2-138">Per bot per thread limit</span></span>

>[!NOTE]
> <span data-ttu-id="e25c2-139">La división de mensajes en el nivel de servicio da como resultado solicitudes superiores a las esperadas por segundo (RPS).</span><span class="sxs-lookup"><span data-stu-id="e25c2-139">Message splitting at the service level results in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="e25c2-140">Si le preocupa acercarse a los límites, debe implementar la [estrategia de despegar](#backoff-example).</span><span class="sxs-lookup"><span data-stu-id="e25c2-140">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="e25c2-141">Los valores proporcionados en esta sección son solo para estimación.</span><span class="sxs-lookup"><span data-stu-id="e25c2-141">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="e25c2-142">El límite por bot por subproceso controla el tráfico que un bot puede generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="e25c2-142">The per bot per thread limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="e25c2-143">Una conversación aquí es 1:1 entre bot y usuario, un chat de grupo o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="e25c2-143">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="e25c2-144">En la tabla siguiente se proporcionan los límites por bot por subproceso:</span><span class="sxs-lookup"><span data-stu-id="e25c2-144">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="e25c2-145">Escenario</span><span class="sxs-lookup"><span data-stu-id="e25c2-145">Scenario</span></span> | <span data-ttu-id="e25c2-146">Período de tiempo en segundos</span><span class="sxs-lookup"><span data-stu-id="e25c2-146">Time period in seconds</span></span> | <span data-ttu-id="e25c2-147">Operaciones máximas permitidas</span><span class="sxs-lookup"><span data-stu-id="e25c2-147">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e25c2-148">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-148">Send to conversation</span></span> | <span data-ttu-id="e25c2-149">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-149">1</span></span> | <span data-ttu-id="e25c2-150">7 </span><span class="sxs-lookup"><span data-stu-id="e25c2-150">7</span></span> |
| <span data-ttu-id="e25c2-151">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-151">Send to conversation</span></span> | <span data-ttu-id="e25c2-152">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-152">2</span></span> | <span data-ttu-id="e25c2-153">8 </span><span class="sxs-lookup"><span data-stu-id="e25c2-153">8</span></span> |
| <span data-ttu-id="e25c2-154">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-154">Send to conversation</span></span> | <span data-ttu-id="e25c2-155">30</span><span class="sxs-lookup"><span data-stu-id="e25c2-155">30</span></span> | <span data-ttu-id="e25c2-156">60</span><span class="sxs-lookup"><span data-stu-id="e25c2-156">60</span></span> |
| <span data-ttu-id="e25c2-157">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-157">Send to conversation</span></span> | <span data-ttu-id="e25c2-158">3600</span><span class="sxs-lookup"><span data-stu-id="e25c2-158">3600</span></span> | <span data-ttu-id="e25c2-159">1800</span><span class="sxs-lookup"><span data-stu-id="e25c2-159">1800</span></span> |
| <span data-ttu-id="e25c2-160">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-160">Create conversation</span></span> | <span data-ttu-id="e25c2-161">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-161">1</span></span> | <span data-ttu-id="e25c2-162">7 </span><span class="sxs-lookup"><span data-stu-id="e25c2-162">7</span></span> |
| <span data-ttu-id="e25c2-163">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-163">Create conversation</span></span> | <span data-ttu-id="e25c2-164">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-164">2</span></span> | <span data-ttu-id="e25c2-165">8 </span><span class="sxs-lookup"><span data-stu-id="e25c2-165">8</span></span> |
| <span data-ttu-id="e25c2-166">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-166">Create conversation</span></span> | <span data-ttu-id="e25c2-167">30</span><span class="sxs-lookup"><span data-stu-id="e25c2-167">30</span></span> | <span data-ttu-id="e25c2-168">60</span><span class="sxs-lookup"><span data-stu-id="e25c2-168">60</span></span> |
| <span data-ttu-id="e25c2-169">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-169">Create conversation</span></span> | <span data-ttu-id="e25c2-170">3600</span><span class="sxs-lookup"><span data-stu-id="e25c2-170">3600</span></span> | <span data-ttu-id="e25c2-171">1800</span><span class="sxs-lookup"><span data-stu-id="e25c2-171">1800</span></span> |
| <span data-ttu-id="e25c2-172">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-172">Get conversation members</span></span>| <span data-ttu-id="e25c2-173">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-173">1</span></span> | <span data-ttu-id="e25c2-174">14 </span><span class="sxs-lookup"><span data-stu-id="e25c2-174">14</span></span> |
| <span data-ttu-id="e25c2-175">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-175">Get conversation members</span></span>| <span data-ttu-id="e25c2-176">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-176">2</span></span> | <span data-ttu-id="e25c2-177">16 </span><span class="sxs-lookup"><span data-stu-id="e25c2-177">16</span></span> |
| <span data-ttu-id="e25c2-178">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-178">Get conversation members</span></span>| <span data-ttu-id="e25c2-179">30</span><span class="sxs-lookup"><span data-stu-id="e25c2-179">30</span></span> | <span data-ttu-id="e25c2-180">120</span><span class="sxs-lookup"><span data-stu-id="e25c2-180">120</span></span> |
| <span data-ttu-id="e25c2-181">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-181">Get conversation members</span></span>| <span data-ttu-id="e25c2-182">3600</span><span class="sxs-lookup"><span data-stu-id="e25c2-182">3600</span></span> | <span data-ttu-id="e25c2-183">3600</span><span class="sxs-lookup"><span data-stu-id="e25c2-183">3600</span></span> |
| <span data-ttu-id="e25c2-184">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="e25c2-184">Get conversations</span></span> | <span data-ttu-id="e25c2-185">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-185">1</span></span> | <span data-ttu-id="e25c2-186">14 </span><span class="sxs-lookup"><span data-stu-id="e25c2-186">14</span></span> |
| <span data-ttu-id="e25c2-187">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="e25c2-187">Get conversations</span></span> | <span data-ttu-id="e25c2-188">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-188">2</span></span> | <span data-ttu-id="e25c2-189">16 </span><span class="sxs-lookup"><span data-stu-id="e25c2-189">16</span></span> |
| <span data-ttu-id="e25c2-190">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="e25c2-190">Get conversations</span></span> | <span data-ttu-id="e25c2-191">30</span><span class="sxs-lookup"><span data-stu-id="e25c2-191">30</span></span> | <span data-ttu-id="e25c2-192">120</span><span class="sxs-lookup"><span data-stu-id="e25c2-192">120</span></span> |
| <span data-ttu-id="e25c2-193">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="e25c2-193">Get conversations</span></span> | <span data-ttu-id="e25c2-194">3600</span><span class="sxs-lookup"><span data-stu-id="e25c2-194">3600</span></span> | <span data-ttu-id="e25c2-195">3600</span><span class="sxs-lookup"><span data-stu-id="e25c2-195">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="e25c2-196">Las versiones anteriores `TeamsInfo.getMembers` de y las API están en `TeamsInfo.GetMembersAsync` desuso.</span><span class="sxs-lookup"><span data-stu-id="e25c2-196">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="e25c2-197">Se limitan a cinco solicitudes por minuto y devuelven un máximo de 10.000 miembros por equipo.</span><span class="sxs-lookup"><span data-stu-id="e25c2-197">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="e25c2-198">Para actualizar el SDK de Bot Framework y el código para usar los extremos de API paginados más recientes, consulte [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span><span class="sxs-lookup"><span data-stu-id="e25c2-198">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="e25c2-199">También puede controlar el límite de velocidad usando el límite por subproceso para todos los bots.</span><span class="sxs-lookup"><span data-stu-id="e25c2-199">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="e25c2-200">Límite por subproceso para todos los bots</span><span class="sxs-lookup"><span data-stu-id="e25c2-200">Per thread limit for all bots</span></span>

<span data-ttu-id="e25c2-201">El límite por subproceso para todos los bots controla el tráfico que todos los bots pueden generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="e25c2-201">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="e25c2-202">Una conversación aquí es 1:1 entre bot y usuario, un chat de grupo o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="e25c2-202">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="e25c2-203">En la tabla siguiente se proporciona el límite por subproceso para todos los bots:</span><span class="sxs-lookup"><span data-stu-id="e25c2-203">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="e25c2-204">Escenario</span><span class="sxs-lookup"><span data-stu-id="e25c2-204">Scenario</span></span> | <span data-ttu-id="e25c2-205">Período de tiempo en segundos</span><span class="sxs-lookup"><span data-stu-id="e25c2-205">Time period in seconds</span></span> | <span data-ttu-id="e25c2-206">Operaciones máximas permitidas</span><span class="sxs-lookup"><span data-stu-id="e25c2-206">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e25c2-207">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-207">Send to conversation</span></span> | <span data-ttu-id="e25c2-208">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-208">1</span></span> | <span data-ttu-id="e25c2-209">14 </span><span class="sxs-lookup"><span data-stu-id="e25c2-209">14</span></span> |
| <span data-ttu-id="e25c2-210">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-210">Send to conversation</span></span> | <span data-ttu-id="e25c2-211">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-211">2</span></span> | <span data-ttu-id="e25c2-212">16 </span><span class="sxs-lookup"><span data-stu-id="e25c2-212">16</span></span> |
| <span data-ttu-id="e25c2-213">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-213">Create conversation</span></span> | <span data-ttu-id="e25c2-214">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-214">1</span></span> | <span data-ttu-id="e25c2-215">14 </span><span class="sxs-lookup"><span data-stu-id="e25c2-215">14</span></span> |
| <span data-ttu-id="e25c2-216">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-216">Create conversation</span></span> | <span data-ttu-id="e25c2-217">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-217">2</span></span> | <span data-ttu-id="e25c2-218">16 </span><span class="sxs-lookup"><span data-stu-id="e25c2-218">16</span></span> |
| <span data-ttu-id="e25c2-219">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-219">Create conversation</span></span>| <span data-ttu-id="e25c2-220">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-220">1</span></span> | <span data-ttu-id="e25c2-221">14 </span><span class="sxs-lookup"><span data-stu-id="e25c2-221">14</span></span> |
| <span data-ttu-id="e25c2-222">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-222">Create conversation</span></span>| <span data-ttu-id="e25c2-223">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-223">2</span></span> | <span data-ttu-id="e25c2-224">16 </span><span class="sxs-lookup"><span data-stu-id="e25c2-224">16</span></span> |
| <span data-ttu-id="e25c2-225">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-225">Get conversation members</span></span>| <span data-ttu-id="e25c2-226">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-226">1</span></span> | <span data-ttu-id="e25c2-227">28</span><span class="sxs-lookup"><span data-stu-id="e25c2-227">28</span></span> |
| <span data-ttu-id="e25c2-228">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="e25c2-228">Get conversation members</span></span>| <span data-ttu-id="e25c2-229">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-229">2</span></span> | <span data-ttu-id="e25c2-230">32</span><span class="sxs-lookup"><span data-stu-id="e25c2-230">32</span></span> |
| <span data-ttu-id="e25c2-231">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="e25c2-231">Get conversations</span></span> | <span data-ttu-id="e25c2-232">1</span><span class="sxs-lookup"><span data-stu-id="e25c2-232">1</span></span> | <span data-ttu-id="e25c2-233">28</span><span class="sxs-lookup"><span data-stu-id="e25c2-233">28</span></span> |
| <span data-ttu-id="e25c2-234">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="e25c2-234">Get conversations</span></span> | <span data-ttu-id="e25c2-235">2</span><span class="sxs-lookup"><span data-stu-id="e25c2-235">2</span></span> | <span data-ttu-id="e25c2-236">32</span><span class="sxs-lookup"><span data-stu-id="e25c2-236">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="e25c2-237">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="e25c2-237">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e25c2-238">Bots de llamadas y reuniones</span><span class="sxs-lookup"><span data-stu-id="e25c2-238">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

