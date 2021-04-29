---
title: 'Introducción: compilación y ejecución de la primera aplicación'
author: girliemac
description: Crea rápidamente una aplicación de Microsoft Teams que muestre un "¡Hola, mundo!" con Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068804"
---
# <a name="create-your-first-microsoft-teams-app"></a>Crear la primera aplicación de Microsoft Teams

Esta guía de inicio rápido te enseña a crear y ejecutar la aplicación de Microsoft Teams que muestra "Hello, World!"

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar, debe configurar el inquilino de desarrollo de [Teams](#set-up-your-teams-development-tenant) e [instalar las herramientas de desarrollo de Teams.](#install-your-development-tools)

### <a name="set-up-your-teams-development-tenant"></a>Configurar el inquilino de desarrollo de Teams

Un **inquilino** es como un contenedor para una organización. En términos de Teams, un inquilino es donde los usuarios de esa organización chat, comparten archivos y ejecutan reuniones. Como desarrollador, necesita un inquilino para realizar la instalación local y probar las aplicaciones de Teams que está creando.  

# <a name="do-not-have-a-tenant"></a>[No tener un inquilino](#tab/do-not-have-a-tenant)

Puedes obtener una cuenta de prueba gratuita de Teams, que incluye un inquilino que permite la instalación local de aplicaciones, uniéndose al programa para desarrolladores de Microsoft 365. El proceso de registro tarda aproximadamente dos minutos.

**Para obtener un inquilino**

1. Vaya al programa para desarrolladores de [Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Selecciona **Unirse ahora** y sigue las instrucciones en pantalla.
1. En la pantalla de bienvenida, seleccione **Configurar suscripción E5**.
1. Configura tu cuenta de desarrollador de Microsoft 365. 
   Después de finalizar, aparecerá la siguiente pantalla:

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa para desarrolladores de Microsoft 365.":::

1. Inicie sesión en Teams con su nueva cuenta.
1. En el cliente de Teams, seleccione **Aplicaciones**.
1. Comprueba que puedes ver la opción **Cargar una aplicación** personalizada. Si lo haces, esto significa que puedes realizar la instalación local de aplicaciones.

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde se puede cargar una aplicación personalizada en Teams.":::

# <a name="have-a-tenant"></a>[Tener un inquilino](#tab/have-a-tenant)

Si ya tienes un inquilino, comprueba si puedes realizar la instalación local de aplicaciones en Teams.

**Comprobar que puedes realizar la instalación local de las aplicaciones** 

1. En el cliente de Teams, seleccione **Aplicaciones**. 
1.  Comprueba que puedes ver la opción **Cargar una aplicación** personalizada. Si lo haces, esto significa que puedes realizar la instalación local de aplicaciones. 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde se puede cargar una aplicación personalizada en Teams.":::

---

### <a name="install-your-development-tools"></a>Instalar las herramientas de desarrollo

Para crear esta aplicación, usarás teams Toolkit for Visual Studio Code para empezar rápidamente. También puedes crear aplicaciones de Teams con cualquiera de tus herramientas predefinidas. 

> [!NOTE]
> Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS. Para depurar ciertos tipos de aplicaciones localmente, como un bot, aprenderás a usar ngrok para configurar un túnel seguro entre Teams y tu aplicación.
> 
> Las aplicaciones de Production Teams se hospedan en la nube.

**Para instalar herramientas de Microsoft Teams**

1. Instale [Node.js](https://nodejs.org/en/).
1. Si planea crear un bot o una extensión de mensajería, instale [ngrok](https://ngrok.com/download) y exponga el localhost a [Internet con ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).
1. Instale la versión más reciente [de Visual Studio Code](https://code.visualstudio.com/download). 
   
   > [!NOTE]
   > El kit de herramientas no admite versiones anteriores de Visual Studio Code.

1. En la barra de actividad izquierda, seleccione **Extensiones** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: .
1. En **Microsoft Teams Toolkit,** seleccione **Instalar**.

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración que muestra dónde en Visual Studio código puede instalar la extensión microsoft Teams Toolkit.":::

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

1. Abra Visual Studio código.
1. Selecciona **Microsoft Teams Toolkit** Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Teams**.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Captura de pantalla que muestra cómo crear el proyecto de la aplicación con Visual Studio Kit de herramientas de Code Teams.":::
   
1. Inicie sesión con su cuenta de desarrollo de Microsoft 365. Ya sea la que acaba de crear o la cuenta que ya tenía que permite la instalación local de aplicaciones.
1. En la **pantalla Seleccionar proyecto,** vaya a **Aplicación personal** y seleccione **JS** (JavaScript) > **Siguiente**.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de la aplicación con Visual Studio Code Teams Toolkit.":::

1. Escribe un nombre para la aplicación de Teams.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Captura de pantalla que muestra cómo agregar un nombre al proyecto de la aplicación con Visual Studio Kit de herramientas de Code Teams.":::

1. Seleccione **Finalizar**. 
   El proyecto ya está configurado. 

## <a name="2-understand-your-app-project-components"></a>2. Comprender los componentes del proyecto de la aplicación

Una vez que el kit de herramientas configura el proyecto de la aplicación, tienes los componentes para crear tu "Hello, World!" Aplicación de Teams. Los directorios y archivos del proyecto se encuentran en el Explorador Visual Studio código. 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Captura de pantalla que muestra el scaffolding en el proyecto de la aplicación con Visual Studio Code Teams Toolkit.":::

El kit de herramientas crea automáticamente scaffolding de aplicaciones en el directorio en función de `src` las capacidades que agregó durante la instalación. Desde que creaste una pestaña durante la instalación, el archivo del directorio controla la inicialización `App.js` y el enrutamiento de la `src/components` aplicación. El archivo también llama al SDK de cliente de JavaScript de Microsoft Teams para establecer la comunicación entre la aplicación y Teams. 

## <a name="3-build-and-run-your-app"></a>3. Crear y ejecutar la aplicación

Compila y ejecuta la aplicación localmente para ahorrar tiempo. 

**Para compilar y ejecutar la aplicación**

1. En Visual Studio, seleccione **Ver**  >  **terminal**.
1. Ejecute `npm install` .
1. Ejecute `npm start` .
  
  Un **compilado correctamente.** mensaje aparece en el terminal. La aplicación se está ejecutando en el localhost en `https://localhost:3000` . 

## <a name="4-sideload-your-app-in-teams"></a>4. Instalación local de la aplicación en Teams

La instalación local es el proceso de instalación de una aplicación en Teams que no ha sido aprobada por el administrador o Microsoft. La instalación local es común al probar y depurar aplicaciones de Teams.

De forma predeterminada, Teams no permite la instalación local de aplicaciones. Puedes cambiar esta configuración en el Centro de administración de Teams.

**Para habilitar la instalación local de aplicaciones en Teams**

1. Inicie sesión en el [Centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.  
1. Seleccione **Mostrar todos los**  >  **equipos**. 

   ![imagen del menú del Centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > La opción **Teams** puede tardar hasta 24 horas en aparecer. 

1. Ve a **Directivas de instalación de aplicaciones** de Teams  >    >  **Global** (configuración predeterminada para toda la organización).

   ![Activar la vista de instalación local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. Activa la **alternancia cargar aplicaciones personalizadas.**

1. Seleccione **Guardar** para guardar los cambios.

   El inquilino de prueba ahora permite la instalación local de aplicaciones personalizadas.

   > [!Note]
   > Comprueba si hay problemas antes de descargar localmente la aplicación con la característica de validación de App Studio, que se incluye en el kit de herramientas. Se corrigen los errores para que la aplicación se desacargue correctamente.


### <a name="sideload-your-app"></a>Instalación local de la aplicación

1. En Visual Studio, abra el Kit de herramientas de Teams.
1. Vaya a **App Studio**.  
1. Seleccione **Probar y distribuir**  >  **instalar**.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Captura de pantalla que muestra cómo descargar localmente la aplicación en el cliente de Teams con Visual Studio Code Teams Toolkit.":::

**Como alternativa**

1. Seleccione la **tecla F5** para abrir la ventana del explorador que desea instalar. Esto omitirá el proceso de instalación en **App Studio** y lajerá Teams en el explorador.
1. En el cuadro de diálogo de instalación, selecciona **Agregar** para instalar la aplicación en Teams.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="Captura de pantalla que muestra cómo descargar localmente la aplicación en el cliente de Teams.":::

   > [!Note]
   > App Studio también está disponible como una aplicación independiente para el cliente de Teams.

### <a name="troubleshoot-sideloading-issues"></a>Solucionar problemas de instalación local

**Error en la instalación**

Si aparece el mensaje de error al instalar la aplicación, comprueba que la información de `Manifest parsing has failed` la aplicación se ha escrito correctamente.

**Para comprobar la información de la aplicación**

* En Teams Toolkit, ve a Detalles de **App Studio** App y comprueba que toda la información  >   necesaria se haya escrito correctamente.
*  Si editó manualmente el archivo, compruebe que el JSON está bien definido en la herramienta Manifiesto de la aplicación `manifest.json` en App Studio. 

**Contenido de tabulación no mostrado**

Comprueba que la aplicación se está ejecutando. Si no es así, vaya al terminal y ejecute `npm start` .

## <a name="see-also"></a>Consulte también

* [Preparar el espacio empresarial de Microsoft 365](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [Elegir una configuración para probar y depurar la aplicación de Microsoft Teams](../concepts/build-and-test/debug.md)
* [Creación de pestañas y otras experiencias hospedadas con el SDK de cliente de JavaScript de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md)
* [Preparar el envío de AppSource](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Desarrolle aplicaciones rápidamente con App Studio para Microsoft Teams](../concepts/build-and-test/app-studio-overview.md)
* [Crear una pestaña de canal](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una pestaña personal para Microsoft Teams](../build-your-first-app/build-personal-tab.md)
