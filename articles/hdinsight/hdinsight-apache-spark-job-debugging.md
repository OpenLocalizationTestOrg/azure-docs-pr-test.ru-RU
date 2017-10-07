---
title: "aaaDebug Apache Spark задания, выполняющиеся на Azure HDInsight | Документы Microsoft"
description: "Используйте YARN пользовательского интерфейса, Spark пользовательского интерфейса и Spark журнал сервера tootrack и отладка задания на кластере Spark в Azure HDInsight"
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
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="5ff04-103">Отладка заданий Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ff04-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="5ff04-104">В этой статье вы узнаете, как tootrack и отладки Поместите здесь заданий, работающих в кластерах HDInsight с помощью hello YARN пользовательского интерфейса, Spark пользовательского интерфейса и hello Spark журнала сервера.</span><span class="sxs-lookup"><span data-stu-id="5ff04-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="5ff04-105">В этой статье мы запустит задание Spark использование записной книжке доступен с кластера Spark hello, **машинное обучение: прогнозирующей аналитики на данные проверки пищевых продуктов с помощью MLLib**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="5ff04-106">Можно использовать следующие tootrack приложение, которое можно отправлять с помощью любого другого подхода, например, действия hello **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ff04-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ff04-107">Prerequisites</span></span>
<span data-ttu-id="5ff04-108">Необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-108">You must have hello following:</span></span>

* <span data-ttu-id="5ff04-109">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff04-109">An Azure subscription.</span></span> <span data-ttu-id="5ff04-110">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5ff04-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5ff04-111">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ff04-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="5ff04-112">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5ff04-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="5ff04-113">Вы должны начали работает hello,  **[машинное обучение: прогнозирующей аналитики на данные проверки пищевых продуктов с помощью MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="5ff04-114">Дополнительные сведения о toorun блокнота, выполните hello ссылку.</span><span class="sxs-lookup"><span data-stu-id="5ff04-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="5ff04-115">Отслеживать приложение hello YARN пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="5ff04-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="5ff04-116">Запустите hello YARN пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5ff04-116">Launch hello YARN UI.</span></span> <span data-ttu-id="5ff04-117">Из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **YARN**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Запуск пользовательского интерфейса YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="5ff04-119">Кроме того вы можете запустить hello YARN пользовательского интерфейса из hello Ambari пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5ff04-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="5ff04-120">hello toolaunch Ambari пользовательского интерфейса, из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **мониторинга кластера HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="5ff04-121">Hello Ambari пользовательского интерфейса, выберите **YARN**, нажмите кнопку **быстрые ссылки**, щелкните Диспетчер ресурсов active hello и нажмите кнопку **пользовательского интерфейса диспетчера ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="5ff04-122">Так как вы начали hello Spark задания с помощью записные книжки Jupyter, приложение hello имеет имя hello **remotesparkmagics** (это имя hello для всех приложений, запускаемых из записных книжек hello).</span><span class="sxs-lookup"><span data-stu-id="5ff04-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="5ff04-123">Дополнительные сведения о задании приветствия нажмите кнопку идентификатора приложения hello с tooget имя приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="5ff04-124">Откроется представление приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-124">This launches hello application view.</span></span>
   
    ![Поиск идентификатора приложения Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="5ff04-126">Для таких приложений, запускаемых из записные книжки Jupyter hello, всегда имеет состояние hello **под УПРАВЛЕНИЕМ** до выхода из записной книжки hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="5ff04-127">Из представления приложения hello можно выполнить детализацию дальнейшей toofind out hello контейнеров, связанных с приложение hello и журналы hello (stdout и stderr).</span><span class="sxs-lookup"><span data-stu-id="5ff04-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="5ff04-128">Можно также запустить hello Spark пользовательского интерфейса, нажав кнопку hello связывания соответствующий toohello **URL-адрес отслеживания**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5ff04-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![Скачивание журналов контейнера](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="5ff04-130">Отслеживать приложение hello Spark пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="5ff04-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="5ff04-131">В hello Spark пользовательского интерфейса можно детализировать hello Spark заданий, порождаемых hello приложения, который был запущен ранее.</span><span class="sxs-lookup"><span data-stu-id="5ff04-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="5ff04-132">hello toolaunch Spark пользовательского интерфейса, из представления приложения hello, щелкните ссылку hello от hello **URL-адрес отслеживания**, как показано выше снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="5ff04-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="5ff04-133">Можно просмотреть все задания Spark hello, которые загружаются hello приложение, работающее в записной книжке Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Просмотр заданий Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="5ff04-135">Нажмите кнопку hello **исполнителей** вкладке toosee обработки и хранения информации для каждого исполнителя.</span><span class="sxs-lookup"><span data-stu-id="5ff04-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="5ff04-136">Стек вызовов hello также можно получить, щелкнув hello **потоков дампа** ссылку.</span><span class="sxs-lookup"><span data-stu-id="5ff04-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Просмотр исполнителей Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="5ff04-138">Нажмите кнопку hello **этапы** вкладке toosee этапы hello, связанных с приложением hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Просмотр этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="5ff04-140">Каждый этап может включать несколько задач. Вы можете просмотреть для них статистику выполнения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5ff04-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Просмотр этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="5ff04-142">На странице сведений о рабочей области hello вы можете запустить DAG визуализации.</span><span class="sxs-lookup"><span data-stu-id="5ff04-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="5ff04-143">Разверните hello **визуализации DAG** ссылку вверху hello страницы приветствия, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5ff04-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Просмотр этапов Spark в формате визуализации DAG](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="5ff04-145">DAG или прямой Aclyic граф представляет различные этапы hello в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="5ff04-146">Каждый прямоугольник blue hello диаграмме представляет Spark операции, вызываемые из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="5ff04-147">На странице сведений о рабочей области hello также можно запустить просмотр временная шкала приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="5ff04-148">Разверните hello **временной шкалы событий** ссылку вверху hello страницы приветствия, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5ff04-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Представление временной шкалы для этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="5ff04-150">Этот монитор отображает события Spark hello в виде hello временной шкалы.</span><span class="sxs-lookup"><span data-stu-id="5ff04-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="5ff04-151">представление временной шкалы Hello доступно три уровня для заданий в задании и в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="5ff04-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="5ff04-152">выше рисунке Hello захватывает hello представлении временной шкалы для данного этапа.</span><span class="sxs-lookup"><span data-stu-id="5ff04-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="5ff04-153">При выборе hello **изменять масштаб** флажок, таблицу можно прокрутить влево и вправо в представлении временной шкалы hello.</span><span class="sxs-lookup"><span data-stu-id="5ff04-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="5ff04-154">Другие вкладки в hello Spark пользовательского интерфейса предоставляют полезные сведения об экземпляре Spark hello также.</span><span class="sxs-lookup"><span data-stu-id="5ff04-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="5ff04-155">Вкладка «хранилище» — Если приложение создает RDDs можно найти сведения о заданиях в вкладка hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="5ff04-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="5ff04-156">Вкладка «среда» — на этой вкладке содержится много полезных сведений о данном экземпляре Spark, например hello</span><span class="sxs-lookup"><span data-stu-id="5ff04-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="5ff04-157">версия Scala;</span><span class="sxs-lookup"><span data-stu-id="5ff04-157">Scala version</span></span>
     * <span data-ttu-id="5ff04-158">Каталог журнала событий, связанный с hello кластера</span><span class="sxs-lookup"><span data-stu-id="5ff04-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="5ff04-159">Число ядер исполнителя для приложения hello</span><span class="sxs-lookup"><span data-stu-id="5ff04-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="5ff04-160">и т. д.</span><span class="sxs-lookup"><span data-stu-id="5ff04-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="5ff04-161">Найти сведения о выполненных заданиях с помощью hello Spark журнала сервера</span><span class="sxs-lookup"><span data-stu-id="5ff04-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="5ff04-162">После завершения задания hello сведения о задании hello сохраняются в hello Spark журнала сервера.</span><span class="sxs-lookup"><span data-stu-id="5ff04-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="5ff04-163">toolaunch hello Server журнал Spark, из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **Spark журнала сервера**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Запуск сервера журнала Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="5ff04-165">Кроме того вы можете запустить hello пользовательский Интерфейс сервера Spark журнала из hello Ambari пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5ff04-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="5ff04-166">hello toolaunch Ambari пользовательского интерфейса, из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **мониторинга кластера HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="5ff04-167">Hello Ambari пользовательского интерфейса, выберите **Spark**, нажмите кнопку **быстрые ссылки**и нажмите кнопку **пользовательский Интерфейс сервера журнал Spark**.</span><span class="sxs-lookup"><span data-stu-id="5ff04-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="5ff04-168">Вы увидите все перечисленные приложения hello завершена.</span><span class="sxs-lookup"><span data-stu-id="5ff04-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="5ff04-169">Щелкните идентификатор приложения toodrill вниз в приложение Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="5ff04-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Запуск сервера журнала Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="5ff04-171">См. также</span><span class="sxs-lookup"><span data-stu-id="5ff04-171">See also</span></span>
*  [<span data-ttu-id="5ff04-172">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ff04-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="5ff04-173">Для специалистов по анализу данных</span><span class="sxs-lookup"><span data-stu-id="5ff04-173">For data analysts</span></span>

* [<span data-ttu-id="5ff04-174">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="5ff04-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5ff04-175">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="5ff04-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5ff04-176">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ff04-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="5ff04-177">Analyze Application Insights telemetry logs with Spark on HDInsight (Анализ журналов телеметрии Application Insights с помощью Spark в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="5ff04-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="5ff04-178">Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения</span><span class="sxs-lookup"><span data-stu-id="5ff04-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="5ff04-179">Для разработчиков Spark</span><span class="sxs-lookup"><span data-stu-id="5ff04-179">For Spark developers</span></span>

* [<span data-ttu-id="5ff04-180">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="5ff04-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5ff04-181">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="5ff04-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="5ff04-182">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений</span><span class="sxs-lookup"><span data-stu-id="5ff04-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5ff04-183">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="5ff04-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="5ff04-184">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5ff04-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5ff04-185">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ff04-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5ff04-186">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ff04-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5ff04-187">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="5ff04-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5ff04-188">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="5ff04-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


