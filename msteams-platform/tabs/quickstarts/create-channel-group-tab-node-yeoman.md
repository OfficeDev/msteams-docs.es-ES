---
title: Cree un canal personalizado y agrupalice tabulador con Node.js y el generador Yeoman para Microsoft Teams
author: laujan
description: Una guía de inicio rápido para crear un canal y una pestaña de grupo con el generador Yeoman para Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 559393884e3b8a4aad1787ea4ca8f9f4de54d151
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566651"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Cree una pestaña de canal y grupo personalizada con Node.js y el generador Yeoman para Microsoft Teams

>[!NOTE]
>Esta guía de inicio rápido sigue los pasos descritos en la wiki [de compilación de la primera aplicación Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) que se encuentra en el repositorio de microsoft officedev GitHub.

En esta guía de inicio rápido vamos a caminar a través de la creación de un canal personalizado y la pestaña de grupo utilizando el [generador de Teams Yeoman](https://github.com/OfficeDev/generator-teams/).

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**¿Desea crear una pestaña configurable o estática?**

Utilice las teclas de flecha para seleccionar la pestaña configurable.

**¿Qué ámbitos tiene la intención de usar para su pestaña?**

Puede seleccionar un equipo y/o un chat de grupo

**¿Desea que esta pestaña esté disponible en SharePoint Online? (Y/n)** 

Seleccione **n**.

>[!IMPORTANT]
>El componente de ruta de acceso al que se hace referencia **suDefaultTabNameTab**, al que se hace referencia en esta guía de inicio rápido, es el valor que ha introducido en el generador de **Nombre de tabulación predeterminado** más la **pestaña** Word .
>
>Por ejemplo: DefaultTabName: **MyTab**  =>  **/MyTabTab/**

En el directorio del proyecto, vaya a lo siguiente:

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

Ahí es donde encontrarás la lógica de la pestaña. Busque el `render()` método y agregue la siguiente etiqueta y contenido a la parte superior del código `<div>` `<PanelBody>` contenedor:

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

Asegúrese de guardar el archivo actualizado.

## <a name="build-and-run-your-application"></a>Compile y ejecute su aplicación

Abra un símbolo del sistema en el directorio del proyecto para completar las siguientes tareas.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Para ver la página de configuración de la pestaña vaya a `https://localhost:3007/<yourDefaultAppNameTab>/config.html` . Debería ver lo siguiente:

![captura de pantalla de la página de configuración](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Establezca un túnel seguro a su lengüeta

Microsoft Teams es un producto completamente basado en la nube y requiere que el contenido de la pestaña esté disponible en la nube mediante puntos de conexión HTTPS. Teams no permite el hospedaje local, por lo tanto, debe publicar la pestaña en una dirección URL pública o usar un proxy que expondrá su puerto local a una DIRECCIÓN URL orientada a Internet.

Para probar la extensión de la pestaña, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación. Ngrok es una herramienta de software proxy inverso que creará un túnel para los puntos de conexión HTTPS disponibles públicamente del servidor web. Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local. Cuando la máquina está apagada o se va a dormir, el servicio ya no estará disponible.

En el símbolo del sistema, salga de localhost e introduzca lo siguiente:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Una vez que la pestaña se haya cargado en equipos de Microsoft y se haya guardado correctamente, puede verla en la galería de pestañas, agregarla a la barra de pestañas e interactuar con ella hasta que finalice la sesión del túnel de ngrok. Si reinicias la sesión de ngrok, deberás actualizar la aplicación con la nueva DIRECCIÓN URL.

## <a name="upload-your-application-to-teams"></a>Upload la aplicación para Teams

- Abra el cliente Microsoft Teams. Si utiliza la [versión basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end utilizando las herramientas para [desarrolladores](~/tabs/how-to/developer-tools.md)de su navegador.
- En el panel *Tus comamos de* la izquierda, selecciona el menú situado junto al equipo que `...` usas para probar tu pestaña y selecciona **Administrar equipo.**
- En el panel principal, seleccione **Aplicaciones** en la barra de pestañas y elija **Upload una aplicación personalizada** ubicada en la esquina inferior derecha de la página.
- Abra el directorio del proyecto, vaya a la carpeta **./package,** seleccione la carpeta zip del paquete de la aplicación y elija **Abrir**. La pestaña se cargará en Teams.
- Vuelve a tu equipo, elige el canal donde quieres mostrar la pestaña, selecciona ➕ en la barra de pestañas y elige tu pestaña en la galería.
- Siga las instrucciones para agregar una pestaña. Tenga en cuenta que hay un cuadro de diálogo de configuración personalizado para la pestaña canal/grupo.
- Selecciona **Guardar** y la pestaña se agregará a la barra de pestañas del canal.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Cree una pestaña de canal y grupo personalizado con ASP.NETCore](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)