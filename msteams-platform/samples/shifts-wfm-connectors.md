---
title: Conectores de turnos listos para producción
description: Obtenga información sobre las ventajas de usar los conectores Shifts de administración de Workforce para Teams, como el conector Kronos-to-Teams Shifts y el conector de JDA a Teams Shifts.
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
ms.localizationpriority: high
keywords: Conectores Kronos de Microsoft Teams
ms.author: lajanuar
ms.openlocfilehash: 3a294d20bc2032df7ef5dfa225922e9dccabf1df
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111769"
---
# <a name="production-ready-shifts-connectors"></a>Conectores de turnos listos para producción  

Los conectores de administración del personal (WFM) de Teams Shift son integraciones preparadas para la producción, de código abierto y controladas por la comunidad, útiles para los trabajadores de primera línea. Ofrecen una experiencia perfecta y un proceso rápido para la transformación digital de los trabajadores de primera línea con los turnos de Teams.

Cada conector proporciona instrucciones detalladas para la implementación y la integración en su organización. El código fuente completo está disponible en el repositorio de GitHub. Puede explorarlo en detalle o bifurcarlo, y personalizarlo para satisfacer sus necesidades específicas.

En este documento se proporciona información general sobre las principales ventajas de los conectores WFM de Teams Shifts, el conector Kronos-to-Teams Shifts y el conector JDA-to-Teams Shifts.

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Ventajas clave de los conectores WFM de Teams Shifts

A continuación se muestran las principales ventajas de los conectores WFM de Teams Shifts:

* **Experiencia plug and play:** Todos los conectores de WFM de Shifts incluyen scripts de implementación de Azure de ARM que permiten hospedar todos los servicios necesarios en Microsoft Azure. No se requiere codificación para implementar las aplicaciones.

* **Código listo para producción:** Todos los conectores de Shifts se ajustan a los procedimientos recomendados de seguridad e infraestructura y se revisan todos los cambios enviados por la comunidad para garantizar la conformidad continua.

* **Personalizable y extensible:** Aunque todos los conectores de WFM de Shifts están listos para implementarse para su uso inmediato, con todo el código base y los scripts de implementación disponibles. Puede personalizarlos o ampliarlos fácilmente para satisfacer sus necesidades únicas.

* **Documentación detallada y soporte técnico:** Todos los conectores de WFM de Shifts van acompañados de documentación de un extremo a otro para los pasos de arquitectura, implementación y configuración de la solución. Los repositorios del conector se supervisan para que pueda notificar cualquier problema, desafío o dificultad que encuentre a través del seguimiento de problemas del repositorio de GitHub.

* **Integración sin problemas:** la integración entre las soluciones WFM y Teams Shifts permite a los trabajadores de primera línea usar la aplicación Teams Shifts para ver o administrar sus horarios y tiempos de desplazamiento, y usar todas las demás características de colaboración enriquecidas proporcionadas en Teams directamente desde su dispositivo móvil o escritorio sin tener que cambiar el contexto a otra aplicación.  

Abra la vista de turnos en Teams:

La vista de turnos de Teams se muestra en la siguiente imagen:

![Abrir turnos en Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Conector Kronos-to-Teams Shifts

Con código abierto, puede integrar Kronos Workforce Central versión 8.1 y versiones posteriores, con Teams Shifts, como la aplicación de Teams de escritorio o móvil para los siguientes escenarios de administrador y trabajo de primera línea:

* Ver programación.

* Publicar y solicitar turnos abiertos.

* Intercambio de turnos.

* Solicitar tiempo libre.

* Ofrecer turnos.

Para obtener más información sobre la implementación del conector Kronos-to-Teams Shifts, consulte [Conseguirlo en GitHub](https://aka.ms/KronosShiftsConnector).

## <a name="jda-to-teams-shifts-connector"></a>Conector de desplazamientos de JDA a Teams Shifts.

Con código de código abierto, puede integrar JDA, como BlueYonder versión 17.2 y posteriores, con Teams Shifts, como, la aplicación de escritorio o móvil de Teams para los siguientes escenarios de trabajador de primera línea y administrador:

* Publique turnos y organizar grupos en JDA y verlos en Teams.

* Habilite escenarios de programación enriquecidos, incluidos la solicitud de intercambios de turnos y tiempo de expiración.

* Establezca la disponibilidad del usuario mediante [Microsoft Graph API para Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).

Para obtener más información sobre la contribución y la sugerencia, consulte [Conseguirlo en GitHub](https://aka.ms/JDAShiftsConnector).

## <a name="see-also"></a>Consulte también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
