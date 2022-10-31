---
title: Introducción a la prueba de su aplicación
description: En este módulo, obtenga información sobre el proceso para probar y depurar la aplicación personalizada de Teams en Microsoft 365 y agregar datos de prueba al inquilino de Microsoft 365.
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 7cb0d194cfa5cab503a632889b5449f086532afd
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791555"
---
# <a name="test-your-app"></a>Probar la aplicación

Después de integrar la aplicación con Microsoft Teams, debe probarla antes de publicarla. El objetivo final es conseguir el mayor número de usuarios para su aplicación, por lo tanto, asegúrese de probar la aplicación en múltiples dispositivos que los usuarios podrían utilizar. Para probar la aplicación:

* Preparar el espacio empresarial de Microsoft 365.
* Elija un área de trabajo para probar y depurar la aplicación.
* Adición de datos de prueba al inquilino de prueba de Microsoft 365.

## <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Antes de empezar a probar la aplicación, prepare el inquilino de prueba de Microsoft 365 y habilite la aplicación personalizada de Teams para que pueda cargar la aplicación. Debe inscribirse en el programa de desarrolladores de Microsoft 365 y gestionar la configuración de Teams para su organización. Configure su suscripción de desarrollador y configúrela mediante [preparar su inquilino de Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

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
