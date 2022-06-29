---
title: Cargar la aplicación personalizada
description: Obtenga información sobre cómo transferir localmente la aplicación en Microsoft Teams. La transferencia local es común al probar y depurar una aplicación durante el desarrollo.
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 12bd5a6e2c72c1095fbb7f6f113cb9126b247289
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503959"
---
# <a name="upload-your-app-in-teams"></a>Cargar la aplicación en Microsoft Teams

Puede cargar lateralmente las aplicaciones de Microsoft Teams sin tener que publicarlas en su organización o en la tienda de Teams en los siguientes casos:

* Quiere probar y depurar una aplicación de manera local usted mismo o con otros desarrolladores.
* Ha creado una aplicación para automatizar un flujo de trabajo.
* Ha creado una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.

> [!NOTE]
> Al realizar la instalación de prueba de la aplicación varias veces se muestra más de una instancia para las extensiones de mensajería.

> [!IMPORTANT]
> En este momento, la transferencia local de aplicaciones está disponible en Government Community Cloud (GCC), pero no está disponible para GCC-High ni para el Departamento de Defensa (DOD).

## <a name="prerequisites"></a>Requisitos previos

* Asegúrese de crear el [paquete de la aplicación](~/concepts/build-and-test/apps-package.md) y [validarlo](https://dev.teams.microsoft.com/appvalidation.html) para encontrar errores.
* [Habilite la carga de aplicaciones personalizadas](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) en Teams.
* Asegúrese de que la aplicación se está ejecutando y es accesible mediante HTTPs.

## <a name="upload-your-app"></a>Cargar la aplicación

Puede transferir localmente la aplicación a un equipo, chat, reunión o para su uso personal en función de cómo haya configurado el ámbito de la aplicación.

1. Inicie sesión en el cliente de Teams con su [cuenta de desarrollo de Microsoft 365](https://developer.microsoft.com/en-us/microsoft-365/dev-program).
1. Seleccione **Aplicaciones** > **Administrar las aplicaciones** y **Publicar una aplicación**.

    :::image type="content" source="~/assets/images/publish-app/manage-apps.png" alt-text="Publicar una aplicación" border="true":::

1. Seleccione **Cargar una aplicación personalizada**.

   :::image type="content" source="~/assets/images/publish-app/publish-app.png" alt-text="Cargar una aplicación personalizada" border="true":::.

1. Seleccione el archivo .zip del paquete de la aplicación.
1. Agregue la aplicación a Teams según sus necesidades:</br>

   a. Seleccione **Agregar** para agregar su aplicación personal.</br> B. Use el menú desplegable para agregar la aplicación a un equipo o chat.

    :::image type="content" source="~/assets/images/publish-app/teams-app-detail.png" alt-text="Descripción de la aplicación" border="true":::

## <a name="troubleshoot"></a>Solucionar problemas

Si la aplicación no se puede transferir localmente o hay problemas para cargarla, compruebe las siguientes opciones:

1. Asegúrese de haber seguido todas las instrucciones para [crear el paquete de la aplicación](../../concepts/build-and-test/apps-package.md).
1. [Validar el paquete de la aplicación](https://dev.teams.microsoft.com/appvalidation.html).
1. Asegúrese de que el manifiesto de la aplicación coincide con el último [esquema](../../resources/schema/manifest-schema.md).

## <a name="manage-your-apps"></a>Administrar las aplicaciones

Administrar las aplicaciones permite a los usuarios tener un lugar dedicado para administrar, actualizar y quitar sus aplicaciones, permisos y suscripciones en el cliente de Teams. Los usuarios pueden instalar las aplicaciones desde **Administrar las aplicaciones**.

### <a name="access-your-app"></a>Acceder a la aplicación

Para acceder a las aplicaciones a través de **Administrar las aplicaciones** siga estos pasos:

1. Vaya a **Aplicaciones** y seleccione **Administrar las aplicaciones** en Teams para ver las aplicaciones instaladas en todos los canales o para su uso personal en un formato de lista.

    :::image type="content" source="~/assets/images/publish-app/manage-apps-list.png" alt-text="Acceso a la lista de aplicaciones de Teams" border="true":::

1. Seleccione la lista desplegable de aplicaciones para ver todos los ámbitos en los que está instalada la aplicación.

    :::image type="content" source="~/assets/images/publish-app/app-scopes.png" alt-text="Acceso al ámbito de la aplicación de Teams" border="true":::

1. Seleccione el ámbito de la aplicación para ir a la aplicación en el canal o en la vista personal. La lista de ámbitos consta solo de ámbito personal y ámbito de equipos. Las aplicaciones instaladas en el ámbito de chat de grupo no se muestran actualmente en esta vista.

Teams proporciona varias maneras de abrir aplicaciones. Para obtener más información, consulte [acceso a las aplicaciones en Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

### <a name="update-your-app"></a>Actualizar la aplicación

No tiene que transferir localmente la aplicación de nuevo si realiza cambios de código (estos se reflejan en Teams en tiempo real). Sin embargo, debe reinstalar si cambia alguna configuración de aplicación.

Si hay una actualización disponible para la aplicación, la opción **Actualización disponible** está habilitada. Para actualizar, siga estos pasos:

1. Seleccione **Actualización disponible** para ver la actualización.

     :::image type="content" source="~/assets/images/publish-app/update-available.png" alt-text="Actualizar la aplicación Teams" border="true":::.

1. Seleccione **Ver actualización**, aparecerá una ventana con la opción de actualización.
1. Seleccione el botón **Actualizar** para actualizar la aplicación.

     :::image type="content" source="~/assets/images/publish-app/update-window.png" alt-text="Actualizar la aplicación Teams en administrar aplicaciones" border="true":::

     :::image type="content" source="~/assets/images/publish-app/updated-app.png" alt-text="Aplicación actualizada" border="true":::

### <a name="remove-your-app"></a>Quitar la aplicación

Para quitar la aplicación de Teams, siga estos pasos:

1. Busque la aplicación en **Administrar la aplicación**.
1. Seleccione &nbsp;:::image type="content" source="~/assets/images/publish-app/bin-icon.png" alt-text="Quitar aplicación en Teams" border="false":::&nbsp; en el ámbito de la aplicación instalada.

    :::image type="content" source="~/assets/images/publish-app/uninstall-from-channel.png" alt-text="Quitar aplicación en un canal" border="true":::

1. Seleccione **Quitar** para quitar la aplicación.

    :::image type="content" source="~/assets/images/publish-app/remove-app-teams.png" alt-text="Quitar una aplicación de Teams" border="true":::

> [!NOTE]
>
> * No puede eliminar por completo la actividad del bot personal. Si elimina la aplicación y la vuelve a agregar, la nueva comunicación con el bot se anexa a la conversación anterior con él.
> * Actualmente, no puede migrar la aplicación personalizada a la tienda de Teams. Si desea mostrar su aplicación en la tienda de Teams, consulte [Publicar su aplicación en la tienda de Microsoft Teams](appsource/publish.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
>[Crear aplicaciones para reuniones de Teams](../../apps-in-teams-meetings/teams-apps-in-meetings.md)

## <a name="see-also"></a>Vea también

* [Configurar las opciones de instalación predeterminadas](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Mantener la aplicación publicada de Microsoft Teams](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
