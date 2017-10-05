---
title: "Использование Microsoft Cognitive Toolkit с Azure HDInsight Spark для глубокого обучения | Документация Майкрософт"
description: "Узнайте, как можно применить обученную модель обучения Microsoft Cognitive Toolkit к набору данных с помощью API Python для Spark в кластере Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: fafd738f782660b824732bab8cc3bec8405947e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="304e2-103">Использование модели глубокого обучения Microsoft Cognitive Toolkit в кластере Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="304e2-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="304e2-104">Ниже перечислены действия, которые вы выполните в этой статье.</span><span class="sxs-lookup"><span data-stu-id="304e2-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="304e2-105">Запуск пользовательского сценария для установки Microsoft Cognitive Toolkit в кластере Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="304e2-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="304e2-106">Передача Jupyter Notebook в кластер Spark для применения обученной модели глубокого обучения Microsoft Cognitive Toolkit к файлам в учетной записи хранилища BLOB-объектов Azure с помощью [API Python для Spark (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html).</span><span class="sxs-lookup"><span data-stu-id="304e2-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="304e2-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="304e2-107">Prerequisites</span></span>

* <span data-ttu-id="304e2-108">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="304e2-108">**An Azure subscription**.</span></span> <span data-ttu-id="304e2-109">Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="304e2-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="304e2-110">Ознакомьтесь со страницей [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="304e2-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="304e2-111">**Кластер Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="304e2-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="304e2-112">В этой статье создайте кластер Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="304e2-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="304e2-113">Инструкции см. в разделе [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="304e2-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="304e2-114">Каково предназначение этой последовательности решения?</span><span class="sxs-lookup"><span data-stu-id="304e2-114">How does this solution flow?</span></span>

<span data-ttu-id="304e2-115">Для описания этого решения используются данная статья и элемент Jupyter Notebook, переданный в рамках данного руководства.</span><span class="sxs-lookup"><span data-stu-id="304e2-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="304e2-116">Ниже перечислены действия, которые вы выполните в этой статье.</span><span class="sxs-lookup"><span data-stu-id="304e2-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="304e2-117">Запуск действия сценария в кластере HDInsight Spark для установки Microsoft Cognitive Toolkit и пакетов Python.</span><span class="sxs-lookup"><span data-stu-id="304e2-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="304e2-118">Передача элемента Jupyter Notebook, запускающего решение в кластере HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="304e2-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="304e2-119">Перечисленные ниже оставшиеся шаги приведены в описании Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="304e2-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="304e2-120">Загрузка примеров изображений в устойчивый распределенный набор данных Spark (RDD).</span><span class="sxs-lookup"><span data-stu-id="304e2-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="304e2-121">Загрузка модулей и определение предустановок.</span><span class="sxs-lookup"><span data-stu-id="304e2-121">Load modules and define presets</span></span>
   - <span data-ttu-id="304e2-122">Скачивание набора данных локально в кластер Spark.</span><span class="sxs-lookup"><span data-stu-id="304e2-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="304e2-123">Преобразование набора данных в RDD.</span><span class="sxs-lookup"><span data-stu-id="304e2-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="304e2-124">Оценка изображений с помощью обученной модели Cognitive Toolkit.</span><span class="sxs-lookup"><span data-stu-id="304e2-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="304e2-125">Скачивание обученной модели Cognitive Toolkit в кластер Spark.</span><span class="sxs-lookup"><span data-stu-id="304e2-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="304e2-126">Определение функций, используемых рабочими узлами.</span><span class="sxs-lookup"><span data-stu-id="304e2-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="304e2-127">Оценка изображений на рабочих узлах.</span><span class="sxs-lookup"><span data-stu-id="304e2-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="304e2-128">Анализ точности модели.</span><span class="sxs-lookup"><span data-stu-id="304e2-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="304e2-129">Установка Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="304e2-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="304e2-130">Microsoft Cognitive Toolkit в кластере Spark можно установить с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="304e2-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="304e2-131">Действие сценария использует пользовательские скрипты для установки компонентов в кластере, которые по умолчанию недоступны.</span><span class="sxs-lookup"><span data-stu-id="304e2-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="304e2-132">Можно использовать пользовательский сценарий с портала Azure, воспользовавшись пакетом SDK .NET для HDInsight или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="304e2-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="304e2-133">Этот сценарий можно также использовать для установки данного набора средств при создании кластера или после его подготовки и запуска.</span><span class="sxs-lookup"><span data-stu-id="304e2-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="304e2-134">В этой статье мы используем портал для установки набора средств после того, как кластер был создан.</span><span class="sxs-lookup"><span data-stu-id="304e2-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="304e2-135">Другие способы выполнения пользовательского сценария описаны в разделе [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="304e2-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="304e2-136">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="304e2-136">Using the Azure Portal</span></span>

<span data-ttu-id="304e2-137">Инструкции по использованию портала Azure для выполнения действия сценария см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="304e2-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="304e2-138">Обязательно укажите приведенные ниже данные для установки Microsoft Cognitive Toolkit.</span><span class="sxs-lookup"><span data-stu-id="304e2-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="304e2-139">Укажите значение имени действия сценария.</span><span class="sxs-lookup"><span data-stu-id="304e2-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="304e2-140">В поле **URI bash-скрипта** введите `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="304e2-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="304e2-141">Настройте выполнение сценария только на головном и рабочем узлах и снимите все остальные флажки.</span><span class="sxs-lookup"><span data-stu-id="304e2-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="304e2-142">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="304e2-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="304e2-143">Передача Jupyter Notebook в кластер Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="304e2-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="304e2-144">Чтобы использовать Microsoft Cognitive Toolkit с кластером Azure HDInsight Spark, необходимо загрузить Jupyter Notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** в кластер Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="304e2-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="304e2-145">Этот элемент Notebook можно найти на сайте GitHub: [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="304e2-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="304e2-146">Клонируйте репозиторий GitHub [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="304e2-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="304e2-147">Инструкции по клонированию приведены в разделе [Cloning a repository](https://help.github.com/articles/cloning-a-repository/) (Клонирование репозитория).</span><span class="sxs-lookup"><span data-stu-id="304e2-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="304e2-148">На портале Azure откройте колонку кластера Spark, который уже подготовлен, щелкните **Панель мониторинга кластера**, а затем щелкните **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="304e2-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="304e2-149">Можно также запустить Jupyter Notebook, перейдя по URL-адресу `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="304e2-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="304e2-150">Замените \<clustername> именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="304e2-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="304e2-151">В Jupyter Notebook нажмите кнопку **Upload** (Передать) в правом верхнем углу, а затем перейдите к расположению, в которое вы клонировали репозиторий GitHub.</span><span class="sxs-lookup"><span data-stu-id="304e2-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="304e2-152">![Передача Jupyter Notebook в кластер Azure HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span><span class="sxs-lookup"><span data-stu-id="304e2-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="304e2-153">Еще раз нажмите кнопку **Upload** (Передать).</span><span class="sxs-lookup"><span data-stu-id="304e2-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="304e2-154">После передачи элемента Notebook щелкните его имя, а затем следуйте отображаемым в Notebook указаниям по загрузке набора данных и выполните задания руководства.</span><span class="sxs-lookup"><span data-stu-id="304e2-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="304e2-155">См. также</span><span class="sxs-lookup"><span data-stu-id="304e2-155">See also</span></span>
* [<span data-ttu-id="304e2-156">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="304e2-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="304e2-157">Сценарии</span><span class="sxs-lookup"><span data-stu-id="304e2-157">Scenarios</span></span>
* [<span data-ttu-id="304e2-158">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="304e2-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="304e2-159">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="304e2-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="304e2-160">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="304e2-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="304e2-161">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="304e2-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="304e2-162">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="304e2-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="304e2-163">Analyze Application Insights telemetry logs with Spark on HDInsight (Анализ журналов телеметрии Application Insights с помощью Spark в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="304e2-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="304e2-164">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="304e2-164">Create and run applications</span></span>
* [<span data-ttu-id="304e2-165">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="304e2-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="304e2-166">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="304e2-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="304e2-167">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="304e2-167">Tools and extensions</span></span>
* [<span data-ttu-id="304e2-168">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="304e2-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="304e2-169">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="304e2-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="304e2-170">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="304e2-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="304e2-171">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="304e2-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="304e2-172">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="304e2-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="304e2-173">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="304e2-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="304e2-174">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="304e2-174">Manage resources</span></span>
* [<span data-ttu-id="304e2-175">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="304e2-175">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="304e2-176">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="304e2-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
