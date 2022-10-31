---
title: Portal para desarrolladores de Teams
description: En este artículo, obtenga más información sobre el Portal para desarrolladores y cómo crear una aplicación completamente nueva e importar una aplicación existente en el Portal para desarrolladores de Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 3c6444f041a996b908e2c6444fecf7e3dc68ee40
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791807"
---
# <a name="developer-portal-for-teams"></a>Portal para desarrolladores de Teams

El <a href="https://dev.teams.microsoft.com" target="_blank">portal para desarrolladores para Teams</a> es la herramienta principal para configurar, distribuir y administrar las aplicaciones de Microsoft Teams. Con el portal para desarrolladores, puede colaborar con compañeros en la aplicación, configurar entornos en tiempo de ejecución y mucho más.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="La captura de pantalla es un ejemplo que muestra la página principal del Portal para desarrolladores para Teams.":::

> [!NOTE]
>
> * Actualmente, el Portal para desarrolladores no está disponible para inquilinos de Government Community Cloud (GCC)-High o del Departamento de Defensa (DOD).
> * Sin embargo, puede usar un inquilino normal para compilar una aplicación en el portal para desarrolladores, descargar la aplicación y cargar la aplicación mediante [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) en una nube nacional. Para obtener más información, consulte [Implementaciones nacionales de nube](/graph/deployments).

## <a name="register-an-app"></a>Registrar una aplicación

El Portal para desarrolladores proporciona las siguientes maneras de registrar una aplicación de Teams:

* [Cree y registre una aplicación nueva](#create-and-register-a-brand-new-app).
* [Importe un paquete de aplicación existente](#import-an-existing-app).

### <a name="create-and-register-a-brand-new-app"></a>Creación y registro de una aplicación nueva

El portal para desarrolladores le permite crear una aplicación completamente nueva:

1. Inicie sesión en [el Portal para desarrolladores](https://dev.teams.microsoft.com) y seleccione **Aplicaciones** en el panel izquierdo.

   :::image type="content" source="../../assets/images/tdp/home-page.png" alt-text="La captura de pantalla es un ejemplo que muestra la página principal del Portal para desarrolladores para Teams.":::

1. Seleccione **Nueva aplicación** y escriba el nombre de la aplicación.

   :::image type="content" source="../../assets/images/tdp/enter-app-name-tdp.png" alt-text="En la captura de pantalla se muestra cómo crear una aplicación nueva en el Portal para desarrolladores para Teams." lightbox="../../assets/images/tdp/create-new-app-in-tdp.png":::

1. Seleccione **Agregar**.

Ahora ha creado correctamente una nueva aplicación y puede ver toda la información básica de la nueva aplicación.

:::image type="content" source="../../assets/images/tdp/basic-information-app-tdp.png" alt-text="La captura de pantalla es un ejemplo que muestra la información básica de la aplicación que creó en el Portal para desarrolladores para Teams.":::

### <a name="import-an-existing-app"></a>Importación de una aplicación existente

Siga los pasos para importar y administrar la aplicación existente en el Portal para desarrolladores.

1. En el Portal para desarrolladores, seleccione **Aplicaciones** en el panel izquierdo.
1. Seleccione **Importar aplicación**.

   :::image type="content" source="../../assets/images/tdp/import-app.png" alt-text="En la captura de pantalla se muestra cómo importar la aplicación existente en el Portal para desarrolladores de Teams para administrar las aplicaciones.":::

1. Seleccione el archivo de manifiesto de la aplicación y, a continuación, seleccione **Abrir**.
1. Seleccione **Importar**.

> [!NOTE]
>
> * El Portal para desarrolladores crea un identificador de aplicación único y bloquea el identificador de la aplicación de Teams registrada. No puede editar ni proporcionar un identificador de su elección, lo que impide tener identificadores de aplicación duplicados para varias aplicaciones.
> * Si crea una aplicación con el Kit de herramientas de Microsoft Teams para Visual Studio Code, puede administrarla en el Portal para desarrolladores. Para obtener más información, consulte [Compilación de aplicaciones con el kit de herramientas de Teams y Visual Studio Code](~/toolkit/visual-studio-code-overview.md).
> * Puede importar una aplicación existente que creó en App Studio al Portal para desarrolladores.

## <a name="see-also"></a>Vea también

[Incluir una oferta de SaaS con la aplicación de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
