---
title: Publicar aplicaciones de Teams con el kit de herramientas de Teams
author: zyxiaoyuer
description: publicar aplicaciones de Teams
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 2c3fdd78d833baba6bbd5f21640765577f29430b
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757454"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>Publicar aplicaciones de Teams con el kit de herramientas de Teams

Después de crear la aplicación, puede distribuirla a un ámbito diferente, por ejemplo, individual, equipo, organización o cualquier usuario. La distribución depende de varios factores, incluidas las necesidades, los requisitos empresariales y técnicos, y el objetivo de la aplicación. La distribución a un ámbito diferente puede necesitar un proceso de revisión diferente. En general, cuanto mayor sea el ámbito, más revisión tendrá que pasar la aplicación por cuestiones de seguridad y cumplimiento.

## <a name="prerequisite"></a>Requisito previo

* [Instale el Kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión v3.0.0+.

> [!TIP]
> Asegúrese de que tiene un proyecto de aplicación de Teams en VS Code.

## <a name="publish-to-individual-scope-or-sideload-permission"></a>Publicar en un ámbito individual o transferir localmente el permiso

Los usuarios pueden agregar una aplicación personalizada a Teams cargando un paquete de aplicación en un archivo *.zip directamente a un equipo o en el contexto personal. Agregar una aplicación personalizada mediante la carga de un paquete de aplicación se conoce como instalación de prueba y permite probar la aplicación mientras se desarrolla, antes de que la aplicación esté lista para distribuirse ampliamente, como se mencionó en los escenarios siguientes:

* Probar y depurar una aplicación localmente.
* Cree una aplicación para usted, por ejemplo, para automatizar un flujo de trabajo.
* Cree una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.

Puede crear una aplicación solo para uso interno y compartirla con su equipo sin enviarla al catálogo de aplicaciones de Teams en la tienda de aplicaciones de Teams.

**Para compilar la aplicación en un *archivo de paquete de la aplicación .zip**

Para compilar el paquete de la aplicación, seleccione `Zip Teams metadata package` en **IMPLEMENTACIÓN** en la Vista de árbol del Kit de herramientas de Teams. Primero debe ejecutar `Provision in the cloud`. El paquete de aplicación generado se ubicará en `{your project folder}/build/appPackage/appPackage.{env}.zip`.

Realice los pasos siguientes para cargar el paquete de la aplicación:

1. En el cliente de Teams, seleccione **Aplicaciones** en la barra izquierda.
2. Seleccione **Administrar las aplicaciones**.
3. Seleccione **publicar una aplicación**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pub.png" alt-text="publish":::

4. Seleccione **Cargar una aplicación personalizada**:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/uplo.png" alt-text="cargar":::

## <a name="publish-to-your-organization"></a>Publicar en la organización

Cuando la aplicación esté lista para usarse en producción, puede enviarla mediante la API de envío de aplicaciones de Teams, llamada desde la API de Graph, un entorno de desarrollo integrado (IDE) como Microsoft Visual Studio Code instalado con el kit de herramientas de Teams. Puede seleccionar **Publicar en Teams** desde **IMPLEMENTACIÓN** en Vista de árbol del Kit de herramientas de Teams, o bien desencadenar **Teams: Publicar en Teams** desde la paleta de comandos. A continuación, seleccione **Instalación para su organización**:

![Instalar para la organización](./images/installforyourorganization.png)

La aplicación está disponible en **Administrar aplicaciones** del Centro de administración de Microsoft Teams, donde usted y el administrador pueden revisarla y aprobarla.

Como administrador, **Administrador de aplicaciones** en el [ Center de administración de Microsoft Teams](https://admin.teams.microsoft.com/policies/manage-apps) es donde puede ver y administrar todas las aplicaciones de Teams para su organización. Puede ver el estado de la organización y las propiedades de las aplicaciones, aprobar o cargar nuevas aplicaciones personalizadas en la tienda de aplicaciones de su organización, bloquear o permitir aplicaciones en el nivel de la organización, agregar aplicaciones a equipos, comprar servicios para aplicaciones de terceros, ver los permisos solicitados por las aplicaciones, dar el consentimiento de administrador a las aplicaciones y [administrar la configuración de aplicaciones para toda la organización](https://admin.teams.microsoft.com/policies/manage-apps).

El Kit de herramientas de Teams para Visual Studio Code basado en la API de envío de aplicaciones de Teams le permite automatizar el proceso de envío a aprobación para aplicaciones personalizadas en Teams.

> [!NOTE]
> La aplicación aún no se publica en la tienda de aplicaciones de la organización. El paso envía la aplicación al Centro de administración de Microsoft Teams, donde puede aprobarla para publicarla en la tienda de aplicaciones de su organización.

## <a name="admin-approval-for-teams-apps"></a>Aprobación de administrador para aplicaciones de Teams

El administrador de su espacio empresarial de Teams puede ir al **Administrador de aplicaciones** en el Centro de administración de Microsoft Teams, en el panel de navegación izquierdo, vaya a Aplicaciones de Teams > Administrar aplicaciones. Puede ver todas las aplicaciones de Teams de su organización. En el widget Aprobación pendiente en la parte superior de la página, podrá saber cuándo se envía una aplicación personalizada para su aprobación.
En la tabla, una aplicación recién enviada publica automáticamente el estado de las aplicaciones enviadas y bloqueadas. Puede ordenar la columna de estado de publicación en orden descendente para buscar la aplicación:

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="aprobación":::

Seleccione el nombre de la aplicación para ir a la página de detalles. En la pestaña Acerca de, puede ver detalles sobre la aplicación, incluida la descripción, el estado y el identificador de la aplicación:

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="aplicaciones enviadas":::

Realice los pasos siguientes para publicar la aplicación:

1. En el panel de navegación izquierdo del Centro de administración de Microsoft Teams, vaya a Aplicaciones de Teams > **Administrar aplicaciones**.
2. Seleccione el nombre de la aplicación para ir a la página de detalles y, a continuación, en el cuadro de estado, seleccione **Publicar**.
Después de publicar la aplicación, el estado de publicación cambia a publicado y el estado cambia automáticamente a permitido.

## <a name="publish-to-microsoft-store"></a>Publicar en Microsoft Store

Puede distribuir la aplicación directamente en la tienda dentro de Microsoft Teams y llegar a millones de usuarios en todo el mundo. Si la aplicación también aparece en la tienda, podría llegar instantáneamente a sus clientes potenciales. Las aplicaciones publicadas en la tienda de Teams también se enumeran automáticamente en Microsoft AppSource, que es el marketplace oficial para aplicaciones y soluciones de Microsoft 365.

Para obtener más información, vea ([Publicar la aplicación en la tienda de Microsoft Teams](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store)).

## <a name="see-also"></a>Consulte también

* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)
