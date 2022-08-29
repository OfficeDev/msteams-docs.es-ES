---
title: Tablas virtuales para tareas, reuniones y archivos en la aplicación de control de colaboración
author: surbhigupta
description: En este módulo, obtenga información sobre las tablas virtuales para tareas, reuniones y archivos en la aplicación de control de colaboración en Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 1913b379e9f24d36948a05190a4ae1804a8ec728
ms.sourcegitcommit: 442d2c8e80a2605b6d0215c973557471f18f8121
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/11/2022
ms.locfileid: "67314598"
---
# <a name="virtual-tables-for-tasks-meetings-files"></a>Tablas virtuales para tareas, reuniones, archivos

Una nueva funcionalidad con esta versión es un conjunto de tablas virtuales. Esto permite a los desarrolladores interactuar con Graph a través de las API de OData.

La solución principal controles de colaboración incluye un conjunto de [tablas virtuales](/power-apps/developer/data-platform/virtual-entities/get-started-ve), que se pueden usar para el acceso mediante programación a los datos creados por los controles de colaboración.

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

> [!TIP]
> [Las tablas virtuales](/power-apps/developer/data-platform/virtual-entities/get-started-ve) también conocidas como entidades virtuales permiten la integración de datos que residen en sistemas externos al representar sin problemas esos datos como tablas en Microsoft Dataverse, sin replicación de datos y, a menudo, sin codificación personalizada.

El sistema externo que usan los controles de colaboración es Microsoft Graph. Hay tablas virtuales para eventos de calendario de grupo, citas de reserva, planes o tareas del planificador y unidades, carpetas y archivos de SharePoint.

En este artículo se proporcionan ejemplos que muestran cómo acceder a las tablas virtuales mediante la API REST de Dataverse para realizar operaciones CRUD (crear, leer, actualizar y eliminar).

> [!TIP]
> Para obtener más información sobre la API REST de Dataverse, consulte [Uso de la API web de Microsoft Dataverse](/power-apps/developer/data-platform/webapi/overview).

* Las tablas virtuales usan la API web de Dataverse estándar, lo que facilita el uso de las tablas virtuales para rellenar los datos de la aplicación.
* Las tablas virtuales implementan flujos de trabajo complejos necesarios para admitir controles de colaboración y se ejecutan en centros de datos de Microsoft para obtener un rendimiento óptimo.  
* Las tablas virtuales usan las funcionalidades estándar de registro y supervisión de Dataverse.

Después de instalar los controles de colaboración, las tablas virtuales se pueden tratar como otro servicio para la aplicación del que puede depender.

:::image type="content" source="~/assets/images/collaboration-control/vt-overview.png" alt-text="Introducción a las tablas virtuales":::

**Requisitos previos**

Para seguir este artículo, necesitará:

1. Entorno de Dataverse donde se han instalado los controles de colaboración.
1. Una cuenta de usuario en el entorno de Dataverse, que tiene asignado el rol **Usuario de controles de colaboración** .
1. Una herramienta de terceros, por ejemplo: Publicar el hombre o algún código de C# personalizado que le permita autenticarse en instancias de Microsoft Dataverse y redactar y enviar solicitudes de API web y ver respuestas.  

> [!TIP]
> Microsoft proporciona información sobre cómo configurar un entorno de Postman que se conecta a la instancia de Dataverse y cómo usar Postman para realizar operaciones con la API web. Consulte [Uso de Postman con Microsoft Dataverse Web API](/power-apps/developer/data-platform/webapi/use-postman-web-api).

## <a name="virtual-tables-sample-scenario"></a>Escenario de ejemplo de tablas virtuales

En el escenario descrito en esta guía se usan las tablas virtuales Plan de Planner y Tarea. El escenario descrito es el mismo que usa el control De colaboración de tareas. Desde la perspectiva del usuario, el escenario muestra cómo se crean un plan de Planner y varias tareas y se asocian a un registro empresarial específico. En el escenario se muestra cómo recuperar las tareas asociadas al registro empresarial y cómo leer, actualizar y eliminar una tarea de planner específica.

En el diagrama de secuencia siguiente se explica la interacción entre el cliente, que podría ser el control de colaboración Tareas, la [API de colaboración](/rest/api/industry/collaboration-controls/) y las tablas virtuales Plan de Planner y Tarea.

:::image type="content" source="~/assets/images/collaboration-control/vt-sequence.png" alt-text="Diagrama de secuencia para tablas virtuales":::

## <a name="virtual-tables-basic-operations"></a>Operaciones básicas de tablas virtuales

En esta sección se describen las solicitudes y respuestas HTTP para cada paso del escenario de ejemplo.

**Tarea 1: Recuperar el identificador de grupo**

Recupere el identificador de grupo usado en [la configuración de la colaboración](~/samples/app-with-collaboration-controls.md#define-settings-for-your-collaboration).

> [!NOTE]
> El usuario que use para crear el plan en las tareas posteriores debe ser miembro de este grupo. Si no es así, obtendrá la respuesta 403 Prohibido.

**Tarea 2: Inicio de una sesión de colaboración**

Una sesión de colaboración es un registro de la tabla raíz de colaboración, que permite asociar varias colaboraciones, por ejemplo, tareas, eventos, citas con un registro empresarial.

Una sesión de colaboración le permite realizar operaciones como una lista de los eventos de calendario asociados a un registro empresarial, por ejemplo, una aplicación de inspecciones.

# <a name="request"></a>[Solicitud](#tab/request)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_begincollaborationsession  
```

```json
{
    "applicationName": "{{applicationName}}", 
    "collaborationRootEntityId": "{{collaborationRootEntityId}}", 
    "collaborationRootEntityName": "{{entityName}}" 
}
```

* `applicationName`: nombre único de la aplicación
* `collaborationRootEntityName`: nombre de la entidad de registro empresarial  
* `collaborationRootEntityId`: clave principal (ID) del registro de negocio específico

# <a name="response"></a>[Respuesta](#tab/response)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.m365_begincollaborationsessionResponse", 
    "collaborationRootId": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
}
```

---

Realice un seguimiento de `collaborationRootId` como será necesario en las solicitudes posteriores.

**Tarea 3: Crear un plan de Planner**

Cree un plan de Planner y asócielo a la sesión de colaboración creada anteriormente con `Group ID` y `collaborationRootId`.

# <a name="request"></a>[Solicitud](#tab/request1)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannerplans  
```

```json

{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_owner": "{{groupId}}", 
    "m365_title": "{{planTitle}}" 
}

```

* `collaborationRootId`: identifica la sesión de colaboración con la que queremos asociar este plan y usa el valor de la tarea 2.

* `groupId`: identifica el grupo propietario de este plan y usa el valor del paso 1.

* `planTitle`: título del plan

# <a name="response"></a>[Respuesta](#tab/response1)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#m365_graphplannerplans/$entity", 
    "@odata.etag": "W/\"JzEtUGxhbiAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:33.1833561Z", 
    "m365_owner": "03614cef-8f5b-4265-9944-080d013c55d6", 
    "m365_title": "Multi-byte plan", 
    "m365_id": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannerplanid": "5c9c3ecf-f157-0f67-dcd9-733a77ad593e", 
    "m365_details": null 
} 

```

---

Realice un seguimiento de`m365_id` como será necesario en las solicitudes posteriores.

**Tarea 4: Crear una tarea de Planner**

Cree una tarea de Planner con `PlanId` y `collaborationRootId`. puede crear varias tareas de Planner y asociarlas a la sesión de colaboración creada anteriormente.

# <a name="request"></a>[Solicitud](#tab/request2)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json
{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
} 

```

* `collaborationRootId`: identifica la sesión de colaboración a la que queremos asociar este plan, el valor de la tarea 2.
* `planId`: identifica el plan al que se asignará esta tarea, use el valor del paso anterior.
* `taskTitle`: título de la tarea

# <a name="response"></a>[Respuesta](#tab/response2)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488865579062167", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-16T16:58:47.571364+00:00\",\"orderHint\":\"8585488866179218449P`\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:47Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_hasdescription": false, 
    "m365_orderhint": "8585488865579062167", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Team-oriented discrete time-frame", 
    "m365_id": "8WSKWaEqAU-aZV4h9VUn0GUALXbH", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannertaskid": "0a2115b9-8b03-90ee-b450-42005d906ce8", 
    "m365_completedby": null, 
    "m365_details": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
} 

```

---

Realice un seguimiento de `m365_graphplannertaskid` como será necesario en las solicitudes posteriores.

> [!NOTE]
> `m365_graphplannertaskid` es la clave principal del registro en la tabla virtual de tareas de Planner. Todas las solicitudes posteriores a la tabla virtual para interactuar con este registro deben usar esta clave principal. Esto se denominará en los `plannerTaskId` pasos siguientes de este documento.

Debe repetir este paso para crear varias tareas en el plan.

**Tarea 5: Recuperar tareas de Planner asociadas**

Recupere tareas de Planner asociadas con `collaborationRootId` asociadas a la sesión de colaboración creada anteriormente.

# <a name="request"></a>[Solicitud](#tab/request3)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

* `$filter`: use la consulta del sistema $filter para solicitar los registros asociados a la sesión de colaboración (especificando el identificador del registro raíz de colaboración).
* `$select`: use la opción de consulta del sistema $select para solicitar propiedades específicas.

# <a name="response"></a>[Respuesta](#tab/response3)

```http
    HTTP/1.1 200 OK 
```

```json

{ 

    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks(m365_graphplannertaskid,m365_title,m365_createddatetime)", 
    "value": [ 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "8537731e-9414-1091-8d7d-ce5b74fc2477", 
            "m365_title": "Diverse executive core", 
            "m365_createddatetime": "2022-05-16T16:58:45Z", 
            "m365_id": "N_A2qmo3j0uvZZY1yd6V_GUADDEg", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "4a89895a-050e-9165-a6e4-19c3850f22ec", 
            "m365_title": "Cloned didactic open architecture", 
            "m365_createddatetime": "2022-05-16T16:58:41Z", 
            "m365_id": "--U0zbgsO0us084C0yCyEWUALbWw", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "20a08b8c-394b-b3fb-f9d1-47496df7a67b", 
            "m365_title": "Synergized zero defect interface", 
            "m365_createddatetime": "2022-05-16T16:58:43Z", 
            "m365_id": "AMn3RtbmV0m6cvkp5HKDCWUAKI0_", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        } 
    ] 
} 

```

---

Realice un seguimiento de como `m365_id‘s` los identificadores serán necesarios en las solicitudes posteriores.

**Tarea 6: Recuperar una tarea de Planner**

Recupere una tarea de Planner con `PlannerTaskID` para realizar una operación de lectura en una de las tareas de Planner creadas anteriormente.

# <a name="request"></a>[Solicitud](#tab/request4)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})  
```

* `plannerTaskId`: la clave principal del registro de tareas de Planner es la `m365_graphplannertaskid` propiedad .

# <a name="response"></a>[Respuesta](#tab/response4)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488204334528131", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-17T11:20:52.0247676+00:00\",\"orderHint\":\"8585488204934840644P2\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-17T11:20:52Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_orderhint": "8585488204334528131", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Secured content-based customer loyalty", 
    "m365_id": "SXmz1hxiOk-E3MKJUyhj0mUABvix", 
    "m365_details": "{\"@odata.context\":\"https://graph.microsoft.com/beta/$metadata#planner/tasks('SXmz1hxiOk-E3MKJUyhj0mUABvix')/details/$entity\",\"@odata.etag\":\"W/\\\"JzEtVGFza0RldGFpbHMgQEBAQEBAQEBAQEBAQEBARCc=\\\"\",\"description\":null,\"previewType\":\"automatic\",\"id\":\"SXmz1hxiOk-E3MKJUyhj0mUABvix\",\"references\":{},\"checklist\":{}}", 
    "m365_graphplannertaskid": "1b326015-bb43-945c-85bc-9b2a4ed16c73", 
    "m365_completedby": null, 
    "m365_hasdescription": null, 
    "m365_collaborationrootid": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
}

```

---

Realice un seguimiento de la `@odata.etag` propiedad y de la`m365_graphplannertaskid` propiedad, ya que serán necesarias para realizar operaciones de actualización o eliminación.

**Tarea 7: Actualizar una tarea de Planner**

Actualice una tarea de Planner con `PlannerTask ID` para realizar una operación de actualización en una de las tareas de Planner creadas en el paso anterior. Para actualizar una tarea de Planner, ejecute la siguiente solicitud:

# <a name="request"></a>[Solicitud](#tab/request5)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* Encabezado: If-Match: {{@odata.etag}}

```json

{
    "m365_title": "{{$planTitle}}" 
}   

```

* `@odata.etag`: Etag para la tarea, debe realizar una lectura para recuperar la versión más actualizada.

* `planTitle`: título actualizado para la tarea

# <a name="response"></a>[Respuesta](#tab/response5)

```http
    HTTP/1.1 204 No Content 
```

---

**Tarea 8: Eliminar una tarea de Planner**

Elimine una tarea de Planner con `PlannerTask ID` para realizar una operación de eliminación en una de las tareas de Planner creadas en el paso anterior. Para eliminar una tarea de Planner, ejecute la siguiente solicitud:

# <a name="request"></a>[Solicitud](#tab/request6)

```http
    HTTP/1.1 DELETE https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* `@odata.etag`: Etag para la tarea, debe realizar una lectura para recuperar la versión más actualizada.

# <a name="response"></a>[Respuesta](#tab/response6)

```http
    HTTP/1.1 204 No Content
```

---

**Tarea 9: Actualizar los detalles de una tarea de Planner**

Actualice una tarea de Planner con `PlannerTask ID` para realizar una operación de actualización en una de las tareas de Planner creadas en el paso anterior.

# <a name="request"></a>[Solicitud](#tab/request7)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

Encabezado: If-Match: {{@odata.etag}}

```json

{ 

    "m365_title": "{{$planTitle}}", 
    "m365_details": "{\"@odata.etag\":\"{{details.etag}}\",\"description\":\"Updated Task Description\"}" 

}   
```

* `@odata.etag`: Etag para la tarea, debe realizar una lectura para recuperar la versión más actualizada.
* `planTitle`: se ha actualizado el título de la tarea.
* `@details.etag`: Etag para los detalles de la tarea, debe realizar una lectura mediante la consulta $select parámetro de consulta para incluir la `m365_details` columna para recuperar la versión más actualizada. Este valor se incluirá en la `m365_details` columna de la respuesta. Este valor no es el mismo que porque `@odata.etag` en el back-end de Planner, la tarea y sus detalles se almacenan por separado.

# <a name="response"></a>[Respuesta](#tab/response7)

```http
HTTP/1.1 204 No Content 
```

---

> [!NOTE]
> Puede establecer el `If-Match` encabezado en '*' y, a continuación, no tendrá que proporcionar ningún valor de etag, pero los cambios siempre sobrescribirán la tarea y sus detalles.

## <a name="virtual-tables-authorization"></a>Autorización de tablas virtuales

A continuación se indican los pasos de autorización necesarios para realizar solicitudes HTTP mediante las tablas virtuales de la solución Controles de colaboración.

### <a name="azure-app-registration"></a>Registro de aplicaciones de Azure

Para adquirir el token de portador correcto, se requiere un registro de aplicación en Azure. Para obtener más información sobre los registros de aplicaciones, consulte [Registro de una aplicación](/azure/active-directory/develop/quickstart-register-app).

1. Cree un registro de aplicación en el Azure Portal para autenticarse.
1. Vaya a **Certificados & secretos**.
1. Cree un nuevo secreto de cliente.

     > [!IMPORTANT]
     > Asegúrese de copiar el valor del secreto y almacenarlo para su uso posterior. No podrá acceder a ella de nuevo después de salir de la página actual.

1. Vaya a **Permisos de API**.
1. Agregue el permiso delegado **user_impersonation** de Dynamics CRM.
1. Conceda el consentimiento del administrador para este permiso.

     :::image type="content" source="../assets/images/collaboration-control/power-automate-api-permission.png" alt-text="La captura de pantalla es un ejemplo que muestra el permiso de API de Power Automate":::

1. Vaya a **Manifiesto**.
1. Establezca el valor de los atributos siguientes en true:

   * oauth2AllowIdTokenImplicitFlow
   * oauth2AllowImplicitFlow

1. Seleccione Guardar.

     :::image type="content" source="../assets/images/collaboration-control/power-automate-manifest.png" alt-text="La captura de pantalla es un ejemplo que muestra el manifiesto de Power Automate":::

### <a name="powerapps-environment-permissions"></a>Permisos de entorno de PowerApps

Una vez configurado el registro de la aplicación, debe configurar un usuario de la aplicación en el entorno de PowerApps. Esto le permitirá autenticarse con los ámbitos de Dynamics correctos que se configuraron anteriormente.

1. Abra el [Centro de Administración de Power Platform](https://admin.powerplatform.microsoft.com/).
1. Vaya a **Entornos** > **Your_Environment** > **Lista de usuarios de aplicaciones** de **usuarios** > .
1. Seleccione **Nuevo usuario de la aplicación** y seleccione el registro de la aplicación de Azure.
1. Seleccione **Editar roles de seguridad** y asigne el rol **Administrador del sistema** al usuario de la aplicación.

   1. El rol **Administrador del sistema** se aplica para permitir la autenticación de cualquier usuario que tenga un rol de seguridad inferior. Por ejemplo, **Colaboración controla User**.
   1. Esto se puede restringir aplicando un rol inferior a la aplicación. Por ejemplo, **la colaboración controla al administrador**.

     :::image type="content" source="../assets/images/collaboration-control/power-automate-admin-center.png" alt-text="La captura de pantalla es un ejemplo que muestra el Centro de administración de Power Automate":::

### <a name="getting-the-bearer-token"></a>Obtención del token de portador

Después de completar el registro de aplicaciones de Azure y los permisos de entorno de PowerApps, envíe la siguiente solicitud HTTP para obtener el token de portador.

```http
POST https://login.microsoftonline.com/<AZURE_APP_TENANT_ID>/oauth2/token
```

* **Content-Type**: application/x-www-form-urlencoded
* **client_id**: <AZURE_APP_CLIENT_ID>
* **&client_secret**: <AZURE_APP_CLIENT_ID>
* **recurso&**: https://\<RESOURCEURL\>/
* **&nombre de usuario**: \<USERNAME\>
* **&contraseña**: \<PASSWORD\>
* **&grant_type**: Contraseña

> [!IMPORTANT]
> Asegúrese de incluir la barra diagonal final en el parámetro de recurso. Si no es así, obtendrá un error relacionado con los ámbitos de Graph al llamar a la tabla virtual.

En la carga de respuesta, copie el valor de la propiedad **access_token** . A continuación, puede pasar este token de portador como parte del encabezado de autorización al realizar solicitudes a las tablas virtuales.

:::image type="content" source="../assets/images/collaboration-control/power-automate-authorization.png" alt-text="La captura de pantalla es un ejemplo que muestra la autorización de Power Automate":::

## <a name="virtual-tables-error-handling"></a>Control de errores de tablas virtuales

El control de errores de tablas virtuales describe escenarios de error comunes y cómo responderán las tablas virtuales.

### <a name="attempt-to-create-a-virtual-record-without-a-collaboration-session"></a>Intento de crear un registro virtual sin una sesión de colaboración

Se requiere una sesión de colaboración válida para que cada solicitud cree un registro virtual.  Cuando se crea un registro virtual, la tabla virtual creará un registro de mapa de colaboración, que incluye la clave principal del registro virtual, el nombre de entidad y el identificador externo, es decir, el identificador de recurso de Graph. Este mapa de colaboración está asociado a una sesión de colaboración y así es como los controles de colaboración realizarán un seguimiento de las colaboraciones asociadas a un registro empresarial.

# <a name="request"></a>[Solicitud](#tab/request8)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json

{ 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
}

```

Falta `collaborationRootId` la propiedad de la solicitud.

# <a name="response"></a>[Respuesta](#tab/response8)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
    "error": { 
        "code": "0x80048d0b", 
        "message": "Parameter 'm365_collaborationrootid' is null, empty, or white-space." 
    } 
} 

```

---

Para resolver este problema, siempre debe proporcionar una propiedad válida `collaborationRootId` al crear un registro virtual.

### <a name="attempt-to-read-a-virtual-record-without-a-collaboration-map"></a>Intento de leer un registro virtual sin un mapa de colaboración

Las tablas virtuales permiten ejecutar solicitudes, que devuelven colecciones de registros virtuales. Lo vimos anteriormente en este documento, donde solicitamos todas las tareas del planificador asociadas a una sesión de colaboración específica. También es posible solicitar todas las tareas de planner asociadas a un plan de planner específico mediante una consulta del sistema de $filter como esta: $filter=m365_planid eq`{{planId}}`. Un problema que se producirá si se usa una consulta de este tipo es que los registros se devolverán para las tareas de Planner, que no están asociadas a una sesión de colaboración, es decir, las tareas de planner creadas por un medio que no sea el uso de un control de colaboración. Si intenta leer, actualizar o eliminar dicho registro, se producirá un error en la solicitud porque la tabla virtual no puede encontrar el mapa de colaboración asociado.  

# <a name="request"></a>[Solicitud](#tab/request9)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

La `plannerTaskId` propiedad está asociada a una tarea de planner, que se creó mediante la interfaz web de Planner y, por lo tanto, no tiene un registro de mapa de colaboración.

# <a name="response"></a>[Respuesta](#tab/response9)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "A record with the specified key values does not exist in m365_collaborationmap entity" 
    }
} 
```

---

Para resolver este problema, debe comprobar el mensaje de error en la respuesta y, si está establecido en el mensaje mostrado anteriormente, significa que el registro virtual no está asociado. Para crear una asociación para este registro, debe llamar [a Asociar mapa de colaboración - API REST](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/associate-collaboration-map).

### <a name="attempt-to-read-a-virtual-record-and-the-graph-resource-has-been-deleted"></a>Intento de leer un registro virtual y se ha eliminado el recurso de Graph

En relación con el error anterior, debe controlar el caso en el que se ha eliminado un recurso de Graph, pero el cliente todavía tiene una referencia al registro virtual eliminado. Esto puede ocurrir si otro usuario eliminó el registro. Si intenta leer, actualizar o eliminar un registro de este tipo, se producirá un error en la solicitud porque la tabla virtual no puede recuperar el recurso de Graph.

# <a name="request"></a>[Solicitud](#tab/request10)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

La `plannerTaskId` propiedad está asociada a una tarea de planner, que se eliminó.

# <a name="response"></a>[Respuesta](#tab/response10)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "REST call failed because: Reason - NotFound, Full error - {\"error\":{\"code\":\"\",\"message\":\"The requested item is not found.\",\"innerError\":{\"date\":\"2022-05-17T16:30:51\",\"request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\",\"client-request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\"}}}." 
    } 
} 
```

---

Este caso debe controlarse mediante cualquier código de cliente, que recupere registros virtuales, ya que otro usuario puede eliminar el recurso de Graph asociado en cualquier momento.

### <a name="attempt-to-update-a-virtual-record-with-an-invalid-odataetag"></a>Intento de actualizar un registro virtual con un @odata.etag no válido

La `@odata.etag` propiedad se usa para la simultaneidad de datos y para evitar la escritura excesiva del mismo registro si otro usuario la ha actualizado. Cuando se lee un registro, se devuelve el etag actual y sigue siendo válido hasta que se cambia el registro. El etag debe incluirse en cualquier solicitud de actualización y se comprobará antes de que se complete la operación. Si otro usuario cambió el registro desde que el usuario actual leyó el registro, se producirá un error en la solicitud de actualización de los usuarios actuales.

Si realiza dos solicitudes de actualizaciones con el mismo @odata.etag, se producirá un error en la segunda solicitud:

# <a name="request"></a>[Solicitud](#tab/request11)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

Encabezado: If-Match: {{@odata.etag}}

```json
{
    "m365_title": "{{$planTitle}}" 
}

```

# <a name="response"></a>[Respuesta](#tab/response11)

```http
    HTTP/1.1 409 Conflict 
```

```json
{ 
    "error": { 
        "code": "0x80048d08", 
        "message": "REST call failed because: Reason - Conflict, Full error - {\"error\":{\"code\":\"\",\"message\":\"The attempted changes conflicted with already accepted changes. Read the latest state and resolve differences.\",\"innerError\":{\"date\":\"2022-05-18T06:54:55\",\"request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\",\"client-request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\"}}}." 
    }
} 
```

---

### <a name="querying-for-associated-virtual-records"></a>Consulta de registros virtuales asociados

En la tarea 5 de anterior, se describe cómo recuperar tareas de Planner asociadas. Esta operación es compatible con todas las tablas virtuales. Al ejecutar esta solicitud, debe incluir una `$filter` consulta, que especifica el identificador raíz de colaboración como se muestra a continuación:

# <a name="request"></a>[Solicitud](#tab/request12)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

---

* Otras opciones de filtrado no se pueden combinar con esta `$filter` consulta y, si las hay, se omitirán.
* Se debe realizar otro filtrado directamente en la respuesta de la solicitud.

### <a name="querying-for-virtual-records-with-required-key-attributes"></a>Consulta de registros virtuales con atributos clave necesarios

Cuando se llama a Dataverse Web API para recuperar varios registros de las siguientes tablas virtuales, se requiere un atributo de clave obligatorio. Graph Booking Appointments requiere que se incluya un valor válido `m365_bookingbusinessid` en la consulta. Si no se proporciona el atributo de clave, se producirá un error en la solicitud como se indica a continuación:

# <a name="response"></a>[Respuesta](#tab/response13)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
  "error": { 
    "code": "0x80048d0b", 
    "message": "Key attribute is missing: 'm365_bookingbusinessid'.", 
    ….
  } 
} 

```

---

Para solucionar este problema, cambie la solicitud a este formato:

# <a name="request"></a>[Solicitud](#tab/request14)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphbookingappointments?$filter=m365_bookingbusinessid eq '{{bookingBusinessId}}'
```

---

### <a name="creating-virtual-records-and-graph-access-control"></a>Creación de registros virtuales y control de acceso de Graph

Las tablas virtuales respetan el control de acceso especificado para Microsoft Graph. Las tablas virtuales no permitirán operaciones que el usuario no pudo realizar mediante microsoft Graph API. Por ejemplo, si el usuario que usa para crear el plan es tarea 3 y no es miembro del grupo que usa, obtendrá 403 respuestas prohibidas.
