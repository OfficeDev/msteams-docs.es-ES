---
title: Configurar opciones de instalación predeterminadas para la aplicación
description: Describe cómo especificar las opciones de instalación predeterminadas de la aplicación.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a4b70df70c7b9442e29953dae8a8c4e892cb72c1
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946493"
---
# <a name="add-a-default-install-scope-and-group-capability"></a>Agregar un ámbito de instalación predeterminado y una funcionalidad de grupo

Es común que una aplicación admita varios escenarios en Teams, pero es posible que la haya diseñado con un ámbito y una funcionalidad específicos en mente. Por ejemplo, si la aplicación es principalmente para uso de equipo o canal, puedes asegurarte de que la primera opción de instalación que los usuarios ven en la tienda es **Agregar a un equipo**.

![Agregar una aplicación](../../assets/images/compose-extensions/addanapp.png)

Si la funcionalidad principal de la aplicación es un bot, también puedes convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo. 

## <a name="configure-your-apps-default-install-scope"></a>Configurar el ámbito de instalación predeterminado de la aplicación

Configure el ámbito de instalación predeterminado para la aplicación. Solo puede establecer un ámbito a la vez.

**Para configurar el ámbito de instalación predeterminado en el manifiesto de la aplicación**

1. Abre el manifiesto de la aplicación y agrega la `defaultInstallScope` propiedad.
2. Establezca un valor de `personal` , `team` , o `groupchat` `meetings` (vea un ejemplo a continuación).

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> Para obtener más información, consulta el esquema [de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).

## <a name="configure-the-default-capability-for-shared-scopes"></a>Configurar la funcionalidad predeterminada para ámbitos compartidos

Configura la funcionalidad predeterminada cuando la aplicación esté instalada para un equipo, una reunión o un chat.

**Para configurar detalles en el manifiesto de la aplicación**

1. Abre el manifiesto de la aplicación y agrega la `defaultGroupCapability` propiedad a él.
2. Guarde las actualizaciones.

    A continuación se muestra un ejemplo json:

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> Para obtener información sobre el esquema completo, vea [esquema de manifiesto](~/resources/schema/manifest-schema.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Elegir cómo distribuir la aplicación](overview.md)
