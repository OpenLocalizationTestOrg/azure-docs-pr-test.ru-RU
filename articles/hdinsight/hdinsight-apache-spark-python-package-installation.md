---
title: "Действие aaaScript — пакеты установки Python с Jupyter на Azure HDInsight | Документы Microsoft"
description: "Пошаговые инструкции по как toouse сценария действия tooconfigure Jupyter портативные компьютеры с HDInsight Spark кластеры пакеты toouse внешних python."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="97cf3-103">Используйте действие сценария tooinstall внешние пакеты Python для записные книжки Jupyter в кластерах Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cf3-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97cf3-104">Использование волшебных команд</span><span class="sxs-lookup"><span data-stu-id="97cf3-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="97cf3-105">Использование действия сценария</span><span class="sxs-lookup"><span data-stu-id="97cf3-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="97cf3-106">Узнайте, как tooconfigure toouse действия скрипта кластера с Apache Spark на HDInsight (Linux) toouse внешних, сообществом **python** пакеты, которые не включены out of box в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="97cf3-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="97cf3-107">Можно также настроить с помощью записной книжке Jupyter `%%configure` магическая toouse внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="97cf3-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="97cf3-108">Дополнительные сведения см. в статье [Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="97cf3-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="97cf3-109">Можно выполнить поиск hello [индекса пакета](https://pypi.python.org/pypi) для hello полного списка доступных пакетов.</span><span class="sxs-lookup"><span data-stu-id="97cf3-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="97cf3-110">Его также можно получить из других источников.</span><span class="sxs-lookup"><span data-stu-id="97cf3-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="97cf3-111">Например, можно установить пакеты, предоставляемые посредством [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) или [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="97cf3-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="97cf3-112">В этой статье вы узнаете, как tooinstall hello [TensorFlow](https://www.tensorflow.org/) пакета с помощью сценария Actoin в кластере и использовать его с помощью книжке Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="97cf3-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97cf3-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="97cf3-113">Prerequisites</span></span>
<span data-ttu-id="97cf3-114">Необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="97cf3-114">You must have hello following:</span></span>

* <span data-ttu-id="97cf3-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="97cf3-115">An Azure subscription.</span></span> <span data-ttu-id="97cf3-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="97cf3-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="97cf3-117">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97cf3-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="97cf3-118">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="97cf3-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="97cf3-119">Если у вас еще нет кластера Spark в HDInsight на платформе Linux, можно выполнить действия сценария во время его создания.</span><span class="sxs-lookup"><span data-stu-id="97cf3-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="97cf3-120">Обратитесь к документации hello на [как toouse пользовательского скрипта действия](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="97cf3-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="97cf3-121">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="97cf3-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="97cf3-122">Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели).</span><span class="sxs-lookup"><span data-stu-id="97cf3-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="97cf3-123">Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="97cf3-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="97cf3-124">Из колонки кластера Spark hello, нажмите кнопку **действия скрипта** под **использование**.</span><span class="sxs-lookup"><span data-stu-id="97cf3-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="97cf3-125">Выполните пользовательское действие hello, устанавливающий TensorFlow в hello головного узла и hello рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="97cf3-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="97cf3-126">Hello bash сценария можно ссылаться из: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh посещение hello документацию по [как toouse пользовательского скрипта действия](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="97cf3-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="97cf3-127">Существует два python установок в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="97cf3-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="97cf3-128">Spark будет использовать установки python hello Anaconda, расположенный в `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="97cf3-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="97cf3-129">Укажите его в настраиваемых действиях с помощью `/usr/bin/anaconda/bin/pip` и `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="97cf3-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="97cf3-130">Открытие Jupyter Notebook PySpark</span><span class="sxs-lookup"><span data-stu-id="97cf3-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="97cf3-131">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="97cf3-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="97cf3-132">Создается и открывается с именем hello Untitled.pynb новый блокнот.</span><span class="sxs-lookup"><span data-stu-id="97cf3-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="97cf3-133">Щелкните имя записной книжки hello вверху hello и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="97cf3-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="97cf3-134">![Введите имя для ноутбука hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "укажите имя для ноутбука hello")</span><span class="sxs-lookup"><span data-stu-id="97cf3-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="97cf3-135">Теперь будет выполнена команда `import tensorflow` и запущен пример hello world.</span><span class="sxs-lookup"><span data-stu-id="97cf3-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="97cf3-136">Toocopy кода:</span><span class="sxs-lookup"><span data-stu-id="97cf3-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="97cf3-137">Hello результат будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="97cf3-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="97cf3-138">![Выполнение кода TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Выполнение кода TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="97cf3-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="97cf3-139"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="97cf3-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="97cf3-140">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cf3-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="97cf3-141">Сценарии</span><span class="sxs-lookup"><span data-stu-id="97cf3-141">Scenarios</span></span>
* [<span data-ttu-id="97cf3-142">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="97cf3-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="97cf3-143">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="97cf3-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="97cf3-144">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="97cf3-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="97cf3-145">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="97cf3-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="97cf3-146">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cf3-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="97cf3-147">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="97cf3-147">Create and run applications</span></span>
* [<span data-ttu-id="97cf3-148">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="97cf3-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="97cf3-149">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="97cf3-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="97cf3-150">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="97cf3-150">Tools and extensions</span></span>
* [<span data-ttu-id="97cf3-151">Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cf3-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="97cf3-152">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений</span><span class="sxs-lookup"><span data-stu-id="97cf3-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="97cf3-153">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="97cf3-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="97cf3-154">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cf3-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="97cf3-155">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cf3-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="97cf3-156">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="97cf3-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="97cf3-157">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="97cf3-157">Manage resources</span></span>
* [<span data-ttu-id="97cf3-158">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cf3-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="97cf3-159">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="97cf3-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
