---
title: 'Introducción: crea la primera aplicación Teams con SPFx'
author: zhenyasav
description: Obtenga información sobre cómo crear una pestaña personalizada con el SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 54886b47bbe70fed5dd1f010517e6c91d8d5a50d
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646862"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a>Compila y ejecuta la primera aplicación Microsoft Teams con SharePoint Framework (SPFx)

En este tutorial, crearás una nueva aplicación Microsoft Teams en SharePoint Framework (SPFx) que implemente una aplicación personal sencilla. (Una *aplicación personal* incluye un conjunto de pestañas con ámbito para uso individual). Durante el tutorial, aprenderás sobre la estructura de una aplicación Teams, cómo ejecutar la aplicación localmente y cómo implementar la aplicación en SharePoint.

## <a name="before-you-begin"></a>Antes de empezar

Asegúrese de que el entorno de desarrollo está configurado mediante la instalación de los [requisitos previos](prerequisites.md)

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="get-organized"></a>Organizarse

Además de los requisitos previos, también debe ser administrador de una colección SharePoint de sitios.  Aquí es donde implementará la aplicación para el hospedaje.  Si usa un inquilino del programa para desarrolladores M365, use la cuenta de administrador que haya configurado al registrarse en el programa.  

## <a name="create-your-project"></a>Crear el proyecto

Use el Teams Toolkit para crear el primer proyecto:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abra Visual Studio código.
1. Abra el Teams Toolkit seleccionando el icono Teams en la barra lateral:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono Teams en la barra lateral Visual Studio Code barra lateral.":::

1. Seleccione **Crear nuevo Project**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Create New Project en la barra lateral Teams Toolkit barra lateral.":::

1. Selecciona **Crear una nueva Teams aplicación**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del asistente para Crear Project":::

1. En el **paso Seleccionar capacidades,** la **funcionalidad Tab** ya estará seleccionada.  Pulse **Aceptar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. En el **paso Tipo de hospedaje front-end,** seleccione SharePoint Framework **(SPFx).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje de la nueva aplicación.":::

1. En el **paso Marco,** seleccione **React**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Seleccionar marco":::

1. Cuando se le pida un **nombre de elemento web,** presione **Entrar** para aceptar el valor predeterminado.

1. Cuando se le pida la **descripción del elemento web,** presione **ENTRAR** para aceptar el valor predeterminado.

1. Cuando se le pida el **lenguaje de programación,** presione **ENTRAR** para aceptar el valor predeterminado.

1. Seleccione una carpeta de área de trabajo.  Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que está creando.

1. Escribe un nombre adecuado para la aplicación, como `helloworld` .  El nombre de la aplicación debe estar formado solo por caracteres alfanuméricos.  Presione **ENTRAR** para continuar.

La Teams se creará en unos segundos.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

Use la `teamsfx` CLI para crear el primer proyecto.  Comience desde la carpeta donde desea crear la carpeta del proyecto.

``` bash
teamsfx new
```

La CLI le guiará por algunas preguntas para crear el proyecto.  Cada pregunta le dirá cómo responderla (por ejemplo, usar teclas de flecha para seleccionar una opción).  Cuando haya respondido a la pregunta, confirme su elección presionando **Entrar**.

1. Selecciona **Crear una nueva Teams aplicación**.
1. Elija la **funcionalidad Tab.**
1. Seleccione **SharePoint Framework (SPFx) de** front-end.
1. Seleccione **React** framework.
1. Presione **Entrar** para el **nombre del elemento web**.
1. Presione **ENTRAR** para la **descripción del elemento web**.
1. Presione **ENTRAR** para el **lenguaje de programación**.
1. Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.
1. Escribe un nombre adecuado para la aplicación, como `helloworld` .  El nombre de la aplicación debe estar formado solo por caracteres alfanuméricos.

Una vez que se hayan contestado todas las preguntas, se creará el proyecto.

---

- [Obtenga más información sobre el desarrollo para SharePoint Framework](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a>Realizar un recorrido por el código fuente

Si quieres omitir esta sección por ahora, puedes [ejecutar la aplicación localmente.](#run-your-app-locally)

Una vez Teams Toolkit configurar el proyecto, tienes los componentes para crear una aplicación personal básica para Teams que se hospeda en el SharePoint Framework.  Los directorios y archivos del proyecto se muestran en el área Explorador de Visual Studio Code.

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio Code.":::

El Toolkit crea automáticamente scaffolding en el directorio del proyecto en función de las capacidades que agregó durante la instalación. El Teams Toolkit mantiene su estado para la aplicación en el `.fx` directorio.  Entre otros elementos de este directorio:

- Los iconos de la aplicación se almacenan como archivos PNG `color.png` en y `outline.png` .
- El manifiesto de la aplicación para publicar en el Portal de desarrolladores para Teams se almacena en `manifest.source.json` .
- La configuración que eligió al crear el proyecto se almacena en `settings.json` .

Dado que ha seleccionado un SPFx webpart, los siguientes archivos son relevantes para la interfaz de usuario:

- La carpeta `SPFx/src/webparts/{webpart}` contiene el SPFx webpart.
- El archivo `.vscode/launch.json` describe las configuraciones de depuración disponibles en la paleta de depuración.

Para obtener más información sobre SharePoint webparts para Teams, [consulte la SharePoint .](/sharepoint/dev/spfx/build-for-teams-overview)

## <a name="run-your-app-locally"></a>Ejecutar la aplicación localmente

Teams Toolkit permite hospedar la aplicación localmente y ejecutarla a través de [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>Cree y ejecute la aplicación localmente en Visual Studio Code

Para compilar y ejecutar la aplicación localmente:

1. Desde Visual Studio Code, presione **F5**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Captura de pantalla que muestra cómo iniciar una SPFx en un área de trabajo local.":::

   > [!NOTE]
   > Cuando ejecutas la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.  Una ventana del explorador se abre automáticamente y carga SharePoint Workbench cuando se completa la compilación.  Esto puede tardar entre 3 y 5 minutos en completarse.

   Una vez que se SharePoint Workbench.

   >[!NOTE]
   > El Toolkit le pedirá que instale un certificado local si es necesario. Este certificado permite Teams cargar la aplicación desde `https://localhost` . Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla que muestra cómo se indica cómo instalar un certificado SSL para Teams cargar la aplicación desde localhost.":::

1. Presione uno de los **iconos Agregar elemento web** (+) para agregar el elemento web.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Captura de pantalla que muestra SPFx workbench que se ejecuta con el elemento emergente para agregar un elemento web que se muestra.":::

1. Elija el elemento web en el menú.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Captura de pantalla que muestra SPFx workbench que se ejecuta con el elemento emergente para agregar una selección de elemento web.":::

La aplicación debería estar ejecutándose.  Puede realizar actividades de depuración normales como si se tratase de otras SPFx webpart (como establecer puntos de interrupción).

> [!TIP]
> Intente colocar puntos de interrupción en el método de representación `SPFx/src/webparts/{webpart}/{webpart}.ts` y volver a cargar la ventana del explorador. VS Code se detendrá en puntos de interrupción en el código.

## <a name="deploy-your-app-to-sharepoint"></a>Implementar la aplicación en SharePoint

Asegúrate de que SharePoint catálogo de aplicaciones existe en la implementación.  Si no existe, [cree uno](/sharepoint/use-app-catalog).  El catálogo de aplicaciones puede tardar hasta 15 minutos en crearse completamente.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abra Visual Studio Code.
1. Seleccione el Teams Toolkit de la barra lateral seleccionando el Teams.
1. Seleccione **Aprovisionar en la nube**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Captura de pantalla que muestra los comandos de aprovisionamiento":::

1. Puede supervisar el progreso viendo los cuadros de diálogo en la esquina inferior derecha.  Después de unos segundos, verá el siguiente aviso:

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo completado de aprovisionamiento.":::

1. Una vez completado el aprovisionamiento, seleccione **Implementar en la nube.**

1. Actualmente, la implementación automatizada no está disponible.  Aparecerá un cuadro de diálogo que le pedirá que cree e implemente manualmente. Presione **Compilar SharePoint paquete**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Captura de pantalla del cuadro de diálogo Compilar paquete de Sharepoint":::

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

En la ventana de terminal:

1. Ejecute `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Es posible que se le pida que inicie sesión en su suscripción de Azure.  Si es necesario, se le pedirá que seleccione una suscripción de Azure que se usará para los recursos de Azure.

   > [!NOTE]
   > Siempre hay algunos recursos de Azure usados para hospedar la aplicación.

1. Ejecute `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

1. Cuando se le pida, **seleccione Compilar SharePoint paquete**.

---

El SharePoint se encuentra dentro `SPFx/sharepoint/solution` del proyecto.  Upload el paquete a SharePoint:

1. Inicie sesión en la Consola de administración de M365 y, a continuación, vaya al catálogo SharePoint de aplicaciones.

   - Abra `https://admin.microsoft.com/AdminPortal/Home` .
   - En **Centros de administración,** seleccione el **SharePoint** de administración.
   - Selecciona **Más características en** el menú de la barra lateral.
   - Presione **Abrir en** **Aplicaciones**.
   - Seleccione **Catálogo de aplicaciones**.

1. Selecciona **Distribuir aplicaciones para SharePoint**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Distribuir aplicaciones para SharePoint.":::

1. Seleccione **Upload**.

1. Presione **Elegir archivo**.

1. Busque el `{project}.sppkg` archivo, ubicado en la `SPFx/sharepoint/solution` carpeta dentro del proyecto.  Presione **Abrir**.

1. Pulse **Aceptar**.

1. El SharePoint de implementación se iniciará automáticamente.  Asegúrese **de que esta solución esté disponible para todos** los sitios de la organización y, a continuación, presione **Implementar**.

1. Seleccione la **pestaña** ARCHIVOS.

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Seleccione la pestaña archivos en el catálogo SharePoint de aplicaciones.":::

1. seleccione el paquete que implementó y, a continuación, presione **Sincronizar para Teams** en la cinta de opciones.

    > [!Note]
    > El proceso de sincronización Teams puede tardar un par de minutos.  Verás un mensaje en el lado derecho del explorador que indica que la aplicación se ha sincronizado correctamente con Teams.

Abra la Teams (o inicie sesión en `https://teams.microsoft.com` ).  Presione el triple punto en la barra lateral y, a continuación, **seleccione Todas las aplicaciones**.  La aplicación se colocará en las **aplicaciones creadas para tu categoría de** organización.  Puedes agregar la aplicación desde allí.

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Captura de pantalla que muestra la aplicación en Teams":::

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre otros métodos para crear Teams aplicaciones:

- [Crear una aplicación Teams con React](first-app-react.md)
- [Crear una Teams con Blazor](first-app-blazor.md)
- [Crear una aplicación de bot conversacional](first-app-bot.md)
- [Crear una extensión de mensajería](first-message-extension.md)
