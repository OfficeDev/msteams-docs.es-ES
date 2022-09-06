---
title: Habilitación de la personalización de aplicaciones y bloqueo de aplicaciones hasta que el administrador lo permita
author: heath-hamilton
description: En este módulo, comprenda cómo los administradores de Teams pueden personalizar la aplicación de Teams para su organización y ocultar la aplicación de Teams hasta que el administrador lo apruebe.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 7d71e341bd1613e9efe6c900f29e1bd340006b49
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2022
ms.locfileid: "67604970"
---
# <a name="enable-app-customization-and-block-apps-till-admin-allows"></a>Habilitación de la personalización de aplicaciones y bloqueo de aplicaciones hasta que el administrador lo permita

Microsoft Teams permite a los administradores personalizar la aplicación de Teams para mejorar la experiencia de la tienda y cumplir con la personalización de marca de su organización. Un desarrollador de aplicaciones puede permitir que un administrador de Teams personalice su aplicación. Para obtener más información, consulte [Personalización de aplicaciones en el Centro de administración de Teams](/MicrosoftTeams/customize-apps).

## <a name="enable-customization-for-your-microsoft-teams-app"></a>Habilitación de la personalización para la aplicación de Microsoft Teams

Puede permitir que los clientes personalicen algunos aspectos de la aplicación de Microsoft Teams en el Centro de administración de Teams. Esta función solo se admite para las aplicaciones publicadas en la tienda de Teams. Las aplicaciones transferidas localmente y las aplicaciones publicadas para una organización no se pueden personalizar.

Algunos ejemplos posibles de esta función son:

* Cambiar el color de énfasis de la aplicación para que coincida con la marca de una organización.
* Actualizando el nombre de la aplicación de *Contoso* a *Agente de Contoso*, que es el nombre que verán los usuarios de la organización.
(Nota: Los usuarios que agreguen un conector a un chat o un canal seguirán viendo el nombre de la aplicación original, *Contoso*).

Para habilitar esta característica, defina las propiedades de la aplicación que los clientes pueden personalizar en la [`configurableProperties` sección del manifiesto de aplicación de Teams](/microsoftteams/platform/resources/schema/manifest-schema#configurableproperties), a partir de la versión 1.11. Esto se puede hacer en el [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/home) si ha elegido usar el Portal para desarrolladores para editar el manifiesto de la aplicación.

> [!IMPORTANT]
> No se puede probar esta característica durante el desarrollo. No se admite la personalización de aplicaciones al transferir localmente o publicar en el catálogo de aplicaciones de una organización.

### <a name="user-considerations"></a>Consideraciones del usuario

Proporcione instrucciones para los clientes (en concreto, los administradores de Teams) que quieran personalizar la aplicación. Para obtener más información, vea [personalizar aplicaciones en Teams](/MicrosoftTeams/customize-apps).

## <a name="block-apps-by-default-for-users-until-an-admin-approves"></a>Bloquear aplicaciones de forma predeterminada para los usuarios hasta que un administrador lo apruebe

Para optimizar la experiencia de la aplicación de Teams, puede ocultar una aplicación a los usuarios de forma predeterminada hasta que el administrador permita mostrar la aplicación. Por ejemplo, Contoso Electronics ha creado una aplicación de soporte técnico para Teams. Para habilitar el funcionamiento adecuado de la aplicación, Contoso Electronics’ quiere que los clientes configuren primero propiedades específicas de la aplicación. La aplicación está oculta de forma predeterminada y solo está disponible para los usuarios después de que el administrador lo permita.

Para ocultar la aplicación, en el archivo de manifiesto de la aplicación, establezca la `defaultBlockUntilAdminAction` propiedad en `true`. Cuando la propiedad se establece en `true`, en el Centro de administración de Teams > **Administrar aplicaciones**, **Bloqueado por el editor** aparece en el **estado**  de la aplicación:

:::image type="content" source="../../assets/images/manage-apps-status.png" alt-text="La captura de pantalla es un ejemplo que muestra una aplicación bloqueada por el publicador." lightbox="../../assets/images/manage-apps-status-expanded.png":::

El administrador obtiene una solicitud para tomar medidas antes de que un usuario pueda acceder a la aplicación. En **Administrar aplicaciones**, los administradores pueden seleccionar **Permitir** para permitir que la aplicación con estado **bloqueado por el editor**:

:::image type="content" source="../../assets/images/manage-apps-allow.png" alt-text="La captura de pantalla es un ejemplo que muestra la opción allow para la aplicación bloqueada por el publicador." lightbox="../../assets/images/manage-apps-allow-expanded.png":::

Si, de forma predeterminada, no desea que la aplicación esté oculta, puede actualizar la propiedad `defaultBlockUntilAdminAction` a `false`. Cuando se aprueba la nueva versión de la aplicación, se permitirá de forma predeterminada la aplicación siempre y cuando el administrador no haya realizado ninguna acción explícita.

> [!NOTE]
> En el caso de las aplicaciones LOB, `defaultBlockUntilAdminAction` no se admite. La aplicación no se bloquea si carga una aplicación LOB con esta propiedad.

## <a name="see-also"></a>Consulte también

* [Esquema del manifiesto de la aplicación](/microsoftteams/platform/resources/schema/manifest-schema)
* [Personalizar aplicaciones en el centro de administración de Teams](/MicrosoftTeams/customize-apps)
