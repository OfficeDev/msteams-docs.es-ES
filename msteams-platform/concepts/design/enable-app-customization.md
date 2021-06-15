---
title: Habilitar la aplicación para personalizarla
author: heath-hamilton
description: Comprender cómo Teams los administradores pueden personalizar la aplicación para su organización.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: bf1b43629c87dd4123520c634772e5dea14e0bb5
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915086"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>Habilitar la aplicación Microsoft Teams personalizada

Puedes permitir a los clientes personalizar algunos aspectos de la aplicación Microsoft Teams en el centro Teams administración. Esta característica solo es compatible con las aplicaciones publicadas en la Teams tienda. Las aplicaciones y aplicaciones de instalación local publicadas para una organización no se pueden personalizar.

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

## <a name="see-also"></a>Ver también

* [Personalizar aplicaciones en el Centro Teams administración](/MicrosoftTeams/customize-apps)
