---
title: Atributo de cookies SameSite
author: laujan
description: Obtenga información sobre los tipos de cookies, incluidas las cookies de SameSite, sus atributos, sus implicaciones en Teams pestañas, módulos de tareas y extensiones de mensaje, y su autenticación en Teams
keywords: atributos de cookie del mismo sitio
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 1fbaf46da93a0d7c253f1f5d2ad6c9ae1764565a
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104493"
---
# <a name="samesite-cookie-attribute"></a>Atributo de cookies SameSite

Las cookies son cadenas de texto enviadas desde sitios web y almacenadas en un equipo por el explorador web. Se usan para la autenticación y la personalización. Por ejemplo, las cookies se usan para recuperar información con estado, conservar la configuración del usuario, registrar la actividad de exploración y mostrar anuncios pertinentes. Las cookies siempre están vinculadas a un dominio determinado y las instalan varias partes.

## <a name="types-of-cookies"></a>Tipos de cookies

Los tipos de cookies y sus ámbitos correspondientes son los siguientes:

|Cookie|Ámbito|
| ------ | ------ |
|Cookie de primera persona|Los sitios web que visita un usuario crean una cookie de primera persona. Se usa para guardar datos, como artículos de carro de la compra, credenciales de inicio de sesión. Por ejemplo, las cookies de autenticación y otros análisis.|
|Cookie de segunda parte|Una cookie de segunda parte es técnicamente la misma que una cookie de primera. La diferencia es que los datos se comparten con una segunda parte a través de un acuerdo de asociación de datos. Por ejemplo, [Microsoft Teams análisis e informes](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference). |
|Cookie de terceros|Una cookie de terceros la instala un dominio distinto del que el usuario visitó explícitamente y se usa principalmente para el seguimiento. Por ejemplo, **Como** botones, publicación de anuncios y chats en directo.|

## <a name="cookies-and-http-requests"></a>Cookies y solicitudes HTTP

Antes de la introducción de las restricciones de SameSite, las cookies se almacenaban en el explorador. Se adjuntaron a cada solicitud web HTTP y se enviaron al servidor mediante el encabezado de `Set Cookie` respuesta HTTP. Este método introdujo vulnerabilidades de seguridad, como la falsificación de solicitudes entre sitios, denominadas ataques CSRF. El componente SameSite redujo la exposición a través de su implementación y administración en el encabezado SetCookie.

## <a name="samesite-cookie-attribute-initial-release"></a>Atributo de cookie SameSite: versión inicial

La versión 51 de Google Chrome introdujo la `SetCookie SameSite` especificación como un atributo opcional. A partir de la compilación 17672, Windows 10 introdujo compatibilidad con cookies de SameSite para el [explorador MicrosoftEdge&nbsp;](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/).

Puede no agregar el atributo de cookie SameSite al `SetCookie` encabezado o agregarlo con una de las dos opciones de configuración, **Lax** y **Strict**. Un atributo SameSite no implementado se consideró el estado predeterminado.

## <a name="samesite-cookie-attribute-2020-release"></a>Atributo de cookie SameSite: versión 2020

Chrome 80, publicado en febrero de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se pasan tres valores al atributo SameSite actualizado: **Strict**, **Lax** o **None**. Si no se especifica, el atributo SameSite de cookies toma el valor `SameSite=Lax` de forma predeterminada.

Los atributos de cookies de SameSite son los siguientes:

|Setting | Aplicación | Valor |Especificación de atributo |
| -------- | ----------- | --------|--------|
| **Lax**  | Las cookies solo se envían automáticamente en un contexto de **primera entidad** y con solicitudes HTTP GET. Las cookies de SameSite se retienen en solicitudes secundarias entre sitios, como llamadas para cargar imágenes o iframes. Se envían cuando un usuario navega a la dirección URL desde un sitio externo, por ejemplo, siguiendo un vínculo.| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Estricto** |El explorador solo envía cookies para solicitudes de contexto de primera entidad. Se trata de solicitudes que se originaron en el sitio que establece la cookie. Si la solicitud se originó desde una dirección URL diferente a la de la ubicación actual, no se envía ninguna de las cookies etiquetadas con el `Strict` atributo .| Opcional |`Set-Cookie: key=value; SameSite=Strict`|
| **Ninguna** | Las cookies se envían tanto en el contexto de origen como en las solicitudes entre orígenes; sin embargo, el valor debe establecerse explícitamente en **`None`** y todas las solicitudes del explorador **deben seguir el protocolo HTTPS** e incluir el **`Secure`** atributo que requiere una conexión cifrada. Se **rechazan** las cookies que no cumplen ese requisito. <br/>**Ambos atributos son necesarios juntos**. Si  **`None`** se especifica sin **`Secure`**  o si no se usa el protocolo HTTPS, se rechazan las cookies de terceros.| Opcional, pero, si se establece, se requiere el protocolo HTTPS. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams implicaciones y ajustes

1. Habilite la configuración pertinente de SameSite para las cookies y valide que las aplicaciones y extensiones sigan funcionando en Teams.
1. Si se produce un error en las aplicaciones o extensiones, realice las correcciones necesarias antes de la versión de Chrome 80.
1. Los asociados internos de Microsoft pueden unirse al siguiente equipo para obtener más información o ayudar con este problema: <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>.

> [!NOTE]
> Debe establecer los atributos de SameSite para reflejar el uso previsto para las cookies. No se base en el comportamiento predeterminado del explorador. Para obtener más información, vea [Developers: Get Ready for New SameSite=None; Protección de Configuración de cookies](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-message-extensions"></a>Pestañas, módulos de tareas y extensiones de mensaje

* Teams pestañas usan `<iframes>` para insertar contenido que se ve en un contexto de nivel superior o de primera entidad.
* Los módulos de tareas le permiten crear experiencias emergentes modales en su aplicación de Teams. De forma similar a una pestaña, se abre una ventana modal dentro de la página actual.
* Las extensiones de mensaje permiten insertar contenido enriquecido en un mensaje de chat desde recursos externos.

Las cookies usadas por el contenido incrustado se consideran de terceros cuando el sitio se muestra en un `<iframe>`. Además, si los recursos remotos de una página se basan en las cookies que se envían con una solicitud `<img>` y `<script>` etiquetas, fuentes externas y contenido personalizado, debe asegurarse de que están marcados para el uso entre sitios, como `SameSite=None; Secure` o asegurarse de que hay una reserva en su lugar.

### <a name="authentication"></a>Autenticación

Debe usar el flujo de autenticación basado en web para lo siguiente:

* Páginas de contenido incrustadas en pestañas.
* Página de configuración, módulo de tareas y extensión de mensaje.
* Bot conversacional con un módulo de tareas.

De acuerdo con las restricciones actualizadas de SameSite, un explorador no agrega una cookie a un sitio web ya autenticado si el vínculo deriva de un sitio externo. Debe asegurarse de que las cookies de autenticación están marcadas para el uso `SameSite=None; Secure` entre sitios o asegurarse de que hay una reserva.

## <a name="android-system-webview"></a>Android System WebView

Android WebView es un componente del sistema chrome que permite a las aplicaciones de Android mostrar el contenido web. Aunque las nuevas restricciones son predeterminadas, a partir de Chrome 80, no se aplican inmediatamente en WebViews. Se aplicarán en el futuro. Para prepararse, Android permite que las aplicaciones nativas establezcan cookies directamente a través de [cookieManager API](https://developer.android.com/reference/android/webkit/CookieManager).

> [!NOTE]
>
> * Debe declarar las cookies propias como `SameSite=Lax` o `SameSite=Strict`, según corresponda.
> * Debe declarar cookies de terceros como `SameSite=None; Secure`.

## <a name="see-also"></a>Vea también

* [Ejemplos de SameSite](https://github.com/GoogleChromeLabs/samesite-examples)
* [Recetas de cookies de SameSite](https://web.dev/samesite-cookie-recipes/)
* [Clientes incompatibles conocidos]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [Desarrolladores: Prepárese para el nuevo SameSite=None; Configuración de cookies seguras](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Próximos cambios de cookies de SameSite en ASP.NET y ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Cookies HTTP](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
