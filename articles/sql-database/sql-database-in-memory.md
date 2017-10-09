---
title: "технологии SQL базы данных в памяти aaaAzure | Документы Microsoft"
description: "Технологии Azure SQL базы данных в памяти значительно повысить производительность hello транзакций и аналитических рабочих нагрузок. Узнайте, как tootake преимущества этих технологий."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>Оптимизация производительности с помощью технологий обработки в оперативной памяти в базе данных SQL

С помощью технологий обработки в оперативной памяти, доступных в базе данных SQL Azure, можно добиться улучшения производительности при различных рабочих нагрузках: транзакции (интерактивная обработка транзакций (OLTP)), аналитические операции (интерактивная аналитическая обработка (OLAP)) и нагрузки смешанного типа (гибридная транзакционная и аналитическая обработка (HTAP)). Из-за Здравствуйте эффективность запросов и обработки транзакций, технологии в памяти также помогают tooreduce затрат. Обычно не требуется tooupgrade hello ценовой категории для повышения производительности tooachieve hello базы данных. В некоторых случаях можно даже будет уменьшить hello ценовой категории, во время по-прежнему присутствует повышена производительность и технологии в памяти.

Ниже приведены два примера как помогла toosignificantly повысить производительность в OLTP в памяти.

- С помощью In-Memory OLTP [кворума бизнес-решений было своей рабочей нагрузки может toodouble при одновременном повышении Dtu на 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - DTU обозначает *единицы передачи данных*. Этот параметр содержит оценку потребления ресурсов.
- Hello следующее видео демонстрирует значительное улучшение в потреблении ресурсов с пример рабочей нагрузки: [In-Memory OLTP в базе данных SQL Azure видео](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Дополнительные сведения см. в разделе hello записи блога: [In-Memory OLTP в записи блога Azure SQL базы данных](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

Технологии в памяти доступны во всех базах данных уровня Premium hello, включая базы данных в пулах эластичных Premium.

Hello следующие видео объясняет выигрыш производительности с технологиями в памяти в базе данных SQL Azure. Помните, что hello прироста производительности, которое вы видите всегда зависит от многих факторов, включая hello характер рабочей нагрузки hello и данных, шаблон доступа hello базы данных и т. д.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

База данных SQL Azure состоит из следующих технологий памяти hello.

- *In-Memory OLTP* повышает пропускную способность и сокращает задержки при обработке транзакций. Выполняющуюся в памяти OLTP полезно использовать в следующих сценариях: обработка транзакций с высокой пропускной способностью, например для торговли и игр, прием данных о событиях или устройствах Интернета вещей, кэширование, загрузка данных, использование временных таблиц и табличных переменных.
- *Кластеризованные индексы columnstore* уменьшить объем хранилища (времен too10) и повысить производительность запросов, отчетов и аналитики. Можно использовать с таблицами фактов в вашей toofit витринах данных больше данных в базе данных и повышения производительности. Кроме того можно использовать со статистическими данными в вашей рабочей базы данных tooarchive и быть может tooquery too10 времени больше данных.
- *Некластеризованные индексы columnstore* HTAP справку в режиме реального времени анализировать toogain ваш бизнес через запрос hello рабочей базы данных напрямую, без необходимости toorun hello дорогих извлечения, преобразования и процесса загрузки (ETL) и ожидания для заполнения hello toobe хранилища данных. Некластеризованные индексы columnstore разрешает быстрого выполнения аналитических запросов на базы данных OLTP hello, одновременно уменьшая hello влияние на hello рабочей нагрузки.
- Также возможно сочетание hello оптимизированных для памяти таблицы с индексом columnstore. Это сочетание позволяет очень быстро транзакции tooperform обработки и слишком*одновременно* выполнения analytics запрашивает очень быстро на hello же данных.

Индексы columnstore и In-Memory OLTP были частью hello продукта SQL Server 2012 и 2014, соответственно. Azure базы данных SQL и SQL Server используют hello же реализации технологии в памяти. При этом новые возможности сначала предоставляются для базы данных SQL Azure, а затем выпускаются для SQL Server.

В этом разделе описываются аспекты In-Memory OLTP и columnstore индексы, определенные tooAzure базы данных SQL и содержит также фрагменты кода:
- Вы увидите hello влияние этих технологий на хранение данных и ограничения на размер.
- Вы увидите, как toomanage hello перемещения баз данных, которые используют эти технологии между hello различным ценовым категориям.
- Вы увидите два примеры, иллюстрирующие использование hello In-Memory OLTP, а также индексов columnstore в базе данных SQL Azure.

См. следующие ресурсы для получения дополнительной информации hello.

Подробные сведения о технологиях hello:

- [Общие сведения о OLTP в памяти и сценариях использования](https://msdn.microsoft.com/library/mt774593.aspx) (включает примеры использования toocustomer ссылки и сведения tooget работы)
- [In-Memory OLTP (оптимизация в памяти)](http://msdn.microsoft.com/library/dn133186.aspx)
- [Описание индексов columnstore](https://msdn.microsoft.com/library/gg492088.aspx)
- Гибридные сценарии транзакционной и аналитической обработки, которые также называются [операционной аналитикой в реальном времени](https://msdn.microsoft.com/library/dn817827.aspx).

Краткое руководство по In-Memory OLTP: [краткое руководство 1: технологии выполнения OLTP в памяти для быстрее производительности T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (Начало работы другого toohelp статье)

Подробные видеоролики о технологиях hello:

- [In-Memory OLTP в базе данных SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (который содержит демонстрационную версию производительности преимущества и шаги tooreproduce эти результаты самостоятельно)
- [In-Memory OLTP видео: Что это такое и когда/как toouse его](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Columnstore Index: In-Memory Analytics (i.e. columnstore index) Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/) (Видео о выполняющейся в памяти аналитике (например, индексах columnstore) с конференции Ignite 2016).

## <a name="storage-and-data-size"></a>Емкость хранилища и объем данных

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Ограничения на объем данных и емкость хранилища для In-Memory OLTP

In-Memory OLTP включает оптимизированные для памяти таблицы, которые используются для хранения пользовательских данных. Эти таблицы являются обязательным toofit в памяти. Так как вы управляете памяти непосредственно в hello служба базы данных SQL, у нас есть концепция hello квоты для пользовательских данных. Идея является ссылка tooas *хранилища In-Memory OLTP*.

Каждая поддерживаемая ценовая категория отдельных баз данных и пулов эластичных баз данных включает некоторый объем хранилища выполняющейся в памяти OLTP. На момент написания статьи hello вы получаете один гигабайт хранилища для каждого 125 единицы транзакций баз данных (Dtu) или эластичной базы данных единицы транзакций (Edtu).

Hello [уровней обслуживания базы данных SQL](sql-database-service-tiers.md) статья имеет hello официальный список hello In-Memory OLTP доступного хранилища для каждого поддерживаемого Автономная база данных и ценовой категории эластичного пула.

Привет, следующие элементы, учитываются украшение хранилища In-Memory OLTP:

- Активные строки пользовательских данных в оптимизированных для памяти таблицах и переменных таблиц. Обратите внимание, что старых версий строк не учитываются при определении hello cap.
- Индексы оптимизированных для памяти таблиц.
- Операционные затраты на операции ALTER TABLE.

При достижении конца hello появляется сообщение об ошибке out из квоты и вы больше не будет tooinsert или обновления данных. toomitigate эту ошибку, удалите данные или увеличьте hello ценовой категории базы данных hello или пула.

Дополнительные сведения о мониторинге использования хранилища In-Memory OLTP и настройка оповещений по достижении конца hello почти см. в разделе [монитор в памяти хранилища](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>О пулах эластичных баз данных

При использовании пулов эластичных hello хранилища In-Memory OLTP совместно среди всех баз данных в пуле hello. Таким образом использование hello в одной базе данных может влиять на другие базы данных. Есть два пути устранения таких проблем.

- Настройте Max-eDTU для баз данных, меньше, чем число hello eDTU пула hello в целом. Использование хранилища In-Memory OLTP hello в любой базе данных в пуле hello, размер toohello, соответствующее число eDTU toohello для креплений максимального.
- Установите для баз данных параметр Min-eDTU больше нуля. Это минимальный гарантирует, что каждая база данных в пуле hello имеет hello объем доступного хранилища In-Memory OLTP, соответствующий toohello настроен Min eDTU.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>Размер данных и хранилище для индексов сolumnstore

Индексы ColumnStore не требуется toofit в памяти. Таким образом, hello только ограничение на размер hello hello индексов является hello максимальный общий размер базы данных, который описан в hello [уровней обслуживания базы данных SQL](sql-database-service-tiers.md) статьи.

При использовании кластеризованных индексов, столбцам сжатия используется для хранения базовой таблицы hello. Такое сжатие может значительно уменьшить объем хранилища hello данные пользователей, это означает, что может поместиться больше данных в базе данных hello. И hello сжатия может быть увеличено с [столбцам архивного сжатия](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). Hello степень сжатия, можно добиться зависит от природы hello hello данных, но 10 раз hello сжатия не возникают.

Например если имеется база данных размером до 1 терабайт (ТБ) и добиться сжатия hello 10 раз с помощью индексов columnstore, может удовлетворить всего 10 ТБ пользовательских данных в базе данных hello.

При использовании некластеризованных индексов columnstore hello базовой таблицы все еще хранятся в формате традиционных rowstore hello. Таким образом hello экономии пространства хранения, не являются большим, чем с кластеризованными индексами columnstore. Тем не менее при замене число традиционной некластеризованные индексы с одним индексом columnstore, по-прежнему видно общей экономии hello сократить объем хранилища для таблицы hello.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Изменение ценовых категорий баз данных, использующих технологии обработки в оперативной памяти

Не может находиться любые проблемы совместимости или других проблем при обновлении tooa ценовой категории, такие как из стандартных tooPremium более поздней версии. доступные функции Hello и ресурсы только повысить.

Но переходе hello ценовой категории может отрицательно повлиять на базу данных. влияние Hello особенно очевиден при переходе с Premium tooStandard или Basic, когда база данных содержит объекты OLTP в памяти. Оптимизированные для памяти таблицы и индексы columnstore будут недоступны после понижения hello (даже если они оставались видимыми). Hello же рекомендации применяются, когда понижение hello ценовой категории пула эластичных БД или перемещение базы данных при использовании технологии в памяти, в стандартный или базовой эластичного пула.

### <a name="in-memory-oltp"></a>In-Memory OLTP;

*Понижение уровня tooBasic/Standard*: OLTP в памяти не поддерживается в базах данных уровня Standard и Basic hello. Кроме того это не значит возможных toomove базу данных с любой toohello объектов In-Memory OLTP уровня Standard и Basic.

До возврата к предыдущей версии базы данных hello tooStandard и простой, удалите все таблицы, оптимизированные для памяти табличных типов, а также всех скомпилированных в собственном коде модулей T-SQL.

Нет toounderstand программный способ поддержку данной базы данных OLTP в памяти. Можно выполнить приветствия при следующем запросе Transact-SQL:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Если запрос hello возвращает **1**, In-Memory OLTP поддерживается в этой базе данных.


*Понижение уровня tooa нижнего уровня Premium*: данные в таблицах, оптимизированных для памяти должны умещаться в хранилища In-Memory OLTP hello, связан с ценовой категории базы данных hello hello, или в hello эластичного пула. При попытке hello toolower ценовой категории или перемещение базы данных hello в пул, не имеет достаточно свободного In-Memory OLTP, hello операция заканчивается неудачно.

### <a name="columnstore-indexes"></a>Индексы columnstore

*Понижение уровня tooBasic или Standard*: Columnstore, индексы поддерживаются только в ценовой категории "премиум" hello, а не в hello уровней Standard и Basic. При переходе с tooStandard базы данных или Basic, индекс columnstore становится недоступной. Hello система сохраняет индекс columnstore, но он никогда не использует индекс hello. При обновлении позже tooPremium назад, индекс columnstore является немедленно готовы toobe попытку использовать.

Если у вас есть **кластеризованный** индекс columnstore hello вся таблица становится недоступным после понижения уровня. Корпорация Майкрософт рекомендует удалить все *кластеризованный* перед переходе базы данных ниже уровня Premium hello индексов columnstore.

*Понижение уровня tooa нижнего уровня Premium*: этот переход к более раннему завершается успешно, если hello вся база данных помещается в hello максимальный размер базы данных для целевого объекта hello ценовой категории, или внутри hello доступного хранилища в пуле эластичных БД hello. Отсутствует влияние конкретных hello индексов columnstore.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Установите образец hello In-Memory OLTP

Можно создать с помощью нескольких щелчков в hello учебной базой данных AdventureWorksLT hello [портал Azure](https://portal.azure.com/). Затем hello действия, описанные в этом разделе объясняется, как можно дополнить базе данных AdventureWorksLT с объектами OLTP в памяти и продемонстрировать преимущества производительности.

Упрощенная, но одновременно более наглядная демонстрация выполняющейся в памяти OLTP представлена здесь:

- Выпуск: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Исходный код: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Шаги установки

1. В hello [портал Azure](https://portal.azure.com/), создание расширенной базы данных на сервере. Набор hello **источника** toohello учебной базой данных AdventureWorksLT. Подробные инструкции см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio](sql-database-get-started-portal.md).

2. Подключение базы данных toohello с SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Копировать hello [сценарий In-Memory OLTP Transact-SQL](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour буфер обмена. Hello скрипт T-SQL создает необходимые в памяти объекты hello в hello AdventureWorksLT образца базы данных, созданной на шаге 1.

4. Вставьте скрипт T-SQL hello в SSMS и затем выполнить сценарий hello. Hello `MEMORY_OPTIMIZED = ON` предложение инструкции CREATE TABLE имеют большое значение. Например:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Ошибка 40536


Если появляется ошибка 40536 при запуске скрипта hello T-SQL, выполните следующие tooverify скрипт T-SQL, hello поддерживает ли база данных в памяти hello:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


Значение **0** указывает на то, что обработка в оперативной памяти не поддерживается, а значение **1** — наоборот. проблема toodiagnose hello, гарантировать hello базы данных уровня Premium hello.


#### <a name="about-hello-created-memory-optimized-items"></a>О hello созданных элементов, оптимизированных для памяти

**Таблицы**: пример hello содержит hello в следующей таблице, оптимизированной для памяти:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


Вы можете проверить оптимизированных для памяти таблиц с помощью hello **обозревателя объектов** в среде SSMS. Щелкните правой кнопкой мыши **Таблицы** > **Фильтры** > **Параметры фильтров** > **Оптимизирован для памяти**. Hello значение равно 1.


Или можно также запросить представления каталога hello, такие как:


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**Скомпилированная в собственном коде хранимая процедура**: процедуру SalesLT.usp_InsertSalesOrder_inmem можно проверить с помощью запроса представления каталога.


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Запустите рабочую нагрузку OLTP образец hello

Здравствуйте разность двух следующих hello *хранимых процедур* hello первая процедура использует оптимизированных для памяти версии таблиц hello, при hello вторая процедура использует hello обычных таблицах на диске:

- SalesLT**.**usp_InsertSalesOrder**_inmem**
- SalesLT**.**usp_InsertSalesOrder**_ondisk**


В этом разделе, показано, как toouse hello под рукой **ostress.exe** tooexecute программа hello две хранимые процедуры на стрессовые уровнях. Можно сравнить, сколько времени занимает toofinish запусков нагрузочных hello двух.


При запуске ostress.exe, мы рекомендуем передавать значения параметров, предназначенных для обоих следующих hello:

- -n100 — для выполнения большого количества одновременных подключений;
- -r500 — для многократного (сотни раз) выполнения каждого цикла подключения.


Тем не менее может потребоваться toostart с намного меньше значения, такие как - n10 и - r50 tooensure, что все работает.


### <a name="script-for-ostressexe"></a>Скрипт для ostress.exe


В этом разделе отображается hello скрипт T-SQL, внедренный в наших ostress.exe командной строки. Hello скрипт использует элементы, которые были созданы путем hello скрипт T-SQL, которое ранее было установлено.


Hello следующий скрипт вставляет образец заказа на продажу с пятью линейными элементами в следующих hello оптимизированных для памяти *таблиц*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


toomake hello *_ondisk* версии Здравствуйте предыдущий сценарий T-SQL для ostress.exe, и замените оба экземпляра hello *_inmem* substring с *_ondisk*. Эти замены влияет на приветствия имен таблиц и хранимых процедур.


### <a name="install-rml-utilities-and-ostress"></a>Установка служебных программ RML и ostress


В идеальном случае следует запланировать toorun ostress.exe на виртуальной машине Azure (ВМ). Вы создадите [виртуальной Машины Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) в hello же Azure географическом регионе, где находится базе данных AdventureWorksLT. Но вы также можете запустить программу ostress.exe и на переносном компьютере.


На hello виртуальной Машины или на узле все, что выбрать, установите служебные программы hello языка разметки воспроизведения (RML). Служебные программы Hello включают ostress.exe.

Дополнительные сведения можно найти в разделе 
- Здравствуйте, обсуждение ostress.exe в [образца базы данных для In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).
- Или ознакомьтесь со статьей [Пример базы данных для выполняющейся в памяти OLTP](http://msdn.microsoft.com/library/mt465764.aspx).
- Hello [блога по установке ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Запустите hello *_inmem* сначала загрузить рабочей нагрузки


Можно использовать *RML Cmd Prompt* окна toorun наших ostress.exe командной строки. параметры командной строки Hello прямой ostress для:

- параллельно выполнять 100 подключений (-n100);
- У каждого соединения, запустите скрипт T-SQL hello 50 раз (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


toorun hello предшествующий ostress.exe командной строки:


1. Сброс данных содержимое hello базы данных, выполнив следующую команду в SSMS, toodelete hello все hello данные, которые вносились во все предыдущие запуски:

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Скопируйте текст hello hello предшествующий буфера tooyour ostress.exe командной строки.

3. Замените hello `<placeholders>` hello параметры -S - U -P -d с hello правильная реальные значения.

4. В окне командной строки RML запустите измененную командную строку.


#### <a name="result-is-a-duration"></a>Результат — это длительность выполнения теста


По завершении ostress.exe она записывает длительность выполнения как его последняя строка выходных данных в окне приветствия RML Cmd hello. Например, более короткий тестовый запуск длится около 1,5 минут:

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Сброс базы данных, изменение значения *_ondisk* и повторный запуск


После того как вы hello в результате hello *_inmem* запуска, выполните следующие шаги для hello hello *_ondisk* запуска:


1. Сброс hello базы данных, выполнив следующую команду в SSMS toodelete hello все данные hello добавленный hello предыдущего выполнения:
```
EXECUTE Demo.usp_DemoReset;
```

2. Изменить tooreplace hello ostress.exe командной строки *_inmem* с *_ondisk*.

3. Повторно запустите ostress.exe для hello во второй раз и записать результат длительность hello.

4. Опять же сбросьте hello базы данных (для ответственно удаление большого объема тестовых данных, которое может быть).


#### <a name="expected-comparison-results"></a>Ожидаемые результаты сравнения

Наши тесты в памяти показали, повысить производительность **девяти раз** для этой простой рабочей нагрузки с ostress запущен на Виртуальной машине Azure в hello же регионе Azure, что hello базы данных.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Установите образец hello аналитики в памяти


В этом разделе вы сравнить hello операции ввода-ВЫВОДА и статистику результатов при работе с индексом columnstore сравнению с традиционной сбалансированного дерева индекса.


Для аналитики в реальном времени рабочей нагрузки OLTP часто бывает наиболее toouse некластеризованный индекс columnstore. Дополнительные сведения см. в статье [Руководство по индексам columnstore](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-hello-columnstore-analytics-test"></a>Подготовка hello columnstore analytics теста


1. Используйте hello Azure портала toocreate из образца hello свежей базы данных AdventureWorksLT.
 - Используйте такое же имя.
 - Выберите любой уровень служб категории «Премиум».

2. Копировать hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour буфер обмена.
 - Hello скрипт T-SQL создает необходимые в памяти объекты hello в hello AdventureWorksLT образца базы данных, созданной на шаге 1.
 - Hello скрипт создает таблицу измерения hello и две таблицы фактов. таблицы фактов Hello заполняются 3.5 миллионов строк.
 - Hello скрипта может занять toocomplete 15 минут.

3. Вставьте скрипт T-SQL hello в SSMS и затем выполнить сценарий hello. Hello **COLUMNSTORE** ключевое слово в hello **CREATE INDEX** большое значение, как и в инструкции:<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. Установите уровень toocompatibility AdventureWorksLT 130:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    Уровень 130 не функции непосредственно связанная tooIn памяти. При этом уровень 130 обычно обеспечивает более высокую скорость обработки запросов, чем уровень 120.


#### <a name="key-tables-and-columnstore-indexes"></a>Ключевые таблицы и индексы columnstore


- dbo. FactResellerSalesXL_CCI является таблица, которая имеет кластеризованный индекс, с расширенным сжатия на hello *данные* уровне.

- dbo. FactResellerSalesXL_PageCompressed является таблица, которая имеет эквивалент регулярного кластеризованный индекс, который сжимается только на hello *страницы* уровне.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>Индекс columnstore hello toocompare запросы ключей


Существуют [несколько типов запросов T-SQL, которые можно выполнить](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee повышение производительности. В шаге 2 раздела hello скрипт T-SQL Обратите внимания пары toothis запросов. Они отличаются только одной строкой.


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Кластеризованный индекс находится в hello FactResellerSalesXL\_CCI таблицы.

Hello следующий фрагмент скрипта T-SQL Выводит статистику ввода-ВЫВОДА и время для запроса hello каждой таблицы.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

В базе данных с hello P2 ценовую категорию можно ожидать около девяти раз hello выигрыш в производительности для этого запроса с помощью hello кластеризованный индекс, по сравнению с традиционными индексами hello. P15 то можно ожидать выигрыш в производительности примерно 57 раз hello с помощью индекса columnstore hello.



## <a name="next-steps"></a>Дальнейшие действия

- [Краткое руководство 1. Технологии выполнения OLTP в памяти для повышения производительности службы Transact-SQL](http://msdn.microsoft.com/library/mt694156.aspx)

- [Повышение производительности приложений в базе данных SQL с помощью выполняющейся в памяти OLTP](sql-database-in-memory-oltp-migration.md)

- [Мониторинг хранилища OLTP в памяти](sql-database-in-memory-oltp-monitoring.md)


## <a name="additional-resources"></a>Дополнительные ресурсы

#### <a name="deeper-information"></a>Подробные сведения

- Узнайте, как [Quorum удваивает ключевую рабочую нагрузку на базу данных при одновременном сокращении DTU на 70 % благодаря использованию In-Memory OLTP для базы данных SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [In-Memory OLTP in Azure SQL Database](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (Выполняющаяся в памяти OLTP в базе данных SQL Azure)

- [Learn about In-Memory OLTP](http://msdn.microsoft.com/library/dn133186.aspx) (Знакомство с In-Memory OLTP)

- [Руководство по индексам columnstore](https://msdn.microsoft.com/library/gg492088.aspx)

- [Начало работы с Columnstore для получения операционной аналитики в реальном времени](http://msdn.microsoft.com/library/dn817827.aspx)

- Технический документ с [рекомендациями по распространенным шаблонам рабочих нагрузок и миграции](http://msdn.microsoft.com/library/dn673538.aspx) включает описание шаблонов рабочих нагрузок, для которых выполняющаяся OLTP обычно обеспечивает значительное повышение производительности.

#### <a name="application-design"></a>Проектирование приложений

- [In-Memory OLTP (оптимизация в памяти)](http://msdn.microsoft.com/library/dn133186.aspx)

- [Повышение производительности приложений в базе данных SQL с помощью выполняющейся в памяти OLTP](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>Средства

- [Портал Azure](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)
