---
title: Microsoft Teams y el atributo de cookie SameSite (actualización de 2020)
author: laujan
description: ''
keywords: atributos de cookie SameSite
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 167266ba0b5af1c8233cffe1fef496dd94c27ae4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675735"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teams y el atributo de cookie SameSite (actualización de 2020)

## <a name="cookies-in-brief"></a>Breves cookies

 Las cookies son cadenas de texto, enviadas de sitios web y almacenadas en un equipo por el explorador Web. Por lo general, se usan para la autenticación y la personalización, por ejemplo, la solicitud de información de estado, la conservación de la configuración de usuario, la grabación de la actividad de exploración y la visualización de anuncios relevantes. Las cookies siempre están vinculadas a un dominio en particular y las pueden instalar varias partes. Se clasifican de la siguiente manera:

 |Cookie|Ámbito|
 | ------ | ------ |
 |**Cookie de origen**|Los sitios web que visita un usuario y se usan para guardar datos como los elementos del carro de la compra, las credenciales de inicio de sesión (por ejemplo, las cookies de autenticación) y otros análisis crean una cookie de origen.|
 |**Cookie de segundo origen**|Las cookies de segundo nombre son técnicamente las mismas que las de una cookie de origen. La diferencia radica en que los datos se comparten con una segunda parte a través de un acuerdo de Asociación de datos (por ejemplo, [análisis y generación de informes de Microsoft Teams](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)). |
 |**Cookies de terceros**|Una cookie de terceros es instalada por un dominio distinto del que visitó el usuario de forma explícita y se usa principalmente para realizar un seguimiento (por ejemplo, botones "like"), Ad Serving y chats en directo.|

### <a name="cookies-and-http-requests"></a>Cookies y solicitudes HTTP

Antes de la introducción de las restricciones de SameSite, cuando se almacenaban cookies en el explorador, se adjuntaban a *cada* solicitud Web http y se enviaban al servidor mediante el encabezado de respuesta http Set-Cookie. De forma predecible, el rendimiento tuvo el potencial de introducir vulnerabilidades de seguridad, como ataques de falsificación de solicitudes entre sitios (CSRF). *Consulte* [cookies http](https://developer.mozilla.org/docs/Web/HTTP/Cookies). El componente SameSite mitiga la exposición a través de su implementación y administración en el encabezado SetCookie.

### <a name="samesite-attribute-initial-release"></a>Atributo SameSite: versión inicial

La versión 51 de Google Chrome ha incluido la especificación SetCookie SameSite como un atributo *opcional* . A partir de la compilación 17672, Windows 10 incorporó la compatibilidad con cookies SameSite para el [Explorador de Microsoft Edge](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/).

Los desarrolladores pueden optar por no agregar el atributo de cookie SameSite al encabezado SetCookie o pueden agregarlo con una de dos opciones, *LAX* y *STRICT*. Un atributo SameSite no implementado se consideró el estado predeterminado.

## <a name="samesite-cookie-attribute-2020-release"></a>Atributo de cookie SameSite: versión 2020

Chrome 80, programado para su lanzamiento en febrero de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se pueden pasar tres valores al atributo SameSite actualizado: *STRICT*, *LAX*o *None*. Las cookies que no especifican el atributo SameSite `SameSite=Lax`se establecerán de forma predeterminada.

|Setting | Título | Valor |Especificación de atributos |
| -------- | ----------- | --------|--------|
| **Rígida**  | Las cookies solo se enviarán automáticamente en un contexto de *origen* y con solicitudes HTTP GET. Las cookies SameSite se retendrán en las subsolicituds entre sitios, como las llamadas para cargar imágenes o iframe, pero se enviarán cuando un usuario navegue a la dirección URL de un sitio externo, por ejemplo, siguiendo un vínculo.| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Estricta** |El explorador solo enviará cookies para las solicitudes de contexto de origen (las solicitudes que se originan desde el sitio que estableció la cookie). Si la solicitud se originó desde una dirección URL diferente a la de la ubicación actual, no se enviará ninguna `Strict` de las cookies etiquetadas con el atributo.| Opcional |`Set-Cookie: key=value; SameSite=Strict`|
| **Ninguna** | Las cookies se enviarán en el contexto de la entidad de confianza y en las solicitudes de origen cruzado; sin embargo, el valor debe establecerse explícitamente en **`None`** y todas las solicitudes del explorador **deben seguir el protocolo HTTPS** e incluir el **`Secure`** atributo que requiere una conexión cifrada. Se **rechazarán**las cookies que no cumplan ese requisito. <br/>**Ambos atributos son necesarios conjuntamente**. Si solo **`None`** se especifica sin **`Secure`** o si no se usa el protocolo HTTPS, se rechazará la cookie de terceros.| Opcional, pero, si se establece, se requiere el protocolo HTTPS. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="handling-incompatible-clients"></a>Administración de clientes incompatibles

> [!IMPORTANT]
> Actualmente no `SameSite=None` es compatible con el cliente de escritorio de Microsoft [**Teams**](/aspnet/core/security/samesite?view=aspnetcore-3.1#test-with-electron) ni con versiones anteriores de Chrome o Safari. *Consulte* [clientes incompatibles conocidos]( https://www.chromium.org/updates/same-site/incompatible-clients).
>Sin embargo, hay dos **soluciones de solución alternativa**:
>
>1. Compruebe el agente de usuario para proporcionar la propiedad SameSite correcta. Puede implementar la comprobación de agente de usuario en [**C#**](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/) y [**node. js**](https://web.dev/samesite-cookie-recipes/).
>2. Establezca los atributos de la cookie con los modelos nuevos y los antiguos. *Consulte* [Administración de clientes incompatibles](https://web.dev/samesite-cookie-recipes/#handling-incompatible-clients)<br><br>
>**Si la aplicación se está ejecutando en el cliente de escritorio de Microsoft Teams y establece el `SameSite=None` atributo SameSite en, la aplicación no funcionará según lo esperado.**

Con cualquiera de estos métodos se asegurará de que la aplicación sigue funcionando correctamente cuando el cliente de escritorio de Microsoft Teams se actualiza a una `SameSite=None` versión compatible de cromo.

## <a name="teams-implications-and-adjustments"></a>Implicaciones y ajustes de Teams

>[!WARNING]
>**Las aplicaciones que se ejecutan en el cliente de escritorio de `SameSite=None` Microsoft Teams son incompatibles con el atributo y no funcionan según lo esperado.** Consulte las **soluciones alternativas**anteriores.

1. Habilite la configuración de SameSite relevante para sus cookies y compruebe que las aplicaciones y extensiones sigan funcionando en Microsoft Teams.
1. Si se produce un error en las aplicaciones o extensiones, realice las correcciones necesarias antes de la versión de Chrome 80.
1. Los socios internos de Microsoft pueden unirse al siguiente equipo si necesitan más información o ayuda con este problema <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>:.

> [!NOTE]
> Para un procedimiento recomendado, se recomienda establecer siempre los atributos SameSite para reflejar el uso previsto de las cookies, no confíe en el comportamiento predeterminado del explorador. *Consulte* [desarrolladores: Get Ready for New SameSite = None; Configuración de cookies segura](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-message-extensions"></a>Pestañas, módulos de tareas y extensiones de mensajes

* Las pestañas `<iframes>` de Microsoft Teams usan para insertar contenido que se visualiza en un contexto de nivel superior o de nombre de origen.
* Los módulos de tareas le permiten crear experiencias de elemento emergente modal en su aplicación de Teams. De forma similar a una pestaña, se abre una ventana modal dentro de la página actual.
* Las extensiones de mensajes le permiten insertar contenido enriquecido en mensajes de chat desde recursos externos.

Las cookies que usa el contenido insertado se considerarán de terceros cuando el sitio se muestra `<iframe>`en un. Además, si los recursos remotos de una página se basan en cookies que se envían con una solicitud ( `<img>` por `<script>` ejemplo, etiquetas, fuentes externas y contenido personalizado), tendrá que asegurarse de que están marcados para el uso `SameSite=None; Secure` entre sitios (o bien, asegúrese de que haya una reserva en su lugar).

### <a name="authentication"></a>Autenticación

* Si necesita autenticación para las páginas de contenido incrustado en las pestañas, deberá usar el flujo de autenticación basado en Web.
* Un flujo de autenticación basada en web también se puede usar para una página de configuración, un módulo de tarea o una extensión de mensajería.
* Puede usar un flujo de autenticación basada en web para un bot de conversación que tendrá que usar un módulo de tareas.

Según las restricciones de SameSite actualizadas, un explorador no agregará una cookie a un sitio web ya autenticado si el vínculo se deriva de un sitio externo. Deberá asegurarse de que las cookies de autenticación están marcadas para el uso entre `SameSite=None; Secure` sitios (o bien, asegúrese de que haya una reserva en su lugar).

### <a name="android-system-webview"></a>WebView del sistema de Android

Android WebView es un componente del sistema de Chrome que permite que las aplicaciones de Android muestren contenido Web. Aunque las nuevas restricciones se convertirán en las predeterminadas, comenzando con Chrome 80, no se aplicarán de forma inmediata en las vistas de webviews. Se aplicarán en el futuro. Para prepararse, Android permite que las aplicaciones nativas establezcan cookies directamente a través de la [API de CookeManager](https://developer.android.com/reference/android/webkit/CookieManager):

* En el caso de las cookies que solo son necesarias en un contexto de nombre de origen `SameSite=Lax` , `SameSite=Strict`debe declararlas como o, según corresponda.
* En el caso de las cookies necesarias en un contexto de terceros, debe asegurarse de que `SameSite=None; Secure`se declaran como.

## <a name="learn-more"></a>Más información

[Ejemplos de SameSite](https://github.com/GoogleChromeLabs/samesite-examples)

[Recetas de cookies de SameSite](https://web.dev/samesite-cookie-recipes/)

[Clientes incompatibles conocidos]( https://www.chromium.org/updates/same-site/incompatible-clients)

[Desarrolladores: prepararse para el nuevo SameSite = ninguno; Configuración de cookies seguros](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**Impacto de OpenId Connect**<br>
[Próximos cambios en la cookie SameSite en ASP.NET y ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
