---
title: Teams Connect canales compartidos
author: Rajeshwari-v
description: Obtenga información sobre Teams Connect canales compartidos para colaborar de forma segura con usuarios internos y externos en un espacio compartido sin cambiar de inquilino.
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: d8c6e46a67c8cfeb1e8fa9bf0196a74fb6e183c6
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819957"
---
# <a name="microsoft-teams-connect-shared-channels"></a>Microsoft Teams Connect canales compartidos

Microsoft Teams Connect canales compartidos permiten a los miembros de un canal colaborar con usuarios de otros equipos y organizaciones. Puede crear y compartir un canal compartido con:

* Miembros de otro equipo de la misma organización.
* Personas de la misma organización.
* Personas y otros equipos de otras organizaciones.

Teams Connect canales compartidos facilitan la colaboración segura sin problemas. Permitir que usuarios externos fuera de su organización colaboren con usuarios internos en Teams sin cambiar su contexto de usuario. Mejore la experiencia del usuario a diferencia del uso de cuentas de invitado; por ejemplo, los miembros deben cerrar la sesión de Teams e iniciar sesión de nuevo con una cuenta de invitado. Las aplicaciones de Teams amplían el eficaz espacio de colaboración.

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="Diagrama que muestra el equipo B de la organización A y el equipo C de la organización B colaborando en un canal compartido como equipo A." border="true" :::

## <a name="enable-your-app-for-shared-channels"></a>Habilitación de la aplicación para canales compartidos

SupportedChannelTypes es una propiedad opcional que habilita la aplicación en canales no estándar. Si la aplicación admite el ámbito de equipo y la propiedad está definida, Teams habilita la aplicación en cada tipo de canal en consecuencia. Actualmente se admiten canales privados y compartidos. Para obtener más información, vea [supportedChannelTypes](../../resources/schema/manifest-schema.md#supportedchanneltypes).

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

## <a name="get-context-for-shared-channels"></a>Obtener contexto para canales compartidos

Cuando la experiencia de usuario de contenido se cargue en un canal compartido, use los datos recibidos de `getContext` la llamada para los cambios de canal compartido. `getContext` call publica dos propiedades nuevas, `hostTeamGroupID` y `hostTenantID`, que se usan para recuperar la pertenencia al canal mediante las API de Microsoft Graph. `hostTeam` es el equipo que crea el canal compartido.

Para obtener más información para habilitar la pestaña, consulte:

* [Obtener contexto para la pestaña para canales privados](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [Obtener contexto en canales compartidos](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

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

## <a name="see-also"></a>Vea también

* [Pestañas de compilación para Teams](../../tabs/what-are-tabs.md)
* [Esquema del manifiesto de la aplicación de Teams](../../resources/schema/manifest-schema.md)
* [Canales compartidos en Microsoft Teams](/MicrosoftTeams/shared-channels)
* [Tipo de recurso de canal](/graph/api/resources/channel)
* [Directiva de retención para ubicaciones de Teams](/microsoft-365/compliance/create-retention-policies)
