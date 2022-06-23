---
title: Solución de Teams para crear aplicaciones
author: heath-hamilton
description: Obtenga información general sobre Teams solución para crear aplicaciones y proporcione soporte técnico desde planear la aplicación hasta distribuirla.
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 11/02/2021
ms.openlocfilehash: 22722d764cf498ff96bb81e9ede65c4ae112011f
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190120"
---
# <a name="the-teams-solution"></a>La solución de Teams


La plataforma de Microsoft Teams es una plataforma potente y flexible para crear aplicaciones para Teams. Ofrece un amplio conjunto de entornos de desarrollo y herramientas que admiten el desarrollo de aplicaciones.

## <a name="the-user-story"></a>El caso del usuario

Ha visto las ofertas de Teams. Ahora puede asignarlas a las necesidades del usuario. Vamos a revisar el escenario.

El desarrollador de la agencia Viajes y Tours quiere construir una aplicación para sus usuarios, los viajeros. La aplicación debe:

- Comprobar y enviar la planificación a los viajeros registrados en la agencia de viajes.
- Informar a los usuarios un día antes de la fecha de salida para que puedan planificar.

Recopilar y asignar requisitos a las características de Teams:

| Necesidades de la aplicación de usuario | Comprobar la previsión | Notificación antes de viajar | Usuario registrado |
| --- |:---:|:---:|:---:|
| **Funcionalidad** | Bot | &nbsp; | &nbsp; |
| **Integración** | &nbsp; | &nbsp; | :::image type="icon" source="assets/icons/microsoft-icon.png" border="false"::: Microsoft Graph, Weather API |
| **Scope** | &nbsp; | Aplicación personal | &nbsp; |
| **Punto de Integración** | &nbsp; | Chat | &nbsp; |

**Solución de la aplicación Teams : Una aplicación** de chat bot personal *personal chat bot* de Teams que comprueba y *envía una notificación de previsión* a los *usuarios registrados* antes de su fecha de viaje.

:::image type="content" source="../msteams-platform/assets/images/overview/developer-scenario-solution.png" alt-text="Un desarrollador de una agencia de viajes crea un bot para Teams que envía la previsión meteorológica a los clientes para que puedan planear con antelación sus fechas de viaje" border="false":::

Teams ofrece estas y muchas más funcionalidades para ofrecer a los usuarios una solución de aplicación con muchas características. Para desarrollar esta aplicación:

1. Cree una aplicación de bot de chat personal.
1. Realice la integración con una API de previsión meteorológica externa para conectarse y solicitar la previsión de una fecha y ubicación específicas.
1. Realice la integración con :::image type="icon" source="assets/icons/teams-icon.png" border="false"::: Microsoft Graph para los usuarios registrados.
1. Compruebe y envíe los detalles de la previsión en función de la fecha de viaje y la ubicación del viaje del usuario.

## <a name="choose-what-suits-you"></a>Elija lo que más le convenga

Puede crear una aplicación de Teams según los requisitos de la aplicación. Basándose en factores como las necesidades del negocio, el entorno de desarrollo y el conocimiento del dominio, seleccione el entorno y las herramientas que desee para desarrollar su aplicación.

Una aplicación de Teams le ofrece la flexibilidad de elegir el entorno de compilación. Incluye herramientas, marcos y lenguajes para enfocar el desarrollo de aplicaciones.

:::image type="content" source="../msteams-platform/assets/images/overview/tools-of-your-choice.png" alt-text="Aplicación para necesidad empresarial" border="false":::

Cree la aplicación de Teams en el entorno que mejor se adapte a sus requisitos concretos. Incluso puede seleccionar una combinación.

Por ejemplo, puede usar el kit de herramientas de Teams para compilar una aplicación con JavaScript y hospedarla en un sitio de SharePoint.

## <a name="teams-collaborative-platform"></a>Plataforma colaborativa de Teams

Una aplicación de Teams ofrece a los usuarios las ventajas de un área de trabajo colaborativa.

Como plataforma para crear aplicaciones, Teams ofrece toda la gama de aplicaciones y kits de herramientas. La plataforma Teams le ayuda en todas las fases, desde planear la aplicación hasta distribuirla.

:::image type="content" source="../msteams-platform/assets/images/overview/teams-dev-life-cycle.png" alt-text="Describiendo un ciclo de vida de desarrollo de aplicaciones de Teams. Planee, diseñe, compile, extienda, pruebe, implemente, distribuya. Detalles que se muestran en una lista con viñetas a continuación." border="false":::

Desde el diseño hasta la creación y distribución de una aplicación de Teams, puede usar varias herramientas y servicios. Un flujo de desarrollo de ejemplo puede ser:

1. Planifique su proyecto y averigüe los requisitos.
1. Diseñe la aplicación. Use el Kit de interfaz de usuario de Teams y la biblioteca de interfaz de usuario para diseñar la interfaz de usuario de pestañas.
1. Compile la aplicación con JavaScript mediante el kit de herramientas de Teams.
1. Amplíe la funcionalidad agregando más funcionalidades de Teams y datos de M365 con :::image type="icon" source="assets/icons/microsoft-icon.png" border="false"::: Microsoft Graph.
1. Pruebe la aplicación en un inquilino de desarrollador con datos de usuario de ejemplo.
1. Implemente la aplicación en Azure.
1. Administre y publique las aplicaciones en Store con el Portal para desarrolladores. Monetice su aplicación con opciones, como ofertas de SaaS, compras desde la aplicación y mucho más.

## <a name="next-step"></a>Paso siguiente

:::row:::
    :::column span="1":::
        **Empezar a compilar**
    :::column-end:::
    :::column span="2":::
        Familiarícese rápidamente con la compilación de Teams mediante la configuración del entorno y la creación de una aplicación sencilla.

        > [!div class="nextstepaction"]
        > [Compilar una aplicación por primera vez](get-started/get-started-overview.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también

:::row:::
    :::column span="1":::
        **Planifique su aplicación**
    :::column-end:::
    :::column span="2":::
        Comprenda y asigne los casos de uso de la aplicación a las características de Teams.

        > [!div class="nextstepaction"]
        > [Planifique su aplicación](~/concepts/app-fundamentals-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Diseño de la aplicación**
    :::column-end:::
    :::column span="2":::
        Diseñe la interfaz de usuario de la aplicación con el Kit de interfaz de usuario de Teams.

        > [!div class="nextstepaction"]
        > [Diseñar la aplicación de Teams](~/concepts/design/design-teams-app-process.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Crear una aplicación**
    :::column-end:::
    :::column span="2":::
        ¿Está buscando inspiración para el desarrollo de aplicaciones? Examine nuestra lista de escenarios reales y soluciones del sector conceptos ficticios de alta fidelidad para comprender las distintas formas en que una aplicación de Teams puede ayudar a los usuarios.

        > [!div class="nextstepaction"]
        > [Ver escenarios de aplicaciones](https://adoption.microsoft.com/extensibility-look-book/scenarios/)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Ampliar la aplicación en todo Microsoft 365**
    :::column-end:::
    :::column span="2":::
Puede obtener una vista previa de las aplicaciones de Teams que se ejecutan en otras experiencias de Microsoft 365 de uso elevado con la versión preliminar del SDK de cliente de JavaScript v2 de Teams.

        > [!div class="nextstepaction"]
        > [Ampliar la aplicación](m365-apps/overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Probar la aplicación**
    :::column-end:::
    :::column span="2":::
        Después de integrar la aplicación con Teams, debe probarla antes de publicarla.

        > [!div class="nextstepaction"]
        > [Probar la aplicación](concepts/build-and-test/test-app-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Distribuir la aplicación**
    :::column-end:::
    :::column span="2":::
        Puede proporcionar su aplicación de Teams a una persona, equipo, organización o cualquier persona que quiera usarla.

        > [!div class="nextstepaction"]
        > [Distribuir la aplicación](~/concepts/deploy-and-publish/apps-publish-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Rentabilizar la aplicación**
    :::column-end:::
    :::column span="2":::
        La tienda de Teams ofrece opciones de monetización de aplicaciones, como ofertas de SaaS y compras desde la aplicación. Elija la mejor opción de monetización adecuada para su aplicación de Teams.

        > [!div class="nextstepaction"]
        > [Rentabilizar la aplicación](concepts/deploy-and-publish/appsource/prepare/monetize-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Integración con Teams**
    :::column-end:::
    :::column span="2":::
        Combine las características que a los usuarios les gustan de una aplicación web, un servicio o un sistema existentes con las características de colaboración de Teams.

        > [!div class="nextstepaction"]
        > [Integrar una aplicación existente](samples/integrating-web-apps.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Con un poco de código se va muy lejos**
    :::column-end:::
    :::column span="2":::
        No es necesario ser un programador experto para crear una excelente aplicación de Teams. Pruebe una de varias soluciones con poco código.

        > [!div class="nextstepaction"]
        > [Crear una aplicación con poco código](samples/teams-low-code-solutions.md)
    :::column-end:::
:::row-end:::
