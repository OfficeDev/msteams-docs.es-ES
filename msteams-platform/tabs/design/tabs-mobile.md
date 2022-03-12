---
title: Pestañas en dispositivos móviles
description: Obtenga información sobre cómo implementar pestañas en Microsoft Teams móvil, su autenticación, conexión de ancho de banda bajo, pruebas en clientes móviles, distribución y mucho más.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Distribución de autenticación de grupo de canal de pestaña móvil de la aplicación
ms.openlocfilehash: 520cad9d295b4f63ca437db5f69abc3ba9464faa
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452595"
---
# <a name="tabs-on-mobile"></a>Pestañas en dispositivos móviles

Cuando crees una aplicación Microsoft Teams que incluya una pestaña, debes probar cómo funciona la pestaña en los clientes de Android y Microsoft Teams iOS. En este artículo se describen algunos de los escenarios clave que debe tener en cuenta.

Si decide que la pestaña canal o grupo aparezca en Teams móviles, [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) la configuración debe tener un valor para la `websiteUrl` propiedad. Para garantizar una experiencia de usuario óptima, debe seguir las instrucciones para las pestañas en el móvil de este artículo al crear las pestañas.

Las [aplicaciones distribuidas a Teams store tienen](~/concepts/deploy-and-publish/appsource/publish.md) un proceso de aprobación independiente para clientes móviles. El comportamiento predeterminado de estas aplicaciones es el siguiente:

| **Funcionalidad de la aplicación** | **Comportamiento si la aplicación está aprobada** | **Comportamiento si la aplicación no está aprobada** |
| --- | --- | --- |
| **Pestañas personales** | La aplicación aparece en la barra inferior de los clientes móviles. Las pestañas se abren en Teams cliente. | La aplicación no aparece en la barra inferior de los clientes móviles. |
| **Pestañas canal y grupo** | La pestaña se abre en el Teams con `contentUrl`. | La pestaña se abre en un explorador fuera del Teams mediante `websiteUrl`. |

> [!NOTE]
>
> * Las aplicaciones enviadas a [AppSource](https://appsource.microsoft.com) para su publicación en Teams se evalúan automáticamente para la capacidad de respuesta móvil. Para cualquier consulta, llegue a teamsubm@microsoft.com.
> * Para todas las aplicaciones que no se distribuyen a través de AppSource, las pestañas se abren en una vista web desde la aplicación dentro de los clientes de Teams de forma predeterminada y no se requiere ningún proceso de aprobación independiente.
> * El comportamiento predeterminado de las aplicaciones solo es aplicable si se distribuye a través Teams tienda. De forma predeterminada, todas las pestañas se abren en el Teams cliente.
> * Para iniciar una evaluación de la aplicación para la facilidad de uso móvil, teamsubm@microsoft.com con los detalles de la aplicación.

## <a name="authentication"></a>Autenticación

Para que la autenticación funcione en clientes móviles, debe actualizar Teams SDK de JavaScript a al menos la versión 1.4.1.

## <a name="low-bandwidth-and-intermittent-connections"></a>Ancho de banda bajo y conexiones intermitentes

Los clientes móviles funcionan con un ancho de banda bajo y conexiones intermitentes. La aplicación debe controlar los tiempos de espera correctamente proporcionando un mensaje contextual al usuario. También debe usar indicadores de progreso para proporcionar comentarios a los usuarios para los procesos de larga ejecución.

## <a name="testing-on-mobile-clients"></a>Pruebas en clientes móviles

Debes validar que la pestaña funciona correctamente en dispositivos móviles de distintos tamaños y calidades. Para dispositivos Android, puedes usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se ejecuta. Se recomienda probar en dispositivos de alto y bajo rendimiento, incluida una tableta.

## <a name="distribution"></a>Distribución

Las aplicaciones que aparecen en la Teams deben aprobarse para que el uso móvil funcione correctamente en el Teams móvil. La disponibilidad y el comportamiento de las pestañas depende de si la aplicación está aprobada.

### <a name="apps-on-teams-store-approved-for-mobile"></a>Aplicaciones en la Teams aprobadas para dispositivos móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la Teams y se aprueba para uso móvil:

|Funcionalidad   |¿Disponibilidad móvil?   |Comportamiento móvil|
|----------|-----------|------------|
|Canal <br /> y ficha grupo|Sí|La pestaña se abre en el Teams móvil mediante la configuración de la `contentUrl` aplicación.|
|Aplicación personal|Sí|Cada pestaña de la pestaña aplicación personal se abre en el Teams móvil mediante su configuración `contentUrl` respectiva.|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Aplicaciones de Teams no aprobadas para móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la Teams pero no se aprueba para el uso móvil:

| Funcionalidad | ¿Disponibilidad móvil? | Comportamiento móvil |
|----------|-----------|------------|
|Pestaña Canal y grupo|Sí|La pestaña se abre en el explorador predeterminado del dispositivo en `websiteUrl` lugar del cliente móvil de Teams mediante la configuración de la aplicación, que también debe incluirse en la función del `setSettings()` código [fuente](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace). Sin embargo, los usuarios pueden ver la pestaña en el cliente móvil de Teams seleccionando Más  junto a la aplicación y **seleccionando Abrir**, lo que desencadena la configuración de la `contentUrl` aplicación.|
|Aplicación personal|No|No aplicable|

### <a name="apps-not-on-teams-store"></a>Aplicaciones que no están Teams tienda

Si vas a descargar localmente la aplicación o publicarla en el catálogo de aplicaciones de una organización, el comportamiento de las pestañas es el mismo que las aplicaciones de la tienda Teams aprobadas por Microsoft para dispositivos móviles.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Obtención del contexto de Teams para la pestaña](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>Vea también

* [Directrices de diseño de pestañas](~/tabs/design/tabs.md)
* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Plan for Teams mobile - Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
