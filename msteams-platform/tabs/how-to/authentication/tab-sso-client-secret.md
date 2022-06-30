---
title: Creación de un secreto de cliente
description: Describe cómo crear un secreto de cliente
ms.topic: how-to
ms.localizationpriority: medium
keywords: pestañas de autenticación de teams Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 77d1c4e43c9bdfb9d2cb9e3e97ee3a26b8b0fa01
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558852"
---
# <a name="create-client-secret"></a>Creación de un secreto de cliente

Un secreto de cliente es una cadena que la aplicación usa para demostrar su identidad al solicitar un token.

1. Seleccione **Administrar** > **certificados & secretos**.

2. Seleccione **+ Nuevo secreto de cliente**.

    :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="Página secreto de cliente":::

   Aparece **la página Agregar un secreto de cliente** .

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-secret.png" alt-text="Agregar una página de secreto de cliente":::

3. Escriba la descripción.
4. Seleccione la duración de validez del secreto.
5. Seleccione **Agregar**.

   Aparece un mensaje en el explorador que indica que el secreto de cliente se actualizó y el secreto de cliente se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-secret-added.png" alt-text="Secreto de cliente agregado":::

6. Seleccione el botón copiar situado junto al **valor** del secreto de cliente.
7. Guarde el valor que copió para su uso posterior.

   > [!NOTE]
   > Asegúrese de copiar el valor del secreto de cliente justo después de crearlo. El valor solo está visible en el momento en que se crea el secreto de cliente y no se puede ver después de eso.
