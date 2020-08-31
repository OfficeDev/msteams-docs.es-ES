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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>Optimizar el bot: límites de velocidad y procedimientos recomendados en Microsoft Teams

Como principio general, la aplicación debe limitar el número de mensajes que envía a un chat o a una conversación de canal individuales. Esto garantiza una experiencia óptima que no siente "correo no deseado" para los usuarios finales.

Para proteger Microsoft Teams y sus usuarios, la API de bot limita la velocidad de las solicitudes entrantes. Las aplicaciones que superen este límite recibirán un `HTTP 429 Too Many Requests` Estado de error. Todas las solicitudes están sujetas a la misma directiva de limitación de velocidad, como el envío de mensajes, enumeraciones de canales e recuperaciones de lista.

Como los valores exactos de los límites de velocidad están sujetos a cambios, recomendamos que la aplicación implemente el comportamiento de interrupción adecuado cuando la API vuelva `HTTP 429 Too Many Requests` .

## <a name="handling-rate-limits"></a>Límites de velocidad de manipulación

Al emitir una operación del SDK de bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.

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

En general, debe tomar precauciones sencillas para evitar recibir `HTTP 429` respuestas. Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal. En su lugar, considere la posibilidad de procesar las solicitudes de API.

El uso de un punto de interrupción exponencial con una vibración aleatoria es la forma recomendada para controlar 429s. Esto garantiza que varias solicitudes no introduzcan colisiones en los reintentos.

## <a name="example-detecting-transient-exceptions"></a>Ejemplo: detectar excepciones transitorias

A continuación se muestra un ejemplo que usa el punto de interrupción exponencial mediante el bloque de aplicaciones transitorio de control de errores.

Puede realizar el multiplicador y los reintentos mediante el [control de errores transitorio](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29). Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea el tema sobre cómo [Agregar el bloque de aplicaciones de control de errores transitorio a la solución](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN). *Consulte también* [control de errores transitorios](/azure/architecture/best-practices/transient-faults).

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

## <a name="example-backoff"></a>Ejemplo: multiplicador

Además de detectar los límites de velocidad, también puede realizar un multiplicador exponencial.

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

También puede realizar una `System.Action` ejecución de método con la Directiva de reintentos descrita anteriormente. La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de interrupción lineal.

Se recomienda almacenar el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.

Para obtener más información, consulte esta práctica guía sobre diversos patrones de reintento: [patrón de reintentos](/azure/architecture/patterns/retry).

## <a name="per-bot-per-thread-limit"></a>Por robot por límite de subprocesos

>[!NOTE]
>La división de mensajes en el nivel de servicio dará como resultado un número de solicitudes por segundo (RPS) superiores a lo esperado. Si le preocupan los límites, debe implementar la estrategia de punto de interrupción descrita anteriormente. Los valores proporcionados a continuación solo son para la estimación.

Este límite controla el tráfico que un bot puede generar en una sola conversación. Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.

| **Escenario** | **Período de tiempo: (seg.)** | **Operaciones máximas permitidas** |
| --- | --- | --- |
| Enviar a conversación | 1  | 7  |
| Enviar a conversación | 2  | 8  |
| Enviar a conversación | semestre | 60 |
| Enviar a conversación | 3600 | 1800 |
| Crear conversación | 1  | 7  |
| Crear conversación | 2  | 8  |
| Crear conversación | semestre | 60 |
| Crear conversación | 3600 | 1800 |
| Obtener miembros de la conversación| 1  | 14  |
| Obtener miembros de la conversación| 2  | 16  |
| Obtener miembros de la conversación| semestre | 120 |
| Obtener miembros de la conversación| 3600 | 3600 |
| Obtener conversaciones | 1  | 14  |
| Obtener conversaciones | 2  | 16  |
| Obtener conversaciones | semestre | 120 |
| Obtener conversaciones | 3600 | 3600 |

## <a name="per-thread-limit-for-all-bots"></a>Límite por subproceso para todos los bots

Este límite controla el tráfico que pueden generar todos los bots a través de una sola conversación. Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.

| **Escenario** | **Período de tiempo: (seg.)** | **Operaciones máximas permitidas** |
| --- | --- | --- |
| Enviar a conversación | 1  | 14  |
| Enviar a conversación | 2  | 16  |
| Crear conversación | 1  | 14  |
| Crear conversación | 2  | 16  |
| CreateConversation| 1  | 14  |
| CreateConversation| 2  | 16  |
| Obtener miembros de la conversación| 1  | 28 |
| Obtener miembros de la conversación| 2  | 32 |
| Obtener conversaciones | 1  | 28 |
| Obtener conversaciones | 2  | 32 |
