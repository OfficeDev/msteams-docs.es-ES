---
title: Administración de permisos de aplicaciones de Teams
author: surbhigupta
description: En este módulo, obtenga información sobre cómo se administran las aplicaciones de Teams en diferentes lugares en función de la característica.
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 2bc501444e52f31061312c325ddf7dd80370240a
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791852"
---
# <a name="permissions-in-teams-app"></a>Permisos en la aplicación Teams

El permiso para la aplicación teams se administra en dos lugares, según la característica de la aplicación:

* [Consentimiento específico del recurso (RSC)](#resource-specific-consent)
* [Azure Active Directory (Azure AD)](#azure-active-directory)

:::image type="content" source="../../assets/images/teams-app-permissions.png" alt-text="En la captura de pantalla se describen los distintos permisos de aplicación de Teams.":::

## <a name="resource-specific-consent"></a>Consentimiento específico del recurso

RSC es una integración de Microsoft Teams y Microsoft Graph API que permite a la aplicación usar puntos de conexión de API para administrar recursos específicos, ya sea equipos o chats, dentro de una organización. Para obtener más información, consulte [Habilitación del consentimiento específico de recursos en Teams](../rsc/resource-specific-consent.md).

Los permisos de RSC solo están disponibles para las aplicaciones de Teams instaladas en el cliente de Teams y actualmente no forman parte del portal de Azure AD y se declaran en el archivo de manifiesto de aplicación (JSON) de Teams.

## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD es un servicio de administración de identidades y acceso basado en la nube. Este servicio ayuda a los empleados a acceder a recursos externos, como Microsoft 365, el Azure Portal y miles de otras aplicaciones SaaS. Para obtener más información, vea [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis).

### <a name="microsoft-graph-api-permission"></a>Permiso de Microsoft Graph API

Graph API permisos se administran en Azure AD. Para que su aplicación pueda obtener acceso a los datos de Microsoft Graph, el usuario o el administrador deben concederle los permisos correctos a través de un proceso de consentimiento. Para más información, vea [Permisos de Microsoft Graph](/graph/permissions-reference).

## <a name="capability-wise-management"></a>Administración eficaz de la funcionalidad

### <a name="bot-and-messaging-extension"></a>Bot y extensión de mensajería

El identificador de extensión de mensajería o bot se genera en función de la siguiente plataforma de registro. Este identificador es necesario para agregar un bot o una extensión de mensajería a una aplicación de Teams.

* Portal de Azure AD
* Portal para desarrolladores o Bot Framework

#### <a name="azure-ad-portal"></a>Portal de Azure AD

Cuando se registra un bot o una extensión de mensajería en el portal de Azure AD, tendrá asociado un identificador de aplicación de Azure AD, que se puede encontrar en el portal de **Azure AD** > **registros de aplicaciones**. Los puntos de conexión y otras configuraciones de bot se administran en el Azure Portal.

#### <a name="developer-or-bot-framework-portal"></a>Portal para desarrolladores o Bot Framework

Cuando se registra un bot o una extensión de mensajería en el portal de Developer o Bot Framework, no tendrá un identificador de aplicación de Azure AD. Sin embargo, el bot o el identificador de extensión de mensajería se pueden encontrar en el portal de Bot Framework. Los puntos de conexión y otras configuraciones de bot se administran en el portal de Bot Framework.

Otras configuraciones específicas de Teams para el bot se pueden administrar en la sección Portal para desarrolladores de la aplicación.

### <a name="connectors"></a>Conectores

Los conectores tienen un identificador de conector y se registran y administran a través del Panel para desarrolladores de conectores. Este identificador es necesario para introducir un conector en la aplicación teams. Otras configuraciones específicas de Teams para conectores se pueden administrar en la sección portal para desarrolladores de la aplicación.
