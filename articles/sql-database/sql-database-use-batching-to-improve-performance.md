---
title: "Пакетная обработка производительность приложений баз данных SQL Azure tooimprove toouse aaaHow"
description: "Hello раздел предоставляет свидетельство, пакетная обработка операций базы данных значительно imroves hello скорости и масштабируемости приложений базы данных SQL Azure. Несмотря на то, что эти методы пакетной обработки работать для любой базы данных SQL Server, hello hello статьи занимается Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Как toouse пакетной обработки tooimprove производительность приложения базы данных SQL
Пакетная обработка операций tooAzure базы данных SQL значительно повышает hello производительности и масштабируемости приложений. В порядке toounderstand hello преимуществ hello первой части этой статьи рассматриваются некоторые образцы результатов теста, которые сравнивают tooa последовательные и пакетные запросы базы данных SQL. Hello оставшейся части статьи hello показаны методы hello, сценарии и рекомендации toohelp toouse успешно пакетной обработки в приложениях Azure.

## <a name="why-is-batching-important-for-sql-database"></a>Почему пакетная обработка так важна при работе с базой данных SQL
Пакетная обработка вызовов tooa удаленной службе является известной стратегией для повышения производительности и масштабируемости. Предусмотрены фиксированные обработки затраты tooany взаимодействия с удаленной службой, например сериализации и десериализации передача по сети. Упаковка нескольких отдельных транзакций в один пакет позволяет сократить эти затраты.

В этом документе мы хотим tooexamine различные стратегии пакетной обработки базы данных SQL и сценариев. Хотя эти стратегии также важны для локальных приложений, использующих SQL Server, существует несколько причин для выделения hello использованию пакетной обработки для базы данных SQL:

* Потенциально большая задержка в сети в имеется доступ к базе данных SQL, особенно в том случае, если доступ к базе данных SQL из внешней hello одного центра обработки данных Microsoft Azure.
* Hello многопользовательских характеристики базы данных SQL означает, что hello эффективность hello данных доступ к toohello соотносится уровень масштабируемости hello базы данных. База данных SQL необходимо предотвратить монополизации базы данных ресурсов toohello ущерб другим клиентам любого одного клиента или пользователя. В ответ toousage ресурсов сверх стандартных квот база данных SQL может уменьшить пропускную способность или реагировать в форме исключений регулирования. Эффективные методы, такие как использование пакетирования, включите вы toodo больше работы в базе данных SQL до достижения этих ограничений. 
* Пакетная обработка также эффективна для архитектур, использующих несколько баз данных (сегментирование). Hello эффективность взаимодействия с каждой единицы базы данных по-прежнему является ключевым фактором масштабируемости. 

Одним из hello преимущества использования базы данных SQL является отсутствие необходимости toomanage hello серверов, hello базы данных. Однако эта управляемая инфраструктура также означает наличие toothink по-разному об оптимизации базы данных. Больше не можно найти tooimprove hello инфраструктуры базы данных оборудования или сети. Этими средами управляет Microsoft Azure. Hello главной области, которые можно контролировать — взаимодействие приложения с базой данных SQL. Пакетная обработка выступает одним из методов такой оптимизации. 

Первая часть Hello бумаги hello анализирует различные методы пакетной обработки для приложений .NET, использующих базу данных SQL. последние два раздела Hello содержат пакетной обработки инструкции и сценарии.

## <a name="batching-strategies"></a>Стратегии пакетной обработки
### <a name="note-about-timing-results-in-this-topic"></a>Примечание о результатах измерения времени в этом разделе
> [!NOTE]
> Результаты не являются тесты, но предназначены tooshow **относительную производительность**. Временные показатели основаны на среднем значении результата выполнения минимум 10 тестов. Операции представляют собой вставки в пустую таблицу. Эти тесты были измеряемые предварительной версии 12, и они могут не соответствует toothroughput, могут возникнуть в версии 12 базы данных с помощью нового hello [уровней служб](sql-database-service-tiers.md). относительное поощрение Hello hello метода пакетной обработки должна быть одинаковой.
> 
> 

### <a name="transactions"></a>Транзакции
Кажется странным toobegin рассмотрение пакетной обработки с обсуждения транзакций. Но hello использование клиентских транзакций слабая пакетирования влияет серверные и улучшает производительность. И транзакции можно добавлять только несколько строк кода, поэтому они обеспечивают быстрый способ tooimprove производительности последовательных операций.

Рассмотрим следующий код C#, который содержит последовательность вставки hello и обновления для простой таблицы.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

Привет, выполнив кода ADO.NET последовательно выполняет эти операции.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Здравствуйте, лучшим способом toooptimize этот код является tooimplement некоторую форму клиентской пакетной обработки этих вызовов. Но есть простой способ tooincrease hello производительность этот код просто обернуть последовательность вызовов hello в транзакции. Вот hello того же кода, использующего транзакцию.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

На самом деле, транзакции используются в обоих этих примерах. В первом примере hello каждый отдельный вызов — это неявная транзакция. В втором примере hello в явную транзакцию включаются все вызовы hello. В соответствии с документацией hello для hello [журнала транзакций с упреждающей записью](https://msdn.microsoft.com/library/ms186259.aspx), записей журнала, передан toohello диск при фиксации транзакции hello. Таким образом, включая больше вызовов в транзакцию, hello записи журнала транзакций toohello можно отложить до hello транзакция фиксируется. В результате включается пакетной обработки для журнала транзакций hello записи toohello сервера.

Hello в следующей таблице показаны некоторые результаты тестирования ad hoc. выполнить тесты Hello приветствия же последовательные вставляет с и без транзакции. Для разнообразия hello первый набор тестов удаленно запускался с ноутбука toohello базы данных в Microsoft Azure. Hello второй набор тестов запускался из облачной службы и базы данных, которые размещались в hello же центре обработки данных Microsoft Azure (Запад США). Hello следующей таблице показаны hello продолжительность в миллисекундах последовательных вставок с и без транзакции.

**В локальной среде tooAzure**:

| Операции | Без транзакций (мс) | С транзакциями (мс) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12 662 |10 395 |
| 1000 |128 852 |102 917 |

**Azure tooAzure (одного центра обработки данных)**:

| Операции | Без транзакций (мс) | С транзакциями (мс) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21 479 |2756 |

> [!NOTE]
> Результаты не являются измерениями производительности. В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).
> 
> 

На основе hello предыдущих результатов теста, фактически заключение одной операции в транзакции снижает производительность. Однако по мере увеличения hello количества операций в рамках одной транзакции улучшение производительности hello становится более заметным. Hello разницы в производительности также является наиболее заметно, когда все операции выполняются в центре обработки данных Microsoft Azure hello. Hello Повышенная задержка при использовании базы данных SQL из центра обработки данных Microsoft Azure вне hello неразборчивым hello рост производительности при использовании транзакций.

Хотя использование hello транзакций может увеличить производительность, по-прежнему слишком[рекомендации для транзакций, а соединения](https://msdn.microsoft.com/library/ms187484.aspx). Сохраните транзакции hello короткими hello возможные и закрыть подключение к базе данных после завершения работы hello. с помощью инструкции в предыдущем примере hello Hello гарантирует, что hello соединение закрывается, когда hello завершения последующего блока кода.

Hello предыдущем примере показано, что можно добавить код ADO.NET tooany локальной транзакции с двумя строками. Транзакции обеспечивают быстрый способ производительность hello tooimprove кодом, который выполняет последовательные вставки, обновления и удаления операций. Однако для hello наибольшую производительность, рассмотрите возможность изменения hello кода дальнейших tootake преимущества клиентской пакетной обработки, такие как параметры, возвращающие табличные значения.

Дополнительные сведения о транзакциях в ADO.NET см. в статье [Локальные транзакции](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>Параметры, которые возвращают табличное значение
Параметры, которые возвращают табличное значение, поддерживают определяемые пользователем типы таблиц в качестве параметров в инструкциях, хранимых процедурах и функциях Transact-SQL. Этот метод пакетной обработки клиентского позволяет toosend несколько строк данных в рамках hello табличное значение параметра. toouse табличное значение параметров, необходимо сначала определить табличный тип. Привет, следующем за инструкцией Transact-SQL создает табличный тип с именем **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


Создайте в коде **DataTable** с hello точного одинаковые имена и типы hello табличного типа. Передайте этот экземпляр **DataTable** в качестве параметра в текстовом запросе или вызове хранимой процедуры. Hello ниже приведен пример этого метода.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

В предыдущем примере hello hello **SqlCommand** объекта вставляет строки из параметров, возвращающих табличные значения,  **@TestTvp** . ранее созданные Hello **DataTable** toothis параметр с hello присваивается объект **SqlCommand.Parameters.Add** метод. Пакетная обработка операций вставки hello в одном вызова значительно повышает hello производительность через последовательные вставки.

tooimprove hello предыдущий пример еще больше, используйте хранимую процедуру вместо команды на основе текста. Hello следующую команду Transact-SQL создает хранимую процедуру, которая принимает hello **SimpleTestTableType** табличное значение параметра.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

Затем измените hello **SqlCommand** объявления hello предыдущего кода примера toohello следующим объекта.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

В большинстве случаев параметры, которые возвращают табличное значение, отличаются аналогичной или более высокой производительностью в сравнении с другими методами пакетной обработки. Зачастую такие параметры более предпочтительны, так как они более универсальны в использовании, чем другие способы. Например другие методы, такие как массовое копирование SQL, разрешите только hello вставки новых строк. Но и параметры, возвращающие табличные значения, можно использовать логику в toodetermine hello хранимые процедуры, какие строки являются обновления и которые являются вставляет. Hello табличный тип также может быть toocontain измененный столбец «Операция», который показывает, определен ли hello строк следует вставить, обновить или удалить.

Hello в следующей таблице показаны результаты теста ad-hoc для hello использование возвращающих табличные значения параметров в миллисекундах.

| Операции | В локальной среде tooAzure (мс) | Один центр обработки данных Azure (мс) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10 000 |23 830 |3586 |

> [!NOTE]
> Результаты не являются измерениями производительности. В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).
> 
> 

Hello выигрыш в производительности благодаря пакетной обработке заметно сразу. В hello предыдущем последовательном тесте 1000 операций выполнялись 129 секунд вне hello центра обработки данных и 21 секунду в центре обработки данных hello. Однако с помощью параметров, возвращающих табличные значения, 1000 операций выполнялись только 2,6 секунды вне центра обработки данных hello и 0,4 секунды в центре обработки данных hello.

Дополнительные сведения о параметрах с табличным значением см. в разделе [Параметры, которые возвращают табличное значение](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>Массовое копирование SQL
Массовое копирование SQL является другим способом tooinsert больших объемов данных в целевую базу данных. Приложения .NET могут использовать hello **SqlBulkCopy** операции класс tooperform массовой вставки. **SqlBulkCopy** работает аналогично функции toohello командной строки, **Bcp.exe**, или hello инструкции Transact-SQL, **BULK INSERT**. Hello следующем примере кода показано, как hello toobulk копирования строк в источнике hello **DataTable**, таблица, toohello целевая таблица в SQL Server, MyTable.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

В некоторых случаях вместо параметров, которые возвращают табличное значение, рекомендуется использовать массовое копирование. См. таблицу сравнения hello возвращающих табличные значения параметров и операций МАССОВОЙ вставки в разделе hello [табличное значение параметры](https://msdn.microsoft.com/library/bb510489.aspx).

Hello следующие ad-результаты теста показывают производительность пакетной обработки с hello **SqlBulkCopy** в миллисекундах.

| Операции | В локальной среде tooAzure (мс) | Один центр обработки данных Azure (мс) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10 000 |21 605 |2737 |

> [!NOTE]
> Результаты не являются измерениями производительности. В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).
> 
> 

В пакетах меньшего размера, hello используют возвращающие табличные значения параметры превзошли hello **SqlBulkCopy** класса. Тем не менее **SqlBulkCopy** выполнить 12-31% быстрее, чем табличное значение параметров для тестов hello 1000 и 10 000 строк. Возвращающие табличные значения параметров, таких как **SqlBulkCopy** будет хорошим вариантом для пакетных вставок, особенно по сравнению производительности toohello непакетном операций.

Дополнительные сведения о массовом копировании в ADO.NET см. в [этой статье](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Многострочные параметризованные инструкции INSERT
Альтернатива небольшим пакетам — большой tooconstruct параметризованные инструкции INSERT, которая вставляет несколько строк. Этот метод продемонстрирован в следующем примере кода Hello.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


Этот пример предназначен основной принцип tooshow hello. Более реалистичном случае будет произведен цикл через строку hello необходимые сущности tooconstruct hello запроса и параметры команды hello одновременно. Может быть не более 2100 параметров запроса, поэтому это ограничивает общее число строк, которые могут быть обработаны таким образом hello tooa всего.

Здравствуйте, следуя ad-hoc тестирование результатов Показать hello производительности этого типа инструкций вставки в миллисекундах.

| Операции | Параметры, которые возвращают табличное значение (мс) | Один оператор INSERT (мс) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> Результаты не являются измерениями производительности. В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).
> 
> 

Этот подход показывает чуть более высокие результаты по времени для пакетов, состоящих менее чем из 100 строк. Несмотря на то, что улучшения hello мал, этот метод является другой параметр, который может работать в конкретном приложении.

### <a name="dataadapter"></a>DataAdapter
Hello **DataAdapter** класс позволяет toomodify **DataSet** а затем отправить hello изменения как операции INSERT, UPDATE и DELETE. Если вы используете hello **DataAdapter** таким образом, важно toonote, отдельные вызовы выполняются для каждой определенной операции. tooimprove производительность, используйте hello **UpdateBatchSize** свойство toohello число операций, которые должны быть объединены одновременно. Дополнительные сведения см. в статье [Выполнение пакетных операций с помощью объектов DataAdapter (ADO.NET)](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Entity Framework
В настоящее время платформа Entity Framework не поддерживает пакетную обработку. Разные разработчики в сообществе hello предпринята toodemonstrate обходные пути, например переопределение hello **SaveChanges** метод. Но hello решения обычно сложны и подогнаны toohello приложения и модели данных. проект codeplex Hello Entity Framework в настоящее время содержит страницу с обсуждением запроса этой функции. tooview данного обсуждения см [заметки о встрече разработки — 2 августа 2012 г.](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Для полноты информации мы думаем, что он является важным tootalk о XML как стратегию пакетной обработки. Тем не менее использование hello XML имеет не преимуществ по сравнению с другими методами зато обладает несколькими недостатками. Hello подход является одинаковых tootable возвращающих табличные значения параметров, но XML-файл или строка передается tooa хранимые процедуры вместо пользовательской таблицы. Hello хранимой процедуры выполняет синтаксический анализ команды hello hello хранимой процедуры.

Есть несколько недостатков toothis подход:

* Работа с содержимым XML может быть весьма трудоемкой и приводить к ошибкам.
* Hello синтаксического анализа XML в базе данных hello может сильно нагружать Процессор.
* В большинстве случаев при использовании этого метода операции выполняются медленнее, чем при использовании параметров, которые возвращают табличное значение.

По этой причине не рекомендуется использовать hello XML для пакетных запросов.

## <a name="batching-considerations"></a>Рекомендации по использованию пакетной обработки
Дополнительные рекомендации по использованию hello пакетной обработки в приложениях баз данных SQL Hello в следующих разделах.

### <a name="tradeoffs"></a>Компромиссы
В зависимости от архитектуры использование пакетной обработки предполагает некоторый компромисс между производительностью и устойчивостью приложения. Например рассмотрим сценарий hello, когда ваша роль неожиданно выходит из строя. При потере одной строки данных, влияние hello меньше, чем потеря большого пакета неотправленных строк влияние hello. Нет повышается риск при буферизации строк перед их отправкой toohello базы данных в заданном периоде времени.

Вследствие этого вычисление типа hello операций этого пакета. Следовательно, с данными, которые менее критичны, можно использовать пакеты более интенсивно (большие пакеты и более продолжительные периоды времени).

### <a name="batch-size"></a>Размер пакета
В наших тестах обычно не было не преимущества toobreaking больших пакетов на более мелкие части. На самом деле такое деление часто приводит к меньшей производительности по сравнению с отправкой одного большого пакета. Например рассмотрим сценарий, где требуется tooinsert 1000 строк. Hello следующей таблице показано время, затрачиваемое табличное значение параметров toouse tooinsert 1000 строк при делении на более мелкие.

| Размер пакета | Количество итераций | Параметры, которые возвращают табличное значение (мс) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> Результаты не являются измерениями производительности. В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).
> 
> 

Можно видеть, что hello Наилучшая производительность для 1000 строк toosubmit их все одновременно. В других тестах (не показанных здесь) было toobreak прирост производительности пакета 10000 строк на 2 пакета 5000. Но hello схема таблицы для этих тестов довольно прост, и вам следует провести, тесты в ваших данных и пакете размеры tooverify эти результаты.

Другой фактор tooconsider, что всего пакета hello становится слишком большой, базы данных SQL может регулировать и отклонить toocommit hello пакета. Для получения наилучших результатов hello тест вашего toodetermine конкретного сценария, если имеется идеальный размер пакета. Сделайте размер пакета hello можно настроить при быстро регулировать tooenable среды выполнения на основе производительности или ошибок.

Наконец Сбалансируйте размер hello hello пакета с hello риски, связанные с пакетной обработки. Если есть временные ошибки или сбоя роли hello, проанализируйте последствия hello повторное выполнение операции hello или потери данных hello в пакете hello.

### <a name="parallel-processing"></a>Параллельная обработка
Если заняло hello путь уменьшения размера пакета hello, а применение рабочих hello tooexecute нескольких потоков? Снова-таки, результаты наших тестов продемонстрировали, что несколько мелких многопоточных пакетов, как правило, обрабатываются хуже, чем один большой пакет. Hello следующий тест пытается tooinsert 1000 строк в одной или нескольких параллельных пакетах. Результаты этого теста демонстрируют, что передача нескольких параллельных пакетов снизила производительность.

| Размер пакета [количество итераций] | Два потока (мс) | Четыре потока (мс) | Шесть потоков (мс) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> Результаты не являются измерениями производительности. В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).
> 
> 

Существует несколько возможных причин hello снижение производительности из-за tooparallelism:

* Выполняется несколько одновременных вызовов сети вместо одного.
* Выполнение нескольких операций с одной таблицей может привести к состязанию и блокировке.
* Возникают издержки, связанные с многопоточностью.
* Hello расходы на открытие нескольких подключений перевешивают hello выгоду от параллельной обработки.

Если целевая различных таблиц или баз данных, это возможно toosee получить некоторые производительности с помощью этой стратегии. Этот метод подходит для сегментирования баз данных или использования федераций. Сегментирование использует несколько баз данных и базы данных tooeach маршруты различных данных. Если каждый небольшой пакет направляется tooa другую базу данных, затем выполнение операций hello в параллельном режиме может быть более эффективным. Тем не менее прирост производительности hello не является достаточной toouse как hello основания для принятия решений сегментирование баз данных toouse в решении.

В некоторых проектах параллельное выполнение небольших пакетов может привести к повышению пропускной способности запросов в системе под нагрузкой. Таким образом несмотря на то, что это быстрее tooprocess один большой пакет, обработка нескольких пакетов в параллельном режиме может быть более эффективным.

При использовании параллельного выполнения, рассмотрите возможность управления hello максимальное число рабочих потоков. Меньшее количество потоков может привести к меньшему количеству состязаний и более быстрому выполнению. Кроме того Учтите hello дополнительную нагрузку это дает на hello целевую базу данных как в соединений и транзакций.

### <a name="related-performance-factors"></a>Связанные факторы производительности
Типичные рекомендации по производительности базы данных относятся и к пакетной обработке. Например, производительность операций вставки снижается для таблиц с большим первичным ключом или несколькими некластеризованными индексами.

Если хранимая процедура табличное значение параметров, можно использовать команду hello **SET NOCOUNT ON** в начале процедуры hello hello. Эта инструкция Подавляет возврат hello hello счетчик строк влияет hello в процедуре hello. Однако в наших тестах hello использование **SET NOCOUNT ON** не оказывает никакого влияния или снижению производительности. Hello хранимая процедура для теста была простой: с одним **вставить** команду hello табличное значение параметра. Возможно, эта инструкция просто больше подходит для более сложных хранимых процедур. Но нельзя предполагать, что добавление **SET NOCOUNT ON** tooyour хранимой процедуре автоматически повысит производительность. toounderstand Здравствуйте эффект, проверьте хранимую процедуру с и без hello **SET NOCOUNT ON** инструкции.

## <a name="batching-scenarios"></a>Сценарии пакетной обработки
Hello ниже описано, как toouse табличное значение параметров в трех различных случаях. первый сценарий Hello показывает пакетную обработку и буферизацию возможной совместной работе. Второй сценарий Hello повышает производительность за счет выполнения операции с основными данными в одном вызове хранимой процедуры. Здравствуйте, последнем сценарии показано как toouse табличное значение параметров в операции «Вставки-обновления».

### <a name="buffering"></a>Буферизация
Хотя некоторые сценарии явно предполагают пакетную обработку, во многих других сценариях можно использовать преимущество отложенной пакетной обработки. Тем не менее отложенная обработка также несет большой риск того, hello данные теряются в событии hello непредвиденный сбой. Он является важным toounderstand этот риск и принимать во внимание последствия hello.

Например рассмотрим веб-приложение, которое отслеживает историю навигации каждого пользователя hello. При каждом запросе страницы приложение hello может делать представление страницы базы данных вызова toorecord hello пользователя. Но более высокую производительность и масштабируемость может осуществляться через буферизации действий пользователей hello навигации и последующей отправки этой базы данных toohello данных в пакетах. Вы можете активировать hello обновление базы данных по истечении определенного времени или размер буфера. Например правило может указывать, что этот пакет hello должен обрабатываться через 20 секунд или когда буфер hello достигает 1000 элементов.

Hello следующий пример кода использует [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess буфер событий, вызванных классом наблюдения. Когда hello заполнения буфера или истечет время ожидания, hello пакет пользовательских данных отправляется toohello базы данных с помощью параметров, возвращающих табличные значения.

Здравствуйте, приведенные ниже сведения навигации в моделях hello NavHistoryData класса пользователя. Он содержит основные сведения, такие как идентификатор пользователя hello, hello URL-адрес доступ и hello времени доступа.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

Hello NavHistoryDataMonitor класс отвечает за буферизацию hello пользовательской навигации данных toohello базы данных. Он содержит метод RecordUserNavigationEntry, который отвечает вызовом события **OnAdded** . Hello следующем коде показана логика hello конструктора, использующего Rx toocreate наблюдаемой коллекции на основе события hello. Затем он подписывается toothis наблюдаемую коллекцию с помощью метода hello буфера. перегрузка Hello указывает этого буфера hello должны отправляться каждые 20 секунд или 1000 элементов.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

Hello обработчик преобразует все элементы в буфер hello в тип возвращающих табличные значения, а затем передает этой tooa хранимой процедуры тип пакета hello процессов. Hello следующем примере кода показано полное определение hello NavHistoryDataEventArgs и классы NavHistoryDataMonitor hello hello.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse этого класса буферизации приложение hello создает статический объект NavHistoryDataMonitor. Каждый раз, пользователь обращается к странице, приложение hello вызывает метод NavHistoryDataMonitor.RecordUserNavigationEntry hello. Логика буферизации Hello продолжается tootake заботиться о отправки следующих записей toohello баз данных в пакетах.

### <a name="master-detail"></a>Основная и подробная информация
Параметры, которые возвращают табличное значение, используются в простых сценариях с использованием инструкции INSERT. Тем не менее он может быть более сложной toobatch вставок, работающих с более одной таблицы. Хорошим примером является сценарий Hello «основной/подробности». Hello главная таблица определяет hello основной сущности. Одна или несколько таблиц, детализации хранить больше данных о сущности hello. В этом случае связи по внешнему ключу обеспечивают связь hello сведения tooa уникальной основной сущностью. Рассмотрим упрощенную версию таблицы PurchaseOrder и связанной с ней таблицы OrderDetail. Привет, следуя Transact-SQL создает таблицу PurchaseOrder hello с четырьмя столбцами: OrderID, OrderDate, CustomerID и состояние.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Каждый заказ содержит информацию об одной или нескольких покупках товара. Эти сведения сохраняются в таблице PurchaseOrderDetail hello. Привет, следуя Transact-SQL создает таблицу hello PurchaseOrderDetail с пятью столбцами: OrderID, OrderDetailID, ProductID, UnitPrice и OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

столбец OrderID Hello таблицы PurchaseOrderDetail hello должен ссылаться на заказ из таблицы PurchaseOrder hello. После определения внешнего ключа Hello принудительно вводит это ограничение.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

В порядке toouse табличное значение параметров необходимо иметь один определяемый пользователем табличный тип для каждой целевой таблицы.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Затем определите хранимую процедуру, которая принимает таблицы этих типов. Эта процедура позволяет пакет приложения toolocally набор заказов и сведения о заказе в рамках одного вызова. Hello следующий запрос Transact-SQL предоставляет hello полное объявление хранимой процедуры для этого примера заказа на покупку.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

В этом примере hello локально определенные @IdentityLink таблице хранятся hello фактические значения OrderID из hello вновь вставке строк. Эти идентификаторы заказов отличаются от временных значений OrderID hello в hello @orders и @details табличное значение параметров. По этой причине hello @IdentityLink таблицы подключает hello OrderID значения из hello @orders параметр toohello реальные OrderID значения для hello новых строк в таблице PurchaseOrder hello. После выполнения этого шага hello @IdentityLink таблицы может упростить вставку подробностей заказа hello с hello фактическое OrderID, удовлетворяющий hello ограничение внешнего ключа.

Эту хранимую процедуру можно использовать из кода или из других вызовов Transact-SQL. В разделе hello табличное значение параметров в этом документе для примера кода. Привет, следуя Transact-SQL показывает, как toocall hello sp_InsertOrdersBatch.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

Это решение позволяет toouse каждого пакета набор значений OrderID, которые начинаются с 1. Эти временные значения OrderID описывают связи hello в пакете hello, но фактические значения OrderID hello определяются во время операции вставки hello hello. Можно выполнениях hello и те же операторы в предыдущем примере hello и сформировать уникальные заказы в базе данных hello. Поэтому рассмотрите возможность добавления дополнительного кода или логики базы данных, которые не допустят повторения заказов при использовании этого метода пакетной обработки.

В этом примере показано, что с помощью параметров, которые возвращают табличное значение, в пакет можно включить даже такие сложные операции с базой данных, как операции с основной и подробной информацией.

### <a name="upsert"></a>Операция UPSERT
Другой случай использования пакетной обработки подразумевает одновременное обновление существующих и вставку новых строк. Эта операция иногда является ссылка tooas операции «Вставки-обновления» (update + insert). Вместо выполнения отдельных вызовов tooINSERT и UPDATE, инструкция MERGE hello осуществляется лучше всего подходит toothis. Hello инструкцию MERGE можно выполнять вставки и обновления в рамках одного вызова.

Возвращающие табличные значения параметры могут использоваться с hello MERGE инструкции tooperform обновления и вставки. Например, рассмотрим таблицу Employee упрощенный, содержит следующие столбцы hello: EmployeeID, FirstName, LastName, SocialSecurityNumber:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

В этом примере можно использовать hello фактов, hello SocialSecurityNumber является уникальным tooperform СЛИЯНИЯ нескольких сотрудников. Сначала создайте hello определяемого пользователем табличного типа.

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

Далее создайте хранимую процедуру или написать код, которая использует hello tooperform hello MERGE инструкции update и insert. Hello следующий пример использует инструкцию MERGE hello для возвращающих табличные значения параметра, @employees, EmployeeTableType типа. Здравствуйте, содержимое hello @employees таблицы здесь не показаны.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Дополнительные сведения см. в разделе документации hello и примеры для инструкции MERGE hello. Несмотря на то, что приветствия же работа может быть выполнена в несколько шагов вызова хранимой процедуры с помощью отдельных операций INSERT и UPDATE, hello инструкции MERGE является более эффективным. Код базы данных можно также создать вызовы Transact-SQL, использующих hello инструкции MERGE напрямую без необходимости двух вызовов базы данных для INSERT и UPDATE.

## <a name="recommendation-summary"></a>Сводка рекомендаций
Hello ниже приведены Сводка hello пакетной обработки рекомендации, описанные в этом разделе.

* Используйте буферизацию и пакетную обработку tooincrease hello производительность и масштабируемость приложений баз данных SQL.
* Понимать hello компромисса между пакетной обработкой или буферизацией и устойчивостью приложения. Во время сбоя роли hello риск потери необработанного пакета важных бизнес-данных может перевесить выигрыш производительности hello пакетной обработки.
* Попробуйте tookeep все вызовы toohello базы данных с задержкой tooreduce одного центра обработки данных.
* Если выбран метод с отправкой одного возвращающих табличные значения параметры обеспечивают hello наилучшую производительность и гибкость.
* Для hello быстрым добавлять производительности, общие рекомендации при этом протестируйте свой сценарий:
  * Для < 100 строк используйте одну параметризованную команду INSERT.
  * Для < 1000 строк используйте параметры, которые возвращают табличное значение.
  * Для >= 1000 строк используйте SqlBulkCopy.
* Для обновления и операции удаления, используйте табличное значение параметров с помощью хранимой процедуры логику, определяющую hello правильную операцию для каждой строки в параметр таблицы hello.
* Рекомендации по размеру пакета.
  * Используйте hello большие размеры пакетов, подходящие для вашего приложения и бизнес-требований.
  * Прирост производительности hello баланс больших пакетов с hello риск использования временных или неожиданных отказов. Что такое hello последствия повторного выполнения операций или потери данных hello в пакете hello 
  * Протестируйте tooverify пакета размер hello для наибольшего, база данных SQL не отклоняет его.
  * Создание параметров конфигурации, управляющие пакетной обработкой, такие как размер пакета hello или буферизации временное окно приветствия. Эти параметры дают возможность гибко управлять пакетной обработкой. Можно изменить поведение в рабочей среде объединения без повторного развертывания облачной службы hello hello.
* Избегайте параллельного выполнения пакетов, которые используют одну таблицу в одной базе данных. Если вы решите toodivide один пакет на несколько рабочих потоков, выполните тесты toodetermine hello оптимальное количество потоков. После достижения неопределенного порогового значения большее число потоков уменьшит производительность, а не повысит ее.
* Рассмотрите буферизацию операций по количеству и времени в качестве способа реализации пакетной обработки для нескольких сценариев.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье основное внимание уделено как структура базы данных и методы написания кода, связанные toobatching может повысить производительность приложения и масштабируемость. Но это всего лишь один фактор в общей стратегии. Дополнительные способы tooimprove производительности и масштабируемости в разделе [руководство по производительности базы данных SQL Azure для отдельных баз данных](sql-database-performance-guidance.md) и [вопросы цены и производительности для эластичного пула](sql-database-elastic-pool-guidance.md).

