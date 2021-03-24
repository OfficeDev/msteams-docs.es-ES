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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>Optimizar el bot: limitación de velocidad y procedimientos recomendados en Microsoft Teams

Como principio general, la aplicación debe limitar el número de mensajes que publica a una conversación de canal o chat individual. Esto garantiza una experiencia óptima que no se sienta "correo no deseado" para los usuarios finales.

Para proteger Microsoft Teams y sus usuarios, las API de bot limitan la velocidad de las solicitudes entrantes. Las aplicaciones que superen este límite reciben un `HTTP 429 Too Many Requests` estado de error. Todas las solicitudes están sujetas a la misma directiva de limitación de tasas, incluido el envío de mensajes, enumeraciones de canales y recuperaciones de listas.

Dado que los valores exactos de los límites de tasa están sujetos a cambios, se recomienda que la aplicación implemente el comportamiento de devolución adecuado cuando la API devuelva `HTTP 429 Too Many Requests` .

## <a name="handling-rate-limits"></a>Control de límites de velocidad

Al emitir una operación del SDK de Bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.

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

## <a name="best-practices"></a>Procedimientos recomendados

En general, debe tomar precauciones simples para evitar recibir `HTTP 429` respuestas. Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal. En su lugar, considere la posibilidad de procesar por lotes las solicitudes de API.

El uso de un retroceso exponencial con un vibración aleatoria es la forma recomendada de controlar 429s. Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.

## <a name="example-detecting-transient-exceptions"></a>Ejemplo: detección de excepciones transitorias

Este es un ejemplo con retroceso exponencial a través del bloque de aplicaciones de control de errores transitorios.

Puede realizar backoff y reintentos mediante [el control de errores transitorios](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29). Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)). *Vea también Control* [de errores transitorios](/azure/architecture/best-practices/transient-faults).

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

## <a name="example-backoff"></a>Ejemplo: backoff

Además de detectar límites de velocidad, también puede realizar un retroceso exponencial.

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

También puede realizar una ejecución `System.Action` de método con la directiva de reintentos descrita anteriormente. La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de desuso lineal.

Se recomienda almacenar el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.

Para obtener más información, consulte esta guía práctica sobre varios patrones de reintentos: [Patrón de reintentos](/azure/architecture/patterns/retry).

## <a name="per-bot-per-thread-limit"></a>Por bot por límite de subprocesos

>[!NOTE]
>La división de mensajes en el nivel de servicio dará como resultado solicitudes superiores a las esperadas por segundo (RPS). Si le preocupa acercarse a los límites, debe implementar la estrategia de backoff descrita anteriormente. Los valores proporcionados a continuación son solo para estimación.

Este límite controla el tráfico que un bot puede generar en una sola conversación. Una conversación aquí es 1:1 entre bot y usuario, un chat en grupo o un canal en un equipo.

| **Escenario** | **Período de tiempo: (seg.)** | **Operaciones máximas permitidas** |
| --- | --- | --- |
| Enviar a conversación | 1 | 7  |
| Enviar a conversación | 2 | 8  |
| Enviar a conversación | 30 | 60 |
| Enviar a conversación | 3600 | 1800 |
| Crear conversación | 1 | 7  |
| Crear conversación | 2 | 8  |
| Crear conversación | 30 | 60 |
| Crear conversación | 3600 | 1800 |
| Obtener miembros de conversación| 1 | 14  |
| Obtener miembros de conversación| 2 | 16  |
| Obtener miembros de conversación| 30 | 120 |
| Obtener miembros de conversación| 3600 | 3600 |
| Obtener conversaciones | 1 | 14  |
| Obtener conversaciones | 2 | 16  |
| Obtener conversaciones | 30 | 120 |
| Obtener conversaciones | 3600 | 3600 |

>[!NOTE]
> Las versiones anteriores `TeamsInfo.getMembers` de y las API están en `TeamsInfo.GetMembersAsync` desuso. Se limitarán a 5 solicitudes por minuto y devolverán un máximo de 10.000 miembros por equipo. Para actualizar el SDK de Bot Framework y el código para usar los extremos de API paginados más recientes, consulte [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).

## <a name="per-thread-limit-for-all-bots"></a>Límite por subproceso para todos los bots

Este límite controla el tráfico que todos los bots pueden generar en una sola conversación. Una conversación aquí es 1:1 entre bot y usuario, un chat en grupo o un canal en un equipo.

| **Escenario** | **Período de tiempo: (seg.)** | **Operaciones máximas permitidas** |
| --- | --- | --- |
| Enviar a conversación | 1 | 14  |
| Enviar a conversación | 2 | 16  |
| Crear conversación | 1 | 14  |
| Crear conversación | 2 | 16  |
| CreateConversation| 1 | 14  |
| CreateConversation| 2 | 16  |
| Obtener miembros de conversación| 1 | 28 |
| Obtener miembros de conversación| 2 | 32 |
| Obtener conversaciones | 1 | 28 |
| Obtener conversaciones | 2 | 32 |
