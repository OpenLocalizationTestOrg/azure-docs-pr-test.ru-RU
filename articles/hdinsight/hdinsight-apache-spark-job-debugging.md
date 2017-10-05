---
title: "Отладка заданий Apache Spark в Azure HDInsight | Документация Майкрософт"
description: "Использование пользовательского интерфейса YARN, пользовательского интерфейса Spark и сервера журнала Spark для отслеживания и отладки заданий, запущенных в кластере Spark в Azure HDInsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="71abc-103">Отладка заданий Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="71abc-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="71abc-104">Из этой статьи вы узнаете, как выполнять отслеживание и отладку заданий Spark, запущенных в кластерах HDInsight, с помощью пользовательского интерфейса YARN, пользовательского интерфейса Spark и сервера журнала Spark.</span><span class="sxs-lookup"><span data-stu-id="71abc-104">In this article you will learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="71abc-105">Для статьи мы создадим задание Spark с помощью записной книжки, прилагающейся к кластеру Spark: **Машинное обучение. Прогнозный анализ на основе данных контроля качества пищевых продуктов**.</span><span class="sxs-lookup"><span data-stu-id="71abc-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="71abc-106">С помощью описанных ниже действий вы сможете отслеживать приложение, отправленное любым другим методом, например с помощью **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="71abc-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71abc-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="71abc-107">Prerequisites</span></span>
<span data-ttu-id="71abc-108">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="71abc-108">You must have the following:</span></span>

* <span data-ttu-id="71abc-109">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="71abc-109">An Azure subscription.</span></span> <span data-ttu-id="71abc-110">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="71abc-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="71abc-111">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="71abc-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="71abc-112">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="71abc-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="71abc-113">Для начала вам следует запустить записную книжку **[Машинное обучение. Прогнозный анализ на основе данных контроля качества пищевых продуктов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="71abc-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="71abc-114">Перейдите по ссылке, чтобы получить инструкции по запуску этой записной книжки.</span><span class="sxs-lookup"><span data-stu-id="71abc-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="71abc-115">Отслеживание приложения в пользовательском интерфейсе YARN</span><span class="sxs-lookup"><span data-stu-id="71abc-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="71abc-116">Запустите пользовательский интерфейс YARN.</span><span class="sxs-lookup"><span data-stu-id="71abc-116">Launch the YARN UI.</span></span> <span data-ttu-id="71abc-117">В колонке кластера щелкните **Панель мониторинга кластера**, а затем выберите пункт **YARN**.</span><span class="sxs-lookup"><span data-stu-id="71abc-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Запуск пользовательского интерфейса YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="71abc-119">Также пользовательский интерфейс YARN можно открыть из пользовательского интерфейса Ambari.</span><span class="sxs-lookup"><span data-stu-id="71abc-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="71abc-120">Чтобы открыть пользовательский интерфейс Ambari, выберите в колонке кластера **Панель мониторинга кластера**, а затем щелкните **Панель мониторинга кластера HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="71abc-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="71abc-121">В пользовательском интерфейсе Ambari щелкните **YARN**, затем — **Быстрые ссылки**. Щелкните активный менеджер ресурсов и нажмите кнопку **ResourceManager UI** (Пользовательский интерфейс диспетчера ресурсов).</span><span class="sxs-lookup"><span data-stu-id="71abc-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="71abc-122">Так как вы запустили задание Spark с помощью записных книжек Jupyter, приложение получило имя **remotesparkmagics** (это стандартное имя для всех приложений, запускаемых из записных книжек).</span><span class="sxs-lookup"><span data-stu-id="71abc-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="71abc-123">Нажмите идентификатор приложения рядом с именем приложения, чтобы посмотреть дополнительные сведения о задании.</span><span class="sxs-lookup"><span data-stu-id="71abc-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="71abc-124">Откроется представление приложения.</span><span class="sxs-lookup"><span data-stu-id="71abc-124">This launches the application view.</span></span>
   
    ![Поиск идентификатора приложения Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="71abc-126">Для приложений, которые запущены из записных книжек Jupyter, состояние всегда будет иметь значение **Запущено** , пока вы не выйдете из записной книжки.</span><span class="sxs-lookup"><span data-stu-id="71abc-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="71abc-127">Из представления приложения вы можете ознакомиться с подробными сведениями о контейнерах, связанных с приложением, а также изучить журналы (stdout и stderr).</span><span class="sxs-lookup"><span data-stu-id="71abc-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="71abc-128">Пользовательский интерфейс Spark можно запустить, щелкнув ссылку в графе **URL-адрес отслеживания**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="71abc-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![Скачивание журналов контейнера](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="71abc-130">Отслеживание приложения в пользовательском интерфейсе Spark</span><span class="sxs-lookup"><span data-stu-id="71abc-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="71abc-131">В пользовательском интерфейсе Spark вы можете подробно изучить задания Spark, которые создаются запущенным вами приложением.</span><span class="sxs-lookup"><span data-stu-id="71abc-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="71abc-132">Чтобы запустить пользовательский интерфейс Spark, щелкните ссылку **URL-адрес отслеживания**в представлении приложения, как показано на снимке экрана выше.</span><span class="sxs-lookup"><span data-stu-id="71abc-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="71abc-133">Здесь вы увидите все задания Spark, созданные приложением, которое запущено в записной книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="71abc-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![Просмотр заданий Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="71abc-135">Щелкните вкладку **Исполнители** , чтобы увидеть сведения о вычислениях и хранении для каждого исполнителя.</span><span class="sxs-lookup"><span data-stu-id="71abc-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="71abc-136">Также можно получить стек вызовов, щелкнув ссылку **Дамп потока** .</span><span class="sxs-lookup"><span data-stu-id="71abc-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![Просмотр исполнителей Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="71abc-138">Щелкните вкладку **Этапы** , чтобы просмотреть этапы, связанные с приложением.</span><span class="sxs-lookup"><span data-stu-id="71abc-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![Просмотр этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="71abc-140">Каждый этап может включать несколько задач. Вы можете просмотреть для них статистику выполнения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="71abc-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Просмотр этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="71abc-142">На странице сведений об этапе вы можете открыть визуализацию DAG.</span><span class="sxs-lookup"><span data-stu-id="71abc-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="71abc-143">Для этого разверните ссылку **Визуализация DAG** в верхней части страницы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="71abc-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![Просмотр этапов Spark в формате визуализации DAG](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="71abc-145">Направленный ациклический граф (DAG) представляет различные этапы в приложении.</span><span class="sxs-lookup"><span data-stu-id="71abc-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="71abc-146">Каждый синий блок графа соответствует определенной операции Spark, вызываемой из приложения.</span><span class="sxs-lookup"><span data-stu-id="71abc-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="71abc-147">На странице сведений об этапах можно также запустить представление временной шкалы для приложения.</span><span class="sxs-lookup"><span data-stu-id="71abc-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="71abc-148">Для этого разверните ссылку **Представление временной шкалы** в верхней части страницы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="71abc-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![Представление временной шкалы для этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="71abc-150">Здесь вы увидите события Spark в формате временной шкалы.</span><span class="sxs-lookup"><span data-stu-id="71abc-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="71abc-151">Это представление доступно на трех уровнях: для заданий, в пределах одного задания и в пределах этапа.</span><span class="sxs-lookup"><span data-stu-id="71abc-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="71abc-152">На рисунке выше представлен пример представления временной шкалы для одного этапа.</span><span class="sxs-lookup"><span data-stu-id="71abc-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="71abc-153">Если установить флажок **Изменять масштаб** , представление временной шкалы можно будет прокручивать влево и вправо.</span><span class="sxs-lookup"><span data-stu-id="71abc-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="71abc-154">Другие вкладки в пользовательском интерфейсе Spark содержат полезные сведения о самом экземпляре Spark.</span><span class="sxs-lookup"><span data-stu-id="71abc-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="71abc-155">Вкладка "Хранилище" — если приложение создает RDD, информацию о них вы найдете на этой вкладке.</span><span class="sxs-lookup"><span data-stu-id="71abc-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="71abc-156">Вкладка "Среда" — на этой вкладке есть много полезных сведений о вашем экземпляре Spark, например:</span><span class="sxs-lookup"><span data-stu-id="71abc-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="71abc-157">версия Scala;</span><span class="sxs-lookup"><span data-stu-id="71abc-157">Scala version</span></span>
     * <span data-ttu-id="71abc-158">каталог журнала событий, связанный с кластером;</span><span class="sxs-lookup"><span data-stu-id="71abc-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="71abc-159">число ядер исполнителя для приложения;</span><span class="sxs-lookup"><span data-stu-id="71abc-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="71abc-160">и т. д.</span><span class="sxs-lookup"><span data-stu-id="71abc-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="71abc-161">Поиск сведений о выполненных заданиях с помощью сервера журнала Spark</span><span class="sxs-lookup"><span data-stu-id="71abc-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="71abc-162">Когда задание завершается, сведения о нем сохраняются на сервере журнала Spark.</span><span class="sxs-lookup"><span data-stu-id="71abc-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="71abc-163">Чтобы открыть сервер журнала Spark, щелкните в колонке кластера **Панель мониторинга кластера**, а затем нажмите кнопку **Сервер журнала Spark**.</span><span class="sxs-lookup"><span data-stu-id="71abc-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Запуск сервера журнала Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="71abc-165">Также пользовательский интерфейс сервера журнала Spark можно открыть из пользовательского интерфейса Ambari.</span><span class="sxs-lookup"><span data-stu-id="71abc-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="71abc-166">Чтобы открыть пользовательский интерфейс Ambari, выберите в колонке кластера **Панель мониторинга кластера**, а затем щелкните **Панель мониторинга кластера HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="71abc-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="71abc-167">В пользовательском интерфейсе Ambari щелкните **Spark**, **Быстрые ссылки**, а затем — **Spark History Server UI** (Пользовательский интерфейс сервера журнала Spark).</span><span class="sxs-lookup"><span data-stu-id="71abc-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="71abc-168">Вы увидите здесь список всех завершенных приложений.</span><span class="sxs-lookup"><span data-stu-id="71abc-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="71abc-169">Выберите идентификатор приложения, чтобы открыть подробные сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="71abc-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Запуск сервера журнала Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="71abc-171">См. также</span><span class="sxs-lookup"><span data-stu-id="71abc-171">See also</span></span>
*  [<span data-ttu-id="71abc-172">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="71abc-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="71abc-173">Для специалистов по анализу данных</span><span class="sxs-lookup"><span data-stu-id="71abc-173">For data analysts</span></span>

* [<span data-ttu-id="71abc-174">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="71abc-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="71abc-175">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="71abc-175">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="71abc-176">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="71abc-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="71abc-177">Analyze Application Insights telemetry logs with Spark on HDInsight (Анализ журналов телеметрии Application Insights с помощью Spark в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="71abc-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="71abc-178">Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения</span><span class="sxs-lookup"><span data-stu-id="71abc-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="71abc-179">Для разработчиков Spark</span><span class="sxs-lookup"><span data-stu-id="71abc-179">For Spark developers</span></span>

* [<span data-ttu-id="71abc-180">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="71abc-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="71abc-181">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="71abc-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="71abc-182">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="71abc-182">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="71abc-183">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="71abc-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="71abc-184">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="71abc-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="71abc-185">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="71abc-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="71abc-186">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="71abc-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="71abc-187">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="71abc-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="71abc-188">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="71abc-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


