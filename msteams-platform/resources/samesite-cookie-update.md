---
title: Microsoft Teams y el atributo de cookie SameSite (actualización de 2020)
author: laujan
description: describe los atributos de la cookie SameSite
keywords: atributos de cookie en el mismo sitio
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: cf28a28050d50b2b6b2601a3231cdad30211ab2c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566715"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teams y el atributo de cookie SameSite (actualización de 2020)

## <a name="cookies-in-brief"></a>Cookies en breve

 Las cookies son cadenas de texto, enviadas desde sitios web y almacenadas en un ordenador por el navegador web. Normalmente se utilizan para la autenticación y la personalización, por ejemplo, recordar información con estado, conservar la configuración del usuario, registrar la actividad de navegación y mostrar anuncios relevantes. Las cookies siempre están vinculadas a un dominio en particular y pueden ser instaladas por varias partes. Se clasifican de la siguiente manera:

 |Cookie|Ámbito|
 | ------ | ------ |
 |**Galleta de primera parte**|Una cookie de origen es creada por sitios web que un usuario visita y se utiliza para guardar datos como artículos del carrito de compras, credenciales de inicio de sesión. Por ejemplo, cookies de autenticación y otros análisis.|
 |**Galleta de segunda parte**|Una cookie de segunda parte es técnicamente la misma que una cookie de origen. La diferencia es que los datos se comparten con una segunda parte a través de un acuerdo de asociación de datos. Por ejemplo, [Microsoft Teams análisis e informes.](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference) |
 |**Galleta de terceros**|Una cookie de terceros es instalada por un dominio distinto del que el usuario visitó explícitamente y se utiliza principalmente para el seguimiento. Por ejemplo, botones "Me gusta", publicación de anuncios y chats en directo.|

### <a name="cookies-and-http-requests"></a>Cookies y solicitudes HTTP

Antes de la introducción de las restricciones de SameSite, cuando las cookies se almacenaban en el navegador, se adjuntaban a *cada* solicitud web HTTP y las enviaba al servidor por el encabezado de respuesta HTTP Set-Cookie. Como era de esperar, ese rendimiento tenía el potencial de introducir vulnerabilidades de seguridad como ataques de falsificación de solicitudes entre sitios (CSRF). *Consulte* [Cookies HTTP](https://developer.mozilla.org/docs/Web/HTTP/Cookies). El componente SameSite mitigó esa exposición a través de su implementación y administración en el encabezado SetCookie.

### <a name="samesite-attribute-initial-release"></a>Atributo SameSite: versión inicial

Google Chrome versión 51 introdujo la especificación SetCookie SameSite como un atributo *opcional.* A partir de Build 17672, Windows 10 introducido el soporte de cookies SameSite para el [navegador Microsoft Edge.](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)

Los desarrolladores podrían optar por no agregar el atributo de cookie SameSite al encabezado SetCookie o podrían agregarlo con una de las dos configuraciones, *Lax* y *Strict.* Un atributo SameSite unmplemented se consideró el estado predeterminado.

## <a name="samesite-cookie-attribute-2020-release"></a>Atributo de cookie SameSite: lanzamiento de 2020

Chrome 80, programado para su lanzamiento en febrero de 2020, introduce nuevos valores de cookies e impone políticas de cookies de forma predeterminada. Tres valores se pueden pasar al atributo SameSite actualizado: *Strict*, *Lax* o *None*. Las cookies que no especifiquen el atributo SameSite tendrán como valor predeterminado `SameSite=Lax` .

|Configuración | aplicación | Valor |Especificación de atributos |
| -------- | ----------- | --------|--------|
| **laxo**  | Las cookies se enviarán automáticamente solo en un contexto *de origen* y con solicitudes HTTP GET. Las cookies samesite se mantendrán en sub-solicitudes entre sitios, como llamadas para cargar imágenes o iframes, pero se enviarán cuando un usuario navegue a la URL desde un sitio externo, por ejemplo, siguiendo un vínculo.| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **estricto** |El navegador solo enviará cookies para solicitudes de contexto de origen de terceros (solicitudes procedentes del sitio que establecen la cookie). Si la solicitud se originó a partir de una URL diferente a la de la ubicación actual, no se enviará ninguna de las cookies etiquetadas con el `Strict` atributo.| Opcional |`Set-Cookie: key=value; SameSite=Strict`|
| **Ninguna** | Las cookies se enviarán tanto en el contexto de origen de terceros como en las solicitudes de origen cruzado; sin embargo, el valor debe establecerse explícitamente **`None`** y todas las solicitudes del explorador deben seguir el protocolo **HTTPS** e incluir el atributo que requiere una **`Secure`** conexión cifrada. Las cookies que no cumplan con ese requisito serán **rechazadas.** <br/>**Ambos atributos son necesarios juntos.** Si **`None`** simplemente se especifica sin **`Secure`**  o si no se utiliza el protocolo HTTPS, se rechazará la cookie de terceros.| Opcional, pero, si se establece, se requiere el protocolo HTTPS. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams implicaciones y ajustes

1. Habilite la configuración relevante de SameSite para sus cookies y valide que sus aplicaciones y extensiones continúan funcionando en Teams.
1. Si tus aplicaciones o extensiones fallan, realiza las correcciones necesarias antes de la versión de Chrome 80.
1. Los socios internos de Microsoft pueden unirse al siguiente equipo si necesitan más información o ayuda con este problema: <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> .

> [!NOTE]
> Para las mejores prácticas, se recomienda que siempre establezca los atributos samesite para reflejar el uso previsto para sus cookies. No confíe en el comportamiento predeterminado del explorador. Para obtener más información, consulte [Desarrolladores: Prepárese para new SameSite=None; Configuración de cookies seguras.](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

### <a name="tabs-task-modules-and-message-extensions"></a>Pestañas, módulos de tareas y extensiones de mensaje

* Teams pestañas se utilizan `<iframes>` para incrustar contenido que se ve en un contexto de nivel superior o de primera parte.
* Los módulos de tareas le permiten crear experiencias emergentes modales en su aplicación de Teams. De forma similar a una pestaña, se abre una ventana modal dentro de la página actual.
* Las extensiones de mensaje le permiten insertar contenido enriquecido en el mensaje de chat desde recursos externos.

Cualquier cookie utilizada por contenido incrustado se considerará de terceros cuando el sitio se muestre en un `<iframe>` archivo . Además, si los recursos remotos de una página dependen de que las cookies se envíen con una solicitud `<img>` y `<script>` etiquetas, fuentes externas y contenido personalizado, debe asegurarse de que están marcadas para su uso entre sitios, como `SameSite=None; Secure` o asegurarse de que hay una reserva.

### <a name="authentication"></a>Autenticación

* Si necesita autenticación para páginas de contenido incrustadas en pestañas, deberá usar el flujo de autenticación basado en web.
* También se puede usar un flujo de autenticación basado en web para una página de configuración, un módulo de tareas o una extensión de mensajería.
* Puede usar un flujo de autenticación basado en web para un bot conversacional que necesitará usar un módulo de tareas.

De conformidad con las restricciones actualizadas de SameSite, un navegador no agregará una cookie a un sitio web ya autenticado si el vínculo deriva de un sitio externo. Deberá asegurarse de que las cookies de autenticación estén marcadas para su uso entre sitios `SameSite=None; Secure` o asegurarse de que hay una reserva.

### <a name="android-system-webview"></a>WebView del sistema Android

Android WebView es un componente del sistema Chrome que permite a las aplicaciones androides mostrar contenido web. Aunque las nuevas restricciones se convertirán en las predeterminadas, empezando por Chrome 80, no se aplicarán inmediatamente en WebViews. Se aplicarán en el futuro. Para prepararse, Android permite a las aplicaciones nativas establecer cookies directamente a través de la [API cookeManager:](https://developer.android.com/reference/android/webkit/CookieManager)

* Para las cookies que solo son necesarias en un contexto de origen, debe declararlas como `SameSite=Lax` `SameSite=Strict` o, según corresponda.
* Para las cookies necesarias en un contexto de terceros, debe asegurarse de que se declaran como `SameSite=None; Secure` .

## <a name="see-also"></a>Vea también

* [Ejemplos samesite](https://github.com/GoogleChromeLabs/samesite-examples)

* [Recetas de galletas SameSite](https://web.dev/samesite-cookie-recipes/)

* [Clientes incompatibles conocidos]( https://www.chromium.org/updates/same-site/incompatible-clients)

* [Desarrolladores: Prepárese para el nuevo SameSite=None; Configuración de cookies seguras](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**Impacto de openid Conectar**<br>
[Próximos cambios de cookies en ASP.NET y ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
