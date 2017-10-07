---
Заголовок: aaa» Azure Analysis Services tutorial дополнительного занятия: неоднородные иерархии | Документы Microsoft» Описание: описание, как toofix неоднородные иерархии в учебнике hello Azure Analysis Services.
службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Дополнительное занятие. Неоднородные иерархии

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

В этом дополнительном занятии вы устраните распространенную проблему, которая возникает при сведении иерархий, содержащих пустые значения (члены) на различных уровнях. Например, организация, где прямыми подчиненными высокопоставленного руководителя являются как руководители подразделений, так и не руководящие работники. Или географические иерархии, состоящие из комбинации страна+регион+город, где некоторые города не относятся к конкретному штату или конкретной провинции, например Вашингтон, округ Колумбия, или Ватикан. Если пустые элементы иерархии, его часто заканчиваются toodifferent или неоднородной, уровни.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Табличные модели на уровне совместимости hello 1400 имеют дополнительный **скрыть элементы** свойство для иерархии. Hello **по умолчанию** предполагается нет пустой членов на любом уровне. Hello **скрыть пустые элементы** позволяет исключить пустые элементы из иерархии hello при добавлении tooa сводной таблице или отчете.  
  
Предполагаемое время toocomplete на этом занятии: **20 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Это дополнительное занятие входит в учебник по табличному моделированию. Перед выполнением задачи hello в этом дополнительном занятии, необходимо завершить все предыдущие занятия или иметь завершенный проект образце модели Интернет-продаж Adventure Works. 

При создании проекта Интернет-продаж AW hello hello учебника по модели не еще содержит любые данные или неровными иерархиями. toocomplete этого дополнительного занятия необходимо определить toocreate Здравствуйте проблему, добавив некоторые дополнительные таблицы, создавать связи, вычисляемые столбцы, меры и новую иерархию организации. Эта часть займет около 15 минут. После этого вы получаете toosolve его через несколько минут.  

## <a name="add-tables-and-objects"></a>Добавление таблиц и объектов
  
### <a name="tooadd-new-tables-tooyour-model"></a>tooadd новой таблицы tooyour модели
  
1.  В обозревателе табличных моделей разверните пункт **Источники данных**, щелкните правой кнопкой мыши подключение и выберите элемент **Импортировать новые таблицы**.
  
2.  В навигаторе выберите **DimEmployee** и **FactResellerSales**, а затем нажмите кнопку **ОК**.

3.  В редакторе запросов щелкните элемент **Импорт**.

4.  Создайте ниже hello [связи](../tutorials/aas-lesson-4-create-relationships.md):

    | Таблица 1           | столбец       | Направление фильтра   | Таблица 2     | столбец      | Активна |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | значение по умолчанию            | DimDate     | Дата        | Да    |
    | FactResellerSales | DueDate      | значение по умолчанию            | DimDate     | Дата        | Нет     |
    | FactResellerSales | ShipDateKey  | значение по умолчанию            | DimDate     | Дата        | Нет     |
    | FactResellerSales | ProductKey   | значение по умолчанию            | DimProduct  | ProductKey  | Да    |
    | FactResellerSales | EmployeeKey  | tooBoth таблиц | DimEmployee | EmployeeKey | Да    |

5. В hello **DimEmployee** таблице, создайте следующие hello [вычисляемых столбцов](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Путь** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  В hello **DimEmployee** , куда вводится [иерархии](../tutorials/aas-lesson-9-create-hierarchies.md) с именем **организации**. Добавьте следующие столбцы в порядке hello: **Level1**, **Level2**, **Level3**, **Level4**, **уровень 5**.

7.  В hello **FactResellerSales** таблице, создайте следующие hello [мер](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Используйте [анализ в Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel и автоматически создать сводную таблицу.

9.  В **полей сводной таблицы**, добавить hello **организации** иерархии из hello **DimEmployee** таблице слишком**строк**и hello **ResellerTotalSales** меру из hello **FactResellerSales** таблице слишком**значения**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Как видно в сводной таблице hello hello иерархии отображаются строки, без выравнивания. Имеется множество строк с пустыми членами.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>toofix hello неоднородные иерархии, присвоив свойству hello скрытие членов

1.  В **обозревателе табличных моделей** разверните пункт **Таблицы** > **DimEmployee** > **Иерархии** > **Organization**.

2.  В области **Свойства** > **Скрыть члены** выберите **Скрыть пустые члены**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Обратно в Excel обновите hello сводной таблицы. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Теперь все выглядит гораздо лучше!

## <a name="see-also"></a>См. также   
[Занятие 9. Создание иерархий](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Дополнительное занятие. Динамическая безопасность](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Дополнительное занятие. Строки детализации](../tutorials/aas-supplemental-lesson-detail-rows.md)  