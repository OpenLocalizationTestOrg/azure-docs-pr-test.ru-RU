---
title: "aaaIn-Memory OLTP повышает производительность транзакций SQL | Документы Microsoft"
description: "In-Memory OLTP adopt tooimprove транзакций производительности в существующую базу данных SQL."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>Использование In-Memory OLTP tooimprove производительность приложений базы данных SQL
[In-Memory OLTP](sql-database-in-memory.md) может быть используется tooimprove hello производительность обработки транзакций, приема данных и сценариев временных данных, в [Premium](sql-database-service-tiers.md) баз данных SQL Azure без увеличения hello ценовой категории. 

> [!NOTE] 
> Узнайте, как [Quorum удваивает ключевую рабочую нагрузку на базу данных при одновременном сокращении DTU на 70 % благодаря использованию базы данных SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).


Выполните эти шаги по tooadopt In-Memory OLTP в существующей базе данных.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Этап 1. Проверка того, что используется база данных уровня "Премиум"
Выполняющаяся в памяти OLTP поддерживается только в базах данных уровня "Премиум". Поддерживаются в памяти, если hello возвращаемый результат равен 1 (не 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

Сокращение *XTP* обозначает технологию *экстремальной обработки транзакций (Extreme Transaction Processing)*.



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>Шаг 2: Определение объектов toomigrate tooIn-Memory OLTP
Среда SSMS позволяет создать отчет **Обзор анализа производительности транзакций** , который затем можно запустить для базы данных с активной рабочей нагрузкой. отчет Hello определяет таблицы и хранимые процедуры, которые являются кандидатами на перенос tooIn-Memory OLTP.

В среде SSMS toogenerate hello отчета:

* В hello **обозревателя объектов**, щелкните правой кнопкой мыши узел вашей базы данных.
* Щелкните **Отчеты** > **Стандартные отчеты** > **Обзор анализа производительности транзакций**.

Дополнительные сведения см. в разделе [определение ли таблица или хранимая процедура должна быть перенесена tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Шаг 3. Создание сопоставимой тестовой базы данных
Предположим, что отчет hello указывает базу данных таблицу, которая будет полезным, преобразовать tooa оптимизированной для памяти таблицы. Рекомендуется сначала протестировать tooconfirm hello указывает путем проверки.

Вам понадобится тестовая копия рабочей базы данных. Hello тестирования базы данных должны находиться в hello же службы уровень как ваша рабочая база данных.

тестирование, tooease настроить тестовой базы данных следующим образом:

1. Подключение toohello тестовую базу данных с помощью среды SSMS.
2. tooavoid необходимости Здравствуйте параметр WITH (SNAPSHOT) в запросах, задайте параметр hello базы данных, как показано в hello, следующие инструкции T-SQL:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Шаг 4. Миграция таблиц
Необходимо создать и заполнить копии оптимизированных для памяти таблицы hello требуется tootest. Ее можно создать с помощью:

* Hello удобные мастера оптимизации памяти в среде SSMS.
* вручную с помощью инструкций T-SQL.

#### <a name="memory-optimization-wizard-in-ssms"></a>Создание таблицы с помощью мастера оптимизации памяти в SSMS
toouse этот вариант миграции:

1. Подключение toohello тестовую базу данных с помощью SSMS.
2. В hello **обозревателя объектов**, щелкните правой кнопкой мыши в таблице hello и нажмите кнопку **помощник по оптимизации памяти**.
   
   * Hello **помощника по оптимизатор памяти таблицы** появится мастер.
3. В мастере приветствия щелкните **проверки миграции** (или hello **Далее** кнопки) toosee, если таблица hello неподдерживаемые функции, которые не поддерживаются в таблицах, оптимизированных для памяти. Дополнительные сведения можно найти в разделе 
   
   * Hello *контрольный список оптимизации памяти* в [помощник по оптимизации памяти](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Конструкции языка Transact-SQL не поддерживаются компонентом In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Миграция tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).
4. Если hello таблицы без неподдерживаемых функций, hello advisor можно выполнять схемой, фактически hello и переноса данных для вас.

#### <a name="manual-t-sql"></a>Создание таблицы вручную с помощью инструкций T-SQL
toouse этот вариант миграции:

1. Подключение tooyour тестовую базу данных с помощью SSMS (или другой подобной программы).
2. Получите hello полный сценарий T-SQL для таблицы и ее индексов.
   
   * В среде SSMS щелкните правой кнопкой мыши узел таблицы.
   * Щелкните **Создать сценарий для таблицы** > **Используя CREATE** > **Новое окно запроса**.
3. В окне приветствия сценария добавьте WITH (MEMORY_OPTIMIZED = ON) toohello инструкции CREATE TABLE.
4. Если имеется КЛАСТЕРИЗОВАННЫЙ индекс, измените его tooNONCLUSTERED.
5. С помощью SP_RENAME переименуйте существующую таблицу hello.
6. Создайте hello новые оптимизированные для памяти копии hello таблицы, выполнив измененного скрипта CREATE TABLE.
7. Копировать hello данных tooyour оптимизированной для памяти таблицы с помощью инструкции INSERT... ВЫБЕРИТЕ * В:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Шаг 5 (необязательный). Миграция хранимых процедур
функция Hello в памяти можно также изменить хранимую процедуру для повышения производительности.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Общие сведения о скомпилированных в собственном коде хранимых процедурах
Скомпилированные в собственном коде хранимой процедуры должен иметь следующие параметры в своем предложении T-SQL с hello:

* NATIVE_COMPILATION;
* SCHEMABINDING: таблицы значения, которые hello хранимая процедура не может иметь свои определения столбцов, изменен каким-либо образом повлияет на hello хранимые процедуры, только удаления hello хранимой процедуры.

Собственный модуль должен использовать один большой [блок ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) для управления транзакциями. Роли для явной транзакции BEGIN TRANSACTION или ROLLBACK TRANSACTION не существует. Если код обнаруживает нарушение бизнес-правила, оно может завершаться блока atomic hello с [THROW](http://msdn.microsoft.com/library/ee677615.aspx) инструкции.

### <a name="typical-create-procedure-for-natively-compiled"></a>Стандартная инструкция CREATE PROCEDURE для создания скомпилированных в собственном коде процедур
Обычно hello T-SQL toocreate скомпилированной хранимой процедуры — примерно toohello следующий шаблон:

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* Для hello TRANSACTION_ISOLATION_LEVEL моментального СНИМКА является наиболее распространенные значение hello скомпилированные в собственном коде хранимые процедуры hello. Однако подмножество hello других поддерживаются значения:
  
  * REPEATABLE READ;
  * SERIALIZABLE.
* Hello значение языка должен присутствовать в представлении sys.languages hello.

### <a name="how-toomigrate-a-stored-procedure"></a>Как toomigrate хранимой процедуры
Hello миграции, необходимо:

1. Получите hello CREATE PROCEDURE сценария toohello обычных интерпретируемых хранимых процедур.
2. Перепишите его toomatch заголовок hello предыдущего шаблона.
3. Проверить, использует ли hello хранимой процедуры код T-SQL любых компонентов, которые не поддерживаются для хранимых процедур, скомпилированных в собственном коде. При необходимости устраните эту проблему.
   
   * Дополнительные сведения см. в статье [Проблемы миграции, связанные с хранимыми процедурами, скомпилированными в собственном коде](http://msdn.microsoft.com/library/dn296678.aspx).
4. С помощью хранимой процедуры SP_RENAME переименуйте hello старую хранимую процедуру. Или просто удалите ее с помощью DROP.
5. Запустите измененный сценарий T-SQL CREATE PROCEDURE.

## <a name="step-6-run-your-workload-in-test"></a>Шаг 6. Запуск рабочей нагрузки в тестовой среде
Запустите рабочую нагрузку в тестовой базы данных, аналогичные toohello рабочая нагрузка, которая выполняется в вашей рабочей базы данных. Должна помочь определить hello выигрыш в производительности достигается путем использования функции hello в памяти для таблиц и хранимых процедур.

Основные атрибуты hello рабочей нагрузки являются:

* количество одновременных подключений;
* отношение количества операций чтения и записи.

tootailor и выполнения hello тестовую рабочую нагрузку, рассмотрите возможность использования средства под рукой ostress.exe hello, которое показано в [здесь](sql-database-in-memory.md).

toominimize задержку в сети и выполнить тест в hello же Azure географическом регионе, где существует hello базы данных.

## <a name="step-7-post-implementation-monitoring"></a>Шаг 7. Мониторинг после реализации
Рассмотрим наблюдения за эффекты производительности hello реализации в памяти в рабочей среде.

* [Мониторинг хранилища In-Memory](sql-database-in-memory-oltp-monitoring.md).
* [Мониторинг базы данных SQL Azure с помощью динамических представлений управления](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Связанные ссылки
* [In-Memory OLTP (оптимизация в памяти)](http://msdn.microsoft.com/library/dn133186.aspx)
* [Введение tooNatively хранимых процедур, скомпилированных](http://msdn.microsoft.com/library/dn133184.aspx)
* [Помощник по оптимизации памяти](http://msdn.microsoft.com/library/dn284308.aspx)

