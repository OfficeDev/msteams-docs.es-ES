---
title: Crear aplicaciones con el Microsoft Teams Toolkit y Visual Studio Code
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente Visual Studio Code con el Microsoft Teams Toolkit
keywords: Kit de herramientas de código visual studio de teams
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 8eeaadf28b9bdb46c91a803a66b4855d2a5e848c
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948442"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Crear aplicaciones con el Teams Toolkit y Visual Studio Code

El Teams Toolkit para Visual Studio Code ayuda a los desarrolladores a crear e implementar aplicaciones de Teams con identidad integrada, acceso al almacenamiento en la nube, datos de Microsoft Graph y otros servicios en Azure y M365 con un enfoque de "configuración cero" para la experiencia del desarrollador.  

También puede usar el kit de herramientas con Visual Studio o como una CLI (denominada `teamsfx` ).

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Instalar el Teams Toolkit para Visual Studio Code

1. Abrir Visual Studio Code.
1. Seleccione la vista Extensiones (**Ctrl+Mayús+X**  /  **,⇧-X** o **Ver > extensiones**).
1. En el cuadro de búsqueda, _escriba Teams Toolkit_.
1. Seleccione el botón de instalación verde junto a la Teams Toolkit.

También puede encontrar el Teams Toolkit en el Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

Las siguientes herramientas las instala la Visual Studio Code cuando son necesarias. Si ya está instalado, la versión instalada se usa en su lugar. Si usa Linux (incluido WSL), debe instalar estas herramientas antes de usar:

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools se usa para ejecutar los componentes back-end localmente durante una ejecución de depuración local, incluidas las aplicaciones auxiliares de autenticación necesarias para ejecutar los servicios en Azure. Se instala en el directorio del proyecto mediante el npm `devDependencies` .

- [SDK de .NET](/dotnet/core/install/)

    El SDK de .NET se usa para instalar enlaces personalizados para la depuración local y las implementaciones de aplicaciones de Azure Functions. Si no ha instalado el SDK de .NET 3.1 o posterior globalmente, se instalará la versión portátil.

- [ngrok](https://ngrok.com/download)

    Algunas Teams de la aplicación (bots de conversación, extensiones de mensajería y webhooks entrantes) requieren conexiones entrantes.  Debe exponer el sistema de desarrollo para Teams a través de un túnel. No es necesario un túnel para las aplicaciones que solo incluyen pestañas.  Este paquete se instala en el directorio del proyecto (mediante npm `devDependencies` ).

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Use el Teams Toolkit para Visual Studio Code

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Ejecutar la aplicación localmente](#install-and-run-your-app-locally)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto Teams proyecto

El Teams Toolkit puede crear aplicaciones React que se hospedan en Azure o en elementos web SPFx hospedados en el entorno de SharePoint M365. Para crear una nueva React que se va a hospedar en Azure:

1. Abra Visual Studio Code.
1. Abra el Kit de herramientas de Teams. Para ello, seleccione el icono de Teams en la barra lateral:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Crear nuevo proyecto**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. Seleccione **Crear una nueva aplicación de Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. En el **paso Seleccionar capacidades,** la **funcionalidad Tab** ya está seleccionada. También puede seleccionar opcionalmente **Bot** y **Messaging Extension**.  Pulse **Aceptar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. En el paso **Tipo de hospedaje del front-end**, seleccione **Azure**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje para la nueva aplicación.":::

1. Opcionalmente, en el paso **Recursos de** nube, seleccione recursos en la nube que use la aplicación. Puede seleccionar el acceso CRUD (crear, leer, actualizar y eliminar) a una tabla SQL una API:

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Captura de pantalla que muestra cómo agregar recursos de nube para la nueva aplicación.":::

1. En el paso **Lenguaje de** programación, puede elegir **JavaScript** o **TypeScript**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. Seleccione una carpeta de área de trabajo. Se crea una carpeta dentro de la carpeta del área de trabajo para el proyecto que está creando.

1. Escriba un nombre adecuado para la aplicación, como `helloworld`. El nombre de la aplicación solo puede contener caracteres alfanuméricos.  Presione **Entrar** para continuar.

La Teams se crea en unos segundos. La aplicación scaffolded contiene código para controlar el inicio de sesión único con Azure Active Directory acceso a microsoft Graph.  Si seleccionó recursos de Azure, también estará disponible el código para esos recursos.

Para obtener un recorrido por el proceso SPFx creación y publicación, vea el [tutorial SPFx .](../get-started/first-app-spfx.md)

## <a name="configure-your-app"></a>Configurar la aplicación

En su núcleo, la aplicación Teams abarca tres componentes:

  1. El Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.
  1. Un servidor que responde a las solicitudes de contenido que se muestran en Teams. Por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.
  1. Un Teams de la aplicación consta de tres archivos:

      > [!div class="checklist"]
      >
      > - Manifest.json.
      > - Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización.
      > - Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra Teams actividad.

El manifiesto y los iconos se almacenan en la carpeta del proyecto antes de `.fx` cargarse en Teams. Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

1. Para configurar la aplicación, vaya a la **pestaña Teams Toolkit** en Visual Studio Code.
1. Seleccione **Editor de manifiestos** **en Project** sección.

La edición de los campos de la página detalles de la aplicación actualiza el contenido del archivo manifest.json que finalmente se envía como parte del paquete de la aplicación.

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación localmente

Para crear y ejecutar la aplicación localmente:

1. Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.

   > Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.  Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.  Este proceso puede tardar entre 3 o 5 minutos.

   El kit de herramientas le pide que instale un certificado local si es necesario. Este certificado permite a Teams cargar la aplicación desde `https://localhost`. Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. Se inicia el explorador web para ejecutar la aplicación. Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador. Es posible que también se le pida que cambie a la Teams en otras ocasiones. Seleccione la aplicación web cuando esto suceda.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Captura de pantalla que muestra cómo elegir la versión web de Teams al iniciarlo":::

1. Es posible que se le pida que inicie sesión. Si es así, inicie sesión con su cuenta de M365.
1. Cuando se le pida que instale la aplicación en Teams, presione **Agregar**.

Tanto el back-end como el front-end están unidos al depurador Visual Studio Code servidor.  Esto le permite establecer puntos de interrupción en cualquier lugar del código e inspeccionar el estado.  También puede usar cualquier herramienta de depuración front-end (como React Developer Tools) en el explorador.  Para obtener más información acerca de la depuración en Visual Studio Code, revise [la documentación](https://code.visualstudio.com/Docs/editor/debugging).

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

Antes de que otras personas la puedan usar, debes publicar la aplicación en el Portal de desarrolladores para Teams.

1. Para publicar la aplicación, vaya a la **pestaña Teams Toolkit** en Visual Studio Code.
1. Seleccione **Publicar para Teams** en la **Project.**

Si usa el hospedaje de Azure, debe haber aprovisionado e implementado en la nube. Para obtener un recorrido por el proceso de SPFx de publicación, vea el [SPFx tutorial](../get-started/first-app-spfx.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mantenimiento y soporte técnico de la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="see-also"></a>Consulte también

* [Crear aplicaciones con el Teams Toolkit y Visual Studio](~/toolkit/visual-studio-overview.md)
* [Crear pestañas y otras experiencias hospedadas con el SDK Microsoft Teams cliente de JavaScript](~/tabs/how-to/using-teams-client-sdk.md)
