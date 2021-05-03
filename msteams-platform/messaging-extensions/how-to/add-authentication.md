---
title: Agregar autenticación a la extensión de mensajería
author: clearab
description: Cómo agregar autenticación a una extensión de mensajería
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1670bcd68def5470f2a590b11f7c25a00ccd06b7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020712"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="576ab-103">Agregar autenticación a la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="576ab-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="576ab-104">Identificar al usuario</span><span class="sxs-lookup"><span data-stu-id="576ab-104">Identify the user</span></span>

<span data-ttu-id="576ab-105">Cada solicitud a los servicios incluye el identificador de usuario, el nombre para mostrar del usuario y Azure Active Directory de objeto.</span><span class="sxs-lookup"><span data-stu-id="576ab-105">Every request to your services includes the user  ID, the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="576ab-106">Los valores y están garantizados para el usuario `id` Teams `aadObjectId` autenticado.</span><span class="sxs-lookup"><span data-stu-id="576ab-106">The `id` and `aadObjectId` values are guaranteed for the authenticated Teams user.</span></span> <span data-ttu-id="576ab-107">Se usan como claves para buscar las credenciales o cualquier estado almacenado en caché en el servicio.</span><span class="sxs-lookup"><span data-stu-id="576ab-107">They are used as keys to look up the credentials or any cached state in your service.</span></span> <span data-ttu-id="576ab-108">Además, cada solicitud contiene el Azure Active Directory de inquilino del usuario, que se usa para identificar la organización del usuario.</span><span class="sxs-lookup"><span data-stu-id="576ab-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which is used to identify the user’s organization.</span></span> <span data-ttu-id="576ab-109">Si procede, la solicitud también contiene el identificador de equipo y el identificador de canal desde el que se originó la solicitud.</span><span class="sxs-lookup"><span data-stu-id="576ab-109">If applicable, the request also contains the team Id and channel ID from which the request is originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="576ab-110">Autenticación</span><span class="sxs-lookup"><span data-stu-id="576ab-110">Authentication</span></span>

<span data-ttu-id="576ab-111">Si el servicio requiere autenticación de usuario, los usuarios deben iniciar sesión antes de usar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="576ab-111">If your service requires user authentication, the users must sign in before they use the messaging extension.</span></span> <span data-ttu-id="576ab-112">Los pasos de autenticación son similares a los de un bot o pestaña. La secuencia es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="576ab-112">The authentication steps are similar to that of a bot or tab. The sequence is as follows:</span></span>

1. <span data-ttu-id="576ab-113">El usuario emite una consulta o la consulta predeterminada se envía automáticamente al servicio.</span><span class="sxs-lookup"><span data-stu-id="576ab-113">User issues a query, or the default query is automatically sent to your service.</span></span>
1. <span data-ttu-id="576ab-114">El servicio comprueba si el usuario está autenticado inspeccionando el Teams de usuario.</span><span class="sxs-lookup"><span data-stu-id="576ab-114">Your service checks whether the user is authenticated by inspecting the Teams user ID.</span></span>
1. <span data-ttu-id="576ab-115">Si el usuario no está autenticado, envíe una respuesta con `auth` una `openUrl` acción sugerida, incluida la dirección URL de autenticación.</span><span class="sxs-lookup"><span data-stu-id="576ab-115">If the user is not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
1. <span data-ttu-id="576ab-116">El Microsoft Teams inicia un cuadro de diálogo que hospeda la página web mediante la dirección URL de autenticación determinada.</span><span class="sxs-lookup"><span data-stu-id="576ab-116">The Microsoft Teams client launches a dialog box hosting your webpage using the given authentication URL.</span></span>
1. <span data-ttu-id="576ab-117">Después de que el usuario inicia sesión, debe cerrar la ventana y enviar **un** código de autenticación al Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="576ab-117">After the user signs in, you should close your window and send an **authentication code** to the Teams client.</span></span>
1. <span data-ttu-id="576ab-118">A continuación, Teams cliente reedición de la consulta al servicio, que incluye el código de autenticación pasado en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="576ab-118">The Teams client then reissues the query to your service, which includes the authentication code passed in Step 5.</span></span>

<span data-ttu-id="576ab-119">El servicio debe comprobar que el código de autenticación recibido en el paso 6 coincide con el del paso 5.</span><span class="sxs-lookup"><span data-stu-id="576ab-119">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="576ab-120">Esto garantiza que un usuario malintencionado no intente suplantar o poner en peligro el flujo de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="576ab-120">This ensures that a malicious user does not try to spoof or compromise the sign in flow.</span></span> <span data-ttu-id="576ab-121">Esto "cierra el bucle" para finalizar la secuencia de autenticación segura.</span><span class="sxs-lookup"><span data-stu-id="576ab-121">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="576ab-122">Responder con una acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="576ab-122">Respond with a sign-in action</span></span>

<span data-ttu-id="576ab-123">Para solicitar a un usuario no autenticado que inicie sesión, responda con una acción sugerida de tipo `openUrl` que incluya la dirección URL de autenticación.</span><span class="sxs-lookup"><span data-stu-id="576ab-123">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="576ab-124">Ejemplo de respuesta para una acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="576ab-124">Response example for a sign-in action</span></span>

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> <span data-ttu-id="576ab-125">Para que la experiencia de inicio de sesión se hospeda en una ventana emergente de Teams, la parte de dominio de la dirección URL debe estar en la lista de dominios válidos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="576ab-125">For the sign in experience to be hosted in a Teams pop-up window, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="576ab-126">Para obtener más información, [vea validDomains](~/resources/schema/manifest-schema.md#validdomains) en el esquema de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="576ab-126">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="576ab-127">Iniciar el flujo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="576ab-127">Start the sign in flow</span></span>

<span data-ttu-id="576ab-128">La experiencia de inicio de sesión debe responder y caber dentro de una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="576ab-128">Your sign in experience must be responsive and fit within a pop-up window.</span></span> <span data-ttu-id="576ab-129">Debe integrarse con el SDK [Microsoft Teams cliente de JavaScript](/javascript/api/overview/msteams-client), que usa el paso de mensajes.</span><span class="sxs-lookup"><span data-stu-id="576ab-129">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="576ab-130">Al igual que con otras experiencias incrustadas que se ejecutan Microsoft Teams, el código dentro de la ventana debe llamar `microsoftTeams.initialize()` primero.</span><span class="sxs-lookup"><span data-stu-id="576ab-130">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="576ab-131">Si el código realiza un flujo de OAuth, puede pasar el identificador de usuario de Teams en la ventana, que luego lo pasa a la dirección URL de inicio de sesión de OAuth.</span><span class="sxs-lookup"><span data-stu-id="576ab-131">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then passes it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="576ab-132">Completar el flujo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="576ab-132">Complete the sign in flow</span></span>

<span data-ttu-id="576ab-133">Cuando la solicitud de inicio de sesión se completa y vuelve a redirigir a la página, debe realizar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="576ab-133">When the sign in request completes and redirects back to your page, it must perform the following steps:</span></span>

1. <span data-ttu-id="576ab-134">Generar un código de seguridad.</span><span class="sxs-lookup"><span data-stu-id="576ab-134">Generate a security code.</span></span> <span data-ttu-id="576ab-135">Este es un número aleatorio.</span><span class="sxs-lookup"><span data-stu-id="576ab-135">This is a random number.</span></span> <span data-ttu-id="576ab-136">Debe almacenar en caché este código en el servicio, junto con las credenciales obtenidas a través del flujo de inicio de sesión, como tokens de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="576ab-136">You must cache this code on your service, along with the credentials obtained through the sign in flow, such as OAuth 2.0 tokens.</span></span>
1. <span data-ttu-id="576ab-137">Llama `microsoftTeams.authentication.notifySuccess` y pasa el código de seguridad.</span><span class="sxs-lookup"><span data-stu-id="576ab-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="576ab-138">En este momento, la ventana se cierra y el control se pasa al Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="576ab-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="576ab-139">El cliente ahora reedita la consulta de usuario original, junto con el código de seguridad de la `state` propiedad.</span><span class="sxs-lookup"><span data-stu-id="576ab-139">The client now reissues the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="576ab-140">El código puede usar el código de seguridad para buscar las credenciales almacenadas anteriormente para completar la secuencia de autenticación y, a continuación, completar la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="576ab-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="576ab-141">Ejemplo de solicitud ree emitida</span><span class="sxs-lookup"><span data-stu-id="576ab-141">Reissued request example</span></span>

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="code-sample"></a><span data-ttu-id="576ab-142">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="576ab-142">Code sample</span></span>
|<span data-ttu-id="576ab-143">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="576ab-143">**Sample name**</span></span> | <span data-ttu-id="576ab-144">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="576ab-144">**Description**</span></span> |<span data-ttu-id="576ab-145">**.NET**</span><span class="sxs-lookup"><span data-stu-id="576ab-145">**.NET**</span></span> | <span data-ttu-id="576ab-146">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="576ab-146">**Node.js**</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="576ab-147">Extensiones de mensajería: autenticación y configuración</span><span class="sxs-lookup"><span data-stu-id="576ab-147">Messaging extensions - auth and config</span></span> | <span data-ttu-id="576ab-148">Una extensión de mensajería que tiene una página de configuración, acepta solicitudes de búsqueda y devuelve resultados después de que el usuario haya iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="576ab-148">A Messaging Extension that has a configuration page, accepts search requests, and returns results after the user has signed in.</span></span> |[<span data-ttu-id="576ab-149">View</span><span class="sxs-lookup"><span data-stu-id="576ab-149">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[<span data-ttu-id="576ab-150">View</span><span class="sxs-lookup"><span data-stu-id="576ab-150">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
