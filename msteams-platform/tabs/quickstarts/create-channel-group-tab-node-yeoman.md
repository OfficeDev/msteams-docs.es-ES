---
title: Crear un canal personalizado y una pestaña de grupo con Node.js y el generador de Yeoman para Microsoft Teams
author: laujan
description: Guía de inicio rápido para crear una pestaña de canal y grupo con el Generador de Yeoman para Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 70b1dbe5a5abafa44ddbdf9045c55a33cf8fcb20
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630244"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Cree una pestaña de canal y grupo personalizada con Node.js y el generador de Yeoman para Microsoft Teams

>[!NOTE]
>Esta guía de inicio rápido sigue los pasos descritos en el wiki crear la primera [aplicación](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Microsoft Teams que se encuentra en el repositorio GitHub Microsoft OfficeDev.

En esta guía de inicio rápido, crearemos un canal personalizado y una pestaña de grupo con el generador [de Yeoman Teams de Yeoman.](https://github.com/OfficeDev/generator-teams/)

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**¿Desea crear una pestaña configurable o estática?**

Use las teclas de flecha para seleccionar la pestaña configurable.

**¿Qué ámbitos tiene previsto usar para la pestaña?**

Puede seleccionar un equipo o un chat de grupo

**¿Desea que esta pestaña esté disponible en SharePoint Online? (Y/n)** 

Seleccione **n**.

>[!IMPORTANT]
>El componente de ruta de acceso **yourDefaultTabNameTab**, al que se hace referencia en esta guía de inicio rápido, es el valor que escribió en el generador para **Default Tab Name** más la palabra **Tab**.
>
>Por ejemplo: DefaultTabName: **MyTab**  =>  **/MyTabTab/**

En el directorio del proyecto, vaya a lo siguiente:

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

Ahí es donde encontrará la lógica de tabulación. Busque el `render()` método y agregue la siguiente etiqueta y contenido a la parte superior del código `<div>` `<PanelBody>` contenedor:

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

Asegúrese de guardar el archivo actualizado.

## <a name="build-and-run-your-application"></a>Crear y ejecutar la aplicación

Abra un símbolo del sistema en el directorio del proyecto para completar las siguientes tareas.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Para ver la página de configuración de pestañas, vaya a `https://localhost:3007/<yourDefaultAppNameTab>/config.html` . Debería ver lo siguiente:

![captura de pantalla de página de configuración](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

Microsoft Teams es un producto totalmente basado en la nube y requiere que el contenido de la pestaña esté disponible desde la nube mediante puntos de conexión HTTPS. Teams no permite el hospedaje local, por lo tanto, debe publicar la pestaña en una dirección URL pública o usar un proxy que exponga el puerto local a una dirección URL orientada a Internet.

Para probar la extensión de pestaña, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación. Ngrok es una herramienta de software de proxy inverso que creará un túnel para los puntos de conexión HTTPS del servidor web que se ejecuta localmente. Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local. Cuando la máquina se apaga o se queda en modo de suspensión, el servicio ya no estará disponible.

En el símbolo del sistema, salga de localhost y escriba lo siguiente:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Después de cargar la pestaña en Microsoft teams y guardarla correctamente, puede verlo en la galería de pestañas, agregarla a la barra de pestañas e interactuar con ella hasta que finalice la sesión del túnel ngrok. Si reinicias la sesión de ngrok, tendrás que actualizar la aplicación con la nueva dirección URL.

## <a name="upload-your-application-to-teams"></a>Upload la aplicación a Teams

- Abra el Microsoft Teams cliente. Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)
- En el panel *YourTeams* de la izquierda, seleccione el menú situado junto al equipo que está usando para probar la pestaña y `...` elija Administrar **equipo**.
- En el panel principal, selecciona **Aplicaciones** en la barra de pestañas y Upload **una** aplicación personalizada ubicada en la esquina inferior derecha de la página.
- Abra el directorio del proyecto, vaya a **la carpeta ./package,** seleccione la carpeta zip del paquete de la aplicación y elija **Abrir**. La pestaña se cargará en Teams.
- Vuelva a su equipo, elija el canal en el que desea mostrar la pestaña, seleccione ➕ en la barra de pestañas y elija la pestaña de la galería.
- Siga las instrucciones para agregar una pestaña. Tenga en cuenta que hay un cuadro de diálogo de configuración personalizado para la pestaña canal o grupo.
- Selecciona **Guardar** y la pestaña se agregará a la barra de pestañas del canal.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear un canal personalizado y una pestaña de grupo con ASP.NETCore](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)
