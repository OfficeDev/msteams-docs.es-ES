---
title: Prueba del comportamiento de la aplicación en un entorno diferente
author: surbhigupta
description: En este módulo, aprenderá a probar el comportamiento de la aplicación en un entorno diferente.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 187219fec76830119e795d1dd60a36b2374c65ac
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617334"
---
# <a name="test-app-behavior-in-different-environment"></a>Prueba del comportamiento de la aplicación en un entorno diferente

Puede probar la aplicación de Teams después de la integración con Microsoft Teams. Para probar la aplicación de Teams, debe crear al menos un área de trabajo en su entorno. Puede usar El kit de herramientas de Teams para probar la aplicación de Teams:

* **Hospedado localmente en Teams**: Teams Toolkit hospeda localmente la aplicación de Teams al transferirla localmente a Teams para realizar pruebas en el entorno local.

* **Hospedado en la nube en Teams**: para probar la aplicación de Teams de forma remota, debe hospedarla en la nube mediante el aprovisionamiento y la implementación en Microsoft Azure Active Directory (Azure AD). Implica cargar la solución en Azure AD y, a continuación, cargarla en Teams.

> [!NOTE]
> Para la depuración y las pruebas a escala de producción, le recomendamos que siga sus propias directrices de empresa para asegurarse de que puede admitir pruebas, ensayos e implementación a través de sus propios procesos.

## <a name="locally-hosted-environment"></a>Entorno hospedado localmente

Teams es un producto basado en la nube que requiere que todos los servicios a los que accede estén disponibles públicamente mediante puntos de conexión HTTPS. El hospedaje local consiste en transferir localmente a Teams para realizar pruebas en el entorno local.

> [!NOTE]
> Aunque puede usar cualquier herramienta de su elección para las pruebas, le recomendamos que use [ngrok](https://ngrok.com/download).

## <a name="cloud-hosted-environment"></a>Entorno hospedado en la nube

Para hospedar el código de desarrollo y producción y sus puntos de conexión HTTPS, debe probar de forma remota la aplicación de teams mediante el aprovisionamiento y la implementación en Azure AD. Debe asegurarse de que todos los dominios son accesibles desde la aplicación de Teams que aparece en el [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) objeto del `manifest.jason` archivo.

> [!NOTE]
> Para garantizar un entorno seguro, sea explícito sobre el dominio y los subdominios exactos a los que hace referencia y esos dominios deben estar en su control. Por ejemplo, no se recomienda `*.azurewebsites.net`, pero se recomienda `contoso.azurewebsites.net`.

## <a name="see-also"></a>Vea también

* [Depuración local de la aplicación de Microsoft Teams](debug-local.md)
* [Depurar procesos en segundo plano](debug-background-process.md)
* [usar el kit de herramientas de Teams para aprovisionar recursos en la nube](provision.md)
* [Implementar en la nube](deploy.md)
* [Vista previa y personalización del manifiesto de la aplicación de Teams](TeamsFx-preview-and-customize-app-manifest.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
