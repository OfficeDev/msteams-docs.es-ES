---
title: Crear aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio Code con el kit de herramientas de Microsoft Teams
keywords: Kit de herramientas de visual Studio Code de teams
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 841dddfd515fd202a36f4c8a6b490faccff7b537
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2022
ms.locfileid: "65887607"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Compilación de aplicaciones con el kit de herramientas de Teams y Visual Studio Code

El kit de herramientas de Teams para Visual Studio Code ayuda a los desarrolladores a crear e implementar aplicaciones de Teams con identidad integrada, acceso al almacenamiento en la nube, datos de Microsoft Graph y otros servicios en Azure y Microsoft 365 con un enfoque de "configuración cero" para la experiencia del desarrollador.  

También puede usar el kit de herramientas con Visual Studio o como una CLI (denominada `teamsfx`).

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Instalación del kit de herramientas de Teams para Visual Studio Code

1. Abrir Visual Studio Code.
1. Seleccione la vista Extensiones (**Ctrl+Mayús+X** / **⌘⇧-X** o **Ver extensiones >**).
1. En el cuadro de búsqueda, escriba _Kit de herramientas de Teams_.
1. Seleccione el botón de instalación verde situado junto al kit de herramientas de Teams.

También puede encontrar el kit de herramientas de Teams en [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

La extensión de Visual Studio Code instala las herramientas siguientes cuando se necesitan. Si ya está instalado, se usa la versión instalada en su lugar. Si usa Linux (incluido WSL), debe instalar estas herramientas antes de usar:

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools se usa para ejecutar los componentes de back-end localmente durante una ejecución de depuración local, incluidos los asistentes de autenticación necesarios al ejecutar los servicios en Azure. Se instala en el directorio del proyecto mediante npm `devDependencies`.

- [SDK de .NET](/dotnet/core/install/)

    El SDK de .NET se usa para instalar enlaces personalizados para la depuración local y las implementaciones de aplicaciones de Azure Functions. Si no ha instalado el SDK de .NET 3.1 o versiones posteriores globalmente, se instala la versión portable.

- [ngrok](https://ngrok.com/download)

    Algunas características de aplicaciones de Teams (bots conversacionales, extensiones de mensajería y webhooks entrantes) requieren conexiones entrantes.  Debe exponer el sistema de desarrollo a Teams a través de un túnel. No es necesario un túnel para las aplicaciones que solo incluyen pestañas.  Este paquete se instala en el directorio del proyecto (mediante npm `devDependencies`).

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Uso del kit de herramientas de Teams para Visual Studio Code

- [Configuración de un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Ejecutar la aplicación localmente](#install-and-run-your-app-locally)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configuración de un nuevo proyecto de Teams

El kit de herramientas de Teams puede crear aplicaciones de React hospedadas en elementos web de Azure o SPFx hospedados en el entorno de Microsoft 365 SharePoint. Para crear una nueva aplicación de React que se hospedará en Azure:

1. Abra Visual Studio Code.
1. Abra el Kit de herramientas de Teams. Para ello, seleccione el icono de Teams en la barra lateral:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Crear nuevo proyecto**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. Seleccione **Crear una nueva aplicación de Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. En el paso **Seleccionar funcionalidades** , ya está seleccionada la funcionalidad **De** tabulación. Opcionalmente, también puede seleccionar **Bot** and **Messaging Extension (Bot y extensión de mensajería).**  Pulse **Aceptar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. En el paso **Tipo de hospedaje del front-end**, seleccione **Azure**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje para la nueva aplicación.":::

1. Opcionalmente, en el paso **Recursos** en la nube, seleccione los recursos en la nube que usa la aplicación. Puede seleccionar acceso CRUD (crear, leer, actualizar y eliminar) a una tabla SQL o a una API:

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Captura de pantalla que muestra cómo agregar recursos de nube para la nueva aplicación.":::

1. En el paso **Lenguaje de programación** , puede elegir **JavaScript** o **TypeScript**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. Seleccione una carpeta de área de trabajo. Se crea una carpeta dentro de la carpeta del área de trabajo para el proyecto que está creando.

1. Escriba un nombre adecuado para la aplicación, como `helloworld`. El nombre de la aplicación solo puede contener caracteres alfanuméricos.  Presione **Entrar** para continuar.

La aplicación de Teams se crea en unos segundos. La aplicación scaffolding contiene código para controlar el inicio de sesión único con Azure Active Directory y el acceso a Microsoft Graph.  Si seleccionó recursos de Azure, el código de esos recursos también estará disponible.

Para obtener un tutorial sobre el proceso de creación y publicación de SPFx, consulte el [tutorial de SPFx](../get-started/first-app-spfx.md).

## <a name="configure-your-app"></a>Configurar la aplicación

En esencia, la aplicación de Teams abarca tres componentes:

  1. Cliente de Microsoft Teams (web, escritorio o móvil) donde los usuarios interactúan con la aplicación.
  1. Servidor que responde a las solicitudes de contenido que se muestran en Teams. Por ejemplo, el contenido de la pestaña HTML o una tarjeta adaptable de bot.
  1. Un paquete de aplicación de Teams consta de tres archivos:

      > [!div class="checklist"]
      >
      > - Manifest.json.
      > - Icono de [color](../resources/schema/manifest-schema.md#icons) para que la aplicación se muestre en el catálogo de aplicaciones pública u organización.
      > - Icono [de esquema](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividad de Teams.

El manifiesto y los iconos se almacenan en la `.fx` carpeta del proyecto antes de cargarse en Teams. Cuando se instala una aplicación, el cliente de Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

1. Para configurar la aplicación, vaya a la pestaña **Kit de herramientas de Teams** en Visual Studio Code.
1. Seleccione **Editor de manifiestos** en la sección **Proyecto** .

La edición de los campos de la página Detalles de la aplicación actualiza el contenido del archivo manifest.json que se envía en última instancia como parte del paquete de la aplicación.

## <a name="install-and-run-your-app-locally"></a>Instalación y ejecución de la aplicación localmente

Para crear y ejecutar la aplicación localmente:

1. Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.

   > Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.  Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.  Este proceso puede tardar entre 3 o 5 minutos.

   El kit de herramientas le pide que instale un certificado local si es necesario. Este certificado permite a Teams cargar la aplicación desde `https://localhost`. Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. Se inicia el explorador web para ejecutar la aplicación. Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador. También se le pedirá que cambie a la aplicación teams en otras ocasiones. Seleccione la aplicación web cuando esto ocurra.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Captura de pantalla que muestra cómo elegir la versión web de Teams al iniciarlo":::

1. Es posible que se le pida que inicie sesión. Si es así, inicie sesión con su cuenta de Microsoft 365.
1. Cuando se le pida que instale la aplicación en Teams, presione **Agregar**.

Tanto el back-end como el front-end se enlazan al depurador de Visual Studio Code.  Esto le permite establecer puntos de interrupción en cualquier parte del código e inspeccionar el estado.  También puede usar cualquier herramienta de depuración de front-end (como React Developer Tools) en el explorador.  Para obtener más información sobre la depuración en Visual Studio Code, revise [la documentación](https://code.visualstudio.com/Docs/editor/debugging).

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

Antes de que lo puedan usar otras personas, debe publicar la aplicación en el Portal para desarrolladores de Teams.

1. Para publicar la aplicación, vaya a la pestaña **Kit de herramientas de Teams** en Visual Studio Code.
1. Seleccione **Publicar en Teams** en la sección **Proyecto** .

Si usa el hospedaje de Azure, debe haber aprovisionado e implementado en la nube. Para obtener un tutorial del proceso de publicación de SPFx, consulte el [tutorial de SPFx](../get-started/first-app-spfx.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mantenimiento y soporte técnico de su aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="see-also"></a>Vea también

* [Compilar aplicaciones con el kit de herramientas de Teams y Visual Studio](~/toolkit/visual-studio-overview.md)
* [Compilación de pestañas y otras experiencias hospedadas con el SDK de cliente de JavaScript de Microsoft Teams](~/tabs/how-to/using-teams-client-sdk.md)
