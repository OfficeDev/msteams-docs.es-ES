---
title: Preguntas frecuentes
description: Respuestas a algunas preguntas comunes
ms.topic: Frequently asked questions on Moodle LMS
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: 587451e3a0e89206a4ea49aaca3c682ab290ac5b
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63454034"
---
# <a name="moodle-faq"></a>Preguntas más frecuentes sobre Moodle

Obtenga respuestas a algunas de sus dudas al utilizar Moodle LMS.<br>

<br>

<details>

<summary><b>¿Qué debo hacer si uno o varios equipos del curso no se han creado después de la sincronización?</b></summary>

Cada curso de Moodle debe tener al menos un profesor y un estudiante emparejados con una cuenta UPN de Microsoft 365 AAD. El equipo no puede ser creado, si la sincronización no encuentra una coincidencia.

Cada instancia de curso de equipo debe tener un propietario, y la sincronización establece la facultad como el propietario, con la suposición de que la facultad tiene la licencia de Teams.

<br>

</details>

<details>

<summary><b>¿Qué debemos hacer para eliminar la página de inicio de sesión de Moodle cuando se trabaja desde Teams? ¿Podemos forzar el inicio de sesión único (SSO)?</b></summary>

Los usuarios tienen múltiples opciones de inicio de sesión desde la página de inicio de sesión de Moodle.

* Para iniciar sesión exclusivamente con las credenciales de Microsoft 365, active los ajustes de configuración de la **redirección forzada** para el **complemento auth_oidc**. Si el servicio está activado, el usuario puede ver la página de inicio de sesión de Microsoft.
* Para iniciar la sesión manualmente en el portal de Moodle consulte [Moodle](https://moodle.org/login/index.php).

<br>

</details>

<details>

<summary><b>¿Cómo puedo especificar qué usuarios sincronizar? No quiero que todos los usuarios de Azure AD se sincronicen con el sitio web de Moodle. </b></summary>

Utilice la opción de **Restricción de creación de usuarios** para especificar los usuarios sincronizando las opciones de configuración del complemento **local_o365**. El menú desplegable a la izquierda del **filtro** ofrece opciones como el país, el nombre de la empresa y el idioma.

> [!TIP]
> Cree un grupo dinámico de Microsoft 365 para habilitar la opción de **filtro** con múltiples propiedades de perfil.

La siguiente imagen muestra las opciones de restricción de creación de usuarios:

:::image type="content" source="../assets/images/MoodleInstructions/faq-2.png" alt-text="Sync" border="true":::

:::image type="content" source="../assets/images/MoodleInstructions/faq-3.png" alt-text="Azure AD" border="true":::

<br>

</details>

<details>

<summary><b>¿Nos gustaría que nuestros profesores pudieran sincronizar los cursos con Teams? ¿Son los administradores de Moodle los únicos que pueden controlar la sincronización de los cursos?</b></summary>

Por defecto, sólo los administradores de Moodle pueden configurar la sincronización. El propietario del equipo puede controlar si un curso se sincroniza con Teams y si la opción **Permitir configurar la sincronización del curso en el curso** está activada. En este caso, el propietario del equipo es el profesor. El bloque muestra la opción de configuración a las personas con los permisos de propietario adecuados. 

<!-- For more information, see Microsoft 365 block within the Moodle course interface. -->

La siguiente imagen muestra la opción **Permitir configurar la sincronización del curso en el curso**:

:::image type="content" source="../assets/images/MoodleInstructions/faq-4.png" alt-text="administrador" border="true":::

La siguiente imagen muestra la sincronización de los cursos:

:::image type="content" source="../assets/images/MoodleInstructions/faq-5.png" alt-text="sincronización" border="true":::

<br>

</details>

<details>

<summary><b> Hemos seguido la documentación, pero las cuentas de usuario no consiguen sincronizar AAD y Moodle. ¿Qué debemos hacer?</b></summary>

El problema puede resolverse antes de que los usuarios realicen la **limpieza de tokens Delta** como último paso para solucionar el problema.

La siguiente tabla proporciona las acciones y dependencias que deben realizarse y comprobarse:

| Dependencia  | Acción | Referencia|
|-------|------------|----------|
| Versión estable| Compruebe que la versión de Moodle aparece como **estable**.| Para más información, consulte [Compatibilidad de versión](https://docs.moodle.org/dev/Releases#Version_support).|
|Permisos| Verifique que la aplicación Azure tiene los permisos necesarios para ejecutar la sincronización.| Para obtener más información, consulte los [permisos de Microsoft](https://docs.moodle.org/311/en/Microsoft_365#Permissions).|
| Sincronización completa| Verifique que la opción **Realizar una sincronización completa cada vez que se ejecute** esté activada y revise los **Registros de tareas** para **Sincronizar usuarios con Azure AD**.| Para más información, consulte [Habilitar la sincronización completa](https://docs.moodle.org/311/en/local_o365)</br>Para obtener más información, consulte [Comprobar los registros de tareas](https://docs.moodle.org/311/en/local_o365#Sync_users_with_Azure_AD). |
|Actualización de tokens|Limpiar el **token delta de sincronización de usuarios** en el complemento local_o365.| Para más información, consulte [Actualización de fichas](https://docs.moodle.org/38/en/Office365).|
<!-- |Actualización de tokens|Limpiar el **token delta de sincronización** de usuario en el complemento local_o365 usuario| {moodle_url}\local_o365\acp.php? Mode=maintenance_cleandeltatoken| -->
<br>

</details>

<details>

<summary><b>Uno o varios usuarios no pueden iniciar sesión con sus credenciales de Microsoft 365, aunque la mayoría de los usuarios pueden iniciar sesión sin problemas. Cuál sería la causa de esta incoherencia?</b></summary>

El motivo de las incoherencias con los usuarios que no pueden firmar con sus credenciales de Microsoft 365 puede estar relacionado con la operación de asignación de usuarios durante la sincronización. Para resolver el problema, realice los siguientes pasos:

* Compruebe si el tipo de autenticación del usuario de Moodle es **OpenID**.
* Compruebe si el **Nombre de usuario** de Moodle coincide con el nombre de usuario de AAD.
* Limpie la **emisión de Tokens** e inténtelo de nuevo.
* Compruebe si los usuarios tienen **permisos** para acceder a la aplicación Azure.

<br>

</details>

<details>

<summary><b>Todos los usuarios no pueden iniciar sesión con sus credenciales de Microsoft 365. ¿Qué podemos hacer para resolver esto?</b></summary>

Los usuarios que no pudieron iniciar sesión al principio deben informar del problema y verificar que el **Secreto del cliente** de la aplicación no ha caducado.

La siguiente imagen muestra el mensaje de error que se recibe cuando el usuario firma con sus credenciales de Microsoft 365:

:::image type="content" source="../assets/images/MoodleInstructions/faq-6.png" alt-text="Notificar problema" border="true":::

La siguiente imagen muestra el error en el portal de Azure:

:::image type="content" source="../assets/images/MoodleInstructions/faq-7.png" alt-text="Portal de Azure" border="true":::

Si el **Secreto del cliente** ha caducado, el usuario debe generar un nuevo **Secreto de cliente** y actualizar la configuración que se encuentra en la página. Los usuarios pueden volver a iniciar sesión después de que se haya actualizado el **Secreto del cliente**, lo que puede tardar hasta 24 horas en volver a aprovisionarse.

<br>

</details>

<details>

<summary><b>¿Cómo cambiar la instancia de los equipos que está vinculada a un curso?</b></summary>

Los administradores pueden cambiar la instancia de equipos asociada a un curso a través de la página **Administrar conexiones de Teams**. Seleccione **Conectar** junto al curso que desea cambiar y seleccione la instancia de equipos. Si utiliza el restablecimiento del curso para archivar un equipo, puede enlazarlo de nuevo con el equipo anterior.

La siguiente imagen muestra la instancia de los equipos:

:::image type="content" source="../assets/images/MoodleInstructions/faq-8.png" alt-text="instancia de equipos" border="true":::

<br>

</details>

<details>

<summary><b> ¿Por qué no aparece la integración de las reuniones de equipos de Atto en el editor de Atto? </b></summary>

El usuario puede enfrentarse al problema de las reuniones de Atto Teams si falta la referencia al icono en la **Configuración de la barra de herramientas**, que muestra el icono de Teams en el editor de Atto. El usuario tiene que agregar el icono de la reunión de Teams a la derecha del icono de vínculos siguiendo los siguientes pasos:

* Instalar el complemento
* Actualizar la **Configuración de la barra de herramientas** con la **reunión de los equipos**.

Las siguientes imágenes muestran el icono de la barra de herramientas después del ajuste de la configuración de la barra de herramientas:

:::image type="content" source="../assets/images/MoodleInstructions/faq-9.png" alt-text="barra de herramientas" border="true":::

:::image type="content" source="../assets/images/MoodleInstructions/faq-10.png" alt-text="icono de vínculos":::

Para obtener más información sobre la edición de la barra de herramientas Atto, consulte:

* [Editor de Atto para los ModdleDocs](https://docs.moodle.org/311/en/Atto_editor)
* [Asignación de icono de editor de Atto](https://docs.moodle.org/311/en/Atto_editor#:~:text=in%20the%20editor.-,Atto%20editor%20toolbar,-Atto%20Row%201)
<br>

</details>

<details>

<summary><b>¿Las reuniones programadas a través de la integración de Microsoft aparecen en Outlook o en los calendarios de Teams? ¿Cuál es el plazo estándar para que aparezcan las reuniones?</b></summary>

Las reuniones programadas a través de la aplicación no aparecen en el calendario de Outlook o Teams del programador, ya que son similares a las Reuniones del Canal. Todos los miembros del canal del curso pueden asistir a la reunión directamente desde el vínculo del canal incrustado. Para obtener más información, consulte [Reuniones de canal](https://www.knowledgewave.com/blog/benefits-of-channel-meetings-in-microsoft-teams).

Sin embargo, puede acceder a la invitación y agregar manualmente los nombres de los participantes a los campos **Obligatorio** u **Opcional** de la invitación a la reunión para mostrar la reunión remota en sus calendarios. Los plazos estándar se basan en la fecha que el usuario especifica al crear la reunión. Para obtener más información, consulte [Límites y especificaciones de Teams](/microsoftteams/limits-specifications-teams).

<br>

</details>

<details>

<summary><b>¿Existe algún sitio de apoyo donde podamos obtener más ayuda sobre los productos y otros problemas?</b></summary>

Para obtener asistencia y ayuda sobre los problemas del producto y los servicios o la ayuda de la comunidad de desarrolladores, consulte el apartado [Asistencia y comentarios](/microsoftteams/platform/feedback)


