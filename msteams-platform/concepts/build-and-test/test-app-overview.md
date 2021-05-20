---
title: Pruebe la descripción general de la aplicación
description: Describe el proceso para probar la aplicación personalizada Teams en Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurar Microsoft 365 inquilino Teams la aplicación de prueba de carga
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565189"
---
# <a name="test-your-app"></a>Probar la aplicación

Después de integrar la aplicación con Microsoft Teams, debe probar la aplicación antes de publicarla. El objetivo final es obtener tantos usuarios para la aplicación, por lo tanto, asegurarse de probar la aplicación en varios dispositivos que los usuarios podrían usar. Para probar la aplicación:

* Prepare su inquilino Microsoft 365.
* Elija un área de trabajo para probar y depurar la aplicación.
* Agregue datos de prueba al inquilino Microsoft 365.

## <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Antes de empezar a probar la aplicación, prepare el inquilino de prueba de Microsoft 365 y habilite la aplicación de Teams personalizada le permite cargar la aplicación. Debe registrarse para Microsoft 365 programa para desarrolladores y administrar la configuración de Teams de su organización. Configure la suscripción para desarrolladores y configúrela mediante [la preparación de la Microsoft 365 Inquilino](~/concepts/build-and-test/prepare-your-o365-tenant.md).

## <a name="test-and-debug"></a>Probar y depurar

Para probar y depurar la aplicación, debe crear al menos un área de trabajo. Puede seleccionar una configuración de prueba, como host local o host basado en la nube para probar y depurar la aplicación. Se proporcionan instrucciones para depurar la aplicación Teams para cargar y ejecutar la experiencia de la aplicación. Para obtener más información, consulta [elegir una configuración y ejecutar la aplicación Microsoft Teams](~/concepts/build-and-test/debug.md).

Pruebe el bot localmente. Para obtener más información, vea [depurar el bot localmente con un IDE](~/bots/how-to/debug/locally-with-an-ide.md). También puede depurar el bot con [middleware de inspección](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) y [herramientas adaptables.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true) 

Para ver los registros de la consola, ver o modificar solicitudes html, css y de red durante el tiempo de ejecución, agregue puntos de interrupción al código JavaScript y realice la depuración interactiva acceda a DevTools. Para obtener más información, consulte [Acceso a las pestañas DevTools for Teams](~/tabs/how-to/developer-tools.md). 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Agregue datos de prueba al inquilino de Microsoft 365

Agregue los datos de prueba a Microsoft 365 inquilino de prueba. Para obtener más información, consulte [Agregar datos de prueba al inquilino de prueba de Office 365](~/concepts/build-and-test/test-data.md)y complete todos los requisitos previos antes de empezar a cargar los datos de prueba.

## <a name="see-also"></a>Vea también

- [Depurar la pestaña](~/tabs/how-to/developer-tools.md)
 
- [Depurar los bots](~/bots/how-to/debug/locally-with-an-ide.md)

- [Permisos RSC de prueba](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Preparar el espacio empresarial de Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
