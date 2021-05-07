---
title: Optimizar un bot con la limitación de volumen en Teams
description: Limitación de tasas y procedimientos recomendados en Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: limitación de velocidad de bots de teams
ms.openlocfilehash: 3b8f80efa50d2fbf44162aec13994b747b9bd7ac
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230963"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a>Optimizar un bot con la limitación de volumen en Teams

La limitación de velocidad es un método para limitar los mensajes a una frecuencia máxima determinada. Como principio general, la aplicación debe limitar el número de mensajes que publica a una conversación de canal o chat individual. Esto garantiza una experiencia óptima y los mensajes no aparecen como correo no deseado para los usuarios.

Para proteger Microsoft Teams y sus usuarios, las API del bot proporcionan un límite de velocidad para las solicitudes entrantes. Las aplicaciones que superen este límite reciben un `HTTP 429 Too Many Requests` estado de error. Todas las solicitudes están sujetas a la misma directiva de limitación de tasas, incluido el envío de mensajes, enumeraciones de canales y recuperaciones de listas.

Como los valores exactos de los límites de tasa están sujetos a cambios, la aplicación debe implementar el comportamiento de devolución adecuado cuando la API devuelva `HTTP 429 Too Many Requests` .

## <a name="handle-rate-limits"></a>Controlar límites de velocidad

Al emitir una operación del SDK de Bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.

El siguiente código muestra un ejemplo de control de límites de velocidad:

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

Después de controlar los límites de velocidad de los bots, puedes controlar `HTTP 429` las respuestas con un retroceso exponencial.

## <a name="handle-http-429-responses"></a>Controlar `HTTP 429` respuestas

En general, debe tomar precauciones simples para evitar recibir `HTTP 429` respuestas. Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal. En su lugar, cree un lote de las solicitudes api.

El uso de un retroceso exponencial con un vibración aleatoria es la forma recomendada de controlar 429s. Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.

Después de controlar `HTTP 429` las respuestas, puede seguir el ejemplo para detectar excepciones transitorias.

> [!NOTE]
> Además de volver a seleccionar el código de error **429**, también se deben volver a seleccionar los códigos de error **412**, **502** y **504.**

## <a name="detect-transient-exceptions-example"></a>Ejemplo de detección de excepciones transitorias

El siguiente código muestra un ejemplo de uso de retroceso exponencial mediante el bloque de aplicación de control de errores transitorios:

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

Puede realizar backoff y reintentos mediante [el control de errores transitorios](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29). Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea agregar el bloque de aplicación de control de errores [transitorios a la solución](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN). Vea también [control de errores transitorios](/azure/architecture/best-practices/transient-faults).

Después de pasar por el ejemplo para detectar excepciones transitorias, vaya a través del ejemplo de retroceso exponencial. Puede usar retroceso exponencial en lugar de reintentar errores.

## <a name="backoff-example"></a>Ejemplo de copia de seguridad

Además de detectar límites de velocidad, también puede realizar un retroceso exponencial.

El código siguiente muestra un ejemplo de retroceso exponencial:

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

También puede realizar una ejecución `System.Action` de método con la directiva de reintentos descrita en esta sección. La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de desuso lineal.

Almacena el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.

Para obtener más información, vea [retry patterns](/azure/architecture/patterns/retry).

También puedes controlar el límite de velocidad usando el límite por bot por subproceso.

## <a name="per-bot-per-thread-limit"></a>Por bot por límite de subprocesos

El límite por bot por subproceso controla el tráfico que un bot puede generar en una sola conversación. Una conversación es 1:1 entre bot y usuario, un chat de grupo o un canal de un equipo. Por lo tanto, si la aplicación envía un mensaje de bot a cada usuario, el límite de subprocesos no limita.

>[!NOTE]
> * El límite de subprocesos de 3600 segundos y 1800 operaciones solo se aplica si se envían varios mensajes de bot a un solo usuario. 
> * El límite global por aplicación por inquilino es de 50 solicitudes por segundo (RPS). Por lo tanto, el número total de mensajes de bot por segundo no debe cruzar el límite de subprocesos.
> * La división de mensajes en el nivel de servicio da como resultado rps superior a lo esperado. Si le preocupa acercarse a los límites, debe implementar la [estrategia de despegar](#backoff-example). Los valores proporcionados en esta sección son solo para estimación.

En la tabla siguiente se proporcionan los límites por bot por subproceso:

| Escenario | Período de tiempo en segundos | Operaciones máximas permitidas |
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
> Las versiones anteriores `TeamsInfo.getMembers` de y las API están en `TeamsInfo.GetMembersAsync` desuso. Se limitan a cinco solicitudes por minuto y devuelven un máximo de 10.000 miembros por equipo. Para actualizar el SDK de Bot Framework y el código para usar los extremos de API paginados más recientes, consulte [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).

También puede controlar el límite de velocidad usando el límite por subproceso para todos los bots.

## <a name="per-thread-limit-for-all-bots"></a>Límite por subproceso para todos los bots

El límite por subproceso para todos los bots controla el tráfico que todos los bots pueden generar en una sola conversación. Una conversación aquí es 1:1 entre bot y usuario, un chat de grupo o un canal en un equipo.

En la tabla siguiente se proporciona el límite por subproceso para todos los bots:

| Escenario | Período de tiempo en segundos | Operaciones máximas permitidas |
| --- | --- | --- |
| Enviar a conversación | 1 | 14  |
| Enviar a conversación | 2 | 16  |
| Crear conversación | 1 | 14  |
| Crear conversación | 2 | 16  |
| Crear conversación| 1 | 14  |
| Crear conversación| 2 | 16  |
| Obtener miembros de conversación| 1 | 28 |
| Obtener miembros de conversación| 2 | 32 |
| Obtener conversaciones | 1 | 28 |
| Obtener conversaciones | 2 | 32 |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Llamadas y reuniones en el bot](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

