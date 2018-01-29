---
title: "Как масштабировать среду Azure Time Series Insights | Документация Майкрософт"
description: "В этом руководстве описано масштабирование среды Azure Time Series Insights. Используйте портал Azure для добавления или вычитания ресурсов в ценовой категории SKU."
services: time-series-insights
ms.service: time-series-insights
author: sandshadow
ms.author: edett
manager: jhubbard
editor: MicrosoftDocs/tsidocs
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.devlang: csharp
ms.workload: big-data
ms.topic: article
ms.date: 11/15/2017
ms.openlocfilehash: edcd9561778998c4df09cc5014f8b8ba81c0e369
ms.sourcegitcommit: 7d107bb9768b7f32ec5d93ae6ede40899cbaa894
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/16/2017
---
# <a name="how-to-scale-your-time-series-insights-environment"></a>Как масштабировать среду Azure Time Series Insights

В этой статье описывается, как изменять емкость среды Time Series Insights с помощью портала Azure. Емкость — множитель, применяемый к скорости входящих данных, емкости хранилища и затратам, связанным с выбранным номером SKU. 

Портал Azure можно использовать для увеличения или уменьшения емкости в пределах ценовой категории SKU. 

Однако изменение ценовой категории SKU запрещено. Например, среду с ценовой категорией SKU S1 нельзя преобразовать в среду S2 или наоборот. 


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

## <a name="change-the-capacity-of-your-environment"></a>Изменение емкости среды
1. Найдите и выберите среду Time Series Insights на портале Azure. 

2. В меню среды службы "Аналитика временных рядов" выберите **Настроить**.

   ![configure.png](media/scale-your-environment/configure.png)

3. Настройте ползунок **емкости** соответственно требованиям скорости приема и емкости хранилища. Обратите внимание, что **скорость приема**, **емкость хранилища** и **оценочная стоимость** обновляются динамически, чтобы показать эффект изменения. 

   ![Ползунок](media/scale-your-environment/slider.png)

   Кроме того, можно ввести число множителя емкости в текстовом поле справа от ползунка. 

4. Выберите **Сохранить**, чтобы масштабировать среду. Индикатор хода выполнения будет отображаться, пока изменения не зафиксируются. 

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Убедитесь, что новой емкости достаточно для предотвращения регулирования](time-series-insights-diagnose-and-solve-problems.md).
