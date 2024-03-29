---
title: Versión preliminar para desarrolladores públicos para Microsoft Teams
description: Una versión preliminar para desarrolladores (beta) es un programa público para explorar y probar las próximas características para su posible inclusión en la aplicación de Microsoft Teams.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: dd0583f453e93a0127bf4cbcc29a6a56dec6655a
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100290"
---
# <a name="public-developer-preview-for-teams"></a>Versión preliminar pública para desarrolladores de Teams

>[!NOTE]
>Es posible que las características incluidas en la versión preliminar no estén completas y experimenten cambios antes de estar disponibles en la versión pública. Se proporcionan solo con fines de prueba y exploración. No deben usarse en aplicaciones de producción.

La versión preliminar para desarrolladores es un programa público para desarrolladores que proporciona acceso anticipado a características inéditas en Microsoft Teams. Esto le permite explorar y probar las próximas características para su posible inclusión en la aplicación de Teams También agradecemos los [comentarios](~/feedback.md) sobre cualquier característica en la versión preliminar para desarrolladores. La versión preliminar para desarrolladores está habilitada por cliente de Microsoft Teams, por lo que no tiene que preocuparse por que afecte a toda la organización.

## <a name="developer-preview-app-manifest"></a>Manifiesto de la aplicación de la versión preliminar para desarrolladores

Muchas características habilitadas en la versión preliminar para desarrolladores requerirán modificaciones en el archivo JSON del manifiesto de la aplicación. Para hacerlo, deberá usar el [esquema de manifiesto de la versión preliminar para desarrolladores](~/resources/schema/manifest-schema-dev-preview.md). Si usa este esquema, no podrá usar el [Portal para desarrolladores para Teams](~/concepts/build-and-test/teams-developer-portal.md) para hacer estos cambios, ni podrá usarlo para cargar la aplicación para realizar pruebas. Para cargar la aplicación, tendrá que seleccionar el icono `More apps` de la barra de aplicaciones y, después, seleccionar `Upload a custom app link`. Con este método solo puede cargar una versión comprimida del paquete de la aplicación.

Es posible que le resulte útil usar Portal para desarrolladores de Teams para crear las partes de la versión preliminar que no sean para desarrolladores del paquete de la aplicación, exportar ese paquete y editar manualmente el archivo `manifest.json` para agregar las características de versión preliminar para desarrolladores que desea usar. Una vez que haya agregado las características de vista previa para desarrolladores al archivo `manifest.json`, no podrá volver a importar el paquete en el Portal para desarrolladores de Teams

## <a name="enable-developer-preview"></a>Habilitar la versión preliminar para desarrolladores

La versión preliminar para desarrolladores está habilitada por cliente, pero la opción de activar la versión preliminar para desarrolladores se controla a nivel de la organización. Para habilitar la opción de activar la versión preliminar para desarrolladores para un individuo, debes asegurarte de que tienen la capacidad de cargar aplicaciones personalizadas. Consulte [Configurar el espacio empresarial](~/concepts/build-and-test/prepare-your-o365-tenant.md) para obtener información adicional.

El uso de una aplicación que contenga características de la versión preliminar para desarrolladores puede hacer que los clientes que no hayan habilitado dicha versión se comporten inesperadamente. Si no ve la entrada a la versión preliminar para desarrolladores, lo más probable es que su organización no esté configurada para la carga de aplicaciones.

### <a name="on-a-desktop-or-web-client"></a>En un escritorio o cliente web

Para habilitar la versión preliminar pública para desarrolladores en un cliente de escritorio o web:

1. Habilite la carga o instalación de prueba de aplicaciones personalizadas para el espacio empresarial del desarrollador. Para obtener más información, vea [Habilitar aplicaciones personalizadas de Teams](../../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).
1. Seleccione el menú de puntos suspensivos (...) situado junto a su perfil de usuario para mostrar el menú de Teams.
1. Seleccione **Acerca de** > **Versión preliminar para desarrolladores**.
1. Seleccione **Cambiar a la versión preliminar para desarrolladores**.

### <a name="on-a-mobile-client"></a>En un cliente móvil

Para habilitar la versión preliminar pública para desarrolladores en un cliente móvil:

1. Habilite la carga o instalación de prueba de aplicaciones para el espacio empresarial del desarrollador. Para obtener más información, vea [Habilitar aplicaciones personalizadas de Teams](../../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).
1. Abra el menú hamburguesa en la parte superior izquierda y, a continuación, seleccione **Configuración**.
1. Seleccione **Información**.
1. Habilite el botón de alternancia **Versión preliminar para desarrolladores**.

## <a name="disable-developer-preview"></a>Deshabilite la versión preliminar para desarrolladores

Use el mismo elemento de menú en Acerca de → Versión preliminar para desarrolladores y selecciónelo para desactivarlo.

## <a name="see-also"></a>Vea también

[Probar y depurar la aplicación Microsoft Teams](~/concepts/build-and-test/debug.md)
