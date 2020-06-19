---
title: Buscar con extensiones de mensajería
description: Describe cómo desarrollar extensiones de mensajería basadas en búsquedas
keywords: búsqueda de extensiones de mensajería de Team Extensions
ms.date: 07/20/2019
ms.openlocfilehash: b791e7cc8f9a311d0610573f2fa3659578c29c7d
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801547"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="f85b6-104">Buscar con extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="f85b6-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="f85b6-105">Las extensiones de mensajería basadas en búsquedas le permiten consultar su servicio y enviar la información en forma de una tarjeta, directamente en su mensaje.</span><span class="sxs-lookup"><span data-stu-id="f85b6-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message</span></span>

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="f85b6-107">En las secciones siguientes se describe cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="f85b6-107">The following sections describe how to do this.</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="f85b6-108">Extensiones de mensajes de tipo de búsqueda</span><span class="sxs-lookup"><span data-stu-id="f85b6-108">Search type message extensions</span></span>

<span data-ttu-id="f85b6-109">Para la extensión de mensajería basada en búsquedas establezca el `type` parámetro en `query` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="f85b6-110">A continuación se muestra un ejemplo de un manifiesto con un único comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f85b6-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="f85b6-111">Una sola extensión de mensajería puede tener hasta 10 comandos diferentes asociados a ella.</span><span class="sxs-lookup"><span data-stu-id="f85b6-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="f85b6-112">Esto puede incluir varios comandos de búsqueda y varios basados en acciones.</span><span class="sxs-lookup"><span data-stu-id="f85b6-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="f85b6-113">Ejemplo de manifiesto de aplicación completo</span><span class="sxs-lookup"><span data-stu-id="f85b6-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a><span data-ttu-id="f85b6-114">Prueba mediante carga</span><span class="sxs-lookup"><span data-stu-id="f85b6-114">Test via uploading</span></span>

<span data-ttu-id="f85b6-115">Puede probar la extensión de mensajería cargando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f85b6-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="f85b6-116">Para abrir la extensión de mensajería, navegue a cualquiera de sus chats o canales.</span><span class="sxs-lookup"><span data-stu-id="f85b6-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="f85b6-117">Elija el botón **más opciones** (**&#8943;**) en el cuadro de redacción y elija su extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f85b6-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="f85b6-118">Agregar controladores de eventos</span><span class="sxs-lookup"><span data-stu-id="f85b6-118">Add event handlers</span></span>

<span data-ttu-id="f85b6-119">La mayor parte de su trabajo implica el `onQuery` evento, que controla todas las interacciones en la ventana de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f85b6-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="f85b6-120">Si establece en `canUpdateConfiguration` `true` en el manifiesto, habilita el elemento de menú **configuración** para la extensión de mensajería y también debe controlar `onQuerySettingsUrl` y `onSettingsUpdate` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="f85b6-121">Controlar eventos de consulta</span><span class="sxs-lookup"><span data-stu-id="f85b6-121">Handle onQuery events</span></span>

<span data-ttu-id="f85b6-122">Una extensión de mensajería recibe un `onQuery` evento cuando ocurre algo en la ventana de la extensión de mensajería o se envía a la ventana.</span><span class="sxs-lookup"><span data-stu-id="f85b6-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="f85b6-123">Si su extensión de mensajería usa una página de configuración, el controlador para `onQuery` debe comprobar primero si hay información de configuración almacenada; si la extensión de mensajería no está configurada, devuelva una `config` respuesta con un vínculo a la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="f85b6-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="f85b6-124">Tenga en cuenta que la respuesta de la página de configuración también se controla mediante `onQuery` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="f85b6-125">(La única excepción es cuando el controlador llama a la página de configuración de `onQuerySettingsUrl` ; Consulte la sección siguiente).</span><span class="sxs-lookup"><span data-stu-id="f85b6-125">(The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section.)</span></span>

<span data-ttu-id="f85b6-126">Si su extensión de mensajería requiere autenticación, Compruebe la información de estado del usuario; Si el usuario no ha iniciado sesión, siga las instrucciones de la sección [autenticación](#authentication) más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="f85b6-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="f85b6-127">A continuación, compruebe si `initialRun` está establecido; si es así, realice las acciones adecuadas, como proporciona instrucciones o una lista de respuestas.</span><span class="sxs-lookup"><span data-stu-id="f85b6-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="f85b6-128">El resto del controlador para `onQuery` solicita información al usuario, muestra una lista de tarjetas de vista previa y devuelve la tarjeta seleccionada por el usuario.</span><span class="sxs-lookup"><span data-stu-id="f85b6-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="f85b6-129">Controlar eventos onQuerySettingsUrl y onSettingsUpdate</span><span class="sxs-lookup"><span data-stu-id="f85b6-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="f85b6-130">Los `onQuerySettingsUrl` `onSettingsUpdate` eventos y funcionan de forma conjunta para habilitar el elemento de menú **configuración** .</span><span class="sxs-lookup"><span data-stu-id="f85b6-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

![Capturas de pantallas de ubicaciones del elemento de menú configuración](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="f85b6-132">El controlador para `onQuerySettingsUrl` devuelve la dirección URL de la página de configuración; una vez que se cierra la página de configuración, el controlador para `onSettingsUpdate` acepta y guarda el estado devuelto.</span><span class="sxs-lookup"><span data-stu-id="f85b6-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="f85b6-133">(Este es el caso en el que `onQuery` *no* recibe la respuesta de la página de configuración.)</span><span class="sxs-lookup"><span data-stu-id="f85b6-133">(This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.)</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="f85b6-134">Recibir y responder a consultas</span><span class="sxs-lookup"><span data-stu-id="f85b6-134">Receive and respond to queries</span></span>

<span data-ttu-id="f85b6-135">Cada solicitud a su extensión de mensajería se realiza a través de un `Activity` objeto que se publica en la dirección URL de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="f85b6-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="f85b6-136">La solicitud contiene información sobre el comando de usuario, como los valores ID y Parameter.</span><span class="sxs-lookup"><span data-stu-id="f85b6-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="f85b6-137">La solicitud también proporciona metadatos sobre el contexto en el que se ha invocado la extensión, incluidos el identificador de usuario y de inquilino, junto con el identificador de chat o los identificadores de canal y de equipo.</span><span class="sxs-lookup"><span data-stu-id="f85b6-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="f85b6-138">Recibir solicitudes de usuario</span><span class="sxs-lookup"><span data-stu-id="f85b6-138">Receive user requests</span></span>

<span data-ttu-id="f85b6-139">Cuando un usuario realiza una consulta, Microsoft Teams envía al servicio un objeto de .NET Framework estándar `Activity` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="f85b6-140">El servicio debe realizar su lógica para un `Activity` que tenga `type` establecido en `invoke` y `name` establecido en un tipo admitido `composeExtension` , como se muestra en la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="f85b6-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="f85b6-141">Además de las propiedades de actividad de bot estándar, la carga contiene los siguientes metadatos de solicitud:</span><span class="sxs-lookup"><span data-stu-id="f85b6-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="f85b6-142">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="f85b6-142">Property name</span></span>|<span data-ttu-id="f85b6-143">Objetivo</span><span class="sxs-lookup"><span data-stu-id="f85b6-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="f85b6-144">Tipo de solicitud; debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="f85b6-145">Tipo de comando que se emite para el servicio.</span><span class="sxs-lookup"><span data-stu-id="f85b6-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="f85b6-146">Actualmente se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f85b6-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="f85b6-147">IDENTIFICADOR del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f85b6-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="f85b6-148">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f85b6-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="f85b6-149">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f85b6-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="f85b6-150">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f85b6-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="f85b6-151">IDENTIFICADOR de canal (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="f85b6-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="f85b6-152">IDENTIFICADOR del equipo (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="f85b6-152">Team ID (if the request was made in a channel).</span></span> |
|`clientInfo`|<span data-ttu-id="f85b6-153">Metadatos opcionales sobre el software de cliente que se usa para enviar un mensaje de un usuario.</span><span class="sxs-lookup"><span data-stu-id="f85b6-153">Optional metadata about the client software used to send a user's message.</span></span> <span data-ttu-id="f85b6-154">La entidad puede contener dos propiedades:</span><span class="sxs-lookup"><span data-stu-id="f85b6-154">The entity can contain two properties:</span></span><br><span data-ttu-id="f85b6-155">El `country` campo contiene la ubicación detectada del usuario.</span><span class="sxs-lookup"><span data-stu-id="f85b6-155">The `country` field contains the user's detected location.</span></span><br><span data-ttu-id="f85b6-156">El `platform` campo describe la plataforma de cliente de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f85b6-156">The `platform` field describes the messaging client platform.</span></span> <br><span data-ttu-id="f85b6-157">Para obtener más información, *vea* [tipos de entidades que no son IRI — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span><span class="sxs-lookup"><span data-stu-id="f85b6-157">For additional information, please *see* [Non-IRI entity types — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>|

<span data-ttu-id="f85b6-158">Los propios parámetros de la solicitud se encuentran en el objeto de valor, que incluye las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="f85b6-158">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="f85b6-159">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="f85b6-159">Property name</span></span> | <span data-ttu-id="f85b6-160">Objetivo</span><span class="sxs-lookup"><span data-stu-id="f85b6-160">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="f85b6-161">Nombre del comando invocado por el usuario, que coincide con uno de los comandos declarados en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f85b6-161">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="f85b6-162">Matriz de parámetros.</span><span class="sxs-lookup"><span data-stu-id="f85b6-162">Array of parameters.</span></span> <span data-ttu-id="f85b6-163">Cada objeto Parameter contiene el nombre del parámetro, junto con el valor del parámetro proporcionado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="f85b6-163">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="f85b6-164">Parámetros de paginación:</span><span class="sxs-lookup"><span data-stu-id="f85b6-164">Pagination parameters:</span></span> <br><span data-ttu-id="f85b6-165">`skip`: recuento de omitidos para esta consulta</span><span class="sxs-lookup"><span data-stu-id="f85b6-165">`skip`: skip count for this query</span></span> <br><span data-ttu-id="f85b6-166">`count`: número de elementos que se devolverá</span><span class="sxs-lookup"><span data-stu-id="f85b6-166">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="f85b6-167">Ejemplo de solicitud</span><span class="sxs-lookup"><span data-stu-id="f85b6-167">Request example</span></span>

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="f85b6-168">Recibir solicitudes de vínculos insertados en el cuadro de mensaje de redacción</span><span class="sxs-lookup"><span data-stu-id="f85b6-168">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="f85b6-169">Como alternativa (o adicional), a la búsqueda en el servicio externo, puede usar una dirección URL insertada en el cuadro de mensaje de redacción para consultar su servicio y devolver una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="f85b6-169">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="f85b6-170">En la captura de pantalla siguiente, un usuario ha pegado en una dirección URL de un elemento de trabajo en Azure DevOps que la extensión de mensajería se ha resuelto en una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="f85b6-170">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Ejemplo de vínculo unfurling](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="f85b6-172">Para habilitar la extensión de mensajería para que interactúe con los vínculos de esta forma, primero tendrá que agregar la `messageHandlers` matriz al manifiesto de la aplicación, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f85b6-172">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

<span data-ttu-id="f85b6-173">Una vez que haya agregado el dominio para escuchar en el manifiesto de la aplicación, deberá cambiar el código de bot para [responder](#respond-to-user-requests) a la siguiente solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="f85b6-173">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="f85b6-174">Si la aplicación devuelve varios elementos solo se usará el primero.</span><span class="sxs-lookup"><span data-stu-id="f85b6-174">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="f85b6-175">Responder a solicitudes de usuario</span><span class="sxs-lookup"><span data-stu-id="f85b6-175">Respond to user requests</span></span>

<span data-ttu-id="f85b6-176">Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica a su servicio.</span><span class="sxs-lookup"><span data-stu-id="f85b6-176">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="f85b6-177">En ese momento, el código tiene 5 segundos para proporcionar una respuesta HTTP a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f85b6-177">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="f85b6-178">Durante este tiempo, el servicio puede realizar búsquedas adicionales o cualquier otra lógica empresarial necesaria para atender la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f85b6-178">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="f85b6-179">El servicio debe responder con los resultados que coincidan con la consulta de usuario.</span><span class="sxs-lookup"><span data-stu-id="f85b6-179">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="f85b6-180">La respuesta debe indicar un código de Estado HTTP de `200 OK` y un objeto Application/JSON válido con el siguiente cuerpo:</span><span class="sxs-lookup"><span data-stu-id="f85b6-180">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="f85b6-181">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="f85b6-181">Property name</span></span>|<span data-ttu-id="f85b6-182">Objetivo</span><span class="sxs-lookup"><span data-stu-id="f85b6-182">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="f85b6-183">Sobre de respuesta de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="f85b6-183">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="f85b6-184">Tipo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="f85b6-184">Type of response.</span></span> <span data-ttu-id="f85b6-185">Se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f85b6-185">The following types are supported:</span></span> <br><span data-ttu-id="f85b6-186">`result`: muestra una lista de los resultados de la búsqueda</span><span class="sxs-lookup"><span data-stu-id="f85b6-186">`result`: displays a list of search results</span></span> <br><span data-ttu-id="f85b6-187">`auth`: pide al usuario que se autentique</span><span class="sxs-lookup"><span data-stu-id="f85b6-187">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="f85b6-188">`config`: pide al usuario que configure la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f85b6-188">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="f85b6-189">`message`: muestra un mensaje de texto sin formato</span><span class="sxs-lookup"><span data-stu-id="f85b6-189">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="f85b6-190">Especifica el diseño de los datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="f85b6-190">Specifies the layout of the attachments.</span></span> <span data-ttu-id="f85b6-191">Se usa para las respuestas de tipo `result` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-191">Used for responses of type `result`.</span></span> <br><span data-ttu-id="f85b6-192">Actualmente se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f85b6-192">Currently the following types are supported:</span></span> <br><span data-ttu-id="f85b6-193">`list`: una lista de objetos Card que contiene miniaturas, títulos y campos de texto</span><span class="sxs-lookup"><span data-stu-id="f85b6-193">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="f85b6-194">`grid`: una cuadrícula de imágenes en miniatura</span><span class="sxs-lookup"><span data-stu-id="f85b6-194">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="f85b6-195">Matriz de objetos Attachment válidos.</span><span class="sxs-lookup"><span data-stu-id="f85b6-195">Array of valid attachment objects.</span></span> <span data-ttu-id="f85b6-196">Se usa para las respuestas de tipo `result` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-196">Used for responses of type `result`.</span></span> <br><span data-ttu-id="f85b6-197">Actualmente se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f85b6-197">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="f85b6-198">Acciones sugeridas.</span><span class="sxs-lookup"><span data-stu-id="f85b6-198">Suggested actions.</span></span> <span data-ttu-id="f85b6-199">Se usa para las respuestas de tipo `auth` o `config` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-199">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="f85b6-200">Mensaje que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="f85b6-200">Message to display.</span></span> <span data-ttu-id="f85b6-201">Se usa para las respuestas de tipo `message` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-201">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="f85b6-202">Tipos y vistas previas de las tarjetas de respuesta</span><span class="sxs-lookup"><span data-stu-id="f85b6-202">Response card types and previews</span></span>

<span data-ttu-id="f85b6-203">Se admiten los siguientes tipos de datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="f85b6-203">We support the following attachment types:</span></span>

* [<span data-ttu-id="f85b6-204">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="f85b6-204">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="f85b6-205">Tarjeta Hero</span><span class="sxs-lookup"><span data-stu-id="f85b6-205">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="f85b6-206">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="f85b6-206">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="f85b6-207">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="f85b6-207">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="f85b6-208">Consulte las [tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general.</span><span class="sxs-lookup"><span data-stu-id="f85b6-208">See [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="f85b6-209">Para obtener información sobre cómo usar los tipos de tarjetas en miniatura y Heroes, consulte [Add Cards and Card Actions](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="f85b6-209">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="f85b6-210">Para obtener documentación adicional sobre la tarjeta de conector de Office 365, consulte [using office 365 Connector Cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="f85b6-210">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="f85b6-211">La lista de resultados se muestra en la interfaz de usuario de Microsoft Teams con una vista previa de cada elemento.</span><span class="sxs-lookup"><span data-stu-id="f85b6-211">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="f85b6-212">La vista previa se genera de una de estas dos maneras:</span><span class="sxs-lookup"><span data-stu-id="f85b6-212">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="f85b6-213">Uso de la `preview` propiedad en el `attachment` objeto.</span><span class="sxs-lookup"><span data-stu-id="f85b6-213">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="f85b6-214">El `preview` archivo adjunto solo puede ser un héroe o una tarjeta de miniaturas.</span><span class="sxs-lookup"><span data-stu-id="f85b6-214">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="f85b6-215">Se extraen de `title` las `text` propiedades Basic, y `image` de los datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="f85b6-215">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="f85b6-216">Solo se usan si la `preview` propiedad no está establecida y estas propiedades están disponibles.</span><span class="sxs-lookup"><span data-stu-id="f85b6-216">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="f85b6-217">Puede mostrar una vista previa de una tarjeta de conector de Office 365 adaptable en la lista de resultados simplemente estableciendo su propiedad Preview; Esto no es necesario si los resultados ya son un héroe o tarjetas en miniatura.</span><span class="sxs-lookup"><span data-stu-id="f85b6-217">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="f85b6-218">Si usa la vista previa de datos adjuntos, debe ser un héroe o una tarjeta en miniatura.</span><span class="sxs-lookup"><span data-stu-id="f85b6-218">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="f85b6-219">Si no se especifica ninguna propiedad de vista previa, se producirá un error en la vista previa de la tarjeta y no se mostrará nada.</span><span class="sxs-lookup"><span data-stu-id="f85b6-219">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="f85b6-220">Ejemplo de respuesta</span><span class="sxs-lookup"><span data-stu-id="f85b6-220">Response example</span></span>

<span data-ttu-id="f85b6-221">En este ejemplo se muestra una respuesta con dos resultados, mezclando distintos formatos de tarjeta: conector de Office 365 y adaptable.</span><span class="sxs-lookup"><span data-stu-id="f85b6-221">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="f85b6-222">Aunque es probable que desee ceñirse a un formato de tarjeta en la respuesta, muestra cómo la `preview` propiedad de cada elemento de la `attachments` colección debe definir explícitamente una vista previa en el formato de héroe o miniatura, como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f85b6-222">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a><span data-ttu-id="f85b6-223">Consulta predeterminada</span><span class="sxs-lookup"><span data-stu-id="f85b6-223">Default query</span></span>

<span data-ttu-id="f85b6-224">Si establece en `initialRun` `true` en el manifiesto, Microsoft Teams emite una consulta "predeterminada" cuando el usuario abre por primera vez la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f85b6-224">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="f85b6-225">El servicio puede responder a esta consulta con un conjunto de resultados rellenados previamente.</span><span class="sxs-lookup"><span data-stu-id="f85b6-225">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="f85b6-226">Esto puede ser útil para mostrar, por ejemplo, elementos vistos recientemente, favoritos o cualquier otra información que no dependa de los datos proporcionados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="f85b6-226">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="f85b6-227">La consulta predeterminada tiene la misma estructura que cualquier consulta de usuario normal, excepto con un parámetro `initialRun` cuyo valor de cadena es `true` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-227">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="f85b6-228">Ejemplo de solicitud de una consulta predeterminada</span><span class="sxs-lookup"><span data-stu-id="f85b6-228">Request example for a default query</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a><span data-ttu-id="f85b6-229">Identificar al usuario</span><span class="sxs-lookup"><span data-stu-id="f85b6-229">Identify the user</span></span>

<span data-ttu-id="f85b6-230">Todas las solicitudes a los servicios incluyen el identificador ofuscado del usuario que realizó la solicitud, así como el nombre para mostrar del usuario y el identificador de objeto de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f85b6-230">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="f85b6-231">`id` `aadObjectId` Se garantiza que los valores y son los del usuario de Teams autenticado.</span><span class="sxs-lookup"><span data-stu-id="f85b6-231">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="f85b6-232">Se pueden usar como claves para buscar credenciales o cualquier estado almacenado en la memoria caché del servicio.</span><span class="sxs-lookup"><span data-stu-id="f85b6-232">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="f85b6-233">Además, cada solicitud contiene el identificador de inquilino de Azure Active Directory del usuario, que se puede usar para identificar la organización del usuario.</span><span class="sxs-lookup"><span data-stu-id="f85b6-233">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="f85b6-234">Si procede, la solicitud también contiene los identificadores de equipo y de canal desde los que se originó la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f85b6-234">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="f85b6-235">Autenticación</span><span class="sxs-lookup"><span data-stu-id="f85b6-235">Authentication</span></span>

<span data-ttu-id="f85b6-236">Si su servicio requiere la autenticación del usuario, debe iniciar sesión en el usuario antes de que pueda usar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f85b6-236">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="f85b6-237">Si ha escrito un bot o una pestaña que inicia sesión en el usuario, esta sección debería resultarle familiar.</span><span class="sxs-lookup"><span data-stu-id="f85b6-237">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="f85b6-238">La secuencia es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f85b6-238">The sequence is as follows:</span></span>

1. <span data-ttu-id="f85b6-239">El usuario emite una consulta o se envía automáticamente la consulta predeterminada a su servicio.</span><span class="sxs-lookup"><span data-stu-id="f85b6-239">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="f85b6-240">El servicio comprueba si el usuario se ha autenticado primero mediante la inspección del identificador de usuario de Teams.</span><span class="sxs-lookup"><span data-stu-id="f85b6-240">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="f85b6-241">Si el usuario no se ha autenticado, vuelva a enviar una `auth` respuesta con una `openUrl` acción sugerida que incluya la dirección URL de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f85b6-241">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="f85b6-242">El cliente de Microsoft Teams inicia una ventana emergente que hospeda la página web con la dirección URL de autenticación especificada.</span><span class="sxs-lookup"><span data-stu-id="f85b6-242">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="f85b6-243">Después de que el usuario inicie sesión, debe cerrar la ventana y enviar un "código de autenticación" al cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="f85b6-243">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="f85b6-244">A continuación, el cliente de Microsoft Teams envía la consulta a su servicio, que incluye el código de autenticación pasado en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="f85b6-244">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="f85b6-245">El servicio debe comprobar que el código de autenticación recibido en el paso 6 coincida con el del paso 5.</span><span class="sxs-lookup"><span data-stu-id="f85b6-245">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="f85b6-246">Esto garantiza que un usuario malintencionado no intente imitar ni poner en peligro el flujo de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f85b6-246">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="f85b6-247">De hecho, "cierra el bucle" para finalizar la secuencia de autenticación segura.</span><span class="sxs-lookup"><span data-stu-id="f85b6-247">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="f85b6-248">Responder con una acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="f85b6-248">Respond with a sign-in action</span></span>

<span data-ttu-id="f85b6-249">Para solicitar a un usuario no autenticado que inicie sesión, responda con una acción sugerida de tipo `openUrl` que incluya la dirección URL de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f85b6-249">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="f85b6-250">Ejemplo de respuesta de una acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="f85b6-250">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="f85b6-251">Para que la experiencia de inicio de sesión se hospede en una ventana emergente de Teams, la parte de dominio de la dirección URL debe estar en la lista de dominios válidos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f85b6-251">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="f85b6-252">(Vea [validDomains](~/resources/schema/manifest-schema.md#validdomains) en el esquema del manifiesto).</span><span class="sxs-lookup"><span data-stu-id="f85b6-252">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="f85b6-253">Iniciar el flujo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="f85b6-253">Start the sign-in flow</span></span>

<span data-ttu-id="f85b6-254">La experiencia de inicio de sesión debe ser eficaz y ajustarse en una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="f85b6-254">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="f85b6-255">Debe integrarse con el [SDK cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client), que usa el paso de mensajes.</span><span class="sxs-lookup"><span data-stu-id="f85b6-255">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="f85b6-256">Al igual que con otras experiencias incrustadas que se ejecutan dentro de Microsoft Teams, el código dentro de la ventana debe llamar primero `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="f85b6-256">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="f85b6-257">Si el código realiza un flujo de OAuth, puede pasar el identificador de usuario de Teams a la ventana, que puede pasarla a la dirección URL de inicio de sesión de OAuth.</span><span class="sxs-lookup"><span data-stu-id="f85b6-257">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="f85b6-258">Completar el flujo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="f85b6-258">Complete the sign-in flow</span></span>

<span data-ttu-id="f85b6-259">Cuando la solicitud de inicio de sesión se completa y redirige de nuevo a la página, debe realizar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f85b6-259">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="f85b6-260">Generar un código de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f85b6-260">Generate a security code.</span></span> <span data-ttu-id="f85b6-261">(Puede ser un número aleatorio). Debe almacenar en caché este código en el servicio, junto con las credenciales obtenidas a través del flujo de inicio de sesión (por ejemplo, los tokens 2,0 de OAuth).</span><span class="sxs-lookup"><span data-stu-id="f85b6-261">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="f85b6-262">Llamar `microsoftTeams.authentication.notifySuccess` y pasar el código de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f85b6-262">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="f85b6-263">En este momento, la ventana se cierra y el control se pasa al cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="f85b6-263">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="f85b6-264">El cliente ahora puede volver a emitir la consulta de usuario original, junto con el código de seguridad de la `state` propiedad.</span><span class="sxs-lookup"><span data-stu-id="f85b6-264">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="f85b6-265">El código puede usar el código de seguridad para buscar las credenciales almacenadas anteriormente para completar la secuencia de autenticación y, a continuación, completar la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="f85b6-265">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="f85b6-266">Ejemplo de solicitud reemitiendo</span><span class="sxs-lookup"><span data-stu-id="f85b6-266">Reissued request example</span></span>

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
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
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

## <a name="sdk-support"></a><span data-ttu-id="f85b6-267">Compatibilidad con SDK</span><span class="sxs-lookup"><span data-stu-id="f85b6-267">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="f85b6-268">.NET</span><span class="sxs-lookup"><span data-stu-id="f85b6-268">.NET</span></span>

<span data-ttu-id="f85b6-269">Para recibir y controlar consultas con el SDK de bot Builder para .NET, puede comprobar el `invoke` tipo de acción en la actividad entrante y, a continuación, usar el método auxiliar en el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) para determinar si se trata de una actividad de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f85b6-269">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="f85b6-270">Código de ejemplo en .NET</span><span class="sxs-lookup"><span data-stu-id="f85b6-270">Example code in .NET</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a><span data-ttu-id="f85b6-271">Node.js</span><span class="sxs-lookup"><span data-stu-id="f85b6-271">Node.js</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="f85b6-272">Código de ejemplo en Node.js</span><span class="sxs-lookup"><span data-stu-id="f85b6-272">Example code in Node.js</span></span>

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```
<span data-ttu-id="f85b6-273">*Vea también* [ejemplos del marco de bot](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="f85b6-273">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
