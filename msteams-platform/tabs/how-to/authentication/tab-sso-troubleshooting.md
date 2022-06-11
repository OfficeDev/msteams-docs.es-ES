---
title: Solución de problemas de autenticación para pestañas mediante sso en Teams
description: Solución de problemas de autenticación de SSO en Teams y cómo usarla en pestañas
ms.topic: how-to
ms.localizationpriority: medium
keywords: Preguntas sobre errores de inicio de sesión único en las pestañas de autenticación de teams Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 74246dce24869bb4645045950de01c179ba129d8
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032812"
---
# <a name="troubleshooting-sso-authentication-in-teams"></a>Solución de problemas de autenticación de SSO en Teams

Esta es una lista de problemas y preguntas sobre el inicio de sesión único y cómo puede corregirlos.
<br>

## <a name="support-for-microsoft-graph"></a>Compatibilidad con Microsoft Graph

<br>
<details>
<summary>1. ¿Graph API funciona en Postman?</summary>
<br>
Puede usar la colección Microsoft Graph Postman con las API de Microsoft Graph.

Para más información, consulte [Usar Postman con la API de Microsoft Graph](/graph/use-postman).
</details>
<br>
<details>
<summary>2. ¿Funciona Graph API en el Explorador de Microsoft Graph?</summary>
<br>
Sí, Graph API funciona en el Explorador de Microsoft Graph.

Para obtener más información, consulte [Graph explorador](https://developer.microsoft.com/graph/graph-explorer).

</details>
<br>

## <a name="error-messages-and-how-to-handle-them"></a>Mensajes de error y cómo controlarlos

<br>
<details>
<summary>1. Error: falta el consentimiento.</summary>
<br>
Cuando Azure AD recibe una solicitud para acceder a un recurso de Microsoft Graph, comprueba si el usuario (o Administrador de inquilinos) ha dado su consentimiento para este recurso. Si no hay ningún registro de consentimiento del usuario o administrador, Azure AD envía un mensaje de error al servicio web.

El código debe indicar al cliente (por ejemplo, en el cuerpo de una respuesta 403 Prohibido) cómo controlar el error:

- Si la aplicación de pestaña necesita ámbitos de Microsoft Graph para los que solo un administrador puede dar su consentimiento, el código debe generar un error.
- Si los únicos ámbitos necesarios pueden ser otorgados por el usuario, entonces el código debe recurrir a un sistema alternativo de autenticación de usuario.

</details>
<br>
<details>
<summary>2. Error: Falta ámbito (permiso).</summary>
<br>
Este error solo se ve durante el desarrollo.

Para controlar este error, el código del lado servidor debe enviar una respuesta 403 Prohibido al cliente. Debe registrar el error en la consola o registrarlo en un registro.
</details>
<br>
<details>
<summary>3. Error: Audiencia no válida en el token de acceso para Microsoft Graph.</summary>
<br>
El código del lado servidor debe enviar una respuesta 403 Prohibido al cliente para mostrar un mensaje al usuario. Se recomienda que también registre el error en la consola o que lo registre en un registro.
</details>
<br>
<details>
<summary>4. Error: El nombre de host no debe basarse en un dominio que ya pertenece.</summary>
<br>
Puede obtener este error en uno de los dos escenarios:

1. El dominio personalizado no se agrega a Azure AD. Para agregar un dominio personalizado a Azure AD y registrarlo, siga el procedimiento [Agregar un nombre de dominio personalizado a Azure AD](/azure/active-directory/fundamentals/add-custom-domain) y, a continuación, siga los pasos para [configurar el ámbito para el token de acceso](tab-sso-register-aad.md#configure-scope-for-access-token) de nuevo.
1. No ha iniciado sesión con las credenciales de administrador en el inquilino de Microsoft 365. Inicie sesión en Microsoft 365 como administrador.

</details>
<br>
<details>
<summary>5. Error: El nombre principal de usuario (UPN) no se recibe en el token de acceso devuelto.</summary>
<br>
Puede agregar UPN como una notificación opcional en Azure AD.

Para obtener más información, consulte [Proporcionar notificaciones opcionales a la aplicación](/azure/active-directory/develop/active-directory-optional-claims) y [tokens de acceso](/azure/active-directory/develop/access-tokens).
</details>
<br>
<details>
<summary>6. Error: Teams error del SDK: resourceDisabled.</summary>
<br>
Para evitar este error, asegúrese de que el URI del identificador de aplicación esté configurado correctamente en el registro de aplicaciones de Azure AD y en el cliente de Teams.

Para obtener más información sobre el URI del identificador de aplicación, consulte [Para exponer una API](tab-sso-register-aad.md#to-expose-an-api).

</details>
<br>

<details>
<summary>7. Error: Error genérico al ejecutar la aplicación de pestaña.</summary>
<br>
Puede aparecer un error genérico cuando una o varias configuraciones de aplicación realizadas en Azure AD son incorrectas. Para resolver este error, compruebe si los detalles de la aplicación configurados en el código y Teams manifiesto coinciden con los valores de Azure AD.

En la imagen siguiente se muestra un ejemplo de los detalles de la aplicación configurados en Azure AD.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-app-details.png" alt-text="Valores de configuración de la aplicación en Azure AD" border="false":::

Compruebe que los siguientes valores coinciden entre Azure AD, el código del lado cliente y Teams manifiesto de aplicación:

- **Id. de** aplicación: el identificador de aplicación que generó en Azure AD debe ser el mismo en el código y en Teams archivo de manifiesto. Compruebe el identificador de la aplicación en Teams manifiesto coincide con el **identificador de aplicación (cliente)** de Azure AD.

- **Secreto de** aplicación: el secreto de aplicación configurado en el back-end de la aplicación debe coincidir con **las credenciales de cliente** de Azure AD.
    También debe comprobar si el secreto de cliente ha expirado.

- **URI del identificador de** aplicación: el URI del identificador de aplicación en el código y en Teams archivo de manifiesto de la aplicación debe coincidir con el **URI del identificador de aplicación** en Azure AD.

- **Permisos de** aplicación: compruebe si los permisos que definió en el ámbito son según los requisitos de la aplicación. Si es así, compruebe si se le concedió al usuario en el token de acceso.

- **Consentimiento del administrador**: si algún ámbito requiere consentimiento del administrador, compruebe si se concedió el consentimiento para el ámbito concreto al usuario.

Además, inspeccione el token de acceso que se envió a la aplicación de pestaña para comprobar si los valores siguientes son correctos:

- **Audiencia (aud):** compruebe si el identificador de la aplicación en el token es correcto tal y como se indica en Azure AD.
- **Identificador de inquilino (tid):** compruebe si el inquilino mencionado en el token es correcto.
- **Identidad de usuario (preferred_username):** compruebe si la identidad del usuario coincide con el nombre de usuario en la solicitud de token de acceso para el ámbito al que el usuario actual quiere acceder.
- **Ámbitos (scp):** compruebe si el ámbito para el que se solicita el token de acceso es correcto y como se define en Azure AD.
- **Versión 1.0 o 2.0 (ver) de Azure AD**: compruebe si la versión de Azure AD es correcta.

Puede usar [JWT](https://jwt.ms) para inspeccionar el token.

</details>
