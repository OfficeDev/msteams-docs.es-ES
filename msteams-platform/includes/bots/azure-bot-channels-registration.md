---
title: Registro del canal de bot de Azure
description: describe los canales de bot de Azure para el registro
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 3cbbd204daf98f1c3528dcb6efcfde299a402912
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020952"
---
1. En [Azure Portal](https://ms.portal.azure.com/#home), en Servicios de Azure, seleccione **Crear un recurso**.
1. En el cuadro de búsqueda, escriba "bot". Y en la lista desplegable, seleccione **Registro de canales de bot.**
1. Seleccione el **botón** Crear.
1. En la **hoja Registro del canal bot,** proporcione la información solicitada sobre el bot.
1. Deje el **cuadro Punto de conexión** de mensajería vacío por ahora, escribirá la dirección URL necesaria después de implementar el bot. En la siguiente imagen se muestra un ejemplo de la configuración de registro:

    ![Registro de canales de aplicación bot](../../assets/images/authentication/auth-bot-channels-registration.png)

1. Haga clic **en Id. de aplicación y contraseña** de Microsoft **y, a continuación, cree nuevo**.

    ![Crear id. de aplicación de Microsoft ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ Crear nuevo id. de aplicación de Microsoft](../../assets/images/authentication/CreateNewMicrosoftAppID.png)    

1. Haz **clic en Crear id. de aplicación en el vínculo Portal de registro de** aplicaciones.

   ![Registros de aplicaciones](../../assets/images/authentication/AppRegistration.png)
   
1. En la ventana **de registro de aplicaciones mostrada,** haga clic en la pestaña Nuevo **registro** de la parte superior izquierda.
1. Escriba el nombre de la aplicación bot que está registrando, hemos usado *BotTeamsAuth* (necesita seleccionar su propio nombre único).
1. Para los **tipos de** cuentas compatibles, seleccione Cuentas en cualquier directorio de la organización (cualquier directorio de Azure AD - Multitenant) y cuentas personales de *Microsoft (por ejemplo, Skype, Xbox).*
1. Haga clic en **el botón** Registrar. Una vez completada, Azure muestra la *página Información* general de la aplicación.
1. Copie y guarde en un archivo el valor del identificador de aplicación **(cliente).**
1. En el panel izquierdo, haga clic **en Certificado y secretos**.
    1. En *Secretos de cliente,* haga clic **en Nuevo secreto de cliente**.
    1. Agrega una descripción para identificar este secreto de otros usuarios que podrías necesitar crear para esta aplicación.
    1. Establece *Expira en* la selección.
    1. Seleccione **Agregar**.
    1. Copie el secreto de cliente y guárdelo en un archivo.
1. Vuelva a la ventana **Registro** del canal bot  y copie el *identificador* de aplicación y el secreto de cliente en los cuadros **Id.** de aplicación de Microsoft y **Contraseña,** respectivamente.
1. Haga clic en **Aceptar**.
1. Por último, haga clic **en Crear**.

Después de que Azure haya creado el recurso de registro, se incluirá en la lista de grupos de recursos.  

![Grupo de registro de canales de aplicación bot](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

Una vez creado el registro de los canales del bot, deberá habilitar el Teams canal.

1. En [Azure Portal](https://ms.portal.azure.com/#home), en Servicios de Azure, seleccione el registro del **canal bot** que acaba de crear.
1. En el panel izquierdo, haga clic en **Canales**.
1. Haga clic en el Microsoft Teams y, a continuación, **elija Guardar**.
