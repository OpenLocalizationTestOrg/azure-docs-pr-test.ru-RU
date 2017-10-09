---
title: "aaaApache Storm с компонентами Python - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Apache Storm топологию, которая использует компоненты Python."
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
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="ae5b6-104">Разработка топологий Apache Storm с помощью Python в HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae5b6-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="ae5b6-105">Узнайте, как toocreate Apache Storm топологию, которая использует компоненты Python.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="ae5b6-106">Apache Storm поддерживает несколько языков, позволяет создавать вы toocombine компоненты из нескольких языков в одной топологии.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="ae5b6-107">Hello framework определен (впервые появилась в Storm 0.10.0) позволяет вам tooeasily создания решений, использующих компоненты Python.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae5b6-108">Hello сведения в этом документе была протестирована с помощью Storm на HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="ae5b6-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ae5b6-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ae5b6-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="ae5b6-111">Hello код для данного проекта находится в [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="ae5b6-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae5b6-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ae5b6-112">Prerequisites</span></span>

* <span data-ttu-id="ae5b6-113">Python 2.7 или выше;</span><span class="sxs-lookup"><span data-stu-id="ae5b6-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="ae5b6-114">Пакет Java JDK 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="ae5b6-115">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-115">Maven 3</span></span>

* <span data-ttu-id="ae5b6-116">(Необязательно.) Локальная среда разработки Storm.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="ae5b6-117">В локальной среде Storm нужна только в том случае, если требуется топологии hello toorun локально.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="ae5b6-118">Дополнительные сведения см. в разделе [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Настройка среды разработки).</span><span class="sxs-lookup"><span data-stu-id="ae5b6-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="ae5b6-119">Многоязыковая поддержка Storm</span><span class="sxs-lookup"><span data-stu-id="ae5b6-119">Storm multi-language support</span></span>

<span data-ttu-id="ae5b6-120">Apache Storm был спроектированный toowork с компонентами, написанными на любом языке программирования.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="ae5b6-121">компоненты Hello необходимо понимать как toowork с hello [Thrift определение Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="ae5b6-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="ae5b6-122">Для Python модуль предоставляется как часть проекта Apache Storm hello, позволяющая интерфейс tooeasily с Storm.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="ae5b6-123">Этот модуль можно найти по адресу [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="ae5b6-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="ae5b6-124">Storm — это процесс Java, которое выполняется на виртуальной машине Java (JVM) hello.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="ae5b6-125">Компоненты, написанные на других языках, выполняются как подпроцессы.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="ae5b6-126">Hello Storm взаимодействует с этих вспомогательных процессов, с помощью JSON сообщений, отправляемых через стандартного ввода вывода.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="ae5b6-127">Дополнительные сведения о связи между компонентами, которые можно найти в hello [протокола многоязыковая](https://storm.apache.org/documentation/Multilang-protocol.html) документации.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="ae5b6-128">Python с framework определен hello</span><span class="sxs-lookup"><span data-stu-id="ae5b6-128">Python with hello Flux framework</span></span>

<span data-ttu-id="ae5b6-129">Hello меняется framework позволяет топологии Storm toodefine отдельно от компонентов hello.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="ae5b6-130">Hello меняется платформа использует hello Storm YAML toodefine топологии.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="ae5b6-131">Hello следующий текст является примером tooreference компонент Python в документе YAML hello:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

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

<span data-ttu-id="ae5b6-132">Здравствуйте, класс `FluxShellSpout` — используется toostart hello `sentencespout.py` скрипт, который реализует hello spout.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="ae5b6-133">Поток ожидает, что toobe скрипты Python hello hello `/resources` каталог внутри hello jar-файл, содержащий hello топологии.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="ae5b6-134">Поэтому в этом примере хранит hello сценариев Python в hello `/multilang/resources` каталога.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="ae5b6-135">Hello `pom.xml` включает этот файл при помощи hello следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="ae5b6-136">Как упоминалось ранее, имеется `storm.py` , реализующей hello определение Thrift Storm.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="ae5b6-137">Hello меняется framework включает в себя `storm.py` автоматически при hello сборке проекта, поэтому не нужно tooworry о ее включении.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="ae5b6-138">Построение проекта hello</span><span class="sxs-lookup"><span data-stu-id="ae5b6-138">Build hello project</span></span>

<span data-ttu-id="ae5b6-139">В корневой hello hello проекта используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="ae5b6-140">Эта команда создает `target/WordCount-1.0-SNAPSHOT.jar` файл, содержащий hello компилированных топологии.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="ae5b6-141">Запускать локально hello топологии</span><span class="sxs-lookup"><span data-stu-id="ae5b6-141">Run hello topology locally</span></span>

<span data-ttu-id="ae5b6-142">Топология hello toorun локально, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="ae5b6-143">Для ее выполнения нужна локальная среда разработки Storm.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="ae5b6-144">Дополнительные сведения см. в разделе [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Настройка среды разработки).</span><span class="sxs-lookup"><span data-stu-id="ae5b6-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="ae5b6-145">Один раз hello топологии запускается, он создает сведения toohello локальной консоли аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="ae5b6-146">Топология toostop hello, используйте __сочетание клавиш Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="ae5b6-147">Запустите топологии Storm hello в HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae5b6-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="ae5b6-148">Используйте hello следующая команда toocopy hello `WordCount-1.0-SNAPSHOT.jar` файл tooyour Storm в кластере HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="ae5b6-149">Замените `sshuser` пользователю hello SSH для кластера.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="ae5b6-150">Замените `mycluster` с именем кластера hello.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="ae5b6-151">Возможно, запрошенные tooenter hello пароль пользователя SSH hello.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="ae5b6-152">Дополнительные сведения об использовании SSH и SCP см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ae5b6-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ae5b6-153">После загрузки файла hello подключение toohello кластера с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="ae5b6-154">Из сеанса SSH hello используйте следующие команды toostart hello топологии на кластере hello hello:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="ae5b6-155">Hello пользовательского интерфейса Storm tooview hello топологии можно использовать в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="ae5b6-156">Hello Storm пользовательского интерфейса находится в https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="ae5b6-157">Замените `mycluster` именем кластера.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="ae5b6-158">После запуска топология Storm выполняется до тех пор, пока она не будет остановлена.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="ae5b6-159">Топология hello toostop, используйте один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="ae5b6-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="ae5b6-160">Hello `storm kill TOPOLOGYNAME` команду из командной строки hello</span><span class="sxs-lookup"><span data-stu-id="ae5b6-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="ae5b6-161">Hello **Kill** кнопку в hello Storm пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ae5b6-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae5b6-162">Next steps</span></span>

<span data-ttu-id="ae5b6-163">См. следующие документы для других способов toouse Python с HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ae5b6-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="ae5b6-164">Как toouse Python для потоковой передачи задания MapReduce</span><span class="sxs-lookup"><span data-stu-id="ae5b6-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="ae5b6-165">Как toouse Python пользовательской функции (UDF) в Pig и Hive</span><span class="sxs-lookup"><span data-stu-id="ae5b6-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
