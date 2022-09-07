---
title: Preparación para compilar aplicaciones con el kit de herramientas de Teams
author: surbhigupta
description: En este artículo, aprenderá a crear el entorno del kit de herramientas de Teams y administrar la aplicación en el Portal para desarrolladores.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 4c6862322b007433f3bdfcdc5da93ec5069c6a36
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617322"
---
# <a name="prepare-to-build-apps-using-microsoft-teams-toolkit"></a>Preparación para compilar aplicaciones mediante el kit de herramientas de Microsoft Teams

Teams Toolkit admite entornos para crear aplicaciones. Teams Toolkit también ayuda a integrar las funcionalidades de Azure Functions, así como los servicios en la nube en la aplicación de Teams que ha creado.

:::image type="content" source="../assets/images/buildapps-TTK.png" alt-text="Preparación para compilar aplicaciones mediante el kit de herramientas de Teams":::

## <a name="build-environments"></a>Entornos de compilación

El kit de herramientas de Teams en Microsoft Visual Studio Code ofrece un conjunto de entornos para compilar la aplicación de Teams. Puedes elegir cualquiera del siguiente entorno que mejor se adapte a tu aplicación:

* JavaScript o TypeScript
* SharePoint Framework (SPFx)

### <a name="create-your-teams-app-using-javascript-or-typescript"></a>Creación de una aplicación de Teams mediante JavaScript o TypeScript

Las aplicaciones compiladas con JavaScript tienen las siguientes ventajas:

* La aplicación incluye sus propias funcionalidades de interfaz de usuario y experiencia de usuario que son enriquecidas y fáciles de usar.
* Proporciona actualizaciones rápidas a las aplicaciones existentes.
* Distribuye aplicaciones en varias plataformas, como Android e iOS.
* Compatible para crear una aplicación con API existentes.

Teams Toolkit en Visual Studio Code admite la creación de las siguientes aplicaciones mediante JavaScript o TypeScript:

* Aplicación de pestaña: la aplicación de pestaña puede tener contenido basado en web, puede tener una pestaña personalizada para el contenido web en Teams o agregar funcionalidad específica de Teams al contenido web.
* Aplicación de bot: los bots pueden ser bots de chat o bot conversacional que le permiten realizar tareas sencillas y repetitivas, como el servicio de atención al cliente o el personal de soporte técnico.
* Bot de notificación: puede enviar mensajes en el canal de Teams o en el chat grupal o personal mediante bots de notificación con una solicitud HTTP.
* Bot de comandos: puede automatizar tareas repetitivas mediante el bot de comandos. Los bots de comandos le ayudan a responder a consultas sencillas o comandos enviados en chats.
* Extensiones de mensaje: puede interactuar con el servicio web a través de botones y formularios. Funcionalidad proporcionada por la extensión de mensaje.

### <a name="create-your-teams-app-using-spfx"></a>Creación de una aplicación de Teams con SPFx

Teams Toolkit en Visual Studio Code permite crear aplicaciones de pestaña mediante SPFx. Estas aplicaciones tienen las siguientes ventajas:

* Proporciona una integración sencilla con los datos que residen en SharePoint en Teams.
* Puede integrar la solución SPFx con las API empresariales protegidas con Microsoft Azure Active Directory (Azure AD).
* Proporciona acceso a varias herramientas de código abierto.
* Crea para aplicaciones eficaces que pueden ofrecer una experiencia de usuario excelente.
* Se integra fácilmente con otras cargas de trabajo de Microsoft (Office) 365.
* Ofrece flexibilidad para hospedar aplicaciones siempre que sea necesario.

## <a name="support-for-azure-functions"></a>Compatibilidad con Azure Functions

Puede usar el kit de herramientas de Teams para integrar [las funcionalidades de Azure Functions](/azure/azure-functions/functions-overview) en la creación de aplicaciones. Puede centrarse en los fragmentos de código que más importan y Azure Functions hacer el resto.
Azure Functions le permiten implementar:

1. Lógica del sistema en los bloques de código disponibles fácilmente. Estos bloques se denominan funciones.
1. A medida que aumentan las solicitudes, Azure Functions cumple el requisito con tantas demandas como sea necesario.

Azure Function se integra con una matriz de [servicios](add-resource.md#types-of-cloud-resources) en la nube que proporcionan implementaciones enriquecidas con características. Los siguientes son solo algunos escenarios comunes para Azure Functions:

* Al compilar una API web
* Procesamiento de cambios en la base de datos
* Procesamiento de flujos de datos de Iot
* Administración de colas de mensajes

## <a name="see-also"></a>Vea también

* [Kit de herramientas de Teams para Visual Studio](visual-studio-overview.md)
* [Administración de aplicaciones de Teams mediante el Portal para desarrolladores](../concepts/build-and-test/teams-developer-portal.md)
* [Crear una nueva aplicación de Teams con el Kit de herramientas de Teams](create-new-project.md)
