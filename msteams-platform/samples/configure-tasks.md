---
title: Configuración de tareas para clientes externos en la aplicación de control de colaboración
author: surbhigupta
description: En este módulo, aprenderá a configurar tareas para clientes externos en la aplicación de control de colaboración en Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 7d458cc97429772695958606835edd4ef953b5db
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243167"
---
# <a name="configure-tasks-for-external-clients"></a>Configurar Tasks para clientes externos

Tareas externas que se pueden asignar a usuarios que no forman parte de su organización o no tienen acceso a la aplicación, como asignar una tarea a un cliente.

Para habilitarlo, necesitará un paso adicional para pasar una cadena XML a cada instancia del control PCF de Tareas asociado al componente de subcuadrícula en el formulario MDA deseado. La cadena XML es una consulta parametrizada que permite al control extraer los datos necesarios de una tabla que contiene información del cliente.

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

Para crear tareas externas, siga estos pasos:

1. Cree una nueva entidad personalizada como Customer o reutilice una entidad de cliente existente como Contactos.

1. Cree nuevos campos que contengan la siguiente información:
    1. Nombre
    1. Correo electrónico
    1. Elemento primario (búsqueda en la tabla primaria, como inspecciones)
    > [!NOTE]
    > La entidad de cliente creada anteriormente es, donde el control de tareas extrae la información del cliente al asignar una tarea externa. El campo Primario garantiza que la entidad de cliente esté vinculada a un registro de inspección.

1. Genere un archivo Fetch XML para permitir que el control PCF extraiga la información correcta del cliente.

    **Configuración del esquema XML**

    A continuación se muestra la definición de esquema para la configuración de tareas Fetch XML. Cualquier xml de captura debe diseñarse para cumplir los siguientes requisitos:

    * El resultado de la consulta devolverá las siguientes propiedades para cada objeto de usuario:
      * Id.
      * Displayname
      * email, use alias si es necesario.
    * La consulta contendrá el parámetro **@top** para permitir que el autor de la llamada limite el número de resultados.
    * La consulta tendrá **@rootEntityId** parámetro para filtrar los resultados solo por registros relacionados, si es necesario.
    * La consulta debe tener **@useName** parámetro para permitir el filtrado de resultados por nombre
    * La consulta tendrá **@useIdentifier** parámetro para permitir la captura de solo los usuarios seleccionados.

    **Ejemplo y esquema XML de configuración**

    La configuración del esquema XML extrae datos de la tabla customer. Puede ajustar el `<fetch/>` nodo para especificar su propia consulta para mostrar usuarios de cualquier otra tabla personalizada.

    > [!NOTE]
    > El nombre de entidad y atributo anterior y el atributo order del XML **están en PublisherPrefix_TableColumn** formato.

    ```xml
    
    <custom-tasks> 
    <custom-task id="external" name="External" for="guest"> 
    <fetch top="@top"> 
    <entity name="[Name of table, e.g. Crb2891_customer]"> 
    <attribute name="[Name of ID column, e.g. Crb2891_customerid]" alias="id" /> 
    <attribute name="[Name of primary name column, e.g. Crb2891_name]" alias="displayname" /> 
    <attribute name="[Name of email column, e.g. Crb2891_email]" alias="email" /> 
    <order attribute ="[Name of primary name column, e.g. Crb2891_name]" descending="false" /> 
    <filter type="and"> 
    <condition attribute="[Name of parent lookup column, e.g. Crb2891_parent]" operator="eq" value="@rootEntityId" /> 
    <condition attribute="[Name of primary name column, e.g. Crb2891_name]" operator="like" value="@userName" /> 
    <condition attribute="[Name of email column, e.g. Crb2891_email]" operator="like" value="@userIdentifier" /> 
    </filter> 
    </link-entity> 
    </entity> 
    </fetch> 
    </custom-task> 
    </custom-tasks> 
    
    ```

1. Enlace los controles Task a la subcuadrícula dentro del diseñador de formularios clásico. Seleccione **Guardar** y, a continuación, **cambiar al clásico**.

1. Desplácese por el diseñador de formularios clásico hasta que encuentre la pestaña **Tareas** . Haga doble clic en la subcuadrícula para abrir el cuadro de diálogo de propiedades.

    :::image type="content" source="~/assets/images/collaboration-control/subgrid-property.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo de la propiedad tasks.":::

1. En el cuadro de diálogo de propiedades, establezca las propiedades como se muestra en la siguiente imagen:

    :::image type="content" source="~/assets/images/collaboration-control/tasks-property.png" alt-text="Sceenshot muestra para establecer las propiedades en la configuración de la propiedad Tasks.":::

1. Vaya a la pestaña Controles y seleccione :::image type="icon" source="~/assets/images/collaboration-control/edit-icon.png" alt-text="Captura de pantalla que muestra cómo editar las tareas."::: en la propiedad Tareas personalizadas para agregar el XML de captura generado anteriormente.

1. Pegar el archivo XML de captura

    :::image type="content" source="~/assets/images/collaboration-control/set-fetchproperties.png" alt-text="Captura de pantalla que muestra cómo pegar Fetch XML.":::

    :::image type="content" source="~/assets/images/collaboration-control/custom-tasksproperty.png" alt-text="Captura de pantalla que muestra cómo configurar las propiedades personalizadas.":::

1. Seleccione **Aceptar** en Configurar propiedad "Tareas personalizadas" y Establecer ventanas propiedades.

1. Guardar y publicar.
