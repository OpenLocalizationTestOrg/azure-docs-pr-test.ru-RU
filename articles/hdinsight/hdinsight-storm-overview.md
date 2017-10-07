---
title: "aaaWhat — Apache Storm - Azure HDInsight | Документы Microsoft"
description: "Apache Storm позволяет tooprocess потоки данных в режиме реального времени. Azure HDInsight позволяет tooeasily создавать кластеры Storm на hello облако Azure. Вместе с Visual Studio можно создавать Storm решения с помощью C#, а затем развернуть tooyour кластеров HDInsight Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "варианты использования apache storm, кластер storm, сведения об apache storm"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>Основные сведения об Apache Storm в Azure HDInsight

[Apache Storm](http://storm.apache.org/) — это распределенная отказоустойчивая вычислительная система с открытым исходным кодом. Storm tooprocess потоки данных в реальном времени можно использовать с Hadoop. Storm также обеспечивают гарантированную обработку данных, с возможностью tooreplay hello данных, который не был успешно обработан hello первый раз.

Storm на HDInsight предоставляет hello следующие ключевые преимущества:

* Решение выполняется как управляемая служба с доступностью в течение 99,9 % времени.

* Простая настройка с помощью скриптов во время или после создания кластера Storm. Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

* Использование различных языков. Компоненты Storm можно написать на языке hello по своему усмотрению, например Java, C# и Python.

    * Visual Studio можно интегрировать с HDInsight для hello разработки, управления и наблюдения за топологии на C#. Дополнительные сведения см. в разделе [разработки C# Storm топологии с hello средства HDInsight для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Поддерживает интерфейс Trident Java hello. Вы можете создавать топологии Storm, поддерживающие обработку сообщений в рамках подхода "только один раз", сохраняемость "транзакционных" хранилищ данных, а также набор распространенных операций Stream Analytics.

*  Простое масштабирование кластеров Storm. Можно добавить или удалить рабочих узлов не топологиям Storm toorunning влияния.

* Интегрируется с hello следующих служб Azure.

    * Концентраторы событий Azure

    * Виртуальная сеть Azure

    * База данных SQL Azure

    * Хранилище Azure

    * Azure Cosmos DB

* Безопасно объединяет возможности hello несколько кластеров HDInsight с помощью виртуальной сети. Вы можете создавать конвейеры аналитики, использующие кластеры Storm, Kafka, Spark, HBase или Hadoop.

Список компаний, использующих Apache Storm в качестве решения для анализа данных в реальном времени, см. на [этой странице](https://storm.apache.org/documentation/Powered-By.html).

tooget работы с использованием урагана, в разделе [Приступая к работе с Storm на HDInsight][gettingstarted].

## <a name="how-does-storm-work"></a>Как работает Storm

Storm выполняется топологии вместо hello задания MapReduce, которые могут быть знакомы. Топологии Storm состоят из нескольких компонентов, которые расположены в виде направленного ациклического графа (DAG). Потоки данных между компонентами hello графике hello. Каждый компонент использует один или несколько потоков данных и может генерировать дополнительные потоки. Hello, следующая схема иллюстрирует порядок обмена данными между компонентами в топологии основные статистика:

![Пример расположения компонентов в топологии Storm](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Компоненты spout переносят данные в топологию. Они выдают один или несколько потоков в топологию hello.

* Компоненты bolt используют потоки, генерируемые элементами spout или другими элементами bolt. Винты при необходимости может выдавать потоки в топологию hello. Винты также отвечает за запись tooexternal службы данных или хранилище, например HDFS, Kafka или HBase.

## <a name="ease-of-creation"></a>Простота создания

Новый кластер Storm в HDInsight можно подготовить за считаные минуты. Сведения о создании кластера Storm см. в статье [Начало работы с примерами Storm Starter для аналитики больших данных в HDInsight под управлением Linux](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Простота использования

* __Secure Shell (SSH) подключения__: hello головного узла кластера Storm для доступа к Интернету hello с помощью SSH. С помощью SSH вы можете выполнять команды непосредственно в кластере.

  Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Веб-подключения__: HDInsight все кластеры обеспечивают hello Ambari web пользовательского интерфейса. Можно легко отслеживать, Настройка и управление службами на кластере с помощью Ambari web hello пользовательского интерфейса. Storm кластеры также предоставляют hello Storm пользовательского интерфейса. Позволяет управлять и управлять выполняющегося Storm топологии из браузера с помощью hello Storm пользовательского интерфейса.

  Дополнительные сведения см. в разделе hello [управления HDInsight с помощью hello Ambari веб-интерфейса](hdinsight-hadoop-manage-ambari.md) и [монитора и управлять ими с помощью пользовательского интерфейса Storm hello](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) документов.

* __Azure PowerShell и Azure CLI__: PowerShell и предоставляют служебные программы командной строки, которые можно использовать из toowork системы вашего клиента с HDInsight и другим службам Azure CLI.

* __Интеграция с Visual Studio__: средства Озера данных Azure для Visual Studio включает шаблоны проектов для создания топологии Storm C# с помощью платформы SCP.Net hello. Средства Озера данных также предоставляют toodeploy средства мониторинга и управления решениями с Storm на HDInsight.

  Дополнительные сведения см. в разделе [разработки C# Storm топологии с hello средства HDInsight для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Интеграция с другими службами Azure

* __Azure Data Lake Store.__ Примеры использования Data Lake Store с помощью кластера Storm см. в статье [Использование Azure Data Lake Store с помощью Apache Storm в HDInsight (Java)](hdinsight-storm-write-data-lake-store.md).

* __Концентраторы событий__: пример использования концентраторов событий с кластером Storm, в разделе hello следующие документы:

    * [Разработка топологии подсчета слов на основе Java для Storm в HDInsight с помощью Maven](hdinsight-storm-develop-java-topology.md)

    * [Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md)

* __База данных SQL__, __Cosmos DB__, __концентраторов событий__, и __HBase__: примеры шаблона включаются в hello Озера Data Tools для Visual Studio. Дополнительные сведения см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="reliability"></a>Надежность

Apache Storm гарантирует, что каждое входящее сообщение всегда полностью обрабатывается, даже в том случае, если анализ данных hello распределяется по сотен узлов.

узел Nimbus Hello предоставляет toohello аналогичные функциональные возможности Hadoop JobTracker и присваивает задачам tooother узлов кластера с помощью Zookeeper. Zookeeper узлы содержат координации для кластера и упрощения взаимодействия между Nimbus и hello процесса начальника на hello рабочих узлов. Если один обработки узел выйдет из строя, уведомления hello Nimbus узла и она назначает задачу hello и связанные данные tooanother узла.

Конфигурация по умолчанию Hello кластеры Apache Storm является только один узел Nimbus toohave. но кластер Storm в HDInsight имеет два. При ошибке основного узла hello, кластер Storm hello переключается toohello дополнительного узла, во время восстановления основного узла hello. Hello следующей схеме показана конфигурация потока задачи hello для Storm на HDInsight.

![Схема с контролерами и компонентами Nimbus и Zookeeper](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Масштаб

Вы можете выполнить динамическое масштабирование кластеров HDInsight, добавив или удалив рабочие узлы, во время обработки данных.

> [!IMPORTANT]
> tootake преимуществами новых узлов добавить с помощью масштабирования, необходимо toorebalance Storm топологии запущены перед запуском был увеличен размер кластера hello.

## <a name="support"></a>Поддержка

Для кластеров Storm в HDInsight действует полная поддержка корпоративного уровня. Кроме того, для кластеров Storm в HDInsight заявлена гарантированная доступность в течение 99,9 % времени. Это означает, что мы гарантируем, что кластер Storm имеет возможности внешнего подключения не менее 99,9% времени hello.

Дополнительные сведения см. на странице [службы поддержки Azure](https://azure.microsoft.com/support/options/).

## <a name="apache-storm-use-cases"></a>Варианты использования Apache Storm

Hello ниже приведены некоторые распространенные сценарии, для которых можно использовать Storm на HDInsight.

* Интернет вещей.
* Обнаружение мошенничества.
* Социальная аналитика.
* Извлечение, преобразование и загрузка.
* Мониторинг сетей.
* Поиск
* Службы мобильного взаимодействия

Сведения о реальных сценариев см. в разделе hello [использования компаний Storm](https://storm.apache.org/documentation/Powered-By.html) документа.

## <a name="development"></a>Разработка

Средства Data Lake для Visual Studio позволяют разработчикам .NET проектировать и реализовывать топологии на языке C#. Вы также можете создавать гибридные топологии, в которых используются компоненты Java и C#.

Дополнительные сведения см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Также можно разрабатывать решения Java с помощью hello IDE по своему усмотрению. Дополнительные сведения см. в статье [Разработка топологии подсчета слов на основе Java для Storm в HDInsight с помощью Maven](hdinsight-storm-develop-java-topology.md).

Python может быть также используется toodevelop Storm компонентов. Дополнительные сведения см. в статье [Разработка топологий Apache Storm с помощью Python в HDInsight](hdinsight-storm-develop-python-topology.md).

## <a name="common-development-patterns"></a>Общие шаблоны разработки

### <a name="guaranteed-message-processing"></a>Гарантированная обработка сообщений

Apache Storm может обеспечить различные уровни гарантированной обработки сообщений. Например, простое приложение Storm гарантирует как минимум одну обработку, в то время как Trident может гарантировать ровно одну обработку.

Дополнительные сведения см. в статье о [гарантированной обработке данных](https://storm.apache.org/about/guarantees-data-processing.html) на сайте apache.org.

### <a name="ibasicbolt"></a>IBasicBolt

Здравствуйте шаблон считывания ввода кортежа, создающие ноль или более кортежей и выполнить метод acking hello входной кортеж немедленно в конце hello hello являются общими. Storm предоставляет hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) интерфейс tooautomate этот шаблон.

### <a name="joins"></a>Соединения

Объединение потоков данных отличается в разных приложениях. Например, вы можете объединять все кортежи с нескольких потоков в один новый поток или объединять только пакеты кортежей для отдельного окна. В любом случае объединение можно выполнить с помощью [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Группирование полей — это способ определения того, как кортежи, перенаправленное toobolts.

В следующий пример Java hello fieldsGrouping не используется tooroute кортежей, которые получаются из молнии MyJoiner toohello компонентов «1», «2» и «3»:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Пакеты

Apache Storm предоставляет внутренний временной механизм (временный кортеж). Вы можете задать частоту использования временного кортежа в топологии.

Пример использования временного кортежа из компонента на C# см. здесь: [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

### <a name="caches"></a>Кэши

Для ускорения обработки часто используется кэширование в памяти, при котором в памяти сохраняются часто используемые ресурсы. Так как топология распределяется между несколькими узлами и несколькими процессами в пределах одного узла, вы можете использовать [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Используйте `fieldsGrouping` tooensure кортежей, содержащих hello полей, которые используются для поиска в кэше всегда являются перенаправленное toohello же процесс. Эта функция группирования избавит от дублирования записей кэша в процессах.

### <a name="stream-top-n"></a>Передача значения "Первые N"

Если топологии зависит от того, вычисление значения top N, вычислите значение top N hello в параллельном режиме. Затем слияния hello выход из этих вычислений в глобальной переменной. Эта операция может быть выполнена с помощью [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute полем для параллельной обработки. Затем можно направлять tooa молнии, глобально определяющее значение top N hello.

Пример вычисления значения top N разделе hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) примере.

## <a name="logging"></a>Ведение журналов

Storm использует Apache Log4j toolog сведения. По умолчанию записывается большой объем данных, и может быть трудно toosort через hello сведения. Файл конфигурации ведения журнала можно включить как часть вашего Storm топологии toocontrol режим ведения журнала.

Для пример топологии, в котором показано, как tooconfigure ведения журнала, в разделе [WordCount на языке Java](hdinsight-storm-develop-java-topology.md) пример Storm на HDInsight.

## <a name="next-steps"></a>Дальнейшие действия

Ниже приведены статьи, в которых можно найти дополнительные сведения о решениях для анализа данных в реальном времени с помощью Storm в HDInsight.

* [Начало работы с примерами Storm Starter для аналитики больших данных в HDInsight под управлением Linux][gettingstarted]
* [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
