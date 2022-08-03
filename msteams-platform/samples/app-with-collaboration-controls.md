---
title: Aplicación con controles de colaboración
author: surbhigupta
description: En este módulo, aprenderá a crear una aplicación basada en modelos con controles de colaboración para Teams y a agregar controles de colaboración a la aplicación.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: b5300a66fa8a5948a2081e90e8ad138858d38f3f
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179511"
---
# <a name="create-a-new-model-driven-app-with-collaboration-controls-for-teams"></a>Creación de una nueva aplicación controlada por modelos con controles de colaboración para Teams

Los controles de colaboración están diseñados para [aplicaciones basadas en modelos](/power-apps/maker/model-driven-apps/model-driven-app-overview). En la sección siguiente se explica cómo crear una aplicación controlada por modelos.

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

## <a name="create-a-model-driven-application"></a>Creación de una aplicación controlada por modelos

1. Abra [https://make.powerapps.com.](https://make.powerapps.com/) o [https://make.preview.powerapps.com.](https://make.preview.powerapps.com/)

1. Seleccione **Soluciones** en el panel izquierdo.

1. Seleccione **Nueva solución** para que pueda proporcionar un hogar para todas las personalizaciones futuras.

   :::image type="content" source="../assets/images/collaboration-control/new-solution.png" alt-text="La captura de pantalla es un ejemplo que muestra la nueva solución.":::

1. Proporcione el nombre y el publicador de la nueva solución; esta solución va a contener el Collaboration Manager personalizado.

   :::image type="content" source="../assets/images/collaboration-control/collaboration-manager.png" alt-text="La captura de pantalla es un ejemplo que muestra el administrador de colaboración.":::

1. Seleccione **Crear**

1. Una vez creada la solución, aparece en la lista de soluciones. Seleccione la solución para abrirla.

1. Antes de crear la aplicación, cree una casa para los datos. seleccione **Nueva** > **tabla** para empezar.

     :::image type="content" source="../assets/images/collaboration-control/create-table.png" alt-text="En la captura de pantalla se describe cómo crear una nueva tabla.":::

1. Asigne un nombre a la tabla. En **Opciones avanzadas**, seleccione **Crear una nueva actividad**.

   :::image type="content" source="../assets/images/collaboration-control/new-activity.png" alt-text="En la captura de pantalla se describe cómo crear una nueva actividad.":::

1. Seleccione **Guardar**.

1. Una vez que haya terminado de crear la tabla, puede personalizarla agregando columnas adicionales, relaciones y mucho más (opcional).

1. Ahora puede crear una nueva aplicación controlada por modelos seleccionando **Nueva** > **aplicación** > **controlada por modelos de aplicación.**

   :::image type="content" source="../assets/images/collaboration-control/model-driven-app.png" alt-text="La captura de pantalla es un ejemplo que muestra la nueva aplicación controlada por modelos.":::

1. Elija nuevo **diseñador de aplicaciones modernas (versión preliminar)** para abrir la nueva aplicación.

   :::image type="content" source="../assets/images/collaboration-control/model-driven-app-blank.png" alt-text="La captura de pantalla es un ejemplo que muestra la nueva aplicación controlada por modelos en blanco.":::

1. Seleccione **Crear.**

1. Asigne un nombre a la aplicación y seleccione **Crear.**

   :::image type="content" source="../assets/images/collaboration-control/collaboration-manager-for-inspection.png" alt-text="La captura de pantalla es un ejemplo que muestra el administrador de colaboración para la inspección.":::

1. Seleccione **Agregar página.**

1. Seleccione **Vista basada en tabla y formulario.**

   :::image type="content" source="../assets/images/collaboration-control/table-based.png" alt-text="La captura de pantalla es un ejemplo que muestra la vista basada en tabla y el formulario.":::

1. Seleccione **Siguiente.**

1. Busque y seleccione la tabla que ha creado anteriormente.

   :::image type="content" source="../assets/images/collaboration-control/table-view-form-pages.png" alt-text="La captura de pantalla es un ejemplo que muestra las páginas del formulario de vista de tabla.":::

1. Seleccione **Agregar.**

1. Seleccione **Publicar** para guardar y publicar la aplicación.

1. Seleccione **Reproducir** para probar la nueva aplicación.

Ahora ha creado correctamente una aplicación basada en modelos.

## <a name="add-collaboration-controls-to-your-application"></a>Adición de controles de colaboración a la aplicación

Estos son los pasos para agregar funcionalidades de control de colaboración como tareas, reuniones, archivos y experiencias de notas a la aplicación creada:

1. Para incluir las pestañas Tareas, Reuniones y Notas, debe editar el formulario Información principal. Para empezar, vuelva al explorador y seleccione la solución.

1. Seleccione la tabla que creó en [Crear una nueva aplicación controlada por modelos para Teams.](#create-a-new-model-driven-app-with-collaboration-controls-for-teams)

1. Vaya a la pestaña Formularios de la tabla.

     :::image type="content" source="../assets/images/collaboration-control/forms-tab.png" alt-text="La captura de pantalla es un ejemplo que muestra la pestaña formularios de la tabla.":::

1. Seleccione el formulario Información del tipo de formulario **Principal** para abrirlo en el diseñador de formularios.

1. Una vez que esté en el diseñador de formularios, presione y arrastre una **pestaña de 1 columna** desde la sección **Componentes** .

     :::image type="content" source="../assets/images/collaboration-control/components.png" alt-text="La captura de pantalla es un ejemplo que muestra los componentes de power apps.":::

1. Después de seleccionar la pestaña, cambie el nombre de la pestaña a "Tareas" en el panel de propiedades.

1. Seleccione el nombre de la pestaña para seleccionar la sección completa y seleccione **Expandir primer componente a pestaña completa** en el panel Propiedades. Esto es necesario, ya que los controles de colaboración se ven mejor en vistas de pestaña completas.

    :::image type="content" source="../assets/images/collaboration-control/tasks-pane.png" alt-text=" En la captura de pantalla se describe cómo seleccionar el primer componente en la pestaña completa.":::

     :::image type="content" source="../assets/images/collaboration-control/expand-first-component.png" alt-text=" En la captura de pantalla se describe cómo expandir el primer componente a la pestaña completa.":::

1. Expanda la categoría Colaboración (versión preliminar) en el cajón de controles y arrastre el control Tareas (versión preliminar) a la sección del formulario Tareas.

     :::image type="content" source="../assets/images/collaboration-control/collab-preview.png" alt-text="Vista previa del control en la sección en el formulario de tareas":::

3. Establezca la tabla en Actividades & seleccione Listo.

     :::image type="content" source="../assets/images/collaboration-control/select-table-activities.png" alt-text="Selección de la tabla a las actividades":::

5. Seleccione "Ocultar etiqueta" en propiedades.

     :::image type="content" source="../assets/images/collaboration-control/hide-label-properties.png" alt-text="Seleccionar ocultar etiqueta":::

1. Ahora se mostrará el control Tareas.

     :::image type="content" source="../assets/images/collaboration-control/new-collab-control.png" alt-text="Visualización del control de tareas":::

1. Repita los pasos de Tareas para agregar controles Aprobaciones, Archivos, Reuniones y Notas a la aplicación.
1. Una vez agregados todos los controles, verá los controles representados a continuación en el Diseñador de formularios. Si un control no se representa en el Diseñador de formularios, por ejemplo muestra un formulario en blanco, ejecute la aplicación en Power Apps y la presencia de una página "configurar" o un "estado vacío" significa que el control se agregó correctamente.

     :::image type="content" source="../assets/images/collaboration-control/new-collab-approval.png" alt-text="Diseñador de formularios de controles":::

1. Ahora puede ejecutar la aplicación de energía en Power Apps seleccionándola.

     :::image type="content" source="../assets/images/collaboration-control/collaboration-manager-for-inspections-power-apps.png" alt-text="Administrador de colaboración para inspecciones":::

1. Cree un nuevo registro seleccionando **+ Nuevo** y, a continuación, abra el registro.

     :::image type="content" source="../assets/images/collaboration-control/power-apps-open-the-record.png" alt-text="La captura de pantalla es un ejemplo que muestra las aplicaciones de energía que abren el registro.":::

1. Ahora puede ver las vistas de cada pestaña que aparecen de forma similar a la siguiente imagen:

     :::image type="content" source="../assets/images/collaboration-control/tabs.png" alt-text="La captura de pantalla es un ejemplo que muestra las tareas.":::

     > [!TIP]
     > Los controles solo están visibles después de guardar un registro en la aplicación. Si las pestañas de control no aparecen en el registro, intente actualizar el explorador o volver a publicar la aplicación desde Power Apps.

Ahora ha agregado correctamente los controles de colaboración a la aplicación. Ahora puede ejecutar la aplicación en Power Apps e iniciar los controles. Como aún no se ha configurado la configuración, no podrá crear entidades como Tareas o Reuniones hasta que se agreguen.

## <a name="define-settings-for-your-collaboration"></a>Definición de la configuración de la colaboración

Puede definir la configuración de los controles de colaboración para la entidad empresarial, como la tabla creada en una [nueva aplicación controlada por modelos](#create-a-new-model-driven-app-with-collaboration-controls-for-teams).

La configuración que puede aplicar es la siguiente:

|Configuración|Usada por|
|---|---|
|Id. de grupo|Tareas, reuniones internas, aprobaciones.|
|Id. de negocio de Bookings|Reuniones externas mediante Bookings |
|Id. de sitio|Archivos de SharePoint |
|Id. de unidad|Archivos de SharePoint|

> [!NOTE]
> La configuración es crtical para iniciar la aplicación, por lo que asegúrese de seguir los pasos sugeridos. Si tiene problemas para iniciar y guardar los controles, vuelva a comprobar los valores.

Para obtener el identificador de grupo, cree un nuevo equipo o use un equipo existente en Microsoft Teams para hospedar la aplicación y crear variables de configuración.

Para crear un nuevo equipo, consulte [Creación de un equipo desde cero](https://support.microsoft.com/en-us/office/create-a-team-from-scratch-174adf5f-846b-4780-b765-de1a0a737e2b).

Use las instrucciones siguientes para recuperar el identificador de grupo del equipo de Teams para aprobaciones, tareas y reuniones internas:

1. Busque el equipo en la lista de equipos.

1. Seleccione la elipse **...** y seleccione **Obtener vínculo al equipo**.

     :::image type="content" source="../assets/images/collaboration-control/get-link.png" alt-text="En la captura de pantalla se describe cómo obtener el vínculo al equipo.":::

1. Copie el vínculo y registre el valor de desde `groupId` la dirección URL. Usará este valor en una fase posterior al definir la configuración de la solución.

     `https://teams.microsoft.com/l/team/19%3akk_TuKhjXu92yJvg4TZ10S6rouLSCgvHIb5NOOTfRjg1%40thread.tacv2/conversations?groupId=4310f270-1aa5-4089-99f3-47eb3b4d69ad&tenantId=b699419b-e0df-47e3-9909-24076fdcf68b`

Use las instrucciones siguientes para recuperar el identificador de sitio de SharePoint y el identificador de unidad para archivos:

1. Para usar el control Archivos, deberá configurar en un sitio de SharePoint existente o crear un nuevo sitio de SharePoint. Para crear un nuevo sitio, consulte [Creación de un sitio](/sharepoint/create-site-collection).

1. Ahora recupere los valores de configuración del identificador de sitio y del identificador de unidad, a los que se puede llamar con los detalles del sitio de SharePoint.

     1. **Id. de sitio**: con [el Explorador de Graph](https://developer.microsoft.com/graph/graph-explorer), inicie sesión y conceda permisos a Directory.ReadWrite.All y User.ReadWrite.All.

         :::image type="content" source="../assets/images/collaboration-control/graph-permissions.png" alt-text="La captura de pantalla es un ejemplo que muestra el Explorador de Graph.":::

     1. Asegúrese de reemplazar el nombre de host por el nombre de host y la ruta de acceso relativa a la ruta de acceso del sitio y realice una llamada de grafo a `https://graph.microsoft.com/v1.0/sites/{hostname}:/{relative-path-to-site}`. A continuación se muestra un ejemplo:
         1. Si la dirección URL del sitio = <https://myhostname.sharepoint.com/sites/MySiteName>
         1. Hostname = myhostname.sharepoint.com
         1. Ruta de acceso relativa al sitio = sites/MySiteName

              :::image type="content" source="../assets/images/collaboration-control/graph-call.png" alt-text="La captura de pantalla es un ejemplo que muestra la llamada a Graph.":::

            La llamada de grafo sería , `https://graph.microsoft.com/v1.0/sites/myhostname.sharepoint.com:/sites/MySiteName`.

     1. La respuesta recibida es un objeto Json que representa el sitio; por ejemplo, el identificador de sitio sería `abcdef.sharepoint.com,0abe7394-6fce-4dcc-9884-7eaceb48cd41,8cb86762-16cd-495e-87cb-893cfdf94054`.

     1. Guarde el parámetro de valor id. de sitio.

     1. **Id. de unidad**: con [el Explorador de Graph](https://developer.microsoft.com/graph/graph-explorer), inicie sesión y realice la llamada al `https://graph.microsoft.com/v1.0/sites/{site-id}/drives` grafo con el valor de Id. de sitio que guardó anteriormente.

     1. Se devuelve una respuesta Json con un valor de parámetro de matriz de tipos o lista de objetos de unidad. Busque en json el objeto Json cuyo parámetro name coincide con el nombre de la biblioteca de documentos. Guarde el valor del parámetro Id. de unidad.

Para crear reuniones con usuarios fuera de la organización, como clientes y usar características de visita virtual dentro de la aplicación, tendría que proporcionar una empresa de Bookings. Para obtener más información, consulte [Microsoft Bookings](/microsoft-365/bookings/bookings-overview?view=o365-worldwide&preserve-view=true).

## <a name="add-settings-to-your-collaboration-manager-app"></a>Agregar configuración a la aplicación de Collaboration Manager

Para aplicar la configuración y explorar las características de colaboración de la aplicación en Power Apps, abra la aplicación que creó anteriormente. Verá una página de vista, donde puede seleccionar los registros existentes o crear uno nuevo. Para empezar con abrir o crear un registro.

Tendría que agregar los identificadores de configuración que guardó anteriormente para la aplicación.

|Configuración|Usada por|
|---|---|
|Id. de grupo|Tareas, reuniones internas, aprobaciones.|
|Id. de negocio de Bookings|Reuniones externas mediante Bookings |
|Id. de sitio|Archivos de SharePoint |
|Id. de unidad|Archivos de SharePoint|

### <a name="add-settings-for-tasks-meetings-and-files"></a>Agregar configuración para tareas, reuniones y archivos

1. Inicie un control y puede ver una ventana como sigue:

     :::image type="content" source="../assets/images/collaboration-control/launch-window.png" alt-text="La captura de pantalla es un ejemplo que muestra la ventana de control.":::

1. Seleccione **Configurar** y vaya a la pestaña General para agregar el identificador de grupo.

     :::image type="content" source="../assets/images/collaboration-control/groupid-general.png" alt-text="En la captura de pantalla se describe cómo agregar el identificador de grupo en la pestaña General.":::

1. Abra la pestaña Archivos para agregar el identificador de sitio y el identificador de unidad.

     :::image type="content" source="../assets/images/collaboration-control/files-tab.png" alt-text="En la captura de pantalla se describe cómo agregar el identificador de sitio y el identificador de unidad en la pestaña de archivos.":::

El control Notes no requiere un valor de configuración. Ahora puede crear entidades como Tareas y reuniones en la aplicación. Si tiene problemas al iniciar y guardar los controles, vuelva a comprobar los valores de configuración.

## <a name="explore-your-new-collaboration-manager-app"></a>Explorar la nueva aplicación de Collaboration Manager

Las secciones siguientes le guían sobre cómo usar los controles Tarea, Notas, Reuniones, Archivos y Aprobaciones.

### <a name="create-tasks"></a>Crear tareas

Explore la colaboración en la pestaña Tareas; para ello, seleccione la pestaña Tareas, que abre una página vacía donde los usuarios pueden agregar todas las tareas pertinentes que necesitan completar.

1. Para crear una nueva tarea para el equipo, seleccione **Agregar una tarea**. Se abre un cuadro de diálogo en el que puede proporcionar detalles sobre la tarea y asignarla a las personas pertinentes del equipo y seleccionar Guardar.

     :::image type="content" source="../assets/images/collaboration-control/add-task.png" alt-text="En la captura de pantalla se describe cómo agregar una tarea.":::

1. La tarea guardada aparecerá en la lista de tareas.

1. Dado que todas las tareas están respaldadas por Microsoft Planner. Los usuarios pueden usar la aplicación Tareas en Microsoft Teams para ver todas las tareas asignadas. Para empezar, seleccione puntos suspensivos **...** en el panel izquierdo de Teams. Busque y seleccione Tareas por planner y Tareas pendientes.

     :::image type="content" source="../assets/images/collaboration-control/tasks-planner.png" alt-text="La captura de pantalla es un ejemplo de tareas de Planner y Tareas pendientes.":::

1. Después de abrir la aplicación Tareas de Planner y Tareas pendientes, los usuarios pueden ver todas las tareas que se crearon en la aplicación en la sección **Asignado a mí** de la aplicación. Los usuarios también pueden ver los detalles de una tarea, agregar datos adjuntos y marcarlos como completados.

### <a name="create-notes"></a>Crear notas

Para crear una nota, seleccione la pestaña **Notas** de la aplicación, que se redirigirá a una pantalla vacía donde los usuarios pueden proporcionar cualquier información relevante. Para agregar una nueva nota, seleccione **Nueva nota**.
Después de agregar los detalles pertinentes en las notas, seleccione **Guardar**.

### <a name="create-meetings"></a>Crear reuniones

Seleccione **la pestaña Reuniones** en un registro para programar reuniones internas y externas.

Para programar una reunión interna, seleccione la lista desplegable situada junto al botón **Nueva reunión** y, a continuación, seleccione **Reunión interna**.

:::image type="content" source="../assets/images/collaboration-control/new-meeting-tab.png" alt-text="En la captura de pantalla se describe cómo programar reuniones internas.":::

> [!NOTE]
>
> La reserva de clientes está habilitada, si ha configurado Microsoft Booking con una configuración válida para la aplicación.

En el cuadro de diálogo **Nueva reunión** , los usuarios pueden proporcionar información relevante sobre la reunión y seleccionar **Guardar**. La reunión aparece en la lista de reuniones.

:::image type="content" source="../assets/images/collaboration-control/new-meeting.png" alt-text="En la captura de pantalla se describe cómo programar una nueva reunión.":::

Para programar una reunión externa con el cliente, seleccione la lista desplegable situada junto al botón **Nueva reunión** y seleccione **Reserva de clientes**. Si la opción **Reserva de clientes** no está disponible en la lista desplegable **Nueva reunión**, confirme si la aplicación está configurada para Microsoft Bookings en configuración y el usuario tiene el rol Administrador de Bookings. Para obtener más información, consulte [Agregar personal a Bookings](/microsoft-365/bookings/add-staff?view=o365-worldwide&preserve-view=true). Puede agregar tipos de reserva adicionales agregando servicios adicionales dentro de su empresa de Bookings.

:::image type="content" source="../assets/images/collaboration-control/customer-booking.png" alt-text="En la captura de pantalla se describe cómo programar reservas de clientes.":::

Los usuarios pueden ver tanto las reuniones internas como las reservas de clientes en su lista de reuniones. Una vez iniciada la reunión, los usuarios pueden unirse seleccionando el botón **Unirse** , que abre la reunión directamente en Microsoft Teams.

A medida que Outlook respalda las reuniones, los usuarios pueden navegar a Bookings o Calendario de Outlook para ver todas las reuniones enumeradas en un solo calendario. Las reuniones internas aparecen en el calendario compartido.

A continuación se indican los pasos para agregar un calendario compartido a Outlook (opcional):

1. En la pestaña Inicio de la cinta de opciones, en la sección Administrar calendarios, seleccione Abrir calendario > Abrir calendario compartido.

1. En el cuadro de diálogo Abrir un calendario compartido , escriba el nombre de la persona. Seleccione la persona que está buscando y, a continuación, seleccione Aceptar.

En el panel izquierdo, en Calendarios compartidos ahora debería ver un calendario adicional con el nombre de la persona.

:::image type="content" source="../assets/images/collaboration-control/customer-booking.png" alt-text="En la captura de pantalla se describe cómo programar reservas de clientes.":::

### <a name="add-files"></a>Agregar archivos

Abra la pestaña **Archivos** de la aplicación y seleccione **Cargar** para cargar archivos desde OneDrive para la Empresa o desde el equipo. Cuando un archivo se carga correctamente, la vista de lista principal se actualiza automáticamente para mostrar los archivos de la lista.

:::image type="content" source="../assets/images/collaboration-control/meeting-calendar.png" alt-text="En la captura de pantalla se describe cómo abrir el calendario compartido.":::

### <a name="approvals"></a>Aprobaciones

Las aprobaciones permiten a los usuarios solicitar el cierre de sesión de otros usuarios cuando trabajan en un registro. Por ejemplo, solicite una aprobación para completar una tarea o cerrar un registro.

1. Vaya a la pestaña **Aprobaciones** de la aplicación.

1. Cuando no hay solicitudes de aprobación, los usuarios ven la siguiente pantalla.

      :::image type="content" source="../assets/images/collaboration-control/no-approvals.png" alt-text="La captura de pantalla es un ejemplo que no muestra ninguna solicitud de aprobación.":::

1. Seleccione la **nueva solicitud de aprobación** para abrir el formulario de solicitud de aprobación.

      :::image type="content" source="../assets/images/collaboration-control/approval-request-form.png" alt-text="La captura de pantalla es un ejemplo que muestra el nuevo formulario de solicitud de aprobación.":::

1. En el formulario Solicitud de aprobación, rellene los campos necesarios y seleccione **Enviar**, que crea una solicitud y se agrega a la lista.

      :::image type="content" source="../assets/images/collaboration-control/approvals-list.png" alt-text="La captura de pantalla es un ejemplo que muestra la lista de aprobaciones.":::

1. Seleccione la aprobación para ver los detalles.

Para obtener más información sobre las aprobaciones, consulte [Creación de una aprobación](https://support.microsoft.com/en-us/office/create-an-approval-6548a338-f837-4e3c-ad02-8214fc165c84).
