---
title: Configurar opciones de instalación predeterminadas para la aplicación
description: Describe cómo especificar las opciones de instalación predeterminadas de la aplicación y la funcionalidad predeterminada para ámbitos compartidos.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: a6857e549c688bd7078aeaceae4b9f5a885ae2c3
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453211"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a>Configurar las opciones de instalación predeterminadas para Microsoft Teams aplicación

Es común que una aplicación admita varios escenarios en Teams, pero es posible que la haya diseñado con un ámbito y capacidad específicos en mente. Por ejemplo, si la aplicación es principalmente para uso de equipo o canal, puedes asegurarte de que la primera opción de instalación que los usuarios ven en la tienda es **Agregar a un equipo**.

:::row:::
   :::column span="2":::

![Agregar un ejemplo desplegable de aplicaciones](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

Si la funcionalidad principal de la aplicación es un bot, también puedes convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo.

## <a name="configure-your-apps-default-install-scope"></a>Configurar el ámbito de instalación predeterminado de la aplicación

Configure el ámbito de instalación predeterminado para la aplicación. Solo puede establecer un ámbito a la vez.

Para configurar el ámbito de instalación predeterminado en el manifiesto de la aplicación:

1. Abre el manifiesto de la aplicación y agrega la `defaultInstallScope` propiedad.
2. Establezca el valor de ámbito de instalación predeterminado como , `personal``team`, `groupchat`, o `meetings`.

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> Para obtener más información, consulta el esquema [de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).

## <a name="configure-the-default-capability-for-shared-scopes"></a>Configurar la funcionalidad predeterminada para ámbitos compartidos

Configura la funcionalidad predeterminada cuando la aplicación esté instalada para un equipo, una reunión o un chat de grupo.

> [!NOTE]
> `defaultGroupCapability` proporciona la funcionalidad predeterminada que se agregará al equipo, al chat de grupo o a la reunión. Selecciona una pestaña, bot o conector como la funcionalidad predeterminada de la aplicación, pero debes asegurarte de que has proporcionado la funcionalidad seleccionada en la definición de la aplicación.

Para configurar detalles en el manifiesto de la aplicación:

1. Abre el manifiesto de la aplicación y agrega la `defaultGroupCapability` propiedad a él.
2. Establezca un valor de `team`, `groupchat`o `meetings`.
3. Para la funcionalidad de grupo seleccionada, las capacidades de grupo disponibles son, `bot`, `tab`o `connector`.

    > [!NOTE]
    > Solo puede seleccionar una funcionalidad predeterminada, `bot`, o `tab`para `connector` la funcionalidad de grupo seleccionada.

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> Para obtener más información, consulta el esquema [de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear el paquete de aplicación](~/concepts/build-and-test/apps-package.md)
