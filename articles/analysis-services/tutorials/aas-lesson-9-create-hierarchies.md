---
Заголовок: aaa «занятие учебника Azure Analysis Services 9: создание иерархий | Документы Microsoft» Описание: службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-9-create-hierarchies"></a>Занятие 9. Создание иерархий

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

На этом занятии мы создадим иерархии. Иерархии — это группы столбцов, упорядоченных по уровням. Например, иерархия "География" может иметь подуровни для страны, области, района и города. Иерархии могут отображаться отдельно от других столбцов в списке полей отчетов клиентского приложения, что упрощает для клиентов toonavigate пользователей и включения в отчет. toolearn более, в разделе [иерархий](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
toocreate иерархии, используйте конструктор моделей hello в *представление диаграммы*. Создание иерархий и управление ими не поддерживается в представлении данных.  
  
Предполагаемое время toocomplete на этом занятии: **20 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 8: Создание перспектив](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Создание иерархий  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>toocreate иерархию категорий в таблице DimProduct hello  
  
1.  В конструкторе моделей hello (представление диаграммы), щелкните правой кнопкой мыши hello **DimProduct** таблицы > **создать иерархию**. Появится новая иерархия hello нижней части окна таблицы hello. Переименовать иерархию hello **категории**.  
  
2.  Щелкните и перетащите hello **ProductCategoryName** toohello столбца нового **категории** иерархии.  
  
3.  В hello **категории** иерархии, щелкните правой кнопкой мыши hello **ProductCategoryName** > **переименование**, а затем введите **категории**.  
  
    > [!NOTE]  
    > Переименование столбца в иерархии не переименовать этот столбец в таблице hello. Столбец в иерархии является просто представлением hello столбца в таблице hello.  
  
4.  Щелкните и перетащите hello **ProductSubcategoryName** toohello столбца **категории** иерархии. Назовите его **Subcategory**. 
  
5.  Щелкните правой кнопкой мыши hello **ModelName** столбца > **добавить toohierarchy**и выберите **категории**. Назовите его **Model**.

6.  Наконец, добавьте **EnglishProductName** toohello иерархию категорий. Назовите его **Product**.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>toocreate иерархий в таблицы DimDate hello  
  
1.  В hello **DimDate** таблице, создайте иерархию с именем **календаря**.  
  
3.  Добавьте следующие столбцы в порядке hello:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  В hello **DimDate** , куда вводится **финансовом** иерархии. Следующие hello следующие столбцы в определенном порядке.  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Наконец, в hello **DimDate** , куда вводится **ProductionCalendar** иерархии. Следующие hello следующие столбцы в определенном порядке.  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Что дальше?
[Занятие 10. Создание разделов](../tutorials/aas-lesson-10-create-partitions.md). 
  
  
