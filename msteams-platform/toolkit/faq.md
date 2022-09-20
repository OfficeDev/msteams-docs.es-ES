---
title: Preguntas más frecuentes
author: MuyangAmigo
description: En este módulo, consulte preguntas más frecuentes sobre el kit de herramientas de Teams mediante Visual Studio Code
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 2b229b14db563a6b7a4dc587ac67c872d461ec72
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806904"
---
# <a name="faq-for-teams-toolkit"></a>Preguntas más frecuentes sobre el kit de herramientas de Teams

Puede ver las preguntas más frecuentes de todas las secciones del kit de herramientas de Teams para Visual Studio Code.

Preguntas más frecuentes sobre [el aprovisionamiento de recursos en la nube mediante el kit de herramientas de Teams](provision.md)

<br>

<details>

<summary><b>Solución de problemas</b></summary>

Si recibe errores con el kit de herramientas de Teams en Visual Studio Code, puede seleccionar **Obtener ayuda** en la notificación del error para navegar al documento relacionado. Si usa la CLI de TeamsFx, al final del mensaje habrá un hipervínculo que apunta al documento de ayuda. También puede ver el [documento de ayuda de aprovisionamiento](https://aka.ms/teamsfx-arm-help) directamente.

<br>

</details>

<details>

<summary><b>¿Cómo puedo cambiar a otra suscripción de Azure durante el aprovisionamiento?</b></summary>

1. Cambie la suscripción en la cuenta actual o cierre la sesión y seleccione una nueva suscripción.
2. Si ya ha aprovisionado el entorno actual, debe crear un nuevo entorno y realizar el aprovisionamiento porque ARM no admite el traslado de recursos.
3. Si no aprovisionó el entorno actual, puede desencadenar el aprovisionamiento directamente.

<br>

</details>

<details>

<summary><b>¿Cómo puedo cambiar el grupo de recursos durante el aprovisionamiento?</b></summary>

Antes del aprovisionamiento, la herramienta le pregunta si desea crear un nuevo grupo de recursos o usar uno existente. Puede proporcionar un nuevo nombre de grupo de recursos o elegir uno existente en este paso.

<br>

</details>

<details>

<summary><b>¿Cómo puedo aprovisionar una aplicación basada en SharePoint?</b></summary>

Puede consultar [aprovisionamiento de aplicaciones basadas en SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4).

> [!NOTE]
> Actualmente, compilar aplicaciones de Teams con SharePoint Framework con el kit de herramientas de Teams no tiene integración directa con Azure. Los contenidos en el documento no se aplican a aplicaciones basadas en SPFx.

<br>

</details>
