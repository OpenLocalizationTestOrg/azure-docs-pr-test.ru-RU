---
Заголовок: aaa» Azure Analysis Services учебника lesson 2: получение данных | Документы Microsoft» Описание: описание, как tooget и импорта данных в hello проекта tutorial служб Azure Analysis Services. службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: н/д ms.workload: н/д ms.date: ms.author 06/01/2017 г.: owend
---

# <a name="lesson-2-get-data"></a>Занятие 2. Получение данных

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

На этом занятии использовать получение данных в SSDT tooconnect toohello AdventureWorksDW2014 образца базы данных, выберите данные, просмотр и фильтрация и затем импортировать в рабочую область модели.  
  
С помощью функции получения данных можно импортировать данные из самых разнообразных источников: базы данных SQL Azure, Oracle, Sybase, канала OData, Teradata, файлов и других. Данные также можно запросить с помощью выражения формулы Power Query M.
  
Предполагаемое время toocomplete на этом занятии: **10 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятия 1: Создание нового проекта табличной модели](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Создание подключения  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>toocreate toohello AdventureWorksDW2014 подключения базы данных  
  
1.  В обозревателе табличных моделей щелкните правой кнопкой мыши **Источники данных** > **Импорт из источника данных**.  
  
    Получение данных, который поможет подключения источника данных tooa будет запущен. Если вы не видите обозревателе табличной модели в **обозревателе решений**, дважды щелкните **Model.bim** tooopen hello модели в конструкторе hello. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  В области функции получения данных щелкните **База данных** > **База данных SQL Server** > **Подключить**.  
  
3.  В hello **базы данных SQL Server** диалоговое окно, в **сервера**, введите имя hello hello сервера, где установлен hello AdventureWorksDW2014 базы данных и нажмите кнопку **Connect**.  

4.  При появлении запроса учетных данных tooenter, необходимо иметь учетные данные hello toospecify, службы Analysis Services используют источник данных tooconnect toohello при импорте и обработке данных. В области **Режим олицетворения** выберите **Олицетворить учетную запись**, а затем введите учетные данные и нажмите кнопку **Подключить**. Рекомендуется использовать учетную запись, где hello срок действия пароля не ограничен.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > Использование учетной записи пользователя Windows и пароль обеспечивает наиболее безопасный метод подключения источника данных tooa hello.
  
5.  Выберите в навигаторе hello **AdventureWorksDW2014** базы данных, а затем нажмите кнопку **ОК**. При этом создается подключение hello toohello к базе данных. 
  
6.  Выберите в навигаторе Здравствуйте, флажок для hello следующие таблицы: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, и **FactInternetSales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
После нажатия кнопки "ОК" откроется редактор запросов. В следующем разделе hello следует выбрать только те данные hello, которые вы хотите tooimport.

  
## <a name="filter-hello-table-data"></a>Фильтрация данных таблицы hello  
Таблицы в образце базы данных hello AdventureWorksDW2014 имеют данных, не требуется tooinclude в модели. Если это возможно, требуется toofilter места в памяти toosave ненужные данные, используемые моделью hello. Вам отфильтровать hello столбцы из таблиц, поэтому их не импорта в базу данных модели hello hello база данных рабочей области, или после его развертывания. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>данные таблицы hello toofilter перед импортом  
  
1.  В редакторе запросов выберите hello **DimCustomer** таблицы. Откроется представление таблицы DimCustomer hello в источник данных hello (AdventureWorksDWQ2014 образца базы данных). 
  
2.  Выполните множественный выбор (CTRL+щелчок мышью) элементов **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, а затем щелкните правой кнопкой мыши и выберите пункт **Удалить столбцы**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Поскольку hello значения для этих столбцов не применимо tooInternet анализа продаж, нет нет необходимости tooimport эти столбцы. После удаления ненужных столбцов модель становится компактнее и эффективнее.  
  
4.  Отфильтруйте оставшиеся таблицы, удалив следующие столбцы в каждой таблице hello hello:  
    
    **DimDate**
    
      |столбец|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |столбец|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |столбец|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |столбец|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |столбец|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |столбец|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Импорт данных hello выбранных таблиц и столбцов  
Предварительного просмотра и фильтрации ненужных данных, можно импортировать rest hello hello данных, которые требуется. Hello мастер импортирует данные таблицы hello вместе со всеми связями между таблицами. Новые таблицы и столбцы создаются в модели hello и не импортируется отфильтрованные ранее данные.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>tooimport hello выбранных таблиц и столбцов данных  
  
1.  Просмотрите выбранные параметры. Если все настроено правильно, нажмите кнопку **Импорт**. диалоговое окно обработки данных Hello показывает состояние hello данные, импортированные из вашего источника данных в базу данных рабочей области.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Нажмите кнопку **Закрыть**  

  
## <a name="save-your-model-project"></a>Сохранение проекта модели  
Очень важно toofrequently сохранять проект модели.  
  
#### <a name="toosave-hello-model-project"></a>проект модели toosave hello  
  
-   Щелкните **Файл** > **Сохранить все**.  
  
## <a name="whats-next"></a>Что дальше?
[Занятие 3. Обозначение таблицы дат](../tutorials/aas-lesson-3-mark-as-date-table.md).

  
  
