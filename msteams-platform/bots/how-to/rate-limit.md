---
title: Limitación de velocidad
description: Limitación de velocidad y procedimientos recomendados en Microsoft Teams
keywords: limitación de velocidad de bots de equipo
ms.openlocfilehash: 2e401b59df075688cb6d459a881e6b813f2cf8e6
ms.sourcegitcommit: b3962a7b36f260aef1af9124d14d71ae08b01ac4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "47303713"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="ffb14-104">Optimizar el bot: límites de velocidad y procedimientos recomendados en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ffb14-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="ffb14-105">Como principio general, la aplicación debe limitar el número de mensajes que envía a un chat o a una conversación de canal individuales.</span><span class="sxs-lookup"><span data-stu-id="ffb14-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="ffb14-106">Esto garantiza una experiencia óptima que no siente "correo no deseado" para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="ffb14-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="ffb14-107">Para proteger Microsoft Teams y sus usuarios, la API de bot limita la velocidad de las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="ffb14-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="ffb14-108">Las aplicaciones que superen este límite recibirán un `HTTP 429 Too Many Requests` Estado de error.</span><span class="sxs-lookup"><span data-stu-id="ffb14-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="ffb14-109">Todas las solicitudes están sujetas a la misma directiva de limitación de velocidad, como el envío de mensajes, enumeraciones de canales e recuperaciones de lista.</span><span class="sxs-lookup"><span data-stu-id="ffb14-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="ffb14-110">Como los valores exactos de los límites de velocidad están sujetos a cambios, recomendamos que la aplicación implemente el comportamiento de interrupción adecuado cuando la API vuelva `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="ffb14-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="ffb14-111">Límites de velocidad de manipulación</span><span class="sxs-lookup"><span data-stu-id="ffb14-111">Handling rate limits</span></span>

<span data-ttu-id="ffb14-112">Al emitir una operación del SDK de bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.</span><span class="sxs-lookup"><span data-stu-id="ffb14-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="ffb14-113">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="ffb14-113">Best practices</span></span>

<span data-ttu-id="ffb14-114">En general, debe tomar precauciones sencillas para evitar recibir `HTTP 429` respuestas.</span><span class="sxs-lookup"><span data-stu-id="ffb14-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="ffb14-115">Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal.</span><span class="sxs-lookup"><span data-stu-id="ffb14-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="ffb14-116">En su lugar, considere la posibilidad de procesar las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="ffb14-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="ffb14-117">El uso de un punto de interrupción exponencial con una vibración aleatoria es la forma recomendada para controlar 429s.</span><span class="sxs-lookup"><span data-stu-id="ffb14-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="ffb14-118">Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.</span><span class="sxs-lookup"><span data-stu-id="ffb14-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="ffb14-119">Ejemplo: detectar excepciones transitorias</span><span class="sxs-lookup"><span data-stu-id="ffb14-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="ffb14-120">A continuación se muestra un ejemplo que usa el punto de interrupción exponencial mediante el bloque de aplicaciones transitorio de control de errores.</span><span class="sxs-lookup"><span data-stu-id="ffb14-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="ffb14-121">Puede realizar el multiplicador y los reintentos mediante el [control de errores transitorio](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="ffb14-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="ffb14-122">Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea el tema sobre cómo [Agregar el bloque de aplicaciones de control de errores transitorio a la solución](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="ffb14-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="ffb14-123">*Consulte también* [control de errores transitorios](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="ffb14-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="ffb14-124">Ejemplo: multiplicador</span><span class="sxs-lookup"><span data-stu-id="ffb14-124">Example: backoff</span></span>

<span data-ttu-id="ffb14-125">Además de detectar los límites de velocidad, también puede realizar un multiplicador exponencial.</span><span class="sxs-lookup"><span data-stu-id="ffb14-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="ffb14-126">También puede realizar una `System.Action` ejecución de método con la Directiva de reintentos descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ffb14-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="ffb14-127">La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de interrupción lineal.</span><span class="sxs-lookup"><span data-stu-id="ffb14-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="ffb14-128">Se recomienda almacenar el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ffb14-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="ffb14-129">Para obtener más información, consulte esta práctica guía sobre diversos patrones de reintento: [patrón de reintentos](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="ffb14-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="ffb14-130">Por robot por límite de subprocesos</span><span class="sxs-lookup"><span data-stu-id="ffb14-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="ffb14-131">La división de mensajes en el nivel de servicio dará como resultado un número de solicitudes por segundo (RPS) superiores a lo esperado.</span><span class="sxs-lookup"><span data-stu-id="ffb14-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="ffb14-132">Si le preocupan los límites, debe implementar la estrategia de punto de interrupción descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ffb14-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="ffb14-133">Los valores proporcionados a continuación solo son para la estimación.</span><span class="sxs-lookup"><span data-stu-id="ffb14-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="ffb14-134">Este límite controla el tráfico que un bot puede generar en una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="ffb14-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="ffb14-135">Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="ffb14-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="ffb14-136">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="ffb14-136">**Scenario**</span></span> | <span data-ttu-id="ffb14-137">**Período de tiempo: (seg.)**</span><span class="sxs-lookup"><span data-stu-id="ffb14-137">**Time-period (sec)**</span></span> | <span data-ttu-id="ffb14-138">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="ffb14-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffb14-139">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-139">Send to Conversation</span></span> | <span data-ttu-id="ffb14-140">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-140">1</span></span> | <span data-ttu-id="ffb14-141">7 </span><span class="sxs-lookup"><span data-stu-id="ffb14-141">7</span></span> |
| <span data-ttu-id="ffb14-142">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-142">Send to Conversation</span></span> | <span data-ttu-id="ffb14-143">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-143">2</span></span> | <span data-ttu-id="ffb14-144">8 </span><span class="sxs-lookup"><span data-stu-id="ffb14-144">8</span></span> |
| <span data-ttu-id="ffb14-145">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-145">Send to Conversation</span></span> | <span data-ttu-id="ffb14-146">semestre</span><span class="sxs-lookup"><span data-stu-id="ffb14-146">30</span></span> | <span data-ttu-id="ffb14-147">60</span><span class="sxs-lookup"><span data-stu-id="ffb14-147">60</span></span> |
| <span data-ttu-id="ffb14-148">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-148">Send to Conversation</span></span> | <span data-ttu-id="ffb14-149">3600</span><span class="sxs-lookup"><span data-stu-id="ffb14-149">3600</span></span> | <span data-ttu-id="ffb14-150">1800</span><span class="sxs-lookup"><span data-stu-id="ffb14-150">1800</span></span> |
| <span data-ttu-id="ffb14-151">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-151">Create Conversation</span></span> | <span data-ttu-id="ffb14-152">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-152">1</span></span> | <span data-ttu-id="ffb14-153">7 </span><span class="sxs-lookup"><span data-stu-id="ffb14-153">7</span></span> |
| <span data-ttu-id="ffb14-154">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-154">Create Conversation</span></span> | <span data-ttu-id="ffb14-155">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-155">2</span></span> | <span data-ttu-id="ffb14-156">8 </span><span class="sxs-lookup"><span data-stu-id="ffb14-156">8</span></span> |
| <span data-ttu-id="ffb14-157">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-157">Create Conversation</span></span> | <span data-ttu-id="ffb14-158">semestre</span><span class="sxs-lookup"><span data-stu-id="ffb14-158">30</span></span> | <span data-ttu-id="ffb14-159">60</span><span class="sxs-lookup"><span data-stu-id="ffb14-159">60</span></span> |
| <span data-ttu-id="ffb14-160">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-160">Create Conversation</span></span> | <span data-ttu-id="ffb14-161">3600</span><span class="sxs-lookup"><span data-stu-id="ffb14-161">3600</span></span> | <span data-ttu-id="ffb14-162">1800</span><span class="sxs-lookup"><span data-stu-id="ffb14-162">1800</span></span> |
| <span data-ttu-id="ffb14-163">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-163">Get Conversation Members</span></span>| <span data-ttu-id="ffb14-164">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-164">1</span></span> | <span data-ttu-id="ffb14-165">14 </span><span class="sxs-lookup"><span data-stu-id="ffb14-165">14</span></span> |
| <span data-ttu-id="ffb14-166">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-166">Get Conversation Members</span></span>| <span data-ttu-id="ffb14-167">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-167">2</span></span> | <span data-ttu-id="ffb14-168">16 </span><span class="sxs-lookup"><span data-stu-id="ffb14-168">16</span></span> |
| <span data-ttu-id="ffb14-169">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-169">Get Conversation Members</span></span>| <span data-ttu-id="ffb14-170">semestre</span><span class="sxs-lookup"><span data-stu-id="ffb14-170">30</span></span> | <span data-ttu-id="ffb14-171">120</span><span class="sxs-lookup"><span data-stu-id="ffb14-171">120</span></span> |
| <span data-ttu-id="ffb14-172">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-172">Get Conversation Members</span></span>| <span data-ttu-id="ffb14-173">3600</span><span class="sxs-lookup"><span data-stu-id="ffb14-173">3600</span></span> | <span data-ttu-id="ffb14-174">3600</span><span class="sxs-lookup"><span data-stu-id="ffb14-174">3600</span></span> |
| <span data-ttu-id="ffb14-175">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="ffb14-175">Get Conversations</span></span> | <span data-ttu-id="ffb14-176">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-176">1</span></span> | <span data-ttu-id="ffb14-177">14 </span><span class="sxs-lookup"><span data-stu-id="ffb14-177">14</span></span> |
| <span data-ttu-id="ffb14-178">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="ffb14-178">Get Conversations</span></span> | <span data-ttu-id="ffb14-179">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-179">2</span></span> | <span data-ttu-id="ffb14-180">16 </span><span class="sxs-lookup"><span data-stu-id="ffb14-180">16</span></span> |
| <span data-ttu-id="ffb14-181">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="ffb14-181">Get Conversations</span></span> | <span data-ttu-id="ffb14-182">semestre</span><span class="sxs-lookup"><span data-stu-id="ffb14-182">30</span></span> | <span data-ttu-id="ffb14-183">120</span><span class="sxs-lookup"><span data-stu-id="ffb14-183">120</span></span> |
| <span data-ttu-id="ffb14-184">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="ffb14-184">Get Conversations</span></span> | <span data-ttu-id="ffb14-185">3600</span><span class="sxs-lookup"><span data-stu-id="ffb14-185">3600</span></span> | <span data-ttu-id="ffb14-186">3600</span><span class="sxs-lookup"><span data-stu-id="ffb14-186">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="ffb14-187">Límite por subproceso para todos los bots</span><span class="sxs-lookup"><span data-stu-id="ffb14-187">Per thread limit for all bots</span></span>

<span data-ttu-id="ffb14-188">Este límite controla el tráfico que pueden generar todos los bots a través de una sola conversación.</span><span class="sxs-lookup"><span data-stu-id="ffb14-188">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="ffb14-189">Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.</span><span class="sxs-lookup"><span data-stu-id="ffb14-189">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="ffb14-190">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="ffb14-190">**Scenario**</span></span> | <span data-ttu-id="ffb14-191">**Período de tiempo: (seg.)**</span><span class="sxs-lookup"><span data-stu-id="ffb14-191">**Time-period (sec)**</span></span> | <span data-ttu-id="ffb14-192">**Operaciones máximas permitidas**</span><span class="sxs-lookup"><span data-stu-id="ffb14-192">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffb14-193">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-193">Send to Conversation</span></span> | <span data-ttu-id="ffb14-194">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-194">1</span></span> | <span data-ttu-id="ffb14-195">14 </span><span class="sxs-lookup"><span data-stu-id="ffb14-195">14</span></span> |
| <span data-ttu-id="ffb14-196">Enviar a conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-196">Send to Conversation</span></span> | <span data-ttu-id="ffb14-197">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-197">2</span></span> | <span data-ttu-id="ffb14-198">16 </span><span class="sxs-lookup"><span data-stu-id="ffb14-198">16</span></span> |
| <span data-ttu-id="ffb14-199">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-199">Create Conversation</span></span> | <span data-ttu-id="ffb14-200">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-200">1</span></span> | <span data-ttu-id="ffb14-201">14 </span><span class="sxs-lookup"><span data-stu-id="ffb14-201">14</span></span> |
| <span data-ttu-id="ffb14-202">Crear conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-202">Create Conversation</span></span> | <span data-ttu-id="ffb14-203">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-203">2</span></span> | <span data-ttu-id="ffb14-204">16 </span><span class="sxs-lookup"><span data-stu-id="ffb14-204">16</span></span> |
| <span data-ttu-id="ffb14-205">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="ffb14-205">CreateConversation</span></span>| <span data-ttu-id="ffb14-206">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-206">1</span></span> | <span data-ttu-id="ffb14-207">14 </span><span class="sxs-lookup"><span data-stu-id="ffb14-207">14</span></span> |
| <span data-ttu-id="ffb14-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="ffb14-208">CreateConversation</span></span>| <span data-ttu-id="ffb14-209">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-209">2</span></span> | <span data-ttu-id="ffb14-210">16 </span><span class="sxs-lookup"><span data-stu-id="ffb14-210">16</span></span> |
| <span data-ttu-id="ffb14-211">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-211">Get Conversation Members</span></span>| <span data-ttu-id="ffb14-212">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-212">1</span></span> | <span data-ttu-id="ffb14-213">28</span><span class="sxs-lookup"><span data-stu-id="ffb14-213">28</span></span> |
| <span data-ttu-id="ffb14-214">Obtener miembros de la conversación</span><span class="sxs-lookup"><span data-stu-id="ffb14-214">Get Conversation Members</span></span>| <span data-ttu-id="ffb14-215">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-215">2</span></span> | <span data-ttu-id="ffb14-216">32</span><span class="sxs-lookup"><span data-stu-id="ffb14-216">32</span></span> |
| <span data-ttu-id="ffb14-217">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="ffb14-217">Get Conversations</span></span> | <span data-ttu-id="ffb14-218">1 </span><span class="sxs-lookup"><span data-stu-id="ffb14-218">1</span></span> | <span data-ttu-id="ffb14-219">28</span><span class="sxs-lookup"><span data-stu-id="ffb14-219">28</span></span> |
| <span data-ttu-id="ffb14-220">Obtener conversaciones</span><span class="sxs-lookup"><span data-stu-id="ffb14-220">Get Conversations</span></span> | <span data-ttu-id="ffb14-221">2 </span><span class="sxs-lookup"><span data-stu-id="ffb14-221">2</span></span> | <span data-ttu-id="ffb14-222">32</span><span class="sxs-lookup"><span data-stu-id="ffb14-222">32</span></span> |
