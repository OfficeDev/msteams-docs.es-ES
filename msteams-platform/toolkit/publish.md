---
title: Publicar aplicaciones de Teams con el kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, aprenderá a publicar aplicaciones de Teams mediante teams Toolkit y a publicar en un ámbito individual o en un permiso de transferencia local.
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d6333afb6d62fc832310c165c30970254998e91e
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833159"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>Publicar aplicaciones de Teams con el kit de herramientas de Teams

Después de crear la aplicación, puede distribuirla a un ámbito diferente, por ejemplo, individual, equipo, organización o cualquier usuario. La distribución depende de varios factores, como las necesidades, los requisitos técnicos y empresariales, y el objetivo de la aplicación. La distribución a un ámbito diferente puede necesitar un proceso de revisión diferente. En general, cuanto mayor sea el ámbito, más revisión tendrá que pasar la aplicación por cuestiones de seguridad y cumplimiento.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish-flow.png" alt-text="flujo de publicación":::

Esto es lo que aprenderá en esta sección:

* [Publicar en un ámbito individual o transferir localmente el permiso](#publish-to-individual-scope-or-sideload-permission)
* [Publicar en la organización](#publish-to-your-organization)
* [Publicación en la tienda de Microsoft Teams](#publish-to-microsoft-teams-store)

## <a name="prerequisites"></a>Requisitos previos

* Asegúrese de crear el [paquete de la aplicación](~/concepts/build-and-test/apps-package.md) y [validarlo](https://dev.teams.microsoft.com/appvalidation.html) para encontrar errores.
* [Habilite la carga de aplicaciones personalizadas](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) en Teams.
* Asegúrese de que la aplicación se está ejecutando y es accesible mediante HTTPs.
* Asegúrese de que ha seguido un conjunto de directrices en la publicación de la aplicación en la tienda de Microsoft Teams para publicar la aplicación.

## <a name="publish-to-individual-scope-or-sideload-permission"></a>Publicar en un ámbito individual o transferir localmente el permiso

Puede agregar una aplicación personalizada a Teams cargando un [paquete de aplicación](../concepts/build-and-test/apps-package.md) en un archivo *.zip directamente en un equipo o en contexto personal. Agregar una aplicación personalizada mediante la carga de un paquete de aplicación se conoce como instalación local. Permite probar la aplicación mientras se carga en Teams. Puede compilar y probar la aplicación en los siguientes escenarios:

* Probar y depurar una aplicación localmente.
* Cree una aplicación para usted, por ejemplo, para automatizar un flujo de trabajo.
* Cree una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.

Puede crear una aplicación solo para uso interno y compartirla con su equipo sin enviarla al catálogo de aplicaciones de Teams en la tienda de aplicaciones de Teams. Para obtener más información, consulte [Carga de la aplicación en Teams](../concepts/deploy-and-publish/apps-upload.md).

### <a name="to-build-your-app-to-zip-app-package-file"></a>Para compilar la aplicación en un archivo de paquete de aplicación zip

Primero debe ejecutar `Provision in the cloud` antes de compilar el paquete de la aplicación. Los pasos siguientes le ayudan a compilar el paquete de la aplicación.

* Seleccione **Zip Teams metadata package (Paquete de metadatos de Teams** ) en **DEPLOYMENT (IMPLEMENTACIÓN**).<br>
    El paquete de aplicación generado se ubicará en `{your project folder}/build/appPackage/appPackage.{env}.zip`.

### <a name="to-upload-app-package"></a>Para cargar el paquete de la aplicación

Realice los pasos siguientes para cargar el paquete de la aplicación:

1. En el cliente de Teams, seleccione **Aplicaciones** > **Administrar las aplicaciones** > **para cargar una aplicación**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish1.png" alt-text="publicar una aplicación":::

   **Aparece la ventana Cargar una aplicación** .

2. Seleccione **Cargar una aplicación personalizada**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/upload.png" alt-text="carga de una aplicación":::

   Ahora la aplicación se carga de forma local en el cliente de Teams y puede agregarla y verla.

## <a name="publish-to-your-organization"></a>Publicar en la organización

Cuando la aplicación esté lista para su uso en producción, puede enviarla mediante la API de envío de aplicaciones de Teams, a la que se llama desde Graph API. La API de envío de aplicaciones de Teams es un entorno de desarrollo integrado (IDE) como Microsoft Visual Studio Code instalado con el kit de herramientas de Teams. Los pasos siguientes le ayudarán a publicar la aplicación en su organización:

* [Publicación desde el kit de herramientas de Teams](#publish-from-teams-toolkit)
* [Aprobar en Administración Center](#approve-on-admin-center)

### <a name="publish-from-teams-toolkit"></a>Publicación desde el kit de herramientas de Teams

Los pasos siguientes le ayudan a publicar la aplicación desde el kit de herramientas de Teams:

1. Puede publicar la aplicación de Teams de una de las siguientes maneras:
     * Seleccione **Publicar en Teams** en **IMPLEMENTACIÓN** en la vista de árbol del kit de herramientas de Teams.
     * Escriba el desencadenador **Teams: Publicar en Teams** desde la paleta de comandos.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-publish.png" alt-text="Seleccione Publicar.":::

1. Seleccione **Instalar para su organización**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/installforyourorganization.png" alt-text="Instalar para la organización":::

   Ahora la aplicación se publica correctamente en el portal de administración y verá el siguiente aviso:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/confirm-publish.png" alt-text="Confirmar publicación":::

Ahora la aplicación está disponible en el Centro de administración de **Administrar aplicaciones** de Microsoft Teams, donde usted y el administrador pueden revisarla y aprobarla.

> [!NOTE]
> La aplicación aún no se publica en la tienda de aplicaciones de la organización. El paso envía la aplicación al Centro de administración de Microsoft Teams, donde puede aprobarla para publicarla en la tienda de aplicaciones de su organización.

### <a name="approve-on-admin-center"></a>Aprobar en Administración Center

El kit de herramientas de Teams para Visual Studio Code se basa en la API de envío de aplicaciones de Teams y le permite automatizar el proceso de envío a aprobación para aplicaciones personalizadas en Teams.

  > [!NOTE]
  > Asegúrese de que tiene un proyecto de aplicación de Teams en VS Code. Como administrador, **Administrador de aplicaciones** en el [ Center de administración de Microsoft Teams](https://admin.teams.microsoft.com/policies/manage-apps) es donde puede ver y administrar todas las aplicaciones de Teams para su organización. Puede realizar las siguientes actividades en el centro de administración:
  >
  > * Consulte el estado de nivel de organización y las propiedades de las aplicaciones.
  > * Apruebe o cargue nuevas aplicaciones personalizadas en la tienda de aplicaciones de su organización.
  > * Bloquear o permitir aplicaciones en el nivel de organización.
  > * Agregar aplicaciones a Teams.
  > * Comprar servicios para aplicaciones de terceros.
  > * Ver los permisos solicitados por las aplicaciones.
  > * Conceder consentimiento de administrador a las aplicaciones.
  > * [Administrar la configuración de la aplicación en toda la organización](https://admin.teams.microsoft.com/policies/manage-apps).

Los pasos siguientes le ayudan a aprobar desde Administración Center:

1. Seleccione **Ir al portal de administración**.

1. Seleccione el :::image type="icon" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Showall.PNG"::: icono > **aplicación** > **De administración de aplicaciones** de Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manage-apps.png" alt-text="Seleccione Administrar aplicaciones.":::

   Puede ver todas las aplicaciones de Teams de su organización.

   En el widget Aprobación pendiente en la parte superior de la página, podrá saber cuándo se envía una aplicación personalizada para su aprobación. En la tabla, una aplicación recién enviada publica automáticamente el estado de las aplicaciones enviadas y bloqueadas. Puede ordenar la columna de estado de publicación en orden descendente para buscar la aplicación.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="aprobación":::

1. Seleccione el nombre de la aplicación para ir a la página de detalles. En la pestaña **Acerca de** , puede ver detalles sobre la aplicación, incluida la descripción, el estado y el identificador de la aplicación.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="aplicaciones enviadas":::

1. Seleccione la lista desplegable de estado y cambie de **Enviado** a **Publicar**.

   Después de publicar la aplicación, el estado de publicación cambia a publicado y el estado cambia automáticamente a permitido.

   Para obtener más información, consulte [Publicación en su organización](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json).

## <a name="publish-to-microsoft-teams-store"></a>Publicación en la tienda de Microsoft Teams

Puede distribuir la aplicación directamente en la tienda dentro de Microsoft Teams y llegar a millones de usuarios en todo el mundo. Si la aplicación también aparece en la tienda, podría llegar instantáneamente a sus clientes potenciales. Las aplicaciones publicadas en la tienda de Teams también se enumeran automáticamente en Microsoft AppSource, que es el marketplace oficial para aplicaciones y soluciones de Microsoft 365.

Para obtener más información, consulte [Publicación de la aplicación en la tienda de Microsoft Teams](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store).

## <a name="see-also"></a>Vea también

* [Distribución de la aplicación de Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md)
* [Crear un paquete de aplicación de Microsoft Teams](../concepts/build-and-test/apps-package.md)
* [Preparar el espacio empresarial de Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md)
* [Publique su aplicación en la tienda de Microsoft Teams](../concepts/deploy-and-publish/appsource/publish.md)
* [Cargar la aplicación en Microsoft Teams](../concepts/deploy-and-publish/apps-upload.md)
* [Administración de aplicaciones de Teams en el Centro de administración de Microsoft Teams](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json)
