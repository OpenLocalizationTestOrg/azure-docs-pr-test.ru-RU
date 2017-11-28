---
title: "aaaUse Ambari Tez представление с HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как hello toouse Ambari Tez Просмотр заданий Tez toodebug на HDInsight."
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
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="d4f47-103">Использование представления Ambari toodebug Tez заданий в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4f47-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="d4f47-104">Hello Ambari веб-интерфейса для HDInsight содержит Tez представление, которое может быть используется toounderstand и отладка задания, использующие Tez.</span><span class="sxs-lookup"><span data-stu-id="d4f47-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="d4f47-105">представление Tez Hello позволяет toovisualize hello задания как граф соединенными элементами можно перейти к каждому элементу и получить статистические данные и сведения о ведении журнала.</span><span class="sxs-lookup"><span data-stu-id="d4f47-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4f47-106">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="d4f47-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="d4f47-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d4f47-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d4f47-108">Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md#hdinsight-windows-retirement)</span><span class="sxs-lookup"><span data-stu-id="d4f47-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4f47-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d4f47-109">Prerequisites</span></span>

* <span data-ttu-id="d4f47-110">Кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="d4f47-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d4f47-111">Инструкции по созданию кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d4f47-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="d4f47-112">Современный веб-браузер, который поддерживает HTML5.</span><span class="sxs-lookup"><span data-stu-id="d4f47-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="d4f47-113">Общие сведения о Tez</span><span class="sxs-lookup"><span data-stu-id="d4f47-113">Understanding Tez</span></span>

<span data-ttu-id="d4f47-114">Tez — это расширяемая платформа для обработки данных в Hadoop, которая характеризуется более высокими скоростями по сравнению с традиционной обработкой MapReduce.</span><span class="sxs-lookup"><span data-stu-id="d4f47-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="d4f47-115">Для кластеров HDInsight под управлением Linux именно модуль по умолчанию hello для куста.</span><span class="sxs-lookup"><span data-stu-id="d4f47-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="d4f47-116">Tez создает направленный ациклического графа (DAG), описывающий hello порядок действий, которые требуются для работы.</span><span class="sxs-lookup"><span data-stu-id="d4f47-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="d4f47-117">Индивидуальные действия, называются вершин и выполнять часть hello задание в целом.</span><span class="sxs-lookup"><span data-stu-id="d4f47-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="d4f47-118">Hello фактическое выполнение работы hello, описываемого вершина вызывается задача и могут быть распределены по нескольким узлам в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="d4f47-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="d4f47-119">Основные сведения о hello Tez представление</span><span class="sxs-lookup"><span data-stu-id="d4f47-119">Understanding hello Tez view</span></span>

<span data-ttu-id="d4f47-120">Hello Tez представление предоставляет исторические данные и сведения для процессов, работающих под управлением.</span><span class="sxs-lookup"><span data-stu-id="d4f47-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="d4f47-121">Здесь можно просмотреть, как задание распределяется по кластерам.</span><span class="sxs-lookup"><span data-stu-id="d4f47-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="d4f47-122">Она также отображает счетчики, используемые задачи и вершин и сведения об ошибках, связанных с toohello задания.</span><span class="sxs-lookup"><span data-stu-id="d4f47-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="d4f47-123">Он может предложить полезную информацию в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="d4f47-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="d4f47-124">Наблюдение за процессами длительное время, просмотр hello ход выполнения сопоставления и сокращения.</span><span class="sxs-lookup"><span data-stu-id="d4f47-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="d4f47-125">Анализ исторических данных для toolearn успешной или неуспешной процессы, как можно улучшить обработку или причину сбоя.</span><span class="sxs-lookup"><span data-stu-id="d4f47-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="d4f47-126">Создание DAG</span><span class="sxs-lookup"><span data-stu-id="d4f47-126">Generate a DAG</span></span>

<span data-ttu-id="d4f47-127">представление содержит данные, только если задание, использующее hello Tez ядра Tez Hello выполняется в данный момент или ранее выполнялись.</span><span class="sxs-lookup"><span data-stu-id="d4f47-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="d4f47-128">Простые запросы Hive можно разрешить без использования Tez.</span><span class="sxs-lookup"><span data-stu-id="d4f47-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="d4f47-129">Подсистема Tez требуется для работы с более сложными запросами, которые выполняют фильтрацию, группировку,</span><span class="sxs-lookup"><span data-stu-id="d4f47-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="d4f47-130">следует используйте механизм Tez hello.</span><span class="sxs-lookup"><span data-stu-id="d4f47-130">use hello Tez engine.</span></span>

<span data-ttu-id="d4f47-131">Используйте следующие шаги toorun запрос Hive, который использует Tez hello.</span><span class="sxs-lookup"><span data-stu-id="d4f47-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="d4f47-132">В веб-браузере перейдите toohttps://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4f47-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="d4f47-133">Hello меню вверху hello страницы приветствия выберите hello **представления** значок.</span><span class="sxs-lookup"><span data-stu-id="d4f47-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="d4f47-134">Он выглядит как набор квадратов.</span><span class="sxs-lookup"><span data-stu-id="d4f47-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="d4f47-135">В раскрывающемся списке hello, который отображается, выберите **Hive представление**.</span><span class="sxs-lookup"><span data-stu-id="d4f47-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Выбор представления Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="d4f47-137">При загрузке hello представление Hive, вставить hello ниже запроса в редактор запросов hello и нажмите кнопку **выполнение**.</span><span class="sxs-lookup"><span data-stu-id="d4f47-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="d4f47-138">После завершения задания hello, вы должны увидеть результаты hello, отображаемых в hello **результаты процесса запроса** раздела.</span><span class="sxs-lookup"><span data-stu-id="d4f47-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="d4f47-139">Hello результаты должны быть примерно toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="d4f47-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="d4f47-140">Выберите hello **журнала** вкладки. Можно увидеть примерно toohello сведения после текста:</span><span class="sxs-lookup"><span data-stu-id="d4f47-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="d4f47-141">Сохранить hello **идентификатор приложения** значение, так как это значение используется в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d4f47-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="d4f47-142">Используйте представление Tez hello</span><span class="sxs-lookup"><span data-stu-id="d4f47-142">Use hello Tez View</span></span>

1. <span data-ttu-id="d4f47-143">Hello меню вверху hello страницы приветствия выберите hello **представления** значок.</span><span class="sxs-lookup"><span data-stu-id="d4f47-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="d4f47-144">В раскрывающемся списке hello, который отображается, выберите **Tez представление**.</span><span class="sxs-lookup"><span data-stu-id="d4f47-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Выбор представления Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="d4f47-146">При загрузке hello представление Tez видно, что список запросов hive, выполняющихся в данный момент, или была выполнена на hello кластера.</span><span class="sxs-lookup"><span data-stu-id="d4f47-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![Все DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="d4f47-148">Если имеется только одна запись, он предназначен для запроса hello, выполнялись в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d4f47-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="d4f47-149">Если у вас есть несколько записей, можно выполнить поиск с помощью полей hello вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="d4f47-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="d4f47-150">Выберите hello **идентификатор запроса** для запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="d4f47-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="d4f47-151">Отображаются сведения о запросе hello.</span><span class="sxs-lookup"><span data-stu-id="d4f47-151">Information about hello query is displayed.</span></span>

    ![Сведения о DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="d4f47-153">Hello вкладки на этой странице разрешить hello tooview следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d4f47-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="d4f47-154">**Запрос сведений**: сведения о запроса Hive hello.</span><span class="sxs-lookup"><span data-stu-id="d4f47-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="d4f47-155">**Временная шкала**: сведения о том, сколько времени занял каждый этап обработки.</span><span class="sxs-lookup"><span data-stu-id="d4f47-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="d4f47-156">**Конфигурации**: hello конфигурацию, используемую для этого запроса.</span><span class="sxs-lookup"><span data-stu-id="d4f47-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="d4f47-157">Из __сведения о запросе__ можно использовать ссылки на сведения toofind hello о hello __приложения__ или hello __DAG__ для этого запроса.</span><span class="sxs-lookup"><span data-stu-id="d4f47-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="d4f47-158">Hello __приложения__ связи отображаются сведения о hello YARN приложения для этого запроса.</span><span class="sxs-lookup"><span data-stu-id="d4f47-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="d4f47-159">Здесь можно получить доступ к журналы приложений YARN hello.</span><span class="sxs-lookup"><span data-stu-id="d4f47-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="d4f47-160">Hello __DAG__ связи отображаются сведения о hello ориентированного ациклического графа для этого запроса.</span><span class="sxs-lookup"><span data-stu-id="d4f47-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="d4f47-161">Здесь можно просмотреть графическое представление hello DAG.</span><span class="sxs-lookup"><span data-stu-id="d4f47-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="d4f47-162">Также можно найти сведения о hello вершин в hello DAG.</span><span class="sxs-lookup"><span data-stu-id="d4f47-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4f47-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4f47-163">Next Steps</span></span>

<span data-ttu-id="d4f47-164">Теперь, когда вы узнали, как просмотреть toouse hello Tez, Дополнительные сведения о [с помощью Hive в HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="d4f47-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="d4f47-165">Более подробные технические сведения о Tez см. в разделе hello [Tez страницу в Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="d4f47-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="d4f47-166">Дополнительные сведения об использовании Ambari с HDInsight см. в разделе [управление кластерами HDInsight с помощью hello Ambari веб-интерфейса](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="d4f47-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
