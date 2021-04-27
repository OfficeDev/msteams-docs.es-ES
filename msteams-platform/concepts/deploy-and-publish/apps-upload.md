---
title: Cargar la aplicación personalizada
description: Describe cómo cargar la aplicación en Microsoft Teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
keywords: carga de aplicaciones de teams
ms.openlocfilehash: 3fa6a3ef00cbb55b5c663891deaabcc908de95d5
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020810"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>Cargar un paquete de aplicación en Microsoft Teams

Para probar la experiencia de la aplicación en Microsoft Teams, debes cargar la aplicación en Teams. La carga agrega la aplicación al equipo seleccionado y todos los miembros del equipo pueden interactuar con ella como usuarios finales.

> [!NOTE]
> Es posible que cargar un paquete actualizado para una aplicación existente con un bot no muestre cambios de pestaña cuando se ve a través de la ventana de conversaciones. Puedes acceder a la aplicación a través de las aplicaciones desvía o prueba en un entorno limpio.

## <a name="create-your-upload-package"></a>Crear el paquete de carga

Para el desarrollo y el envío de AppSource, debe crear un paquete que pueda cargar. El paquete debe contener la información para describir su experiencia. El paquete es un archivo .zip que contiene el manifiesto de la aplicación y los iconos que definen de forma única la experiencia.

Para crear un paquete de carga, consulta [Crear el paquete para la aplicación de Microsoft Teams](../build-and-test/apps-package.md).

Después de crear el paquete, cárbalo en un equipo. El paquete cargado solo está disponible para los usuarios del equipo seleccionado.

## <a name="load-your-package-into-teams"></a>Cargar el paquete en Teams

Para probar el paquete, cárbalo en Teams.

> [!NOTE]
> Para que la carga funcione, el administrador del espacio empresarial debe habilitar primero [la carga de aplicaciones](/microsoftteams/admin-settings).

Hay dos formas de cargar la aplicación en Teams:

* Uso de la Tienda
* Uso de la pestaña Aplicaciones

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>Cargar el paquete en un equipo o conversación con la Tienda

1. En la esquina inferior izquierda de Teams, elija el **icono De** la Tienda. En la página Tienda, elija **Cargar una aplicación personalizada.**

  ![Ver equipo](../../assets/images/store-upload-a-custom-app2.png)

2. En el **cuadro de** diálogo Abrir, vaya al paquete que desea cargar y elija Abrir.

   ![Menú Agregar](../../assets/images/NewappAddmenudropdown.png)

El paquete cargado debe estar disponible para su uso en el equipo o conversación especificado en el cuadro de diálogo de consentimiento. Si la aplicación no aparece, el motivo más común es un error en el manifiesto, en particular los IDs de las extensiones de aplicación, bot y mensajería. Si la aplicación no está en el ámbito de las conversaciones, esa opción no aparece.

>[!NOTE]
> Las aplicaciones en conversaciones se encuentran actualmente en [Developer Preview](../../resources/dev-preview/developer-preview-intro.md)y la opción no aparece si Teams no se ejecuta en ese modo.

![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>Cargar el paquete en un equipo mediante la pestaña Aplicaciones

1. En el equipo de destino, elija **Más opciones** (**&#8943;**) y seleccione **Administrar equipo**.

   > [!NOTE]
   > Debes ser el propietario del equipo o el propietario debe dar acceso a los usuarios para agregar los tipos de aplicación adecuados para que aparezca esta funcionalidad.

2. Selecciona la **pestaña** Aplicaciones y elige **Cargar una aplicación personalizada** en la parte inferior derecha.

   ![Punto de entrada de carga](../../assets/images/UploadACustomApp.png)

3. Seleccione el paquete .zip del equipo.

4. Puedes ver la aplicación cargada en la lista.

   ![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

Si la aplicación no se carga, el motivo más común es un error en el manifiesto, en particular los IDs de las extensiones de aplicación, bot y mensajería.

## <a name="access-your-uploaded-configurable-tab"></a>Acceder a la pestaña configurable cargada

Si la aplicación contiene pestañas, los usuarios pueden anclarlas a cualquier conversación o canal de grupo mediante el flujo de galería de pestañas estándar:

1. Vaya a un canal del equipo. Elija **+** agregar una pestaña a la derecha de las pestañas existentes.

2. Seleccione la pestaña de la galería que aparece.

3. Acepte el símbolo del sistema de consentimiento.

4. Configure la pestaña a través de [su página de configuración](../../tabs/how-to/create-tab-pages/configuration-page.md) y seleccione **Guardar**.

  ![Cuadro de diálogo Agregar una pestaña con una galería de pestañas disponibles](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a>Obtener acceso al bot cargado

Después de agregar el bot a un equipo, debe ser usable por cualquiera de ese equipo, dentro y fuera de los canales del equipo, según la definición del ámbito del bot. Todos los miembros del equipo pueden ver una publicación en el **canal General** que indica que el bot se ha agregado al equipo.

Para un bot de Teams, puede empezar invocando el bot @mentioning el nombre del bot.

Para probar chats directos con el bot, puedes acceder a él a través de la página principal de la aplicación, @mention en un canal o buscarlo en la ventana Nuevo **chat.**

Puedes @mention bot en una conversación o buscarlo en la ventana Nuevo **chat** para probar chats directos con el bot.

## <a name="access-your-uploaded-connector"></a>Obtener acceso al conector cargado

Con la aplicación cargada en el equipo o la conversación, los usuarios pueden configurar un conector con el flujo de galería de conectores estándar:

1. Vaya a un canal del equipo. Elija **Más opciones** (*&#8943;*) y elija **Conectores**.

2. Seleccione el conector en la **sección Sideloaded** en la parte inferior.

3. Configure el conector a través de su [página de configuración](../../webhooks-and-connectors/how-to/connectors-creating.md) y seleccione **Guardar**.

  ![El cuadro de diálogo Agregar una pestaña, con una galería de pestañas disponibles.](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a>Obtener acceso a la extensión de mensajería cargada

Una aplicación cargada con una extensión de mensajería aparece automáticamente en el menú Más **opciones** (*&#8943;*) en el cuadro de redacción.

![Extensiones de mensajería](../../assets/images/compose-extensions/cesampleapp.png)


## <a name="remove-or-update-your-app"></a>Quitar o actualizar la aplicación

Para quitar la aplicación, selecciona el icono eliminar situado junto al nombre de la aplicación en la lista Ver bots de **Teams.** Si cambias la información del manifiesto, primero quitas la aplicación y luego agregas el paquete actualizado, consulta [Cargar el paquete en un equipo](#load-your-package-into-teams). Los cambios de código en el servicio no requieren que vuelva a cargar el manifiesto. Sin embargo, si los cambios de código requieren actualizaciones de manifiesto, como cambios en la dirección URL o el identificador de aplicación de Microsoft para su bot, debes cargar el manifiesto de nuevo.

> [!NOTE]
> No se puede quitar un bot de un contexto personal por completo. Si el bot se quita y se agrega de nuevo, la comunicación adicional con el bot se anexa a la conversación anterior.

## <a name="troubleshooting-notes"></a>Notas de solución de problemas

Si el manifiesto no se carga, compruebe si ha seguido todas las instrucciones de [Crear el](../../concepts/build-and-test/apps-package.md) paquete y validó el manifiesto con el [esquema](../../resources/schema/manifest-schema.md).
