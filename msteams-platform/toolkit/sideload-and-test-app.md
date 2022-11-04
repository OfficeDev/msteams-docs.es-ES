---
title: Instalación local y prueba de la aplicación en el entorno de Teams
author: zyxiaoyuer
description: En este módulo, aprenderá a transferir localmente y probar la aplicación en un entorno diferente.
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 721b3a30bcc8c2fa49bb06491f4ab24bbeb844fd
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833005"
---
# <a name="sideload-and-test-app-in-teams-environment"></a>Instalación local y prueba de la aplicación en el entorno de Teams

Después de agregar la conexión de API, puede probar la conexión de API en el entorno local del Kit de herramientas de Teams e implementar la aplicación en la nube. En la canalización de CI/CD, después de la configuración con otra plataforma, debe crear una entidad de servicio de Azure para aprovisionar e implementar recursos.

En esta sección, aprenderá

* [Prueba de la conexión de API en el entorno local](#test-api-connection-in-local-environment)
* [Implementación de la aplicación en Azure](#deploy-your-application-to-azure)
* [Aprovisionamiento e implementación de recursos de CI/CD](#provision-and-deploy-cicd-resources)

## <a name="test-api-connection-in-local-environment"></a>Prueba de la conexión de API en el entorno local

Los pasos siguientes ayudan a probar la conexión de API en el entorno local del kit de herramientas de Teams:

 1. **Ejecución de la instalación de npm**

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

Para implementar la aplicación en Azure, debe agregar la autenticación a la configuración de la aplicación para el entorno adecuado. Por ejemplo, la API podría tener credenciales diferentes para `dev` y `prod`. En función de las necesidades del entorno, configure El kit de herramientas de Teams.

Teams Toolkit configura el entorno local. El código de ejemplo de arranque contiene comentarios que le indican qué configuración de aplicación debe configurar. Para obtener más información sobre la configuración de la aplicación, consulte [Agregar configuración de aplicación](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings).

## <a name="provision-and-deploy-cicd-resources"></a>Aprovisionamiento e implementación de recursos de CI/CD

Para aprovisionar e implementar recursos destinados a Azure dentro de CI/CD, debe crear una entidad de servicio de Azure para su uso.

Siga estos pasos para crear entidades de servicio de Azure:

1. Registre una aplicación de Microsoft Azure Active Directory (Azure AD) en un solo inquilino.
2. Assign a role to your Azure AD application to access your Azure subscription. The `Contributor` role is recommended.
3. Crear una nueva aplicación de Azure AD para el complemento

> [!TIP]
> Guarde el identificador de inquilino, el identificador de aplicación (AZURE_SERVICE_PRINCIPAL_NAME) y el secreto (AZURE_SERVICE_PRINCIPAL_PASSWORD) para su uso futuro.

Para obtener más información, consulte [Directrices de entidades de servicio de Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Estas son las tres maneras de crear entidades de servicio:

* [Portal de Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [CLI de Microsoft Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="see-also"></a>Vea también

[Publicar aplicaciones de Teams con el kit de herramientas de Teams](publish.md)
