---
title: Referencias de API REST de configuración y control de colaboración
author: surbhigupta
description: En este módulo, obtenga información sobre el control de colaboración y la referencia de la API REST de configuración para administrar la configuración, iniciar, asignar y recuperar actividades de colaboración.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: bc0a5e6834077e199c1dff26568ef2acfeb72745
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179241"
---
# <a name="collaboration-control-and-settings-rest-api-reference"></a>Referencia de la API REST de configuración y control de colaboración

Los desarrolladores pueden usar el control de colaboración y la API REST configuración para administrar la configuración, iniciar, asignar y recuperar actividades de colaboración con sus propias entidades de modelo de negocio.

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

En este artículo se proporciona referencia a la API REST de la solución de control de colaboración.

## <a name="rest-operations-collaboration---custom-api"></a>Operaciones REST: Colaboración: API personalizada

|Operación|Descripción|
|---------|-----------|
|[Asociar mapa de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/associate-collaboration-map)|Asocia una entidad de colaboración a una sesión de colaboración.|
|[Iniciar sesión de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/begin-collaboration-session)|Crea un registro de sesión de colaboración vinculado a una entidad empresarial, contexto de aplicación y metadatos opcionales.|
|[Desasociar mapa de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/disassociate-collaboration-map-custom-api)|Desasocia una entidad asignada de la sesión de colaboración determinada.|
|[Recuperar mapas de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/retrieve-collaboration-maps-custom-api)|Obtiene una lista de asignaciones de colaboración para una sesión de un tipo de entidad específico.|
|[Recuperar sesión de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/retrieve-collaboration-session-custom-api)|Obtiene un registro de sesión de colaboración basado en los parámetros proporcionados.|
|[Actualizar mapa de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/update-collaboration-map-custom-api)|Novedades un registro de mapa de colaboración y sus metadatos si se proporcionan.|
|[Actualizar sesión de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/update-collaboration-session)|Novedades un registro de sesión de colaboración y, opcionalmente, sus metadatos.|

## <a name="rest-operations-collaboration---standard-odata-apis"></a>Operaciones REST: colaboración: API estándar de OData

|Operación|Descripción|
|---------|-----------|
|[Obtención del mapa de colaboración por identificador](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-map-by-id)|Obtiene los detalles de un registro de mapa de colaboración.|
|[Obtener metadatos de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-metadata)|Obtiene una lista de los registros de metadatos de colaboración para un mapa de colaboración determinado o un nombre de entidad raíz de colaboración.|
|[Obtener raíz de colaboración](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-root)|Enumera todas las sesiones de colaboración creadas.|

## <a name="rest-operations-settings---custom-apis"></a>Operaciones REST: configuración: API personalizadas

|Operación|Descripción|
|---------|-----------|
|[Crear y actualizar la configuración](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/create-update-setting-custom-api)|Crea o actualiza una configuración que coincide con la ruta de acceso del grupo y el nombre de la definición de configuración.|
|[Recuperar la configuración null](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/retrieve-null-settings-custom-api)|Devuelve una lista de definiciones de configuración que no tienen un valor.|
|[Recuperar configuración](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/retrieve-settings-custom-api)|Devuelve una lista de configuraciones o configuraciones específicas en grupos.|

## <a name="rest-operations-settings---standard-odata-apis"></a>Operaciones REST: Configuración: API estándar de OData

|Operación|Descripción|
|---------|-----------|
|[Eliminar definición de configuración](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-definition)|Elimina una definición de configuración.|
|[Eliminar grupo de configuración](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-group)|Elimina un grupo de configuración.|
|[Eliminar tipo de configuración](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-type)|Elimine un tipo de configuración.|
|[Eliminar valor de configuración](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-value)|Elimina un valor de configuración.|
|[Obtener definiciones de configuración](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-definitions)|Enumera las definiciones de configuración.|
|[Obtener grupos de configuración](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-groups)|Enumera los grupos de configuración.|
|[Obtener tipos de configuración](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-types)|Enumera los tipos de configuración.|
|[Obtener valor de configuración](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-value)|Enumera los valores de configuración.|
|[Definición de configuración de revisión](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-definition)|Novedades una definición de configuración.|
|[Grupo de configuración de revisiones](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-group)|Novedades un grupo de configuración.|
|[Tipo de configuración de revisión](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-type)|Novedades un tipo de configuración.|
|[Valor de configuración de revisión](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-value)|Novedades un valor de configuración.|
|[Definición de configuración posterior](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-definition)|Crea una nueva definición de configuración.|
|[Grupo de configuración de publicación](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-group)|Crea un nuevo grupo de configuración.|
|[Tipo de configuración de publicación](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-type)|Crea un nuevo tipo de configuración.|
|[Valor de configuración de publicación](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-value)|Crea un nuevo valor de configuración.|
