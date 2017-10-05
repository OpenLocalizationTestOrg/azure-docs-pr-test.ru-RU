---
title: "Учебник по службам Azure Analysis Services: занятие 7 \"Создание ключевых показателей эффективности\" | Документы Майкрософт"
description: "Описывает создание ключевых показателей эффективности в учебном проекте служб Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: d78808421dd5acd907aa9e9000bb3b770a42c061
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-7-create-key-performance-indicators"></a>Занятие 7. Создание ключевых показателей эффективности

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

В этом занятии вы создадите ключевые показатели эффективности (КПЭ). Ключевые показатели эффективности используются для оценки эффективности значения, определенного *базовой* мерой, по отношению к *целевому* значению, также определенному мерой или абсолютным значением. В клиентских приложениях по ведению отчетности ключевые показатели эффективности позволяют специалистам быстро и просто получить сводку по успешности бизнеса или выявить тенденции. Дополнительные сведения см. в разделе [Ключевые показатели эффективности](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular).
  
Предполагаемое время выполнения этого занятия: **15 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Прежде чем выполнять задачи в этом разделе, нужно завершить предыдущее занятие: [Занятие 6. Создание мер](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Создание ключевых показателей эффективности  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Создание ключевого показателя эффективности InternetCurrentQuarterSalesPerformance  
  
1.  В конструкторе моделей выберите таблицу **FactInternetSales**.  
  
2.  Щелкните пустую ячейку в сетке мер.  
  
3.  В строке формул над таблицей введите следующую формулу: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Эта мера будет использоваться в качестве базовой для ключевого показателя эффективности.  
  
4.  Щелкните правой кнопкой мыши **InternetCurrentQuarterSalesPerformance** > **Создать ключевой показатель эффективности**.   
  
5.  В поле **Цель** диалогового окна "Ключевой показатель эффективности" выберите **Абсолютное значение**, а затем введите **1.1**.  
  
7.  В левом (нижнем) поле с ползунком введите **1**, а в правом (верхнем) — **1.07**.  
  
8.  В области **Выберите стиль значка** выберите значок в виде ромба (красного цвета), треугольника (желтого цвета), круга (зеленого цвета).
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Обратите внимание на развертываемую метку **Описания** под доступными стилями значков. Используйте описания для разных элементов ключевых показателей эффективности, чтобы сделать их более понятными в клиентских приложениях.  
  
9. Нажмите кнопку **ОК**, чтобы завершить создание КПЭ.  
  
    В сетке мер обратите внимание на значок рядом с мерой **InternetCurrentQuarterSalesPerformance**. Он указывает, что мера служит базовым значением для КПЭ.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>Создание ключевого показателя эффективности InternetCurrentQuarterMarginPerformance  
  
1.  Щелкните пустую ячейку в сетке мер для таблицы **FactInternetSales**.  
  
2.  В строке формул над таблицей введите следующую формулу:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Щелкните правой кнопкой мыши **InternetCurrentQuarterMarginPerformance** > **Создать ключевой показатель эффективности**.  
  
4.  В поле **Цель** диалогового окна "Ключевой показатель эффективности" выберите **Абсолютное значение**, а затем введите **1.25**.   
  
5.  В левом (нижнем) поле с ползунком прокрутите до значения **0.8**, а в правом (верхнем) — до значения **1.03**.  
  
6.  В области **Выберите стиль значка** выберите значок в виде ромба (красного цвета), треугольника (желтого цвета), круга (зеленого цвета) и нажмите кнопку **ОК**.  
  
## <a name="whats-next"></a>Что дальше?
[Занятие 8. Создание перспектив](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
