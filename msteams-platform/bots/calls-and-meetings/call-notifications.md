---
title: Notificaciones de llamadas entrantes
description: Obtenga información técnica detallada sobre cómo controlar las notificaciones de llamadas entrantes, redirigir y autenticar llamadas mediante ejemplos de código
ms.topic: conceptual
ms.localizationpriority: medium
keywords: afinidad de región de devolución de llamada de llamadas de llamadas
ms.date: 04/02/2019
ms.openlocfilehash: a1d2362347643badc06a23d967120c8f14a17200
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453057"
---
# <a name="incoming-call-notifications"></a>Notificaciones de llamadas entrantes

Al [registrar un bot de llamadas y reuniones para Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities), se menciona el webhook para la dirección URL de llamada. Esta dirección URL es el extremo de webhook para todas las llamadas entrantes al bot.

## <a name="protocol-determination"></a>Determinación del protocolo

La notificación entrante se proporciona en un formato heredado para la compatibilidad con el protocolo [Skype anterior](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true). Para convertir la llamada al protocolo de microsoft Graph, el bot debe determinar si la notificación está en un formato heredado y proporcionar la siguiente respuesta:

```http
HTTP/1.1 204 No Content
```

El bot vuelve a recibir la notificación, pero esta vez en el protocolo Graph Microsoft.

En una versión futura de la Plataforma multimedia en tiempo real, puede configurar el protocolo que admite la aplicación para evitar recibir la devolución de llamada inicial en el formato heredado.

En la siguiente sección se proporcionan detalles sobre las notificaciones de llamadas entrantes redirigidas por afinidad de región a la implementación.

## <a name="redirects-for-region-affinity"></a>Redirecciones para afinidad de región

Se llama al webhook desde el centro de datos que hospeda la llamada. La llamada se inicia en cualquier centro de datos y no tiene en cuenta las afinidades de región. La notificación se envía a la implementación en función de la resolución de GeoDNS. Si la aplicación determina, mediante la inspección de la carga de notificación inicial o de otro modo, que debe ejecutarse en una implementación diferente, la aplicación proporciona la siguiente respuesta:

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Habilite el bot para responder a una llamada entrante mediante la API [de respuesta](/graph/api/call-answer?view=graph-rest-1.0&tabs=http&preserve-view=true) . Puede especificar el para `callbackUri` controlar esta llamada en particular. Esto es útil para instancias con estado en las que una partición determinada controla la llamada y `callbackUri` desea insertar esta información en el enrutamiento a la instancia correcta.

La siguiente sección proporciona detalles sobre la autenticación de la devolución de llamada inspeccionando el token publicado en el webhook.

## <a name="authenticate-the-callback"></a>Autenticar la devolución de llamada

El bot debe inspeccionar el token publicado en el webhook para validar la solicitud. Cada vez que la API se publica en el webhook, el mensaje HTTP POST contiene un token OAuth en el encabezado Authorization como token portador, con la audiencia como id. de aplicación de la aplicación.

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

El token OAuth tiene los siguientes valores y está firmado por Skype:

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

* `aud` donde audiencia es el URI de id. de aplicación especificado para la aplicación.
* `tid` es el identificador de inquilino para Contoso.com.
* `iss` es el emisor de tokens, `https://api.botframework.com`.

Para el control de código, el webhook debe validar el token, asegurarse de que no ha expirado y comprobar si ha sido firmado por la configuración de OpenID publicada. También debes comprobar si aud coincide con tu id. de aplicación antes de aceptar la solicitud de devolución de llamada.

Para obtener más información, vea [Validar solicitudes entrantes](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Requisitos y consideraciones para bots multimedia hospedados en aplicaciones](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
