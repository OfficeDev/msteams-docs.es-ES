---
title: Creación de un secreto de cliente
description: Describe cómo crear un secreto de cliente
ms.topic: how-to
ms.localizationpriority: medium
keywords: Pestañas de autenticación de teams De Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 79116a0da845cd143de695424a904cf5b5968a15
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888308"
---
# <a name="create-client-secret"></a>Creación de un secreto de cliente

Un secreto de cliente es una cadena que la aplicación usa para demostrar su identidad al solicitar un token.

1. Seleccione **Administrar** > **certificados & secretos**.

2. Seleccione **+ Nuevo secreto de cliente**.

    :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="Página secreto de cliente":::

   Aparece **la página Agregar un secreto de cliente** .

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-secret.png" alt-text="Agregar una página de secreto de cliente" border="true":::

3. Escriba la descripción.
4. Seleccione la duración de validez del secreto.
5. Seleccione **Agregar**.

   Aparece un mensaje en el explorador que indica que el secreto de cliente se actualizó y el secreto de cliente se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-secret-added.png" alt-text="Secreto de cliente agregado":::

6. Seleccione el botón copiar situado junto al **valor** del secreto de cliente.
7. Guarde el valor que copió para su uso posterior.

   > [!NOTE]
   > Asegúrese de copiar el valor del secreto de cliente justo después de crearlo. El valor solo está visible en el momento en que se crea el secreto de cliente y no se puede ver después de eso.
