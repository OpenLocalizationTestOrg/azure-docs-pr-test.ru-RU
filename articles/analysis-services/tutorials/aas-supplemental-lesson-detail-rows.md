---
Заголовок: aaa» Azure Analysis Services tutorial дополнительного занятия: строки детализации | Документы Microsoft» Описание: описание, как toocreate a выражение строки детализации в hello Azure Analysis Services tutorial.
службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>Дополнительное занятие. Строки детализации

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

В этом дополнительном занятии используется hello toodefine редактор DAX пользовательское выражение строки детализации. Выражение строки детализации — это свойство измерения, предоставляя конечным пользователям Дополнительные сведения о результатах hello статистическую обработку меры. 
  
Предполагаемое время toocomplete на этом занятии: **10 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Это дополнительное занятие входит в учебник по табличному моделированию. Перед выполнением задачи hello в этом дополнительном занятии, необходимо завершить все предыдущие занятия или иметь завершенный проект образце модели Интернет-продаж Adventure Works.  
  
## <a name="what-do-we-need-toosolve"></a>Что делать нам нужно toosolve?
Давайте взглянем на hello сведений о нашей меры InternetTotalSales, прежде чем добавлять выражение строки детализации.

1.  В SSDT выберите hello **модель** меню > **анализ в Excel** tooopen Excel и создайте пустую сводную таблицу.
  
2.  В **полей сводной таблицы**, добавить hello **InternetTotalSales** мер из таблицы FactInternetSales hello слишком**значения**, **CalendarYear**из hello DimDate таблице слишком**столбцы**, и **EnglishCountryRegionName** слишком**строк**. Теперь наши сводной таблицы дает нам сводных результатов из мер InternetTotalSales hello, регионы и года. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Hello сводной таблицы дважды щелкните сводное значение для года, а имя области. Здесь мы дважды щелкнули значение hello Австралия и hello 2014 года. Открывается новый лист с данными, но это не те данные, которые нам требуются.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
Что мы хотели бы toosee здесь является таблицей, содержащей столбцы и строки данных, которые влияют на результат toohello статистическую обработку меры InternetTotalSales. toodo, можно добавить выражение строки детализации как свойство измерения hello.

## <a name="add-a-detail-rows-expression"></a>Добавление выражения строк детализации

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate выражение строк детализации 
  
1. В SSDT, в сетке мер таблицы FactInternetSales hello, щелкните hello **InternetTotalSales** мер. 

2. В **свойства** > **выражение строки детализации**, нажмите кнопку hello редактор кнопка tooopen hello редактор DAX.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. В редакторе DAX введите hello, следующее выражение:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Это выражение указывает имена столбцов и мер из таблицы FactInternetSales hello и связанные таблицы результатов при двойном щелчке результат статистической обработки в сводной таблице или отчете.

4. В Excel удалить лист hello, созданной на шаге 3, а затем дважды щелкните это статистическое выражение. На этот раз со свойством выражение строки детализации, определенные для меры hello, новый лист открывается с гораздо более полезными данными.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Разверните модель заново.

  
## <a name="see-also"></a>См. также  
[Функция SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Дополнительное занятие. Динамическая безопасность](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Дополнительное занятие. Неоднородные иерархии](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
