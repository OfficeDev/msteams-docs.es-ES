---
title: Introducción a la prueba de la aplicación
description: Describe el proceso para probar la aplicación personalizada de Teams en Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurar microsoft 365 inquilino Teams cargar aplicación de prueba
ms.openlocfilehash: d95d65961b060ff1938d51c0f3fafc2b1e56fa7e
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058610"
---
# <a name="test-your-app"></a>Probar la aplicación

Después de integrar la aplicación con Microsoft Teams, debes probar la aplicación antes de publicarla. El objetivo final es obtener tantos usuarios para tu aplicación, por lo tanto, asegúrate de probar la aplicación en varios dispositivos que los usuarios podrían usar. Para probar la aplicación:

* Preparar el espacio empresarial de Microsoft 365
* Elegir un área de trabajo para probar y depurar la aplicación
* Agregar datos de prueba al inquilino de Microsoft 365

## <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Antes de empezar a probar la aplicación, prepare el inquilino de prueba de Microsoft 365 y habilite la aplicación personalizada de Teams que le permita cargar la aplicación. Debe registrarse en el programa para desarrolladores de Microsoft 365 y administrar la configuración de Teams para su organización. Configure la suscripción de desarrollador y configúrela a través [de preparar el inquilino de Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

## <a name="test-and-debug"></a>Probar y depurar

Para probar y depurar la aplicación, debes crear al menos un área de trabajo. Puedes seleccionar una configuración de prueba, como host local o host basado en la nube para probar y depurar la aplicación. Se proporcionan instrucciones para depurar la aplicación de Teams para cargar y ejecutar la experiencia de la aplicación. Para obtener más información, [consulta elegir una configuración y ejecutar la aplicación de Microsoft Teams](~/concepts/build-and-test/debug.md).

Pruebe el bot localmente. Para obtener más información, [vea depurar el bot localmente con un IDE](~/bots/how-to/debug/locally-with-an-ide.md). También puede depurar el bot con software intermedio [de inspección](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) y [herramientas adaptables.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true) 

Para ver los registros de la consola, ver o modificar las solicitudes html, css y de red durante el tiempo de ejecución, agregue puntos de interrupción al código JavaScript y realice la depuración interactiva para obtener acceso a DevTools. Para obtener más información, [vea Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md). 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Agregar datos de prueba al inquilino de Microsoft 365

Agregue los datos de prueba al inquilino de prueba de Microsoft 365. Para obtener más información, vea Agregar datos de prueba al inquilino de prueba de [Office 365](~/concepts/build-and-test/test-data.md)y completar todos los requisitos previos antes de empezar a cargar los datos de prueba.

## <a name="see-also"></a>Vea también

- [Depurar la pestaña](~/tabs/how-to/developer-tools.md)
 
- [Depurar los bots](~/bots/how-to/debug/locally-with-an-ide.md)

- [Probar permisos de RSC](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Preparar el espacio empresarial de Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
