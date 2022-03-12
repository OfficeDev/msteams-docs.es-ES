---
title: Complementos de Microsoft 365
description: Detalles de los complementos de Microsoft 365
ms.topic: Microsoft 365 plugins
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: 3a1847a01687d2d363f29938ed589d3a12179c9c
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63454055"
---
# <a name="microsoft-365-plugins"></a>Complementos de Microsoft 365

Los complementos de Microsoft 365 proporcionan integración entre el sitio web de Moodle y Teams. Estos complementos facilitan al usuario la programación, entrega y colaboración del contenido del curso. Los complementos pueden utilizarse de forma independiente o en asociación, según las necesidades.

## <a name="plugin-list-and-labels"></a>Lista de complementos y etiquetas

La siguiente tabla enumera los complementos y las etiquetas de GitHub que deben utilizarse en función de los requisitos.

<!--Old content of the table updated and revamped |Plugins to install |Description |GitHub label(s)|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|Enable SSO for users who work using both Moodle and Microsoft Teams|auth_oidc|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) |Create Teams instances for each course in Moodle, and sync faculty as owners, and students as team members|• auth_oidc </br> • local_o365|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Teams Theme**](#microsoft-365-teams-theme)| Remove Moodle blocks and extra chrome within the Moodle iframes for Teams, which applies while mapping courses to Teams instances | • auth_oidc </br> • local_o365 </br> • themeboost_o365teams |
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Microsoft 365 Repository**](#microsoft-365-repository) |Leverage Microsoft 365 OneDrive content for file repositories to reduce storage needs in Moodle | • auth_oidc </br> * local_o365 </br> • repository_office 365|
|• [**OpenID Connect**](#openid-connect) </br> • [**OneNote**](#onenote-integration) </br> • [**OneNote Submissions**](#onenote-integration) </br> • [**OneNote Feedback**](#onenote-integration) | Enable OneNote to be used for assignment, submission and feedback |• auth_oidc </br> • local_onenote </br> • assignsubmission_onenote </br> • assignfeedback_onenote |  
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) • [**Microsoft 365 Repository**](#microsoft-365-repository) </br> • [**Microsoft Block**](#microsoft-365-repository) | Enable 365 quick access blocks within Moodle with links to Microsoft 365 collaboration services and install links for Microsoft Office | • auth_oidc </br> • local_o365 </br> • repository_office365 </br> • block_microsoft |
|[**Teams Meeting**](#teams-meetings) | Enable Atto editor in Moodle to create Teams meeting links |atto_teamsmeeting |
|[**oEmbed Filter**](#oembed-filter) | Enable video links in Moodle | Filter_oembed| -->

|Complementos a instalar |Descripción |Etiquetas de GitHub|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|Permite el SSO para los usuarios que trabajan tanto con Moodle como con Teams.|auth_oidc|
|[**Integración con Microsoft 365**](#microsoft-365-integration)|Cree instancias de Teams para cada curso en Moodle, y sincronice a los profesores como propietarios, y a los estudiantes como miembros del equipo.|local_o365|
|[**Repositorio de Microsoft 365**](#microsoft-365-repository) |Admite el contenido de Microsoft 365 OneDrive para los repositorios de archivos para reducir las necesidades de almacenamiento en Moodle.| repository_office 365|
|[**Reunión de Teams**](#teams-meetings) |Habilita el editor Atto en Moodle para crear vínculos de reuniones de Teams.|atto_teamsmeeting |
|[**Tema de Teams**](#microsoft-365-teams-theme)| Eliminar los bloques de Moodle y el cromo extra dentro de los iframes de Moodle para Teams, que se aplica mientras se mapean los cursos a las instancias de Teams.| themeboost_o365teams |
|[**OneNote**](#onenote-integration)| Habilitar el uso de OneNote para la asignación, el envío y los informes|local_onenote, assignsubmission_onenote, y assignfeedback_onenote </br>|  
|[**Bloque de Microsoft**](#microsoft-block) | Habilita bloques de acceso rápido a Microsoft 365 dentro de Moodle con vínculos a los servicios de colaboración de Microsoft 365 y vínculos de instalación para Microsoft Office.|block_microsoft |
|[**Filtro de oEmbed**](#oembed-filter) | Habilitar los vínculos de vídeo en Moodle.|Filter_oembed|

Moodle LMS admite los siguientes complementos:

## <a name="openid-connect"></a>OpenID Connect

El complemento Open ID Connect permite a los usuarios autenticar cualquier sitio web o herramienta que admita la especificación necesaria y proporciona soporte de inicio de sesión único (SSO) con Microsoft Office 365. El complemento OpenID Connect ofrece a las instituciones las siguientes opciones de inicio de sesión para satisfacer sus necesidades específicas:

* Los usuarios pueden introducir sus credenciales de Office 365, como el correo electrónico y la contraseña para iniciar sesión directamente o iniciar sesión utilizando los campos de nombre de usuario y contraseña de Moodle, sin iniciar sesión en Office 365.
* Los usuarios pueden seleccionar el vínculo para iniciar sesión a través de Office 365 o del proveedor OpenID Connect en la página de Moodle.

La siguiente imagen muestra la página de inicio de sesión de OpenID connect:

:::image type="content" source="../../assets/images/MoodleInstructions/openid-connect.png" alt-text="Inicio de sesión para conectarse con open-id" border="true":::

## <a name="microsoft-365-integration"></a>Integración con Microsoft 365

La integración de Microsoft 365 se compone de varias aplicaciones con múltiples funcionalidades, lo que permite a los usuarios estar conectados y realizar diferentes acciones según sus necesidades. El complemento permite a los administradores comprobar lo siguiente:

* Compruebe las funciones de integración adecuadas.
* Sincronizar usuarios entre Office 365 y Moodle.
* Configurar los permisos necesarios para los usuarios.
* Configurar el sitio web de SharePoint para los archivos del curso.

La siguiente imagen muestra la página de configuración de la integración de Microsoft 365:

:::image type="content" source="../../assets/images/MoodleInstructions/365-integration.png" alt-text="Integración con Microsoft 365" border="true":::

### <a name="user-functions"></a>Funciones de usuario

Los usuarios pueden realizar las siguientes acciones con la integración de Microsoft 365:

* Compruebe el funcionamiento general de todas las integraciones de complementos de Microsoft 365.
* Cargar un archivo CSV, que compara los usuarios de Moodle con los de Office 365.
* Compruebe la configuración de los permisos de Azure AD.

## <a name="microsoft-365-repository"></a>Repositorio de Microsoft 365

El complemento del repositorio de Microsoft 365 permite a los usuarios almacenar los archivos del curso en OneDrive. Los profesores pueden agregar archivos desde la sección de archivos del curso de OneDrive o desde su propio espacio personal al repositorio.

El repositorio de Microsoft 365 permite al usuario utilizarlo como repositorio de archivos para una institución, manteniendo la estructura de datos de Moodle simple. El complemento del repositorio de Microsoft 365 proporciona los siguientes servicios:

* Los profesores puede almacenar los archivos del curso en OneDrive. Cada curso tiene su propia carpeta creada en OneDrive, lo que permite a los profesores agregar archivos desde el área de archivos del curso de OneDrive o desde su propio espacio personal.  
* Para agregar archivos a Moodle como copia o crear un vínculo al archivo. El archivo vinculado se muestra en una nueva ventana de la aplicación o se incrusta en la página web.
* Para subir archivos a OneDrive o SharePoint utilizando el selector de archivos de Moodle.

La siguiente imagen muestra el repositorio de archivos de Microsoft 365:

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-365- repository.png" alt-text="Repositorio M365"  border="true":::

## <a name="teams-meetings"></a>Reuniones de Teams

El complemento de reuniones de Teams permite al usuario crear solicitudes de reuniones en el calendario, las asignaciones, los mensajes del foro y también en el editor de Atto según la disponibilidad.

Una vez instalado el complemento, los profesores y los estudiantes pueden crear una reunión de audio o vídeo utilizando Moodle, lo que requiere una cuenta de Microsoft 365 y permisos de Moodle.

>[!NOTE]
>Las reuniones de Teams no aparecen en el calendario de Outlook o Teams, sin embargo, se pueden agregar nombres de estudiantes individuales a la invitación para las mismas.

La siguiente imagen muestra la página de registro de la reunión de Teams:

:::image type="content" source="../../assets/images/MoodleInstructions/teams-meeting.png" alt-text="iniciar sesión en la reunión de teams" border="true":::

## <a name="microsoft-365-teams-theme"></a>Tema de Teams en Microsoft 365

El complemento del tema de Teams en Microsoft 365 proporciona a los usuarios una vista personalizada de la página de inicio del curso de Moodle y está disponible para su visualización cuando el usuario accede a sus cursos de Moodle dentro de Teams.

El complemento del tema ofrece a los usuarios una experiencia mejorada y unificada con las siguientes características:

* Se adapta a los cambios de tema de Microsoft Teams, como el predeterminado, el oscuro y el de alto contraste.
* Proporciona un enfoque en las actividades del curso.
* Elimina los bloques de Moodle, la navegación, la encabezado y el pie de página.
* Proporciona elementos de la interfaz de usuario (UI) de Microsoft Team.

La siguiente imagen muestra el tema de Teams configurado por el usuario:

:::image type="content" source="../../assets/images/MoodleInstructions/teams-theme.png" alt-text="Tema de Microsoft Teams" border="true":::

## <a name="onenote-integration"></a>Integración a OneNote

El complemento de integración de OneNote proporciona a los usuarios opciones para navegar por los blocs de notas, las secciones y las páginas; donde se envían las tareas, y los profesores proporcionan los comentarios necesarios sobre las tareas correspondientes en OneNote. OneNote también mejora la experiencia del usuario agregando funciones que van más allá de las pruebas y los vínculos, al tiempo que amplía las capacidades al móvil mediante el uso de bolígrafos digitales, medios fotográficos o de vídeo, y la coautoría con grupos.

La integración de OneNote ayuda a acceder a los textos, gráficos y repositorios de audio. El complemento ofrece las siguientes ventajas:

* Incluye blocs de notas de navegación, secciones y páginas, donde los estudiantes trabajan en las tareas y proporcionan comentarios sobre esas tareas en OneNote.
* Combine la cuaderno digital para las notas, las tareas y los comentarios de referencia y revisión.
* Amplíe las capacidades de redacción más allá del texto y los vínculos, y extienda el uso del móvil utilizando bolígrafos digitales, medios fotográficos o de vídeo, y la coautoría con grupos.
* Incluya la página de envío y comentarios para cada tarea en la cuenta de los profesores Cuando se guarda dentro de Moodle, una copia del HTML y las imágenes asociadas se empaquetan en un archivo zip.

> [!NOTE]
> Los eventos de envío o comentarios desencadenan la creación de OneNote con una sección para cada curso en el que el estudiante se ha inscrito.

## <a name="microsoft-block"></a>Bloque de Microsoft

El complemento de bloqueo de Microsoft permite al usuario acceder a la ubicación del archivo de SharePoint del curso y ver el curso en el bloc de notas de OneNote para los envíos, junto con la opción de modificar las preferencias de integración de Office 365. Los administradores pueden configurar el bloque para que aparezca en todas las páginas del curso.

El bloque de Microsoft mejora la experiencia del usuario proporcionando una interfaz de usuario para modificar las características de integración de Microsoft 365 y el acceso a sus numerosos recursos. Los administradores pueden configurar el bloque para que los cambios modificados aparezcan en cada página del curso. El bloque permite al usuario realizar las siguientes actividades:

* Acceda a la ubicación del archivo de SharePoint del curso y al bloc de notas de OneNote.
* Ver el curso en el bloc de notas de OneNote para los envíos.
* Configure la sincronización Outlook calendario.
* Administra la conexión con Office 365.
* Personalizar las preferencias personales de integración de Office 365.

La siguiente imagen muestra la interfaz de usuario del bloque de Microsoft:

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-block-1.png" alt-text="bloque de Microsoft" border="true":::

## <a name="oembed-filter"></a>Filtro oEmbed

El complemento de filtro oEmbed simplifica y mejora la experiencia del usuario al simplificar la inclusión del contenido HTML externo dentro de Moodle. Las siguientes son las ventajas del filtro oEmbed. 

* Reduce el tiempo de incrustación de vídeos en una página HTML.
* Permite incrustar múltiples proveedores de contenidos de vídeo.
* Garantiza un método más rápido para copiar e incrustar el código de cualquiera de los servicios compatibles.
* Permite incrustar vídeos sin una clave API.

La siguiente imagen muestra la inclusión de contenido HTML externo dentro de Moodle:

:::image type="content" source="../../assets/images/MoodleInstructions/oEmbed-filter.png" alt-text="Página de filtro de oEmbed" border="true":::

## <a name="see-also"></a>Vea también

* [Aplicaciones de asociados para Moodle](../partner-apps-for-moodle.md)
* [Preguntas más frecuentes sobre Moodle](../faqs.md)