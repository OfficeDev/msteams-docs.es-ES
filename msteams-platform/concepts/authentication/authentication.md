---
title: Autenticación de usuarios de aplicaciones
description: Describe la autenticación en Teams y cómo usarla en las aplicaciones
ms.topic: conceptual
ms.localizationpriority: medium
keywords: autenticación de teams Microsoft Azure Active Directory SSO de OAuth (Azure AD)
ms.openlocfilehash: db1a16959755668ec9aa298ed355ef657503ca03
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2022
ms.locfileid: "65887761"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Autenticar usuarios en Microsoft Teams

La autenticación consiste en validar a los usuarios de la aplicación y proteger a los usuarios de la aplicación y de la aplicación contra el acceso injustificado. Puede usar un método de autenticación adecuado para que la aplicación valide a los usuarios de la aplicación que quieran usar la aplicación de Teams.

Elija agregar autenticación para la aplicación de una de las dos maneras siguientes:

- **Habilitar el inicio de sesión único (SSO) en una aplicación de Teams**: el inicio de sesión único en Teams es un método de autenticación que usa la identidad de Teams de un usuario de la aplicación para proporcionarle acceso a la aplicación. Un usuario que haya iniciado sesión en Teams no tiene que volver a iniciar sesión en la aplicación en el entorno de Teams. Con solo un consentimiento necesario del usuario de la aplicación, la aplicación de Teams recupera los detalles de acceso de Azure Active Directory (AD). Una vez que el usuario de la aplicación ha dado su consentimiento, puede acceder a la aplicación incluso desde otros dispositivos sin tener que volver a validarla.

- **Habilitar la autenticación con un proveedor de OAuth de terceros**: puede usar un proveedor de identidades de OAuth (IdP) de terceros para autenticar a los usuarios de la aplicación. El usuario de la aplicación está registrado con el proveedor de identidades, que tiene una relación de confianza con la aplicación. Cuando el usuario intenta iniciar sesión, el proveedor de identidades valida al usuario de la aplicación y le proporciona acceso a la aplicación. Azure AD es uno de estos proveedores de OAuth de terceros. Puede usar otros proveedores, como Google, Facebook, GitHub o cualquier otro proveedor.

## <a name="select-authentication-method"></a>Selección del método de autenticación

Habilite la autenticación con sso o idP de OAuth de terceros en la aplicación de pestaña, la aplicación de bot y la aplicación de extensión de mensajería. Seleccione uno de los dos métodos para agregar autenticación en la aplicación:

:::row:::
    :::column span="1":::
        SSO
    :::column-end:::
    :::column span="1":::
        &nbsp;
    :::column-end:::
    :::column span="1":::
        OAuth
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-sso-icon.png" alt-text="Inicio de sesión único para la aplicación de pestaña" link="../../tabs/how-to/authentication/tab-sso-overview.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **Aplicación tab**  
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-app-idp.png" alt-text="Autenticación con un proveedor de OAuth de terceros para la aplicación de pestaña." link="../../tabs/how-to/authentication/auth-tab-aad.md" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-sso-icon.png" alt-text="Inicio de sesión único para la aplicación bot" link="../../bots/how-to/authentication/auth-aad-sso-bots.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **Aplicación bot**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-app-idp.png" alt-text="Autenticación con un proveedor de OAuth de terceros para la aplicación bot." link="../../bots/how-to/authentication/add-authentication.md" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-sso-icon.png" alt-text="Inicio de sesión único para la aplicación de extensión de mensajería" link="../../messaging-extensions/how-to/enable-SSO-auth-me.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; **Aplicación de extensión de mensaje**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-app-idp.png" alt-text="Autenticación con idP de oAuth de terceros para la aplicación de extensión de mensajería." link="../../messaging-extensions/how-to/add-authentication.md" border="false":::
    :::column-end:::
:::row-end:::

> [!NOTE]
> La página Autenticación silenciosa se mueve al módulo Recursos. Para obtener más información, consulte [Autenticación silenciosa](../../tabs/how-to/authentication/auth-silent-aad.md).

## <a name="see-also"></a>Vea también

- [Habilitación del inicio de sesión único en una aplicación de pestaña](../../tabs/how-to/authentication/tab-sso-overview.md)
- [Flujo de autenticación de Microsoft Teams para pestañas](~/tabs/how-to/authentication/auth-flow-tab.md)
- [Compatibilidad con inicio de sesión único para bots](~/bots/how-to/authentication/auth-aad-sso-bots.md)
- [Agregar autenticación a la extensión de mensaje](~/messaging-extensions/how-to/add-authentication.md)
