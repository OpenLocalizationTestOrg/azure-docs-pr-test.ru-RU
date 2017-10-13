---
title: "Запросы к сегментированным базам данных SQL Azure | Документация Майкрософт"
description: "Выполнение запросов по сегментам с использованием клиентской библиотеки эластичной базы данных."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: 67bcb3c7fe33341103f28bc70e8cc2acbb924cae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="multi-shard-querying"></a>Многосегментное формирование запросов
## <a name="overview"></a>Обзор
[Средства работы с эластичными базами данных](sql-database-elastic-scale-introduction.md)позволяют создавать решения сегментированных баз данных. **Многосегментное формирование запросов** используется для таких задач, как сбор данных и создание отчетов, требующих запуска запроса, распространяющегося на несколько сегментов. (Сравните с [маршрутизацией, зависящей от данных](sql-database-elastic-scale-data-dependent-routing.md), когда все действия выполняются в пределах одного сегмента.) 

1. Получение [**RangeShardMap**](https://msdn.microsoft.com/library/azure/dn807318.aspx) или [**ListShardMap**](https://msdn.microsoft.com/library/azure/dn807370.aspx) с помощью методов [**TryGetRangeShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), [**TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) или [**GetShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx). См. раздел [**Создание объекта ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) и [**Получение RangeShardMap или ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Создание объекта **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**.
3. Создание **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Задание для **[свойства CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)** команды T-SQL.
5. Выполнение команды путем вызова **[метода ExecuteReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Просмотр результатов с помощью **[класса MultiShardDataReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Пример
В следующем примере кода показано применение многосегментного формирования запросов с использованием заданного сопоставления **ShardMap** с именем *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


Основное различие состоит в построении многосегментных подключений. Если **SqlConnection** действует для отдельной базы данных, то **MultiShardConnection** принимает в качестве входных данных ***коллекцию сегментов***. Коллекция сегментов заполняется из карты сегментов. Затем выполняется запрос для коллекции сегментов с использованием семантики **UNION ALL** для формирования общего результата. При необходимости к выходным данным можно добавить имя сегмента, из которого поступает строка, используя свойство **ExecutionOptions** команды. 

Обратите внимание на вызов **myShardMap.GetShards()**. С помощью этого метода все сегменты извлекаются из карты сегментов, и обеспечивается простой способ выполнения запроса по всем соответствующим базам данных. Коллекцию сегментов для многосегментного запроса можно дополнительно ограничить, выполнив запрос LINQ к коллекции, полученной в результате вызова **myShardMap.GetShards()**. Эта возможность в многосегментном формировании запросов, в сочетании с политикой частичных результатов, разработана для применения к сегментам в количестве от десятков до сотен.

В настоящий момент существует ограничение для многосегментного формирования запросов, состоящее в отсутствии проверки для сегментов и шардлетов, к которым обращен запрос. Если при маршрутизации, зависящей от данных, выполняется проверка того, что указанный сегмент является частью карты сегментов на момент выполнения запроса, то при многосегментном формировании запросов такая проверка не происходит. Это может привести к тому, что многосегментные запросы будут обращаться к базам данных, удаленным из карты сегментов.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Многосегментные запросы и операции разбиения-слияния
При многосегментных запросах не выполняется проверка на участие шардлетов из запрашиваемой базы данных в операциях разбиения или слияния. (См. статью [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md).) Это может привести к несогласованности, когда строки одного шардлета отображаются для нескольких баз данных в одном многосегментном запросе. Следует учитывать эти ограничения, фильтрование текущих операций разбиения или слияния, а также изменения сопоставления сегментов при выполнении многосегментных запросов.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Дополнительные материалы
Классы и методы **[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**.

Управление сегментами с использованием [клиентской библиотеки эластичной базы данных](sql-database-elastic-database-client-library.md). Она включает в себя новое пространство имен с именем [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx), предоставляющее возможность выполнять запрос к нескольким сегментам, используя один запрос и один результат. Это позволяет абстрагировать обработку запросов по набору сегментов. Также предоставляются альтернативные политики выполнения, в особенности частичные результаты для обработки сбоев при выполнении запросов по нескольким сегментам.  

