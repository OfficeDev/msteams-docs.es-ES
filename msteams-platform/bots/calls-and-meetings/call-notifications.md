---
title: Detalles técnicos sobre el control de las notificaciones de llamadas entrantes
description: Información técnica detallada sobre cómo controlar las notificaciones de llamadas entrantes
keywords: llamar a las notificaciones de llamadas afinidad de región de devolución de llamada
ms.date: 04/02/2019
ms.openlocfilehash: be8860ff70cd7dff4fd9599079ea7aab4f454174
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676130"
---
# <a name="incoming-call-notifications-technical-details"></a>Notificaciones de llamadas entrantes: detalles técnicos

Al [registrar un bot de llamadas y reuniones para Microsoft Teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), mencionamos la URL del **webhook (para llamadas)** : el punto de conexión de webhook para todas las llamadas entrantes a su bot. En este tema se describen los detalles técnicos que necesitará para responder a estas notificaciones.

## <a name="protocol-determination"></a>Determinación de protocolo

La notificación entrante se proporciona en el formato heredado para la compatibilidad con el [Protocolo de Skype](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0)anterior. Para convertir la llamada al Protocolo de Microsoft Graph, el bot debe determinar si la notificación está en formato heredado y responder con:

```http
HTTP/1.1 204 No Content
```

El bot recibirá la notificación de nuevo, pero esta vez en el protocolo Microsoft Graph.

En una versión futura de la plataforma de medios en tiempo real, le permitirá configurar el protocolo que admite la aplicación para evitar recibir la devolución de llamada inicial en el formato heredado.

## <a name="redirects-for-region-affinity"></a>Redireccionamientos para la afinidad regional

Llamará a su webhook desde el centro de datos que hospeda la llamada. La llamada puede iniciarse en cualquier centro de datos y no se toma en cuenta las afinidades de región. La notificación se enviará a su implementación en función de la resolución de GeoDNS. Si la aplicación determina, mediante la inspección de la carga de notificación inicial o de otro modo, que debe ejecutarse en una implementación distinta, la aplicación puede responder con:

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Permita que el bot conteste una llamada entrante mediante la API de [respuesta](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) . Puede especificar el `callbackUri` para controlar esta llamada en particular. Esto es útil para las instancias de _Estado_ en las que la llamada se controla con una partición determinada y se desea incrustar esta `callbackUri` información en el para el enrutamiento a la instancia correcta.

## <a name="authenticating-the-callback"></a>Autenticación de la devolución de llamada

El bot debe inspeccionar el token publicado en el webhook para validar la solicitud. Siempre que la API publique en el webhook, el mensaje HTTP POST contiene un token de OAuth en el encabezado Authorization como token de portador, con la audiencia como identificador de aplicación de la aplicación.

La aplicación debe validar este token antes de aceptar la solicitud de devolución de llamada.

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

El token de OAuth tendrá valores como los siguientes y será firmado por Skype. La configuración de OpenID publicada <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> en puede usarse para comprobar el token.

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

* la audiencia de **500 AUD** es el URI de identificador de aplicación especificado para la aplicación.
* **TID** es el identificador de inquilino de contoso.com.
* **ISS** es el emisor de tokens `https://api.botframework.com`.

El código que controla el webhook debe validar el token, asegurarse de que no ha expirado y comprobar si la configuración de OpenID publicada está firmada. También debe comprobar si **AUD** coincide con el identificador de la aplicación antes de aceptar la solicitud de devolución de llamada.

[Ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) se muestra cómo validar las solicitudes entrantes.
