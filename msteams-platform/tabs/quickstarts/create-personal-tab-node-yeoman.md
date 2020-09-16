---
title: 'Inicio rápido: crear una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams'
author: laujan
description: Una guía de inicio rápido para crear una pestaña personal con el generador de Yeoman para Microsoft Teams.
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: e39878d117b0b1b1f8c0e2450021d9238f5b7877
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818888"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Inicio rápido: crear una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams

>[!NOTE]
>En este tutorial, se siguen los pasos descritos en el sitio de creación de la [primera aplicación Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) wiki que se encuentra en el repositorio de github de Microsoft.

En este tutorial rápido, vamos a crear una pestaña personal personalizada mediante el [generador Yeoman de Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App). También cargaremos la aplicación en el equipo.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**¿Desea crear una pestaña configurable o una etiqueta estática?**

Use las teclas de dirección para seleccionar la pestaña estática.

>[!IMPORTANT]
>El componente de ruta de *yourDefaultTabNameTab*, al que se hace referencia en este tutorial rápido, es el valor que escribió en el generador para el nombre de la *pestaña predeterminada* más la *pestaña*de Word.
>
>Por ejemplo: DefaultTabName: *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>Crear una pestaña personal

Para agregar una pestaña personal a esta aplicación, deberá crear una página de contenido y actualizar los archivos existentes:

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

- Guarde **personal.html** en la carpeta **Web** de la aplicación:

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- Abra **manifest.js** en el editor de código:

```bash
./src/manifest/manifest.json/
```

Agregue lo siguiente a la `staticTabs` matriz vacía ( `staticTabs":[]` ) y agregue el siguiente objeto JSON:

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

Recuerde actualizar el componente de ruta **"contentURL"** **yourDefaultTabNameTab** con el nombre de la pestaña real.

- Guarde el **manifest.jsactualizado en**.

- La página de contenido debe atenderse en un IFrame. Abra la **pestaña. ts** en el editor de código:

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- Agregue lo siguiente a la lista de decoradores IFrame:

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- Asegúrese de guardar el archivo **Tab. ts** actualizado. El código de pestaña está completo.

## <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

Abra un símbolo del sistema en el directorio del proyecto para completar las tareas siguientes.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Para ver tu pestaña personal, ve a `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![captura de pantalla de pestaña personal](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro a la pestaña

Microsoft Teams es un producto basado en la nube completamente y requiere que el contenido de la pestaña esté disponible en la nube con puntos de conexión HTTPS. Teams no permite el hospedaje local, por lo tanto, debe publicar su ficha en una dirección URL pública o usar un proxy que expondrá el puerto local a una dirección URL con conexión a Internet.

Para probar la extensión de pestañas, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación. Ngrok es una herramienta de software de proxy inverso que creará un túnel a los puntos de conexión HTTPS disponibles públicamente del servidor Web que se ejecutan de forma local. Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local. Cuando el equipo se apaga o entra en suspensión, el servicio dejará de estar disponible.

En el símbolo del sistema, salga de localhost y escriba lo siguiente:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Una vez que se haya cargado la pestaña en Microsoft Teams, a través de *ngrok*, y se haya guardado correctamente, podrá verla en Teams hasta que finalice la sesión de túnel.

## <a name="upload-your-application-to-teams"></a>Cargar la aplicación en Teams

- Abra el cliente de Microsoft Teams. Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.
- En el panel de *YourTeams* de la izquierda, seleccione el `...` menú situado junto al equipo que está usando para probar la pestaña y elija **administrar equipo**.
- En el panel principal, seleccione **aplicaciones** en la barra de pestañas y elija **cargar una aplicación personalizada** ubicada en la esquina inferior derecha de la página.
- Abra el directorio del proyecto, vaya a la carpeta **./Package** , seleccione la carpeta ZIP, haga clic con el botón secundario y elija **abrir**. La pestaña se cargará en Teams.

## <a name="view-your-personal-tabs"></a>Ver las pestañas personales

En la barra de exploración situada en el extremo izquierdo del cliente de Microsoft Teams, seleccione el `...` menú y elija la aplicación en la lista.
