---
title: Developer Preview
description: Describe las características de la versión preliminar para desarrolladores públicos de Microsoft Teams
ms.topic: conceptual
keywords: Características para desarrolladores de vista previa de teams
ms.openlocfilehash: b8e8847d71ec3a571d434f952c79f3dd6a8f5bf1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014078"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Versión preliminar para desarrolladores públicos de Microsoft Teams

>[!NOTE]
>Es posible que las características incluidas en la versión preliminar no estén completas y que se someta a cambios antes de estar disponibles en la versión pública. Solo se proporcionan con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

Developer Preview es un programa público para desarrolladores que proporciona acceso anticipado a las características no publicados en Microsoft Teams. Esto le permite explorar y probar las próximas características para su posible inclusión en su aplicación de Microsoft Teams. También agradecemos los [comentarios sobre](~/feedback.md) cualquier característica de la versión preliminar del desarrollador. La vista previa del desarrollador está habilitada para cada cliente de Microsoft Teams, por lo que no es necesario preocuparse por afectar a toda la organización.

## <a name="developer-preview-app-manifest"></a>Manifiesto de la aplicación de vista previa del desarrollador

Muchas características habilitadas en la vista previa del desarrollador requerirán modificaciones en el archivo JSON del manifiesto de la aplicación. Para ello, tendrás que usar [](~/resources/schema/manifest-schema-dev-preview.md) el esquema de manifiesto de versión preliminar del desarrollador Si usas este esquema, no podrás usar [App Studio](~/concepts/build-and-test/app-studio-overview.md) para realizar estos cambios, ni podrás usarlo para cargar la aplicación para realizar pruebas. Para cargar la aplicación, tendrás que hacer clic en el icono de la barra de la aplicación y, a `More apps` continuación, seleccionar el archivo `Upload a custom app link` . Con este método solo puedes cargar una versión comprimida del paquete de la aplicación.

Es posible que te sea útil usar App Studio para crear las partes de vista previa que no son para desarrolladores del paquete de la aplicación y, a continuación, exportar ese paquete y editar manualmente el archivo para agregar las características de vista previa para desarrolladores que quieras `manifest.json` usar. Una vez que hayas agregado características de vista previa de desarrollador al archivo, no podrás volver a importar `manifest.json` el paquete a App Studio.

## <a name="enable-developer-preview"></a>Habilitar la vista previa del desarrollador

La vista previa del desarrollador está habilitada para cada cliente, pero la opción para activar la vista previa del desarrollador se controla en el nivel de la organización. Para habilitar la opción de activar la vista previa del desarrollador para una persona, debes asegurarte de que tienen la capacidad de cargar aplicaciones personalizadas. Vea [la configuración del espacio empresarial](~/concepts/build-and-test/prepare-your-o365-tenant.md) para obtener información adicional.

El uso de una aplicación que contiene características de vista previa para desarrolladores puede provocar que los clientes que no han habilitado la vista previa de desarrollador se comporten de forma inesperada. Si no ves una entrada para la vista previa del desarrollador, lo más probable es que la organización no esté configurada para la carga de aplicaciones.

### <a name="on-a-desktop-or-web-client"></a>En un cliente web o de escritorio

Para habilitar la vista previa del desarrollador público en un cliente de escritorio o web, debe hacer lo siguiente:

1. Habilitar la carga de aplicaciones en la consola de administración de su espacio empresarial, como se [describe aquí.](~/concepts/build-and-test/prepare-your-o365-tenant.md)
1. Haga clic en su perfil (en la parte superior derecha o inferior izquierda de la interfaz de Teams) para mostrar el menú de Teams.
1. Selecciona Acerca de → versión preliminar del desarrollador.
1. Seleccione **Cambiar a la vista previa del programador.**

### <a name="on-a-mobile-client"></a>En un cliente móvil

Para habilitar la vista previa del desarrollador público en un cliente móvil, debe hacer lo siguiente:

1. Habilitar la carga de aplicaciones en la consola de administración de su espacio empresarial, como se [describe aquí.](~/concepts/build-and-test/prepare-your-o365-tenant.md)
1. Abra el menú hamburguesa en la parte superior izquierda y, a continuación, **seleccione Configuración.**
1. Seleccione **Acerca de**.
1. Haga clic en el botón de alternancia de vista previa del programador.

## <a name="disable-developer-preview"></a>Deshabilitar la vista previa del desarrollador

Usa el mismo elemento de menú en Acerca de → Vista previa del desarrollador y haz clic en él para desactivarlo.

## <a name="features-available-in-developer-preview"></a>Características disponibles en la versión preliminar para desarrolladores

Para obtener una lista completa de las características habilitadas actualmente en la versión preliminar del desarrollador, vea: [Características en la versión preliminar pública para desarrolladores.](../../resources/dev-preview/developer-preview-features.md)
