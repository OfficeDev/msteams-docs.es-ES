---
title: Referencias de entidad de tabla virtual
author: surbhigupta
description: En este módulo, obtenga información sobre la referencia de entidad de tablas virtuales y sus atributos en Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 98e9ee6a2bc565c35a9b46c2990a7c548dab2e31
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243055"
---
# <a name="virtual-tables-entity-reference"></a>Referencia de entidad de tablas virtuales

Los controles de colaboración de las entidades virtuales y sus atributos tienen una asignación uno a uno con un tipo de recurso específico de Microsoft Graph. Por ejemplo, las entidades de tarea de Graph Planner se asignan al [tipo de recurso Tarea de Microsoft Graph Planner](/graph/api/resources/plannertask). La entidad virtual comparte los mismos atributos que el tipo de recurso.

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

## <a name="collaboration-controls-virtual-entities"></a>La colaboración controla las entidades virtuales

| Nombre | Descripción |
|---|---|
| Tarea de Graph Planner | La tabla Tarea de Graph Planner representa una tarea de Planner en Microsoft 365. |
| Graph Planner Plan | La tabla Plan de Graph Planner representa un plan de Planner en Microsoft 365. |
| Graph (evento) | La tabla De eventos de Graph representa un evento en un calendario de usuario o el calendario predeterminado de un grupo de Microsoft 365. |
| Cita de reserva de Graph | La tabla Citas de reserva de Graph representa una cita de cliente para un servicio de reserva, realizada por un conjunto de miembros del personal, provIDed por una Microsoft Bookings empresa. |
| Unidad de grafo | La tabla Graph Drive representa el objeto de nivel superior que representa onedrive de un usuario o una biblioteca de documentos en SharePoint. |
| Elemento de unidad de grafo | La tabla Graph Drive Item representa un archivo, una carpeta u otro elemento almacenado en una unidad. |

## <a name="graph-planner-task"></a>Tarea de Graph Planner

* Nombre de entidad: m365_graphplannertask.
* Recurso de Graph: [tipo de recurso plannerTask](/graph/api/resources/plannertask)
* No se admite la ordenación.
* No se admite el filtrado.
* Se admite la paginación controlada por el servidor, con un tamaño máximo de página de 400.

### <a name="attributes-for-graph-planner-task"></a>Atributos para la tarea Graph Planner

| Column  | Tipo de dataverse | Detalles |
|---|---|---|
| `m365_collaborationrootid` | Cadena | El identificador raíz de colaboración del registro de sesión de colaboración está asociado a varias sesiones de colaboración. Esto se devolverá como una cadena delimitada por comas. Tenga en cuenta que este atributo no se devolverá al recuperar varios registros. |
| `m365_activechecklistitemcount` | Int32 | Número de elementos de lista de comprobación con el valor establecido en false, que representa elementos incompletos. |
| `m365_graphplannertaskId` | Guid | Identificador único de la tarea del planificador de grafos. |
| `m365_appliedcategories` | Cadena | Número de elementos de lista de comprobación con el valor establecido en false, que representa elementos incompletos. |
| `m365_appliedcategories` | Cadena | Categorías a las que se ha aplicado la tarea. Este atributo es una cadena codificada en JSON, por ejemplo "{ \"category1\": true, \"category6\": true, \"category9\": true }" |
| `m365_assigneepriority` | Cadena | Sugerencia usada para ordenar elementos de este tipo en una vista de lista. El formato se define como se describe en [el uso de sugerencias de orden en Planner](/graph/api/resources/planner-order-hint-format). |
| `m365_assignments` | Cadena | El conjunto de asignados a los que se asigna la tarea. Este atributo es una cadena codificada en JSON por ejemplo "{\" 7be...\": {\"assignedBy\": {\"user\": {\"displayName\", \"email\", \"ID\":\" 7be...\"}, \"group\": null, \"application\": null \"device\": null}" |
| `m365_bucketid` | Cadena | Id. del depósito al que pertenece la tarea. El depósito debe estar en el plan en el que se encuentra la tarea. Tiene 28 caracteres y distingue mayúsculas de minúsculas. La [validación del formato](/graph/api/resources/planner-identifiers-disclaimer) se efectúa en el servicio. |
| `m365_checklistitemcount` | Int32 | Número de elementos de lista de comprobación que están presentes en la tarea. |
| `m365_completedby` | Cadena | Identidad del usuario que ha completado la tarea. Este atributo es una cadena codificada en JSON, por ejemplo {\"user\": {\"displayName,ID\"\"\":\"d55...\"}} |
| `m365_completeddatetime` | DateTime | Solo lectura. Fecha y hora a la que se establece "percentComplete" de la tarea en "100". El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z |
| `m365_conversationthreadid` |Cadena | Identificador de subproceso de la conversación en la tarea. Este es el identificador del objeto de subproceso de conversación creado en el grupo. |
| `m365_createdby` | Cadena | Identidad del usuario que ha creado la tarea. Este atributo es una cadena codificada en JSON, por ejemplo {\"user\": {\"displayName,ID\"\"\":\"d55...\"}} |
| `m365_createddatetime` | DateTime | Solo lectura. Fecha y hora en que se crea la tarea. El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z |
| `m365_duedatetime` | DateTime | Fecha y hora en que vence la tarea. El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z |
| `m365_hasdescription` | Boolean | Solo lectura. El valor es true si el objeto de detalles de la tarea tiene una descripción no vacía y false en caso contrario. |
| `m365_id` | Cadena | Solo lectura. Id. de la tarea. Tiene 28 caracteres y distingue mayúsculas de minúsculas. La [validación del formato](/graph/api/resources/planner-identifiers-disclaimer) se efectúa en el servicio.|
| `m365_orderhint` | Cadena | Sugerencia usada para ordenar elementos de este tipo en una vista de lista. El formato se define como se describe en [el uso de sugerencias de orden en Planner](/graph/api/resources/planner-order-hint-format). |
| `m365_percentcomplete` | Int32 | Porcentaje de finalización de la tarea. Cuando se establece en 100, la tarea se considera completada. |
| `m365_priority` | Int32 | Prioridad de la tarea. El intervalo válido de valores está comprendido entre 0 y 10, y el valor creciente es menor prioridad (0 tiene la prioridad más alta y 10 tiene la prioridad más baja). Actualmente, Planner interpreta los valores 0 y 1 como "urgentes", 2, 3 y 4 como "importantes", 5, 6 y 7 como "medio", y 8, 9 y 10 como "bajo". Además, Planner establece el valor 1 para "urgente", 3 para "importante", 5 para "medio" y 9 para "bajo". |
| `m365_planid` | Cadena | Id. de plan al que pertenece la tarea. |
| `m365_previewtype` | Cadena | Establece el tipo de vista previa que aparece en la tarea. Los valores posibles son: automatic, noPreview, checklist, description, reference. |
| `m365_referencecount` | Int32 | Número de referencias externas que existen en la tarea.|
| `m365_startdatetime` | DateTime | Fecha y hora en que comienza la tarea. El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z |
| `m365_title` | String |Título de la tarea. Columna de búsqueda principal |

## <a name="graph-planner-plan"></a>Graph Planner Plan

* Nombre de entidad: m365_graphplannerplan.
* Recurso de Graph: [tipo de recurso plannerPlan](/graph/api/resources/plannerplan).
* No se admite la ordenación.
* No se admite el filtrado.
* Se admite la paginación controlada por el servidor, con un tamaño máximo de página de 400.

### <a name="attributes-for-graph-planner-plan"></a>Atributos para el plan de Graph Planner

| Column  | Tipo de dataverse | Detalles |
|---|---|---|
| `m365_collaborationrootid` | Cadena | Identificador raíz de colaboración de la sesión de colaboración a la que está asociado el registro. Si el registro está asociado a varias sesiones de colaboración, se devolverá como una cadena delimitada por comas. Tenga en cuenta que este atributo no se devolverá al recuperar varios registros.|
| `m365_graphplannerplanid` |Guid |Identificador único del plan del planificador de grafos.|
| `m365_createdby` | Cadena | Identidad del usuario que ha creado la tarea. Este atributo es una cadena codificada en JSON, por ejemplo {\"user\": {\"displayName,ID\"\"\":\"d55...\"}} |
| `m365_createddatetime` | DateTime | Solo lectura. Fecha y hora en que se crea la tarea. El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z |
| `m365_id` | Cadena | Solo lectura. Id. del plan. Tiene 28 caracteres y distingue mayúsculas de minúsculas. La [validación del formato](/graph/api/resources/planner-identifiers-disclaimer) se efectúa en el servicio.|
| `m365_owner` | Cadena | Id. del [grupo](/graph/api/resources/group) que tiene el plan. Una vez establecido, esta propiedad no se puede actualizar.|
| `m365_title` | Cadena | El título del plan. Columna de búsqueda principal |

## <a name="graph-event"></a>Graph (evento)

* Nombre de entidad: m365_graphevent
* Recurso de Graph: [tipo de recurso de evento](/graph/api/resources/event)
* La ordenación se admite en las columnas siguientes:
  * m365_lastmodifieddatetime
  * m365_createddatetime
  * m365_hasattachments
  * m365_importance
  * m365_responserequested
  * m365_sensitivity
  * m365_showas
  * m365_subject
* El filtrado se admite en las columnas siguientes:
  * m365_allownewtimeproposals
  * m365_lastmodifieddatetime
  * m365_createddatetime
  * m365_icaluID
  * m365_importance
  * m365_isallday
  * m365_iscancelled
  * m365_isdraft
  * m365_responserequested
  * m365_sensitivity
  * m365_showas
  * m365_subject
  * m365_type
* Se admite la paginación controlada por el servidor.

### <a name="attributes-for-graph-event"></a>Atributos para el evento Graph

| Column |Tipo de dataverse |Detalles |
|---|---|---|
|`m365_collaborationrootid` |Cadena |Raíz de colaboración de la sesión de colaboración a la que está asociado el registro. Si el registro está asociado a varias sesiones de colaboración, se devolverá como una cadena delimitada por comas. Tenga en cuenta que este atributo no se devolverá al recuperar varios registros. |
|`m365_allownewtimeproposals` |Boolean |True, si el organizador de la reunión permite a los invitados proponer una nueva hora al responder. De lo contrario, false, que es opcional. El valor predeterminado es "true". |
|`m365_attendees` |Cadena |La colección de asistentes del evento. Este atributo es una cadena codificada en JSON, con una longitud máxima de 15000. Por ejemplo, [{{\"type\":\"required,status\"\"\":{{\"response\":\"none,time\"\"\":\"0001-01-01T00:00:00Z\"}},\"emailAddress\":\"test@contoso.com\"}}] |
|`m365_body` |Cadena |El cuerpo del mensaje asociado con el evento. Puede mostrarse en formato de texto o HTML. Este atributo es una cadena codificada en JSON, con una longitud máxima de 15000. Por ejemplo{\" contentType\":\"html,content\"\"\":\"html/html\"} |
|`m365_bodypreview` |Cadena |La vista previa del mensaje asociado al evento. Se muestra en formato de texto. |
|`m365_categories` |String |Las categorías asociadas con el evento. Cada categoría se corresponde con la propiedad displayName de un elemento outlookCategory definido para el usuario. Por ejemplo [\"string\"] |
|`m365_changekey` |Cadena |Identifies the version of the event object. Every time the event is changed, ChangeKey changes as well. This allows Exchange to apply changes to the correct version of the object. |
|`m365_createddatetime` |DateTime |El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z |
|`m365_start` |DateTime |La fecha de inicio, la hora y la zona horaria del evento. Este atributo es una cadena codificada en JSON, con una longitud máxima de 100. Por ejemplo{\" dateTime\":\"2022-01-19T11:00:00+00:00,timeZone\"\"\":\"UTC}\"|
|`m365_end` |DateTime |La fecha, la hora y la zona horaria en que finaliza el evento. Este atributo es una cadena codificada en JSON, con una longitud máxima de 100. Por ejemplo{\" dateTime\":\"2022-01-19T11:00:00+00:00,timeZone\"\"\":\"UTC}\" |
|`m365_hasattachments` |Booleano |Se establece como true si el evento tiene datos adjuntos. |
|`m365_hideattendees` |Boolean |Cuando se establece en true, cada asistente solo se ve en la convocatoria de reunión y en la lista de seguimiento de reuniones. El valor predeterminado es false. |
|`m365_icaluid` |String |Un identificador único para un evento entre calendarios. Este id. es diferente para cada repetición en una serie periódica. Solo lectura. |
|`m365_isallday`|Boolean |Set to true if the event lasts all day. If true, regardless of whether it's a single-day or multi-day event, start and end time must be set to midnight and be in the same time zone. |
|`m365_iscancelled` |Booleano |Se establece como true si el evento ha sido cancelado. |
|`m365_id`| Cadena |Solo lectura. Identificador del evento. |
|`m365_isdraft` |Boolean |Establezca en true si el usuario ha actualizado la reunión en Outlook, pero no ha enviado las actualizaciones a los asistentes. Se establece como false si se han enviado todos los cambios, o si el evento es una cita sin asistentes.|
|`m365_isonlinemeeting`|Boolean|True si este evento tiene información de reunión en línea (es decir, onlineMeeting apunta a un recurso onlineMeetingInfo), false en caso contrario. El valor predeterminado es false (onlineMeeting es null). Opcional. Después de establecer isOnlineMeeting en true, Microsoft Graph inicializa onlineMeeting. Outlook posterior omite cualquier cambio adicional en isOnlineMeeting y la reunión permanece disponible en línea.|
|`m365_isorganizer`|Boolean|Se establece en true si el propietario del calendario (especificado por la propiedad owner de calendar) es el organizador del evento (especificado por la propiedad organizer del event). Esto también se aplica si un delegado organizó el evento en nombre del propietario.|
|`m365_isremindero`n|Booleano|Se establece como true si se crea una alerta para recordarle el evento al usuario.|
|`m365_lastmodifieddatetime`|DateTime|El tipo de marca de tiempo representa la información de fecha y hora con el formato ISO 8601 y está siempre en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z|
|`m365_location`|Cadena|La ubicación del evento. Cadena con codificación JSON, longitud máxima de 4000. Por ejemplo[{\"address\":null,coordinates\"\":null,displayName\"\":\"Harry\'s Bar,locationEmailAddress\"\"\":null,locationType\"\":\"default,locationUri\"\"\":null,uniqueId\"\":\"Harry\'s Bar,uniqueIdType\"\"\":\"private}\"|
|`m365_locations`|Cadena|Ubicaciones donde se celebra el evento o en las que se asiste. Las propiedades location y locations siempre se corresponden entre sí. Si se actualiza la propiedad location, se eliminarían las ubicaciones anteriores de la colección locations y se reemplazarían por el nuevo valor de location. Cadena codificada en JSON, un máximo de 4000 en longitud.por ejemplo[{\"address:null,coordinates\"\":null,displayName\"\":\"Harry\'s Bar,locationEmailAddress\"\"\":null,locationType\"\":\"default,locationUri\"\"\":null,uniqueId\"\":\"Harry\'s Bar,uniqueIdType\"\"\":\"private\"}]\"|
|`m365_onlinemeeting`|Cadena|Detalles para que un asistente participe en la reunión en línea. El valor predeterminado es null. Solo lectura.Después de establecer las propiedades isOnlineMeeting y onlineMeetingProvider para habilitar una reunión en línea, Microsoft Graph inicializa onlineMeeting. Cuando se establece, la reunión permanece disponible en línea y no se pueden cambiar las propiedades isOnlineMeeting, onlineMeetingProvider y onlneMeeting de nuevo. Cadena codificada en JSON, un máximo de 4000 en longitud.por ejemplo{conferenceId: String,joinUrl\"\"\": \"String,phones\"\"\": [{\"@odata.type\": \"microsoft.graph.phone\"}],\"quickDial\": \"String,tollFreeNumbers\"\"\": [\"String\"],\"tollNumber\": \"String}\"\"\"\"|
|`m365_onlinemeetingprovider`|Cadena|Detalles para que un asistente participe en la reunión en línea. El valor predeterminado es null. Solo lectura. Después de establecer las propiedades isOnlineMeeting y `onlineMeetingProvider` para habilitar una reunión en línea, Microsoft Graph inicializa onlineMeeting. Cuando se establece, la reunión permanece disponible en línea y no se pueden volver a cambiar las propiedades isOnlineMeeting, `onlineMeetingProvider`y onlneMeeting.|
|`m365_onlinemeetingurl`|String|Una dirección URL para una reunión en línea. Solo se establece la propiedad cuando el organizador especifica en Outlook un evento como reunión en línea (por ejemplo, Skype). Solo lectura. Para acceder a la dirección URL para unirse a una reunión en línea, use `joinUrl`, que se expone a través de la `onlineMeeting` propiedad del evento. La `onlineMeetingUrl` propiedad quedará en desuso en el futuro.|
|`m365_organizer`|Cadena|Organizador del evento. Cadena con codificación JSON, longitud máxima de 4000. {\"emailAddress\":{\"@odata.type\":\"microsoft.graph.emailAddress\"}}|
|`m365_originalendtimezone`|Cadena|Zona horaria de finalización que se estableció cuando se creó el evento. Un valor de tzone://Microsoft/Custom indica que se estableció una zona horaria personalizada heredada en Outlook de escritorio.|
|`m365_originalstart`|DateTime|Representa la hora de inicio de un evento cuando se crea inicialmente como una repetición o una excepción en una serie periódica. Esta propiedad no se devuelve para los eventos que son instancias únicas. Su información de fecha y hora se expresa en formato ISO 8601 y siempre está en hora UTC. Por ejemplo, medianoche UTC del 1 de enero de 2014 es 2014-01-01T00:00:00Z|
|`m365_originalstarttimezone`|Cadena|La zona horaria de inicio que se estableció cuando se creó el evento. Un valor de tzone://Microsoft/Custom indica que se estableció una zona horaria personalizada heredada en Outlook de escritorio.|
|`m365_recurrence`|Cadena|El patrón de periodicidad del evento. Cadena con codificación JSON, máximo de 4000 en longitud.por ejemplo{\"pattern\":{\"dayOfMonth\":0,daysOfWeek\"\":[\"monday,wednesday,friday\"\"\"\"\"],\"firstDayOfWeek\":\"sunday,index\"\"\":\"first,interval\"\"\":1,month\"\":0,type\"\":\"weekly\"},\"range\":{\"startDate\":\"2017-08-14,endDate\"\"\":\"2018-08-14,\"\" numberOfOccurrences\":0,recurrenceTimeZone\"\":\"Eastern Standard Time,type\"\"\":\"endDate\"}}|
|`m365_reminderminutesbeforestart`|Int32|El número de minutos antes de la hora de inicio del evento en que se producirá la alerta del recordatorio.|
|`m365_responserequested`|Boolean|El valor predeterminado es verdadero. Esto indica que el organizador quiere que un invitado envíe una respuesta al evento.|
|`m365_responsestatus`|Cadena|Indica el tipo de respuesta que se envía en respuesta a un mensaje de evento. Cadena con codificación JSON, longitud máxima de 4000. {\"response\": \"String,time\"\"\": \"String (timestamp)\"}|
|`m365_sensitivity`|Cadena|Los valores posibles son: normal, personal, privado, confidencial.|
|`m365_seriesmasterid`|Cadena|Identificador del elemento de patrón de serie periódica, si el evento forma parte de una serie periódica.|
|`m365_showas`|String|El estado que se mostrará. Los valores posibles son: free, tentative, busy, oof, workingElsewhere, unknown.|
|`m365_subject`|String|El texto de la línea de asunto del evento. Columna de búsqueda principal|
|`m365_transactionid`|Cadena|Identificador personalizado especificado por una aplicación cliente para el servidor para evitar operaciones POST redundantes si el cliente vuelve a intentar crear el mismo evento. Esto es útil cuando la conectividad de red baja hace que el cliente agote el tiempo de espera antes de recibir una respuesta del servidor para la solicitud previa de creación de eventos del cliente. Después de establecer `transactionId` al crear un evento, no puede cambiar transactionId en una actualización posterior. Esta propiedad se devuelve solo en una carga de respuesta si una aplicación la ha configurado. Opcional.|
|`m365_type`|String|El tipo de evento. Los valores posibles son: singleInstance, occurrence, exception, seriesMaster. Solo lectura|
|`m365_weblink`|Cadena|Dirección URL para abrir el evento en Outlook en la web. Outlook en la Web abre el evento en el explorador si ha iniciado sesión en el buzón. En caso contrario, Outlook en la Web le pedirá que inicie sesión. No se puede acceder a esta dirección URL desde dentro de un iFrame.|
|`m365_grapheventid`|Guid|Identificador único del evento de grafo.|
|`m365_groupid`|Cadena|Identificador de grupo al que pertenece el evento.|

## <a name="graph-booking-appointment"></a>Cita de reserva de Graph

* Nombre de entidad: m365_graphbookingappointment
* Recurso de Graph: [tipo de recurso bookingAppointment](/graph/api/resources/bookingappointment)
* No se admite la ordenación.
* El filtrado se admite en las columnas siguientes:
  * m365_bookingbusinessID
  * m365_collaborationrootID
  * m365_customertimezone
  * m365_optoutofcustomeremail
  * m365_price
  * m365_pricetype
  * m365_serviceID
  * m365_servicename
* No se admite la paginación.

### <a name="attributes-for-graph-booking-appointment"></a>Atributos de la cita de reserva de Graph

| Column  | Tipo de dataverse | Detalles |
|---|---|---|
| `m365_collaborationrootid`| Cadena| Identificador raíz de colaboración de la sesión de colaboración a la que está asociado el registro. Si el registro está asociado a varias sesiones de colaboración, se devolverá como una cadena delimitada por comas. Tenga en cuenta que este atributo no se devolverá al recuperar varios registros.|
| `m365_graphbookingappointmentid` | Guid | Identificador único de la cita de reserva de gráficos.|
| `m365_bookingbusinessid` | Cadena | Identificador único de la empresa de reserva en la que está programada la cita.|
| `m365_additionalinformation` | Cadena | Información adicional que se envía al cliente cuando se confirma una cita.|
| `m365_customers` | Cadena| Enumera las propiedades del cliente para una cita. appointment contendrá una lista de información del cliente y cada unidad indicará las propiedades de un cliente que forma parte de esa cita. Opcional[{\"customerID\":\"d243c77b-f1ff-4615-a01f-1660b5cb0e79,customQuestionAnswers\"\"\":[],\"emailAddress\":\"jordanm@contoso.com,location\"\"\":{\"address\":{\"city\":\"\",\"countryOrRegion\":\"\",\"postalCode\":\"\",\"postOfficeBox,state\"\"\":,\"\"\"street\":\"\",\"type\" },\"coordinates\":{\" accuracy,altitude,altitudeAccuracy,latitude,longitude\"\"\"\"\"\"\"\"\" },\"displayName\":\"\",\"locationEmailAddress,locationType,locationUri\"\"\"\"\":\"\",\"uniqueID,uniqueIDType\"\"\" },\"name\":\"Jordan Miller,notes,phone,timeZone\"\"\"\"\"\"\",\"@odata.type:\"\" #microsoft.graph.bookingCustomerInformation\"}] |
| `m365_customertimezone` | Cadena | Zona horaria del cliente. Para obtener una lista de valores posibles, vea [tipo de recurso dateTimeTimeZone](/graph/api/resources/datetimetimezone). |
| `m365_duration` | Cadena | La longitud de la cita, indicada en formato ISO8601.|
| `m365_enddatetime` | DateTime | Fecha, hora y zona horaria que finaliza la cita.|
| `m365_filledattendeescount` | Int32 | Número actual de clientes en la cita.|
| `m365_id` | Cadena | Identificador del bookingAppointment. Solo lectura.|
| `m365_islocationonline` | Boolean | True indica que la cita se realizará en línea. El valor predeterminado es false.|
| `m365_joinweburl` | Cadena | Dirección URL de la reunión en línea de la cita.|
| `m365_maximumattendeescount` | Int32 | Número máximo de clientes permitidos en una cita.|
| `m365_optoutofcustomeremail` | Boolean | True indica que bookingCustomer para esta cita no desea recibir una confirmación para esta cita.|
| `m365_postbuffer` | Cadena | Cantidad de tiempo que se reserva una vez finalizada la cita, para limpiar, por ejemplo. El valor se expresa en formato ISO8601.|
| `m365_prebuffer` | Cadena | La cantidad de tiempo que se debe reservar antes de que comience la cita, para su preparación, como ejemplo. El valor se expresa en formato ISO8601.|
| `m365_price` | DecimalType | Precio normal de una cita para el bookingService especificado.|
| `m365_pricetype` | Cadena | Una configuración para proporcionar flexibilidad para la estructura de precios de los servicios. Los valores posibles son: undefined, fixedPrice, startingAt, hourly, free, priceVaries, callUs, notSet.|
| `m365_reminders` | Cadena | Colección de recordatorios de clientes enviados para esta cita. El valor de esta propiedad solo está disponible al leer este bookingAppointment por su identificador. [{\"message\":\"We forward to seeing you!\",\"offset\":\"P1D,recipients\"\"\":\"customer\"},{\"message\":\"Reminder that you have an appointment!\",\"offset\":\"P1D,recipients\"\"\":\"staff\"}] |
| `m365_selfserviceappointmentid` | Cadena | Otro identificador de seguimiento para la cita, si el cliente ha creado la cita directamente en la página de programación, en lugar de un miembro del personal en nombre del cliente.|
| `m365_serviceid` | Cadena | Identificador del bookingService asociado a esta cita.|
| `m365_servicelocation` | Cadena | Ubicación donde se entrega el servicio. {\"address\":{\"city\":\"\",\"countryOrRegion\":\"\",\"postalCode\":\"\",\"postOfficeBox,state\"\"\":\"\",\"street\":\"\",\"type\" },\"coordinates\":{\"accuracy,altitude,altitudeAccuracy,latitude,longitude\"\"\"\"\"\"\"\"\" },\"displayName\":\"Our office address,locationEmailAddress\"\" \",\"locationType,locationUri\"\"\":\"\",\"uniqueID,uniqueIDType\"\"\" } |
| `m365_servicename` | Cadena | Nombre del bookingService asociado a esta cita. Esta propiedad es opcional al crear una nueva cita. Si no se especifica, se calcula a partir del servicio asociado a la cita por la propiedad serviceID. |
| `m365_servicenotes` |Cadena | Notas de un bookingStaffMember. El valor de esta propiedad solo está disponible al leer esta reservaAppointment por su identificador.|
| `m365_smsnotificationsenabled` | Boolean | True indica que se enviarán notificaciones SMS a los clientes para la cita. El valor predeterminado es false.|
| `m365_staffmemberids` | Cadena | El identificador de cada bookingStaffMember que está programado en esta cita. Se almacena como una cadena separada por comas. [\"string\"] |
| `m365_startdatetime` | DateTime | Fecha, hora y zona horaria a la que comienza la cita.|

## <a name="graph-drive"></a>Unidad de grafo

* Nombre de entidad: m365_graphdrive
* Recurso de Graph: [tipo de recurso de unidad](/graph/api/resources/drive)
* No se admite la ordenación.
* No se admite el filtrado.
* Se admite la paginación controlada por el servidor.

### <a name="attributes-for-graph-drive"></a>Atributos de Graph Drive

|Column |Tipo de dataverse |Detalles |
|---|---|---|
|`m365_collaborationrootid` |Cadena | Identificador raíz de colaboración de la sesión de colaboración a la que está asociado el registro. Si el registro está asociado a varias sesiones de colaboración, se devolverá como una cadena delimitada por comas. Tenga en cuenta que este atributo no se devolverá al recuperar varios registros. |
|`m365_createdby` |Cadena |Identidad del usuario, dispositivo o aplicación que creó el elemento. Solo lectura. Este atributo es una cadena codificada en JSON, por ejemplo { "user": { "displayName": "System Account" } } |
|`m365_createddatetime` |DateTime |Fecha y hora de creación del elemento. Solo lectura. |
|`m365_description` |String |Proporciona una descripción de la unidad visible para el usuario. Solo lectura. |
|`m365_drivetype` |Cadena |Describe el tipo de unidad que representa este recurso. Las unidades personales de OneDrive devolverán personal. OneDrive para la Empresa devolverán el negocio. Las bibliotecas de documentos de SharePoint devolverán documentLibrary. Solo lectura. |
|`m365_graphdriveid` |Guid |Identificador único de la unidad de gráfico. |
|`m365_id` |Cadena |Identificador único de la unidad. Solo lectura. |
|`m365_lastmodifiedby` | Cadena |Identidad del usuario, dispositivo y aplicación, que modificó por última vez el elemento. Solo lectura. Este atributo es una cadena codificada en JSON por ejemplo { "user": { "email": "user@contoso.com", "ID": "61de164e-21ff-4b1c-8cbd-77ac440894f8", "displayName": "User Name" } } |
|`m365_lastmodifieddatetime` |DateTime |Fecha y hora de la última modificación del elemento. Solo lectura.|
|`m365_name` |Cadena |Nombre del elemento. Solo lectura. |
|`m365_owner` |Cadena |Opcional. La cuenta de usuario propietaria de la unidad. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo { "group": { "ID": "76c7286f-8645-4ba8-bc0f-c65a16424aaa", "displayName": "Group Name" }} |
|`m365_quota` |Cadena |Opcional. Información sobre la cuota de espacio de almacenamiento de la unidad. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo { "deleted": 482586, "remaining": 27487788645969, "state": "normal", "total": 27487790694400, "used": 1565845 } |
|`m365_sharepointids` |Cadena |Devuelve identificadores útiles para la compatibilidad con REST de SharePoint. Solo lectura. Esta propiedad no se devuelve de forma predeterminada y debe seleccionarse mediante el parámetro de consulta $select. Este atributo es una cadena codificada en JSON. Por ejemplo"sharePointIDs": { "listID": "29d8457a-8e26-4291-9901-09718a388aaa", "siteID": "93618739-b3ca-4107-a77c-fba278c48aaa", "siteUrl": "<https://contoso.sharepoint.com>", "tenantID": "53986071-de92-43ad-a41f-f3c4adb2beef", "webID": "a0d0e9ec-e547-4338-92d9-4c2c62e5beef" } |
| `m365_siteid` |Cadena |Identificador del sitio que contiene la biblioteca de documentos.
|`m365_system` |Cadena |Si está presente, indica que se trata de una unidad administrada por el sistema. Solo lectura.
|`m365_weburl` |Cadena |Dirección URL que muestra el recurso en el explorador. Solo lectura.

### <a name="graph-drive-item"></a>Elemento de unidad de grafo

* Nombre de entidad: m365_graphdriveitem
* Recurso de Graph: [tipo de recurso driveItem](/graph/api/resources/driveitem)
* La ordenación se admite en la columna siguiente:
  * m365_name
* El filtrado se admite en la columna siguiente:
  * m365_name
* Se admite la paginación controlada por el servidor.

### <a name="attributes-for-graph-drive-item"></a>Atributos para el elemento de unidad de Graph

|Column |Tipo de dataverse |Detalles |
|---|---|---|
|`m365_audio` |Cadena |Metadatos de audio, si el elemento es un archivo de audio. Solo lectura. Solo en OneDrive Personal. Este atributo es una cadena codificada en JSON. { "album": "string", "albumArtist": "string", artist": "string", bitrate": 128, "composers": "string", copyright": "string", "disc": 0, "discCount": 0, "duration": 567, "genre": "string", "hasDrm": false, "isVariableBitrate": false, "title": "string", "track": 1, "trackCount": 16, "year": 2014 }|
|`M365_bundle` |Cadena |Metadatos de agrupación, si el elemento es una agrupación. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "childCount": 3, "album": { "@odata.type": "microsoft.graph.album" }, } |
|`m365_collaborationrootid` |Cadena |Identificador raíz de colaboración de la sesión de colaboración a la que está asociado el registro. Si el registro está asociado a varias sesiones de colaboración, se devolverá como una cadena delimitada por comas. Tenga en cuenta que este atributo no se devolverá al recuperar varios registros. |
|`m365_copy` |Cadena |Si está presente en la solicitud, se realiza una operación de copia. |
|`m365_createdby` |Cadena |Identidad del usuario, dispositivo y aplicación, que creó el elemento. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, {"user":{"displayName":"User Name","email":"alias@contoso.com","ID":"a298b975-3493-4d9e-b2d4-3cad78f00000"},"group": null,"application","device" } |
|`m365_createddatetime` |DateTime |Fecha y hora de creación del elemento. Solo lectura. |
|`m365_ctag` |Cadena |Un eTag del contenido del elemento. Esta eTag no se cambia si solo se cambian los metadatos. Nota. Esta propiedad no se devuelve si el elemento es una carpeta. Solo lectura. |
|`m365_deleted` |Cadena |Información sobre el estado del elemento eliminado. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "state": "string" } |
|`m365_description` |Cadena |Proporciona una descripción del elemento visible para el usuario. Lectura y escritura. Solo en OneDrive Personal. |
|`m365_driveid` |Cadena |Identificador de la unidad que contiene el elemento de unidad.|
|`m365_etag` |Cadena |ETag de todo el elemento (metadatos + contenido). Solo lectura. |
| `m365_file` |Cadena |Metadatos de archivo, si el elemento es un archivo. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, {"hashes":{"crc32Hash","quickXorHash":"Biuzvwdu+Tmu6yRefayD27hD9vD=","sha1Hash","sha256Hash" },"mimeType":"application/vnd.openxmlformats-officedocument.wordprocessingml.document","processingMetadata" } |
| `m365_filesysteminfo` |Cadena |Información del sistema de archivos del cliente. Este atributo es una cadena codificada en JSON. Por ejemplo, {"createdDateTime":"2022-07-21T15:02:47+00:00","lastAccessedDateTime","lastModifiedDateTime":"2022-07-21T15:02:55+00:00"} |
|`m365_folder` |Cadena | Metadatos de carpeta, si el elemento es una carpeta. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, {"childCount":0,"view" } |
|`m365_graphdriveitemid` |Guid |Identificador único del elemento de unidad de grafo. |
|`m365_id` |Cadena |Identificador único del elemento dentro de la unidad. Solo lectura. |
|`m365_image` |Cadena |Metadatos de imagen, si el elemento es una imagen. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, {"height","width" } |
|`m365_lastmodifiedby` |Cadena |Identidad del usuario, dispositivo y aplicación, que modificó por última vez el elemento. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, {"user":{"displayName":"User Name","email":"alias@contoso.com","ID":"a298b975-3493-4d9e-b2d4-3cad78f9a00e"},"group","application","device" } |
|`m365_lastmodifieddatetime` |DateTime |Fecha y hora de la última modificación del elemento. Solo lectura. |
|`m365_location` |Cadena |Metadatos de ubicación, si el elemento tiene datos de ubicación. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, "location": { "altitude": 1.0, "latitude": 1.0, "longitude": 1.0 } |
|`m365_malware` |Cadena |Metadatos de malware, si se detectó que el elemento contenía malware. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "description": "string" } |
|`m365_name` |Cadena |El nombre del elemento (nombre de archivo y extensión). Lectura y escritura. |
|`m365_package` |Cadena |Si está presente, indica que este elemento es un paquete en lugar de una carpeta o archivo. Los paquetes se tratan como archivos en algunos contextos y como carpetas en otros. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "type": "oneNote" } |
|`m365_parentreference` |Cadena |Información primaria, si el elemento tiene un elemento primario. Este atributo es una cadena codificada en JSON. Por ejemplo, {"driveID":"b!qgK-8nOzX0qISvfGCiC2Smbv0m0RlNhDvNQDZsCMpbSnchFAhWAaQoiTLZcSo1gq","driveType":"documentLibrary","ID".:"01EYDCV4YHV77FE3EDDFHIVD6WJ2ETT3PP","name","path":"/drives/b!qgK-8nOzX0qISvfGCiC2Smbv0m0RlNhDvNQDZsCMpbSnchFAhWAaQoiTLZcSo1no/root: /folder name","shareID","sharepointIDs":{"listID":"401172a8-6085-421a-8893-2d9712a35c3c","listItemID","listItemUniqueID":"52feaf12-836c-4e19-8a8f-d64e8939ee52","siteID":" f34e02aa-b373-4a5f-884a-f7c60a20b64a","siteUrl":"https://contoso.sharepoint.com/sites/Contoso,"tenantID","webID":"6dd2ef66-9411-43d8-bcd4-0366c08ccabd"},"siteID" } |
|`m365_parentreferenceid` |Cadena |Identificador del elemento de unidad que es el elemento primario del elemento de unidad. |
|`m365_pendingoperations` |Cadena |Si está presente, indica que hay una o más operaciones que podrían afectar al estado del driveItem y que están pendientes de finalización. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "pendingContentUpdate": {"@odata.type": "microsoft.graph.pendingContentUpdate"} } |
|`m365_photo` |Cadena |Metadatos de foto, si el elemento es una foto. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "cameraMake": "Camera Make", "cameraModel": "Camera Model", "exposureDenominator": 1000000, "exposureNumerator": 41671, "focalLength": 4.38, "fNumber": 1.73, "iso": 70, "orientation": 6, "takenDateTime": "2020-04-29T14:17:39Z" } |
|`m365_publication` |Cadena |Proporciona información sobre el estado publicado o extraído de un elemento, en ubicaciones que admiten esas acciones. Esta propiedad no se devuelve de forma predeterminada. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, {"level":"published","versionID":"2.0"} |
|`m365_remoteitem` |Cadena |Datos de elemento remoto, si el elemento se comparte desde una unidad distinta a la de acceso. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "ID": "string", "createdBy": { "@odata.type": "microsoft.graph.IdentitySet" }, "createdDateTime": "timestamp", "file": { "@odata.type": "microsoft.graph.file" }, "fileSystemInfo": { "@odata.type": "microsoft.graph.fileSystemInfo" }, "folder": { "@odata.type": "microsoft.graph.folder" }, "image": { "@odata.type": "microsoft.graph.image" }, "lastModifiedBy": { "@odata.type": "microsoft.graph.IdentitySet" }, "lastModifiedDateTime": "timestamp", "name": "string", "package": { " @odata.type": "microsoft.graph.package" }, "parentReference": { "@odata.type": "microsoft.graph.itemReference" }, "shared": { "@odata.type": "microsoft.graph.shared" }, "sharepointIDs": { "@odata.type": "microsoft.graph.sharepointIDs" }, "specialFolder": { "@odata.type": "microsoft.graph.specialFolder" }, "size": 1024, "video": { "@odata.type": "microsoft.graph.video" }, "webDavUrl": "url", "webUrl": "url" } |
|`m365_root` |Cadena |Si esta propiedad no es NULL, indica que el driveItem es el driveItem de nivel superior de la unidad. |
|`m365_searchresult` |Cadena |Metadatos de búsqueda, si el elemento es un resultado de búsqueda. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "onClickTelemetryUrl": "url" } |
|`m365_shared` |Cadena |Indica que el elemento se ha compartido con otros usuarios y proporciona información sobre el estado del elemento compartido. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "scope": "users", "owner": { "user": { "displayName": "User Name", "ID": "bbbb6fa48aaaaaaa" } } } |
|`m365_sharepointids` |Cadena |Devuelve identificadores útiles para la compatibilidad con REST de SharePoint. Solo lectura. Este atributo es una cadena codificada en JSON. por ejemplo{"listID":"401172a7-6085-421a-8893-2d9712a35aba","listItemID":"338"."listItemUniqueID":"0edc89e5-24ea-4c6b-a019-dc51f45eeccc","siteID":"f2be02aa-b373-4a5f-884a-f7c60a20bddd","siteUrl":"https://contoso.sharepoint.com/sites/Contoso","tenantID":"1c137272-0581-487f-b195-aeeb93cc4ccc","webID":"6dd2ef66-9411-43d8-bcd4-0366c08caaaa"} |
|`m365_siteid` |Cadena |Identificador del sitio que contiene la biblioteca de documentos. |
|`m365_size` |IntType |Tamaño del elemento en bytes. Solo lectura. |
|`m365_specialfolder` |Cadena |Si el elemento actual también está disponible como una carpeta especial, se devuelve esta faceta. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, { "name": "documents" } |
|`m365_thumbnail` |Cadena |Si está presente en la solicitud, se recuperarán las miniaturas del elemento de unidad. |
|`m365_video` |Cadena |Si el elemento actual también está disponible como una carpeta especial, se devuelve esta faceta. Solo lectura. Este atributo es una cadena codificada en JSON. Por ejemplo, {"bitrate": 10646968, "duration": 1050683, "height": 720, "width": 1280, "audioBitsPerSample": 16, "audioChannels": 1, "audioFormat": "PCM", "audioSamplesPerSecond": 32000, "fourCC": "H264", "frameRate": 60} |
|`m365_webdavurl` |Cadena | Dirección URL compatible con WebDAV del elemento. |
|`m365_weburl` |Cadena |Dirección URL que muestra el recurso en el explorador. Solo lectura. |
