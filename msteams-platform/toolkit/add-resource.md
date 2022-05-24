---
title: Agregar recursos a aplicaciones Teams
author: MuyangAmigo
description: Describe Agregar recursos del kit de herramientas de Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f3b96b60447596eae8c1cdf37f4b38f6653c444b
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656652"
---
# <a name="add-cloud-resources-to-teams-app"></a>Agregar recursos en la nube a la aplicación de Teams

TeamsFx ayuda a aprovisionar los recursos en la nube para el hospedaje de aplicaciones. Opcionalmente, puede agregar los recursos en la nube que se ajusten a sus necesidades de desarrollo.

## <a name="advantages"></a>Ventajas

En la lista siguiente se proporcionan ventajas para agregar más recursos en la nube en TeamsFx:

* Proporciona comodidad
* Genera automáticamente todos los archivos de configuración y se conecta a Teams aplicación mediante Teams Toolkit

## <a name="limitation"></a>Limitación

Si ha creado SPFx proyecto de pestaña basado en , no puede agregar recursos en la nube de Azure.

## <a name="add-cloud-resources"></a>Agregar recursos en la nube

**Puede agregar recursos en la nube mediante los métodos siguientes:**

* Para agregar recursos en la nube mediante Teams Toolkit en Visual Studio Code
* Para agregar recursos en la nube mediante la paleta de comandos

  > [!NOTE]
  > Debe aprovisionar para cada entorno, después de haber agregado correctamente el recurso en la aplicación de Teams.
  
* **Para agregar recursos en la nube mediante Teams Toolkit en Visual Studio Code:**

   1. Abra **Visual Studio Code**.
   1. Seleccione **Teams Toolkit** en el panel izquierdo.
   1. Seleccione **Agregar características** en **DESARROLLO**.

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/select-feature-updated.png" alt-text="agregar característica" border="true":::

* **Para agregar recursos en la nube mediante la paleta de comandos:**

   1. Abra **la paleta de comandos**.
   1. Escriba **Teams:Agregar características**.
   1. Presione **Entrar**.

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features.png" alt-text="Nube" border="true":::

   1. En el elemento emergente, seleccione los recursos en la nube que se van a agregar en el proyecto.

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/updated-final-cloud.png" alt-text="final" border="true":::

## <a name="add-cloud-resources-using-teamsfx-cli"></a>Adición de recursos en la nube mediante la CLI de TeamsFx

* Cambie el directorio de trabajo al **directorio del proyecto**.
* En la tabla siguiente se enumeran las funcionalidades y los comandos necesarios:

  |Recurso en la nube|Comando|
  |---------------|----------|
  | Proteger la función de Azure|`teamsfx add azure-function`|
  | Base de datos SQL Azure|`teamsfx add azure-sql`|
  | Administración de Azure API|`teamsfx add azure-apim`|
  | Azure Key Vault|`teamsfx add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Tipos de recursos en la nube

En los escenarios siguientes, TeamsFx se integra con los servicios de Azure:

- [Funciones de Azure](/azure/azure-functions/functions-overview): una solución sin servidor para satisfacer los requisitos a petición, como la creación de API web para el back-end de aplicaciones de Teams.
- [Base de datos de Azure SQL](/azure/azure-sql/database/sql-database-paas-overview): motor de la base de datos de la plataforma como servicio (PaaS) que sirve como almacén de datos de las aplicaciones Teams.
- [Azure API Management](deploy.md): se puede usar una puerta de enlace de API para administrar las API creadas para Teams aplicaciones y publicarlas para usarlas en otras aplicaciones, como Power Apps.
- [Azure Key Vault](/azure/key-vault/general/overview): proteja las claves criptográficas y otros secretos que usan los servicios y las aplicaciones en la nube.

## <a name="add-cloud-resources"></a>Agregar recursos en la nube

Los siguientes cambios aparecen después de agregar recursos en el proyecto:

- Nuevos parámetros agregados a azure.parameter. {env}.json para proporcionar la información necesaria para el aprovisionamiento.
- El nuevo contenido se incluye en la plantilla de ARM en `templates/azure`, excepto que los archivos están en `templates/azure/teamsfx` la carpeta para agregar los recursos de Azure.
- Los archivos de la carpeta `templates/azure/teamsfx` se vuelven a generar para asegurarse de que la configuración necesaria de TeamsFx está actualizada para los recursos de Azure agregados.
- `.fx/projectSettings.json` se actualiza para realizar un seguimiento de los recursos disponibles en el proyecto.

Después de agregar recursos en el proyecto, aparecen los siguientes cambios adicionales:

|Recursos|Cambios|Descripción|
|---------------|---------------|-----------------------------|
|Funciones de Azure|Se agrega un código de plantilla de las funciones de Azure a una subcarpeta con ruta de acceso `yourProjectFolder/api`</br></br>`launch.json` y `task.json` se actualizan en la carpeta `.visual studio code`.| Incluye una plantilla de desencadenador HTTP hello world en el proyecto.</br></br> Incluye los scripts necesarios para que Visual Studio Code se ejecute cuando quiera depurar la aplicación localmente.|
|Administración de Azure API|Un archivo de especificación de API abierto agregado a una subcarpeta con ruta de acceso `yourProjectFolder/openapi`.|Define la API después de la publicación, es el archivo de especificación de la API.|

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Crear una nueva aplicación de Teams](create-new-project.md)
* [Adición de funcionalidades a aplicaciones Teams](add-capability.md)
* [Implementar en la nube](deploy.md)