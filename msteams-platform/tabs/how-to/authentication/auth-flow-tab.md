---
title: Flujo de autenticación para pestañas
description: Describe el flujo de autenticación en pestañas
ms.topic: conceptual
keywords: pestañas de flujo de autenticación de teams
ms.openlocfilehash: 9505419a6594529bcf8d19a90d029705e573c67b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014589"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Flujo de autenticación de Microsoft Teams para pestañas

> [!Note]
> Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que está usando al menos la versión 1.4.1 del SDK de JavaScript de Teams.
> El SDK de Teams inicia una ventana independiente para el flujo de autenticación y, por lo tanto, el mismo atributo de sitio se puede establecer en "Lax". Actualmente, SameSite=None no es compatible con el cliente de escritorio de Teams ni con versiones anteriores de Chrome o Safari.

OAuth 2.0 es un estándar abierto para la autenticación y autorización usados por Azure AD y muchos otros proveedores de identidades. Un conocimiento básico de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams; [esta es una buena introducción](https://aaronparecki.com/oauth-2-simplified/) que es más fácil de seguir que la [especificación formal.](https://oauth.net/2/) El flujo de autenticación para pestañas y bots es un poco diferente porque las pestañas son muy similares a los sitios web para que puedan usar OAuth 2.0 directamente; Los bots no son y deben hacer algunas cosas de forma diferente, pero los conceptos básicos son idénticos.

*Vea*, iniciar el flujo de autenticación para [pestañas](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow) para obtener un ejemplo de flujo de autenticación para pestañas y bots con Node y el tipo de concesión implícita [de OAuth 2.0](https://oauth.net/2/grant-types/implicit/).

![Diagrama de secuencia de autenticación de tabulación](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. El usuario interactúa con el contenido de la página de configuración o contenido de la pestaña, normalmente un botón denominado "Iniciar sesión" o "Iniciar sesión".
2. La pestaña crea la dirección URL para su página de inicio de autenticación, opcionalmente usando información de marcadores de posición de dirección URL o llamando al método de SDK de cliente de Teams para simplificar la experiencia de autenticación `microsoftTeams.getContext()` para el usuario. Por ejemplo, al autenticar con Azure AD, si el parámetro se establece en la dirección de correo electrónico del usuario, es posible que el usuario ni siquiera tenga que iniciar sesión si lo ha hecho recientemente, porque Azure AD usará las credenciales almacenadas en caché del usuario si es posible: el elemento emergente parpadeará brevemente y `login_hint` desaparecerá.
3. A continuación, la pestaña llama `microsoftTeams.authentication.authenticate()` al método y registra las funciones `successCallback` `failureCallback` y.
4. Teams abre la página de inicio en un iframe en una ventana emergente. La página de inicio genera datos aleatorios, los guarda para su validación futura y redirige al punto de conexión del proveedor de identidades, como `state` `/authorize` azure `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` AD. Reemplace `<tenant id>` por su propio identificador de inquilino (context.tid).
    * Al igual que otros flujos de autenticación de aplicaciones en Teams, la página de inicio debe estar en un dominio que esté en su lista y en el mismo dominio que la página de redireccionamiento posterior al inicio `validDomains` de sesión.
    * **IMPORTANTE:** Las llamadas implícitas de flujo de concesión de OAuth 2.0 para un parámetro en la solicitud de autenticación que contiene datos de sesión únicos para evitar un ataque de falsificación de solicitud entre `state` [sitios.](https://en.wikipedia.org/wiki/Cross-site_request_forgery) Los ejemplos siguientes usan un GUID generado aleatoriamente para los `state` datos.
5. En el sitio del proveedor, el usuario inicia sesión y concede acceso a la pestaña.
6. El proveedor lleva al usuario a la página de redireccionamiento de OAuth 2.0 de la pestaña con un token de acceso.
7. La pestaña comprueba que el valor devuelto coincide con lo que se guardó anteriormente y llama , que a su vez llama a la función `state` registrada en el paso `microsoftTeams.authentication.notifySuccess()` `successCallback` 3.
8. Teams cierra la ventana emergente.
9. La pestaña muestra la interfaz de usuario de configuración o actualiza o vuelve a cargar el contenido de las pestañas, según desde dónde se inició el usuario.

## <a name="treat-tab-context-as-hints"></a>Tratar el contexto de pestaña como sugerencias

Aunque el contexto de la pestaña proporciona información útil sobre el usuario, no use esta información para autenticar al usuario, ya sea que la obtenga como parámetros de dirección URL a la dirección URL de contenido de la pestaña o llamando a la función en el SDK de cliente de `microsoftTeams.getContext()` Microsoft Teams. Un actor malintencionado podría invocar la dirección URL del contenido de la pestaña con sus propios parámetros, y una página web que suplanta Microsoft Teams podría cargar la dirección URL de contenido de la pestaña en un iframe y devolver sus propios datos a la `getContext()` función. Debe tratar la información relacionada con la identidad en el contexto de la pestaña simplemente como sugerencias y validarla antes de usarla. Consulte las notas en Navegar [a la página de autorización desde la página emergente.](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)

## <a name="samples"></a>Ejemplos

Para obtener código de ejemplo que muestra el proceso de autenticación de pestañas, vea:

* [Ejemplo de autenticación de pestañas de Microsoft Teams (Nodo)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Ejemplo de autenticación de pestañas de Microsoft Teams (C#)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="more-details"></a>Más detalles

Para obtener un tutorial de implementación detallado para la autenticación de pestañas destinada a Azure Active Directory, vea:

* [Autenticar a un usuario en una pestaña de Microsoft Teams](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Autenticación silenciosa](~/tabs/how-to/authentication/auth-silent-AAD.md)
