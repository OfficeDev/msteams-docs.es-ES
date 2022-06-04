---
title: Configuración del consentimiento del administrador
description: Describe la configuración del consentimiento del administrador
ms.topic: how-to
ms.localizationpriority: medium
keywords: Pestañas de autenticación de teams De Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: dd954ef1ede05b6025b12512dfcee03044223642
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888309"
---
# <a name="configure-admin-consent"></a>Configuración del consentimiento del administrador

Puede definir el ámbito de la aplicación para una API expuesta y determinar si los usuarios pueden dar su consentimiento a este ámbito en los directorios donde está habilitado el consentimiento del usuario. Solo puede permitir que los administradores proporcionen consentimiento para permisos con privilegios superiores.

## <a name="to-expose-an-api"></a>Para exponer una API

1. Seleccione **Administrar** > **Exponer una API** en el panel izquierdo.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="Opción de menú Exponer una API." border="false":::

    Aparece **la página Exponer una API** .

1. Seleccione **Establecer** para generar el URI del identificador de aplicación.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="Establecimiento del URI del identificador de aplicación" border="false":::

    Aparece la sección para establecer el URI del identificador de aplicación.

1. Escriba el URI del identificador de aplicación y, a continuación, seleccione **Guardar**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="URI de id. de aplicación" border="true":::

    Aparece un mensaje en el explorador que indica que se actualizó el URI del identificador de aplicación.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text="Mensaje uri de id. de aplicación" border="false":::

    El URI del identificador de aplicación se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text="Uri de id. de aplicación actualizado" border="false":::

## <a name="to-configure-api-scope"></a>Para configurar el ámbito de la API

1. Seleccione **+ Agregar un ámbito** en la sección **Ámbitos definidos por esta API** .

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="Seleccionar ámbito" border="true":::

    Aparece **la página Agregar un ámbito** .

1. Escriba los detalles de la aplicación para el ámbito de la aplicación.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="Agregar detalles del ámbito" border="true":::

    1. Escriba el nombre del ámbito. Este campo es obligatorio.
    1. Seleccione **Administradores y usuarios** para configurar los usuarios que pueden dar su consentimiento para usar las credenciales de inicio de sesión del usuario. La opción predeterminada es **Solo administradores**.
    1. Escriba el **nombre para mostrar del consentimiento del administrador**. Este campo es obligatorio.
    1. Escriba la descripción del consentimiento del administrador. Este campo es obligatorio.
    1. Escriba el **nombre para mostrar consentimiento del usuario**.
    1. Escriba la descripción del consentimiento del usuario.
    1. Seleccione la opción **Habilitado** para el estado.
    1. Seleccione **Agregar ámbito**.

    Aparece un mensaje en el explorador que indica que se agregó el ámbito.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="Mensaje agregado de ámbito" border="false":::

    El URI del identificador de aplicación se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="Ámbito agregado y mostrado" border="false":::

## <a name="to-configure-authorized-client-application"></a>Para configurar la aplicación cliente autorizada

1. Vaya a la página **Exponer una API** a la sección **Aplicación cliente autorizada** y seleccione **+ Agregar una aplicación cliente**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="Aplicación cliente autorizada" border="true":::

    Aparece **la página Agregar una aplicación cliente** .

1. Escriba los detalles para agregar una aplicación cliente. En esta sección, agregará dos aplicaciones cliente.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="Adición de una aplicación cliente" border="true":::

    1. Escriba **1fec8e78-bce4-4aaf-ab1b-5451cc387264** como identificador de cliente para la aplicación móvil o de escritorio de Teams.
    1. Seleccione el identificador de aplicación que creó para la aplicación para los **ámbitos autorizados**.
    1. Seleccione **Agregar aplicación**.

    Aparece un mensaje en el explorador que indica que se agregó la aplicación cliente.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Mensaje agregado de la aplicación cliente" border="false":::

    Los identificadores de aplicación cliente se muestran en la página.

1. Repita el paso anterior para agregar la aplicación cliente para la aplicación web de Teams.

    1. Escriba **5e3ce6c0-2b1f-4285-8d4b-75ee78787346** como identificador de cliente para la aplicación web.
    1. Seleccione el identificador de aplicación que creó para la aplicación para los **ámbitos autorizados**.
    1. Seleccione **Agregar aplicación**.

    Aparece un mensaje en el explorador que indica que se agregó la aplicación cliente.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Mensaje agregado de aplicación cliente para la aplicación web" border="false":::

    Los identificadores de aplicación cliente se muestran en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="Aplicación cliente agregada y mostrada" border="true":::
