---
title: "Обновление REST API службы поиска Azure до версии 2016-09-01 | Документация Майкрософт"
description: "Обновление REST API службы поиска Azure до версии 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="f71e1-103">Обновление REST API службы поиска Azure до версии 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="f71e1-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="f71e1-104">Если вы используете предварительную версию 2015-02-28 или 2015-02-28-Preview [REST API службы поиска Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx) или более раннюю, эта статья поможет вам обновить приложения для использования следующей общедоступной версии API 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="f71e1-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="f71e1-105">Версия 2016-09-01 REST API содержит некоторые изменения из более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="f71e1-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="f71e1-106">Эти отличия в основном обратно совместимы, поэтому изменение кода потребует минимальных усилий в зависимости от версии, которая использовался ранее.</span><span class="sxs-lookup"><span data-stu-id="f71e1-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="f71e1-107">В разделе [Действия по обновлению](#UpgradeSteps) вы найдете инструкции о том, как изменить код для использования новой версии API.</span><span class="sxs-lookup"><span data-stu-id="f71e1-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="f71e1-108">Экземпляр службы поиска Azure поддерживает несколько версий REST API, включая последнюю.</span><span class="sxs-lookup"><span data-stu-id="f71e1-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="f71e1-109">Можно продолжать использовать версию, которая больше не является последней, но рекомендуется выполнить перенос кода, чтобы использовать последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="f71e1-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="f71e1-110">Новые возможности в версии 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="f71e1-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="f71e1-111">Версия 2016-09-01 — это второй общедоступный выпуск REST API службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="f71e1-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="f71e1-112">Новые возможности в этой версии API:</span><span class="sxs-lookup"><span data-stu-id="f71e1-112">New features in this API version include:</span></span>

* <span data-ttu-id="f71e1-113">[Пользовательские анализаторы](https://aka.ms/customanalyzers) позволяют получить контроль над процессом преобразования текста в индексируемые и поддерживающие поиск токены.</span><span class="sxs-lookup"><span data-stu-id="f71e1-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="f71e1-114">Индексаторы [хранилища BLOB-объектов Azure](search-howto-indexing-azure-blob-storage.md) и [хранилища таблиц Azure](search-howto-indexing-azure-tables.md) позволяют легко импортировать данные из хранилища Azure в службу поиска Azure по расписанию или по требованию.</span><span class="sxs-lookup"><span data-stu-id="f71e1-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="f71e1-115">[Сопоставления полей](search-indexer-field-mappings.md) позволяют настроить, каким образом индексаторы будут импортировать данные в службу поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="f71e1-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="f71e1-116">Теги eTag позволяют обновлять определения индексов, индексаторов и источников данных безопасно в отношении параллельного выполнения.</span><span class="sxs-lookup"><span data-stu-id="f71e1-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="f71e1-117">Действия по обновлению</span><span class="sxs-lookup"><span data-stu-id="f71e1-117">Steps to upgrade</span></span>
<span data-ttu-id="f71e1-118">При обновлении с версии 2015-02-28 вам, вероятно, понадобится изменить в коде только номер версии.</span><span class="sxs-lookup"><span data-stu-id="f71e1-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="f71e1-119">Изменение кода может потребоваться только в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="f71e1-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="f71e1-120">Код завершается ошибкой, если в ответе API возвращаются нераспознанные свойства.</span><span class="sxs-lookup"><span data-stu-id="f71e1-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="f71e1-121">По умолчанию приложение должно игнорировать свойства, которые не распознаются.</span><span class="sxs-lookup"><span data-stu-id="f71e1-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="f71e1-122">Код сохраняет запросы API и пытается повторно отправить их в новую версию API.</span><span class="sxs-lookup"><span data-stu-id="f71e1-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="f71e1-123">Например, это может произойти, если приложение сохраняет маркеры продолжения, возвращенные API поиска (см. сведения об `@search.nextPageParameters` в [справочнике по API поиска](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="f71e1-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="f71e1-124">Если одна из этих ситуаций относится к вам, может потребоваться изменить код соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="f71e1-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="f71e1-125">В противном случае вам понадобится вносить изменения, только если вы хотите использовать [новые возможности](#WhatsNew) версии 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="f71e1-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="f71e1-126">Тоже самое относится и к обновлению с версии 2015-02-28-Preview. Однако следует учитывать, что некоторые возможности предварительной версии недоступны в версии 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="f71e1-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="f71e1-127">Поддержка индексатора хранилища BLOB-объектов Azure для CSV-файлов и больших двоичных объектов, содержащих массивы JSON.</span><span class="sxs-lookup"><span data-stu-id="f71e1-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="f71e1-128">синонимы;</span><span class="sxs-lookup"><span data-stu-id="f71e1-128">Synonyms</span></span>
* <span data-ttu-id="f71e1-129">Запросы "Скорее всего".</span><span class="sxs-lookup"><span data-stu-id="f71e1-129">"More like this" queries</span></span>

<span data-ttu-id="f71e1-130">Если код использует эти возможности, вы не сможете выполнить обновление до версии 2016-09-01, если не отключите их.</span><span class="sxs-lookup"><span data-stu-id="f71e1-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f71e1-131">Помните, что предварительные версии API предназначены для тестирования и ознакомления. Они не должны использоваться в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f71e1-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="f71e1-132">Заключение</span><span class="sxs-lookup"><span data-stu-id="f71e1-132">Conclusion</span></span>
<span data-ttu-id="f71e1-133">Дополнительные сведения об использовании REST API службы поиска Azure см. в [справочнике по API](https://msdn.microsoft.com/library/azure/dn798935.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="f71e1-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="f71e1-134">Будем рады вашим отзывам о службе поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="f71e1-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="f71e1-135">Если вы столкнулись с проблемами, то всегда можете обратиться за помощью на [форуме по службе поиску Azure на сайте MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) или [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="f71e1-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="f71e1-136">Если вы задаете вопрос о службе поиска Azure на сайте StackOverflow, обязательно добавьте к нему `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="f71e1-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="f71e1-137">Благодарим вас за использование поиска Azure!</span><span class="sxs-lookup"><span data-stu-id="f71e1-137">Thank you for using Azure Search!</span></span>

