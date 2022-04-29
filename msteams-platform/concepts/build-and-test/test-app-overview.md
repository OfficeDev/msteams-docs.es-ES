---
title: Introducción a la prueba de su aplicación
description: Describe el proceso de probar y depurar su aplicación personalizada de Teams en Microsoft 365
ms.topic: how-to
ms.localizationpriority: high
keywords: Configurar el inquilino de Microsoft 365 Teams que está cargando la aplicación de prueba
ms.openlocfilehash: 98c00ece54e1654570556bac122e6760b283b73f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111531"
---
# <a name="test-your-app"></a>Probar la aplicación

Después de integrar la aplicación con Microsoft Teams, debe probarla antes de publicarla. El objetivo final es conseguir el mayor número de usuarios para su aplicación, por lo tanto, asegúrese de probar la aplicación en múltiples dispositivos que los usuarios podrían utilizar. Para probar la aplicación:

* Preparar el espacio empresarial de Microsoft 365.
* Elija un área de trabajo para probar y depurar la aplicación.
* Adición de datos de prueba al inquilino de prueba de Microsoft 365.

## <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Antes de comenzar a probar su aplicación, prepare su inquilino de prueba de Microsoft 365 y habilite la aplicación personalizada de Teams para que pueda cargar su aplicación. Debe inscribirse en el programa de desarrolladores de Microsoft 365 y gestionar la configuración de Teams para su organización. Configure su suscripción de desarrollador y configúrela mediante [preparar su inquilino de Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

## <a name="test-and-debug"></a>Probar y depurar

Para probar y depurar la aplicación, debe crear al menos un área de trabajo. Puede seleccionar una configuración de prueba, como un host local o un host basado en la nube para probar y depurar la aplicación. Se proporciona una guía para la depuración de su aplicación Teams para cargar y ejecutar su experiencia de aplicación. Para obtener más información, vea [elegir una configuración y ejecutar su aplicación de Microsoft Teams](~/concepts/build-and-test/debug.md).

Pruebe el bot localmente. Para obtener más información, consulte [depurar el bot localmente con un IDE](~/bots/how-to/debug/locally-with-an-ide.md). También puede depurar su bot con [middleware de inspección](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) y [herramientas de adaptación](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).

Para ver los registros de la consola, ver o modificar las solicitudes html, css y de red durante el tiempo de ejecución, añadir puntos de interrupción a su código JavaScript y realizar una depuración interactiva, acceda a las DevTools. Para obtener más información, vea [Acceso a las pestañas DevTools para Teams](~/tabs/how-to/developer-tools.md).

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Adición de datos de prueba al inquilino de Microsoft 365

Agregue los datos de prueba a un inquilino de prueba de Microsoft 365. Para obtener más información, vea [agregar datos de prueba a su espacio empresarial de prueba de Office 365](~/concepts/build-and-test/test-data.md) y complete todos los requisitos previos antes de empezar a cargar los datos de prueba.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Preparar el espacio empresarial de Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="see-also"></a>Consulte también

* [Depurar la pestaña](~/tabs/how-to/developer-tools.md)
* [Depurar los bots](~/bots/how-to/debug/locally-with-an-ide.md)
* [Prueba de permisos de RSC](~/graph-api/rsc/test-resource-specific-consent.md)
