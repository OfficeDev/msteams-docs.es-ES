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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>Optimizar el bot: límites de velocidad y procedimientos recomendados en Microsoft Teams

Como principio general, la aplicación debe limitar el número de mensajes que envía a un chat o a una conversación de canal individuales. Esto garantiza una experiencia óptima que no siente "correo no deseado" para los usuarios finales.

Para proteger Microsoft Teams y sus usuarios, la API de bot limita la velocidad de las solicitudes entrantes. Las aplicaciones que superen este límite recibirán un `HTTP 429 Too Many Requests` estado de error. Todas las solicitudes están sujetas a la misma directiva de limitación de velocidad, como el envío de mensajes, enumeraciones de canales e recuperaciones de lista.

Como los valores exactos de los límites de velocidad están sujetos a cambios, recomendamos que la aplicación implemente el comportamiento `HTTP 429 Too Many Requests`de interrupción adecuado cuando la API vuelva.

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

Puede usar el multiplicador y los reintentos mediante [bibliotecas de control de errores transitorias](/previous-versions/msp-n-p/hh680901(v=pandp.50)). Para obtener instrucciones sobre cómo obtener e instalar el paquete NuGet, vea [Agregar el bloque de aplicación de control de errores transitorio a la solución](/previous-versions/msp-n-p/hh680891(v=pandp.50)) .

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
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), fixedIntervalRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync((Activity)reply)).ConfigureAwait(false);
```

También puede realizar una `System.Action` ejecución de método con la Directiva de reintentos descrita anteriormente. La biblioteca a la que se hace referencia también permite especificar un intervalo fijo o un mecanismo de interrupción lineal.

Se recomienda almacenar el valor y la estrategia en un archivo de configuración para ajustar y ajustar los valores en tiempo de ejecución.

Para obtener más información, consulte esta práctica guía sobre diversos patrones de reintento: [patrón de reintentos](/azure/architecture/patterns/retry).

## <a name="per-bot-per-thread-limit"></a>Por robot por límite de subprocesos

>[!NOTE]
>La división de mensajes en el nivel de servicio dará como resultado un número de solicitudes por segundo (RPS) superiores a lo esperado. Si le preocupan los límites, debe implementar la estrategia de punto de interrupción descrita anteriormente. Los valores proporcionados a continuación solo son para la estimación.

Este límite controla el tráfico que un bot puede generar en una sola conversación. Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.

| **Escenario** | **Tiempo: período (seg.)** | **Operaciones máximas permitidas** |
| --- | --- | --- |
| NewMessage | 1  | 7  |
| NewMessage | 2  | 8  |
| NewMessage | semestre | 60 |
| NewMessage | 3600 | 1800 |
| UpdateMessage | 1  | 7  |
| UpdateMessage | 2  | 8  |
| UpdateMessage | semestre | 60 |
| UpdateMessage | 3600 | 1800 |
| NewThread | 1  | 7  |
| NewThread | 2  | 8  |
| NewThread | semestre | 60 |
| NewThread | 3600 | 1800 |
| GetThreadMembers | 1  | 14  |
| GetThreadMembers | 2  | 16  |
| GetThreadMembers | semestre | 120 |
| GetThreadMembers | 3600 | 3600 |
| GetThread | 1  | 14  |
| GetThread | 2  | 16  |
| GetThread | semestre | 120 |
| GetThread | 3600 | 3600 |

## <a name="per-thread-limit-for-all-bots"></a>Límite por subproceso para todos los bots

Este límite controla el tráfico que pueden generar todos los bots a través de una sola conversación. Una conversación aquí es 1:1 entre el bot y el usuario, un grupo de chat o un canal en un equipo.

| **Escenario** | **Tiempo: período (seg.)** | **Operaciones máximas permitidas** |
| --- | --- | --- |
| NewMessage | 1  | 14  |
| NewMessage | 2  | 16  |
| UpdateMessage | 1  | 14  |
| UpdateMessage | 2  | 16  |
| NewThread | 1  | 14  |
| NewThread | 2  | 16  |
| GetThreadMembers | 1  | 28 |
| GetThreadMembers | 2  | 32 |
| GetThread | 1  | 28 |
| GetThread | 2  | 32 |

## <a name="bot-per-data-center-limit"></a>Bot por límite de centro de datos

Este límite controla el tráfico que un bot puede generar a través de todos los subprocesos de un centro de datos (en varios inquilinos).

|**Tiempo: período (seg.)** | **Operaciones máximas permitidas** |
| --- | --- |
| 1  | 20 |
| 1800 | 8000 |
| 3600 | 15000 |
