---
title: "aaaUse toowork Ambari представления с Hive в HDInsight (Hadoop) - Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Hive представления из вашего веб-браузера toosubmit Hive запросы. Hello Hive представление является частью hello, предоставленные Ambari веб-интерфейса пользователя с кластером HDInsight под управлением Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="bc21f-104">Использовать hello Hive представление на Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc21f-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="bc21f-105">Узнайте, как toorun Hive запросов с помощью Ambari Hive представления.</span><span class="sxs-lookup"><span data-stu-id="bc21f-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="bc21f-106">Ambari — это служебная программа для управления и мониторинга, предоставляемая с кластерами HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="bc21f-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="bc21f-107">Одна из функций hello, предоставленные с помощью Ambari — веб-интерфейса, можно использовать toorun запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="bc21f-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="bc21f-108">У Ambari много разных функций, которые не рассматриваются в этом документе.</span><span class="sxs-lookup"><span data-stu-id="bc21f-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="bc21f-109">Дополнительные сведения см. в разделе [кластеры HDInsight управление с помощью веб-интерфейса Ambari hello](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="bc21f-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc21f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bc21f-110">Prerequisites</span></span>

* <span data-ttu-id="bc21f-111">Кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="bc21f-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="bc21f-112">Сведения о создании кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc21f-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc21f-113">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="bc21f-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="bc21f-114">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="bc21f-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bc21f-115">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bc21f-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="bc21f-116">Откройте представление Hive hello</span><span class="sxs-lookup"><span data-stu-id="bc21f-116">Open hello Hive view</span></span>

<span data-ttu-id="bc21f-117">Вы можете Ambari представления из hello портал Azure; Выберите кластер HDInsight, а затем выберите **представления Ambari** из hello **быстрые ссылки** раздела.</span><span class="sxs-lookup"><span data-stu-id="bc21f-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![Быстрые ссылки раздел hello портала](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="bc21f-119">Выберите из списка hello представлений hello __Hive представление__.</span><span class="sxs-lookup"><span data-stu-id="bc21f-119">From hello list of views, select hello __Hive View__.</span></span>

![Hello Hive представления, выбранного](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="bc21f-121">При доступе к Ambari, все запрашиваемые tooauthenticate toohello сайта.</span><span class="sxs-lookup"><span data-stu-id="bc21f-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="bc21f-122">Введите Здравствуйте, администратор (по умолчанию `admin`) учетной записи, имя и пароль, используемый при создании hello кластера.</span><span class="sxs-lookup"><span data-stu-id="bc21f-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="bc21f-123">Вы увидите примерно toohello страницы, следующие изображения:</span><span class="sxs-lookup"><span data-stu-id="bc21f-123">You should see a page similar toohello following image:</span></span>

![Изображение листа hello запрос для представления Hive hello](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="bc21f-125"><a name="hivequery"></a>Выполнение запроса</span><span class="sxs-lookup"><span data-stu-id="bc21f-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="bc21f-126">toorun запрос hive с помощью hello, выполнив действия из представления Hive hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="bc21f-127">Из hello __запроса__ , вставьте следующие инструкции HiveQL лист hello hello:</span><span class="sxs-lookup"><span data-stu-id="bc21f-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="bc21f-128">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bc21f-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="bc21f-129">`DROP TABLE`— Удаляет hello таблицы и файла данных hello, в случае, если таблица hello уже существует.</span><span class="sxs-lookup"><span data-stu-id="bc21f-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="bc21f-130">`CREATE EXTERNAL TABLE` — создание "внешней" таблицы в Hive.</span><span class="sxs-lookup"><span data-stu-id="bc21f-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="bc21f-131">Внешние таблицы хранить только определение таблицы hello в кусте.</span><span class="sxs-lookup"><span data-stu-id="bc21f-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="bc21f-132">Hello данные остаются в исходном расположении hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="bc21f-133">`ROW FORMAT`-Способа форматирования данных hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="bc21f-134">В этом случае hello полей в каждом журнале разделенные пробелом.</span><span class="sxs-lookup"><span data-stu-id="bc21f-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="bc21f-135">`STORED AS TEXTFILE LOCATION`-Hello хранения данных и хранится как текст.</span><span class="sxs-lookup"><span data-stu-id="bc21f-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="bc21f-136">`SELECT`-Выбор количества всех строк, где t4 столбец содержит значение hello [ошибка].</span><span class="sxs-lookup"><span data-stu-id="bc21f-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="bc21f-137">Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="bc21f-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="bc21f-138">Например, с использованием процесса автоматической передачи данных или другой операции MapReduce.</span><span class="sxs-lookup"><span data-stu-id="bc21f-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="bc21f-139">Удаление внешней таблицы *не* удаление данных hello, только определение таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bc21f-140">Оставьте hello __базы данных__ Выбор __по умолчанию__.</span><span class="sxs-lookup"><span data-stu-id="bc21f-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="bc21f-141">Hello примерах в этом документе используется базой данных по умолчанию hello в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc21f-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="bc21f-142">запрос toostart hello, используйте hello **Execute** кнопки ниже hello листа.</span><span class="sxs-lookup"><span data-stu-id="bc21f-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="bc21f-143">Включает оранжевый и hello изменения текста слишком**остановить**.</span><span class="sxs-lookup"><span data-stu-id="bc21f-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="bc21f-144">После завершения запроса hello, hello **результатов** вкладка отображает hello результаты операции hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="bc21f-145">После текста Hello представляет hello результат запроса hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="bc21f-146">Hello **журналы** вкладке может быть используется tooview hello ведения журнала данных, созданных заданием hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="bc21f-147">Hello **сохранить результаты** диалоговое окно раскрывающегося списка в hello верхнего левого угла hello **результаты процесса запроса** раздел позволяет вам toodownload или сохранить результаты.</span><span class="sxs-lookup"><span data-stu-id="bc21f-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="bc21f-148">Выберите hello первые четыре строки этого запроса, затем выберите **Execute**.</span><span class="sxs-lookup"><span data-stu-id="bc21f-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="bc21f-149">Обратите внимание, что нет результатов при завершении задания hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="bc21f-150">С помощью hello **Execute** как часть запроса hello выбран только запусков hello выбранных инструкций.</span><span class="sxs-lookup"><span data-stu-id="bc21f-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="bc21f-151">В этом случае Выбор hello не были включены hello последнюю инструкцию, которая извлекает строки из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="bc21f-152">Если выбрать только этой строки и использовать **Execute**, вы увидите результаты ожидается hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="bc21f-153">tooadd лист, используйте hello **новый лист** кнопку внизу hello hello **редактора запросов**.</span><span class="sxs-lookup"><span data-stu-id="bc21f-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="bc21f-154">В новом листе hello введите следующие инструкции HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="bc21f-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="bc21f-155">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bc21f-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="bc21f-156">**CREATE TABLE IF NOT EXISTS** : создание таблицы, если она до этого не существовала.</span><span class="sxs-lookup"><span data-stu-id="bc21f-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="bc21f-157">С момента hello **ВНЕШНИХ** ключевое слово не используется, создается внутренней таблицы.</span><span class="sxs-lookup"><span data-stu-id="bc21f-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="bc21f-158">Внутренняя таблица хранится в хранилище данных Hive hello и полностью управляются Hive.</span><span class="sxs-lookup"><span data-stu-id="bc21f-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="bc21f-159">В отличие от внешних таблиц при удалении внутренней таблицы удаляются hello базовые данные.</span><span class="sxs-lookup"><span data-stu-id="bc21f-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="bc21f-160">**ORC ХРАНИМОЙ AS** -хранит данные hello в оптимизированные строк по столбцам (формат ORC.).</span><span class="sxs-lookup"><span data-stu-id="bc21f-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="bc21f-161">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="bc21f-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="bc21f-162">**INSERT OVERWRITE ... ВЫБЕРИТЕ** -выбирает строки из hello **log4jLogs** таблицы, которые содержат `[ERROR]`, и затем вставляет hello данных в hello **журналы ошибок** таблицы.</span><span class="sxs-lookup"><span data-stu-id="bc21f-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="bc21f-163">Используйте hello **Execute** кнопку toorun этот запрос.</span><span class="sxs-lookup"><span data-stu-id="bc21f-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="bc21f-164">Hello **результатов** вкладка не содержит все сведения, когда hello запрос возвращает 0 строк.</span><span class="sxs-lookup"><span data-stu-id="bc21f-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="bc21f-165">состояние Hello должно отображаться как **успешно** после завершения выполнения запроса hello.</span><span class="sxs-lookup"><span data-stu-id="bc21f-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="bc21f-166">Визуальное объяснение</span><span class="sxs-lookup"><span data-stu-id="bc21f-166">Visual explain</span></span>

<span data-ttu-id="bc21f-167">toodisplay визуализации плана запроса hello, выберите hello **Visual объяснить** под hello листа.</span><span class="sxs-lookup"><span data-stu-id="bc21f-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="bc21f-168">Hello **Visual объяснить** представление hello запроса могут быть полезны для понимания hello потока сложных запросов.</span><span class="sxs-lookup"><span data-stu-id="bc21f-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="bc21f-169">Текстовый эквивалент этого представления можно просмотреть с помощью hello **объяснение** кнопку в hello редактора запросов.</span><span class="sxs-lookup"><span data-stu-id="bc21f-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="bc21f-170">Пользовательский интерфейс Tez</span><span class="sxs-lookup"><span data-stu-id="bc21f-170">Tez UI</span></span>

<span data-ttu-id="bc21f-171">toodisplay hello Tez пользовательского интерфейса для запроса hello, выберите hello **Tez** под hello листа.</span><span class="sxs-lookup"><span data-stu-id="bc21f-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc21f-172">Tez является tooresolve не используется все запросы.</span><span class="sxs-lookup"><span data-stu-id="bc21f-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="bc21f-173">Многие запросы можно разрешить и без применения Tez.</span><span class="sxs-lookup"><span data-stu-id="bc21f-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="bc21f-174">Если Tez запроса используется tooresolve hello, отображается hello расширенный ациклического графа (DAG).</span><span class="sxs-lookup"><span data-stu-id="bc21f-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="bc21f-175">Tooview hello DAG для запросов уже выполнялись в прошлом hello, или отладке hello Tez процесса, используйте hello [Tez представление](hdinsight-debug-ambari-tez-view.md) вместо него.</span><span class="sxs-lookup"><span data-stu-id="bc21f-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="bc21f-176">Просмотр журнала заданий</span><span class="sxs-lookup"><span data-stu-id="bc21f-176">View job history</span></span>

<span data-ttu-id="bc21f-177">Hello __заданий__ вкладка отображается История запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="bc21f-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Изображение hello журнал заданий](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="bc21f-179">Таблицы базы данных</span><span class="sxs-lookup"><span data-stu-id="bc21f-179">Database tables</span></span>

<span data-ttu-id="bc21f-180">Можно использовать hello __таблиц__ вкладке toowork с таблицами в базе данных Hive.</span><span class="sxs-lookup"><span data-stu-id="bc21f-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Изображение вкладку таблицы hello](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="bc21f-182">Сохраненные запросы</span><span class="sxs-lookup"><span data-stu-id="bc21f-182">Saved queries</span></span>

<span data-ttu-id="bc21f-183">На вкладке запросов hello при необходимости можно сохранить запросы.</span><span class="sxs-lookup"><span data-stu-id="bc21f-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="bc21f-184">После сохранения можно повторно использовать запрос hello из hello __сохраненные запросы__ вкладки.</span><span class="sxs-lookup"><span data-stu-id="bc21f-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![Изображение вкладки "Сохраненные запросы"](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="bc21f-186">Определяемые пользователем функции</span><span class="sxs-lookup"><span data-stu-id="bc21f-186">User-defined functions</span></span>

<span data-ttu-id="bc21f-187">Инфраструктуру Hive также можно расширить с помощью определяемых пользователем функций (UDF).</span><span class="sxs-lookup"><span data-stu-id="bc21f-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="bc21f-188">Определяемая пользователем Функция позволяет tooimplement функциональность или логику, которая не легко моделируется в HiveQL.</span><span class="sxs-lookup"><span data-stu-id="bc21f-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="bc21f-189">Hello UDF вкладку вверху hello hello Hive представление позволяет toodeclare и сохраните набор определяемых пользователем функций.</span><span class="sxs-lookup"><span data-stu-id="bc21f-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="bc21f-190">Эти пользовательские функции могут использоваться с hello **редактора запросов**.</span><span class="sxs-lookup"><span data-stu-id="bc21f-190">These UDFs can be used with hello **Query Editor**.</span></span>

![Изображение вкладки "Определяемая пользователем функция"](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="bc21f-192">После добавления определяемой пользователем функции toohello представление Hive, **Вставка определяемых пользователем функций** появляется кнопка внизу hello hello **редактора запросов**.</span><span class="sxs-lookup"><span data-stu-id="bc21f-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="bc21f-193">При выборе этой записи отображаются раскрывающиеся hello определяемые пользователем функции, определенные в hello Hive представления.</span><span class="sxs-lookup"><span data-stu-id="bc21f-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="bc21f-194">При выборе определяемой пользователем функции добавляется hello HiveQL инструкций tooyour запроса tooenable определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="bc21f-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="bc21f-195">Например, если вы определили определяемой пользователем функции с hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="bc21f-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="bc21f-196">имя ресурса — myudfs;</span><span class="sxs-lookup"><span data-stu-id="bc21f-196">Resource name: myudfs</span></span>

* <span data-ttu-id="bc21f-197">путь к ресурсу — /myudfs.jar;</span><span class="sxs-lookup"><span data-stu-id="bc21f-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="bc21f-198">имя определяемой пользователем функции — myawesomeudf;</span><span class="sxs-lookup"><span data-stu-id="bc21f-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="bc21f-199">имя класса определяемой пользователем функции — com.myudfs.Awesome.</span><span class="sxs-lookup"><span data-stu-id="bc21f-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="bc21f-200">С помощью hello **Вставка определяемых пользователем функций** кнопки отображаются записи с именем **myudfs**, с другим раскрывающегося списка для каждой определяемой пользователем функции определен для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="bc21f-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="bc21f-201">В нашем примере это функция **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="bc21f-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="bc21f-202">При выборе этой записи добавляет hello после начала toohello hello запроса:</span><span class="sxs-lookup"><span data-stu-id="bc21f-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="bc21f-203">Затем можно использовать hello определяемой пользователем функции в запросе.</span><span class="sxs-lookup"><span data-stu-id="bc21f-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="bc21f-204">Например, `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="bc21f-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="bc21f-205">Дополнительные сведения об использовании определяемых пользователем функций с Hive в HDInsight см. в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="bc21f-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="bc21f-206">Использование Python с Hive и Pig в HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc21f-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="bc21f-207">Как tooadd пользовательские tooHDInsight Hive определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="bc21f-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="bc21f-208">Параметры Hive</span><span class="sxs-lookup"><span data-stu-id="bc21f-208">Hive settings</span></span>

<span data-ttu-id="bc21f-209">Параметры могут быть различные параметры Hive используется toochange.</span><span class="sxs-lookup"><span data-stu-id="bc21f-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="bc21f-210">Например изменение hello подсистема выполнения для куста tooMapReduce Tez (по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="bc21f-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="bc21f-211"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc21f-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="bc21f-212">Общая информация о Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc21f-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="bc21f-213">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc21f-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="bc21f-214">Дополнительная информация о других способах работы с Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc21f-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="bc21f-215">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc21f-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="bc21f-216">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc21f-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
