---
title: "кластер aaaCreate Apache Spark в Azure HDInsight | Документы Microsoft"
description: "Примеры использования HDInsight Spark на как кластер toocreate Apache Spark в HDInsight."
keywords: "краткое руководство Spark,интерактивный запрос Spark,интерактивный запрос,Hdinsight Spark,Azure Spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="0cd95-104">Создание кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0cd95-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="0cd95-105">В этой статье вы узнаете, как кластер toocreate Apache Spark в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0cd95-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="0cd95-106">Сведения о Spark в HDInsight см. в [этой статье](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cd95-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="0cd95-107">![Краткое руководство схема, описывающая шаги toocreate кластера с Apache Spark на Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark начало работы с помощью Apache Spark в HDInsight. Описанные действия: создание кластера; выполнение интерактивного запроса Spark")</span><span class="sxs-lookup"><span data-stu-id="0cd95-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cd95-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0cd95-108">Prerequisites</span></span>

* <span data-ttu-id="0cd95-109">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="0cd95-109">**An Azure subscription**.</span></span> <span data-ttu-id="0cd95-110">Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd95-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="0cd95-111">Ознакомьтесь со страницей [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="0cd95-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="0cd95-112">Создание кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="0cd95-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="0cd95-113">Следуя инструкциям из этого раздела, вы создадите кластер HDInsight Spark, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="0cd95-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="0cd95-114">Другие способы создания кластера см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0cd95-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="0cd95-115">Щелкните hello следующий шаблон hello tooopen изображения в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd95-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="0cd95-116">Введите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="0cd95-116">Enter hello following values:</span></span>

    <span data-ttu-id="0cd95-117">![Создание кластера HDInsight Spark с использованием шаблона Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Создание кластера Spark в HDInsight с использованием шаблона Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="0cd95-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="0cd95-118">**Подписка.** Выберите свою подписку Azure для этого кластера.</span><span class="sxs-lookup"><span data-stu-id="0cd95-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="0cd95-119">**Группа ресурсов.** Создайте группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="0cd95-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="0cd95-120">Группы ресурсов — используется toomanage ресурсы Azure для проектов.</span><span class="sxs-lookup"><span data-stu-id="0cd95-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="0cd95-121">**Расположение**: выберите расположение для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="0cd95-122">шаблон Hello использует это расположение для создания кластера hello также и для хранения данных кластера по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="0cd95-123">**Имя_кластера**: Введите имя кластера HDInsight hello, которое следует toocreate.</span><span class="sxs-lookup"><span data-stu-id="0cd95-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="0cd95-124">**Версия Spark**: выберите **2.0** hello версии, которые должны tooinstall на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="0cd95-125">**Имя входа и пароль кластера**: hello имя входа по умолчанию — admin.</span><span class="sxs-lookup"><span data-stu-id="0cd95-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="0cd95-126">**Имя пользователя SSH и пароль**.</span><span class="sxs-lookup"><span data-stu-id="0cd95-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="0cd95-127">Запишите эти значения.</span><span class="sxs-lookup"><span data-stu-id="0cd95-127">Write down these values.</span></span>  <span data-ttu-id="0cd95-128">Они необходимы далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="0cd95-129">Выберите **я принимаю условия, указанных выше, toohello**выберите **toodashboard ПИН-код**и нажмите кнопку **покупки**.</span><span class="sxs-lookup"><span data-stu-id="0cd95-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="0cd95-130">Появится новый элемент под названием "Идет отправка развертывания для развертывания шаблона".</span><span class="sxs-lookup"><span data-stu-id="0cd95-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="0cd95-131">Он принимает кластера hello toocreate около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="0cd95-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="0cd95-132">Если возникли проблемы с создания кластеров HDInsight, возможно, у вас toodo hello нужные разрешения таким образом.</span><span class="sxs-lookup"><span data-stu-id="0cd95-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="0cd95-133">Дополнительные сведения см. в разделе [Требования к контролю доступа](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="0cd95-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="0cd95-134">В этой статье создается кластер Spark, использующий [BLOB-объектов хранилища Azure как hello кластера хранилища](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0cd95-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="0cd95-135">Можно также создать кластер Spark, которая использует [хранилища Озера данных Azure](hdinsight-hadoop-use-data-lake-store.md) хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="0cd95-136">Инструкции см. в инструкциях по [созданию кластера HDInsight с Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0cd95-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="0cd95-137">Выполнение запросов Hive с помощью Spark SQL</span><span class="sxs-lookup"><span data-stu-id="0cd95-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="0cd95-138">При использовании записной книжке Jupyter, настроенных для кластера HDInsight Spark, вы получаете стиль `sqlContext` , которые можно использовать запросы Hive toorun с помощью Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="0cd95-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="0cd95-139">В этом разделе вы узнаете, как toostart записной книжке Jupyter, а затем запустите базового запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="0cd95-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="0cd95-140">Откройте hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0cd95-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="0cd95-141">Если вы выбрали мониторинга toohello toopin hello кластера, щелкните плитку кластера hello из hello мониторинга toolaunch hello кластера колонки.</span><span class="sxs-lookup"><span data-stu-id="0cd95-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="0cd95-142">Если не закрепить мониторинга toohello кластера hello hello левой панели, нажмите кнопку **кластеров HDInsight**и нажмите кнопку hello кластера, вы создали.</span><span class="sxs-lookup"><span data-stu-id="0cd95-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="0cd95-143">В разделе **Быстрые ссылки** щелкните **Панели мониторинга кластера**, а затем — **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="0cd95-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="0cd95-144">При появлении запроса введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0cd95-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="0cd95-145">![Откройте Jupyter записной книжки toorun интерактивного Spark SQL-запроса](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "откройте Jupyter записной книжки toorun интерактивного Spark SQL-запроса")</span><span class="sxs-lookup"><span data-stu-id="0cd95-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="0cd95-146">Также может обращаться к записной книжки Jupyter hello для кластера, открыв hello следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="0cd95-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="0cd95-147">Замените **CLUSTERNAME** с hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="0cd95-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="0cd95-148">Создайте записную книжку.</span><span class="sxs-lookup"><span data-stu-id="0cd95-148">Create a notebook.</span></span> <span data-ttu-id="0cd95-149">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="0cd95-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="0cd95-150">![Создать интерактивный запрос Spark SQL Jupyter записной книжки toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "создания Jupyter записной книжки toorun интерактивного Spark SQL-запроса")</span><span class="sxs-lookup"><span data-stu-id="0cd95-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="0cd95-151">Создается и открывается с именем hello Untitled(Untitled.pynb) новый блокнот.</span><span class="sxs-lookup"><span data-stu-id="0cd95-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="0cd95-152">Щелкните имя записной книжки hello вверху hello и введите понятное имя, если требуется.</span><span class="sxs-lookup"><span data-stu-id="0cd95-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="0cd95-153">![Введите имя для hello Jupter записной книжки toorun интерактивных Spark запросов из](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "укажите имя для hello Jupter записной книжки toorun интерактивных Spark запросов из")</span><span class="sxs-lookup"><span data-stu-id="0cd95-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="0cd95-154">Ниже hello вставить код в пустой ячейке и нажмите клавишу **SHIFT + ВВОД** toorun кода hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="0cd95-155">В следующем примере кода hello `%%sql` (вызываемой hello sql magic) сообщает предустановку hello toouse записной книжки Jupyter `sqlContext` toorun запроса Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="0cd95-156">Hello запрос извлекает hello первые 10 строк из таблицы Hive (**hivesampletable**), доступное по умолчанию для всех кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0cd95-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="0cd95-157">![Запрос Hive в HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="0cd95-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="0cd95-158">Дополнительные сведения о hello `%%sql` magic и hello предустановленный набор контекстов см. в разделе [Jupyter ядер, доступных для кластера HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="0cd95-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="0cd95-159">Показывает каждый раз при выполнении запроса в Jupyter, заголовок окна обозревателя вашей веб **(Busy)** состояния вместе с hello записной книжки заголовка.</span><span class="sxs-lookup"><span data-stu-id="0cd95-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="0cd95-160">Появится следующий toohello сплошной кружок **PySpark** текст в верхнем правом углу hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="0cd95-161">По завершении задания hello изменяется tooa полый круг.</span><span class="sxs-lookup"><span data-stu-id="0cd95-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="0cd95-162">экран приветствия следует обновить результат запроса tooshow hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="0cd95-163">![Выходные данные запроса Hive в HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="0cd95-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="0cd95-164">Завершение работы ресурсов кластера hello toorelease записной книжки hello, после завершения работы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0cd95-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="0cd95-165">toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.</span><span class="sxs-lookup"><span data-stu-id="0cd95-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="0cd95-166">Если в дальнейшем планируется toocomplete hello дальнейшие действия, убедитесь, что удаление кластера HDInsight hello, созданный в этой статье.</span><span class="sxs-lookup"><span data-stu-id="0cd95-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="0cd95-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0cd95-167">Next step</span></span> 

<span data-ttu-id="0cd95-168">В этой статье вы узнали, как кластер HDInsight Spark toocreate и выполнения основных Spark SQL запроса.</span><span class="sxs-lookup"><span data-stu-id="0cd95-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="0cd95-169">Переместить toohello toolearn далее в статье как кластер HDInsight Spark toouse toorun интерактивной обработки запросов на образце данных.</span><span class="sxs-lookup"><span data-stu-id="0cd95-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="0cd95-170">Выполнение интерактивных запросов в кластере HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="0cd95-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



