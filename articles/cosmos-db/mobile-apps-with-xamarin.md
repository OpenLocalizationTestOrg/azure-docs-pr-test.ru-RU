---
title: "aaaBuild мобильных приложений с помощью Xamarin и Azure Cosmos DB | Документы Microsoft"
description: "В этом руководстве описывается создание приложений с помощью Xamarin iOS, Android или Forms, а также Azure Cosmos DB. Azure Cosmos DB — это быстро растущая облачная база данных глобального масштаба для мобильных приложений."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Создание мобильных приложений с помощью Xamarin и Azure Cosmos DB
Большинство мобильных приложений требуется toostore данных в облаке hello и Azure Cosmos DB — облачная база данных для мобильных приложений. В ней есть все, что необходимо для разработчика мобильных приложений. Это полностью управляемая база данных как услуга, которая масштабируется по запросу. Обновит приложение tooyour данных прозрачно, ни находились пользователи земного шара hello. С помощью hello [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md), можно включить toointeract мобильных приложений Xamarin непосредственно с Azure Cosmos DB без среднего уровня.

В этой статье содержится руководство по созданию мобильных приложений с помощью Xamarin и Azure Cosmos DB. Hello полный исходный код можно найти в учебнике hello в [Xamarin и DB Cosmos Azure на GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), включая то, как toomanage пользователей и разрешений.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>Возможности Azure Cosmos DB для мобильных приложений
Azure Cosmos DB предоставляет следующие основные возможности для разработчиков, мобильное приложение hello:

![Возможности Azure Cosmos DB для мобильных приложений](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* Широкие возможности запросов к данным без схемы. Azure Cosmos DB хранит данные в виде бессхемных документов JSON в разнородных коллекциях. Он обеспечивает [подробный и быстрый запросы](documentdb-sql-query.md) без hello должны tooworry о схем или индексов.
* Высокая пропускная способность. Он принимает лишь несколько миллисекунд tooread и записи документов с использованием Azure Cosmos DB. Разработчики могут указать hello пропускной способности, которые им необходимы, и Azure Cosmos DB учитывает его с помощью соглашений об уровне обслуживания 99,99%.
* Безграничные возможности масштабирования. Коллекции Azure Cosmos DB [увеличиваются по мере расширения приложения](partition-data.md). Вы можете начать с данных небольшого объема и пропускной способности в сотни запросов в секунду. Коллекции могут увеличиваться toopetabytes данных и произвольно большое пропускной способности с сотнями миллионов запросов в секунду.
* Глобальное распределение. Через Здравствуй, мир! перейдите мобильного приложения, которые пользователи находятся в hello часто. Azure Cosmos DB — это [глобально распределенная база данных](distribute-data-globally.md). Щелкните toomake карты hello пользователей доступен tooyour данных.
* Встроенные средства для расширенной проверки подлинности. С помощью Azure Cosmos DB можно легко реализовать популярные возможности, например [данные пользователей](https://aka.ms/documentdb-xamarin-todouser) или многопользовательские общие данные, без настраиваемого сложного кода проверки подлинности.
* Геопространственные запросы. Многие мобильные приложения включают геоконтекстные возможности уже сегодня. Первоклассная поддержка [картографических типов](geospatial.md), Azure Cosmos DB делает создание простой tooaccomplish эти интерфейсы.
* Двоичные вложения. Данные приложения часто включают большие двоичные объекты. Собственная поддержка для вложений позволяет упростить toouse Azure Cosmos DB как единый узел для данных приложений.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Руководство по Azure Cosmos DB и Xamarin
Здравствуйте, следуя учебника показано, как toobuild мобильных приложений с помощью Xamarin и Azure Cosmos DB. Hello полный исходный код можно найти в учебнике hello в [Xamarin и DB Cosmos Azure на GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).

### <a name="get-started"></a>Начало работы
Это легко tooget работы с Azure Cosmos DB. Перейдите toohello портал Azure и создайте новую учетную запись Azure Cosmos DB. Нажмите кнопку hello **краткого** вкладки. Загрузка hello Xamarin Forms задача список образец уже Подключенная учетная запись Azure Cosmos DB tooyour. 

![Быстрый запуск Azure Cosmos DB для мобильных приложений](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

Или при наличии существующего приложения Xamarin, можно добавить hello [пакет Azure Cosmos DB NuGet](documentdb-sdk-dotnet-core.md). Azure Cosmos DB поддерживает общие библиотеки для Xamarin.iOS, Xamarin.Android и Xamarin Forms.

### <a name="work-with-data"></a>Работа с данными
Записи данных хранятся в Azure Cosmos DB как бессхемные документы JSON в разнородных коллекциях. Можно хранить документы с разной структурой в hello одной коллекции:

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

В проектах Xamarin можно использовать запросы LINQ к бессхемным данным:

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>Добавление пользователей
Как и многие получить образцы работы, образец hello Azure Cosmos DB загруженный пройти проверку toohello службы жестко главного ключа в коде приложения hello. Это значение по умолчанию не рекомендуется для приложения требуется toorun в любом месте за исключением того, на ваш локальный эмулятор. Если неавторизованный пользователь получить hello главного ключа, все данные hello в базе данных Azure Cosmos учетной записи может быть нарушена. Вместо этого вы хотите tooaccess вашего приложения hello только записи для пользователя, выполнившего вход hello. Azure Cosmos DB разработчики приложений toogrant чтение или чтение и запись коллекции tooa разрешение, набор документов, сгруппированные по ключа секции или конкретный документ. 

Выполните эти шаги toomodify hello задача список приложение tooa многопользовательской задача список приложений. 

  1. Добавьте приложение tooyour входа с помощью Facebook, Active Directory или другими поставщиками.

  2. Создание коллекции Azure Cosmos DB UserItems с **/UserID** в качестве ключа секции hello. Указание hello ключа секции для коллекции позволяет Azure Cosmos DB tooscale бесконечно как hello число пользователей приложения возрастает, продолжая toooffer быстрые запросы.

  3. Добавьте брокер маркера ресурса Azure Cosmos DB. Этот простой веб-API проверяет подлинность пользователей и выдает кратковременных токены в toosigned пользователи с доступом только документы toohello в их секции. В этом примере брокер маркера ресурса размещен в службе приложений.

  4. Измените tooResource tooauthenticate приложения hello маркера брокера с Facebook, а запроса маркеров hello ресурсов для hello вошедших пользователей Facebook. Затем можно получить доступ к их данные в коллекции UserItems hello.  

Полный образец кода из этого примера можно найти в материалах по [брокеру маркера ресурса на сайте GitHub](http://aka.ms/documentdb-xamarin-todouser). Диаграмма иллюстрирует hello решения.

![Пользователи Azure Cosmos DB и брокер разрешений](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

Если требуется два toohello доступа toohave пользователей тот же список дел маркер доступа toohello дополнительных разрешений можно добавить в токен Broker ресурсов.

### <a name="scale-on-demand"></a>Масштабирование по необходимости
Azure Cosmos DB — это управляемая база данных как услуга. По мере роста базы пользователей не требуется tooworry о подготовке виртуальных машин и увеличение ядер. Все что нужно tootell Azure Cosmos DB —, сколько операций в секунду (пропускная способность) необходимый вашему приложению. Можно указать hello пропускной способности через hello **шкалы** с помощью измерения пропускной способности, вызывается единиц запроса (RUs) в секунду. Например, для чтения документа размером 1 КБ требуется 1 ЕЗ. Можно также добавить оповещения toohello **пропускной способности** метрики toomonitor hello увеличение трафика и программно изменить hello пропускную способность как предупреждения fire.

![Пропускная способность масштабирования по запросу в Azure Cosmos DB](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>Переход на глобальный масштаб
Как популярности прибыли вашего приложения пользователи могут получить по всему миру hello. Или может возникнуть необходимость toobe подготовлен для непредвиденных событий. Перейдите toohello портал Azure и откройте адрес Cosmos Azure DB. Щелкните ваш номер данных постоянно реплицировать tooany областей toomake карты hello через Здравствуй, мир. Эта возможность предоставит пользователям доступ к данным в любой точке мира. Можно также добавить toobe политики отработки отказа, подготовленных для ситуаций.

![Масштабирование Azure Cosmos DB в географических регионах](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

Поздравляем! Выполнить решение hello и мобильного приложения с помощью Xamarin и Azure Cosmos DB. Выполните аналогичную приложения Cordova toobuild действия с помощью Azure Cosmos DB JavaScript SDK hello и собственных приложений iOS и Android с помощью API-интерфейсы DB Cosmos REST Azure.

## <a name="next-steps"></a>Дальнейшие действия
* Просмотр исходного кода hello для [Xamarin и DB Cosmos Azure на GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).
* Загрузите hello [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md).
* Ознакомьтесь с другими примерами кода для [приложений .NET](documentdb-dotnet-samples.md).
* Узнайте о [расширенных возможностях запросов в Azure Cosmos DB](documentdb-sql-query.md).
* Узнайте о [геопространственной поддержке в Azure Cosmos DB](geospatial.md).



