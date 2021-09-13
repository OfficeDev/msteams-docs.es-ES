---
title: 'Introducción: requisitos previos'
author: adrianhall
description: Obtén información sobre cómo empezar con el Microsoft Teams de aplicaciones y configurar el entorno.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.localizationpriority: none
ms.openlocfilehash: de9b351761f45999ce8cb0438c5d83041727f7f5
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157298"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>Requisitos previos: Introducción al Microsoft Teams de aplicaciones

Antes de empezar a crear la primera aplicación Teams, debes instalar algunas herramientas y configurar el entorno de desarrollo.

## <a name="install-required-tools"></a>Instalar las herramientas necesarias

Algunas de las herramientas que necesitas dependen de cómo prefieras crear tu Teams aplicación:

- [Node.js](https://nodejs.org/en/download/) (use la versión más reciente de LTS de v14)
- Un explorador con herramientas para desarrolladores, como, [Microsoft Edge](https://www.microsoft.com/edge) (recomendado) o [Google Chrome](https://www.google.com/chrome/)
- Si está desarrollando con JavaScript, TypeScript o el SharePoint Framework (SPFx), instale [Visual Studio Code](https://code.visualstudio.com/download), versión 1.55 o posterior.  
- Si está desarrollando con .NET, instale [Visual Studio 2019](https://visualstudio.com/download). Asegúrese de instalar la carga ASP.NET **desarrollo web y web** o la carga de trabajo de desarrollo **multiplataforma de .NET Core.**

> [!WARNING]
> Existen problemas conocidos con `npm@7` , empaquetados con node v15 y versiones posteriores. Si tiene problemas para ejecutarse, asegúrese de que está `npm install` usando el nodo v14 (LTS)

## <a name="install-the-teams-toolkit"></a>Instale el Teams Toolkit

El Teams Toolkit ayuda a simplificar el proceso de desarrollo con herramientas para aprovisionar e implementar recursos en la nube para tu aplicación, publicar en la Teams y mucho más. Puede usar el kit de herramientas con Visual Studio Code, Visual Studio o como una CLI (denominada `teamsfx` ). Para obtener más información, [vea Teams Toolkit para Visual Studio Code](../toolkit/visual-studio-code-overview.md), Teams Toolkit para [Visual Studio](../toolkit/visual-studio-overview.md) y herramienta cli [de Teamsfx](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli).

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abrir Visual Studio Code.
1. Seleccione la **vista Extensiones** (**Ctrl+Mayús+X**  /  **,⇧-X** o **Ver > extensiones**).
1. En el cuadro de búsqueda, **escriba Teams Toolkit**.
1. Seleccione **Instalar** junto a la Teams Toolkit.

También puede encontrar el Teams Toolkit en el Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

La extensión de Visual Studio Code puede instalar las siguientes herramientas cuando sean necesarias. Si ya está instalada, la versión instalada se puede usar en su lugar. Si usa Linux incluido WSL, debe instalar estas herramientas antes de usar:

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools se usa para ejecutar los componentes back-end localmente durante una ejecución de depuración local, incluidas las aplicaciones auxiliares de autenticación necesarias para ejecutar los servicios en Azure. Se instala en el directorio del proyecto (mediante el npm `devDependencies` ).

- [SDK de .NET](/dotnet/core/install/)

    El SDK de .NET se usa para instalar enlaces personalizados para la depuración local y las implementaciones de aplicaciones de Azure Functions. Si no ha instalado el SDK de .NET 3.1 (o posterior) globalmente, se puede instalar la versión portátil.

- [ngrok](https://ngrok.com/download)

    Algunas Teams de la aplicación (bots de conversación, extensiones de mensajería y webhooks entrantes) requieren conexiones entrantes. Debe exponer el sistema de desarrollo para Teams a través de un túnel. No es necesario un túnel para las aplicaciones que solo incluyen pestañas. Este paquete se instala en el directorio del proyecto (mediante npm `devDependencies` ).

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Puedes usar Visual Studio 2019 para desarrollar aplicaciones Teams con Blazor Server en .NET. Si no tiene la intención de desarrollar aplicaciones Teams en .NET, instale la versión Visual Studio Code de Teams Toolkit.

Para instalar la Teams Toolkit extensión:

1. Abra Visual Studio 2019.
1. Seleccione **Extensiones Administrar**  >  **extensiones**.
1. En el cuadro de búsqueda, **escriba Teams Toolkit**.
1. Seleccione la Teams Toolkit y seleccione **Descargar**. Se descarga la extensión.
1. Cierre Visual Studio 2019 para instalar la extensión.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

Para instalar la CLI de TeamsFx, use el administrador `npm` de paquetes:

``` bash
npm install -g @microsoft/teamsfx-cli
```

Según la configuración, es posible que deba usar `sudo` para instalar la CLI:

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

Esto es más común en sistemas Linux y macOS.

Asegúrese de agregar la caché global de npm a la ruta de acceso. Normalmente, esto se realiza como parte del instalador Node.js instalación.  

Puede usar la CLI con el `teamsfx` comando. Compruebe que el comando funciona ejecutando `teamsfx -h` .

> [!CAUTION]
> Para poder ejecutar TeamsFx en terminales de PowerShell, debe habilitar la directiva de ejecución "firmada remotamente" para PowerShell. Para obtener más información, consulte la [documentación de PowerShell](/powershell/module/microsoft.powershell.core/about/about_signing).

---

## <a name="install-optional-tools"></a>Instalar herramientas opcionales

Instalar herramientas de explorador para el desarrollo de aplicaciones. Por ejemplo, si la aplicación está escrita con React, puedes usar React Developer Tools:

- [React Herramientas para desarrolladores para Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
- [React Herramientas para desarrolladores para Edge](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil)

Si desea obtener acceso a los datos almacenados en Azure o implementar un back-end basado en la nube para su aplicación Teams en Azure, instale estas herramientas:

- [Herramientas de Azure para Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Si trabaja con datos de microsoft Graph, debe obtener información y marcar el Explorador de Graph Microsoft. Esta herramienta basada en explorador te permite consultar Microsoft Graph fuera de una aplicación.

- [Explorador de Microsoft Graph](https://developer.microsoft.com/graph/graph-explorer)

Con el Portal de desarrolladores para Teams, puedes configurar, administrar y distribuir la aplicación Teams, incluida la organización o la Teams tienda.

- [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>Habilitar la instalación local

Durante el desarrollo, debes cargar la aplicación en Teams sin distribuirla. Esto se conoce como instalación local.

Si tienes una cuenta Teams, comprueba si puedes realizar la instalación local de aplicaciones en Teams:

1. En el Teams, seleccione **Aplicaciones**.
1. Selecciona **Upload una aplicación personalizada**.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde Teams puedes cargar una aplicación personalizada.":::

> [!NOTE]
> Si aún no puedes realizar la instalación local de aplicaciones, habla con el Teams usuario. Consulta [Habilitar aplicaciones Teams personalizadas y activar la](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) carga de aplicaciones personalizadas para obtener más información.

## <a name="get-a-free-teams-developer-tenant-optional"></a>Obtener un espacio empresarial Teams desarrollador (opcional)

Si no puede ver la opción de instalación local o no tiene una cuenta de Teams, puede obtener una cuenta de desarrollador Teams gratuita uniéndose al programa de desarrolladores M365.  El proceso de registro tarda aproximadamente dos minutos.

1. Vaya al programa [Microsoft 365 desarrollador](https://developer.microsoft.com/microsoft-365/dev-program).
1. Selecciona **Unirse ahora** y sigue las instrucciones en pantalla.
1. En la pantalla de bienvenida, seleccione **Configurar la suscripción de E5**.
1. Configurar la cuenta de administrador. Después de finalizar, debería ver una pantalla como esta.

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa Microsoft 365 desarrollador.":::

1. Inicie sesión en Teams la cuenta de administrador que acaba de configurar. Comprueba que tienes la Upload **una opción de aplicación** personalizada.

## <a name="get-a-free-azure-account"></a>Obtener una cuenta gratuita de Azure

Si quieres hospedar la aplicación o acceder a recursos dentro de Azure, debes tener una suscripción a Azure.  Puede crear [una cuenta gratuita antes](https://azure.microsoft.com/free/) de comenzar.

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>Iniciar sesión en las cuentas Microsoft 365 y Azure

Debe tener acceso a dos cuentas:

- Sus Microsoft 365 de cuenta. Esta es la cuenta que usa para iniciar sesión en Teams. Si usa un inquilino de un Microsoft 365 programa para desarrolladores, esta es la cuenta de administrador que estableció cuando se registró para el programa.
- Sus credenciales de Azure. Esta es la cuenta que usa para obtener acceso a Azure Portal y para aprovisionar nuevos recursos en la nube para admitir la aplicación.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abra Visual Studio Code
1. Selecciona el Teams en la barra lateral:

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Iniciar sesión en M365**.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Ubicación de la sección Cuentas usada para iniciar sesión.":::

    El proceso de inicio de sesión comienza a usar el explorador web normal. Complete el proceso de inicio de sesión de su cuenta M365. Cuando se le pida, puede cerrar el explorador y volver a Visual Studio Code.
1. Vuelva al Teams Toolkit dentro de Visual Studio Code.
1. Seleccione **Iniciar sesión en Azure**.

    > [!TIP]
    > Si tiene instalada la extensión cuenta de Azure y usa la misma cuenta, puede omitir este paso. Usa la misma cuenta que usas en otras extensiones.

1. El proceso de inicio de sesión comienza a usar el explorador web normal.  Complete el proceso de inicio de sesión de su cuenta de Azure. Cuando se le pida, puede cerrar el explorador y volver a Visual Studio Code.

    Cuando se completa, la **sección CUENTAS** de la barra lateral muestra las dos cuentas por separado, junto con el número de suscripciones de Azure utilizables disponibles. Asegúrese de que tiene al menos una suscripción de Azure utilizable disponible. Si no es así, cerrar sesión y usar una cuenta diferente.

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Visual Studio 2019 le pedirá que inicie sesión en cada servicio según sea necesario. No es necesario que inicie sesión en sus cuentas de M365 y Azure por adelantado.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

1. Inicie sesión en Microsoft 365 con la CLI de TeamsFx:

    ``` bash
    teamsfx account login m365
    ```

    El proceso de inicio de sesión comienza a usar el explorador web normal. Complete el proceso de inicio de sesión de su cuenta M365. Se le pedirá cuándo puede cerrar el explorador.

2. Inicie sesión en Azure con la CLI de TeamsFx:

    ``` bash
    teamsfx account login azure
    ```

    El proceso de inicio de sesión comienza a usar el explorador web normal. Complete el proceso de inicio de sesión de su cuenta de Azure. Se le pedirá cuándo puede cerrar el explorador.

    Los inicios de sesión de la cuenta se comparten Visual Studio Code la CLI de TeamsFx.



    Ahora que el entorno de desarrollo está configurado, puedes crear, crear e implementar la primera aplicación Teams desarrollo.

## <a name="see-also"></a>Consulte también

* [Introducción a tutoriales](code-samples.md) 
* [Crear una aplicación con React](first-app-react.md)
* [Crear una aplicación con Blazor](first-app-blazor.md)
* [Crear una aplicación con SPFx](first-app-spfx.md)
* [Crear una aplicación con C# o .NET](get-started-dotnet-app-studio.md)
* [Crear una aplicación con Node.js](get-started-nodejs-app-studio.md)
* [Crear una aplicación con el generador de Yeoman](get-started-yeoman.md)
* [Crear una aplicación de bots de conversación](first-app-bot.md)
* [Crear una extensión de mensajería](first-message-extension.md)
* [Muestras de código](https://github.com/OfficeDev/Microsoft-Teams-Samples)
