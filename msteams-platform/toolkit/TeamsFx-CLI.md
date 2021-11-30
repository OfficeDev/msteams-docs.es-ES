---
title: Interfaz de línea de comandos de TeamsFx
author: MuyangAmigo
description: Describe la interfaz de línea de comandos de TeamsFx
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: b5ef65ec8d1377a99ddebe298e8f3ec4c4c8d3f0
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227804"
---
# <a name="teamsfx-command-line-interface"></a>Interfaz de línea de comandos de TeamsFx

La CLI de TeamsFx es una interfaz de línea de comandos basada en texto que acelera Teams desarrollo de aplicaciones. Su objetivo es proporcionar experiencia centrada en el teclado al crear Teams aplicaciones. También permite escenarios de CI/CD en los que la CLI se puede integrar fácilmente en scripts para la automatización.

* [Código fuente](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli) 
* [Paquete (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>Introducción

Empecemos instalando desde `teamsfx-cli` `npm` y ejecutando para comprobar todos los `teamsfx -h` comandos disponibles:

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>Comandos compatibles

| `teamsfx` Comandos  | Descripciones |
|:----------------  |:-------------|
| `teamsfx new`       | Cree una nueva Teams aplicación. |
| `teamsfx account`   | Administrar cuentas de servicio en la nube. Los servicios en la nube admitidos son "Azure" y "Microsoft 365".          |
| `teamsfx env`       | Administrar los entornos. |
| `teamsfx capability`| Agregue nuevas funcionalidades a la aplicación actual.         |
| `teamsfx resource`  | Administrar los recursos de la aplicación actual.         |
| `teamsfx provision` | Aprovisionar los recursos de nube en la aplicación actual.             |
| `teamsfx deploy`    | Implemente la aplicación actual.  |
| `teamsfx package`   | Crea tu Teams en un paquete para su publicación.         |
| `teamsfx validate`  | Validar la aplicación actual.             |
| `teamsfx publish`   | Publique la aplicación en Teams.             |
| `teamsfx preview`   | Obtener una vista previa de la aplicación actual. |
| `teamsfx config`    | Administrar los datos de configuración. |
| `teamsfx permission`| Colaborar con otros desarrolladores en el mismo proyecto.|

## `teamsfx new`

`teamsfx new`de forma predeterminada, pasará al modo interactivo y le guiará a través del proceso de creación de una nueva aplicación Teams haciendo algunas preguntas. También puede hacerlo en modo no interactivo estableciendo `--interactive` la marca en `false` .

| `teamsFx new` Comandos  | Descripciones |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Crear una aplicación a partir de una plantilla existente |
| `teamsfx new template list`     | Enumerar todas las plantillas disponibles |

### <a name="parameters-for-teamsfx-new"></a>Parámetros para `teamsfx new`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--app-name` | Sí| Nombre de la Teams aplicación.|
|`--interactive`| No | Seleccione las opciones de forma interactiva. Las opciones son `true` y `false` . El valor predeterminado es `true`.|
|`--capabilities`| No| Elija Teams de aplicación, varias opciones son: `tab` `bot` , y `messaging-extension` `tab-spfx` . El valor predeterminado es: `tab` .|
|`--programming-language`| No| Lenguaje de programación para el proyecto. Las opciones `javascrip` son o y el valor predeterminado `typescript` es: `javascript` .|
|`--folder`| No | Project directorio. Se creará una sub carpeta con el nombre de la aplicación en este directorio. El valor predeterminado es: `./` .|
|`--spfx-framework-type`| No| Aplicable si `Tab(SPfx)` la funcionalidad está seleccionada. Marco de front-end. Las opciones `none` son y , el valor predeterminado `react` es: `none` .|
|`--spfx-web part-name`| No | Aplicable si `Tab(SPfx)` la funcionalidad está seleccionada. Nombre del elemento web. El valor predeterminado es: "helloworld". |
|`--spfx-web part-desp`| No | Aplicable si `Tab(SPfx)` la funcionalidad está seleccionada. Descripción del elemento web. El valor predeterminado es: "helloworld description". |
|`--azure-resources`| No| Aplicable si contiene `tab` funcionalidad. Agregue recursos de Azure al proyecto. Options(Multiple) son `sql` (Azure SQL Database) y `function` (Funciones de Azure). |

### <a name="scenarios-for-teamsfx-new"></a>Escenarios para `teamsfx new`

Usar el modo interactivo para crear una aplicación Teams es muy intuitivo, pruébalo empezando por `teamsfx new` . Los siguientes son los pocos scenerios sobre el control de todos los parámetros:

#### <a name="a-tab-app-hosted-on-spfx-using-react"></a>Una aplicación de pestaña hospedada en SPFx mediante React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="a-teams-app-in-javascript-contains-tab-bot-capabilities-and-azure-functions"></a>Una Teams en JavaScript contiene pestaña, funcionalidades de bot y Funciones de Azure

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="a-teams-tab-app-with-azure-functions-and-azure-sql"></a>Una Teams pestaña con Azure Functions y Azure SQL

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

Administrar cuentas de servicio en la nube. Los servicios en la nube compatibles `Azure` son y `Microsoft 365` .

| `teamsFx account` Comandos  | Descripciones |
|:----------------  |:-------------|
| `teamsfx account login <service>`      | Inicie sesión en el servicio en la nube seleccionado. |
| `teamsfx account logout <service>`      | cierre sesión del servicio en la nube seleccionado. |
| `teamsfx account set --subscription`      | Actualice la configuración de la cuenta para establecer un identificador de suscripción. |

## `teamsfx env`

Administrar los entornos.

| `teamsfx env` Comandos  | Descripciones |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Agregue un nuevo entorno copiando desde el entorno especificado. |
| `teamsfx env list` | Enumerar todos los entornos. |

### <a name="scenarios-for-teamsfx-env"></a>Escenarios para `teamsfx env`

#### <a name="create-a-new-environment"></a>Crear un nuevo entorno

Agregue un nuevo entorno copiando desde el entorno de desarrollo existente:

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Agregue nuevas funcionalidades a la aplicación actual.

| `teamsFx capability` Comandos  | Descripciones |
|:----------------  |:-------------|
| `teamsfx capability add tab`      | Agregue una pestaña. |
| `teamsfx capability add bot`      | Agregar un bot. |
| `teamsfx capability add messaging-extension`      | Agregar una extensión de mensajería. |

> [!NOTE]
> Una vez que el proyecto incluye un bot, la extensión de mensajería no se puede agregar más y se aplica viceversa. Puede incluir extensiones de bot y mensajería en el proyecto al crear un nuevo proyecto Teams aplicación.

## `teamsfx resource`

Administrar los recursos de la aplicación actual. Los `<resource-type>` admitidos son: `azure-sql` y `azure-function` `azure-apim` .

| `teamsFx resource` Comandos  | Descripciones |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Agregue un recurso a la aplicación actual.|
| `teamsfx resource show <resource-type>`      | Mostrar los detalles de configuración del recurso. |
| `teamsfx resource list`      | Enumerar todos los recursos de la aplicación actual. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Parámetros para `teamsfx resource add azure-function`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--function-name`| Sí | Proporcione un nombre de función. El valor predeterminado es: `getuserprofile` . |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Parámetros para `teamsfx resource add azure-sql`

#### `--function-name`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--function-name`| Sí | Proporcione un nombre de función. El valor predeterminado es: `getuserprofile` . |

> [!NOTE]
> El nombre de la función se comprueba SQL debe tener acceso desde la carga de trabajo del servidor. Si el proyecto no contiene `Azure Functions` , se creará uno para usted.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Parámetros para `teamsfx resource add azure-apim`

> [!TIP]
> Las siguientes opciones tendrán efecto cuando intente usar una instancia `APIM` existente. De forma predeterminada, no tiene que especificar ninguna opción y creará una nueva instancia durante el `teamsfx provision` paso.

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--subscription`| Sí | Seleccionar una suscripción de Azure|
|`--apim-resource-group`| Sí| Nombre del grupo de recursos. |
|`--apim-service-name`| Sí | El nombre de la instancia de servicio de administración de API. |
|`--function-name`| Sí | Proporcione un nombre de función. El valor predeterminado es: `getuserprofile` . |

> [!NOTE]
> Pedimos el nombre de la función `Azure API Management` porque necesita trabajar con `Azure Functions` . Si el proyecto no `Azure Functions` contiene, crearemos uno para usted.

## `teamsfx provision`

Aprovisionar los recursos de nube en la aplicación actual.

### <a name="parameters-for-teamsfx-provision"></a>Parámetros para `teamsfx provision`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--env`| Sí| Seleccione un entorno para el proyecto. |
|`--subscription`| No | Especifique un identificador de suscripción de Azure. |
|`--resource-group`| No | Establezca el nombre de un grupo de recursos existente. |
|`--sql-admin-name`| No | Aplicable cuando hay SQL recurso en el proyecto. Nombre de administrador de SQL.|
|`--sql-password`| No| Aplicable cuando hay SQL recurso en el proyecto. Contraseña de administrador de SQL.|

## `teamsfx deploy`

Este comando se usa para implementar la aplicación actual. De forma predeterminada, implementará todo el proyecto, pero también es posible implementarlo parcialmente. Options(Multiple) son: `frontend-hosting` , , , , `function` `apim` `teamsbot` `spfx` .

### <a name="parameters-for-teamsfx-deploy"></a>Parámetros para `teamsfx deploy`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--env`| Sí| Seleccione un entorno existente para el proyecto. |
|`--open-api-document`| No | Aplicable cuando hay un recurso APIM en el proyecto. Ruta de acceso del archivo de documento de la API abierta. |
|`--api-prefix`| No | Aplicable cuando hay un recurso APIM en el proyecto. Prefijo de nombre de API. El nombre único predeterminado de la API será `{api-prefix}-{resource-suffix}-{api-version}` . |
|`--api-version`| No | Aplicable cuando hay un recurso APIM en el proyecto. Versión de la API. |

## `teamsfx validate`

Validar la aplicación actual. Este comando validará el archivo de manifiesto de la aplicación.

### <a name="parameters-for-teamsfx-validate"></a>Parámetros para `teamsfx validate`

`--env`: (Obligatorio) Seleccione un entorno existente para el proyecto.

## `teamsfx publish`

Publique la aplicación en Teams.

### <a name="parameters-for-teamsfx-publish"></a>Parámetros para `teamsfx publish`

`--env`: (Obligatorio) Seleccione un entorno existente para el proyecto.

## `teamsfx package`

Crea tu Teams en un paquete para su publicación.

## `teamsfx preview`

Obtenga una vista previa de la aplicación actual desde local o remoto.

### <a name="parameters-for-teamsfx-preview"></a>Parámetros para `teamsfx preview`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--local`| No | Vista previa de la aplicación desde local. `--local` es exclusivo con `--remote` . |
|`--remote`| No | Obtenga una vista previa de la aplicación desde el control remoto. `--remote` es exclusivo con `--local` . |
|`--env`| No | Seleccione un entorno existente para el proyecto cuando se `--remote` anexa el parámetro. |
|`--folder`| No | Project raíz. El valor predeterminado es `./`. |
|`--browser`| No | El explorador para abrir Teams cliente web. Las opciones `chrome` son y `edge` `default` (explorador predeterminado del sistema). El valor predeterminado es `default`. |
|`--browser-arg`| No | Argumento para pasar al explorador, requiere --browser, se puede usar varias veces (por ejemplo, --browser-args="--guest") |
|`--sharepoint-site`| No | SharePoint dirección URL del sitio, como `{your-tenant-name}.sharepoint.com` (solo para SPFx vista previa remota del proyecto). |

### <a name="scenarios-for-teamsfx-preview"></a>Escenarios para `teamsfx preview`

#### <a name="local-preview"></a>Vista previa local

Dependencias:

- Node.js
- SDK de .NET
- Azure Functions Core Tools

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Vista previa remota

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!Note]
> Los registros de los servicios en segundo React se guardarán en `~/.fx/cli-log/local-preview/` .

## `teamsfx config`

Administre los datos de configuración en el ámbito de usuario o en el ámbito del proyecto.

| `teamsfx config` Comandos  | Descripciones |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Ver el valor de configuración de option |
| `teamsfx config set <option> <value>` | Actualizar el valor de configuración de option |

### <a name="parameters-for-teamsfx-config"></a>Parámetros para `teamsfx config`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Seleccione un entorno existente para el proyecto. |
|`--folder`| No | Project directorio. Esto se usa cuando se obtiene o establece la configuración del proyecto. El valor predeterminado es: `./` . |
|`--global`| No | Cope de la configuración. Si esto es así, el ámbito se limita al ámbito de usuario en lugar del ámbito del proyecto. El valor predeterminado es: `false` . Las configuraciones globales admitidas actualmente incluyen: `telemetry` `validate-dotnet-sdk` , , , `validate-func-core-tools` `validate-node` . |

### <a name="scenerios-for-teamsfx-config"></a>Scenerios for `teamsfx config`

Los `.userdata` secretos del archivo están `teamsfx config` cifrados, lo que podría ayudarle a ver o actualizar estos valores.

#### <a name="stop-sending-telemetry-data"></a>Detener el envío de datos de telemetría

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Deshabilitar el control de entorno

Hay tres configuraciones para activar o desactivar la Node.js, la validación de .NET SDK y Azure Functions Core Tools, y todas están habilitadas de forma predeterminada. Puede establecer la configuración en "desactivado" si no necesita la validación de dependencias y desea instalar las dependencias usted mismo. Consulte la [ guíaNode.js instalación,](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)la guía de instalación del [SDK de .NET y](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk) la guía de instalación de Azure Functions Core [Tools](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools).

Por ejemplo, para deshabilitar la validación del SDK de .NET, puede usar el siguiente comando.

```bash
teamsfx config set validate-dotnet-sdk off
```

Para habilitar la validación del SDK de .NET, puede usar el siguiente comando.

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Ver toda la configuración de ámbito de usuario

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Ver toda la configuración del proyecto

El secreto se descifrará automáticamente:

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Actualizar la configuración secreta en el proyecto

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

La CLI de TeamsFx proporciona `teamsFx permission` comandos para el escenario de colaboración.

| `teamsFx permission` Comandos | Descripciones |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Conceda permiso para la cuenta Microsoft 365 colaborador para el proyecto de un entorno especificado. |
| `teamsfx permission status` | Mostrar el estado de permisos para el proyecto |

### <a name="parameters-for-teamsfx-permission-grant"></a>Parámetros para `teamsfx permission grant`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Proporcione el nombre de env. |
|`--email`| Sí | Proporcione la dirección de correo electrónico Microsoft 365 colaborador. Tenga en cuenta que la cuenta del colaborador debe estar en el mismo inquilino con creator. |

### <a name="parameters-for-teamsfx-permission-status"></a>Parámetros para `teamsfx permission status`

| Parámetros  | Necesario | Descripciones |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Proporcione el nombre de env. |
|`--list-all-collaborators` | No | Con esta marca, Teams Toolkit CLI imprimirá todos los colaboradores para este proyecto. |

### <a name="scenarios-for-teamsfx-permission"></a>Escenarios para `teamsfx permission`

Estos son algunos ejemplos para controlar mejor los permisos de `TeamsFx` los proyectos.

#### <a name="grant-permission"></a>Conceder permiso

Project creadores y colaboradores pueden usar `teamsfx permission grant` el comando para agregar un nuevo colaborador al proyecto:

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

Después de conceder el permiso correctamente, los creadores y colaboradores del proyecto pueden compartir el proyecto con el nuevo colaborador de Github y el nuevo colaborador tendrá todos los permisos para Microsoft 365 cuenta.

#### <a name="show-permission-status"></a>Mostrar estado de permisos

Project creador y colaboradores pueden usar el comando para ver su `teamsfx permission status` Microsoft 365 cuenta para env específico:

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Enumerar todos los colaboradores

Project creadores y colaboradores pueden usar el comando para ver todos los `teamsfx permission status` colaboradores de una env específica:

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Flujo de trabajo de colaboración E2E en CLI

Como creador de proyectos:

- Cree un nuevo proyecto de pestaña TeamsFx (también puede seleccionar bot) y el tipo de hospedaje seleccione Azure.

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

- Inicie Microsoft 365 cuenta y cuenta de Azure.

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

- Aprovisionar el proyecto.

  ```bash
  teamsfx provision
  ```

- Ver colaboradores. Deberías verte aquí.

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  ![list-all-collaborators](./images/permission-status-all.png)
- Agregue otra cuenta como colaborador. Tenga en cuenta que la cuenta agregada debe estar en el mismo inquilino:

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  ![add-new-collaborator](./images/permission-grant.png)
- Insertar el proyecto en GitHub

Como colaborador Project:

- Clone el proyecto desde GitHub.
- Inicie Microsoft 365 cuenta. Tenga en cuenta que Microsoft 365 cuenta debe ser la misma que se agregó anteriormente:

  ```bash
  teamsfx account login Microsoft 365
  ```

- Cuenta de Azure de inicio de sesión que tiene permiso de colaborador para todos los recursos de Azure.

  ```bash
  teamsfx account login azure
  ```

- Compruebe el estado del permiso. Debe encontrarse con el permiso de propietario del proyecto:

  ```bash
  teamsfx permission status --env dev
  ```

  ![estado del permiso](./images/permission-status.png)
- Actualice el código tab e implemente el proyecto en remoto.
- Inicie el control remoto y el proyecto debe funcionar bien.
