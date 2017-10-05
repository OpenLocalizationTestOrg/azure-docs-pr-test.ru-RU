---
title: "Использование представления Ambari Tez в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как использовать представление Ambari Tez для отладки заданий Tez в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="402e4-103">Отладка заданий Tez в HDInsight с помощью представлений Ambari </span><span class="sxs-lookup"><span data-stu-id="402e4-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="402e4-104">Пользовательский веб-интерфейс Ambari для HDInsight содержит представление Tez, которое можно использовать для получения общих сведений о заданиях и отладки заданий, применяющих Tez.</span><span class="sxs-lookup"><span data-stu-id="402e4-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="402e4-105">Представление Tez позволяет визуализировать задание в виде схемы связанных элементов, выполнять детализацию каждого элемента и получать статистические данные и данные журнала.</span><span class="sxs-lookup"><span data-stu-id="402e4-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="402e4-106">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="402e4-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="402e4-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="402e4-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="402e4-108">Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md#hdinsight-windows-retirement)</span><span class="sxs-lookup"><span data-stu-id="402e4-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="402e4-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="402e4-109">Prerequisites</span></span>

* <span data-ttu-id="402e4-110">Кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="402e4-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="402e4-111">Инструкции по созданию кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="402e4-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="402e4-112">Современный веб-браузер, который поддерживает HTML5.</span><span class="sxs-lookup"><span data-stu-id="402e4-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="402e4-113">Общие сведения о Tez</span><span class="sxs-lookup"><span data-stu-id="402e4-113">Understanding Tez</span></span>

<span data-ttu-id="402e4-114">Tez — это расширяемая платформа для обработки данных в Hadoop, которая характеризуется более высокими скоростями по сравнению с традиционной обработкой MapReduce.</span><span class="sxs-lookup"><span data-stu-id="402e4-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="402e4-115">Она является подсистемой по умолчанию для Hive для кластеров HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="402e4-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="402e4-116">Tez создает направленный ациклический граф (DAG), описывающий порядок действий, необходимых для заданий.</span><span class="sxs-lookup"><span data-stu-id="402e4-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="402e4-117">Отдельные действия называются вершинами и выполняют часть всего задания.</span><span class="sxs-lookup"><span data-stu-id="402e4-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="402e4-118">Фактическое выполнение работы, описываемое вершиной, называется задачей и может быть распределено среди нескольких узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="402e4-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="402e4-119">Общие сведения о представлении Tez </span><span class="sxs-lookup"><span data-stu-id="402e4-119">Understanding the Tez view</span></span>

<span data-ttu-id="402e4-120">В представлении Tez содержатся накопленные сведения и данные о процессах, которые выполняются.</span><span class="sxs-lookup"><span data-stu-id="402e4-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="402e4-121">Здесь можно просмотреть, как задание распределяется по кластерам.</span><span class="sxs-lookup"><span data-stu-id="402e4-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="402e4-122">А также здесь отображаются счетчики, используемые задачами и вершинами, и сведения об ошибках, относящихся к заданию.</span><span class="sxs-lookup"><span data-stu-id="402e4-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="402e4-123">Отображаемые сведения могут быть полезными в следующих сценариях.</span><span class="sxs-lookup"><span data-stu-id="402e4-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="402e4-124">Мониторинг длительных процессов, просмотр хода выполнения задач map и reduce.</span><span class="sxs-lookup"><span data-stu-id="402e4-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="402e4-125">Анализ исторических данных успешных или неудачных процессов для получения сведений о причинах сбоев и возможностях улучшения обработки.</span><span class="sxs-lookup"><span data-stu-id="402e4-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="402e4-126">Создание DAG</span><span class="sxs-lookup"><span data-stu-id="402e4-126">Generate a DAG</span></span>

<span data-ttu-id="402e4-127">Представление Tez содержит данные только в том случае, если задание, которое использует подсистему Tez, выполняется в данный момент или было выполнено ранее.</span><span class="sxs-lookup"><span data-stu-id="402e4-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="402e4-128">Простые запросы Hive можно разрешить без использования Tez.</span><span class="sxs-lookup"><span data-stu-id="402e4-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="402e4-129">Подсистема Tez требуется для работы с более сложными запросами, которые выполняют фильтрацию, группировку,</span><span class="sxs-lookup"><span data-stu-id="402e4-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="402e4-130">упорядочение, соединения и т. д.</span><span class="sxs-lookup"><span data-stu-id="402e4-130">use the Tez engine.</span></span>

<span data-ttu-id="402e4-131">Приведенные ниже действия предназначены для запуска запроса Hive, использующего Tez.</span><span class="sxs-lookup"><span data-stu-id="402e4-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="402e4-132">В веб-браузере перейдите на страницу с адресом https://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="402e4-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="402e4-133">В меню в верхней части страницы щелкните значок **Представления**.</span><span class="sxs-lookup"><span data-stu-id="402e4-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="402e4-134">Он выглядит как набор квадратов.</span><span class="sxs-lookup"><span data-stu-id="402e4-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="402e4-135">В появившемся раскрывающемся списке выберите **Представление Hive**.</span><span class="sxs-lookup"><span data-stu-id="402e4-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Выбор представления Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="402e4-137">После загрузки представления Hive вставьте следующий запрос в редактор запросов и нажмите кнопку **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="402e4-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="402e4-138">После завершения задания выходные данные должны отображаться в разделе **Query Process Results** (Результаты обработки запроса).</span><span class="sxs-lookup"><span data-stu-id="402e4-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="402e4-139">Результаты должны иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="402e4-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="402e4-140">Откройте вкладку **Журнал**.</span><span class="sxs-lookup"><span data-stu-id="402e4-140">Select the **Log** tab.</span></span> <span data-ttu-id="402e4-141">Отобразятся сведения, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="402e4-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="402e4-142">Сохраните значение поля **ИД приложения**, так как оно будет использоваться в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="402e4-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="402e4-143">Использование представления Tez</span><span class="sxs-lookup"><span data-stu-id="402e4-143">Use the Tez View</span></span>

1. <span data-ttu-id="402e4-144">В меню в верхней части страницы щелкните значок **Представления**.</span><span class="sxs-lookup"><span data-stu-id="402e4-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="402e4-145">В появившемся раскрывающемся списке выберите **Tez view** (Представление Tez).</span><span class="sxs-lookup"><span data-stu-id="402e4-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![Выбор представления Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="402e4-147">После загрузки представления Tez вы увидите список запросов Hive, которые выполняются в настоящее время или выполнялись в кластере.</span><span class="sxs-lookup"><span data-stu-id="402e4-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![Все DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="402e4-149">Если у вас имеется только одна запись, то она используется для запроса, выполненного в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="402e4-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="402e4-150">Если у вас несколько записей, можно выполнить поиск, используя поля в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="402e4-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="402e4-151">Выберите **идентификатор запроса** Hive.</span><span class="sxs-lookup"><span data-stu-id="402e4-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="402e4-152">Появятся сведения о запросе.</span><span class="sxs-lookup"><span data-stu-id="402e4-152">Information about the query is displayed.</span></span>

    ![Сведения о DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="402e4-154">С помощью вкладок на этой странице можно просмотреть указанные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="402e4-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="402e4-155">**Сведения о запросе**: подробные сведения о запросе Hive.</span><span class="sxs-lookup"><span data-stu-id="402e4-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="402e4-156">**Временная шкала**: сведения о том, сколько времени занял каждый этап обработки.</span><span class="sxs-lookup"><span data-stu-id="402e4-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="402e4-157">**Конфигурации**: конфигурация, используемая для этого запроса.</span><span class="sxs-lookup"><span data-stu-id="402e4-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="402e4-158">В разделе __Сведения о запросе__ можно перейти по ссылкам, чтобы получить сведения о __приложении__ или __направленном ациклическом графе__ запроса.</span><span class="sxs-lookup"><span data-stu-id="402e4-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="402e4-159">По ссылке __Приложение__ можно получить сведения о приложении YARN для этого запроса.</span><span class="sxs-lookup"><span data-stu-id="402e4-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="402e4-160">Здесь также можно открыть журналы приложения YARN.</span><span class="sxs-lookup"><span data-stu-id="402e4-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="402e4-161">По ссылке __DAG__ открываются сведения о направленном ациклическом графе запроса (DAG).</span><span class="sxs-lookup"><span data-stu-id="402e4-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="402e4-162">Здесь также можно просмотреть графическое представление DAG</span><span class="sxs-lookup"><span data-stu-id="402e4-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="402e4-163">и найти сведения о вершинах DAG.</span><span class="sxs-lookup"><span data-stu-id="402e4-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="402e4-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="402e4-164">Next Steps</span></span>

<span data-ttu-id="402e4-165">Теперь, когда вы поняли, как работать с представлением Tez, узнайте больше об [использовании Hive в HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="402e4-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="402e4-166">Более подробные технические сведения о Tez см. на [странице Tez на сайте Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="402e4-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="402e4-167">Дополнительные сведения об использовании Ambari в HDInsight см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="402e4-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
