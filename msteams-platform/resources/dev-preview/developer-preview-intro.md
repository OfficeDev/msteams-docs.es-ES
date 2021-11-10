---
title: Vista previa del desarrollador
description: Describe las características de public developer preview de Microsoft Teams
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Características para desarrolladores de teams preview
ms.openlocfilehash: 756d30b0cbeb47be2b355bc9fe126e3bc39b3806
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888506"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Versión preliminar de desarrolladores públicos para Microsoft Teams

>[!NOTE]
>Es posible que las características incluidas en la versión preliminar no estén completas y que se someten a cambios antes de estar disponibles en la versión pública. Solo se proporcionan con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

Developer Preview es un programa público para desarrolladores que proporciona acceso anticipado a características inéditas en Microsoft Teams. Esto te permite explorar y probar las próximas características para la posible inclusión en tu Microsoft Teams aplicación. También agradecemos los [comentarios](~/feedback.md) sobre cualquier característica en la vista previa del desarrollador. La vista previa del desarrollador está habilitada Microsoft Teams cliente, por lo que no es necesario preocuparse por afectar a toda la organización.

## <a name="developer-preview-app-manifest"></a>Manifiesto de la aplicación de vista previa del desarrollador

Muchas características habilitadas en la vista previa del desarrollador requerirán alteraciones en el archivo JSON del manifiesto de la aplicación. Para ello, deberá usar el esquema de manifiesto [de vista previa del desarrollador](~/resources/schema/manifest-schema-dev-preview.md). Si usas este esquema, no podrás usar [App Studio](~/concepts/build-and-test/app-studio-overview.md) para realizar estos cambios ni podrás usarlo para cargar la aplicación para realizar pruebas. Para cargar la aplicación, tendrás que hacer clic en el icono de la barra de aplicaciones y, a `More apps` continuación, selecciona `Upload a custom app link` . Con este método solo puedes cargar una versión comprimida del paquete de la aplicación.

Es posible que te sea útil usar App Studio para crear las partes de vista previa no para desarrolladores del paquete de la aplicación, luego exportar ese paquete y editar manualmente el archivo para agregar las características de vista previa del desarrollador que quieras `manifest.json` usar. Una vez que hayas agregado características de vista previa de desarrolladores al archivo, no podrás volver a importar `manifest.json` el paquete en App Studio.

## <a name="enable-developer-preview"></a>Habilitar la vista previa del desarrollador

La vista previa del desarrollador está habilitada por cliente, pero la opción de activar la vista previa del desarrollador se controla en el nivel de la organización. Para habilitar la opción para activar la vista previa del desarrollador para un individuo, debes asegurarte de que tienen la capacidad de cargar aplicaciones personalizadas. Consulte [Configurar el espacio empresarial](~/concepts/build-and-test/prepare-your-o365-tenant.md) para obtener información adicional.

El uso de una aplicación que contiene características de vista previa para desarrolladores puede hacer que los clientes que no han habilitado la vista previa del desarrollador se comporten inesperadamente. Si no ve una entrada para la vista previa del desarrollador, lo más probable es que su organización no esté configurada para la carga de aplicaciones.

### <a name="on-a-desktop-or-web-client"></a>En un cliente de escritorio o web

Para habilitar la vista previa del desarrollador público en un cliente de escritorio o web, debe hacer lo siguiente:

1. Habilitar la carga de aplicaciones en la consola de administración de su inquilino como se describe [aquí](~/concepts/build-and-test/prepare-your-o365-tenant.md).
1. Haga clic en el perfil (en la parte superior derecha o inferior izquierda de la Teams interfaz) para mostrar el Teams menú.
1. Selecciona Acerca de → versión preliminar del desarrollador.
1. Seleccione **Cambiar a vista previa del programador**.

### <a name="on-a-mobile-client"></a>En un cliente móvil

Para habilitar la vista previa del desarrollador público en un cliente móvil, debe hacer lo siguiente:

1. Habilitar la carga de aplicaciones en la consola de administración de su inquilino como se describe [aquí](~/concepts/build-and-test/prepare-your-o365-tenant.md).
1. Abra el menú hamburguesa en la parte superior izquierda y, a continuación, **seleccione Configuración**.
1. Seleccione **Acerca de**.
1. Haga clic en el botón de alternancia Vista previa del programador.

## <a name="disable-developer-preview"></a>Deshabilitar la vista previa del desarrollador

Usa el mismo elemento de menú en Acerca de → vista previa del desarrollador y haz clic en él para desactivarlo.

## <a name="see-also"></a>Consulte también

[Probar y depurar la Microsoft Teams aplicación](~/concepts/build-and-test/debug.md)