---
title: "Использование записных книжек Zeppelin с кластером Apache Spark в Azure HDInsight | Документация Майкрософт"
description: "Пошаговые инструкции по использованию записных книжек Zeppelin с кластерами Apache Spark в Azure HDInsight."
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
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="8a47a-103">Использование записных книжек Zeppelin с кластером Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8a47a-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="8a47a-104">Кластеры Spark HDInsight включают в себя записные книжки Zeppelin, которые можно использовать для выполнения заданий Spark.</span><span class="sxs-lookup"><span data-stu-id="8a47a-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="8a47a-105">Из этой статьи вы узнаете, как использовать записную книжку Zeppelin в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8a47a-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8a47a-106">Записные книжки Zeppelin доступны только для Spark 1.6.3 в HDInsight 3.5 и для Spark 2.1.0 в HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="8a47a-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="8a47a-107">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="8a47a-107">**Prerequisites:**</span></span>

* <span data-ttu-id="8a47a-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="8a47a-108">An Azure subscription.</span></span> <span data-ttu-id="8a47a-109">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8a47a-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8a47a-110">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8a47a-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8a47a-111">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8a47a-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="8a47a-112">Запуск записной книжки Zeppelin</span><span class="sxs-lookup"><span data-stu-id="8a47a-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="8a47a-113">В колонке кластера Spark щелкните **Панель мониторинга кластера**, а затем выберите **Записная книжка Zeppelin**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="8a47a-114">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="8a47a-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8a47a-115">Также можно открыть Zeppelin Notebook для своего кластера, открыв следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="8a47a-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="8a47a-116">Замените **CLUSTERNAME** именем кластера:</span><span class="sxs-lookup"><span data-stu-id="8a47a-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="8a47a-117">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="8a47a-117">Create a new notebook.</span></span> <span data-ttu-id="8a47a-118">На панели заголовка щелкните элемент **Notebook** (Записная книжка), а затем — **Create New Note** (Создать заметку).</span><span class="sxs-lookup"><span data-stu-id="8a47a-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="8a47a-119">![Создание записной книжки Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Создание записной книжки Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="8a47a-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="8a47a-120">Введите имя для записной книжки и щелкните **Создать заметку**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="8a47a-121">Кроме того, убедитесь, что в заголовке записной книжки отображается состояние "Подключено".</span><span class="sxs-lookup"><span data-stu-id="8a47a-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="8a47a-122">Оно обозначается зеленой точкой в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="8a47a-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="8a47a-123">![Состояния записной книжки Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Состояния записной книжки Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="8a47a-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="8a47a-124">Загрузите демонстрационные данные во временную таблицу.</span><span class="sxs-lookup"><span data-stu-id="8a47a-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="8a47a-125">При создании кластера Spark в HDInsight файл с демонстрационными данными **hvac.csv** копируется в связанную учетную запись хранения по следующему пути: **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="8a47a-126">В пустой абзац, созданный по умолчанию в новой записной книжке, вставьте следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="8a47a-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
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
   
    <span data-ttu-id="8a47a-127">Нажмите клавиши **SHIFT+ВВОД** или кнопку **воспроизведения** для абзаца, чтобы выполнить фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="8a47a-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="8a47a-128">Состояние, которое отображается в правом верхнем углу абзаца, должно изменяться в следующей последовательности: READY (ГОТОВО), PENDING (ОЖИДАЕТ), RUNNING (ВЫПОЛНЯЕТСЯ) и FINISHED (ЗАВЕРШЕНО).</span><span class="sxs-lookup"><span data-stu-id="8a47a-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="8a47a-129">Выходные данные отображаются в нижней части того же абзаца.</span><span class="sxs-lookup"><span data-stu-id="8a47a-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="8a47a-130">Снимок экрана выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8a47a-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="8a47a-131">![Создание временной таблицы из необработанных данных](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Создание временной таблицы из необработанных данных")</span><span class="sxs-lookup"><span data-stu-id="8a47a-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="8a47a-132">Можно указать заголовок для каждого абзаца.</span><span class="sxs-lookup"><span data-stu-id="8a47a-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="8a47a-133">В правом верхнем углу экрана щелкните значок **Параметры**, а затем выберите элемент **Показать заголовок**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="8a47a-134">Теперь вы можете выполнить инструкции Spark SQL для таблицы **hvac** .</span><span class="sxs-lookup"><span data-stu-id="8a47a-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="8a47a-135">Вставьте следующий запрос в новый абзац.</span><span class="sxs-lookup"><span data-stu-id="8a47a-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="8a47a-136">Запрос извлекает идентификатор здания и разницу между целевой и фактической температурами для каждого здания в указанный день.</span><span class="sxs-lookup"><span data-stu-id="8a47a-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="8a47a-137">Нажмите **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="8a47a-138">Инструкция **%sql** в начале сообщает записной книжке, что необходимо использовать интерпретатор Livy Scala.</span><span class="sxs-lookup"><span data-stu-id="8a47a-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="8a47a-139">Выходные данные показаны на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="8a47a-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="8a47a-140">![Выполнение инструкции Spark SQL с помощью записной книжки](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Выполнение инструкции Spark SQL с помощью записной книжки")</span><span class="sxs-lookup"><span data-stu-id="8a47a-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="8a47a-141">Используйте параметры отображения (выделены красным прямоугольником) для переключения между различными представлениями одних и тех же выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8a47a-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="8a47a-142">Щелкните элемент **Параметры** , чтобы определить ключи и значения в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8a47a-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="8a47a-143">На снимке экрана выше параметр **buildingID** используется в качестве ключа, а среднее значение **temp_diff** — как значение.</span><span class="sxs-lookup"><span data-stu-id="8a47a-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="8a47a-144">Можно также запустить инструкции Spark SQL с помощью переменных в запросе.</span><span class="sxs-lookup"><span data-stu-id="8a47a-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="8a47a-145">В следующем фрагменте кода показано, как определить переменную ( **Temp**) в запросе с возможными значениями, с которыми необходимо выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="8a47a-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="8a47a-146">При первом выполнении запроса раскрывающийся список автоматически заполняется значениями, указанными для переменной.</span><span class="sxs-lookup"><span data-stu-id="8a47a-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="8a47a-147">Вставьте этот фрагмент кода в новый абзац и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="8a47a-148">Выходные данные показаны на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="8a47a-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="8a47a-149">![Выполнение инструкции Spark SQL с помощью записной книжки](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Выполнение инструкции Spark SQL с помощью записной книжки")</span><span class="sxs-lookup"><span data-stu-id="8a47a-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="8a47a-150">Для последующих запросов можно выбрать новое значение из раскрывающегося списка и повторно выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="8a47a-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="8a47a-151">Щелкните элемент **Параметры** , чтобы определить ключи и значения в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8a47a-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="8a47a-152">На снимке экрана выше параметр **buildingID** используется в качестве ключа, среднее значение **temp_diff** используется как значение, а **targettemp** — как группа.</span><span class="sxs-lookup"><span data-stu-id="8a47a-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="8a47a-153">Перезапустите интерпретатор Livy, чтобы выйти из приложения.</span><span class="sxs-lookup"><span data-stu-id="8a47a-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="8a47a-154">Для этого откройте параметры интерпретатора: щелкните имя вошедшего в систему пользователя в правом верхнем углу и нажмите кнопку **Interpreter** (Интерпретатор).</span><span class="sxs-lookup"><span data-stu-id="8a47a-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="8a47a-155">![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")</span><span class="sxs-lookup"><span data-stu-id="8a47a-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="8a47a-156">Прокрутите до параметров интерпретатора Livy и выберите **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="8a47a-157">![Перезапуск интерпретатора Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Перезапуск интерпретатора Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="8a47a-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="8a47a-158">Использование внешних пакетов с записной книжкой</span><span class="sxs-lookup"><span data-stu-id="8a47a-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="8a47a-159">Вы можете настроить записную книжку Zeppelin в кластере Apache Spark в HDInsight (Linux) для использования внешних, предоставленных сообществом пакетов, которые не включены в готовую версию кластера.</span><span class="sxs-lookup"><span data-stu-id="8a47a-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="8a47a-160">Полный список доступных пакетов можно найти в [репозитории Maven](http://search.maven.org/) .</span><span class="sxs-lookup"><span data-stu-id="8a47a-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="8a47a-161">Его также можно получить из других источников.</span><span class="sxs-lookup"><span data-stu-id="8a47a-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="8a47a-162">Например, полный список предоставленных сообществом пакетов можно найти в разделе [Пакеты Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="8a47a-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="8a47a-163">В этой статье показано, как использовать пакет [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) с записной книжкой Jupyter.</span><span class="sxs-lookup"><span data-stu-id="8a47a-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="8a47a-164">Откройте параметры интерпретатора.</span><span class="sxs-lookup"><span data-stu-id="8a47a-164">Open interpreter settings.</span></span> <span data-ttu-id="8a47a-165">В правом верхнем углу щелкните имя вошедшего в систему пользователя и выберите **Interpreter** (Интерпретатор).</span><span class="sxs-lookup"><span data-stu-id="8a47a-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="8a47a-166">![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")</span><span class="sxs-lookup"><span data-stu-id="8a47a-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="8a47a-167">Прокрутите до параметров интерпретатора Livy и выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="8a47a-168">![Изменение параметров интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Изменение параметров интерпретатора")</span><span class="sxs-lookup"><span data-stu-id="8a47a-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="8a47a-169">Добавьте новый ключ с именем **livy.spark.jars.packages** и присвойте ему значение в формате `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="8a47a-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="8a47a-170">Если вы хотите использовать пакет [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar), для ключа необходимо задать значение `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="8a47a-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="8a47a-171">![Изменение параметров интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Изменение параметров интерпретатора")</span><span class="sxs-lookup"><span data-stu-id="8a47a-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="8a47a-172">Нажмите кнопку **Сохранить**, а затем перезапустите интерпретатор Livy.</span><span class="sxs-lookup"><span data-stu-id="8a47a-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="8a47a-173">**Подсказка.** Вот как можно получить значение указанного выше ключа.</span><span class="sxs-lookup"><span data-stu-id="8a47a-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="8a47a-174">а.</span><span class="sxs-lookup"><span data-stu-id="8a47a-174">a.</span></span> <span data-ttu-id="8a47a-175">Найдите пакет в репозитории Maven.</span><span class="sxs-lookup"><span data-stu-id="8a47a-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="8a47a-176">В этом руководстве мы используем [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="8a47a-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="8a47a-177">b.</span><span class="sxs-lookup"><span data-stu-id="8a47a-177">b.</span></span> <span data-ttu-id="8a47a-178">В репозитории найдите значения для параметров **GroupId**, **ArtifactId** и **Version**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="8a47a-179">![Использование внешних пакетов с записными книжками Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Использование внешних пакетов с записными книжками Jupyter")</span><span class="sxs-lookup"><span data-stu-id="8a47a-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="8a47a-180">c.</span><span class="sxs-lookup"><span data-stu-id="8a47a-180">c.</span></span> <span data-ttu-id="8a47a-181">Объедините три значения, разделив их двоеточием (**:**).</span><span class="sxs-lookup"><span data-stu-id="8a47a-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="8a47a-182">Место сохранения записных книжек Zeppelin</span><span class="sxs-lookup"><span data-stu-id="8a47a-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="8a47a-183">Записные книжки Zeppelin сохраняются на головных узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="8a47a-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="8a47a-184">Поэтому при удалении кластера записные книжки также будут удалены.</span><span class="sxs-lookup"><span data-stu-id="8a47a-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="8a47a-185">Если вы хотите сохранить записные книжки для последующего использования в других кластерах, необходимо экспортировать их после выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="8a47a-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="8a47a-186">Чтобы экспортировать записную книжку, щелкните значок **Экспорт**, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="8a47a-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="8a47a-187">![Скачивание записной книжки](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Скачивание записной книжки")</span><span class="sxs-lookup"><span data-stu-id="8a47a-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="8a47a-188">Это действие сохраняет записную книжку в формате JSON в расположение для скачивания.</span><span class="sxs-lookup"><span data-stu-id="8a47a-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="8a47a-189">Управление сеансом Livy</span><span class="sxs-lookup"><span data-stu-id="8a47a-189">Livy session management</span></span>
<span data-ttu-id="8a47a-190">При выполнении первого абзаца кода в записной книжке Zeppelin в кластере HDInsight Spark создается новый сеанс Livy.</span><span class="sxs-lookup"><span data-stu-id="8a47a-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="8a47a-191">Этот сеанс будет общим в записных книжках Zeppelin, которые вы затем создадите.</span><span class="sxs-lookup"><span data-stu-id="8a47a-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="8a47a-192">Если по какой-то причине сеанс Livy будет завершен (перезагрузка кластера и т. д.), вы не сможете запускать задания из записной книжки Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="8a47a-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="8a47a-193">В этом случае перед началом выполнения заданий из записной книжки Zeppelin необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="8a47a-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="8a47a-194">Перезапустите интерпретатор Livy из записной книжки Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="8a47a-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="8a47a-195">Для этого откройте параметры интерпретатора: щелкните имя вошедшего в систему пользователя в правом верхнем углу и нажмите кнопку **Interpreter** (Интерпретатор).</span><span class="sxs-lookup"><span data-stu-id="8a47a-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="8a47a-196">![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")</span><span class="sxs-lookup"><span data-stu-id="8a47a-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="8a47a-197">Прокрутите до параметров интерпретатора Livy и выберите **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="8a47a-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="8a47a-198">![Перезапуск интерпретатора Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Перезапуск интерпретатора Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="8a47a-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="8a47a-199">Запустите ячейку кода из имеющейся записной книжки Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="8a47a-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="8a47a-200">При этом в кластере HDInsight будет создан сеанс Livy.</span><span class="sxs-lookup"><span data-stu-id="8a47a-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="8a47a-201"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="8a47a-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8a47a-202">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8a47a-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8a47a-203">Сценарии</span><span class="sxs-lookup"><span data-stu-id="8a47a-203">Scenarios</span></span>
* [<span data-ttu-id="8a47a-204">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="8a47a-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8a47a-205">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="8a47a-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8a47a-206">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="8a47a-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8a47a-207">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="8a47a-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="8a47a-208">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="8a47a-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8a47a-209">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="8a47a-209">Create and run applications</span></span>
* [<span data-ttu-id="8a47a-210">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="8a47a-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8a47a-211">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="8a47a-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8a47a-212">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="8a47a-212">Tools and extensions</span></span>
* [<span data-ttu-id="8a47a-213">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="8a47a-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8a47a-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely on HDInsight Spark Linux cluster (Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA)</span><span class="sxs-lookup"><span data-stu-id="8a47a-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8a47a-215">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="8a47a-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8a47a-216">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="8a47a-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="8a47a-217">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="8a47a-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8a47a-218">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="8a47a-218">Manage resources</span></span>
* [<span data-ttu-id="8a47a-219">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8a47a-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8a47a-220">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="8a47a-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







