---
title: Proceso de diseño de aplicaciones
author: heath-hamilton
description: Obtén una idea general de cómo y cuándo puedes usar herramientas y recursos de Microsoft para diseñar una aplicación Microsoft Teams eficaz.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 34401bf53196601b8836012fa4c96296510472a8
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157618"
---
# <a name="design-process-for-microsoft-teams-apps"></a>Proceso de diseño para Microsoft Teams aplicaciones

Hay varias herramientas y recursos para diseñar tu Microsoft Teams aplicación. Los pasos siguientes describen cuándo y cómo puede usarlos durante el proceso de diseño. (Algunos de los pasos pueden estar técnicamente fuera del proceso de diseño, pero se incluyen para contexto adicional).

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="Diagrama que muestra un ejemplo del proceso Teams diseño de la aplicación." border="false":::

## <a name="plan-your-app"></a>Planear la aplicación

El diseño de una aplicación de Teams de alta calidad requiere comprender lo que quieres que haga la aplicación y cómo crees que la usarán las personas. Sin embargo, antes de empezar a diseñar, responda a las siguientes preguntas:

* ¿Quiénes son sus usuarios?
* ¿Cuál es su problema?
* ¿Cómo puede resolver su problema la aplicación?
* ¿Con qué frecuencia se usará la aplicación?
* ¿Cuántas personas usarán la aplicación?
* ¿Qué tipo de retorno de la inversión puede proporcionar la aplicación?

Para obtener más información, consulta [comprender los casos](~/concepts/design/understand-use-cases.md) de uso de la aplicación y asignar los casos [de uso a Teams](~/concepts/design/map-use-cases.md).

## <a name="get-teams-design-tools"></a>Obtener Teams de diseño

Microsoft proporciona herramientas para facilitar el diseño de la Teams aplicación. Como mínimo, recomendamos encarecidamente usar el kit Microsoft Teams interfaz de usuario.

### <a name="get-the-microsoft-teams-ui-kit"></a>Obtener el kit Microsoft Teams interfaz de usuario

El kit Microsoft Teams interfaz de usuario puede ayudarte a desarrollar una aplicación Teams eficaz en el menor tiempo posible. El kit de interfaz de usuario tiene todo lo que ves en estos documentos relacionados con Teams diseño de aplicaciones y mucho más, incluidos extensos ejemplos y variaciones.

El kit de interfaz de usuario también tiene plantillas y componentes predefinidos que puedes copiar y modificar según sea necesario, por lo que puedes dedicar más tiempo a diseñar la mejor experiencia del usuario en lugar de preocuparte por cómo debería ser un botón.

> [!TIP]
> **¿El kit de interfaz de usuario es para mí?** Si tienes alguna parte en la creación de una Teams, sí. Comprender cómo crear una aplicación Teams no solo es útil para los diseñadores, sino también para los jefes de producto, los desarrolladores que usan id. de usuario y los creadores que se construyen con herramientas de código bajo (como Microsoft Power Platform).

1. Vaya a la [página Microsoft Teams Kit de interfaz de usuario de La Figma](https://www.figma.com/community/file/916836509871353159).
1. Selecciona **Duplicar para** abrir el kit de interfaz de usuario. (Es posible que primero tenga que crear una cuenta de Figma).

### <a name="try-the-sample-app"></a>Probar la aplicación de ejemplo

Puedes cargar una aplicación de ejemplo para ver cómo deben verse y comportarse las aplicaciones en el Teams cliente.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a>Información sobre Teams de diseño

Lea en profundidad o, al menos, familiarícese con los [conceptos básicos](design-teams-app-fundamentals.md)del diseño Teams aplicación, incluido el diseño, las esquemas de color y mucho más.

## <a name="choose-app-capabilities"></a>Elegir funcionalidades de la aplicación

Después de la fase de planeación, puedes determinar qué Teams se ajustan a los casos de uso de la aplicación. Por ejemplo, si quieres notificar proactivamente a las personas, un bot puede ser la funcionalidad adecuada.

El kit de interfaz de usuario tiene diseños predefinidos que muestran cómo las personas suelen agregar, configurar, usar y administrar cada funcionalidad. Para obtener una referencia rápida, esta información también está en estos documentos, pero con el kit de interfaz de usuario puedes copiar y pegar cualquiera de estos diseños en el diseño de la aplicación.

1. En la navegación izquierda del kit de interfaz de usuario, ve **a Funcionalidades de la** aplicación y selecciona la funcionalidad que quieras para la aplicación.
1. Copia lo que necesitas de esa página para diseñar la aplicación.<br />
   Por ejemplo, si la aplicación admite la autenticación con inicio de sesión único, copie y pegue el diseño para controlar ese escenario exacto.

## <a name="design-your-ux-flow"></a>Diseñar el flujo de experiencia de usuario

Una vez que tienes un diseño de aplicación básico Teams, puedes modificarlo y refinarlo tanto como quieras copiando plantillas de interfaz de usuario y componentes básicos del kit de interfaz de usuario.

### <a name="design-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Las plantillas de interfaz de usuario son diseños complejos y de alta fidelidad para Teams casos de uso y flujos de trabajo comunes. En lugar de empezar de abajo hacia arriba con componentes básicos, se recomienda usar estas plantillas para simplificar y acelerar el proceso de diseño.

1. En la navegación izquierda del kit de interfaz de usuario, vaya a **Plantillas de interfaz de usuario**.
1. Copia plantillas que tienen sentido para el diseño de la aplicación.<br />
   Por ejemplo, si estás diseñando una aplicación personal, es posible que quieras usar una plantilla de panel.

### <a name="design-with-basic-ui-components"></a>Diseño con componentes básicos de la interfaz de usuario

En función Fluent interfaz de usuario, estos son los elementos principales para crear interfaces Teams familiares. Usa estos componentes si falta una plantilla de interfaz de usuario o quieres diseñar la aplicación desde cero.

1. En la navegación izquierda del kit de interfaz de usuario, vaya a **Componentes básicos de la interfaz de usuario**.
1. Copia los componentes que necesitas para el diseño de la aplicación (por ejemplo, un botón o un botón de alternancia).

## <a name="implement-your-design"></a>Implementar el diseño

El diseño está listo y está listo para empezar a compilar. Las siguientes herramientas pueden ayudar a simplificar el desarrollo front-end de la aplicación.

### <a name="build-with-ui-templates"></a>Crear con plantillas de interfaz de usuario

Si usaste plantillas de interfaz de usuario en el diseño, puedes implementar estas plantillas con la biblioteca de interfaz de usuario Microsoft Teams (una biblioteca de componentes React basada en Fluent interfaz de usuario).

Actualmente, no todas las plantillas que aparecen en el kit de interfaz de usuario están disponibles en la biblioteca.

> [!div class="nextstepaction"]
> [Obtener la biblioteca (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a>Compilación con componentes básicos de la interfaz de usuario

A diferencia de la fase de diseño, puedes usar estos componentes de interfaz de usuario de Fluent en el proyecto de aplicación si falta una plantilla de interfaz de usuario o si solo quieres crear la aplicación desde cero. 

(Nota: Si observa que falta algo o tiene una idea para una plantilla, considere la posibilidad de contribuir al repositorio Teams biblioteca de interfaz de usuario).

> [!div class="nextstepaction"]
> [Obtener la biblioteca (Fluent interfaz de usuario)](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a>Revisar recursos de diseño

Tanto si estás empezando en la aplicación como si estás cerca de una aplicación lista para producción, te recomendamos que revises periódicamente los siguientes recursos:

* **Microsoft Teams de validación de** la tienda: proporciona estándares que todas las Teams deben esforzarse y no solo las aplicaciones enumeradas en la tienda. Para obtener más información, vea las [directrices](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).
* **Procedimientos recomendados de** diseño: estos documentos y el kit de interfaz de usuario proporcionan procedimientos recomendados para diseñar aplicaciones de alta calidad. Por ejemplo, vea los [procedimientos recomendados para diseñar bots](~/bots/design/bots.md#best-practices).

