---
title: Solución de problemas de autenticación para pestañas con SSO en Teams
description: Solución de problemas de autenticación SSO en Teams y cómo usarla en pestañas
ms.topic: how-to
ms.localizationpriority: high
keywords: teams autenticación pestañas Microsoft Azure Active Directory (Azure AD) SSO errores preguntas
ms.openlocfilehash: fa17ffef08f85124a230f76419158f4216f55416
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2022
ms.locfileid: "66658948"
---
# <a name="troubleshoot-sso-authentication-in-teams"></a>Solución de problemas de autenticación SSO en Teams

Esta es una lista de problemas y preguntas sobre SSO y cómo puede corregirlos.
<br>

## <a name="support-for-microsoft-graph"></a>Compatibilidad con Microsoft Graph

<br>
<details>
<summary>1. ¿Funciona la API de Graph en Postman?</summary>
<br>
Puede usar la colección Microsoft Graph Postman con la API de Microsoft Graph.

Para más información, consulte [Usar Postman con la API de Microsoft Graph](/graph/use-postman).
</details>
<br>
<details>
<summary>2. ¿Funciona la API de Graph en el probador de Graph?</summary>
<br>
Sí, la API de Graph funciona en el probador de Graph.

Para más información, vea [Probador de Graph](https://developer.microsoft.com/graph/graph-explorer).

</details>
<br>

## <a name="error-messages-and-how-to-handle-them"></a>Mensajes de error y cómo abordarlos

<br>
<details>
<summary>1. Error: falta el consentimiento.</summary>
<br>
Cuando Azure AD recibe una solicitud de acceso a un recurso de Microsoft Graph, comprueba si el usuario (o el administrador de inquilinos) ha dado su consentimiento para este recurso. Si no hay ningún registro de consentimiento del usuario o administrador, Azure AD envía un mensaje de error al servicio web.

El código debe indicar al cliente (por ejemplo, en el cuerpo de una respuesta 403 Prohibido) cómo abordar el error:

- Si la aplicación de pestañas necesita ámbitos de Microsoft Graph para los que solo un administrador puede dar su consentimiento, el código debería generar un error.
- Si los únicos ámbitos necesarios pueden ser otorgados por el usuario, entonces el código debe recurrir a un sistema alternativo de autenticación de usuario.

</details>
<br>
<details>
<summary>2. Error: falta el ámbito (permiso).</summary>
<br>
Este error solo se ve durante el desarrollo.

Para controlar este error, el código del lado servidor debe enviar una respuesta 403 Prohibido al cliente. Debe registrar el error en la consola o en un registro.
</details>
<br>
<details>
<summary>3. Error: audiencia no válida en el token de acceso para Microsoft Graph.</summary>
<br>
El código del lado servidor debe enviar una respuesta 403 Prohibido al cliente para mostrar un mensaje al usuario. Se recomienda que también registre el error en la consola o en un registro.
</details>
<br>
<details>
<summary>4. Error: el nombre de host no debe basarse en un dominio ya en propiedad.</summary>
<br>
Puede obtener este error en uno de los dos escenarios:

1. El dominio personalizado no está agregado a Azure AD. Para agregar un dominio personalizado a Azure AD y registrarlo, siga el procedimiento [agregar un nombre de dominio personalizado a Azure AD](/azure/active-directory/fundamentals/add-custom-domain) y siga los pasos para [Configurar el ámbito del token de acceso](tab-sso-register-aad.md#configure-scope-for-access-token) de nuevo.
1. No ha iniciado sesión con credenciales de administrador en el inquilino de Microsoft 365. Inicie sesión en Microsoft 365 como administrador.

</details>
<br>
<details>
<summary>5. Error: no se recibió el nombre principal de usuario (UPN) en el token de acceso devuelto.</summary>
<br>
Puede agregar UPN como una notificación opcional en Azure AD.

Para más información, consulte [Proporcionar notificaciones opcionales a la aplicación](/azure/active-directory/develop/active-directory-optional-claims) y [tokens de acceso](/azure/active-directory/develop/access-tokens).
</details>
<br>
<details>
<summary>6. Error: error del SDK de Teams: resourceDisabled.</summary>
<br>
Para evitar este error, asegúrese de que el URI del identificador de aplicación esté configurado correctamente en el registro de aplicaciones de Azure AD y en el cliente de Teams.

Para más información sobre el URI del identificador de aplicación, consulte [Exponer una API](tab-sso-register-aad.md#to-expose-an-api).

</details>
<br>

<details>
<summary>7. Error: error genérico al ejecutar la aplicación de pestañas.</summary>
<br>
Un error genérico puede aparecer cuando una o varias configuraciones de aplicaciones realizadas en Azure AD son incorrectas. Para resolver este error, compruebe si los detalles de la aplicación configurados en el código y el manifiesto de Teams coinciden con los valores de Azure AD.

En la imagen siguiente se muestra un ejemplo de los detalles de la aplicación configurados en Azure AD.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-app-details.png" alt-text="Valores de configuración de aplicaciones en Azure AD":::

Compruebe que los siguientes valores coinciden entre Azure AD, el código del lado cliente y el manifiesto de aplicación de Teams:

- **Id. de aplicación**: el identificador de aplicación que generó en Azure AD debería ser el mismo en el código y en el archivo de manifiesto de Teams. Compruebe que el identificador de aplicación del manifiesto de Teams coincide con el **Id. de aplicación (cliente)** en Azure AD.

- **Secreto de aplicación**: el secreto de aplicación configurado en el back-end de la aplicación debe coincidir con las **credenciales de cliente** de Azure AD.
    También debe comprobar si el secreto de cliente ha expirado.

- **URI de id. de aplicación**: el URI de id. de aplicación en el código y en el archivo de manifiesto de aplicación de Teams debe coincidir con el **URI de id. de aplicación** en Azure AD.

- **Aplicación de permisos**: compruebe si los permisos definidos en el ámbito cumplen los requisitos de la aplicación. Si es así, compruebe si se concedieron al usuario en el token de acceso.

- **Consentimiento del administrador**: si algún ámbito requiere consentimiento del administrador, compruebe si el consentimiento se concedió para el ámbito concreto para el usuario.

Además, inspeccione el token de acceso que se envió a la aplicación de pestañas para comprobar si los valores siguientes son correctos:

- **Audiencia (aud):** compruebe si el identificador de aplicación en el token es correcto como se indica en Azure AD.
- **Id. de inquilino (tid)**: compruebe si el inquilino mencionado en el token es correcto.
- **Identidad de usuario (preferred_username):** compruebe si la identidad del usuario coincide con el nombre de usuario en la solicitud de token de acceso para el ámbito al que el usuario actual quiere acceder.
- **Ámbitos (scp):** compruebe si el ámbito para el que se solicita el token de acceso es correcto y como se define en Azure AD.
- **Azure AD versión 1.0 o 2.0 (ver)**: compruebe si la versión de Azure AD es correcta.

Puede usar [JWT](https://jwt.ms) para inspeccionar el token.

</details>
