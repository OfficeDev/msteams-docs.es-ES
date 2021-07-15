---
title: Optimizar un bot con la limitación de volumen en Teams
description: Limitación de tasas y procedimientos recomendados en Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: limitación de velocidad de bots de teams
ms.openlocfilehash: 41070bec7905c7003afb917aedcdd08495418602
ms.sourcegitcommit: e327c9766dfa05abb468cdc71319e3cba7c6c79f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/14/2021
ms.locfileid: "53428698"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="9c7df-104">Optimizar un bot con la limitación de volumen en Teams</span><span class="sxs-lookup"><span data-stu-id="9c7df-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="9c7df-105">La limitación de velocidad es un método para limitar los mensajes a una frecuencia máxima determinada.</span><span class="sxs-lookup"><span data-stu-id="9c7df-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="9c7df-106">Como principio general, la aplicación debe limitar el número de mensajes que publica a una conversación de canal o chat individual.</span><span class="sxs-lookup"><span data-stu-id="9c7df-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="9c7df-107">Esto garantiza una experiencia óptima y los mensajes no aparecen como correo no deseado para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="9c7df-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="9c7df-108">Para proteger Microsoft Teams y sus usuarios, las API del bot proporcionan un límite de velocidad para las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="9c7df-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="9c7df-109">Las aplicaciones que superen este límite reciben un `HTTP 429 Too Many Requests` estado de error.</span><span class="sxs-lookup"><span data-stu-id="9c7df-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="9c7df-110">Todas las solicitudes están sujetas a la misma directiva de limitación de tasas, incluido el envío de mensajes, enumeraciones de canales y recuperaciones de listas.</span><span class="sxs-lookup"><span data-stu-id="9c7df-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="9c7df-111">Como los valores exactos de los límites de tasa están sujetos a cambios, la aplicación debe implementar el comportamiento de devolución adecuado cuando la API devuelva `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="9c7df-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="9c7df-112">Controlar límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="9c7df-112">Handle rate limits</span></span>

<span data-ttu-id="9c7df-113">Al emitir una operación del SDK de Bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.</span><span class="sxs-lookup"><span data-stu-id="9c7df-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="9c7df-114">El siguiente código muestra un ejemplo de control de límites de velocidad:</span><span class="sxs-lookup"><span data-stu-id="9c7df-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="9c7df-115">Después de controlar los límites de velocidad de los bots, puedes controlar `HTTP 429` las respuestas con un retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="9c7df-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="9c7df-116">Controlar `HTTP 429` respuestas</span><span class="sxs-lookup"><span data-stu-id="9c7df-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="9c7df-117">En general, debe tomar precauciones simples para evitar recibir `HTTP 429` respuestas.</span><span class="sxs-lookup"><span data-stu-id="9c7df-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="9c7df-118">Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal.</span><span class="sxs-lookup"><span data-stu-id="9c7df-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="9c7df-119">En su lugar, cree un lote de las solicitudes api.</span><span class="sxs-lookup"><span data-stu-id="9c7df-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="9c7df-120">El uso de un retroceso exponencial con un vibración aleatoria es la forma recomendada de controlar 429s.</span><span class="sxs-lookup"><span data-stu-id="9c7df-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="9c7df-121">Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.</span><span class="sxs-lookup"><span data-stu-id="9c7df-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="9c7df-122">Después de controlar `HTTP 429` las respuestas, puede seguir el ejemplo para detectar excepciones transitorias.</span><span class="sxs-lookup"><span data-stu-id="9c7df-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

> [!NOTE]
> <span data-ttu-id="9c7df-123">Además de reintentar el código de error **429**, también se deben volver a intentar los códigos de error **412**, **502** y **504.**</span><span class="sxs-lookup"><span data-stu-id="9c7df-123">In addition to retrying error code **429**, error codes **412**, **502**, and **504** must also be retried.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="9c7df-124">Ejemplo de detección de excepciones transitorias</span><span class="sxs-lookup"><span data-stu-id="9c7df-124">Detect transient exceptions example</span></span>

<span data-ttu-id="9c7df-125">El siguiente código muestra un ejemplo de uso de retroceso exponencial mediante el bloque de aplicación de control de errores transitorios:</span><span class="sxs-lookup"><span data-stu-id="9c7df-125">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="9c7df-126">Puede realizar backoff y reintentos mediante [el control de errores transitorios](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="9c7df-126">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="9c7df-127">Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea agregar el bloque de aplicación de control de errores [transitorios a la solución](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="9c7df-127">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="9c7df-128">Vea también [control de errores transitorios](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="9c7df-128">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="9c7df-129">Después de pasar por el ejemplo para detectar excepciones transitorias, vaya a través del ejemplo de retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="9c7df-129">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="9c7df-130">Puede usar retroceso exponencial en lugar de reintentar errores.</span><span class="sxs-lookup"><span data-stu-id="9c7df-130">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="9c7df-131">Ejemplo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9c7df-131">Backoff example</span></span>

<span data-ttu-id="9c7df-132">Además de detectar límites de velocidad, también puede realizar un retroceso exponencial.</span><span class="sxs-lookup"><span data-stu-id="9c7df-132">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="9c7df-133">El código siguiente muestra un ejemplo de retroceso exponencial:</span><span class="sxs-lookup"><span data-stu-id="9c7df-133">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="9c7df-134">También puede realizar una ejecución `System.Action` de método con la directiva de reintentos descrita en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9c7df-134">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="9c7df-135">La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de desuso lineal.</span><span class="sxs-lookup"><span data-stu-id="9c7df-135">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="9c7df-136">Almacena el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9c7df-136">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="9c7df-137">Para obtener más información, vea [retry patterns](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="9c7df-137">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="9c7df-138">También puedes controlar el límite de velocidad usando el límite por bot por subproceso.</span><span class="sxs-lookup"><span data-stu-id="9c7df-138">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="9c7df-139">Por bot por límite de subprocesos</span><span class="sxs-lookup"><span data-stu-id="9c7df-139">Per bot per thread limit</span></span>

<span data-ttu-id="9c7df-140">El límite por bot por subproceso controla el tráfico que un bot puede generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="9c7df-140">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="9c7df-141">Una conversación es 1:1 entre bot y usuario, un chat de grupo o un canal de un equipo.</span><span class="sxs-lookup"><span data-stu-id="9c7df-141">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="9c7df-142">Por lo tanto, si la aplicación envía un mensaje de bot a cada usuario, el límite de subprocesos no limita.</span><span class="sxs-lookup"><span data-stu-id="9c7df-142">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="9c7df-143">El límite de subprocesos de 3600 segundos y 1800 operaciones solo se aplica si se envían varios mensajes de bot a un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="9c7df-143">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="9c7df-144">El límite global por aplicación por inquilino es de 50 solicitudes por segundo (RPS).</span><span class="sxs-lookup"><span data-stu-id="9c7df-144">The global limit per app per tenant is 50 Requests Per Second (RPS).</span></span> <span data-ttu-id="9c7df-145">Por lo tanto, el número total de mensajes de bot por segundo no debe cruzar el límite de subprocesos.</span><span class="sxs-lookup"><span data-stu-id="9c7df-145">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="9c7df-146">La división de mensajes en el nivel de servicio da como resultado rps superior a lo esperado.</span><span class="sxs-lookup"><span data-stu-id="9c7df-146">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="9c7df-147">Si le preocupa acercarse a los límites, debe implementar la [estrategia de despegar](#backoff-example).</span><span class="sxs-lookup"><span data-stu-id="9c7df-147">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="9c7df-148">Los valores proporcionados en esta sección son solo para estimación.</span><span class="sxs-lookup"><span data-stu-id="9c7df-148">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="9c7df-149">En la tabla siguiente se proporcionan los límites por bot por subproceso:</span><span class="sxs-lookup"><span data-stu-id="9c7df-149">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="9c7df-150">Escenario</span><span class="sxs-lookup"><span data-stu-id="9c7df-150">Scenario</span></span> | <span data-ttu-id="9c7df-151">Período de tiempo en segundos</span><span class="sxs-lookup"><span data-stu-id="9c7df-151">Time period in seconds</span></span> | <span data-ttu-id="9c7df-152">Operaciones máximas permitidas</span><span class="sxs-lookup"><span data-stu-id="9c7df-152">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c7df-153">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-153">Send to conversation</span></span> | <span data-ttu-id="9c7df-154">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-154">1</span></span> | <span data-ttu-id="9c7df-155">7 </span><span class="sxs-lookup"><span data-stu-id="9c7df-155">7</span></span> |
| <span data-ttu-id="9c7df-156">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-156">Send to conversation</span></span> | <span data-ttu-id="9c7df-157">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-157">2</span></span> | <span data-ttu-id="9c7df-158">8 </span><span class="sxs-lookup"><span data-stu-id="9c7df-158">8</span></span> |
| <span data-ttu-id="9c7df-159">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-159">Send to conversation</span></span> | <span data-ttu-id="9c7df-160">30</span><span class="sxs-lookup"><span data-stu-id="9c7df-160">30</span></span> | <span data-ttu-id="9c7df-161">60</span><span class="sxs-lookup"><span data-stu-id="9c7df-161">60</span></span> |
| <span data-ttu-id="9c7df-162">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-162">Send to conversation</span></span> | <span data-ttu-id="9c7df-163">3600</span><span class="sxs-lookup"><span data-stu-id="9c7df-163">3600</span></span> | <span data-ttu-id="9c7df-164">1800</span><span class="sxs-lookup"><span data-stu-id="9c7df-164">1800</span></span> |
| <span data-ttu-id="9c7df-165">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-165">Create conversation</span></span> | <span data-ttu-id="9c7df-166">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-166">1</span></span> | <span data-ttu-id="9c7df-167">7 </span><span class="sxs-lookup"><span data-stu-id="9c7df-167">7</span></span> |
| <span data-ttu-id="9c7df-168">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-168">Create conversation</span></span> | <span data-ttu-id="9c7df-169">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-169">2</span></span> | <span data-ttu-id="9c7df-170">8 </span><span class="sxs-lookup"><span data-stu-id="9c7df-170">8</span></span> |
| <span data-ttu-id="9c7df-171">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-171">Create conversation</span></span> | <span data-ttu-id="9c7df-172">30</span><span class="sxs-lookup"><span data-stu-id="9c7df-172">30</span></span> | <span data-ttu-id="9c7df-173">60</span><span class="sxs-lookup"><span data-stu-id="9c7df-173">60</span></span> |
| <span data-ttu-id="9c7df-174">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-174">Create conversation</span></span> | <span data-ttu-id="9c7df-175">3600</span><span class="sxs-lookup"><span data-stu-id="9c7df-175">3600</span></span> | <span data-ttu-id="9c7df-176">1800</span><span class="sxs-lookup"><span data-stu-id="9c7df-176">1800</span></span> |
| <span data-ttu-id="9c7df-177">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-177">Get conversation members</span></span>| <span data-ttu-id="9c7df-178">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-178">1</span></span> | <span data-ttu-id="9c7df-179">14 </span><span class="sxs-lookup"><span data-stu-id="9c7df-179">14</span></span> |
| <span data-ttu-id="9c7df-180">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-180">Get conversation members</span></span>| <span data-ttu-id="9c7df-181">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-181">2</span></span> | <span data-ttu-id="9c7df-182">16 </span><span class="sxs-lookup"><span data-stu-id="9c7df-182">16</span></span> |
| <span data-ttu-id="9c7df-183">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-183">Get conversation members</span></span>| <span data-ttu-id="9c7df-184">30</span><span class="sxs-lookup"><span data-stu-id="9c7df-184">30</span></span> | <span data-ttu-id="9c7df-185">120</span><span class="sxs-lookup"><span data-stu-id="9c7df-185">120</span></span> |
| <span data-ttu-id="9c7df-186">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-186">Get conversation members</span></span>| <span data-ttu-id="9c7df-187">3600</span><span class="sxs-lookup"><span data-stu-id="9c7df-187">3600</span></span> | <span data-ttu-id="9c7df-188">3600</span><span class="sxs-lookup"><span data-stu-id="9c7df-188">3600</span></span> |
| <span data-ttu-id="9c7df-189">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="9c7df-189">Get conversations</span></span> | <span data-ttu-id="9c7df-190">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-190">1</span></span> | <span data-ttu-id="9c7df-191">14 </span><span class="sxs-lookup"><span data-stu-id="9c7df-191">14</span></span> |
| <span data-ttu-id="9c7df-192">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="9c7df-192">Get conversations</span></span> | <span data-ttu-id="9c7df-193">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-193">2</span></span> | <span data-ttu-id="9c7df-194">16 </span><span class="sxs-lookup"><span data-stu-id="9c7df-194">16</span></span> |
| <span data-ttu-id="9c7df-195">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="9c7df-195">Get conversations</span></span> | <span data-ttu-id="9c7df-196">30</span><span class="sxs-lookup"><span data-stu-id="9c7df-196">30</span></span> | <span data-ttu-id="9c7df-197">120</span><span class="sxs-lookup"><span data-stu-id="9c7df-197">120</span></span> |
| <span data-ttu-id="9c7df-198">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="9c7df-198">Get conversations</span></span> | <span data-ttu-id="9c7df-199">3600</span><span class="sxs-lookup"><span data-stu-id="9c7df-199">3600</span></span> | <span data-ttu-id="9c7df-200">3600</span><span class="sxs-lookup"><span data-stu-id="9c7df-200">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="9c7df-201">Las versiones anteriores `TeamsInfo.getMembers` de y las API están en `TeamsInfo.GetMembersAsync` desuso.</span><span class="sxs-lookup"><span data-stu-id="9c7df-201">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="9c7df-202">Se limitan a cinco solicitudes por minuto y devuelven un máximo de 10.000 miembros por equipo.</span><span class="sxs-lookup"><span data-stu-id="9c7df-202">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="9c7df-203">Para actualizar el SDK de Bot Framework y el código para usar los extremos de API paginados más recientes, consulte [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span><span class="sxs-lookup"><span data-stu-id="9c7df-203">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="9c7df-204">También puede controlar el límite de velocidad usando el límite por subproceso para todos los bots.</span><span class="sxs-lookup"><span data-stu-id="9c7df-204">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="9c7df-205">Límite por subproceso para todos los bots</span><span class="sxs-lookup"><span data-stu-id="9c7df-205">Per thread limit for all bots</span></span>

<span data-ttu-id="9c7df-206">El límite por subproceso para todos los bots controla el tráfico que todos los bots pueden generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="9c7df-206">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="9c7df-207">Una conversación aquí es 1:1 entre bot y usuario, un chat de grupo o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="9c7df-207">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="9c7df-208">En la tabla siguiente se proporciona el límite por subproceso para todos los bots:</span><span class="sxs-lookup"><span data-stu-id="9c7df-208">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="9c7df-209">Escenario</span><span class="sxs-lookup"><span data-stu-id="9c7df-209">Scenario</span></span> | <span data-ttu-id="9c7df-210">Período de tiempo en segundos</span><span class="sxs-lookup"><span data-stu-id="9c7df-210">Time period in seconds</span></span> | <span data-ttu-id="9c7df-211">Operaciones máximas permitidas</span><span class="sxs-lookup"><span data-stu-id="9c7df-211">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c7df-212">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-212">Send to conversation</span></span> | <span data-ttu-id="9c7df-213">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-213">1</span></span> | <span data-ttu-id="9c7df-214">14 </span><span class="sxs-lookup"><span data-stu-id="9c7df-214">14</span></span> |
| <span data-ttu-id="9c7df-215">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-215">Send to conversation</span></span> | <span data-ttu-id="9c7df-216">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-216">2</span></span> | <span data-ttu-id="9c7df-217">16 </span><span class="sxs-lookup"><span data-stu-id="9c7df-217">16</span></span> |
| <span data-ttu-id="9c7df-218">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-218">Create conversation</span></span> | <span data-ttu-id="9c7df-219">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-219">1</span></span> | <span data-ttu-id="9c7df-220">14 </span><span class="sxs-lookup"><span data-stu-id="9c7df-220">14</span></span> |
| <span data-ttu-id="9c7df-221">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-221">Create conversation</span></span> | <span data-ttu-id="9c7df-222">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-222">2</span></span> | <span data-ttu-id="9c7df-223">16 </span><span class="sxs-lookup"><span data-stu-id="9c7df-223">16</span></span> |
| <span data-ttu-id="9c7df-224">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-224">Create conversation</span></span>| <span data-ttu-id="9c7df-225">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-225">1</span></span> | <span data-ttu-id="9c7df-226">14 </span><span class="sxs-lookup"><span data-stu-id="9c7df-226">14</span></span> |
| <span data-ttu-id="9c7df-227">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-227">Create conversation</span></span>| <span data-ttu-id="9c7df-228">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-228">2</span></span> | <span data-ttu-id="9c7df-229">16 </span><span class="sxs-lookup"><span data-stu-id="9c7df-229">16</span></span> |
| <span data-ttu-id="9c7df-230">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-230">Get conversation members</span></span>| <span data-ttu-id="9c7df-231">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-231">1</span></span> | <span data-ttu-id="9c7df-232">28</span><span class="sxs-lookup"><span data-stu-id="9c7df-232">28</span></span> |
| <span data-ttu-id="9c7df-233">Obtener miembros de conversación</span><span class="sxs-lookup"><span data-stu-id="9c7df-233">Get conversation members</span></span>| <span data-ttu-id="9c7df-234">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-234">2</span></span> | <span data-ttu-id="9c7df-235">32</span><span class="sxs-lookup"><span data-stu-id="9c7df-235">32</span></span> |
| <span data-ttu-id="9c7df-236">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="9c7df-236">Get conversations</span></span> | <span data-ttu-id="9c7df-237">1</span><span class="sxs-lookup"><span data-stu-id="9c7df-237">1</span></span> | <span data-ttu-id="9c7df-238">28</span><span class="sxs-lookup"><span data-stu-id="9c7df-238">28</span></span> |
| <span data-ttu-id="9c7df-239">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="9c7df-239">Get conversations</span></span> | <span data-ttu-id="9c7df-240">2</span><span class="sxs-lookup"><span data-stu-id="9c7df-240">2</span></span> | <span data-ttu-id="9c7df-241">32</span><span class="sxs-lookup"><span data-stu-id="9c7df-241">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="9c7df-242">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="9c7df-242">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9c7df-243">Llamadas y reuniones en el bot</span><span class="sxs-lookup"><span data-stu-id="9c7df-243">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

