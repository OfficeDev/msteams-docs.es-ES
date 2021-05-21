---
title: 'Inicio rápido: cree una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams'
author: laujan
description: Guía de inicio rápido para crear una pestaña personal con el Generador de Yeoman para Microsoft Teams.
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
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Crear una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams

>[!NOTE]
>Esta guía de inicio rápido sigue los pasos descritos en el wiki crear la primera [aplicación](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Microsoft Teams que se encuentra en el repositorio GitHub Microsoft OfficeDev.

En esta guía de inicio rápido crearemos una pestaña personal personalizada con [el generador de Yeoman Teams de Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App). También cargaremos la aplicación en Team.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Crear una pestaña configurable o estática**

Use las teclas de flecha para seleccionar la pestaña estática.

>[!IMPORTANT]
>El componente de ruta de acceso *yourDefaultTabNameTab*, al que se hace referencia en esta guía de inicio rápido, es el valor que escribió en el generador para *Default Tab Name* más la palabra *Tab*.
>
>Por ejemplo: DefaultTabName: *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>Crear la pestaña personal

Para agregar una pestaña personal a esta aplicación, creará una página de contenido y actualizará los archivos existentes:

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

- Guarde **personal.html** en la carpeta web de **la** aplicación:

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- Abra **manifest.jsen** el editor de código:

    ```bash
    ./src/manifest/manifest.json/
    ```

Agregue lo siguiente a la matriz `staticTabs` vacía ( ) y agregue el siguiente objeto `staticTabs":[]` JSON:

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

Recuerde actualizar el componente de ruta **de acceso "contentURL"** **yourDefaultTabNameTab** con el nombre de la pestaña real.

- Guarde el archivo **manifest.jsen**.

- La página de contenido debe servirse en un IFrame. Abra **Tab.ts en** el editor de código:

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- Agregue lo siguiente a la lista de decoradores de IFrame:

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- Asegúrese de guardar el archivo **Tab.ts actualizado.** El código de pestaña se ha completado.

## <a name="build-and-run-your-application"></a>Crear y ejecutar la aplicación

Abra un símbolo del sistema en el directorio del proyecto para completar las siguientes tareas.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Para ver la pestaña personal, vaya a `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![captura de pantalla de pestaña personal](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

Microsoft Teams es un producto totalmente basado en la nube y requiere que el contenido de la pestaña esté disponible desde la nube mediante puntos de conexión HTTPS. Teams no permite el hospedaje local, por lo tanto, debe publicar la pestaña en una dirección URL pública o usar un proxy que exponga el puerto local a una dirección URL orientada a Internet.

Para probar la extensión de pestaña, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación. Ngrok es una herramienta de software de proxy inverso que creará un túnel para los puntos de conexión HTTPS del servidor web que se ejecuta localmente. Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local. Cuando la máquina se apaga o se queda en modo de suspensión, el servicio ya no estará disponible.

En el símbolo del sistema, salga de localhost y escriba lo siguiente:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Después de cargar la pestaña en Microsoft teams, a través de **ngrok** y guardarla correctamente, puede verlo en Teams hasta que finalice la sesión de túnel.

## <a name="upload-your-application-to-teams"></a>Upload la aplicación a Teams

- Abra el Microsoft Teams cliente. Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)
- En el panel **YourTeams** de la izquierda, seleccione el menú situado junto al equipo que está usando para probar la pestaña y `...` elija Administrar **equipo**.
- En el panel principal, selecciona **Aplicaciones** en la barra de pestañas y Upload **una** aplicación personalizada ubicada en la esquina inferior derecha de la página.
- Abra el directorio del proyecto, vaya a **la carpeta ./package,** seleccione la carpeta zip, haga clic con el botón secundario y elija **Abrir**. La pestaña se cargará en Teams.

## <a name="view-your-personal-tabs"></a>Ver las pestañas personales

En la barra de navegación situada en el extremo izquierdo del cliente Teams, seleccione el menú y elija la `...` aplicación de la lista.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una pestaña personal con ASP.NETCore](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
