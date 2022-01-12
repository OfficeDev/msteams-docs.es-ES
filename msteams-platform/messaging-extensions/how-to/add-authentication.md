---
title: Agregar autenticación a la extensión de mensajería
author: surbhigupta
description: Obtenga información sobre cómo agregar autenticación a una extensión de mensajería mediante ejemplos de código y ejemplo
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5c990bd46f145d34616b20e25dc6a0f776f022f9
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768450"
---
# <a name="add-authentication-to-your-messaging-extension"></a>Agregar autenticación a la extensión de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>Identificar al usuario

Cada solicitud a los servicios incluye el identificador de usuario, el nombre para mostrar del usuario y Azure Active Directory de objeto.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Los valores y están garantizados para el usuario `id` Teams `aadObjectId` autenticado. Se usan como claves para buscar las credenciales o cualquier estado almacenado en caché en el servicio. Además, cada solicitud contiene el Azure Active Directory de inquilino, que se usa para identificar la organización del usuario. Si procede, la solicitud también contiene el identificador de equipo y el identificador de canal desde el que se originó la solicitud.

## <a name="authentication"></a>Autenticación

Si el servicio requiere autenticación de usuario, los usuarios deben iniciar sesión antes de usar la extensión de mensajería. Los pasos de autenticación son similares a los de un bot o pestaña. La secuencia es la siguiente:

1. El usuario emite una consulta o la consulta predeterminada se envía automáticamente al servicio.
1. El servicio comprueba si el usuario está autenticado inspeccionando el Teams de usuario.
1. Si el usuario no está autenticado, envíe una respuesta con una `auth` `openUrl` acción sugerida, incluida la dirección URL de autenticación.
1. El Microsoft Teams inicia un cuadro de diálogo que hospeda la página web mediante la dirección URL de autenticación determinada.
1. Después de que el usuario inicia sesión, debe cerrar la ventana y enviar **un** código de autenticación al Teams cliente.
1. A continuación, Teams cliente reedición de la consulta al servicio, que incluye el código de autenticación pasado en el paso 5.

El servicio debe comprobar que el código de autenticación recibido en el paso 6 coincide con el del paso 5. Esto garantiza que un usuario malintencionado no intente suplantar o poner en peligro el flujo de inicio de sesión. Esto "cierra el bucle" para finalizar la secuencia de autenticación segura.

### <a name="respond-with-a-sign-in-action"></a>Responder con una acción de inicio de sesión

Para solicitar a un usuario no autenticado que inicie sesión, responda con una acción sugerida de tipo `openUrl` que incluya la dirección URL de autenticación.

#### <a name="response-example-for-a-sign-in-action"></a>Ejemplo de respuesta para una acción de inicio de sesión

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
> * Para que la experiencia de inicio de sesión se hospeda en una ventana emergente de Teams, la parte de dominio de la dirección URL debe estar en la lista de dominios válidos de la aplicación. Para obtener más información, [vea validDomains](~/resources/schema/manifest-schema.md#validdomains) en el esquema de manifiesto.
> * El tamaño de la ventana emergente de autenticación se puede definir mediante la inclusión de parámetros de cadena de consulta de ancho y alto, `Value = $"{_siteUrl}/searchSettings.html?settings={escapedSettings}",` .

### <a name="start-the-sign-in-flow"></a>Iniciar el flujo de inicio de sesión

La experiencia de inicio de sesión debe responder y caber dentro de una ventana emergente. Debe integrarse con el SDK [Microsoft Teams cliente de JavaScript](/javascript/api/overview/msteams-client), que usa el paso de mensajes.

Al igual que con otras experiencias incrustadas que se ejecutan Microsoft Teams, el código dentro de la ventana debe llamar `microsoftTeams.initialize()` primero. Si el código realiza un flujo de OAuth, puede pasar el identificador de usuario de Teams en la ventana, que luego lo pasa a la dirección URL de inicio de sesión de OAuth.

### <a name="complete-the-sign-in-flow"></a>Completar el flujo de inicio de sesión

Cuando la solicitud de inicio de sesión se completa y vuelve a redirigir a la página, debe realizar los siguientes pasos:

1. Generar un código de seguridad, un número aleatorio. Debe almacenar en caché este código en el servicio, junto con las credenciales obtenidas a través del flujo de inicio de sesión, como tokens de OAuth 2.0.
1. Llama `microsoftTeams.authentication.notifySuccess` y pasa el código de seguridad.

En este momento, la ventana se cierra y el control se pasa al Teams cliente. El cliente ahora reedita la consulta de usuario original, junto con el código de seguridad de la `state` propiedad. El código puede usar el código de seguridad para buscar las credenciales almacenadas anteriormente para completar la secuencia de autenticación y, a continuación, completar la solicitud de usuario.

#### <a name="reissued-request-example"></a>Ejemplo de solicitud ree emitida

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

## <a name="code-sample"></a>Ejemplo de código
|**Ejemplo de nombre** | **Descripción** |**.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Extensiones de mensajería: autenticación y configuración | Una extensión de mensajería que tiene una página de configuración, acepta solicitudes de búsqueda y devuelve resultados después de que el usuario haya iniciado sesión. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[Ver](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

## <a name="see-also"></a>Consulte también

[Compatibilidad con inicio de sesión único (SSO) para extensiones de mensajería](~/messaging-extensions/how-to/enable-sso-auth-me.md)
