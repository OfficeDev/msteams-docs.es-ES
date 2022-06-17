---
title: Notificaciones de llamadas entrantes
description: En este módulo, obtenga información técnica detallada sobre cómo controlar las notificaciones de llamadas entrantes, redirigir y autenticar llamadas mediante ejemplos de código.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 04/02/2019
ms.openlocfilehash: fd68b85a3c6f5f4682a728461d792093bcd8cac0
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143833"
---
# <a name="incoming-call-notifications"></a>Notificaciones de llamadas entrantes

Al [registrar un bot de llamadas y reuniones para Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities), se menciona el webhook para la dirección URL de llamada. Esta dirección URL es el punto de conexión de webhook para todas las llamadas entrantes al bot.

## <a name="protocol-determination"></a>Determinación del protocolo

La notificación entrante se proporciona en un formato heredado por compatibilidad con el [protocolo de Skype](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true) anterior. Para convertir la llamada al protocolo microsoft Graph, el bot debe determinar si la notificación está en un formato heredado y proporciona la siguiente respuesta:

```http
HTTP/1.1 204 No Content
```

El bot recibe la notificación de nuevo, pero esta vez en el protocolo Microsoft Graph.

En una versión futura de la plataforma multimedia en tiempo real, podrá configurar el protocolo que admite la aplicación para evitar recibir la devolución de llamada inicial en el formato heredado.

En la sección siguiente se proporcionan detalles sobre las notificaciones de llamada entrantes redirigidas para la afinidad de región a la implementación.

## <a name="redirects-for-region-affinity"></a>Redireccionamientos por afinidad de región

Llame al webhook desde el centro de datos que hospeda la llamada. La llamada se inicia en cualquier centro de datos y no tiene en cuenta las afinidades entre regiones. La notificación se envía a la implementación en función de la resolución de GeoDNS. Si mediante la inspección de la carga de notificación inicial o de otro modo la aplicación determina que debe ejecutarse en una implementación diferente, la aplicación proporcionará la siguiente respuesta:

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Habilite el bot para responder a una llamada entrante mediante la API de [ respuesta](/graph/api/call-answer?view=graph-rest-1.0&tabs=http&preserve-view=true). Puede especificar el `callbackUri` para controlar esta llamada en particular. Esto es útil para las instancias con estado en las que la llamada se controla mediante una partición determinada y desea insertar esta información en `callbackUri` para enrutar a la instancia correcta.

En la sección siguiente se proporcionan detalles sobre la autenticación de la devolución de llamada mediante la inspección del token publicado en el webhook.

## <a name="authenticate-the-callback"></a>Autenticar la devolución de llamada

El bot debe inspeccionar el token publicado en el webhook para validar la solicitud. Cada vez que la API publica en el webhook, el mensaje HTTP POST contiene un token de OAuth en el encabezado de autorización que sirve como token de portador, con la audiencia como el identificador de la aplicación.

La aplicación debe validar este token antes de aceptar la solicitud de devolución de llamada.

El siguiente código de ejemplo se usa para autenticar la devolución de llamada:

```http
POST https://bot.contoso.com/api/calls
Content-Type: application/json
Authentication: Bearer <TOKEN>

"value": [
    "subscriptionId": "2887CEE8344B47C291F1AF628599A93C",
    "subscriptionExpirationDateTime": "2016-11-20T18:23:45.9356913Z",
    "changeType": "updated",
    "resource": "/app/calls/8A934F51F25B4EE19613D4049491857B",
    "resourceData": {
        "@odata.type": "#microsoft.graph.call",
        "state": "Established"
    }
]
```

El token de OAuth tiene los siguientes valores y está firmado por Skype:

```json
{
    "aud": "0efc74f7-41c3-47a4-8775-7259bfef4241",
    "iss": "https://api.botframework.com",
    "iat": 1466741440,
    "nbf": 1466741440,
    "exp": 1466745340,
    "tid": "1fdd12d0-4620-44ed-baec-459b611f84b2"
}
```

La configuración de OpenID publicada en <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> se puede usar para comprobar el token. Cada valor de token de OAuth se usa de la siguiente manera:

* `aud` donde la audiencia es el URI de id. de aplicación especificado para la aplicación.
* `tid` es el identificador de inquilino de Contoso.com.
* `iss` es el emisor del token, `https://api.botframework.com`.

Para el control de código, el webhook debe validar el token, asegurarse de que no ha expirado y comprobar si la configuración de OpenID publicada lo ha firmado. También debe comprobar si "aud" coincide con el identificador de la aplicación antes de aceptar la solicitud de devolución de llamada.

Para obtener más información, vea [Validar las solicitudes entrantes](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Requisiciones y consideraciones para bots multimedia hospedados en la aplicación](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)

## <a name="see-also"></a>Consulte también

* [Configurar un operador automático](/microsoftteams/create-a-phone-system-auto-attendant)
* [Configuración de la respuesta automática para las salas de Teams en dispositivos Android y de vídeo de teléfono Teams](/microsoftteams/set-up-auto-answer-on-teams-android)