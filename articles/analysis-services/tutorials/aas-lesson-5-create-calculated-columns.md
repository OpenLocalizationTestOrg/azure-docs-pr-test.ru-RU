---
Заголовок: aaa» Azure Analysis Services tutorial занятие 5: Создание вычисляемых столбцов | Документы Microsoft» Описание: описание как toocreate вычисляемых столбцов в проект tutorial служб Azure Analysis Services hello. службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: н/д ms.workload: н/д ms.date: ms.author 06/01/2017 г.: owend
---
# <a name="lesson-5-create-calculated-columns"></a>Занятие 5. Создание вычисляемых столбцов

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

В этом занятии вы создадите в модели данные, добавив вычисляемые столбцы. Можно создать вычисляемые столбцы (как пользовательские столбцы) при использовании получение данных, с помощью hello редактора запросов или более поздней версии в конструкторе like hello модели выполните здесь. toolearn более, в разделе [вычисляемых столбцов](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Вы создадите пять вычисляемых столбцов в трех разных таблицах. шаги Hello немного отличаются для каждой задачи, показывающей, существует несколько способов toocreate столбцы, переименуйте их и разместить их в различных местах в таблице.  

Кроме того, на этом занятии вы впервые воспользуетесь выражениями анализа данных (DAX). DAX — это специальный язык, позволяющий создавать сложные настраиваемые выражения формул для табличных моделей. В этом учебнике используется DAX toocreate вычисляемые столбцы, меры и фильтры. toolearn более, в разделе [DAX в табличных моделях](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Предполагаемое время toocomplete на этом занятии: **15 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятия 4: Создание связей](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Создание вычисляемых столбцов  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Создание вычисляемого столбца MonthCalendar таблицы DimDate hello  
  
1.  Нажмите кнопку hello **модель** меню > **представление модели** > **представление данных**.  
  
    Вычисляемые столбцы могут создаваться только с помощью конструктора моделей hello в представлении данных.  
  
2.  В конструкторе моделей hello щелкните hello **DimDate** таблицу (вкладку).  
  
3.  Щелкните правой кнопкой мыши hello **CalendarQuarter** заголовок столбца, а затем щелкните **вставить столбец**.  
  
    Новый столбец с именем **вычисляемый столбец 1** — toohello вставленный слева от hello **Календарный квартал** столбца.  
  
4.  В hello формул над таблицей hello, введите следующую формулу DAX hello: Автозаполнение помогает ввести hello полные имена столбцов и таблиц и списков hello функций, доступных.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Для всех строк hello в вычисляемом столбце hello будут заполнены значениями. Если прокрутите через таблицу hello видно, что строки могут иметь разные значения для этого столбца на основе данных hello в каждой строке.    
  
5.  Переименовать этот столбец слишком**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
вычисляемый столбец MonthCalendar Hello содержит сортируемое имя для месяца.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Создание вычисляемого столбца DayOfWeek таблицы DimDate hello  
  
1.  С hello **DimDate** активной таблице, нажмите кнопку hello **столбца** меню, а затем нажмите **добавить столбец**.  
  
2.  В строке формул hello введите следующую формулу hello:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Завершив построение формулы hello, нажмите клавишу ВВОД. toohello правого края hello таблицу добавляется новый столбец Hello.  
  
3.  Переименовать столбец hello слишком**DayOfWeek**.  
  
4.  Щелкните заголовок столбца hello, а затем перетащите столбец hello между hello **EnglishDayNameOfWeek** столбец и hello **DayNumberOfMonth** столбца.  
  
    > [!TIP]  
    > Перемещение столбцов в таблице позволяет упростить toonavigate.  
  
вычисляемый столбец DayOfWeek Hello содержит сортируемое имя дня недели hello.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Создание вычисляемого столбца ProductSubcategoryName в таблице DimProduct hello  
  
  
1.  В hello **DimProduct** таблица, прокрутите toohello правому краю таблицы hello. Обратите внимание hello самый правый столбец называется **добавить столбец** (курсивом), щелкните заголовок столбца hello.  
  
2.  В строке формул hello введите следующую формулу hello:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Переименовать столбец hello слишком**ProductSubcategoryName**.  
  
вычисляемый столбец Hello ProductSubcategoryName — используется toocreate иерархии в таблице DimProduct hello, которое включает данные из столбца EnglishProductSubcategoryName hello в таблице DimProductSubcategory hello. Иерархии не могут охватывать более одной таблицы. Вы создадите иерархии позднее в занятии 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Создание вычисляемого столбца ProductCategoryName в таблице DimProduct hello  
  
1.  С hello **DimProduct** активной таблице, нажмите кнопку hello **столбца** меню, а затем нажмите **добавить столбец**.  
  
2.  В строке формул hello введите следующую формулу hello:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Переименовать столбец hello слишком**ProductCategoryName**.  
  
вычисляемый столбец ProductCategoryName Hello — используется toocreate иерархии в таблице DimProduct hello, которое включает данные из столбца EnglishProductCategoryName hello в таблице DimProductCategory hello. Иерархии не могут охватывать более одной таблицы.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Создание вычисляемого столбца поля таблицы FactInternetSales hello  
  
1.  Выберите в конструкторе моделей hello hello **FactInternetSales** таблицы.  
  
2.  Создать новый вычисляемый столбец между hello **SalesAmount** столбец и hello **TaxAmt** столбца.  
  
3.  В строке формул hello введите следующую формулу hello:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Переименовать столбец hello слишком**поля**.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    вычисляемый столбец Hello поля — используется tooanalyze прибыли для каждой продажи.  
  
## <a name="whats-next"></a>Что дальше?
[Занятие 6. Создание мер](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
