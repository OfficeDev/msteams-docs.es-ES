---
title: Conectar a las API existentes
author: MuyangAmigo
description: En este artículo, aprenderá cómo el kit de herramientas le ayuda a arrancar el acceso de ejemplo a las API existentes. Proporciona una lista de diferentes tipos de autenticación.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: dc987718233801a6855fd534d561fe2f3d964aa7
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143301"
---
# <a name="add-api-connection-to-teams-app"></a>Agregar conexión de API a la aplicación de Teams

Teams Toolkit le ayuda a acceder a las API existentes para compilar aplicaciones Teams. Su organización o terceros desarrollan estas API.

## <a name="advantage"></a>Ventaja

Teams Toolkit le ayuda a arrancar código de ejemplo para acceder a las API si no tiene los SDK adecuados para el lenguaje para acceder a estas API.

## <a name="connect-to-the-api"></a>Conectar a la API

Cuando se usa Teams Toolkit para conectarse a una API existente, Teams Toolkit realiza la siguiente función:

* Genere código de ejemplo en `./bot` o `./api` carpeta.
* Agregue una referencia al `@microsoft/teamsfx` paquete a `package.json`.
* Agregue la configuración de la aplicación para la API en  `.env.teamsfx.local` que configure la depuración local.

### <a name="connect-to-api-in-visual-studio-code"></a>Conectar a la API en Visual Studio Code

* Puede agregar una conexión de API mediante Teams Toolkit en Visual Studio Code:

    1. Abrir Microsoft Visual Studio Code.
    2. Seleccione Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="icono de api"::: en la barra de navegación izquierda.
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

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-auth.png" alt-text="autenticación de api":::

         > [!NOTE]
         > En función del tipo de autenticación seleccionado, se necesita una configuración adicional.

### <a name="api-connection-in-teamsfx-cli"></a>Conexión de API en la CLI de TeamsFx

El comando base de esta característica es `teamsfx add api-connection [authentication type]`. En la tabla siguiente se proporciona una lista de los distintos tipos de autenticación y sus comandos de ejemplo correspondientes:

 > [!Tip]
 > Puede usar `teamsfx add api-connection [authentication type] -h` para obtener el documento de ayuda.

   |**Tipo de autenticación**|**Comando de ejemplo**|
   |-----------------------|------------------|
   |Básico|teamsfx add api-connection basic --endpoint <https://example.com> --component bot --alias example--user-name exampleuser --interactive false|
   |Clave de API|teamsfx add api-connection apikey --endpoint <https://example.com> --component bot --alias example --key-location header --key-name example-key-name --interactive false|
   |Azure AD|teamsfx add api-connection aad --endpoint <https://example.com> --component bot --alias example --app-type custom --tenant-id your_tenant_id --app-id your_app_id --interactive false|
   |Certificado|teamsfx add api-connection cert --endpoint <https://example.com> --component bot --alias example --interactive false|
   |Personalizado|teamsfx add api-connection custom --endpoint <https://example.com> --component bot --alias example --interactive false|

## <a name="understand-toolkit-updates-to-your-project"></a>Descripción de Toolkit actualizaciones del proyecto

 Teams Toolkit modifica `bot` o `api` carpeta en función de las selecciones:

1. Generar `{your_api_alias}.js/ts` archivo. El archivo inicializa un cliente de API para la API y exporta el cliente de API.

2. Agregue `@microsoft/teamsfx` el paquete a `package.json`. El paquete proporciona compatibilidad con los métodos de autenticación de API comunes.

3. Agregue variables de entorno a `.env.teamsfx.local`. Son las configuraciones del tipo de autenticación seleccionado. El código generado lee valores de las variables de entorno.

## <a name="test-api-connection-in-local-environment"></a>Prueba de la conexión de API en el entorno local

Los pasos siguientes ayudan a probar la conexión de API en el entorno local de Teams Toolkit:

 1. **Ejecución npm instalación**

    Ejecute `npm install` en `bot` o `api` en la carpeta para instalar los paquetes agregados.

 2. **Adición de credenciales de API a la configuración de la aplicación local**

    Teams Toolkit no solicita credenciales, pero deja marcadores de posición en el archivo de configuración de la aplicación local. Reemplace los marcadores de posición por las credenciales adecuadas para acceder a la API. El archivo de configuración de la aplicación local es el `.env.teamsfx.local` archivo de la `bot` carpeta o `api` .

 3. **Uso del cliente de API para realizar solicitudes de API**

    Importe el cliente de API desde el código fuente que necesita acceso a la API:

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **Generación de solicitudes HTTP para la API de destino (con Axios)**

    El cliente de API generado es un cliente de API de Axios. Use el cliente de Axios para realizar solicitudes a la API.

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) es un popular paquete nodejs que le ayuda con las solicitudes HTTP. Para obtener más información sobre cómo realizar solicitudes HTTP, consulte la documentación de [ejemplo de Axios](https://axios-http.com/docs/example) para obtener información sobre cómo realizar http(s).

## <a name="deploy-your-application-to-azure"></a>Implementación de la aplicación en Azure

Para implementar la aplicación en Azure, debe agregar la autenticación a la configuración de la aplicación para el entorno adecuado. Por ejemplo, la API podría tener credenciales diferentes para `dev` y `prod`. En función de las necesidades del entorno, configure Teams Toolkit.

Teams Toolkit configura el entorno local. El código de ejemplo de arranque contiene comentarios que le indican qué configuración de aplicación debe configurar. Para obtener más información sobre la configuración de la aplicación, consulte [Agregar configuración de aplicación](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings).

## <a name="advanced-scenarios"></a>Escenarios avanzados

  En la sección siguiente se explican los escenarios avanzados:

<br>

<details>
<summary><b>Proveedor de autenticación personalizado</b></summary>

Además del proveedor de autenticación incluido en `@microsoft/teamsfx` el paquete, también puede implementar un proveedor de autenticación personalizado que implemente `AuthProvider` la interfaz y la use en `createApiClient(..)` función:

```Bash
import { AuthProvider } from '@microsoft/teamsfx'

class CustomAuthProvider implements AuthProvider {
    constructor() {
        // You can add necessary parameters for your customized logic in constructor
    }

    AddAuthenticationInfo: (config: AxiosRequestConfig) => Promise<AxiosRequestConfig> = async (
        config
    ) => {
        /*
        * The config parameter contains all the request information and can be updated to include extra authentication info.
        * Refer https://axios-http.com/docs/req_config for detailed document for the config object.
        * 
        * Add your customized logic that returns updated config
        */
    };
}
```

</details>
<details>
<summary><b>Conectar a las API para permisos de Azure AD</b></summary>
Azure AD autentica algunos servicios. La lista siguiente ayuda a acceder a estos servicios para configurar permisos de API.

* [Uso de listas de Access Control (ACL)](#access-control-lists-acls)
* [Uso de permisos de aplicación de Azure AD](#azure-ad-application-permissions)

La obtención de un token con los ámbitos de recursos adecuados para la API depende de la implementación de la API.

Puede seguir los pasos para acceder a estas API mientras usa:

#### <a name="access-control-lists-acls"></a>listas de Access Control (ACL)

   1. Inicie la depuración local en el entorno en la nube para el proyecto. Crea un registro de aplicación de Azure AD para la aplicación Teams.
  
   2. Abra `.fx/states/state.{env}.json`y anote el valor de `clientId` en `fx-resource-aad-app-for-teams` la propiedad .

   3. Proporcione el identificador de cliente al proveedor de API para configurar las ACL en el servicio de API.

#### <a name="azure-ad-application-permissions"></a>Permisos de aplicación de Azure AD

  1. Abra `templates/appPackage/aad.template.json` y agregue el siguiente contenido a la `requiredResourceAccess` propiedad :

```JSON
 {
     "resourceAppId": "The AAD App Id for the service providing the API you are connecting to",
     "resourceAccess": [
         {
             "id": "Target API's application permission Id",
             "type": "Role"
         }
     ]
 }
```

   2. Inicie la depuración local en el entorno en la nube para el proyecto. Crea un registro de aplicación de Azure AD para la aplicación Teams.

   3. Abra `.fx/states/state.{env}.json` y anote el valor de `clientId` en `fx-resource-aad-app-for-teams` la propiedad . Es el identificador de cliente de la aplicación.

   4. Conceda el consentimiento del administrador para el permiso de aplicación necesario. Para obtener más información, consulte [Concesión de consentimiento del administrador](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations).

        > [!NOTE]
        > Para el permiso de aplicación, use el identificador de cliente.
        >
</details>

## <a name="see-also"></a>Consulte también

* [Publicar aplicaciones de Teams con el kit de herramientas de Teams](publish.md)
