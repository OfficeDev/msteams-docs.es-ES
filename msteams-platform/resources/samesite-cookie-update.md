---
title: Atributo cookie SameSite
author: laujan
description: describe los atributos de la cookie SameSite
keywords: atributos cookie samesite
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 34674ab58cc9808525d315cea3db464ddf11b4f9
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140568"
---
# <a name="samesite-cookie-attribute"></a>Atributo cookie SameSite 

Las cookies son cadenas de texto, enviadas desde sitios web y almacenadas en un equipo por el explorador web. Se usan para la autenticación y personalización. Por ejemplo, las cookies se usan para recuperar información con estado, conservar la configuración del usuario, registrar la actividad de exploración y mostrar anuncios relevantes. Las cookies siempre están vinculadas a un dominio determinado y las instalan varias partes. 

## <a name="types-of-cookies"></a>Tipos de cookies

Los tipos de cookies y sus ámbitos correspondientes son los siguientes:

|Cookie|Ámbito|
| ------ | ------ |
|Cookie de primer partido|Los sitios web que visita un usuario crean una cookie de primera persona. Se usa para guardar datos, como elementos del carro de la compra, credenciales de inicio de sesión. Por ejemplo, cookies de autenticación y otros análisis.|
|Cookie de segunda parte|Una cookie de segunda parte es técnicamente la misma que una cookie de primera parte. La diferencia es que los datos se comparten con una segunda parte a través de un contrato de asociación de datos. Por ejemplo, [Microsoft Teams análisis e informes](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference). |
|Cookie de terceros|Una cookie de terceros la instala un dominio distinto del que el usuario visitó explícitamente y se usa principalmente para el seguimiento. Por ejemplo, Botones de me **gusta,** servicio de anuncios y chats en directo.|

## <a name="cookies-and-http-requests"></a>Cookies y solicitudes HTTP

Antes de la introducción de las restricciones de SameSite, las cookies se almacenaban en el explorador. Se adjuntaron a cada solicitud web HTTP y se enviaron al servidor mediante el `Set Cookie` encabezado de respuesta HTTP. Este método introdujo vulnerabilidades de seguridad, como la falsificación de solicitudes entre sitios, denominadas ataques CSRF. El componente SameSite redujo la exposición a través de su implementación y administración en el encabezado SetCookie.

## <a name="samesite-cookie-attribute-initial-release"></a>Atributo cookie SameSite: versión inicial

Google Chrome versión 51 introdujo la `SetCookie SameSite` especificación como un atributo opcional. A partir de la compilación 17672, Windows 10 compatibilidad con cookies SameSite para el [explorador Microsoft Edge .](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)

Puede optar por no agregar el atributo cookie SameSite al encabezado o agregarlo con una de las dos opciones `SetCookie` de configuración, **Lax** y **Strict**. Un atributo SameSite sin implementar se consideró el estado predeterminado.

## <a name="samesite-cookie-attribute-2020-release"></a>Atributo cookie SameSite: versión 2020

Chrome 80, publicado en febrero de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se pasan tres valores al atributo SameSite actualizado: **Strict**, **Lax** o **None**. Si no se especifica, el atributo cookies SameSite toma el valor `SameSite=Lax` de forma predeterminada.    
 
Los atributos de cookie SameSite son los siguientes:

|Configuración | Aplicación | Valor |Especificación de atributos |
| -------- | ----------- | --------|--------|
| **Lax**  | Las cookies se envían automáticamente solo en un **contexto de primera** parte y con solicitudes HTTP GET. Las cookies de SameSite se retienen en solicitudes de subsitio entre sitios, como llamadas para cargar imágenes o iframes. Se envían cuando un usuario navega a la dirección URL desde un sitio externo, por ejemplo, siguiendo un vínculo.| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Estricto** |El explorador solo envía cookies para solicitudes de contexto de primera parte. Se trata de solicitudes procedentes del sitio que establecen la cookie. Si la solicitud se originó desde una dirección URL diferente a la de la ubicación actual, no se enviará ninguna de las cookies `Strict` etiquetadas con el atributo.| Opcional |`Set-Cookie: key=value; SameSite=Strict`|
| **Ninguna** | Las cookies se envían tanto en el contexto de la primera parte como en las solicitudes entre orígenes; sin embargo, el valor debe establecerse explícitamente en y todas las solicitudes de explorador deben seguir el protocolo HTTPS e incluir el **`None`** atributo que requiere una conexión  **`Secure`** cifrada. Se rechazan las cookies que no cumplen ese **requisito.** <br/>**Ambos atributos son necesarios juntos.** Si se especifica sin o si no se usa el protocolo HTTPS, se  **`None`** **`Secure`**  rechazan las cookies de terceros.| Opcional, pero, si se establece, se requiere el protocolo HTTPS. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams implicaciones y ajustes

1. Habilita la configuración de SameSite relevante para las cookies y valida que tus aplicaciones y extensiones siguen funcionando en Teams.
1. Si las aplicaciones o las extensiones fallan, realiza las correcciones necesarias antes de la versión de Chrome 80.
1. Los partners internos de Microsoft pueden unirse al siguiente equipo para obtener más información o ayuda con este problema: <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> .

> [!NOTE]
> Debe establecer los atributos SameSite para reflejar el uso previsto para las cookies. No confíe en el comportamiento predeterminado del explorador. Para obtener más información, vea [Developers: Get Ready for New SameSite=None; Cookie segura Configuración](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-messaging-extensions"></a>Pestañas, módulos de tareas y extensiones de mensajería

* Teams pestañas para insertar contenido que se `<iframes>` ve en un contexto de nivel superior o de primera parte.
* Los módulos de tareas te permiten crear experiencias emergentes modales en tu  aplicación de Teams. De forma similar a una pestaña, se abre una ventana modal dentro de la página actual.
* Las extensiones de mensajería permiten insertar contenido enriquecido en un mensaje de chat desde recursos externos.

Las cookies usadas por el contenido incrustado se consideran de terceros cuando el sitio se muestra en un `<iframe>` archivo . Además, si los recursos remotos de una página dependen de las cookies que se envían con una solicitud y etiquetas, fuentes externas y contenido personalizado, debe asegurarse de que están marcadas para el uso entre sitios, como o asegurarse de que hay una `<img>` `<script>` `SameSite=None; Secure` reserva.

### <a name="authentication"></a>Autenticación

Debe usar el flujo de autenticación basado en web para lo siguiente:

* Páginas de contenido incrustadas en pestañas.
* Página de configuración, módulo de tareas y extensión de mensajería.
* Bot conversacional con un módulo de tareas.

Según las restricciones de SameSite actualizadas, un explorador no agrega una cookie a un sitio web ya autenticado si el vínculo deriva de un sitio externo. Debe asegurarse de que las cookies de autenticación están marcadas para el uso entre sitios o asegurarse de que hay una `SameSite=None; Secure` reserva en su lugar.

## <a name="android-system-webview"></a>Android System WebView

Android WebView es un componente del sistema Chrome que permite a las aplicaciones Android mostrar el contenido web. Aunque las nuevas restricciones son predeterminadas, a partir de Chrome 80, no se aplican inmediatamente en WebViews. Se aplicarán en el futuro. Para prepararse, Android permite que las aplicaciones nativas establezcan cookies directamente a través de la [API cookieManager](https://developer.android.com/reference/android/webkit/CookieManager).

> [!NOTE]     
> * Debe declarar las cookies de primera persona `SameSite=Lax` como o , según `SameSite=Strict` corresponda.      
> * Debe declarar cookies de terceros como `SameSite=None; Secure` .   

## <a name="see-also"></a>Vea también

* [Ejemplos de SameSite](https://github.com/GoogleChromeLabs/samesite-examples)
* [Recetas de cookies de SameSite](https://web.dev/samesite-cookie-recipes/)
* [Clientes incompatibles conocidos]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [Desarrolladores: Prepárese para new SameSite=None; Secure Cookie Configuración](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Próximos cambios en las cookies de SameSite ASP.NET y ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Cookies HTTP](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
