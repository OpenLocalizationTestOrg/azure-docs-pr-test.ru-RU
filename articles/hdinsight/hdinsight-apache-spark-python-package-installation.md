---
title: "Действие скрипта: установка пакетов Python с Jupyter в Azure HDInsight | Документация Майкрософт"
description: "Пошаговые инструкции по использованию действия скрипта для настройки записных книжек Jupyter с кластерами Spark HDInsight для использования внешних пакетов Python."
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
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="93d35-103">Использование действия сценария для установки внешних пакетов Python для записных книжек Jupyter в кластерах Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="93d35-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93d35-104">Использование волшебных команд</span><span class="sxs-lookup"><span data-stu-id="93d35-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="93d35-105">Использование действия сценария</span><span class="sxs-lookup"><span data-stu-id="93d35-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="93d35-106">Узнайте, как с помощью действий сценария настроить кластер Apache Spark в HDInsight (Linux) для использования внешних, предоставленных сообществом пакетов **Python**, которые не включены в готовую версию кластера.</span><span class="sxs-lookup"><span data-stu-id="93d35-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="93d35-107">Можно также настроить записную книжку Jupyter с помощью волшебной команды `%%configure`, чтобы использовать внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="93d35-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="93d35-108">Дополнительные сведения см. в статье [Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="93d35-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="93d35-109">Полный список доступных пакетов можно найти в [указателе пакетов](https://pypi.python.org/pypi).</span><span class="sxs-lookup"><span data-stu-id="93d35-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="93d35-110">Его также можно получить из других источников.</span><span class="sxs-lookup"><span data-stu-id="93d35-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="93d35-111">Например, можно установить пакеты, предоставляемые посредством [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) или [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="93d35-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="93d35-112">В этой статье вы узнаете, как установить в кластере пакет [TensorFlow](https://www.tensorflow.org/) с помощью действия сценария и использовать его посредством Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="93d35-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93d35-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="93d35-113">Prerequisites</span></span>
<span data-ttu-id="93d35-114">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="93d35-114">You must have the following:</span></span>

* <span data-ttu-id="93d35-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="93d35-115">An Azure subscription.</span></span> <span data-ttu-id="93d35-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="93d35-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="93d35-117">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="93d35-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="93d35-118">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="93d35-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="93d35-119">Если у вас еще нет кластера Spark в HDInsight на платформе Linux, можно выполнить действия сценария во время его создания.</span><span class="sxs-lookup"><span data-stu-id="93d35-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="93d35-120">Обратитесь к документации по [использованию настраиваемых действий сценария](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="93d35-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="93d35-121">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="93d35-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="93d35-122">На начальной панели [портала Azure](https://portal.azure.com/)щелкните элемент кластера Spark (если он закреплен на начальной панели).</span><span class="sxs-lookup"><span data-stu-id="93d35-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="93d35-123">Кроме того, вы можете перейти к кластеру, последовательно щелкнув **Просмотреть все** > **Кластеры HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="93d35-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="93d35-124">В колонке кластера Spark щелкните **Действия скрипта** в разделе **Использование**.</span><span class="sxs-lookup"><span data-stu-id="93d35-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="93d35-125">Выполните настраиваемое действие, устанавливающее TensorFlow на головные узлы и рабочие узлы.</span><span class="sxs-lookup"><span data-stu-id="93d35-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="93d35-126">Сценарий bash может быть основан на https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh. Обратитесь к документации по [использованию настраиваемых действий сценария](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="93d35-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="93d35-127">В кластере имеются два установленных компонента Python.</span><span class="sxs-lookup"><span data-stu-id="93d35-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="93d35-128">Spark будет использовать компонент Python Anaconda, расположенный в `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="93d35-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="93d35-129">Укажите его в настраиваемых действиях с помощью `/usr/bin/anaconda/bin/pip` и `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="93d35-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="93d35-130">Открытие Jupyter Notebook PySpark</span><span class="sxs-lookup"><span data-stu-id="93d35-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="93d35-131">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="93d35-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="93d35-132">Будет создана и открыта записная книжка с именем Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="93d35-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="93d35-133">Щелкните имя записной книжки в верхней части страницы сверху и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="93d35-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="93d35-134">![Указание имени для записной книжки](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Указание имени для записной книжки")</span><span class="sxs-lookup"><span data-stu-id="93d35-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="93d35-135">Теперь будет выполнена команда `import tensorflow` и запущен пример hello world.</span><span class="sxs-lookup"><span data-stu-id="93d35-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="93d35-136">Следует скопировать приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="93d35-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="93d35-137">Результат должен выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="93d35-137">The result will look like this:</span></span>
    
    <span data-ttu-id="93d35-138">![Выполнение кода TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Выполнение кода TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="93d35-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="93d35-139"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="93d35-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="93d35-140">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="93d35-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="93d35-141">Сценарии</span><span class="sxs-lookup"><span data-stu-id="93d35-141">Scenarios</span></span>
* [<span data-ttu-id="93d35-142">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="93d35-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="93d35-143">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="93d35-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="93d35-144">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="93d35-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="93d35-145">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="93d35-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="93d35-146">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="93d35-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="93d35-147">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="93d35-147">Create and run applications</span></span>
* [<span data-ttu-id="93d35-148">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="93d35-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="93d35-149">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="93d35-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="93d35-150">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="93d35-150">Tools and extensions</span></span>
* [<span data-ttu-id="93d35-151">Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="93d35-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="93d35-152">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="93d35-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="93d35-153">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="93d35-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="93d35-154">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="93d35-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="93d35-155">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="93d35-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="93d35-156">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="93d35-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="93d35-157">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="93d35-157">Manage resources</span></span>
* [<span data-ttu-id="93d35-158">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="93d35-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="93d35-159">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="93d35-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
