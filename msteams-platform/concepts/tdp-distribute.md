---
title: Distribuir las aplicaciones
description: Aprende a distribuir tus aplicaciones mediante el Portal de desarrolladores para Microsoft Teams.
keywords: introducción a los equipos del portal de desarrolladores
localization_priority: Normal
ms.topic: Conceptual
ms.openlocfilehash: d1d098b295492a7dc3b691db4625307b6c3170ce
ms.sourcegitcommit: 25539046d408c4270b988fd826d7cf1275f4b9dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2021
ms.locfileid: "52763156"
---
# <a name="distribute-your-apps"></a>Distribuir las aplicaciones

## <a name="distribute"></a>Distribuir

Una vez que haya terminado  de definir la aplicación, la sección Distribuir le permite exportar la definición de la aplicación como un archivo zip que, a continuación, se puede compartir y cargar en el cliente de Teams para pruebas. Al hacer clic en exportar, se descarga el archivo zip **nombredeapp.zip** en el directorio de descarga predeterminado.

:::image type="content" source="~/assets/images/tdp/tdp_distribute_1.png" alt-text="Captura de pantalla que muestra la página Distribuir de Teams Developer Portal.":::

### <a name="manifest"></a>Manifiesto

El manifiesto describe cómo se configura la aplicación, incluidas sus capacidades, los recursos necesarios y otros atributos importantes. Vea [esquema de manifiesto](~/resources/schema/manifest-schema.md) para obtener más información.

### <a name="flights"></a>Vuelos

Controlar quién obtiene las actualizaciones de la aplicación. Por ejemplo, puede publicar una actualización a los empleados de Microsoft para identificar y corregir errores antes de publicarla al público. Seleccione **Crear una nueva solicitud** para crear una nueva solicitud de piloto.

### <a name="publish-to-org"></a>Publicar en la organización

Haz que la aplicación esté disponible para los usuarios de tu organización. Una vez aprobado por el administrador de TI, la aplicación aparecerá en Teams en Aplicaciones > integradas para tu organización.

### <a name="publish-your-app-to-teams-store"></a>Publicar la aplicación en Teams tienda

En la página principal del proyecto, puede cargar la aplicación a un equipo, enviarla a la tienda de aplicaciones personalizada de la organización para los usuarios de su organización o enviarla al origen de la aplicación para todos los usuarios de Teams. El administrador de TI revisará estas entregas. Puede volver a la página **Publicar** para comprobar el estado de entrega y saber si su administrador de TI aprobó o rechazó la aplicación. Aquí también es a donde deberá acudir para enviar las actualizaciones a su aplicación o cancelar cualquier entrega activa en este momento.

## <a name="see-also"></a>Consulte también

* [Información general sobre Teams Developer Portal](~/concepts/build-and-test/teams-developer-portal.md)
* [Configurar Teams Developer Portal](~/concepts/tdp-configuration.md)
* [Herramientas en Teams Developer Portal](~/concepts/tdp-tools.md)