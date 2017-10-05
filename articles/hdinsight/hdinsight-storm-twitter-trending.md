---
title: "Определение популярных тем в Twitter с помощью Apache Storm в HDInsight | Документация Майкрософт"
description: "Узнайте, как с помощью Trident можно создать топологию Apache Storm, которая будет определять популярные темы в Twitter на основе хэш-тегов."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="9b20d-103">Определение популярных тем в Twitter с помощью Apache Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b20d-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="9b20d-104">Узнайте, как с помощью Trident можно создать топологию Storm, которая будет определять популярные темы (хэш-теги) в Twitter.</span><span class="sxs-lookup"><span data-stu-id="9b20d-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="9b20d-105">Trident — это высокоуровневая абстракция, которая предоставляет такие средства, как соединения, функции, фильтры, агрегирование и группирование.</span><span class="sxs-lookup"><span data-stu-id="9b20d-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="9b20d-106">Кроме того, Trident добавляет примитивы для выполнения добавочной обработки с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="9b20d-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="9b20d-107">В качестве примера в этом документе приведена топология Trident с пользовательскими spout и функцией.</span><span class="sxs-lookup"><span data-stu-id="9b20d-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="9b20d-108">В ней также используется несколько встроенных функций Trident.</span><span class="sxs-lookup"><span data-stu-id="9b20d-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="9b20d-109">Требования</span><span class="sxs-lookup"><span data-stu-id="9b20d-109">Requirements</span></span>

* <span data-ttu-id="9b20d-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java и пакет JDK 1.8</a>.</span><span class="sxs-lookup"><span data-stu-id="9b20d-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="9b20d-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="9b20d-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="9b20d-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="9b20d-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="9b20d-113">Учетная запись разработчика Twitter</span><span class="sxs-lookup"><span data-stu-id="9b20d-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="9b20d-114">Скачивание проекта</span><span class="sxs-lookup"><span data-stu-id="9b20d-114">Download the project</span></span>

<span data-ttu-id="9b20d-115">С помощью приведенного ниже кода клонируйте проект локально.</span><span class="sxs-lookup"><span data-stu-id="9b20d-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="9b20d-116">Общие сведения о топологии</span><span class="sxs-lookup"><span data-stu-id="9b20d-116">Understanding the topology</span></span>

<span data-ttu-id="9b20d-117">На следующей схеме показано, как данные перемещаются в топологии.</span><span class="sxs-lookup"><span data-stu-id="9b20d-117">The following diagram shows of how data flows through this topology:</span></span>

![Топология](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="9b20d-119">Это упрощенное представление топологии.</span><span class="sxs-lookup"><span data-stu-id="9b20d-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="9b20d-120">Между узлами в кластере распределено несколько экземпляров компонентов.</span><span class="sxs-lookup"><span data-stu-id="9b20d-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="9b20d-121">Реализующий топологию код Trident выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9b20d-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="9b20d-122">Этот код выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9b20d-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="9b20d-123">Создает поток из spout.</span><span class="sxs-lookup"><span data-stu-id="9b20d-123">Creates a stream from the spout.</span></span> <span data-ttu-id="9b20d-124">Воронка извлекает из Твиттера твиты и фильтрует их по определенным ключевым словам (в нашем примере это love, music и coffee).</span><span class="sxs-lookup"><span data-stu-id="9b20d-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="9b20d-125">Пользовательская функция HashtagExtractor извлекает из каждого твита хэш-теги.</span><span class="sxs-lookup"><span data-stu-id="9b20d-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="9b20d-126">Хэш-теги отправляются в поток.</span><span class="sxs-lookup"><span data-stu-id="9b20d-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="9b20d-127">Поток группируется по хэш-тегам и передается в агрегатор.</span><span class="sxs-lookup"><span data-stu-id="9b20d-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="9b20d-128">Агрегатор определяет количество вхождений каждого хэш-тега.</span><span class="sxs-lookup"><span data-stu-id="9b20d-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="9b20d-129">Эти данные сохраняются в памяти.</span><span class="sxs-lookup"><span data-stu-id="9b20d-129">This data is persisted in memory.</span></span> <span data-ttu-id="9b20d-130">Наконец отправляется новый поток, содержащий хэш-тег и количество вхождений.</span><span class="sxs-lookup"><span data-stu-id="9b20d-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="9b20d-131">Применяется сборка **FirstN** для возврата только первых 10 значений по полю количества.</span><span class="sxs-lookup"><span data-stu-id="9b20d-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="9b20d-132">Дополнительные сведения о работе с Trident см. в документе [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) (Обзор API Trident).</span><span class="sxs-lookup"><span data-stu-id="9b20d-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="9b20d-133">Воронка</span><span class="sxs-lookup"><span data-stu-id="9b20d-133">The spout</span></span>

<span data-ttu-id="9b20d-134">Для извлечения твитов из Twitter воронка **TwitterSpout** использует библиотеку [Twitter4j](http://twitter4j.org/en/).</span><span class="sxs-lookup"><span data-stu-id="9b20d-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="9b20d-135">Создается фильтр для слов __love__, **music** и **coffee**.</span><span class="sxs-lookup"><span data-stu-id="9b20d-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="9b20d-136">Входящие твиты (состояния), соответствующие фильтру, сохраняются в связанной блокирующей очереди.</span><span class="sxs-lookup"><span data-stu-id="9b20d-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="9b20d-137">Наконец элементы извлекаются из очереди и передаются в топологию.</span><span class="sxs-lookup"><span data-stu-id="9b20d-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="9b20d-138">HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="9b20d-138">The HashtagExtractor</span></span>

<span data-ttu-id="9b20d-139">Для извлечения хэш-тегов используется метод [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--). Он позволяет получить все содержащиеся в твитах хэш-теги.</span><span class="sxs-lookup"><span data-stu-id="9b20d-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="9b20d-140">Затем они отправляются в поток.</span><span class="sxs-lookup"><span data-stu-id="9b20d-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="9b20d-141">Настройка Twitter</span><span class="sxs-lookup"><span data-stu-id="9b20d-141">Configure Twitter</span></span>

<span data-ttu-id="9b20d-142">Чтобы зарегистрировать новое приложение для Твиттера и получить ключ потребителя и маркер доступа, необходимые для чтения из Твиттера, сделайте вот что.</span><span class="sxs-lookup"><span data-stu-id="9b20d-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="9b20d-143">Перейдите на страницу [Twitter Apps](https://apps.twitter.com) (Приложения для Twitter) и нажмите кнопку **Create new app** (Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="9b20d-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="9b20d-144">После заполнения формы оставьте поле **Callback URL** (URL-адрес обратного вызова) пустым.</span><span class="sxs-lookup"><span data-stu-id="9b20d-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="9b20d-145">Когда приложение создано, перейдите на вкладку **Keys and Access Tokens** (Ключи и маркеры доступа).</span><span class="sxs-lookup"><span data-stu-id="9b20d-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="9b20d-146">Скопируйте **ключ** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="9b20d-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="9b20d-147">Если у вас нет маркеров, в нижней части страницы выберите **Create my access token** (Создать мой маркер доступа).</span><span class="sxs-lookup"><span data-stu-id="9b20d-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="9b20d-148">Создав маркеры, скопируйте **маркер доступа** и **секрет маркера доступа**.</span><span class="sxs-lookup"><span data-stu-id="9b20d-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="9b20d-149">В клонированном ранее проекте **TwitterSpoutTopology** откройте файл **resources/twitter4j.properties** и добавьте в него сведения, полученные на предыдущих этапах. После этого сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9b20d-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="9b20d-150">Сборка топологии</span><span class="sxs-lookup"><span data-stu-id="9b20d-150">Build the topology</span></span>

<span data-ttu-id="9b20d-151">Скомпилируйте проект с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="9b20d-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="9b20d-152">Тестирование топологии</span><span class="sxs-lookup"><span data-stu-id="9b20d-152">Test the topology</span></span>

<span data-ttu-id="9b20d-153">Чтобы локально протестировать топологию, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9b20d-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="9b20d-154">После запуска топологии вы должны увидеть отладочную информацию, содержащую хэш-теги и количество их вхождений. Эти данные отправляет топология.</span><span class="sxs-lookup"><span data-stu-id="9b20d-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="9b20d-155">Результат должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9b20d-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="9b20d-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b20d-156">Next steps</span></span>

<span data-ttu-id="9b20d-157">Протестировав топологию локально, вы можете ее развернуть. Сведения о том, как это сделать, см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Windows и управление ими](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9b20d-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="9b20d-158">Возможно, вас также заинтересуют следующие разделы по Storm:</span><span class="sxs-lookup"><span data-stu-id="9b20d-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="9b20d-159">Разработка топологий на Java для Storm в HDInsight с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="9b20d-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="9b20d-160">Разработка топологий для Storm в HDInsight на C# с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b20d-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="9b20d-161">Дополнительные примеры Storm для HDinsight:</span><span class="sxs-lookup"><span data-stu-id="9b20d-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="9b20d-162">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b20d-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

