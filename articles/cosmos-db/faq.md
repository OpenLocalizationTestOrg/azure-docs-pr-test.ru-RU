---
title: "часто задаваемые вопросы DB Cosmos aaaAzure | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о Cosmos базу данных Azure, служба распределенной, моделей базы данных. Сведения о емкости, уровнях производительности и масштабировании."
keywords: "Вопросы о базе данных DocumentDB — вопросы и ответы по DocumentDB | Microsoft Azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Вопросы и ответы об Azure Cosmos DB
## <a name="azure-cosmos-db-fundamentals"></a>Основные сведения об Azure Cosmos DB
### <a name="what-is-azure-cosmos-db"></a>Что такое Azure Cosmos DB?
Azure Cosmos DB — это глобально реплицируемая многомодельная служба базы данных, которая предлагает расширенные возможности обращения к данным без определения схем. Она гарантирует надежный настраиваемый уровень производительности и повышает скорость разработки. Он все достигается с помощью управляемой платформы, поддерживаемый hello power и эффективность использования Microsoft Azure. 

Azure Cosmos DB — hello подходящее решение для web, мобильных устройств, игры, и IoT приложения при прогнозируемой пропускной способности, высокая доступность, Низкая задержка и модели данных без схемы, требования к ключу. Azure Cosmos DB обеспечивает гибкие возможности использования схем и расширенное индексирование, а также включает поддержку транзакций нескольких документов с интегрированным языком JavaScript. 

Дополнительные базы данных вопросы, ответы и инструкции по развертыванию и использованию этой службы см. в разделе hello [страницы документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/cosmos-db/).

### <a name="what-happened-toodocumentdb"></a>Какая ошибка tooDocumentDB?
Hello DocumentDB API является одним из hello поддерживается API-интерфейсов и модели данных для Azure Cosmos DB. Кроме того, Azure Cosmos DB предоставляет поддержку для предварительной версии API Graph, предварительной версии API таблиц, а также API MongoDB. См. дополнительные сведения в разделе с [вопросами клиентов DocumentDB](#moving-to-cosmos-db).

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>Получение toomy учетная запись DocumentDB в hello портал Azure
В hello портал Azure щелкните значок Azure Cosmos DB hello hello левой панели. При наличии учетной записи DocumentDB, прежде чем вы получите Azure Cosmos DB учетная запись, с выставления счетов tooyour без изменений.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>Что такое hello типичные случаи использования для Azure Cosmos DB
Azure Cosmos DB лучше всего подойдет для новых мобильных устройств, web, игры, и важно приложений IoT автоматическое масштабирование, прогнозируемую производительность быстрый заказ миллисекунд времени ответа куда hello возможность tooquery над данными без схемы. Azure Cosmos DB пригоден toorapid разработки и поддержки непрерывного итерации hello модели данных приложения. [Распространенным примером использования Azure Cosmos DB](use-cases.md) являются приложения, которые управляют содержимым и данными пользователей. 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Как Azure Cosmos DB обеспечивает прогнозируемую производительность?
Объект [единица запроса](request-units.md) (RU) является мерой hello пропускной способности в базе данных Azure Cosmos. Пропускной способностью 1-RU соответствует toohello пропускной способности hello GET документа 1 КБ. Каждая операция в Cosmos базу данных Azure, включая операции чтения, записи, SQL-запросов и выполнения хранимой процедуры, имеет значение детерминированным RU, которое зависит от операции hello toocomplete пропускная способность, необходимая hello. Вместо того, чтобы разбираться с показателями загрузки ЦП, числом операций ввода-вывода и объемом потребляемой памяти, а также думать о том, как эти ресурсы влияют на пропускную способность приложения, можно просто рассматривать единицу запроса как меру производительности.

Каждый контейнер Azure Cosmos DB можно зарезервировать с подготовленной пропускной способностью, выраженной в единицах запроса в секунду. Для приложений любого масштаба производительности отдельных запросов toomeasure значениями единиц Запросов и подготовки контейнера toohandle hello общее количество единиц запроса для всех запросов. Также можно масштабировать или масштабировать контейнера пропускную способность как hello потребностей вашего приложения evolve. Дополнительные сведения о единицах запроса и справки определение контейнера см. [Оценка потребностей пропускной](request-units.md#estimating-throughput-needs) и повторите hello [пропускной способности калькулятора](https://www.documentdb.com/capacityplanner). Термин Hello *контейнера* здесь понимается коллекции DocumentDB API tooa toorefers, graph Graph API, коллекции MongoDB API и API таблиц таблицы. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>Как Azure Cosmos DB поддерживает различные модели данных, например пары "ключ — значение", столбцы, документы и графы?

Ключ значение (таблица), один столбец, Документирование и графические данные модели — это все поддерживаемые из-за ARS hello (атомами, записи и последовательностей) проектирования, DB Cosmos Azure основан на. Атомами записей и последовательности может быть легко сопоставленных и прогнозируемом toovarious моделей данных. Hello API-интерфейсы для подмножества моделей, доступных прямо сейчас (DocumentDB, MongoDB, таблицы и Graph API) и других пользователей определенного tooadditional модели данных будут доступны в hello будущее.

Azure Cosmos DB есть схема зависит от индексирования подсистема может автоматически индексирования все hello данные, которые он принимает не требуя схемы или вторичные индексы от разработчика hello. механизм Hello зависит от набора макетов логического индекса (зеркально, один столбец, дерево), которые отделять hello структуры хранилища из индекса hello и подсистемы обработки запросов. Cosmos DB toosupport возможность hello набор протоколы передачи и API-интерфейсы расширяемой способом, а также перевести их эффективно toohello основных данных модели (1) hello логического индекса макеты и (2) делая однозначно может поддерживать несколько моделей данных в собственном коде .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Соответствует ли Azure Cosmos DB HIPAA?
Да, соответствует. HIPAA устанавливает требования для hello использовать раскрытия и защита данных однозначно работоспособности. Дополнительные сведения см. в разделе hello [Центр управления безопасностью Microsoft](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>Что такое hello ограничения хранилища Azure Cosmos БД
Отсутствует ограничение toohello Общая сумма данных, в контейнере может храниться в базе данных Azure Cosmos.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>Каковы ограничения пропускной способности hello Azure Cosmos DB?
Отсутствует общая сумма toohello ограничение пропускной способности, который контейнер может поддерживать в базе данных Azure Cosmos. Здравствуйте идея ключа является toodistribute рабочей нагрузки примерно равномерно между достаточно большое количество разделов.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Сколько стоит Azure Cosmos DB?
Дополнительные сведения приведены toohello [Azure DB Cosmos, сведения о ценах](https://azure.microsoft.com/pricing/details/cosmos-db/) страницы. Azure взимает плату использования Cosmos DB определяются hello количество подготовленных контейнеров hello количество часов контейнеры hello находились в оперативном режиме, а hello подготовлен пропускную способность для каждого контейнера. Термин Hello *контейнеры* здесь понимается коллекции DocumentDB API toohello, graph Graph API, коллекции MongoDB API и API таблиц таблиц. 

### <a name="is-a-free-account-available"></a>Предусмотрена ли бесплатная учетная запись?
Если новый tooAzure, вы можете зарегистрироваться в [Azure бесплатную учетную запись](https://azure.microsoft.com/free/), которое позволяет 30 дней и и кредит tootry все hello служб Azure. Если у вас есть подписка Visual Studio, вам доступно также [освободить кредиты Azure](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse на любой службы Azure. 

Можно также использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) toodevelop и тестирования приложения локально для освобождения, без создания подписки Azure. Если вас устраивают, как приложение работает в hello эмулятор DB Cosmos Azure, можно переключиться toousing учетную запись Azure Cosmos DB в облаке hello.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Как я могу получить помощь по работе с Azure Cosmos DB?
Если необходимо, чтобы помочь, направляться на toous [переполнения стека](http://stackoverflow.com/questions/tagged/azure-cosmosdb) или hello [форум MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), или запланировать индивидуального разговора с командой разработчиков Azure Cosmos DB hello путем отправки почты слишком[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Настройка Azure Cosmos DB
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Как зарегистрироваться в Azure Cosmos DB?
Azure Cosmos DB доступен в hello портал Azure. Во-первых, вам нужно зарегистрироваться для получения подписки Azure. После зарегистрировались вы, вы можете добавить DocumentDB API, API Graph (Предварительная версия), API-Интерфейс API таблиц (Предварительная версия) или MongoDB учетной записи tooyour подписки Azure.

### <a name="what-is-a-master-key"></a>Что такое главный ключ?
Главный ключ является tooaccess маркеров безопасности все ресурсы для учетной записи. Пользователи с ключом hello имеют ресурсы tooall чтение и запись в учетной записи базы данных hello. Будьте осторожны при распространении главных ключей. Hello первичный ключ основной и вторичный ключ master доступны на hello **ключей** колонке hello [портал Azure][azure-portal]. Дополнительные сведения о ключах см. в разделе [Просмотр, копирование и повторное создание ключей доступа](manage-account.md#keys).

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>Что такое hello областей, которые можно задать PreferredLocations 
Hello PreferredLocations значение можно задать tooany из hello Azure областей, в которых доступен Cosmos DB. Список доступных регионов см. на странице с [регионами Azure](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>Есть все, что я следует иметь в виду при распределение данных между Здравствуй, мир! через hello центрами обработки данных Azure? 
Azure Cosmos DB присутствует по всем регионам Azure, как указано на hello [регионах Azure](https://azure.microsoft.com/regions/) страницы. Поскольку hello основную службу, каждый новый центр обработки данных есть присутствия Azure Cosmos DB. 

Указывая регион, помните, что служба Azure Cosmos DB учитывает ограничения, связанные с использованием независимых облаков и облаков для государственных организаций. То есть, создав учетную запись в регионе с независимым облаком, вы не сможете выполнять репликацию из такого региона. Также вы не сможете включить репликацию в других таких регионах из внешней учетной записи. 

## <a name="develop-against-hello-documentdb-api"></a>Осуществлять разработку hello DocumentDB API

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>Как начать разработку hello DocumentDB API?
Microsoft DocumentDB API доступна в hello [портал Azure][azure-portal]. Во-первых, вам нужно зарегистрироваться для получения подписки Azure. После регистрации для получения подписки Azure, можно добавить tooyour контейнера DocumentDB API подписки Azure. Инструкции по добавлению учетной записи Azure Cosmos DB см. в статье [Azure Cosmos DB. Создание веб-приложения API DocumentDB с использованием языка .NET и портала Azure](create-documentdb-dotnet.md#create-account). Если у вас есть учетная запись DocumentDB последние hello, вы получите учетную запись Azure Cosmos DB. 

[Пакеты SDK](documentdb-sdk-dotnet.md) доступны для .NET, Python, Node.js, JavaScript и Java. Разработчики также могут использовать hello [интерфейсы API RESTful HTTP](/rest/api/documentdb/) toointeract с ресурсами Azure Cosmos DB различных платформах и языках.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>Получить доступ к tooget некоторые образцы готовых надежную основу?
Образцы для hello DocumentDB API [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), и [Python](documentdb-python-samples.md) пакеты SDK доступны на сайте GitHub.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>Поддерживает hello данных без схемы поддержки DocumentDB API базы данных?
Да, hello DocumentDB API позволяет приложениям toostore произвольных JSON документов без определения схемы и указания. Данные немедленно доступна для запросов через интерфейс запросов базы данных SQL Azure Cosmos hello.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>Hello DocumentDB API поддерживает ACID-транзакции?
Да, hello DocumentDB API поддерживает транзакции между документами, выражается в виде JavaScript хранимых процедур и триггеров. Транзакции являются область tooa один раздел в каждой коллекции и выполняется в соответствии с семантикой ACID как «все или ничего,» изолированная от других одновременно выполняющихся запросов кода и пользовательского. При возникновении исключений через выполнение на стороне сервера hello код приложения и код JavaScript, hello вся транзакция откатывается. Дополнительные сведения о транзакциях см. в разделе [Транзакции программы базы данных](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>Что такое коллекция?
Коллекция представляет собой группу документов и связанную с ними логику в виде приложения JavaScript. Коллекция является оплачиваемые сущности, в котором hello [стоимость](performance-levels.md) определяется пропускная способность hello и использовали хранилище. Коллекции могут охватывать один или несколько секций или серверы и можно масштабировать toohandle практически неограниченное тома хранилища или пропускной способности.

Коллекции также являются hello выставления счетов сущностей для Azure Cosmos DB. Каждая коллекция оплачивается каждый час, основании hello пропускная способность и использовать дисковое пространство. Ознакомьтесь с дополнительными сведениями о [ценах на Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>Как создать базу данных?
Базы данных можно создать с помощью hello [портал Azure](https://portal.azure.com), как описано в [добавить коллекцию](create-documentdb-dotnet.md#create-collection), один из hello [пакеты SDK Azure Cosmos DB](documentdb-sdk-dotnet.md), или hello [API-интерфейс REST](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>Как устанавливать настройки для пользователей и разрешений?
Можно создать пользователей и разрешений с помощью одного из hello [SDK API DB Cosmos](documentdb-sdk-dotnet.md) или hello [API-интерфейс REST](/rest/api/documentdb/).  

### <a name="does-hello-documentdb-api-support-sql"></a>Hello DocumentDB API поддерживает SQL?
Hello язык запросов SQL имеет расширенную подмножество hello функциональности, которая поддерживается в SQL. язык запросов SQL базы данных Azure Cosmos Hello играет форматированного иерархических операторов и операторов отношения через на базе JavaScript, определяемой пользователем функции (UDF). Для моделирования документов JSON в виде деревьев с меткой узлы, которые используются методы автоматического индексирования Azure Cosmos DB hello и диалект запроса SQL hello Azure Cosmos DB позволяет грамматики JSON. Сведения об использовании грамматику SQL см. в разделе hello [QueryDocumentDB] [ query] статьи.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>Поддерживает DocumentDB API поддержки SQL статистические функции hello?
Hello DocumentDB API поддерживает агрегирование низкой задержкой любых объемов через агрегатные функции `COUNT`, `MIN`, `MAX`, `AVG`, и `SUM` через hello грамматику SQL. Дополнительные сведения см. в разделе [Статистические функции](documentdb-sql-query.md#Aggregates).

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>Как hello DocumentDB API обеспечивает параллелизм
Hello DocumentDB API поддерживает управление оптимистичным параллелизмом (OCC) через теги сущности HTTP или теги eTag. Каждый ресурс DocumentDB API имеет значение ETag и hello ETag установлено на сервере hello каждый раз при обновлении документа. заголовок ETag Hello и текущее значение hello включены во все сообщения ответа. Теги eTag можно использовать с сервера hello If-Match заголовок tooallow hello toodecide ли ресурс должны быть обновлены. Hello If-Match значение — toobe значение ETag hello, проверяется. Если hello значение ETag соответствует серверу hello значение ETag, обновляется ресурс hello. Hello ETag больше не является текущей, hello сервер отклоняет hello операцию с «HTTP 412 предварительных условий сбоя» код ответа. Затем клиент Hello повторно выбирается hello ресурсов tooacquire hello текущее значение ETag для ресурса hello. Кроме того теги eTag можно использовать с toodetermine Заголовок If-None-Match hello ли требуется заново ресурса.

toouse оптимистичного параллелизма в .NET, используйте hello [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) класса. Пример .NET см. в разделе [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) в образце hello DocumentManagement на GitHub.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>Выполнение транзакций в hello DocumentDB API
Hello DocumentDB API поддерживает встроенные в язык транзакции через JavaScript хранимых процедур и триггеров. Все операции с базой данных в скрипте выполняются в режиме изоляции моментального снимка. Если это коллекции одной секции, hello выполнения является коллекцией с областью toohello. Если коллекция hello секционирована, выполнение hello происходит с областью toodocuments с hello того же значения ключа раздела hello коллекции в коллекции. Моментальный снимок версии документа hello (теги eTag) берется в начале транзакции hello hello и зафиксирована только в том случае, если скрипт hello завершается успешно. Если hello JavaScript вызывает ошибку, hello транзакция откатывается. Дополнительные сведения см. в статье [Программирование Azure Cosmos DB на стороне сервера: хранимые процедуры, триггеры баз данных и определяемые пользователем функции](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Как выполнять массовую вставку документов в Cosmos DB?
Массовую вставку документов в Azure Cosmos DB можно выполнять так:

* Средство переноса Hello данных, как описано в [средство миграции базы данных для базы данных Azure Cosmos](import-data.md).
* С помощью хранимых процедур, как описано в статье [Программирование Azure Cosmos DB на стороне сервера: хранимые процедуры, триггеры баз данных и определяемые пользователем функции](programming.md).

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>Hello DocumentDB API поддерживает кэширование ресурсов ссылку?
Да, так как Azure Cosmos DB — это служба RESTful, ссылки на ресурсы являются неизменяемыми и могут кэшироваться. DocumentDB API клиентов можно указать заголовок «If-None-Match» для чтения к любой документ как ресурс или коллекции, а затем обновлять их локальные копии после изменения версии сервера hello.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>Доступен ли локальный экземпляр API DocumentDB?
Да. Hello [DB эмулятор Azure Cosmos](local-emulator.md) предоставляет эмуляцию hello Cosmos DB службы высокого качества. Он поддерживает функциональные возможности, идентичные tooAzure Cosmos DB, включая поддержку для создания и выполнения запросов документов JSON, подготовку и масштабирование коллекции и выполнения хранимых процедур и триггеров. Можно разрабатывать и тестирования приложений с помощью hello Azure Cosmos DB эмулятор и развернуть tooAzure по всему миру, делая изменение toohello конечной точки подключения для базы данных Azure Cosmos одной конфигурации.

## <a name="develop-against-hello-api-for-mongodb"></a>Осуществлять разработку hello API для MongoDB
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>Что такое hello Azure Cosmos DB API для MongoDB
Hello Azure Cosmos DB API для MongoDB имеет уровень совместимости, которая позволяет tooeasily приложений и прозрачно взаимодействовать с hello собственного Azure Cosmos DB компонент database engine с помощью существующей, поддерживаемые сообществом Apache MongoDB API-интерфейсов и драйверов. Разработчикам теперь можно использовать существующие MongoDB средство цепочки и навыки toobuild приложения, использующие преимущества Azure Cosmos БД. Разработчикам использовать преимущества hello уникальные возможности Azure Cosmos DB, включающие обслуживания автоматической индексации, то команда backup, соглашения об уровне финансовые резервные службы (SLA) и т. д.

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>Как подключаться toomy API для базы данных MongoDB?
Здравствуйте tooconnect toohello быстрым способом Azure Cosmos DB API для MongoDB превышает toohead toohello [портал Azure](https://portal.azure.com). Go tooyour учетной записи и выберите в меню навигации слева hello, **быстрый запуск**. Краткое руководство предназначено hello лучшим способом tooget код фрагменты tooconnect tooyour базы данных. 

В Azure Cosmos DB строгие требования к безопасности и стандарты. Учетные записи Azure Cosmos DB требовать проверку подлинности и безопасного взаимодействия через SSL, поэтому следует убедиться, что toouse TLSv1.2.

Дополнительные сведения см. в разделе [подключения tooyour API для базы данных MongoDB](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>Существуют ли дополнительные коды ошибок API для базы данных MongoDB?
В дополнение toohello распространенные MongoDB коды ошибок hello MongoDB API имеет свой собственный конкретные коды ошибок:


| Ошибка               | Код  | Описание  | Решение  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | Общее количество единиц запроса потребляет Hello превысил заданную частоту hello блок-подготовленного запроса для коллекции hello и отрегулировано. | Рассмотрите возможность масштабирования hello пропускную способность коллекции hello из hello портал Azure или повтором. |
| ExceededMemoryLimit | 16501 | Как служба несколькими клиентами hello операции был превышен выделенный памяти hello клиента. | Уменьшите область hello hello операции через более строгие критерии запроса или обратитесь в службу поддержки из hello [портал Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>Пример: *&nbsp;&nbsp;&nbsp;&nbsp;db.getCollection('users').aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Разработка с hello API таблиц (Предварительная версия)

### <a name="terms"></a>Термины 
Hello Azure Cosmos DB: API таблиц (Предварительная версия) означает toohello предложение premium в Azure Cosmos DB для поддержки таблицы было объявлено на построения 2017 г. 

Стандартная таблица Hello SDK — hello существующей таблицы хранилища Azure SDK. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>Как использовать hello новое предложение API таблиц (Предварительная версия) 
Hello Azure Cosmos DB таблицы API доступен в hello [портал Azure][azure-portal]. Во-первых, вам нужно зарегистрироваться для получения подписки Azure. После зарегистрировались, можно добавить tooyour учетная запись Azure Cosmos DB таблицы API подписки Azure и добавьте учетную запись tooyour таблиц. 

Время hello предварительной версии при [пакеты SDK](../cosmos-db/table-sdk-dotnet.md) , доступные для .NET, вы можете начать работу, выполнив hello [API таблиц](../cosmos-db/create-table-dotnet.md) статьи краткого руководства.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>Использовать новый hello toouse SDK API таблиц (Предварительная версия)? 
Да, hello [таблицу Premium хранилища Windows Azure SDK (Предварительная версия)](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) доступен в NuGet. Дополнительные сведения можно найти в hello [Cosmos DB таблицы .NET API-интерфейса Azure: загрузка и заметки о выпуске](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) страницы. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>Как оставить отзыв о hello SDK или ошибок?
Вы можете совместно использовать ваши отзывы в любом из следующих способов hello:

* [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [Форум MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>Что такое hello строку соединения, необходимость toohello tooconnect toouse API таблиц (Предварительная версия)
Строка подключения Hello является:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
Строка подключения hello можно получить на странице ключи hello hello портал Azure. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>Как переопределить параметры конфигурации hello hello параметров запроса в API новых таблиц hello (Предварительная версия)?
Сведения о параметрах конфигурации см. в описании [возможностей Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Hello параметры можно изменить, добавив tooapp.config в разделе appSettings hello в клиентском приложении hello.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>Существуют ли все изменения для заказчиков, использующих стандартные существующую таблицу hello SDK?
Отсутствует. Существующие или новые пользователи, использующие стандартный существующую таблицу hello SDK не изменяются. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>Как просмотреть табличные данные, хранящиеся в базе данных Azure Cosmos для использования с hello API таблиц (проверка)? 
Можно использовать данные hello Azure портала toobrowse hello. Можно также использовать hello кода API таблиц (Предварительная версия) или hello средства, описанные в следующей ответов hello. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>Какие средства работы с hello API таблиц (Предварительная версия)? 
Можно использовать старую версию hello обозреватель Azure (0.8.9).

Средства с tootake гибкость hello, поддерживаемых строку подключения в формате hello, указанном ранее hello новый API таблицы (Предварительная версия). Список средств таблиц предоставляется на hello [клиентские средства хранилища Azure](../storage/common/storage-explorers.md) страницы. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>PowerShell или Azure CLI работают с новым API таблицы hello (Предварительная версия)?
Мы планируем tooadd поддержка PowerShell и Azure CLI для таблицы API (Предварительная версия). 

### <a name="is-hello-concurrency-on-operations-controlled"></a>Имеет hello параллелизма для операции, которые управляются?
Да, оптимистичный параллелизм обеспечивается за счет использования hello механизма ETag hello. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>Hello модель запроса OData поддерживаются для сущностей? 
Да, hello API таблиц (Предварительная версия) поддерживает OData и запросов LINQ. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>Можно ли подключить toohello стандартных таблиц Azure и hello premium новый API таблиц (Предварительная версия) рядом друг с другом в hello того же приложения? 
Да, можно подключить путем создания двух разных экземплярах hello CloudTableClient, каждый из которых указывает tooits владельцем URI через строку подключения hello.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>Как перенести существующие таблицы Azure приложения toothis новый метод хранения?
преимущества tootake hello новое предложение API таблиц на существующих таблиц хранилища данных, обратитесь к [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com). 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>Что такое hello стратегия для этой службы, и при предложит других стандартных функциональных возможностей API таблицы?
Мы планируем tooadd поддержку SAS токены, ServiceContext, статистики, клиента стороны шифрования, аналитики и другие функции, как к общедоступной. Вы можете оставить свой отзыв на сайте [UserVoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api). 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>Как обеспечивается расширения размера хранилища hello выполняется для этой службы, если, например, начать с  *n*  ГБ данных и данные будут увеличиваться ТБ too1 с течением времени? 
Azure Cosmos DB — спроектированный tooprovide неограниченное хранение, посредством использования hello горизонтального масштабирования. Hello службы можно отслеживать и эффективно увеличить хранилище. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>Как отслеживать предложения hello API таблиц (Предварительная версия)?
Можно использовать hello API таблиц (Предварительная версия) **метрики** панели toomonitor запросов и использования хранилища. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>Расчет пропускной способности hello необходимому
Можно использовать hello емкости оценки toocalculate hello TableThroughput, необходимые для операций hello. Дополнительные сведения см. на странице [оценки единиц запросов и хранилища данных](https://www.documentdb.com/capacityplanner). В общем случае можно представляют сущности как JSON и предоставлять hello номера для операций. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>Можно ли использовать hello новые таблицы API пакета SDK локально в эмуляторе hello (Предварительная версия)?
Да, можно использовать hello API таблиц (Предварительная версия) с hello локальный эмулятор при использовании hello новый пакет SDK. новый эмулятор toodownload, перейти слишком[используйте hello DB эмулятор Azure Cosmos локальной разработки и тестирования](local-emulator.md). Hello StorageConnectionString значение в файле app.config должен toobe:

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>Мои существующего приложения работают со hello API таблиц (Предварительная версия)? 
Hello контактную зону hello новый API таблицы (Предварительная версия) совместим с существующие таблицы Azure standard SDK для hello создание, удаление, обновление и операций в .NET API hello запросов hello. Обеспечьте ключ строки, так как hello API таблиц (Предварительная версия) требуется ключ раздела и ключ строки. Мы также запланировать tooadd дополнительную поддержку SDK, как к общедоступной версии этого предложения службы.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>Нужен ли мне toomigrate Мой существующего приложения Azure на основе таблицы toohello новый пакет SDK не выполнять функций API таблиц (Предварительная версия) hello toouse?
Нет, вы можете создавать и использовать существующие ресурсы таблиц уровня "Стандартный", не прерывая работу. Однако если не используется новый API таблицы hello (Предварительная версия), невозможно преимущества hello автоматического индекса, параметр дополнительных согласованности hello или глобального распространения. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>Как добавить репликации данных hello premium hello API таблиц (Предварительная версия) в нескольких регионах Azure?
Вы можете использовать портал Azure Cosmos DB hello [параметры глобальной репликации](tutorial-global-distribution-documentdb.md#portal) tooadd области, которые подходят для вашего приложения. toodevelop глобально распределенного приложения, следует также добавить приложение hello PreferredLocation сведения набор toohello местный регион для предоставления Низкая задержка чтения. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>Изменение области hello основной записи для учетной записи hello в premium hello API таблиц (Предварительная версия)
Можно использовать hello Azure Cosmos DB глобального репликации панели портала tooadd области и затем отработки отказа требуется область toohello. См. дополнительные сведения о [разработке с использованием учетных записей Azure Cosmos DB с поддержкой нескольких регионов](regional-failover.md). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>Как настроить предпочитаемые регионы для чтения, чтобы обеспечить низкую задержку при распределении данных? 
toohelp чтение из hello локальное расположение, используйте ключ PreferredLocation hello в файле app.config hello. Для существующих приложений hello API таблиц (Предварительная версия) вызывает ошибку, если значение LocationMode. Удалите этот код, так как hello premium API таблиц (Предварительная версия) забирает эти сведения из файла app.config hello. См. дополнительные сведения о [возможностях Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>Как следует обдумать уровни согласованности в hello API таблиц (Предварительная версия)? 
В Azure Cosmos DB реализованы продуманные компромиссные сочетания показателей согласованности, доступности и задержки. Azure Cosmos DB предоставляет пять уровней согласованности tooTable разработчикам API (Предварительная версия), чтобы вы могли выбрать модель hello правой согласованность на уровне таблицы hello и выполнения отдельных запросов при отправке запросов данных hello. Подключаемый клиент может выбирать уровень согласованности. Можно изменить уровень hello через файл app.config приветствия для hello значение ключа TableConsistencyLevel hello. 

Hello API таблиц (Предварительная версия) предоставляет небольшой задержкой считывает с «для чтения собственные записи» с согласованностью сеанса по умолчанию hello. Дополнительные сведения см. в статье [Настраиваемые уровни согласованности данных в DocumentDB](consistency-levels.md). 

По умолчанию хранилище таблиц Azure предоставляет и надежный согласованности в области Eventual в hello вторичного расположения. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>Предусмотрено ли в Azure Cosmos DB больше уровней согласованности, чем в таблицах уровня "Стандартный"?
Да, сведения о распределение toobenefit из hello характер Azure Cosmos DB см. в разделе [уровни согласованности](consistency-levels.md). Так как для уровни согласованности hello предоставляются гарантии, их можно использовать с достоверности. См. дополнительные сведения о [возможностях Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>При включении глобального распространения, как долго требуется tooreplicate hello данных?
Мы зафиксируйте данных hello устойчивую в локальной области hello и отправьте области tooother hello данных непосредственно в течение нескольких миллисекунд. Такая репликация зависит только hello приема-передачи время с hello центра обработки данных. toolearn Дополнительные сведения о возможности глобального распространения hello Azure Cosmos DB, в разделе [Azure Cosmos DB: глобально распределенной базы данных в Azure службы](distribute-data-globally.md).

### <a name="can-hello-read-request-consistency-level-be-changed"></a>Можно изменить уровень согласованности hello запрос чтения?
DB Cosmos Azure можно задать уровень согласованности hello на уровне контейнера hello (в таблице hello). С помощью пакета SDK для hello, можно изменить уровень hello, предоставляя hello значение для ключа TableConsistencyLevel в файле app.config hello. Hello возможные значения: Strong, Bounded Staleness, сеанса, согласованных префикса и Eventual. См. дополнительные сведения о [настраиваемых уровнях согласованности данных в Azure Cosmos DB](consistency-levels.md). Hello ключа идея состоит, не может установить согласованности запрос hello уровень превышает приветствия для таблицы hello. Например нельзя установить hello согласованности для таблицы hello в Eventual hello запрос согласованности уровне и на строгих. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>Как учетной записи таблицы API (Предварительная версия) premium hello обрабатывает переход на другой ресурс, если область выходит из строя? 
Hello premium API таблиц (Предварительная версия) заимствует hello глобально Распределенная платформа Azure Cosmos DB. tooensure, что приложение допускает время простоя в центре обработки данных, включите по крайней мере один дополнительные области для hello учетной записи на портале Azure Cosmos DB hello [разработки с использованием учетных записей Azure Cosmos DB регионов](regional-failover.md). Приоритет hello hello области можно задать с помощью портала hello [разработки с использованием учетных записей Azure Cosmos DB регионов](regional-failover.md). 

Можно добавить столько областей, как для учетной записи hello и управления, где он может переключить tooby, предоставляя приоритет отработки отказа. Конечно, toouse hello базы данных, вы должны tooprovide приложения существует слишком. Но этот простой не отразится на работе клиентов. пакет SDK для клиента Hello — auto ящиков. То есть он может определить область hello, не работает и автоматически переходить на новую область toohello.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>Включен ли hello premium API таблиц (Предварительная версия) для резервного копирования?
Да, hello premium API таблиц (Предварительная версия) заимствует hello платформы Azure Cosmos БД для резервных копий. Резервные копии создаются автоматически. См. дополнительные сведения об [оперативном резервном копировании и восстановлении с помощью Azure Cosmos DB](online-backup-and-restore.md).

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Hello API таблиц (Предварительная версия) индексировать все атрибуты сущности по умолчанию
Да, по умолчанию индексируются все атрибуты сущности. См. дополнительные сведения о [политиках индексации Azure Cosmos DB](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>Значит ли это, не возникают toocreate несколько запросов hello toosatisfy индексы? 
Да, Azure Cosmos DB обеспечивает автоматическое индексирование всех атрибутов без определения схемы. Автоматизация освобождает разработчиков toofocus на приложения hello вместо создания индексов и управления. См. дополнительные сведения о [политиках индексации Azure Cosmos DB](indexing-policies.md).

### <a name="can-i-change-hello-indexing-policy"></a>Можно изменить политики индексирования hello
Да, можно изменить политики индексирования hello, предоставляя определение индекса hello. См. дополнительные сведения о [возможностях Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Требуется tooproperly кодирования и escape-параметры hello. 

В формате json строка в файле app.config hello:
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>Azure DB Cosmos как платформы кажется toohave много возможностей, таких как сортировка, статистические выражения, иерархии и другие функциональные возможности. Вы добавит эти возможности toohello API таблицы? 
В режиме предварительного просмотра, hello таблицы API предоставляет hello же запрос, функциональные возможности, что хранилище таблиц Azure. Кроме того, эта база данных поддерживает сортировку, выполнение статистических вычислений, геопространственные запросы, иерархию и множество встроенных функций. Корпорация Майкрософт предоставляет дополнительные функциональные возможности в hello таблицы API в будущих версиях. Дополнительные сведения см. в статье [SQL-запросы для API DocumentDB в Azure Cosmos DB](../documentdb/documentdb-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>Когда изменяйте TableThroughput для hello API таблиц (Предварительная версия)
Необходимо изменить TableThroughput выполняется одно из следующих условий hello:
* Для выполнения извлечения, преобразования и загрузки (ETL) данных, либо требуется tooupload большой объем данных за короткий промежуток времени. 
* Требуется более высокая пропускная способность из контейнера hello в серверной части hello. Например см hello используется пропускная способность больше, чем пропускная способность hello, которое вы начало регулируются. Дополнительные сведения см. в статье [Настройка пропускной способности для коллекций Azure Cosmos DB](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>Можно ли масштабирования вверх и вниз hello пропускной способности таблицей API таблиц (Предварительная версия)? 
Да, можно использовать портал Azure Cosmos DB hello Масштаб области tooscale hello пропускной способности. См. дополнительные сведения о [настройке пропускной способности](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>Определяется ли пропускная способность таблицы по умолчанию для новых подготовленных таблиц?
Да, если не переопределить hello TableThroughput через файл app.config и не использовать предварительно созданной контейнер в базе данных Azure Cosmos hello службы создает таблицу с пропускной способностью 400.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>Есть ли изменения цен для существующих клиентов hello стандартные API-Интерфейс таблиц?
Отсутствует. Цены для существующих клиентов API таблиц уровня "Стандартный" не изменились. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Как вычисляется hello цены для hello API таблиц (Предварительная версия) 
Hello Цена зависит от выделенного TableThroughput hello. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>Как обрабатывать любые регулирования hello таблиц в таблицы API (Предварительная версия) предложения? 
Если частота запросов hello превышает емкость hello hello пропускная способность для hello базового контейнера, возникает сообщение об ошибке и hello SDK будет повторять попытки вызова hello путем применения политики повтора hello.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>Почему необходимо toochoose пропускной способности, помимо свойств PartitionKey и RowKey tootake преимуществами hello premium API таблиц (Предварительная версия) предложение Azure Cosmos DB?
Azure Cosmos DB задает пропускной способности по умолчанию для контейнера, если не указывается в файле app.config hello. 

Azure Cosmos DB предоставляет гарантии производительности и задержки с верхними границами для операций. Эта гарантия возможна в том случае, если обработчик hello можно принудительно задать руководства по операциям клиента hello. Установка TableThroughput гарантирует получение гарантируется пропускной способности и задержки, поскольку платформа hello резервирует емкости и гарантирует успешности оперативной hello. 

С помощью спецификации hello пропускную способность, можно гибко изменить toobenefit с сезонными hello приложения, потребностям hello пропускной способности и затраты.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>Пакет SDK службы хранилища Azure была очень недорогим для меня, потому что я плачу только данные toostore hello и редко запроса. новое предложение Azure Cosmos DB Hello кажется toobe заряжается мне даже в том случае, если не выполняется за одну транзакцию или хранятся ничего. Расскажите об этом подробнее.

Azure Cosmos DB — спроектированный toobe глобально распределенных систем на основе соглашения об уровне ОБСЛУЖИВАНИЯ с гарантией доступность, задержка и пропускная способность. При резервировании пропускной способности в базе данных Azure Cosmos гарантируется, в отличие от пропускной способности hello других систем. Azure Cosmos DB предоставляет такие запрашиваемые клиентами дополнительные возможности, как вторичные индексы и глобальное распространение. Время hello предварительной версии мы предоставляем модели оптимизации пропускной способности и со временем мы планируем tooprovide toomeet оптимизированными для хранения модели требований наших заказчиков. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>При приеме данных в хранилище таблиц мне не приходили уведомления о достижении квоты, информирующие о заполнении секции. С hello API таблиц (Предварительная версия) появляется сообщение. Данный проект ограничение me и принудительное мне toochange Мой существующее приложение?

Azure Cosmos DB — это система на основе соглашений об уровне обслуживания, которая предоставляет неограниченные возможности масштабирования, а также гарантирует согласованность, низкую задержку, высокую пропускную способность и доступность. tooensure гарантируется рекордной производительности, убедитесь, что размер данных и индекс управляемость и масштабируемость. Hello 10 ГБ лимит hello сущностей или других элементов на ключ секционирования — tooensure, предоставляемые высокую производительность для просмотра и запроса. tooensure, которая масштабируется приложения даже для хранилища Azure, рекомендуется, чтобы вы *не* создать раздел горячей хранить все данные в одной секции, и к ней запросы. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>Поэтому PartitionKey и RowKey по-прежнему требуются с hello новый API таблицы (Предварительная версия)? 
Да. Поскольку hello контактную зону hello API таблиц (Предварительная версия) аналогичные toothat hello SDK таблицы хранилища, ключа раздела hello предоставляет эффективный способ toodistribute hello данные. ключ строки Hello уникален в пределах этой секции. Hello toobe основных требований строки существует и не может иметь значение null в качестве hello standard SDK. Длина Hello RowKey составляет 255 байт, а длина hello PartitionKey составляет 100 байт (скоро toobe повышение too1 КБ). 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Что такое hello сообщения об ошибках для hello API таблиц (Предварительная версия)
Поскольку эта Предварительная версия совместима с Стандартная таблица hello, большинство ошибок hello сопоставит toohello ошибки из таблицы Стандартная hello. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>Почему ли получить регулированию при попытке toocreate большое количество таблиц друг за другом в hello API таблиц (Предварительная версия)?
Azure Cosmos DB — это система на основе соглашений об уровне обслуживания, которая гарантирует согласованность, низкую задержку, высокую пропускную способность и доступность. Так как это подготовленных системы резервирует tooguarantee ресурсы этим требованиям. Hello быстро создавать таблицы обнаруживается и регулирование. Рекомендуется рассмотреть hello скорость создания таблиц и понизить его сборки, чем 5 в минуту. Помните, что этот hello API таблиц (Предварительная версия) — это система, подготовленных. Hello момент ее подготовки, сначала для него toopay. 

## <a name="develop-against-hello-graph-api-preview"></a>Осуществлять разработку hello API Graph (Предварительная версия)
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>Применение функции hello API Graph (Предварительная версия) tooAzure Cosmos DB
Можно использовать расширение библиотеки tooapply hello функциональные возможности API Graph (Предварительная версия). Эта библиотека называется Microsoft Azure Graphs. Она доступна в NuGet. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Похоже, поддержки graph обхода hello Gremlin языка. Планируется tooadd другие формы запроса?
Да, мы планируем tooadd другие механизмы для запроса в будущем hello. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>Как использовать hello новое предложение API Graph (Предварительная версия) 
запущена, полный hello tooget [Graph API](../cosmos-db/create-graph-dotnet.md) статьи краткого руководства.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>Вопросы от клиентов DocumentDB
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>Почему перемещение tooAzure Cosmos DB? 

Azure Cosmos DB — високосный больших Далее hello в глобально распределенной базы данных в масштабе облака. Как клиент DocumentDB теперь у вас есть доступ toohello рекордной системы и возможности, предлагаемые Azure Cosmos DB.

Azure Cosmos DB запущен как «Проект Florence» в 2010 tooaddress hello сложностями сталкиваются разработчики при сборке крупномасштабных приложений в корпорации Майкрософт. Hello задачи построения глобально распределенных приложений не являются уникальными tooMicrosoft, поэтому мы внесли hello первого поколения этой технологии в 2015 tooAzure разработчики в форме hello Azure DocumentDB. 

С этого момента мы добавили новые функции и возможности. Azure Cosmos DB является результатом hello. В рамках этого выпуска клиенты DocumentDB автоматически становятся клиентами Azure Cosmos DB. Их данные также переносятся в Azure Cosmos DB. Эти возможности являются в областях hello hello ядра СУБД, а также глобальные распространения, эластичной масштабируемостью и отрасли, полнофункциональными соглашений об уровне обслуживания. В частности мы усовершенствовали hello Azure Cosmos DB базы данных подсистемы tooefficiently карты все популярные моделями, систем типов и API-интерфейсы toohello базовую модель данных из базы данных Azure Cosmos. 

Hello текущего проявления ориентированных на разработчиков часть этой работы является hello новая поддержка [Gremlin](../cosmos-db/graph-introduction.md) и [хранилище API-интерфейсов таблиц](../cosmos-db/table-introduction.md). И это начало просто hello. Мы планируем tooadd других популярных API-интерфейсов и новой модели данных с течением времени, несколько улучшений производительности и объем хранилища по всему миру. 

Это важные toopoint out, hello DocumentDB [диалекта SQL](../documentdb/documentdb-sql-query.md) всегда было несколько hello многие API, hello базовой DB Cosmos Azure может поддерживать. Для разработчиков, использующих полностью управляемой службы, такие как Azure Cosmos DB, hello только интерфейс toohello служба имеет hello API-интерфейсы, предоставляемые службой hello. Для существующих клиентов DocumentDB действительно ничего не изменилось. В DB Cosmos Azure вы получаете точно hello предлагаемых SQL же API, DocumentDB. А теперь (и в будущем hello) другие функции, ранее недоступным доступны 

Другой проявления нашей непрерывной работы — foundation hello расширенных глобальный, так и гибко масштабируемости пропускной способности и хранилища. Мы внесли ряд улучшений фундаментальные toohello глобального распространения подсистемы. Одним из hello много таких компонентов, ориентированных на разработчиков является hello согласованное префикса согласованности модель, которая делает всего пять моделей четко определенных согласованности. Мы будем внедрять и другие интересные возможности по мере их реализации. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>Что делать требуется дальнейшее Мои ресурсы DocumentDB toorun на Azure Cosmos DB tooensure toodo?

Необходимо toomake без изменений во всех. К ресурсам DocumentDB теперь Azure Cosmos DB ресурсы, и было без перерывов в обслуживании hello возникновения этот переход.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>Что делать изменения требуется toomake toowork Мои приложения с помощью Azure Cosmos DB?

Нет toomake без изменений. Классы, пространства имен и имена пакетов NuGet не изменились. Как всегда мы рекомендуем оставить вашей SDK вверх toodate tootake преимущества новейших функций hello и усовершенствований. 

### <a name="whats-changed-in-hello-azure-portal"></a>Изменения в hello портал Azure?

DocumentDB больше не отображается на портале hello службы Azure. Вместо него является новый значок Azure Cosmos DB, как показано в hello после изображения. Все коллекции остаются доступными, и вы как и прежде можете масштабировать пропускную способность, изменять уровни согласованности и выполнять мониторинг соглашений об уровне обслуживания. улучшены возможности Hello обозревателя данных (Предварительная версия). Вы теперь просмотра и редактирования документов, создания и выполнения запросов и работать с хранимых процедур, триггеров и определяемых пользователем Функций с одной страницы, как показано в hello после изображения: 

![Hello Azure коллекции DB Cosmos колонку](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>Существуют toopricing изменения?

Нет, hello стоимость выполнения приложения в базе данных Azure Cosmos — hello таким же, как до.

### <a name="are-there-changes-toohello-slas"></a>Есть ли изменения toohello соглашений об уровне обслуживания?

Нет, Здравствуйте соглашений об уровне обслуживания для обеспечения доступности, согласованности, задержка и пропускная способность не изменяются и по-прежнему отображаются на портале hello. См дополнительные сведения о [соглашениях об уровне обслуживания для Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/).
   
![Приложение со списком задач с примерами данных](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
