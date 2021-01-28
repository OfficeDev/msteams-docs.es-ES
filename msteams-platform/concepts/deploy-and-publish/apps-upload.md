---
title: Cargar la aplicación personalizada
description: Describe cómo cargar la aplicación en Microsoft Teams
ms.topic: how-to
keywords: Carga de aplicaciones de teams
ms.openlocfilehash: 2e7a21dc27fdfe824ecacebabbb61a3b99ae8e79
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014344"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>Cargar un paquete de aplicación en Microsoft Teams

Para probar la experiencia de la aplicación en Microsoft Teams, debe cargar la aplicación en Teams. La carga agrega la aplicación al equipo que seleccione y usted y los miembros del equipo pueden interactuar con ella como los usuarios finales.

> [!NOTE]
> Es posible que al cargar un paquete actualizado para una aplicación existente con un bot no se muestren cambios en las pestañas cuando se visualizan a través de la ventana Conversaciones. Es mejor acceder a él a través del control desplegable Aplicaciones o probar en un entorno de prueba limpio.

## <a name="create-your-upload-package"></a>Crear el paquete de carga

Para el desarrollo, así como el envío de AppSource (anteriormente Tienda Office), debe crear un paquete que se pueda cargar que contenga la información para describir su experiencia. El paquete, un archivo .zip, contiene el manifiesto de la aplicación y los iconos que definen de forma única tu experiencia.

Para crear un paquete de carga, [consulte Crear el paquete para su aplicación de Microsoft Teams.](../build-and-test/apps-package.md)

Con el paquete creado, ahora puede cargarlo en un equipo. Una vez cargado, estará disponible para todos los usuarios del equipo seleccionado y solo para los usuarios de ese equipo.

## <a name="load-your-package-into-teams"></a>Cargar el paquete en Teams

Puede probar el paquete carcándoselo en Teams.

> [!NOTE]
> Para que la carga funcione, el administrador del espacio empresarial debe habilitar primero [la carga de aplicaciones.](/microsoftteams/admin-settings)

Hay dos formas de cargar la aplicación en Teams:

* Uso de la Tienda
* Uso de la pestaña Aplicaciones

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>Cargar el paquete en un equipo o conversación con la Tienda

1. En la esquina inferior izquierda de Teams, elija el icono de la Tienda. En la página de la Tienda, elija "Cargar una aplicación personalizada".

  ![Ver equipo](../../assets/images/store-upload-a-custom-app2.png)

2. En el *cuadro de* diálogo Abrir, vaya al paquete que desea cargar y elija *Abrir.*

   ![Menú Agregar](../../assets/images/NewappAddmenudropdown.png)

El paquete cargado ahora debe estar disponible para su uso en el equipo o la conversación especificada en el cuadro de diálogo de consentimiento. Si la aplicación no aparece, la razón más común es un error en el manifiesto, especialmente ids para la aplicación, bot y extensiones de mensajería. Si la aplicación no está en el ámbito de las conversaciones, esa opción no aparecerá.

>[!NOTE]
> Las aplicaciones en conversaciones se encuentran actualmente en [la versión](../../resources/dev-preview/developer-preview-intro.md)preliminar del desarrollador y la opción no aparecerá si Teams no se ejecuta en ese modo.

![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>Cargar el paquete en un equipo mediante la pestaña Aplicaciones

1. En el equipo de destino, elija *Más opciones* (**&#8943;**) y elija *Administrar equipo*.

   > [!NOTE]
   > Debe ser el propietario del equipo o el propietario debe permitir que los usuarios agreguen los tipos de aplicación adecuados para que esta funcionalidad aparezca.

2. Seleccione la pestaña Aplicaciones y, a continuación, *elija Cargar una aplicación personalizada* en la esquina inferior derecha.

   ![Punto de entrada de carga](../../assets/images/UploadACustomApp.png)

3. Busca y selecciona el paquete .zip del equipo.

4. Después de una breve pausa, verás la aplicación cargada en la lista.

   ![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

Si la aplicación no se carga, la razón más común es un error en el manifiesto, especialmente ids para la aplicación, bot y extensiones de mensajería.

## <a name="accessing-your-uploaded-configurable-tab"></a>Acceso a la pestaña configurable cargada

Si la aplicación contiene pestañas, los usuarios pueden anclarlas a cualquier conversación o canal de equipo mediante el flujo estándar de la galería de pestañas:

1. Vaya a un canal del equipo. Elija *+* ( Agregar una pestaña )*a* la derecha de las pestañas existentes.

2. Seleccione la pestaña de la galería que aparece.

3. Acepte la solicitud de consentimiento.

4. Configure la pestaña a través de [su página de configuración](../../tabs/how-to/create-tab-pages/configuration-page.md) y elija *Guardar*.

  ![El cuadro de diálogo Agregar una pestaña, con una galería de pestañas disponibles](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a>Obtener acceso al bot cargado

Cuando agrega un bot a un equipo, debe poderlo usar cualquier persona de ese equipo, dentro y fuera de los canales del equipo, según la definición del ámbito del bot. Usted y otros miembros del equipo verán una publicación en el canal General que indica que el bot se ha agregado al equipo.

Para un bot habilitado para equipos, puede empezar invocando el bot @mentioning nombre del bot, que debería autocompletar.

Para probar chats directos con el bot, puede acceder a él a través de la página principal de la aplicación, @mention en un canal o buscarlo en la ventana De nuevo **chat.**

Al agregar el bot a una conversación Para probar chats directos con el bot, puede @mention en una conversación o buscarlo en la ventana Nuevo **chat.**

## <a name="accessing-your-uploaded-connector"></a>Acceso al conector cargado

Con la aplicación cargada en el equipo o la conversación, los usuarios pueden configurar un conector mediante el flujo estándar de la galería de conectores:

1. Vaya a un canal del equipo. Elija *Más opciones* (*&#8943;*) y elija *Conectores*.

2. Seleccione el conector en la **sección de instalación local** en la parte inferior.

3. Configure el conector a través de [su página de configuración](../../webhooks-and-connectors/how-to/connectors-creating.md) y elija *Guardar*.

  ![El cuadro de diálogo Agregar una pestaña, con una galería de pestañas disponibles.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a>Acceso a la extensión de mensajería cargada

Una aplicación cargada con una extensión de mensajería aparece automáticamente en el menú Más opciones *(* *&#8943;*) en el cuadro de redacción.

![Extensiones de mensajería](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a>Quitar o actualizar la aplicación

Si desea quitar la aplicación, seleccione el icono de papelera junto al nombre de la aplicación en la lista Ver bots de Teams.

Si cambia la información del manifiesto, primero debe quitar la aplicación y, a continuación, agregar el paquete actualizado (por cargar el paquete [en un equipo).](#load-your-package-into-teams) Ten en cuenta que, en general, los cambios de código en el servicio no requieren que vuelvas a cargar el manifiesto, a menos que dichos cambios requieran actualizaciones de manifiesto (como cambios en la dirección URL o el identificador de aplicación de Microsoft para su bot).

> [!NOTE]
> No hay ninguna manera de quitar completamente un bot del contexto personal. Si el bot se quita y se vuelve a agregar, la comunicación adicional con el bot se anexará a la conversación anterior.

## <a name="troubleshooting-notes"></a>Notas de solución de problemas

* Si el manifiesto no se carga, compruebe que ha [](../../concepts/build-and-test/apps-package.md) seguido todas las instrucciones de Crear el paquete y ha validado el manifiesto con el [esquema.](../../resources/schema/manifest-schema.md)
