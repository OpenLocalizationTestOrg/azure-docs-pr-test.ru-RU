---
title: "уровни производительности aaaDocumentDB API | Документы Microsoft"
description: "Узнайте, как уровни производительности DocumentDB API включить tooreserve пропускной способности на основе каждого контейнера."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Уровни производительности S1, S2 и S3 hello снятия с учета

> [!IMPORTANT] 
> Hello S1, S2 и S3 уровни производительности в этой статье будут выведены из эксплуатации и больше не доступны для новых учетных записей DocumentDB API.
>

В этой статье Общие сведения о S1, S2 и S3 уровни производительности и рассматриваются как hello коллекциях, которые используют эти уровни производительности будут коллекции секцией перенесенных toosingle на 1 августа 2017 г. После считывания в этой статье, вы будете иметь доступ tooanswer hello следующие вопросы:

- [Почему — производительности S1, S2 и S3 hello уровни выведены из эксплуатации?](#why-retired)
- [Как один раздел и секционированных коллекций соотносятся toohello S1, S2, S3 уровни производительности?](#compare)
- [Что мне требуются toodo tooensure непрерывного доступа к данным toomy?](#uninterrupted-access)
- [Как изменится Мои коллекции после миграции hello](#collection-change)
- [Как изменится my выставления счетов после я перенесенных toosingle секции коллекций](#billing-change)
- [Что делать, если мне нужен объем хранилища больше 10 ГБ?](#more-storage-needed)
- [Можно ли изменить между hello S1, S2 и S3 уровни производительности до 1 августа 2017 г.](#change-before)
- [Как узнать, что моя коллекция перенесена?](#when-migrated)
- [Как перенести из hello S1, S2, S3 коллекции производительности уровней toosingle секции вручную?](#migrate-diy)
- [Как на мне отразится перенос, если я являюсь пользователем подписки EA?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>Почему — производительности S1, S2 и S3 hello уровни выведены из эксплуатации?

уровни производительности S1, S2 и S3 Hello сделать не предложение hello гибкость, обеспечиваемая DocumentDB API коллекций. Hello S1, S2, S3 уровни производительности, hello пропускной способности и емкость были предварительно установлены и не предложена эластичности. Azure Cosmos DB теперь предоставляет возможность toocustomize hello пропускной способности и объема хранилища, предлагающее гораздо более гибкие возможности вашего tooscale возможность при изменении потребностей.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>Как один раздел и секционированных коллекций соотносятся toohello S1, S2, S3 уровни производительности?

Привет, в следующей таблице сравниваются hello пропускной способности и хранения параметров, доступных в коллекции с одной секцией, секционированных коллекций и S1, S2, S3 уровни производительности. В этом примере данные приводятся для региона "Восточная часть США 2":

|   |Секционированная коллекция|Односекционная коллекция|S1|S2|S3|
|---|---|---|---|---|---|
|Максимальная пропускная способность|Без ограничений|10 000 ЕЗ/с|250 ЕЗ/с|1000 ЕЗ/с|2500 ЕЗ/с|
|Минимальная пропускная способность|2500 ЕЗ/с|400 ЕЗ/с|250 ЕЗ/с|1000 ЕЗ/с|2500 ЕЗ/с|
|Максимальный объем хранилища|Без ограничений|10 ГБ|10 ГБ|10 ГБ|10 ГБ|
|Цена (ежемесячно)|Пропускная способность: 6 долл. США за 100 ЕЗ/с<br><br>Хранилище: 0,25 долл. США за 1 ГБ|Пропускная способность: 6 долл. США за 100 ЕЗ/с<br><br>Хранилище: 0,25 долл. США за 1 ГБ|25 долл. США|50 долл. США|100 долл. США|

Вы являетесь пользователем подписки EA? Если это так, то ознакомьтесь с разделом [Как на мне отразится перенос, если я являюсь пользователем подписки EA?](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>Что мне требуются toodo tooensure непрерывного доступа к данным toomy?

Nothing, Cosmos DB обработки hello миграции для вас. При наличии коллекцию S1, S2 и S3 текущей коллекции будет коллекции перенесенных tooa одной секции на 31 июля 2017 г. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Как изменится Мои коллекции после миграции hello

Если у вас есть набор S1, можно перенесенных tooa коллекции одну секцию с пропускной способностью 400 единиц Запросов в секунду. 400 единиц Запросов в секунду — hello наименьшее пропускной способности в коллекции с одной секцией. Тем не менее стоимость hello 400 единиц Запросов в секунду в коллекции одну секцию — приблизительно hello, такими же, как оплаты по вашей коллекции S1 приветствия и 250 единиц Запросов в секунду — так вы платите не для hello лишние 150 tooyou доступных единиц Запросов в секунду.

Если имеется коллекция S2 можно коллекции перенесенных tooa один раздел с 1 K единиц Запросов в секунду. Вы увидите уровень пропускной способности tooyour без изменений.

Если имеется коллекция S3 можно перенесенных tooa коллекции одну секцию с 2,5 K единиц Запросов в секунду. Вы увидите уровень пропускной способности tooyour без изменений.

В каждом из этих случаев после миграции коллекции необходимо быть может toocustomize уровень пропускной способности, или масштабирования вверх и вниз как пользователи tooyour необходимые tooprovide доступа малой задержкой. уровень пропускной способности toochange hello после переноса коллекции, просто откройте адрес Cosmos DB в hello портал Azure, щелкните шкалу, выберите коллекции и измените уровень пропускной способности hello, как показано на следующий снимок экрана приветствия:

![Как tooscale пропускной способности в hello портал Azure](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>Как изменится my выставления счетов после я коллекции с одной секцией перенесенных toohello

При условии, что у коллекций 10 S1, 1 ГБ памяти для каждого региона Востоке hello, и переместить эти 10 S1 коллекций too10 коллекции с одной секцией на 400 единиц Запросов в секунду (hello минимальный уровень). Следует коллекций hello 10 одну секцию для полного месяца счете будет выглядеть следующим образом:

![S1 цены на 10 коллекций сравнение too10 коллекций с помощью цены для коллекции одну секцию](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>Что делать, если мне нужен объем хранилища больше 10 ГБ?

Коллекции с помощью S1, S2 и S3 уровня производительности, так и коллекция одной секции, которые имеют 10 ГБ доступного хранилища, можно использовать toomigrate средство переноса данных DB Cosmos hello, вашей tooa данные секционированы коллекции с практически неограниченное хранилище. Дополнительные сведения о преимуществах hello секционированную коллекцию, в разделе [секционирование и масштабирование в базе данных Azure Cosmos](documentdb-partition-data.md). Сведения о том, как toomigrate см. в S1, S2, S3 или коллекция tooa секционированы одну секцию, [перенос из одной секции toopartitioned коллекций](documentdb-partition-data.md#migrating-from-single-partition). 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>Можно ли изменить между hello S1, S2 и S3 уровни производительности до 1 августа 2017 г.

Только учетные записи с S1, S2 и S3 производительность будет может toochange и alter уровни производительности уровня через портал hello или программными средствами. По 1 августа 2017 г. hello S1, S2, и уровни производительности S3 больше не будут доступны. При переключении из коллекции один раздел tooa S1, S3 или S3 не может возвращать toohello уровни производительности S1, S2 и S3.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>Как узнать, что моя коллекция перенесена?

Hello миграции будет выполняться на 31 июля 2017 г. Если имеется коллекция, использующий hello S1, S2 или S3 производительности уровней, hello Cosmos DB team свяжется с вами по электронной почте до выполнения миграции hello. После завершения миграции hello на 1 августа 2017 г., hello портал Azure будет отображаться, ваша коллекция использует стандартные цены.

![Как tooconfirm вашей коллекции имеет перенести toohello ценовой категории Standard](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>Как перенести из hello S1, S2, S3 коллекции производительности уровней toosingle секции вручную?

Можно перенести из hello S1, S2, и уровни производительности S3 коллекций toosingle секции, с помощью hello портал Azure или программным путем. Из параметров hello гибкие пропускной способности, доступных в коллекции с одной секцией это можно сделать на собственных до 1 августа toobenefit или к коллекции из мы перенесем на 31 июля 2017 г.

**с помощью портала Azure hello коллекции секцией toosingle toomigrate**

1. В hello [ **портал Azure**](https://portal.azure.com), нажмите кнопку **Azure Cosmos DB**, выберите toomodify учетной записи Cosmos DB hello. 
 
    Если **Azure Cosmos DB** не hello Jumpbar, нажмите кнопку >, прокрутите слишком**баз данных**выберите **Azure Cosmos DB**и затем выберите учетную запись DocumentDB hello.  

2. Ресурс меню hello под **контейнеры**, нажмите кнопку **шкалы**, выберите из раскрывающегося списка hello toomodify hello коллекции и нажмите кнопку **ценовую категорию**. Учетные записи со стандартной пропускной способностью имеют ценовую категорию S1, S2 или S3.  В hello **выберите ценовую категорию** колонке нажмите кнопку **Стандартная** пропускной способности определяемых toouser toochange и нажмите кнопку **выберите** toosave внесенные изменения.

    ![Снимок колонку параметров hello, показывающий, где toochange hello значение пропускной способности](./media/performance-levels/change-performance-set-thoughput.png)

3. Обратно в hello **шкалы** колонки, hello **ценовую категорию** изменяется слишком**Стандартная** и hello **пропускной способности (единиц Запросов в секунду)** появится окно с значение по умолчанию 400. Пропускная способность hello набор от 400 до 10 000 [единиц запросов](request-units.md)обращений (единиц Запросов в секунду). Hello **оценка ежемесячный счет** внизу hello hello Страница обновится, автоматически tooprovide оценку hello ежемесячную плату. 

    >[!IMPORTANT] 
    > После сохранения изменений и переместить toohello ценовой категории Standard, нельзя произвести откат toohello уровни производительности S1, S2 и S3.

4. Нажмите кнопку **Сохранить** toosave изменения.

    Если в ходе работы выяснится, что требуется более высокая пропускная способность (больше 10 000 единиц запроса в секунду) или больший объем хранилища (больше 10 ГБ), то вы можете создать секционированную коллекцию. toomigrate коллекции tooa секционированные коллекции одну секцию, в разделе [перенос из одной секции toopartitioned коллекций](documentdb-partition-data.md#migrating-from-single-partition).

    > [!NOTE]
    > Изменение с S1, S2 и S3 tooStandard может занять too2 минут.
    > 
    > 

**Здравствуйте, toomigrate toosingle секции коллекций с помощью пакета SDK для .NET**

Другой вариант изменения уровней производительности вашей коллекции — с помощью наших пакетов SDK. В этом разделе рассматривается только изменение коллекции производительности уровня с помощью наших [API .NET для DocumentDB](documentdb-sdk-dotnet.md), но hello процесс аналогичен для наших других пакетов SDK.

Ниже приведен фрагмент кода для изменения too5 пропускную способность коллекции hello, 000 единиц запросов в секунду.
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

Посетите [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview Дополнительные примеры и Дополнительные сведения о наши методы предложения:

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>Как на мне отразится перенос, если я являюсь пользователем подписки EA?

Клиентам EA будут цены, защищены только hello конце своего текущего контракта.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о ценах и управление данными с помощью Azure Cosmos DB, изучение этих ресурсов.

1.  [Секционирование, ключи секции и масштабирование в Cosmos DB](documentdb-partition-data.md). Понимать hello различие между контейнера одной секции секционированной контейнеров, а также советы по реализации секционирования tooscale стратегии без проблем.
2.  [Страница цен Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). Дополнительные сведения о стоимости hello подготовки пропускную способность и использование хранилища.
3.  [Единицы запроса в DocumentDB](request-units.md). Понимать hello потребление пропускной способности для типов различные операции, например, чтение, запись, запрос.
