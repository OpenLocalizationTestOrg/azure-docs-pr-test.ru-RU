---
Заголовок: aaa «занятие учебника по Azure Analysis Services 7: Создание ключевых показателей эффективности | Документы Microsoft» Описание: описание, как toocreate ключевых показателей эффективности в hello проекта tutorial служб Azure Analysis Services. службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>Занятие 7. Создание ключевых показателей эффективности

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

В этом занятии вы создадите ключевые показатели эффективности (КПЭ). Ключевые показатели эффективности, используемые toogauge производительность значения, определенного *базы* измерения, от *целевой* значения, также определенного мерой или абсолютным значением. В службах reporting клиентских приложений, ключевые показатели эффективности предоставляют бизнесменам быстрый и простой способ toounderstand сводку по бизнес-успех или tooidentify трендов. toolearn более, в разделе [ключевые показатели эффективности](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Предполагаемое время toocomplete на этом занятии: **15 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [Lesson 6: создание мер](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Создание ключевых показателей эффективности  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>toocreate InternetCurrentQuarterSalesPerformance ключевого показателя Эффективности  
  
1.  В конструкторе моделей hello щелкните hello **FactInternetSales** таблицы.  
  
2.  В сетке мер hello щелкните пустую ячейку.  
  
3.  В строке формул hello над таблицей hello введите hello следующую формулу: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Эта мера служит hello базовой мерой для ключевого показателя Эффективности hello.  
  
4.  Щелкните правой кнопкой мыши **InternetCurrentQuarterSalesPerformance** > **Создать ключевой показатель эффективности**.   
  
5.  В диалоговом окне ключевого индикатора производительности (KPI) hello в **целевой** выберите **абсолютное значение**, а затем введите **1.1**.  
  
7.  Введите в поле слева (низкий) ползунок hello **1**, а затем в правом (верхнем) ползунок hello введите **1.07**.  
  
8.  В **Выбор стиля значков**выберите hello ромб (красный), треугольник (желтый), круг (зеленый) значок типа.
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Расширяемый hello уведомление **описания** подпись под hello доступными стилями значков. Используйте для hello описания различных toomake элементы ключевого показателя Эффективности их идентификацию в клиентских приложениях.  
  
9. Нажмите кнопку **ОК** toocomplete hello ключевого показателя Эффективности.  
  
    В сетке мер hello, обратите внимание, далее toohello hello значок **InternetCurrentQuarterSalesPerformance** мер. Он указывает, что мера служит базовым значением для КПЭ.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>toocreate InternetCurrentQuarterMarginPerformance ключевого показателя Эффективности  
  
1.  В сетке мер hello hello **FactInternetSales** таблицы, щелкните пустую ячейку.  
  
2.  В строке формул hello над таблицей hello введите hello следующую формулу:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Щелкните правой кнопкой мыши **InternetCurrentQuarterMarginPerformance** > **Создать ключевой показатель эффективности**.  
  
4.  В диалоговом окне ключевого индикатора производительности (KPI) hello в **целевой** выберите **абсолютное значение**, а затем введите **1.25**.   
  
5.  В (hello левом нижнем) поле ползунка, слайдов, пока не отобразится поле hello **0,8**, и затем hello слайд правой поле ползунка (высокий), пока не отобразится поле hello **1.03**.  
  
6.  В **Выбор стиля значков**, выберите hello ромб (красный), треугольник (желтый), круг (зеленый) тип значка и нажмите кнопку **ОК**.  
  
## <a name="whats-next"></a>Что дальше?
[Занятие 8. Создание перспектив](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
