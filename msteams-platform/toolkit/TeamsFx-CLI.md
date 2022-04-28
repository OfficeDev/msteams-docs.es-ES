---
title: Interfaz de línea de comandos de TeamsFx
author: MuyangAmigo
description: Describe la interfaz de línea de comandos de TeamsFx
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 5fde7e94c198bfe76810a52ede78d0be7270ba0c
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104521"
---
# <a name="teamsfx-library"></a>Biblioteca TeamsFx

Microsoft Teams Framework (TeamsFx) es una biblioteca que encapsula patrones comunes de integración y funcionalidad (como el acceso simplificado a Microsoft Identity). Puede crear aplicaciones para Microsoft Teams sin configuración.

Esta es una lista de las principales características de TeamsFx:

* **Colaboración de TeamsFx**: permite a los desarrolladores y propietarios del proyecto invitar a otros colaboradores al proyecto TeamsFx. Puede colaborar para depurar e implementar un proyecto de TeamsFx.

* **CLI de TeamsFx**: acelera el desarrollo de aplicaciones Teams. También habilita el escenario de CI/CD, donde puede integrar la CLI en scripts para la automatización.

* **SDK de TeamsFx**: TeamsFx Software Development Kit (SDK) es la biblioteca de código de TeamsFx principal que encapsula la autenticación simple para el código cliente y del lado servidor adaptado para desarrolladores de Teams.

## <a name="teamsfx-command-line-interface"></a>Interfaz de línea de comandos de TeamsFx

La CLI de TeamsFx es una interfaz de línea de comandos basada en texto que acelera Teams desarrollo de aplicaciones. Su objetivo es proporcionar experiencia centrada en el teclado al crear aplicaciones Teams. También habilita el escenario de CI/CD, donde puede integrar la CLI en scripts para la automatización.

Para más información, consulte lo siguiente:

* [Código fuente](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [Paquete (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>Introducción

Instale `teamsfx-cli` desde `npm` y ejecute `teamsfx -h` para comprobar todos los comandos disponibles:

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>Comandos admitidos

| Comando | Descripción |
|----------------|-------------|
| `teamsfx new`| Cree una nueva aplicación de Teams.|
| `teamsfx account`| Administrar cuentas de servicio en la nube. Los servicios en la nube admitidos son "Azure" y "Microsoft 365". |
| `teamsfx env` | Administrar entornos. |
| `teamsfx capability`| Agregue nuevas funcionalidades a la aplicación actual.|
| `teamsfx resource`  | Administre los recursos de la aplicación actual.|
| `teamsfx provision` | Aprovisionamiento de recursos en la nube en la aplicación actual.|
| `teamsfx deploy` | Implemente la aplicación actual.  |
| `teamsfx package` | Compile la aplicación Teams en un paquete para su publicación.|
| `teamsfx validate` | Valide la aplicación actual.|
| `teamsfx publish` | Publique la aplicación en Teams.|
| `teamsfx preview` | Vista previa de la aplicación actual. |
| `teamsfx config`  | Administrar los datos de configuración. |
| `teamsfx permission`| Colabore con otros desarrolladores en el mismo proyecto.|

## `teamsfx new`

De forma predeterminada, `teamsfx new` entra en modo interactivo y le guía por el proceso de creación de una nueva aplicación Teams. También puede trabajar con el modo no interactivo estableciendo la `--interactive` marca en `false`.

| `teamsFx new` Comando | Descripción |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Creación de una aplicación a partir de una plantilla existente |
| `teamsfx new template list`     | Enumerar todas las plantillas disponibles |

### <a name="parameters-for-teamsfx-new"></a>Parámetros para `teamsfx new`

| Parámetro | Requisito | Descripción |
|:---------------- |:-------------|:-------------|
|`--app-name` | Sí| Nombre de la aplicación Teams.|
|`--interactive`| No | Seleccione las opciones de forma interactiva. Las opciones son `true` y y `false` el valor predeterminado es `true`.|
|`--capabilities`| No| Elija Teams funcionalidades de la aplicación, las varias opciones son `tab`, `bot``messaging-extension` y `tab-spfx`. El valor predeterminado es `tab`.|
|`--programming-language`| No| Lenguaje de programación para el proyecto. Las opciones son `javascript` o `typescript` y el valor predeterminado es `javascript`.|
|`--folder`| No | Project directorio. En este directorio se crea una subcarpeta con el nombre de la aplicación. El valor predeterminado es `./`.|
|`--spfx-framework-type`| No| Aplicable si `Tab(SPfx)` la funcionalidad está seleccionada. Front-end Framework. Las opciones son `none` y , `react`y el valor predeterminado es `none`.|
|`--spfx-web part-name`| No | Aplicable si `Tab(SPfx)` la funcionalidad está seleccionada. El valor predeterminado es "helloworld".|
|`--spfx-web part-desp`| No | Aplicable si `Tab(SPfx)` la funcionalidad está seleccionada. El valor predeterminado es "helloworld description". |
|`--azure-resources`| No| Aplicable si contiene `tab` funcionalidad. Agregue recursos de Azure al proyecto. Las opciones múltiples son `sql` (Azure SQL Database) y `function` (Azure Functions). |

### <a name="scenarios-for-teamsfx-new"></a>Escenarios para `teamsfx new`

Puede usar el modo interactivo para crear una aplicación Teams. Los escenarios para controlar todos los parámetros con `teamsfx new` son los siguientes:

#### <a name="tab-app-hosted-on-spfx-using-react"></a>Aplicación de tabulación hospedada en SPFx mediante React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>Teams aplicación en JavaScript con funciones de pestaña, bot y Azure Functions

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Teams aplicación de pestaña con Azure Functions y Azure SQL

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

Administrar cuentas de servicio en la nube. Los servicios en la nube admitidos son `Azure` y `Microsoft 365`.

| `teamsFx account` Comando | Descripción |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Inicie sesión en el servicio en la nube seleccionado. |
| `teamsfx account logout <service>`  | cierre la sesión del servicio en la nube seleccionado. |
| `teamsfx account set --subscription` | Actualice la configuración de la cuenta para establecer un identificador de suscripción. |

## `teamsfx env`

Administrar los entornos.

| `teamsfx env` Comando  | Descripción |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Agregue un nuevo entorno copiando desde el entorno especificado. |
| `teamsfx env list` | Enumere todos los entornos. |

### <a name="scenarios-for-teamsfx-env"></a>Escenarios para `teamsfx env`

Los escenarios para `teamsfx env` son los siguientes:

#### <a name="create-a-new-environment"></a>Creación de un nuevo entorno

Agregue un nuevo entorno copiando desde el entorno de desarrollo existente:

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Agregue nuevas funcionalidades a la aplicación actual.

| `teamsFx capability` Comando  | Descripción |
|:----------------  |:-------------|
| `teamsfx capability add tab` | Agregar pestaña |
| `teamsfx capability add bot` | Agregar bot |
| `teamsfx capability add messaging-extension`| Adición de la extensión messagE |

> [!NOTE]
> Si el proyecto incluye un bot, no se puede agregar la extensión de mensaje y se aplica viceversa. Puede incluir extensiones de bot y mensaje en el proyecto al crear un nuevo proyecto de aplicación Teams.

## `teamsfx resource`

Administre los recursos de la aplicación actual. Se admiten `<resource-type>` : `azure-sql`, `azure-function` y `azure-apim` .

| `teamsFx resource` Comando  | Descripción |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Agregue el recurso a la aplicación actual.|
| `teamsfx resource show <resource-type>`      | Mostrar los detalles de configuración del recurso. |
| `teamsfx resource list`      | Enumere todos los recursos de la aplicación actual. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Parámetros para `teamsfx resource add azure-function`

| Parámetro  | Requisito | Descripción |
|----------------  |-------------|-------------|
|`--function-name`| Sí | Proporcione un nombre de función. El valor predeterminado es `getuserprofile`. |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Parámetros para `teamsfx resource add azure-sql`

#### `--function-name`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--function-name`| Sí | Proporcione un nombre de función. El valor predeterminado es `getuserprofile`. |

> [!NOTE]
> El nombre de la función se comprueba como SQL y es necesario acceder a este desde la carga de trabajo del servidor. Si el proyecto no contiene `Azure Functions`, cree uno automáticamente.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Parámetros para `teamsfx resource add azure-apim`

> [!TIP]
> Las opciones surten efecto al intentar usar una instancia existente `APIM` . De forma predeterminada, no es necesario especificar ninguna opción y crea una nueva instancia durante el `teamsfx provision` paso.

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--subscription`| Sí | Selección de una suscripción de Azure|
|`--apim-resource-group`| Sí| Nombre del grupo de recursos. |
|`--apim-service-name`| Sí | Nombre de la instancia del servicio API Management. |
|`--function-name`| Sí | Proporcione un nombre de función. El valor predeterminado es `getuserprofile`. |

> [!NOTE]
> `Azure API Management` debe trabajar con `Azure Functions`. Si el proyecto no contiene `Azure Functions`, puede crear uno.

## `teamsfx provision`

Aprovisione los recursos en la nube en la aplicación actual.

### <a name="parameters-for-teamsfx-provision"></a>Parámetros para `teamsfx provision`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí| Seleccione un entorno para el proyecto. |
|`--subscription`| No | Especifique un identificador de suscripción de Azure. |
|`--resource-group`| No | Establezca el nombre de un grupo de recursos existente. |
|`--sql-admin-name`| No | Aplicable cuando hay SQL recurso en el proyecto. Nombre de administrador de SQL.|
|`--sql-password`| No| Aplicable cuando hay SQL recurso en el proyecto. Contraseña de administrador de SQL.|

## `teamsfx deploy`

Este comando se usa para implementar la aplicación actual. De forma predeterminada, implementa todo el proyecto, pero también es posible realizar la implementación parcial. Las varias opciones son `frontend-hosting`, `function`, `apim`, `teamsbot`y `spfx`.

### <a name="parameters-for-teamsfx-deploy"></a>Parámetros para `teamsfx deploy`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí| Seleccione un entorno existente para el proyecto. |
|`--open-api-document`| No | Aplicable cuando hay un recurso de APIM en el proyecto. Ruta de acceso del archivo de documento de API abierta. |
|`--api-prefix`| No | Aplicable cuando hay un recurso de APIM en el proyecto. Prefijo de nombre de API. El nombre único predeterminado de la API es `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| No | Aplicable cuando hay un recurso de APIM en el proyecto. Versión de la API. |

## `teamsfx validate`

Valide la aplicación actual. Este comando valida el archivo de manifiesto de la aplicación.

### <a name="parameters-for-teamsfx-validate"></a>Parámetros para `teamsfx validate`

`--env`: seleccione un entorno existente para el proyecto.

## `teamsfx publish`

Publique la aplicación en Teams.

### <a name="parameters-for-teamsfx-publish"></a>Parámetros para `teamsfx publish`

`--env`: seleccione un entorno existente para el proyecto.

## `teamsfx package`

Compile la aplicación Teams en un paquete para su publicación.

## `teamsfx preview`

Obtenga una vista previa de la aplicación actual desde local o remoto.

### <a name="parameters-for-teamsfx-preview"></a>Parámetros para `teamsfx preview`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--local`| No | Vista previa de la aplicación desde local. `--local` es exclusivo con `--remote`. |
|`--remote`| No | Obtenga una vista previa de la aplicación desde el control remoto. `--remote` es exclusivo con `--local`. |
|`--env`| No | Seleccione un entorno existente para el proyecto cuando se anexe el parámetro `--remote` . |
|`--folder`| No | Project directorio raíz. El valor predeterminado es `./`. |
|`--browser`| No | Explorador para abrir Teams cliente web. Las opciones son `chrome`, `edge` y `default` como el explorador predeterminado del sistema y el valor es `default`. |
|`--browser-arg`| No | El argumento para pasar al explorador, requiere --browser, se puede usar varias veces, por ejemplo, --browser-args="--guest" |
|`--sharepoint-site`| No | SharePoint dirección URL del sitio, como `{your-tenant-name}.sharepoint.com` para SPFx versión preliminar remota del proyecto. |

### <a name="scenarios-for-teamsfx-preview"></a>Escenarios para `teamsfx preview`

#### <a name="local-preview"></a>Versión preliminar local

Dependencias:

* Node.js
* SDK de .NET
* herramientas básicas de Azure Functions

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Versión preliminar remota

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> Los registros de los servicios en segundo plano, como React se guardan en `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Administre los datos de configuración en el ámbito de usuario o en el ámbito del proyecto.

| `teamsfx config` Comando  | Descripción |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Ver el valor de configuración de la opción |
| `teamsfx config set <option> <value>` | Actualizar el valor de configuración de la opción |

### <a name="parameters-for-teamsfx-config"></a>Parámetros para `teamsfx config`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Seleccione un entorno existente para el proyecto. |
|`--folder`| No | Project directorio. Esto se usa para obtener o establecer la configuración del proyecto. El valor predeterminado es `./`. |
|`--global`| No | Hacer frente a la configuración. Si esto es cierto, el ámbito se limita al ámbito de usuario en lugar del ámbito del proyecto. El valor predeterminado es `false`. En la actualidad, las configuraciones globales admitidas incluyen `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools`, `validate-node`. |

### <a name="scenerios-for-teamsfx-config"></a>Scenerios para `teamsfx config`

Los secretos del `.userdata` archivo se cifran `teamsfx config` y pueden ayudarle a ver o actualizar los valores.

#### <a name="stop-sending-telemetry-data"></a>Detener el envío de datos de telemetría

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Deshabilitación del comprobador de entorno

Hay tres configuraciones para activar o desactivar Node.js, el SDK de .NET y la validación de Azure Functions Core Tools, y todas están habilitadas de forma predeterminada. Puede establecer la configuración en "off" si no necesita la validación de dependencias y quiere instalar las dependencias por sí mismo. Consulte las siguientes guías:

* [ guía de instalación deNode.js](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [Guía de instalación del SDK de .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Azure Functions guía de instalación de Core Tools](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools).

Para deshabilitar la validación del SDK de .NET, puede usar el siguiente comando:

```bash
teamsfx config set validate-dotnet-sdk off
```

Para habilitar la validación del SDK de .NET, puede usar el siguiente comando:

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Visualización de toda la configuración del ámbito de usuario

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Visualización de toda la configuración en el proyecto

El secreto se descifra automáticamente:

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Actualización de la configuración del secreto en el proyecto

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

La CLI de TeamsFx proporciona comandos `teamsFx permission` para el escenario de colaboración.

| `teamsFx permission` Comando | Descripción |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Conceda permiso a la cuenta de Microsoft 365 del colaborador para el proyecto de un entorno especificado. |
| `teamsfx permission status` | Mostrar el estado del permiso para el proyecto |

### <a name="parameters-for-teamsfx-permission-grant"></a>Parámetros para `teamsfx permission grant`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Proporcione el nombre de env. |
|`--email`| Sí | Proporcione la dirección de correo electrónico Microsoft 365 del colaborador. Asegúrese de que la cuenta del colaborador está en el mismo inquilino con creator. |

### <a name="parameters-for-teamsfx-permission-status"></a>Parámetros para `teamsfx permission status`

| Parámetro | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Proporcione el nombre de env. |
|`--list-all-collaborators` | No | Con esta marca, Teams Toolkit CLI imprime todos los colaboradores de este proyecto. |

### <a name="scenarios-for-teamsfx-permission"></a>Escenarios para `teamsfx permission`

Los permisos para `TeamsFx` proyectos son los siguientes:

#### <a name="grant-permission"></a>Conceder permiso

Project creador y colaboradores pueden usar `teamsfx permission grant` el comando para agregar un nuevo colaborador al proyecto:

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

Después de recibir el permiso necesario, el creador del proyecto y los colaboradores pueden compartir el proyecto con el nuevo colaborador GitHub y el nuevo colaborador puede tener todos los permisos para Microsoft 365 cuenta.

#### <a name="show-permission-status"></a>Mostrar estado de permiso

Project creador y colaboradores pueden usar `teamsfx permission status` el comando para ver su permiso de cuenta de Microsoft 365 para determinados desarrolladores:

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Enumerar todos los colaboradores

Project creador y colaboradores pueden usar `teamsfx permission status` el comando para ver todos los colaboradores de una env específica:

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Flujo de trabajo de colaboración E2E en la CLI

Como creador del proyecto:

* Para crear una pestaña o un proyecto de bot de TeamsFx y seleccione Azure como tipo de host:

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

* Para iniciar sesión en Microsoft 365 cuenta y cuenta de Azure:

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

* Para aprovisionar el proyecto:

  ```bash
  teamsfx provision
  ```

* Para ver los colaboradores:

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

* Para agregar otra cuenta como colaborador. Asegúrese de que la cuenta agregada está en el mismo inquilino:

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

* Para insertar el proyecto en GitHub

Como colaborador Project:

* Clone el proyecto de GitHub.
* Inicie sesión en Microsoft 365 cuenta. Asegúrese de que se agrega la misma cuenta de Microsoft 365:

  ```bash
  teamsfx account login Microsoft 365
  ```

* Inicie sesión en la cuenta de Azure con el permiso de colaborador para todos los recursos de Azure.

  ```bash
  teamsfx account login azure
  ```

* Compruebe el estado del permiso. Debería tener el permiso de propietario del proyecto:

  ```bash
  teamsfx permission status --env dev
  ```

  ![estado del permiso](./images/permission-status.png)

* Actualice el código de la pestaña e implemente el proyecto en el remoto.
* Inicie el control remoto y el proyecto debería funcionar correctamente.

## <a name="see-also"></a>Vea también

* [SDK de TeamsFx para TypeScript o JavaScript](TeamsFx-SDK.md)
* [administrar varios entornos en el kit de herramientas de Teams](TeamsFx-multi-env.md)
* [Colaborar en Teams proyecto mediante Teams Toolkit](TeamsFx-collaboration.md)
* [Introducción al kit de herramientas de Teams](teams-toolkit-fundamentals.md)
