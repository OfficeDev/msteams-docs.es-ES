---
title: Compartir en Teams desde una aplicación personal o una pestaña
description: Aprenda a agregar el recurso compartido en Teams insertado en la pestaña o aplicación personal.
ms.topic: reference
ms.localizationpriority: medium
keywords: Compartir Teams con Teams
ms.openlocfilehash: c40263504b77a8a848251431de1eb49b85253b77
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757265"
---
# <a name="share-to-teams-from-personal-app-or-tab"></a>Compartir en Teams desde una aplicación personal o una pestaña

> [!NOTE]
> El uso compartido en Teams solo está disponible actualmente en la [versión preliminar para desarrolladores públicos](../../resources/dev-preview/developer-preview-intro.md).

Compartir en Teams permite a los usuarios compartir el contenido desde una aplicación personal o una pestaña con otro usuario o grupo o canal dentro de Teams. Los usuarios pueden seleccionar Compartir para Teams para iniciar la experiencia Compartir en Teams en una ventana emergente. La ventana emergente permite a los usuarios agregar otro usuario o grupo o canal para compartir el contenido.

En la imagen siguiente se muestra la ventana emergente Compartir en Teams:

:::image type="content" source="../../assets/images/share-to-teams/share-to-teams.PNG" alt-text="compartir a equipos emergentes":::

## <a name="enable-share-to-teams-button"></a>Habilitar el botón Compartir para Teams

> [!NOTE]
> Asegúrese de que tiene [Microsoft Teams SDK de cliente de JavaScript](../../tabs/how-to/using-teams-client-sdk.md) o [Microsoft Teams versión preliminar v2 del SDK de cliente de JavaScript](../../tabs/how-to/using-teams-client-sdk.md) (`@microsoft/teams-js@1.11.0-beta.7` o posterior) para habilitar Share para Teams para la aplicación o pestaña personal.

Para habilitar El recurso compartido para Teams:

1. Cree una aplicación personal o una pestaña con **Teams SDK de cliente de Javascript**.

2. Crear un botón **Compartir para Teams**.

3. En el botón Compartir para Teams, llame a `microsoftTeams.sharing.shareWebContent` con una carga de contenido.

En el ejemplo siguiente se explica cómo crear una carga de contenido:

```json
microsoftTeams.sharing.shareWebContent({
        content: [
          {
            type: 'URL',
            url: '<URL to be shared>',
            message: 'Default message to be loaded in the compose box',
            preview: true
          }
        ]
      });
```

La carga contiene los parámetros siguientes:

| Nombre de propiedad | Objetivo |
|---|---|
| `type` | El tipo debe ser `URL` |
| `url` | `URL` que se va a compartir |
|`message`| Mensaje predeterminado que se va a cargar en el cuadro de redacción |
| `preview` | Establézcalo `true` en para habilitar la versión preliminar de la dirección URL. |

En la imagen siguiente se muestra la opción Compartir en Teams:

:::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="botón compartir a equipos":::

## <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **100** | LA API no se admite en la plataforma actual. |
| **404** | El archivo especificado no se encontró en la ubicación especificada. |
| **500** | Error interno al realizar la operación necesaria. |
| **501** | La API no se admite en el contexto actual. |
| **1 000** | Permisos denegados por el usuario. |
| **2000** | Problema de red. |
| **3000** | El hardware subyacente no admite la funcionalidad. |
| **4000** | Uno o más argumentos no son válidos. |
| **5000** | El usuario no está autorizado para esta operación. |
| **6000** | No se pudo completar la operación debido a recursos insuficientes. |
| **7000** | La plataforma limitó la solicitud debido a que la API se invocó con demasiada frecuencia. |
| **8000** | El usuario anuló la operación. |
| **9000** | El código de la plataforma es antiguo y no implementa esta API. |
| **10000** | El valor devuelto es demasiado grande y ha superado los límites de tamaño. |

## <a name="limitations"></a>Limitaciones

Las limitaciones para agregar Share a Teams botón:

* El botón Compartir en Teams se puede hospedar o incrustar en una aplicación que se ejecuta dentro de Teams.
* Puede agregar el botón Compartir a Teams a la aplicación creada mediante **Teams SDK de cliente de Javascript**.

## <a name="end-user-share-to-teams-experience"></a>Uso compartido del usuario final para Teams experiencia

Después de habilitar el botón Compartir en teams en la pestaña o aplicación personal, puede compartir el contenido. Para obtener acceso, siga estos pasos:

1. Abra una aplicación o pestaña personal y seleccione **Compartir para Teams**.

    :::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="botón compartir a equipos":::

2. Agregue otro usuario, grupo o canal para compartir el contenido.

    :::image type="content" source="../../assets/images/share-to-teams/add-recepient.PNG" alt-text="add-recipient":::

    > [!NOTE]
    > Puede agregar una nota en **decir algo al respecto**.

3. Seleccione **Compartir**.

   :::image type="content" source="../../assets/images/share-to-teams/add-notes.PNG" alt-text="add-note":::

4. Seleccione **Ver** para llegar a la conversación donde se ha compartido el vínculo.

   :::image type="content" source="../../assets/images/share-to-teams/link-shared.PNG" alt-text="share-to-teams-link-shared":::

## <a name="see-also"></a>Vea también

* [Compartir en Teams desde aplicaciones web](share-to-teams-from-web-apps.md)
* [Crear una pestaña personal](../../tabs/how-to/create-personal-tab.md)
