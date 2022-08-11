---
title: Creación de una nueva aplicación de Teams en Visual Studio
author: surbhigupta
description: En este módulo, aprenderá a crear una nueva aplicación de Teams mediante el kit de herramientas de Teams para Visual Studio.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: 12f0b74726aed8cdca50d9f5c078acd0f22cbeaa
ms.sourcegitcommit: 52a11f7614c43172bc2d57401a60d569db5310a9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2022
ms.locfileid: "67291663"
---
# <a name="create-new-teams-app-in-visual-studio"></a>Creación de una nueva aplicación de Teams en Visual Studio

Teams Toolkit proporciona plantillas de aplicación de Microsoft Teams en Visual Studio para crear una aplicación de Teams.  Puede buscar y seleccionar la plantilla de aplicación de Teams que necesite al crear un nuevo proyecto. Puede tener plantillas de aplicación de Teams para crear.

* Aplicación tab
* Bot de comandos
* Bot de notificación
* Extensión de mensaje

## <a name="prerequisites"></a>Requisitos previos

| &nbsp; | Instalar | Para usar... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Versión 17.3 de Visual Studio | Puede instalar la edición enterprise de Visual Studio e instalar la carga de trabajo "ASP.NET" y las herramientas de desarrollo de Microsoft Teams. |
| &nbsp; | Kit de herramientas de Teams | Extensión de Visual Studio que crea un scaffolding de proyecto para la aplicación. Use la versión más reciente. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams para colaborar con todos los usuarios con los que trabaja a través de aplicaciones de chat, reuniones, llamadas, todo en un solo lugar. |
 | &nbsp; | [Preparar el espacio empresarial de Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Acceso a la cuenta de Teams con los permisos adecuados para instalar una aplicación. |

1. Seleccione **Crear un nuevo proyecto** en la sección **Introducción** al iniciar Visual Studio.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1.png" alt-text="Creación de un nuevo proyecto a partir de la introducción":::

   También puede crear un nuevo proyecto directamente desde la aplicación.

1. Seleccione **el menú Archivo** .
1. Seleccione  **Nuevo**.
1. Seleccione **Proyecto**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2.png" alt-text="Menú Crear nuevo proyecto desde el archivo":::

1. Busque la aplicación de Microsoft **Teams** en la lista.
1. Seleccione **Aplicación de Microsoft Teams**.
1. Seleccione **Siguiente**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app.png" alt-text="Buscar y elegir una aplicación de Microsoft Teams":::

1. Seleccione **Nombre del** proyecto y escriba el nombre del proyecto.
1. Seleccione **Crear**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name.png" alt-text="Asignar un nombre a la aplicación":::

1. Seleccione el **tipo de aplicación de Teams** que desea crear.
1. Seleccione **Crear**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type.png" alt-text="Seleccionar el tipo de aplicación de Teams":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Plantillas de aplicación de Teams en Teams Toolkit for Visual Studio

Puede ver las plantillas de aplicación de Teams ya rellenadas en Teams Toolkit para varios tipos de aplicación de Teams. En la tabla siguiente se enumeran todas las plantillas disponibles:

|Plantilla de aplicación de Teams  |Descripción  |
|---------|---------|
|Bot de notificación     |La aplicación Bot de notificación puede enviar una notificación al cliente de Teams; hay varias maneras de desencadenar la notificación. Por ejemplo, desencadene la notificación por solicitud HTTP o por tiempo. También puede seleccionar la notificación desencadenada en función del escenario empresarial.         |
|Bot de comandos     |Los usuarios pueden escribir un comando para interactuar con el bot mediante la aplicación Bot de comandos.         |
|Tab     |La aplicación Tab muestra una página web dentro de Teams y habilita el inicio de sesión único con la cuenta de Teams.         |
|Extensión de mensaje     |La aplicación extensión de mensaje implementa características sencillas, como crear tarjeta adaptable, buscar paquetes Nugget, desenlazar vínculos para el dominio "dev.botframework.com".         |

> [!NOTE]
>Una vez creado el proyecto, El kit de herramientas de Teams abre automáticamente Introducción. Ahora puede ver las instrucciones de Introducción y consultar las distintas características del kit de herramientas de Teams.

## <a name="see-also"></a>Vea también

* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)
