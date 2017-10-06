---
Заголовок: aaa» Azure Analysis Services tutorial занятие 3: пометить как таблицу дат | Документы Microsoft» Описание: описание как toomark даты таблицу в проект tutorial служб Azure Analysis Services hello. службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: н/д ms.workload: н/д ms.date: ms.author 06/01/2017 г.: owend
---
# <a name="lesson-3-mark-as-date-table"></a>Занятие 3. Обозначение таблицы дат

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

В занятии 2 "Получение данных" вы импортировали таблицу измерения DimDate. Хотя в вашей модели эта таблица имеет имя DimDate, она также может называться *таблицей дат*, так как содержит данные о датах и времени.  
  
Каждый раз при использовании функций логики операций со временем DAX (вы займетесь этим чуть позже при создании мер) нужно указывать такие свойства, как *Таблица дат* и уникальный идентификатор *Столбец даты* в ней.
  
На этом занятии пометить таблицы DimDate hello как hello *таблицу дат* и hello столбец даты (в таблице Date hello) как hello *столбец даты* (идентификатор).  

Прежде отметить столбец таблицы и дата даты hello это подходящий момент toodo немного housekeeping toomake проще toounderstand вашей модели. Обратите внимание, в таблицы DimDate hello столбец с именем **FullDateAlternateKey**. Этот столбец содержит по одной строке на каждый день каждого календарного года, добавляются в таблицу hello. Этот столбец часто используется в формулах мер и отчетах. Однако FullDateAlternateKey нельзя назвать уместным идентификатором для этого столбца. Переименование слишком**Дата**, сделав его проще tooidentify и включать в формулы. Когда это возможно, это toorename смысл объекты как таблицы и столбцы toomake их проще tooidentify в SSDT и клиентские приложения, такие как Power BI и Excel. 
  
Предполагаемое время toocomplete на этом занятии: **три минуты**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [Lesson 2: получение данных](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>toorename столбца FullDateAlternateKey hello

1.  В конструкторе моделей hello щелкните hello **DimDate** таблицы.

2.  Дважды щелкните заголовок hello для hello **FullDateAlternateKey** столбца, а затем переименуйте слишком**даты**.

  
### <a name="tooset-mark-as-date-table"></a>tooset пометить как таблицу дат  
  
1.  Выберите hello **даты** столбца и затем в hello **свойства** окна в разделе **тип данных**, убедитесь, что **даты** выбран.  
  
2.  Щелкните hello **таблицы** меню, нажмите кнопку **даты**, а затем нажмите кнопку **пометить как таблицу дат**.  
  
3.  В hello **пометить как таблицу дат** диалогового окна hello **даты** списка выберите hello **даты** столбец как уникальный идентификатор hello. Обычно он уже выбран по умолчанию. Нажмите кнопку **ОК**. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>Что дальше?
[Занятие 4. Создание связей](../tutorials/aas-lesson-4-create-relationships.md).
  
