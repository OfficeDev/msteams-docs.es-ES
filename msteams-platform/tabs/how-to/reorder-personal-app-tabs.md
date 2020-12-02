---
title: Reordenar pestañas de aplicaciones personales
description: Cómo cambiar el orden de las pestañas estáticas de la aplicación personal en su aplicación personal
keywords: desarrollo de pestañas de Microsoft Teams
ms.openlocfilehash: a8a7c3d23bac98ef1085a8f3443ca0fc92ae0a31
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "49554832"
---
# <a name="reorder-personal-app-tabs"></a>Reordenar pestañas de aplicaciones personales

A partir de la versión del manifiesto 1,7, los desarrolladores pueden reorganizar todas las pestañas en su aplicación personal. En concreto, un desarrollador puede mover la pestaña "chat de bot" (que siempre tiene el valor predeterminado a la primera posición) en cualquier lugar del encabezado de la pestaña de la aplicación personal. Hemos declarado dos palabras clave de entityId de pestaña reservadas: "Conversations" y "About".

## <a name="moving-the-chatconversation-tab"></a>Mover la pestaña "chat/conversación"

Si crea un bot con un ámbito "personal", se mostrará siempre en la primera tabulación de una aplicación personal. Si desea moverla a otro lugar, debe agregar un objeto de pestaña estático al manifiesto con la palabra clave reservada "conversaciones". Siempre que agregue la pestaña "conversaciones" en la matriz "staticTabs", aquí es donde aparecerá la ficha conversación en el escritorio y en la Web. 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

> [!NOTE]
> Tenga en cuenta que este comportamiento no se ve reflejado en dispositivos móviles, ya que el chat de bot personal ya tiene un lugar dedicado dentro de la aplicación personal.

## <a name="moving-the-about-tab"></a>Mover la pestaña "acerca de"

La pestaña "acerca de" siempre es el final de la barra de encabezado de la pestaña de la aplicación personal. Si desea moverla a otra posición, debe usar la "acerca de" entityId.

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
> [!NOTE]
> Tenga en cuenta que la pestaña acerca de no se muestra en dispositivos móviles.

## <a name="example-code"></a>Código de ejemplo

```json
{
   "staticTabs":[
      {
         "entityId":"homeTab",
         "name":"Home",
         "contentUrl":"https://www.contoso.com",
         "websiteUrl":" https://www.contoso.com ",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
