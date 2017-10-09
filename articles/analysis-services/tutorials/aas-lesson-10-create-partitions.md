---
Заголовок: aaa «занятие учебника Azure Analysis Services 10: Создание разделов | Документы Microsoft» Описание: описание как toocreate секции в проект tutorial служб Azure Analysis Services hello. службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-10-create-partitions"></a>Занятие 10. Создание секций

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

На этом занятии создайте таблицу FactInternetSales hello toodivide секций на более мелкие логические части, которые могут быть обработан (Обновить) независимо от других секций. По умолчанию каждая таблица, включить в модель имеет одну секцию, которая включает все таблицы hello столбцов и строк. Для таблицы FactInternetSales hello мы хотим toodivide hello данные по годам; одну секцию для каждой таблицы hello пять лет. После этого каждую секцию можно будет обрабатывать отдельно. toolearn более, в разделе [секций](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular). 
  
Предполагаемое время toocomplete на этом занятии: **15 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 9: создание иерархий](../tutorials/aas-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Создание секций  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>toocreate секций таблицы FactInternetSales hello  
  
1.  В обозревателе табличных моделей разверните пункт **Таблицы** и щелкните правой кнопкой мыши **FactInternetSales** > **Секции**.  
  
2.  Щелкните в диспетчере секций **копирования**, измените имя hello слишком**FactInternetSales2010**.
  
    Так как вы хотите tooinclude секции hello только те строки, в течение определенного периода, за год hello 2010, необходимо изменить выражение запроса hello.
  
4.  Нажмите кнопку **разработки** tooopen редактор запросов, а затем нажмите кнопку hello **FactInternetSales2010** запроса.

5.  В режиме предварительного просмотра, нажмите кнопку hello стрелки вниз в hello **OrderDate** заголовок столбца, а затем щелкните **фильтров даты и времени** > **между**.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  В диалоговом окне фильтр строк hello в **отображает строки, где: OrderDate**, оставьте **после или равно**и введите в поля «Дата» hello **1/1/2010**. Оставьте hello **и** оператор выбран, выберите **перед**, введите в поля «Дата» hello **1/1/2011**и нажмите кнопку **ОК**.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    В разделе "Примененные шаги" редактора запросов появится еще один шаг с именем "Строки с примененным фильтром". Этот фильтр рекомендуется только даты заказа tooselect 2010.

8.  Щелкните **Импорт**.

    В диспетчере секций Обратите внимание запросов hello, теперь выражение имеет дополнительное предложение фильтрации строк.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    Эта инструкция указывает, что эта секция должна включать только данные hello в этих строках, где hello OrderDate — в hello 2010 календарного года, как указано в предложении hello отфильтрованные строки.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>toocreate секции для hello 2011 года  
  
1.  В списке секций hello выберите hello **FactInternetSales2010** секции был создан и нажмите кнопку **копирования**.  Изменить имя секции hello слишком**FactInternetSales2011**. 

    Toouse редактор запросов toocreate предложение отфильтрованные строки не обязательно. Так как вы создали копию запроса hello 2010, все, что нужно toodo — убедиться в небольшое изменение в запросе hello для 2011.
  
2.  В **выражение запроса**, в определенном порядке для этой секции tooinclude только те строки hello 2011 года, замените лет hello в предложении фильтрации строк hello с **2011** и **2012**соответственно, например:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>разделы toocreate для 2012, 2013 и 2014.  
  
- Выполните действия предыдущего hello, создания разделов для 2012, 2013 и 2014, изменение годы hello в hello фильтрации строк предложения tooinclude только строк за этот год. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Удалить раздел FactInternetSales hello
Теперь, когда у вас есть секции для каждого года, можно удалить раздел FactInternetSales hello; Предотвращение перекрытия при выборе всех процесс при обработке секций.

#### <a name="toodelete-hello-factinternetsales-partition"></a>hello toodelete FactInternetSales секции
-  Щелкните раздел FactInternetSales hello и нажмите кнопку **удалить**.



## <a name="process-partitions"></a>Обработка секций  
Обратите внимание, в диспетчере секций hello **последней обработки** столбец для каждого из новых секций hello, вы создали показаны эти разделы никогда не будут обработаны. При создании секций, следует запустить эти разделы обработки секций или процесса операции toorefresh hello данные таблицы.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>FactInternetSales секций tooprocess hello  
  
1.  Нажмите кнопку **ОК** tooclose диспетчер секций.  
  
2.  Нажмите кнопку hello **FactInternetSales** , а затем нажмите кнопку hello **модели** меню > **процесс** > **Обработка секций**.  
  
3.  В диалоговом окне Обработка секций hello, проверьте **режим** задано слишком**обработка по умолчанию**.  
  
4.  Установите флажок hello в hello **процесс** столбец для каждого из пяти hello секции был создан, а затем щелкните **ОК**.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    При появлении запроса учетных данных олицетворения, введите имя пользователя Windows hello и пароль, которые указаны в занятии 2.  
  
    Hello **обработки данных** диалогового окна и отобразит сведения обработки для каждой секции. Обратите внимание, что для каждой секции передается разное количество строк. Каждая секция включает только те строки, для hello года, указанного в предложение WHERE в инструкции SQL hello hello. После завершения обработки пойти дальше и закройте диалоговое окно приветствия обработки данных.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Что дальше?
Последовательно выберите toohello занятию: [занятие 11: Создание ролей](../tutorials/aas-lesson-11-create-roles.md). 
