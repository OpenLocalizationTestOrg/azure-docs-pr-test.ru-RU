---
title: "Обработка событий из концентраторов событий с помощью Storm в HDInsight с использованием Java | Документация Майкрософт"
description: "Узнайте, как обрабатывать данные концентраторов событий, используя топологии Java Storm, созданные с помощью Maven."
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
ms.openlocfilehash: 2e8ebbdab2be7bed224a67facec798820615bb22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="d6bd4-103">Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="d6bd4-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="d6bd4-104">Узнайте, как использовать концентраторы событий Azure со Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="d6bd4-105">В этом примере используются компоненты на основе Java для чтения и записи данных в концентраторах событий Azure.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="d6bd4-106">Служба концентраторов событий Azure позволяет обрабатывать значительные объемы данных из веб-сайтов, приложений и устройств.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="d6bd4-107">Элемент spout концентратора событий упрощает использование Apache Storm в HDInsight для анализа этих данных в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="d6bd4-108">Вы также можете записывать данные в службу концентраторов событий из Storm с помощью сита службы концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6bd4-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d6bd4-109">Prerequisites</span></span>

* <span data-ttu-id="d6bd4-110">Кластер Apache Storm в кластере HDInsight версии 3.6.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="d6bd4-111">Дополнительные сведения см. в статье [Руководство по Apache Storm в HDInsight: начало работы с анализом больших объемов данных в HDInsight с помощью примеров Storm Starter](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d6bd4-112">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d6bd4-113">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d6bd4-114">[Концентратор событий Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="d6bd4-115">Пакет [Oracle Java Developer Kit (JDK) версии 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) или аналогичный пакет, например [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="d6bd4-116">[Maven](https://maven.apache.org/download.cgi) — это система сборки проектов Java.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="d6bd4-117">Текстовый редактор либо интегрированная среда разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d6bd4-118">В редакторе или интегрированной среде разработки могут быть предусмотрены специальные функциональные возможности для работы с Maven, не описанные в настоящем документе.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="d6bd4-119">Информацию о возможностях среды редактирования см. в документации продукта, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span></span>

    * <span data-ttu-id="d6bd4-120">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-120">An SSH client.</span></span> <span data-ttu-id="d6bd4-121">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="d6bd4-122">Команды `ssh` и `scp`.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-122">The `ssh` and `scp` commands.</span></span> <span data-ttu-id="d6bd4-123">Они используются для копирования файлов в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-123">These are used to copy files to the HDInsight cluster.</span></span> <span data-ttu-id="d6bd4-124">В Windows вы можете получить их через Bash в Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-the-example"></a><span data-ttu-id="d6bd4-125">Общие сведения о примере</span><span class="sxs-lookup"><span data-stu-id="d6bd4-125">Understanding the example</span></span>

<span data-ttu-id="d6bd4-126">Пример [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) включает две топологии:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="d6bd4-127">Топология `resources/writer.yaml` записывает случайные данные в концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-127">The `resources/writer.yaml` topology writes random data to an Azure Event Hub.</span></span> <span data-ttu-id="d6bd4-128">Данные генерируются с помощью компонента `DeviceSpout` и представляют собой случайные идентификатор устройства и значение устройства.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-128">The data is generated by the `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="d6bd4-129">Определенное устройство получает команду на передачу идентификатора строки и числового значения.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="d6bd4-130">Топология `resources/reader.yaml` считывает данные из концентратора событий (данные, записанные EventHubWriter), анализирует данные JSON, а затем регистрирует данные `deviceId` и `deviceValue`.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-130">Thee `resources/reader.yaml` topology reads data from Event Hub (the data written by EventHubWriter,) parses the JSON data, and then logs the `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="d6bd4-131">Перед записью в концентратор событий данные преобразуются в формат JSON, а при чтении содержимое файла JSON анализируется и преобразуется в кортежи.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="d6bd4-132">Используется следующий формат JSON:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-132">The JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="d6bd4-133">Конфигурация проекта</span><span class="sxs-lookup"><span data-stu-id="d6bd4-133">Project configuration</span></span>

<span data-ttu-id="d6bd4-134">Файл `POM.xml` содержит сведения о конфигурации проекта Maven.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-134">The `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="d6bd4-135">Интересные фрагменты:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-135">The interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="d6bd4-136">Компоненты концентратора событий</span><span class="sxs-lookup"><span data-stu-id="d6bd4-136">Event Hub components</span></span>

<span data-ttu-id="d6bd4-137">Компонент, который считывает и записывает в концентраторы событий Azure, находится в [репозитории HDInsight](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-137">The component that reads and writes to Azure Event Hubs is located in the [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="d6bd4-138">Следующие разделы в файле `POM.xml` загружают компоненты из этого репозитория.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-138">The following sections in the `POM.xml` file load the components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="the-eventhubs-storm-spout-dependency"></a><span data-ttu-id="d6bd4-139">Зависимость EventHubs Storm Spout</span><span class="sxs-lookup"><span data-stu-id="d6bd4-139">The EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="d6bd4-140">Этот XML-файл определяет зависимость для пакета eventhubs, который содержит как элемент spout для чтения данных из концентратора событий, так и элемент bolt для записи в него.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="d6bd4-141">Этот XML-файл настраивает проект для создания выходных данных для Java 8, которые использует HDInsight версии 3.5 или выше.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-141">This xml configures the project to generate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="the-maven-shade-plugin"></a><span data-ttu-id="d6bd4-142">maven-shade-plugin</span><span class="sxs-lookup"><span data-stu-id="d6bd4-142">The maven-shade-plugin</span></span>

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

<span data-ttu-id="d6bd4-143">Этот подключаемый модуль xml настраивает решение, чтобы упаковать выходные данные в файл типа uber jar.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-143">This xml configures the solution to package the output into an uber jar.</span></span> <span data-ttu-id="d6bd4-144">JAR-файл содержит код проекта и требуемые зависимости.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-144">The jar contains both the project code and required dependencies.</span></span> <span data-ttu-id="d6bd4-145">Он также используется для:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-145">It is also used to:</span></span>

* <span data-ttu-id="d6bd4-146">Переименования файлов лицензии для зависимостей.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-146">Rename license files for the dependencies.</span></span>
* <span data-ttu-id="d6bd4-147">Исключения групп безопасности и подписей.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="d6bd4-148">Различные реализации одного и того же интерфейса должны быть объединены в одну запись.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-148">Ensure that multiple implementations of the same interface are merged into one entry.</span></span>

<span data-ttu-id="d6bd4-149">Эти параметры конфигурации предотвращают ошибки во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="d6bd4-150">Определения топологии</span><span class="sxs-lookup"><span data-stu-id="d6bd4-150">Topology definitions</span></span>

<span data-ttu-id="d6bd4-151">В этом примере используется платформа [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-151">This example uses the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="d6bd4-152">Она использует YAML для определения топологий.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-152">This framework uses YAML to define the topologies.</span></span> <span data-ttu-id="d6bd4-153">Основное преимущество заключается в том, что вы не жестко кодируете топологию в коде Java.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-153">The primary benefit is that you aren't hard coding the topology in Java code.</span></span> <span data-ttu-id="d6bd4-154">Так как определение типа YAML, вы можете изменить его перед отправкой топологии, не перекомпилируя все.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-154">Since the definition is YAML, you can change it before submitting the topology, without having to recompile everything.</span></span>

<span data-ttu-id="d6bd4-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure the Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through the components
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

<span data-ttu-id="d6bd4-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure the Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
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

# How data flows through the components
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

#### <a name="tell-the-topology-about-event-hub"></a><span data-ttu-id="d6bd4-157">Передача конфигурации концентратора событий в топологию</span><span class="sxs-lookup"><span data-stu-id="d6bd4-157">Tell the topology about Event Hub</span></span>

<span data-ttu-id="d6bd4-158">Во время выполнения файл `dev.properties` используется для передачи конфигурации концентратора событий в топологию.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-158">At run time, the `dev.properties` file is used to pass the Event Hub configuration to the topology.</span></span> <span data-ttu-id="d6bd4-159">Ниже приведено содержимое этого файла по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-159">The following example is the default contents of the file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="d6bd4-160">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="d6bd4-160">Configure environment variables</span></span>

<span data-ttu-id="d6bd4-161">Во время установки Java и JDK на компьютере, где ведется разработка, могут быть установлены следующие переменные среды.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-161">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="d6bd4-162">Однако следует убедиться, что они существуют и что они содержат правильные значения для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-162">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="d6bd4-163">**JAVA_HOME** — эта переменная должна указывать на каталог, в который установлена среда выполнения Java (JRE).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-163">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="d6bd4-164">Например, в дистрибутиве Unix или Linux она должна иметь примерно такое значение: `/usr/lib/jvm/java-7-oracle`</span><span class="sxs-lookup"><span data-stu-id="d6bd4-164">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="d6bd4-165">В Windows значение будет приблизительно таким: `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="d6bd4-165">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="d6bd4-166">**PATH** — эта переменная должна содержать следующие пути:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-166">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="d6bd4-167">**JAVA_HOME** или эквивалентный путь;</span><span class="sxs-lookup"><span data-stu-id="d6bd4-167">**JAVA_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="d6bd4-168">**JAVA_HOME\bin** или эквивалентный путь.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-168">**JAVA_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="d6bd4-169">Каталог, в который установлено ПО Maven.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-169">The directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="d6bd4-170">Настройка концентраторов Event Hub</span><span class="sxs-lookup"><span data-stu-id="d6bd4-170">Configure Event Hub</span></span>

<span data-ttu-id="d6bd4-171">Служба концентраторов событий используется в качестве источника данных для этого примера.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-171">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="d6bd4-172">Чтобы создать концентратор событий, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-172">Use the following steps to create a Event Hub.</span></span>

1. <span data-ttu-id="d6bd4-173">На [классическом портале Azure](https://manage.windowsazure.com) выберите **Создать** > **Служебная шина** > **Концентратор событий** > **Настраиваемое создание**.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-173">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="d6bd4-174">В диалоговом окне **Добавить новый концентратор событий** введите **имя концентратора событий**.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-174">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="d6bd4-175">Выберите **регион** для его создания и создайте пространство имен или выберите имеющееся.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-175">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="d6bd4-176">Затем щелкните **стрелку**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-176">Finally, click the **Arrow** to continue.</span></span>

    ![страница мастера 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="d6bd4-178">Чтобы сократить задержки и затраты, в поле **Расположение** следует выбрать то же расположение, в котором находится сервер Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-178">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span></span>

3. <span data-ttu-id="d6bd4-179">В диалоговом окне **Настроить концентратор событий** введите значения параметров **Количество разделов** и **Хранение сообщений**.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-179">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="d6bd4-180">В этом примере числу разделов присвойте значение 10, а хранению сообщений — 1.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="d6bd4-181">Запомните количество разделов, так как позже вам понадобится это значение.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-181">Note the partition count because you need this value later.</span></span>

    ![страница мастера 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="d6bd4-183">После создания концентратора событий выберите пространство имен, выберите **Концентраторы событий**, а затем выберите концентратор событий, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-183">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span></span>
5. <span data-ttu-id="d6bd4-184">Выберите **Настроить** и создайте две политики доступа, используя следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-184">Select **Configure**, then create two new access policies by using the following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="d6bd4-185">Имя</span><span class="sxs-lookup"><span data-stu-id="d6bd4-185">Name</span></span></th><th><span data-ttu-id="d6bd4-186">Разрешения</span><span class="sxs-lookup"><span data-stu-id="d6bd4-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="d6bd4-187">Модуль записи</span><span class="sxs-lookup"><span data-stu-id="d6bd4-187">Writer</span></span></td><td><span data-ttu-id="d6bd4-188">Отправка</span><span class="sxs-lookup"><span data-stu-id="d6bd4-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="d6bd4-189">читатель.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-189">Reader</span></span></td><td><span data-ttu-id="d6bd4-190">Прослушивание</span><span class="sxs-lookup"><span data-stu-id="d6bd4-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="d6bd4-191">После создания разрешений выберите значок **Сохранить** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-191">After You create the permissions, select the **Save** icon at the bottom of the page.</span></span> <span data-ttu-id="d6bd4-192">Эти политики общего доступа используются для чтения и записи в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-192">These shared access policies are used to read and write to Event Hub.</span></span>

    ![политики](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="d6bd4-194">После сохранения политик используйте **генератор общего ключа доступа** в нижней части страницы для получения ключа для политик **writer** и **reader**.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-194">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span></span> <span data-ttu-id="d6bd4-195">Сохраните эти значения.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-195">Save these keys.</span></span>

## <a name="download-and-build-the-project"></a><span data-ttu-id="d6bd4-196">Загрузка и сборка проекта</span><span class="sxs-lookup"><span data-stu-id="d6bd4-196">Download and build the project</span></span>

1. <span data-ttu-id="d6bd4-197">Скачайте проект [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) с сайта GitHub</span><span class="sxs-lookup"><span data-stu-id="d6bd4-197">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="d6bd4-198">в виде ZIP-файла либо клонируйте проект локально с помощью [git](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-198">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span></span>

2. <span data-ttu-id="d6bd4-199">Измените файл `dev.properties`, используя конфигурацию вашего концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-199">Modify the `dev.properties` file with the configuration for your Event Hub.</span></span>

3. <span data-ttu-id="d6bd4-200">Используйте следующую команду, чтобы собрать и упаковать проект:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-200">Use the following to build and package the project:</span></span>

        mvn package

    <span data-ttu-id="d6bd4-201">Эта команда скачивает необходимые зависимости, а также создает и упаковывает проект.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-201">This command downloads required dependencies, builds, and then packages the project.</span></span> <span data-ttu-id="d6bd4-202">Выходные данные сохраняются в файл **EventHubExample-1.0-SNAPSHOT.jar** в каталоге **/target**.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-202">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="d6bd4-203">Локальное тестирование</span><span class="sxs-lookup"><span data-stu-id="d6bd4-203">Test locally</span></span>

<span data-ttu-id="d6bd4-204">Так как эти топологии просто считываются и записываются в концентраторы событий, вы можете протестировать их локально, если у вас есть [среда разработки Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-204">Since these topologies just read and write to Event Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="d6bd4-205">Для запуска локально в среде разработки выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-205">Use the following steps to run locally in the dev environment:</span></span>

1. <span data-ttu-id="d6bd4-206">Запустите средство записи:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-206">Run the writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="d6bd4-207">Запустите средство чтения:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-207">Run the reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="d6bd4-208">`--local`: запускает топологию в локальном режиме (нераспространяемый).</span><span class="sxs-lookup"><span data-stu-id="d6bd4-208">`--local`: Run the topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="d6bd4-209">`-R /writer.yaml`: загружает определение топологии из раздела `resources`, упакованного в JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-209">`-R /writer.yaml`: Load the topology definition from the `resources` packaged in the jar.</span></span> <span data-ttu-id="d6bd4-210">Если топология — это файл в локальной файловой системе, укажите путь к нему в качестве последнего параметра.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-210">If the topology is a file on the local file system, specify the path to it as the last parameter instead.</span></span>
> * <span data-ttu-id="d6bd4-211">`--filter dev.properties`: использование содержимого `dev.properties`, чтобы заполнить значения в определениях топологии.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-211">`--filter dev.properties`: Use the contents of `dev.properties` to fill in the values in the topology definitions.</span></span> <span data-ttu-id="d6bd4-212">Пример: `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="d6bd4-213">Выходные данные регистрируются в консоли при локальном выполнении.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-213">Output is logged to the console when running locally.</span></span> <span data-ttu-id="d6bd4-214">Чтобы остановить топологию, нажмите клавиши __CTRL+C__.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-214">Use __Ctrl+C__ to stop the topology.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="d6bd4-215">Развертывание топологий</span><span class="sxs-lookup"><span data-stu-id="d6bd4-215">Deploy the topologies</span></span>

1. <span data-ttu-id="d6bd4-216">Используя SCP, скопируйте JAR-пакет в свой кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-216">Use SCP to copy the jar package to your HDInsight cluster.</span></span> <span data-ttu-id="d6bd4-217">Замените USERNAME именем пользователя SSH для кластера.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-217">Replace USERNAME with the SSH user for your cluster.</span></span> <span data-ttu-id="d6bd4-218">Замените CLUSTERNAME именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-218">Replace CLUSTERNAME with the name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="d6bd4-219">Если для учетной записи SSH используется пароль, вам потребуется его ввести.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-219">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="d6bd4-220">Если для учетной записи SSH используется ключ, возможно, вам потребуется использовать параметр `-i` , чтобы указать путь к файлу ключа.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-220">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="d6bd4-221">Например, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="d6bd4-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="d6bd4-222">Эта команда скопирует файл в основной каталог пользователя SSH в кластере.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-222">This command copies the file to the home directory of your SSH user on the cluster.</span></span>

2. <span data-ttu-id="d6bd4-223">После завершения передачи подключитесь к кластеру HDInsight по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-223">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="d6bd4-224">Замените **USERNAME** именем пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-224">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="d6bd4-225">Замените **CLUSTERNAME** именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="d6bd4-226">Если для учетной записи SSH используется пароль, вам потребуется его ввести.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-226">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="d6bd4-227">Если для учетной записи SSH используется ключ, возможно, вам потребуется использовать параметр `-i` , чтобы указать путь к файлу ключа.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-227">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="d6bd4-228">В следующем примере выполняется загрузка закрытого ключа из файла `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-228">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="d6bd4-229">Запустите топологии, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-229">Use the following command to start the topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="d6bd4-230">`--remote`: отправляет топологию в службу Nimbus, которая запускает ее на рабочих узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-230">`--remote`: Submits the topology to the Nimbus service, which starts it on the worker nodes in the cluster.</span></span>

4. <span data-ttu-id="d6bd4-231">Чтобы просмотреть зарегистрированные данные, перейдите на страницу https://CLUSTERNAME.azurehdinsight.net/stormui, где __CLUSTERNAME__ — это имя вашего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-231">To view the logged data, go to https://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is the name of your HDInsight cluster.</span></span> <span data-ttu-id="d6bd4-232">Выберите топологии и перейдите к компонентам.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-232">Select the topologies and drill down to the components.</span></span> <span data-ttu-id="d6bd4-233">Выберите запись __port__, чтобы просмотреть зарегистрированные сведения об этом компоненте.</span><span class="sxs-lookup"><span data-stu-id="d6bd4-233">Select the __port__ entry for an instance of a component to view logged information.</span></span>

5. <span data-ttu-id="d6bd4-234">Чтобы остановить топологии, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="d6bd4-234">Use the following commands to stop the topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="d6bd4-235">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="d6bd4-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d6bd4-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6bd4-236">Next steps</span></span>

* [<span data-ttu-id="d6bd4-237">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6bd4-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
