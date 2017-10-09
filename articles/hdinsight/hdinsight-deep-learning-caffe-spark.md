---
title: "aaaUse Caffe на Azure HDInsight Spark для распределенных углубленного обучения | Документы Microsoft"
description: "Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения"
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="f0354-103">Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения</span><span class="sxs-lookup"><span data-stu-id="f0354-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="f0354-104">Введение</span><span class="sxs-lookup"><span data-stu-id="f0354-104">Introduction</span></span>

<span data-ttu-id="f0354-105">Углубленного обучения влияет все данные из сферы здравоохранения tootransportation toomanufacturing и многое другое.</span><span class="sxs-lookup"><span data-stu-id="f0354-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="f0354-106">Компании требуется включить toodeep обучения toosolve сложных проблем, таких как [изображения классификации](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [распознавания речи](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)объекта распознавания и машинного перевода.</span><span class="sxs-lookup"><span data-stu-id="f0354-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="f0354-107">Существует [множество популярных платформ](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), в том числе [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano и т. д. Caffe является одним из hello самый знаменитый платформы не являющиеся символьными (императивного) нейронной сети и широко используется во многих областях, включая компьютерного зрения.</span><span class="sxs-lookup"><span data-stu-id="f0354-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="f0354-108">Более того, система [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) сочетает в себе возможности Caffe и Apache Spark, за счет чего глубокое обучение может выполняться непосредственно в кластере Hadoop с конвейерами извлечения, преобразования и загрузки Spark. Это уменьшает сложность системы комплексного обучения и задержки при выполнении этого процесса.</span><span class="sxs-lookup"><span data-stu-id="f0354-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="f0354-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) — hello только предложения Hadoop полностью управляются облака, предоставляющий оптимизированный аналитической кластеров открытым исходным кодом для Spark, Hive, MapReduce, HBase, Storm, Kafka и R Server, поддерживаемый 99,9% SLA.</span><span class="sxs-lookup"><span data-stu-id="f0354-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="f0354-110">Каждую из этих технологий работы с большими данными и каждое из этих приложений от независимых поставщиков программного обеспечения можно с легкостью развернуть в качестве управляемого кластера, обеспечив при этом безопасность и мониторинг корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="f0354-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="f0354-111">Некоторые пользователи просим нам о том, как toouse глубокого изучения на HDInsight PaaS Hadoop продуктов корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f0354-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="f0354-112">Мы должны иметь дополнительные tooshare в будущем hello, однако сегодня мы хотим toosummarize Технический блог о том, как toouse Caffe на HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f0354-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="f0354-113">Если вы устанавливали Caffe раньше, вы заметили, что этот процесс связан с определенными трудностями.</span><span class="sxs-lookup"><span data-stu-id="f0354-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="f0354-114">В этом блоге мы будет показано как tooinstall [Caffe на Spark](https://github.com/yahoo/CaffeOnSpark) для кластера HDInsight, затем использовать hello встроенных MNIST Демонстрация toodemostrate как toouse распределенных углубленного обучения с помощью HDInsight Spark на процессорах.</span><span class="sxs-lookup"><span data-stu-id="f0354-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="f0354-115">Существует четыре основных шагов tooget, он работает в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0354-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="f0354-116">Установите необходимые hello зависимости на всех узлах hello</span><span class="sxs-lookup"><span data-stu-id="f0354-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="f0354-117">Построение Caffe на Spark для HDInsight на головном узле hello</span><span class="sxs-lookup"><span data-stu-id="f0354-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="f0354-118">Распространение hello необходимые библиотеки tooall hello рабочих узлов</span><span class="sxs-lookup"><span data-stu-id="f0354-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="f0354-119">Разработка модели и распределенный запуск Caffe.</span><span class="sxs-lookup"><span data-stu-id="f0354-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="f0354-120">Так как HDInsight решением PaaS, он обеспечивает значительные функций - это довольно просто tooperform некоторые задачи.</span><span class="sxs-lookup"><span data-stu-id="f0354-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="f0354-121">Одна из функций hello, активно используемые в этой записи блога называется [действие сценария](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), с которой выполнен оболочки команды toocustomize узлов кластера (головного узла, рабочий узел или граничного узла).</span><span class="sxs-lookup"><span data-stu-id="f0354-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="f0354-122">Шаг 1: Установка hello необходимые зависимости на всех узлах hello</span><span class="sxs-lookup"><span data-stu-id="f0354-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="f0354-123">tooget к работе, нам нужна tooinstall hello зависимости, которые необходимы.</span><span class="sxs-lookup"><span data-stu-id="f0354-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="f0354-124">узел Caffe Hello и [CaffeOnSpark сайта](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) предлагает некоторые вики-сайте очень полезен для установки зависимостей hello для Spark на YARN режиме (режим hello для HDInsight Spark), но нам нужен tooadd несколько Дополнительные зависимости для платформы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0354-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="f0354-125">Мы будет используйте действие скрипта hello, как показано ниже и запустите его на всех узлах головного hello и узлов рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="f0354-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="f0354-126">Его выполнение занимает примерно 20 минут, так как эти зависимости также зависят от других пакетов.</span><span class="sxs-lookup"><span data-stu-id="f0354-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="f0354-127">Необходимо поместить его в нужное расположение, доступный tooyour кластера HDInsight, такие как расположение GitHub или учетной записи хранилища больших двоичных ОБЪЕКТОВ по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


<span data-ttu-id="f0354-128">Действие сценария hello выше состоит из двух этапов.</span><span class="sxs-lookup"><span data-stu-id="f0354-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="f0354-129">Hello первым шагом является tooinstall Здравствуйте, все необходимые библиотеки.</span><span class="sxs-lookup"><span data-stu-id="f0354-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="f0354-130">Эти библиотеки включают в себя необходимые библиотеки hello для компиляции Caffe (например, gflags glog) и на которых работает Caffe (например, numpy).</span><span class="sxs-lookup"><span data-stu-id="f0354-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="f0354-131">Мы используем libatlas оптимизации использования ЦП, но может всегда следуют за hello CaffeOnSpark wiki об установке других библиотек оптимизации, например MKL или CUDA (для GPU).</span><span class="sxs-lookup"><span data-stu-id="f0354-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="f0354-132">Hello второй шаг — toodownload, скомпилировать и установить protobuf 2.5.0 для Caffe во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="f0354-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="f0354-133">Protobuf 2.5.0 [требуется](https://github.com/yahoo/CaffeOnSpark/issues/87), однако эта версия не предоставляется в виде пакета на Ubuntu 16, поэтому мы должны toocompile его из исходного кода hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="f0354-134">Есть несколько ресурсов на hello Интернет о том, как toocompile, такие как [это](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="f0354-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="f0354-135">toosimply начать работу, просто выполните это действие сценария для вашей рабочей hello tooall кластера узлов, узлов и head (для HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="f0354-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="f0354-136">Можно либо запустить hello действий сценария для выполнения кластера или hello действия скрипта можно также запустить во время подготовки кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="f0354-137">Дополнительные сведения о действиях скрипта hello см. в разделе документации hello [здесь](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="f0354-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Действия сценария tooInstall зависимости](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="f0354-139">Шаг 2: Построение Caffe на Spark для HDInsight на головном узле hello</span><span class="sxs-lookup"><span data-stu-id="f0354-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="f0354-140">второй шаг Hello — toobuild Caffe на hello головному узлу, а затем распространите hello скомпилированные библиотеки tooall hello рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="f0354-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="f0354-141">На этом шаге необходимо будет слишком[ssh в к головному узлу](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), просто выполните hello [процесс построения CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), а ниже приведен скрипт hello toobuild CaffeOnSpark можно использовать ряд дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="f0354-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="f0354-142">Может потребоваться toodo больше, чем говорит документации CaffeOnSpark какие hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="f0354-143">Hello изменениям относятся:</span><span class="sxs-lookup"><span data-stu-id="f0354-143">hello changes are:</span></span>
- <span data-ttu-id="f0354-144">Изменение только tooCPU и использование libatlas для этой конкретной цели.</span><span class="sxs-lookup"><span data-stu-id="f0354-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="f0354-145">Поместите hello наборы данных toohello BLOB-ОБЪЕКТА хранилища, которое является общей папкой, доступный tooall рабочих узлов для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="f0354-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="f0354-146">PUT hello скомпилированных Caffe библиотеки tooBLOB хранилища, а позже будет копировать с помощью дополнительных компиляции действия сценария tooavoid этих библиотек tooall hello узлов.</span><span class="sxs-lookup"><span data-stu-id="f0354-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="f0354-147">Устранение неполадок, связанных с ошибкой An Ant BuildException has occured: exec returned: 2</span><span class="sxs-lookup"><span data-stu-id="f0354-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="f0354-148">При первом toobuild CaffeOnSpark иногда появится сообщение</span><span class="sxs-lookup"><span data-stu-id="f0354-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="f0354-149">Репозиторий кода просто чистой hello, «создание чистой», а затем выполнения» убедитесь построения» решает эту проблему, поскольку имеют правильные зависимости hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="f0354-150">Устранение неполадок, связанных с ошибкой времени ожидания подключения к репозиторию Maven</span><span class="sxs-lookup"><span data-stu-id="f0354-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="f0354-151">Иногда maven дает мне ошибка времени ожидания подключения hello, аналогичные toobelow:</span><span class="sxs-lookup"><span data-stu-id="f0354-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="f0354-152">Оно ОК после ожидания в течение нескольких минут и затем повторите toorebuild hello кода, поэтому он может быть Maven каким-либо образом ограничения hello трафик от данного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f0354-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="f0354-153">Устранение неполадок, связанных со сбоем тестирования Caffe</span><span class="sxs-lookup"><span data-stu-id="f0354-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="f0354-154">Возможно, появится сбоя теста при выполнении hello окончательная проверка для CaffeOnSpark, аналогичные с ниже.</span><span class="sxs-lookup"><span data-stu-id="f0354-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="f0354-155">Это prabably, связанные с кодировкой UTF-8, но не должен влиять hello использование Caffe</span><span class="sxs-lookup"><span data-stu-id="f0354-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="f0354-156">Шаг 3: Распространять hello необходимые библиотеки tooall hello рабочих узлов</span><span class="sxs-lookup"><span data-stu-id="f0354-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="f0354-157">Hello следующим шагом является toodistribute hello библиотеки (по сути hello библиотек в CaffeOnSpark/caffe-public или распространять/lib/и CaffeOnSpark/caffe автомат или распространять/lib /) tooall hello узлов.</span><span class="sxs-lookup"><span data-stu-id="f0354-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="f0354-158">На шаге 2 мы поместили эти библиотеки в хранилище больших двоичных ОБЪЕКТОВ, и на этом шаге мы используем скрипт действия toocopy его tooall hello головного узла и узлов рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="f0354-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="f0354-159">toodo, простого выполнения сценария действия, как показано ниже (требуется правильное местоположение конкретного tooyour toopoint toohello кластера):</span><span class="sxs-lookup"><span data-stu-id="f0354-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="f0354-160">Так как на шаге 2 мы поместили в хранилище больших двоичных ОБЪЕКТОВ, т. е узлы hello доступного tooall hello, на этом шаге мы просто скопировать tooall hello узлов.</span><span class="sxs-lookup"><span data-stu-id="f0354-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="f0354-161">Этап 4. Разработка модели и распределенный запуск Caffe</span><span class="sxs-lookup"><span data-stu-id="f0354-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="f0354-162">После выполнения hello выше действия, который, установлены на головному узлу hello уже Caffe и мы являются хорошим toogo.</span><span class="sxs-lookup"><span data-stu-id="f0354-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="f0354-163">Hello следующим шагом является toowrite Caffe модели.</span><span class="sxs-lookup"><span data-stu-id="f0354-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="f0354-164">Caffe использует «выразительный архитектура,» там, где для составления модель, точно так же, вы должны toodefine файл конфигурации, а также без создания кода (в большинстве случаев).</span><span class="sxs-lookup"><span data-stu-id="f0354-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="f0354-165">Давайте рассмотрим этот процесс более подробно.</span><span class="sxs-lookup"><span data-stu-id="f0354-165">So let's take a look there.</span></span> 

<span data-ttu-id="f0354-166">Сегодня мы обучить модель Hello является образца модели для обучения MNIST.</span><span class="sxs-lookup"><span data-stu-id="f0354-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="f0354-167">База данных MNIST Hello рукописные цифр имеет 60 000 примеров обучающий и проверочный набор из 10 000 примеров.</span><span class="sxs-lookup"><span data-stu-id="f0354-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="f0354-168">Это подмножество более широкого набора из базы данных NIST.</span><span class="sxs-lookup"><span data-stu-id="f0354-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="f0354-169">Hello цифр были нормализованы размер и по центру в образе фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="f0354-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="f0354-170">CaffeOnSpark имеет некоторые сценарии toodownload hello dataset и преобразовать его в нужном формате hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="f0354-171">Эта система предоставляет несколько образцов сетевых топологий для обучения MNIST.</span><span class="sxs-lookup"><span data-stu-id="f0354-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="f0354-172">Он имеет четкий разработки разделения hello сетевую архитектуру (hello топологии сети hello) и оптимизации.</span><span class="sxs-lookup"><span data-stu-id="f0354-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="f0354-173">В этом случае вам потребуется два указанных ниже файла.</span><span class="sxs-lookup"><span data-stu-id="f0354-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="f0354-174">файл «Поиск решения» Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) используется для наблюдения за hello оптимизации и создания параметра обновления.</span><span class="sxs-lookup"><span data-stu-id="f0354-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="f0354-175">Например, определяет ли ЦП или GPU будет использован, какова импульс hello, число итераций, будут выполняться, и т. д. Он также определяет топологию сети нейрон следует Здравствуйте, используйте программу (который является второй файл hello будут).</span><span class="sxs-lookup"><span data-stu-id="f0354-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="f0354-176">Дополнительные сведения о поиска решения можно найти слишком[Caffe документации](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="f0354-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="f0354-177">Например так как мы используем ЦП, а не GPU, мы следует изменить hello последней строки для:</span><span class="sxs-lookup"><span data-stu-id="f0354-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Конфигурация Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="f0354-179">При необходимости вы можете изменить и другие строки.</span><span class="sxs-lookup"><span data-stu-id="f0354-179">You can change other lines as needed.</span></span>

<span data-ttu-id="f0354-180">второй файл Hello (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) определяет как сети нейрон hello выглядит и соответствующих входных данных hello и выходного файла.</span><span class="sxs-lookup"><span data-stu-id="f0354-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="f0354-181">Мы также должны tooupdate hello tooreflect hello обучающих данных местоположения.</span><span class="sxs-lookup"><span data-stu-id="f0354-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="f0354-182">Изменение hello следующие части в lenet_memory_train_test.prototxt (требуется правильное местоположение конкретного tooyour toopoint toohello кластера).</span><span class="sxs-lookup"><span data-stu-id="f0354-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="f0354-183">изменить file:/Users/mridul/bigml/demodl/mnist_train_lmdb «hello» слишком "wasb: / / / проекты/machine_learning/image_dataset/mnist_train_lmdb»</span><span class="sxs-lookup"><span data-stu-id="f0354-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="f0354-184">Измените «file:/Users/mridul/bigml/demodl/mnist_test_lmdb/» слишком "wasb: / / / проекты/machine_learning/image_dataset/mnist_test_lmdb»</span><span class="sxs-lookup"><span data-stu-id="f0354-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Конфигурация Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="f0354-186">Дополнительные сведения о как toodefine hello сети Проверьте hello [Caffe документацию по MNIST набора данных](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="f0354-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="f0354-187">Целью этого блога hello мы просто используйте этот простой пример MNIST.</span><span class="sxs-lookup"><span data-stu-id="f0354-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="f0354-188">Hello указанную ниже команду необходимо запускать из головного узла hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="f0354-189">По сути он распределяет hello необходимые файлы (lenet_memory_solver.prototxt и lenet_memory_train_test.prototxt) tooeach YARN контейнера, а также задать hello соответствующие пути каждого tooLD_LIBRARY_PATH драйвера или исполнитель Spark, которая определена в hello предыдущего фрагмента и точки toohello расположения в коде с CaffeOnSpark библиотеки.</span><span class="sxs-lookup"><span data-stu-id="f0354-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="f0354-190">Мониторинг и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f0354-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="f0354-191">Так как мы используем режим YARN кластера, в этом случае драйвер Spark hello будет запланированных tooan произвольный контейнер (и произвольные рабочий узел) вы должны видеть только в вывод консоли hello что-то наподобие:</span><span class="sxs-lookup"><span data-stu-id="f0354-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="f0354-192">Если вы хотите tooknow, что произошло, обычно требуется журнал tooget hello Spark драйвер, который содержит дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="f0354-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="f0354-193">В этом случае необходимо toogo toohello пользовательского интерфейса YARN toofind hello YARN журналы.</span><span class="sxs-lookup"><span data-stu-id="f0354-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="f0354-194">Чтобы узнать hello YARN пользовательского интерфейса, этот URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="f0354-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Пользовательский интерфейс YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="f0354-196">Здесь вы можете просмотреть сведения о количестве выделенных ресурсов для этого конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="f0354-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="f0354-197">Можно щелкнуть ссылку «Планировщик» hello, и будет отображаться для этого приложения, 9 запущенных контейнеров.</span><span class="sxs-lookup"><span data-stu-id="f0354-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="f0354-198">Мы просим YARN tooprovide 8 исполнителей, а другой контейнер — для процесса драйвера.</span><span class="sxs-lookup"><span data-stu-id="f0354-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![Планировщик YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="f0354-200">Вы можете toocheck hello драйвер журналов или контейнер журналов в случае сбоев.</span><span class="sxs-lookup"><span data-stu-id="f0354-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="f0354-201">Для журналов драйвера можно щелкните идентификатор приложения hello в пользовательском Интерфейсе YARN, а затем нажмите кнопку «Журналы» hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="f0354-202">Hello драйвер журналы записываются в stderr.</span><span class="sxs-lookup"><span data-stu-id="f0354-202">hello driver logs are written into stderr.</span></span>

![Пользовательский интерфейс YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="f0354-204">Например может появиться некоторые hello следующую ошибку из журналов драйвер hello, о том, что выделено слишком много исполнителей.</span><span class="sxs-lookup"><span data-stu-id="f0354-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

<span data-ttu-id="f0354-205">В некоторых случаях hello проблема может произойти на исполнителей, а не драйверы.</span><span class="sxs-lookup"><span data-stu-id="f0354-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="f0354-206">В этом случае необходимо toocheck hello контейнера журналы.</span><span class="sxs-lookup"><span data-stu-id="f0354-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="f0354-207">Всегда получать журналы контейнера hello и затем получить hello сбой контейнер.</span><span class="sxs-lookup"><span data-stu-id="f0354-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="f0354-208">Например, этот сбой может произойти при запуске Caffe.</span><span class="sxs-lookup"><span data-stu-id="f0354-208">For example, you might meet this failure when running Caffe.</span></span>

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

<span data-ttu-id="f0354-209">В этом случае требуется идентификатор контейнера hello сбой tooget (hello выше случая при container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="f0354-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="f0354-210">Затем необходимо toorun</span><span class="sxs-lookup"><span data-stu-id="f0354-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="f0354-211">из головному узлу hello.</span><span class="sxs-lookup"><span data-stu-id="f0354-211">from hello headnode.</span></span> <span data-ttu-id="f0354-212">вы определите, что он произошел из-за использования режима графического процессора в файле lenet_memory_solver.prototxt (вместо режима ЦП).</span><span class="sxs-lookup"><span data-stu-id="f0354-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="f0354-213">Получение результатов</span><span class="sxs-lookup"><span data-stu-id="f0354-213">Getting results</span></span>

<span data-ttu-id="f0354-214">Поскольку мы выделяемый 8 исполнителей и топология сети hello проста, его обычно занимает около 30 минут toorun hello результат.</span><span class="sxs-lookup"><span data-stu-id="f0354-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="f0354-215">Из командной строки hello, вы увидите мы поместить toowasb:///mnist.model модели hello и помещать hello результаты tooa папку с именем wasb: / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="f0354-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="f0354-216">Hello результаты можно получить, выполнив</span><span class="sxs-lookup"><span data-stu-id="f0354-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="f0354-217">и как выглядит результат hello:</span><span class="sxs-lookup"><span data-stu-id="f0354-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="f0354-218">Hello SampleID представляет идентификатор hello в наборе данных MNIST hello и hello метки является определяет число hello, hello модели.</span><span class="sxs-lookup"><span data-stu-id="f0354-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="f0354-219">Заключение</span><span class="sxs-lookup"><span data-stu-id="f0354-219">Conclusion</span></span>

<span data-ttu-id="f0354-220">В этой документации предпринята tooinstall CaffeOnSpark с работающими простой пример.</span><span class="sxs-lookup"><span data-stu-id="f0354-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="f0354-221">HDInsight — это платформа распределенных вычислений полный управляемой облачной и hello лучше всего подходит для выполнения машинного обучения и расширенных аналитических рабочих нагрузок на большой набор данных, и для распределенной углубленного обучения, можно использовать Caffe на HDInsight Spark tooperform углубленного обучения задачи.</span><span class="sxs-lookup"><span data-stu-id="f0354-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="f0354-222"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="f0354-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f0354-223">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0354-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f0354-224">Сценарии</span><span class="sxs-lookup"><span data-stu-id="f0354-224">Scenarios</span></span>
* [<span data-ttu-id="f0354-225">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="f0354-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f0354-226">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="f0354-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="f0354-227">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="f0354-227">Manage resources</span></span>
* [<span data-ttu-id="f0354-228">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0354-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

