---
title: Publicar aplicaciones de Teams con el kit de herramientas de Teams
author: zyxiaoyuer
description: publicar Teams aplicaciones
ms.author: yanjiang
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d232ac1d0ac96d46aa5f265f3fedd7b65afb3a86
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435764"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>Publicar aplicaciones de Teams con el kit de herramientas de Teams

Después de crear la aplicación, puedes distribuir la aplicación a diferentes ámbitos, como individual, de equipo, de organización o de cualquier persona. La distribución depende de varios factores, como las necesidades, los requisitos técnicos y empresariales, y el objetivo de la aplicación. La distribución a distinto ámbito puede necesitar un proceso de revisión diferente. En general, cuanto mayor sea el ámbito, más revisión debe pasar la aplicación por cuestiones de seguridad y cumplimiento.

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de tener Teams proyecto de aplicación en el código VS.

## <a name="publish-to-individual-scope-or-sideload-permission"></a>Publicar en un ámbito individual o permiso de instalación local

Los usuarios pueden agregar una aplicación personalizada a Teams cargando un paquete de aplicación en un archivo *.zip directamente a un equipo o en contexto personal. Agregar una aplicación personalizada al cargar un paquete de la aplicación se conoce como instalación local y te permite probar la aplicación mientras se desarrolla, antes de que la aplicación esté lista para distribuirse ampliamente, como se menciona en los siguientes escenarios:

* Probar y depurar una aplicación localmente.
* Crea una aplicación para ti, como automatizar un flujo de trabajo.
* Crea una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.

Puedes crear una aplicación solo para uso interno y compartirla con tu equipo sin enviarla al catálogo de aplicaciones Teams en la Teams de aplicaciones.

**Para crear la aplicación para crear *.zip de paquete de la aplicación**

Puedes crear el paquete de la aplicación seleccionando `Zip Teams metadata package` **DEPLOYMENT** en Treeview de Teams Toolkit. Debe ejecutar primero `Provision in the cloud` . El paquete de aplicación generado se ubicará en `{your project folder}/build/appPackage/appPackage.{env}.zip`.

Realice los siguientes pasos para cargar el paquete de la aplicación:

1. En el Teams, seleccione **Aplicaciones en** la barra izquierda.
2. Selecciona **Administrar aplicaciones**.
3. Seleccionar **publicar una aplicación**

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pub.png" alt-text="publish":::

4. Selecciona **Upload una aplicación personalizada**:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/uplo.png" alt-text="cargar":::

## <a name="publish-to-your-organization"></a>Publicar en la organización 

Cuando la aplicación esté lista para su uso en producción, puedes enviar la aplicación mediante la API de envío de aplicaciones de Teams, llamada Graph desde una API, un entorno de desarrollo integrado (IDE) como Microsoft Visual Studio Code instalado con el kit de herramientas Teams. Puede seleccionar Publicar a **Teams** **desde DEPLOYMENT** en TreeView de Teams Toolkit o desencadenar Teams **: Publicar** en Teams desde la paleta de comandos. A **continuación, seleccione Instalar para su organización**:

![Instalar para su organización](./images/installforyourorganization.png)

La aplicación está disponible en el  Centro de administración Microsoft Teams administrar aplicaciones, donde tú y el administrador pueden revisarla y aprobarla.

Como administrador, manage **apps** in the [Microsoft Teams admin center](https://admin.teams.microsoft.com/policies/manage-apps) is where you can view and manage all Teams apps for your organization. Puedes ver el estado del nivel de organización y las propiedades de las aplicaciones, aprobar o cargar nuevas aplicaciones personalizadas en la tienda de aplicaciones de tu organización, bloquear o permitir aplicaciones en el nivel de la organización, agregar aplicaciones a equipos, comprar servicios para aplicaciones de terceros, ver los permisos solicitados por las aplicaciones, conceder el consentimiento de administrador a las aplicaciones y administrar la configuración de aplicaciones de toda la [organización.](https://admin.teams.microsoft.com/policies/manage-apps)

Teams kit de herramientas para Visual Studio Code integrado en la API de envío de aplicaciones de Teams y permite automatizar el proceso de envío a aprobación para aplicaciones personalizadas en Teams.

> [!NOTE]
> La aplicación aún no se publica en la tienda de aplicaciones de la organización. El paso envía la aplicación al Centro de administración de Microsoft Teams donde puedes aprobarla para su publicación en la tienda de aplicaciones de tu organización.

## <a name="admin-approval-for-teams-apps"></a>Aprobación de administrador para Teams aplicaciones

El administrador de tu inquilino de Teams puede ir al Administrar aplicaciones en el  Centro de administración de Microsoft Teams, en la navegación izquierda, ir Teams aplicaciones > Administrar aplicaciones. Puedes ver todas las aplicaciones Teams para tu organización. En el widget Aprobación pendiente en la parte superior de la página te permite saber cuándo se envía una aplicación personalizada para su aprobación.
En la tabla, una aplicación recién enviada publica automáticamente el estado de las aplicaciones enviadas y bloqueadas. Puedes ordenar la columna de estado de publicación en orden descendente para buscar la aplicación:

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="aprobación":::

Selecciona el nombre de la aplicación para ir a la página de detalles de la aplicación. En la pestaña Acerca de, puedes ver detalles sobre la aplicación, incluida la descripción, el estado y el identificador de la aplicación:

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="aplicación enviada":::

Realice los siguientes pasos para publicar la aplicación:

1. En la navegación izquierda del Centro Microsoft Teams administración, ve a Teams aplicaciones > **Administrar aplicaciones**.
2. Selecciona el nombre de la aplicación para ir a la página de detalles de la aplicación y, a continuación, en el cuadro estado, selecciona **Publicar**.
Después de publicar la aplicación, el estado de publicación cambia a publicado y el estado cambia automáticamente a permitido.

## <a name="publish-to-microsoft-store"></a>Publicar en Microsoft Store

Puedes distribuir la aplicación directamente a la tienda dentro de Microsoft Teams y llegar a millones de usuarios de todo el mundo. Si la aplicación también se incluye en la tienda, puedes llegar al instante a los clientes potenciales. Las aplicaciones publicadas en la tienda Teams también listan automáticamente en Microsoft AppSource, que es el mercado oficial para Microsoft 365 aplicaciones y soluciones.

Para obtener más información, [vea publish to microsoft Teams store]([Publish your app to the Microsoft Teams store](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store))

## <a name="see-also"></a>Vea también

* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en Teams proyecto](TeamsFx-collaboration.md)