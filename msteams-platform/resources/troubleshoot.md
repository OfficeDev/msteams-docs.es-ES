---
title: Solucionar problemas de la aplicación
description: Solucionar problemas o errores al crear aplicaciones para Microsoft Teams
keywords: Solución de problemas de desarrollo de aplicaciones de teams
localization_priority: Normal
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: ce45a75869e8b6694cd84c10f8fac1f9bd55bad4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020432"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Solucionar problemas de la aplicación de Microsoft Teams

## <a name="troubleshooting-tabs"></a>Pestañas de solución de problemas

### <a name="accessing-the-devtools"></a>Acceso a DevTools

Puede abrir [DevTools](~/tabs/how-to/developer-tools.md) en el cliente de Teams para una experiencia similar a la de presionar F12 (en Windows) o Command-Option-I (en MacOS) en un explorador.

### <a name="blank-tab-screen"></a>Pantalla de pestaña en blanco

Si no ve el contenido en la vista de pestañas, podría ser:

* el contenido no se puede mostrar en un `<iframe>` archivo .
* el dominio de contenido no está en la [lista validDomains](~/resources/schema/manifest-schema.md#validdomains) del manifiesto.

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>El botón Guardar no está habilitado en el cuadro de diálogo de configuración

Asegúrese de llamar una vez que el usuario haya ingresado o seleccionado todos los datos necesarios en la página de configuración `microsoftTeams.settings.setValidityState(true)` para habilitar el botón guardar.

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>Después de seleccionar el botón Guardar, la configuración de ficha no se puede guardar

Al agregar una pestaña, si hace clic en los botones de guardar pero se muestra un mensaje de error que indica que la configuración no se puede guardar, el problema podría ser una de las dos clases de problemas:

* El mensaje de guardado correcto nunca se recibió. Si se registró un controlador de guardado con `microsoftTeams.settings.registerOnSaveHandler(handler)` , la devolución de llamada debe llamar `saveEvent.notifySuccess()` a . Si la devolución de llamada no llama a esto en 30 segundos o llama en su lugar, se `saveEvent.notifyFailure(reason)` mostrará este error.

* Si no se registró ningún controlador de guardado, la llamada se realiza automáticamente inmediatamente `saveEvent.notifySuccess()` cuando el usuario selecciona el botón guardar.

* La configuración proporcionada no era válida. La otra razón por la que es posible que la configuración no se guarde es si la llamada a un objeto de configuración no válido o si la llamada `microsoftTeams.setSettings(settings)` no se realizó en absoluto. Consulte la siguiente sección, Problemas comunes con el objeto settings.

### <a name="common-problems-with-the-settings-object"></a>Problemas comunes con el objeto settings

* `settings.entityId` falta. Este campo es necesario.
* `settings.contentUrl` falta. Este campo es necesario.
* `settings.contentUrl` o el opcional `settings.removeUrl` , o se proporcionan pero no son `settings.websiteUrl` válidos. Las direcciones URL deben usar HTTPS y también deben ser el mismo dominio que la página de configuración o especificadas en la lista del `validDomains` manifiesto.

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>No se puede autenticar al usuario ni mostrar el proveedor de autenticación en la pestaña

A menos que realice la autenticación silenciosa, debe seguir el proceso de autenticación proporcionado por el SDK de [cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client.md).

> [!NOTE]
>Se requiere todo el flujo de autenticación para iniciar y finalizar en el dominio, que debe aparecer en el `validDomains` objeto del manifiesto.

Para obtener más información acerca de la autenticación, vea [Authenticate a user](~/concepts/authentication/authentication.md).

### <a name="static-tabs-not-showing-up"></a>Pestañas estáticas que no se muestran

Existe un problema conocido por el que la actualización de una aplicación de bot existente con una pestaña estática nueva o actualizada no mostrará ese cambio de pestaña al acceder a la aplicación desde una conversación de chat personal.  Para ver el cambio, debes probar en un nuevo usuario o instancia de prueba, o acceder al bot desde el control desplegable Aplicaciones.

## <a name="troubleshooting-bots"></a>Solución de problemas de bots

### <a name="cant-add-my-bot"></a>No se puede agregar el bot

El administrador de inquilinos de Office 365 debe habilitar las aplicaciones para que las carguen los usuarios finales. Tenga en cuenta que, en algunos casos, el inquilino de Office 365 puede tener varias SKU asociadas y, para que los bots funcionen en cualquiera, deben estar habilitados en todas las SKU. Consulte [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) para obtener más información.

### <a name="cant-add-bot-as-a-member-of-a-team"></a>No se puede agregar bot como miembro de un equipo

Los bots deben cargarse primero en un equipo antes de que sea accesible en cualquier canal de ese equipo. Consulta [Cargar la aplicación en un equipo](~/concepts/deploy-and-publish/apps-upload.md) para obtener más información sobre este proceso.

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>Mi bot no recibe mi mensaje en un canal

Los bots de los canales reciben mensajes solo cuando se @mentioned explícitamente, incluso si estás respondiendo a un mensaje de bot anterior. La única excepción en la que es posible que no vea el nombre del bot en un mensaje es si el bot recibe una acción como resultado de un CardAction que `imBack` envió originalmente.

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>Mi bot no entiende mis comandos cuando está en un canal

Dado que los bots de los canales solo reciben mensajes cuando se @mentioned, todos los mensajes que el bot recibe en un canal incluyen @mention en el campo de texto. Es una práctica recomendada quitar el nombre del bot de todos los mensajes de texto entrantes antes de pasar a la lógica de análisis. Revise [las menciones](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) para obtener sugerencias sobre cómo tratar este caso.

## <a name="issues-with-packaging-and-uploading"></a>Problemas con el empaquetado y la carga

### <a name="error-while-reading-manifestjson"></a>Error al leer manifest.jsen

La mayoría de los errores de manifiesto proporcionarán una sugerencia sobre qué campo específico falta o no es válido. Sin embargo, si el archivo JSON no se puede leer como JSON en absoluto, se usa este mensaje de error genérico.

Motivos comunes de errores de lectura de manifiesto:

* JSON no válido. Use un IDE como [Visual Studio code](https://code.visualstudio.com) [o Visual Studio](https://www.visualstudio.com/vs/) que valide automáticamente la sintaxis JSON.
* Problemas de codificación. Use UTF-8 para el *manifest.jsen* el archivo. Es posible que otras codificaciones, específicamente con la lista de materiales, no sean legibles.
* Paquete .zip malformado. El *manifest.jsen* debe estar en el nivel superior del archivo .zip. Tenga en cuenta que la compresión de archivos mac predeterminada puede colocar el *manifest.jsen* un subdirectorio, que no se cargará correctamente en Microsoft Teams.

### <a name="another-extension-with-same-id-exists"></a>Existe otra extensión con el mismo identificador

Si intenta volver a cargar un paquete actualizado con el  mismo identificador, elija el icono Reemplazar al final de la fila de tabla de la pestaña en lugar del **botón** Cargar.

Si no va a volver a cargar un paquete actualizado, asegúrese de que el identificador es único.
