---
title: Power Automate en la aplicación de control de colaboración
author: surbhigupta
description: En este módulo, obtenga información sobre Power Automate en la aplicación de control de colaboración en Microsoft Teams y cómo crear una aplicación de Azure.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: deda9f0178c51410e2208e81263b315de4ca1da4
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179325"
---
# <a name="power-automate"></a>Power Automate

Power Automate se puede usar para automatizar flujos de trabajo en torno a la aplicación de Collaboration Manager. Por ejemplo, cree automáticamente tareas cuando se cree un nuevo registro.

El conector de control de colaboración permite a los desarrolladores acceder a las API de control de colaboración mediante desencadenadores o acciones en flujos de trabajo automatizados en Microsoft Power Automate, Microsoft Power Apps y Azure Logic Apps.

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

En esta versión, el conector permite a los creadores configurar desencadenadores:

1. Cuando se crea una sesión de colaboración.
1. Cuando se crea o modifica una tarea de Planner.

También incluye un conjunto de API y tareas de controles de colaboración que se pueden invocar con un flujo. Las acciones del conector se encuentran en las selecciones de pasos de flujo de trabajo. El propio conector se encontraría en conectores personalizados con opciones configurables. Para usar el conector en la solución, es necesario crear un App de Azure de confianza para el entorno para ejecutar los flujos.

## <a name="create-an-azure-app"></a>Creación de un App de Azure

En el [Azure Portal](https://ms.portal.azure.com/#home) para la administración de Azure Active Directory, inicie sesión en su cuenta con los permisos adecuados para agregar una aplicación de usuario al entorno con los pasos siguientes:

1. En la página principal de Azure Portal, seleccione **Azure Active Directory**. En Azure Active Directory, seleccione la lista desplegable **Agregar** y seleccione **Registro de aplicaciones**.

   :::image type="content" source="../assets/images/collaboration-control/azure-active-directory-home-portal.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo agregar un nuevo registro de aplicaciones":::

   :::image type="content" source="../assets/images/collaboration-control/new-app-registration.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo agregar un nuevo registro de aplicaciones":::

1. En el registro de la aplicación, establezca el nombre de la aplicación y agregue el URI de redirección web a `https://global.consent.azure-apim.net/redirect`.

   :::image type="content" source="../assets/images/collaboration-control/register-an-application.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo registrar una aplicación":::

1. En la sección Concesión implícita y flujos híbridos, seleccione tokens de acceso y tokens de identificador.

   :::image type="content" source="../assets/images/collaboration-control/authorisation-endpoint-tokens.png" alt-text="La captura de pantalla es un ejemplo que muestra los tokens y los tokens de identificador":::

1. Seleccione Permiso de API en el panel izquierdo, seleccione **Agregar un permiso** y, a continuación, busque **Permiso de CRM dinámico** .

   :::image type="content" source="../assets/images/collaboration-control/dynamic-crm.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo agregar un permiso":::

1. Asegúrese de seleccionar **user_impersonation** en Permisos después de seleccionar Dynamics CRM.

   :::image type="content" source="../assets/images/collaboration-control/admin-consent-required.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo habilitar la casilla user_impersonation":::

1. En la página Certificados & secretos, agregue un **nuevo secreto de cliente** y guarde el valor para usarlo más adelante al configurar la seguridad del conector.

   :::image type="content" source="../assets/images/collaboration-control/copy-new-secret-value.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo copiar un nuevo valor secreto":::

1. En la página Información general de la aplicación, copie el **identificador de aplicación (cliente)** y guárdelo para usarlo más adelante al configurar la seguridad del conector.

   :::image type="content" source="../assets/images/collaboration-control/application-client-ID.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo guardar el identificador de cliente":::

Ahora la aplicación de Azure está establecida y debe agregarla como una aplicación de usuario en su entorno.

## <a name="add-azure-app-to-power-automate-environment"></a>Incorporación de una aplicación de Azure al entorno de Power Automate

1. Abra el portal de Power Apps, en la esquina superior derecha, seleccione **configuración** y abra **Administración centro**.

   :::image type="content" source="../assets/images/collaboration-control/power-apps-interface.png" alt-text="La captura de pantalla es un ejemplo que muestra la interfaz de Power Apps":::

1. En el centro de administración, seleccione **Entorno** en el panel izquierdo y seleccione el entorno en la lista que desea agregar a la aplicación del conector.

   :::image type="content" source="../assets/images/collaboration-control/power-platform-admin-center.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo agregar una aplicación conector":::

1. En la página de detalles del entorno, seleccione **Configuración**.

   :::image type="content" source="../assets/images/collaboration-control/settings-environment.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo seleccionar la configuración":::

1. En la página de detalles de configuración, seleccione **la sección Usuarios y permisos** y seleccione **Usuarios de la aplicación**.

   :::image type="content" source="../assets/images/collaboration-control/users-link.png" alt-text="La captura de pantalla es un ejemplo que muestra el vínculo de usuario de la aplicación":::

1. En la página Usuarios de la aplicación, seleccione + **Nuevo usuario de la aplicación**. **Aparece la ventana Crear un nuevo usuario de aplicación** .

   :::image type="content" source="../assets/images/collaboration-control/new-app-user.png" alt-text="La captura de pantalla es un ejemplo que muestra el nuevo usuario de la aplicación.":::

1. Seleccione **+ Agregar una aplicación**.

   :::image type="content" source="../assets/images/collaboration-control/create-new-app-user.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo crear un nuevo usuario de aplicación":::

1. Seleccione la aplicación en el cuadro de búsqueda y seleccione Agregar de nuevo.

   :::image type="content" source="../assets/images/collaboration-control/add-app-aad.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo agregar una aplicación desde Azure Active Directory":::

Una vez agregada la aplicación, establezca la **unidad de negocio** y **los roles de seguridad** en la aplicación del conector. Seleccione **Crear** y la aplicación estará en la lista. Con el usuario de la aplicación establecido en el entorno, podemos continuar con la configuración del conector personalizado.

## <a name="custom-connector-configuration"></a>Configuración del conector personalizado

1. Abra PowerApps o Power Automate y seleccione el menú **Conectores personalizados** . Seleccione **Editar** para el conector de colaboración.

   :::image type="content" source="../assets/images/collaboration-control/collaboration-connector.png" alt-text="menú del conector personalizado":::

1. En la pestaña Información general, escriba el host con la dirección del dominio de instancia dinámica 365 (sin el https://).

   :::image type="content" source="../assets/images/collaboration-control/general-information.png" alt-text="La captura de pantalla es un ejemplo que muestra la información general":::

1. En la pestaña Seguridad, escriba las siguientes entradas:

   * Secreto de cliente: use el valor del secreto de aplicación guardado en la entrada.
   * Id. de cliente: la aplicación de Azure (id. de cliente).
   * Dirección URL del recurso: dirección URL de la instancia dinámica de 365 (`https://org.crm.dynamics.com/`).
   * Ámbito: igual que anteriormente con. Sufijo predeterminado (`https://org.crm.dynamics.com/.default`).

   :::image type="content" source="../assets/images/collaboration-control/dynamic-365-instance.png" alt-text="La captura de pantalla es un ejemplo que muestra la instancia de Dynamic 365.":::

1. Seleccione **Actualizar conector** para guardar los cambios y permitir que el flujo establezca conexiones.

   :::image type="content" source="../assets/images/collaboration-control/custom-connector.png" alt-text="captura de pantalla de él es un ejemplo que muestra el conector personalizado.":::

## <a name="how-to-invoke-the-connector"></a>Cómo invocar el conector  

Los desencadenadores y las acciones se definen previamente con entrada y salida configurables como un paso de flujo de trabajo. Agregar el paso de flujo de trabajo a la posición de flujo de trabajo adecuada con la configuración de entrada y salida correcta para definir cuándo se va a invocar el desencadenador o la acción.

  :::image type="content" source="../assets/images/collaboration-control/invoke-the-connector.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo invocar el conector.":::

### <a name="triggers-and-actions-supported-with-connector"></a>Desencadenadores y acciones compatibles con el conector

Los siguientes desencadenadores y acciones se admiten dentro de un flujo:

* **Desencadenantes**

  1. Cuando se crea una sesión de colaboración.

      :::image type="content" source="../assets/images/collaboration-control/colab-session-created-preview.png" alt-text="Sesión de colaboración creada":::

      **Alcance:** Ámbito que se va a limitar, que filas pueden desencadenar el flujo.

      **Ejecute como:** El usuario en ejecución para los pasos en los que se usan las conexiones de invocador.

  1. Cuando se crea o modifica una tarea

      :::image type="content" source="../assets/images/collaboration-control/task-created.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo se crea o modifica la tarea.":::

      De forma predeterminada, la tarea de planner del desencadenador se deshabilitará y no se desencadenará. Para habilitarlo, el administrador de inquilinos debe completar los pasos siguientes:

      * Cree una incidencia de soporte técnico en la ruta de acceso Power Apps/Controles de colaboración/Configuración.
      * Solicite que el entorno esté habilitado para el conector de colaboración y proporcione la dirección URL del entorno (preferida) o el identificador de la organización.  
      * Puede agregar el siguiente texto de ejemplo a la solicitud de soporte técnico: "Enable Environment URL: `url` for the Collaboration Connector".
      * Para abrir una incidencia de soporte técnico, consulte [Obtener ayuda y soporte técnico](/power-platform/admin/get-help-support).

* **Acciones**

  1. Inicio de la sesión de colaboración

      :::image type="content" source="../assets/images/collaboration-control/begin-collab-session.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo iniciar la sesión de colaboración":::

     Esta acción de paso crea una nueva sesión de colaboración para la entidad empresarial dataverse:

      * **Nombre de la aplicación:** El nombre de la aplicación asociada, por ejemplo, podría ser "Collaboration Manager para préstamos" o "Collaboration Manager para la auditoría de préstamos cerrados".
      * **Nombre de entidad raíz de colaboración:** El tipo de registro de aplicación (nombre de tabla), por ejemplo, podría ser "msfi_loanapplication" para una Collaboration Manager para la aplicación De préstamos.
      * **Identificador de entidad raíz de colaboración:** Identificador del registro de aplicación asociado, por ejemplo, podría ser el identificador de un registro de solicitud de préstamo.  

      ***Opciones avanzadas***

      **Metadatos (avanzados):** Agrega metadatos para una sesión de colaboración.

        * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
        * **Llave:** Clave asociada al atributo de metadatos.
        * **Valor:** Valor asociado al atributo de metadatos.

  1. Recuperar sesión de colaboración

      ::image type="content" source=".. /assets/images/collaboration-control/retrieve-collab-session.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo recuperar la sesión de colaboración."::

     Esta acción de paso devuelve la sesión de colaboración que coincide con las entradas proporcionadas:

     * **Nombre de la aplicación:** Contexto del nombre de la aplicación para la sesión de colaboración.
     * **Identificador de entidad raíz de colaboración:** Identificador de entidad empresarial para la sesión de colaboración.  
     * **Nombre de entidad raíz de colaboración:** Tipo de entidad de negocio para la sesión de colaboración.

  1. Actualización de la sesión de colaboración

      :::image type="content" source="../assets/images/collaboration-control/update-collab-session.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo actualizar la sesión de colaboración.":::

     Esta acción de paso actualiza una sesión de colaboración existente:

     * **Identificador raíz de colaboración:** GUID para el registro raíz o sesión de colaboración de destino.
     * **Identificador de entidad raíz de colaboración:** Identificador de entidad empresarial al que hace referencia la sesión de colaboración.
     * **Nombre de entidad raíz de colaboración:** Nombre de tipo de entidad empresarial al que hace referencia la sesión de colaboración.

     ***Opciones avanzadas:***

      **Crear metadatos (avanzado):** Agrega más metadatos a un registro de sesión de colaboración.

      * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
      * **Llave:** Clave asociada al atributo de metadatos.
      * **Valor:** Valor asociado al atributo de metadatos.

      **Actualizar metadatos (avanzado):** Novedades metadatos existentes en un registro de sesión de colaboración.

      * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
      * **Llave:** Clave asociada al atributo de metadatos que se va a actualizar.
      * **Valor:** Valor asociado al atributo de metadatos.

      **Eliminar metadatos (avanzado):** Quita los metadatos existentes en un registro de sesión de colaboración.

      * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
      * **Llave:** Clave asociada al atributo de metadatos que se va a quitar.

  1. Asociar mapa de colaboración (externo)

      :::image type="content" source="../assets/images/collaboration-control/associate-collab-map.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo asociar el mapa de colaboración.":::

     Esta acción de paso crea una asignación de una entidad de colaboración externa (fuera del dataverse) con la sesión de colaboración:

     * **Identificador raíz de colaboración:** Identificador único de la sesión de colaboración que se va a asignar a una entidad de colaboración.
     * **Identificador externo del mapa de colaboración:** Identificador de recurso de colaboración externo que se va a asignar.
     * **Nombre de entidad del mapa de colaboración:** Nombre del tipo de entidad de colaboración externa que se va a asignar.

     ***Opciones avanzadas:***

     **Metadatos:** Agregue metadatos para un mapa de colaboración.
     * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
     * **Llave:** Clave asociada al atributo de metadatos.
     * **Valor:** Valor asociado al atributo de metadatos.

  1. Asociar mapa de colaboración (interno)

      :::image type="content" source="../assets/images/collaboration-control/associate-collab-map-internal.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo asociar el mapa de colaboración interno.":::

     Esta acción de paso crea una asignación de una entidad de colaboración (tabla de dataverse) con la sesión de colaboración. Las instancias internas están diseñadas para crear asignaciones entre las entidades o tablas internas de Dataverse.

     * **Identificador raíz de colaboración:** Identificador único de la sesión de colaboración que se va a asignar a una entidad de colaboración.
     * **Id. de entidad del mapa de colaboración:** Identificador de entidad de colaboración de Dataverse que se va a asignar.
     * **Nombre de entidad del mapa de colaboración:** Nombre del tipo de entidad de colaboración Dataverse que se va a asignar.

     ***Opciones avanzadas:***

     **Metadatos (avanzados)** Agregue metadatos para un mapa de colaboración.

     * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata
     * **Llave:** Clave asociada al atributo de metadatos
     * **Valor:** Valor asociado al atributo de metadatos

  1. Actualizar mapa de colaboración

      :::image type="content" source="../assets/images/collaboration-control/update-collab-map.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo actualizar el mapa de colaboración.":::

     Esta acción de paso actualiza un mapa de colaboración existente:

     * **Identificador de mapa de colaboración:** Identificador único del mapa de colaboración que se va a actualizar.
     * **Id. de entidad del mapa de colaboración:** Identificador de entidad de colaboración que se va a asignar. Este valor debe estar vacío si se proporciona el identificador externo.
     * **Nombre de entidad del mapa de colaboración**
     * **Identificador externo del mapa de colaboración:** Identificador de recurso de colaboración externo que se va a asignar. Este valor debe estar vacío si se proporciona el identificador de entidad.  

     ***Opciones avanzadas:***

     **Crear metadatos:** Agrega más metadatos a un registro de mapa de colaboración.

     * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
     * **Llave:** Clave asociada al atributo de metadatos.
     * **Valor:** Valor asociado al atributo de metadatos.

     **Actualizar metadatos:** Novedades metadatos existentes en un registro de mapa de colaboración.

     * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata
     * **Llave:** Clave asociada al atributo de metadatos que se va a actualizar
     * **Valor:** Valor asociado al atributo de metadatos

     **Eliminar metadatos:** Quita los metadatos existentes en un registro de mapa de colaboración.

     * **Tipo OData:** Este campo debe proporcionarse si se establece la otra clave o valor y debe coincidir exactamente con #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
     * **Llave:** Clave asociada al atributo de metadatos que se va a quitar.

  1. Obtener metadatos de colaboración

      :::image type="content" source="../assets/images/collaboration-control/get-collab-metadata.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo obtener metadatos de colaboración.":::

     En esta acción de paso se enumeran todos los metadatos que coinciden con el filtro especificado.

     **Filtro:** Filtro que se va a aplicar a la consulta de metadatos.
     Ejemplo de recuperación de todos los metadatos relacionados con un identificador de entidad de mapa de colaboración  
     m365_entityname eq 'm365_collaborationmap' y m365_entityid eq 'GUID'

  1. Crear tarea de Planner

      :::image type="content" source="../assets/images/collaboration-control/create-planner-task.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo crear una tarea de planner.":::

     Esta acción de paso crea una tarea de Graph Planner mediante controles de colaboración Tabla virtual de tareas de Planner:

     * **Identificador raíz de colaboración (obligatorio):** Identificador único de sesión de colaboración
     * **Id. del plan (obligatorio):** Identificador de plan al que pertenece la tarea
     * **Título (obligatorio):** Título de la tarea
     * **Asignaciones:** Objeto con formato JSON que representa todas las asignaciones de una tarea. Consulte el [tipo de recurso plannerAssignments](/graph/api/resources/plannerassignments).
     * **Id. de bucket:** Id. de bucket al que pertenecen las tareas.
     * **Prioridad:** Prioridad de la tarea. 0 y 10 (inclusive) el valor creciente es menor prioridad.

     ***Opciones avanzadas:***

     * **Número activo de elementos de lista de comprobación** (avanzado): número de elementos de lista de comprobación con el valor establecido en false que representa elementos incompletos.
     * **Categorías aplicadas:** Objeto de formateador json que representa todas las categorías que se van a aplicar a la tarea. Consulte el [tipo de recurso plannerAppliedCategories](/graph/api/resources/plannerappliedcategories).
     * **Prioridad de asignado:** Sugerencias de valor de cadena usadas para ordenar elementos de este tipo en una vista de lista. Consulte [el uso de sugerencias de pedido en Planner](/graph/api/resources/planner-order-hint-format).
     * **Recuento de elementos de lista de comprobación:** Número de elementos de lista de comprobación que están presentes en la tarea.
     * **Completado por:** Objeto con formato JSON que representa la identidad del usuario que completó la tarea. Consulte tipo [de recurso identitySet](/graph/api/resources/identityset).
     * **Identificador de subproceso de conversación:** Identificador de subproceso de la conversación en la tarea. Este es el identificador del objeto de subproceso de conversación creado en el grupo.
     * **Creado por:** Objeto con formato JSON que representa la identidad del usuario que creó la tarea. Consulte tipo [de recurso identitySet](/graph/api/resources/identityset).
     * **Fecha de vencimiento:** Fecha y hora a la que vence la tarea. El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z.
     * **Sugerencia de pedido:** Sugerencia usada para ordenar elementos de este tipo en una vista de lista. El formato se define como se describe en [el uso de sugerencias de orden en Planner](/graph/api/resources/planner-order-hint-format).
     * **Porcentaje completado:** Porcentaje de finalización de tareas (0-100)
     * **Tipo de vista previa:** Esto establece el tipo de vista previa que aparece en la tarea. Los valores posibles son: automatic, noPreview, checklist, description, reference.
     * **Recuento de referencias:** Número de referencias externas que existen en la tarea.
     * **Hora de la fecha de inicio:** Fecha y hora en que se inicia la tarea. El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z.

  1. Obtener tarea de Planner

      :::image type="content" source="../assets/images/collaboration-control/get-planner-task.png" alt-text="La captura de pantalla es un ejemplo que muestra la tarea get planner.":::

     Esta acción de paso devuelve datos de tareas de Planner mediante controles de colaboración Tabla virtual de tareas de Planner:

     **Identificador de tarea (obligatorio):** Identificador único de tarea

  1. Tarea Update Planner

      :::image type="content" source="../assets/images/collaboration-control/update-planner-task-preview.png" alt-text="Tarea De actualización de Planner":::

     Esta acción de paso actualiza un registro de tareas de Planner mediante controles de colaboración Tabla virtual de tareas de Planner

     * **Identificador de tarea (obligatorio):** Identificador único de tarea.
     * **Asignaciones:** Objeto con formato JSON que representa todas las asignaciones de una tarea. Ver. Tipo de recurso plannerAssignments: Microsoft Graph v1.0 | Microsoft Docs  
     * **Id. de bucket:** Id. de cubo al que pertenece la tarea.  
     * **Detalles de la tarea de Planner:** Representa la información adicional sobre una tarea.
     * **Fecha de vencimiento:** Fecha y hora a la que vence la tarea. El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z.
     * **Prioridad:** Prioridad de la tarea. 0 y 10 (inclusive) el valor creciente es menor prioridad.  
     * **Porcentaje completado:** Porcentaje de finalización de tareas (0-100)
     * **Título:** Título de la tarea

     ***Opciones avanzadas:***

     * **Categorías aplicadas:** Objeto con formato JSON que representa todas las categorías que se van a aplicar a la tarea. Consulte el [tipo de recurso plannerAppliedCategories](/graph/api/resources/plannerappliedcategories).
     * **Prioridad de asignado:** Sugerencias de valor de cadena usadas para ordenar elementos de este tipo en una vista de lista. Consulte [el uso de sugerencias de pedido en Planner](/graph/api/resources/planner-order-hint-format).
     * **Identificador de subproceso de conversación:** Identificador de subproceso de la conversación en la tarea. Este es el identificador del objeto de subproceso de conversación creado en el grupo.
     * **Identificador raíz de colaboración:** Identificador único de la sesión de colaboración.
     * **Sugerencia de pedido:** Sugerencia usada para ordenar elementos de este tipo en una vista de lista. El formato se define como esquema aquí.
     * **Hora de la fecha de inicio:** Fecha y hora en que se inicia la tarea. El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z.

**Escenario de flujo de ejemplo**

A continuación se muestra un ejemplo de flujos:

1. Obtener una respuesta de Microsoft Forms, crear una sesión de colaboración y una tarea asociada.

   :::image type="content" source="../assets/images/collaboration-control/response-submitted.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo enviar una nueva respuesta.":::

1. Cada vez que se crea una sesión de colaboración, captura los detalles y envía una notificación por correo electrónico.

   :::image type="content" source="../assets/images/collaboration-control/colab-session-created-preview.png" alt-text="La captura de pantalla es un ejemplo que muestra la sesión de colaboración creada":::

> [!NOTE]
> Se pueden desencadenar varios flujos de esta manera para realizar diferentes acciones, utilizando datos de la respuesta de la creación de la sesión de colaboración.
