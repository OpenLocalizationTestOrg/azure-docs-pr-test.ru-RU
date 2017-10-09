---
title: "кластер записных книжек Zeppelin aaaUse с Apache Spark на Azure HDInsight | Документы Microsoft"
description: "Пошаговые инструкции по как кластеры записных книжек Zeppelin toouse с Apache Spark на Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="23798-103">Использование записных книжек Zeppelin с кластером Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="23798-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="23798-104">Кластеры HDInsight Spark включают Zeppelin портативные компьютеры, которые можно использовать toorun Spark заданий.</span><span class="sxs-lookup"><span data-stu-id="23798-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="23798-105">В этой статье вы узнаете, как toouse hello записной книжки Zeppelin в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23798-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="23798-106">Записные книжки Zeppelin доступны только для Spark 1.6.3 в HDInsight 3.5 и для Spark 2.1.0 в HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="23798-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="23798-107">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="23798-107">**Prerequisites:**</span></span>

* <span data-ttu-id="23798-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="23798-108">An Azure subscription.</span></span> <span data-ttu-id="23798-109">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="23798-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="23798-110">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23798-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="23798-111">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="23798-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="23798-112">Запуск записной книжки Zeppelin</span><span class="sxs-lookup"><span data-stu-id="23798-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="23798-113">Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **Zeppelin ноутбук**.</span><span class="sxs-lookup"><span data-stu-id="23798-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="23798-114">При появлении запроса введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="23798-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="23798-115">Также может достигать hello Zeppelin ноутбук для кластера, открыв hello следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="23798-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="23798-116">Замените **CLUSTERNAME** с hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="23798-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="23798-117">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="23798-117">Create a new notebook.</span></span> <span data-ttu-id="23798-118">Hello заголовка области, щелкните ссылку **записной книжки**, а затем нажмите кнопку **создать новую заметку**.</span><span class="sxs-lookup"><span data-stu-id="23798-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="23798-119">![Создание записной книжки Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Создание записной книжки Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="23798-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="23798-120">Введите имя для hello портативного компьютера и нажмите кнопку **создать Примечание**.</span><span class="sxs-lookup"><span data-stu-id="23798-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="23798-121">Кроме того убедитесь, что заголовок записной книжки hello показывает подключенном состоянии.</span><span class="sxs-lookup"><span data-stu-id="23798-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="23798-122">Он обозначается зеленая точка в верхнем правом углу hello.</span><span class="sxs-lookup"><span data-stu-id="23798-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="23798-123">![Состояния записной книжки Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Состояния записной книжки Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="23798-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="23798-124">Загрузите демонстрационные данные во временную таблицу.</span><span class="sxs-lookup"><span data-stu-id="23798-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="23798-125">При создании кластера Spark в HDInsight hello образец файла данных **hvac.csv**, является скопированный toohello связанные учетной записи хранилища в группе **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="23798-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="23798-126">В пустой абзац hello, создаваемый по умолчанию в новой записной книжки hello вставьте следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="23798-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="23798-127">Нажмите клавишу **SHIFT + ВВОД** или нажмите кнопку hello **воспроизведение** кнопки для hello абзаца toorun hello фрагмента.</span><span class="sxs-lookup"><span data-stu-id="23798-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="23798-128">состояние Hello в правом углу hello абзаца hello следует хода выполнения Готово, ОЖИДАЮЩИХ ВЫПОЛНЕНИЯ tooFINISHED.</span><span class="sxs-lookup"><span data-stu-id="23798-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="23798-129">выходные данные Hello отображается внизу hello hello того же абзаца.</span><span class="sxs-lookup"><span data-stu-id="23798-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="23798-130">Снимок экрана приветствия выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="23798-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="23798-131">![Создание временной таблицы из необработанных данных](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Создание временной таблицы из необработанных данных")</span><span class="sxs-lookup"><span data-stu-id="23798-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="23798-132">Можно также ввести заголовок tooeach абзаца.</span><span class="sxs-lookup"><span data-stu-id="23798-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="23798-133">В правом углу hello, выберите hello **параметры** значок, а затем щелкните **Показать заголовок**.</span><span class="sxs-lookup"><span data-stu-id="23798-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="23798-134">Теперь можно запустить инструкции Spark SQL для hello **кондиционирования** таблицы.</span><span class="sxs-lookup"><span data-stu-id="23798-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="23798-135">Вставьте приветствия при следующем запросе в новый абзац.</span><span class="sxs-lookup"><span data-stu-id="23798-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="23798-136">Hello запрос извлекает код здания hello и hello разницу между целевой hello и фактический температуру для каждой сборки в определенную дату.</span><span class="sxs-lookup"><span data-stu-id="23798-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="23798-137">Нажмите **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="23798-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="23798-138">Hello **% sql** оператор в начале hello указывает hello записной книжки toouse hello Livy Scala интерпретатора.</span><span class="sxs-lookup"><span data-stu-id="23798-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="23798-139">Hello следующем снимке экрана показаны выходные данные hello.</span><span class="sxs-lookup"><span data-stu-id="23798-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="23798-140">![Выполнить Spark SQL с помощью записной книжки hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "выполнить Spark SQL с помощью записной книжки hello")</span><span class="sxs-lookup"><span data-stu-id="23798-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="23798-141">Нажмите кнопку tooswitch (выделенный в прямоугольник) параметры отображения hello между различными представлениями для hello такие же выходные данные.</span><span class="sxs-lookup"><span data-stu-id="23798-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="23798-142">Нажмите кнопку **параметры** toochoose какие consitutes hello ключа и значения в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="23798-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="23798-143">Здравствуйте, снимки экрана выше используется **buildingID** как ключ hello и среднее значение hello **temp_diff** как значение hello.</span><span class="sxs-lookup"><span data-stu-id="23798-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="23798-144">Можно также запустить инструкции Spark SQL, использование переменных в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="23798-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="23798-145">Далее показан фрагмент кода Hello как toodefine переменной, **Temp**, в запросе hello с возможными значениями hello требуется tooquery с.</span><span class="sxs-lookup"><span data-stu-id="23798-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="23798-146">При первом запуске запроса hello, раскрывающийся список заполняется автоматически со значениями hello, указанное для переменной hello.</span><span class="sxs-lookup"><span data-stu-id="23798-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="23798-147">Вставьте этот фрагмент кода в новый абзац и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="23798-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="23798-148">Hello следующем снимке экрана показаны выходные данные hello.</span><span class="sxs-lookup"><span data-stu-id="23798-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="23798-149">![Выполнить Spark SQL с помощью записной книжки hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "выполнить Spark SQL с помощью записной книжки hello")</span><span class="sxs-lookup"><span data-stu-id="23798-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="23798-150">Для последующих запросов можно выбрать новое значение из раскрывающегося списка hello и снова запустите запрос hello.</span><span class="sxs-lookup"><span data-stu-id="23798-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="23798-151">Нажмите кнопку **параметры** toochoose какие consitutes hello ключа и значения в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="23798-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="23798-152">Здравствуйте, снимки экрана выше используется **buildingID** в качестве ключа hello hello среднее **temp_diff** как значение hello и **targettemp** как группа hello.</span><span class="sxs-lookup"><span data-stu-id="23798-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="23798-153">Перезапустите приложения hello tooexit интерпретатор Livy hello.</span><span class="sxs-lookup"><span data-stu-id="23798-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="23798-154">Откройте интерпретатор параметры, нажав кнопку входа имя пользователя в правом верхнем углу hello hello toodo и нажмите кнопку **интерпретатор**.</span><span class="sxs-lookup"><span data-stu-id="23798-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="23798-155">![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")</span><span class="sxs-lookup"><span data-stu-id="23798-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="23798-156">Прокрутите tooLivy интерпретатор параметры и нажмите кнопку **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="23798-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="23798-157">![Перезапустите hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "перезапустите hello Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="23798-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="23798-158">Как использовать внешние пакеты с ноутбука hello?</span><span class="sxs-lookup"><span data-stu-id="23798-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="23798-159">Можно настроить записной книжки Zeppelin hello в кластере Apache Spark на HDInsight (Linux) toouse внешних сообществом пакеты, которые не включены out-of box в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="23798-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="23798-160">Можно выполнить поиск hello [Maven репозитория](http://search.maven.org/) hello полный список доступных пакетов.</span><span class="sxs-lookup"><span data-stu-id="23798-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="23798-161">Его также можно получить из других источников.</span><span class="sxs-lookup"><span data-stu-id="23798-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="23798-162">Например, полный список предоставленных сообществом пакетов можно найти в разделе [Пакеты Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="23798-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="23798-163">В этой статье вы увидите как toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) пакет записной книжки Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="23798-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="23798-164">Откройте параметры интерпретатора.</span><span class="sxs-lookup"><span data-stu-id="23798-164">Open interpreter settings.</span></span> <span data-ttu-id="23798-165">Hello верхний правый угол, щелкните hello вход от имени пользователя и нажмите кнопку **интерпретатор**.</span><span class="sxs-lookup"><span data-stu-id="23798-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="23798-166">![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")</span><span class="sxs-lookup"><span data-stu-id="23798-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="23798-167">Прокрутите tooLivy интерпретатор параметры и нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="23798-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="23798-168">![Изменение параметров интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Изменение параметров интерпретатора")</span><span class="sxs-lookup"><span data-stu-id="23798-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="23798-169">Добавьте новый раздел, называется **livy.spark.jars.packages** и присвойте ему значение в формате hello `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="23798-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="23798-170">Таким образом, если вы хотите toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) пакета, необходимо задать значение hello hello ключа слишком`com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="23798-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="23798-171">![Изменение параметров интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Изменение параметров интерпретатора")</span><span class="sxs-lookup"><span data-stu-id="23798-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="23798-172">Нажмите кнопку **Сохранить** , а затем перезапустите hello Livy интерпретатора.</span><span class="sxs-lookup"><span data-stu-id="23798-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="23798-173">**Совет**: Если необходимо, чтобы toounderstand как tooarrive hello значения ключа hello на введенный выше, Вот каким образом.</span><span class="sxs-lookup"><span data-stu-id="23798-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="23798-174">а.</span><span class="sxs-lookup"><span data-stu-id="23798-174">a.</span></span> <span data-ttu-id="23798-175">Найдите пакет hello в hello Maven репозитория.</span><span class="sxs-lookup"><span data-stu-id="23798-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="23798-176">В этом руководстве мы используем [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="23798-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="23798-177">b.</span><span class="sxs-lookup"><span data-stu-id="23798-177">b.</span></span> <span data-ttu-id="23798-178">Из репозитория hello сбора значений hello **GroupId**, **ArtifactId**, и **версии**.</span><span class="sxs-lookup"><span data-stu-id="23798-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="23798-179">![Использование внешних пакетов с записными книжками Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Использование внешних пакетов с записными книжками Jupyter")</span><span class="sxs-lookup"><span data-stu-id="23798-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="23798-180">c.</span><span class="sxs-lookup"><span data-stu-id="23798-180">c.</span></span> <span data-ttu-id="23798-181">Объединение hello трех значений, разделенных точкой с запятой (**:**).</span><span class="sxs-lookup"><span data-stu-id="23798-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="23798-182">Где находятся hello записных книжек Zeppelin сохранить?</span><span class="sxs-lookup"><span data-stu-id="23798-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="23798-183">портативные компьютеры Zeppelin Hello сохраняются headnodes toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="23798-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="23798-184">Поэтому при удалении кластера hello записных книжек hello также будут удалены.</span><span class="sxs-lookup"><span data-stu-id="23798-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="23798-185">Если требуется toopreserve записных книжек для последующего использования в других кластерах, необходимо экспортировать их после завершения выполнения заданий hello.</span><span class="sxs-lookup"><span data-stu-id="23798-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="23798-186">tooexport записной книжке щелкните hello **Экспорт** значок, как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="23798-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="23798-187">![Загрузите записной книжки](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "записной книжки hello загрузки")</span><span class="sxs-lookup"><span data-stu-id="23798-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="23798-188">Это экономит записной книжки hello в формате JSON в место для загрузки.</span><span class="sxs-lookup"><span data-stu-id="23798-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="23798-189">Управление сеансом Livy</span><span class="sxs-lookup"><span data-stu-id="23798-189">Livy session management</span></span>
<span data-ttu-id="23798-190">При выполнении первого абзаца кода hello в блокноте Zeppelin Livy новый сеанс создается в кластере HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="23798-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="23798-191">Этот сеанс будет общим в записных книжках Zeppelin, которые вы затем создадите.</span><span class="sxs-lookup"><span data-stu-id="23798-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="23798-192">Если для некоторых hello причина Livy сеанс завершен (Перезагрузка кластера, т. д.), не будет возможности toorun заданий из записной книжки Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="23798-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="23798-193">В этом случае необходимо выполнить следующие действия перед началом выполнения заданий из записной книжке Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="23798-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="23798-194">Перезапустите hello интерпретатор Livy из записной книжки Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="23798-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="23798-195">Откройте интерпретатор параметры, нажав кнопку входа имя пользователя в правом верхнем углу hello hello toodo и нажмите кнопку **интерпретатор**.</span><span class="sxs-lookup"><span data-stu-id="23798-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="23798-196">![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")</span><span class="sxs-lookup"><span data-stu-id="23798-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="23798-197">Прокрутите tooLivy интерпретатор параметры и нажмите кнопку **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="23798-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="23798-198">![Перезапустите hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "перезапустите hello Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="23798-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="23798-199">Запустите ячейку кода из имеющейся записной книжки Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="23798-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="23798-200">Будет создан новый сеанс Livy hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23798-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="23798-201"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="23798-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="23798-202">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="23798-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="23798-203">Сценарии</span><span class="sxs-lookup"><span data-stu-id="23798-203">Scenarios</span></span>
* [<span data-ttu-id="23798-204">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="23798-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="23798-205">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="23798-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="23798-206">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="23798-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="23798-207">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="23798-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="23798-208">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="23798-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="23798-209">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="23798-209">Create and run applications</span></span>
* [<span data-ttu-id="23798-210">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="23798-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="23798-211">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="23798-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="23798-212">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="23798-212">Tools and extensions</span></span>
* [<span data-ttu-id="23798-213">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений</span><span class="sxs-lookup"><span data-stu-id="23798-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="23798-214">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="23798-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="23798-215">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="23798-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="23798-216">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="23798-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="23798-217">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="23798-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="23798-218">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="23798-218">Manage resources</span></span>
* [<span data-ttu-id="23798-219">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="23798-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="23798-220">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="23798-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







