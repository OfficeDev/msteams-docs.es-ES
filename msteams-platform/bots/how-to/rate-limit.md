---
title: Optimizar un bot con la limitación de volumen en Teams
description: Limitación de tasas y procedimientos recomendados en Microsoft Teams
ms.topic: conceptual
keywords: limitación de velocidad de bots de teams
ms.openlocfilehash: 690d09e4a3b611c024f32d3776ca73e42d63ee7f
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922506"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="3f0bf-104">Optimizar un bot con la limitación de volumen en Teams</span><span class="sxs-lookup"><span data-stu-id="3f0bf-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="3f0bf-105">La limitación de velocidad es un método para limitar los mensajes a una frecuencia máxima determinada.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="3f0bf-106">Como principio general, la aplicación debe limitar el número de mensajes que publica a una conversación de canal o chat individual.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="3f0bf-107">Esto garantiza una experiencia óptima y los mensajes no aparecen como correo no deseado para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="3f0bf-108">Para proteger Microsoft Teams y sus usuarios, las API de bot proporcionan un límite de velocidad para las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="3f0bf-109">Las aplicaciones que superen este límite reciben un `HTTP 429 Too Many Requests` estado de error.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="3f0bf-110">Todas las solicitudes están sujetas a la misma directiva de limitación de tasas, incluido el envío de mensajes, enumeraciones de canales y recuperaciones de listas.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="3f0bf-111">Como los valores exactos de los límites de tasa están sujetos a cambios, la aplicación debe implementar el comportamiento de devolución adecuado cuando la API devuelva `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="3f0bf-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="3f0bf-112">Controlar límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="3f0bf-112">Handle rate limits</span></span>

<span data-ttu-id="3f0bf-113">Al emitir una operación del SDK de Bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="3f0bf-114">El siguiente código muestra un ejemplo de control de límites de velocidad:</span><span class="sxs-lookup"><span data-stu-id="3f0bf-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="3f0bf-115">Después de controlar los límites de velocidad de los bots, puedes controlar `HTTP 429` las respuestas con un retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="3f0bf-116">Controlar `HTTP 429` respuestas</span><span class="sxs-lookup"><span data-stu-id="3f0bf-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="3f0bf-117">En general, debe tomar precauciones simples para evitar recibir `HTTP 429` respuestas.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="3f0bf-118">Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="3f0bf-119">En su lugar, cree un lote de las solicitudes api.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="3f0bf-120">El uso de un retroceso exponencial con un vibración aleatoria es la forma recomendada de controlar 429s.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="3f0bf-121">Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="3f0bf-122">Después de controlar `HTTP 429` las respuestas, puede seguir el ejemplo para detectar excepciones transitorias.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="3f0bf-123">Ejemplo de detección de excepciones transitorias</span><span class="sxs-lookup"><span data-stu-id="3f0bf-123">Detect transient exceptions example</span></span>

<span data-ttu-id="3f0bf-124">El siguiente código muestra un ejemplo de uso de retroceso exponencial mediante el bloque de aplicación de control de errores transitorios:</span><span class="sxs-lookup"><span data-stu-id="3f0bf-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="3f0bf-125">Puede realizar backoff y reintentos mediante [el control de errores transitorios](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="3f0bf-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="3f0bf-126">Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea agregar el bloque de aplicación de control de [errores transitorios a la solución](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="3f0bf-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="3f0bf-127">Vea también [control de errores transitorios](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="3f0bf-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="3f0bf-128">Después de pasar por el ejemplo para detectar excepciones transitorias, vaya a través del ejemplo de retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="3f0bf-129">Puede usar retroceso exponencial en lugar de reintentar errores.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="3f0bf-130">Ejemplo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="3f0bf-130">Backoff example</span></span>

<span data-ttu-id="3f0bf-131">Además de detectar límites de velocidad, también puede realizar un retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="3f0bf-132">El código siguiente muestra un ejemplo de retroceso exponencial:</span><span class="sxs-lookup"><span data-stu-id="3f0bf-132">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="3f0bf-133">También puede realizar una ejecución `System.Action` de método con la directiva de reintentos descrita en esta sección.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="3f0bf-134">La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de desuso lineal.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="3f0bf-135">Almacena el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="3f0bf-136">Para obtener más información, vea [retry patterns](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="3f0bf-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="3f0bf-137">También puedes controlar el límite de velocidad usando el límite por bot por subproceso.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="3f0bf-138">Por bot por límite de subprocesos</span><span class="sxs-lookup"><span data-stu-id="3f0bf-138">Per bot per thread limit</span></span>

<span data-ttu-id="3f0bf-139">El límite por bot por subproceso controla el tráfico que un bot puede generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-139">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="3f0bf-140">Una conversación es 1:1 entre bot y usuario, un chat de grupo o un canal de un equipo.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-140">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="3f0bf-141">Por lo tanto, si la aplicación envía un mensaje de bot a cada usuario, el límite de subprocesos no limita.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-141">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="3f0bf-142">El límite de subprocesos de 3600 segundos y 1800 operaciones solo se aplica si se envían varios mensajes de bot a un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-142">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="3f0bf-143">El límite global por aplicación por inquilino es de 30 solicitudes por segundo (RPS).</span><span class="sxs-lookup"><span data-stu-id="3f0bf-143">The global limit per app per tenant is 30 Requests Per Second (RPS).</span></span> <span data-ttu-id="3f0bf-144">Por lo tanto, el número total de mensajes de bot por segundo no debe cruzar el límite de subprocesos.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-144">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="3f0bf-145">La división de mensajes en el nivel de servicio da como resultado rps superior a lo esperado.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-145">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="3f0bf-146">Si le preocupa acercarse a los límites, debe implementar la [estrategia de despegar](#backoff-example).</span><span class="sxs-lookup"><span data-stu-id="3f0bf-146">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="3f0bf-147">Los valores proporcionados en esta sección son solo para estimación.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-147">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="3f0bf-148">En la tabla siguiente se proporcionan los límites por bot por subproceso:</span><span class="sxs-lookup"><span data-stu-id="3f0bf-148">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="3f0bf-149">Escenario</span><span class="sxs-lookup"><span data-stu-id="3f0bf-149">Scenario</span></span> | <span data-ttu-id="3f0bf-150">Período de tiempo en segundos</span><span class="sxs-lookup"><span data-stu-id="3f0bf-150">Time period in seconds</span></span> | <span data-ttu-id="3f0bf-151">Operaciones máximas permitidas</span><span class="sxs-lookup"><span data-stu-id="3f0bf-151">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f0bf-152">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-152">Send to conversation</span></span> | <span data-ttu-id="3f0bf-153">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-153">1</span></span> | <span data-ttu-id="3f0bf-154">7 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-154">7</span></span> |
| <span data-ttu-id="3f0bf-155">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-155">Send to conversation</span></span> | <span data-ttu-id="3f0bf-156">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-156">2</span></span> | <span data-ttu-id="3f0bf-157">8 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-157">8</span></span> |
| <span data-ttu-id="3f0bf-158">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-158">Send to conversation</span></span> | <span data-ttu-id="3f0bf-159">30</span><span class="sxs-lookup"><span data-stu-id="3f0bf-159">30</span></span> | <span data-ttu-id="3f0bf-160">60</span><span class="sxs-lookup"><span data-stu-id="3f0bf-160">60</span></span> |
| <span data-ttu-id="3f0bf-161">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-161">Send to conversation</span></span> | <span data-ttu-id="3f0bf-162">3600</span><span class="sxs-lookup"><span data-stu-id="3f0bf-162">3600</span></span> | <span data-ttu-id="3f0bf-163">1800</span><span class="sxs-lookup"><span data-stu-id="3f0bf-163">1800</span></span> |
| <span data-ttu-id="3f0bf-164">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-164">Create conversation</span></span> | <span data-ttu-id="3f0bf-165">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-165">1</span></span> | <span data-ttu-id="3f0bf-166">7 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-166">7</span></span> |
| <span data-ttu-id="3f0bf-167">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-167">Create conversation</span></span> | <span data-ttu-id="3f0bf-168">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-168">2</span></span> | <span data-ttu-id="3f0bf-169">8 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-169">8</span></span> |
| <span data-ttu-id="3f0bf-170">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-170">Create conversation</span></span> | <span data-ttu-id="3f0bf-171">30</span><span class="sxs-lookup"><span data-stu-id="3f0bf-171">30</span></span> | <span data-ttu-id="3f0bf-172">60</span><span class="sxs-lookup"><span data-stu-id="3f0bf-172">60</span></span> |
| <span data-ttu-id="3f0bf-173">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-173">Create conversation</span></span> | <span data-ttu-id="3f0bf-174">3600</span><span class="sxs-lookup"><span data-stu-id="3f0bf-174">3600</span></span> | <span data-ttu-id="3f0bf-175">1800</span><span class="sxs-lookup"><span data-stu-id="3f0bf-175">1800</span></span> |
| <span data-ttu-id="3f0bf-176">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-176">Get conversation members</span></span>| <span data-ttu-id="3f0bf-177">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-177">1</span></span> | <span data-ttu-id="3f0bf-178">14 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-178">14</span></span> |
| <span data-ttu-id="3f0bf-179">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-179">Get conversation members</span></span>| <span data-ttu-id="3f0bf-180">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-180">2</span></span> | <span data-ttu-id="3f0bf-181">16 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-181">16</span></span> |
| <span data-ttu-id="3f0bf-182">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-182">Get conversation members</span></span>| <span data-ttu-id="3f0bf-183">30</span><span class="sxs-lookup"><span data-stu-id="3f0bf-183">30</span></span> | <span data-ttu-id="3f0bf-184">120</span><span class="sxs-lookup"><span data-stu-id="3f0bf-184">120</span></span> |
| <span data-ttu-id="3f0bf-185">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-185">Get conversation members</span></span>| <span data-ttu-id="3f0bf-186">3600</span><span class="sxs-lookup"><span data-stu-id="3f0bf-186">3600</span></span> | <span data-ttu-id="3f0bf-187">3600</span><span class="sxs-lookup"><span data-stu-id="3f0bf-187">3600</span></span> |
| <span data-ttu-id="3f0bf-188">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="3f0bf-188">Get conversations</span></span> | <span data-ttu-id="3f0bf-189">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-189">1</span></span> | <span data-ttu-id="3f0bf-190">14 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-190">14</span></span> |
| <span data-ttu-id="3f0bf-191">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="3f0bf-191">Get conversations</span></span> | <span data-ttu-id="3f0bf-192">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-192">2</span></span> | <span data-ttu-id="3f0bf-193">16 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-193">16</span></span> |
| <span data-ttu-id="3f0bf-194">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="3f0bf-194">Get conversations</span></span> | <span data-ttu-id="3f0bf-195">30</span><span class="sxs-lookup"><span data-stu-id="3f0bf-195">30</span></span> | <span data-ttu-id="3f0bf-196">120</span><span class="sxs-lookup"><span data-stu-id="3f0bf-196">120</span></span> |
| <span data-ttu-id="3f0bf-197">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="3f0bf-197">Get conversations</span></span> | <span data-ttu-id="3f0bf-198">3600</span><span class="sxs-lookup"><span data-stu-id="3f0bf-198">3600</span></span> | <span data-ttu-id="3f0bf-199">3600</span><span class="sxs-lookup"><span data-stu-id="3f0bf-199">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="3f0bf-200">Las versiones anteriores `TeamsInfo.getMembers` de y las API están en `TeamsInfo.GetMembersAsync` desuso.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-200">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="3f0bf-201">Se limitan a cinco solicitudes por minuto y devuelven un máximo de 10.000 miembros por equipo.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-201">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="3f0bf-202">Para actualizar el SDK de Bot Framework y el código para usar los extremos de API paginados más recientes, consulte [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span><span class="sxs-lookup"><span data-stu-id="3f0bf-202">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="3f0bf-203">También puede controlar el límite de velocidad usando el límite por subproceso para todos los bots.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-203">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="3f0bf-204">Límite por subproceso para todos los bots</span><span class="sxs-lookup"><span data-stu-id="3f0bf-204">Per thread limit for all bots</span></span>

<span data-ttu-id="3f0bf-205">El límite por subproceso para todos los bots controla el tráfico que todos los bots pueden generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-205">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="3f0bf-206">Una conversación aquí es 1:1 entre bot y usuario, un chat de grupo o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="3f0bf-206">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="3f0bf-207">En la tabla siguiente se proporciona el límite por subproceso para todos los bots:</span><span class="sxs-lookup"><span data-stu-id="3f0bf-207">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="3f0bf-208">Escenario</span><span class="sxs-lookup"><span data-stu-id="3f0bf-208">Scenario</span></span> | <span data-ttu-id="3f0bf-209">Período de tiempo en segundos</span><span class="sxs-lookup"><span data-stu-id="3f0bf-209">Time period in seconds</span></span> | <span data-ttu-id="3f0bf-210">Operaciones máximas permitidas</span><span class="sxs-lookup"><span data-stu-id="3f0bf-210">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f0bf-211">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-211">Send to conversation</span></span> | <span data-ttu-id="3f0bf-212">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-212">1</span></span> | <span data-ttu-id="3f0bf-213">14 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-213">14</span></span> |
| <span data-ttu-id="3f0bf-214">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-214">Send to conversation</span></span> | <span data-ttu-id="3f0bf-215">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-215">2</span></span> | <span data-ttu-id="3f0bf-216">16 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-216">16</span></span> |
| <span data-ttu-id="3f0bf-217">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-217">Create conversation</span></span> | <span data-ttu-id="3f0bf-218">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-218">1</span></span> | <span data-ttu-id="3f0bf-219">14 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-219">14</span></span> |
| <span data-ttu-id="3f0bf-220">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-220">Create conversation</span></span> | <span data-ttu-id="3f0bf-221">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-221">2</span></span> | <span data-ttu-id="3f0bf-222">16 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-222">16</span></span> |
| <span data-ttu-id="3f0bf-223">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-223">Create conversation</span></span>| <span data-ttu-id="3f0bf-224">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-224">1</span></span> | <span data-ttu-id="3f0bf-225">14 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-225">14</span></span> |
| <span data-ttu-id="3f0bf-226">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-226">Create conversation</span></span>| <span data-ttu-id="3f0bf-227">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-227">2</span></span> | <span data-ttu-id="3f0bf-228">16 </span><span class="sxs-lookup"><span data-stu-id="3f0bf-228">16</span></span> |
| <span data-ttu-id="3f0bf-229">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-229">Get conversation members</span></span>| <span data-ttu-id="3f0bf-230">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-230">1</span></span> | <span data-ttu-id="3f0bf-231">28</span><span class="sxs-lookup"><span data-stu-id="3f0bf-231">28</span></span> |
| <span data-ttu-id="3f0bf-232">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="3f0bf-232">Get conversation members</span></span>| <span data-ttu-id="3f0bf-233">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-233">2</span></span> | <span data-ttu-id="3f0bf-234">32</span><span class="sxs-lookup"><span data-stu-id="3f0bf-234">32</span></span> |
| <span data-ttu-id="3f0bf-235">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="3f0bf-235">Get conversations</span></span> | <span data-ttu-id="3f0bf-236">1</span><span class="sxs-lookup"><span data-stu-id="3f0bf-236">1</span></span> | <span data-ttu-id="3f0bf-237">28</span><span class="sxs-lookup"><span data-stu-id="3f0bf-237">28</span></span> |
| <span data-ttu-id="3f0bf-238">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="3f0bf-238">Get conversations</span></span> | <span data-ttu-id="3f0bf-239">2</span><span class="sxs-lookup"><span data-stu-id="3f0bf-239">2</span></span> | <span data-ttu-id="3f0bf-240">32</span><span class="sxs-lookup"><span data-stu-id="3f0bf-240">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="3f0bf-241">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="3f0bf-241">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f0bf-242">Llamadas y reuniones en el bot</span><span class="sxs-lookup"><span data-stu-id="3f0bf-242">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

