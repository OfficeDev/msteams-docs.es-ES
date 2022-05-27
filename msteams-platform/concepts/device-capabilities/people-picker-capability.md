---
title: Integrar Selector de personas
description: Uso del SDK de cliente de JavaScript de Teams para integrar el control Selector de personas
keywords: Control Selector de personas
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: a2e2a21f0485e0df87f8963defbe54ed540e455a
ms.sourcegitcommit: d9025e959dcdd011ed4feca820dae7c5d1251b27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65755898"
---
# <a name="integrate-people-picker"></a>Integrar Selector de personas

Selector de personas es un control de entrada en Teams que permite a los usuarios buscar y seleccionar personas. Puede integrar el control de entrada Selector de personas en una aplicación web, lo que permite a los usuarios finales realizar diferentes funciones, como buscar y seleccionar personas en un chat, canal o en toda la organización dentro de Teams. El control Selector de personas está disponible en todos los clientes de Teams, ya sea en la Web, el escritorio o el móvil.

Puede usar el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), que proporciona la API `selectPeople` para integrar el control de entrada de Selector de personas en la aplicación web.

## <a name="advantages-of-using-people-picker"></a>Ventajas del uso de Selector de personas

* Funciona en todas las funcionalidades de Teams, como el módulo de tareas, el chat, el canal, la pestaña de la reunión y la aplicación personal.
* Permite al usuario buscar y seleccionar personas en un chat, canal o toda la organización dentro de Teams.
* Ayuda en escenarios que implican la asignación de tareas, el etiquetado y la notificación al usuario.
* Ahorra mucho tiempo y esfuerzo en comparación con la creación de cualquier control similar.

Para integrar el control de entrada de Selector de personas en la aplicación Teams, use la API [`selectPeople`](#selectpeople-api). Para integrar y llamar a la API, debe comprender bien el [fragmento de código](#code-snippet) adjunto. También necesita familiarizarse con los [errores de respuesta de la API](#error-handling).

## <a name="selectpeople-api"></a>API `selectPeople`

La API `selectPeople` le permite agregar el control de entrada de Selector de personas en Teams a las aplicaciones web y también le ayuda con lo siguiente:

* Permite al usuario buscar y seleccionar una o más personas de la lista.
* Devuelve el identificador, el nombre y la dirección de correo electrónico de los usuarios seleccionados a la aplicación web.

En caso de una aplicación personal, el control busca el nombre o el identificador de correo electrónico en toda la organización dentro de Teams. Si la aplicación se agrega a un chat o canal, el contexto de búsqueda se configura en función del escenario. La búsqueda está restringida a los miembros de ese chat o canal.

La API `selectPeople` incluye las siguientes configuraciones de entrada:

|Parámetro de configuración|Tipo|Descripción| Valor predeterminado|
|-----|------|--------------|------|
|`title`|Cadena| Es un parámetro opcional y establece el título del control Selector de personas.|`selectPeople`|
|`setSelected`|Cadena| Es un parámetro opcional. Debe pasar los identificadores de Microsoft Azure Active Directory (Azure AD) de las personas que se van a preseleccionar. Este parámetro preselecciona a las personas al iniciar el control de entrada Selector de personas. En caso de una sola selección, solo el primer usuario válido se rellena previamente ignorando el resto.|**Null**|
|`openOrgWideSearchInChatOrChannel`|Boolean| Es un parámetro opcional y cuando se establece en True, inicia el Selector de personas en el ámbito de toda la organización incluso si la aplicación se agrega a un chat o canal.|**False**|
|`singleSelect`|Boolean|Es un parámetro opcional y cuando se establece en True, inicia el Selector de personas y restringe la selección a un solo usuario.|**False**|

En la siguiente imagen se muestra la experiencia del Selector de personas en dispositivos móviles y de escritorio:

# <a name="mobile"></a>[Móvil](#tab/Samplemobileapp)

El control de entrada de Selector de personas permite al usuario buscar y agregar personas mediante los siguientes pasos:

1. Escriba el nombre de la persona que quiere invitar. La lista aparece con sugerencias de nombre.
1. Seleccione el nombre de la persona necesaria de la lista. 

   :::image type="content" source="../../assets/images/tabs/people-picker-control-capability-mobile-updated.png" alt-text="Picker Picker Móvil" border="true":::

# <a name="desktop"></a>[Escritorio](#tab/Sampledesktop)

El control Selector de personas en la web o el escritorio se inicia en una ventana modal en la parte superior de la aplicación web y para agregar personas, siga estos pasos:

1. Escriba el nombre de la persona que quiere invitar. La lista aparece con sugerencias de nombre.
1. Seleccione el nombre de la persona necesaria de la lista. 

   :::image type="content" source="../../assets/images/tabs/select-people-picker-byname.png" alt-text="Selector de personas por nombre Escritorio" border="true":::

---

## <a name="code-snippet"></a>Fragmento de código

El siguiente fragmento de código muestra el uso de los usuarios de la API `selectPeople` de una lista:

```javascript
microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  },{ setSelected: ["aad id"], openOrgWideSearchInChatOrChannel: true, singleSelect: false});
```

## <a name="error-handling"></a>Control de errores

En la tabla siguiente se enumeran los códigos de error y sus descripciones:

|Código de error |  Nombre de error     | Descripción|
| --------- | --------------- | --------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **500** | INTERNAL_ERROR | Error interno detectado al iniciar Selector de personas.|
| **4000** | InvalidArguments | La API se invoca con argumentos obligatorios incorrectos o insuficientes.|
| **8000** | USER_ABORT |El usuario canceló la operación.|
| **9000** | OLD_PLATFORM | El usuario se encuentra en una compilación de plataforma antigua donde la implementación de la API no está disponible. Actualice a la versión más reciente de la compilación para resolver el problema.|

## <a name="see-also"></a>Consulte también

* [Integrar funcionalidades multimedia en Teams](mobile-camera-image-permissions.md)
* [Integrar la funcionalidad de escáner de código QR o código de barras en Teams](qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
