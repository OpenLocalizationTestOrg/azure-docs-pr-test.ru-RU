---
title: "Apache Storm с компонентами Python. Azure HDInsight | Документация Майкрософт"
description: "Сведения о создании топологии Apache Storm, использующей компоненты Python."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="21aa9-104">Разработка топологий Apache Storm с помощью Python в HDInsight</span><span class="sxs-lookup"><span data-stu-id="21aa9-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="21aa9-105">В этой статье приведены сведения о создании топологии Apache Storm, использующей компоненты Python.</span><span class="sxs-lookup"><span data-stu-id="21aa9-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="21aa9-106">Apache Storm поддерживает несколько языков и даже позволяет объединять компоненты из нескольких языков в одной топологии.</span><span class="sxs-lookup"><span data-stu-id="21aa9-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="21aa9-107">Платформа Flux (впервые появилась в Storm 0.10.0) позволяет легко создавать решения, использующие компоненты Python.</span><span class="sxs-lookup"><span data-stu-id="21aa9-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21aa9-108">Сведения в этом документе были проверены с использованием Storm в HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="21aa9-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="21aa9-109">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="21aa9-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="21aa9-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="21aa9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="21aa9-111">Код для этого проекта доступен здесь: [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="21aa9-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21aa9-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="21aa9-112">Prerequisites</span></span>

* <span data-ttu-id="21aa9-113">Python 2.7 или выше;</span><span class="sxs-lookup"><span data-stu-id="21aa9-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="21aa9-114">Пакет Java JDK 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="21aa9-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="21aa9-115">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="21aa9-115">Maven 3</span></span>

* <span data-ttu-id="21aa9-116">(Необязательно.) Локальная среда разработки Storm.</span><span class="sxs-lookup"><span data-stu-id="21aa9-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="21aa9-117">Локальная среда разработки Storm требуется только в том случае, если вы хотите запускать топологию локально.</span><span class="sxs-lookup"><span data-stu-id="21aa9-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="21aa9-118">Дополнительные сведения см. в разделе [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Настройка среды разработки).</span><span class="sxs-lookup"><span data-stu-id="21aa9-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="21aa9-119">Многоязыковая поддержка Storm</span><span class="sxs-lookup"><span data-stu-id="21aa9-119">Storm multi-language support</span></span>

<span data-ttu-id="21aa9-120">Среда разработки Apache Storm была разработана для работы с компонентами, написанными на любом языке программирования.</span><span class="sxs-lookup"><span data-stu-id="21aa9-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="21aa9-121">Компоненты должны "понимать", как работать с [определением Thrift для Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="21aa9-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="21aa9-122">В рамках проекта Apache Storm предоставляется модуль для Python, который позволяет легко взаимодействовать со Storm.</span><span class="sxs-lookup"><span data-stu-id="21aa9-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="21aa9-123">Этот модуль можно найти по адресу [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="21aa9-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="21aa9-124">Storm является процессом Java, который работает на виртуальной машине Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="21aa9-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="21aa9-125">Компоненты, написанные на других языках, выполняются как подпроцессы.</span><span class="sxs-lookup"><span data-stu-id="21aa9-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="21aa9-126">Storm взаимодействуют с этими подпроцессами с помощью сообщений JSON, отправляемых через стандартные потоки stdin и stdout.</span><span class="sxs-lookup"><span data-stu-id="21aa9-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="21aa9-127">Дополнительные сведения о связи между компонентами можно найти в документации по [многоязыковому протоколу](https://storm.apache.org/documentation/Multilang-protocol.html) .</span><span class="sxs-lookup"><span data-stu-id="21aa9-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="21aa9-128">Python с платформой Flux</span><span class="sxs-lookup"><span data-stu-id="21aa9-128">Python with the Flux framework</span></span>

<span data-ttu-id="21aa9-129">Платформа Flux позволяет определять топологии Storm отдельно от компонентов.</span><span class="sxs-lookup"><span data-stu-id="21aa9-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="21aa9-130">Она использует YAML для определения топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="21aa9-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="21aa9-131">Ниже приведен пример указания ссылки на компонент Python в документе YAML.</span><span class="sxs-lookup"><span data-stu-id="21aa9-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="21aa9-132">Класс `FluxShellSpout` используется для сценария `sentencespout.py`, который реализует spout.</span><span class="sxs-lookup"><span data-stu-id="21aa9-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="21aa9-133">Flux ожидает, что сценарии Python находятся в каталоге `/resources` в JAR-файле, содержащем топологию.</span><span class="sxs-lookup"><span data-stu-id="21aa9-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="21aa9-134">Поэтому в этом примере сценарии Python хранятся в каталоге `/multilang/resources`.</span><span class="sxs-lookup"><span data-stu-id="21aa9-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="21aa9-135">В `pom.xml` этот файл указан с помощью приведенного ниже кода XML.</span><span class="sxs-lookup"><span data-stu-id="21aa9-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="21aa9-136">Как упоминалось ранее, существует файл `storm.py`, который реализует определение Thrift для Storm.</span><span class="sxs-lookup"><span data-stu-id="21aa9-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="21aa9-137">Платформа Flux добавляет `storm.py` автоматически при выполнении сборки проекта, поэтому не нужно беспокоиться о его добавлении.</span><span class="sxs-lookup"><span data-stu-id="21aa9-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="21aa9-138">Сборка проекта</span><span class="sxs-lookup"><span data-stu-id="21aa9-138">Build the project</span></span>

<span data-ttu-id="21aa9-139">В корневом каталоге проекта выполите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="21aa9-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="21aa9-140">Она создает файл `target/WordCount-1.0-SNAPSHOT.jar`, содержащий скомпилированную топологию.</span><span class="sxs-lookup"><span data-stu-id="21aa9-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="21aa9-141">Локальный запуск топологии</span><span class="sxs-lookup"><span data-stu-id="21aa9-141">Run the topology locally</span></span>

<span data-ttu-id="21aa9-142">Для локального запуска топологии введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="21aa9-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="21aa9-143">Для ее выполнения нужна локальная среда разработки Storm.</span><span class="sxs-lookup"><span data-stu-id="21aa9-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="21aa9-144">Дополнительные сведения см. в разделе [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Настройка среды разработки).</span><span class="sxs-lookup"><span data-stu-id="21aa9-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="21aa9-145">После запуска топология выдает в локальную консоль информацию следующего вида.</span><span class="sxs-lookup"><span data-stu-id="21aa9-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="21aa9-146">Чтобы остановить топологию, нажмите сочетание клавиш __CTRL+C__.</span><span class="sxs-lookup"><span data-stu-id="21aa9-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="21aa9-147">Запуск топологии Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="21aa9-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="21aa9-148">Воспользуйтесь приведенной ниже командой, чтобы скопировать файл `WordCount-1.0-SNAPSHOT.jar` в кластер Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21aa9-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="21aa9-149">Замените `sshuser` именем пользователя SSH для кластера.</span><span class="sxs-lookup"><span data-stu-id="21aa9-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="21aa9-150">Замените `mycluster` именем кластера.</span><span class="sxs-lookup"><span data-stu-id="21aa9-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="21aa9-151">При появлении запроса введите пароль пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="21aa9-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="21aa9-152">Дополнительные сведения об использовании SSH и SCP см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="21aa9-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="21aa9-153">После завершения передачи файла подключитесь к кластеру с помощью протокола SSH.</span><span class="sxs-lookup"><span data-stu-id="21aa9-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="21aa9-154">В сеансе SSH используйте следующую команду, чтобы запустить топологию на кластере.</span><span class="sxs-lookup"><span data-stu-id="21aa9-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="21aa9-155">Для просмотра топологии в кластере можно использовать пользовательский интерфейс Storm.</span><span class="sxs-lookup"><span data-stu-id="21aa9-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="21aa9-156">Он доступен по адресу https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="21aa9-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="21aa9-157">Замените `mycluster` именем кластера.</span><span class="sxs-lookup"><span data-stu-id="21aa9-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="21aa9-158">После запуска топология Storm выполняется до тех пор, пока она не будет остановлена.</span><span class="sxs-lookup"><span data-stu-id="21aa9-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="21aa9-159">Чтобы остановить топологию, используйте один из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="21aa9-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="21aa9-160">выполните команду `storm kill TOPOLOGYNAME` из командной строки;</span><span class="sxs-lookup"><span data-stu-id="21aa9-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="21aa9-161">нажмите кнопку **Kill** (Завершить) в пользовательском интерфейсе Storm.</span><span class="sxs-lookup"><span data-stu-id="21aa9-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="21aa9-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21aa9-162">Next steps</span></span>

<span data-ttu-id="21aa9-163">Чтобы узнать о других способах использования Python с HDInsight, см. следующие документы.</span><span class="sxs-lookup"><span data-stu-id="21aa9-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="21aa9-164">Использование Python для потоковой передачи заданий MapReduce.</span><span class="sxs-lookup"><span data-stu-id="21aa9-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="21aa9-165">Использование определяемых пользователем функций Python (UDF) в Pig и Hive.</span><span class="sxs-lookup"><span data-stu-id="21aa9-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
