---
title: Agregar recursos a las aplicaciones de Teams
author: MuyangAmigo
description: Describe Agregar recursos del kit de herramientas de Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 50cd3de693f70fd0c8414408bd6f4e6d3332d544
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2022
ms.locfileid: "65297208"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>Agregar recursos en la nube a la aplicación de Teams

TeamsFx ayuda a aprovisionar recursos en la nube para el hospedaje de aplicaciones. Opcionalmente, también puede agregar recursos en la nube que se ajusten a sus necesidades de desarrollo.

## <a name="prerequisite"></a>Requisito previo

[Instale el Kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión v3.0.0+.

> [!TIP]
> Asegúrese de que tiene el proyecto de aplicación de Teams en Visual Studio Code.

## <a name="add-cloud-resources-using-teams-toolkit"></a>Agregar de recursos en la nube mediante el kit de herramientas de Teams

> [!IMPORTANT]
> Debe aprovisionar cada entorno después de agregar un recurso.

1. Abrir **Microsoft Visual Studio Code**.
1. Seleccione **Kit de herramientas de Teams** en el panel izquierdo.
1. En el panel de la barra lateral del kit de herramientas de Teams, seleccione **Agregar recursos en la nube**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="Agregar recursos":::

   También puede abrir la paleta de comandos y escribir **Teams: Agregar recursos en la nube**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="agregar recursos en la nube":::

1. En el elemento emergente, seleccione los recursos en la nube que desea agregar al proyecto de aplicación de Teams:

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="agregar":::

1. Seleccione **Aceptar**.

Los recursos seleccionados se agregan correctamente al proyecto.

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>Agregar recursos en la nube mediante la CLI de TeamsFx en la ventana de comandos

1. Cambie el directorio de trabajo al **directorio del proyecto**.
1. Ejecute el siguiente comando para agregar diferentes recursos en el proyecto:

|Recurso en la nube|Comando|
|---------------|----------|
| Proteger la función de Azure|`teamsfx resource add azure-function --function-name your-func-name`|
| Base de datos SQL Azure|`teamsfx resource add --function-name your-func-name`|
| Administración de Azure API|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Tipos de recursos en la nube

TeamsFx se integra con los servicios de Azure para los siguientes escenarios:

- [Funciones de Azure](/azure/azure-functions/functions-overview): una solución sin servidor para satisfacer los requisitos a petición, como la creación de API web para el back-end de aplicaciones de Teams.
- [Base de datos de Azure SQL](/azure/azure-sql/database/sql-database-paas-overview): motor de la base de datos de la plataforma como servicio (PaaS) que sirve como almacén de datos de las aplicaciones Teams.
- [Administración de Azure API](deploy.md): una puerta de enlace de API que se puede usar para administrar las API creadas para las aplicaciones de Teams y publicarlas para usarlas en otras aplicaciones, como Power Apps.
- [Azure Key Vault](/azure/key-vault/general/overview): proteja las claves criptográficas y otros secretos que usan los servicios y las aplicaciones en la nube.

## <a name="add-cloud-resources"></a>Agregar recursos en la nube

Después de agregar cualquier recurso, los cambios en el proyecto son los siguientes:

- Se pueden agregar nuevos parámetros a azure.parameter.{env}.json para proporcionar la información necesaria para el aprovisionamiento.
- El nuevo contenido se anexa a la plantilla de ARM en `templates/azure` carpeta, excepto los archivos en `templates/azure/teamsfx` carpeta para crear los recursos de Azure agregados.
- Los archivos de la carpeta `templates/azure/teamsfx` se vuelven a generar para asegurarse de que la configuración necesaria de TeamsFx está actualizada para los recursos de Azure agregados.
- `.fx/projectSettings.json` se actualiza para realizar un seguimiento de los recursos presentes en el proyecto.

Después de agregar recursos, los cambios adicionales en el proyecto son los siguientes:

|Recursos|Cambios|Descripción|
|---------------|---------------|-----------------------------|
|Funciones de Azure|Se agrega un código de plantilla de las funciones de Azure a una subcarpeta con ruta de acceso `yourProjectFolder/api`</br></br>`launch.json` y `task.json` se actualizan en la carpeta `.visual studio code`.| Incluye una plantilla de desencadenador HTTP hello world en el proyecto.</br></br> Incluye los scripts necesarios para que Visual Studio Code se ejecute cuando quiera depurar la aplicación localmente.|
|Administración de Azure API|Un archivo de especificación de API abierto agregado a una subcarpeta con ruta de acceso `yourProjectFolder/openapi`.|Define la API después de la publicación, es el archivo de especificación de la API.|

## <a name="limitation"></a>Limitación

No puede agregar recursos si ha creado un proyecto de pestaña basado en SPFx.

## <a name="see-also"></a>Vea también

[Aprovisionar recursos en la nube](provision.md)
