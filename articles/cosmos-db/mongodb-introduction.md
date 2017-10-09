---
title: "Введение tooAzure Cosmos DB: API для MongoDB | Документы Microsoft"
description: "Дополнительные сведения об использовании toostore Azure Cosmos DB и API-интерфейсы для популярных OSS MongoDB hello значительных объемов документы JSON с небольшой задержкой, с помощью запроса."
keywords: "что такое MongoDB"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Введение tooAzure Cosmos DB: API для MongoDB

[Azure Cosmos DB](../cosmos-db/introduction.md) — это глобально распределенная, многомодельная служба базы данных Майкрософт, необходимая для работы с критически важными приложениями. Azure Cosmos DB предоставляет [под ключ глобального распространения](distribute-data-globally.md), [гибкое Масштабирование пропускной способности и хранения](partition-data.md) задержки по всему миру, десяти миллисекунды в 99-й процентиль hello, [пять хорошо определенные уровни согласованности](consistency-levels.md)и гарантировать высокий уровень доступности, все сохраненные по [отрасли соглашений об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [автоматически индексирует данных](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) без необходимости toodeal с управлением схемы и индекса. Так как эта база данных является многомодельной, она поддерживает модели данных документа, пары "ключ — значение", графа и столбчатые модели данных. 

![Azure Cosmos DB: API MongoDB](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Cosmos DB баз данных можно использовать как hello хранилища данных для приложений, написанных в [MongoDB](https://docs.mongodb.com/manual/introduction/). Это означает, что используя имеющиеся [драйверы](https://docs.mongodb.org/ecosystem/drivers/), приложение, написанное для MongoDB, теперь может взаимодействовать с Cosmos DB и использовать базы данных Cosmos DB вместо баз данных MongoDB. Во многих случаях вы можете переключиться с помощью MongoDB tooCosmos DB при простом изменении строки подключения. С помощью этой функции, можно легко создавать и запуск приложений базы данных MongoDB в hello Azure облачной с распределением глобального Azure Cosmos DB и [комплексное отрасли соглашений об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/cosmos-db), продолжая toouse знакомые навыки и средства для MongoDB.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>Что такое преимущество использования Azure Cosmos DB для приложений MongoDB hello

**Одновременно создать масштабируемые пропускной способности и хранения:** легко вверх и вниз к toomeet базы данных MongoDB приложению. Ваши данные хранятся на твердотельных накопителях (SSD), что обеспечивает прогнозируемость и малую продолжительность задержек. Cosmos DB поддерживает MongoDB коллекции, которые можно масштабировать toovirtually размеры неограниченное хранение и пропускная способность. Вы можете гибко масштабировать Cosmos DB с предсказуемым уровнем производительности по мере увеличения объема данных приложения. 

**Репликация с несколькими регионами:** Cosmos DB прозрачно реплицирует вашей tooall областей данных, сопоставленный с вашей учетной записи MongoDB, позволяя toodevelop приложений, которые требуют toodata глобальный доступ, предоставляя компромисса между согласованность, доступности и производительности в рамках соответствующего гарантии. Cosmos DB обеспечивает прозрачное региональной отработки отказа с множественной адресацией API и hello tooelastically возможности масштабирования, пропускной способности, а также хранения по всему миру hello. Дополнительные сведения см. в статье [DocumentDB — глобально распределенная служба базы данных в Azure](distribute-data-globally.md).

**Совместимость MongoDB.** Вы можете применять имеющиеся навыки работы с MongoDB, код приложения и средства. Можно разрабатывать приложения с использованием MongoDB и развертывать их tooproduction с помощью hello полностью управляемого глобально распределенная служба Cosmos DB.

**Нет сервера управления**: отсутствует toomanage и масштабирование базы данных MongoDB. Cosmos DB является полностью управляемой службы, это означает, что у вас toomanage любой инфраструктуры, так и виртуальными самостоятельно. Cosmos DB доступна в более 30 [регионах Azure](https://azure.microsoft.com/regions/services/).

**Уровни согласованности пройтись:** Select из пяти хорошо определенные согласованности уровни tooachieve оптимальное соотношение согласованность и производительность. Для запросов и операций чтения служба Cosmos DB предлагает пять отдельных уровней согласованности — строгий, с ограниченным устареванием, сеансовый, с согласованностью префиксов и согласованный в конечном счете. Эти уровни согласованности детальные, четко определенных разрешить toomake звуковой компромиссы между согласованности, доступность и задержки. Дополнительные сведения см. в разделе [согласованности с помощью уровней toomaximize доступности и производительности](consistency-levels.md).

**Автоматическое индексирование**: по умолчанию Cosmos DB автоматически индексирует все свойства hello в документах базы данных MongoDB и не ожидается и не требует любой схемы или создания вторичных индексов.

**Корпоративного уровня** -Azure Cosmos DB поддерживает несколько локальные реплики toodeliver 99,99% доступности и защиты данных шрифтом hello локальных и региональный сбоев. Azure Cosmos DB имеет [сертификаты соответствия требованиям](https://www.microsoft.com/trustcenter) и функции обеспечения безопасности корпоративного класса. 

Узнайте больше в этом видео из цикла "Пятница с Azure" от Скотта Хансельмана (Scott Hanselman) и главного технического руководителя Azure Cosmos DB, Кирилла Гаврилюка.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>Запуск tooget

Выполните hello MongoDB краткие руководства toocreate учетной записи Cosmos DB и перенести вашей существующей toouse приложений Mongo DB Cosmos DB или создавать новую:

* [Перемещение имеющегося веб-приложения MongoDB Node.js](create-mongodb-nodejs.md)
* [Построение MongoDB API веб-приложения с помощью .NET и hello портал Azure](create-mongodb-dotnet.md)
* [Построение консольного приложения MongoDB API с использованием Java и hello портал Azure](create-mongodb-java.md)

## <a name="next-steps"></a>Дальнейшие действия

Сведения об API MongoDB Azure Cosmos DB интегрирован в hello в целом Azure Cosmos DB документации, но ниже приведены несколько tooget указатели, который был запущен:

* Выполните hello [подключения учетной записи MongoDB tooa](connect-mongodb-account.md) учебника toolearn как tooget данные строки подключения учетной записи.
* Выполните hello [MongoChef использования с Azure Cosmos DB](mongodb-mongochef.md) учебника toolearn как соединение между Azure Cosmos DB базы данных и приложения MongoDB в MongoChef toocreate.
* Выполните hello [переноса данных tooAzure Cosmos DB с поддержкой протоколов для MongoDB](mongodb-migrate.md) учебника tooimport вашей данных tooan API для базы данных MongoDB.
* Подключение tooan API для MongoDB учетной записи с помощью [Robomongo](mongodb-robomongo.md).
* Узнайте, сколько RUs операций с hello [GetLastRequestStatistics команды и hello Azure портала метрики](request-units.md#GetLastRequestStatistics).
* Узнайте, каким образом слишком[настроить чтения глобально распределенных приложений](../cosmos-db/tutorial-global-distribution-mongodb.md).
