---
title: Agregar autenticación a la extensión de mensajería
author: clearab
description: Cómo agregar autenticación a una extensión de mensajería
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 4ebe65af06240d13ceb99fe3b7640ab402d716c5
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911873"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="ca5d3-103">Agregar autenticación a la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="ca5d3-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="ca5d3-104">Identificar al usuario</span><span class="sxs-lookup"><span data-stu-id="ca5d3-104">Identify the user</span></span>

<span data-ttu-id="ca5d3-105">Cada solicitud a los servicios incluye el identificador ofuscado del usuario que realizó la solicitud, así como el nombre para mostrar del usuario y el identificador de objeto de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="ca5d3-106">Se `id` garantiza que los valores y son los del usuario `aadObjectId` autenticado de Teams.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="ca5d3-107">Se pueden usar como claves para buscar credenciales o cualquier estado almacenado en caché en el servicio.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="ca5d3-108">Además, cada solicitud contiene el identificador de inquilino de Azure Active Directory del usuario, que se puede usar para identificar la organización del usuario.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="ca5d3-109">Si procede, la solicitud también contiene los IDs de equipo y canal desde los que se originó la solicitud.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="ca5d3-110">Autenticación</span><span class="sxs-lookup"><span data-stu-id="ca5d3-110">Authentication</span></span>

<span data-ttu-id="ca5d3-111">Si el servicio requiere autenticación de usuario, debe iniciar sesión en el usuario para poder usar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="ca5d3-112">Si ha escrito un bot o una pestaña que inicia sesión en el usuario, esta sección debe ser familiar.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="ca5d3-113">La secuencia es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca5d3-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="ca5d3-114">El usuario emite una consulta o la consulta predeterminada se envía automáticamente al servicio.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="ca5d3-115">El servicio comprueba si el usuario se ha autenticado primero inspeccionando el identificador de usuario de Teams.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="ca5d3-116">Si el usuario no se ha autenticado, envíe una respuesta con `auth` una `openUrl` acción sugerida, incluida la dirección URL de autenticación.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="ca5d3-117">El cliente de Microsoft Teams inicia una ventana emergente que hospeda su página web con la dirección URL de autenticación especificada.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="ca5d3-118">Después de que el usuario inicia sesión, debe cerrar la ventana y enviar un "código de autenticación" al cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="ca5d3-119">A continuación, el cliente de Teams devuelve la consulta al servicio, que incluye el código de autenticación pasado en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="ca5d3-120">El servicio debe comprobar que el código de autenticación recibido en el paso 6 coincide con el del paso 5.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="ca5d3-121">Esto garantiza que un usuario malintencionado no intente suplantar o poner en peligro el flujo de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="ca5d3-122">Esto "cierra el bucle" para finalizar la secuencia de autenticación segura.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="ca5d3-123">Responder con una acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ca5d3-123">Respond with a sign-in action</span></span>

<span data-ttu-id="ca5d3-124">Para solicitar a un usuario no autenticado que inicie sesión, responda con una acción sugerida de tipo `openUrl` que incluya la dirección URL de autenticación.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="ca5d3-125">Ejemplo de respuesta para una acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ca5d3-125">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="ca5d3-126">Para que la experiencia de inicio de sesión se hospeda en una ventana emergente de Teams, la parte de dominio de la dirección URL debe estar en la lista de dominios válidos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="ca5d3-127">(Vea [validDomains en](~/resources/schema/manifest-schema.md#validdomains) el esquema del manifiesto).</span><span class="sxs-lookup"><span data-stu-id="ca5d3-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="ca5d3-128">Iniciar el flujo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ca5d3-128">Start the sign-in flow</span></span>

<span data-ttu-id="ca5d3-129">La experiencia de inicio de sesión debe ser dinámica y cabe dentro de una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="ca5d3-130">Debe integrarse con el SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client)de Microsoft Teams, que usa el paso de mensajes.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="ca5d3-131">Al igual que con otras experiencias incrustadas que se ejecutan dentro de Microsoft Teams, el código dentro de la ventana debe llamar `microsoftTeams.initialize()` primero.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="ca5d3-132">Si el código realiza un flujo de OAuth, puede pasar el identificador de usuario de Teams a la ventana, que luego puede pasarlo a la dirección URL de inicio de sesión de OAuth.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="ca5d3-133">Completar el flujo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ca5d3-133">Complete the sign-in flow</span></span>

<span data-ttu-id="ca5d3-134">Cuando la solicitud de inicio de sesión se completa y vuelve a redirigir a la página, debe realizar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ca5d3-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="ca5d3-135">Generar un código de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-135">Generate a security code.</span></span> <span data-ttu-id="ca5d3-136">(Puede ser un número aleatorio). Debe almacenar en caché este código en el servicio, junto con las credenciales obtenidas a través del flujo de inicio de sesión (como tokens de OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="ca5d3-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="ca5d3-137">Llama `microsoftTeams.authentication.notifySuccess` y pasa el código de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="ca5d3-138">En este punto, la ventana se cierra y el control se pasa al cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="ca5d3-139">El cliente ahora puede volver a emitir la consulta de usuario original, junto con el código de seguridad de la `state` propiedad.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="ca5d3-140">El código puede usar el código de seguridad para buscar las credenciales almacenadas anteriormente para completar la secuencia de autenticación y, a continuación, completar la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="ca5d3-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="ca5d3-141">Ejemplo de solicitud ree emitida</span><span class="sxs-lookup"><span data-stu-id="ca5d3-141">Reissued request example</span></span>

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

## <a name="samples"></a><span data-ttu-id="ca5d3-142">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ca5d3-142">Samples</span></span>
<span data-ttu-id="ca5d3-143">Para obtener código de ejemplo que muestra el proceso de autenticación de extensiones de mensajería, vea:</span><span class="sxs-lookup"><span data-stu-id="ca5d3-143">For sample code showing the messaging-extensions authentication process, see:</span></span>

[<span data-ttu-id="ca5d3-144">Ejemplo de autenticación de extensiones de mensajería de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ca5d3-144">Microsoft Teams messaging-extensions authentication sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)

 
