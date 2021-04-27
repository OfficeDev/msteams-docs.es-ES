---
title: Microsoft Teams y el atributo cookie SameSite (actualización de 2020)
author: laujan
description: describe los atributos de la cookie SameSite
keywords: atributos cookie samesite
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 5713c7aae0461e577627ae7296f0a58a25ba062f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020439"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teams y el atributo cookie SameSite (actualización de 2020)

## <a name="cookies-in-brief"></a>Cookies breves

 Las cookies son cadenas de texto, enviadas desde sitios web y almacenadas en un equipo por el explorador web. Normalmente se usan para la autenticación y personalización, por ejemplo, recuperar información con estado, conservar la configuración del usuario, registrar la actividad de exploración y mostrar anuncios relevantes. Las cookies siempre están vinculadas a un dominio determinado y pueden ser instaladas por varias partes. Se clasifican de la siguiente manera:

 |Cookie|Ámbito|
 | ------ | ------ |
 |**Cookie de primera persona**|Los sitios web que visita un usuario crean una cookie de origen y se usa para guardar datos como elementos del carro de la compra, credenciales de inicio de sesión (por ejemplo, cookies de autenticación) y otros análisis.|
 |**Cookie de terceros**|Las cookies de terceros son técnicamente las mismas que las cookies de terceros. La diferencia es que los datos se comparten con una segunda parte a través de un contrato de asociación de datos (por ejemplo, análisis [e informes de Microsoft Teams).](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference) |
 |**Cookie de terceros**|Un dominio distinto del que visitó explícitamente una cookie de terceros se instala y se usa principalmente para el seguimiento (por ejemplo, los botones "Me gusta"), la función de anuncios y los chats en directo.|

### <a name="cookies-and-http-requests"></a>Cookies y solicitudes HTTP

Antes de la introducción de las restricciones samesite, cuando las cookies se almacenaban en el explorador, se adjuntaban a cada solicitud web *HTTP* y se enviaban al servidor mediante el encabezado de respuesta HTTP Set-Cookie http. Previsiblemente, ese rendimiento tenía el potencial de introducir vulnerabilidades de seguridad, como ataques de falsificación de solicitudes entre sitios (CSRF). *Consulte* [Cookies HTTP](https://developer.mozilla.org/docs/Web/HTTP/Cookies). El componente SameSite mitigaba esa exposición a través de su implementación y administración en el encabezado SetCookie.

### <a name="samesite-attribute-initial-release"></a>Atributo SameSite: versión inicial

Google Chrome versión 51 introdujo la especificación SetCookie SameSite como *un atributo* opcional. A partir de la compilación 17672, Windows 10 introdujo la compatibilidad con cookies SameSite para el [explorador Microsoft Edge](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/).

Los desarrolladores podrían optar por no agregar el atributo cookie SameSite al encabezado SetCookie o podrían agregarlo con una de las dos opciones de configuración, *Lax* y *Strict*. Un atributo SameSite sin implementar se consideró el estado predeterminado.

## <a name="samesite-cookie-attribute-2020-release"></a>Atributo cookie SameSite: versión 2020

Chrome 80, programado para su lanzamiento en febrero de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se pueden pasar tres valores al atributo SameSite actualizado: *Strict*, *Lax* o *None*. Las cookies que no especifican el atributo SameSite se establecerán de forma predeterminada en `SameSite=Lax` .

|Valor | Aplicación | Valor |Especificación de atributos |
| -------- | ----------- | --------|--------|
| **Lax**  | Las cookies se enviarán automáticamente solo en un contexto *de origen* y con solicitudes HTTP GET. Las cookies de SameSite se retienen en solicitudes entre sitios, como llamadas para cargar imágenes o iframes, pero se enviarán cuando un usuario navegue a la dirección URL desde un sitio externo, por ejemplo, siguiendo un vínculo.| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Estricto** |El explorador solo enviará cookies para solicitudes de contexto de origen (solicitudes que se originaron desde el sitio que establece la cookie). Si la solicitud se originó desde una dirección URL diferente a la de la ubicación actual, no se enviará ninguna de las cookies `Strict` etiquetadas con el atributo.| Opcional |`Set-Cookie: key=value; SameSite=Strict`|
| **Ninguna** | Las cookies se enviarán tanto en el contexto de origen como en las solicitudes entre orígenes; sin embargo, el valor debe establecerse explícitamente en y todas las solicitudes de explorador deben seguir el protocolo HTTPS e incluir el **`None`** atributo que requiere una conexión  **`Secure`** cifrada. Las cookies que no cumplan con ese requisito se **rechazarán**. <br/>**Ambos atributos son necesarios juntos.** Si solo se especifica sin o si no se usa el protocolo HTTPS, se rechazará la **`None`** **`Secure`**  cookie de terceros.| Opcional, pero, si se establece, se requiere el protocolo HTTPS. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="handling-incompatible-clients"></a>Controlar clientes incompatibles

> [!IMPORTANT]
> Actualmente, no es compatible con el cliente de escritorio de Teams ni con versiones `SameSite=None` anteriores de Chrome o Safari. [](/aspnet/core/security/samesite?view=aspnetcore-3.1#test-with-electron&preserve-view=true) **Consulte** [Clientes incompatibles conocidos]( https://www.chromium.org/updates/same-site/incompatible-clients).
>Sin embargo, hay dos soluciones **alternativas:**
>
>1. Compruebe el agente de usuario para proporcionar la propiedad SameSite correcta. Puede implementar la comprobación de agente de usuario [**C#**](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/) y [**Node.js**](https://web.dev/samesite-cookie-recipes/).
>2. Establece los atributos de cookie con los modelos nuevos y antiguos. *Consulte Control* [de clientes incompatibles](https://web.dev/samesite-cookie-recipes/#handling-incompatible-clients)<br><br>
>**Si la aplicación se ejecuta en el cliente de escritorio de Teams y estableces el atributo SameSite en , la aplicación `SameSite=None` no funcionará como se esperaba.**

El uso de cualquiera de los métodos garantizará que la aplicación siga funcionando correctamente cuando el cliente de escritorio de Teams se actualice a una `SameSite=None`   versión compatible de Chromium.

## <a name="teams-implications-and-adjustments"></a>Implicaciones y ajustes de Teams

>[!WARNING]
>**Las aplicaciones que se ejecutan en el cliente de escritorio de Teams son incompatibles con el `SameSite=None`  atributo y no funcionarán como se esperaba.** Consulte las soluciones **alternativas** anteriores.

1. Habilita la configuración de SameSite relevante para las cookies y valida que tus aplicaciones y extensiones sigan funcionando en Teams.
1. Si las aplicaciones o las extensiones fallan, realiza las correcciones necesarias antes de la versión de Chrome 80.
1. Los partners internos de Microsoft pueden unirse al siguiente equipo si necesitan más información o ayuda con este problema: <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> .

> [!NOTE]
> Para los procedimientos recomendados, se recomienda establecer siempre los atributos SameSite para reflejar el uso previsto para las cookies, ya que no se basan en el comportamiento predeterminado del explorador. *Vea* [Developers: Get Ready for New SameSite=None; Configuración de cookie segura](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-message-extensions"></a>Pestañas, módulos de tareas y extensiones de mensaje

* Las pestañas de Teams se usan para insertar contenido que se ve en un contexto de primer `<iframes>` nivel o de primera.
* Los módulos de tareas le permiten crear experiencias emergentes modales en su aplicación de Teams. De forma similar a una pestaña, se abre una ventana modal dentro de la página actual.
* Las extensiones de mensajes permiten insertar contenido enriquecido en un mensaje de chat desde recursos externos.

Las cookies usadas por el contenido incrustado se considerarán de terceros cuando el sitio se muestre en un `<iframe>` archivo . Además, si algún recurso remoto de una página se basa en las cookies que se envían con una solicitud (por ejemplo, etiquetas, fuentes externas y contenido personalizado), deberá asegurarse de que están marcadas para el uso entre sitios , o asegurarse de que hay una `<img>` `<script>` `SameSite=None; Secure` reserva.

### <a name="authentication"></a>Autenticación

* Si necesita autenticación para páginas de contenido incrustadas en pestañas, deberá usar el flujo de autenticación basado en web.
* También se puede usar un flujo de autenticación basado en web para una página de configuración, un módulo de tareas o una extensión de mensajería.
* Puedes usar un flujo de autenticación basado en web para un bot de conversación que necesitarás usar un módulo de tareas.

De acuerdo con las restricciones de SameSite actualizadas, un explorador no agregará una cookie a un sitio web ya autenticado si el vínculo deriva de un sitio externo. Deberá asegurarse de que las cookies de autenticación están marcadas para el uso entre sitios, o asegurarse de que hay una `SameSite=None; Secure` reserva.

### <a name="android-system-webview"></a>Android System WebView

Android WebView es un componente del sistema Chrome que permite a las aplicaciones Android mostrar contenido web. Aunque las nuevas restricciones se convertirán en el valor predeterminado, a partir de Chrome 80, no se aplicarán inmediatamente en WebViews. Se aplicarán en el futuro. Para prepararse, Android permite que las aplicaciones nativas establezcan cookies directamente a través de la [API de CookeManager:](https://developer.android.com/reference/android/webkit/CookieManager)

* Para las cookies que solo son necesarias en un contexto de primera persona, debe declararlas como `SameSite=Lax` o `SameSite=Strict` , según corresponda.
* Para las cookies necesarias en un contexto de terceros, debe asegurarse de que se declaran como `SameSite=None; Secure` .

## <a name="learn-more"></a>Más información

[Ejemplos de SameSite](https://github.com/GoogleChromeLabs/samesite-examples)

[Recetas de cookies de SameSite](https://web.dev/samesite-cookie-recipes/)

[Clientes incompatibles conocidos]( https://www.chromium.org/updates/same-site/incompatible-clients)

[Desarrolladores: Prepárese para new SameSite=None; Configuración de cookies seguras](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**Impacto de OpenId Connect**<br>
[Próximos cambios de cookies de SameSite en ASP.NET y ASP.NET core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
