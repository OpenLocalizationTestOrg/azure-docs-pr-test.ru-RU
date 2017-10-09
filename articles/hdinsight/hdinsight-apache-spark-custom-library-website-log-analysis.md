---
title: "журналы веб-сайт aaaAnalyze с библиотеками Python в Spark - Azure | Документы Microsoft"
description: "Записной книжки показано, как tooanalyze данных журнала с помощью пользовательская библиотека с Spark на Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="0bcb9-103">Анализ журналов веб-сайтов с помощью пользовательской библиотеки Python и кластера Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bcb9-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="0bcb9-104">Записной книжки показано, как tooanalyze данных журнала с помощью пользовательская библиотека с Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="0bcb9-105">Мы используем пользовательская библиотека Hello является именем библиотеки Python **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="0bcb9-106">Кроме того, это руководство доступно в виде записной книжки Jupyter в кластере Spark (на платформе Linux), созданном в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="0bcb9-107">взаимодействие с ноутбука Hello позволяет выполнять фрагменты кода Python hello из записной книжки hello сам.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="0bcb9-108">Учебник hello tooperform в записной книжке создать кластер Spark, запустить записной книжке Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), и запустите записной книжки hello **анализировать журналы с помощью Spark, с помощью пользовательских library.ipynb** под hello  **PySpark** папки.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="0bcb9-109">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="0bcb9-109">**Prerequisites:**</span></span>

<span data-ttu-id="0bcb9-110">Необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-110">You must have hello following:</span></span>

* <span data-ttu-id="0bcb9-111">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-111">An Azure subscription.</span></span> <span data-ttu-id="0bcb9-112">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0bcb9-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="0bcb9-113">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0bcb9-114">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="0bcb9-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="0bcb9-115">Сохранение необработанных данных в формате RDD</span><span class="sxs-lookup"><span data-stu-id="0bcb9-115">Save raw data as an RDD</span></span>
<span data-ttu-id="0bcb9-116">В этом разделе мы используем hello [Jupyter](https://jupyter.org) ноутбук, связанные с кластера с Apache Spark в HDInsight toorun задания, которые обрабатывают необработанные образцы данных и сохраните его как таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="0bcb9-117">Образец Hello данных является CSV-файла (hvac.csv) доступен во всех кластерах по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="0bcb9-118">После сохранения данных как таблицу Hive в следующем разделе hello мы будут подключаться с помощью средств бизнес-Аналитики, таких как Power BI и Tableau таблицу Hive toohello.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="0bcb9-119">Из hello [портал Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели).</span><span class="sxs-lookup"><span data-stu-id="0bcb9-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="0bcb9-120">Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="0bcb9-121">Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="0bcb9-122">При появлении запроса введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0bcb9-123">Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="0bcb9-124">Замените **CLUSTERNAME** с hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="0bcb9-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="0bcb9-125">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-125">Create a new notebook.</span></span> <span data-ttu-id="0bcb9-126">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="0bcb9-127">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="0bcb9-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="0bcb9-128">Создается и открывается с именем hello Untitled.pynb новый блокнот.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="0bcb9-129">Щелкните имя записной книжки hello вверху hello и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="0bcb9-130">![Введите имя для ноутбука hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "укажите имя для ноутбука hello")</span><span class="sxs-lookup"><span data-stu-id="0bcb9-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="0bcb9-131">Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="0bcb9-132">контексты Spark и Hive Hello автоматически создается автоматически при выполнении первой ячейке кода hello.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="0bcb9-133">Можно запустить, импортировав hello типы, необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="0bcb9-134">Вставьте следующий фрагмент кода в пустой ячейке hello и нажмите клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="0bcb9-135">Создайте RDD, используя данные журнала образца hello уже доступны в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="0bcb9-136">Доступ к hello в учетной записи хранения по умолчанию hello связанные с кластером hello в **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="0bcb9-137">Получить образец tooverify набор журнала, который hello в предыдущем шаге, завершилась успешно.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="0bcb9-138">Вы должны увидеть следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="0bcb9-139">Анализ данных журнала с помощью пользовательской библиотеки Python</span><span class="sxs-lookup"><span data-stu-id="0bcb9-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="0bcb9-140">В приведенных выше входных данных hello hello первые несколько строк учитываются сведения заголовков hello и hello схема, описанная в заголовок, соответствующий каждой оставшиеся строки.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="0bcb9-141">Анализ таких журналов может быть сложным,</span><span class="sxs-lookup"><span data-stu-id="0bcb9-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="0bcb9-142">поэтому мы используем настраиваемую библиотеку Python (**iislogparser.py**), которая делает эту задачу намного проще.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="0bcb9-143">По умолчанию эта библиотека входит в состав кластера Spark в HDInsight и расположена в **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="0bcb9-144">Однако эта библиотека не является hello `PYTHONPATH` , нельзя использовать с помощью инструкции импорта, как `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="0bcb9-145">toouse этой библиотеки, нам необходимо распространить tooall hello рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="0bcb9-146">Запустите следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="0bcb9-147">`iislogparser`предоставляет функцию `parse_log_line` , возвращающий `None` Если строку журнала представляет собой строку и возвращает экземпляр hello `LogLine` класса при обнаружении строки журнала.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="0bcb9-148">Используйте hello `LogLine` tooextract класс только hello строк журнала из hello RDD:</span><span class="sxs-lookup"><span data-stu-id="0bcb9-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="0bcb9-149">Получить несколько tooverify извлеченных строк журнала, hello шаге, завершилась успешно.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="0bcb9-150">Hello выходные данные должны быть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="0bcb9-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="0bcb9-151">Hello `LogLine` класс, в свою очередь, имеет некоторые методы, например `is_error()`, который показывает, имеет ли запись в журнал код ошибки.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="0bcb9-152">Использовать это число hello toocompute ошибок в строках журнала извлечены hello и войдите все hello ошибки tooa другой файл.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="0bcb9-153">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0bcb9-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="0bcb9-154">Можно также использовать **Matplotlib** tooconstruct визуализации данных hello.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="0bcb9-155">Например следует tooisolate причину hello запросы выполняются в течение длительного времени может потребоваться toofind hello файлы hello tooserve большая часть времени в среднем.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="0bcb9-156">в приведенном ниже фрагменте Hello извлекает hello top 25 ресурсы, предпринятые большинство tooserve время запроса.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="0bcb9-157">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0bcb9-157">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="0bcb9-158">Можно также представить эти сведения в виде hello построения.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="0bcb9-159">Как первый toocreate шаг построения, сообщите нам сначала создать временную таблицу **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="0bcb9-160">Hello таблицы групп hello регистрирует по toosee времени при наличии каких-либо пиков необычные задержки в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="0bcb9-161">Можно выполнять hello, следуя tooget запроса SQL все записи hello в hello **AverageTime** таблицы.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="0bcb9-162">Hello `%%sql` следуют магическое `-o averagetime` гарантирует, что hello выходных данных запроса hello сохраняется локально на сервере Jupyter hello (обычно hello головному узлу кластера hello).</span><span class="sxs-lookup"><span data-stu-id="0bcb9-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="0bcb9-163">Hello выходные данные сохраняются в виде [Pandas](http://pandas.pydata.org/) кадр данных с hello указано имя **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="0bcb9-164">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0bcb9-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="0bcb9-165">![Результат SQL-запроса](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Результат SQL-запроса")</span><span class="sxs-lookup"><span data-stu-id="0bcb9-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="0bcb9-166">Дополнительные сведения о hello `%%sql` magic, см. в разделе [поддерживает параметры с hello %% sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="0bcb9-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="0bcb9-167">Теперь вы можете использовать Matplotlib, библиотеку используется tooconstruct визуализации данных, toocreate построение.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="0bcb9-168">Так как hello рисунка должны быть созданы из локально hello материализованные **averagetime** кадр данных, фрагмент кода hello должно начинаться с hello `%%local` магическое значение.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="0bcb9-169">Это гарантирует, что hello код запускается локально на сервере Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="0bcb9-170">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0bcb9-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="0bcb9-171">![Выходные данные Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Выходные данные Matplotlib")</span><span class="sxs-lookup"><span data-stu-id="0bcb9-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="0bcb9-172">После завершения работы приложения hello, необходимо hello toorelease ресурсы для завершения работы hello ноутбуков.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="0bcb9-173">toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="0bcb9-174">В этом будет завершена и закрыть hello ноутбука.</span><span class="sxs-lookup"><span data-stu-id="0bcb9-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="0bcb9-175"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="0bcb9-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0bcb9-176">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bcb9-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="0bcb9-177">Сценарии</span><span class="sxs-lookup"><span data-stu-id="0bcb9-177">Scenarios</span></span>
* [<span data-ttu-id="0bcb9-178">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="0bcb9-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0bcb9-179">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="0bcb9-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0bcb9-180">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="0bcb9-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0bcb9-181">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="0bcb9-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="0bcb9-182">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="0bcb9-182">Create and run applications</span></span>
* [<span data-ttu-id="0bcb9-183">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="0bcb9-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0bcb9-184">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="0bcb9-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0bcb9-185">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="0bcb9-185">Tools and extensions</span></span>
* [<span data-ttu-id="0bcb9-186">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений</span><span class="sxs-lookup"><span data-stu-id="0bcb9-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0bcb9-187">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0bcb9-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0bcb9-188">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bcb9-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0bcb9-189">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bcb9-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0bcb9-190">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="0bcb9-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0bcb9-191">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="0bcb9-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="0bcb9-192">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="0bcb9-192">Manage resources</span></span>
* [<span data-ttu-id="0bcb9-193">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bcb9-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0bcb9-194">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="0bcb9-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
