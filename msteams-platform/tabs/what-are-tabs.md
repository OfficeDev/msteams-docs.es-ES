---
title: ¿Qué son las pestañas personalizadas en Teams?
author: laujan
description: Una visión general de las pestañas personalizadas en la plataforma de Teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 19c51d5c30f938dc5368b28b69ffeb29330887b4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566596"
---
# <a name="microsoft-teams-tabs"></a>Pestañas de Microsoft Teams

Las pestañas son páginas web Teams compatibles incrustadas en Microsoft Teams. Son etiquetas html simples <iframe \> que apuntan a dominios declarados en el manifiesto de la aplicación y se pueden agregar como parte de un canal dentro de un equipo, chat de grupo o aplicación personal para un usuario individual. Puede incluir pestañas personalizadas con la aplicación para incrustar su propio contenido web en Teams o agregar funcionalidad específica de Teams a su contenido web. Para obtener más información, consulte [Teams SDK de cliente de JavaScript](/javascript/api/overview/msteams-client).

Hay dos tipos de pestañas disponibles en Teams: canal/grupo y personal. Las pestañas de canal/grupo entregan contenido a canales y chats grupales, y son una excelente manera de crear espacios colaborativos en torno al contenido basado en web dedicado. Las pestañas personales, junto con los bots de ámbito personal, forman parte de aplicaciones personales y están seleccionadas para un solo usuario. Se pueden fijar a la barra de navegación izquierda para facilitar el acceso.

## <a name="tab-features"></a>Características de la pestaña

> [!div class="checklist"]
>
> * Si se agrega una pestaña a una aplicación que también tiene un bot, el bot también se agrega al equipo.
> * Conocimiento del identificador de Azure Active Directory (Azure AD) del usuario actual.
> * Reconocimiento de la configuración regional para que el usuario indique el idioma, es decir, `en-us` . 
> * Capacidad de inicio de sesión único (SSO), si es compatible.
> * Capacidad de usar bots o notificaciones de aplicaciones para vincular profundamente a la pestaña o a una subentulación dentro del servicio, por ejemplo, un elemento de trabajo individual.
> * La capacidad de abrir un módulo de tareas desde vínculos dentro de una pestaña.
> * Reutilización de SharePoint elementos web dentro de la pestaña.

## <a name="tabs-user-scenarios"></a>Tabula escenarios de usuario

**Escenario:** Traiga un recurso basado en web existente dentro de Teams. \
**Ejemplo:** Creas una pestaña personal en tu aplicación de Teams que presenta un sitio web corporativo informativo a los usuarios.

**Escenario:** Agregue páginas de soporte técnico a una Teams bot o extensión de mensajería. \
**Ejemplo:** Las pestañas personales sobre las que *se* proporciona y *ayuda* al contenido de la página web ayudan a los usuarios.

**Escenario:** Proporcione acceso a los elementos con los que interactúan los usuarios regularmente para el diálogo cooperativo y la colaboración. \
**Ejemplo:** Cree una pestaña de canal/grupo con vinculación profunda a elementos individuales.

## <a name="understand-how-tabs-work"></a>Entender cómo funcionan las pestañas

Se declara una pestaña personalizada en el manifiesto de aplicación del paquete de la aplicación. Para cada página web que desee incluir como pestaña en la aplicación, defina una dirección URL y un ámbito. Además, debe agregar el [SDK de cliente de JavaScript Teams](/javascript/api/overview/msteams-client) a la página y llamar después de cargar la `microsoftTeams.initialize()` página. Al hacerlo, se indicará a Teams que muestre la página, le dará acceso a información específica de Teams (por ejemplo, si el cliente Teams está ejecutando el *tema oscuro)* y le permitirá tomar medidas en función de los resultados.

Ya sea que elijas exponer tu pestaña dentro del canal/grupo o el ámbito personal, deberás presentar una página de contenido HTML de iframe <\> en tu pestaña. [](~/tabs/how-to/create-tab-pages/content-page.md) Para pestañas personales, la dirección URL del contenido se establece directamente en el manifiesto de la aplicación Teams por la `contentUrl` propiedad de la `staticTabs` matriz. El contenido de la pestaña será el mismo para todos los usuarios.

Para las pestañas de canal/grupo, también debe crear una página de configuración adicional que permita a los usuarios configurar la dirección URL de la página de contenido, normalmente mediante parámetros de cadena de consulta de DIRECCIÓN URL para cargar el contenido adecuado para ese contexto. Esto se debe a que la pestaña canal/grupo se puede agregar a varios equipos diferentes o chats de grupo. En cada instalación posterior, los usuarios podrán configurar la pestaña, lo que le permitirá adaptar la experiencia según sea necesario. Cuando los usuarios agregan o configuran una pestaña, se asocia una dirección URL a la pestaña que se presenta en la interfaz de usuario de Teams. Configurar una pestaña es simplemente agregar parámetros adicionales a esa DIRECCIÓN URL. Por ejemplo, al agregar la pestaña Azure Boards, la página de configuración le permite elegir qué placa se cargará la pestaña. La propiedad de la matriz especifica la dirección URL de la página de configuración  `configurationUrl` en el manifiesto de la `configurableTabs` aplicación.

Puede tener varios canales o pestañas de grupo, y hasta dieciséis pestañas personales por aplicación.

## <a name="mobile-considerations"></a>Consideraciones móviles

Si decide que la pestaña de canal o grupo aparezca en Teams clientes móviles, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad. Para garantizar una experiencia de usuario óptima, debe seguir las [instrucciones de las pestañas en el móvil](~/tabs/design/tabs-mobile.md) al crear las pestañas. Las aplicaciones [distribuidas a través de la tienda Teams](~/concepts/deploy-and-publish/appsource/publish.md) tienen un proceso de aprobación independiente para los clientes móviles. El comportamiento predeterminado de estas aplicaciones es el siguiente:

| **Capacidad de la aplicación** | **Comportamiento si se aprueba la aplicación** | **Comportamiento si la aplicación no está aprobada** |
| --- | --- | --- |
| **Pestañas personales** | La aplicación aparece en la barra inferior de los clientes móviles. Las pestañas se abren en el cliente Teams. | La aplicación no aparece en la barra inferior de los clientes móviles. |
| **Pestañas de canal y grupo** | La pestaña se abre en el cliente Teams mediante `contentUrl` . | La pestaña se abre en un explorador fuera del cliente Teams mediante `websiteUrl` . |

> [!NOTE]
>
> El comportamiento predeterminado de las aplicaciones solo es aplicable si se distribuye a través de la tienda Teams. De forma predeterminada, todas las pestañas se abren en el cliente Teams.
> Para iniciar una evaluación de su aplicación para la facilidad de uso móvil, póngase en contacto con teamsubm@microsoft.com con los detalles de la aplicación.

## <a name="see-also"></a>Vea también

* [Solicitar permisos de dispositivo](../concepts/device-capabilities/native-device-permissions.md)
* [Integrar capacidades multimedia](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Integrar un escáner QR o de código de barras](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Integrar capacidades de ubicación](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Requisitos de pestaña](~/tabs/how-to/tab-requirements.md)