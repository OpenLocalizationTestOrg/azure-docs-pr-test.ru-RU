---
title: "пропускная способность aaaProvision для Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, каким образом tooset провизионирование пропускной способности для вашего Azure Cosmos DB containsers, коллекций, диаграмм и таблиц."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Настройка пропускной способности для коллекций Azure Cosmos DB

Можно задать пропускную способность для вашей базы данных Azure Cosmos контейнеров в hello портал Azure или с помощью hello клиентских пакетов SDK. 

Привет, в следующей таблице перечислены hello пропускной способности, доступных для контейнеров.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Односекционный контейнер</strong></p></td>
            <td valign="top"><p><strong>Секционированный контейнер</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Минимальная пропускная способность</p></td>
            <td valign="top"><p>400 единиц запроса в секунду</p></td>
            <td valign="top"><p>2500 единиц запроса в секунду</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Максимальная пропускная способность</p></td>
            <td valign="top"><p>10 000 единиц запроса в секунду</p></td>
            <td valign="top"><p>Без ограничений</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>пропускная способность hello tooset с помощью портала Azure hello

1. В новом окне, откройте hello [портал Azure](https://portal.azure.com).
2. На левой панели hello щелкните **Azure Cosmos DB**, или нажмите кнопку **более служб** внизу hello прокрутите слишком**баз данных**и нажмите кнопку **Cosmos Azure DB**.
3. Выберите учетную запись Cosmos DB.
4. В новом окне приветствия щелкните **обозреватель данных (Предварительная версия)** в меню навигации hello.
5. В новом окне приветствия, разверните базу данных и контейнера и нажмите кнопку **параметры масштабирования и**.
6. В новом окне приветствия, введите новое значение пропускной способности hello в hello **пропускной способности** , а затем щелкните **Сохранить**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>пропускная способность hello tooset с помощью hello DocumentDB API для .NET

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>Часто задаваемые вопросы о пропускной способности

**Можно задать Мой сборки пропускной способности, чем 400 единиц Запросов в секунду.**

400 единиц Запросов в секунду — hello минимальная пропускная способность доступны в коллекции с одной секцией Cosmos DB (2500 единиц Запросов в секунду — hello минимальное для секционированных коллекций). Запрос единицы устанавливаются в интервалах 100 единиц Запросов в секунду, но пропускная способность невозможно задать too100 единиц Запросов в секунду или любое значение меньше, чем 400 единиц Запросов в секунду. Если вы ищете toodevelop экономичным способом и тестов Cosmos DB, можно использовать бесплатно hello [DB эмулятор Azure Cosmos](local-emulator.md), которое можно развертывать локально без затрат. 

**Как задать с помощью MongoDB API hello througput?**

Нет пропускной способности MongoDB API расширения tooset не существует. Hello рекомендуется hello toouse DocumentDB API, как показано в [пропускной способности hello tooset с помощью hello DocumentDB API для .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о подготовке и планеты шкалы переход с Cosmos DB. в разделе [секционирование и масштабирование с Cosmos DB](partition-data.md).
