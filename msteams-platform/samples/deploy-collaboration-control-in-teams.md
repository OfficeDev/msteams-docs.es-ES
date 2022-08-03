---
title: Implementación de una aplicación con controles de colaboración en Microsoft Teams
author: surbhigupta
description: En este módulo, aprenderá a implementar la aplicación con el control colaboración en Microsoft Teams y a permitir que otros usuarios usen la aplicación.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 0ea4f1c25a84ec1bcbefc379e5021815a5bea650
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179409"
---
# <a name="deploy-collaboration-controls-to-microsoft-teams"></a>Implementación de controles de colaboración en Microsoft Teams

Actualmente, los controles de colaboración funcionan mejor en Microsoft Teams. Puede crear una nueva aplicación que se pueda insertar dentro de la aplicación de Teams como una aplicación personal y una aplicación de pestaña.

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

## <a name="configure-the-app-for-teams"></a>Configuración de la aplicación para Teams

La aplicación que ha creado en [la creación de una aplicación controlada por modelos](/samples/app-with-collaboration-controls.md#create-a-model-driven-application) solo tiene un único panel izquierdo y no hay comandos complejos. Por lo tanto, antes de agregar la aplicación a Teams, puede ocultar el panel izquierdo y hacer una vista de encabezado más comprensible.

> [!NOTE]
> No habilite los pasos siguientes si desea mostrar el panel izquierdo y el encabezado de alta densidad a los usuarios.

Para ello, usaremos la nueva configuración de **la aplicación** de Power Apps.

1. Vaya a **Soluciones** en el panel izquierdo.

1. Vaya a la parte inferior de la lista de soluciones y seleccione **Solución predeterminada**.

1. Busque y seleccione **Definición de configuración**.

     :::image type="content" source="../assets/images/collaboration-control/settings-defnition.png" alt-text="Definición de configuración":::

1. Busque y seleccione **Ocultar la barra de navegación** de la lista de definiciones de configuración. Esto oculta el panel izquierdo de la aplicación.

     :::image type="content" source="../assets/images/collaboration-control/hide-the-nav-bar.png" alt-text="Ocultar la barra de navegación":::

1. En la parte inferior derecha de la aplicación en el panel de edición, hay una sección titulada **Establecer valores de aplicación**. Si creaste la aplicación con el diseñador de aplicaciones moderno, la aplicación aparece en la lista. Seleccione **Nuevo valor de aplicación** en la aplicación.

1. Cambie el valor de **No** a **Sí.**

     :::image type="content" source="../assets/images/collaboration-control/value-to-yes.png" alt-text="Cambiar el valor a sí":::

1. Seleccione **Guardar.**

1. Busque y seleccione **Encabezado de página De alta densidad** de aplicaciones en la lista de definiciones de configuración y repita el proceso.

     :::image type="content" source="../assets/images/collaboration-control/density-page-header.png" alt-text="Encabezado de página de densidad":::

1. Seleccione **Volver a las soluciones**.

     :::image type="content" source="../assets/images/collaboration-control/default-solution.png" alt-text="Solución predeterminada":::

1. Seleccione **Publicar todas las personalizaciones** para publicar todo el trabajo que ha completado.

     :::image type="content" source="../assets/images/collaboration-control/publish-cusomization.png" alt-text="Publicación de todas las personalizaciones":::

## <a name="add-the-app-to-microsoft-teams-app-catalog"></a>Adición de la aplicación al catálogo de aplicaciones de Microsoft Teams

A medida que se define la configuración, ahora puede agregar la aplicación a Microsoft Teams. Para empezar, vaya a la página **Aplicaciones** del portal creador de Power Apps y busque la aplicación que ha creado y seleccione elipse **...**.

Para agregar la aplicación a Teams, seleccione **Agregar a Teams**.

:::image type="content" source="../assets/images/collaboration-control/add-to-teams.png" alt-text="Agregar a Teams":::

Al seleccionar **Agregar a Teams** , se abre un cuadro de diálogo en el que puede revisar los detalles y seleccionar **Descargar aplicación**, que guarda el manifiesto de aplicación de Microsoft Teams en el dispositivo.

:::image type="content" source="../assets/images/collaboration-control/colab-manager-inspection.png" alt-text="La captura de pantalla es un ejemplo que muestra la inspección del administrador de colaboración":::

Para cargar la aplicación en Teams, consulte [Carga de la aplicación en equipo](~/concepts/deploy-and-publish/apps-upload.md).

## <a name="enable-others-to-use-your-application"></a>Permitir que otros usuarios usen la aplicación

A continuación se requieren para permitir que los usuarios ejecuten las aplicaciones de Collaboration Manager implementadas creadas mediante los controles de colaboración:

* Creación de un equipo de colaboración
* Agregar miembros al equipo
* Creación de un rol de seguridad
* Asignación de roles de seguridad a miembros del equipo

### <a name="create-a-collaboration-team"></a>Creación de un equipo de colaboración

1. Inicie sesión en el [Centro de administración de Power Platform](https://admin.powerplatform.microsoft.com/environments).

     1. Seleccione el entorno donde se implementa la aplicación.
     1. Seleccione **Configuración** > **Permisos de usuarios** + **.**
     1. Seleccione **Teams**.

1. Seleccione el botón **+ Crear equipo** en la parte superior de la página.

1. Agregue todos los campos necesarios:
     1. **Nombre del equipo:** Asegúrese de que el nombre es único dentro de la unidad de negocio.
     1. **Descripción:** Escriba una descripción del equipo.
     1. **Unidad de negocio:** Seleccione una unidad de negocio en la lista desplegable.
     1. **Administrador:** Busque el usuario de la organización que desea asignar como administrador escribiendo caracteres.
     1. **Tipo de equipo:** Seleccione el tipo de equipo. En los pasos siguientes se supone que ha seleccionado Propietario en la lista desplegable. Los otros tipos de equipo (equipo de Microsoft 365 y equipo de Microsoft Azure Active Directory) rellenan automáticamente los miembros del equipo de Azure Active Directory.

         :::image type="content" source="../assets/images/collaboration-control/new-team.png" alt-text="Nuevo equipo":::

     1. Asegúrese de anotar el nombre del equipo. Necesitará esto más adelante para asignar este equipo como propietario de un registro.

     1. Seleccione **Siguiente.**

### <a name="add-members-to-the-team"></a>Agregar miembros al equipo

> [!NOTE]
> No es necesario agregar miembros al equipo si el tipo de equipo es Azure Active Directory o Microsoft 365.

1. Seleccione un equipo y, a continuación, seleccione **Administrar miembros del equipo**.

1. Para agregar nuevos miembros del equipo, seleccione **+ Agregar miembros del equipo** y elija usuarios de su organización para agregar.

     :::image type="content" source="../assets/images/collaboration-control/add-team-members.png" alt-text="En la captura de pantalla se describe cómo agregar miembros del equipo":::

1. Para eliminar un miembro del equipo, seleccione el usuario y, a continuación, elija **Quitar**.

### <a name="create-a-security-role"></a>Creación de un rol de seguridad

1. Seleccione **Configuración** > **Permisos de usuarios** + **en el** entorno donde se implementa la aplicación.

1. Seleccione **Roles de seguridad**.

     :::image type="content" source="../assets/images/collaboration-control/users-permission.png" alt-text="Permisos de usuarios":::

1. Seleccione **Nuevo rol** en la parte superior izquierda de la página, que ahora abre una nueva página.

1. En la **pestaña Detalles**, proporcione un nombre para el rol de seguridad.

1. Vaya a la pestaña **Entidades personalizadas** .

     1. Conceda permisos de organización (círculo verde completo) para cada una de las entidades de colaboración, **mapa de colaboración**, **metadatos de colaboración** y **raíz de colaboración**.

         :::image type="content" source="../assets/images/collaboration-control/collab-map.png" alt-text="Mapa de colaboración":::

1. Seleccione **Guardar** y **cerrar**.

### <a name="assign-security-roles"></a>Asignación de roles de seguridad

1. Seleccione **Configuración** > **Permisos de usuarios** + **en el** entorno donde se implementa la aplicación.

1. Seleccione **Teams** y, a continuación, el equipo que creó para [crear un equipo de colaboración](#create-a-collaboration-team).

1. Elija **Administrar roles de seguridad** en el encabezado.

     :::image type="content" source="../assets/images/collaboration-control/edit-team.png" alt-text="Editar equipo":::

1. Seleccione los roles [creados en un rol de seguridad](#create-a-security-role).

1. Seleccione **Guardar**.

Para obtener más información sobre los privilegios de rol, consulte [Configuración de la seguridad del usuario en un entorno](/power-platform/admin/database-security).
