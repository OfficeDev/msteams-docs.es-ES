---
title: Notificaciones de llamadas entrantes
description: Información técnica detallada sobre cómo controlar las notificaciones de llamadas entrantes
ms.topic: conceptual
localization_priority: Normal
keywords: afinidad de región de devolución de llamada de llamadas de llamadas
ms.date: 04/02/2019
ms.openlocfilehash: 06068c13d27598b9a7b5e70181c69f9efb2c0afb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020179"
---
# <a name="incoming-call-notifications"></a><span data-ttu-id="46c90-104">Notificaciones de llamadas entrantes</span><span class="sxs-lookup"><span data-stu-id="46c90-104">Incoming call notifications</span></span>

<span data-ttu-id="46c90-105">Al registrar un bot de llamadas y reuniones para [Microsoft Teams,](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)se menciona el webhook para la dirección URL de llamada.</span><span class="sxs-lookup"><span data-stu-id="46c90-105">In [registering a calls and meetings bot for Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities), the Webhook for calling URL is mentioned.</span></span> <span data-ttu-id="46c90-106">Esta dirección URL es el extremo de webhook para todas las llamadas entrantes al bot.</span><span class="sxs-lookup"><span data-stu-id="46c90-106">This URL is the webhook endpoint for all incoming calls to your bot.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="46c90-107">Determinación del protocolo</span><span class="sxs-lookup"><span data-stu-id="46c90-107">Protocol determination</span></span>

<span data-ttu-id="46c90-108">La notificación entrante se proporciona en un formato heredado para la compatibilidad con el protocolo [de Skype anterior](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="46c90-108">The incoming notification is provided in a legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="46c90-109">Para convertir la llamada al protocolo de Microsoft Graph, el bot debe determinar si la notificación está en un formato heredado y proporcionar la siguiente respuesta:</span><span class="sxs-lookup"><span data-stu-id="46c90-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in a legacy format and provide the following response:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="46c90-110">El bot recibe la notificación de nuevo, pero esta vez en el protocolo de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="46c90-110">Your bot receives the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="46c90-111">En una versión futura de la Plataforma multimedia en tiempo real, puede configurar el protocolo que admite la aplicación para evitar recibir la devolución de llamada inicial en el formato heredado.</span><span class="sxs-lookup"><span data-stu-id="46c90-111">In a future release of the Real-time Media Platform, you can configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

<span data-ttu-id="46c90-112">En la siguiente sección se proporcionan detalles sobre las notificaciones de llamadas entrantes redirigidas por afinidad de región a la implementación.</span><span class="sxs-lookup"><span data-stu-id="46c90-112">The next section provides details on incoming call notifications redirected for region affinity to your deployment.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="46c90-113">Redirecciones para afinidad de región</span><span class="sxs-lookup"><span data-stu-id="46c90-113">Redirects for region affinity</span></span>

<span data-ttu-id="46c90-114">Se llama al webhook desde el centro de datos que hospeda la llamada.</span><span class="sxs-lookup"><span data-stu-id="46c90-114">You call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="46c90-115">La llamada se inicia en cualquier centro de datos y no tiene en cuenta las afinidades de región.</span><span class="sxs-lookup"><span data-stu-id="46c90-115">The call starts in any data center and does not take into account region affinities.</span></span> <span data-ttu-id="46c90-116">La notificación se envía a la implementación en función de la resolución de GeoDNS.</span><span class="sxs-lookup"><span data-stu-id="46c90-116">The notification is sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="46c90-117">Si la aplicación determina, mediante la inspección de la carga de notificación inicial o de otro modo, que debe ejecutarse en una implementación diferente, la aplicación proporciona la siguiente respuesta:</span><span class="sxs-lookup"><span data-stu-id="46c90-117">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application provides the following response:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="46c90-118">Habilite el bot para responder a una llamada entrante mediante la API [de respuesta.](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer)</span><span class="sxs-lookup"><span data-stu-id="46c90-118">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="46c90-119">Puede especificar el para `callbackUri` controlar esta llamada en particular.</span><span class="sxs-lookup"><span data-stu-id="46c90-119">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="46c90-120">Esto es útil para instancias con estado en las que una partición determinada controla la llamada y desea insertar esta información en el enrutamiento a `callbackUri` la instancia correcta.</span><span class="sxs-lookup"><span data-stu-id="46c90-120">This is useful for stateful instances where your call is handled by a particular partition, and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

<span data-ttu-id="46c90-121">La siguiente sección proporciona detalles sobre la autenticación de la devolución de llamada inspeccionando el token publicado en el webhook.</span><span class="sxs-lookup"><span data-stu-id="46c90-121">The next section provides details on authenticating the callback by inspecting the token posted to your webhook.</span></span>

## <a name="authenticate-the-callback"></a><span data-ttu-id="46c90-122">Autenticar la devolución de llamada</span><span class="sxs-lookup"><span data-stu-id="46c90-122">Authenticate the callback</span></span>

<span data-ttu-id="46c90-123">El bot debe inspeccionar el token publicado en el webhook para validar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="46c90-123">Your bot must inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="46c90-124">Cada vez que la API se publica en el webhook, el mensaje HTTP POST contiene un token OAuth en el encabezado Authorization como token portador, con la audiencia como id. de aplicación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="46c90-124">Every time the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a bearer token, with the audience as your application's App ID.</span></span>

<span data-ttu-id="46c90-125">La aplicación debe validar este token antes de aceptar la solicitud de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="46c90-125">Your application must validate this token before accepting the callback request.</span></span>

<span data-ttu-id="46c90-126">El siguiente código de ejemplo se usa para autenticar la devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="46c90-126">The following sample code is used to authenticate the callback:</span></span>

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

<span data-ttu-id="46c90-127">El token OAuth tiene los siguientes valores y está firmado por Skype:</span><span class="sxs-lookup"><span data-stu-id="46c90-127">The OAuth token has the following values, and is signed by Skype:</span></span>

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

<span data-ttu-id="46c90-128">La configuración de OpenID publicada en <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> se puede usar para comprobar el token.</span><span class="sxs-lookup"><span data-stu-id="46c90-128">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span> <span data-ttu-id="46c90-129">Cada valor de token de OAuth se usa de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="46c90-129">Each OAuth token value is used as follows:</span></span>

* <span data-ttu-id="46c90-130">`aud` donde audiencia es el URI de id. de aplicación especificado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="46c90-130">`aud` where audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="46c90-131">`tid` es el identificador de inquilino para Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="46c90-131">`tid` is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="46c90-132">`iss` es el emisor de tokens, `https://api.botframework.com` .</span><span class="sxs-lookup"><span data-stu-id="46c90-132">`iss` is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="46c90-133">Para el control de código, el webhook debe validar el token, asegurarse de que no ha expirado y comprobar si ha sido firmado por la configuración de OpenID publicada.</span><span class="sxs-lookup"><span data-stu-id="46c90-133">For your code handling, the webhook must validate the token, ensure it has not expired, and check whether it has been signed by the published OpenID configuration.</span></span> <span data-ttu-id="46c90-134">También debes comprobar si aud coincide con tu id. de aplicación antes de aceptar la solicitud de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="46c90-134">You must also check whether aud matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="46c90-135">Para obtener más información, vea [validate inbound requests](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).</span><span class="sxs-lookup"><span data-stu-id="46c90-135">For more information, see [validate inbound requests](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).</span></span>

## <a name="next-step"></a><span data-ttu-id="46c90-136">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="46c90-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46c90-137">Requisitos y consideraciones para bots multimedia hospedados en aplicaciones</span><span class="sxs-lookup"><span data-stu-id="46c90-137">Requirements and considerations for application-hosted media bots</span></span>](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
