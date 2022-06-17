---
title: Habilitación de la autenticación mediante un proveedor de OAuth de terceros
description: En este artículo, aprenda el flujo de autenticación de Teams con pestañas, el proveedor de OAuth de terceros, OAuth por Azure AD y ejemplos de código de autenticación.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 2edd52d80428e47a8586ec27de4b1595d872df8c
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144253"
---
# <a name="enable-authentication-using-third-party-oauth-provider"></a>Habilitación de la autenticación mediante un proveedor de OAuth de terceros

Puede habilitar la autenticación en la aplicación de pestañas mediante proveedores de identidades de OAuth (IdP) de terceros. En este método, un IdP de OAuth valida y concede acceso a la identidad de usuario de la aplicación, como Azure AD, Google, Facebook, GitHub o cualquier otro proveedor. Tendrá que configurar una relación de confianza con el IdP y los usuarios de la aplicación también deben estar registrados con él.

> [!NOTE]
> Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que usa al menos la versión 1.4.1 del SDK de JavaScript de Microsoft Teams.  
> El SDK de Teams inicia una ventana independiente para el flujo de autenticación. Establezca el `SameSite`atributo en **Laxo** El cliente de escritorio de Teams o las versiones anteriores de Chrome o Safari no admiten `SameSite`=None.

## <a name="use-oauth-idp-to-enable-authentication"></a>Uso de OAuth IdP para habilitar la autenticación

OAuth 2.0 es un estándar abierto para la autenticación y autorización que usan Microsoft Azure Active Directory (Azure AD) y muchos otros proveedores de identidades. Tener conocimientos básicos del flujo de concesión implícito de OAuth 2.0 es un requisito previo para trabajar con la autenticación en pestañas de Microsoft Teams. Para obtener más información, vea [OAuth 2 simplificado](https://aaronparecki.com/oauth-2-simplified/) que es más fácil de seguir que la [especificación formal](https://oauth.net/2/). El flujo de autenticación para pestañas y bots es diferente porque las pestañas son similares a los sitios web, por lo que pueden usar OAuth 2.0 directamente. Los bots hacen algunas cosas de forma diferente, pero los conceptos básicos son idénticos.

Por ejemplo, el flujo de autenticación para pestañas y bots que usan Node y el [Tipo de concesión implícita de OAuth 2.0](https://oauth.net/2/grant-types/implicit/), consulte [initiate authentication flow for tabs](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow).

En esta sección se usa Azure AD como ejemplo de un proveedor de OAuth de terceros para habilitar la autenticación en una aplicación de pestañas.

> [!NOTE]
> Antes de mostrar un botón **Login** al usuario y llamar a la API `microsoftTeams.authentication.authenticate` en respuesta a la selección del botón, debe esperar a que se complete la inicialización del SDK. Puede pasar una devolución de llamada a la API `microsoftTeams.initialize` a la que se llama cuando se completa la inicialización.

![Diagrama de secuencia de autenticación de bots](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. El usuario interactúa con el contenido de la configuración de pestaña o la página de contenido, normalmente un **Sign in** o **Log in** botón.
2. La pestaña construye la dirección URL para su página de inicio de autenticación. Opcionalmente, usa información de marcadores de posición de dirección URL o llamadas `microsoftTeams.getContext()` método del SDK de cliente de Teams para simplificar la experiencia de autenticación del usuario. Por ejemplo, al autenticarse con Azure AD, si el parámetro `login_hint` está establecido en la dirección de correo electrónico del usuario, puede que el usuario no tenga que iniciar sesión si ya lo ha hecho recientemente. Esto se debe a que Azure AD usa las credenciales almacenadas en caché del usuario. La ventana emergente se muestra brevemente y, a continuación, desaparece.
3. A continuación, la pestaña llama al método `microsoftTeams.authentication.authenticate()` y registra las funciones `successCallback` y `failureCallback`.
4. Microsoft Teams abre la página de inicio en un  en una ventana emergente. La página de inicio genera datos aleatorios `state`, lo guarda para la validación futura y redirige al punto de conexión `/authorize` del proveedor de identidades, como `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` para Azure AD. Reemplace `<tenant id>` por su propio identificador de inquilino que es context.tid.
Al igual que sucede con otros flujos de autenticación de aplicación en Teams, la página de inicio debe estar en un dominio que esté en su lista `validDomains`, y en el mismo dominio que la página de redireccionamiento tras el inicio de sesión.

    > [!NOTE]
    > El flujo de concesión implícita de OAuth 2.0 exige un `state`parámetro en la solicitud de autenticación, que contiene datos de sesión únicos para evitar un [ataque de falsificación de solicitudes entre sitios](https://en.wikipedia.org/wiki/Cross-site_request_forgery). Los ejemplos utilizan un GUID generado aleatoriamente para los datos `state`.

5. En el sitio web del proveedor, el usuario inicia sesión y concede acceso a la pestaña.
6. El proveedor lleva al usuario a la página de redireccionamiento de OAuth 2.0 de la pestaña con un token de acceso.
7. La pestaña comprueba que el valor devuelto `state` coincida con lo que se guardó anteriormente, y llama a `microsoftTeams.authentication.notifySuccess()`, que a su vez llama a la función `successCallback` registrada en el paso 3.
8. Teams cierra la ventana emergente.
9. La pestaña o bien muestra la configuración de la interfaz de usuario o bien actualiza o vuelve a cargar el contenido de la pestaña, en función de dónde haya empezado el usuario.

> [!NOTE]
> Si la aplicación soporta SAML SSO, entonces el token JWT generado por la pestaña SSO no puede ser utilizado ya que no es soportado.

## <a name="treat-tab-context-as-hints"></a>Tratar el contexto de la pestaña como sugerencias

Aunque el contexto de pestaña proporciona información útil sobre el usuario, no use esta información para autenticar al usuario. Autentique al usuario incluso si obtiene la información como parámetros de dirección URL en la dirección URL del contenido de la pestaña o llamando a la función `microsoftTeams.getContext()` en el SDK de cliente de Microsoft Teams. Un actor malintencionado puede invocar la dirección URL del contenido de la pestaña con sus propios parámetros. El actor también puede invocar una página web que suplante Microsoft Teams para cargar la dirección URL del contenido de la pestaña en un iframe y devolver sus propios datos a la función `getContext()`. Debe tratar la información relacionada con la identidad en el contexto de la pestaña como una sugerencia y validarla antes de usarla. Consulte las notas de [navigate a la página de autorización desde la página emergente](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page).

## <a name="code-sample"></a>Ejemplo de código

Código de ejemplo que muestra el proceso de autenticación de la pestaña:

| **Ejemplo de nombre** | **Descripción** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Autenticación de pestañas de Teams | Proceso de autenticación para pestañas que usan Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="see-also"></a>Consulte también

Para obtener una implementación detallada de la autenticación con tabulación mediante Azure AD, consulte:

* [Authenticate un usuario en una pestaña de Teams](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Autenticación silenciosa](~/tabs/how-to/authentication/auth-silent-AAD.md)
