---
title: ¿Qué son las pestañas personalizadas Teams?
author: laujan
description: Introducción a las pestañas personalizadas en la Teams web
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 21499a4e18acee369b4b1bda6184e4b14b6262ec
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629973"
---
# <a name="microsoft-teams-tabs"></a>Pestañas de Microsoft Teams

Las pestañas Teams páginas web que se integran en Microsoft Teams. Son etiquetas sencillas html <iframe que apuntan a dominios declarados en el manifiesto de la aplicación y se pueden agregar como parte de un canal dentro de un equipo, chat de grupo o aplicación personal para un usuario \> individual. Puedes incluir pestañas personalizadas con la aplicación para insertar tu propio contenido web en Teams o agregar una funcionalidad específica Teams al contenido web. Para obtener más información, [vea Teams SDK de cliente de JavaScript](/javascript/api/overview/msteams-client).

Hay dos tipos de pestañas disponibles en Teams: canal/grupo y personal. Las pestañas canal o grupo entregan contenido a canales y chats de grupo, y son una excelente forma de crear espacios de colaboración en torno al contenido basado en web dedicado. Las pestañas personales, junto con los bots de ámbito personal, forman parte de aplicaciones personales y están en el ámbito de un solo usuario. Se pueden anclar a la barra de navegación izquierda para facilitar el acceso.

## <a name="tab-features"></a>Características de tabulación

> [!div class="checklist"]
>
> * Si se agrega una pestaña a una aplicación que también tiene un bot, el bot también se agrega al equipo.
> * Reconocimiento del Azure Active Directory (Azure AD) del usuario actual.
> * Reconocimiento de configuración regional para que el usuario indique el idioma, es decir, `en-us` . 
> * Funcionalidad de inicio de sesión único (SSO), si es compatible.
> * Capacidad de usar bots o notificaciones de aplicaciones para vincular profundamente a la pestaña o a una sub entidad dentro del servicio, por ejemplo, un elemento de trabajo individual.
> * La capacidad de abrir un módulo de tareas desde vínculos dentro de una pestaña.
> * Reutilización de SharePoint web dentro de la pestaña.

## <a name="tabs-user-scenarios"></a>Escenarios de usuario de pestañas

**Escenario:** Lleve un recurso basado en web existente dentro de Teams. \
**Ejemplo:** Creas una pestaña personal en tu aplicación Teams que presenta un sitio web corporativo informativo a los usuarios.

**Escenario:** Agregue páginas de soporte técnico a Teams bot o extensión de mensajería. \
**Ejemplo:** Se crean pestañas personales que proporcionan *información sobre* *el* contenido de la página web y ayudan a los usuarios.

**Escenario:** Proporcionar acceso a elementos con los que los usuarios interactúan regularmente para el diálogo y la colaboración cooperativos. \
**Ejemplo:** Se crea una pestaña de canal o grupo con vínculos profundos a elementos individuales.

## <a name="understand-how-tabs-work"></a>Comprender cómo funcionan las pestañas

Se declara una pestaña personalizada en el manifiesto de la aplicación del paquete de la aplicación. Para cada página web que quieras incluir como pestaña en la aplicación, defines una dirección URL y un ámbito. Además, debe agregar el SDK de cliente Teams [JavaScript a](/javascript/api/overview/msteams-client) la página y llamar después `microsoftTeams.initialize()` de que se cargue la página. Si lo hace, le dirá Teams que muestre su página, le dará acceso a información específica de Teams (por ejemplo, si el cliente de Teams ejecuta el tema *oscuro)* y le permitirá realizar acciones en función de los resultados.

Independientemente de si elige exponer la pestaña dentro del ámbito de canal o grupo o personal, deberá presentar una página de contenido HTML de iframe <en \> la pestaña. [](~/tabs/how-to/create-tab-pages/content-page.md) Para las pestañas personales, la dirección URL de contenido se establece directamente en el manifiesto Teams aplicación mediante la `contentUrl` propiedad de la `staticTabs` matriz. El contenido de la pestaña será el mismo para todos los usuarios.

Para las pestañas de canal o grupo, también debe crear una página de configuración adicional que permita a los usuarios configurar la dirección URL de la página de contenido, normalmente mediante parámetros de cadena de consulta url para cargar el contenido adecuado para ese contexto. Esto se debe a que la pestaña canal o grupo se puede agregar a varios equipos o chats de grupo diferentes. En cada instalación posterior, los usuarios podrán configurar la pestaña, lo que le permitirá adaptar la experiencia según sea necesario. Cuando los usuarios agregan o configuran una pestaña, se asocia una dirección URL a la pestaña que se presenta en la interfaz Teams usuario. Configurar una pestaña es simplemente agregar parámetros adicionales a esa dirección URL. Por ejemplo, al agregar la pestaña Azure Boards, la página de configuración le permite elegir qué placa se cargará la pestaña. La dirección URL de la página de configuración la especifica la  `configurationUrl` propiedad en la `configurableTabs` matriz del manifiesto de la aplicación.

Puedes tener varios canales o pestañas de grupo y hasta dieciséis pestañas personales por aplicación.

## <a name="mobile-considerations"></a>Consideraciones móviles

Si decide que la pestaña canal o grupo aparezca en Teams móviles, la configuración debe tener un `setSettings()` valor para la `websiteUrl` propiedad. Para garantizar una experiencia de usuario óptima, debe seguir las instrucciones para las [pestañas](~/tabs/design/tabs-mobile.md) en el móvil al crear las pestañas. Las [aplicaciones distribuidas a Teams tienda tienen](~/concepts/deploy-and-publish/appsource/publish.md) un proceso de aprobación independiente para clientes móviles. El comportamiento predeterminado de estas aplicaciones es el siguiente:

| **Funcionalidad de la aplicación** | **Comportamiento si la aplicación está aprobada** | **Comportamiento si la aplicación no está aprobada** |
| --- | --- | --- |
| **Pestañas personales** | La aplicación aparece en la barra inferior de los clientes móviles. Las pestañas se abren en Teams cliente. | La aplicación no aparece en la barra inferior de los clientes móviles. |
| **Pestañas canal y grupo** | La pestaña se abre en el Teams mediante `contentUrl` . | La pestaña se abre en un explorador fuera del Teams con `websiteUrl` . |

> [!NOTE]
>
> El comportamiento predeterminado de las aplicaciones solo es aplicable si se distribuye a través Teams tienda. De forma predeterminada, todas las pestañas se abren en el Teams cliente.
> Para iniciar una evaluación de la aplicación para la facilidad de uso móvil, teamsubm@microsoft.com con los detalles de la aplicación.

## <a name="see-also"></a>Vea también

* [Solicitar permisos de dispositivo](../concepts/device-capabilities/native-device-permissions.md)
* [Integrar capacidades multimedia](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Integrar un escáner qr o de código de barras](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Integrar capacidades de ubicación](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Requisitos de pestaña](~/tabs/how-to/tab-requirements.md)
