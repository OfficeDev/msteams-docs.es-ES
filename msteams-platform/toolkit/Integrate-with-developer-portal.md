---
title: Integración con el Portal para desarrolladores en el kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, aprenderá a integrarse con el Portal para desarrolladores en el kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: b54e833f5c8292c0b426e859e63d858102860a47
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617335"
---
# <a name="integrate-with-developer-portal"></a>Integración con el Portal para desarrolladores

Puede configurar y administrar la aplicación en el portal para desarrolladores dentro del kit de herramientas de Teams.

## <a name="to-publish-app-using-developer-portal"></a>Para publicar la aplicación mediante el Portal para desarrolladores

Los pasos siguientes le ayudarán a publicar la aplicación en el Portal para desarrolladores:

1. Seleccione **Portal para desarrolladores para Teams** en **IMPLEMENTACIÓN**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/dev-portal-ttk.png" alt-text="Portal para desarrolladores de Teams":::

   Ahora se abre el Portal para desarrolladores en un explorador.

1. Inicie sesión en el [portal para desarrolladores de Teams](https://dev.teams.microsoft.com) con la cuenta correspondiente.
1. Importe el paquete de la aplicación en zip y seleccione **Aplicación de** > **importación de aplicaciones**.
1. Seleccione **Publicar** > **publicación en su organización**.

## <a name="to-update-manifest-file-and-app-package"></a>Para actualizar el archivo de manifiesto y el paquete de aplicación

Si hay cambios relacionados con el archivo de manifiesto de la aplicación de Teams, puede actualizar el manifiesto y volver a publicar la aplicación de Teams. Para publicar la aplicación de Teams manualmente, puede aprovechar el [portal para desarrolladores para Teams](https://dev.teams.microsoft.com/home).

1. Inicie sesión en el [portal para desarrolladores de Teams](https://dev.teams.microsoft.com) con la cuenta correspondiente.
1. Importe el paquete de la aplicación en zip y seleccione **Aplicación de** > **importación de aplicaciones**.<br>
   Debe reemplazar la aplicación que cargó anteriormente en el Portal para desarrolladores.
1. Para publicar la aplicación, seleccione **Publicar** > **publicación en su organización**.

Puede realizar la siguiente configuración en el Portal para desarrolladores:

* **Información básica**: esta sección muestra y permite editar el nombre de la aplicación, el identificador de la aplicación, las descripciones, la versión, la información del desarrollador, las direcciones URL de la aplicación, el identificador de la aplicación (cliente) y el identificador de Microsoft Partner Network.
* **Personalización de marca**: esta página muestra los detalles del icono de la aplicación.
* **Características de** la aplicación: puede agregar las siguientes características a la aplicación:
  * Aplicación personal
  * Bot
  * Connector
  * Escena
  * Aplicación de grupo y canal
  * Extensión de mensajería
  * Extensión de reunión
  * Notificación de fuente de actividad
* **Permisos**: esta sección le permite conceder permisos de dispositivo, permisos de equipo, permisos de chat o reunión y permisos de usuario para la aplicación.
* **Inicio de sesión único**: puede configurar la aplicación para autenticar a los usuarios con el inicio de sesión único (SSO).
* **Idiomas**: puede configurar o cambiar el idioma de la aplicación.
* **Dominio**: puede agregar los dominios para cargar las aplicaciones en el cliente de Teams (por ejemplo: *.example.com).

## <a name="see-also"></a>Vea también

* [Portal para desarrolladores de Teams](../concepts/build-and-test/teams-developer-portal.md)
* [Administre sus aplicaciones en el Portal para desarrolladores](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)
