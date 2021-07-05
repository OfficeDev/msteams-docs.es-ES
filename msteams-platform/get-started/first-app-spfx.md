---
title: 'Introducción: crea la primera aplicación Teams con SPFx'
author: zhenyasav
description: Obtenga información sobre cómo crear una pestaña personalizada con el SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 4df2bb71837af520a2d2500a45b8605e5fae08b2
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254226"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a>Compila y ejecuta la primera aplicación Microsoft Teams con SharePoint Framework (SPFx)

En este tutorial, aprenderás a crear una nueva aplicación Microsoft Teams en SharePoint Framework SPFx que implemente una aplicación personal sencilla. Por ejemplo, una *aplicación personal incluye* un conjunto de pestañas para uso individual. Durante el tutorial, aprenderás sobre la estructura de una aplicación de Teams, cómo ejecutar una aplicación localmente y cómo implementar la aplicación en SharePoint.

## <a name="before-you-begin"></a>Antes de empezar

Asegúrese de que el entorno de desarrollo está configurado instalando los requisitos previos.

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="get-organized"></a>Organizarse

Además de los requisitos previos, también debe ser administrador de una colección SharePoint de sitios.  Aquí es donde implementará la aplicación para el hospedaje.  Si usa un inquilino del programa para desarrolladores M365, use la cuenta de administrador que haya configurado al registrarse en el programa.  

## <a name="create-your-project"></a>Crear un proyecto

Use el Kit de herramientas de Teams para crear su primer proyecto:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abra Visual Studio Code.
1. Seleccione el Teams en la barra lateral para abrir el Teams Toolkit.

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. Seleccione **Crear nuevo proyecto**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. Seleccione **Crear una nueva aplicación de Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. En la **sección Seleccionar capacidades,** seleccione **Ficha** y seleccione **Aceptar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. En la **sección Tipo de hospedaje front-end,** seleccione SharePoint Framework **(SPFx).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje para la nueva aplicación.":::

1. En la **sección Marco,** **seleccione React**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Seleccionar marco":::

1. Cuando se le pida un **nombre de elemento web,** presione **Entrar** para aceptar el valor predeterminado.

1. Cuando se le pida la **descripción del elemento web,** presione **ENTRAR** para aceptar el valor predeterminado.

1. Cuando se le pida el **lenguaje de programación,** presione **ENTRAR** para aceptar el valor predeterminado.

1. Seleccione una carpeta de área de trabajo.  Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que esté creando.

1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo puede contener caracteres alfanuméricos.  Presione **Entrar** para continuar.

   La aplicación Teams se creará en unos segundos.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

Use la CLI de `teamsfx` para crear su primer proyecto:  Comience en la carpeta en la que quiera crear la carpeta del proyecto.

``` bash
teamsfx new
```

La CLI le guiará por varias preguntas para crear el proyecto.  En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).  Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.

1. Seleccione **Crear una nueva aplicación de Teams**.
1. Seleccione **Tab**.
1. Seleccione **SharePoint Framework (SPFx) de** front-end.
1. Seleccione **React** framework.
1. Presione **Entrar** para el **nombre del elemento web**.
1. Presione **ENTRAR** para la **descripción del elemento web**.
1. Presione **ENTRAR** para el **lenguaje de programación**.
1. Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.
1. Escriba un nombre adecuado para la aplicación, como `helloworld`.  El nombre de la aplicación solo puede contener caracteres alfanuméricos.

   Una vez contestadas todas las preguntas, se creará el proyecto.

---

- [Obtenga más información sobre el desarrollo para SharePoint Framework](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a>Dar un paseo por el código fuente

Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).

Después de Teams Toolkit configurar el proyecto, tienes los componentes para crear una aplicación personal básica para Teams que se hospeda en el SharePoint Framework.  Los archivos y directorios del proyecto se muestran en el área del Explorador de Visual Studio Code.

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio Code.":::

El kit de herramientas crea automáticamente el scaffolding en el directorio del proyecto en función de las funcionalidades que ha agregado durante la configuración. El Kit de herramientas de Teams mantiene el estado para la aplicación en el directorio `.fx`.  Entre otros elementos de este directorio:

- Los iconos de aplicación se almacenan como archivos PNG en `color.png` y `outline.png`.
- El manifiesto de la aplicación para publicar en el Portal de desarrolladores para Teams se almacena en `manifest.source.json` .
- La configuración que eligió al crear el proyecto se almacena en `settings.json`.

Dado que ha seleccionado un SPFx webpart, los siguientes archivos son relevantes para la interfaz de usuario:

- La carpeta `SPFx/src/webparts/{webpart}` contiene el SPFx webpart.
- El archivo `.vscode/launch.json` describe las configuraciones de depuración disponibles en la paleta de depuración.

Para obtener más información sobre SharePoint webparts para Teams, [consulte la SharePoint .](/sharepoint/dev/spfx/build-for-teams-overview)

## <a name="run-your-app-locally"></a>Ejecutar la aplicación localmente

Teams Toolkit permite hospedar la aplicación localmente y ejecutarla a través de [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>Compilar y ejecutar la aplicación de forma local en Visual Studio Code

Para crear y ejecutar la aplicación localmente:

1. Desde Visual Studio Code, presione la **tecla F5.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Captura de pantalla que muestra cómo iniciar una SPFx en un área de trabajo local.":::

   > [!NOTE]
   > Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.  Una ventana del explorador se abre automáticamente y carga SharePoint Workbench cuando se completa la compilación.  Este proceso puede tardar entre 3 o 5 minutos.

   Después de cargar SharePoint Workbench.

   >[!NOTE]
   > El Kit de herramientas le pedirá que instale un certificado local si es necesario. Este certificado permite a Teams cargar la aplicación desde `https://localhost`. Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. Seleccione **Agregar elemento web + iconos** para agregar el elemento web.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Captura de pantalla que muestra SPFx workbench que se ejecuta con el elemento emergente para agregar un elemento web que se muestra.":::

1. Seleccione el elemento web en el menú.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Captura de pantalla que muestra SPFx workbench que se ejecuta con el elemento emergente para agregar una selección de elemento web.":::

   La aplicación debería estar ejecutándose.  Puede realizar actividades de depuración normales como si se tratase de otras SPFx webpart (como establecer puntos de interrupción).

   > [!TIP]
   > Intente colocar puntos de interrupción en el método de representación `SPFx/src/webparts/{webpart}/{webpart}.ts` y volver a cargar la ventana del explorador. VS Code se detendrá en puntos de interrupción en el código.

## <a name="deploy-your-app-to-sharepoint"></a>Implementar la aplicación en SharePoint

Asegúrate de que SharePoint catálogo de aplicaciones existe en la implementación.  Si no existe, [cree uno](/sharepoint/use-app-catalog).  El catálogo de aplicaciones puede tardar hasta 15 minutos en crearse completamente.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abrir Visual Studio Code.
1. Seleccione el Teams Toolkit de la barra lateral seleccionando el Teams.
1. Seleccione **Aprovisionar en la nube**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Captura de pantalla que muestra los comandos de aprovisionamiento":::

   Puede supervisar el progreso viendo los cuadros de diálogo en la esquina inferior derecha.  Después de unos segundos, verá el siguiente aviso:

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo completado de aprovisionamiento.":::

1. Una vez completado el aprovisionamiento, seleccione **Implementar en la nube.**

1. Actualmente, la implementación automatizada no está disponible.  Aparecerá un cuadro de diálogo que le pedirá que cree e implemente manualmente. Seleccione **Compilar SharePoint paquete**.

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

   1. Abra `https://admin.microsoft.com/AdminPortal/Home` .
   1. En **Centros de administración,** seleccione el **SharePoint** de administración.
   1. Selecciona **Más características en** el menú de la barra lateral.
   1. Presione **Abrir en** **Aplicaciones**.
   1. Seleccione **Catálogo de aplicaciones**.

1. Selecciona **Distribuir aplicaciones para SharePoint**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Distribuir aplicaciones para SharePoint.":::

1. Seleccione **Upload**.

1. Seleccione **Elegir archivo**.

1. Busque el `{project}.sppkg` archivo en la carpeta dentro del `SPFx/sharepoint/solution` proyecto. Seleccione **Abrir**.

1. Seleccione **Aceptar**.

1. El SharePoint de implementación se iniciará automáticamente. Compruebe que **esta solución esté disponible para todos los sitios de la** organización. A continuación, **seleccione Implementar**.

1. Seleccione la **pestaña** ARCHIVOS.

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Seleccione la pestaña archivos en el catálogo SharePoint de aplicaciones.":::

1. seleccione el paquete que implementó y, a **continuación, seleccione Sincronizar para Teams** desde la esquina superior derecha.

    > [!Note]
    > El proceso de sincronización Teams puede tardar un par de minutos.  Verás un mensaje en el lado derecho del explorador que indica que la aplicación se ha sincronizado correctamente con Teams.

   Abra la Teams (o inicie sesión en `https://teams.microsoft.com` ).  Presione el triple punto en la barra lateral y, a continuación, **seleccione Todas las aplicaciones**.  La aplicación se colocará en las **aplicaciones creadas para tu categoría de** organización.  Puedes agregar la aplicación desde allí.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Captura de pantalla que muestra la aplicación en Teams":::

## <a name="see-also"></a>Vea también

* [Introducción a tutoriales](code-samples.md)
* [Crear una aplicación de bots de conversación](first-app-bot.md)
* [Crear una extensión de mensajería](first-message-extension.md)
* [Muestras de código](https://github.com/OfficeDev/Microsoft-Teams-Samples)
