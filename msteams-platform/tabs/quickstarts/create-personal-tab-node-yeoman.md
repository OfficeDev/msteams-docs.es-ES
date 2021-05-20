---
title: 'Inicio rápido: Crea una pestaña personal personalizada con Node.js y el generador Yeoman para Microsoft Teams'
author: laujan
description: Una guía de inicio rápido para crear una pestaña personal con el generador Yeoman para Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 88ad05aacaed69d695bc918e3e8a44ec18e560ae
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566612"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Cree una pestaña personal personalizada con Node.js y el generador Yeoman para Microsoft Teams

>[!NOTE]
>Esta guía de inicio rápido sigue los pasos descritos en la wiki [de compilación de la primera aplicación Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) que se encuentra en el repositorio de microsoft officedev GitHub.

En esta guía de inicio rápido vamos a caminar a través de la creación de una pestaña personal personalizada utilizando el [generador de Teams Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App). También subiremos la aplicación al equipo.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Crear una pestaña configurable o estática**

Utilice las teclas de flecha para seleccionar la pestaña estática.

>[!IMPORTANT]
>El componente de ruta de acceso al que se hace referencia *suDefaultTabNameTab*, al que se hace referencia en esta guía de inicio rápido, es el valor que ha introducido en el generador de *Nombre de tabulación predeterminado* más la *pestaña* Word .
>
>Por ejemplo: DefaultTabName: *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>Crea tu pestaña personal

Para agregar una pestaña personal a esta aplicación creará una página de contenido y actualizará los archivos existentes:

- En el editor de código, cree un nuevo archivo HTML, **personal.html** y agregue el siguiente marcado:

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

- Guarde **personal.html** en la carpeta **web** de la aplicación:

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- Abramanifest.jsen **el** editor de código:

    ```bash
    ./src/manifest/manifest.json/
    ```

Agregue lo siguiente a la matriz vacía `staticTabs` ( ) y agregue el siguiente objeto `staticTabs":[]` JSON:

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

Recuerde actualizar el componente de ruta de acceso **"contentURL"** **yourDefaultTabNameTab** con su nombre de pestaña real.

- Guarde lamanifest.jsactualizada **en**.

- La página de contenido debe servirse en un IFrame. Abra **Tab.ts** en el editor de código:

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- Agregue lo siguiente a la lista de decoradores de IFrame:

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- Asegúrese de guardar el archivo **Tab.ts** actualizado. El código de la pestaña está completo.

## <a name="build-and-run-your-application"></a>Compile y ejecute su aplicación

Abra un símbolo del sistema en el directorio del proyecto para completar las siguientes tareas.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Para ver tu pestaña personal, ve a `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![captura de pantalla de pestaña personal](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Establezca un túnel seguro a su lengüeta

Microsoft Teams es un producto completamente basado en la nube y requiere que el contenido de la pestaña esté disponible en la nube mediante puntos de conexión HTTPS. Teams no permite el hospedaje local, por lo tanto, debe publicar la pestaña en una dirección URL pública o usar un proxy que expondrá su puerto local a una DIRECCIÓN URL orientada a Internet.

Para probar la extensión de la pestaña, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación. Ngrok es una herramienta de software proxy inverso que creará un túnel para los puntos de conexión HTTPS disponibles públicamente del servidor web. Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local. Cuando la máquina está apagada o se va a dormir, el servicio ya no estará disponible.

En el símbolo del sistema, salga de localhost e introduzca lo siguiente:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Una vez que la pestaña se haya cargado en equipos de Microsoft, a través de **ngrok** y guardada correctamente, puede verla en Teams hasta que finalice la sesión del túnel.

## <a name="upload-your-application-to-teams"></a>Upload la aplicación para Teams

- Abra el cliente Microsoft Teams. Si utiliza la [versión basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end utilizando las herramientas para [desarrolladores](~/tabs/how-to/developer-tools.md)de su navegador.
- En el panel **Tus comamos de** la izquierda, selecciona el menú situado junto al equipo que `...` usas para probar tu pestaña y selecciona **Administrar equipo.**
- En el panel principal, seleccione **Aplicaciones** en la barra de pestañas y elija **Upload una aplicación personalizada** ubicada en la esquina inferior derecha de la página.
- Abra el directorio del proyecto, vaya a la carpeta **./package,** seleccione la carpeta zip, haga clic con el botón derecho y elija **Abrir**. La pestaña se cargará en Teams.

## <a name="view-your-personal-tabs"></a>Ver sus pestañas personales

En la barra de navegación situada a la izquierda del cliente Teams, seleccione el `...` menú y elija la aplicación de la lista.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Cree una pestaña personal con ASP.NETCore](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
