---
title: Proceso de diseño de aplicaciones
author: heath-hamilton
description: Obtenga información sobre cómo y cuándo puede usar herramientas y recursos de Microsoft para diseñar una aplicación de Microsoft Teams eficaz.
ms.localizationpriority: mediums
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 97ff20e0ffc6cc802c2226cc7767873cd3a25416
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144379"
---
# <a name="design-process-for-microsoft-teams-apps"></a>Proceso de diseño para aplicaciones de Microsoft Teams

Hay varias herramientas y recursos para diseñar la aplicación de Microsoft Teams. En los pasos siguientes se describe cuándo y cómo se pueden usar durante el proceso de diseño. (Algunos de los pasos pueden estar técnicamente fuera del proceso de diseño, pero se incluyen para un contexto adicional).

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="Diagrama que muestra un ejemplo del proceso de diseño de aplicaciones de Teams." border="false":::

## <a name="plan-your-app"></a>Planear la aplicación

Diseñar una aplicación de Teams de alta calidad requiere comprender lo que quiere que haga la aplicación y cómo cree que la usarán los usuarios. Sin embargo, antes de empezar a diseñar, responda a las siguientes preguntas:

* ¿Quiénes son sus usuarios?
* ¿Cuál es su problema?
* ¿Cómo puede resolver su problema la aplicación?
* ¿Con qué frecuencia se usará la aplicación?
* ¿Cuántas personas usarán la aplicación?
* ¿Qué tipo de rentabilidad de la inversión puede proporcionar la aplicación?

Para obtener más información, vea [comprender los casos de uso de las aplicaciones ](~/concepts/design/understand-use-cases.md) y [asignar casos de uso a Teams](~/concepts/design/map-use-cases.md).

## <a name="get-teams-design-tools"></a>Obtener herramientas de diseño de Teams

Microsoft proporciona herramientas para facilitar el diseño de la aplicación de Teams. Como mínimo, se recomienda usar el Kit de interfaz de usuario de Microsoft Teams.

### <a name="get-the-microsoft-teams-ui-kit"></a>Obtener el Kit de interfaz de usuario de Microsoft Teams

El Kit de interfaz de usuario de Microsoft Teams puede ayudarle a desarrollar una aplicación de Teams eficaz en el menor tiempo posible. El kit de interfaz de usuario tiene todo lo que ve en estos documentos relacionados con el diseño de aplicaciones de Teams y mucho más, incluidos amplios ejemplos y variaciones.

El kit de interfaz de usuario también tiene plantillas y componentes predefinidos que puede copiar y modificar según sea necesario, por lo que puede dedicar más tiempo a diseñar la mejor experiencia de usuario en lugar de tener que preocuparse por el aspecto que debería tener un botón.

> [!TIP]
> **¿El kit de interfaz de usuario es para mí?** Si tiene alguna parte en la creación de una aplicación de Teams, sí. Comprender cómo crear una aplicación de Teams no solo es útil para diseñadores, sino también para administradores de productos, desarrolladores que usan IDE y creadores que crean con herramientas de escaso código (como es Microsoft Power Platform).

1. Vaya a la página [Figma del kit de interfaz de usuario de Microsoft Teams](https://www.figma.com/community/file/916836509871353159).
1. Seleccione **Duplicar** para abrir el kit de interfaz de usuario  (es posible que primero tenga que crear una cuenta de Figma).

### <a name="try-the-sample-app"></a>Prueba de la aplicación de ejemplo

Puede cargar una aplicación de ejemplo para ver cómo deben verse y comportarse las aplicaciones en el cliente Teams.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a>Aprender el sistema de diseño de Teams

Lea en profundidad o al menos familiarícese con los [aspectos básicos del diseño de aplicaciones de Teams](design-teams-app-fundamentals.md), incluido diseño, combinaciones de colores y mucho más.

## <a name="choose-app-capabilities"></a>Elección de las funcionalidades de la aplicación

Después de la fase de planificación, puede determinar qué funcionalidades de Teams se ajustan a los casos de uso de las aplicaciones. Por ejemplo, si quiere notificar de forma proactiva a las personas, un bot podría ser la funcionalidad correcta.

El kit de interfaz de usuario tiene diseños creados previamente que muestran cómo los usuarios suelen agregar, configurar, usar y administrar cada funcionalidad. Como referencia rápida, esta información también está en estos documentos, pero con el kit de interfaz de usuario puede copiar y pegar cualquiera de esos diseños en el diseño de las aplicaciones.

1. En el panel de navegación izquierdo del kit de interfaz de usuario, vaya a **Funcionalidades de la aplicación** y seleccione la funcionalidad que quiera para la aplicación.
1. Copie lo que necesite de esa página para diseñar la aplicación.<br />
   Por ejemplo, si la aplicación admite la autenticación con inicio de sesión único, copie y pegue el diseño para controlar ese exacto necesario.

## <a name="design-your-ux-flow"></a>Diseño del flujo de experiencia del usuario

Una vez que tenga un diseño de aplicación básico, puede modificarlo y refinarlo tanto como desee copiando las plantillas de interfaz de usuario de Teams y los componentes básicos del kit de interfaz de usuario.

### <a name="design-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Las plantillas de interfaz de usuario son diseños complejos y de alta fidelidad para flujos de trabajo y casos de uso comunes de Teams. En lugar de empezar de abajo hacia arriba con componentes básicos, se recomienda usar estas plantillas para simplificar y acelerar el proceso de diseño.

1. En el panel de navegación izquierdo del kit de interfaz de usuario, vaya a **plantillas de interfaz de usuario**.
1. Copie las plantillas que tengan sentido para el diseño de la aplicación.<br />
   Por ejemplo, si está diseñando una aplicación personal, puede usar una plantilla de panel.

### <a name="design-with-basic-ui-components"></a>Diseño con componentes básicos de la interfaz de usuario

En función de la interfaz de usuario de Fluent, estos son los elementos principales para crear interfaces conocidas de Teams. Use estos componentes si a una plantilla de interfaz de usuario le falta algo que necesita o solo quiere diseñar la aplicación desde cero.

1. En el panel de navegación izquierdo del kit de interfaz de usuario, vaya a **Componentes básicos de la interfaz de usuario**.
1. Copie los componentes que necesita para el diseño de la aplicación (por ejemplo, un botón o un botón de alternancia).

## <a name="implement-your-design"></a>Implementar el diseño

El diseño está listo y listo para empezar a crear. Las siguientes herramientas pueden ayudar a simplificar el desarrollo front-end de la aplicación.

### <a name="build-with-ui-templates"></a>Compilación con plantillas de interfaz de usuario

Si ha usado plantillas de interfaz de usuario en el diseño, puede implementar estas plantillas con la biblioteca de interfaz de usuario de Microsoft Teams (una biblioteca de componentes de React basada en la interfaz de usuario de Fluent).

Actualmente, no todas las plantillas que aparecen en el kit de interfaz de usuario están disponibles en la biblioteca.

> [!div class="nextstepaction"]
> [Obtener la biblioteca (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a>Compilación con componentes básicos de la interfaz de usuario

De forma no diferente a la fase de diseño, puede usar estos componentes de la interfaz de usuario de Fluent en el proyecto de aplicación si falta algo que necesita en una plantilla de interfaz de usuario o solo quiere compilar la aplicación desde cero. 

(Nota: Si observa que falta algo o tiene una idea para una plantilla, puede considerar la posibilidad de contribuir al repositorio de la biblioteca de interfaz de usuario de Teams).

> [!div class="nextstepaction"]
> [Obtener la biblioteca (interfaz de usuario de Fluent)](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a>Revisar los recursos de diseño

Tanto si está empezando en la aplicación como si está cerca de una aplicación lista para producción, le recomendamos que revise periódicamente los siguientes recursos:

* **Directrices de validación de la tienda de Microsoft Teams**: proporciona estándares que todas las aplicaciones de Teams deben buscar y no solo las aplicaciones que aparecen en la tienda. Para obtener más información, consulte las [directrices](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).
* **Procedimientos recomendados de diseño**: estos documentos y el kit de interfaz de usuario proporcionan procedimientos recomendados para diseñar aplicaciones de alta calidad. Por ejemplo, puede consultar los [ procedimientos recomendados para diseñar bots](~/bots/design/bots.md#best-practices).

## <a name="see-also"></a>Consulte también

[Diseñar notificaciones de fuentes de actividades](~/concepts/design/activity-feed-notifications.md)
