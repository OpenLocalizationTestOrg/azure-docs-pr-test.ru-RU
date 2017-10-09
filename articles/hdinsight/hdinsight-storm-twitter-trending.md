---
title: "aaaTwitter тенденций разделы с описанием Apache Storm на HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Trident toocreate Apache Storm топологию, которая определяет статистические разделы в Twitter на основе хэш."
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
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="9933c-103">Определение популярных тем в Twitter с помощью Apache Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="9933c-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="9933c-104">Узнайте, как toocreate Trident toouse топологии Storm, определяет сведения о тенденциях разделы (хэш теги) в Twitter.</span><span class="sxs-lookup"><span data-stu-id="9933c-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="9933c-105">Trident — это высокоуровневая абстракция, которая предоставляет такие средства, как соединения, функции, фильтры, агрегирование и группирование.</span><span class="sxs-lookup"><span data-stu-id="9933c-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="9933c-106">Кроме того, Trident добавляет примитивы для выполнения добавочной обработки с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="9933c-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="9933c-107">пример Hello, используемые в этом документе является топологии Trident пользовательских spout и функции.</span><span class="sxs-lookup"><span data-stu-id="9933c-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="9933c-108">В ней также используется несколько встроенных функций Trident.</span><span class="sxs-lookup"><span data-stu-id="9933c-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="9933c-109">Требования</span><span class="sxs-lookup"><span data-stu-id="9933c-109">Requirements</span></span>

* <span data-ttu-id="9933c-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java и hello JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="9933c-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="9933c-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="9933c-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="9933c-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="9933c-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="9933c-113">Учетная запись разработчика Twitter</span><span class="sxs-lookup"><span data-stu-id="9933c-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="9933c-114">Загрузите проект hello</span><span class="sxs-lookup"><span data-stu-id="9933c-114">Download hello project</span></span>

<span data-ttu-id="9933c-115">Используйте следующие hello кода проекта hello tooclone локально.</span><span class="sxs-lookup"><span data-stu-id="9933c-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="9933c-116">Основные сведения о топологии hello</span><span class="sxs-lookup"><span data-stu-id="9933c-116">Understanding hello topology</span></span>

<span data-ttu-id="9933c-117">Hello следующей схеме показано из потоки данных посредством этой топологии:</span><span class="sxs-lookup"><span data-stu-id="9933c-117">hello following diagram shows of how data flows through this topology:</span></span>

![Топология](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="9933c-119">Эта диаграмма представляет упрощенное представление топологии hello.</span><span class="sxs-lookup"><span data-stu-id="9933c-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="9933c-120">Несколько экземпляров компонентов hello распределены между узлами hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="9933c-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="9933c-121">Hello Trident код, который реализует топологии hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9933c-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="9933c-122">Этот код выполняет следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="9933c-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="9933c-123">Создает поток из hello spout.</span><span class="sxs-lookup"><span data-stu-id="9933c-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="9933c-124">Hello spout извлекает твиты из Twitter и фильтрует их определенные ключевые слова (любви, музыке и кофе в этом примере).</span><span class="sxs-lookup"><span data-stu-id="9933c-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="9933c-125">HashtagExtractor пользовательской функции, — используется tooextract хэш тегов из каждой твит.</span><span class="sxs-lookup"><span data-stu-id="9933c-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="9933c-126">теги Hello хэш — порожденную toohello потока.</span><span class="sxs-lookup"><span data-stu-id="9933c-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="9933c-127">Hello потока сгруппированы по тегу хэш и передается tooan инвентаризации программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="9933c-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="9933c-128">Агрегатор определяет количество вхождений каждого хэш-тега.</span><span class="sxs-lookup"><span data-stu-id="9933c-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="9933c-129">Эти данные сохраняются в памяти.</span><span class="sxs-lookup"><span data-stu-id="9933c-129">This data is persisted in memory.</span></span> <span data-ttu-id="9933c-130">Наконец создается новый поток, содержащий тег хэш hello и число hello.</span><span class="sxs-lookup"><span data-stu-id="9933c-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="9933c-131">Hello **FirstN** сборка является примененных tooreturn только hello 10 верхних значений, на основе поля число hello.</span><span class="sxs-lookup"><span data-stu-id="9933c-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="9933c-132">Дополнительные сведения о работе с Trident см. в разделе hello [Обзор Trident API](http://storm.apache.org/releases/current/Trident-API-Overview.html) документа.</span><span class="sxs-lookup"><span data-stu-id="9933c-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="9933c-133">Hello spout</span><span class="sxs-lookup"><span data-stu-id="9933c-133">hello spout</span></span>

<span data-ttu-id="9933c-134">Hello spout **TwitterSpout**, использует [Twitter4j](http://twitter4j.org/en/) твиты tooretrieve из Twitter.</span><span class="sxs-lookup"><span data-stu-id="9933c-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="9933c-135">Создать фильтр для слова hello __нравятся__, **Музыка**, и **кофе**.</span><span class="sxs-lookup"><span data-stu-id="9933c-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="9933c-136">Входящие твиты (состояние), соответствующие фильтру hello хранятся в связанной блокирующей очереди.</span><span class="sxs-lookup"><span data-stu-id="9933c-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="9933c-137">Наконец элементы извлекаются очереди hello и создаваться toohello топологии.</span><span class="sxs-lookup"><span data-stu-id="9933c-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="9933c-138">Hello HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="9933c-138">hello HashtagExtractor</span></span>

<span data-ttu-id="9933c-139">теги хэш tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) является используется tooretrieve все теги хэш, содержащихся в твит hello.</span><span class="sxs-lookup"><span data-stu-id="9933c-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="9933c-140">Эти затем последовательно порожденную toohello потока.</span><span class="sxs-lookup"><span data-stu-id="9933c-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="9933c-141">Настройка Twitter</span><span class="sxs-lookup"><span data-stu-id="9933c-141">Configure Twitter</span></span>

<span data-ttu-id="9933c-142">Используйте следующие шаги tooregister нового приложения Twitter hello и получить tooread необходимые сведения о токене hello потребителя и доступа Twitter:</span><span class="sxs-lookup"><span data-stu-id="9933c-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="9933c-143">Go слишком[Twitter приложения](https://apps.twitter.com) и нажмите кнопку hello **создать новое приложение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9933c-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="9933c-144">После заполнения формы hello, оставьте hello **URL-адрес обратного вызова** пустым.</span><span class="sxs-lookup"><span data-stu-id="9933c-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="9933c-145">При создании приложения hello щелкните hello **ключей и маркеры доступа** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9933c-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="9933c-146">Копировать hello **ключ потребителя** и **секрет пользователя** сведения.</span><span class="sxs-lookup"><span data-stu-id="9933c-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="9933c-147">Hello нижней части страницы приветствия, выберите **создать Мой маркер доступа** Если токены не существует.</span><span class="sxs-lookup"><span data-stu-id="9933c-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="9933c-148">После создания токенов hello, hello копирования **токена доступа** и **секрет маркера доступа** сведения.</span><span class="sxs-lookup"><span data-stu-id="9933c-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="9933c-149">В hello **TwitterSpoutTopology** проекта вы ранее клонированной, откройте hello **resources/twitter4j.properties** файл, добавьте hello сведения, собранные в предыдущих шагах hello и затем сохраните файл hello .</span><span class="sxs-lookup"><span data-stu-id="9933c-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="9933c-150">Выполнить сборку топологии hello</span><span class="sxs-lookup"><span data-stu-id="9933c-150">Build hello topology</span></span>

<span data-ttu-id="9933c-151">Используйте следующий проект hello toobuild кода hello.</span><span class="sxs-lookup"><span data-stu-id="9933c-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="9933c-152">Топология теста hello</span><span class="sxs-lookup"><span data-stu-id="9933c-152">Test hello topology</span></span>

<span data-ttu-id="9933c-153">Используйте hello следующая команда tootest локально hello топологии:</span><span class="sxs-lookup"><span data-stu-id="9933c-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="9933c-154">После запуска топологии hello, вы увидите отладочной информации, содержащий хэш hello теги и подсчитывает порожденную по топологии hello.</span><span class="sxs-lookup"><span data-stu-id="9933c-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="9933c-155">Hello вывод должен выглядеть примерно toohello после текста:</span><span class="sxs-lookup"><span data-stu-id="9933c-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="9933c-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9933c-156">Next steps</span></span>

<span data-ttu-id="9933c-157">Можно тестировать локально топологии hello обнаружение как toodeploy hello топологии: [развертывание и управление ими Apache Storm топологии на HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9933c-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="9933c-158">Кроме того, могут быть интересны следующие вопросы Storm hello:</span><span class="sxs-lookup"><span data-stu-id="9933c-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="9933c-159">Разработка топологий на Java для Storm в HDInsight с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="9933c-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="9933c-160">Разработка топологий для Storm в HDInsight на C# с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9933c-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="9933c-161">Дополнительные примеры Storm для HDinsight:</span><span class="sxs-lookup"><span data-stu-id="9933c-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="9933c-162">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="9933c-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

