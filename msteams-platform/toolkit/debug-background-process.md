---
title: Depurar procesos en segundo plano
author: surbhigupta
description: En este módulo, cómo funcionan el código de Visual Studio y el kit de herramientas de Teams durante el proceso de depuración local, también se explica cómo registrar y configurar la aplicación de Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 4d654d5da598b9bf2b9bacfc189c97df08f9a359
ms.sourcegitcommit: 707dad21dc3cf79ac831afe05096c0341bcf2fee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68653653"
---
# <a name="debug-background-process"></a>Depurar procesos en segundo plano

El proceso de depuración local implica los `.vscode/launch.json` archivos y `.vscode/tasks.json` para configurar el depurador en Microsoft Visual Studio Code. El Visual Studio Code inicia los depuradores y Microsoft Edge o Google Chrome inicia una nueva instancia del explorador.

El flujo de trabajo del proceso de depuración es el siguiente:

1. `launch.json`file configura el depurador en Visual Studio Code.

2. Visual Studio Code ejecuta el **elemento compuesto preLaunchTask**, **Iniciar la aplicación teams localmente** en el `.vscode/tasks.json` archivo.

3. Visual Studio Code inicia los depuradores especificados en las configuraciones compuestas, como **Attach to Bot**, **Attach to Backend**, **Attach to Frontend** y **Launch Bot**.

4. Microsoft Edge o Google Chrome inicia una nueva instancia del explorador y abre una página web para cargar el cliente de Teams.

## <a name="verification-of-prerequisites"></a>Comprobación de los requisitos previos

Kit de herramientas de Teams comprueba los siguientes requisitos previos durante el proceso de depuración:

* Node.js, aplicable a los siguientes tipos de proyecto:

  |Tipo de proyecto|Versión LTS de Node.js|
  |----------|--------------------------------|
  |Tab | 14, 16 (recomendado) |
  |Pestaña SPFx | 14, 16 (recomendado)|
  |Bot |  14, 16 (recomendado)|
  |Extensión de mensajería | 14, 16 (recomendado) |

* Teams Toolkit le pide que inicie sesión en la cuenta de Microsoft 365 si no ha iniciado sesión con sus credenciales válidas.
* La carga de aplicaciones personalizadas o la instalación local para el inquilino del desarrollador está activada, para evitar la terminación de depuración local.
* Teams Toolkit instala el paquete `ngrok@4.2.2` NPM de Ngrok en `~/.fx/bin/ngrok`, si Ngrok no está instalado o la versión no coincide con el requisito. La versión binaria 2.3 de Ngrok es aplicable para la extensión de bot y mensaje. El paquete Ngrok NPM administra el binario Ngrok en `/.fx/bin/ngrok/node modules/ngrok/bin`.
* Teams Toolkit instala el paquete NPM de Azure Functions Core Tools, azure-functions-core-tools@3 para **Windows** y **MacOs** en  `~/.fx/bin/func`, si azure Functions Core Tools versión 4 no está instalada o la versión no coincide con el requisito. El Azure Functions Core Tools paquete NPM en `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` administra Azure Functions Core Tools binario. Para Linux, finaliza la depuración local.
* Teams Toolkit instala el SDK de .NET Core para **Windows** y **MacOS** en `~/.fx/bin/dotnet`la versión del SDK de .NET Core aplicable a Azure Functions, si el SDK de .NET Core no está instalado o la versión no coincide con el requisito. Para Linux, finaliza la depuración local.

  En la tabla siguiente se enumeran las versiones de .NET Core:

  | Plataforma  | Software|
  | --- | --- |
  |Windows, macOS (x64) y Linux | **3.1 (Recomendado)**, 5.0, 6-0 |
  |macOS (arm64) |6.0 |

* Certificado de desarrollo, si el certificado de desarrollo para localhost no está instalado para la pestaña en **Windows** o **MacOS**, teams Toolkit le pide que lo instale.
* Las extensiones de enlace de Azure Functions definidas en `api/extensions.csproj`, si las extensiones de enlace de Azure Functions no están instaladas, teams Toolkit instala las extensiones de enlace de Azure Functions.
* Paquetes NPM, que se aplican a aplicaciones de pestañas, aplicaciones de bot, aplicaciones de extensión de mensaje y Azure Functions. Si los paquetes NPM no están instalados, Teams Toolkit instala todos los paquetes NPM.
* Bot y extensión de mensaje, Teams Toolkit inicia Ngrok para crear un túnel HTTP para bot y extensión de mensaje.
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

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck1.png" alt-text="Resumen de comprobación de requisitos previos" lightbox="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck1.png":::

## <a name="register-and-configure-teams-app"></a>Registrar y configurar la aplicación de Teams

En el proceso de configuración, el kit de herramientas de Teams prepara los siguientes registros y configuraciones para la aplicación de Teams:

1. [Registra y configura Microsoft Azure Active Directory aplicación (Azure AD)](#registers-and-configures-microsoft-azure-active-directoryazure-ad-app)

1. [Registra y configura el bot](#registers-and-configures-bot).

1. [Registra y configura la aplicación de Teams](#registers-and-configures-teams-app).

### <a name="registers-and-configures-microsoft-azure-active-directoryazure-ad-app"></a>Registra y configura Microsoft Azure Active Directory aplicación (Azure AD)

1. Registra una aplicación de Azure AD.

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

Registra una aplicación de Teams en el [Portal para desarrolladores](https://dev.teams.microsoft.com/home) mediante la plantilla de manifiesto en `templates/appPackage/manifest.template.json`.

Después de registrar y configurar la aplicación, se generan archivos de depuración locales.

## <a name="take-a-tour-of-your-app-source-code"></a>Realice un paseo por el código fuente de la aplicación

Puede ver las carpetas y los archivos del proyecto en **el Explorador** en Visual Studio Code después de que el Kit de herramientas de Teams registre y configure la aplicación. En la tabla siguiente se enumeran los archivos de depuración locales y los tipos de configuración:

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
