---
title: Atributo de cookies SameSite
author: laujan
description: Obtenga información sobre los tipos de cookies, incluidas las cookies samesite, sus atributos, sus implicaciones en las pestañas de Teams, los módulos de tareas y las extensiones de mensaje, y su autenticación en Teams.
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: fee4855c8dd6c8dfdb83bce8b6d4d0c5da348724
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142740"
---
# <a name="samesite-cookie-attribute"></a>Atributo de cookies SameSite

Las cookies son cadenas de texto enviadas desde sitios web y almacenadas en un equipo por el explorador web. Se usan para la autenticación y la personalización. Por ejemplo, las cookies se usan para recuperar información con estado, conservar la configuración del usuario, registrar la actividad de exploración y mostrar anuncios relevantes. Las cookies siempre están vinculadas a un dominio determinado y las instalan varias partes.

## <a name="types-of-cookies"></a>Tipos de cookies

Los tipos de cookie y sus ámbitos correspondientes son los siguientes:

|Cookie|Ámbito|
| ------ | ------ |
|Cookie propia|Los sitios web que visita un usuario crean una cookie de origen. Se usa para guardar datos, como artículos de carro de la compra, credenciales de inicio de sesión. Por ejemplo, cookies de autenticación y otros análisis.|
|Cookie de segundas partes|Técnicamente, una cookie de terceros es la misma que una cookie de origen. La diferencia es que los datos se comparten con un tercero a través de un acuerdo de asociación de datos. Por ejemplo, [análisis e informes de Microsoft Teams](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference). |
|Cookie de terceros|Una cookie de terceros la instala un dominio distinto del que el usuario visitó explícitamente y se usa para realizar el seguimiento. Por ejemplo, botones **Me gusta**, servicios de anuncios y chats en directo.|

## <a name="cookies-and-http-requests"></a>Cookies y solicitudes HTTP

Antes de la introducción de las restricciones de SameSite, las cookies se almacenaban en el explorador. Se adjuntaron a cada solicitud web HTTP y se enviaron al servidor por el encabezado de respuesta HTTP `Set Cookie`. Este método introdujo vulnerabilidades de seguridad, como es la falsificación de solicitudes entre sitios, denominadas ataques CSRF. El componente SameSite redujo la exposición a través de su implementación y administración en el encabezado SetCookie.

## <a name="samesite-cookie-attribute-initial-release"></a>Atributo de cookie SameSite: versión inicial

La versión 51 de Google Chrome introdujo la especificación de `SetCookie SameSite` como un atributo opcional. A partir de la compilación 17672, Windows 10 introdujo la compatibilidad con cookies samesite para el explorador [Microsoft&nbsp;Edge](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/).

Puede optar por no agregar el atributo de cookie SameSite al encabezado `SetCookie` o agregarlo con uno de dos valores, **Lax** y **Strict**. Un atributo SameSite no implementado se consideró el estado predeterminado.

## <a name="samesite-cookie-attribute-2020-release"></a>Atributo de cookie SameSite: versión 2020

Chrome 80, publicado en febrero de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se pasan tres valores al atributo SameSite actualizado: **Estricto**, **Laxo** o **Ninguno**. Si no se especifica, el atributo SameSite de cookies toma el valor `SameSite=Lax` de forma predeterminada.

Los atributos de cookie SameSite son los siguientes:

|Configuración | Aplicación | Valor |Especificación de atributo |
| -------- | ----------- | --------|--------|
| **Laxo**  | Las cookies solo se envían automáticamente en un contexto de **tercera parte** y con solicitudes HTTP GET. Las cookies samesite se retienen en las subconsultas entre sitios, como son las llamadas para cargar imágenes o iframes. Se envían cuando un usuario navega a la dirección URL desde un sitio externo, por ejemplo, siguiendo un vínculo.| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Estricto** |El explorador solo envía cookies para solicitudes de contexto propias. Se trata de solicitudes procedentes del sitio que establecen la cookie. Si la solicitud se originó desde una dirección URL diferente a la de la ubicación actual, no se envía ninguna de las cookies etiquetadas con el atributo `Strict`.| Opcional |`Set-Cookie: key=value; SameSite=Strict`|
| **Ninguna** | Las cookies se envían tanto en el contexto de origen como en las solicitudes entre orígenes; sin embargo, el valor debe establecerse explícitamente en **`None`** y todas las solicitudes del explorador **deben seguir el protocolo HTTPS** e incluir el **`Secure`** atributo , que requiere una conexión cifrada. Se **rechazan** las cookies que no cumplen ese requisito. <br/>**Se requieren ambos atributos juntos**. Si  **`None`** se especifica sin **`Secure`**  o si no se usa el protocolo HTTPS, se rechazan las cookies de terceros.| Opcional, pero, si se establece, se requiere el protocolo HTTPS. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Implicaciones y ajustes de Teams

1. Habilite la configuración de SameSite relevante para las cookies y valide que las aplicaciones y extensiones sigan funcionando en Teams.
1. Si se produce un error en tus aplicaciones o extensiones, realiza las correcciones necesarias antes de la versión Chrome 80.
1. Los partners internos de Microsoft pueden unirse al siguiente equipo para obtener más información o ayuda con este problema: <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>.

> [!NOTE]
> Debe establecer atributos SameSite para reflejar el uso previsto para las cookies. No deberá basarse en el comportamiento predeterminado del explorador. Para más información, vea [Developers: Get Ready for New SameSite=None; Secure Cookie Settings](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-message-extensions"></a>Pestañas, módulos de tareas y extensiones de mensaje

* Las pestañas de Teams usan `<iframes>` para incrustar contenido que se ve en un contexto de nivel superior o de primera entidad.
* Los módulos de tareas le permiten crear experiencias emergentes modales en su aplicación de Teams. De forma similar a una pestaña, se abre una ventana modal dentro de la página actual.
* Las extensiones de mensaje permiten incrustar contenido enriquecido en un mensaje de chat desde recursos externos.

Las cookies utilizadas por el contenido insertado se consideran de terceros cuando el sitio se muestra en un `<iframe>`. Además, si los recursos remotos de una página dependen de las cookies que se envían con una solicitud `<img>` y `<script>` etiquetas, fuentes externas y contenido personalizado, debe cerciorarse de que están marcadas para uso entre sitios, como es `SameSite=None; Secure` o debe cerciórese de que se ha implementado una reserva.

### <a name="authentication"></a>Autenticación

Debe usar el flujo de autenticación basado en web para lo siguiente:

* Páginas de contenido incrustadas en pestañas.
* Página de configuración, módulo de tareas y extensión de mensaje.
* Bot conversacional con un módulo de tareas.

Según las restricciones actualizadas de SameSite, un explorador no agrega una cookie a un sitio web ya autenticado si el vínculo deriva de un sitio externo. Debe cerciorarse de que las cookies de autenticación están marcadas para el uso entre sitios `SameSite=None; Secure` o cerciorarse de que hay una reserva en su lugar.

## <a name="android-system-webview"></a>Android System WebView

Android WebView es un componente del sistema Chrome que permite que las aplicaciones Android muestren el contenido web. Aunque las nuevas restricciones son predeterminadas, a partir de Chrome 80, no se aplican inmediatamente en WebViews. Se aplicarán en el futuro. Para prepararse, Android permite que las aplicaciones nativas establezcan cookies directamente a través de la API [CookieManager](https://developer.android.com/reference/android/webkit/CookieManager).

> [!NOTE]
>
> * Debe declarar las cookies de origen como `SameSite=Lax` o `SameSite=Strict`, según corresponda.
> * Debe declarar las cookies de terceros como `SameSite=None; Secure`.

## <a name="see-also"></a>Consulte también

* [Ejemplos de SameSite](https://github.com/GoogleChromeLabs/samesite-examples)
* [Recetas de cookies de SameSite](https://web.dev/samesite-cookie-recipes/)
* [Clientes incompatibles conocidos]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [Desarrolladores: Prepárese para el nuevo SameSite=None; Configuración de cookies seguras](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Próximos cambios de cookies de SameSite en ASP.NET y ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Cookies HTTP](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
