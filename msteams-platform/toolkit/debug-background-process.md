---
title: Depurar procesos en segundo plano
author: zyxiaoyuer
description: Función de Visual Studio Code y el kit de herramientas de Teams durante la depuración local
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: d692f3f6869767e4b9948b36e521a56d799ebe4b
ms.sourcegitcommit: ff31cbe4840191f004d8fc61dd4fd93d35fcaecb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2022
ms.locfileid: "65938929"
---
# <a name="debug-background-processes"></a>Depurar procesos en segundo plano

El flujo de trabajo de depuración local implica los archivos `.vscode/launch.json` y `.vscode/tasks.json` para configurar el depurador en Visual Studio Code (VS Code). El VS Code iniciará los depuradores, y Microsoft Edge o Google Chrome iniciarán una nueva instancia del explorador, tal y como se indica a continuación:

1. El archivo `launch.json` configura el depurador en VS Code.

2. VS Code ejecuta el archivo **preLaunchTask** compuesto, **Comprobación previa a la depuración e Iniciar todo** en el archivo `.vscode/tasks.json`.

3. VS Code inicia los depuradores especificados en las configuraciones compuestas, como **Attach to Bot**, **Attach to Backend**, **Attach to Frontend** y **Launch Bot**

4. Microsoft Edge o Google Chrome inicia una nueva instancia del explorador y abre una página web para cargar el cliente de Teams.

## <a name="prerequisites"></a>Requisitos previos

Kit de herramientas de Teams comprueba los siguientes requisitos previos durante el proceso de depuración:

* Node.js, aplicable a los siguientes tipos de proyecto:

  |Tipo de proyecto|Versión LTS de Node.js|
  |----------|--------------------------------|
  |Tab | 14, 16 (recomendado) |
  |Pestaña SPFx | 12, 14 (recomendado)|
  |Bot |  14, 16 (recomendado)|
  |Extensión de mensajería | 14, 16 (recomendado) |

* La cuenta de Microsoft 365 con credenciales válidas, el kit de herramientas de Teams le pedirá que inicie sesión en la cuenta de Microsoft 365, si todavía no ha iniciado sesión.
* Habilite la carga o instalación de prueba de aplicaciones personalizadas para el espacio empresarial del desarrollador, si no es así, la depuración local finalizará.
* La versión binaria Ngrok 2.3 se aplica a la extensión de bot y mensajería. Si Ngrok no está instalado o la versión no coincide con el requisito, el kit de herramientas de Teams instalará el paquete Ngrok NPM `ngrok@4.2.2` en `~/.fx/bin/ngrok`. El paquete NPM de Ngrok en `/.fx/bin/ngrok/node modules/ngrok/bin` administra el binario Ngrok.
* Azure Functions Core Tools versión 3. Si Azure Functions Core Tools no está instalado o la versión no coincidiera con el requisito, el kit de herramientas de Teams instalará el paquete NPM de Azure Functions Core Tools, azure-functions-core-tools@3 para **Windows** y para **MacOs** en `~/.fx/bin/func`. El Azure Functions Core Tools paquete NPM en `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` administra Azure Functions Core Tools binario. Para Linux, finaliza la depuración local.
* SDK de .NET Core versión aplicable a Azure Functions. Si SDK de .NET Core no está instalado o la versión no coincide con el requisito, el kit de herramientas de Teams instalará SDK de .NET Core para Windows y MacOS en `~/.fx/bin/dotnet`. Para Linux, finaliza la depuración local.
* La versión binaria Ngrok 2.3 se aplica a la extensión de bot y mensajería. Si Ngrok no está instalado o la versión no coincide con el requisito, el kit de herramientas de Teams instalará el paquete Ngrok NPM `ngrok@4.2.2` en `~/.fx/bin/ngrok`. El paquete Ngrok NPM administra el binario Ngrok en `/.fx/bin/ngrok/node modules/ngrok/bin`.
* Azure Functions Core Tools versión 4, si Azure Functions Core Tools no está instalado o la versión no coincide con el requisito, el kit de herramientas de Teams instala el paquete NPM de Azure Functions Core Tools, azure-functions-core-tools@3 para **Windows** y para **macOs** en `~/.fx/bin/func`. El Azure Functions Core Tools paquete NPM en `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` administra Azure Functions Core Tools binario. Para Linux, finaliza la depuración local.
* SDK de .NET Core versión aplicable a Azure Functions, si SDK de .NET Core no está instalado o la versión no coincide con el requisito, el kit de herramientas de Teams instala SDK de .NET Core para Windows y MacOS en `~/.fx/bin/dotnet`. Para Linux, finaliza la depuración local.

  En la tabla siguiente se enumeran las versiones de .NET Core:

  | Plataforma  | Software|
  | --- | --- |
  |Windows, macOs (x64) y Linux | **3.1 (Recomendado)**, 5.0, 6-0 |
  |macOs (arm64) |6.0 |

* Certificado de desarrollo. Si el certificado de desarrollo para localhost no estuviera instalado para la pestaña en Windows o macOS, el kit de herramientas de Teams le pedirá que lo instale.
* Las extensiones de enlace de Azure Functions definidas en `api/extensions.csproj`. Si las extensiones de enlace de Azure Functions no están instaladas, el kit de herramientas de Teams instalará las extensiones de enlace de Azure Functions
* Paquetes NPM, que se aplican a aplicaciones de pestañas, aplicaciones de bot, aplicaciones de extensión de mensaje y Azure Functions. Si NPM no está instalado, el kit de herramientas de Teams instalará todos los paquetes NPM.
* Extensión de bot y mensaje. El kit de herramientas de Teams inicia Ngrok para crear un túnel HTTP para el bot y la extensión de mensaje
* Puertos disponibles. Si los puertos de pestaña, bot, extensión de mensaje y Azure Functions no están disponibles, la depuración local finaliza

  En la tabla siguiente se enumeran los puertos disponibles para los componentes:

  | Componente  | Puerto |
  | --- | --- |
  | Tab | 53000 |
  | Bot o extensión de mensaje | 3978 |
  | Inspector de nodo para bot o extensión de mensaje | 9239 |
  | Azure Functions | 7071 |
  | Inspector de nodo para Azure Functions | 9229 |

<!-- The following table lists the limitations if the required software is unavailable for debugging:

|Project type|Installation| Limitation|
|----------|--------------------------------|-----|
|Tab without Azure functions | Node.js LTS versions 10, 12, **14 (recommended)**, 16 | The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Tab with Azure functions | Node.js LTS versions 10, 12, **14 (recommended)** |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Bot | Node.js LTS versions 10, 12, **14 (recommended)**, 16|The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Message extension | Node.js LTS versions 10, 12, **14 (recommended)**, 16 |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Sign-in to Microsoft 365 account | Microsoft 365 credentials |Teams Toolkit prompts you to sign-in to Microsoft 365 account, if you haven't signed in. |
|Bot, message extension | Ngrok version 2.3| • If Ngrok isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Ngrok NPM package `ngrok@4.2.2` in `~/.fx/bin/ngrok`. </br> • The Ngrok binary is managed by Ngrok NPM package in `/.fx/bin/ngrok/node modules/ngrok/bin`.|
|Azure functions | Azure Functions Core Tools version 3| • If Azure Functions Core Tools isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Azure Functions Core Tools NPM package, azure-functions-core-tools@3 for **Windows** and for **macOs** in  `~/.fx/bin/func`. </br> • The Azure Functions Core Tools NPM package in `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` manages Azure Functions Core Tools binary. For Linux, the local debug terminates.|
|Azure functions |.NET Core SDK version|• If .NET Core SDK isn't installed or the version  doesn't match the requirement, the Toolkit installs .NET Core SDK for Windows and macOS in `~/.fx/bin/dotnet`.</br> • For Linux, the local debug terminates.|
|Azure functions | Azure functions binding extensions defined in `api/extensions.csproj`| If Azure functions binding extensions isn't installed, the Toolkit installs Azure functions binding extensions.|
|NPM packages| NPM packages for tab app, bot app, message extension app, and Azure functions|If NPM isn't installed, the Toolkit installs all NPM packages.|
|Bot and message extension | Ngrok |Toolkit starts Ngrok to create a HTTP tunnel for bot and message extension. |

> [!NOTE]
> If tab, bot, message extension, and Azure functions ports are unavailable, the local debug terminates.

Use the following .NET Core versions:

| Platform  | Software|
| --- | --- |
|Windows, macOs (x64), Linux | **3.1 (recommended)**, 5.0, 6.0 |
|macOs (arm64) |6.0 |

> [!NOTE]
> If the development certificate for localhost isn't installed for tab in Windows or MacOS, the Teams Toolkit prompts you to install it.</br> -->

Al seleccionar **Start Debugging (F5)**, el canal de salida del kit de herramientas de Teams muestra el progreso y el resultado después de comprobar los requisitos previos.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck.png" alt-text="Requisitos previos":::

## <a name="register-and-configure-teams-app"></a>Registrar y configurar la aplicación de Teams

En el proceso de configuración, el kit de herramientas de Teams prepara los siguientes registros y configuraciones para la aplicación de Teams:

1. [ Registra y configura Azure AD aplicación](#registers-and-configures-azure-ad-application): El kit de herramientas de Teams registra y configura la aplicación Azure AD.

1. [ Registra y configura el bot](#registers-and-configures-bot): El kit de herramientas de Teams registra y configura el bot para la aplicación de extensión de mensajes o las pestañas.

1. [ Registra y configura la aplicación teams](#registers-and-configures-teams-app): El kit de herramientas de Teams registra y configura la aplicación de Teams.

### <a name="registers-and-configures-azure-ad-application"></a>Registra y configura Azure AD aplicación

1. Registrar una aplicación de Azure AD

1. Crea un secreto de cliente.

1. Expone una API.

    a. Configura el URI de id. de aplicación. Para la pestaña, `api://localhost/{appId}`. Para el bot o extensión de mensajes,  `api://botid-{botid}`

    b. Agrega un ámbito denominado `access_as_user`. Lo habilita para **Admin y usuarios**.

4. Configura los permisos de API. Agrega Microsoft Graph permiso a **User.Read**.

    En la tabla siguiente se muestra la configuración de la autenticación como se indica a continuación:

      | Tipo de proyecto | URI de redirección para web | URI de redirección para una aplicación de página única |
      | --- | --- | --- |
      | Tab | `https://localhost:53000/auth-end.html` | `https://localhost:53000/auth-end.html?clientId={appId>}` |
      | Bot o extensión de mensaje | `https://ngrok.io/auth-end.html` | ND |

    En la tabla siguiente se enumeran las configuraciones de la aplicación cliente de Microsoft 365 con los identificadores de cliente:

      | Microsoft 365 aplicación cliente | Id. de cliente |
      | --- | --- |
      | Escritorio de Teams, móvil | 1fec8e78-bli4-4aaf-ab1b-5451cc387264 |
      | Web de Teams | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
      | Office.com | 4345a7b9-9a63-4910-a426-35363201d503 |
      | Office.com | 4765445b-32c6-49b0-83e6-1d93765276ca |
      | Escritorio de Office | 0ec893e0-5785-4de6-99da-4ed124e5296c |
      | Versión de escritorio de Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
      | Outlook Web Access | 00000002-0000-0ff1-ce00-0000000000000 |
      | Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

### <a name="registers-and-configures-bot"></a>Registra y configura el bot

Para la aplicación de pestaña o la aplicación de extensión de mensajes:

1. Registrar una aplicación de Azure AD

1. Crea un secreto de cliente para la aplicación Azure AD.

1. Registra un bot en [Microsoft Bot Framework](https://dev.botframework.com/) mediante la aplicación Azure AD.

1. Agrega el canal de Teams.

1. Configura el punto de conexión de mensajería como `https://{ngrokTunnelId}.ngrok.io/api/messages`.

### <a name="registers-and-configures-teams-app"></a>Registra y configura la aplicación teams

Registra una aplicación de Teams en [Developer](https://dev.teams.microsoft.com/home) mediante la plantilla de manifiesto en `templates/appPackage/manifest.template.json`.

Después de registrar y configurar la aplicación, se generan archivos de depuración locales.

## <a name="take-a-tour-of-your-app-source-code"></a>Realice un paseo por el código fuente de la aplicación

Puede ver las carpetas y los archivos del proyecto en el área **Explorer** de VS Code después de que el kit de herramientas de Teams registre y configure la aplicación. En la tabla siguiente se enumeran los archivos de depuración locales y los tipos de configuración:

| Nombre de la carpeta| Contenido| Tipo de configuración de depuración |
| --- | --- | --- |
|  `.fx/configs/config.local.json` | Archivo de configuración de depuración local | Los valores de cada configuración se generan y guardan durante la depuración local. |
|  `templates/appPackage/manifest.template.json` | Archivo de plantilla de manifiesto de aplicación de Teams para depuración local | Los marcadores de posición del archivo durante la depuración local. |
|  `tabs/.env.teams.local`  | Archivo de variables de entorno para la pestaña | Los valores de cada variable de entorno se generan y guardan durante la depuración local. |
|  `bot/.env.teamsfx.local` | Archivo de variables de entorno para el bot y la extensión de mensaje| Los valores de cada variable de entorno se generan y guardan durante la depuración local. |
| `api/.env.teamsfx.local`  | Archivo de variables de entorno para Azure Functions | Los valores de cada variable de entorno se generan y guardan durante la depuración local. |

## <a name="see-also"></a>Vea también

* [Debug de la aplicación teams con el kit de herramientas de Teams](debug-local.md)
* [usar el kit de herramientas de Teams para aprovisionar recursos en la nube](provision.md)
* [Implementar en la nube](deploy.md)
* [Vista previa y personalización del manifiesto de la aplicación de Teams](TeamsFx-preview-and-customize-app-manifest.md)
