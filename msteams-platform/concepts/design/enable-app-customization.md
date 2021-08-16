---
title: Habilitar la aplicación para personalizarla
author: heath-hamilton
description: Comprender cómo Teams los administradores pueden personalizar la aplicación para su organización.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 0af96eebb50aeb650cdd5a1b3bd6a93439fb57b8
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345568"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>Habilitar la aplicación Microsoft Teams personalizada

Puedes permitir a los clientes personalizar algunos aspectos de la aplicación Microsoft Teams en el centro Teams administración. Esta característica solo es compatible con las aplicaciones publicadas en la Teams tienda. Las aplicaciones y aplicaciones de instalación local publicadas para una organización no se pueden personalizar.

> [!IMPORTANT]
> Actualmente, las aplicaciones de instalación local están disponibles en Government Community Cloud (GCC), pero no están disponibles para GCC-High y departamento de defensa (DOD).

Algunos ejemplos posibles de esta característica incluyen:

* Cambiar el color de acento de la aplicación para que coincida con la marca de una organización.
* Actualizar el nombre de la aplicación de *Contoso* al *agente contoso*, que es el nombre que verán los usuarios de la organización. (Nota: Los usuarios que agreguen un conector a un chat o un canal seguirán ven el nombre de la aplicación original, *Contoso*.)

Puede habilitar esta característica en el Portal de [desarrolladores para Teams](https://dev.teams.microsoft.com/home). Esto configura , que no están disponibles en versiones anteriores a `configurableProperties` la 1.10 del manifiesto Teams aplicación.

## <a name="test-your-app"></a>Probar la aplicación

No puede probar esta característica durante el desarrollo. La personalización de aplicaciones no se admite para la instalación local o la publicación en el catálogo de aplicaciones de una organización.

## <a name="user-considerations"></a>Consideraciones del usuario

Como editor de aplicaciones, proporcione la siguiente información a los clientes de Teams administradores:
* Incluya una nota que recomiende probar los cambios de personalización en Teams inquilino de prueba antes de realizar cambios en su entorno de producción. 
* Proporciona procedimientos recomendados para personalizar la aplicación.

## <a name="see-also"></a>Vea también

* [Personalizar aplicaciones en el Centro Teams administración](/MicrosoftTeams/customize-apps)
