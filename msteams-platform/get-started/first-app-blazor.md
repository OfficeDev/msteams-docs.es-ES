---
title: 'Introducción: crea la primera aplicación Teams con Blazor'
author: adrianhall
description: Cree rápidamente una aplicación de Microsoft Teams en la que se muestre un mensaje de "Hola a todos" con el Microsoft Teams Toolkit y .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: c14f55d014af120cab88044d31ee8600017e3c57
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254310"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a>Crear y ejecutar la primera aplicación Microsoft Teams con Blazor

En este tutorial, aprenderás a crear una nueva aplicación Microsoft Teams en .NET/Blazor que implemente una aplicación personal sencilla para extraer información de microsoft Graph. Por ejemplo, una *aplicación personal incluye* un conjunto de pestañas para uso individual. Durante el tutorial, aprenderás sobre la estructura de una aplicación Teams, cómo ejecutar una aplicación localmente y cómo implementar la aplicación en Azure.

La aplicación que se crea muestra información básica del usuario para el usuario actual.  Cuando se conceda permiso, la aplicación se conectará a Microsoft Graph como el usuario actual para obtener el perfil completo.

## <a name="before-you-begin"></a>Antes de empezar

Asegúrese de que el entorno de desarrollo está configurado instalando los requisitos previos.

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)

## <a name="create-your-project"></a>Crear un proyecto

Use el Kit de herramientas de Teams para crear su primer proyecto:

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

1. Abra Visual Studio 2019.

1. Seleccione **Crear un nuevo proyecto**.

1. Selecciona **Microsoft Teams app y,** a continuación, **selecciona Siguiente**.  Para ayudarle a encontrar la plantilla, use el tipo de **proyecto Microsoft Teams**.

1. Escriba un nombre y seleccione **Siguiente**.

1. Escriba el nombre de la aplicación y el nombre de la compañía.

1. Seleccione **Crear**.  El nombre de la aplicación y el nombre de la compañía se muestran a los usuarios finales. La aplicación Teams se creará en unos segundos.  Después de crear el proyecto, configure el inicio de sesión único con M365:

   1. Seleccione **Project**  >  **Configuración de TeamsFx** para  >  **SSO...**.
   1. Cuando se le pida, inicie sesión en su cuenta de administrador de M365.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

1. Abra un terminal y seleccione el directorio donde desea crear el proyecto.

1. Ejecute `dotnet new -i` para instalar la plantilla desde NuGet:

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   Solo tiene que hacerlo la primera vez o al actualizar la plantilla. Compruebe [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) la versión más reciente de este paquete.

1. Crear un directorio:

   ``` bash
   mkdir helloworld
   ```

1. Ejecute `dotnet new` para crear un nuevo proyecto:

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. Después de scaffolding, configure el proyecto para Teams implementación:

   ``` bash
   teamsfx init
   ```

   Ahora puede abrir la solución en Visual Studio para la depuración.

---

## <a name="take-a-tour-of-the-source-code"></a>Dar un paseo por el código fuente

Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).

Después de Teams Toolkit configurar el proyecto, tienes los componentes para crear una aplicación personal básica para Teams. Los directorios y archivos del proyecto se muestran en el área Explorador de soluciones de Visual Studio 2019.

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio 2019.":::

- Los iconos de aplicación se almacenan como archivos PNG en `color.png` y `outline.png`.
- El manifiesto de la aplicación para publicar a través del Portal de desarrolladores para Teams se almacena en `Properties/manifest.json` .
- Se proporciona un controlador back-end `Controllers/BackendController.cs` para ayudar con la autenticación.

Desde que creaste una aplicación de pestaña durante la instalación, Teams Toolkit scaffolding todo el código necesario para una pestaña básica como [un servidor de Blazor](/aspnet/core/blazor).

- `Pages/Tab.razor` es el punto de entrada de la aplicación front-end.
- `TeamsFx.cs`y `JS/src/index.js` se usa para inicializar las comunicaciones con el Teams host.

Puede agregar funcionalidad back-end agregando controladores ASP.NET Core adicionales a la aplicación.

## <a name="run-your-app-locally"></a>Ejecutar la aplicación localmente

El Kit de herramientas de Teams le permite ejecutar la aplicación localmente.  Se compone de varias partes que son necesarias para proporcionar la infraestructura correcta que espera Teams:

- Una aplicación se registra con Azure Active Directory.  Esta aplicación tiene permisos asociados a la ubicación desde la que se carga la aplicación y a cualquier recurso del back-end al que accede.
- Una API web se hospeda (a través de IIS Express) para ayudar con las tareas de autenticación, actuando como proxy entre la aplicación y Azure Active Directory.  
- Se genera un manifiesto de aplicación y existe en el Portal de desarrolladores para Teams.  Teams usa el manifiesto de la aplicación para decir a los clientes conectados desde dónde cargar la aplicación.

Una vez hecho esto, la aplicación se puede cargar en el Teams cliente.  Usamos el cliente web de Teams para poder ver el código HTML, CSS y JavaScript en un entorno de desarrollo web estándar.

Para crear y ejecutar la aplicación localmente:


1. Desde Visual Studio Code, presione la **tecla F5** para ejecutar la aplicación en modo de depuración.


1. Si se solicita, instale el certificado SSL autofirmado para la depuración local.

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. Se cargará Teams en un explorador web y se le pedirá que inicie sesión. Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador. Inicie sesión con su cuenta de M365.

1. Cuando se le pida que instale la aplicación en Teams, seleccione **Agregar**.

   Ahora se mostrará su aplicación:

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Captura de pantalla de la aplicación completada":::

   Puede realizar las actividades de depuración como si se tratase de cualquier otra aplicación web, como establecer puntos de interrupción. La aplicación es compatible con "hot reloading".  Si cambia cualquier archivo dentro del proyecto, la página se volverá a cargar.

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</summary>

Al presionar la tecla **F5,** el Teams Toolkit:

1. Registra la aplicación con Azure Active Directory.
1. Registra la aplicación para la "carga lateral" en Microsoft Teams.
1. Inicia el back-end de la aplicación ejecutándose localmente.
1. Inicia la aplicación front-end hospedada localmente.
1. Inicia Microsoft Teams en un explorador web con un comando para indicar a Teams que cargue de lado la aplicación (la dirección URL está registrada dentro del manifiesto de la aplicación).

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</summary>

Para ejecutar correctamente la aplicación en Teams, debes tener una cuenta de desarrollo Microsoft 365 que permita la carga del lado de la aplicación. Para obtener más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).

</details>

## <a name="deploy-your-app-to-azure"></a>Implementar la aplicación en Azure

La implementación consta de dos pasos: 

1. Se crean los recursos en la nube necesarios. Esto también se conoce como aprovisionamiento.
1. Inicia la codificación y copia la aplicación en los recursos de nube creados.

> **Vista previa**
>
> La compatibilidad con aplicaciones de Blazor es nueva en Teams Toolkit.  El aprovisionamiento y la implementación se realizan con una combinación de Visual Studio 2019 y el Portal de desarrolladores para Teams.

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a>Aprovisionar e implementar la aplicación en Azure App Service

1. En el Explorador de soluciones, haga clic con el botón secundario en el nodo del proyecto y seleccione **Publicar**. También puede usar el elemento **de menú Generar**  >  **publicación.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Seleccione la operación Publicar en el proyecto":::

1. En la **ventana Publicar,** **seleccione Azure** y selct **Next**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Seleccionar Azure como destino de publicación":::

1. Seleccione **Azure App Service (Windows)** y seleccione **Siguiente**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Seleccione Azure App Service como destino de publicación":::

1. Seleccione **+** esta opción para crear una nueva instancia de App Service.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Cree una nueva instancia.":::

1. En el cuadro de diálogo Crear servicio de **aplicaciones (Windows),** se rellenan los campos de entrada **Nombre,** **Nombre** de **suscripción,** Grupo de recursos y **Plan** de hospedaje. Si ya tienes un App Service en ejecución, se selecciona la configuración existente.  Puede optar por crear un nuevo grupo de recursos y un plan de hospedaje.  Cuando esté listo, seleccione **Crear**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Seleccionar plan de hospedaje y suscripción":::

1. En el **cuadro de** diálogo Publicar, la instancia recién creada se ha seleccionado automáticamente.  Cuando esté listo, seleccione **Finalizar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Seleccione la nueva instancia.":::

1. Seleccione el **icono Editar** (lápiz) junto al **Modo de** implementación y seleccione **Autocontenido**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Seleccione modo de implementación independiente.":::

1. Seleccione **Publicar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Publicar la aplicación en el servicio de aplicaciones":::

   Visual Studio implementa la aplicación en Azure App Service y la aplicación web se carga en el explorador.  Agregue `/tab` al final de la dirección URL para ver la página.

   El panel **Publicar de propiedades** del proyecto muestra la dirección URL del sitio y otros detalles. Anote la dirección URL del sitio.

## <a name="create-an-environment-for-your-app"></a>Crear un entorno para la aplicación

El Portal para desarrolladores para Teams administra desde dónde se cargan las pestañas de la aplicación con un **entorno**.  

**Para crear un entorno:**

1. Abra el [Portal de desarrolladores para Teams](https://dev.teams.microsoft.com).  Inicie sesión con su cuenta administrativa M365.

1. En la barra lateral, selecciona **Aplicaciones**.

1. Si solo tienes una aplicación, se seleccionará automáticamente.  Si no es así, selecciona la aplicación de la lista.

1. Seleccione **Entornos**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Seleccionar entornos":::

1. Seleccione **Crear el primer entorno**.

1. Escriba un nombre para el entorno y seleccione **Agregar**. Por ejemplo, `_Production_`.

1. Seleccione **Crear la primera variable de entorno**.

1. Escriba `azure_app_url` para el **nombre**.  Escriba la dirección URL del sitio de Azure sin `https://` el valor **.**

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Crear variable de entorno":::

   Presione **Agregar**.

## <a name="update-the-app-manifest"></a>Actualizar el manifiesto de la aplicación

El manifiesto de la aplicación carga la pestaña desde una `localhost` dirección URL.  En esta sección, configurará el manifiesto de la aplicación para cargar la pestaña desde la dirección URL que aparece en el entorno que acaba de crear.

1. En la barra lateral, seleccione **Información básica**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Seleccionar información básica":::

1. Hay varios lugares dentro del manifiesto que enumera una `locahost:XXXXX` como parte de una dirección URL.  Reemplace todas las repeticiones por `{{azure_app_url}}` , incluidas las llaves.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Ajustar la información básica del entorno":::

1. Cuando haya finalizado, seleccione **Guardar**.

1. En la barra lateral, seleccione **Funcionalidades**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Seleccionar funcionalidades":::

1. Seleccione **Ficha Personal**.
1. Junto a la **pestaña Personal**, seleccione los puntos triples y, a continuación, **seleccione Editar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Editar la configuración de pestañas personales":::

1. Reemplace la dirección URL por la variable de entorno dentro de los campos **Dirección URL de contenido** y Dirección URL **del** sitio web.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Editar direcciones URL de pestañas personales":::

1. Seleccione **Actualizar**.

1. Seleccione **Guardar**.

1. En la barra lateral, seleccione **Inicio de sesión único**.

1. Reemplace el `localhost` URI de **id. de aplicación por** `{{azure_app_url}}` .

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Editar URI de id. de aplicación de inicio de sesión único":::

1. Seleccione **Guardar**.

1. En la barra lateral, seleccione **Dominios**.

1. Seleccione **Agregar un dominio**.

1. Si `{{azure_app_url}}` no aparece como un dominio válido, agréelo como un dominio válido y, a continuación, seleccione **Agregar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Agregar un dominio":::

   Ahora puedes usar la opción Vista previa **en Teams** en la parte superior de la página para iniciar la aplicación en Teams.

## <a name="see-also"></a>Vea también

* [Introducción a tutoriales](code-samples.md)
* [Crear una aplicación de bots de conversación](first-app-bot.md)
* [Crear una extensión de mensajería](first-message-extension.md)
* [Muestras de código](https://github.com/OfficeDev/Microsoft-Teams-Samples)
