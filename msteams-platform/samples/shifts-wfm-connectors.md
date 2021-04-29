---
title: Conectores de turnos listos para producción
description: Conectores de turnos de administración de personal para Teams
ms.topic: reference
author: laujan
ms.date: 03/09/2020
localization_priority: Normal
keywords: Kronos de conectores de Microsoft Teams
ms.author: lajanuar
ms.openlocfilehash: 459797dd3f8425223c0dcbedc335955bf106ae37
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075741"
---
# <a name="production-ready-shifts-connectors"></a>Conectores de turnos listos para producción  

Los conectores de administración de fuerza de trabajo (WFM) de Teams Shifts son integraciones basadas en la comunidad, listas para producción y de código abierto, útiles para los trabajadores de primera línea. Ofrecen una experiencia perfecta y un proceso rápido para la transformación digital de los trabajadores de primera línea con Teams Shifts. 

Cada conector proporciona instrucciones detalladas para la implementación e integración en la organización. El código fuente completo está disponible en el repositorio de GitHub. Puede explorar en detalle o bifurcar, y personalizar para satisfacer sus necesidades específicas.   

En este documento se ofrece información general sobre las principales ventajas de los conectores WFM de Turnos de Teams, el conector de turnos de Kronos a Teams y el conector de turnos de JDA a Teams.

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Ventajas clave de los conectores WFM de Teams Shifts

A continuación se desconocien las principales ventajas de los conectores WFM de Teams Shifts:

* **Experiencia de plug and play:** Todos los conectores WFM de shifts incluyen ARM scripts de implementación de Azure que le permiten hospedar todos los servicios necesarios en Microsoft Azure. No se requiere codificación para implementar las aplicaciones.

* **Código listo para producción:** Todos los conectores Shifts se ajustan a los procedimientos recomendados de seguridad e infraestructura y se revisan todos los cambios enviados por la comunidad para garantizar la conformidad continua.

* **Personalizable y extensible:**   Mientras que todos los conectores DE WFM de turnos están listos para implementarse para su uso inmediato, con la base de código completa y los scripts de implementación disponibles. Puede personalizarlos o ampliarlos fácilmente para que se ajusten a sus necesidades únicas.

* **Documentación detallada & soporte técnico:**   Todos los conectores DE WFM de turnos se acompañan de documentación completa para los pasos de configuración, implementación y arquitectura de soluciones. Los repositorios del conector se supervisan, de modo que pueda informar de los problemas, desafíos o dificultades que encuentre a través del rastreador de problemas de GitHub del repositorio.

* **Integración perfecta:** La integración entre las soluciones WFM y Teams Shifts permite a los trabajadores de primera línea usar la aplicación Teams Shifts para ver o administrar sus horarios y turnos de trabajo, y usar todas las demás características de colaboración enriquecciones proporcionadas en Teams directamente desde su dispositivo móvil o escritorio sin tener que cambiar el contexto a otra aplicación.  

**Vista Abrir turnos en Teams** 

La vista turnos de Teams se muestra en la siguiente imagen: 

![Turnos abiertos en Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Conector de cambios de Kronos a Teams

Con el código de código abierto, puedes integrar Kronos Workforce Central Versión 8.1 y versiones posteriores, con cambios de Teams como, aplicaciones de escritorio o móviles de Teams para los siguientes escenarios de administrador y trabajador de primera línea:

* Ver programación.

* Publicar y solicitar turnos abiertos.

* Turnos de intercambio.

* Solicitar tiempo de espera.

* Turnos de oferta.

Para obtener más información sobre la implementación del conector de cambios de Kronos a Teams, consulte [Get it on GitHub](https://aka.ms/KronosShiftsConnector).

## <a name="jda-to-teams-shifts-connector"></a>Conector de turnos de JDA a Teams

Con el código de código abierto, puedes integrar JDA, como BlueYonder versión 17.2 y versiones posteriores, con cambios de Teams como, aplicaciones de teams móviles o de escritorio para los siguientes escenarios de administrador y trabajador de primera línea:

* Publicar turnos y programar grupos en JDA y verlos en Teams.

* Habilitar escenarios de programación enriquecidos, incluida la solicitud de intercambios de turnos y el tiempo de espera.

* Establecer la disponibilidad del usuario mediante la [API de Microsoft Graph para turnos](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).

Para obtener más información sobre la contribución y la sugerencia, vea [Get it on GitHub](https://aka.ms/JDAShiftsConnector).</br></br>

## <a name="see-also"></a>Consulte también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
