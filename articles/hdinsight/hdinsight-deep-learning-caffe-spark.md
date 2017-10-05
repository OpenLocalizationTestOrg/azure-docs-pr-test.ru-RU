---
title: "Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения | Документация Майкрософт"
description: "Сведения об использовании Caffe в кластере Azure HDInsight Spark для выполнения распределенного глубокого обучения."
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
ms.openlocfilehash: 14b7808c9534bce3049422d6bce1e8914b2c2fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="f9264-103">Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения</span><span class="sxs-lookup"><span data-stu-id="f9264-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="f9264-104">Введение</span><span class="sxs-lookup"><span data-stu-id="f9264-104">Introduction</span></span>

<span data-ttu-id="f9264-105">Глубокое обучение используется во всех отраслях, начиная от здравоохранения и заканчивая сферой транспортировки и производством.</span><span class="sxs-lookup"><span data-stu-id="f9264-105">Deep learning is impacting everything from healthcare to transportation to manufacturing, and more.</span></span> <span data-ttu-id="f9264-106">Компании используют глубокое обучение для решения сложных проблем, таких так [классификация образов](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [распознавание речи](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), распознавание объектов и машинный перевод.</span><span class="sxs-lookup"><span data-stu-id="f9264-106">Companies are turning to deep learning to solve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="f9264-107">Существует [множество популярных платформ](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), в том числе [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano и т. д. Caffe — это самая известная платформа изучения нейронных сетей, работающая на уровне машинных команд. Она широко используется во многих областях, в том числе в компьютерном зрении.</span><span class="sxs-lookup"><span data-stu-id="f9264-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of the most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="f9264-108">Более того, система [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) сочетает в себе возможности Caffe и Apache Spark, за счет чего глубокое обучение может выполняться непосредственно в кластере Hadoop с конвейерами извлечения, преобразования и загрузки Spark. Это уменьшает сложность системы комплексного обучения и задержки при выполнении этого процесса.</span><span class="sxs-lookup"><span data-stu-id="f9264-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="f9264-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) — это единственное полностью управляемое облачное предложение Hadoop, предоставляющее оптимизированные аналитические кластеры с открытым кодом для Spark, Hive, MapReduce, HBase, Storm, Kafka и R Server и поддерживающее Соглашение об уровне обслуживания на 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="f9264-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is the only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="f9264-110">Каждую из этих технологий работы с большими данными и каждое из этих приложений от независимых поставщиков программного обеспечения можно с легкостью развернуть в качестве управляемого кластера, обеспечив при этом безопасность и мониторинг корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="f9264-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="f9264-111">Некоторые пользователи спрашивают нас, как выполнять глубокое обучение в кластере HDInsight, который является решением PaaS для Hadoop, предоставленным корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f9264-111">Some users are asking us about how to use deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="f9264-112">В будущем мы предоставим более детальные сведения, но сейчас хотим рассказать о технических моментах использования Caffe в HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f9264-112">We will have more to share in the future, but today we want to summarize a technical blog on how to use Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="f9264-113">Если вы устанавливали Caffe раньше, вы заметили, что этот процесс связан с определенными трудностями.</span><span class="sxs-lookup"><span data-stu-id="f9264-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="f9264-114">В этом блоге мы сначала рассмотрим процесс установки [CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark) в кластере HDInsight, а затем используем встроенную демоверсию базы данных MNIST, чтобы продемонстрировать, как выполнить распределенное глубокое обучение с помощью HDInsight Spark на ЦП.</span><span class="sxs-lookup"><span data-stu-id="f9264-114">In this blog, we will first illustrate how to install [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use the built-in MNIST demo to demostrate how to use Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="f9264-115">Установка Caffe on Spark в кластере HDInsight состоит из приведенных ниже четырех основных этапов.</span><span class="sxs-lookup"><span data-stu-id="f9264-115">There are four major steps to get it work on HDInsight.</span></span>

1. <span data-ttu-id="f9264-116">Установка необходимых зависимостей на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="f9264-116">Install the required dependencies on all the nodes</span></span>
2. <span data-ttu-id="f9264-117">Создание CaffeOnSpark для HDInsight на головном узле.</span><span class="sxs-lookup"><span data-stu-id="f9264-117">Build Caffe on Spark for HDInsight on the head node</span></span>
3. <span data-ttu-id="f9264-118">Развертывание необходимых библиотек на всех рабочих узлах.</span><span class="sxs-lookup"><span data-stu-id="f9264-118">Distribute the required libraries to all the worker nodes</span></span>
4. <span data-ttu-id="f9264-119">Разработка модели и распределенный запуск Caffe.</span><span class="sxs-lookup"><span data-stu-id="f9264-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="f9264-120">HDInsight — это платформа PaaS, предоставляющая расширенные функции, которые значительно упрощают выполнение некоторых заданий.</span><span class="sxs-lookup"><span data-stu-id="f9264-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy to perform some tasks.</span></span> <span data-ttu-id="f9264-121">Одна из функций, которую вы будете часто использовать при выполнении действий, описанных в этой записи блога, называется [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux) (Действие скрипта). Она позволяет выполнять команды оболочки, необходимые для настройки узлов кластера (головного, рабочего или граничного).</span><span class="sxs-lookup"><span data-stu-id="f9264-121">One of the features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands to customize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-the-required-dependencies-on-all-the-nodes"></a><span data-ttu-id="f9264-122">Этап 1. Установка необходимых зависимостей на всех узлах</span><span class="sxs-lookup"><span data-stu-id="f9264-122">Step 1:  Install the required dependencies on all the nodes</span></span>

<span data-ttu-id="f9264-123">Чтобы начать работу, нужно установить необходимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="f9264-123">To get started, we need to install the dependencies we need.</span></span> <span data-ttu-id="f9264-124">На сайте Caffe и [CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) доступны некоторые очень полезные вики-сайты для установки зависимостей Spark в режиме YARN (режим для HDInsight Spark), но нам нужно добавить дополнительные зависимости для платформы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9264-124">The Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing the dependencies for Spark on YARN mode (which is the mode for HDInsight Spark), but we need to add a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="f9264-125">Мы будем использовать приведенное ниже действие скрипта и выполним его на всех головных и рабочих узлах.</span><span class="sxs-lookup"><span data-stu-id="f9264-125">We will use the script action as below and run it on all the head nodes and worker nodes.</span></span> <span data-ttu-id="f9264-126">Его выполнение занимает примерно 20 минут, так как эти зависимости также зависят от других пакетов.</span><span class="sxs-lookup"><span data-stu-id="f9264-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="f9264-127">Это действие скрипта следует разместить в доступном для кластера HDInsight расположении, например в репозитории GitHub или в учетной записи хранилища BLOB-объектов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f9264-127">You should put it in some location that is accessible to your HDInsight cluster, such as a GitHub location or the default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing the below will add additional 20 mins to cluster creation because of the dependencies
    #installing all dependencies, including the ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all the nodes

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


<span data-ttu-id="f9264-128">Приведенный выше скрипт выполняется в два этапа.</span><span class="sxs-lookup"><span data-stu-id="f9264-128">There are two steps in the script action above.</span></span> <span data-ttu-id="f9264-129">Первый этап — установка всех необходимых библиотек.</span><span class="sxs-lookup"><span data-stu-id="f9264-129">The first step is to install all the required libraries.</span></span> <span data-ttu-id="f9264-130">Это библиотеки, необходимые для компиляции (например, gflags, glog) и запуска Caffe (например, numpy).</span><span class="sxs-lookup"><span data-stu-id="f9264-130">Those libraries include the necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="f9264-131">Для оптимизации ЦП мы используем библиотеку libatlas, но вы можете установить другие библиотеки, например MKL или CUDA (для графического процессора), следуя указаниям, приведенным на вики-сайте CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="f9264-131">We are using libatlas for CPU optimization, but you can always follow the CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="f9264-132">Второй этап — скачивание, компиляция и установка ProtoBuf 2.5.0 для Caffe во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="f9264-132">The second step is to download, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="f9264-133">ProtoBuf 2.5.0 — это [обязательный](https://github.com/yahoo/CaffeOnSpark/issues/87) элемент, но эта версия недоступна в виде пакета для Ubuntu 16. Поэтому ее нужно скомпилировать из исходного кода.</span><span class="sxs-lookup"><span data-stu-id="f9264-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need to compile it from the source code.</span></span> <span data-ttu-id="f9264-134">В Интернете также можно найти несколько ресурсов по компиляции этой версии, таких как [эта запись блога](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html).</span><span class="sxs-lookup"><span data-stu-id="f9264-134">There are also a few resources on the Internet on how to compile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="f9264-135">Чтобы приступить к работе, вы можете просто выполнить это действие скрипта в кластере для всех рабочих и головных узлов (для HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="f9264-135">To simply get started, you can just run this script action against your cluster to all the worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="f9264-136">Эти действия скрипта можно выполнить в работающем кластере или во время его подготовки.</span><span class="sxs-lookup"><span data-stu-id="f9264-136">You can either run the script actions for a running cluster, or you can also run the script actions during the cluster provision time.</span></span> <span data-ttu-id="f9264-137">Дополнительные сведения о действиях скрипта см. в [этой документации](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions).</span><span class="sxs-lookup"><span data-stu-id="f9264-137">For more details on the script actions, please see the documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Действия скриптов для установки зависимостей](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-the-head-node"></a><span data-ttu-id="f9264-139">Этап 2. Создание CaffeOnSpark для HDInsight на головном узле</span><span class="sxs-lookup"><span data-stu-id="f9264-139">Step 2: Build Caffe on Spark for HDInsight on the head node</span></span>

<span data-ttu-id="f9264-140">Второй этап заключается в создании Caffe на головном узле и развертывании скомпилированных библиотек на всех рабочих узлах.</span><span class="sxs-lookup"><span data-stu-id="f9264-140">The second step is to build Caffe on the headnode, and then distribute the compiled libraries to all the worker nodes.</span></span> <span data-ttu-id="f9264-141">На этом этапе вам потребуется [подключиться к головному узлу по протоколу SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), а затем просто выполнить [указания по созданию CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn). Ниже приведен скрипт, который позволяет создать CaffeOnSpark, но он подразумевает выполнение нескольких дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="f9264-141">In this step, you will need to [ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow the [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is the script you can use to build CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need to be updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want to update those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up the environment before building (especially when rebuiding), or there will be errors such as "failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #the build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put the already compiled CaffeOnSpark libraries to wasb storage, then read back to each node using script actions. This is because CaffeOnSpark requires all the nodes have the libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="f9264-142">Вам может потребоваться выполнить больше действий, чем описано в документации по CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="f9264-142">You may need to do more than what the documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="f9264-143">К этим дополнительным действиям относятся:</span><span class="sxs-lookup"><span data-stu-id="f9264-143">The changes are:</span></span>
- <span data-ttu-id="f9264-144">Переход к конфигурации ЦП и настройка использования библиотеки libatlas именно для этого.</span><span class="sxs-lookup"><span data-stu-id="f9264-144">Change to CPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="f9264-145">Отправка наборов данных в хранилище BLOB-объектов, которое находится в общем расположении, доступном для всех рабочих узлов (для последующего использования).</span><span class="sxs-lookup"><span data-stu-id="f9264-145">Put the datasets to the BLOB storage, which is a shared location that is accessible to all worker nodes for later use.</span></span>
- <span data-ttu-id="f9264-146">Отправка скомпилированных библиотек Caffe в хранилище BLOB-объектов и копирование этих библиотек во все узлы с помощью действий скриптов, чтобы сократить время компиляции.</span><span class="sxs-lookup"><span data-stu-id="f9264-146">Put the compiled Caffe libraries to BLOB storage, and later you will copy those libraries to all the nodes using script actions to avoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="f9264-147">Устранение неполадок, связанных с ошибкой An Ant BuildException has occured: exec returned: 2</span><span class="sxs-lookup"><span data-stu-id="f9264-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="f9264-148">При первом создании CaffeOnSpark может отобразиться следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="f9264-148">When first trying to build CaffeOnSpark, sometimes it will say</span></span>

    failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="f9264-149">Чтобы решить эту проблему, просто очистите репозиторий кода, используя команду make clean, а затем выполните команду make build (при условии, что вы установили правильные зависимости).</span><span class="sxs-lookup"><span data-stu-id="f9264-149">Simply clean the code repository by "make clean" and then run "make build" will solve this issue, as long as you have the correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="f9264-150">Устранение неполадок, связанных с ошибкой времени ожидания подключения к репозиторию Maven</span><span class="sxs-lookup"><span data-stu-id="f9264-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="f9264-151">Иногда при подключении к Maven возникает ошибка времени ожидания подключения, аналогичная представленной ниже.</span><span class="sxs-lookup"><span data-stu-id="f9264-151">Sometimes maven gives me the connection time out error, similar to below:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request to {s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="f9264-152">Подождите несколько минут, а затем просто перестройте код. Возможно, это связано с тем, что Maven каким-либо образом ограничивает трафик из указанного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f9264-152">It will be OK after waiting for a few minutes and then just try to rebuild the code, so it might be Maven somehow limits the traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="f9264-153">Устранение неполадок, связанных со сбоем тестирования Caffe</span><span class="sxs-lookup"><span data-stu-id="f9264-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="f9264-154">При выполнении окончательной проверки CaffeOnSpark может возникнуть ошибка тестирования, аналогичная представленной ниже.</span><span class="sxs-lookup"><span data-stu-id="f9264-154">You probably will see a test failure when doing the final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="f9264-155">Скорее всего, это связано с кодировкой UTF-8, но эта ошибка не влияет на использование Caffe.</span><span class="sxs-lookup"><span data-stu-id="f9264-155">This is prabably related with UTF-8 encoding, but should not impact the usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-the-required-libraries-to-all-the-worker-nodes"></a><span data-ttu-id="f9264-156">Этап 3. Развертывание необходимых библиотек на всех рабочих узлах.</span><span class="sxs-lookup"><span data-stu-id="f9264-156">Step 3: Distribute the required libraries to all the worker nodes</span></span>

<span data-ttu-id="f9264-157">Следующий этап заключается в развертывании библиотек (в основном они расположены в каталоге CaffeOnSpark/caffe-public/distribute/lib/ и CaffeOnSpark/caffe-distri/distribute/lib/) на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="f9264-157">The next step is to distribute the libraries (basically the libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) to all the nodes.</span></span> <span data-ttu-id="f9264-158">На этапе 2 мы поместили эти библиотеки в хранилище BLOB-объектов. Теперь с помощью действий скриптов это хранилище необходимо скопировать на все головные и рабочие узлы.</span><span class="sxs-lookup"><span data-stu-id="f9264-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions to copy it to all the head nodes and worker nodes.</span></span>

<span data-ttu-id="f9264-159">Для этого просто выполните действие скрипта, как показано ниже (укажите расположение в соответствии с используемым кластером).</span><span class="sxs-lookup"><span data-stu-id="f9264-159">To do this, simple run a script action as below (you need to point to the right location specific to your cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="f9264-160">На этапе 2 мы поместили это действие скрипта в хранилище BLOB-объектов, доступное для всех узлов, поэтому сейчас его нужно просто скопировать на все узлы.</span><span class="sxs-lookup"><span data-stu-id="f9264-160">Because in step 2, we put it on the BLOB storage which is accessible to all the nodes, in this step we just simply copy it to all the nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="f9264-161">Этап 4. Разработка модели и распределенный запуск Caffe</span><span class="sxs-lookup"><span data-stu-id="f9264-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="f9264-162">Выполнив описанные выше действия, вы установили Caffe на головном узле, и теперь мы можем продолжить.</span><span class="sxs-lookup"><span data-stu-id="f9264-162">After running the above steps, Caffe is alreay installed on the headnode and we are good to go.</span></span> <span data-ttu-id="f9264-163">Следующий этап заключается в написании модели Caffe.</span><span class="sxs-lookup"><span data-stu-id="f9264-163">The next step is to write a Caffe model.</span></span> 

<span data-ttu-id="f9264-164">Caffe использует "выразительную" архитектуру, где для разработки модели необходимо просто определить файл конфигурации, не выполняя работу с кодом (в большинстве случаев).</span><span class="sxs-lookup"><span data-stu-id="f9264-164">Caffe is using an "expressive architecture", where for composing a model, you just need to define a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="f9264-165">Давайте рассмотрим этот процесс более подробно.</span><span class="sxs-lookup"><span data-stu-id="f9264-165">So let's take a look there.</span></span> 

<span data-ttu-id="f9264-166">Сегодня мы обучим модель, которая является образцом модели для обучения MNIST.</span><span class="sxs-lookup"><span data-stu-id="f9264-166">The model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="f9264-167">База данных образцов рукописного написания цифр MNIST содержит 60 000 образцов наборов данных для обучения и тестовый набор из 10 000 образцов.</span><span class="sxs-lookup"><span data-stu-id="f9264-167">The MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="f9264-168">Это подмножество более широкого набора из базы данных NIST.</span><span class="sxs-lookup"><span data-stu-id="f9264-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="f9264-169">Цифры были нормализованы по размеру и расположены в центре изображения фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="f9264-169">The digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="f9264-170">CaffeOnSpark содержит некоторые скрипты, которые позволяют скачать набор данных и преобразовать его в правильный формат.</span><span class="sxs-lookup"><span data-stu-id="f9264-170">CaffeOnSpark has some scripts to download the dataset and convert it into the right format.</span></span>

<span data-ttu-id="f9264-171">Эта система предоставляет несколько образцов сетевых топологий для обучения MNIST.</span><span class="sxs-lookup"><span data-stu-id="f9264-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="f9264-172">Она предоставляет эффективную модель разбиения и оптимизации сетевой инфраструктуры (топология сети).</span><span class="sxs-lookup"><span data-stu-id="f9264-172">It has a nice design of splitting the network architecture (the topology of the network) and optimization.</span></span> <span data-ttu-id="f9264-173">В этом случае вам потребуется два указанных ниже файла.</span><span class="sxs-lookup"><span data-stu-id="f9264-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="f9264-174">Файл "алгоритма решения" (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) используется для отслеживания оптимизаций и создания обновлений параметров.</span><span class="sxs-lookup"><span data-stu-id="f9264-174">the "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing the optimization and generating parameter updates.</span></span> <span data-ttu-id="f9264-175">Например, он определяет, следует ли использовать ЦП или графический процессор, а также определяет динамику, число итераций и т. д. Кроме того, он определяет, какую топологию нейронных сетей должна использовать программа (в этом случае нам нужен второй файл).</span><span class="sxs-lookup"><span data-stu-id="f9264-175">For example, it defines whether CPU or GPU will be used, what's the momentum, how many iterations will be, etc. It also defines which neuron network topology should the program use (which is the second file we need).</span></span> <span data-ttu-id="f9264-176">Дополнительные сведения об алгоритме решения см. в [документации по Caffe](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="f9264-176">For more information about Solver, please refer to [Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="f9264-177">Так как мы используем ЦП, а не графический процессор, измените последнюю строку следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9264-177">For this example, since we are using CPU rather than GPU, we should change the last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Конфигурация Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="f9264-179">При необходимости вы можете изменить и другие строки.</span><span class="sxs-lookup"><span data-stu-id="f9264-179">You can change other lines as needed.</span></span>

<span data-ttu-id="f9264-180">Второй файл (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) определяет, как выглядит нейронная сеть, а также соответствующий входной и выходной файл.</span><span class="sxs-lookup"><span data-stu-id="f9264-180">The second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how the neuron network looks like, and the relevant input and output file.</span></span> <span data-ttu-id="f9264-181">Этот файл также необходимо обновить в соответствии с расположением данных для обучения.</span><span class="sxs-lookup"><span data-stu-id="f9264-181">We also need to update the file to reflect the training data location.</span></span> <span data-ttu-id="f9264-182">Измените в файле lenet_memory_train_test.prototxt следующие части (укажите расположение в соответствии с используемым кластером):</span><span class="sxs-lookup"><span data-stu-id="f9264-182">Change the following part in lenet_memory_train_test.prototxt (you need to point to the right location specific to your cluster):</span></span>

- <span data-ttu-id="f9264-183">Замените file:/Users/mridul/bigml/demodl/mnist_train_lmdb на wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb.</span><span class="sxs-lookup"><span data-stu-id="f9264-183">change the "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" to "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="f9264-184">Замените file:/Users/mridul/bigml/demodl/mnist_test_lmdb/ на wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb.</span><span class="sxs-lookup"><span data-stu-id="f9264-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" to "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Конфигурация Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="f9264-186">Дополнительные сведения об определении сети см. в [документации Caffe по использованию набора данных MNIST](http://caffe.berkeleyvision.org/gathered/examples/mnist.html).</span><span class="sxs-lookup"><span data-stu-id="f9264-186">For more information on how to define the network, please check the [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="f9264-187">В этом блоге мы используем простой образец данных MNIST.</span><span class="sxs-lookup"><span data-stu-id="f9264-187">For the purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="f9264-188">На головном узле выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f9264-188">You should run the command below from the head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="f9264-189">Эта команда отправляет необходимые файлы в каждый контейнер YARN (lenet_memory_solver.prototxt и lenet_memory_train_test.prototxt), а также задает соответствующий путь каждого драйвера или исполнителя Spark к LD_LIBRARY_PATH, который определен в предыдущем фрагменте кода, и указывает расположение, в котором сохранены библиотеки CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="f9264-189">Basically it distributes the required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) to each YARN container, and also set the relevant PATH of each Spark driver/executor to LD_LIBRARY_PATH, which is defined in the previous code snippet and points to the location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="f9264-190">Мониторинг и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f9264-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="f9264-191">Так как мы используем режим кластера YARN, время, когда драйвер Spark будет выполняться в случайном контейнере (и случайном рабочем узле), можно узнать, просто просмотрев выходные данные консоли примерно такого содержания:</span><span class="sxs-lookup"><span data-stu-id="f9264-191">Since we are using YARN cluster mode, in which case the Spark driver will be scheduled to an arbitrary container (and an arbitrary worker node) you should only see in the console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="f9264-192">Если вы хотите узнать, что произошло, просмотрите эти сведения в журнале драйвера Spark.</span><span class="sxs-lookup"><span data-stu-id="f9264-192">If you want to know what happened, you usually need to get the Spark driver's log, which has more information.</span></span> <span data-ttu-id="f9264-193">В этом случае, чтобы найти соответствующие журналы YARN, вам потребуется перейти к пользовательскому интерфейсу YARN.</span><span class="sxs-lookup"><span data-stu-id="f9264-193">In this case, you need to go to the YARN UI to find the relevant YARN logs.</span></span> <span data-ttu-id="f9264-194">Для этого перейдите по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="f9264-194">You can get the YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Пользовательский интерфейс YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="f9264-196">Здесь вы можете просмотреть сведения о количестве выделенных ресурсов для этого конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="f9264-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="f9264-197">Щелкнув ссылку "Планировщик", вы увидите, что для этого приложения запущено 9 контейнеров.</span><span class="sxs-lookup"><span data-stu-id="f9264-197">You can click the "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="f9264-198">Восемь из них используется в качестве исполнителей, а один для обработки драйвера.</span><span class="sxs-lookup"><span data-stu-id="f9264-198">We ask YARN to provide 8 executors, and another container is for driver process.</span></span> 

![Планировщик YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="f9264-200">При сбое можно проверить журналы драйвера или контейнера.</span><span class="sxs-lookup"><span data-stu-id="f9264-200">You may want to check the  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="f9264-201">Чтобы просмотреть журналы драйвера, в пользовательском интерфейсе YARN щелкните идентификатор приложения, а затем нажмите кнопку "Журналы".</span><span class="sxs-lookup"><span data-stu-id="f9264-201">For driver logs, you can click the application ID in YARN UI, then click the "Logs" button.</span></span> <span data-ttu-id="f9264-202">Журналы драйвера записываются в поток stderr.</span><span class="sxs-lookup"><span data-stu-id="f9264-202">The driver logs are written into stderr.</span></span>

![Пользовательский интерфейс YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="f9264-204">Например, в некоторых журналах вы можете увидеть указанные ниже сообщения об ошибках, указывающие на наличие слишком большого числа исполнителей.</span><span class="sxs-lookup"><span data-stu-id="f9264-204">For example, you might see some of the error below from the driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="f9264-205">Иногда проблемы возникают с исполнителями, а не с драйверами.</span><span class="sxs-lookup"><span data-stu-id="f9264-205">Sometimes, the issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="f9264-206">В этом случае необходимо проверить журналы контейнера.</span><span class="sxs-lookup"><span data-stu-id="f9264-206">In this case, you need to check the container logs.</span></span> <span data-ttu-id="f9264-207">Вы всегда можете получить журналы контейнера, чтобы определить контейнер со сбоем.</span><span class="sxs-lookup"><span data-stu-id="f9264-207">You can always get the container logs, and then get the failed container.</span></span> <span data-ttu-id="f9264-208">Например, этот сбой может произойти при запуске Caffe.</span><span class="sxs-lookup"><span data-stu-id="f9264-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="f9264-209">В этом случае необходимо получить идентификатор контейнера, в котором произошел сбой (в приведенном выше примере это container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="f9264-209">In this case, you need to get the failed container ID (in the above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="f9264-210">Затем на головном узле необходимо выполнить следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f9264-210">Then you need to run</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="f9264-211">Проверив сведения о сбое контейнера,</span><span class="sxs-lookup"><span data-stu-id="f9264-211">from the headnode.</span></span> <span data-ttu-id="f9264-212">вы определите, что он произошел из-за использования режима графического процессора в файле lenet_memory_solver.prototxt (вместо режима ЦП).</span><span class="sxs-lookup"><span data-stu-id="f9264-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written to STDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="f9264-213">Получение результатов</span><span class="sxs-lookup"><span data-stu-id="f9264-213">Getting results</span></span>

<span data-ttu-id="f9264-214">Так как мы выделяем 8 исполнителей и используем простую топологию сети, получение результатов занимает около 30 минут.</span><span class="sxs-lookup"><span data-stu-id="f9264-214">Since we are allocating 8 executors, and the network topology is simple, it should only take around 30 minutes to run the result.</span></span> <span data-ttu-id="f9264-215">В окне командной строки вы можете видеть, что мы поместили модель в папку wasb:///mnist.model, а результаты — в папку wasb:///mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="f9264-215">From the command line, you can see that we put the model to wasb:///mnist.model, and put the results to a folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="f9264-216">Чтобы получить результаты, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f9264-216">You can get the results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="f9264-217">Результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9264-217">and the result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="f9264-218">Параметр SampleID представляет идентификатор в наборе данных MNIST, а параметр label — это номер, определенный моделью.</span><span class="sxs-lookup"><span data-stu-id="f9264-218">The SampleID represents the ID in the MNIST dataset, and the label is the number that the model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="f9264-219">Заключение</span><span class="sxs-lookup"><span data-stu-id="f9264-219">Conclusion</span></span>

<span data-ttu-id="f9264-220">В этой статье представлены сведения об установке CaffeOnSpark с использованием простого образца данных.</span><span class="sxs-lookup"><span data-stu-id="f9264-220">In this documentation, you have tried to install CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="f9264-221">HDInsight — это полностью управляемая облачная распределенная вычислительная платформа, оптимизированная для выполнения рабочих нагрузок машинного обучения и расширенной аналитики с использованием большого набора данных, а также для выполнения заданий распределенного глубокого обучения с помощью Caffe в HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f9264-221">HDInsight is a full managed cloud distributed compute platform, and is the best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark to perform deep learning tasks.</span></span>


## <span data-ttu-id="f9264-222"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="f9264-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f9264-223">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9264-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f9264-224">Сценарии</span><span class="sxs-lookup"><span data-stu-id="f9264-224">Scenarios</span></span>
* [<span data-ttu-id="f9264-225">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="f9264-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f9264-226">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="f9264-226">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="f9264-227">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="f9264-227">Manage resources</span></span>
* [<span data-ttu-id="f9264-228">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9264-228">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

