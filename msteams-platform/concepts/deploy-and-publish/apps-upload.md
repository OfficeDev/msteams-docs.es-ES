---
title: Cargar la aplicación personalizada en Microsoft Teams
description: Describe cómo cargar la aplicación en Microsoft Teams.
keywords: Carga de aplicaciones de Microsoft Teams
ms.openlocfilehash: c130ef48d3ad7476de9ca5afeb7b613197c43f18
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2020
ms.locfileid: "45103029"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>Cargar un paquete de aplicación en Microsoft Teams

Para probar la experiencia de la aplicación en Microsoft Teams, debe cargar la aplicación en Teams. La carga agrega la aplicación al equipo que seleccione, y usted y los miembros del equipo pueden interactuar con ella como los usuarios finales.

> [!NOTE]
> Cargar un paquete actualizado para una aplicación existente con un bot no puede mostrar cambios de ficha cuando se muestra en la ventana conversaciones. Es mejor acceder a él a través de la volar con las aplicaciones o probar en un entorno de prueba limpio.

## <a name="create-your-upload-package"></a>Crear el paquete de carga

Para el envío de AppSource (anteriormente tienda Office), debe crear un paquete que se pueda cargar y que contenga la información que describe su experiencia. El paquete, un archivo. zip, contiene el manifiesto de aplicación y los iconos que definen su experiencia de forma exclusiva.

Para crear un paquete de carga, consulte [Create the Package for your Microsoft Teams App](../build-and-test/apps-package.md).

Una vez creado el paquete, ahora puede cargarlo en un equipo. Una vez cargada, estará disponible para todos los usuarios del equipo seleccionado y solo para los usuarios de ese equipo.

## <a name="load-your-package-into-teams"></a>Cargar el paquete en Teams

Puede probar el paquete al cargarlo en Teams.

> [!NOTE]
> Para que funcione la carga, el administrador de espacios empresariales debe [Habilitar primero la carga de aplicaciones](/microsoftteams/admin-settings).

Hay dos formas de cargar la aplicación a Microsoft Teams:

* Uso de la tienda
* Uso de la pestaña apps

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>Cargar el paquete en un equipo o conversación mediante la tienda

1. En la esquina inferior izquierda de Microsoft Teams, elija el icono de tienda. En la página tienda, elija "cargar una aplicación personalizada".

   ![Ver equipo](../../assets/images/store-upload-a-custom-app.png)

2. En el cuadro de diálogo *abrir* , navegue hasta el paquete que desea cargar y elija *abrir*.

El paquete cargado ahora debería estar disponible para su uso en el equipo o la conversación especificados en el cuadro de diálogo de consentimiento. Si la aplicación no aparece, la causa más común es un error en el manifiesto, especialmente identificadores para las extensiones de aplicación, Bot y mensajería. Si la aplicación no tiene el ámbito de las conversaciones, esa opción no aparecerá.

>[!NOTE]
> Aplicaciones en conversaciones se encuentra actualmente en [versión preliminar para desarrolladores](../../resources/dev-preview/developer-preview-intro.md)y la opción no aparecerá si Teams no se está ejecutando en ese modo.

![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>Cargar el paquete en un equipo mediante la pestaña aplicaciones

1. En el equipo de destino, elija *más opciones* (**&#8943;**) y elija *administrar equipo*.

   > [!NOTE]
   > Debe ser el propietario del equipo o el propietario debe permitir que los usuarios agreguen los tipos de aplicación adecuados para que aparezca esta funcionalidad.

2. Seleccione la pestaña Aplicaciones y, a continuación, elija *cargar una aplicación personalizada* en la esquina inferior derecha.

   ![Cargar punto de entrada](../../assets/images/UploadACustomApp.png)

3. Busca y selecciona el paquete. zip del equipo.

4. Tras una breve pausa, verá la aplicación cargada en la lista.

   ![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

Si la aplicación no se carga, la causa más común es un error en el manifiesto, especialmente identificadores para las extensiones de aplicación, Bot y mensajería.

## <a name="accessing-your-uploaded-configurable-tab"></a>Acceso a la pestaña configurable cargada

Si la aplicación contiene pestañas, los usuarios pueden anclarlos a cualquier canal de conversación o equipo mediante el flujo de la galería de pestañas estándar:

1. Vaya a un canal del equipo. Elija *+* (*Agregar una pestaña*) a la derecha de las pestañas existentes.

2. Seleccione su pestaña en la galería que aparece.

3. Acepte la solicitud de consentimiento.

4. Configure su pestaña mediante su [Página de configuración](../../tabs/how-to/create-tab-pages/configuration-page.md) y elija *Guardar*.

  ![El cuadro de diálogo Agregar una pestaña, que incluye una galería de pestañas disponibles](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a>Acceso a su bot cargado

Cuando se agrega un bot a un equipo, el usuario debe usarlo en ese equipo, dentro y fuera de los canales del equipo, según la definición del ámbito de los robots. Usted y otros miembros del equipo verán una publicación en el canal general que indica que el bot se ha agregado al equipo.

Para un bot habilitado para Teams, puede empezar invocando el bot @mentioning el nombre del bot, que debe Autocompletar.

Para probar chats directos con el bot, puede tener acceso a él a través de la Página principal de la aplicación, @mention en un canal o buscarlo en la nueva ventana de **chat** .

Cuando se agrega un bot a una conversación para probar chats directos con el bot, se puede @mention en una conversación o buscar en la nueva ventana de **chat** .

## <a name="accessing-your-uploaded-connector"></a>Obtener acceso al conector cargado

Con la aplicación cargada en el equipo o la conversación, los usuarios pueden configurar un conector mediante el flujo de la galería de conectores estándar:

1. Vaya a un canal del equipo. Elija *más opciones* (*&#8943;*) y elija *conectores*.

2. Seleccione el conector de la sección **transferidas localmente** en la parte inferior.

3. Configure el conector mediante su [Página de configuración](../../webhooks-and-connectors/how-to/connectors-creating.md) y elija *Guardar*.

  ![El cuadro de diálogo Agregar una pestaña, que incluye una galería de pestañas disponibles.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a>Obtener acceso a la extensión de mensajería cargada

Una aplicación cargada con una extensión de mensajería aparece automáticamente en el menú *más opciones* (*&#8943;*) en el cuadro de redacción.

![Extensiones de mensajería](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a>Quitar o actualizar la aplicación

Si quiere quitar la aplicación, seleccione el icono de papelera que aparece junto al nombre de la aplicación en la lista Ver bots de Microsoft Teams.

Si cambia la información del manifiesto, primero debe quitar la aplicación y, a continuación, agregar el paquete actualizado (por [cargar el paquete en un equipo](#load-your-package-into-teams)). Tenga en cuenta que, en general, los cambios de código en el servicio no requieren que vuelva a cargar el manifiesto, a menos que estos cambios requieran actualizaciones del manifiesto (como cambios en la dirección URL o el identificador de aplicación de Microsoft para su bot).

> [!NOTE]
> No hay ninguna forma de quitar por completo un bot del contexto personal. Si se quita y vuelve a agregar el bot, la comunicación adicional con el bot se agregará a la conversación anterior.

## <a name="troubleshooting-notes"></a>Notas de solución de problemas

* Si el manifiesto no se carga, compruebe que ha seguido todas las instrucciones de [Create the package](../../concepts/build-and-test/apps-package.md) y validad The manifest en el [esquema](../../resources/schema/manifest-schema.md).

