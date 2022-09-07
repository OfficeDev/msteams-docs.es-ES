---
title: Requisitos previos para crear la aplicación de Teams mediante Visual Studio Code
author: zyxiaoyuer
description: En este módulo, obtenga información sobre los requisitos previos necesarios para Herramientas y SDK.
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 412b7bfedb6ba39f1d38f42aac56cc793ea385b1
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617279"
---
# <a name="prerequisites-for-creating-your-teams-app"></a>Requisitos previos para crear la aplicación de Teams

Asegúrese de que se cumplen los siguientes requisitos previos antes de empezar a crear la aplicación de Teams:

* [Requisitos básicos para compilar la aplicación de Teams](#basic-requirements-to-build-your-teams-app)
* [Preparar cuentas para compilar la aplicación de Teams](#accounts-to-build-your-teams-app)
* [Permiso de instalación local](#sideloading-permission)

## <a name="basic-requirements-to-build-your-teams-app"></a>Requisitos básicos para compilar la aplicación de Teams

Asegúrese de que se cumplen los siguientes requisitos antes de empezar a compilar la aplicación de Teams:

| &nbsp; | Requisitos básicos | Para usar| Para el tipo de entorno|
   | --- | --- | --- |
   | **Required** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | Kit de herramientas de Teams| Extensión de Microsoft Visual Studio Code que crea un scaffolding de proyecto para la aplicación. Use la versión más reciente. | JavaScript y SPFx|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Colabore con todos los usuarios con los que trabaja a través de aplicaciones para chat, reuniones, llamadas, todo en un solo lugar.| JavaScript y SPFx|
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | Entorno de tiempo de ejecución de JavaScript de back-end. Use la versión v16 LTS más reciente.| JavaScript y SPFx|
   | &nbsp; |[Administrador de paquetes de Node (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx) | Instale y administre paquetes para su uso en aplicaciones Node.js y ASP.NET Core.| JavaScript y SPFx|
   | &nbsp; | [Microsoft&nbsp; Edge](https://www.microsoft.com/edge) (recomendado) o [Google Chrome](https://www.google.com/chrome/) | Un explorador con herramientas de desarrollo. | JavaScript y SPFx|
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | Entornos de compilación de JavaScript, TypeScript o SharePoint Framework (SPFx). Use la versión 1.55 o posterior. | JavaScript y SPFx|
   | **Optional** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | [Herramientas de Azure para Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) y [la CLI de Azure](/cli/azure/install-azure-cli) | Acceda a los datos almacenados o implemente un back-end basado en la nube para la aplicación de Teams en Azure. | JavaScript|
   | &nbsp; | [React Developer Tools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) OR [React Developer Tools for Microsoft&nbsp;Edge](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil) | Extensión DevTools del explorador para la biblioteca de Código abierto React JavaScript. | JavaScript|
   | &nbsp; | [Explorador de Microsoft Graph](https://developer.microsoft.com/graph/graph-explorer) | Herramienta basada en explorador que permite ejecutar una consulta desde datos de Microsoft Graph. | JavaScript y SPFx|
   | &nbsp; | [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/) | Portal basado en web para configurar, administrar y distribuir la aplicación de Teams, incluida su organización o la tienda de Teams.| JavaScript y SPFx|

   > [!NOTE]
   >
   > * El documento se prueba con la versión 4.0.0 del kit de herramientas de Teams y nodejs, versión 16.
   > * Marque el Explorador de Microsoft Graph para obtener información sobre los servicios de Microsoft Graph. Esta herramienta basada en explorador permite consultar y acceder a Microsoft Graph fuera de una aplicación.

## <a name="accounts-to-build-your-teams-app"></a>Cuentas para compilar la aplicación de Teams

Asegúrese de que tiene las siguientes cuentas antes de empezar a compilar la aplicación de Teams:

| Cuentas | Para usar| Para el tipo de entorno|
| --- | --- |
|[Cuenta de Microsoft 365 con una suscripción válida](#microsoft-365-developer-program)|Cuenta de desarrollador de Teams al desarrollar una aplicación.| JavaScript y SPFx|
|[Cuenta de Azure](accounts.md#azure-account-to-host-backend-resources)|Recursos de back-end en Azure.| JavaScript y SPFx|
|[Cuenta de administrador del sitio de colección de SharePoint](#sharepoint-collection-site-administrator-account) |Implementación para el hospedaje.| SPFx|

### <a name="microsoft-365-developer-program"></a>Programa de desarrolladores de Microsoft 365

Para crear una cuenta de Microsoft 365, regístrese para obtener una suscripción al programa para desarrolladores de Microsoft 365. La suscripción es gratuita durante 90 días y continúa renovándose mientras se use para actividades de desarrollo.

Si tiene una suscripción de Visual Studio Enterprise o Professional, ambos programas incluyen una [suscripción de desarrollador](https://aka.ms/MyVisualStudioBenefits) de Microsoft 365 gratuita. Seguirá activa mientras la suscripción a Visual Studio también lo esté. Para obtener más información, vea [suscripción de desarrollador de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).

Puede registrarse en el programa de desarrolladores con uno de los siguientes tipos de cuenta:

* **Cuenta de Microsoft para uso personal**

  :::row:::

    :::column span="3":::

       La cuenta le proporciona acceso a productos y servicios en la nube de Microsoft, como Outlook, Messenger, OneDrive, MSN, Xbox Live o Microsoft 365. 

       Puede registrarse para obtener un buzón de Outlook.com y, así, crear una cuenta de Microsoft que se puede usar para acceder a Azure o a servicios en la nube de Microsoft relacionados con el consumidor.

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/personal-account-icon.png" alt-text="cuenta personal.":::
   :::column-end:::

  :::row-end:::

* **Cuenta profesional de Microsoft para empresas**

  :::row:::

    :::column span="3":::

       La cuenta proporciona acceso a todos los servicios en la nube de Microsoft de nivel empresarial, medianos y pequeños. Los servicios incluyen Azure, Microsoft Intune o Microsoft 365. 

       Cuando inicia sesión como una organización en uno de estos servicios, un directorio en la nube se aprovisiona automáticamente en Azure AD para representar a su organización.

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/work-account-icon.png" alt-text="cuenta profesional.":::
    :::column-end:::

  :::row-end:::

#### <a name="create-a-free-microsoft-365-developer-account"></a>Creación de una cuenta gratuita para desarrolladores de Microsoft 365

Para crear una cuenta de desarrollador gratuita de Microsoft 365, únase al programa para desarrolladores de Microsoft 365 y realice la siguiente cuenta:

1. Vaya al [programa para desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Seleccione **Unirse ahora**.
1. Configure su cuenta de administrador.

   Puede ver la siguiente imagen después de completar la suscripción:

    :::image type="content" source="../assets/images/teams-toolkit-v2/m365-account.png" alt-text="Cuenta de M365":::

### <a name="azure-account"></a>Cuenta de Azure

Necesita una cuenta de Azure para hospedar una aplicación de Teams o los recursos de back-end de la aplicación de Teams mediante el kit de herramientas de Teams en Visual Studio Code. Debe necesitar una suscripción de Azure en los siguientes escenarios:

* Si ya tiene una aplicación existente en un proveedor de nube diferente a Azure y quiere integrar la aplicación en la plataforma Teams, debe tener una suscripción a Azure.
* Puede seleccionar una suscripción de Azure para hospedar los recursos de back-end mediante otro proveedor de nube o en sus propios servidores si están disponibles en el dominio público.

> [!NOTE]
> Debe [crear una cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.

### <a name="sharepoint-collection-site-administrator-account"></a>Cuenta de administrador del sitio de colección de SharePoint

Al crear una aplicación de Teams mediante el entorno SPFx, necesitará una cuenta de administrador del sitio de recopilación de SharePoint en la implementación para el hospedaje. Si usa un inquilino del programa para desarrolladores de Microsoft 365, puede usar la cuenta de administrador que creó en ese momento.

## <a name="sideloading-permission"></a>Permiso de instalación local

Después de crear la aplicación, debe cargarla en Teams sin distribuirla. Este proceso se conoce como instalación de prueba. Inicie sesión en su cuenta de Microsoft 365 para ver esta opción.

Puede comprobar si el permiso de instalación de prueba está habilitado con Visual Studio Code o con el cliente de Teams.

<br>
<details>
<summary><b>Comprobar el permiso de instalación de prueba mediante Visual Studio Code</b></summary>

1. Abra **Visual Studio Code**.
1. Seleccione el icono kit de herramientas de :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams en la barra de herramientas del kit de herramientas de Teams.

   > [!NOTE]
   > Si no puede ver la opción, consulte [Instalación del kit de herramientas de Teams](install-Teams-Toolkit.md) para instalar la extensión Teams Toolkit en Visual Studio Code.
1. Seleccione **Iniciar sesión en M365** en **CUENTAS** e iniciar sesión en su cuenta de Microsoft 365.

    :::image type="content" source="../assets/images/teams-toolkit-v2/accounts.png" alt-text="detalles de las cuentas":::

1. Compruebe si puede ver la opción **Instalación de prueba habilitada** como se muestra en la siguiente imagen:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="Habilitar la instalación prueba":::

</details>
<br>
<details>
<summary><b>Comprobar el permiso de instalación de prueba mediante el cliente de Teams</b></summary>

1. En el cliente de Teams, seleccione **Aplicaciones**.
1. Seleccione **Administrar la aplicación**.
1. Seleccione **Cargar una aplicación**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-app.png" alt-text="Publicar una aplicación":::

4. Compruebe si puede ver la opción **Cargar una aplicación personalizada** como se muestra en la siguiente imagen:

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-custom-app1.png" alt-text="Cargar una aplicación personalizada":::.

</details>

### <a name="enable-sideloading-using-admin-center"></a>Habilitación de la instalación local mediante el Centro de administración

Si no puede ver la opción **Cargar una aplicación personalizada,** indica que no tiene el permiso necesario para la instalación local.

* Para un administrador de inquilinos, habilite la configuración de instalación de prueba para su inquilino u organización en el Centro de administración de Teams.
* Si no es administrador de inquilinos, deberá ponerse en contacto con el administrador de inquilinos para habilitar la instalación de prueba.

Si tiene derechos de administrador, siga estos pasos para cargar la aplicación personalizada mediante el Centro de administración:

  1. Inicie sesión en el [Centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.

  1. Seleccione el :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG"::: icono > **Teams**.

       :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center.png" alt-text="centro de Administración de Microsoft 365":::

     > [!Note]
     > La opción **Teams** puede tardar **hasta 24 horas** en aparecer. Puede [cargar la aplicación personalizada en un entorno de Teams](/microsoftteams/upload-custom-apps) para pruebas y validación.

  1. Inicie sesión en el Centro de administración de Microsoft Teams con sus credenciales de administrador.
  1. Seleccione el :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG"::: icono > **directivas****de instalación de aplicaciones** >  de Teams.

     :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center1.png" alt-text="centro de Administración de Microsoft 365 1":::

  1. Seleccione **Global (valor predeterminado para toda la organización)**

     :::image type="content" source="../assets/images/teams-toolkit-v2/select-manage-policies.png" alt-text="Seleccione Administrar directivas.":::

  1. Establezca el botón de alternancia **Carga de aplicaciones personalizadas** en la posición **Activado**.

     :::image type="content" source="../assets/images/teams-toolkit-v2/Upload-custom-apps.png" alt-text="Carga de aplicaciones personalizadas":::

  5. Haga clic en **Guardar**.

     > [!Note]
     > La instalación de prueba puede tardar hasta 24 horas en activarse. Mientras tanto, puede usar **cargar para el inquilino** y, así, probar la aplicación. Para cargar el archivo de paquete .zip de la aplicación, consulte [Cargar aplicaciones personalizadas](/microsoftteams/teams-app-setup-policies).

     Asegúrese de que, ahora tiene el permiso de instalación local mediante los pasos mencionados en [Comprobación del permiso de instalación local mediante Visual Studio Code o cliente de Teams.](#sideloading-permission)

</details>

## <a name="see-also"></a>Vea también

* [Administrar configuración y directivas de aplicación personalizadas en Teams](/microsoftteams/teams-custom-app-policies-and-settings)
* [Administrar directivas de configuración de aplicación en Teams](/microsoftteams/teams-app-setup-policies)
* [Carga de aplicaciones personalizadas](/microsoftteams/teams-app-setup-policies)
* [Aprovisionamiento de recursos en la nube mediante el kit de herramientas de Teams](provision.md)
* [Implementar la aplicación de Teams en la nube](deploy.md)
