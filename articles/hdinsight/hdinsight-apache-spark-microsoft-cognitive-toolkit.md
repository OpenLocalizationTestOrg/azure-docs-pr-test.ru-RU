---
title: "aaaMicrosoft Когнитивных Toolkit с Azure HDInsight Spark для углубленного обучения | Документы Microsoft"
description: "Дополнительные сведения как обученной Когнитивных набор средств Майкрософт глубокой модели обучения может быть применен tooa набора данных, с помощью hello Spark Python API в кластере Azure HDInsight Spark."
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
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="df1a9-103">Использование модели глубокого обучения Microsoft Cognitive Toolkit в кластере Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="df1a9-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="df1a9-104">В этой статье hello следующие действия.</span><span class="sxs-lookup"><span data-stu-id="df1a9-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="df1a9-105">Выполнения пользовательского скрипта tooinstall Когнитивных набор средств Microsoft на кластере Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="df1a9-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="df1a9-106">Как отправить Jupyter записной книжки toohello Spark кластера toosee tooapply обученной Когнитивных набор средств Майкрософт глубокого изучения toofiles модели в учетной записи хранения BLOB-объектов Azure с помощью hello [API Spark Python (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="df1a9-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df1a9-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="df1a9-107">Prerequisites</span></span>

* <span data-ttu-id="df1a9-108">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="df1a9-108">**An Azure subscription**.</span></span> <span data-ttu-id="df1a9-109">Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="df1a9-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="df1a9-110">Ознакомьтесь со страницей [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="df1a9-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="df1a9-111">**Кластер Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="df1a9-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="df1a9-112">В этой статье создайте кластер Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="df1a9-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="df1a9-113">Инструкции см. в разделе [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="df1a9-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="df1a9-114">Каково предназначение этой последовательности решения?</span><span class="sxs-lookup"><span data-stu-id="df1a9-114">How does this solution flow?</span></span>

<span data-ttu-id="df1a9-115">Для описания этого решения используются данная статья и элемент Jupyter Notebook, переданный в рамках данного руководства.</span><span class="sxs-lookup"><span data-stu-id="df1a9-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="df1a9-116">В этой статье выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="df1a9-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="df1a9-117">Выполните действие сценария в кластере HDInsight Spark tooinstall пакетов Когнитивных набор средств Майкрософт и Python.</span><span class="sxs-lookup"><span data-stu-id="df1a9-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="df1a9-118">Отправьте книжке Jupyter hello, запускаемую toohello решения hello кластера HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="df1a9-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="df1a9-119">Hello следующие оставшиеся шаги описаны в записной книжке Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="df1a9-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="df1a9-120">Загрузка примеров изображений в устойчивый распределенный набор данных Spark (RDD).</span><span class="sxs-lookup"><span data-stu-id="df1a9-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="df1a9-121">Загрузка модулей и определение предустановок.</span><span class="sxs-lookup"><span data-stu-id="df1a9-121">Load modules and define presets</span></span>
   - <span data-ttu-id="df1a9-122">Скачать набор данных hello локально на кластере Spark hello</span><span class="sxs-lookup"><span data-stu-id="df1a9-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="df1a9-123">Преобразовать в RDD hello набора данных</span><span class="sxs-lookup"><span data-stu-id="df1a9-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="df1a9-124">Оценка hello изображения с помощью обученной модели Когнитивных Toolkit</span><span class="sxs-lookup"><span data-stu-id="df1a9-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="df1a9-125">Загрузите кластера Spark toohello модели Когнитивных Toolkit hello обучения</span><span class="sxs-lookup"><span data-stu-id="df1a9-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="df1a9-126">Определение функции toobe используемых рабочих узлов</span><span class="sxs-lookup"><span data-stu-id="df1a9-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="df1a9-127">Оценка hello изображений на рабочих узлов</span><span class="sxs-lookup"><span data-stu-id="df1a9-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="df1a9-128">Анализ точности модели.</span><span class="sxs-lookup"><span data-stu-id="df1a9-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="df1a9-129">Установка Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="df1a9-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="df1a9-130">Microsoft Cognitive Toolkit в кластере Spark можно установить с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="df1a9-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="df1a9-131">Действие сценария использует компоненты tooinstall пользовательские сценарии в кластере hello, которые недоступны по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="df1a9-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="df1a9-132">С помощью HDInsight .NET SDK, или с помощью Azure PowerShell можно использовать hello пользовательского скрипта из hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="df1a9-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="df1a9-133">Hello сценария tooinstall hello toolkit также можно использовать либо в процессе создания кластера или после hello кластера запущен и работает.</span><span class="sxs-lookup"><span data-stu-id="df1a9-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="df1a9-134">В этой статье мы используем toolkit hello портала tooinstall hello, после создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="df1a9-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="df1a9-135">Другие способы toorun hello пользовательского скрипта, в разделе [HDInsight настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="df1a9-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="df1a9-136">С помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="df1a9-136">Using hello Azure Portal</span></span>

<span data-ttu-id="df1a9-137">Как портал Azure toorun toouse hello записать действие в скрипт инструкции см. в разделе [HDInsight настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="df1a9-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="df1a9-138">Убедитесь, что предоставляют следующие входные данные tooinstall Когнитивных набор средств Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="df1a9-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="df1a9-139">Укажите значение для имени действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="df1a9-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="df1a9-140">В поле **URI bash-скрипта** введите `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="df1a9-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="df1a9-141">Убедитесь, что выполнение сценария hello только для hello head и рабочих узлов и снимите все hello остальные флажки.</span><span class="sxs-lookup"><span data-stu-id="df1a9-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="df1a9-142">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="df1a9-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="df1a9-143">Отправка tooAzure записной книжки Jupyter hello кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="df1a9-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="df1a9-144">hello toouse Когнитивных набор средств Microsoft с кластера Azure HDInsight Spark hello, необходимо загрузить hello книжке Jupyter **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello кластера Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="df1a9-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="df1a9-145">Этот элемент Notebook можно найти на сайте GitHub: [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="df1a9-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="df1a9-146">Репозитории GitHub клон hello [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="df1a9-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="df1a9-147">Tooclone инструкции в разделе [клонирование репозитория](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="df1a9-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="df1a9-148">Hello портал Azure, откройте колонку кластера Spark hello, которая уже подготовлена, щелкните **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="df1a9-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="df1a9-149">Можно также запустить книжке Jupyter hello, последовательно выбрав URL-адрес toohello `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="df1a9-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="df1a9-150">Замените \<имя_кластера > с именем hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df1a9-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="df1a9-151">Из записной книжки Jupyter hello, нажмите кнопку **отправить** в hello в правом верхнем углу, а затем toohello расположение, где клонировать репозиторий GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="df1a9-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="df1a9-152">![Отправка tooAzure записной книжки Jupyter кластера HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "tooAzure записной книжки Jupyter отправить кластера HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="df1a9-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="df1a9-153">Еще раз нажмите кнопку **Upload** (Передать).</span><span class="sxs-lookup"><span data-stu-id="df1a9-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="df1a9-154">После передачи записной книжки hello щелкните имя hello hello портативного компьютера и следуйте указаниям hello в записной книжке hello сам как tooload hello набора данных и выполнять учебника hello.</span><span class="sxs-lookup"><span data-stu-id="df1a9-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="df1a9-155">См. также</span><span class="sxs-lookup"><span data-stu-id="df1a9-155">See also</span></span>
* [<span data-ttu-id="df1a9-156">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="df1a9-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="df1a9-157">Сценарии</span><span class="sxs-lookup"><span data-stu-id="df1a9-157">Scenarios</span></span>
* [<span data-ttu-id="df1a9-158">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="df1a9-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="df1a9-159">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="df1a9-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="df1a9-160">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="df1a9-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="df1a9-161">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="df1a9-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="df1a9-162">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="df1a9-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="df1a9-163">Analyze Application Insights telemetry logs with Spark on HDInsight (Анализ журналов телеметрии Application Insights с помощью Spark в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="df1a9-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="df1a9-164">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="df1a9-164">Create and run applications</span></span>
* [<span data-ttu-id="df1a9-165">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="df1a9-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="df1a9-166">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="df1a9-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="df1a9-167">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="df1a9-167">Tools and extensions</span></span>
* [<span data-ttu-id="df1a9-168">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений</span><span class="sxs-lookup"><span data-stu-id="df1a9-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="df1a9-169">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="df1a9-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="df1a9-170">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="df1a9-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="df1a9-171">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="df1a9-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="df1a9-172">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="df1a9-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="df1a9-173">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="df1a9-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="df1a9-174">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="df1a9-174">Manage resources</span></span>
* [<span data-ttu-id="df1a9-175">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="df1a9-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="df1a9-176">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="df1a9-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
