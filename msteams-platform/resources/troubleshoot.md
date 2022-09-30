---
title: Solución de problemas de la aplicación
description: Solución de problemas o errores al compilar aplicaciones para Microsoft Teams
keywords: Solución de problemas de desarrollo de aplicaciones de teams
localization_priority: Normal
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: 0b3f4f7b3a38b6e61b4fbc7e58c5ed5897ed427e
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243475"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Solucionar problemas de la aplicación de Microsoft Teams

## <a name="troubleshooting-tabs"></a>Pestañas de solución de problemas

### <a name="accessing-the-devtools"></a>Acceso a DevTools

Puede abrir [DevTools en el cliente de Teams](~/tabs/how-to/developer-tools.md) para obtener una experiencia similar a presionar F12 (en Windows) o Command-Option-I (en MacOS) en un explorador.

### <a name="blank-tab-screen"></a>Pantalla de tabulación en blanco

Si no ve el contenido en la vista de pestaña, podría ser:

* el contenido no se puede mostrar en un objeto `<iframe>`.
* el dominio de contenido no está en la lista [validDomains](~/resources/schema/manifest-schema.md#validdomains) del manifiesto.

> [!NOTE]
> Aparece una pestaña en blanco cuando la dirección URL de pestaña determinada redirige a la pantalla de inicio de sesión. Las páginas de inicio de sesión no se representan en iFrames como medida de seguridad contra el secuestro de clics. La lógica de autenticación debe usar un método distinto del redireccionamiento.

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>El botón Guardar no está habilitado en el cuadro de diálogo de configuración

Asegúrese de llamar `microsoftTeams.settings.setValidityState(true)` a una vez que el usuario haya introducido o seleccionado todos los datos necesarios en la página de configuración para habilitar el botón guardar.

### <a name="the-tab-settings-cant-be-saved-on-selecting-save"></a>La configuración de la pestaña no se puede guardar al seleccionar Guardar

Al agregar una pestaña, si selecciona **Guardar** pero recibe un mensaje de error que indica que la configuración no se puede guardar, el problema podría ser una de las dos clases de problemas:

* **El mensaje de operación correcta de guardado nunca se recibió**: Si se registró un controlador de guardado mediante `microsoftTeams.settings.registerOnSaveHandler(handler)`, la devolución de llamada debe llamar a `saveEvent.notifySuccess()`.

  * Si la devolución de llamada no llama en `saveEvent.notifySuccess()` 30 segundos o llama `saveEvent.notifyFailure(reason)` en su lugar, se muestra este error.
  * Si no se registró ningún controlador de guardado, la `saveEvent.notifySuccess()` llamada se realiza automáticamente cuando el usuario selecciona **Guardar**.

* **La configuración proporcionada no era válida**: la otra razón por la que la configuración no se puede guardar es si la llamada a `microsoftTeams.setSettings(settings)` proporcionó un objeto de configuración no válido o si la llamada no se realizó en absoluto. Consulte la sección siguiente, Problemas comunes con el objeto settings.

### <a name="common-problems-with-the-settings-object"></a>Problemas comunes con el objeto settings

* `settings.entityId` falta. Este campo es necesario.
* `settings.contentUrl` falta. Este campo es necesario.
* `settings.contentUrl` o el opcional `settings.removeUrl`, o `settings.websiteUrl` se proporcionan pero no son válidos. Las direcciones URL deben usar HTTPS y también deben ser el mismo dominio que la página de configuración o especificarse en la lista del `validDomains` manifiesto.

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>No se puede autenticar al usuario ni mostrar el proveedor de autenticación en la pestaña

A menos que realice la autenticación silenciosa, debe seguir el proceso de autenticación proporcionado por el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client).

> [!NOTE]
> Se requiere que todo el flujo de autenticación se inicie y finalice en el dominio, que debe aparecer en el `validDomains` objeto del manifiesto.

Para obtener más información sobre la autenticación, consulte [Autenticación de un usuario](~/concepts/authentication/authentication.md).

### <a name="static-tabs-not-showing-up"></a>Pestañas estáticas que no se muestran

Hay un problema conocido por el que la actualización de una aplicación de bot existente con una pestaña estática nueva o actualizada no mostrará ese cambio de pestaña al acceder a la aplicación desde una conversación de chat personal.  Para ver el cambio, debe probar en un nuevo usuario o instancia de prueba, o acceder al bot desde el control flotante Aplicaciones.

## <a name="troubleshooting-bots"></a>Solución de problemas de bots

### <a name="cant-add-my-bot"></a>No se puede agregar mi bot

El administrador de inquilinos de Office 365 debe habilitar las aplicaciones para que las carguen los usuarios finales. En algunos casos, el inquilino de Office 365 podría tener varias SKU asociadas y, para que los bots funcionen en cualquiera, deben estar habilitados en todas las SKU. Para obtener más información, consulte [Preparación del inquilino de Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

### <a name="cant-add-bot-as-a-member-of-a-team"></a>No se puede agregar un bot como miembro de un equipo

Los bots deben cargarse primero en un equipo antes de que sea accesible dentro de cualquier canal de ese equipo. Para obtener más información sobre este proceso, consulte [Carga de la aplicación en un equipo](~/concepts/deploy-and-publish/apps-upload.md).

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>Mi bot no recibe mi mensaje en un canal

Los bots de los canales reciben mensajes solo cuando se @mentioned explícitamente, incluso si responde a un mensaje de bot anterior. La única excepción en la que es posible que no vea el nombre del bot en un mensaje es si el bot recibe una `imBack` acción como resultado de una CardAction que envió originalmente.

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>Mi bot no entiende mis comandos cuando se encuentra en un canal

Dado que los bots de los canales solo reciben mensajes cuando se @mentioned, todos los mensajes que recibe el bot en un canal incluyen ese @mention en el campo de texto. Se recomienda quitar el nombre del bot de todos los mensajes de texto entrantes antes de pasar a la lógica de análisis. Revise [las menciones](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) para obtener sugerencias sobre cómo controlar este caso.

## <a name="issues-with-packaging-and-uploading"></a>Problemas con el empaquetado y la carga

### <a name="error-while-reading-manifestjson"></a>Error al leer manifest.json

La mayoría de los errores de manifiesto proporcionarán una sugerencia sobre qué campo específico falta o no es válido. Sin embargo, si el archivo JSON no se puede leer como JSON en absoluto, se usa este mensaje de error genérico.

Motivos comunes de errores de lectura de manifiestos:

* JSON no válido. Use un IDE como [Visual Studio Code](https://code.visualstudio.com) o [Visual Studio](https://www.visualstudio.com/vs/) que valide automáticamente la sintaxis JSON.
* Problemas de codificación. Use UTF-8 para el archivo *manifest.json* . Es posible que otras codificaciones, específicamente con la lista de materiales, no sean legibles.
* Paquete de .zip con formato incorrecto. El archivo *manifest.json* debe estar en el nivel superior del archivo .zip. Tenga en cuenta que la compresión predeterminada de archivos Mac podría colocar *el archivo manifest.json* en un subdirectorio, que no se cargará correctamente en Microsoft Teams.

### <a name="another-extension-with-same-id-exists"></a>Existe otra extensión con el mismo identificador

Si intenta cargar de nuevo un paquete actualizado con el mismo identificador, elija el icono **Reemplazar** al final de la fila de tabla de la pestaña en lugar del botón **Cargar** .

Si no va a volver a cargar un paquete actualizado, asegúrese de que el identificador sea único.
