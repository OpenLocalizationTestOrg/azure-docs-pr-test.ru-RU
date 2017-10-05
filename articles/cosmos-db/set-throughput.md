---
title: "Подготовка пропускной способности для Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как задать подготовленную пропускную способность для контейнеров, коллекций, графов и таблиц Azure Cosmos DB."
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
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="32368-103">Настройка пропускной способности для коллекций Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="32368-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="32368-104">Пропускную способность для контейнеров Azure Cosmos DB можно настроить на портале Azure или с помощью клиентских пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="32368-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="32368-105">В следующей таблице указана пропускная способность, доступная для каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="32368-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="32368-106"><strong>Односекционный контейнер</strong></span><span class="sxs-lookup"><span data-stu-id="32368-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="32368-107"><strong>Секционированный контейнер</strong></span><span class="sxs-lookup"><span data-stu-id="32368-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="32368-108">Минимальная пропускная способность</span><span class="sxs-lookup"><span data-stu-id="32368-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="32368-109">400 единиц запроса в секунду</span><span class="sxs-lookup"><span data-stu-id="32368-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="32368-110">2500 единиц запроса в секунду</span><span class="sxs-lookup"><span data-stu-id="32368-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="32368-111">Максимальная пропускная способность</span><span class="sxs-lookup"><span data-stu-id="32368-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="32368-112">10 000 единиц запроса в секунду</span><span class="sxs-lookup"><span data-stu-id="32368-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="32368-113">Без ограничений</span><span class="sxs-lookup"><span data-stu-id="32368-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="32368-114">Настройка пропускной способности с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="32368-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="32368-115">В новом окне откройте [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32368-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="32368-116">На панели слева щелкните **Azure Cosmos DB** или выберите внизу пункт **Больше служб**, перейдите к разделу **Базы данных** и выберите **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="32368-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="32368-117">Выберите учетную запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="32368-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="32368-118">В новом окне в меню навигации щелкните **Data Explorer (Preview)** (Обозреватель данных (предварительная версия)).</span><span class="sxs-lookup"><span data-stu-id="32368-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="32368-119">В новом окне разверните узел базы данных и контейнера и щелкните **Scale & Settings** (Параметры масштабирования).</span><span class="sxs-lookup"><span data-stu-id="32368-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="32368-120">В новом окне в поле **Пропускная способность** введите новое значение пропускной способности, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="32368-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="32368-121">Настройка пропускной способности с помощью DocumentDB API для .NET</span><span class="sxs-lookup"><span data-stu-id="32368-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="32368-122">Часто задаваемые вопросы о пропускной способности</span><span class="sxs-lookup"><span data-stu-id="32368-122">Throughput FAQ</span></span>

<span data-ttu-id="32368-123">**Можно ли задать значение пропускной способности ниже 400 ЕЗ/с?**</span><span class="sxs-lookup"><span data-stu-id="32368-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="32368-124">400 ЕЗ/с — это минимальное значение пропускной способности, доступное для односекционных коллекций Cosmos DB (минимальное значение для секционированных коллекций — 2500 ЕЗ/с).</span><span class="sxs-lookup"><span data-stu-id="32368-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="32368-125">Единицы запроса можно задать с интервалом в 100 ЕЗ/с, но невозможно задать значение пропускной способности равное 100 ЕЗ/с или любое значение менее 400 ЕЗ/с.</span><span class="sxs-lookup"><span data-stu-id="32368-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="32368-126">Чтобы определить экономически эффективный метод разработки и тестирования в Cosmos DB, можно воспользоваться бесплатным [эмулятором Azure Cosmos DB](local-emulator.md), который развертывается локально и без дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="32368-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="32368-127">**Как настроить пропускную способность с использованием API MongoDB?**</span><span class="sxs-lookup"><span data-stu-id="32368-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="32368-128">Для настройки пропускной способности нет расширения API MongoDB.</span><span class="sxs-lookup"><span data-stu-id="32368-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="32368-129">Мы рекомендуем использовать DocumentDB API, как показано в разделе [Настройка пропускной способности с помощью API DocumentDB для .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="32368-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32368-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32368-130">Next steps</span></span>

<span data-ttu-id="32368-131">Дополнительные сведения о подготовке и глобальном масштабировании с помощью Cosmos DB см. в статье [Секционирование в базе данных Azure Cosmos DB с помощью API DocumentDB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="32368-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
