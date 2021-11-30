---
title: Publicar Teams aplicaciones con Teams Toolkit
author: zyxiaoyuer
description: publicar Teams aplicaciones
ms.author: yanjiang
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3060a3b36f63c30a6068887ab3112cfe49d16ae5
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228200"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>Publicar Teams aplicaciones con Teams Toolkit

Después de crear la aplicación, puedes distribuir la aplicación a diferentes ámbitos, como individual, de equipo, de organización o de cualquier persona. La distribución depende de varios factores, como las necesidades, los requisitos técnicos y empresariales, y el objetivo de la aplicación. La distribución a distinto ámbito puede necesitar un proceso de revisión diferente. En general, cuanto mayor sea el ámbito, más revisión tendrá que pasar la aplicación por cuestiones de seguridad y cumplimiento.

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Ya deberías tener un proyecto Teams aplicación.

## <a name="publish-to-individual-scope-sideloading-permission"></a>Publicar en un ámbito individual (permiso de instalación local)

Los usuarios pueden agregar aplicaciones personalizadas a Teams cargando un paquete de aplicación en un archivo .zip directamente a un equipo o en contexto personal. Agregar una aplicación personalizada cargando un paquete de aplicación, también conocido como carga lateral, te permite probar la aplicación mientras se está desarrollando, antes de que esté lista para distribuirse ampliamente, como se mencionó en los siguientes escenarios:

* Pruebe y depure una aplicación localmente usted mismo o con otros desarrolladores.
* Ha creado una aplicación solo para usted. Por ejemplo, para automatizar un flujo de trabajo.
* Has creado una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.

También te permite crear una aplicación solo para uso interno y compartirla con tu equipo sin enviarla al catálogo de aplicaciones de Teams en la Teams de aplicaciones.

* Crear la aplicación en *.zip archivo de paquete de la aplicación

    Puedes crear el paquete de la aplicación seleccionando `Zip Teams metadata package` en el panel IMPLEMENTACIÓN en Vista de árbol de Teams Toolkit. Es posible que deba `Provision in the cloud` ejecutarse al principio. El paquete de aplicación generado se ubicará `{your project folder}/build/appPackage/appPackage.{env}.zip` en, como se muestra en la siguiente imagen:

 ![cargar aplicación personalizada](./images/sideload-check.png)

## <a name="publish-to-your-organization"></a>Publicar en la organización 

Cuando la aplicación esté lista para su uso en producción, el desarrollador puede enviar la aplicación mediante la API de envío de aplicaciones de Teams, llamada desde la API de Graph, un entorno de desarrollo integrado (IDE), como Visual Studio Code instalado con el kit de herramientas de Teams. Puede seleccionar Publicar a **Teams** desde el panel IMPLEMENTACIÓN en TreeView de Teams Toolkit o desencadenar **Teams: Publicar** en Teams desde la paleta de comandos. A **continuación, seleccione Instalar para su organización** como se muestra en la siguiente imagen:

![Instalar para su organización](./images/installforyourorganization.png)

Al hacerlo, la aplicación está disponible en la página Administrar aplicaciones del Centro de administración de Microsoft Teams, donde tú y el administrador pueden revisarla y aprobarla.

Como administrador, la página administrar aplicaciones del Centro de administración de [Microsoft Teams](https://admin.teams.microsoft.com/policies/manage-apps) es donde se ven y administran todas las Teams de la organización. Aquí, puedes ver el estado y las propiedades de las aplicaciones a nivel de organización, aprobar o cargar nuevas aplicaciones personalizadas en la tienda de aplicaciones de tu organización, bloquear o permitir aplicaciones en el nivel de la organización, agregar aplicaciones a equipos, comprar servicios para aplicaciones de terceros, ver los permisos solicitados por las aplicaciones, conceder el consentimiento de administrador a las aplicaciones y administrar la configuración de aplicaciones para toda la organización.

Página Administrar aplicaciones en teams [admin center](https://admin.teams.microsoft.com/policies/manage-apps) Teams toolkit for Visual Studio Code built on top of the Teams App Submission API and it allows you to automates the submission-to-approval process for custom apps on Teams.

> [!NOTE]
> Ten en cuenta que esto aún no publica la aplicación en la tienda de aplicaciones de tu organización. Este paso envía la aplicación al Centro de administración de Microsoft Teams donde puedes aprobarla para su publicación en la tienda de aplicaciones de la organización.

## <a name="admin-approval-for-submitted-teams-apps"></a>Aprobación de administrador para aplicaciones Teams enviadas

El administrador del inquilino de Teams puede ir a la página Administrar aplicaciones en el Centro de administración de Microsoft Teams (en la navegación izquierda, vaya Teams aplicaciones > Administrar aplicaciones), le ofrece una vista de todas las aplicaciones de Teams para su organización. El widget Aprobación pendiente en la parte superior de la página te permite saber cuándo se envía una aplicación personalizada para su aprobación.
En la tabla, una aplicación recién enviada muestra automáticamente un estado de publicación de Enviado y Estado de bloqueado. Puedes ordenar la columna Estado de publicación en orden descendente para encontrar rápidamente la aplicación:

 ![Aprobación de administrador para la aplicación de teams enviada](./images/admin-approval-for-teams-app.png)

Selecciona el nombre de la aplicación para ir a la página de detalles de la aplicación. En la pestaña Acerca de, puedes ver detalles sobre la aplicación, como la descripción, el estado, el enviador y el identificador de la aplicación:

 ![Detalles sobre la aplicación de teams enviada aprobada por el administrador](./images/about-submitted-app.png)

Cuando estés listo para que la aplicación esté disponible para los usuarios, sigue los pasos para publicar la aplicación:

1. En la navegación izquierda del Centro Microsoft Teams administración, ve a Teams aplicaciones > Administrar aplicaciones.
2. Selecciona el nombre de la aplicación para ir a la página de detalles de la aplicación y, a continuación, en el cuadro Estado de publicación, selecciona Publicar.
Después de publicar la aplicación, el estado de publicación cambia a Publicado y el estado cambia automáticamente a Permitido.

## <a name="publish-to-microsoft-store"></a>Publicar en Microsoft Store

Puedes distribuir la aplicación directamente a la tienda dentro de Microsoft Teams y llegar a millones de usuarios de todo el mundo. Si la aplicación también se incluye en la tienda, puedes llegar al instante a los clientes potenciales.
Las aplicaciones publicadas en la tienda Teams también listan automáticamente en Microsoft AppSource, que es el mercado oficial para Microsoft 365 aplicaciones y soluciones.
Comprender el proceso de publicación Cuando sientas que la aplicación está lista para la producción, puedes comenzar el proceso de obtenerla en la Teams tienda.

>[!Tip]
> Seguir los pasos previos al envío puede aumentar la posibilidad de que Microsoft apruebe la aplicación para su publicación.

![Pasos de envío previo](./images/pre-submission-steps.png)

* Revisa las Teams de validación de la tienda para asegurarte de que la aplicación cumple Teams estándares de la aplicación y la tienda.
* Crear una cuenta de desarrollador del Centro de partners.
* Prepare el envío de la tienda, que incluye la ejecución de pruebas automatizadas, la compilación de notas de pruebas, la creación de una descripción de la tienda, entre otras tareas importantes para ayudar a acelerar el proceso de revisión.
* Envía tu aplicación a través del Centro de partners.
* Trabaje con Microsoft directamente para resolver los problemas y volver a enviar la aplicación (vínculo para resolver los problemas y volver a enviar la aplicación).

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Administrar varios entornos](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [Colaborar con otros desarrolladores en Teams proyecto](TeamsFx-collaboration.md)