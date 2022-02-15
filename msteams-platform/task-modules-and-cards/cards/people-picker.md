---
title: Selector de usuarios en Tarjetas adaptables
description: Describe cómo usar el control Selector de personas en tarjetas adaptables
localization_priority: Normal
keywords: Selector de personas de tarjetas adaptables
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: 18e4268258e008485617cb10fd11070963cf3ed1
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821636"
---
# <a name="people-picker-in-adaptive-cards"></a>Selector de usuarios en Tarjetas adaptables

>[!NOTE]
> Actualmente, el Selector de personas en tarjetas adaptables [](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) solo está disponible en la versión preliminar de desarrolladores públicos para dispositivos móviles y, por lo general, disponible (GA) para escritorio.

El Selector de personas ayuda a los usuarios a buscar y seleccionar usuarios en la tarjeta adaptable. Puedes agregar el Selector de personas como control de entrada a la tarjeta adaptable, que funciona en chats, canales, módulos de tareas y pestañas. El Selector de personas admite las siguientes características:        

* Busca en uno o varios usuarios.
* Selecciona uno o varios usuarios. 
* Reasigna a uno o varios usuarios. 
* Rellenar previamente el nombre de los usuarios seleccionados.

## <a name="popular-scenarios"></a>Escenarios populares 

En la tabla siguiente se proporcionan escenarios populares para el Selector de personas en tarjetas adaptables y las acciones correspondientes:

|Escenarios|Acciones|
|----------|-------------------------|
|Escenarios basados en aprobación| Para solicitar, asignar y reasignar la aprobación al usuario previsto en función del requisito.|
|Administración de incidencias| Para realizar un seguimiento de incidentes y notificar, asignar y reasignar al usuario previsto para una acción inmediata.| 
|Administración de proyectos| Para asignar vales o errores a usuarios concretos.|
|Búsqueda de usuarios| Para buscar usuarios en toda la organización.|

# <a name="desktop"></a>[Escritorio](#tab/desktop)

El cliente web y de escritorio admiten el selector de personas en la tarjeta adaptable. Durante la búsqueda en la web, el selector de personas implica una experiencia de escritura en línea.

### <a name="reassignment-scenario-example"></a>Ejemplo de escenario de reasignación

El usuario A (Robert) recibe un vale para una tarea en un canal y se da cuenta de que el usuario asignado es incorrecto. El usuario A reasigna la tarea que devuelve la información al bot. 

**Para reasignar cualquier tarea**

1. Seleccione **Reasignar** donde el campo del selector de personas está prepoblado con el nombre para reasignar la tarea al usuario previsto.
1. Quite el nombre del usuario incorrecto. 
1. Seleccione los usuarios previstos según el escenario de imagen, el usuario B (Mona) y el usuario C (Robin) para la tarea. 
1. Seleccione **Asignar**. Después de asignar, la información se envía al bot. 
   El bot actualiza la tarjeta adaptable y notifica a los usuarios previstos. 
 
La siguiente imagen muestra el escenario de reasignación:    

![Selector de personas en el escritorio](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[Móvil](#tab/mobile)

> [!NOTE]
> Actualmente, esta característica solo está disponible en [la versión preliminar del desarrollador](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) público.

Los clientes móviles de Android e iOS admiten el selector de personas en tarjetas adaptables. Puede usar el Selector de personas en el móvil para buscar y seleccionar usuario para mejorar la experiencia del usuario. La experiencia de búsqueda es similar a cualquier otra experiencia de selección de usuario en dispositivos móviles.

### <a name="reassignment-scenario-example"></a>Ejemplo de escenario de reasignación

El usuario A (Robert) recibe un vale para una tarea en un canal y se da cuenta de que el usuario asignado es incorrecto. El usuario A reasigna la tarea que devuelve la información al bot. 

**Para reasignar cualquier tarea**

1. Seleccione **Reasignar** donde el campo del selector de personas está prepoblado con el nombre para reasignar la tarea al usuario previsto.
1. Quite el nombre del usuario incorrecto.
1. Seleccione los usuarios previstos según el escenario de imagen, el usuario B (Mona) y el usuario C (Robin) para la tarea.
1. Seleccione **Listo**.
1. Seleccione **Asignar**. Después de asignar, la información se envía al bot. 
   El bot actualiza la tarjeta adaptable y notifica a los usuarios previstos. 

La siguiente imagen muestra el escenario de reasignación: 

![Selector de personas en móvil](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>Implementar selector de personas

El selector de personas se implementa como una extensión del control [Input.ChoiceSet](https://adaptivecards.io/explorer/Input.ChoiceSet.html) . El control de entrada incluye las siguientes selecciones:   

* Desplegable, como una selección expandida.
* Botón de radio, como una sola selección.
* Casillas, como varias selecciones.  

> [!NOTE]
> El `Input.ChoiceSet` control se basa en las `style` propiedades y `isMultiSelect` .  

### <a name="update-schema"></a>Actualizar esquema

Las siguientes propiedades son adiciones al esquema `Input.ChoiceSet` para habilitar la experiencia del selector de personas en la tarjeta:  

#### <a name="inputchoiceset-control"></a>Control Input.ChoiceSet

|Propiedad |Tipo |Necesario |Descripción |
|----|----|----|----|
|**choices.data** |**Data.Query** |No |Habilita el autocompletar dinámico para diferentes tipos de usuario mediante la captura de resultados del conjunto de datos especificado. |

#### <a name="dataquery"></a>Data.Query

|Propiedad |Tipo |Obligatorio |Descripción|
|--|--|--|--|
|**conjunto de datos** |Cadena |Sí |Tipo de datos que se deben capturar dinámicamente.|   

#### <a name="dataset"></a>conjunto de datos
En la tabla siguiente se proporcionan valores predefinidos **como conjunto de datos** para el selector de personas:   

|conjunto de datos|Ámbito de búsqueda
|--|--|
|**graph.microsoft.com/users** |Busque en todos los miembros de la organización.|
|**graph.microsoft.com/users?scope=currentContext** |Busque dentro de los miembros de la conversación actual, como chat o canal en el que se envía la tarjeta en particular.|        

### <a name="example"></a>Ejemplo
El ejemplo de código para crear selector de personas con búsqueda de organización es el siguiente:

```json 
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```  

En la siguiente imagen se muestra el Selector de personas en tarjetas adaptables con la búsqueda de la organización:

![Búsqueda de la organización del selector de personas](../../assets/images/cards/peoplepicker-org-search.png)

Para habilitar la búsqueda en una lista de miembros de conversación, use el conjunto de datos adecuado definido en la tabla [del conjunto de](#dataset) datos. `isMultiSelect` se usa para habilitar la selección de varios usuarios en el control. Se establece en false de forma predeterminada y esta configuración permite seleccionar solo un usuario.

### <a name="data-submission"></a>Envío de datos

Puede usar o `Action.Submit` enviar `Action.Execute` datos seleccionados al bot. La `invoke` carga recibida en el bot es una lista de Microsoft Azure Active Directory (Azure AD) o los IDs proporcionados en la lista estática.
En el Selector de personas, cuando se selecciona un usuario en el control, `Azure AD ID` el del usuario es el valor devuelto. Se `Azure AD ID` trata de una cadena e identifica de forma única a un usuario en el directorio.

El formato del valor enviado al bot depende del valor de la `isMultiSelect` propiedad:

|valor de `isMultiSelect`|Formato|
|--|--|
|false _(selección única)_|<selected_Azure_AD_ID>|
|true _(selección múltiple)_|<selected_Azure_AD_ID_1>,<selected_Azure_AD_ID_2>,<selected_Azure_AD_ID_3>|  

Con el `Azure AD ID`selector de personas, se selecciona previamente el usuario correspondiente. 

## <a name="preselection-of-user"></a>Selección previa del usuario

El Selector de personas admite la selección previa del usuario en el control, al crear y enviar una tarjeta adaptable. `Input.ChoiceSet` admite la `value` propiedad que se usa para preseleccionar un usuario. El formato de esta propiedad `value` es el mismo que el formato de valor enviado en [el envío de datos](#data-submission).  
La siguiente lista proporciona la información para preseleccionar usuarios:

* Para un solo usuario del control, especifique el `Azure AD ID` del usuario como `value`. 
* Para varios usuarios, como `isMultiSelect` es `true`, especifique una cadena separada por comas de `Azure AD ID`s.  

En el ejemplo siguiente se describe la selección previa de un solo usuario:

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "value": "<Azure AD ID 1>"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```  

En el siguiente ejemplo se describe la selección previa de varios usuarios:

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true,
            "value": "<Azure AD ID 1>,<Azure AD ID 2>,<Azure AD ID 3>"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```
 
## <a name="static-choices"></a>Opciones estáticas

Las opciones estáticas admiten escenarios donde los perfiles personalizados deben insertarse en los conjuntos de datos predefinidos. `Input.ChoiceSet` admite la especificación `choices` estática en el json. La opción estática se usa para crear las opciones entre las que el usuario puede seleccionar.

> [!NOTE]
> Los estáticos `choices` se usan con conjuntos de datos dinámicos. 

La elección consta de `title` y `value`. Cuando se usa junto con el selector de personas, `title` estas opciones se convierten en perfiles de usuario que tienen el nombre y el `value` como identificador. Estos perfiles personalizados también forman parte de los resultados de búsqueda cuando la consulta de búsqueda coincide con el .`title`    
En el siguiente ejemplo se describen las opciones estáticas: 

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [
                {
                    "title": "Custom Profile 1",
                    "value": "Profile1"
                },
                {
                    "title": "Custom Profile 2",
                    "value": "Profile2"
                }
            ],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

En la siguiente imagen se muestra el Selector de personas en tarjetas adaptables con opciones estáticas en la búsqueda de la organización:

![Elección estática del selector de personas](../../assets/images/cards/peoplepicker-static-choice.png)


Puede implementar el selector de personas para una administración eficiente de tareas en diferentes escenarios.  

## <a name="see-also"></a>Vea también

[Referencia de tarjetas](cards-reference.md)

