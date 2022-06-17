---
title: Pestañas en dispositivos móviles
description: En este módulo, obtenga información sobre la implementación de pestañas en Microsoft Teams móvil, su autenticación, conexión de ancho de banda bajo, pruebas en clientes móviles, distribución y mucho más.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: da9757ee0153b3f2fe80e576e156f45bc90a15cd
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144279"
---
# <a name="tabs-on-mobile"></a>Pestañas en dispositivos móviles

Al compilar una aplicación de Microsoft Teams que incluye una pestaña, debe probar cómo funciona la pestaña en los clientes Android y iOS Microsoft Teams. En este artículo se describen algunos de los escenarios clave que debe tener en cuenta.

Si decide que la pestaña de canal o grupo aparezca en Teams clientes móviles, la [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) configuración debe tener un valor para la `websiteUrl` propiedad . Para garantizar una experiencia de usuario óptima, debe seguir las instrucciones de las pestañas en el móvil de este artículo al crear las pestañas.

Las aplicaciones [distribuidas a través de la tienda Teams](~/concepts/deploy-and-publish/appsource/publish.md) tienen un proceso de aprobación independiente para los clientes móviles. El comportamiento predeterminado de estas aplicaciones es el siguiente:

| **Funcionalidad de la aplicación** | **Comportamiento si se aprueba la aplicación** | **Comportamiento si no se aprueba la aplicación** |
| --- | --- | --- |
| **Pestañas personales** | La aplicación aparece en la barra inferior de los clientes móviles. Las pestañas se abren en el cliente Teams. | La aplicación no aparece en la barra inferior de los clientes móviles. |
| **Pestañas de canal y grupo** | La pestaña se abre en el cliente Teams mediante `contentUrl`. | La pestaña se abre en un explorador fuera del cliente de Teams mediante `websiteUrl`. |

> [!NOTE]
>
> * Las aplicaciones enviadas a [AppSource](https://appsource.microsoft.com) para su publicación en Teams se evalúan automáticamente para la capacidad de respuesta móvil. Para cualquier consulta, póngase en contacto con teamsubm@microsoft.com.
> * Para todas las aplicaciones que no se distribuyen a través de AppSource, las pestañas se abren en una vista web dentro de la aplicación dentro de los clientes Teams de forma predeterminada y no se requiere ningún proceso de aprobación independiente.
> * El comportamiento predeterminado de las aplicaciones solo es aplicable si se distribuye a través del almacén de Teams. De forma predeterminada, todas las pestañas se abren en el cliente de Teams.
> * Para iniciar una evaluación de la aplicación para la facilidad de uso móvil, póngase en contacto con teamsubm@microsoft.com con los detalles de la aplicación.

## <a name="authentication"></a>Autenticación

Para que la autenticación funcione en clientes móviles, debe actualizar Teams SDK de JavaScript a al menos la versión 1.4.1.

## <a name="low-bandwidth-and-intermittent-connections"></a>Ancho de banda bajo y conexiones intermitentes

Los clientes móviles funcionan con un ancho de banda bajo y conexiones intermitentes. La aplicación debe controlar los tiempos de espera correctamente proporcionando un mensaje contextual al usuario. También debe usar indicadores de progreso para proporcionar comentarios a los usuarios sobre los procesos de ejecución prolongada.

## <a name="testing-on-mobile-clients"></a>Pruebas en clientes móviles

Debe validar que la pestaña funciona correctamente en dispositivos móviles de varios tamaños y calidades. Para Android dispositivos, puede usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se está ejecutando. Se recomienda probar en dispositivos de alto y bajo rendimiento, incluida una tableta.

## <a name="distribution"></a>Distribución

Las aplicaciones que aparecen en la tienda de Teams deben aprobarse para que el uso móvil funcione correctamente en el cliente móvil de Teams. La disponibilidad y el comportamiento de las pestañas depende de si la aplicación está aprobada.

### <a name="apps-on-teams-store-approved-for-mobile"></a>Aplicaciones en Teams tienda aprobadas para dispositivos móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la tienda Teams y se aprueba para su uso móvil:

|Funcionalidad   |¿Disponibilidad móvil?   |Comportamiento móvil|
|----------|-----------|------------|
|Canal <br /> y pestaña de grupo|Sí|La pestaña se abre en el cliente móvil de Teams mediante la configuración de la `contentUrl` aplicación.|
|Aplicación personal|Sí|Cada pestaña de la pestaña aplicación personal se abre en el Teams cliente móvil con su configuración respectiva`contentUrl`.|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Aplicaciones en Teams tienda no aprobadas para dispositivos móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la tienda de Teams, pero no se aprueba para su uso móvil:

| Funcionalidad | ¿Disponibilidad móvil? | Comportamiento móvil |
|----------|-----------|------------|
|Pestaña Canal y grupo|Sí|La pestaña se abre en el explorador predeterminado del dispositivo en lugar del Teams cliente móvil mediante la configuración de la `websiteUrl` aplicación, que también debe incluirse en la [función](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace) del `setSettings()` código fuente. Sin embargo, los usuarios pueden ver la pestaña en el Teams cliente móvil seleccionando **Más** junto a la aplicación y eligiendo **Abrir**, lo que desencadena la configuración de la `contentUrl` aplicación.|
|Aplicación personal|No|No aplicable|

### <a name="apps-not-on-teams-store"></a>Aplicaciones que no están en Teams tienda

Si va a transferir localmente la aplicación o publicarla en el catálogo de aplicaciones de una organización, el comportamiento de las pestañas es el mismo que Teams aplicaciones de la Tienda aprobadas por Microsoft para dispositivos móviles.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Obtención del contexto de Teams para la pestaña](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>Consulte también

* [Directrices de diseño de pestañas](~/tabs/design/tabs.md)
* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o de canal](~/tabs/how-to/create-channel-group-tab.md)
* [Planeamiento de Teams móvil: Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
