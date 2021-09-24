---
title: Habilitar la aplicación para personalizarla
author: heath-hamilton
description: Comprender cómo Teams los administradores pueden personalizar la aplicación para su organización.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 193b4baeee16badb1dcb26139831d3e298de9a5c
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157112"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>Habilitar la aplicación Microsoft Teams personalizada

Puedes permitir a los clientes personalizar algunos aspectos de la aplicación Microsoft Teams en el centro Teams administración. Esta característica solo es compatible con las aplicaciones publicadas en la Teams tienda. Las aplicaciones y aplicaciones de instalación local publicadas para una organización no se pueden personalizar.

Algunos ejemplos posibles de esta característica incluyen:

* Cambiar el color de acento de la aplicación para que coincida con la marca de una organización.
* Actualizar el nombre de la aplicación de *Contoso* al *agente contoso*, que es el nombre que verán los usuarios de la organización. (Nota: Los usuarios que agreguen un conector a un chat o un canal seguirán ven el nombre de la aplicación original, *Contoso*.)

Puede habilitar esta característica en el Portal de [desarrolladores para Teams](https://dev.teams.microsoft.com/home). Esto configura , que no está disponible en versiones anteriores a `configurableProperties` la 1.10 del manifiesto Teams aplicación.

## <a name="test-your-app"></a>Probar la aplicación

No puede probar esta característica durante el desarrollo. La personalización de aplicaciones no se admite al cargar o publicar localmente en el catálogo de aplicaciones de una organización.

## <a name="user-considerations"></a>Consideraciones del usuario

Proporciona instrucciones para los clientes (específicamente Teams administradores) que desean personalizar la aplicación. Para obtener más información, [consulta Personalizar aplicaciones en Teams](/MicrosoftTeams/customize-apps).

## <a name="see-also"></a>Vea también

* [Personalizar aplicaciones en el Centro Teams administración](/MicrosoftTeams/customize-apps)
