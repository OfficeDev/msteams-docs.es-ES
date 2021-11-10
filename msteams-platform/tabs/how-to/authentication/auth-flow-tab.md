---
title: Flujo de autenticación para pestañas
description: Describe el flujo de autenticación en pestañas, OAuth por AAD y proporciona un ejemplo de código
ms.topic: conceptual
ms.localizationpriority: medium
keywords: pestañas de flujo de autenticación de teams
ms.openlocfilehash: 0b58e0182714921745fa911cc747aa1c314d3df2
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888450"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Microsoft Teams de autenticación para pestañas

> [!NOTE]
> Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que está usando al menos la versión 1.4.1 del SDK Microsoft Teams JavaScript.  
> Teams SDK inicia una ventana independiente para el flujo de autenticación. Establezca el `SameSite` atributo en **Lax**. Teams cliente de escritorio o versiones anteriores de Chrome o Safari no `SameSite` admiten =None.

OAuth 2.0 es un estándar abierto para la autenticación y autorización que usan Azure Active Directory (AAD) y muchos otros proveedores de identidades. Un conocimiento básico de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams. Para obtener más información, vea [OAuth 2 simplified](https://aaronparecki.com/oauth-2-simplified/) that is easier to follow than the [formal specification](https://oauth.net/2/). El flujo de autenticación para pestañas y bots es diferente porque las pestañas son similares a los sitios web para que puedan usar OAuth 2.0 directamente. Los bots hacen algunas cosas de forma diferente, pero los conceptos básicos son idénticos.

Por ejemplo, el flujo de autenticación para pestañas y bots que usan Node y el tipo de concesión implícita [OAuth 2.0](https://oauth.net/2/grant-types/implicit/), vea Iniciar flujo de autenticación [para pestañas](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow).

> [!NOTE]
> Antes de mostrar **un botón Inicio** de sesión al usuario y llamar a la API en respuesta a la selección del botón, debe esperar a que se complete la `microsoftTeams.authentication.authenticate` inicialización del SDK. Puede pasar una devolución de llamada a la API a `microsoftTeams.initialize` la que se llama cuando se complete la inicialización.

![Diagrama de secuencia de autenticación de tabulación](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. El usuario interactúa con el contenido de la página de contenido o configuración de pestañas, normalmente un botón **Iniciar** **sesión o Iniciar** sesión.
2. La pestaña construye la dirección URL de su página de inicio de autenticación. Opcionalmente, usa información de marcadores de posición de dirección URL o llamadas Teams método SDK de cliente para simplificar la `microsoftTeams.getContext()` experiencia de autenticación del usuario. Por ejemplo, al autenticar con AAD, si el parámetro está establecido en la dirección de correo electrónico del usuario, el usuario no tiene que iniciar sesión si lo ha hecho `login_hint` recientemente. Esto se debe a AAD las credenciales almacenadas en caché del usuario. La ventana emergente se muestra brevemente y, a continuación, desaparece.
3. A continuación, la pestaña llama al método `microsoftTeams.authentication.authenticate()` y registra las funciones `successCallback` y `failureCallback`.
4. Teams abre la página de inicio en un iframe en una ventana emergente. La página de inicio genera datos aleatorios, los guarda para la validación futura y redirige al extremo del proveedor de identidades, por ejemplo, `state` `/authorize` para `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` Azure AD. Reemplace `<tenant id>` por su propio identificador de inquilino que sea context.tid.
De forma similar a otros flujos de autenticación de aplicación en Teams, la página de inicio debe estar en un dominio que esté en su lista y en el mismo dominio que la página de redireccionamiento de inicio de `validDomains` sesión.

    > [!NOTE]
    > El flujo de concesión implícito de OAuth 2.0 llama a un parámetro de la solicitud de autenticación, que contiene datos de sesión únicos para evitar un ataque de falsificación de solicitudes `state` [entre sitios.](https://en.wikipedia.org/wiki/Cross-site_request_forgery) Los ejemplos usan un GUID generado aleatoriamente para los `state` datos.

5. En el sitio del proveedor, el usuario inicia sesión y concede acceso a la pestaña.
6. El proveedor lleva al usuario a la página de redireccionamiento de OAuth 2.0 de la pestaña con un token de acceso.
7. La pestaña comprueba que el valor devuelto coincide con lo que se guardó anteriormente y llama a , que a su vez llama a `state` la función registrada en el paso `microsoftTeams.authentication.notifySuccess()` `successCallback` 3.
8. Teams cierra la ventana emergente.
9. La pestaña muestra la interfaz de usuario de configuración, actualiza o vuelve a cargar el contenido de las pestañas, en función del lugar desde el que se inició el usuario.

## <a name="treat-tab-context-as-hints"></a>Tratar el contexto de tabulación como sugerencias

Aunque el contexto de pestaña proporciona información útil sobre el usuario, no use esta información para autenticar al usuario. Autentique al usuario incluso si obtiene la información como parámetros de dirección URL en la dirección URL de contenido de la pestaña o llamando a la función en el SDK Microsoft Teams `microsoftTeams.getContext()` cliente. Un actor malintencionado puede invocar la dirección URL de contenido de la pestaña con sus propios parámetros. El actor también puede invocar una página web que suplanta Microsoft Teams para cargar la dirección URL de contenido de la pestaña en un iframe y devolver sus propios datos a la `getContext()` función. Debe tratar la información relacionada con la identidad en el contexto de la pestaña como una sugerencia y validarla antes de usarlo. Consulte las notas de [navegar a la página de autorización desde la página emergente](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page).

## <a name="code-sample"></a>Ejemplo de código

Código de ejemplo que muestra el proceso de autenticación de tabulación:

| **Ejemplo de nombre** | **Descripción** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Teams de pestañas | Proceso de autenticación para pestañas que usan AAD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="more-details"></a>Más detalles

Para obtener una implementación detallada para la autenticación de pestañas AAD, vea:

* [Autenticar a un usuario en una Teams pestaña](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Autenticación silenciosa](~/tabs/how-to/authentication/auth-silent-AAD.md)
