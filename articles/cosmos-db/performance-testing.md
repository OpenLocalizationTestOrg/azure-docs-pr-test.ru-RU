---
title: "aaaAzure Cosmos DB шкала и тестирование производительности | Документы Microsoft"
description: "Узнайте, как масштабировать tooperform и тестирование производительности с помощью Azure Cosmos DB"
keywords: "тестирование производительности"
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Проверка производительности и масштабирования с помощью Azure Cosmos DB
Проверка производительности и масштабирования — ключевой этап в разработке приложения. Для многих приложений уровня базы данных hello оказывает существенное влияние hello общей производительности и масштабируемости и является таким образом это важная составляющая производительности тестирования. Система [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) разработана с расчетом на эластичное масштабирование и предсказуемую производительность. Поэтому она отлично подходит для приложений, требующих высокую производительность для уровня базы данных. 

Эта статья предназначена для специалистов, разрабатывающих наборы тестов производительности для рабочих нагрузок Cosmos DB или оценивающих Cosmos DB для сценариев с высокопроизводительными приложениями. В основном ориентировано на тестирование производительности изолированной hello базы данных, но также содержит рекомендации для производственных приложений.

После считывания в этой статье, можно будет tooanswer hello следующие вопросы:   

* Где найти образец клиентского приложения .NET для проверки производительности Azure Cosmos DB? 
* Как добиться высокой пропускной способности с помощью Cosmos DB из клиентского приложения?

tooget к выполнению кода, загрузите проект hello из [пример тестирование Azure Cosmos DB производительности](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> Задача Hello этого приложения — toodemonstrate советы и рекомендации для извлечения более высокую производительность за пределы Cosmos DB с небольшим числом клиентских машин. Это не была сделана пиковую hello toodemonstrate hello службы, которая позволяет масштабировать limitlessly.
> 
> 

Если вы ищете tooimprove параметры конфигурации клиента Cosmos DB производительности, см. раздел [советы по повышению производительности базы данных Azure Cosmos](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Запустите приложение тестирования производительности, hello
Здравствуйте, tooget быстрый способ работы — toocompile и образец hello выполнения .NET ниже, как описано в шагах hello ниже. Также можно просмотреть исходный код hello и реализовать аналогичный конфигураций tooyour собственные клиентские приложения.

**Шаг 1.** загрузка hello проект из [пример тестирование Azure Cosmos DB производительности](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), или репозитория GitHub hello вилки.

**Шаг 2.** изменения параметров hello EndpointUrl, AuthorizationKey, CollectionThroughput и DocumentTemplate (необязательно) в файле App.config.

> [!NOTE]
> Перед подготовкой коллекции с высокой пропускной способностью, можно найти toohello [цены](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello затраты на коллекции. Azure Cosmos DB выставляет счет за хранение и пропускную способность независимо друг от друга на почасовой основе затрат можно сохранить, удалив или понизить пропускную способность hello вашей коллекции Azure Cosmos DB после тестирования.
> 
> 

**Шаг 3.** скомпилировать и запустить консольное приложение hello из командной строки hello. Вы должны увидеть результаты hello следующим образом:

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**Шаг 4 (при необходимости):** hello пропускная способность сообщил (единиц Запросов в секунду) из средства hello должен быть hello же или более поздней версии, чем пропускная способность hello hello коллекции. В противном случае возрастающей hello DegreeOfParallelism небольшими шагами могут помочь в достижении предела hello. Plateaus пропускной способности hello из клиентского приложения, запуск нескольких экземпляров приложения hello на hello таким же или разными компьютерами поможет достигнуто hello подготовить через hello различных экземпляров. Если требуется помощь на этом этапе, напишите сообщение электронной почты tooaskcosmosdb@microsoft.com или файл запрос в службу поддержки hello [портала Azure](https://portal.azure.com).

После выполнения приложения hello, можно попробовать другой [политики индексирования](indexing-policies.md) и [уровни согласованности](consistency-levels.md) toounderstand их влияние на пропускной способности и задержки. Также можно просмотреть исходный код hello и реализовать аналогичный конфигураций tooyour собственные наборы или приложений в производственной среде.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье мы рассмотрели способы тестирования производительности и масштабируемости с помощью консольного приложения .NET Cosmos DB. Дополнительные сведения о работе с Azure Cosmos DB см. ниже toohello ссылки.

* [Пример для тестирования производительности Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Tooimprove параметры конфигурации клиента Azure Cosmos DB производительности](performance-tips.md)
* [Секционирование, ключи секции и масштабирование в Azure Cosmos DB](partition-data.md)


