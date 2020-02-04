---
title: Vista previa para desarrolladores
description: Describe las características de la versión preliminar para desarrolladores públicos de Microsoft Teams.
keywords: características para desarrolladores de Team Preview
ms.openlocfilehash: a09e715e4e2d4aba72726cc96c4d248c550a3ab1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676003"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Versión preliminar para desarrolladores públicos para Microsoft Teams

>[!NOTE]
>Las características incluidas en la versión preliminar pueden no estar completas y pueden sufrir cambios antes de que estén disponibles en la versión pública. Se proporcionan solo con fines de prueba y exploración. No deben usarse en las aplicaciones de producción.

Developer Preview es un programa público para desarrolladores que proporciona acceso anticipado a características no publicadas en Microsoft Teams. Esto le permite explorar y probar las próximas características para obtener una inclusión potencial en su aplicación de Microsoft Teams. También le damos la bienvenida a [comentarios](~/feedback.md) sobre cualquier característica en Developer Preview. La vista previa para desarrolladores está habilitada por el cliente de Microsoft Teams, por lo que no tiene que preocuparse por afectar a toda la organización.

## <a name="developer-preview-app-manifest"></a>Manifiesto de la aplicación de vista previa para desarrolladores

Muchas de las características que se habilitan en la vista previa para desarrolladores requerirán alteraciones en el archivo JSON del manifiesto de la aplicación. Para ello, necesitará usar el esquema del [manifiesto de vista previa de desarrollador](~/resources/schema/manifest-schema-dev-preview.md) si usa este esquema, no podrá usar [App Studio](~/concepts/build-and-test/app-studio-overview.md) para realizar estos cambios, ni podrá usarlo para cargar la aplicación para realizar pruebas. Para cargar la aplicación, deberá hacer clic en el `More apps` icono de la barra de la aplicación y, `Upload a custom app link`a continuación, seleccionar el. Con este método solo puede cargar una versión comprimida del paquete de la aplicación.

Puede que le resulte útil usar App Studio para crear las partes no de vista previa para desarrolladores del paquete de la aplicación, exportar el paquete y editar `manifest.json` manualmente el archivo para agregar las características de vista previa para desarrolladores que desea usar. Una vez que haya agregado las características de vista `manifest.json` previa para desarrolladores al archivo, no podrá volver a importar el paquete en App Studio.

## <a name="enable-developer-preview"></a>Habilitar la vista previa para desarrolladores

La vista previa para desarrolladores está habilitada para cada cliente, pero la opción de activar la vista previa para desarrolladores se controla en el nivel de la organización. Para habilitar la opción de activar la vista previa para desarrolladores para un usuario individual, debe asegurarse de que tienen la capacidad de cargar aplicaciones personalizadas. Consulte [configuración del espacio empresarial](~/concepts/build-and-test/prepare-your-o365-tenant.md) para obtener información adicional.

El uso de una aplicación que contiene características de vista previa para desarrolladores puede hacer que los clientes que no hayan habilitado la vista previa para desarrolladores se comporten de manera inesperada. Si no ve una entrada para Developer Preview, la razón más probable es que su organización no esté configurada para la carga de aplicaciones.

### <a name="on-a-desktop-or-web-client"></a>En un cliente de escritorio o Web

Para habilitar la vista previa para desarrolladores públicos en un cliente de escritorio o Web, debe hacer lo siguiente:

1. Habilitar la carga de aplicaciones en la consola de administración del inquilino como se describe [aquí](~/concepts/build-and-test/prepare-your-o365-tenant.md).
1. Haga clic en su perfil (ya sea en la esquina superior derecha o en la parte inferior izquierda de la interfaz de Teams) para mostrar el menú de Microsoft Teams.
1. Seleccione información sobre → vista previa para desarrolladores.
1. Seleccione **cambiar a vista previa para desarrolladores**.

### <a name="on-a-mobile-client"></a>En un cliente móvil

Para habilitar la vista previa para desarrolladores públicos en un cliente móvil, debe hacer lo siguiente:

1. Habilitar la carga de aplicaciones en la consola de administración del inquilino como se describe [aquí](~/concepts/build-and-test/prepare-your-o365-tenant.md).
1. Abra el menú hamburguesa en la parte superior izquierda y, a continuación, seleccione **configuración**.
1. Seleccione **acerca de**.
1. Haga clic en el botón de alternancia vista previa para desarrolladores.

## <a name="disable-developer-preview"></a>Deshabilitar la vista previa para desarrolladores

Use el mismo elemento de menú en about → Developer Preview y haga clic en él para desactivarlo.

## <a name="features-available-in-developer-preview"></a>Características disponibles en la vista previa para desarrolladores

Para obtener una lista completa de las características actualmente habilitadas en Developer Preview, vea: [Features in Public Developer Preview](../../resources/dev-preview/developer-preview-features.md).
