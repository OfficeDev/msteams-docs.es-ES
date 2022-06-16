---
title: Configuración de opciones de instalación predeterminadas para la aplicación
description: Obtenga información sobre cómo especificar las opciones de instalación predeterminadas de la aplicación de Teams y la funcionalidad predeterminada para los ámbitos compartidos.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 9055b765c30f83c4031ad0e2ba5f18f4e747ac3f
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2022
ms.locfileid: "66122904"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a>Configuración de opciones de instalación predeterminadas para la aplicación de Microsoft Teams

Es habitual que una aplicación admita varios escenarios en Teams, pero es posible que la haya diseñado teniendo en cuenta un ámbito y una funcionalidad específicos. Por ejemplo, si la aplicación es principalmente para uso en equipo o canal, puedes asegurarte de que la primera opción de instalación que ven los usuarios en la tienda es **Agregar a un equipo**.

:::row:::
   :::column span="2":::

![Ejemplo de lista desplegable Agregar una aplicación](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

Si la funcionalidad principal de la aplicación es un bot, también puede convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo.

## <a name="configure-your-apps-default-install-scope"></a>Configuración del ámbito de instalación predeterminado de la aplicación

Configure el ámbito de instalación predeterminado para la aplicación. Solo puede establecer un ámbito a la vez.

Para configurar el ámbito de instalación predeterminado en el manifiesto de la aplicación:

1. Abra el manifiesto de la aplicación y agregue la `defaultInstallScope` propiedad .
2. Establezca el valor predeterminado del ámbito de `personal`instalación como , , `team``groupchat`o `meetings`.

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> Para obtener más información, consulte el [esquema del manifiesto de la aplicación](~/resources/schema/manifest-schema.md).

## <a name="configure-the-default-capability-for-shared-scopes"></a>Configuración de la funcionalidad predeterminada para ámbitos compartidos

Configure la funcionalidad predeterminada cuando la aplicación esté instalada para un equipo, reunión o chat de grupo.

> [!NOTE]
> `defaultGroupCapability` proporciona la funcionalidad predeterminada que se agregará al equipo, a groupchat o a la reunión. Seleccione una pestaña, un bot o un conector como la funcionalidad predeterminada para la aplicación, pero debe asegurarse de que ha proporcionado la funcionalidad seleccionada en la definición de la aplicación.

Para configurar los detalles en el manifiesto de la aplicación:

1. Abra el manifiesto de la aplicación y agréguele la `defaultGroupCapability` propiedad.
2. Establezca un valor de `team`, `groupchat`o `meetings`.
3. Para la funcionalidad de grupo seleccionada, las funcionalidades de grupo disponibles son, `bot`, `tab`o `connector`.

    > [!NOTE]
    > Solo puede seleccionar una funcionalidad predeterminada, `bot`, `tab`o `connector` para la funcionalidad de grupo seleccionada.

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> Para obtener más información, consulte el [esquema del manifiesto de la aplicación](~/resources/schema/manifest-schema.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear el paquete de aplicación](~/concepts/build-and-test/apps-package.md)
