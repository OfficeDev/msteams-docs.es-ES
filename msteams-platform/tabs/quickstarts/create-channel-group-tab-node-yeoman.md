---
title: Crear una ficha de canal y de grupo personalizada con node. js y el generador de Yeoman para Microsoft Teams
author: laujan
description: Una guía de inicio rápido para crear una ficha de canal y de grupo con el generador de Yeoman para Microsoft Teams.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: c5e028dcc117d729f2bf366923d03568b7f557a4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675919"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Crear una ficha de canal y de grupo personalizada con node. js y el generador de Yeoman para Microsoft Teams

>[!NOTE]
>En este tutorial, se siguen los pasos descritos en el sitio de creación de la [primera aplicación Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) wiki que se encuentra en el repositorio de github de Microsoft.

En este tutorial rápido, vamos a crear una pestaña de canal y de grupo personalizados mediante el [generador Yeoman de Teams](https://github.com/OfficeDev/generator-teams/).

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**¿Desea crear una pestaña configurable o una etiqueta estática?**

Use las teclas de dirección para seleccionar la pestaña configurable.

**¿Qué ámbitos desea usar para la pestaña?**

Puede seleccionar un equipo o un chat en grupo

**¿Desea que esta pestaña esté disponible en SharePoint Online? (S/n)** 

Seleccione **n**.

>[!IMPORTANT]
>El componente de ruta de **yourDefaultTabNameTab**, al que se hace referencia en este tutorial rápido, es el valor que escribió en el generador para el nombre de la **pestaña predeterminada** más la **pestaña**de Word.
>
>Por ejemplo: DefaultTabName: **MyTab** => **/MyTabTab/**

En el directorio del proyecto, vaya a lo siguiente:

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

Es aquí donde encontrará la lógica de la pestaña. Busque el `render()` método y agregue la siguiente `<div>` etiqueta y el contenido a la parte superior `<PanelBody>` del código de contenedor:

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

Asegúrese de guardar el archivo actualizado.

## <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

Abra un símbolo del sistema en el directorio del proyecto para completar las tareas siguientes.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Para ver la página de configuración de pestañas, vaya a `https://localhost:3007/<yourDefaultAppNameTab>/config.html`. Debería ver lo siguiente:

![captura de pantalla de la página de configuración](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro a la pestaña

Microsoft Teams es un producto basado en la nube completamente y requiere que el contenido de la pestaña esté disponible en la nube con puntos de conexión HTTPS. Teams no permite el hospedaje local, por lo tanto, debe publicar su ficha en una dirección URL pública o usar un proxy que expondrá el puerto local a una dirección URL con conexión a Internet.

Para probar la extensión de pestañas, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación. Ngrok es una herramienta de software de proxy inverso que creará un túnel a los puntos de conexión HTTPS disponibles públicamente del servidor Web que se ejecutan de forma local. Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local. Cuando el equipo se apaga o entra en suspensión, el servicio dejará de estar disponible.

En el símbolo del sistema, salga de localhost y escriba lo siguiente:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Una vez cargada la pestaña en Microsoft Teams y guardada correctamente, puede verla en la galería de pestañas, agregarla a la barra de pestañas e interactuar con ella hasta que finalice la sesión de túnel ngrok. Si reinicia la sesión de ngrok, tendrá que actualizar la aplicación con la nueva dirección URL.

## <a name="upload-your-application-to-teams"></a>Cargar la aplicación en Teams

- Abra el cliente de Microsoft Teams. Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.
- En el panel de *YourTeams* de la izquierda, seleccione `...` el menú situado junto al equipo que está usando para probar la pestaña y elija **administrar equipo**.
- En el panel principal, seleccione **aplicaciones** en la barra de pestañas y elija **cargar una aplicación personalizada** ubicada en la esquina inferior derecha de la página.
- Abra el directorio del proyecto, vaya a la carpeta **./Package** , seleccione la carpeta ZIP del paquete de la aplicación y elija **abrir**. La pestaña se cargará en Teams.
- Vuelva a su equipo, elija el canal en el que desea mostrar la pestaña, seleccione ➕ de la barra de pestañas y elija la pestaña de la galería.
- Siga las instrucciones para agregar una pestaña. tenga en cuenta que hay un cuadro de diálogo de configuración personalizada para la ficha canal o grupo.
- Seleccione **Guardar** y la pestaña se agregará a la barra de pestañas del canal.
