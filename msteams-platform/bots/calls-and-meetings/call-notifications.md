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
# <a name="incoming-call-notifications-technical-details"></a><span data-ttu-id="cc14a-104">Notificaciones de llamadas entrantes: detalles técnicos</span><span class="sxs-lookup"><span data-stu-id="cc14a-104">Incoming call notifications: technical details</span></span>

<span data-ttu-id="cc14a-105">Al [registrar un bot de llamadas y reuniones para Microsoft Teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), mencionamos la URL del **webhook (para llamadas)** : el punto de conexión de webhook para todas las llamadas entrantes a su bot.</span><span class="sxs-lookup"><span data-stu-id="cc14a-105">In [Registering a calling and meeting bot for Microsoft Teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), we mentioned the **Webhook (for calling)** URL — the webhook endpoint for all incoming calls to your bot.</span></span> <span data-ttu-id="cc14a-106">En este tema se describen los detalles técnicos que necesitará para responder a estas notificaciones.</span><span class="sxs-lookup"><span data-stu-id="cc14a-106">This topic discusses the technical details you'll need to respond to these notifications.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="cc14a-107">Determinación de protocolo</span><span class="sxs-lookup"><span data-stu-id="cc14a-107">Protocol determination</span></span>

<span data-ttu-id="cc14a-108">La notificación entrante se proporciona en el formato heredado para la compatibilidad con el [Protocolo de Skype](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0)anterior.</span><span class="sxs-lookup"><span data-stu-id="cc14a-108">The incoming notification is provided in legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="cc14a-109">Para convertir la llamada al Protocolo de Microsoft Graph, el bot debe determinar si la notificación está en formato heredado y responder con:</span><span class="sxs-lookup"><span data-stu-id="cc14a-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in legacy format and reply with:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="cc14a-110">El bot recibirá la notificación de nuevo, pero esta vez en el protocolo Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="cc14a-110">Your bot will receive the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="cc14a-111">En una versión futura de la plataforma de medios en tiempo real, le permitirá configurar el protocolo que admite la aplicación para evitar recibir la devolución de llamada inicial en el formato heredado.</span><span class="sxs-lookup"><span data-stu-id="cc14a-111">In a future release of the Real-time Media Platform, we'll allow you to configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="cc14a-112">Redireccionamientos para la afinidad regional</span><span class="sxs-lookup"><span data-stu-id="cc14a-112">Redirects for region affinity</span></span>

<span data-ttu-id="cc14a-113">Llamará a su webhook desde el centro de datos que hospeda la llamada.</span><span class="sxs-lookup"><span data-stu-id="cc14a-113">You'll call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="cc14a-114">La llamada puede iniciarse en cualquier centro de datos y no se toma en cuenta las afinidades de región.</span><span class="sxs-lookup"><span data-stu-id="cc14a-114">The call may start in any data center and doesn't take into account region affinities.</span></span> <span data-ttu-id="cc14a-115">La notificación se enviará a su implementación en función de la resolución de GeoDNS.</span><span class="sxs-lookup"><span data-stu-id="cc14a-115">The notification will be sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="cc14a-116">Si la aplicación determina, mediante la inspección de la carga de notificación inicial o de otro modo, que debe ejecutarse en una implementación distinta, la aplicación puede responder con:</span><span class="sxs-lookup"><span data-stu-id="cc14a-116">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application may reply with:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="cc14a-117">Permita que el bot conteste una llamada entrante mediante la API de [respuesta](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) .</span><span class="sxs-lookup"><span data-stu-id="cc14a-117">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="cc14a-118">Puede especificar el `callbackUri` para controlar esta llamada en particular.</span><span class="sxs-lookup"><span data-stu-id="cc14a-118">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="cc14a-119">Esto es útil para las instancias de _Estado_ en las que la llamada se controla con una partición determinada y se desea incrustar esta `callbackUri` información en el para el enrutamiento a la instancia correcta.</span><span class="sxs-lookup"><span data-stu-id="cc14a-119">This is useful for _stateful_ instances where your call is handled by a particular partition and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

## <a name="authenticating-the-callback"></a><span data-ttu-id="cc14a-120">Autenticación de la devolución de llamada</span><span class="sxs-lookup"><span data-stu-id="cc14a-120">Authenticating the callback</span></span>

<span data-ttu-id="cc14a-121">El bot debe inspeccionar el token publicado en el webhook para validar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="cc14a-121">Your bot should inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="cc14a-122">Siempre que la API publique en el webhook, el mensaje HTTP POST contiene un token de OAuth en el encabezado Authorization como token de portador, con la audiencia como identificador de aplicación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc14a-122">Whenever the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a Bearer token, with audience as your application's App ID.</span></span>

<span data-ttu-id="cc14a-123">La aplicación debe validar este token antes de aceptar la solicitud de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="cc14a-123">Your application should validate this token before accepting the callback request.</span></span>

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

<span data-ttu-id="cc14a-124">El token de OAuth tendrá valores como los siguientes y será firmado por Skype.</span><span class="sxs-lookup"><span data-stu-id="cc14a-124">The OAuth token will have values like the following, and will be signed by Skype.</span></span> <span data-ttu-id="cc14a-125">La configuración de OpenID publicada <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> en puede usarse para comprobar el token.</span><span class="sxs-lookup"><span data-stu-id="cc14a-125">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span>

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

* <span data-ttu-id="cc14a-126">la audiencia de **500 AUD** es el URI de identificador de aplicación especificado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc14a-126">**aud** audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="cc14a-127">**TID** es el identificador de inquilino de contoso.com.</span><span class="sxs-lookup"><span data-stu-id="cc14a-127">**tid** is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="cc14a-128">**ISS** es el emisor de tokens `https://api.botframework.com`.</span><span class="sxs-lookup"><span data-stu-id="cc14a-128">**iss** is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="cc14a-129">El código que controla el webhook debe validar el token, asegurarse de que no ha expirado y comprobar si la configuración de OpenID publicada está firmada.</span><span class="sxs-lookup"><span data-stu-id="cc14a-129">Your code handling the webhook should validate the token, ensure it hasn't expired, and check whether it has been signed by our published OpenID configuration.</span></span> <span data-ttu-id="cc14a-130">También debe comprobar si **AUD** coincide con el identificador de la aplicación antes de aceptar la solicitud de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="cc14a-130">You should also check whether **aud** matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="cc14a-131">[Ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) se muestra cómo validar las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="cc14a-131">[Sample](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) shows how to validate inbound requests.</span></span>
