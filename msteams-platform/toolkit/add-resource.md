---
title: Agregar recursos a las aplicaciones Teams aplicaciones
author: MuyangAmigo
description: Describe Agregar recursos de Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# <a name="add-cloud-resources-to-your-teams-app"></a>Agregar recursos en la nube a la Teams aplicación

TeamsFx ayuda a aprovisionar recursos en la nube para el hospedaje de aplicaciones. También puede agregar recursos en la nube que se adapten a sus necesidades de desarrollo.

## <a name="prerequisite"></a>Requisito previo

[Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de tener Teams proyecto de aplicación en VS Code.

## <a name="add-cloud-resources-using-teams-toolkit"></a>Agregar recursos en la nube mediante Teams Toolkit

> [!IMPORTANT]
> Debe aprovisionar cada entorno después de agregar un recurso.

1. Abra **Visual Studio Code**.
1. Seleccione **Teams Toolkit** desde el panel izquierdo.
1. En el panel Teams Toolkit barra lateral, seleccione **Agregar recursos en la nube**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="Agregar recursos":::

   También puede abrir la paleta de comandos y escribir **Teams: Agregar recursos en la nube**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="agregar recursos en la nube":::

1. En la ventana emergente, selecciona los recursos en la nube que quieres agregar a tu proyecto Teams aplicación:

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="agregar":::

1. Seleccione **Aceptar**.

Los recursos seleccionados se agregan correctamente al proyecto.

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>Agregar recursos en la nube mediante la CLI de TeamsFx en la ventana de comandos

1. Cambie el directorio al **directorio del proyecto**.
1. Ejecute el siguiente comando para agregar diferentes recursos al proyecto:

|Recurso en la nube|Comando|
|---------------|----------|
| Función Azure|`teamsfx resource add azure-function --function-name your-func-name`|
| Base de datos SQL Azure|`teamsfx resource add --function-name your-func-name`|
| Administración de API de Azure|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Tipos de recursos en la nube

TeamsFx se integra con los servicios de Azure para los siguientes escenarios:

- [Funciones de Azure](/azure/azure-functions/functions-overview): una solución sin servidor para satisfacer los requisitos a petición, como la creación de API web para el back-end Teams aplicaciones.
- [Base SQL de datos de Azure](/azure/azure-sql/database/sql-database-paas-overview): un motor de base de datos de plataforma como servicio (PaaS) que sirve como almacén de datos Teams aplicaciones.
- [Administración de API de Azure](/azure/azure-sql/database/sql-database-paas-overview): una puerta de enlace de API que se puede usar para administrar las API creadas para Teams aplicaciones y publicarlas para que las consuman en otras aplicaciones, como power apps.
- [Azure Key Vault](/azure/key-vault/general/overview): proteger las claves criptográficas y otros secretos usados por servicios y aplicaciones en la nube.

## <a name="add-cloud-resources"></a>Agregar recursos en la nube

Después de agregar cualquier recurso, los cambios en el proyecto son los siguientes:

- Se pueden agregar nuevos parámetros a azure.parameter. {env}.json para proporcionar la información necesaria para la provisión.
- El nuevo contenido se anexa a ARM debajo `templates/azure` de la carpeta excepto los archivos de `templates/azure/teamsfx` la carpeta para crear los recursos de Azure agregados.
- Los archivos de la `templates/azure/teamsfx` carpeta se regeneran para garantizar que la configuración necesaria de TeamsFx está actualizada para los recursos de Azure agregados.
- `.fx/projectSettings.json` se actualiza para realizar un seguimiento de los recursos presentes en el proyecto.

Después de agregar resouces, los cambios adicionales en el proyecto son los siguientes:

|Recursos|Cambios|Descripción|
|---------------|---------------|-----------------------------|
|Funciones de Azure|Se agrega un código de plantilla de funciones de Azure a una subcarpeta con ruta de acceso `yourProjectFolder/api`</br></br>`launch.json` y `task.json` se actualiza en carpeta `.vscode` .| Incluye una plantilla de desencadenador http hello world en el proyecto.</br></br> Incluye scripts necesarios para Visual Studio Code ejecutar cuando desee depurar la aplicación localmente.|
|Administración de API de Azure|Un archivo de especificación de API abierto agregado a una subcarpeta con ruta de acceso `yourProjectFolder/openapi`|Define la API después de la publicación, es el archivo de especificación de la API .|

## <a name="limitation"></a>Limitación

No puede agregar recursos si ha creado un proyecto de pestaña SPFx base.

## <a name="see-also"></a>Vea también

[Aprovisionar recursos en la nube](provision.md)
