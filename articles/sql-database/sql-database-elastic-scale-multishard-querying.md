---
title: "aaaQuery сегментированных баз данных Azure SQL | Документы Microsoft"
description: "Выполнение запросов по сегментам с помощью клиентской библиотеки hello эластичной базы данных."
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
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Многосегментное формирование запросов
## <a name="overview"></a>Обзор
С hello [эластичной базы данных средства](sql-database-elastic-scale-introduction.md), можно создать сегментированных баз данных. **Многосегментное формирование запросов** используется для таких задач, как сбор данных и создание отчетов, требующих запуска запроса, распространяющегося на несколько сегментов. (Сравните это слишком[маршрутизации в зависимости от данных](sql-database-elastic-scale-data-dependent-routing.md), который выполняет всю работу в одном сегменте.) 

1. Получить [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) или [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) с помощью hello [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), или hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) метод. См. раздел [**Создание объекта ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) и [**Получение RangeShardMap или ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Создание объекта **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**.
3. Создание **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Набор hello  **[свойства CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa команды T-SQL.
5. Выполните команду hello, вызывающему Привет  **[метод ExecuteReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Просмотр результатов hello, с помощью hello  **[класса MultiShardDataReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Пример
Hello следующий код иллюстрирует использование hello нескольких сегментов и выполнение запросов с помощью заданного **ShardMap** с именем *myShardMap*. 

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


Ключевое различие — построение hello соединений нескольких сегментов. Где **SqlConnection** работает с одной базой данных, hello **MultiShardConnection** принимает ***коллекции сегментов*** качестве входных данных. Заполнение коллекции hello сегментов из карты сегментов. Hello запрос выполняется на hello коллекцию сегментов с помощью **UNION ALL** семантику tooassemble общий результат. При необходимости hello сегментов hello и происхождения строку hello можно добавлять имя выходных данных с помощью hello toohello **ExecutionOptions** свойство команды. 

Обратите внимание на вызов hello слишком**myShardMap.GetShards()**. Этот метод извлекает все сегменты из карты сегментов hello и предоставляет простой способ toorun запрос всех соответствующих баз данных. Hello коллекции сегментов для запроса нескольких сегментов можно более точно распределить ресурсы дальнейшей, выполняя LINQ запрос коллекции hello, возвращенный вызовом hello слишком**myShardMap.GetShards()**. В сочетании с политикой hello частичные результаты текущего возможность hello в запросе нескольких сегментов был спроектированный toowork подходит для десятков вверх toohundreds сегментов.

Ограничением с запросами нескольких сегментов в настоящее время является отсутствие проверки для сегменты и Подсегменты, получат hello. При маршрутизации в зависимости от данных проверяет, является ли данный сегмент часть карты сегментов hello во время hello запросов, запросов нескольких сегментов не выполняется проверка. Это может привести к toomulti сегментов запросы, выполняемые в базах данных, которые были удалены из карты сегментов hello.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Многосегментные запросы и операции разбиения-слияния
Запросы нескольких сегментов не проверять ли подсегментов в запрашиваемой базе данных hello участвуют в ходе эксплуатации разделения слияния. (См. [масштабирования с помощью средства hello разделения эластичной базы данных-слияния](sql-database-elastic-scale-overview-split-and-merge.md).) Это может привести tooinconsistencies где строки из hello же презентации подсегмента для нескольких баз данных в hello того же запроса нескольких сегментов. Следует учитывать эти ограничения и примите к сведению очисткой текущих разделения слияния операции и изменения toohello карта сегментов при выполнении запросов нескольких сегментов.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>См. также
Классы и методы **[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**.

Управление с помощью hello сегментов [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md). Включает в себя пространство имен с именем [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) , предоставляющий возможности tooquery hello несколько сегментов с помощью одного запроса и результатов. Это позволяет абстрагировать обработку запросов по набору сегментов. Он также предоставляет альтернативные выполнения политики, в частности частичные результаты, toodeal со сбоями при выполнении запросов через много сегментов.  

