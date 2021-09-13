---
title: Conectores de turnos listos para producción
description: Administración de personal Conectores de turnos para Teams
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
ms.localizationpriority: medium
keywords: Microsoft Teams conectores de Microsoft Teams kronos
ms.author: lajanuar
ms.openlocfilehash: f734bc4491826f5afee4147b55fdbc10b69fd433
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157133"
---
# <a name="production-ready-shifts-connectors"></a>Conectores de turnos listos para producción  

Teams Los conectores de administración de personal de turnos (WFM) son integraciones basadas en la comunidad, listas para producción y de código abierto, útiles para los trabajadores de primera línea. Ofrecen una experiencia perfecta y un proceso rápido para la transformación digital de trabajadores de primera línea con Teams Shifts. 

Cada conector proporciona instrucciones detalladas para la implementación e integración en la organización. El código fuente completo está disponible en GitHub repositorio. Puede explorar en detalle o bifurcar, y personalizar para satisfacer sus necesidades específicas.   

En este documento se ofrece información general sobre las principales ventajas de los conectores WFM de Teams Shifts, el conector De Kronos a Teams Shifts y el conector de turnos de Teams JDA a Teams.

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Ventajas clave de los Teams de WFM de shifts

A continuación se incluyen las principales ventajas de los Teams de WFM de shifts:

* **Experiencia de plug and play:** Todos los conectores WFM de shifts incluyen ARM scripts de implementación de Azure que le permiten hospedar todos los servicios necesarios en Microsoft Azure. No se requiere codificación para implementar las aplicaciones.

* **Código listo para producción:** Todos los conectores Shifts se ajustan a los procedimientos recomendados de seguridad e infraestructura y se revisan todos los cambios enviados por la comunidad para garantizar la conformidad continua.

* **Personalizable y extensible:**   Mientras que todos los conectores DE WFM de turnos están listos para implementarse para su uso inmediato, con la base de código completa y los scripts de implementación disponibles. Puede personalizarlos o ampliarlos fácilmente para que se ajusten a sus necesidades únicas.

* **Documentación detallada & soporte técnico:**   Todos los conectores DE WFM de turnos se acompañan de documentación completa para los pasos de configuración, implementación y arquitectura de soluciones. Los repositorios del conector se supervisan, de modo que pueda informar de los problemas, desafíos o dificultades que encuentre a través del rastreador de problemas GitHub repositorio.

* **Integración perfecta:** La integración entre las soluciones WFM y los turnos de Teams permite a los trabajadores de primera línea usar la aplicación Teams Shifts para ver o administrar sus horarios y horas de turnos, y usar todas las demás características de colaboración enriquecciones proporcionadas en Teams directamente desde su dispositivo móvil o escritorio sin tener que cambiar de contexto a otra aplicación.  

**Abrir la vista de turnos en Teams** 

La vista de turnos Teams se muestra en la siguiente imagen: 

![Abrir turnos en Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Conector de kronos a Teams shifts

Con el código de código abierto, puede integrar Kronos Workforce Central Versión 8.1 y versiones posteriores, con cambios de Teams como, aplicación de escritorio o móvil Teams para los siguientes escenarios de administrador y trabajador de primera línea:

* Ver programación.

* Publicar y solicitar turnos abiertos.

* Turnos de intercambio.

* Solicitar tiempo de espera.

* Turnos de oferta.

Para obtener más información sobre la implementación de Kronos-to-Teams Shifts connector, vea [Get it on GitHub](https://aka.ms/KronosShiftsConnector).

## <a name="jda-to-teams-shifts-connector"></a>Conector de turnos de Teams JDA a Teams

Con código de código abierto, puedes integrar JDA, como BlueYonder versión 17.2 y versiones posteriores, con cambios de Teams como, aplicaciones de escritorio o de Teams móviles para los siguientes escenarios de administrador y trabajador de primera línea:

* Publicar turnos y programar grupos en JDA y verlos en Teams.

* Habilitar escenarios de programación enriquecidos, incluida la solicitud de intercambios de turnos y el tiempo de espera.

* Establecer la disponibilidad del usuario mediante la [API Graph Microsoft para Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).

Para obtener más información sobre la contribución y la sugerencia, vea [Obtenerla en GitHub](https://aka.ms/JDAShiftsConnector).</br></br>

## <a name="see-also"></a>Vea también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
