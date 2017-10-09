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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Определение популярных тем в Twitter с помощью Apache Storm в HDInsight

Узнайте, как toocreate Trident toouse топологии Storm, определяет сведения о тенденциях разделы (хэш теги) в Twitter.

Trident — это высокоуровневая абстракция, которая предоставляет такие средства, как соединения, функции, фильтры, агрегирование и группирование. Кроме того, Trident добавляет примитивы для выполнения добавочной обработки с отслеживанием состояния. пример Hello, используемые в этом документе является топологии Trident пользовательских spout и функции. В ней также используется несколько встроенных функций Trident.

## <a name="requirements"></a>Требования

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java и hello JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Учетная запись разработчика Twitter

## <a name="download-hello-project"></a>Загрузите проект hello

Используйте следующие hello кода проекта hello tooclone локально.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Основные сведения о топологии hello

Hello следующей схеме показано из потоки данных посредством этой топологии:

![Топология](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Эта диаграмма представляет упрощенное представление топологии hello. Несколько экземпляров компонентов hello распределены между узлами hello в кластере hello.


Hello Trident код, который реализует топологии hello выглядит следующим образом:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Этот код выполняет следующие действия hello:

1. Создает поток из hello spout. Hello spout извлекает твиты из Twitter и фильтрует их определенные ключевые слова (любви, музыке и кофе в этом примере).

2. HashtagExtractor пользовательской функции, — используется tooextract хэш тегов из каждой твит. теги Hello хэш — порожденную toohello потока.

3. Hello потока сгруппированы по тегу хэш и передается tooan инвентаризации программного обеспечения. Агрегатор определяет количество вхождений каждого хэш-тега. Эти данные сохраняются в памяти. Наконец создается новый поток, содержащий тег хэш hello и число hello.

4. Hello **FirstN** сборка является примененных tooreturn только hello 10 верхних значений, на основе поля число hello.

> [!NOTE]
> Дополнительные сведения о работе с Trident см. в разделе hello [Обзор Trident API](http://storm.apache.org/releases/current/Trident-API-Overview.html) документа.

### <a name="hello-spout"></a>Hello spout

Hello spout **TwitterSpout**, использует [Twitter4j](http://twitter4j.org/en/) твиты tooretrieve из Twitter. Создать фильтр для слова hello __нравятся__, **Музыка**, и **кофе**. Входящие твиты (состояние), соответствующие фильтру hello хранятся в связанной блокирующей очереди. Наконец элементы извлекаются очереди hello и создаваться toohello топологии.

### <a name="hello-hashtagextractor"></a>Hello HashtagExtractor

теги хэш tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) является используется tooretrieve все теги хэш, содержащихся в твит hello. Эти затем последовательно порожденную toohello потока.

## <a name="configure-twitter"></a>Настройка Twitter

Используйте следующие шаги tooregister нового приложения Twitter hello и получить tooread необходимые сведения о токене hello потребителя и доступа Twitter:

1. Go слишком[Twitter приложения](https://apps.twitter.com) и нажмите кнопку hello **создать новое приложение** кнопки. После заполнения формы hello, оставьте hello **URL-адрес обратного вызова** пустым.

2. При создании приложения hello щелкните hello **ключей и маркеры доступа** вкладки.

3. Копировать hello **ключ потребителя** и **секрет пользователя** сведения.

4. Hello нижней части страницы приветствия, выберите **создать Мой маркер доступа** Если токены не существует. После создания токенов hello, hello копирования **токена доступа** и **секрет маркера доступа** сведения.

5. В hello **TwitterSpoutTopology** проекта вы ранее клонированной, откройте hello **resources/twitter4j.properties** файл, добавьте hello сведения, собранные в предыдущих шагах hello и затем сохраните файл hello .

## <a name="build-hello-topology"></a>Выполнить сборку топологии hello

Используйте следующий проект hello toobuild кода hello.

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>Топология теста hello

Используйте hello следующая команда tootest локально hello топологии:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

После запуска топологии hello, вы увидите отладочной информации, содержащий хэш hello теги и подсчитывает порожденную по топологии hello. Hello вывод должен выглядеть примерно toohello после текста:

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>Дальнейшие действия

Можно тестировать локально топологии hello обнаружение как toodeploy hello топологии: [развертывание и управление ими Apache Storm топологии на HDInsight](hdinsight-storm-deploy-monitor-topology.md).

Кроме того, могут быть интересны следующие вопросы Storm hello:

* [Разработка топологий на Java для Storm в HDInsight с помощью Maven](hdinsight-storm-develop-java-topology.md)
* [Разработка топологий для Storm в HDInsight на C# с помощью Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Дополнительные примеры Storm для HDinsight:

* [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md)

