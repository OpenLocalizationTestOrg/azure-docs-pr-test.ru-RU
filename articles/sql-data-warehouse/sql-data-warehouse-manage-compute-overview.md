---
title: "aaaManage вычислительная мощность в хранилище данных SQL Azure (Обзор) | Документы Microsoft"
description: "Возможности масштабирования производительности в хранилище данных SQL Azure. Горизонтальное масштабирование, перемещая Dwu или приостанавливать и возобновлять toosave затраты вычислительных ресурсов."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>Управление вычислительными ресурсами в хранилище данных SQL Azure (обзор)
> [!div class="op_single_selector"]
> * [Обзор](sql-data-warehouse-manage-compute-overview.md)
> * [Портал](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

Hello архитектура хранилища данных SQL отделяет хранилища и вычислений, позволяя каждого tooscale независимо друг от друга. В результате вычислений может быть требований к производительности масштабированный toomeet независимо от hello объем данных. При такой архитектуре [выставление счетов][billed] за ресурсы вычисления и хранения осуществляется отдельно. 

В этом обзоре описываются как горизонтальное масштабирование работает с хранилищем данных SQL и как tooutilize hello приостановки, возобновления и возможности масштабирования хранилища данных SQL. Обратитесь к hello [единицы (Dwu) в хранилище данных] [ data warehouse units (DWUs)] toolearn страницы, как связаны Dwu и производительности. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>Как работают операции управления вычислениями в хранилище данных SQL
Архитектура Hello для хранилища данных SQL состоит из узла управления, вычислительных узлов и hello распределяться 60 распределения уровня хранилища. 

Во время обычной активного сеанса в хранилище данных SQL головной узел системы управляет метаданными hello и содержит оптимизатор hello распределенных запросов. Вычислительные узлы и уровень хранилища размещены под головным узлом. 400 DWU в системе установлены одного головного узла, четыре вычислительных узлов и уровень хранилища hello, состоящий из 60 распределения. 

Когда быть тщательно проанализирован на шкале или приостанавливать операции, система hello сначала разрывает все входящие запросы и откатывает транзакции tooensure согласованное состояние. Операции масштабирования можно выполнить только после завершения отката транзакций. Для операции масштабирования Подготовка системы hello hello лишние нужное количество вычислительных узлов и затем начинает повторное присоединение слой hello вычислительных узлов toohello хранилища. Для операции уменьшения масштаба hello ненужные узлы освобождаются и hello оставшиеся вычислительные узлы заново присоединить сами toohello соответствующего числа распределений. Для операции приостановки все вычислительные узлы выпущены и системы подвергнется разнообразные операции tooleave метаданных окончательного системы в устойчивом состоянии.

| DWU  | \# вычислительных узлов | \# распределений на узел |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4.                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1200 | 12                 | 5                            |
| 1500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

Hello три основные функции управления вычислений —:

1. Приостановить
2. Продолжить
3. Масштаб

Каждый из этих операций может занять несколько минут toocomplete. Если масштабирование или приостановка и возобновление работы автоматически, вы можете tooimplement логику tooensure что некоторые операции были завершены перед выполнением другого действия. 

Проверка состояния базы данных hello через различные конечные точки можно toocorrectly реализация автоматизации таких операций. Hello портал предоставляет уведомление о завершении операции и hello базы данных текущее состояние, но не допускает программный о проверке состояния. 

>  [!NOTE]
>
>  Функцию управления вычислениями можно выполнять не для всех конечных точек.
>
>  

|              | Приостановка и возобновление | Масштаб | Проверка состояния базы данных |
| ------------ | ------------ | ----- | -------------------- |
| Портал Azure | Да          | Да   | **Нет**               |
| PowerShell   | Да          | Да   | Да                  |
| Интерфейс REST API     | Да          | Да   | Да                  |
| T-SQL        | **Нет**       | Да   | Да                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Масштабирование вычислительных ресурсов

Производительность в хранилище данных SQL измеряется в [единицах использования хранилища данных (DWU)][data warehouse units (DWUs)], которые являются абстрактной мерой вычислительных ресурсов, таких как ЦП, память и пропускная способность ввода-вывода. Пользователь, который хотел tooscale производительность свои системы можно сделать различными способами, например через портал hello, T-SQL и API-интерфейс REST. 

### <a name="how-do-i-scale-compute"></a>Как масштабировать вычислительные ресурсы
Вычислительной мощности осуществляется хранилище данных SQL путем изменения параметра DWU hello. При добавлении дополнительных DWU для некоторых операций производительность будет повышаться [линейно][linearly].  Мы разработали предложения DWU, благодаря которым ваша производительность заметно изменится при уменьшении или увеличении масштаба системы. 

tooadjust Dwu, можно использовать любой из этих отдельных методов.

* [Масштабирование вычислительных ресурсов с помощью портала Azure][Scale compute power with Azure portal]
* [Масштабирование вычислительных ресурсов с помощью PowerShell][Scale compute power with PowerShell]
* [Масштабирование вычислительных ресурсов с помощью REST API][Scale compute power with REST APIs]
* [Масштабирование вычислительных ресурсов с помощью TSQL][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>Сколько DWU нужно использовать

toounderstand является какие вашей оптимальное значение DWU, попробуйте масштабирование вверх и вниз, а запустить несколько запросов после загрузки данных. Так как масштабирование выполняется достаточно быстро, попробуйте использовать разные уровни производительности не дольше одного часа. 

> [!Note] 
> Хранилище данных SQL — спроектированный tooprocess больших объемов данных. toosee истинные возможности масштабирования, особенно в больших Dwu требуется toouse большой набор данных, который достигает или превышает 1 ТБ.

Рекомендации при поиске hello наиболее DWU для рабочей нагрузки:

1. Если хранилище данных только создается, начните с небольшого уровня производительности, обеспечиваемого DWU.  В качестве отправной точки можно использовать DW400 или DW200.
2. Отслеживать производительность приложений, наблюдая hello число выбранных Dwu по сравнению toohello производительности, которые вы заметили.
3. Определяет, насколько снизится производительность быстрее или медленнее, должна быть вы tooreach hello оптимальный уровень производительности требований, предполагая, что линейной шкалы.
4. Увеличьте или уменьшите число hello Dwu в toohow пропорции гораздо быстрее или медленнее, которую должна tooperform вашей рабочей нагрузки. 
5. Вносите изменения, пока не достигнете уровня производительности, который оптимально отвечает вашим бизнес-требованиям.

> [!NOTE]
>
> Производительность запросов увеличивается только с дополнительные параллелизации, если hello работы могут быть разделены вычислительных узлов. Если обнаружится, что масштабирование не меняет его производительности, проверьте out наши статьи toocheck ли ваш данные распределяются неравномерно или представили большой объем перемещения данных с настройкой производительности. 

### <a name="when-should-i-scale-dwus"></a>Когда следует масштабировать DWU
Масштабирование Dwu изменяет hello следующие обстоятельства:

1. Линейно изменения производительности системы hello для сканирования, статистические выражения и операторы CTAS
2. При увеличении числа hello средств чтения и записи при загрузке с помощью PolyBase
3. Максимальное количество параллельных запросов и слотов выдачи.

Рекомендации по tooscale Dwu:

1. Прежде чем выполнять ресурсоемкую загрузку данных или их преобразование, увеличьте объем DWU, чтобы быстрее получать доступ к данным.
2. Рабочее время масштабируйте tooaccommodate большое количество параллельных запросов. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Приостановка работы вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause базы данных, используйте любой из этих отдельные методы.

* [Приостановка работы вычислительных ресурсов с помощью портала Azure][Pause compute with Azure portal]
* [Приостановка работы вычислительных ресурсов с помощью PowerShell][Pause compute with PowerShell]
* [Приостановка работы вычислительных ресурсов с помощью REST API][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Возобновление работы вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume базы данных, используйте любой из этих отдельные методы.

* [Возобновление работы вычислительных ресурсов с помощью портала Azure][Resume compute with Azure portal]
* [Возобновление работы вычислительных ресурсов с помощью PowerShell][Resume compute with PowerShell]
* [Возобновление работы вычислительных ресурсов с помощью REST API][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>Проверка состояния базы данных 

tooresume базы данных, используйте любой из этих отдельные методы.

- [проверка состояния базы данных с помощью T-SQL;][Check database state with T-SQL]
- [проверка состояния базы данных с помощью PowerShell;][Check database state with PowerShell]
- [проверка состояния базы данных с помощью REST API.][Check database state with REST APIs]

## <a name="permissions"></a>Разрешения

Масштабирования hello база данных требует hello разрешениями, описанными в [инструкции ALTER DATABASE][ALTER DATABASE].  Приостановка и возобновление требуют hello [участника базы данных SQL] [ SQL DB Contributor] разрешение, в частности Microsoft.Sql/servers/databases/action.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Дальнейшие действия
См. следующие статьи toohelp вы понимаете такие концепции некоторые дополнительные производительности toohello:

* [Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Workload and concurrency management]
* [Общие сведения о таблицах в хранилище данных SQL][Table design overview]
* [Распределение таблиц в хранилище данных SQL][Table distribution]
* [Indexing tables in SQL Data Warehouse (Индексирование таблиц в хранилище данных SQL)][Table indexing]
* [Секционирование таблиц в хранилище данных SQL][Table partitioning]
* [Управление статистикой таблиц в хранилище данных SQL][Table statistics]
* [Рекомендации по использованию хранилища данных SQL Azure][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
