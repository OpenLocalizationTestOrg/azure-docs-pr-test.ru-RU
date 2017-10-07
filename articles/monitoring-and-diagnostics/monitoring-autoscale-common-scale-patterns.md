---
title: "aaaOverview общих шаблонов автомасштабирования | Документы Microsoft"
description: "Узнайте, что некоторые распространенные шаблоны tooauto hello масштабировать ресурс в Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>Обзор общих шаблонов автомасштабирования
В этой статье описаны некоторые распространенные шаблоны tooscale hello ресурс в Azure.

Автоматическое масштабирование Azure монитор применяется только tooVirtual задает масштаб компьютера (VMSS), облачные службы, планах службы приложений и среды службы приложений. 

# <a name="lets-get-started"></a>Начало работы

В данной статье предполагается, что вы знакомы с автомасштабированием. Вы можете [получить ресурс работы здесь tooscale][1]. Hello ниже приведены некоторые распространенные шаблоны шкалы hello.

## <a name="scale-based-on-cpu"></a>Масштабирование на основе использования ЦП

У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того: 

- Вы хотите tooscale out/шкалы, в зависимости от ЦП.
- Кроме того, требуется tooensure имеется минимальное число экземпляров. 
- Кроме того требуется tooensure, toohello максимального количества экземпляров, которыми можно масштабировать до.

![Масштабирование на основе использования ЦП][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Масштабирование в рабочие и выходные дни

У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того:

- требуется 3 экземпляра по умолчанию (в рабочие дни);
- Трафик не нужна в выходные и таким образом вы хотите tooscale работу экземпляра too1 на выходные дни.

![Масштабирование в рабочие и выходные дни][3]

## <a name="scale-differently-during-holidays"></a>Масштабирование в праздничные дни

У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того: 

- Вы хотите tooscale вверх или вниз по умолчанию, основанное на ЦП
- Однако во время праздников (или в определенные дни, которые важны для бизнеса) необходимо toooverride hello значения по умолчанию и имеют больший объем в вашем распоряжении.

![Масштабирование в праздничные дни][4]

## <a name="scale-based-on-custom-metric"></a>Масштабирование на основе пользовательской метрики

У вас есть веб-интерфейса и уровня API, который взаимодействует с серверной hello. 

- Требуется tooscale hello API уровня на основе пользовательских событий в hello внешнего интерфейса (пример: требуется, чтобы процесс извлечения на основе hello числа элементов в корзину hello tooscale)

![Масштабирование на основе пользовательской метрики][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png