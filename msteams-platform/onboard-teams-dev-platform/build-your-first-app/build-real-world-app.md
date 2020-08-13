---
title: Compilar la primera aplicación de Microsoft Teams
author: heath-hamilton
description: Tutorial para crear una aplicación de Microsoft Teams en el mundo real
ms.openlocfilehash: 4915dde4ef5a852f4fc5d1e4c83e3349db2eaf6b
ms.sourcegitcommit: 80bf79a952bb14cbc38c0bd1e3cf8a346158e28e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "46655677"
---
# <a name="learn-how-to-build-your-first-teams-app"></a>Obtenga información sobre cómo crear su primera aplicación de Teams

En **compilar la primera aplicación**, aprenderá a crear una aplicación básica de Teams a través de tutoriales. Las lecciones se compilan unas a otras, que le guiarán por cada paso de la creación de una aplicación sencilla y real de Teams. Le presentamos las herramientas comunes, conceptos fundamentales y vínculos útiles a lo largo del proceso.

Empezar? creando y ejecutando una "Hello, World!" aplicación de pestañas. A continuación, creará una interfaz de usuario sencilla y aprenderá a obtener un contexto útil con el SDK de JavaScript de Microsoft Teams.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
  >
  > - **Póngase en marcha rápidamente con Team Toolkit**: el kit de herramientas de Microsoft Teams para Visual Studio Code se encarga de crear el proyecto de la aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.
  > - **Definir la aplicación con el manifiesto**: el manifiesto es un plano en el que se especifican las capacidades y los servicios que usa la aplicación de Microsoft Teams.
  > - **Alcance su público**: puede crear una aplicación de Microsoft Teams para uso o colaboración personal. En los tutoriales, aprenderá a crear una pestaña para usuarios individuales o a un grupo de personas en un canal o chat.
  > - **Usar Teams SDK para obtener contexto**: Aprenda a usar el SDK de JavaScript de Microsoft Teams para realizar cambios de tema o configurar la experiencia de configuración.  
  > - **Amplíe en su aplicación**: a lo largo de los tutoriales, nos vinculamos a temas relacionados que probablemente le interesen (algunos de los cuales incluyen directrices de autenticación y de diseño).

## <a name="teams-app-fundamentals"></a>Conceptos básicos de las aplicaciones de Microsoft Teams

Antes de empezar con los tutoriales, debe conocer lo siguiente acerca de la creación de aplicaciones para Microsoft Teams.

### <a name="apps-can-have-multiple-capabilities"></a>Las aplicaciones pueden tener varias funcionalidades

Las aplicaciones de Microsoft Teams se componen de una o varias [capacidades de plataforma](../capabilities-overview.md), como [fichas](../doc-links/what-are-tabs.md), [bots](../doc-links/what-are-bots.md ), [extensiones de mensajería](../doc-links/what-are-messaging-extensions.md)y [webhooks y conectores](../doc-links/what-are-webhooks-and-connectors.md). Las aplicaciones de Microsoft Teams también tienen muchas [convenciones y elementos](../doc-links/teams-ui-conventions.md)de la interfaz de usuario, como tarjetas, módulos de tareas y vínculos profundos, que puede usar para crear la mejor experiencia de usuario posible.

Para estos tutoriales, compilaremos solo las pestañas, pero puede Agregar un bot u otra función a la aplicación como desee.

### <a name="teams-doesnt-host-your-app"></a>Microsoft Teams no hospeda la aplicación  

Una aplicación de Microsoft Teams consta de tres partes principales:

1. El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios interactúan con la aplicación.
1. La aplicación, el servicio, el flujo de trabajo o el sitio web que realiza la lógica, el almacenamiento de datos y las llamadas API necesarias para potenciar la aplicación.
1. El paquete de la aplicación, que se usa para instalar la aplicación en Microsoft Teams. Contiene los metadatos de la aplicación (nombre, iconos, etc.) y punteros a los servicios.

## <a name="next-step"></a>Paso siguiente

Para ahora, vamos a empezar.

> [!div class="nextstepaction"]
> [Compilar y ejecutar la primera aplicación](build-and-run-with-toolkit.md)
