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
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="93ff0-103">Настройка пропускной способности для коллекций Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="93ff0-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="93ff0-104">Можно задать пропускную способность для вашей базы данных Azure Cosmos контейнеров в hello портал Azure или с помощью hello клиентских пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="93ff0-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="93ff0-105">Привет, в следующей таблице перечислены hello пропускной способности, доступных для контейнеров.</span><span class="sxs-lookup"><span data-stu-id="93ff0-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="93ff0-106"><strong>Односекционный контейнер</strong></span><span class="sxs-lookup"><span data-stu-id="93ff0-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="93ff0-107"><strong>Секционированный контейнер</strong></span><span class="sxs-lookup"><span data-stu-id="93ff0-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="93ff0-108">Минимальная пропускная способность</span><span class="sxs-lookup"><span data-stu-id="93ff0-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="93ff0-109">400 единиц запроса в секунду</span><span class="sxs-lookup"><span data-stu-id="93ff0-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="93ff0-110">2500 единиц запроса в секунду</span><span class="sxs-lookup"><span data-stu-id="93ff0-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="93ff0-111">Максимальная пропускная способность</span><span class="sxs-lookup"><span data-stu-id="93ff0-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="93ff0-112">10 000 единиц запроса в секунду</span><span class="sxs-lookup"><span data-stu-id="93ff0-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="93ff0-113">Без ограничений</span><span class="sxs-lookup"><span data-stu-id="93ff0-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="93ff0-114">пропускная способность hello tooset с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="93ff0-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="93ff0-115">В новом окне, откройте hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="93ff0-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="93ff0-116">На левой панели hello щелкните **Azure Cosmos DB**, или нажмите кнопку **более служб** внизу hello прокрутите слишком**баз данных**и нажмите кнопку **Cosmos Azure DB**.</span><span class="sxs-lookup"><span data-stu-id="93ff0-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="93ff0-117">Выберите учетную запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="93ff0-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="93ff0-118">В новом окне приветствия щелкните **обозреватель данных (Предварительная версия)** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="93ff0-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="93ff0-119">В новом окне приветствия, разверните базу данных и контейнера и нажмите кнопку **параметры масштабирования и**.</span><span class="sxs-lookup"><span data-stu-id="93ff0-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="93ff0-120">В новом окне приветствия, введите новое значение пропускной способности hello в hello **пропускной способности** , а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="93ff0-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="93ff0-121">пропускная способность hello tooset с помощью hello DocumentDB API для .NET</span><span class="sxs-lookup"><span data-stu-id="93ff0-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

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

## <a name="throughput-faq"></a><span data-ttu-id="93ff0-122">Часто задаваемые вопросы о пропускной способности</span><span class="sxs-lookup"><span data-stu-id="93ff0-122">Throughput FAQ</span></span>

<span data-ttu-id="93ff0-123">**Можно задать Мой сборки пропускной способности, чем 400 единиц Запросов в секунду.**</span><span class="sxs-lookup"><span data-stu-id="93ff0-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="93ff0-124">400 единиц Запросов в секунду — hello минимальная пропускная способность доступны в коллекции с одной секцией Cosmos DB (2500 единиц Запросов в секунду — hello минимальное для секционированных коллекций).</span><span class="sxs-lookup"><span data-stu-id="93ff0-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="93ff0-125">Запрос единицы устанавливаются в интервалах 100 единиц Запросов в секунду, но пропускная способность невозможно задать too100 единиц Запросов в секунду или любое значение меньше, чем 400 единиц Запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="93ff0-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="93ff0-126">Если вы ищете toodevelop экономичным способом и тестов Cosmos DB, можно использовать бесплатно hello [DB эмулятор Azure Cosmos](local-emulator.md), которое можно развертывать локально без затрат.</span><span class="sxs-lookup"><span data-stu-id="93ff0-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="93ff0-127">**Как задать с помощью MongoDB API hello througput?**</span><span class="sxs-lookup"><span data-stu-id="93ff0-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="93ff0-128">Нет пропускной способности MongoDB API расширения tooset не существует.</span><span class="sxs-lookup"><span data-stu-id="93ff0-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="93ff0-129">Hello рекомендуется hello toouse DocumentDB API, как показано в [пропускной способности hello tooset с помощью hello DocumentDB API для .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="93ff0-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93ff0-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="93ff0-130">Next steps</span></span>

<span data-ttu-id="93ff0-131">toolearn Дополнительные сведения о подготовке и планеты шкалы переход с Cosmos DB. в разделе [секционирование и масштабирование с Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="93ff0-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
