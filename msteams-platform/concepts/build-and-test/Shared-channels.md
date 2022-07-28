---
title: Canales compartidos
author: Rajeshwari-v
description: Colaborar con canales compartidos.
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 96cd3014fa1cee38832724e1b50cf29db372d711
ms.sourcegitcommit: d40ea0d504db66d49bbe0955f7031db1cd210056
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2022
ms.locfileid: "67060044"
---
# <a name="shared-channels"></a>Canales compartidos

Los canales compartidos de Microsoft Teams permiten a los miembros de un canal colaborar con usuarios de otros equipos y organizaciones. Puede crear y compartir un canal compartido con:

* Miembros de otro equipo de la misma organización.
* Personas de la misma organización.
* Personas y otros equipos de otras organizaciones.

Los canales compartidos facilitan la colaboración sin problemas. Permitir que usuarios externos fuera de su organización colaboren con usuarios internos en Teams sin cambiar su contexto de usuario. Mejore la experiencia del usuario a diferencia del uso de cuentas de invitado; por ejemplo, los miembros deben cerrar la sesión de Teams e iniciar sesión de nuevo con una cuenta de invitado. Las aplicaciones de Teams ahora pueden ampliar el eficaz espacio de colaboración.

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="Imagen de canal compartido"border="true" :::

## <a name="manifest-update-in-shared-channels"></a>Actualización del manifiesto en canales compartidos

Cuando la experiencia de usuario de contenido se cargue en un canal compartido, use los datos recibidos de `getContext` la llamada para los cambios de canal compartido. `getContext` call publica dos propiedades nuevas, `hostTeamGroupID` y `hostTenantID`, que se usan para recuperar la pertenencia al canal mediante las API de Microsoft Graph. `hostTeam` es el equipo que crea el canal compartido.

SupportedChannelTypes es una propiedad opcional que habilita la aplicación en canales no estándar. Si la aplicación admite el ámbito del equipo y la propiedad está definida, Teams habilitará la aplicación en cada tipo de canal en consecuencia. Actualmente se admiten canales privados y compartidos. Para obtener más información, vea [supportedChannelTypes](../../resources/schema/manifest-schema.md#supportedchanneltypes)

```JSON
"supportedChannelTypes": {
      "type": "array",
      "description": "List of ‘non-standard’ channel types that the app supports. Note: Channels of standard type are supported by default if the app supports team scope. ",
      "maxItems": 2,
      "items": { 
        "enum": [
          "sharedChannels",
          "privateChannels"
        ]
      }
    }
```

> [!NOTE]
>
> * Si la aplicación admite el ámbito de equipo, funciona en canales estándar, independientemente de los valores que se definan en esta propiedad.
> * Es posible que la aplicación tenga que tener en cuenta las propiedades únicas de cada uno de estos tipos de canal para poder funcionar correctamente.

Para obtener más información sobre cómo habilitar la pestaña, consulte:

* [Obtener contexto para la pestaña para canales privados](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [Obtener contexto de la pestaña para canales compartidos](../../tabs/how-to/access-teams-context.md#retrieve-context-in-microsoft-teams-connect-shared-channels)

## <a name="apps-and-permissions-in-shared-channels"></a>Aplicaciones y permisos en canales compartidos

Puede colaborar con miembros externos fuera de la organización mediante canales compartidos. Los permisos de aplicación en canales compartidos siguen la lista de aplicaciones del equipo host y la directiva de aplicación del inquilino del host.

> [!NOTE]
> La [API de notificación de fuente de actividad](/graph/teams-send-activityfeednotifications) no admite notificaciones entre inquilinos para las aplicaciones de un canal compartido.

## <a name="get-shared-channel-membership"></a>Obtención de la pertenencia a canales compartidos

Puede obtener la pertenencia directa a canales compartidos mediante los `hostTeamGroupID` `getContext` siguientes pasos:

1. Obtener miembros directos con [la API DE API de miembros del canal GET](/graph/api/channel-list-members?view=graph-rest-beta&tabs=http&preserve-view=true) .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. Obtenga cada equipo compartido con GET `sharedWithTeams` API.

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams
    ```

3. Use los miembros GET de cada equipo compartido (Team X) con GET `sharedWithTeams` API.

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams/{teamX}/members
    ```

## <a name="classify-members-in-the-shared-channel-as-in-tenant-or-out-tenant"></a>Clasificación de miembros en el canal compartido como inquilinos o fuera del espacio empresarial

Puede clasificar los miembros como inquilinos o fuera del inquilino comparando `tenantID` el miembro o equipo con `hostTeamTenantID` como se indica a continuación:

1. Obtenga el miembro que desea comparar.

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. Use `getContext`, compare el `tenantID` elemento del miembro con la `hostTenantID` propiedad .

## <a name="azure-ad-native-identity"></a>Identidad nativa de Azure AD

Las aplicaciones deben funcionar entre inquilinos en la instalación y el uso. En la tabla siguiente se enumeran los tipos de canal y sus identificadores de grupo correspondientes:

|Tipo de canal| groupId | hostTeamGroupId |
|----------|---------|-----------------|
|Regular | Identificador de grupo de Team Azure AD | Identificador de grupo de Team Azure AD |
|Compartido | En blanco | Identificador de grupo de Azure AD del equipo host |

## <a name="see-also"></a>Consulte también

* [Pestañas de compilación para Teams](../../tabs/what-are-tabs.md)
* [Esquema del manifiesto de la aplicación de Teams](../../resources/schema/manifest-schema.md)
