---
title: 'Introducción: requisitos previos'
author: adrianhall
description: Obtén información sobre cómo empezar con el desarrollo de aplicaciones de Microsoft Teams y cómo configurar el entorno.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 6496d238b3858c1df974732fa57c28eed7c54eb2
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994192"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>Requisitos previos: Introducción al desarrollo de aplicaciones de Microsoft Teams

Antes de crear la primera aplicación de Teams, debes instalar algunas herramientas y configurar el entorno de desarrollo.

## <a name="install-required-tools"></a>Instalar las herramientas necesarias

Algunas de las herramientas que necesitas dependen de cómo prefieras crear la aplicación de Teams:

- [Node.js](https://nodejs.org/en/download/) (use la versión más reciente de LTS de v14)
- Un explorador con herramientas de desarrollador, como [Microsoft Edge](https://www.microsoft.com/edge) (recomendado) o [Google Chrome](https://www.google.com/chrome/)
- Si está desarrollando con JavaScript, TypeScript o SharePoint Framework (SPFx), instale [Visual Studio Code](https://code.visualstudio.com/download), versión 1.55 o posterior.  
- Si está desarrollando con .NET, instale [Visual Studio 2019](https://visualstudio.com/download). Asegúrese de instalar la carga **ASP.NET desarrollo web y web** o la carga de trabajo de desarrollo **multiplataforma de .NET Core.**

> [!WARNING]
> Existen problemas conocidos con `npm@7` , empaquetados con node v15 y versiones posteriores. Si tiene problemas para ejecutarse, asegúrese de que está `npm install` usando el nodo v14 (LTS)

## <a name="install-the-teams-toolkit"></a>Instalar el kit de herramientas de Teams

Teams Toolkit ayuda a simplificar el proceso de desarrollo con herramientas para aprovisionar e implementar recursos en la nube para la aplicación, publicar en la tienda de Teams y mucho más. Puede usar el kit de herramientas con Visual Studio code, Visual Studio o como una CLI (llamada `teamsfx` ).

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abrir Visual Studio Code.
1. Seleccione la vista Extensiones (**Ctrl+Mayús+X**  /  **,⇧-X** o **Ver > extensiones**).
1. En el cuadro de búsqueda, escriba **Teams Toolkit**.
1. Seleccione el botón de instalación verde junto al Kit de herramientas de Teams.

También puede encontrar el Kit de herramientas de Teams en [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

Las siguientes herramientas se pueden instalar mediante la Visual Studio code cuando sean necesarias. Si ya está instalada, la versión instalada se puede usar en su lugar. Si usa Linux incluido WSL, debe instalar estas herramientas antes de usar:

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools se usa para ejecutar los componentes back-end localmente durante una ejecución de depuración local, incluidas las aplicaciones auxiliares de autenticación necesarias para ejecutar los servicios en Azure. Se instala en el directorio del proyecto (mediante el npm `devDependencies` ).

- [SDK de .NET](/dotnet/core/install/)

    El SDK de .NET se usa para instalar enlaces personalizados para la depuración local y las implementaciones de aplicaciones de Azure Functions. Si no ha instalado el SDK de .NET 3.1 (o posterior) globalmente, se puede instalar la versión portátil.

- [ngrok](https://ngrok.com/download)

    Algunas características de la aplicación de Teams (bots de conversación, extensiones de mensajería y webhooks entrantes) requieren conexiones entrantes. Debe exponer el sistema de desarrollo a Teams a través de un túnel. No es necesario un túnel para las aplicaciones que solo incluyen pestañas. Este paquete se instala en el directorio del proyecto (mediante npm `devDependencies` ).

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Puedes usar Visual Studio 2019 para desarrollar aplicaciones de Teams con Blazor Server en .NET. Si no tiene la intención de desarrollar aplicaciones de Teams en .NET, instale la Visual Studio code de Teams Toolkit.

Para instalar la extensión de Teams Toolkit:

1. Abra Visual Studio 2019.
1. Seleccione **Extensiones Administrar**  >  **extensiones**.
1. En el cuadro de búsqueda, escriba **Teams Toolkit**.
1. Seleccione la extensión Kit de herramientas de Teams y **seleccione Descargar**.

La extensión se puede descargar. Cierre Visual Studio 2019 para instalar la extensión.

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

- [Herramientas para desarrolladores de React para Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

Si quieres tener acceso a los datos almacenados en Azure o implementar un back-end basado en la nube para tu aplicación de Teams en Azure, instala estas herramientas:

- [Azure Tools for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Si trabaja con datos de Microsoft Graph, debe obtener más información y marcar el Explorador de Microsoft Graph. Esta herramienta basada en explorador te permite consultar Microsoft Graph fuera de una aplicación.

- [Explorador de Microsoft Graph](https://developer.microsoft.com/graph/graph-explorer)

Con el Portal para desarrolladores para Teams, puedes configurar, administrar y distribuir la aplicación de Teams, incluida la organización o la tienda de Teams.

- [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>Habilitar la instalación local

Durante el desarrollo, debes cargar la aplicación en Teams sin distribuirla. Esto se conoce como "sideloading".

1. Si tienes una cuenta de Teams, comprueba si puedes realizar la instalación local de aplicaciones en Teams:

    1. En el cliente de Teams, seleccione **Aplicaciones**.
    1. Busque una opción para **Cargar una aplicación personalizada.**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde se puede cargar una aplicación personalizada en Teams.":::

> [!NOTE]
> Si aún no puedes realizar la instalación local de aplicaciones, habla con el administrador de Teams. Consulta [Habilitar aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) para obtener más información.

## <a name="get-a-free-teams-developer-tenant-optional"></a>Obtener un inquilino para desarrolladores de Teams gratuito (opcional)

Si no puede ver la opción de instalación local o no tiene una cuenta de Teams, puede obtener una cuenta para desarrolladores de Teams gratuita uniéndose al programa de desarrolladores M365.  El proceso de registro tarda aproximadamente dos minutos.

1. Vaya al programa para desarrolladores de [Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Selecciona **Unirse ahora** y sigue las instrucciones en pantalla.
1. Cuando llegue a la pantalla de bienvenida, seleccione **Configurar la suscripción de E5**.
1. Configurar la cuenta de administrador. Una vez que termines, deberías ver una pantalla como esta.

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa para desarrolladores de Microsoft 365.":::

1. Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.
1. Comprueba si ahora tienes la opción **Cargar una aplicación** personalizada.

## <a name="get-a-free-azure-account"></a>Obtener una cuenta gratuita de Azure

Si quieres hospedar la aplicación o acceder a recursos dentro de Azure, debes tener una suscripción a Azure.  Puede crear [una cuenta gratuita antes](https://azure.microsoft.com/free/) de comenzar.

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>Iniciar sesión en sus cuentas de Microsoft 365 y Azure

Debe tener acceso a dos cuentas:

- Sus credenciales de cuenta de Microsoft 365. Esta es la cuenta que usa para iniciar sesión en Teams. Si usas un inquilino del programa para desarrolladores de Microsoft 365, esta es la cuenta de administrador que configuraste al registrarte en el programa.
- - Sus credenciales de Azure. Esta es la cuenta que usa para obtener acceso a Azure Portal y para aprovisionar nuevos recursos en la nube para admitir la aplicación.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abrir Visual Studio código
1. Selecciona el Teams en la barra lateral:

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Iniciar sesión en M365**.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Ubicación de la sección Cuentas usada para iniciar sesión.":::

1. El proceso de inicio de sesión comienza a usar el explorador web normal. Complete el proceso de inicio de sesión de su cuenta M365. Se le pedirá cuándo puede cerrar el explorador y volver a Visual Studio Code.
1. Vuelva al Teams Toolkit dentro de Visual Studio Code.
1. Seleccione **Iniciar sesión en Azure**.

    > [!TIP]
    > Si tiene instalada la extensión cuenta de Azure y usa la misma cuenta, puede omitir este paso. Usa la misma cuenta que usas en otras extensiones.

1. El proceso de inicio de sesión comienza a usar el explorador web normal.  Complete el proceso de inicio de sesión de su cuenta de Azure. Se le pedirá cuándo puede cerrar el explorador y volver a Visual Studio Code.

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

---

Ahora que el entorno de desarrollo está configurado, puedes crear, crear e implementar la primera aplicación Teams desarrollo.

## <a name="see-also"></a>Ver también

- [Crear la primera aplicación Teams con Blazor](first-app-blazor.md)
- [Crear la primera aplicación Teams con SharePoint Framework (SPFx)](first-app-spfx.md)
- [Crear una aplicación de bots de conversación](first-app-bot.md)
- [Crear una extensión de mensajería](first-message-extension.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crea la primera aplicación Teams con React](first-app-react.md)
