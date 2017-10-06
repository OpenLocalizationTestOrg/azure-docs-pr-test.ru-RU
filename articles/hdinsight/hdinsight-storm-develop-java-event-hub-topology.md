---
title: "события aaaProcess из концентраторов событий с Storm на HDInsight с помощью Java | Документы Microsoft"
description: "Дополнительные сведения, создание концентраторов событий данных из топологии Java Storm tooprocess Maven."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="dc5ec-103">Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="dc5ec-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="dc5ec-104">Узнайте, как toouse концентраторов событий Azure с Storm на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="dc5ec-105">В этом примере использует компоненты на основе Java tooread и запись данных в концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="dc5ec-106">Концентраторы событий Azure позволяет tooprocess значительные объемы данных из веб-сайтов, приложений и устройств.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="dc5ec-107">Hello spout концентратора событий позволяет легко toouse Apache Storm на HDInsight tooanalyze эти данные в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="dc5ec-108">Можно также написать tooEvent данных концентраторов из Storm с помощью приветствия винта концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc5ec-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc5ec-109">Prerequisites</span></span>

* <span data-ttu-id="dc5ec-110">Кластер Apache Storm в кластере HDInsight версии 3.6.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="dc5ec-111">Дополнительные сведения см. в статье [Руководство по Apache Storm в HDInsight: начало работы с анализом больших объемов данных в HDInsight с помощью примеров Storm Starter](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="dc5ec-112">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dc5ec-113">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="dc5ec-114">[Концентратор событий Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="dc5ec-115">Пакет [Oracle Java Developer Kit (JDK) версии 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) или аналогичный пакет, например [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="dc5ec-116">[Maven](https://maven.apache.org/download.cgi) — это система сборки проектов Java.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="dc5ec-117">Текстовый редактор либо интегрированная среда разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc5ec-118">В редакторе или интегрированной среде разработки могут быть предусмотрены специальные функциональные возможности для работы с Maven, не описанные в настоящем документе.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="dc5ec-119">Сведения о возможностях hello среды редактирования документации hello hello продукта, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="dc5ec-120">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-120">An SSH client.</span></span> <span data-ttu-id="dc5ec-121">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="dc5ec-122">Hello `ssh` и `scp` команд.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="dc5ec-123">Это кластер HDInsight toohello toocopy используемых файлов.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="dc5ec-124">В Windows вы можете получить их через Bash в Windows 10.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="dc5ec-125">Основные сведения о примере hello</span><span class="sxs-lookup"><span data-stu-id="dc5ec-125">Understanding hello example</span></span>

<span data-ttu-id="dc5ec-126">Hello [hdinsight java-storm eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) пример содержит две топологии:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="dc5ec-127">Hello `resources/writer.yaml` топологии записывает случайные данные tooan концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="dc5ec-128">Hello данные формируются hello `DeviceSpout` компонента, и идентификатор случайных устройства и устройства.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="dc5ec-129">Определенное устройство получает команду на передачу идентификатора строки и числового значения.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="dc5ec-130">Три `resources/reader.yaml` топологии считывает данные из концентратора событий (hello данные, записанные в EventHubWriter,) выполняет синтаксический анализ данных JSON hello, а затем регистрирует hello `deviceId` и `deviceValue` данных.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="dc5ec-131">Hello данные форматируются как документ JSON перед его записи tooEvent концентратора и при считывании модулем чтения hello он анализируется из JSON и в кортежи.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="dc5ec-132">Hello JSON имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="dc5ec-133">Конфигурация проекта</span><span class="sxs-lookup"><span data-stu-id="dc5ec-133">Project configuration</span></span>

<span data-ttu-id="dc5ec-134">Hello `POM.xml` файл содержит сведения о конфигурации для этого проекта Maven.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="dc5ec-135">Ниже приведены интересные участки Hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="dc5ec-136">Компоненты концентратора событий</span><span class="sxs-lookup"><span data-stu-id="dc5ec-136">Event Hub components</span></span>

<span data-ttu-id="dc5ec-137">Hello компонент, который считывает и записывает концентраторов событий tooAzure расположен в hello [HDInsight репозитория](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="dc5ec-138">Здравствуйте, следующие разделы в hello `POM.xml` компонентами hello загрузки файлов из этого репозитория</span><span class="sxs-lookup"><span data-stu-id="dc5ec-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="dc5ec-139">Hello EventHubs Storm Spout зависимостей</span><span class="sxs-lookup"><span data-stu-id="dc5ec-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="dc5ec-140">Этот XML-документ определяет зависимости для hello eventhubs пакет, который содержит spout на чтение из концентраторов событий и молнии для записи tooit.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="dc5ec-141">Этот XML-документ настраивает hello toogenerate выходные файлы проекта Java 8, который используется с HDInsight 3.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="dc5ec-142">Здравствуйте, maven оттенок подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-142">hello maven-shade-plugin</span></span>

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

<span data-ttu-id="dc5ec-143">Этот XML-документ настраивает hello решения toopackage hello вывода в полный jar.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="dc5ec-144">Hello JAR-файл содержит код проекта hello и необходимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="dc5ec-145">Он также используется для:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-145">It is also used to:</span></span>

* <span data-ttu-id="dc5ec-146">Переименование файлов лицензии для hello зависимости.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="dc5ec-147">Исключения групп безопасности и подписей.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="dc5ec-148">Убедитесь, что несколько реализаций hello же интерфейс объединяются в одну запись.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="dc5ec-149">Эти параметры конфигурации предотвращают ошибки во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="dc5ec-150">Определения топологии</span><span class="sxs-lookup"><span data-stu-id="dc5ec-150">Topology definitions</span></span>

<span data-ttu-id="dc5ec-151">В этом примере используется hello [определен](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="dc5ec-152">Эта платформа использует YAML toodefine hello топологии.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="dc5ec-153">Hello основное преимущество состоит в том, что вы не являетесь жесткого кодирования топологии hello в коде Java.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="dc5ec-154">Поскольку определение hello YAML, его можно изменить перед отправкой топологии hello без необходимости toorecompile все.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="dc5ec-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

<span data-ttu-id="dc5ec-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="dc5ec-157">Расскажите о концентратора событий hello топологии</span><span class="sxs-lookup"><span data-stu-id="dc5ec-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="dc5ec-158">Во время выполнения hello `dev.properties` файл является используется toopass hello концентратора событий конфигурации toohello топологии.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="dc5ec-159">Hello следующий пример — содержимое по умолчанию hello hello файла:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="dc5ec-160">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="dc5ec-160">Configure environment variables</span></span>

<span data-ttu-id="dc5ec-161">Hello следующие переменные среды можно задать при установке Java и hello JDK на рабочей станции разработки.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="dc5ec-162">Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="dc5ec-163">**JAVA_HOME** -должен указывать toohello каталог, где установлен hello среда выполнения Java (JRE).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="dc5ec-164">Например, при распределении Unix или Linux, возможно только значение, схожее слишком`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="dc5ec-165">В Windows он будет иметь значение, схожее слишком`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="dc5ec-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="dc5ec-166">**ПУТЬ** -должна содержать hello, следующие пути:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="dc5ec-167">**JAVA_HOME** (или эквивалентный путь hello)</span><span class="sxs-lookup"><span data-stu-id="dc5ec-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="dc5ec-168">**JAVA_HOME\bin** (или эквивалентный путь hello)</span><span class="sxs-lookup"><span data-stu-id="dc5ec-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="dc5ec-169">Hello каталог для установки Maven</span><span class="sxs-lookup"><span data-stu-id="dc5ec-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="dc5ec-170">Настройка концентраторов Event Hub</span><span class="sxs-lookup"><span data-stu-id="dc5ec-170">Configure Event Hub</span></span>

<span data-ttu-id="dc5ec-171">Концентраторы событий — hello источника данных для этого примера.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="dc5ec-172">Используйте следующие шаги toocreate концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="dc5ec-173">Из hello [классический портал Azure](https://manage.windowsazure.com)выберите **NEW** > **Service Bus** > **концентратора событий**  >  **Настраиваемое создание**.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="dc5ec-174">На hello **добавить новый концентратор событий** экране, введите **имя концентратора событий**.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="dc5ec-175">Выберите hello **область** toocreate hello концентратора и затем создать пространство имен или выберите существующий.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="dc5ec-176">Наконец, нажмите кнопку hello **стрелка** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![страница мастера 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="dc5ec-178">Выберите hello же **расположение** как ваш Storm задержка tooreduce сервера HDInsight и цены.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="dc5ec-179">На hello **Настройка концентратора событий** экране, введите hello **секции количество** и **хранение сообщений** значения.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="dc5ec-180">В этом примере числу разделов присвойте значение 10, а хранению сообщений — 1.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="dc5ec-181">Обратите внимание hello число секций, поскольку это значение требуется более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-181">Note hello partition count because you need this value later.</span></span>

    ![страница мастера 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="dc5ec-183">После концентратора событий hello hello создан, выберите пространство имен, выберите **концентраторов событий**, а затем выберите концентратор событий hello, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="dc5ec-184">Выберите **Настройка**, затем создайте два новых политик доступа с помощью hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="dc5ec-185">Имя</span><span class="sxs-lookup"><span data-stu-id="dc5ec-185">Name</span></span></th><th><span data-ttu-id="dc5ec-186">Разрешения</span><span class="sxs-lookup"><span data-stu-id="dc5ec-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="dc5ec-187">Модуль записи</span><span class="sxs-lookup"><span data-stu-id="dc5ec-187">Writer</span></span></td><td><span data-ttu-id="dc5ec-188">Отправка</span><span class="sxs-lookup"><span data-stu-id="dc5ec-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="dc5ec-189">читатель.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-189">Reader</span></span></td><td><span data-ttu-id="dc5ec-190">Прослушивание</span><span class="sxs-lookup"><span data-stu-id="dc5ec-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="dc5ec-191">После создания разрешения hello выберите hello **Сохранить** значок hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="dc5ec-192">Эти политики общего доступа используется tooread и записать tooEvent концентратора.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![политики](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="dc5ec-194">После сохранения политики hello использовать hello **генератор ключей общего доступа** hello нижней части страницы приветствия tooretrieve ключ hello hello **записи** и **чтения** политики.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="dc5ec-195">Сохраните эти значения.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="dc5ec-196">Загрузка и построение проекта hello</span><span class="sxs-lookup"><span data-stu-id="dc5ec-196">Download and build hello project</span></span>

1. <span data-ttu-id="dc5ec-197">Загрузите проект hello из GitHub: [hdinsight java-storm eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="dc5ec-198">Можно загрузить пакет hello в виде ZIP-архив, или использовать [git](https://git-scm.com/) tooclone проекта hello локально.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="dc5ec-199">Изменение hello `dev.properties` файл с конфигурацией hello для концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="dc5ec-200">Используйте следующие toobuild и пакет проекта hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="dc5ec-201">Эта команда загружает необходимые зависимости построения, и затем пакеты hello проекта.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="dc5ec-202">Hello выходные данные, хранящиеся в hello **/target-** каталог как **EventHubExample 1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="dc5ec-203">Локальное тестирование</span><span class="sxs-lookup"><span data-stu-id="dc5ec-203">Test locally</span></span>

<span data-ttu-id="dc5ec-204">Поскольку эти топологии только чтение и запись tooEvent концентраторы, можно проверить их локально в том случае, если у вас есть [среды разработки Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="dc5ec-205">Используйте следующие шаги toorun локально в среде разработки hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="dc5ec-206">Запустите средство записи hello:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="dc5ec-207">Запустите средство чтения hello:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="dc5ec-208">`--local`: Топология выполнения hello в локальном режиме (без распределенных).</span><span class="sxs-lookup"><span data-stu-id="dc5ec-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="dc5ec-209">`-R /writer.yaml`: Загрузки определения топологии hello из hello `resources` упакованных в банке hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="dc5ec-210">Если топология hello представляет собой файл hello локальной файловой системе, укажите путь tooit hello как последний параметр hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="dc5ec-211">`--filter dev.properties`: Используется содержимое hello `dev.properties` toofill в значениях hello в определениях топологии hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="dc5ec-212">Например, `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="dc5ec-213">Выходные данные выглядят toohello журнал консоли при выполнении локально.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="dc5ec-214">Используйте __Ctrl + C__ toostop hello топологии.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="dc5ec-215">Hello топологии развертывания</span><span class="sxs-lookup"><span data-stu-id="dc5ec-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="dc5ec-216">Использование SCP toocopy hello jar пакета tooyour кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="dc5ec-217">Замените имя пользователя hello пользователя SSH для кластера.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="dc5ec-218">Замените ИМЯ_КЛАСТЕРА hello имя кластера HDInsight:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="dc5ec-219">Если используется пароль для учетной записи SSH, не запрошенные tooenter hello пароль.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="dc5ec-220">При использовании ключа SSH с учетной записью hello, может потребоваться toouse hello `-i` параметр toospecify hello путь toohello файл ключа.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="dc5ec-221">Например, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="dc5ec-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="dc5ec-222">Эта команда копирует hello файл toohello домашний каталог пользователя SSH в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="dc5ec-223">После завершения передачи файла hello используйте кластер HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="dc5ec-224">Замените **USERNAME** hello имя входа SSH.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="dc5ec-225">Замените **CLUSTERNAME** именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="dc5ec-226">Если используется пароль для учетной записи SSH, не запрошенные tooenter hello пароль.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="dc5ec-227">При использовании ключа SSH с учетной записью hello, может потребоваться toouse hello `-i` параметр toospecify hello путь toohello файл ключа.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="dc5ec-228">Hello следующем примере загружаются hello закрытый ключ из `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="dc5ec-229">Используйте следующие команды toostart hello топологии hello:</span><span class="sxs-lookup"><span data-stu-id="dc5ec-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="dc5ec-230">`--remote`: Отправляет toohello топологии hello Nimbus службу, которая запускает его на hello рабочих узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="dc5ec-231">tooview hello в журнал данных, перейдите в раздел toohttps://CLUSTERNAME.azurehdinsight.net/stormui, где __CLUSTERNAME__ — hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="dc5ec-232">Выберите топологии hello и детализацию toohello компонентов.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="dc5ec-233">Выберите hello __порт__ входа для экземпляра tooview компонента данных журнала.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="dc5ec-234">Используйте следующие команды toostop hello топологии hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ec-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="dc5ec-235">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="dc5ec-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="dc5ec-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc5ec-236">Next steps</span></span>

* [<span data-ttu-id="dc5ec-237">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc5ec-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
