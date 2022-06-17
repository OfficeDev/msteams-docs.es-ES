---
title: Optimizar un bot con la limitación de volumen en Teams
description: Obtenga información sobre el control del límite de velocidad de bots con por bot por subproceso y por límite para todos los bots mediante ejemplos de código
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: f6afb9cd3b3894dff31ecaf5e8d9ece7204248a1
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143735"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a>Optimizar un bot con la limitación de volumen en Teams

La limitación de volumen es un método para limitar los mensajes a una determinada frecuencia máxima. Como principio general, la aplicación debe limitar el número de mensajes que envía a una conversación de chat o canal individual. Esto garantiza una experiencia óptima y que los mensajes no aparezcan como correo no deseado para los usuarios.

Para proteger Microsoft Teams y a sus usuarios, las API del bot proporcionan un límite de velocidad para las solicitudes entrantes. Las aplicaciones que superan este límite reciben un estado de error `HTTP 429 Too Many Requests`. Todas las solicitudes están sujetas a la misma directiva de limitación de velocidad, incluido el envío de mensajes, enumeraciones de canales y capturas de lista de participantes.

Dado que los valores exactos de los límites de velocidad están sujetos a cambios, la aplicación debe implementar el comportamiento de retroceso adecuado cuando la API devuelva `HTTP 429 Too Many Requests`.

## <a name="handle-rate-limits"></a>Controlar los límites de volumen

Al emitir una operación del SDK de Bot Builder, puede controlar `Microsoft.Rest.HttpOperationException` y comprobar el código de estado.

En el código siguiente se muestra un ejemplo de control de límites de volumen:

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

Después de controlar los límites de volumen de los bots, puede controlar `HTTP 429` las respuestas mediante un retroceso exponencial.

## <a name="handle-http-429-responses"></a>Controlar `HTTP 429` respuestas

En general, debe tomar precauciones simples para evitar recibir `HTTP 429` respuestas. Por ejemplo, evite emitir varias solicitudes a la misma conversación personal o de canal. En su lugar, cree un lote de las solicitudes de API.

Usar un retroceso exponencial con una vibración aleatoria es la manera recomendada de controlar 429s. Esto garantiza que varias solicitudes no introducen colisiones en los reintentos.

Después de controlar las `HTTP 429` respuestas, puede seguir el ejemplo para detectar excepciones transitorias.

> [!NOTE]
> Además de reintentar el código de error **429**, también se deben reintentar los códigos de error **412**, **502** y **504**.

## <a name="detect-transient-exceptions-example"></a>Ejemplo de detección de excepciones transitorias

En el código siguiente se muestra un ejemplo de uso de retroceso exponencial mediante el bloque de aplicación de control de errores transitorio:

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
    {
        // List of error codes to retry on
        List<int> transientErrorStatusCodes = new List<int>() { 429 };

        public static bool IsTransient(Exception ex)
          {
              if (ex.Message.Contains("429"))
                  return true;

              HttpResponseMessageWrapper? response = null;
              if (ex is HttpOperationException httpOperationException)
              {
                  response = httpOperationException.Response;
              }
              else
              if (ex is ErrorResponseException errorResponseException)
              {
                  response = errorResponseException.Response;
              }
              return response != null && transientErrorStatusCodes.Contains((int)response.StatusCode);
          }
    }
```

Puede realizar reintentos y reintentos mediante el [control de errores transitorios](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29). Para obtener instrucciones sobre cómo obtener e instalar el paquete de NuGet, consulte [adición del bloque de aplicación de control de errores transitorios a la solución](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN). Consulte también [Control de errores transitorios](/azure/architecture/best-practices/transient-faults).

Después de pasar por el ejemplo para detectar excepciones transitorias, pase por el ejemplo de retroceso exponencial. Puede usar el retroceso exponencial en lugar de reintentar en los errores.

## <a name="backoff-example"></a>Ejemplo de retroceso

Además de detectar límites de volumen, también puede realizar un retroceso exponencial.

El siguiente código muestra un ejemplo de retroceso exponencial:

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

También puede realizar una ejecución de método `System.Action` con la directiva de reintentos descrita en esta sección. La biblioteca a la que se hace referencia también le permite especificar un intervalo fijo o un mecanismo de retroceso lineal.

Almacene el valor y la estrategia en un archivo de configuración para ajustar los valores en tiempo de ejecución.

Para obtener más información, consulte [patrones de reintento](/azure/architecture/patterns/retry).

También puede controlar el límite de velocidad mediante el límite por bot por subproceso.

## <a name="per-bot-per-thread-limit"></a>Límite por bot subproceso

El límite por bot por subproceso controla el tráfico que un bot puede generar en una sola conversación. Una conversación es 1:1 entre bot y usuario, un chat grupal o un canal en un equipo. Por lo tanto, si la aplicación envía un mensaje de bot a cada usuario, el límite de subprocesos no se limita.

>[!NOTE]
>
> * El límite de subprocesos de 3600 segundos y 1800 operaciones solo se aplica si se envían varios mensajes de bot a un único usuario.
> * El límite global por aplicación por inquilino es de 50 solicitudes por segundo (RPS). Por lo tanto, el número total de mensajes de bot por segundo no debe superar el límite de subprocesos.
> * La división de mensajes en el nivel de servicio da como resultado un RPS superior al esperado. Si le preocupa acercarse a los límites, debe implementar la [estrategia de retroceso](#backoff-example). Los valores proporcionados en esta sección son solo para estimación.

En la tabla siguiente se proporcionan los límites por bot por subproceso:

| Escenario | Tiempo en segundos | Máximo de operaciones permitidas |
| --- | --- | --- |
| Enviar a la conversación | 1 | 7  |
| Enviar a la conversación | 2 | 8  |
| Enviar a la conversación | 30 | 60 |
| Enviar a la conversación | 3600 | 1800 |
| Crear conversación | 1 | 7  |
| Crear conversación | 2 | 8  |
| Crear conversación | 30 | 60 |
| Crear conversación | 3600 | 1800 |
| Obtener miembros de la conversación| 1 | 14  |
| Obtener miembros de la conversación| 2 | 16  |
| Obtener miembros de la conversación| 30 | 120 |
| Obtener miembros de la conversación| 3600 | 3600 |
| Obtener conversaciones | 1 | 14  |
| Obtener conversaciones | 2 | 16  |
| Obtener conversaciones | 30 | 120 |
| Obtener conversaciones | 3600 | 3600 |

>[!NOTE]
> Las versiones anteriores de las API de `TeamsInfo.getMembers` y `TeamsInfo.GetMembersAsync` están en desuso. Se limitan a cinco solicitudes por minuto y devuelven un máximo de 10 000 miembros por equipo. Para actualizar el SDK del marco del bot y el código para usar los puntos de conexión de API paginados más recientes, consulte [Cambios de bot API para miembros del equipo y del chat](../../resources/team-chat-member-api-changes.md).

También puede controlar el límite de velocidad mediante el límite por subproceso para todos los bots.

## <a name="per-thread-limit-for-all-bots"></a>Límite por subproceso para todos los bots

El límite por subproceso para todos los bots controla el tráfico que todos los bots pueden generar en una sola conversación. Una conversación aquí es 1:1 entre bot y usuario, un chat de grupo o un canal en un equipo.

En la tabla siguiente se proporciona el límite por subproceso para todos los bots:

| Escenario | Tiempo en segundos | Máximo de operaciones permitidas |
| --- | --- | --- |
| Enviar a la conversación | 1 | 14  |
| Enviar a la conversación | 2 | 16  |
| Crear conversación | 1 | 14  |
| Crear conversación | 2 | 16  |
| Crear conversación| 1 | 14  |
| Crear conversación| 2 | 16  |
| Obtener miembros de la conversación| 1 | 28 |
| Obtener miembros de la conversación| 2 | 32 |
| Obtener conversaciones | 1 | 28 |
| Obtener conversaciones | 2 | 32 |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Bots de llamadas y reuniones](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
