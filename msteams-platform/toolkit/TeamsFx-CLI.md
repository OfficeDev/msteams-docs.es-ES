---
title: Interfaz de línea de comandos de TeamsFx
author: MuyangAmigo
description: Describe la interfaz de la línea de comandos de TeamsFx
ms.author: zhany
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ab9bad973d337d783c1de70c2ad8575a67d6cb6e
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111440"
---
# <a name="teamsfx-library"></a>Biblioteca de TeamsFx

Microsoft Teams Framework (TeamsFx) es una biblioteca que encapsula patrones de integración y funcionalidad comunes (como el acceso simplificado a Microsoft Identity). Puede crear aplicaciones para Microsoft Teams sin configuración.

Esta es una lista de las características principales de TeamsFx:

* **Colaboración de TeamsFx**: permitir que los desarrolladores y el propietario del proyecto inviten a otros colaboradores al proyecto de TeamsFx. Puede colaborar para depurar e implementar un proyecto de TeamsFx.

* **CLI de TeamsFx**: acelera el desarrollo de aplicaciones de Teams. También habilita un escenario de CI/CD en el que puede integrar la CLI en scripts para la automatización.

* **SDK de TeamsFx**: el Kit de desarrollo de software (SDK) de TeamsFx es la biblioteca de código principal de TeamsFx que agrupa la autenticación simple para el código del lado cliente y servidor adaptado a los desarrolladores de Teams.

## <a name="teamsfx-command-line-interface"></a>Interfaz de línea de comandos de TeamsFx

La CLI de TeamsFx es una interfaz de línea de comandos basada en texto que acelera el desarrollo de aplicaciones de Teams. Su objetivo es proporcionar experiencia centrada en el teclado al crear aplicaciones de Teams. También habilita un escenario de CI/CD en el que puede integrar la CLI en scripts para la automatización.

Para obtener más información, vea:

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
| `teamsfx new`| Crear una nueva aplicación de Teams.|
| `teamsfx account`| Administrar cuentas de servicio en la nube. Los servicios en la nube admitidos son "Azure" y "Microsoft 365". |
| `teamsfx env` | Administrar entornos. |
| `teamsfx capability`| Agregar nuevas funcionalidades a la aplicación actual.|
| `teamsfx resource`  | Administrar los recursos de la aplicación actual.|
| `teamsfx provision` | Aprovisionar recursos en la nube en la aplicación actual.|
| `teamsfx deploy` | Implementar la aplicación actual.  |
| `teamsfx package` | Crear la aplicación de Teams en un paquete para su publicación.|
| `teamsfx validate` | Validar la aplicación actual.|
| `teamsfx publish` | Publicar la aplicación en Teams.|
| `teamsfx preview` | Obtener una vista previa de la aplicación actual. |
| `teamsfx config`  | Administrar los datos de configuración |
| `teamsfx permission`| Colaborar con otros desarrolladores en el mismo proyecto.|

## `teamsfx new`

De forma predeterminada, `teamsfx new` entra en modo interactivo y le guía a través del proceso de creación de una nueva aplicación de Teams. También puede trabajar con el modo no interactivo estableciendo la marca `--interactive` en `false`.

| Comando `teamsFx new` | Descripción |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Crear una aplicación a partir de una plantilla existente |
| `teamsfx new template list`     | Enumerar todas las plantillas disponibles |

### <a name="parameters-for-teamsfx-new"></a>Parámetros para `teamsfx new`

| Parámetro | Requisito | Descripción |
|:---------------- |:-------------|:-------------|
|`--app-name` | Sí| Nombre de la aplicación de Teams.|
|`--interactive`| No | Seleccionar las opciones de forma interactiva. Las opciones son `true` y `false` y el valor predeterminado es `true`.|
|`--capabilities`| No| Elegir las funcionalidades de la aplicación de Teams, las distintas opciones son `tab`, `bot`, `messaging-extension` y `tab-spfx`. El valor predeterminado es `tab`.|
|`--programming-language`| No| Lenguaje de programación para el proyecto. Las opciones son `javascript` o `typescript` y el valor predeterminado es `javascript`.|
|`--folder`| No | Directorio del proyecto. En este directorio se crea una subcarpeta con el nombre de la aplicación. El valor predeterminado es `./`.|
|`--spfx-framework-type`| No| Aplicable si la funcionalidad `Tab(SPfx)` está seleccionada. Marco de front-end. Las opciones son `none` y `react` y el valor predeterminado es `none`.|
|`--spfx-web part-name`| No | Aplicable si la funcionalidad `Tab(SPfx)` está seleccionada. El valor predeterminado es "helloworld".|
|`--spfx-web part-desp`| No | Aplicable si la funcionalidad `Tab(SPfx)` está seleccionada. El valor predeterminado es "helloworld description". |
|`--azure-resources`| No| Aplicable si contiene la funcionalidad `tab`. Agregar recursos de Azure al proyecto. Las opciones múltiples son `sql` (Azure SQL Database) y `function` (Azure Functions). |

### <a name="scenarios-for-teamsfx-new"></a>Escenarios para `teamsfx new`

Puede usar el modo interactivo para crear una aplicación de Teams. Los escenarios para controlar todos los parámetros con `teamsfx new` son los siguientes:

#### <a name="tab-app-hosted-on-spfx-using-react"></a>Aplicación de pestañas hospedada en SPFx con React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>Aplicación de Teams en JavaScript con pestaña, funcionalidades de bot y Azure Functions

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Aplicación de pestaña de Teams con Azure Functions y Azure SQL

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

Administrar cuentas de servicio en la nube. Los servicios en la nube admitidos son `Azure` y `Microsoft 365`.

| Comando `teamsFx account` | Descripción |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Iniciar sesión en el servicio en la nube seleccionado. |
| `teamsfx account logout <service>`  | Cerrar sesión en el servicio en la nube seleccionado. |
| `teamsfx account set --subscription` | Actualizar la configuración de la cuenta para establecer un identificador de suscripción. |

## `teamsfx env`

Administrar los entornos.

| Comando `teamsfx env`  | Descripción |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Agregar un nuevo entorno copiando desde el entorno especificado. |
| `teamsfx env list` | Enumerar todos los entornos. |

### <a name="scenarios-for-teamsfx-env"></a>Escenarios para `teamsfx env`

Los escenarios de `teamsfx env` son los siguientes:

#### <a name="create-a-new-environment"></a>Crear un nuevo entorno

Agregar un nuevo entorno copiando desde el entorno de desarrollo existente:

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Agregar nuevas funcionalidades a la aplicación actual.

| Comando `teamsFx capability`  | Descripción |
|:----------------  |:-------------|
| `teamsfx capability add tab` | Agregar pestaña |
| `teamsfx capability add bot` | Agregar bot |
| `teamsfx capability add messaging-extension`| Agregar extensión de mensajería |

> [!NOTE]
> Si el proyecto incluye un bot, no se puede agregar la extensión de mensajería y se aplica viceversa. Puede incluir extensiones de bot y de mensajería en el proyecto al crear un nuevo proyecto de aplicación de Teams.

## `teamsfx resource`

Administrar los recursos de la aplicación actual. Los `<resource-type>` admitidos son: `azure-sql`, `azure-function` y `azure-apim` .

| Comando `teamsFx resource`  | Descripción |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Agregar el recurso a la aplicación actual.|
| `teamsfx resource show <resource-type>`      | Mostrar los detalles de configuración del recurso. |
| `teamsfx resource list`      | Enumerar todos los recursos de la aplicación actual. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Parámetros para `teamsfx resource add azure-function`

| Parámetro  | Requisito | Descripción |
|----------------  |-------------|-------------|
|`--function-name`| Sí | Proporcionar un nombre de función. El valor predeterminado es `getuserprofile`. |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Parámetros para `teamsfx resource add azure-sql`

#### `--function-name`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--function-name`| Sí | Proporcionar un nombre de función. El valor predeterminado es `getuserprofile`. |

> [!NOTE]
> El nombre de la función se comprueba como SQL y es necesario tener acceso a él desde la carga de trabajo del servidor. Si el proyecto no contiene `Azure Functions`, cree uno.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Parámetros para `teamsfx resource add azure-apim`

> [!TIP]
> Las opciones surten efecto al intentar usar una instancia existente de `APIM`. De forma predeterminada, no es necesario especificar ninguna opción y se crea una nueva instancia durante el paso `teamsfx provision`.

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--subscription`| Sí | Seleccionar una suscripción de Azure|
|`--apim-resource-group`| Sí| Nombre del grupo de recursos. |
|`--apim-service-name`| Sí | Nombre de la instancia del servicio de API Management. |
|`--function-name`| Sí | Proporcionar un nombre de función. El valor predeterminado es `getuserprofile`. |

> [!NOTE]
> `Azure API Management` debe funcionar con `Azure Functions`. Si el proyecto no contiene `Azure Functions`, puede crear uno.

## `teamsfx provision`

Aprovisionare los recursos en la nube en la aplicación actual.

### <a name="parameters-for-teamsfx-provision"></a>Parámetros para `teamsfx provision`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí| Seleccionar un entorno para el proyecto. |
|`--subscription`| No | Especificar un identificador de suscripción de Azure. |
|`--resource-group`| No | Establecer el nombre de un grupo de recursos existente. |
|`--sql-admin-name`| No | Aplicable cuando hay un recurso SQL en el proyecto. Nombre de administrador de SQL.|
|`--sql-password`| No| Aplicable cuando hay un recurso SQL en el proyecto. Contraseña de administrador de SQL.|

## `teamsfx deploy`

Este comando se usa para implementar la aplicación actual. De forma predeterminada, implementa todo el proyecto, pero también es posible implementarlo parcialmente. Las distintas opciones son `frontend-hosting`, `function`, `apim`, `teamsbot` y `spfx`.

### <a name="parameters-for-teamsfx-deploy"></a>Parámetros para `teamsfx deploy`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí| Seleccionar un entorno existente para el proyecto. |
|`--open-api-document`| No | Aplicable cuando hay un recurso de APIM en el proyecto. Ruta de acceso del archivo de documento de la API abierta. |
|`--api-prefix`| No | Aplicable cuando hay un recurso de APIM en el proyecto. Prefijo de nombre de API. El nombre único predeterminado de la API es `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| No | Aplicable cuando hay un recurso de APIM en el proyecto. La versión de la API. |

## `teamsfx validate`

Validar la aplicación actual. Este comando valida el archivo de manifiesto de la aplicación.

### <a name="parameters-for-teamsfx-validate"></a>Parámetros para `teamsfx validate`

`--env`: seleccione un entorno existente para el proyecto.

## `teamsfx publish`

Publicar la aplicación en Teams.

### <a name="parameters-for-teamsfx-publish"></a>Parámetros para `teamsfx publish`

`--env`: seleccione un entorno existente para el proyecto.

## `teamsfx package`

Crear la aplicación de Teams en un paquete para su publicación.

## `teamsfx preview`

Obtener una vista previa de la aplicación actual desde el entorno local o remoto.

### <a name="parameters-for-teamsfx-preview"></a>Parámetros para `teamsfx preview`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--local`| No | Obtener una vista previa de la aplicación desde el ámbito local. `--local` es exclusivo con `--remote`. |
|`--remote`| No | Obtener una vista previa de la aplicación desde el modo remoto. `--remote` es exclusivo con `--local`. |
|`--env`| No | Seleccionar un entorno existente para el proyecto cuando se anexe el parámetro `--remote`. |
|`--folder`| No | Directorio raíz del proyecto. El valor predeterminado es `./`. |
|`--browser`| No | Explorador para abrir el cliente web de Teams. Las opciones son `chrome`, `edge` y `default` como el explorador predeterminado del sistema y el valor es `default`. |
|`--browser-arg`| No | El argumento para pasar al explorador, requiere --browser, se puede usar varias veces, por ejemplo, --browser-args="--guest". |
|`--sharepoint-site`| No | Dirección URL del sitio de SharePoint, como `{your-tenant-name}.sharepoint.com` para la versión preliminar remota del proyecto de SPFx. |

### <a name="scenarios-for-teamsfx-preview"></a>Escenarios para `teamsfx preview`

#### <a name="local-preview"></a>Vista previa local

Dependencias:

* Node.js
* SDK de .NET
* Azure Functions Core Tools

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Vista previa remota

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> Los registros de los servicios en segundo plano, como React, se guardan en `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Administrar los datos de configuración en el ámbito de usuario o en el ámbito del proyecto.

| Comando `teamsfx config`  | Descripción |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Ver el valor de configuración de la opción |
| `teamsfx config set <option> <value>` | Actualizar el valor de configuración de la opción |

### <a name="parameters-for-teamsfx-config"></a>Parámetros para `teamsfx config`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Seleccionar un entorno existente para el proyecto. |
|`--folder`| No | Directorio del proyecto. Se usa para obtener o establecer la configuración del proyecto. El valor predeterminado es `./`. |
|`--global`| No | Ámbito de la configuración. Si es true, el ámbito se limita al ámbito de usuario en lugar del ámbito del proyecto. El valor predeterminado es `false`. Actualmente, las configuraciones globales admitidas incluyen `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools`, `validate-node`. |

### <a name="scenerios-for-teamsfx-config"></a>Escenarios para `teamsfx config`

Los secretos del archivo `.userdata` se cifran, `teamsfx config` puede ayudarle a ver o actualizar los valores.

#### <a name="stop-sending-telemetry-data"></a>Dejar de enviar datos de telemetría

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Deshabilitar comprobador de entorno

Hay tres configuraciones para activar o desactivar Node.js, el SDK de .NET y la validación de Azure Functions Core Tools, y todas ellas están habilitadas de forma predeterminada. Puede establecer la configuración en "off" si no necesita la validación de dependencias y quiere instalar las dependencias usted mismo. Consulte las siguientes guías:

* [Guía de instalación de Node.js](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [Guía de instalación del SDK de .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Guía de instalación de Azure Functions Core Tools](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools).

Para deshabilitar la validación del SDK de .NET, puede usar el siguiente comando:

```bash
teamsfx config set validate-dotnet-sdk off
```

Para habilitar la validación del SDK de .NET, puede usar el siguiente comando:

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Ver toda la configuración del ámbito de usuario

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Ver toda la configuración en el proyecto

El secreto se descifra automáticamente:

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Actualizar la configuración del secreto en el proyecto

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

La CLI de TeamsFx proporciona comandos `teamsFx permission` para el escenario de colaboración.

| Comando `teamsFx permission` | Descripción |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Conceder permiso para la cuenta de Microsoft 365 del colaborador para el proyecto de un entorno especificado. |
| `teamsfx permission status` | Mostrar el estado del permiso para el proyecto |

### <a name="parameters-for-teamsfx-permission-grant"></a>Parámetros para `teamsfx permission grant`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Proporcionar el nombre del entorno. |
|`--email`| Sí | Proporcionar la dirección de correo electrónico de Microsoft 365 del colaborador. Asegúrese de que la cuenta del colaborador está en el mismo inquilino con el creador. |

### <a name="parameters-for-teamsfx-permission-status"></a>Parámetros para `teamsfx permission status`

| Parámetro | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Proporcionar el nombre del entorno. |
|`--list-all-collaborators` | No | Con esta marca, la CLI del kit de herramientas de Teams imprime todos los colaboradores de este proyecto. |

### <a name="scenarios-for-teamsfx-permission"></a>Escenarios para `teamsfx permission`

Los permisos para los proyectos de `TeamsFx` son los siguientes:

#### <a name="grant-permission"></a>Conceder permiso

El creador del proyecto y los colaboradores pueden usar el comando `teamsfx permission grant` para agregar un nuevo colaborador al proyecto:

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

Después de recibir el permiso necesario, el creador del proyecto y los colaboradores pueden compartir el proyecto con el nuevo colaborador mediante GitHub, y el nuevo colaborador puede tener todos los permisos para la cuenta de Microsoft 365.

#### <a name="show-permission-status"></a>Mostrar estado de permiso

El creador del proyecto y los colaboradores pueden usar el comando `teamsfx permission status` para ver su permiso de cuenta de Microsoft 365 para entornos específicos:

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Enumerar todos los colaboradores

El creador del proyecto y los colaboradores pueden usar el comando `teamsfx permission status` para ver todos los colaboradores de entornos específicos:

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Flujo de trabajo de colaboración E2E en la CLI

Como creador de proyectos:

* Para crear una nueva pestaña de TeamsFx o un proyecto de bot y seleccionar Azure como tipo de host:

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

* Para iniciar sesión en la cuenta de Microsoft 365 y de Azure:

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

* Para aprovisionar el proyecto:

  ```bash
  teamsfx provision
  ```

* Para ver colaboradores:

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

Como colaborador de proyecto:

* Clone el proyecto desde GitHub.
* Inicie sesión en la cuenta de Microsoft 365. Asegúrese de que se agrega la misma cuenta de Microsoft 365:

  ```bash
  teamsfx account login Microsoft 365
  ```

* Inicie sesión en la cuenta de Azure con permiso de colaborador para todos los recursos de Azure.

  ```bash
  teamsfx account login azure
  ```

* Compruebe el estado del permiso. Debería encontrarse con el permiso de propietario del proyecto:

  ```bash
  teamsfx permission status --env dev
  ```

  ![estado de permiso](./images/permission-status.png)

* Actualice el código de la pestaña e implemente el proyecto en remoto.
* Inicie de forma remota y el proyecto debería funcionar bien.

## <a name="see-also"></a>Vea también

* [SDK de TeamsFx para TypeScript o JavaScript](TeamsFx-SDK.md)
* [administrar varios entornos en el kit de herramientas de Teams](TeamsFx-multi-env.md)
* [Colaborar en un proyecto de Teams con el kit de herramientas de Teams](TeamsFx-collaboration.md)
* [Introducción al kit de herramientas de Teams](teams-toolkit-fundamentals.md)
