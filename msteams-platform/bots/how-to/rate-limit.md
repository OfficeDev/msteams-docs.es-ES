---
title: Limitación de velocidad
description: Limitación de velocidad y procedimientos recomendados en Microsoft Teams
keywords: limitación de velocidad de bots de equipo
ms.openlocfilehash: 145f65a7e17b833e11631dfc219d9f5732f43bc6
ms.sourcegitcommit: 6c692734a382865531a83b9ebd6f604212f484fc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "42371768"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="556cf-104">Optimizar el bot: límites de velocidad y procedimientos recomendados en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="556cf-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="556cf-105">Como principio general, la aplicación debe limitar el número de mensajes que envía a un chat o a una conversación de canal individuales.</span><span class="sxs-lookup"><span data-stu-id="556cf-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="556cf-106">Esto garantiza una experiencia óptima que no siente "correo no deseado" para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="556cf-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="556cf-107">Para proteger Microsoft Teams y sus usuarios, la API de bot limita la velocidad de las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="556cf-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="556cf-108">Las aplicaciones que superen este límite recibirán un `HTTP 429 Too Many Requests` estado de error.</span><span class="sxs-lookup"><span data-stu-id="556cf-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="556cf-109">Todas las solicitudes están sujetas a la misma directiva de limitación de velocidad, como el envío de mensajes, enumeraciones de canales e recuperaciones de lista.</span><span class="sxs-lookup"><span data-stu-id="556cf-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="556cf-110">Como los valores exactos de los límites de velocidad están sujetos a cambios, recomendamos que la aplicación implemente el comportamiento `HTTP 429 Too Many Requests`de interrupción adecuado cuando la API vuelva.</span><span class="sxs-lookup"><span data-stu-id="556cf-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="556cf-111">Límites de velocidad de manipulación</span><span class="sxs-lookup"><span data-stu-id="556cf-111">Handling rate limits</span></span>

<span data-ttu-id="556cf-112">Al emitir una operación del SDK de bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.</span><span class="sxs-lookup"><span data-stu-id="556cf-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="556cf-113">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="556cf-113">Best practices</span></span>

<span data-ttu-id="556cf-114">En general, debe tomar precauciones sencillas para evitar recibir `HTTP 429` respuestas.</span><span class="sxs-lookup"><span data-stu-id="556cf-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="556cf-115">Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal.</span><span class="sxs-lookup"><span data-stu-id="556cf-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="556cf-116">En su lugar, considere la posibilidad de procesar las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="556cf-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="556cf-117">El uso de un punto de interrupción exponencial con una vibración aleatoria es la forma recomendada para controlar 429s.</span><span class="sxs-lookup"><span data-stu-id="556cf-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="556cf-118">Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.</span><span class="sxs-lookup"><span data-stu-id="556cf-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="556cf-119">Ejemplo: detectar excepciones transitorias</span><span class="sxs-lookup"><span data-stu-id="556cf-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="556cf-120">A continuación se muestra un ejemplo que usa el punto de interrupción exponencial mediante el bloque de aplicaciones transitorio de control de errores.</span><span class="sxs-lookup"><span data-stu-id="556cf-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="556cf-121">Puede realizar el multiplicador y los reintentos mediante el [control de errores transitorio](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="556cf-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="556cf-122">Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea el tema sobre cómo [Agregar el bloque de aplicaciones de control de errores transitorio a la solución](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="556cf-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="556cf-123">*Consulte también* [control de errores transitorios](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="556cf-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="556cf-124">Ejemplo: multiplicador</span><span class="sxs-lookup"><span data-stu-id="556cf-124">Example: backoff</span></span>

<span data-ttu-id="556cf-125">Además de detectar los límites de velocidad, también puede realizar un multiplicador exponencial.</span><span class="sxs-lookup"><span data-stu-id="556cf-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="556cf-126">También puede realizar una `System.Action` ejecución de método con la Directiva de reintentos descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="556cf-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="556cf-127">La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de interrupción lineal.</span><span class="sxs-lookup"><span data-stu-id="556cf-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="556cf-128">Se recomienda almacenar el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="556cf-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="556cf-129">Para obtener más información, consulte esta práctica guía sobre diversos patrones de reintento: [patrón de reintentos](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="556cf-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="556cf-130">Por robot por límite de subprocesos</span><span class="sxs-lookup"><span data-stu-id="556cf-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="556cf-131">La división de mensajes en el nivel de servicio dará como resultado un número de solicitudes por segundo (RPS) superiores a lo esperado.</span><span class="sxs-lookup"><span data-stu-id="556cf-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="556cf-132">Si le preocupan los límites, debe implementar la estrategia de punto de interrupción descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="556cf-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="556cf-133">Los valores proporcionados a continuación solo son para la estimación.</span><span class="sxs-lookup"><span data-stu-id="556cf-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="556cf-134">Este límite controla el tráfico que un bot puede generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="556cf-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="556cf-135">Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="556cf-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="556cf-136">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="556cf-136">**Scenario**</span></span> | <span data-ttu-id="556cf-137">**Período de tiempo: (seg.)**</span><span class="sxs-lookup"><span data-stu-id="556cf-137">**Time-period (sec)**</span></span> | <span data-ttu-id="556cf-138">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="556cf-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
|| <span data-ttu-id="556cf-139">1</span><span class="sxs-lookup"><span data-stu-id="556cf-139">1</span></span> | <span data-ttu-id="556cf-140">0,7</span><span class="sxs-lookup"><span data-stu-id="556cf-140">7</span></span> |
| <span data-ttu-id="556cf-141">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-141">Send to Conversation</span></span> | <span data-ttu-id="556cf-142">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-142">2</span></span> | <span data-ttu-id="556cf-143">8,5</span><span class="sxs-lookup"><span data-stu-id="556cf-143">8</span></span> |
| <span data-ttu-id="556cf-144">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-144">Send to Conversation</span></span> | <span data-ttu-id="556cf-145">semestre</span><span class="sxs-lookup"><span data-stu-id="556cf-145">30</span></span> | <span data-ttu-id="556cf-146">60</span><span class="sxs-lookup"><span data-stu-id="556cf-146">60</span></span> |
| <span data-ttu-id="556cf-147">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-147">Send to Conversation</span></span> | <span data-ttu-id="556cf-148">3600</span><span class="sxs-lookup"><span data-stu-id="556cf-148">3600</span></span> | <span data-ttu-id="556cf-149">1800</span><span class="sxs-lookup"><span data-stu-id="556cf-149">1800</span></span> |
| <span data-ttu-id="556cf-150">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-150">Create Conversation</span></span> | <span data-ttu-id="556cf-151">1</span><span class="sxs-lookup"><span data-stu-id="556cf-151">1</span></span> | <span data-ttu-id="556cf-152">0,7</span><span class="sxs-lookup"><span data-stu-id="556cf-152">7</span></span> |
| <span data-ttu-id="556cf-153">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-153">Create Conversation</span></span> | <span data-ttu-id="556cf-154">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-154">2</span></span> | <span data-ttu-id="556cf-155">8,5</span><span class="sxs-lookup"><span data-stu-id="556cf-155">8</span></span> |
| <span data-ttu-id="556cf-156">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-156">Create Conversation</span></span> | <span data-ttu-id="556cf-157">semestre</span><span class="sxs-lookup"><span data-stu-id="556cf-157">30</span></span> | <span data-ttu-id="556cf-158">60</span><span class="sxs-lookup"><span data-stu-id="556cf-158">60</span></span> |
| <span data-ttu-id="556cf-159">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-159">Create Conversation</span></span> | <span data-ttu-id="556cf-160">3600</span><span class="sxs-lookup"><span data-stu-id="556cf-160">3600</span></span> | <span data-ttu-id="556cf-161">1800</span><span class="sxs-lookup"><span data-stu-id="556cf-161">1800</span></span> |
| <span data-ttu-id="556cf-162">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-162">Get Conversation Members</span></span>| <span data-ttu-id="556cf-163">1</span><span class="sxs-lookup"><span data-stu-id="556cf-163">1</span></span> | <span data-ttu-id="556cf-164">14 </span><span class="sxs-lookup"><span data-stu-id="556cf-164">14</span></span> |
| <span data-ttu-id="556cf-165">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-165">Get Conversation Members</span></span>| <span data-ttu-id="556cf-166">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-166">2</span></span> | <span data-ttu-id="556cf-167">16 </span><span class="sxs-lookup"><span data-stu-id="556cf-167">16</span></span> |
| <span data-ttu-id="556cf-168">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-168">Get Conversation Members</span></span>| <span data-ttu-id="556cf-169">semestre</span><span class="sxs-lookup"><span data-stu-id="556cf-169">30</span></span> | <span data-ttu-id="556cf-170">120</span><span class="sxs-lookup"><span data-stu-id="556cf-170">120</span></span> |
| <span data-ttu-id="556cf-171">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-171">Get Conversation Members</span></span>| <span data-ttu-id="556cf-172">3600</span><span class="sxs-lookup"><span data-stu-id="556cf-172">3600</span></span> | <span data-ttu-id="556cf-173">3600</span><span class="sxs-lookup"><span data-stu-id="556cf-173">3600</span></span> |
| <span data-ttu-id="556cf-174">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="556cf-174">Get Conversations</span></span> | <span data-ttu-id="556cf-175">1</span><span class="sxs-lookup"><span data-stu-id="556cf-175">1</span></span> | <span data-ttu-id="556cf-176">14 </span><span class="sxs-lookup"><span data-stu-id="556cf-176">14</span></span> |
| <span data-ttu-id="556cf-177">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="556cf-177">Get Conversations</span></span> | <span data-ttu-id="556cf-178">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-178">2</span></span> | <span data-ttu-id="556cf-179">16 </span><span class="sxs-lookup"><span data-stu-id="556cf-179">16</span></span> |
| <span data-ttu-id="556cf-180">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="556cf-180">Get Conversations</span></span> | <span data-ttu-id="556cf-181">semestre</span><span class="sxs-lookup"><span data-stu-id="556cf-181">30</span></span> | <span data-ttu-id="556cf-182">120</span><span class="sxs-lookup"><span data-stu-id="556cf-182">120</span></span> |
| <span data-ttu-id="556cf-183">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="556cf-183">Get Conversations</span></span> | <span data-ttu-id="556cf-184">3600</span><span class="sxs-lookup"><span data-stu-id="556cf-184">3600</span></span> | <span data-ttu-id="556cf-185">3600</span><span class="sxs-lookup"><span data-stu-id="556cf-185">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="556cf-186">Límite por subproceso para todos los bots</span><span class="sxs-lookup"><span data-stu-id="556cf-186">Per thread limit for all bots</span></span>

<span data-ttu-id="556cf-187">Este límite controla el tráfico que pueden generar todos los bots a través de una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="556cf-187">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="556cf-188">Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="556cf-188">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="556cf-189">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="556cf-189">**Scenario**</span></span> | <span data-ttu-id="556cf-190">**Período de tiempo: (seg.)**</span><span class="sxs-lookup"><span data-stu-id="556cf-190">**Time-period (sec)**</span></span> | <span data-ttu-id="556cf-191">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="556cf-191">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="556cf-192">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-192">Send to Conversation</span></span> | <span data-ttu-id="556cf-193">1</span><span class="sxs-lookup"><span data-stu-id="556cf-193">1</span></span> | <span data-ttu-id="556cf-194">14 </span><span class="sxs-lookup"><span data-stu-id="556cf-194">14</span></span> |
| <span data-ttu-id="556cf-195">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-195">Send to Conversation</span></span> | <span data-ttu-id="556cf-196">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-196">2</span></span> | <span data-ttu-id="556cf-197">16 </span><span class="sxs-lookup"><span data-stu-id="556cf-197">16</span></span> |
| <span data-ttu-id="556cf-198">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-198">Create Conversation</span></span> | <span data-ttu-id="556cf-199">1</span><span class="sxs-lookup"><span data-stu-id="556cf-199">1</span></span> | <span data-ttu-id="556cf-200">14 </span><span class="sxs-lookup"><span data-stu-id="556cf-200">14</span></span> |
| <span data-ttu-id="556cf-201">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-201">Create Conversation</span></span> | <span data-ttu-id="556cf-202">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-202">2</span></span> | <span data-ttu-id="556cf-203">16 </span><span class="sxs-lookup"><span data-stu-id="556cf-203">16</span></span> |
| <span data-ttu-id="556cf-204">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="556cf-204">CreateConversation</span></span>| <span data-ttu-id="556cf-205">1</span><span class="sxs-lookup"><span data-stu-id="556cf-205">1</span></span> | <span data-ttu-id="556cf-206">14 </span><span class="sxs-lookup"><span data-stu-id="556cf-206">14</span></span> |
| <span data-ttu-id="556cf-207">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="556cf-207">CreateConversation</span></span>| <span data-ttu-id="556cf-208">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-208">2</span></span> | <span data-ttu-id="556cf-209">16 </span><span class="sxs-lookup"><span data-stu-id="556cf-209">16</span></span> |
| <span data-ttu-id="556cf-210">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-210">Get Conversation Members</span></span>| <span data-ttu-id="556cf-211">1</span><span class="sxs-lookup"><span data-stu-id="556cf-211">1</span></span> | <span data-ttu-id="556cf-212">28</span><span class="sxs-lookup"><span data-stu-id="556cf-212">28</span></span> |
| <span data-ttu-id="556cf-213">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="556cf-213">Get Conversation Members</span></span>| <span data-ttu-id="556cf-214">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-214">2</span></span> | <span data-ttu-id="556cf-215">32</span><span class="sxs-lookup"><span data-stu-id="556cf-215">32</span></span> |
| <span data-ttu-id="556cf-216">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="556cf-216">Get Conversations</span></span> | <span data-ttu-id="556cf-217">1</span><span class="sxs-lookup"><span data-stu-id="556cf-217">1</span></span> | <span data-ttu-id="556cf-218">28</span><span class="sxs-lookup"><span data-stu-id="556cf-218">28</span></span> |
| <span data-ttu-id="556cf-219">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="556cf-219">Get Conversations</span></span> | <span data-ttu-id="556cf-220">segundo</span><span class="sxs-lookup"><span data-stu-id="556cf-220">2</span></span> | <span data-ttu-id="556cf-221">32</span><span class="sxs-lookup"><span data-stu-id="556cf-221">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="556cf-222">Bot por límite de centro de datos</span><span class="sxs-lookup"><span data-stu-id="556cf-222">Bot per data center limit</span></span>

<span data-ttu-id="556cf-223">Este límite controla el tráfico que un bot puede generar a través de todos los subprocesos de un centro de datos (en varios inquilinos).</span><span class="sxs-lookup"><span data-stu-id="556cf-223">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="556cf-224">**Período de tiempo: (seg.)**</span><span class="sxs-lookup"><span data-stu-id="556cf-224">**Time-period (sec)**</span></span> | <span data-ttu-id="556cf-225">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="556cf-225">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="556cf-226">1</span><span class="sxs-lookup"><span data-stu-id="556cf-226">1</span></span> | <span data-ttu-id="556cf-227">20</span><span class="sxs-lookup"><span data-stu-id="556cf-227">20</span></span> |
| <span data-ttu-id="556cf-228">1800</span><span class="sxs-lookup"><span data-stu-id="556cf-228">1800</span></span> | <span data-ttu-id="556cf-229">8000</span><span class="sxs-lookup"><span data-stu-id="556cf-229">8000</span></span> |
| <span data-ttu-id="556cf-230">3600</span><span class="sxs-lookup"><span data-stu-id="556cf-230">3600</span></span> | <span data-ttu-id="556cf-231">15000</span><span class="sxs-lookup"><span data-stu-id="556cf-231">15000</span></span> |
