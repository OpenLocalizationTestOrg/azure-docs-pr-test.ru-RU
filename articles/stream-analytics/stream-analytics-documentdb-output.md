---
title: "выходные данные aaaJSON для Stream Analytics | Документы Microsoft"
description: "Сведения о том, каким образом Stream Analytics направляет данные из Azure Cosmos DB в формат JSON и позволяет архивировать данные и уменьшать задержки запросов в отношении неструктурированных данных JSON."
keywords: "Выходные данные JSON"
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Направление Azure Cosmos DB из Stream Analytics в формат JSON
Stream Analytics позволяет направлять данные из [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) в формат JSON, позволяя архивировать данные и уменьшать задержки запросов в отношении неструктурированных данных JSON. В этом документе представлены некоторые рекомендации по реализации данной конфигурации.

Для тех, кто не знаком с Cosmos DB, взгляните на [план обучения Azure Cosmos DB](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget работы. 

Примечание. Коллекции Cosmos DB, использующие API-интерфейсы Mongo DB, пока не поддерживаются. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>Основные сведения о Cosmos DB как объекте вывода данных
Hello Azure Cosmos DB выходные данные в Stream Analytics включает записи потока обработки результатов в качестве выходных данных JSON в вашей Cosmos DB коллекций. Stream Analytics не создавать коллекции в базе данных, вместо необходимости toocreate их заранее. Это так, чтобы hello выставления счетов затраты коллекций Cosmos DB прозрачный tooyou и hello, можно настроить производительность hello, согласованности и емкость непосредственно с помощью коллекций [API-интерфейсы DB Cosmos](https://msdn.microsoft.com/library/azure/dn781481.aspx). Рекомендуется использовать одну базу данных DB Cosmos каждого отдельного toologically задания потоковой передачи коллекций для потокового задания.

Ниже описаны некоторые из параметров коллекции Cosmos DB hello.

## <a name="tune-consistency-availability-and-latency"></a>Настройка согласованности, доступности и задержки
toomatch требований приложения Cosmos DB позволяет toofine настраивать hello база данных коллекций и сделать компромисс между согласованности, доступность и задержки. В зависимости от того, какие уровни согласованности чтения потребуются вашему сценарию для чтения и записи задержки, вы можете выбирать уровень согласованности в своей учетной записи базы данных. По умолчанию Cosmos DB позволяет синхронной индексирования в каждой коллекции tooyour операции CRUD. Это другой параметр полезно toocontrol hello чтения/записи производительности в базу данных, Cosmos. Сведения по этой теме можно найти hello [изменить уровни согласованности вашей базы данных и запрос](../documentdb/documentdb-consistency-levels.md) статьи.

## <a name="upserts-from-stream-analytics"></a>Вставка и обновление Upsert в Stream Analytics
Stream Analytics интеграция с Cosmos DB позволяет tooinsert или обновления записей в Cosmos DB коллекции на основе данного столбца Идентификаторов документов. Это также назывались tooas *Upsert*.

Stream Analytics использует оптимистичный подход Upsert, где обновления только выполняется, когда операция вставки завершается неудачно из-за конфликта tooa идентификатор документа. Это обновление выполняется Stream Analytics как обновления, поэтому он позволяет частичных обновлений toohello документа, т. е. Добавление новых свойств или замены существующего свойства выполняется последовательно. Обратите внимание, что изменения в значения свойств массива в документе JSON hello привести ко всему массиву hello перезаписаны начало массива hello т. е. не объединяются.

## <a name="data-partitioning-in-cosmos-db"></a>Секционирование данных в Cosmos DB
Cosmos DB [секционированных коллекций](../cosmos-db/partition-data.md) являются hello рекомендованный подход для секционирования данных. 

Для одной коллекции Cosmos DB Stream Analytics по-прежнему можно toopartition данных основании шаблонов запросов hello и требованиям к производительности приложения. Каждая коллекция может содержать вверх too10GB данных (максимум) и в настоящее время нет не tooscale способом копирования (или переполнение) коллекции. Для горизонтального масштабирования, Stream Analytics позволяет toowrite toomultiple коллекции с заданным префиксом (см. сведения об использовании ниже). Stream Analytics использует согласованные hello [распознавателя раздела хэш](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) стратегию на основе пользовательского hello предоставленный toopartition столбца PartitionKey ее записи выходных данных. Hello количество коллекций с hello, предоставленных во время запуска задания потоковой передачи hello префикс используется в качестве количество разделов выходного hello, задание hello toowhich записывает параллельного tooin (коллекции Cosmos DB = секций выходных данных). Можно предположить, что для одной коллекции с отложенным индексированием, в которой выполняются только операции вставки, пропускная способность записи составит приблизительно 0,4 МБ/с. Используется несколько коллекций можно разрешить, вы tooachieve более высокую пропускную способность и расширенные возможности.

Если количество разделов tooincrease hello в будущем hello, может потребоваться toostop должностных обязанностей, repartition hello данные из существующих коллекций в новые коллекции, а затем перезапустите задание Stream Analytics hello. В следующую публикацию будут включены дополнительные сведения об использовании PartitionResolver и перераспределении, а также образец программного кода. статья Hello [секционирование и масштабирование в Cosmos DB](../documentdb/documentdb-partition-data.md) также предоставляет подробные сведения об этом.

## <a name="cosmos-db-settings-for-json-output"></a>Параметры Cosmos DB для выходных данных JSON
При создании Cosmos DB как средства обработки выходных данных в Stream Analytics создается запрос информации, показанный ниже. В этом разделе объясняется hello определения свойства.

Секционированная коллекция | Несколько односекционных коллекций
---|---
![экран выходных данных documentdb stream analytics](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![экран выходных данных documentdb stream analytics](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> Hello **несколько коллекций «Одна секция»** сценария требуется ключ секции и поддерживаемой конфигурацией. 

* **Псевдоним вывода** — псевдоним toorefer эти выходные данные в запросе ASA  
* **Имя учетной записи** — имя hello или конечной точки URI hello Cosmos DB учетной записи.  
* **Ключ учетной записи** — hello общий ключ доступа для hello Cosmos DB учетной записи.  
* **База данных** — имя базы данных Cosmos DB hello.  
* **Шаблон имени коллекции** — имя коллекции hello или их шаблон для hello коллекций toobe используется. формат имени коллекции Hello могут создаваться с помощью hello необязательного токена {partition}, где отсчет разделов начинается с 0. Далее приведены примеры допустимых входных данных:  
  1\) MyCollection — должна существовать одна коллекция с именем MyCollection;  
  2\) MyCollection{partition} — должны существовать такие коллекции: MyCollection0, MyCollection1, MyCollection2 и т. д.  
* **Partition Key** — необязательно. Требуется, только если в шаблоне имени коллекции используется маркер {partition}. Имя Hello hello поля в выходных данных событий, которые используются toospecify hello ключа выходных данных секционирования в коллекциях. Для выходных данных одной коллекции можно использовать любой столбец произвольных выходных данных, например PartitionId.  
* **Document ID** — необязательно. Имя Hello hello поля в исходящих событиях, используемое toospecify hello первичный ключ на какие insert или update основаны операции.  
