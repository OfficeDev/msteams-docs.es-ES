---
title: Análisis del uso de la aplicación en el Portal para desarrolladores
description: En este módulo, aprenderá a analizar el uso de la aplicación en el Portal para desarrolladores.
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 43758fdebd1f2e76318880a51d9173469b0ed604
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232428"
---
# <a name="analyze-your-apps-usage-in-developer-portal"></a>Análisis del uso de la aplicación en el Portal para desarrolladores

En el Portal para desarrolladores de Teams, en la página **Información general** , puede ver el número total de usuarios activos de la aplicación.

> [!NOTE]
> El análisis de uso solo está disponible actualmente para las nuevas aplicaciones personalizadas publicadas en su organización a través del **Portal para desarrolladores** para Teams o importadas en **el Portal para desarrolladores** para Teams después de abril de 2022. El análisis de uso de todas las aplicaciones publicadas en la tienda de Teams está disponible en el **Centro de partners** para obtener más información sobre el [informe de uso de aplicaciones de Teams](/office/dev/store/teams-apps-usage).

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *R30 mensual* | Métrica de uso predeterminada. Muestra el recuento de usuarios activos únicos que usaron la aplicación en esa ventana gradual de 30 días en UTC. |
| *A diario* | Muestra el recuento de usuarios activos únicos que usaron la aplicación en un día determinado en UTC. |

El uso de la aplicación para un día determinado se refleja dentro de 24 a 48 horas, y los datos de uso de las nuevas aplicaciones pueden tardar hasta tres o cinco días en reflejarse en los gráficos.

Puede ver el uso de la aplicación y otras conclusiones desde la página **Análisis** . Para acceder a la página:

1. Vaya al **[Portal para desarrolladores de Teams](https://dev.teams.microsoft.com)**.
1. Seleccione **Aplicaciones** en el panel izquierdo.
1. Seleccione la aplicación necesaria en la página **Aplicaciones** .
1. Seleccione **Análisis** en **Información general** o seleccione **Ver detalles** en la tarjeta **Usuarios activos (versión preliminar).**

 :::image type="content" source="../../assets/images/tdp/dev-app-portal.png" alt-text="En las capturas de pantalla se muestra la página de análisis de la aplicación en el Portal para desarrolladores."lightbox="../../assets/images/tdp/dev-app-portal.png":::

A medida que explore métricas individuales en esta página, puede usar el botón **Filtrar** para analizar el uso de la aplicación a partir de las siguientes opciones de filtro:

* Tipo de agregación: este filtro permite agrupar las siguientes métricas por un recuento de usuarios distintos o un recuento de inquilinos o clientes distintos.
* Plataforma
* Sistema operativo
* Área

 :::image type="content" source="../../assets/images/tdp/dev-analytics-filter.png" alt-text="En las capturas de pantalla se muestra el filtro de página de análisis en el Portal para desarrolladores.":::

Después de seleccionar los filtros deseados, puede explorar los siguientes widgets individuales:

* [Uso por período de tiempo](#usage-by-time-period)
* [Uso por plataforma y sistema operativo](#usage-by-platform-and-os)
* [Uso por estado de retención](#usage-by-retention-state)
* [Intensidad de uso](#usage-intensity)

## <a name="usage-by-time-period"></a>Uso por período de tiempo

El gráfico **Uso por período de tiempo** muestra el número de usuarios o inquilinos activos que han abierto y usado la aplicación en distintos períodos de tiempo.

 :::image type="content" source="../../assets/images/tdp/usage-by-time-period.png" alt-text="En las capturas de pantalla se muestra el gráfico de uso por período de tiempo de la aplicación publicada.":::

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| R30 mensual | Cada punto de datos representa un período R30 (30 días graduales) determinado. |
| R28 mensual | Cada punto de datos representa un período R28 (28 días graduales) determinado. |
| R7 semanal| Cada punto de datos representa un período de R7 (7 días consecutivos) determinado. |
| Diario | Cada punto de datos representa un período R1 (1 día gradual) determinado. |

## <a name="usage-by-platform-and-os"></a>Uso por plataforma y sistema operativo

El gráfico **Uso por plataforma y sistema operativo** muestra el uso activo de la aplicación en varios puntos de conexión, como **Windows**, **Mac**, **iOS**, **Android** y **Web**. El mismo usuario o inquilino puede usar una aplicación en varios puntos de conexión. Cada punto de datos representa un período R30 (30 días graduales) determinado.

 :::image type="content" source="../../assets/images/tdp/usage-by-platform-OS.png" alt-text="En las capturas de pantalla se muestra el uso por plataforma y gráfico del sistema operativo de la aplicación publicada.":::

## <a name="usage-by-retention-state"></a>Uso por estado de retención

El gráfico **De uso por estado de retención** permite realizar un seguimiento de cuatro métricas de retención o renovación de claves de la aplicación a lo largo del tiempo.

:::image type="content" source="../../assets/images/tdp/usage-by-retention-state.png" alt-text="En las capturas de pantalla se muestra el gráfico de estado de uso por retención de la aplicación publicada.":::

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| Nuevos usuarios o inquilinos | Usuarios activos o inquilinos que son nuevos y no han usado la aplicación. |
| Devolver usuarios o inquilinos | Usuarios activos o inquilinos que usaron la aplicación durante un período de tiempo R30 (30 días consecutivos) determinado y el período de tiempo R30 inmediatamente anterior. |
| Usuarios o inquilinos resucitados | Usuarios activos o inquilinos que usaron la aplicación una o varias veces antes, pero no en el período de tiempo R30 inmediatamente anterior. |
| Usuarios o inquilinos vencidos | Usuarios activos o inquilinos que no se vieron durante un período de tiempo R30 determinado, pero que se vieron durante el período de tiempo R30 inmediatamente anterior. |

## <a name="usage-intensity"></a>Intensidad de uso

El gráfico **Intensidad de** uso muestra las métricas clave de intensidad de uso de la aplicación.

 :::image type="content" source="../../assets/images/tdp/usage-intensity.png" alt-text="En las capturas de pantalla se muestra el gráfico de intensidad de uso de la aplicación publicada.":::

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| Mediana de días usados al mes | Número medio de días en los que se abrió la aplicación en el último período de tiempo R30 (30 días consecutivos). |
| % de uso de más de 5 días | Porcentaje de usuarios activos que han abierto o usado la aplicación más de cinco días en el último período de tiempo de R30. |
| DAU/MAU | La proporción del número medio de usuarios o inquilinos únicos que usaron la aplicación en cada día dividido entre los usuarios activos mensuales para el período de tiempo R30 seleccionado. |

## <a name="app-dashboard"></a>Panel de la aplicación

En la tabla **del panel Mi aplicación** se muestran los datos R30 (30 días graduales) más recientes para cada una de las métricas de las cuatro categorías anteriores y el cambio Mes a mes. Use el selector de tiempo en la parte superior izquierda y seleccione la fecha deseada; puede ver los datos R30 diarios de los últimos 75 días y finales del mes R30 datos durante un máximo de 12 meses.

Puede seleccionar cada uno de estos **nombres de métrica** para ver las tendencias a lo largo del tiempo.

 :::image type="content" source="../../assets/images/tdp/app-dashboard.png" alt-text="En las capturas de pantalla se muestra el gráfico del panel de aplicaciones de la aplicación publicada.":::

## <a name="see-also"></a>Vea también

[Incluir una oferta de SaaS con la aplicación de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
