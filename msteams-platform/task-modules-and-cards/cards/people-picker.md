---
title: Selector de usuarios en Tarjetas adaptables
description: Describe cómo usar el control Selector de personas en tarjetas adaptables
localization_priority: Normal
keywords: Selector de personas de tarjetas adaptables
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: 8a78be74d8142600ccc08093744491a19900e60b
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073431"
---
# <a name="people-picker-in-adaptive-cards"></a>Selector de usuarios en Tarjetas adaptables

>[!NOTE]
> Actualmente, el selector de personas en tarjetas adaptables está disponible en [versión preliminar para desarrolladores públicos](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) solo para dispositivos móviles y disponible con carácter general (GA) para escritorio.

Selector de personas ayuda a los usuarios a buscar y seleccionar usuarios en tarjeta adaptable. Puede agregar el selector de personas como control de entrada a la tarjeta adaptable, que funciona en chats, canales, módulos de tareas y pestañas. Selector de personas admite las siguientes características:

* Busca en uno o varios usuarios.
* Selecciona uno o varios usuarios.
* Reasigna a uno o varios usuarios.
* Rellena previamente el nombre de los usuarios seleccionados.

## <a name="popular-scenarios"></a>Escenarios populares

En la tabla siguiente se proporcionan escenarios populares para el selector de personas en tarjetas adaptables y las acciones correspondientes:

|Escenarios|Acciones|
|----------|-------------------------|
|Escenarios basados en la aprobación| Para solicitar, asignar y reasignar la aprobación al usuario previsto según el requisito.|
|Administración de incidencias| Para realizar un seguimiento de incidentes y notificar, asignar y reasignar al usuario previsto para realizar una acción inmediata.|
|Administración de proyectos| Para asignar incidencias o errores a usuarios concretos.|
|Búsqueda de usuarios| Para buscar usuarios en toda la organización.|

# <a name="desktop"></a>[Escritorio](#tab/desktop)

El cliente web y de escritorio admite el selector de personas en la tarjeta adaptable. Al buscar en la web, el selector de personas implica una experiencia de escritura en línea.

### <a name="reassignment-scenario-example"></a>Ejemplo de escenario de reasignación

El usuario A (Robert) recibe un vale para una tarea en un canal y se da cuenta de que el usuario asignado es incorrecto. El usuario A reasigna la tarea que envía la información al bot.

Para reasignar cualquier tarea:

1. Seleccione **Reasignar** donde se rellena previamente el campo selector de personas con el nombre para reasignar la tarea al usuario previsto.
1. Quite el nombre del usuario incorrecto.
1. Seleccione los usuarios previstos según el escenario de imagen, el usuario B (Mona) y el usuario C (Robin) para la tarea.
1. Seleccione **Asignar**. Después de la asignación, la información se envía al bot.
   El bot actualiza la tarjeta adaptable y notifica a los usuarios previstos.

En la imagen siguiente se muestra el escenario de reasignación:

![Selector de personas en el escritorio](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[Móvil](#tab/mobile)

> [!NOTE]
> Actualmente, esta característica solo está disponible en [versión preliminar para desarrolladores públicos](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) .

Los clientes móviles de Android e iOS admiten el selector de personas en tarjetas adaptables. Puede usar el selector de personas en el móvil para buscar y seleccionar usuario para mejorar la experiencia del usuario. La experiencia de búsqueda es similar a cualquier otra experiencia de selección de usuarios en dispositivos móviles.

### <a name="reassignment-scenario-example"></a>Ejemplo de escenario de reasignación

El usuario A (Robert) recibe un vale para una tarea en un canal y se da cuenta de que el usuario asignado es incorrecto. El usuario A reasigna la tarea que envía la información al bot.

Para reasignar cualquier tarea:

1. Seleccione **Reasignar** donde se rellena previamente el campo selector de personas con el nombre para reasignar la tarea al usuario previsto.
1. Quite el nombre del usuario incorrecto.
1. Seleccione los usuarios previstos según el escenario de imagen, el usuario B (Mona) y el usuario C (Robin) para la tarea.
1. Seleccione **Listo**.
1. Seleccione **Asignar**. Después de la asignación, la información se envía al bot.
   El bot actualiza la tarjeta adaptable y notifica a los usuarios previstos.

En la imagen siguiente se muestra el escenario de reasignación:

![Selector de personas en el móvil](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>Implementar selector de personas

El selector de personas se implementa como una extensión del control [Input.ChoiceSet](https://adaptivecards.io/explorer/Input.ChoiceSet.html) . El control de entrada incluye las siguientes selecciones:

* Lista desplegable, como una selección expandida.
* Botón de radio, como una sola selección.
* Casillas, como varias selecciones.  

> [!NOTE]
> El `Input.ChoiceSet` control se basa en las `style` propiedades y `isMultiSelect` .  

### <a name="update-schema"></a>Actualizar esquema

Las siguientes propiedades son adiciones al esquema para habilitar la `Input.ChoiceSet` experiencia del selector de personas en la tarjeta:  

#### <a name="inputchoiceset-control"></a>Control Input.ChoiceSet

|Propiedad |Tipo |Obligatorio |Descripción |
|----|----|----|----|
|**choices.data** |**Data.Query** |No |Habilita el autocompletar dinámico para distintos tipos de usuario mediante la captura de resultados del conjunto de datos especificado. |

#### <a name="dataquery"></a>Data.Query

|Propiedad |Tipo |Obligatorio |Descripción|
|--|--|--|--|
|**Dataset** |Cadena |Sí |Tipo de datos que se deben capturar dinámicamente.|

#### <a name="dataset"></a>Dataset

En la tabla siguiente se proporcionan valores predefinidos como **conjunto de datos** para el selector de personas:

|Dataset|Ámbito de búsqueda
|--|--|
|**graph.microsoft.com/users** |Busque en todos los miembros de la organización.|
|**graph.microsoft.com/users?scope=currentContext** |Busque en los miembros de la conversación actual, como chat o canal en el que se envía la tarjeta determinada.|

### <a name="example"></a>Ejemplo

El ejemplo de código para crear el selector de personas con la búsqueda de la organización es el siguiente:

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

En la imagen siguiente se muestra el selector de personas en tarjetas adaptables con la búsqueda de la organización:

:::image type="content" source="../../assets/images/Cards/peoplepicker-org-search.png" alt-text="Búsqueda de la organización del selector de personas":::

Para habilitar la búsqueda en una lista de miembros de conversación, use el conjunto de datos adecuado definido en la tabla [del conjunto de datos](#dataset) . `isMultiSelect` se usa para habilitar la selección de varios usuarios en el control. Se establece en false de forma predeterminada y esta configuración le permite seleccionar solo un usuario.

### <a name="data-submission"></a>Envío de datos

Puede usar `Action.Submit` o `Action.Execute` enviar los datos seleccionados al bot. La `invoke` carga recibida en el bot es una lista de identificadores de Microsoft Azure Active Directory (Azure AD) o los identificadores proporcionados en la lista estática.
En selector de personas, cuando se selecciona un usuario en el control, el `Azure AD ID` valor del usuario es el que se devuelve. `Azure AD ID` es una cadena e identifica de forma única a un usuario en el directorio.

El formato del valor enviado al bot depende del valor de la `isMultiSelect` propiedad :

|valor de `isMultiSelect`|Formato|
|--|--|
|false _(selección única)_|<selected_Azure_AD_ID>|
|true _(selección múltiple)_|<selected_Azure_AD_ID_1>,<selected_Azure_AD_ID_2>,<selected_Azure_AD_ID_3>|  

Con , el `Azure AD ID`selector de personas preselecciona al usuario correspondiente.

## <a name="preselection-of-user"></a>Preselección del usuario

Selector de personas admite la preselección del usuario en el control al crear y enviar una tarjeta adaptable. `Input.ChoiceSet` admite la `value` propiedad que se usa para preseleccionar a un usuario. El formato de esta `value` propiedad es el mismo que el formato de valor enviado en el [envío de datos](#data-submission).  
En la lista siguiente se proporciona la información para preseleccionar usuarios:

* Para un único usuario del control, especifique el `Azure AD ID` del usuario como `value`.
* Para varios usuarios, como `isMultiSelect` es `true`, especifique una cadena separada por comas de `Azure AD ID`s.  

En el ejemplo siguiente se describe la preselección de un único usuario:

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

En el ejemplo siguiente se describe la preselección de varios usuarios:

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

Las opciones estáticas admiten escenarios en los que se deben insertar perfiles personalizados en los conjuntos de datos predefinidos. `Input.ChoiceSet` admite la especificación `choices` estática en json. La opción estática se usa para crear las opciones a partir de las cuales el usuario puede seleccionar.

> [!NOTE]
> Las estáticas `choices` se usan con conjuntos de datos dinámicos.

La elección consta de `title` y `value`. Cuando se usan junto con el selector de personas, estas opciones se convierten en perfiles de usuario que tienen como `title` nombre y `value` como identificador. Estos perfiles personalizados también forman parte de los resultados de la búsqueda cuando la consulta de búsqueda coincide con el especificado `title`.
En el ejemplo siguiente se describen las opciones estáticas:

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

En la imagen siguiente se muestra el selector de personas en tarjetas adaptables con opciones estáticas en la búsqueda de la organización:

:::image type="content" source="../../assets/images/Cards/peoplepicker-static-choice.png" alt-text="people-picker-static-choice":::

Puede implementar el selector de personas para una administración eficaz de tareas en diferentes escenarios.  

## <a name="code-sample"></a>Ejemplo de código

| Nombre de ejemplo           | Descripción | C#    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Control de selector de personas en tarjetas adaptables| En este ejemplo se muestra cómo usar el control selector de personas en tarjetas adaptables.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/nodejs) |

## <a name="see-also"></a>Consulte también

[Referencia de tarjetas](cards-reference.md)
