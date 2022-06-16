---
title: Interfaz de línea de comandos de TeamsFx
author: MuyangAmigo
description: Describe la interfaz de la línea de comandos de TeamsFx
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f26593c409f0b2f7d64093fa90e65afebd27c0ec
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123797"
---
# <a name="teamsfx-library"></a>Biblioteca de TeamsFx

Microsoft Teams Framework (TeamsFx) es una biblioteca que encapsula patrones comunes de integración y funcionalidad, como el acceso simplificado a Microsoft Identity. Puede crear aplicaciones para Microsoft Teams sin configuración.

Esta es una lista de las características principales de TeamsFx:

* **Colaboración de TeamsFx**: permite a los desarrolladores y propietarios del proyecto invitar a otros colaboradores al proyecto TeamsFx. Puede colaborar para depurar e implementar un proyecto de TeamsFx.

* **CLI de TeamsFx**: acelera el desarrollo de aplicaciones Teams. También habilita un escenario de CI/CD en el que puede integrar la CLI en scripts para la automatización.

* **SDK de TeamsFx**: proporciona acceso a la base de datos, como la biblioteca de código de TeamsFx principal que contiene autenticación simple para el código del cliente y del lado servidor adaptado para desarrolladores de Teams.

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
| `teamsfx add`| Agrega características a la aplicación de Teams.|
| `teamsfx account`| Administrar cuentas de servicio en la nube. Los servicios en la nube admitidos son "Azure" y "Microsoft 365". |
| `teamsfx env` | Administrar entornos. |
| `teamsfx provision` | Aprovisionar recursos en la nube en la aplicación actual.|
| `teamsfx deploy` | Implementar la aplicación actual.  |
| `teamsfx package` | Crear la aplicación de Teams en un paquete para su publicación.|
| `teamsfx validate` | Validar la aplicación actual.|
| `teamsfx publish` | Publicar la aplicación en Teams.|
| `teamsfx preview` | Obtener una vista previa de la aplicación actual. |
| `teamsfx config`  | Administrar los datos de configuración |
| `teamsfx permission`| Colaborar con otros desarrolladores en el mismo proyecto.|

## `teamsfx new`

De forma predeterminada, `teamsfx new` está en modo interactivo y guías para crear una nueva aplicación Teams. Puede trabajar en el modo no interactivo estableciendo la `--interactive` marca `false`en .

| Comando | Descripción |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Crear una aplicación a partir de una plantilla existente |
| `teamsfx new template list`     | Enumerar todas las plantillas disponibles |

### <a name="parameters-for-teamsfx-new"></a>Parámetros para `teamsfx new`

| Parámetro | Requisito | Descripción |
|:---------------- |:-------------|:-------------|
|`--app-name` | Sí| Nombre de la aplicación de Teams.|
|`--interactive`| No | Seleccionar las opciones de forma interactiva. Las opciones son `true` y `false` y el valor predeterminado es `true`.|
|`--capabilities`| No| Elija Teams funcionalidades de aplicación, las opciones son , , , , , , , , `sso-launch-page`, `search-app`. `command-bot``notification``message-extension``bot``tab-spfx``tab-non-sso``tab` El valor predeterminado es `tab`.|
|`--programming-language`| No| Lenguaje de programación para el proyecto. Las opciones son `javascript` o `typescript` y el valor predeterminado es `javascript`.|
|`--folder`| No | Directorio del proyecto. En este directorio se crea una subcarpeta con el nombre de la aplicación. El valor predeterminado es `./`.|
|`--spfx-framework-type`| No| Aplicable si la funcionalidad `SPFx tab` está seleccionada. Marco de front-end. Las opciones son `none`, `react` y `minimal`, y el valor predeterminado es `none`.|
|`--spfx-web part-name`| No | Aplicable si la funcionalidad `SPFx tab` está seleccionada. El valor predeterminado es "helloworld".|
|`--bot-host-type-trigger`| No | Aplicable si la funcionalidad `Notification bot` está seleccionada. Las opciones son `http-restify`, `http-functions`y `timer-functions`. El valor predeterminado es `http-restify`.|

### <a name="scenarios-for-teamsfx-new"></a>Escenarios para `teamsfx new`

Puede usar el modo interactivo para crear una aplicación Teams. En la lista siguiente se proporcionan escenarios para controlar todos los parámetros con `teamsfx new`:

* Bot de notificación desencadenada por Http con el servidor restify

  ```bash
  teamsfx new --interactive false --capabilities "notification" --bot-host-type-trigger "http-restify" --programming-language "typescript" --folder "./" --app-name       MyAppName
  ```

* Teams bot de comandos y respuesta

  ```bash
  teamsfx new --interactive false --capabilities "command-bot" --programming-language "typescript" --folder "./" --app-name myAppName
  ```

* Aplicación de pestañas hospedada en SPFx con React

  ```bash
  teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
  ```

## `teamsfx add`

En la tabla siguiente se enumeran las distintas características de la aplicación Teams junto con su descripción.

| Comando | Descripción |
|:----------------  |:-------------|
| `teamsfx add notification` | Envíe una notificación a Microsoft Teams a través de varios desencadenadores. |
| `teamsfx add command-and-response` | Responda a comandos simples en Microsoft Teams chat.|
| `teamsfx add sso-tab` | Teams páginas web compatibles con identidad incrustadas en Microsoft Teams.|
| `teamsfx add tab` | Páginas web de hola mundo incrustadas en Microsoft Teams.|
| `teamsfx add bot` | Hello world chatbot para ejecutar tareas simples y repetitivas por parte del usuario. |
| `teamsfx add message-extension` | Extensión hello world message que permite interacciones a través de botones y formularios. |
| `teamsfx add azure-function`| Una solución de proceso sin servidor y controlada por eventos que permite escribir menos código. |
| `teamsfx add azure-apim` | Una plataforma de administración híbrida y multinube para LAS API en todos los entornos.|
| `teamsfx add azure-sql` | Un servicio de base de datos relacional siempre actualizado creado para la nube. |
| `teamsfx add azure-keyvault` | Un servicio en la nube para almacenar y acceder a secretos de forma segura. |
| `teamsfx add sso` | Desarrolle una característica de Sign-On única para Teams las páginas de inicio y la funcionalidad bot. |
| `teamsfx add api-connection [auth-type]` | Conectar a una API con compatibilidad con la autenticación mediante el SDK de TeamsFx. |
| `teamsfx add cicd` | Agregue flujos de trabajo de CI/CD para GitHub, Azure DevOps o Jenkins.|

## `teamsfx account`

En la tabla siguiente se enumeran las cuentas de servicio en la nube, como Azure y Microsoft 365.

| Comando | Descripción |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Iniciar sesión en el servicio en la nube seleccionado. Las opciones de servicio son M365 o Azure. |
| `teamsfx account logout <service>`  | Cerrar sesión en el servicio en la nube seleccionado. Las opciones de servicio son M365 o Azure. |
| `teamsfx account set --subscription` | Actualizar la configuración de la cuenta para establecer un identificador de suscripción. |

## `teamsfx env`

En la tabla siguiente se enumeran los diferentes entornos.

|  Comando  | Descripción |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Agregar un nuevo entorno copiando desde el entorno especificado. |
| `teamsfx env list` | Enumerar todos los entornos. |

### <a name="scenarios-for-teamsfx-env"></a>Escenarios para `teamsfx env`

Cree un nuevo entorno copiando desde el entorno de desarrollo existente:

```bash
teamsfx env add staging --env dev
```

## `teamsfx provision`

Aprovisionare los recursos en la nube en la aplicación actual.

| Comando `teamsFx provision` | Descripción |
|:----------------  |:-------------|
| `teamsfx provision manifest` | Aprovisione una aplicación de Teams en Teams portal para desarrolladores con la información correspondiente especificada en el archivo de manifiesto especificado. |

### <a name="parameters-for-teamsfx-provision"></a>Parámetros para `teamsfx provision`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí| Seleccionar un entorno para el proyecto. |
|`--subscription`| No | Especificar un identificador de suscripción de Azure. |
|`--resource-group`| No | Establecer el nombre de un grupo de recursos existente. |
|`--sql-admin-name`| No | Aplicable cuando hay SQL recurso en el proyecto. Nombre de administrador de SQL.|
|`--sql-password`| No| Aplicable cuando hay SQL recurso en el proyecto. Contraseña de administrador de SQL.|

## `teamsfx deploy`

Este comando se usa para implementar la aplicación actual. De forma predeterminada, implementa todo el proyecto, pero también es posible implementarlo parcialmente. Las opciones son `frontend-hosting`, `function`, `apim`, `bot`, `spfx``aad-manifest` y `manifest`.

### <a name="parameters-for-teamsfx-deploy"></a>Parámetros para `teamsfx deploy`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí| Seleccionar un entorno existente para el proyecto. |
|`--open-api-document`| No | Aplicable cuando hay un recurso de APIM en el proyecto. Ruta de acceso del archivo de documento de la API abierta. |
|`--api-prefix`| No | Aplicable cuando hay un recurso de APIM en el proyecto. Prefijo de nombre de API. El nombre único predeterminado de la API es `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| No | Aplicable cuando hay un recurso de APIM en el proyecto. La versión de la API. |
|`--include-app-manifest`| No | Si se va a implementar el manifiesto de aplicación en Teams plataforma. Las opciones son `yes` y `not`. El valor predeterminado es `no`. |
|`--include-aad-manifest`| No | Si se va a implementar el manifiesto de aad. Las opciones son `yes` y `not`. El valor predeterminado es `no`. |

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
|`--m365-host`| Obtenga una vista previa de la aplicación en Teams, Outlook o Office. Las opciones son `teams`, `outlook` y `office`. El valor predeterminado es `teams`. |

### <a name="scenarios-for-teamsfx-preview"></a>Escenarios para `teamsfx preview`

En la lista siguiente se proporcionan los escenarios comunes para la versión preliminar de teamsfx:

* Vista previa local

  Dependencias:

  * Node.js
  * SDK de .NET
  * Azure Functions Core Tools

  ```bash
  teamsfx preview --local
  teamsfx preview --local --browser chrome
  ```

* Vista previa remota

  ```bash
  teamsfx preview --remote
  teamsfx preview --remote --browser edge
  ```

  > [!NOTE]
  > Los registros de los servicios en segundo plano, como React, se guardan en `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Los datos de configuración están en el ámbito del usuario o en el ámbito del proyecto.

|  Comando  | Descripción |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Ver el valor de configuración de la opción |
| `teamsfx config set <option> <value>` | Actualizar el valor de configuración de la opción |

### <a name="parameters-for-teamsfx-config"></a>Parámetros para `teamsfx config`

| Parámetro  | Requisito | Descripción |
|:----------------  |:-------------|:-------------|
|`--env`| Sí | Seleccionar un entorno existente para el proyecto. |
|`--folder`| No | Project directorio usado para obtener o establecer la configuración del proyecto. El valor predeterminado es `./`. |
|`--global`| No | Ámbito de la configuración. Si es true, el ámbito se limita al ámbito de usuario en lugar del ámbito del proyecto. El valor predeterminado es `false`. Ahora, las configuraciones globales admitidas incluyen `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools`, `validate-node`. |

### <a name="scenarios-for-teamsfx-config"></a>Escenarios para `teamsfx config`

Los secretos del `.userdata` archivo están cifrados `teamsfx config` y pueden ayudarle a ver o actualizar los valores necesarios.

* Dejar de enviar datos de telemetría

  ```bash
  teamsfx config set telemetry off
  ```

* Deshabilitar comprobador de entorno

  Hay tres configuraciones para activar o desactivar Node.js, el SDK de .NET y la validación de Azure Functions Core Tools, y todas ellas están habilitadas de forma predeterminada. Puede establecer la configuración en "off" si no necesita la validación de dependencias y quiere instalar las dependencias usted mismo. Consulte las siguientes guías:

  * [Guía de instalación de Node.js](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
  * [Guía de instalación del SDK de .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
  * [Azure Functions guía de instalación de Core Tools](<https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure>- functions-core-tools).

  Para deshabilitar la validación del SDK de .NET, puede usar el siguiente comando:

  ```bash
  teamsfx config set validate-dotnet-sdk off
  ```

  Para habilitar la validación del SDK de .NET, puede usar el siguiente comando:

  ```bash
  teamsfx config set validate-dotnet-sdk on
  ```

* Ver toda la configuración del ámbito de usuario

  ```bash
  teamsfx config get -g
  ```

* Ver toda la configuración en el proyecto

  El secreto se descifra automáticamente:

    ```bash
    teamsfx config get --env dev
    ```

* Actualizar la configuración del secreto en el proyecto

  ```bash
  teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
  ```

## `teamsfx permission`

La CLI de TeamsFx proporciona comandos `teamsFx permission` para escenarios de colaboración.

|  Comando | Descripción |
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

En la lista siguiente se proporcionan los permisos necesarios para los `TeamsFx` proyectos:

* Conceder permiso

  El creador del proyecto y los colaboradores pueden usar el comando `teamsfx permission grant` para agregar un nuevo colaborador al proyecto:

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  Después de recibir el permiso necesario, el creador del proyecto y los colaboradores pueden compartir el proyecto con el nuevo colaborador por GitHub y el nuevo colaborador puede tener todos los permisos para Microsoft 365 cuenta.

* Mostrar estado de permiso

  Project creador y colaboradores pueden usar `teamsfx permission status` el comando para ver Microsoft 365 permiso de cuenta para env específico:

  ```bash
  teamsfx permission status --env dev
  ```

* Enumerar todos los colaboradores

  El creador del proyecto y los colaboradores pueden usar el comando `teamsfx permission status` para ver todos los colaboradores de entornos específicos:

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

* Flujo de trabajo de colaboración E2E en la CLI

  * Como creador de proyectos:

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

  * Como colaborador de proyecto:

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
