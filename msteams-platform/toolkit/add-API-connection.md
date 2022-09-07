---
title: Integración de API de terceros existentes
author: MuyangAmigo
description: En este artículo, aprenderá cómo el kit de herramientas le ayuda a arrancar el acceso de ejemplo a las API existentes. Proporciona una lista de diferentes tipos de autenticación.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: 5933227f9ba4c8b684d624a8857304c044761578
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616812"
---
# <a name="integrate-existing-third-party-apis"></a>Integración de API de terceros existentes

Teams Toolkit le ayuda a acceder a las API existentes para compilar aplicaciones de Teams. Su organización o terceros desarrollan estas API. Cuando se usa Teams Toolkit para conectarse a una API existente, Teams Toolkit realiza la siguiente función:

* Genere código de ejemplo en `./bot` o `./api` carpeta.
* Agregue una referencia al `@microsoft/teamsfx` paquete a `package.json`.
* Agregue la configuración de la aplicación para la API en  `.env.teamsfx.local` que configure la depuración local.

## <a name="steps-to-connect-to-api"></a>Pasos para conectarse a la API

Puede agregar la conexión de API mediante Visual Studio Code y el comando de la CLI.

### <a name="add-api-connection-using-visual-studio-code"></a>Adición de conexión de API mediante Visual Studio Code

Los pasos siguientes le ayudan a agregar la conexión de API mediante Visual Studio Code:

1. Abrir Microsoft Visual Studio Code.
2. Seleccione :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="el icono de api"::: del kit de herramientas de Teams en la barra de herramientas de Visual Studio Code.
3. Seleccione **Agregar características** en **DESARROLLO**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="api add features":::

    * También puede abrir la paleta de comandos y escribir **Teams: Agregar recursos en la nube**.

4. En el elemento emergente, seleccione la **conexión de API** que desea agregar al proyecto de aplicación de Teams:

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="api select features":::

5. Seleccione **Aceptar**.

6. Escriba el punto de conexión para la API. Se agrega a la configuración de la aplicación local del proyecto y es la dirección URL base para las solicitudes de API.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="punto de conexión de api":::

     > [!NOTE]
     > Asegúrese de que el punto de conexión es una dirección URL http(s) válida.

7. Seleccione el componente que accede a la API.

8. Seleccione **Aceptar**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="api invoke":::

9. Escriba un alias para la API. El alias genera un nombre de configuración de aplicación para la API que se agrega a la configuración de la aplicación local del proyecto.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="alias de api":::

10. Seleccione la autenticación necesaria para la solicitud de API del **tipo de autenticación de API**. Genera el código de ejemplo adecuado y agrega la configuración de aplicación local correspondiente en función de la selección.

     :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/myAPI connection.png" alt-text="autenticación de api":::

     En función del tipo de autenticación seleccionado, se requieren los pasos siguientes para completar la configuración adicional.

# <a name="basic"></a>[Basic](#tab/basic)

* Escriba el nombre de usuario para la autenticación básica.

  Ahora se generó el código de ejemplo para llamar a la API en bot\myAPI.js.

# <a name="certification"></a>[Certificación](#tab/certification)

   Ahora se generó el código de ejemplo para llamar a la API en bot\myAPI.js.

# <a name="azure-active-directory"></a>[Azure Active Directory](#tab/AAD)

  Ahora se generó el código de ejemplo para llamar a la API en bot\myAPI.js.

# <a name="api-key"></a>[Clave de API](#tab/apikey)

* Seleccione la posición de clave de API necesaria en la solicitud.

* Escriba un nombre de clave de API.

  Ahora se generó el código de ejemplo para llamar a la API en bot\myAPI.js.

# <a name="custom-auth-implementation"></a>[Implementación de autenticación personalizada](#tab/CustomAuthImplementation)

  Ahora se generó el código de ejemplo para llamar a la API en bot\myAPI.js.

---

## <a name="add-api-connection-using-cli"></a>Adición de una conexión de API mediante la CLI

El comando base de esta característica es `teamsfx add api-connection [authentication type]`. En la tabla siguiente se proporciona una lista de los distintos tipos de autenticación y sus comandos de ejemplo correspondientes:

 > [!TIP]
 > Puede usar `teamsfx add api-connection [authentication type] -h` para obtener el documento de ayuda.

   |**Tipo de autenticación**|**Comando de ejemplo**|
   |-----------------------|------------------|
   |Básico|teamsfx add api-connection basic--endpoint <https://example.com> --component bot--alias example--user-name exampleuser--interactive false|
   |Clave de API|teamsfx add api-connection apikey--endpoint <https://example.com> --component bot--alias example--key-location header--key-name example-key-name--interactive false|
   |Azure AD|teamsfx add api-connection aad--endpoint <https://example.com> --component bot--alias example--app-type custom--tenant-id your_tenant_id--app-id your_app_id--interactive false|
   |Certificado|teamsfx add api-connection cert--endpoint <https://example.com> --component bot--alias example--interactive false|
   |Personalizado|teamsfx add api-connection custom--endpoint <https://example.com> --component bot--alias example--interactive false|

---

## <a name="directory-structure-updates-to-your-project"></a>Actualizaciones de la estructura de directorios en el proyecto

 El kit de herramientas de `bot` Teams modifica o `api` la carpeta en función de las selecciones:

1. Generar `{your_api_alias}.js/ts` archivo. El archivo inicializa un cliente de API para la API y exporta el cliente de API.

2. Agregue `@microsoft/teamsfx` el paquete a `package.json`. El paquete proporciona compatibilidad con los métodos de autenticación de API comunes.

3. Agregue variables de entorno a `.env.teamsfx.local`. Son las configuraciones del tipo de autenticación seleccionado. El código generado lee valores de las variables de entorno.

## <a name="advantages"></a>Ventajas

Teams Toolkit le ayuda a arrancar código de ejemplo para acceder a las API, si no tiene los SDK adecuados para el lenguaje para acceder a estas API.

## <a name="see-also"></a>Vea también

* [Publicar aplicaciones de Teams con el kit de herramientas de Teams](publish.md)
