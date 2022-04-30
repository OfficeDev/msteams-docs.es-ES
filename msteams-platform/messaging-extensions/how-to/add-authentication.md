---
title: Agregar autenticación a la extensión de mensaje
author: surbhigupta
description: Aprenda a agregar autenticación a una extensión de mensajería mediante ejemplos de código y muestras
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 36a2aa269bfc43f4c07e97a5c214e3081a38ffeb
ms.sourcegitcommit: 591bab4c7e01ac9099b9a540f149b64e6e31e6e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2022
ms.locfileid: "65135713"
---
# <a name="add-authentication-to-your-message-extension"></a>Agregar autenticación a la extensión de mensaje

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>Identificación del usuario

Cada solicitud a los servicios incluye el identificador de usuario, el nombre para mostrar del usuario y el identificador de objeto de Azure Active Directory.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Los valores `id` y `aadObjectId` están garantizados para el usuario autenticado de Teams. Se usan como claves para buscar las credenciales o cualquier estado almacenado en caché en el servicio. Además, cada solicitud contiene el identificador del espacio empresarial de Azure Active Directory, el cual se usa para identificar a la organización del usuario. Si procede, la solicitud también contiene el identificador del equipo y el identificador del canal desde el cual se origina la solicitud.

## <a name="authentication"></a>Autenticación

Si el servicio requiere la autenticación del usuario, los usuarios deben iniciar sesión antes de usar la extensión de mensaje. Los pasos de autenticación son similares a los de un bot o una pestaña. La secuencia es la siguiente:

1. El usuario emite una consulta o se envía la consulta predeterminada automáticamente al servicio.
1. El servicio comprueba si el usuario fue autenticado al inspeccionar el identificador de usuario de Teams.
1. Si el usuario no está autenticado, envíe una respuesta `auth` con una acción sugerida `openUrl` que incluya la dirección URL de autenticación.
1. El cliente de Microsoft Teams inicia un cuadro de diálogo que hospeda la página web mediante la dirección URL de autenticación especificada.
1. Después de que el usuario inicie sesión, debe cerrar la ventana y enviar un **código de autenticación** al cliente de Teams.
1. A continuación, el cliente de Teams vuelve a emitir la consulta al servicio, lo que incluye el código de autenticación aprobado en el paso 5.

El servicio debe comprobar que el código de autenticación recibido en el paso 6 coincida con el del paso 5. Esto garantiza que ningún usuario malintencionado intente suplantar o poner en peligro el flujo de inicio de sesión. Así se “cierra el bucle” de forma eficaz para finalizar la secuencia de autenticación segura.

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
>
> * Para que la experiencia de inicio de sesión se hospede en una ventana emergente de Teams, la parte del dominio de la dirección URL debe estar en la lista de dominios válidos de la aplicación. Para obtener más información, consulte [validDomains](~/resources/schema/manifest-schema.md#validdomains) en el esquema de manifiesto.
> * El tamaño del elemento emergente de autenticación se puede definir mediante la inclusión de parámetros de la cadena de consulta de ancho y alto, `Value = $"{_siteUrl}/searchSettings.html?height=600&width=600"`.

### <a name="start-the-sign-in-flow"></a>Iniciar el flujo de inicio de sesión

La experiencia de inicio de sesión debe ser receptiva y ajustarse a una ventana emergente. Debe integrarse con el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client), que usa el paso de mensajes.

Al igual que con otras experiencias incrustadas que se ejecutan dentro de Microsoft Teams, el código dentro de la ventana debe llamar primero a `microsoftTeams.initialize()`. Si el código realiza un flujo de OAuth, puede pasar al identificador de usuario de Teams a la ventana, que luego lo pasa a la dirección URL de inicio de sesión de OAuth.

### <a name="complete-the-sign-in-flow"></a>Completar el flujo de inicio de sesión

Cuando la solicitud de inicio de sesión se complete y lo redirija de vuelta a la página, debe realizar los siguientes pasos:

1. Genere un código de seguridad, un número aleatorio. Debe almacenar en caché este código en el servicio, junto con las credenciales obtenidas a través del flujo de inicio de sesión, como los tokens de OAuth 2.0.
1. Llame a `microsoftTeams.authentication.notifySuccess` y pase el código de seguridad.

En este momento, la ventana se cierra y el control se pasa al cliente de Teams. El cliente ahora vuelve a emitir la consulta de usuario original, junto con el código de seguridad de la propiedad `state`. El código puede usar un código de seguridad para buscar las credenciales almacenadas anteriormente y completar la secuencia de autenticación, y así completar la solicitud del usuario.

#### <a name="reissued-request-example"></a>Ejemplo de solicitud reemitido

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
|Extensiones de mensaje: autenticación y configuración | Extensión de mensaje que tiene una página de configuración, acepta solicitudes de búsqueda y devuelve los resultados después de que el usuario haya iniciado sesión. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[Ver](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="see-also"></a>Consulte también

[Compatibilidad del inicio de sesión único (SSO) con las extensiones de mensaje](~/messaging-extensions/how-to/enable-sso-auth-me.md)
