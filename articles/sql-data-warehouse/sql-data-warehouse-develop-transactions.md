---
title: "aaaTransactions в хранилище данных SQL | Документы Microsoft"
description: "Советы по реализации транзакций Transact-SQL в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>Транзакции в хранилище данных SQL
Как и следовало ожидать, хранилище данных SQL поддерживает транзакции, как часть загрузки хранилища данных hello. Однако tooensure hello производительности хранилища данных SQL поддерживается в масштабе, некоторые функции будут ограничены при сравниваемых tooSQL сервера. В этой статье указаны различия hello и списки hello другим пользователям. 

## <a name="transaction-isolation-levels"></a>Уровни изоляции транзакций
Хранилище данных SQL реализует транзакции ACID. Однако hello изоляции транзакций поддержки hello ограничено слишком`READ UNCOMMITTED` и его изменить нельзя. Можно реализовать несколько методов кодирования, которые считывает tooprevent "грязных" данных, в случае серьезной проблемой. Hello наиболее популярных методов использовать как CTAS и переключения секций таблицы (часто называемом hello шаблон скользящего окна) пользователям tooprevent выполнение запросов к данным по-прежнему идет подготовка. Представления hello предварительную фильтрацию данных также является популярным подходом.  

## <a name="transaction-size"></a>Размер транзакции
Размер одной транзакции, изменяющей данные, ограничен. ограничение Hello сегодня применяется «по распространения». Таким образом можно вычислить общее выделение hello путем умножения hello ограничение на число распределения hello. tooapproximate hello максимальное число строк в транзакции hello разделите cap распространения hello hello общий размер каждой строки. Для столбцов переменной длины, рассмотрите возможность создания является длина столбца среднее, а не с помощью hello максимальный размер.

Hello таблицы ниже hello были сделаны следующие допущения:

* выполнено равномерное распределение данных; 
* Hello Средняя длина строки составляет 250 байт

| [DWU][DWU] | Ограничение распределения (ГиБ) | Число распределений | Максимальный размер транзакции (ГиБ) | # Строк на распространения | Максимальное число строк на транзакцию |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4 000 000 |240 000 000 |
| DW200 |1.5 |60 |90 |6 000 000 |360 000 000 |
| DW300 |2.25 |60 |135 |9 000 000 |540 000 000 |
| DW400 |3 |60 |180 |12 000 000 |720 000 000 |
| DW500 |3,75 |60 |225 |15 000 000 |900 000 000 |
| DW600 |4.5. |60 |270 |18 000 000 |1 080 000 000 |
| DW1000 |7.5 |60 |450 |30 000 000 |1 800 000 000 |
| DW1200 |9 |60 |540 |36 000 000 |2 160 000 000 |
| DW1500 |11,25 |60 |675 |45 000 000 |2 700 000 000 |
| DW2000 |15 |60 |900 |60 000 000 |3 600 000 000 |
| DW3000 |22,5 |60 |1350 |90 000 000 |5 400 000 000 |
| DW6000 |45 |60 |2700 |180 000 000 |10 800 000 000 |

Ограничение размера транзакции Hello применяется по операции или операции. Оно не применяется к совокупности параллельных транзакций. Поэтому каждая транзакция не допускается toowrite такой объем данных журнала toohello. 

toooptimize и свести к минимуму объем hello данные, записанные в журнал toohello можно найти toohello [транзакций рекомендации] [ Transactions best practices] статьи.

> [!WARNING]
> Максимальный размер транзакций могут быть осуществлены только для ХЭШИРОВАНИЯ или ROUND_ROBIN распределенных таблиц, где распространяться hello hello данных Hello является четным. Если hello транзакции записывает данные в виде асимметричные toohello распределения затем hello ограничен скорее всего toobe достигла размера предыдущих toohello максимальное транзакции.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>Состояние транзакции
Хранилище данных SQL использует tooreport функции hello XACT_STATE() поврежденную транзакцию, используя hello значение -2. Это означает, что транзакции hello произошел сбой и помечен только для отката

> [!NOTE]
> Hello использовать-2, toodenote Функция XACT_STATE hello tooSQL другое поведение представляет поврежденную транзакцию сервера. SQL Server использует значение -1 hello toorepresent нефиксируемой транзакции. SQL Server может выдержать некоторые ошибки внутри транзакции без обращения toobe помечен как нефиксируемой. Например, `SELECT 1/0` вызовет ошибку, но не приведет к переходу транзакции в состояние нефиксируемой. SQL Server также позволяет считывает hello нефиксируемой транзакции. Тем не менее хранилище данных SQL не позволяет это сделать. При возникновении ошибки в ходе транзакции, хранилище данных SQL автоматически перейдет в состояние hello -2 и не будет возможности toomake любые дополнительные инструкции select пока не будет выполнен откат инструкции hello. Вот почему важно toocheck, что toosee код вашего приложения, если она использует XACT_STATE(), что вы может потребовать изменения в код toomake.
> 
> 

Например, в SQL Server можно увидеть транзакцию следующего вида.

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Если оставить код как выше вы получите hello следующие сообщение об ошибке:

Msg 111233, уровень 16, состояние 1, строка 1 111233; hello текущих транзакция была прервана, и все ожидающие изменения, был выполнен откат. Причина: для транзакции в состоянии "только откат" не был выполнен явный откат перед инструкцией DDL, DML или SELECT.

Также не будет hello вывода hello ошибку_ * функций.

В хранилище данных SQL кода hello должно toobe немного изменены:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Hello ожидается, что теперь соблюдается режим работы. Ошибка Hello в транзакции hello осуществляется и hello ошибку_ * функции предоставляют значения, как ожидалось.

Все, что изменилось — что hello `ROLLBACK` из hello транзакции имела toohappen до чтения hello hello сведения об ошибках в hello `CATCH` блока.

## <a name="errorline-function"></a>Функция Error_Line()
Это также Обратите внимание, хранилище данных SQL не реализации поддержки функция ERROR_LINE() hello. Если у вас есть это в коде необходимо будет tooremove его toobe, совместимый с хранилищем данных SQL. Вместо этого используйте запрос метки в коде tooimplement эквивалентную функциональность. См. toohello [МЕТКА] [ LABEL] Дополнительные сведения о данной функции.

## <a name="using-throw-and-raiserror"></a>Использование THROW и RAISERROR
THROW — hello более современные реализацию для вызова исключения в хранилище данных SQL, но также поддерживается RAISERROR. Существует несколько различий, которые стоит рассмотреть обращая внимания toohowever.

* Определяемые пользователем сообщения об ошибках номера не может быть в hello 150 000 100 000 диапазона для THROW
* Номера сообщений об ошибках RAISERROR не должны превышать 50 000.
* Не поддерживается использование sys.messages.

## <a name="limitiations"></a>Ограничения
Хранилище данных SQL имеет несколько ограничений, которые связаны tootransactions.

Вот они:

* не поддерживаются распределенные транзакции;
* вложенные транзакции не разрешены;
* не допускается точки сохранения.
* не допускаются именованные транзакции;
* не допускаются помеченные транзакции;
* не поддерживаются операторы DDL, такие как `CREATE TABLE` , внутри определенной пользователем транзакции.

## <a name="next-steps"></a>Дальнейшие действия
toolearn более об оптимизации операций, в разделе [транзакций рекомендации][Transactions best practices].  toolearn другие хранилища данных SQL советы и рекомендации, в разделе [рекомендации по хранилищу данных SQL][SQL Data Warehouse best practices].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
