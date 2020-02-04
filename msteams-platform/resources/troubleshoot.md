---
title: Solucionar problemas de la aplicación
description: Solucionar problemas o errores durante la creación de aplicaciones para Microsoft Teams
keywords: solución de problemas de desarrollo de aplicaciones de Microsoft Teams
ms.date: 07/09/2018
ms.openlocfilehash: f7fe42e7c1f3ff2c4d8d1cbe81ed8f71e6c04384
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675732"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Solucionar problemas de la aplicación de Microsoft Teams

## <a name="troubleshooting-tabs"></a>Solución de problemas de pestañas

### <a name="accessing-the-devtools"></a>Acceso a DevTools

Puede abrir [DevTools en el cliente de Microsoft Teams](~/tabs/how-to/developer-tools.md) para obtener una experiencia similar a la de presionar F12 (en Windows) o Comando-opción-I (en MacOS) en un explorador.

### <a name="blank-tab-screen"></a>Pantalla de ficha en blanco

Si no ve el contenido en la vista de pestaña, puede ser:

* el contenido no se puede mostrar en `<iframe>`un.
* el dominio de contenido no está en la lista [validDomains](~/resources/schema/manifest-schema.md#validdomains) en el manifiesto.

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>El botón Guardar no está habilitado en el cuadro de diálogo de configuración

Asegúrese de llamar `microsoftTeams.settings.setValidityState(true)` una vez que el usuario haya introducido o seleccionado todos los datos necesarios en la página de configuración para habilitar el botón Guardar.

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>Después de seleccionar el botón Guardar, no se puede guardar la configuración de la pestaña.

Al agregar una pestaña, si hace clic en los botones para guardar, pero aparece un mensaje de error que indica que no se puede guardar la configuración, el problema puede deberse a dos clases de problemas:

* No se recibió nunca el mensaje guardar correctamente. Si un controlador de almacenamiento se registró con `microsoftTeams.settings.registerOnSaveHandler(handler)`, la devolución `saveEvent.notifySuccess()`de llamada debe llamar. Si la devolución de llamada no llama a este método antes `saveEvent.notifyFailure(reason)` de 30 segundos o llamadas en su lugar, se mostrará este error.

* Si no se registró ningún controlador de `saveEvent.notifySuccess()` guardado, la llamada se realiza automáticamente inmediatamente después de que el usuario seleccione el botón Guardar.

* La configuración proporcionada no es válida. La otra razón por la que no se puede guardar la configuración es que `microsoftTeams.setSettings(settings)` la llamada para la que se ha proporcionado un objeto de configuración no válido o la llamada no se haya realizado. Vea la sección siguiente, problemas comunes con el objeto Settings.

### <a name="common-problems-with-the-settings-object"></a>Problemas comunes con el objeto Settings

* `settings.entityId`falta. Este campo es necesario.
* `settings.contentUrl`falta. Este campo es necesario.
* `settings.contentUrl`o el opcional `settings.removeUrl`, o `settings.websiteUrl` se proporcionan pero no son válidos. Las direcciones URL deben usar HTTPS y también deben ser el mismo dominio que la página de configuración o especificarse en la `validDomains` lista del manifiesto.

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>No se puede autenticar al usuario ni mostrar su proveedor de autenticación en su pestaña

A menos que esté realizando una autenticación silenciosa, debe seguir el proceso de autenticación proporcionado por el [SDK de Microsoft Teams](/javascript/api/overview/msteams-client.md)para el cliente de JavaScript.

> [!NOTE]
>Es necesario que el flujo de autenticación se inicie y finalice en su dominio, que debe aparecer en `validDomains` el objeto del manifiesto.

Para obtener más información acerca de la autenticación, consulte [Authenticate a User](~/concepts/authentication/authentication.md).

### <a name="static-tabs-not-showing-up"></a>Pestañas estáticas que no aparecen

Hay un problema conocido en el que, al actualizar una aplicación de bot existente con una pestaña estática nueva o actualizada, no se muestra el cambio de la pestaña cuando se accede a la aplicación desde una conversación de chat personal.  Para ver el cambio, debe probar una nueva instancia de usuario o prueba, o tener acceso al bot desde el control flotante de aplicaciones.

## <a name="troubleshooting-bots"></a>Solución de problemas de bots

### <a name="cant-add-my-bot"></a>No se puede agregar mi bot

El administrador de inquilinos de Office 365 debe habilitar las aplicaciones para que las carguen los usuarios finales. Tenga en cuenta que, en algunos casos, es posible que el inquilino de Office 365 tenga varios SKU asociados y que para que los bots trabajen en ellos, deben estar habilitados en todas las SKU. Consulte [preparar el inquilino de Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md) para obtener más información.

### <a name="cant-add-bot-as-a-member-of-a-team"></a>No se puede Agregar un bot como miembro de un equipo

Los bots deben cargarse primero en un equipo antes de que se pueda tener acceso a ellos dentro de cualquier canal de ese equipo. Consulte la información de [la aplicación en un equipo](~/concepts/deploy-and-publish/apps-upload.md) para obtener más información sobre este proceso.

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>Mi bot no recibe mi mensaje en un canal

Los bots de los canales reciben mensajes solo cuando se @mentionedn explícitamente, incluso si está respondiendo a un mensaje de bot anterior. La única excepción en la que es posible que no vea el nombre de bot en un mensaje es si `imBack` el bot recibe una acción como resultado de un CardAction que envió originalmente.

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>Mi bot no entiende mis comandos cuando está en un canal

Como los bots de los canales solo reciben mensajes cuando se @mentioned, todos los mensajes que el bot recibe en un canal incluyen ese @mention en el campo de texto. Se recomienda quitar el nombre del bot de todos los mensajes de texto entrantes antes de pasar a la lógica de análisis. Revise las [menciones](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions) para ver sugerencias sobre cómo controlar este caso.

## <a name="issues-with-packaging-and-uploading"></a>Problemas con el empaquetado y la carga

### <a name="error-while-reading-manifestjson"></a>Error al leer manifest. JSON

La mayoría de los errores del manifiesto proporcionarán una sugerencia en qué campo específico falta o no es válido. Sin embargo, si el archivo JSON no se puede leer como JSON, se usa este mensaje de error genérico.

Motivos comunes de los errores de lectura del manifiesto:

* JSON no válido. Use un IDE como [Visual Studio Code](https://code.visualstudio.com) o [Visual Studio](https://www.visualstudio.com/vs/) que valide automáticamente la sintaxis JSON.
* Problemas de codificación. Use UTF-8 para el archivo *manifest. JSON* . Es posible que no se puedan leer otras codificaciones, en concreto con la l. MAT.
* Paquete. zip con formato incorrecto. El archivo *manifest. JSON* debe estar en el nivel superior del archivo. zip. Tenga en cuenta que la compresión de archivos Mac predeterminada puede poner *manifest. JSON* en un subdirectorio, que no se cargará correctamente en Microsoft Teams.

### <a name="another-extension-with-same-id-exists"></a>Existe otra extensión con el mismo identificador

Si está intentando volver a cargar un paquete actualizado con el mismo identificador, elija el icono **reemplazar** situado al final de la fila de la tabla de la pestaña en lugar del botón **cargar** .

Si no va a volver a cargar un paquete actualizado, asegúrese de que el identificador es único.
