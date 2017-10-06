---
Заголовок: aaa «занятие учебника Azure Analysis Services 6: создание мер | Документы Microsoft» Описание: описание как toocreate меры в проект tutorial служб Azure Analysis Services hello. службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: н/д ms.workload: н/д ms.date: ms.author 06/01/2017 г.: owend
---
# <a name="lesson-6-create-measures"></a>Занятие 6. Создание мер

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

На этом занятии создается toobe меры, включенные в модель. Аналогичные toohello вычисляемые столбцы, созданные, мера представляет собой вычисление, созданное с помощью формулы DAX. Но в отличие от вычисляемых столбцов меры вычисляются на основе выбранного пользователем *фильтра*. Например, определенного столбца или среза toohello метки строк поле добавлено в сводной таблице. Значение для каждой ячейки в фильтре hello вычисляется по мере применения hello. Меры — это мощные гибкие вычисления, которые должны tooinclude в почти все динамические вычисления табличных моделей tooperform с числовыми данными. toolearn более, в разделе [меры](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).
  
меры toocreate использовать hello *сетку мер*. По умолчанию в каждой таблице есть пустая сетка мер. Но меры обычно требуется создавать не для всех таблиц. Hello сетка мер появляется внизу таблицы в конструкторе моделей hello в представлении данных. toohide или Показывать сетку мер hello для таблицы, щелкните hello **таблицы** меню, а затем нажмите **Показать сетку мер**.  
  
Можно создать меру, щелкнув пустую ячейку в сетке мер hello и введя DAX-формулы в строке формул hello. Если щелкните toocomplete hello ввод формулы, hello мер, то появится в ячейке hello. Можно также создать меры, используя стандартную статистическую функцию, щелкнув столбец и выбрав hello кнопки автосуммирования (**∑**) на панели инструментов hello. Меры, созданные с помощью функции автосуммирования hello отображается в ячейке сетки мер hello непосредственно под столбцом hello, но могут быть перемещены.  
  
На этом занятии вы создаете меры обоих ввода формулы DAX в строке формул hello, а также с помощью функции автосуммирования hello.  
  
Предполагаемое время toocomplete на этом занятии: **30 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятия 5: Создание вычисляемых столбцов](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Создание мер  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>toocreate DaysCurrentQuarterToDate мера в таблице DimDate hello  
  
1.  В конструкторе моделей hello щелкните hello **DimDate** таблицы.  
  
2.  В сетке мер hello щелкните пустую ячейку в левом верхнем hello.  
  
3.  В строке формул hello введите следующую формулу hello:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Обратите внимание hello верхняя левая ячейка теперь содержит имя меры, **DaysCurrentQuarterToDate**, а затем результат hello **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    В отличие от вычисляемых столбцов причем формулы для мер можно ввести имя меры hello, за которым следует двоеточие, следуют hello выражении формулы.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>toocreate DaysInCurrentQuarter мера в таблице DimDate hello  
  
1.  С hello **DimDate** таблицы все еще активна в конструкторе моделей hello в сетку мер hello, щелкните пустую ячейку hello ниже созданной мерой hello.  
  
2.  В строке формул hello введите следующую формулу hello:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Во время создания пропорции сравнения между одним неполным периодом и hello предыдущего периода. Формула Hello необходимо вычислить долю hello hello прошедшего времени периода и сравнивают его toohello же пропорция в hello предыдущего периода. В этом случае [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] дает hello соотношение времени текущего периода в hello.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>toocreate InternetDistinctCountSalesOrder мера в таблице FactInternetSales hello  
  
1.  Нажмите кнопку hello **FactInternetSales** таблицы.   
  
2.  Нажмите кнопку hello **SalesOrderNumber** заголовок столбца.  
  
3.  На панели инструментов hello, нажмите кнопку Далее toohello стрелка вниз hello автосуммирования (**∑**) и затем выберите **DistinctCount**.  
  
    Hello автосуммирования автоматически создаст меру для выбранного столбца hello, используя стандартную статистическую формулу DistinctCount hello.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  В сетке мер hello, щелкните новую меру hello, а затем в hello **свойства** окна в **имя меры**, переименуйте меру hello слишком**InternetDistinctCountSalesOrder**. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>toocreate дополнительных мер в таблицу FactInternetSales hello  
  
1.  С помощью функции автосуммирования hello, создайте и назовите следующие меры hello.  

    |столбец|Имя меры|Автосумма (∑)|Формула|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Sum|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Sum|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Sum|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Sum|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Sum|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Sum|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Sum|=SUM([Freight])|  
  
2.  Щелкнув создайте пустую ячейку в сетке мер hello и с помощью строки формул hello, и hello следующее имя меры в порядке:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Меры, созданные для таблицы FactInternetSales hello может быть используется tooanalyze критических финансовых данных, таких как продажи, издержки и маржа прибыли для элементов, которые определены по hello пользователя выбранного фильтра.  
  
## <a name="whats-next"></a>Что дальше?
[Занятие 7. Создание ключевых показателей эффективности](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  

  
