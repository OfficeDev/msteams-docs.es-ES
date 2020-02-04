---
title: Limitación de velocidad
description: Limitación de velocidad y procedimientos recomendados en Microsoft Teams
keywords: limitación de velocidad de bots de equipo
ms.openlocfilehash: 4e9efab539ec7817d259fd6c149c438ba02e3ce5
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675836"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="58239-104">Optimizar el bot: límites de velocidad y procedimientos recomendados en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="58239-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="58239-105">Como principio general, la aplicación debe limitar el número de mensajes que envía a un chat o a una conversación de canal individuales.</span><span class="sxs-lookup"><span data-stu-id="58239-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="58239-106">Esto garantiza una experiencia óptima que no siente "correo no deseado" para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="58239-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="58239-107">Para proteger Microsoft Teams y sus usuarios, la API de bot limita la velocidad de las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="58239-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="58239-108">Las aplicaciones que superen este límite recibirán un `HTTP 429 Too Many Requests` estado de error.</span><span class="sxs-lookup"><span data-stu-id="58239-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="58239-109">Todas las solicitudes están sujetas a la misma directiva de limitación de velocidad, como el envío de mensajes, enumeraciones de canales e recuperaciones de lista.</span><span class="sxs-lookup"><span data-stu-id="58239-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="58239-110">Como los valores exactos de los límites de velocidad están sujetos a cambios, recomendamos que la aplicación implemente el comportamiento `HTTP 429 Too Many Requests`de interrupción adecuado cuando la API vuelva.</span><span class="sxs-lookup"><span data-stu-id="58239-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="58239-111">Límites de velocidad de manipulación</span><span class="sxs-lookup"><span data-stu-id="58239-111">Handling rate limits</span></span>

<span data-ttu-id="58239-112">Al emitir una operación del SDK de bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.</span><span class="sxs-lookup"><span data-stu-id="58239-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="58239-113">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="58239-113">Best practices</span></span>

<span data-ttu-id="58239-114">En general, debe tomar precauciones sencillas para evitar recibir `HTTP 429` respuestas.</span><span class="sxs-lookup"><span data-stu-id="58239-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="58239-115">Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal.</span><span class="sxs-lookup"><span data-stu-id="58239-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="58239-116">En su lugar, considere la posibilidad de procesar las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="58239-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="58239-117">El uso de un punto de interrupción exponencial con una vibración aleatoria es la forma recomendada para controlar 429s.</span><span class="sxs-lookup"><span data-stu-id="58239-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="58239-118">Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.</span><span class="sxs-lookup"><span data-stu-id="58239-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="58239-119">Ejemplo: detectar excepciones transitorias</span><span class="sxs-lookup"><span data-stu-id="58239-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="58239-120">A continuación se muestra un ejemplo que usa el punto de interrupción exponencial mediante el bloque de aplicaciones transitorio de control de errores.</span><span class="sxs-lookup"><span data-stu-id="58239-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="58239-121">Puede usar el multiplicador y los reintentos mediante [bibliotecas de control de errores transitorias](/previous-versions/msp-n-p/hh680901(v=pandp.50)).</span><span class="sxs-lookup"><span data-stu-id="58239-121">You can perform backoff and retries using [Transient Fault Handling libraries](/previous-versions/msp-n-p/hh680901(v=pandp.50)).</span></span> <span data-ttu-id="58239-122">Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea [Agregar el bloque de aplicación de control de errores transitorio a la solución](/previous-versions/msp-n-p/hh680891(v=pandp.50)) .</span><span class="sxs-lookup"><span data-stu-id="58239-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/hh680891(v=pandp.50))</span></span>

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
{
    // List of error codes to retry on
    List<int> transientErrorStatusCodes = new List<int>() { 429 };

    public bool IsTransient(Exception ex)
    {
        var httpOperationException = ex as HttpOperationException;
        if (httpOperationException != null)
        {
            return httpOperationException.Response != null &&
                    transientErrorStatusCodes.Contains((int) httpOperationException.Response.StatusCode);
        }

        return false;
    }
}
```

## <a name="example-backoff"></a><span data-ttu-id="58239-123">Ejemplo: multiplicador</span><span class="sxs-lookup"><span data-stu-id="58239-123">Example: backoff</span></span>

<span data-ttu-id="58239-124">Además de detectar los límites de velocidad, también puede realizar un multiplicador exponencial.</span><span class="sxs-lookup"><span data-stu-id="58239-124">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

```csharp
/**
* The first parameter specifies the number of retries before failing the operation.
* The second parameter specifies the minimum and maximum backoff time respectively.
* The last parameter is used to add a randomized  +/- 20% delta to avoid numerous clients retrying simultaneously.
*/
var exponentialBackoffRetryStrategy = new ExponentialBackoff(3, TimeSpan.FromSeconds(2),
                        TimeSpan.FromSeconds(20), TimeSpan.FromSeconds(1));


// Define the Retry Policy
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), fixedIntervalRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync((Activity)reply)).ConfigureAwait(false);
```

<span data-ttu-id="58239-125">También puede realizar una `System.Action` ejecución de método con la Directiva de reintentos descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="58239-125">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="58239-126">La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de interrupción lineal.</span><span class="sxs-lookup"><span data-stu-id="58239-126">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="58239-127">Se recomienda almacenar el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="58239-127">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="58239-128">Para obtener más información, consulte esta práctica guía sobre diversos patrones de reintento: [patrón de reintentos](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="58239-128">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="58239-129">Por robot por límite de subprocesos</span><span class="sxs-lookup"><span data-stu-id="58239-129">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="58239-130">La división de mensajes en el nivel de servicio dará como resultado un número de solicitudes por segundo (RPS) superiores a lo esperado.</span><span class="sxs-lookup"><span data-stu-id="58239-130">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="58239-131">Si le preocupan los límites, debe implementar la estrategia de punto de interrupción descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="58239-131">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="58239-132">Los valores proporcionados a continuación solo son para la estimación.</span><span class="sxs-lookup"><span data-stu-id="58239-132">The values provided below are for estimation only.</span></span>

<span data-ttu-id="58239-133">Este límite controla el tráfico que un bot puede generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="58239-133">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="58239-134">Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="58239-134">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="58239-135">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="58239-135">**Scenario**</span></span> | <span data-ttu-id="58239-136">**Tiempo: período (seg.)**</span><span class="sxs-lookup"><span data-stu-id="58239-136">**Time-period (sec)**</span></span> | <span data-ttu-id="58239-137">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="58239-137">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58239-138">NewMessage</span><span class="sxs-lookup"><span data-stu-id="58239-138">NewMessage</span></span> | <span data-ttu-id="58239-139">1 </span><span class="sxs-lookup"><span data-stu-id="58239-139">1</span></span> | <span data-ttu-id="58239-140">7 </span><span class="sxs-lookup"><span data-stu-id="58239-140">7</span></span> |
| <span data-ttu-id="58239-141">NewMessage</span><span class="sxs-lookup"><span data-stu-id="58239-141">NewMessage</span></span> | <span data-ttu-id="58239-142">2 </span><span class="sxs-lookup"><span data-stu-id="58239-142">2</span></span> | <span data-ttu-id="58239-143">8 </span><span class="sxs-lookup"><span data-stu-id="58239-143">8</span></span> |
| <span data-ttu-id="58239-144">NewMessage</span><span class="sxs-lookup"><span data-stu-id="58239-144">NewMessage</span></span> | <span data-ttu-id="58239-145">semestre</span><span class="sxs-lookup"><span data-stu-id="58239-145">30</span></span> | <span data-ttu-id="58239-146">60</span><span class="sxs-lookup"><span data-stu-id="58239-146">60</span></span> |
| <span data-ttu-id="58239-147">NewMessage</span><span class="sxs-lookup"><span data-stu-id="58239-147">NewMessage</span></span> | <span data-ttu-id="58239-148">3600</span><span class="sxs-lookup"><span data-stu-id="58239-148">3600</span></span> | <span data-ttu-id="58239-149">1800</span><span class="sxs-lookup"><span data-stu-id="58239-149">1800</span></span> |
| <span data-ttu-id="58239-150">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="58239-150">UpdateMessage</span></span> | <span data-ttu-id="58239-151">1 </span><span class="sxs-lookup"><span data-stu-id="58239-151">1</span></span> | <span data-ttu-id="58239-152">7 </span><span class="sxs-lookup"><span data-stu-id="58239-152">7</span></span> |
| <span data-ttu-id="58239-153">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="58239-153">UpdateMessage</span></span> | <span data-ttu-id="58239-154">2 </span><span class="sxs-lookup"><span data-stu-id="58239-154">2</span></span> | <span data-ttu-id="58239-155">8 </span><span class="sxs-lookup"><span data-stu-id="58239-155">8</span></span> |
| <span data-ttu-id="58239-156">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="58239-156">UpdateMessage</span></span> | <span data-ttu-id="58239-157">semestre</span><span class="sxs-lookup"><span data-stu-id="58239-157">30</span></span> | <span data-ttu-id="58239-158">60</span><span class="sxs-lookup"><span data-stu-id="58239-158">60</span></span> |
| <span data-ttu-id="58239-159">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="58239-159">UpdateMessage</span></span> | <span data-ttu-id="58239-160">3600</span><span class="sxs-lookup"><span data-stu-id="58239-160">3600</span></span> | <span data-ttu-id="58239-161">1800</span><span class="sxs-lookup"><span data-stu-id="58239-161">1800</span></span> |
| <span data-ttu-id="58239-162">NewThread</span><span class="sxs-lookup"><span data-stu-id="58239-162">NewThread</span></span> | <span data-ttu-id="58239-163">1 </span><span class="sxs-lookup"><span data-stu-id="58239-163">1</span></span> | <span data-ttu-id="58239-164">7 </span><span class="sxs-lookup"><span data-stu-id="58239-164">7</span></span> |
| <span data-ttu-id="58239-165">NewThread</span><span class="sxs-lookup"><span data-stu-id="58239-165">NewThread</span></span> | <span data-ttu-id="58239-166">2 </span><span class="sxs-lookup"><span data-stu-id="58239-166">2</span></span> | <span data-ttu-id="58239-167">8 </span><span class="sxs-lookup"><span data-stu-id="58239-167">8</span></span> |
| <span data-ttu-id="58239-168">NewThread</span><span class="sxs-lookup"><span data-stu-id="58239-168">NewThread</span></span> | <span data-ttu-id="58239-169">semestre</span><span class="sxs-lookup"><span data-stu-id="58239-169">30</span></span> | <span data-ttu-id="58239-170">60</span><span class="sxs-lookup"><span data-stu-id="58239-170">60</span></span> |
| <span data-ttu-id="58239-171">NewThread</span><span class="sxs-lookup"><span data-stu-id="58239-171">NewThread</span></span> | <span data-ttu-id="58239-172">3600</span><span class="sxs-lookup"><span data-stu-id="58239-172">3600</span></span> | <span data-ttu-id="58239-173">1800</span><span class="sxs-lookup"><span data-stu-id="58239-173">1800</span></span> |
| <span data-ttu-id="58239-174">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="58239-174">GetThreadMembers</span></span> | <span data-ttu-id="58239-175">1 </span><span class="sxs-lookup"><span data-stu-id="58239-175">1</span></span> | <span data-ttu-id="58239-176">14 </span><span class="sxs-lookup"><span data-stu-id="58239-176">14</span></span> |
| <span data-ttu-id="58239-177">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="58239-177">GetThreadMembers</span></span> | <span data-ttu-id="58239-178">2 </span><span class="sxs-lookup"><span data-stu-id="58239-178">2</span></span> | <span data-ttu-id="58239-179">16 </span><span class="sxs-lookup"><span data-stu-id="58239-179">16</span></span> |
| <span data-ttu-id="58239-180">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="58239-180">GetThreadMembers</span></span> | <span data-ttu-id="58239-181">semestre</span><span class="sxs-lookup"><span data-stu-id="58239-181">30</span></span> | <span data-ttu-id="58239-182">120</span><span class="sxs-lookup"><span data-stu-id="58239-182">120</span></span> |
| <span data-ttu-id="58239-183">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="58239-183">GetThreadMembers</span></span> | <span data-ttu-id="58239-184">3600</span><span class="sxs-lookup"><span data-stu-id="58239-184">3600</span></span> | <span data-ttu-id="58239-185">3600</span><span class="sxs-lookup"><span data-stu-id="58239-185">3600</span></span> |
| <span data-ttu-id="58239-186">GetThread</span><span class="sxs-lookup"><span data-stu-id="58239-186">GetThread</span></span> | <span data-ttu-id="58239-187">1 </span><span class="sxs-lookup"><span data-stu-id="58239-187">1</span></span> | <span data-ttu-id="58239-188">14 </span><span class="sxs-lookup"><span data-stu-id="58239-188">14</span></span> |
| <span data-ttu-id="58239-189">GetThread</span><span class="sxs-lookup"><span data-stu-id="58239-189">GetThread</span></span> | <span data-ttu-id="58239-190">2 </span><span class="sxs-lookup"><span data-stu-id="58239-190">2</span></span> | <span data-ttu-id="58239-191">16 </span><span class="sxs-lookup"><span data-stu-id="58239-191">16</span></span> |
| <span data-ttu-id="58239-192">GetThread</span><span class="sxs-lookup"><span data-stu-id="58239-192">GetThread</span></span> | <span data-ttu-id="58239-193">semestre</span><span class="sxs-lookup"><span data-stu-id="58239-193">30</span></span> | <span data-ttu-id="58239-194">120</span><span class="sxs-lookup"><span data-stu-id="58239-194">120</span></span> |
| <span data-ttu-id="58239-195">GetThread</span><span class="sxs-lookup"><span data-stu-id="58239-195">GetThread</span></span> | <span data-ttu-id="58239-196">3600</span><span class="sxs-lookup"><span data-stu-id="58239-196">3600</span></span> | <span data-ttu-id="58239-197">3600</span><span class="sxs-lookup"><span data-stu-id="58239-197">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="58239-198">Límite por subproceso para todos los bots</span><span class="sxs-lookup"><span data-stu-id="58239-198">Per thread limit for all bots</span></span>

<span data-ttu-id="58239-199">Este límite controla el tráfico que pueden generar todos los bots a través de una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="58239-199">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="58239-200">Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="58239-200">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="58239-201">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="58239-201">**Scenario**</span></span> | <span data-ttu-id="58239-202">**Tiempo: período (seg.)**</span><span class="sxs-lookup"><span data-stu-id="58239-202">**Time-period (sec)**</span></span> | <span data-ttu-id="58239-203">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="58239-203">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58239-204">NewMessage</span><span class="sxs-lookup"><span data-stu-id="58239-204">NewMessage</span></span> | <span data-ttu-id="58239-205">1 </span><span class="sxs-lookup"><span data-stu-id="58239-205">1</span></span> | <span data-ttu-id="58239-206">14 </span><span class="sxs-lookup"><span data-stu-id="58239-206">14</span></span> |
| <span data-ttu-id="58239-207">NewMessage</span><span class="sxs-lookup"><span data-stu-id="58239-207">NewMessage</span></span> | <span data-ttu-id="58239-208">2 </span><span class="sxs-lookup"><span data-stu-id="58239-208">2</span></span> | <span data-ttu-id="58239-209">16 </span><span class="sxs-lookup"><span data-stu-id="58239-209">16</span></span> |
| <span data-ttu-id="58239-210">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="58239-210">UpdateMessage</span></span> | <span data-ttu-id="58239-211">1 </span><span class="sxs-lookup"><span data-stu-id="58239-211">1</span></span> | <span data-ttu-id="58239-212">14 </span><span class="sxs-lookup"><span data-stu-id="58239-212">14</span></span> |
| <span data-ttu-id="58239-213">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="58239-213">UpdateMessage</span></span> | <span data-ttu-id="58239-214">2 </span><span class="sxs-lookup"><span data-stu-id="58239-214">2</span></span> | <span data-ttu-id="58239-215">16 </span><span class="sxs-lookup"><span data-stu-id="58239-215">16</span></span> |
| <span data-ttu-id="58239-216">NewThread</span><span class="sxs-lookup"><span data-stu-id="58239-216">NewThread</span></span> | <span data-ttu-id="58239-217">1 </span><span class="sxs-lookup"><span data-stu-id="58239-217">1</span></span> | <span data-ttu-id="58239-218">14 </span><span class="sxs-lookup"><span data-stu-id="58239-218">14</span></span> |
| <span data-ttu-id="58239-219">NewThread</span><span class="sxs-lookup"><span data-stu-id="58239-219">NewThread</span></span> | <span data-ttu-id="58239-220">2 </span><span class="sxs-lookup"><span data-stu-id="58239-220">2</span></span> | <span data-ttu-id="58239-221">16 </span><span class="sxs-lookup"><span data-stu-id="58239-221">16</span></span> |
| <span data-ttu-id="58239-222">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="58239-222">GetThreadMembers</span></span> | <span data-ttu-id="58239-223">1 </span><span class="sxs-lookup"><span data-stu-id="58239-223">1</span></span> | <span data-ttu-id="58239-224">28</span><span class="sxs-lookup"><span data-stu-id="58239-224">28</span></span> |
| <span data-ttu-id="58239-225">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="58239-225">GetThreadMembers</span></span> | <span data-ttu-id="58239-226">2 </span><span class="sxs-lookup"><span data-stu-id="58239-226">2</span></span> | <span data-ttu-id="58239-227">32</span><span class="sxs-lookup"><span data-stu-id="58239-227">32</span></span> |
| <span data-ttu-id="58239-228">GetThread</span><span class="sxs-lookup"><span data-stu-id="58239-228">GetThread</span></span> | <span data-ttu-id="58239-229">1 </span><span class="sxs-lookup"><span data-stu-id="58239-229">1</span></span> | <span data-ttu-id="58239-230">28</span><span class="sxs-lookup"><span data-stu-id="58239-230">28</span></span> |
| <span data-ttu-id="58239-231">GetThread</span><span class="sxs-lookup"><span data-stu-id="58239-231">GetThread</span></span> | <span data-ttu-id="58239-232">2 </span><span class="sxs-lookup"><span data-stu-id="58239-232">2</span></span> | <span data-ttu-id="58239-233">32</span><span class="sxs-lookup"><span data-stu-id="58239-233">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="58239-234">Bot por límite de centro de datos</span><span class="sxs-lookup"><span data-stu-id="58239-234">Bot per data center limit</span></span>

<span data-ttu-id="58239-235">Este límite controla el tráfico que un bot puede generar a través de todos los subprocesos de un centro de datos (en varios inquilinos).</span><span class="sxs-lookup"><span data-stu-id="58239-235">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="58239-236">**Tiempo: período (seg.)**</span><span class="sxs-lookup"><span data-stu-id="58239-236">**Time-period (sec)**</span></span> | <span data-ttu-id="58239-237">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="58239-237">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="58239-238">1 </span><span class="sxs-lookup"><span data-stu-id="58239-238">1</span></span> | <span data-ttu-id="58239-239">20</span><span class="sxs-lookup"><span data-stu-id="58239-239">20</span></span> |
| <span data-ttu-id="58239-240">1800</span><span class="sxs-lookup"><span data-stu-id="58239-240">1800</span></span> | <span data-ttu-id="58239-241">8000</span><span class="sxs-lookup"><span data-stu-id="58239-241">8000</span></span> |
| <span data-ttu-id="58239-242">3600</span><span class="sxs-lookup"><span data-stu-id="58239-242">3600</span></span> | <span data-ttu-id="58239-243">15000</span><span class="sxs-lookup"><span data-stu-id="58239-243">15000</span></span> |
