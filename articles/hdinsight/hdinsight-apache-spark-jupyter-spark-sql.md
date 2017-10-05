---
title: "Создание кластера Apache Spark в Azure HDInsight | Документация Майкрософт"
description: "Краткое руководство HDInsight Spark по созданию кластера Apache Spark в HDInsight."
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
ms.openlocfilehash: ad4330a1fc7f8de154d9aaa8df3acc2ab59b9dc1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="5a01c-104">Создание кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a01c-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="5a01c-105">Из этой статьи вы узнаете, как создать кластер Apache Spark в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a01c-105">In this article, you learn how to create an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="5a01c-106">Сведения о Spark в HDInsight см. в [этой статье](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a01c-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="5a01c-107">![Схема быстрого руководства, описывающая шаги по созданию кластера Apache Spark в Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Краткое руководство по Spark с использованием Apache Spark в HDInsight. Описанные действия: создание кластера; выполнение интерактивного запроса Spark")</span><span class="sxs-lookup"><span data-stu-id="5a01c-107">![Quickstart diagram describing steps to create an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a01c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5a01c-108">Prerequisites</span></span>

* <span data-ttu-id="5a01c-109">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a01c-109">**An Azure subscription**.</span></span> <span data-ttu-id="5a01c-110">Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01c-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="5a01c-111">Ознакомьтесь со страницей [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="5a01c-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="5a01c-112">Создание кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="5a01c-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="5a01c-113">Следуя инструкциям из этого раздела, вы создадите кластер HDInsight Spark, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="5a01c-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="5a01c-114">Другие способы создания кластера см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5a01c-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="5a01c-115">Щелкните следующее изображение, чтобы открыть шаблон на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01c-115">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="5a01c-116">Введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="5a01c-116">Enter the following values:</span></span>

    <span data-ttu-id="5a01c-117">![Создание кластера HDInsight Spark с использованием шаблона Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Создание кластера Spark в HDInsight с использованием шаблона Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="5a01c-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="5a01c-118">**Подписка.** Выберите свою подписку Azure для этого кластера.</span><span class="sxs-lookup"><span data-stu-id="5a01c-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="5a01c-119">**Группа ресурсов.** Создайте группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="5a01c-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="5a01c-120">Она используется для управления ресурсами Azure для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="5a01c-120">Resource group is used to manage Azure resources for your projects.</span></span>
    * <span data-ttu-id="5a01c-121">**Расположение**. Выберите расположение группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a01c-121">**Location**: Select a location for the resource group.</span></span> <span data-ttu-id="5a01c-122">В шаблоне используется это расположение для создания кластера и его хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5a01c-122">The template uses this location for creating the cluster as well as for the default cluster storage.</span></span>
    * <span data-ttu-id="5a01c-123">**Имя кластера**. Введите имя создаваемого кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a01c-123">**ClusterName**: Enter a name for the HDInsight cluster that you want to create.</span></span>
    * <span data-ttu-id="5a01c-124">**Версия Spark**. Для версии, которую необходимо установить в кластере, выберите значение **2.0**.</span><span class="sxs-lookup"><span data-stu-id="5a01c-124">**Spark version**: Select **2.0** as the version that you want to install on the cluster.</span></span>
    * <span data-ttu-id="5a01c-125">**Имя для входа в кластер и пароль**: имя для входа по умолчанию — admin.</span><span class="sxs-lookup"><span data-stu-id="5a01c-125">**Cluster login name and password**: The default login name is admin.</span></span>
    * <span data-ttu-id="5a01c-126">**Имя пользователя SSH и пароль**.</span><span class="sxs-lookup"><span data-stu-id="5a01c-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="5a01c-127">Запишите эти значения.</span><span class="sxs-lookup"><span data-stu-id="5a01c-127">Write down these values.</span></span>  <span data-ttu-id="5a01c-128">Они потребуются позже в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="5a01c-128">You need them later in the tutorial.</span></span>

3. <span data-ttu-id="5a01c-129">Установите флажок **Я принимаю указанные выше условия** и **Закрепить на панели мониторинга**, а затем нажмите кнопку **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="5a01c-129">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="5a01c-130">Появится новый элемент под названием "Идет отправка развертывания для развертывания шаблона".</span><span class="sxs-lookup"><span data-stu-id="5a01c-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="5a01c-131">Процесс создания кластеров занимает около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="5a01c-131">It takes about 20 minutes to create the cluster.</span></span>

<span data-ttu-id="5a01c-132">Если при создании кластера HDInsight возникают проблемы, возможно, у вас нет необходимых разрешений.</span><span class="sxs-lookup"><span data-stu-id="5a01c-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span></span> <span data-ttu-id="5a01c-133">Дополнительные сведения см. в разделе [Требования к контролю доступа](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="5a01c-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="5a01c-134">В этой статье описано, как создать кластер Spark, использующий [большие двоичные объекты службы хранилища Azure в качестве хранилища кластера](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5a01c-134">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="5a01c-135">Кроме того, вы можете создать кластер Spark, использующий [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) в качестве хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5a01c-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as the default storage.</span></span> <span data-ttu-id="5a01c-136">Инструкции см. в инструкциях по [созданию кластера HDInsight с Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a01c-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="5a01c-137">Выполнение запросов Hive с помощью Spark SQL</span><span class="sxs-lookup"><span data-stu-id="5a01c-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="5a01c-138">При использовании записной книжки Jupyter, настроенной для кластера HDInsight Spark, вы получаете предустановку `sqlContext`, которую можно применять для выполнения запросов Hive с помощью Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="5a01c-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span></span> <span data-ttu-id="5a01c-139">Из этого раздела вы узнаете, как запустить записную книжку Jupyter и выполнить простой запрос Hive.</span><span class="sxs-lookup"><span data-stu-id="5a01c-139">In this section, you learn how to start a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="5a01c-140">Откройте [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5a01c-140">Open the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="5a01c-141">Если закрепили кластер на панели мониторинга, щелкните элемент кластера на панели мониторинга, чтобы открыть колонку кластера.</span><span class="sxs-lookup"><span data-stu-id="5a01c-141">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="5a01c-142">Если вы не закрепили кластер на панели мониторинга, в области слева щелкните **Кластеры HDInsight**, а затем выберите созданный кластер.</span><span class="sxs-lookup"><span data-stu-id="5a01c-142">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="5a01c-143">В разделе **Быстрые ссылки** щелкните **Панели мониторинга кластера**, а затем — **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="5a01c-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="5a01c-144">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="5a01c-144">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="5a01c-145">![Открытие записной книжки Jupyter для выполнения интерактивного запроса Spark SQL](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Открытие записной книжки Jupyter для выполнения интерактивного запроса Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="5a01c-145">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="5a01c-146">Также можно открыть записную книжку Jupyter для своего кластера, открыв следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="5a01c-146">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="5a01c-147">Замените **CLUSTERNAME** именем кластера:</span><span class="sxs-lookup"><span data-stu-id="5a01c-147">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="5a01c-148">Создайте записную книжку.</span><span class="sxs-lookup"><span data-stu-id="5a01c-148">Create a notebook.</span></span> <span data-ttu-id="5a01c-149">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="5a01c-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="5a01c-150">![Создание записной книжки Jupyter для выполнения интерактивного запроса Spark SQL](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Создание записной книжки Jupyter для выполнения интерактивного запроса Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="5a01c-150">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="5a01c-151">Будет создана и открыта записная книжка с именем Untitled (Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="5a01c-151">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="5a01c-152">Щелкните имя записной книжки вверху и по желанию введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="5a01c-152">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="5a01c-153">![Указание имени записной книжки Jupter, из которой будет выполняться интерактивный запрос Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Указание имени записной книжки Jupter, из которой будет выполняться интерактивный запрос Spark")</span><span class="sxs-lookup"><span data-stu-id="5a01c-153">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5.  <span data-ttu-id="5a01c-154">Вставьте указанный ниже код в пустую ячейку и нажмите сочетание клавиш **SHIFT + ВВОД**, чтобы выполнить код.</span><span class="sxs-lookup"><span data-stu-id="5a01c-154">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="5a01c-155">В примере кода ниже `%%sql` (sql magic) указывает записной книжке Jupyter использовать предустановку `sqlContext` для выполнения запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="5a01c-155">In the code below `%%sql` (called the sql magic) tells Jupyter notebook to use the preset `sqlContext` to run the Hive query.</span></span> <span data-ttu-id="5a01c-156">Запрос извлекает первые 10 строк из таблицы Hive (**hivesampletable**), которая по умолчанию доступна для всех кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a01c-156">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="5a01c-157">![Запрос Hive в HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="5a01c-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="5a01c-158">Дополнительные сведения о `%%sql` magic и предустановленных контекстах см. в статье [Ядра для записной книжки Jupyter в кластерах Spark в Azure HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="5a01c-158">For more information on the `%%sql` magic and the preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5a01c-159">При каждом выполнении запроса в Jupyter в заголовке окна веб-браузера будет отображаться состояние **(Занято)**, а также название записной книжки.</span><span class="sxs-lookup"><span data-stu-id="5a01c-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="5a01c-160">Кроме того, рядом с надписью **PySpark** в верхнем правом углу окна будет показан закрашенный кружок.</span><span class="sxs-lookup"><span data-stu-id="5a01c-160">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="5a01c-161">После завершения задания он изменится на кружок без заливки.</span><span class="sxs-lookup"><span data-stu-id="5a01c-161">After the job is completed, it changes to a hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="5a01c-162">Экран обновится, и отобразятся выходные данные запроса.</span><span class="sxs-lookup"><span data-stu-id="5a01c-162">The screen should refresh to show the query output.</span></span>

    <span data-ttu-id="5a01c-163">![Выходные данные запроса Hive в HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="5a01c-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="5a01c-164">Завершив работу с приложением, можно закрыть записную книжку, чтобы освободить ресурсы кластера.</span><span class="sxs-lookup"><span data-stu-id="5a01c-164">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="5a01c-165">Для этого в записной книжке в меню **Файл** выберите пункт **Close and Halt** (Закрыть и остановить).</span><span class="sxs-lookup"><span data-stu-id="5a01c-165">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="5a01c-166">Если вы планируете выполнить следующие действия позже, обязательно удалите кластер HDInsight, созданный во время работы с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="5a01c-166">If you plan to complete the next steps at a later time, make sure you delete the HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="5a01c-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a01c-167">Next step</span></span> 

<span data-ttu-id="5a01c-168">Из этой статьи вы узнали, как создать кластер HDInsight Spark и выполнить базовый запрос Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="5a01c-168">In this article you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="5a01c-169">Из следующей статьи вы узнаете, как с помощью кластера HDInsight Spark выполнять интерактивные запросы, используя пример данных.</span><span class="sxs-lookup"><span data-stu-id="5a01c-169">Advance to the next article to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="5a01c-170">Выполнение интерактивных запросов в кластере HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="5a01c-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



