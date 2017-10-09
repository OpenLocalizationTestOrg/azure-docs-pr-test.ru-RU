---
title: "aaaHow tooscale среды аналитики ряда времени Azure | Документы Microsoft"
description: "В этом учебнике описано как tooscale среды Azure Insights ряда времени"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>Как tooscale среды времени серии аналитики

В этом учебнике описано как tooscale среды аналитики ряда времени.

> [!NOTE]
> Увеличение масштаба в разных номерах SKU запрещено. Среду с номером SKU S1 нельзя преобразовать в среду S2.

## <a name="s1-sku-ingress-rates-and-capacities"></a>Скорость приема и емкость номера SKU S1

| Емкость номера SKU S1 | Скорость приема | Максимальная емкость хранилища
| --- | --- | --- |
| 1 | 1 ГБ (1 млн событий) | 30 ГБ в месяц (30 млн событий) |
| 10 | 10 ГБ (10 млн событий) | 300 ГБ в месяц (300 млн событий) |

## <a name="s2-sku-ingress-rates-and-capacities"></a>Скорость приема и емкость номера SKU S2

| Емкость номера SKU S2 | Скорость приема | Максимальная емкость хранилища
| --- | --- | --- |
| 1 | 10 ГБ (10 млн событий) | 300 ГБ в месяц (300 млн событий) |
| 10 | 100 ГБ (100 млн событий) | 3 ТБ в месяц (3 млрд событий) |

Емкость масштабируется линейно, поэтому номер SKU S1 с емкостью 2 поддерживает скорость приема 2 ГБ (2 млн событий) в неделю и 60 ГБ (60 млн событий) в месяц.

## <a name="changing-hello-capacity-of-your-environment"></a>Изменение емкости hello среды

1. В hello портал Azure, выберите hello среды, емкость которого вы хотите toochange.
1. В разделе "Параметры" щелкните "Настроить".
1. Используйте hello емкость ползунок tooselect hello емкость, удовлетворяющий требованиям тарифы входящих сообщений hello и емкость хранилища.

## <a name="next-steps"></a>Дальнейшие действия

* Убедитесь, что достаточно hello новой емкости tooprevent регулирования. Дополнительные сведения см. в разделе hello *среды возможно получение регулироваться* раздел [здесь](time-series-insights-diagnose-and-solve-problems.md).
