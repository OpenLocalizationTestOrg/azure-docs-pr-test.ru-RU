---
Заголовок: aaa» Azure Analysis Services tutorial занятия 4: Создание связей | Документы Microsoft» Описание: описание, как связи toocreate в hello проекта tutorial служб Azure Analysis Services. службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-4-create-relationships"></a>Занятие 4. Создание связей

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

На этом занятии проверьте hello связи, которые были автоматически созданы во время импорта данных и добавить новые связи между различными таблицами. Связь — это соединение между двумя таблицами, которое определяет, каким образом должны соотноситься данные этих таблиц hello. Например таблица hello DimProduct и таблица DimProductSubcategory hello иметь связи, в зависимости от hello факт, что каждый продукт принадлежит подкатегории tooa. toolearn более, в разделе [связи](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Предполагаемое время toocomplete на этом занятии: **10 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятия 3: пометить как таблицу дат](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Просмотр существующих и добавление новых связей  
Во время импорта данных с помощью получения данных, полученный семь таблиц из базы данных AdventureWorksDW2014 hello. Как правило при импорте данных из реляционного источника существующие связи автоматически импортируются вместе с данными hello. Однако прежде чем продолжить создание модели, нужно убедиться, что эти связи между таблицами созданы правильно. В этом руководстве вы добавите три новых связи.  
  
#### <a name="tooreview-existing-relationships"></a>tooreview существующих связей  
  
1.  Нажмите кнопку hello **модель** меню > **представление модели** > **представление диаграммы**.  

    Hello конструктор моделей появится в представлении диаграммы — графическом формате отображения всех таблиц hello импортированные линиями. Hello линии между таблицами указывают hello связей, которые были автоматически созданы во время импорта данных hello.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Включите любое количество hello таблиц можно с помощью мини-карту элементов управления в hello правом нижнем углу конструктора моделей hello. Кроме того, можно также щелкнуть и перетащить расположения toodifferent таблиц, свести вместе или разместить их в определенном порядке. Перемещение таблиц не влияет на hello связи между таблицами hello. tooview все столбцы hello в определенной таблице щелкните и перетащите край таблицы tooexpand или уменьшить ее.  
  
2.  Нажмите кнопку hello сплошную линию между hello **DimCustomer** таблицы и hello **DimGeography** таблицы. Hello сплошная линия между этими двумя таблицами показывает, что связь активна, то есть, он используется по умолчанию при расчете DAX-формул.  
  
    Уведомление hello **GeographyKey** столбца в hello **DimCustomer** таблицы и hello **GeographyKey** столбца в hello **DimGeography** таблицы появились в поле. Эти столбцы используются в отношении hello. Hello свойства связи также отображаются в hello **свойства** окна.  
  
    > [!TIP]  
    > В дополнение к этому toousing Здравствуйте конструктора моделей в представлении диаграммы, можно также использовать hello управление связями диалогового окна поле tooshow hello связей между всеми таблицами в табличном формате. В обозревателе табличных моделей щелкните правой кнопкой мыши **Связи** > **Управление связями**.
  
3.  Проверьте hello следующие связи были созданы во время каждой из таблиц hello были импортированы из базы данных AdventureWorksDW hello:  
  
    |Активна|Таблица|Соответствующая таблица подстановки|  
    |----------|---------|------------------------|  
    |Да|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Да|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Да|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Да|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Да|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Если какие-либо связи hello отсутствуют, убедитесь, что модель включает следующие таблицы hello: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory DimProductSubcategory и FactInternetSales. Если таблицы из одного подключения к источнику данных, импортируются в hello отдельные раз, все связи между этими таблицами не создаются и должны быть созданы вручную.  

### <a name="take-a-closer-look"></a>Более подробный взгляд
В представлении диаграммы Обратите внимание, стрелки, звездочку и номер на линии hello, указывающие hello связи между таблицами.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

Hello стрелка показывает направление фильтрации hello. звездочка Hello показывает, что эта таблица будет hello стороне многие в количество элементов связи hello и hello один показывает, что эта таблица составляет hello одной стороны связи "hello". Если вам требуется tooedit связь. Например измените направление фильтрации hello отношение или количество элементов, дважды щелкните диалоговое окно Изменение связи hello tooopen в строки связь hello.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Эти функции предназначены для моделирования данных и находящиеся вне области видимости hello этого учебника. toolearn более, в разделе [двунаправленные кросс-фильтры для табличных моделей в службах Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

В некоторых случаях может потребоваться toocreate дополнительных связей между таблицами в вашей модели toosupport определенную бизнес-логику. В этом учебнике требуется toocreate три дополнительные связи между таблицами FactInternetSales hello и таблицы DimDate hello.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>tooadd новых связей между таблицами  
  
1.  В конструкторе моделей hello в hello **FactInternetSales** таблицы, нажмите и удерживайте на hello **OrderDate** столбца, а затем перетащите hello курсор toohello **даты** столбца в hello  **DimDate** таблицы, а затем отпустите.  

    Появится сплошная линия, показывающая создана активная связь между hello **OrderDate** столбца в hello **продажи через Интернет** таблицы и hello **даты** столбца в hello **Даты** таблицы. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > При создании связи, hello количества элементов и фильтр направлении между первичной таблицей hello и hello связанная таблица подстановки выбирается автоматически.  
  
2.  В hello **FactInternetSales** щелкните и удерживайте hello **DueDate** столбца, а затем перетащите hello курсор toohello **даты** столбца в hello **DimDate** таблицы, а затем отпустите.  
  
    Появится пунктирная линия, показывающая создана неактивная связь между hello **DueDate** столбца в hello **FactInternetSales** таблицы и hello **даты** столбца Hello **DimDate** таблицы. Можно использовать несколько связей между таблицами, но одновременно может быть активна только одна из них. Неактивные связи можно сделать агрегаты специальные active tooperform пользовательских выражений DAX.  
  
3.  Теперь создайте еще одну связь. В hello **FactInternetSales** щелкните и удерживайте hello **ShipDate** столбца, а затем перетащите hello курсор toohello **даты** столбца в hello **DimDate** таблицы, а затем отпустите.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Что дальше?
[Занятие 5. Создание вычисляемых столбцов](../tutorials/aas-lesson-5-create-calculated-columns.md).
  
  
  
